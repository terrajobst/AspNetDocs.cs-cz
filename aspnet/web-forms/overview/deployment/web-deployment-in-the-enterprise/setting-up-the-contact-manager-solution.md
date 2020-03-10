---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
title: Nastavení řešení Contact Manager | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak stáhnout a nakonfigurovat řešení Správce kontaktů, aby se spouštělo místně na pracovní stanici pro vývojáře.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 200b973c-776b-4a9b-9e82-39fda6120a52
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: d9774ee01cb0515d7e733b24baa661f2648bd7c4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78629855"
---
# <a name="setting-up-the-contact-manager-solution"></a>Nastavení řešení správce kontaktů

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak stáhnout a nakonfigurovat řešení Správce kontaktů, aby se spouštělo místně na pracovní stanici pro vývojáře.

## <a name="system-requirements"></a>Systémové požadavky

Pokud chcete řešení Správce kontaktů spustit místně a provést další úkoly popsané v tomto kurzu, budete muset tento software nainstalovat na pracovní stanici pro vývojáře:

- Visual Studio 2010 Service Pack 1, Premium nebo Ultimate Edition
- Internetová informační služba (IIS) 7,5 Express
- SQL Server Express 2008 R2
- Nástroj pro nasazení webu služby IIS (Nasazení webu) 2,1 nebo novější
- ASP.NET 4.0
- ASP.NET MVC 3
- .NET Framework 4
- .NET Framework 3.5 SP1

S výjimkou sady Visual Studio 2010 můžete stáhnout a nainstalovat nejnovější verze všech těchto produktů a součástí pomocí [instalačního programu webové platformy](https://go.microsoft.com/?linkid=9805118).

## <a name="download-and-extract-the-solution"></a>Stažení a extrakce řešení

Ukázkovou aplikaci Správce kontaktů si můžete stáhnout [z Galerie kódu](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0)na webu MSDN.

## <a name="configure-and-run-the-solution"></a>Konfigurace a spuštění řešení

Pokud chcete nakonfigurovat a spustit řešení Contact Manageru na místním počítači, musíte provést tyto kroky vysoké úrovně:

1. Pokud ho ještě nemáte, vytvořte místní databázi ASP.NET aplikačních služeb s povolenými funkcemi členství a správy rolí.
2. Upravte připojovací řetězce v souborech *Web. config* tak, aby odkazovaly na místní instanci SQL Server Express.
3. Spusťte řešení ze sady Visual Studio 2010.

Zbývající část této části poskytuje další informace o tom, jak provést každou z těchto úloh.

**Vytvoření databáze služby Application Services**

1. Otevřete příkazový řádek sady Visual Studio 2010. Provedete to tak, že v nabídce **Start** přejdete na položku **všechny programy**, kliknete na možnost **Microsoft Visual Studio 2010**, kliknete na položku **Visual Studio Tools**a potom kliknete na **příkaz Visual Studio Command Prompt (2010)** .
2. Na příkazovém řádku zadejte tento příkaz a stiskněte klávesu ENTER:

    [!code-console[Main](setting-up-the-contact-manager-solution/samples/sample1.cmd)]

    1. Pro zadání připojovacího řetězce pro databázový server použijte přepínač **– C** .
    2. Pomocí přepínače **– a** určete funkce aplikačních služeb, které chcete přidat do databáze. V takovém případě **m** označuje, že chcete přidat podporu pro poskytovatele členství a **r** označuje, že chcete přidat podporu pro správce rolí.
    3. Pomocí přepínače **– d** zadejte název vaší databáze služby Application Services. Pokud tento přepínač vynecháte, nástroj vytvoří databázi s výchozím názvem **aspnetdb**.
3. Po úspěšném vytvoření databáze se na příkazovém řádku zobrazí potvrzení.

    ![](setting-up-the-contact-manager-solution/_static/image1.png)

> [!NOTE]
> Další informace o nástroji ASPNET\_regsql naleznete v tématu [ASP.NET SQL Server Registration Tool (aspnet\_regsql. exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx).

V dalším kroku se ujistěte, že připojovací řetězce v řešení Contact Manageru ukazují na vaši místní instanci SQL Server Express.

**Aktualizace připojovacích řetězců**

1. Otevřete řešení Contact Manager v aplikaci Visual Studio 2010.
2. V okně **Průzkumník řešení** rozbalte projekt **ContactManager. Mvc** a dvakrát klikněte na uzel **Web. config** .

    > [!NOTE]
    > Projekt ContactManager. Mvc obsahuje dva soubory *Web. config* . Je nutné upravit soubor na úrovni projektu.

    ![](setting-up-the-contact-manager-solution/_static/image2.png)
3. V elementu **connectionStrings** ověřte, zda je připojovací řetězec s názvem **ApplicationServices** Points do místní databáze služby ASP.NET Application Services.

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample2.xml)]
4. V okně **Průzkumník řešení** rozbalte projekt **ContactManager. Service** a dvakrát klikněte na uzel **Web. config** .

    ![](setting-up-the-contact-manager-solution/_static/image3.png)
