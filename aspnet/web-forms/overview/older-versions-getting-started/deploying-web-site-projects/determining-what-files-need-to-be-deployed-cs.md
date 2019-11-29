---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/determining-what-files-need-to-be-deployed-cs
title: Určení, které soubory je třeba nasadit (C#) | Microsoft Docs
author: rick-anderson
description: Jaké soubory je potřeba nasadit z vývojového prostředí do produkčního prostředí, závisí částečně na tom, jestli byla aplikace ASP.NET vytvořená v USA...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: f8d78a88-cc91-40d8-bce3-3d7954f6033b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/determining-what-files-need-to-be-deployed-cs
msc.type: authoredcontent
ms.openlocfilehash: 1dd4a1179d32f776626c08a07205dc9aabed588d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74596399"
---
# <a name="determining-what-files-need-to-be-deployed-c"></a>Zjištění souborů, které je potřeba nasadit (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_02_CS.zip) nebo [stažení PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial02_FilesToDeploy_cs.pdf)

> Jaké soubory je potřeba nasadit z vývojového prostředí do produkčního prostředí, závisí částečně na tom, jestli byla aplikace ASP.NET sestavená pomocí modelu webu nebo modelu webové aplikace. Přečtěte si další informace o těchto dvou modelech projektu a o tom, jaký vliv má model projektu na nasazení.

## <a name="introduction"></a>Úvod

Nasazení webové aplikace v ASP.NET zahrnuje kopírování souborů souvisejících s ASP.NET z vývojového prostředí do produkčního prostředí. Soubory související s ASP.NET zahrnují kód webové stránky ASP.NET a kód a podpůrné soubory na straně klienta a serveru. Soubory podpory na straně klienta jsou soubory, na které odkazuje vaše webová stránka a které se odesílají přímo do prohlížeče – obrázky, soubory CSS a soubory JavaScriptu, například. Soubory podpory na straně serveru obsahují ty, které se používají ke zpracování žádosti na straně serveru. To zahrnuje konfigurační soubory, webové služby, soubory tříd, typové datové sady a LINQ to SQL soubory mimo jiné.

Obecně platí, že všechny soubory podpory na straně klienta by měly být zkopírovány z vývojového prostředí do produkčního prostředí, ale kopírování souborů podpory na straně serveru závisí na tom, zda explicitně kompilujete kód na straně serveru do sestavení (`.dll` soubor), nebo pokud máte tato sestavení automaticky vygenerována. V tomto kurzu se zvýrazní, které soubory je potřeba nasadit, když kód explicitně zkompilujete do sestavení, oproti kterému má tento krok kompilace automaticky.

## <a name="explicit-compilation-versus-automatic-compilation"></a>Explicitní kompilace versus Automatická kompilace

Webové stránky ASP.NET jsou rozděleny na deklarativní značky a zdrojový kód. Část deklarativní označení obsahuje kód HTML, webové ovládací prvky a syntaxi datové vazby; část s kódem obsahuje obslužné rutiny událostí napsané C# v Visual Basic nebo kódu. Části značky a kódu jsou obvykle rozděleny do různých souborů: `WebPage.aspx` obsahuje deklarativní označení, zatímco `WebPage.aspx.cs` domů kódu.

Zvažte stránku ASP.NET s názvem Clock. aspx, která obsahuje ovládací prvek popisek, jehož vlastnost text je nastavená na aktuální datum a čas, kdy se stránka načte. Deklarativní část označení (v `Clock.aspx`) by měla obsahovat označení pro webový ovládací prvek popisku-`<asp:Label runat="server" id="TimeLabel" />`-zatímco část kódu (v `Clock.aspx.cs`) by měla obslužnou rutinu události `Page_Load` s následujícím kódem:

[!code-csharp[Main](determining-what-files-need-to-be-deployed-cs/samples/sample1.cs)]

Aby modul ASP.NET mohl obsluhovat požadavek na tuto stránku, musí být nejprve kompilována část kódu stránky (`WebPage.aspx.cs` soubor). Tato kompilace může být provedena explicitně nebo automaticky.

Pokud k zkompilování dojde explicitně, je zdrojový kód aplikace zkompilován do jednoho nebo více sestavení (`.dll` soubory) umístěných v adresáři `Bin` aplikace. Pokud k kompilaci dojde automaticky, výsledné automaticky generované sestavení je ve výchozím nastavení umístěno ve složce `Temporary ASP.NET` soubory, které lze najít v `%WINDOWS%\Microsoft.NET\Framework\` *&lt;verze&gt;* , i když je toto umístění konfigurovatelné prostřednictvím [prvku`<compilation>`](https://msdn.microsoft.com/library/s10awwz0.aspx) v `Web.config`. Při explicitní kompilaci musíte provést určitou akci pro zkompilování kódu aplikace ASP.NET do sestavení a tento krok nastane před nasazením. Při automatické kompilaci dojde k procesu kompilace na webovém serveru při prvním otevření prostředku.

Bez ohledu na to, jaký model kompilace použijete, je nutné zkopírovat část všech ASP.NET stránek (`WebPage.aspx` soubory) do produkčního prostředí. V případě explicitní kompilace je nutné zkopírovat sestavení ve složce `Bin`, ale nemusíte kopírovat části kódu stránky ASP.NET (soubory `WebPage.aspx.cs`). Při automatické kompilaci potřebujete zkopírovat soubory kódových částí, aby byl kód přítomen a mohl by být kompilován automaticky při návštěvě stránky. Část označení každé webové stránky v ASP.NET zahrnuje direktivu `@Page` s atributy, které označují, zda byl přidružený kód stránky již explicitně zkompilován nebo zda je nutné automaticky kompilovat. V důsledku toho produkční prostředí může pracovat s modelem kompilace hladce a nemusíte použít žádné speciální nastavení konfigurace, abyste označili, že se používá explicitní nebo Automatická kompilace.

Tabulka 1 shrnuje různé soubory k nasazení při použití explicitní kompilace versus automatické kompilace. Všimněte si, že bez ohledu na použitý model kompilace byste měli vždy nasadit sestavení ve složce `Bin`, pokud tato složka existuje. Složka `Bin` obsahuje sestavení specifická pro webovou aplikaci, která zahrnuje kompilovaný zdrojový kód při použití explicitního kompilačního modelu. `Bin` adresář obsahuje také sestavení z jiných projektů a jakékoli Open-Source sestavení nebo sestavení třetích stran, která můžete používat a které musí být na provozním serveru. Proto se jako obecné pravidlo povede při nasazení zkopírovat složku `Bin` až do produkčního prostředí. (Pokud používáte automatický kompilační model a nepoužíváte žádná externí sestavení, nebudete mít `Bin` adresář – to je OK!)

| **Model kompilace** | **Nasadit soubor s označením kódu?** | **Nasadit soubor zdrojového kódu?** | **Nasadit sestavení v adresáři `Bin`?** |
| --- | --- | --- | --- |
| Explicitní kompilace | Ano | Ne | Ano |
| Automatická kompilace | Ano | Ano | Ano (pokud existuje) |

**Tabulka 1:** Jaké soubory, které nasazujete, závisí na použitém modelu kompilace.

## <a name="taking-a-trip-down-memory-lane"></a>Vytvoření cesty k paměti Lane

Jaký přístup k kompilaci je použit, závisí částečně na tom, jak je aplikace ASP.NET spravována v aplikaci Visual Studio. Doby. Vyvzniká netto v roce 2000 existují čtyři různé verze sady Visual Studio – Visual Studio .NET 2002, Visual Studio .NET 2003, Visual Studio 2005 a Visual Studio 2008. Aplikace sady Visual Studio .NET 2002 a 2003 spravované ASP.NET pomocí *modelu projektu webové aplikace*. Klíčové funkce modelu projektu webové aplikace jsou:

- Soubory, které strukturu projekt, jsou definovány v jednom souboru projektu. Všechny soubory, které nejsou definovány v souboru projektu, nejsou považovány za součást webové aplikace sady Visual Studio.
- Používá explicitní kompilaci. Sestavení projektu zkompiluje soubory kódu v rámci projektu do jednoho sestavení, které je umístěno ve složce `Bin`.

Když společnost Microsoft vydala Visual Studio 2005, že odstranila podporu pro model projektu webové aplikace a nahradila ji modelem projektu webu. Model projektu webu, který se odlišuje od modelu projektu webové aplikace, následujícími způsoby:

- Místo toho, abyste měli jeden soubor projektu, který vypíše soubory projektu, se místo toho použije systém souborů. V krátkém případě jsou všechny soubory v rámci složky webové aplikace (nebo podsložek) považovány za součást projektu.
- Sestavení projektu v aplikaci Visual Studio nevytvoří sestavení v adresáři `Bin`. Místo toho sestavení webového projektu ohlásí chyby při kompilaci.
- Podpora automatické kompilace. Webové projekty jsou obvykle nasazeny zkopírováním značky a zdrojového kódu do produkčního prostředí, i když kód může být předkompilován (explicitní kompilace).

Microsoft obnovená model projektu webové aplikace při vydání sady Visual Studio 2005 Service Pack 1. Visual Web Developer však nadále podporuje pouze model projektu webu. Dobrá zpráva je, že toto omezení bylo vyřazeno s aplikací Visual Web Developer 2008 Service Pack 1. V současné době můžete vytvářet ASP.NET aplikace v aplikaci Visual Studio (a Visual Web Developer) pomocí modelu projektu webové aplikace nebo modelu projektu webu. Oba modely mají své specialisty i nevýhody. Přečtěte si [Úvod do projektů webových aplikací: porovnání projektů webových serverů a projektů webových aplikací](https://msdn.microsoft.com/library/aa730880.aspx#wapp_topic5) pro porovnání dvou modelů a určení toho, jaký model projektu nejlépe vyhovuje vaší situaci.

## <a name="exploring-the-sample-web-application"></a>Zkoumání ukázkové webové aplikace

Stažení pro tento kurz obsahuje aplikaci ASP.NET s názvem recenze knih. Web napodobuje web hobby, který může někdo vytvořit ke sdílení svých knih v online komunitě. Tato webová aplikace ASP.NET je velmi jednoduchá a skládá se z následujících prostředků:

- `Web.config`konfigurační soubor aplikace.
- Stránka předlohy (`Site.master`).
- Sedm různých ASP.NET stránek: 

    - ~`/Default.aspx`– Domovská stránka webu.
    - ~`/About.aspx`-stránka o webu.
    - ~`/Fiction/Default.aspx` – stránka obsahující seznam fiktivních literatur, které byly zkontrolovány. 

        - ~`/Fiction/Blaze.aspx` – přezkoumání Richard Bachman a nové *Blaze*.
    - ~/`Tech/Default.aspx` – stránka se seznamem technologických knih, které byly zkontrolovány. 

        - ~/`Tech/CYOW.aspx`– kontrola *Vytvoření vlastního webu*.
        - ~/`Tech/TYASP35.aspx` – přezkoumání *učení ASP.NET 3,5 za 24 hodin*.
- Tři různé soubory CSS ve složce Styles.
- Čtyři soubory obrázků – s využitím loga ASP.NET a obrázků pro tři revidované knihy, které se nacházejí ve složce `Images`.
- `Web.sitemap` soubor, který definuje mapu lokality a slouží k zobrazení nabídek na stránkách `Default.aspx` v kořenovém adresáři a v `Fiction` a `Tech` složkách.
- Soubor třídy s názvem `BasePage.cs`, který definuje základní třídu `Page`. Tato třída rozšiřuje funkčnost třídy `Page` tím, že automaticky nastaví vlastnost `Title` na základě pozice stránky v mapě webu. V kostce bude mít všechny třídy ASP.NET kódu na pozadí, která rozšiřuje `BasePage` (místo `System.Web.UI.Page`), název nastavený na hodnotu v závislosti na jeho umístění v mapě webu. Například při zobrazení stránky ~/`Tech/CYOW.aspx` je název nastaven na "domů: technologie: vytvořit vlastní web".

Obrázek 1 znázorňuje snímek obrazovky webu Recenze, který je zobrazený v prohlížeči. Tady se zobrazí stránka ~/`Tech/TYASP35.aspx`, která zkontroluje, že se *v knize naučíte ASP.NET 3,5 za 24 hodin*. Popis cesty, který se nachází v horní části stránky, a nabídka v levém sloupci vychází z struktury mapy webu definované v `Web.sitemap`. Obrázek v pravém horním rohu je jedním z titulů brožury umístěných ve složce `Images`. Vzhled a chování webu jsou definovány pomocí kaskádových pravidel šablon stylů, které jsou vyhledány v souborech šablon stylů CSS ve složce styly, zatímco rozložení stránky je definováno na stránce předlohy `Site.master`.

[![web recenze nabídek nabízí recenze pro sortiment názvů](determining-what-files-need-to-be-deployed-cs/_static/image2.png)](determining-what-files-need-to-be-deployed-cs/_static/image1.png)

**Obrázek 1:** Web recenze webů nabízí recenze pro seznam názvů ([kliknutím zobrazíte obrázek v plné velikosti).](determining-what-files-need-to-be-deployed-cs/_static/image3.png)

Tato aplikace nepoužívá databázi. Každá revize je implementována jako samostatná webová stránka v aplikaci. Tento kurz (a další několik kurzů) vás provede nasazením webové aplikace, která nemá databázi. V budoucím kurzu ale tuto aplikaci vylepšíme tak, aby ukládala recenze, komentáře ke čtenářům a další informace v rámci databáze a prozkoumali, jaké kroky je potřeba provést, aby se mohla správně nasadit webová aplikace řízená daty.

> [!NOTE]
> Tyto kurzy se zaměřují na hostování ASP.NET aplikací pomocí poskytovatele webového hostitele a nezkoumejte pomocná témata, jako je například ASP. Systém mapy webu nebo používá základní třídu `Page`. Další informace o těchto technologiích a další informace o dalších tématech popsaných v celém kurzu najdete v části Další materiály pro čtení na konci každého kurzu.

Stažení tohoto kurzu má dvě kopie webové aplikace, z nichž každá je implementována jako jiný typ projektu sady Visual Studio: BookReviewsWAP, projekt webové aplikace a BookReviewsWSP, projekt webu. Oba projekty byly vytvořeny pomocí aplikace Visual Web Developer 2008 SP1 a používají ASP.NET 3,5 SP1. Pokud chcete s těmito projekty pracovat, začněte tím, že rozzipovává obsah na plochu. Chcete-li otevřít projekt webové aplikace (BookReviewsWAP), přejděte do složky BookReviewsWAP a dvakrát klikněte na soubor řešení `BookReviewsWAP.sln`. Chcete-li otevřít projekt webu (BookReviewsWSP), spusťte aplikaci Visual Studio a potom v nabídce soubor zvolte možnost otevřít web, přejděte do složky `BookReviewsWSP` na ploše a klikněte na tlačítko OK.

Zbývajících dvou částech tohoto kurzu se dozvíte, jaké soubory budete potřebovat zkopírovat do provozního prostředí při nasazování aplikace. Následující dva kurzy – *[nasazení lokality pomocí FTP](deploying-your-site-using-an-ftp-client-cs.md)* a *[nasazení webu pomocí sady Visual Studio](deploying-your-site-using-visual-studio-cs.md)* – zobrazení různých způsobů kopírování těchto souborů do poskytovatele webového hostitele.

## <a name="determining-the-files-to-deploy-for-the-web-application-project"></a>Určení souborů pro nasazení pro projekt webové aplikace

Model projektu webové aplikace používá explicitní kompilaci – zdrojový kód projektu je zkompilován do jediného sestavení při každém sestavení aplikace. Tato kompilace zahrnuje soubory ASP.NET kódu na pozadí (~/`Default.aspx.cs`, ~/`About.aspx.cs`a tak dále) a také třídu `BasePage.cs`. Výsledné sestavení má název BookReviewsWAP. dll a je umístěno v adresáři `Bin` aplikace.

Na obrázku 2 jsou uvedeny soubory, které tvoří knihu pro revize projektu webové aplikace.

[![Průzkumník řešení zobrazí seznam souborů, které tvoří projekt webové aplikace.](determining-what-files-need-to-be-deployed-cs/_static/image5.png)](determining-what-files-need-to-be-deployed-cs/_static/image4.png)

**Obrázek 2**: Průzkumník řešení obsahuje seznam souborů, které tvoří projekt webové aplikace.

Chcete-li nasadit aplikaci ASP.NET vyvinutou pomocí modelu projektu webové aplikace, začněte sestavením aplikace tak, aby explicitně zkompiluje nejaktuálnější zdrojový kód do sestavení. V dalším kroku zkopírujte do produkčního prostředí následující soubory:

- Soubory, které obsahují deklarativní označení pro každou stránku ASP.NET, například ~/`Default.aspx`, ~/`About.aspx`a tak dále. Také zkopírujte deklarativní označení pro všechny stránky předlohy a uživatelské ovládací prvky.
- Sestavení (`.dll` soubory) ve složce `Bin` Nemusíte kopírovat soubory databáze programu (`.pdb`) ani žádné soubory XML, které se mohou v adresáři `Bin` najít.

Nemusíte kopírovat soubory zdrojového kódu stránky ASP.NET do produkčního prostředí ani nemusíte kopírovat soubor třídy `BasePage.cs`.

> [!NOTE]
> Jak ukazuje obrázek 2, třída `BasePage` je implementována jako soubor třídy v projektu, umístěn do složky s názvem `HelperClasses`. Když je projekt kompilován, kód v `BasePage.cs` souboru je zkompilován společně s třídami kódu na pozadí ASP.NET stránek do jediného sestavení, `BookReviewsWAP.dll.` ASP.NET má speciální složku s názvem `App_Code`, která je navržena tak, aby obsahovala soubory tříd pro webové projekty. Kód ve složce `App_Code` je automaticky zkompilován, a proto by neměl být použit s projekty webových aplikací. Místo toho byste měli umístit soubory třídy vaší aplikace do normální složky s názvem `HelperClasses`nebo `Classes`nebo podobným způsobem. Alternativně můžete umístit soubory třídy do samostatného projektu knihovny tříd.

Kromě kopírování souborů značek souvisejících s ASP.NET a sestavení ve složce `Bin` je také nutné zkopírovat soubory podpory na straně klienta – obrázky a soubory CSS a také jiné soubory podpory na straně serveru, `Web.config` a `Web.sitemap`. Tyto soubory podpory na straně klienta a serveru musí být zkopírovány do produkčního prostředí bez ohledu na to, zda používáte explicitní nebo automatickou kompilaci.

## <a name="determining-the-files-to-deploy-for-the-web-site-project-files"></a>Určení souborů pro nasazení pro soubory projektu webu

Model projektu webu podporuje automatickou kompilaci, funkce není k dispozici při použití modelu projektu webové aplikace. Pomocí explicitní kompilace musíte zkompilovat zdrojový kód projektu do sestavení a zkopírovat toto sestavení do provozního prostředí. Na druhé straně s automatickou kompilací stačí zkopírovat zdrojový kód do provozního prostředí a v případě potřeby ho zkompilovat na vyžádání.

Možnost nabídky sestavení v aplikaci Visual Studio je k dispozici v projektech webové aplikace i v projektech webu. Sestavení projektů webové aplikace zkompiluje zdrojový kód projektu do jednoho sestavení umístěného v adresáři `Bin`; sestavování projektu webu kontroluje jakékoli chyby při kompilaci, ale nevytváří žádná sestavení. Pro nasazení aplikace ASP.NET vyvinuté pomocí modelu projektu webu stačí zkopírovat příslušné soubory do produkčního prostředí, ale doporučujeme nejprve sestavit projekt, aby se zajistilo, že nedojde k žádným chybám při kompilaci.

Obrázek 3 ukazuje soubory, které tvoří knihu web Project Reviews.

 [![Průzkumník řešení obsahuje seznam souborů, které tvoří projekt webu.](determining-what-files-need-to-be-deployed-cs/_static/image7.png)](determining-what-files-need-to-be-deployed-cs/_static/image6.png) 

**Obrázek 3**: Průzkumník řešení obsahuje seznam souborů, které tvoří projekt webu.

Nasazení webového projektu zahrnuje kopírování všech souborů souvisejících s ASP.NET do produkčního prostředí – to zahrnuje stránky značek pro stránky ASP.NET, stránky předlohy a uživatelské ovládací prvky spolu s jejich soubory kódu. Také je nutné zkopírovat všechny soubory třídy, například BasePage.cs. Všimněte si, že `BasePage.cs` soubor se nachází ve složce `App_Code`, která je speciální složkou ASP.NET použitou v projektech webu pro soubory tříd. Speciální složku je nutné vytvořit také v produkčním prostředí, protože soubory třídy ve složce `App_Code` ve vývojovém prostředí musí být zkopírovány do složky `App_Code` v produkčním prostředí.

Kromě kopírování souborů značek ASP.NET a zdrojového kódu je také nutné zkopírovat soubory podpory na straně klienta – obrázky a soubory CSS a také jiné soubory podpory na straně serveru, `Web.config` a `Web.sitemap`.

> [!NOTE]
> Webové projekty mohou také používat explicitní kompilaci. V budoucím kurzu se podíváme, jak explicitně zkompilovat projekt webu.

## <a name="summary"></a>Přehled

Nasazení aplikace ASP.NET zahrnuje kopírování potřebných souborů z vývojového prostředí do provozního prostředí. Přesná sada souborů, které je třeba synchronizovat, závisí na tom, zda je kód aplikace ASP.NET explicitně nebo automaticky zkompilován. Použitá strategie kompilace je ovlivněna tím, že je aplikace Visual Studio nakonfigurována pro správu aplikace ASP.NET pomocí modelu projektu webové aplikace nebo modelu webu projektu.

Model projektu webové aplikace používá explicitní kompilaci a zkompiluje kód projektu do jednoho sestavení ve složce `Bin`. Při nasazování aplikace musí být část kódu stránky ASP.NET a obsah složky `Bin` vloženy do produkčního prostředí; zdrojový kód v aplikaci – soubory kódu a třídy kódu na pozadí, například nemusejí být kopírovány do produkčního prostředí.

Model webu projektu používá automatickou kompilaci ve výchozím nastavení, i když je možné explicitně zkompilovat projekt webu, jak uvidíme v budoucích kurzech. Nasazení aplikace ASP.NET, která používá automatickou kompilaci, vyžaduje zkopírování části kódu *a* zdrojového kódu do produkčního prostředí. Kód je automaticky zkompilován v produkčním prostředí, když je vyžádán poprvé.

Teď, když jsme prozkoumali, jaké soubory je třeba synchronizovat mezi vývojovým a produkčním prostředím, jsme připraveni nasadit aplikaci recenze do poskytovatele webového hostitele.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Přehled kompilace ASP.NET](https://msdn.microsoft.com/library/ms178466.aspx)
- [Uživatelské ovládací prvky ASP.NET](https://msdn.microsoft.com/library/y6wb1a0e.aspx)
- [Prozkoumává se ASP. SÍŤ – navigace na webu](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [Úvod do projektů webových aplikací](https://msdn.microsoft.com/library/aa730880.aspx)
- [Kurzy k hlavní stránce](../master-pages/creating-a-site-wide-layout-using-master-pages-cs.md)
- [Sdílení kódu mezi stránkami](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/pages/code.aspx)
- [Použití vlastní základní třídy pro třídy kódu na pozadí ASP.NET stránek](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)
- [Systém projektu webu sady Visual Studio 2005: co je to a proč to máme?](https://weblogs.asp.net/scottgu/archive/2005/08/21/423201.aspx)
- [Návod: převod webu na projekt webové aplikace v aplikaci Visual Studio](https://msdn.microsoft.com/library/aa983476.aspx)

> [!div class="step-by-step"]
> [Předchozí](asp-net-hosting-options-cs.md)
> [Další](deploying-your-site-using-an-ftp-client-cs.md)
