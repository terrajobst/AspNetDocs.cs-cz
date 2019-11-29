---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/precompiling-your-website-vb
title: Předkompilace webu (VB) | Microsoft Docs
author: rick-anderson
description: 'Visual Studio nabízí vývojářům ASP.NET dva typy projektů: projekty webových aplikací (WAPs) a projekty webu (WSPs). Jedna z klíčových rozdílů betwe...'
ms.author: riande
ms.date: 06/09/2009
ms.assetid: c285dc6f-a1c6-46e6-ac03-3830947f57e3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/precompiling-your-website-vb
msc.type: authoredcontent
ms.openlocfilehash: 1a46870b73f95300ef5bc1f72dda74d7d62ab11f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74588387"
---
# <a name="precompiling-your-website-vb"></a>Předkompilace webu (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_15_VB.zip) nebo [stažení PDF](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial15_Precompiling_vb.pdf)

> Visual Studio nabízí vývojářům ASP.NET dva typy projektů: projekty webových aplikací (WAPs) a projekty webu (WSPs). Jedním z klíčových rozdílů mezi těmito dvěma typy projektů je, že WAPs musí mít kód explicitně zkompilován před nasazením, zatímco kód v WSP lze automaticky zkompilovat na webovém serveru. Před nasazením je však možné předkompilovat WSP. Tento kurz zkoumá výhody předkompilace a ukazuje, jak předkompilovat web z aplikace Visual Studio a z příkazového řádku.

## <a name="introduction"></a>Úvod

Visual Studio nabízí vývojářům ASP.NET dva různé typy projektů: projekty webových aplikací (WAP) a webové projekty (WSP). Jedním z klíčových rozdílů mezi těmito typy projektů je, že WAPs vyžaduje *explicitní kompilaci* , zatímco WSPs ve výchozím nastavení používá *automatickou kompilaci*. Pomocí WAPs zkompilujete kód webové aplikace do jednoho sestavení, které je vytvořeno v `Bin` složce webu. Nasazení zahrnuje kopírování obsahu značek (`.aspx.ascx`a `.master` souborů) v projektu společně se sestavením ve složce `Bin`; samotné soubory třídy kódu na pozadí není nutné nasazovat. Na druhé straně nasadíte WSPs zkopírováním stránek značek a jejich odpovídajících tříd kódu na pozadí do provozního prostředí. Třídy kódu na pozadí jsou kompilovány na vyžádání na webovém serveru.

> [!NOTE]
> Další informace o rozdílech mezi projektovými modely, explicitní a automatickou kompilací a způsobu, jakým má model kompilace vliv na nasazení, naleznete v části "explicitní kompilace a Automatická kompilace" v tématu [ *určení, které soubory je nutné nasadit* ](determining-what-files-need-to-be-deployed-vb.md) .

Možnost automatické kompilace se snadno používá. Není k dispozici žádný explicitní krok kompilace a je třeba nasadit pouze soubory, které byly upraveny, zatímco explicitní kompilace vyžaduje nasazení změněných stránek značek a právě zkompilovaného sestavení. Automatické nasazení ale má dvě potenciální nevýhody:

- Vzhledem k tomu, že stránky musí být při prvním navštívení automaticky kompilovány, může při prvním spuštění stránky ASP.NET při prvním nasazení aplikace dojít k výraznému zpoždění, ale při prvním vyžádání stránky.
- Automatická kompilace vyžaduje, aby na webovém serveru existovaly deklarativní označení a zdrojový kód. Tato možnost může být neatraktivní, pokud plánujete prodej webové aplikace zákazníkům, kteří si ji nainstalují na své webové servery.

Pokud jsou některé ze dvou výše uvedených nedostatků, můžete buď přepnout na model WAP, nebo *předkompilovat* WSP před nasazením. Tento kurz prověřuje možnosti předkompilace, které jsou nejvhodnější pro hostovaný web, a projde procesem předkompilace a nasazením předkompilovaného webu.

## <a name="an-overview-of-aspnet-code-generation-and-compilation"></a>Přehled generování a kompilace kódu ASP.NET

