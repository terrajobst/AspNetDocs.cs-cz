---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: Představení rozhraní ASP.NET Web Pages – publikování webu pomocí služby WebMatrix | Dokumentace Microsoftu
author: Rick-Anderson
description: Tento kurz je finální pokračování v této sérii kurzů, který představuje rozhraní ASP.NET Web Pages a Microsoft WebMatrix. Popisuje, jak publikovat svůj web t...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: 49a841dbda183bf1d59153b83f694c9f517e0b94
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78633614"
---
# <a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a>Úvod do webových stránek ASP.NET – publikování webu pomocí Webmatrixu

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento kurz je finální pokračování v této sérii kurzů, který představuje rozhraní ASP.NET Web Pages a Microsoft WebMatrix. Popisuje, jak publikovat svůj web na Internetu, ostatní mohli pracovat s ním. Předpokládá, že jste dokončili sérii [vytvořením konzistentního vzhledu webů webových stránek ASP.NET](https://go.microsoft.com/fwlink/?LinkId=251585).
> 
> Dozvíte se víc o publikování vašeho webu pomocí:
> 
> - Microsoft Azure
> - Webové hostingové společnosti

## <a name="about-publishing-your-site"></a>Publikování webu

Až dosud jste provedli všechny práce na místním počítači, včetně testování stránek. Chcete-li spustit vaše stránky<em>. cshtml</em> , použili jste webový server, který je součástí WebMatrix, konkrétně IIS Express. Můžete ale samozřejmě nikdo můžete zobrazit na webu, který jste vytvořili s výjimkou je. Informovat tak ostatní uživatele práci s webem, je nutné ji publikovat na Internetu.

Pokud už nemáte přístup k veřejnému webovému serveru, publikování znamená, že musíte mít účet s *cloudovou platformou* nebo *poskytovatelem hostingu*. Cloudové platformy, jako je například Microsoft Azure poskytuje infrastrukturu na vyžádání pro vaše aplikace. Poskytovatel hostingu je společnost, která vlastní servery veřejně přístupný webový a, který bude poskytovat do nájmu můžete místo pro váš web. Spuštění z za pár dolarů za měsíc (nebo dokonce bezplatná) plány hostování pro malé weby na stovky dolarů za měsíc pro komerční websites velkého rozsahu.

> [!NOTE]
> Můžete mít přístup public webový server prostřednictvím poskytovatele internetových služeb (ISP), který použijete k získání doma internetové služby. Váš poskytovatel hostingu však musí podporovat rozhraní ASP.NET Web Pages. Není mnoho poskytovatelů internetových služeb, ale je vždy vhodné kontrolu.

V tomto kurzu dáme vám přehled o tom, jak publikovat. Není praktické poskytnout přesné informace pro všechno, protože proces se trochu liší pro každý poskytovatele hostingu. Ale získáte představu o tom, jak tento proces funguje.

Tento kurz obsahuje čtyři části:

1. [Nastavení výchozí stránky](#defaultpage)
2. Publikování (zvolte jednu z následujících)  
 a. [Publikování webu na Microsoft Azure](#azure)  
 b. [Publikování webu na společnosti hostující na webu](#host)
3. [Aktualizace živého webu: Opětovné publikování](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a>Nastavení výchozí stránky

Když uživatel přejde na základní adresu pro web, se uživateli zobrazí výchozí stránka pro váš web. Pokud je například *Default. htm* nastaven jako výchozí stránka pro web na `www.contoso.com`a pak přejdete na `www.contoso.com` je stejná jako navigace na `www.contoso.com/Default.htm`.

V současné době váš web používá jako výchozí stránku **výchozí. cshtml** . Tato stránka je v pořádku pro výchozí stránku, ale v tomto kurzu jste nepřidali žádný obsah na této stránce tak, že by se zobrazily prázdnou stránku. Otevřete stránku Default.cshtml a nahraďte obsah následujícím kódem.

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

Váš web je nyní připraveno k publikaci. Nejprve se zobrazí postup nasazení webu do Azure a jak ji nasadit do webové firma poskytující hosting. Funguje kterákoli z nich možností pro webové stránky a je potřeba jenom použijte jednu z možností nasazení.

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a>Publikování webu ve službě Microsoft Azure

V tomto kurzu se nejprve ukazují, jak nasadit svůj web do Microsoft Azure. Když se přihlásíte pomocí účtu Microsoft, můžete vytvořit až 10 bezplatných webů v Azure. Tyto bezplatné lokality poskytují pohodlný způsob, jak testovat svoje weby. Vždy můžete odstranit tento příklad web později, abyste se vyhnuli použití všech bezplatných webů. Můžete si během několika minut vytvořit bezplatný zkušební účet. Podrobnosti najdete v tématu [Bezplatná zkušební verze Azure](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).

Na pásu karet WebMatrix klikněte na tlačítko **publikovat** .

!["Publikovat" tlačítko na pásu karet nástroje WebMatrix](publishing/_static/image1.png)

Zobrazí se dialogové okno **publikování webu** . Pokud jste se k vašemu účet Microsoft přihlásili, bude dialogové okno obsahovat odkaz **Začínáme s Azure** . Kliknutím na tento odkaz.

![Publikování webu](publishing/_static/image2.png)

Pokud nejste přihlášeni k účtu Microsoft, budete mít znovu příležitost k přihlášení. Musíte se přihlásit k účtu Microsoft k publikování webu v Azure.

![Přihlásit se](publishing/_static/image3.png)

Po přihlášení ke svému účtu Microsoft, dialogové okno obsahuje odkazy na vytvoření nového webu v Azure nebo se připojit k jednomu z existující weby v Azure.

![Vytvoří nový web.](publishing/_static/image4.png)

Vyberte **vytvořit novou lokalitu**.

Pokud jste najmenovali svůj projekt jako **WebPagesMovies**, výchozí název vašeho webu bude **webpagesmovies.azurewebsites.NET**. Tento výchozí název je s největší pravděpodobností není k dispozici, je určeno červený vykřičník.

![název výchozí webové stránky](publishing/_static/image5.png)

Změnit název serveru, který je k dispozici a vyberte umístění, které je blízko vaší polohy.

![název změněné lokality](publishing/_static/image6.png)

Klikněte na tlačítko **OK**.

Služba WebMatrix performss testu k určení, zda je server kompatibilní s vaší lokality.

![testování kompatibility](publishing/_static/image7.png)

Vyberte **Pokračovat**.

Výsledky testování kompatibility se zobrazí.

![výsledek kompatibility](publishing/_static/image8.png)

Vyberte **Pokračovat**.

Služba WebMatrix zobrazí soubory a databáze, které bude publikována do lokality. Protože při prvním publikování webu, jsou uvedeny všechny soubory. Zrušte zaškrtnutí políčka soubor, který není připravená k publikování. V následující publikace se zobrazí pouze soubory, které se změnily. Viz [aktualizace živého webu: Opětovné publikování](#update).

![Náhled publikování](publishing/_static/image9.png)

Vyberte **Pokračovat**.

Po nasazení webu do Azure, zobrazí se zpráva, která označuje, že dokončení nasazení.

![publikování dokončeno](publishing/_static/image10.png)

Web a databáze byly publikovány do Azure a jsou teď dostupné pro veřejnost. Klikněte na odkaz ve zprávě označující publikování dokončí a zobrazí se vám teď váš web. Vy nebo každý, kdo má přístup k Internetu, můžete přidat nebo upravit záznamy v databázi.

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a>Publikování webu na webu firma poskytující Hosting

Pokud se rozhodnete nebude publikován do Azure, můžete místo toho publikování webu pro webové hostování společnosti.

Klikněte na odkaz **Najít hostování webu** .

![Tlačítka 'Najít hostování webů' v dialogovém okně Nastavení publikování](publishing/_static/image12.png)

Přejděte na stránku na webu společnosti Microsoft, který obsahuje seznam poskytovatelé hostitelských služeb, které podporují ASP.NET.

![Stránka na webu Microsoftu, který obsahuje seznam poskytovatelů hostingu](publishing/_static/image13.png)

Samozřejmě může být obtížné zjistit, teď právě jaké funkce hostování může vyžadovat v dlouhodobém horizontu. Tady je několik věcí, které byste měli zvážit:

- Pro účely WebPagesMovies lokality nemusíte mít samostatné doplněk pro SQL Server, který často velmi náklady. Ve vaší lokalitě používáte SQL Server Compact Edition, který je samostatný. Přístup k SQL serveru však může být zapotřebí pro některé budoucí webu práce, kterou děláte. Pokud se domníváte, že máte, ujistěte se, že funkce SQL serveru můžete později přidat.
- Zkontrolujte, zda poskytovatel hostingu podporuje protokol publikování nasazení webu. Můžete publikovat pomocí protokolu FTP, ale je pohodlnější službu Web Deploy používat.

Některé servery nabízejí bezplatné zkušební období. Bezplatnou zkušební verzi je dobrým způsobem, jak opakujte publikování a hostování při budete stále experimentování s nástrojem WebMatrix a webové stránky ASP.NET.

Vyberte si ten, který vám vyhovuje. Pro účely tohoto kurzu jsme vybrali DiscountASP.NET, protože když jsme vytvářeli kurzu, měli této společnosti v rámci propagační akce, která lidem hostovat lokalitu zdarma po dobu několika měsíců.

> [!NOTE]
> Námi zvolený prostřednictvím poskytovatele hostitelských služeb pro účely tohoto kurzu, neměly by být vykládány jako o potvrzení této společnosti přes jakýkoli jiný. Ale jsme měli vybrat jednu pro obrázek a DiscountASP.NET je jednou z mnoha společnosti, které podporuje rozhraní ASP.NET Web Pages a protokolu Webdeploy publikovat.

Obvykle poté, co jste se zaregistrovali u poskytovatele hostingu, společnost vám pošle e-mailu, který obsahuje uživatelské jméno a heslo, adresu URL webového serveru a tak dále. Pokud hostovací společnost podporuje protokolu Webdeploy, se může odeslat je soubor, který obsahuje nastavení publikování, nebo můžete stáhnout z Internetu. Soubor nastavení publikování zjednodušuje proces za vás.

Po přihlášení a připraven k publikování klikněte na pásu karet WebMatrix na tlačítko **publikovat** . Zobrazí se dialogové okno **publikování nastavení** .

Pokud poskytovatel hostingu poslal soubor nastavení publikování, klikněte na odkaz **importovat nastavení publikování** a importujte soubor. Pokud nemáte soubor nastavení publikování, vyplňte pole pomocí hodnot, které hostingové společnosti vám poslali e-mailem. Toto dialogové okno **Nastavení publikování** může vypadat, jako když jste hotovi:

![Nastavení publikování vyplněna v dialogovém okně "nastavení publikování.](publishing/_static/image14.png)

Klikněte na **ověřit připojení**. Pokud je vše v pořádku, zobrazí se dialogové okno se zprávou **úspěšně připojeno**, což znamená, že může komunikovat se serverem poskytovatele hostingu.

![Úspěch zprávu při publikování se používají správná nastavení](publishing/_static/image15.png)

Pokud je nějaký problém, služba WebMatrix provede nejlépe, říct, že problém je:

![Chybová zpráva, pokud je nějaký problém s nastavením publikování](publishing/_static/image16.png)

Uložte nastavení kliknutím na **Uložit** . Služba WebMatrix nabízí proveďte test, abyste měli jistotu, že můžete správně komunikují s lokalitou hostingu:

![Zpráva k provedení testu se proces publikování nabídky](publishing/_static/image17.png)

Klikněte na **Ano**. Služba WebMatrix některé ukázkové soubory nahraje do poskytovatele hostingu. Po dokončení testování kompatibility se službou WebMatrix hlásí výsledky:

![Výsledky testu pro publikování](publishing/_static/image18.png)

Pokud jste připraveni přejít, pokračujte a klikněte na **pokračovat** a spusťte proces publikování pro reálný. Služba WebMatrix přijde na to, co soubory jsou ve vaší lokalitě a jsou už na hostitelském serveru (ihned, žádné) a nabízí přehled procesu publikování:

![Ve verzi Preview, jaké soubory, které odešlete proces publikování](publishing/_static/image19.png)

Seznam souborů, které mají být publikovány, obsahuje webové stránky, které jste vytvořili jako *filmy. cshtml*. Seznam obsahuje také soubory pro pomocné funkce, které jste nainstalovali, soubory, které chcete spustit SQL Server Compact Edition pro vaši databázi a tak dále. V důsledku toho počáteční procesu publikování může být významné.

Klikněte na **Pokračovat**. Služba WebMatrix zkopíruje soubory na server poskytovatele hostingu. Po dokončení, výsledky jsou uvedeny ve stavovém řádku:

![Stav panelu zprávy, když proces publikování byl úspěšně dokončen.](publishing/_static/image20.png)

Pokud chcete zobrazit živého webu, klikněte na odkaz ve stavovém řádku. Přidejte do adresy URL *filmy* a zobrazí se soubor *filmů. cshtml* , který jste vytvořili:

![Živý web stránkou filmy](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a>Aktualizuje se živého webu: opětovné publikování

Po publikování webu (do Azure nebo do společnosti hostující na webu) se v počítači nacházejí dvě kopie &mdash; verze a verze poskytovatele služeb. Pravděpodobně budete chtít pokračovat ve vývoji webu (Pokud nic jiného, další sérii kurzů v rámci). Když použijete, budete muset znovu publikovat svůj web, aby bylo možné kopírovat změny z vašeho počítače k poskytovateli služby. Proces publikování ve Webmatrixu můžete zjistit, co byly změněné soubory na váš web a publikovat pouze tyto soubory.

Pokud chcete zjistit, jak funguje opětovné publikování, otevřete web *filmy. cshtml* , udělejte nějakou malou změnu a pak soubor uložte. Například změňte název na `Movies - Updated`.

Klikněte na tlačítko **publikovat** na pásu karet. Služba WebMatrix Určuje, co se změnilo a zobrazí náhled souborů, které budete publikovat.

![Dialogové okno "Publikovat" zobrazující změněné soubory připravené k opětovné publikování](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> Ve výchozím nastavení publikuje WebMatrix vaši databázi (soubor *. sdf* ) pouze při prvním publikování webu. Jakmile se vaše lokalita je publikována a uživatelé interagují s webem, databázi na živém webu má obvykle reálná data lokality. Musíte být velmi opatrní, nemusíte přepsat živou databázi souborem *. sdf* , který je ve vašem počítači, což obvykle obsahuje pouze testovací data. To je důvod, proč se zobrazí upozornění, že při **publikování dojde k přepsání všech vzdálených databází**a proč je ve výchozím nastavení zaškrtnuté políčko pro *WebPagesMovies. sdf* .

Klikněte na **Pokračovat**. Služba WebMatrix publikuje změněných souborů a zobrazí zprávu o úspěšném dokončení stejně, jako kdyby poprvé, kterou jste publikovali.

Přejít do živého webu (můžete kliknout na odkaz v zpráva o úspěchu Pokud je stále zobrazena) a ověřte, že vaše změny se publikoval.

> [!TIP] 
> 
> **Vzdálená úprava souborů**
> 
> Jako alternativu k změně webu a pak znovu publikovat můžete upravit vzdálené soubory přímo ve službě WebMatrix. V tomto scénáři otevřete soubor, který je u poskytovatelů služeb a služba WebMatrix stáhne kopii jej můžete upravit. Pokaždé, když se soubor uložíte, služba WebMatrix odešle změny do lokality.
> 
> Vzdálené úpravy je snadný způsob, jak provádět změny živého webu. Změny provedené tímto způsobem se však nejsou synchronizované s souborů ve vaší místní lokalitě. K synchronizaci místních souborů s vzdálené lokality, může stahování vzdálených souborů. Tento proces funguje stejně jako publikování, s výjimkou v opačném pořadí.
> 
> Nebude popisujeme více o vzdálené úpravy a stáhnout vzdálené zařízení WebMatrix tady. Jsou velmi užitečné, pokud máte více lidem pracovat na stejném místě na různých počítačích. Další informace najdete v tématu [publikování a úprava vzdáleného webu pomocí WebMatrix 2 beta](https://go.microsoft.com/fwlink/?LinkId=251591).

## <a name="additional-resources"></a>Další prostředky

- [ASP.NET Fórum webových stránek WebMatrix ASP.NET](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages), což je skvělé místo pro publikování otázek a získání odpovědí.

> [!div class="step-by-step"]
> [Předchozí](layouts.md)