5. V elementu **connectionStrings** v připojovacím řetězci s názvem **ContactManagerContext**ověřte, zda je vlastnost **zdroj dat** nastavena na místní instanci SQL Server Express. V připojovacím řetězci nemusíte nic dalšího měnit.

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample3.xml)]
6. Uložte všechny otevřené soubory.

Nyní byste měli být připraveni spustit řešení Contact Manager na místním počítači.

> [!NOTE]
> Pokud budete postupovat podle těchto kroků bez předchozího vytvoření databáze služby Application Services, ASP.NET vytvoří databázi při prvním pokusu o vytvoření uživatele. Ruční vytvoření databáze ale vám umožní mnohem větší kontrolu nad sadou funkcí služby Application Services, kterou chcete podporovat.

**Spuštění řešení Contact Manager**

1. V aplikaci Visual Studio 2010 stiskněte klávesu F5.
2. Spustí se aplikace Internet Explorer a požádá o adresu URL aplikace ASP.NET MVC 3 pro správce kontaktů. Ve výchozím nastavení aplikace zobrazí stránku **všechny kontakty** .

    ![](setting-up-the-contact-manager-solution/_static/image4.png)
3. Přidejte několik kontaktů a pak ověřte, že aplikace funguje podle očekávání.

    ![](setting-up-the-contact-manager-solution/_static/image5.png)
4. Přejděte na `http://localhost:50114/Account/Register` (Pokud aplikaci hostuje na jiném portu, upravte adresu URL). Přidejte uživatelské jméno, e-mailovou adresu a heslo a ověřte, že jste se mohli úspěšně zaregistrovat účet.

    ![](setting-up-the-contact-manager-solution/_static/image6.png)
5. Přejděte na `http://localhost:50114/Account/LogOn` (Pokud aplikaci hostuje na jiném portu, upravte adresu URL). Ověřte, že jste se mohli přihlásit pomocí účtu, který jste právě vytvořili.

    ![](setting-up-the-contact-manager-solution/_static/image7.png)
6. Ukončete aplikaci Internet Explorer a zastavte ladění.

## <a name="conclusion"></a>Závěr

V tomto okamžiku by mělo být řešení Správce kontaktů úplně nakonfigurované tak, aby se spouštělo na místním počítači. Řešení můžete použít jako referenci při práci prostřednictvím dalších témat v tomto kurzu.

V dalším tématu [Principy souboru projektu](understanding-the-project-file.md)je vysvětleno, jak můžete použít soubory projektu Custom Microsoft Build Engine (MSBuild) v rámci řešení Správce kontaktů k řízení procesu nasazení.

> [!div class="step-by-step"]
> [Předchozí](the-contact-manager-solution.md)
> [Další](understanding-the-project-file.md)