Než se podíváme na dostupné možnosti předkompilace, Podívejme se nejprve na generování a kompilaci kódu, ke kterému dochází, když se na stránce ASP.NET požadavek poprvé, od jejího vytvoření nebo Poslední aktualizace. Jak víte, stránky ASP.NET se skládají ze dvou částí: deklarativní označení v souboru `.aspx`; a část zdrojového kódu, obvykle v samostatném souboru třídy kódu na pozadí (`.aspx.vb`). Kroky prováděné modulem runtime při vyžádání stránky ASP.NET závisí na modelu kompilace aplikace.

V WAPs musí být zdrojový kód stránky explicitně zkompilován do jednoho sestavení před jeho nasazením. Během nasazení se toto sestavení a různé stránky s označením zkopírují do produkčního prostředí. Když je žádost doručena webovému serveru pro stránku ASP.NET, modul runtime vytvoří instanci třídy kódu na pozadí stránky a vyvolá svoji `ProcessRequest` metodu, která spustí životní cyklus stránky a nakonec vygeneruje obsah stránky, který je vrácen žadateli. Modul runtime může pracovat s třídou kódu na pozadí stránky ASP.NET, protože třída kódu na pozadí již byla zkompilována do sestavení před nasazením.

Pomocí WSPs a automatické kompilace není před nasazením k dispozici žádný explicitní kompilační krok. Místo toho nasazení zahrnuje kopírování deklarativního i obsahu zdrojového kódu do produkčního prostředí. Při prvním doručení žádosti webovému serveru pro stránku ASP.NET od vytvoření nebo Poslední aktualizace stránky musí modul runtime nejprve kompilovat třídu Code-on do sestavení. Toto zkompilované sestavení je uloženo ve složce `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files`, i když umístění této složky lze přizpůsobit pomocí `<pages>` elementu v `Web.config`. Vzhledem k tomu, že je sestavení uloženo na disk, není nutné ho znovu zkompilovat u dalších požadavků na stejnou stránku.

> [!NOTE]
> Vzhledem k tomu, že byste očekávali, dojde k mírnému zpoždění při žádosti o stránku poprvé (nebo poprvé, kdy se změnila) v lokalitě, která používá automatickou kompilaci, protože chvíli trvá, než server zkompiluje kód stránky a uloží výsledné sestavení do disk.

V krátkém případě explicitní kompilace je nutná pro zkompilování zdrojového kódu webu před nasazením a uložení modulu runtime pro provedení tohoto kroku. Při automatické kompilaci modul runtime zpracovává kompilaci zdrojového kódu stránky, ale s mírnými náklady na inicializaci pro první návštěvu stránky od vytvoření nebo Poslední aktualizace.

Ale jak deklarativní část stránek ASP.NET (soubor `.aspx`)? Je zřejmé, že existuje vztah mezi `.aspx`mi soubory a kódem ve svých třídách kódu na pozadí, protože webové ovládací prvky definované v deklarativních označeních jsou přístupné v kódu. Je také zřejmé, že obsah v `.aspx` soubory významně ovlivňuje vykreslený kód vygenerovaný stránkou. Takže jak modul runtime pracuje s syntaxí text, HTML a webového ovládacího prvku, která je definovaná v souboru `.aspx` k vygenerování vykresleného obsahu požadované stránky?

