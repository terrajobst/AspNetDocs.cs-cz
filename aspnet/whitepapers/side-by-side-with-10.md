---
uid: whitepapers/side-by-side-with-10
title: ASP.NET souběžného spouštění .NET Framework 1,0 a 1,1 | Microsoft Docs
author: rick-anderson
description: Tento dokument white paper popisuje, jak nainstalovat rozhraní .NET 1,0 i .NET 1,1 na váš počítač, což umožňuje spuštění webové aplikace v ASP.NET v obou verzích Fram...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: c123545099013af71569bce4707f2b3eb732c344
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78632970"
---
# <a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a>ASP.NET – souběžné spuštění .NET Framework 1.0 a 1.1

> Tento dokument white paper popisuje, jak nainstalovat rozhraní .NET 1,0 i .NET 1,1 na váš počítač, což umožňuje spuštění webové aplikace v ASP.NET v obou verzích rozhraní.
> 
> Platí pro ASP.NET 1,0 a ASP.NET 1,1.

V ASP.NET jsou aplikace označeny jako spuštěné souběžně, když jsou nainstalovány ve stejném počítači, ale používají různé verze .NET Framework. Následující téma popisuje, jak nakonfigurovat aplikace ASP.NET pro souběžné spouštění a poskytuje podrobné kroky pro:

- [Udržovat mapování webové aplikace na verzi .NET Framework 1,0 během instalace](#1)
- [Mapování webové aplikace na konkrétní verzi .NET Framework](#2)
- [Vyhledání verze .NET Framework, kterou používá web](#3)

Tradičně platí, že při aktualizaci součásti nebo aplikace v počítači je starší verze odebrána a nahrazena novější verzí. Pokud nová verze není kompatibilní s předchozí verzí, obvykle se tím přeruší jiné aplikace, které používají komponentu nebo aplikaci. .NET Framework poskytuje podporu pro souběžné spouštění, které umožňuje nainstalovat více verzí sestavení nebo aplikace do stejného počítače současně. Vzhledem k tomu, že je možné nainstalovat více verzí současně, můžou spravované aplikace vybrat, která verze se má použít, aniž by to ovlivnilo aplikace, které používají jinou verzi.

Ve výchozím nastavení se při instalaci .NET Framework verze 1,1 všechny existující aplikace ASP.NET automaticky překonfigurují tak, aby používaly nejnovější verzi .NET Framework. Pokud nechcete, aby se aplikace ASP.NET ve výchozím nastavení .NET Framework 1,1, kliknutím [sem](#1) se dozvíte, jak v průběhu instalace zabránit.

Pokud aktualizujete webový server na .NET Framework 1,1 a chcete, aby jedna nebo více webových aplikací běžela .NET Framework 1,0, je nutné aktualizovat mapu skriptů Internetová informační služba (IIS). Mapování skriptu je mechanismus pro mapování přípony souboru. aspx pro konkrétní webovou aplikaci na verzi .NET Framework. Kliknutím [sem](#2) se dozvíte, jak namapovat webovou aplikaci na konkrétní verzi .NET Framework.

K vyhledání, na které .NET Framework verze je spuštěná konkrétní webová aplikace, můžete použít nástroj pro registraci internetových informací nebo ASP.NET služby IIS (ASPNET\_regiis. exe). Kliknutím [sem](#3) zjistíte, jak najít verzi .NET Framework, kterou používá web.

Jedním z importovaných aspektů při migraci na .NET Framework 1,1 je, že každá verze .NET Framework používá vlastní soubor Machine. config. V důsledku toho, pokud webový správce provedl změny v souboru Machine. config, musí být tyto změny migrovány do souboru .NET Framework 1,1 Machine. config.

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a>Údržba mapování webové aplikace na .NET Framework 1,0 během instalace

Ve výchozím nastavení se všechny existující aplikace ASP.NET při instalaci automaticky překonfigurují, aby používaly novější verzi .NET Framework. Pomocí novější verze .NET Framework můžou aplikace plně využívat vylepšení a nové funkce, které jsou součástí nové verze. Zároveň správce webu, který může chtít podrobnou kontrolu nad tím, které aplikace se aktualizují, může zabránit automatickému přemapování všech stávajících aplikací ASP.NET během instalace .NET Framework.

Chcete-li zabránit automatickému přemapování celé aplikace ASP.NET na novější verzi .NET Framework, může správce webu použít možnost příkazového řádku/noaspupgrade s instalačním programem Dotnetfx. exe.

**Zamezení úplného přemapování aplikace ASP.NET na novější verzi**

1. Přejít na **začátek**.
2. Klikněte na **Spustit**.
3. Zadejte **příkaz cmd**.
4. Klikněte na tlačítko **OK**.  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. Na příkazovém řádku zadejte následující řádek, který spustí instalaci .NET Framework: **Dotnetfx. exe/c: "Install/noaspupgrade?** .  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. V instalačním programu Microsoft .NET Framework 1,1 klikněte na **Ano** . Tím se spustí proces instalace .NET Framework 1,1.  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a>Mapování webové aplikace na konkrétní verzi .NET Framework

Každá verze .NET Framework zahrnuje verzi registračního nástroje ASP.NET služby IIS (ASPNET\_regiis. exe). Tento nástroj umožňuje správcům určit, že webová aplikace bude spuštěna v konkrétní verzi .NET Framework. To se označuje jako mapování webové aplikace na verzi .NET Framework. Správci musí vybrat soubor ASPNET\_regiis. exe, který odpovídá verzi .NET Framework, která bude přidružena k webové aplikaci. Například správce, který chce určit, aby web používal .NET Framework 1,1, musí použít soubor ASPNET\_regiis. exe, který je součástí .NET Framework 1,1.

ASPNET\_regiis. exe pro verzi 1,0 se nachází v:

- C:\WINDOWS\Microsoft.NET\Framework\\**v 1.0.3705**\ASPNET\_regiis

ASPNET\_regiis. exe pro verzi 1, 1 je umístěn v:

- C:\WINDOWS\Microsoft.NET\Framework\\**v 1.1.4322**\ASPNET\_regiis

ASPNET\_regiis. exe poskytuje dvě možnosti mapování skriptu webové aplikace:

- **-s** Nastaví mapu skriptu v cestě a v jejích podřízených adresářích.
- **-sn** Nastaví mapu skriptu pouze v cestě.

Cesta definuje cestu metadat služby IIS webové aplikace, která je definovaná ve formě W3SVC/ROOT/{WebSiteNumber}/{Application\_Name}. Například pro webovou aplikaci s názvem portál umístěný na výchozím webu je cesta metabáze W3SVC/1/ROOT/Portal.

![](side-by-side-with-10/_static/image4.gif)

Poznámka: k získání cesty k metabázi můžete použít také nástroj nazvaný Editor metabáze. Tento nástroj si můžete stáhnout z webu podpora Microsoftu na [https://support.microsoft.com/default.aspx?scid=kb; en-US; 232068.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)

- Spuštěním ASPNET\_regiis. exe-s W3SVC/1/ROOT/Portal aktualizujte mapu skriptů služby IIS portálu a její podaplikaci.  
  
    ![](side-by-side-with-10/_static/image5.gif)

- Spuštěním ASPNET\_regiis. exe-SN W3SVC/1/ROOT/Portal aktualizujte mapu skriptů služby IIS portálu, aniž by to ovlivnilo aplikace v podadresářích portálu.  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a>Najít .NET Framework verzi, kterou webová aplikace používá

Správce může použít Service Manager internetu k nalezení verze .NET Framework, na které běží Web. Různé verze operačního systému spouštějí Internet Service Manager odlišně. Chcete-li spustit nástroj Service Manager, postupujte podle kroků uvedených níže.

**Spuštění Service Manager Internetu**

1. Přejít na **začátek**.
2. Klikněte na **Spustit**.
3. Zadejte **inetmgr**.  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. Z Service Manager Internetu vyberte webovou aplikaci, jejíž verze .NET Framework chcete znát.  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. Klikněte pravým tlačítkem na webovou aplikaci a pak klikněte na **Vlastnosti.**  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. V okně vlastností vyberte **konfigurace.**  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. V tabulce mapování aplikace vyberte **. aspx**a klikněte na **Upravit**.  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. V textovém poli **spustitelný soubor** vyhledejte v adresáři verze posouváním. Pokud je adresář verze v. 1.1.4322, aplikace je namapována na .NET Framework 1,1. Naopak, pokud je adresář verze v 1.0.3705, aplikace je namapována na .NET Framework 1,0.  
  
    ![](side-by-side-with-10/_static/image12.gif)
