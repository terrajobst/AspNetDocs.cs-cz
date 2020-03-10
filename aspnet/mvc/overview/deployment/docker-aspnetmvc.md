---
uid: mvc/overview/deployment/docker
title: Migrace aplikací ASP.NET MVC do kontejnerů s Windows
description: Naučte se, jak převzít existující aplikaci ASP.NET MVC a spustit ji v kontejneru Docker ve Windows
keywords: Kontejnery Windows, Docker, ASP. NET MVC
author: BillWagner
ms.author: wiwagn
ms.date: 12/14/2018
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
ms.openlocfilehash: ef184f4256c20e2a66de8fd2d4f8e67f07d9a086
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583627"
---
# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a>Migrace aplikací ASP.NET MVC do kontejnerů s Windows

Spuštění existující aplikace založené na .NET Framework v kontejneru Windows nevyžaduje žádné změny aplikace. Pokud chcete aplikaci spustit v kontejneru Windows, vytvořte image Docker obsahující vaši aplikaci a spusťte kontejner. Toto téma vysvětluje, jak přijmout existující [aplikaci ASP.NET MVC](http://www.asp.net/mvc) a jak ji nasadit do kontejneru Windows.

Začnete s existující aplikací ASP.NET MVC a pak sestavíte publikované assety pomocí sady Visual Studio. Pomocí Docker vytvoříte image, která obsahuje a spustí vaši aplikaci. Přejdete na web běžící v kontejneru Windows a ověříte, že aplikace funguje.

Tento článek předpokládá základní znalost Dockeru. Informace o Dockeru najdete v článku [Docker Overview](https://docs.docker.com/engine/understanding-docker/) (Přehled Dockeru).

Aplikace, kterou spouštíte v kontejneru, je jednoduchý web, který je náhodně zodpovězený na otázky. Tato aplikace je základní aplikace MVC bez ověřování nebo úložiště databáze. Díky tomu se můžete zaměřit na přesun webové vrstvy do kontejneru. V budoucích tématech se dozvíte, jak přesunout a spravovat trvalé úložiště v kontejnerových aplikacích.

Přesunutí aplikace zahrnuje tyto kroky:

1. [Vytvoření úlohy publikování pro sestavení assetů pro obrázek.](#publish-script)
1. [Sestavení image Docker, která spustí vaši aplikaci.](#build-the-image)
1. [Spouští se kontejner Docker, který spouští vaši image.](#start-a-container)
1. [Ověřuje se aplikace v prohlížeči.](#verify-in-the-browser)

[Dokončená aplikace](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator) je na GitHubu.

## <a name="prerequisites"></a>Předpoklady

Vývojový počítač musí mít následující software:

- [Windows 10 – aktualizace pro výročí](https://www.microsoft.com/software-download/windows10/) (nebo vyšší) nebo [Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (nebo vyšší)
- [Docker for Windows](https://docs.docker.com/docker-for-windows/) – stabilní verze 1.13.0 nebo 1,12 beta 26 (nebo novější verze)
- [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

> [!IMPORTANT]
> Pokud používáte Windows Server 2016, postupujte podle pokynů pro [nasazení hostitele kontejnerů – Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment).

Po nainstalování a spuštění Dockeru klikněte pravým tlačítkem myši na ikonu na hlavním panelu a vyberte **Switch to Windows containers** (Přepnout na kontejnery Windows). To se vyžaduje pro spuštění imagí Dockeru založených na Windows. Spuštění tohoto příkazu trvá několik sekund:

![Kontejner Windows][windows-container]

## <a name="publish-script"></a>Publikovat skript

Shromážděte na jednom místě všechny prostředky, které potřebujete nahrát do image Dockeru. Pomocí příkazu **publikovat** v aplikaci Visual Studio můžete pro svou aplikaci vytvořit profil publikování. Tento profil vloží všechny prostředky do jednoho adresářového stromu, které zkopírujete do cílové image později v tomto kurzu.

**Kroky publikování**

1. Klikněte pravým tlačítkem na webový projekt v aplikaci Visual Studio a vyberte **publikovat**.
1. Klikněte na **tlačítko vlastní profil**a pak jako metodu vyberte **systém souborů** .
1. Vyberte adresář. Podle konvence stažený vzorek používá `bin\Release\PublishOutput`.

![Publikovat připojení][publish-connection]

Otevřete část **Možnosti publikování souboru** na kartě **Nastavení** . Vyberte **předkompilovat během publikování**. Tato optimalizace znamená, že budete kompilovat zobrazení v kontejneru Docker, kopírujete Předkompilovaná zobrazení.

![Nastavení publikování][publish-settings]

Klikněte na **publikovat**a Visual Studio zkopíruje všechny potřebné prostředky do cílové složky.

## <a name="build-the-image"></a>Sestavení image

Vytvořte nový soubor s názvem *souboru Dockerfile* a definujte image Docker. *Souboru Dockerfile* obsahuje pokyny pro sestavení finální image a zahrnuje všechny základní názvy imagí, požadované komponenty, aplikaci, kterou chcete spustit, a další konfigurační image. *Souboru Dockerfile* je vstup k příkazu `docker build`, který vytváří bitovou kopii.

Pro toto cvičení sestavíte image na základě `microsoft/aspnet` image, která se nachází v [Docker Hub](https://hub.docker.com/r/microsoft/aspnet/).
Základní bitová kopie, `microsoft/aspnet`, je image Windows serveru. Obsahuje Windows Server Core, IIS a ASP.NET 4.7.2. Když spustíte tuto image ve vašem kontejneru, automaticky se spustí IIS a nainstalují weby.

Souboru Dockerfile, který vytváří obrázek, vypadá takto:

```console
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# The final instruction copies the site you published earlier into the container.
COPY ./bin/Release/PublishOutput/ /inetpub/wwwroot
```

V tomto souboru Dockerfile není žádný příkaz `ENTRYPOINT`. Žádný nepotřebujete. Při spuštění Windows serveru se službou IIS je proces IIS vstupním parametrem, který je nakonfigurovaný tak, aby se spouštěl v základní imagi ASPNET.

Spuštěním příkazu Docker Build vytvořte image, která spustí vaši aplikaci ASP.NET. Provedete to tak, že otevřete okno prostředí PowerShell v adresáři projektu a v adresáři řešení zadáte následující příkaz:

```console
docker build -t mvcrandomanswers .
```

Tento příkaz sestaví novou image pomocí instrukcí ve vašem souboru Dockerfile, pojmenovávání (-t označení) obrázku jako mvcrandomanswers. To může zahrnovat přijetí základní image z [Docker Hub](http://hub.docker.com)a přidání vaší aplikace do této image.

Po dokončení tohoto příkazu můžete spustit příkaz `docker images`, abyste viděli informace na nové imagi:

```console
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       10.1 GB
```

ID IMAGE se na vašem počítači liší. Teď aplikaci spusťte.

## <a name="start-a-container"></a>Spuštění kontejneru

Spusťte kontejner spuštěním následujícího příkazu `docker run`:

```console
docker run -d --name randomanswers mvcrandomanswers
```

Argument `-d` instruuje Docker, aby spustil obrázek v odpojeném režimu. To znamená, že se image Docker spustí odpojený od aktuálního prostředí.

V mnoha ukázkách Docker se může zobrazit – p pro mapování kontejneru a hostitelských portů. Výchozí image ASPNET již nakonfigurovala kontejner pro naslouchání na portu 80 a zpřístupňuje ho.

`--name randomanswers` poskytuje název ke spuštěnému kontejneru. Ve většině příkazů můžete použít tento název místo ID kontejneru.

`mvcrandomanswers` je název obrázku, který se má spustit.

## <a name="verify-in-the-browser"></a>Ověření v prohlížeči

Po spuštění kontejneru se připojte ke spuštěnému kontejneru pomocí `http://localhost` v zobrazeném příkladu. Zadejte tuto adresu URL do prohlížeče a měli byste vidět běžící Web.

> [!NOTE]
> Některé software VPN nebo proxy serveru vám může bránit v přechodu na váš web.
> Můžete ho dočasně zakázat, abyste se ujistili, že váš kontejner funguje.

Ukázkový adresář na GitHubu obsahuje [skript PowerShellu](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1) , který tyto příkazy spouští za vás. Otevřete okno PowerShellu, změňte adresář na adresář řešení a zadejte:

```console
./run.ps1
```

Výše uvedený příkaz sestaví image, zobrazí seznam imagí na vašem počítači a spustí kontejner.

Pokud chcete kontejner zastavit, vydejte `docker stop` příkaz:

```console
docker stop randomanswers
```

Pokud chcete kontejner odebrat, vydejte příkaz `docker rm`:

```console
docker rm randomanswers
```

[windows-container]: media/aspnetmvc/SwitchContainer.png "Přepnout do kontejneru Windows"
[publish-connection]: media/aspnetmvc/PublishConnection.png "Publikovat do systému souborů"
[publish-settings]: media/aspnetmvc/PublishSettings.png "Nastavení publikování"