Nechci získat příliš sidetracked podrobností implementace nízké úrovně, které se liší mezi WAPs a WSPs, ale v kostce modul runtime automaticky generuje soubor třídy, který obsahuje různé webové ovládací prvky jako chráněné členy a metody. Tento vygenerovaný soubor je implementován jako *Částečná třída* odpovídající třídě kódu na pozadí. ([Částečné třídy](http://www.dotnet-guide.com/partialclasses.html) umožňují rozdělit obsah jedné třídy mezi více souborů.) Třída kódu na pozadí je proto definována na dvou místech: v souboru `.aspx.vb`, který vytvoříte, a v této automaticky generované třídě, která je vytvořena modulem runtime. Tato automaticky generovaná třída je uložena ve složce `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files`.

Důležité z těchto důvodů je, že aby se stránka ASP.NET vykreslila modulem runtime, musí být jejich deklarativní a zdrojové části kódu zkompilovány do sestavení. V WAPs je zdrojový kód explicitně zkompilován do sestavení před nasazením, ale deklarativní kód musí být stále převeden na kód a kompilován modulem runtime na webovém serveru. Pomocí WSPs s použitím automatické kompilace musí být zdrojový i deklarativní kód zkompilován webovým serverem.

Je možné použít explicitní kompilaci s modelem WSP. Můžete explicitně kompilovat část zdrojového kódu, například s modelem WAP. Co je více, můžete také kompilovat deklarativní označení.

## <a name="precompilation-options"></a>Možnosti předkompilace

.NET Framework se dodává s [nástrojem ASP.NET Compilation (`aspnet_compiler.exe`)](https://msdn.microsoft.com/library/ms229863.aspx) , který umožňuje kompilovat zdrojový kód (a dokonce i obsah) aplikace ASP.NET vytvořené pomocí modelu WSP. Tento nástroj byl vydán s .NET Framework verze 2,0 a je umístěn ve složce `%WINDIR%\Microsoft.NET\Framework\v2.0.50727`; dá se použít z příkazového řádku nebo spustit z aplikace Visual Studio prostřednictvím možnosti publikování webu v nabídce sestavení.

Kompilační nástroj poskytuje dvě obecné formy kompilace: místní předkompilace a předkompilace pro nasazení. Pomocí místní předkompilace spustíte nástroj `aspnet_compiler.exe` z příkazového řádku a zadáte cestu k virtuálnímu adresáři nebo fyzické cestě webu, který se nachází ve vašem počítači. Nástroj pro kompilaci potom zkompiluje každou stránku ASP.NET v projektu a uloží zkompilované verze do složky `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files` stejným způsobem, jako kdyby byly stránky v první době navštíveny v prohlížeči. Místní předkompilace může urychlit první požadavek na nově nasazené stránky ASP.NET na vašem webu, protože to přinese modul runtime, aby nemusel provést tento krok. Nicméně předkompilace není vhodná pro většinu hostovaných webů, protože vyžaduje, abyste mohli spouštět programy z příkazového řádku webového serveru. Ve sdílených hostitelských prostředích není tato úroveň přístupu povolena.

> [!NOTE]
> Další informace o místní předběžné kompilaci najdete v tématu [Postup: Předkompilace webů ASP.NET](https://msdn.microsoft.com/library/ms227972.aspx) a [předkompilace v ASP.NET 2,0](http://www.odetocode.com/Articles/417.aspx).

Namísto kompilování stránek na webu do složky `Temporary ASP.NET Files`, předkompilace pro nasazení zkompiluje stránky do adresáře podle vašeho výběru a ve formátu, který lze nasadit do provozního prostředí.

Existují dva typy předkompilace pro nasazení, které prozkoumáme v tomto kurzu: Předkompilace s aktualizovatelným uživatelským rozhraním a předkompilace s neaktualizovatelným uživatelským rozhraním. Předkompilace s aktualizovatelným uživatelským rozhraním ponechá deklarativní označení v souborech `.aspx`, `.ascx`a `.master`. tím se umožní vývojářům zobrazit a v případě potřeby upravit deklarativní označení na provozním serveru. Předkompilace s neaktualizovatelným uživatelským rozhraním generuje `.aspx` stránky, které jsou anulování jakéhokoli obsahu a odstraňují `.ascx` a `.master` soubory. tím se skryje deklarativní označení a zabrání vývojářovi v jeho změně z produkčního prostředí.

### <a name="precompiling-for-deployment-with-an-updatable-user-interface"></a>Předkompilace pro nasazení s aktualizovatelným uživatelským rozhraním

Nejlepším způsobem, jak pochopit předkompilaci pro nasazení, je zobrazit příklad v akci. Pojďme předkompilovat knihu WSP pro nasazení pomocí aktualizovatelného uživatelského rozhraní. Kompilační nástroj ASP.NET lze vyvolat z nabídky sestavení sady Visual Studio nebo z příkazového řádku. Tato část se zabývá používáním nástroje z aplikace Visual Studio; oddíl "předkompilace z příkazového řádku" podívá na spuštění nástroje kompilátoru z příkazového řádku.

Otevřete knihu revize WSP v aplikaci Visual Studio, přejděte do nabídky sestavení a vyberte možnost nabídky publikovat web. Tím se otevře dialogové okno Publikovat web (viz **Obrázek 1**), kde můžete zadat cílové umístění, bez ohledu na to, jestli je možné aktualizovat uživatelské rozhraní předkompilovaných webů, a další možnosti nástrojů kompilátoru. Cílovým umístěním může být vzdálený webový server nebo server FTP, ale pro tuto chvíli vyberte složku na pevném disku vašeho počítače. Vzhledem k tomu, že chceme předkompilovat web s aktualizovatelným uživatelským rozhraním, ponechejte zaškrtnuté políčko umožnit tuto předkompilovaný web jako aktualizovatelnou a klikněte na OK.

[![](precompiling-your-website-vb/_static/image2.png)](precompiling-your-website-vb/_static/image1.png)

**Obrázek 1**: Nástroj pro kompilaci ASP.NET předkompiluje web do zadaného cílového umístění.  
 ([Kliknutím zobrazíte obrázek v plné velikosti.](precompiling-your-website-vb/_static/image3.png))

> [!NOTE]
> Možnost publikovat web není v nabídce sestavení k dispozici v aplikaci Visual Web Developer. Pokud používáte Visual Web Developer, budete muset použít verzi příkazového řádku nástroje ASP.NET Compilation Tool, který je popsaný v části "předkompilace z příkazového řádku".

Po Předkompilování webu přejděte do cílového umístění, které jste zadali v dialogovém okně Publikovat web. Chvíli Porovnejte obsah této složky s obsahem vašeho webu. **Obrázek 2** ukazuje složku webu recenze v knize. Všimněte si, že obsahuje soubory `.aspx` i `.aspx.cs`. Všimněte si také, že `Bin` adresář obsahuje jenom jeden soubor, `Elmah.dll`, který jsme přidali v [předchozím kurzu](logging-error-details-with-elmah-vb.md) .

[![](precompiling-your-website-vb/_static/image5.png)](precompiling-your-website-vb/_static/image4.png)

**Obrázek 2**: adresář projektu obsahuje soubory `.aspx` a `.aspx.cs`; Složka `Bin` obsahuje pouze `Elmah.dll`  
 ([Kliknutím zobrazíte obrázek v plné velikosti.](precompiling-your-website-vb/_static/image6.png))

**Obrázek 3** ukazuje složku cílového umístění, jejíž obsah byl vytvořen kompilačním nástrojem ASP.NET. Tato složka neobsahuje žádné soubory kódu na pozadí. Kromě toho `Bin` adresář této složky obsahuje několik sestavení a dva soubory `.compiled` kromě sestavení `Elmah.dll`.

[![](precompiling-your-website-vb/_static/image8.png)](precompiling-your-website-vb/_static/image7.png)

**Obrázek 3**: složka cílového umístění obsahuje soubory pro nasazení  
 ([Kliknutím zobrazíte obrázek v plné velikosti.](precompiling-your-website-vb/_static/image9.png))

Na rozdíl od explicitní kompilace v WAPs nevytvoří předkompilace pro proces nasazení jedno sestavení pro celou lokalitu. Místo toho se skládá z několika stránek do každého sestavení. Také zkompiluje soubor `Global.asax` (Pokud je k dispozici) do vlastního sestavení a také do všech tříd v `App_Code` složce. Soubory, které obsahují deklarativní označení pro webové stránky ASP.NET, uživatelské ovládací prvky a stránky předlohy (`.aspx`, `.ascx`a `.master` soubory), jsou zkopírovány do adresáře cílového umístění. Podobně se soubor `Web.config` kopíruje přímo přes, spolu se všemi statickými soubory, jako jsou obrázky, třídy CSS a soubory PDF. Chcete-li podrobnější popis toho, jak Nástroj pro kompilaci zpracovává různé typy souborů, přečtěte si téma [zpracování souborů během předkompilace ASP.NET](https://msdn.microsoft.com/library/e22s60h9.aspx).

> [!NOTE]
> Můžete nastavit, aby nástroj pro kompilaci mohl vytvořit jedno sestavení na stránce ASP.NET, uživatelský ovládací prvek nebo hlavní stránku, a to zaškrtnutím políčka používané pevné pojmenování a jednostránkové sestavení v dialogovém okně Publikovat web. Každá stránka ASP.NET kompilovaná s vlastním sestavením umožňuje přesnější kontrolu nad nasazením. Například pokud jste aktualizovali jednu webovou stránku ASP.NET a potřebujete nasadit tuto změnu, budete potřebovat nasadit soubor `.aspx` stránky a přidružené sestavení do produkčního prostředí. Další informace najdete v tématu [Postupy: generování pevných názvů pomocí kompilačního nástroje ASP.NET](https://msdn.microsoft.com/library/ms228040.aspx) .

Adresář cílového umístění obsahuje také soubor, který nebyl součástí předkompilovaného webového projektu, konkrétně `PrecompiledApp.config`. Tento soubor informuje modul runtime ASP.NET, že aplikace byla předkompilována a zda byla předkompilována s aktualizovatelným nebo neaktualizovatelným uživatelským rozhraním.

Nakonec chvíli počkejte, než se otevře jeden z `.aspx` souborů v cílovém umístění pomocí sady Visual Studio nebo vašeho textového editoru dle vlastního výběru. Pokud předkompilujete nasazení s aktualizovatelným uživatelským rozhraním, stránky ASP.NET v adresáři cílového umístění obsahují přesně stejný kód jako odpovídající soubory na webu.

### <a name="precompiling-for-deployment-with-a-non-updatable-user-interface"></a>Předkompilace pro nasazení s neaktualizovatelným uživatelským rozhraním

Nástroj kompilátoru ASP.NET lze také použít k Předkompilování webu pro nasazení s neaktualizovatelným uživatelským rozhraním. Předkompilování webu s neaktualizovatelným uživatelským rozhraním funguje podobně jako předkompilace s aktualizovatelným uživatelským rozhraním, což je hlavní rozdíl spočívá v tom, že stránky ASP.NET, uživatelské ovládací prvky a stránky předlohy v cílovém adresáři jsou odstraněny ze svých značek. Chcete-li předkompilovat web pro nasazení s neaktualizovatelným uživatelským rozhraním, vyberte možnost publikovat web z nabídky sestavit, ale zrušte výběr možnosti "umožnit této předkompilovaným webu, aby bylo možné aktualizovat" (viz **Obrázek 4**).

[![](precompiling-your-website-vb/_static/image11.png)](precompiling-your-website-vb/_static/image10.png)

**Obrázek 4**: zrušte u možnosti "umožnit tomuto předkompilovanému webu možnost aktualizace" předkompilovatelné uživatelské rozhraní bez možnosti aktualizace.  
 ([Kliknutím zobrazíte obrázek v plné velikosti.](precompiling-your-website-vb/_static/image12.png))

**Obrázek 5** zobrazuje cílovou složku umístění po předkompilování s neaktualizovatelným uživatelským rozhraním.

[![](precompiling-your-website-vb/_static/image14.png)](precompiling-your-website-vb/_static/image13.png)

**Obrázek 5**: složka cílového umístění pro nasazení s neaktualizovatelným uživatelským rozhraním  
 ([Kliknutím zobrazíte obrázek v plné velikosti.](precompiling-your-website-vb/_static/image15.png))

Porovnejte **Obrázek 3** s **obrázkem 5**. I když tyto dvě složky mohou vypadat stejně, Všimněte si, že složka uživatelského rozhraní, která není aktualizovatelná, nemá stránku předlohy, `Site.master`. I když **Obrázek 5** obsahuje různé stránky ASP.NET, pokud si zobrazíte obsah těchto souborů, zjistíte, že byly odstraněny jejich deklarativní značky a nahrazeny zástupným textem: "Toto je soubor značky generovaný nástrojem pro předkompilaci a neměl by být odstraněn!"

[![](precompiling-your-website-vb/_static/image17.png)](precompiling-your-website-vb/_static/image16.png)

**Obrázek 5**: deklarativní označení bylo odebráno ze stránek ASP.NET

`Bin` složky na **obrázcích 3** a **5** se podstatně liší. Kromě sestavení obsahuje `Bin` složka na **obrázku 5** `.compiled` soubor pro každou stránku ASP.NET, uživatelský ovládací prvek a stránku předlohy.

Předkompilování webu s neaktualizovatelným uživatelským rozhraním je užitečné v situacích, kdy nechcete, aby byl obsah stránek ASP.NET změněn osobou nebo společností, která instaluje nebo spravuje web v produkčním prostředí. Pokud vytvoříte webovou aplikaci ASP.NET, kterou prodáte zákazníkům pro instalaci na jejich vlastních webových serverech, možná budete chtít zajistit, aby nedošlo ke změně vzhledu a chování vašeho webu, a to přímým úpravou `.aspx` stránek, které dodáváte. Po Předkompilování webu s neaktualizovatelným uživatelským rozhraním dodáte jako součást instalace zástupné symboly `.aspx` stránky, čímž zabráníte zákazníkům v prohlížení a úpravách jejich obsahu.

### <a name="precompiling-from-the-command-line"></a>Předkompilace z příkazového řádku

Na pozadí dialogové okno publikování webu sady Visual Studio vyvolá kompilační nástroj ASP.NET (`aspnet_compiler.exe`) pro Předkompilování webu. Alternativně můžete tento nástroj vyvolat z příkazového řádku. Ve skutečnosti, pokud používáte Visual Web Developer, budete muset spustit nástroj kompilátoru z příkazového řádku, protože nabídka sestavení Visual Web Developer nezahrnuje možnost publikovat web.

Chcete-li použít nástroj kompilátoru z příkazového řádku, začněte vyřazením z příkazového řádku a přechodem do adresáře rozhraní `%WINDIR%\Microsoft.NET\Framework\v2.0.50727`. Dále do příkazového řádku zadejte následující příkaz:

`aspnet_compiler -p "physical_path_to_app" -v / -f -u "target_location_folder"`

Výše uvedený příkaz spustí nástroj ASP.NET Compiler (`aspnet_compiler.exe`) a přes `-p` přepínač dá pokyn, aby předkompiluje web rootem na *fyzické cestě\_\_na\_aplikaci*. Tato hodnota bude podobná `C:\MySites\BookReviews`a měla by být oddělená uvozovkami.

Přepínač `-v` určuje virtuální adresář webu. Pokud je váš web zaregistrován jako výchozí web v metabázi služby IIS, můžete vynechat přepínač `-p` a zadat pouze virtuální adresář aplikace. Použijete-li přepínač `-p`, hodnota, která pokračuje přepínačem `-v` označuje kořen webu a slouží k překladu kořenových odkazů aplikace. Pokud například zadáte hodnotu `-v /MySite` pak budou odkazy v aplikaci na `~/path/file` vyřešeny jako `~/MySite/path/file`. Vzhledem k tomu, že je web recenze webů umístěný v kořenovém adresáři na naší webové hostující společnosti, použili jste `-v /`přepínače.

`-f` přepínač, pokud je k dispozici, instruuje Nástroj pro kompilaci, aby přepsal *cílový\_umístění adresáře\_složky* , pokud již existuje. Vynecháte-li přepínač `-f` a složka cílového umístění již existuje, bude kompilační nástroj ukončen s chybou: "Error ASPRUNTIME: cílový adresář není prázdný. Odstraňte ji ručně nebo zvolte jiný cíl. "

Přepínač `-u`, pokud je k dispozici, informuje nástroj o vytvoření aktualizovatelného uživatelského rozhraní. Tento přepínač vynechejte, pokud chcete předkompilovat web s neaktualizovatelným uživatelským rozhraním.

Nakonec je *cílová\_umístění\_složky* fyzickou cestou k adresáři cílového umístění. Tato hodnota bude podobná `C:\MySites\Output\BookReviews`a měla by být oddělená uvozovkami.

## <a name="deploying-the-precompiled-website"></a>Nasazení předkompilovaného webu

V tuto chvíli jsme viděli, jak pomocí kompilačního nástroje ASP.NET předkompilovat web pomocí možností aktualizovatelné a neaktualizovatelné možnosti uživatelského rozhraní. Naše příklady proto zatím mají Předkompilování webu do místní složky a nikoli do provozního prostředí. Dobrá zpráva je, že nasazení předkompilovaného webu je Breeze a dá se dělat prostřednictvím sady Visual Studio nebo pomocí nějakého jiného mechanismu kopírování souborů, jako je například ze samostatného klienta FTP.

Dialogové okno Publikovat web (poprvé zobrazené na **obrázku 1**) má možnost cílového umístění, která označuje, kam se zkopírují soubory předkompilovaných webů. Toto umístění může být vzdálený webový server nebo server FTP. Zadáním vzdáleného serveru do tohoto textového pole předkompilujete a nasadíte web na určený server v jednom kroku. Případně můžete web předkompilovat do místní složky a pak ručně zkopírovat obsah této složky do provozního prostředí prostřednictvím FTP nebo nějakého jiného přístupu.

Automatické nasazení předkompilovaného webu prostřednictvím dialogového okna Publikovat web v aplikaci Visual Studio je užitečné pro jednoduché weby, u kterých neexistují žádné rozdíly v konfiguraci mezi vývojovým a produkčním prostředím. Jak je uvedeno v části [ *běžné rozdíly v konfiguraci mezi vývojovým a provozním* kurzem](common-configuration-differences-between-development-and-production-vb.md) , nejedná se ale o tyto rozdíly neobvyklým způsobem. Například kniha recenze webové aplikace používá jinou databázi v produkčním prostředí, než ve vývojovém prostředí. Když Visual Studio publikuje web na vzdáleném serveru, na kterém se nekopíruje informace o konfiguračním souboru ve vývojovém prostředí.

Pro weby, které mají rozdíly v konfiguraci mezi vývojovým a produkčním prostředím, může být nejvhodnější předkompilovat web do místního adresáře, zkopírovat je do konfiguračních souborů specifických pro produkční prostředí a pak zkopírovat obsah předkompilovaného výstupu do produkční.

Pro aktualizační program, který kopíruje soubory z vývojového prostředí do produkčního prostředí, odkazuje na [*nasazení webu pomocí klienta FTP*](deploying-your-site-using-an-ftp-client-vb.md) a [*nasazení webu pomocí kurzů sady Visual Studio*](determining-what-files-need-to-be-deployed-vb.md) .

## <a name="summary"></a>Přehled

ASP.NET podporuje dva režimy kompilace: Automatic a Explicit. Jak je popsáno v předchozích kurzech, projekty webové aplikace (WAPs) používají explicitní kompilaci, zatímco webové projekty (WSPs) používají ve výchozím nastavení automatickou kompilaci. Je však možné explicitně kompilovat WSP před nasazením pomocí kompilačního nástroje ASP.NET.

Tento kurz se zaměřuje na předkompilaci kompilačního nástroje pro podporu nasazení. Při předkompilování pro nasazení vytvoří Nástroj kompilace cílovou složku umístění, zkompiluje zadaný zdrojový kód webové aplikace a zkopíruje tyto zkompilované sestavení a soubory obsahu do složky cílového umístění. Kompilační nástroj lze nakonfigurovat tak, aby vytvořil aktualizovatelné nebo neaktualizovatelné uživatelské rozhraní. Je-li předkompilována s možností uživatelského rozhraní bez možnosti aktualizace, je odebráno deklarativní označení v souborech obsahu. V kostce umožňuje předkompilace nasadit webovou aplikaci založenou na projektu bez zahrnutí souborů zdrojového kódu a s odebraným deklarativním označením v případě potřeby.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Předkompilace webu ASP.NET](https://msdn.microsoft.com/library/ms228015.aspx)
- [CodeBehind a kompilace v ASP.NET 2,0](https://msdn.microsoft.com/magazine/cc163675.aspx)
- [Předkompilace v ASP.NET](http://www.odetocode.com/Articles/417.aspx)
- [Možnosti předkompilovaných webů v ASP.NET](http://www.dotnetperls.com/precompiled)

> [!div class="step-by-step"]
> [Předchozí](logging-error-details-with-elmah-vb.md)
> [Další](users-and-roles-on-the-production-website-vb.md)
