---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-visual-studio-vb
title: Nasazení webu pomocí sady Visual Studio (VB) | Microsoft Docs
author: rick-anderson
description: Visual Studio obsahuje nástroje pro nasazení webu. Další informace o těchto nástrojích najdete v tomto kurzu.
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 977105f3-7987-4e50-8be7-afb53b4ca28a
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-visual-studio-vb
msc.type: authoredcontent
ms.openlocfilehash: 6c71e36a8a434947882cc767cd2f903ff6e8d422
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78587211"
---
# <a name="deploying-your-site-using-visual-studio-vb"></a>Nasazení webu pomocí sady Visual Studio (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_04_VB.zip) nebo [stažení PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial04_DeployingViaVS_vb.pdf)

> Visual Studio obsahuje nástroje pro nasazení webu. Další informace o těchto nástrojích najdete v tomto kurzu.

## <a name="introduction"></a>Úvod

Předchozí kurz se vyhledal při nasazení jednoduché webové aplikace v ASP.NET do poskytovatele webového hostitele. Konkrétně tento kurz ukázal, jak používat klienta FTP, jako je FileZilly, k přenosu potřebných souborů z vývojového prostředí do provozního prostředí. Visual Studio také nabízí integrované nástroje pro usnadnění nasazení pro poskytovatele webového hostitele. V tomto kurzu prochází dva z těchto nástrojů: Nástroj pro kopírování webu, kde můžete přesouvat soubory do a ze vzdáleného webového serveru pomocí serverových rozšíření FTP nebo FrontPage. a nástroj publikování, který zkopíruje celý web do zadaného umístění.

> [!NOTE]
> Další nástroje související s nasazením, které nabízí Visual Studio, obsahují [projekty pro instalaci webu](https://msdn.microsoft.com/library/wx3b589t.aspx) a doplněk [projekty nasazení webu](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en) . Projekty nastavení webu zabalí obsah webu a konfigurační informace do jednoho souboru MSI. Tato možnost je nejužitečnější pro weby, které jsou nasazeny v intranetu nebo pro společnosti, které prodávají předbalenou webovou aplikaci, kterou si zákazníci nainstalují na vlastní webové servery. Doplněk projekty nasazení webu je doplněk sady Visual Studio, který usnadňuje určení rozdílů v konfiguraci mezi sestaveními pro vývojová prostředí a produkční prostředí. Projekty instalace webu nejsou v této sérii kurzů popsány. Projekty nasazení webu jsou shrnuty v [*obecných rozdílech konfigurace mezi kurzem vývoje a produkce*](common-configuration-differences-between-development-and-production-vb.md) .

## <a name="deploying-your-site-using-the-copy-web-site-tool"></a>Nasazení lokality pomocí nástroje pro kopírování webu

Nástroj pro kopírování webu sady Visual Studio je podobný jako v funkčnosti samostatného klienta FTP. Nástroj kopírování webu ve kostce umožňuje připojit se ke vzdálenému webu prostřednictvím rozšíření FTP nebo serveru FrontPage. Podobně jako v uživatelském rozhraní FileZilly se uživatelské rozhraní kopírování webu skládá ze dvou podoken: v levém podokně jsou uvedeny místní soubory a v pravém podokně jsou uvedeny soubory na cílovém serveru.

> [!NOTE]
> Nástroj pro kopírování webu je k dispozici pouze pro webové projekty. Visual Studio nabízí tento nástroj při práci s projektem webové aplikace.

Pojďme se podívat na použití nástroje pro kopírování webu k publikování knihy recenze aplikace do produkčního prostředí. Vzhledem k tomu, že nástroj pro kopírování webu pracuje pouze s projekty, které používají model projektu webu, můžeme prostudovat pouze pomocí tohoto nástroje s projektem BookReviewsWSP. Otevřete tento projekt.

Kliknutím na ikonu Kopírovat web v Průzkumník řešení otevřete projekt nástroje pro kopírování webu (Tato ikona je v kruhu na obrázku 1); Alternativně můžete vybrat možnost Kopírovat web z nabídky Web. Buď se přiblíží, spustí se uživatelské rozhraní pro kopírování webu zobrazené na obrázku 1. naplní se jenom levé podokno na obrázku 1, protože se ještě máme připojit ke vzdálenému serveru.

[![uživatelské rozhraní nástroje Kopírovat web je rozdělené do dvou podoken.](deploying-your-site-using-visual-studio-vb/_static/image2.png)](deploying-your-site-using-visual-studio-vb/_static/image1.png)

**Obrázek 1**: uživatelské rozhraní nástroje Kopírovat web je rozdělené do dvou podoken ([kliknutím zobrazíte obrázek v plné velikosti).](deploying-your-site-using-visual-studio-vb/_static/image3.png)

Aby bylo možné nasadit náš web, musíme se nejdřív připojit k poskytovateli webového hostitele. Klikněte na tlačítko připojit v horní části uživatelského rozhraní Kopírovat web. Tím se zobrazí dialogové okno otevřít webovou stránku zobrazené na obrázku 2.

K cílovému webu se můžete připojit tak, že vyberete jednu ze čtyř možností zleva:

- **Systém souborů** – tuto možnost vyberte, pokud chcete web nasadit do složky nebo sdílené síťové složky dostupné z vašeho počítače.
- **Místní služba IIS** – pomocí této možnosti nasaďte lokalitu na webový server služby IIS nainstalovaný na vašem počítači.
- **Server FTP** – připojení ke vzdálenému webu pomocí FTP.
- **Vzdálený web** – připojení ke vzdálenému webu pomocí rozšíření serveru FrontPage.

Většina poskytovatelů webových hostitelů podporuje FTP, ale méně nabízí podporu rozšíření serveru FrontPage. Z tohoto důvodu jsem vybral možnost Server FTP a pak zadal informace o připojení, jak je znázorněno na obrázku 2.

[![určení cílového webu](deploying-your-site-using-visual-studio-vb/_static/image5.png)](deploying-your-site-using-visual-studio-vb/_static/image4.png)

**Obrázek 2**: určení cílového webu ([kliknutím zobrazíte obrázek v plné velikosti](deploying-your-site-using-visual-studio-vb/_static/image6.png))

Po připojení nástroj kopírování webu načte soubory ze vzdáleného webu v pravém podokně a určí stav každého souboru: nový, odstraněno, změněno nebo nezměněno. Můžete zkopírovat soubor z místní lokality do vzdálené lokality nebo naopak.

Pojďme do projektu BookReviewsWSP přidat novou stránku a pak ji nasadit, aby bylo možné zobrazit nástroj pro kopírování webu v akci. Vytvořte novou stránku ASP.NET v aplikaci Visual Studio v kořenovém adresáři s názvem `Privacy.aspx`. Použijte stránku předlohy `Site.master` a přidejte na tuto stránku zásady ochrany osobních údajů vaší lokality. Obrázek 3: po vytvoření této stránky se zobrazí Visual Studio.

[![do kořenové složky webu přidejte novou stránku s názvem &lt;Code&gt;Privacy. aspx&lt;/Code&gt;](deploying-your-site-using-visual-studio-vb/_static/image8.png)](deploying-your-site-using-visual-studio-vb/_static/image7.png)

**Obrázek 3**: přidejte novou stránku s názvem `Privacy.aspx` do kořenové složky webu ([kliknutím zobrazíte obrázek v plné velikosti).](deploying-your-site-using-visual-studio-vb/_static/image9.png)

Potom se vraťte do uživatelského rozhraní pro kopírování webu. Jak ukazuje obrázek 4, levé podokno nyní obsahuje nové soubory – `Policy.aspx` a `Policy.aspx.vb`. A co více, tyto soubory jsou označeny ikonou šipky a stavem nový, což značí, že existují v místní lokalitě, ale ne ve vzdálené lokalitě.

[![Nástroj pro kopírování webu obsahuje ve svém levém podokně nový kód &lt;&gt;osobních údajů. aspx&lt;/Code&gt;.](deploying-your-site-using-visual-studio-vb/_static/image11.png)](deploying-your-site-using-visual-studio-vb/_static/image10.png)

**Obrázek 4**: nástroj kopírování webu zahrnuje novou `Privacy.aspx` stránku v levém podokně ([kliknutím zobrazíte obrázek v plné velikosti).](deploying-your-site-using-visual-studio-vb/_static/image12.png)

Chcete-li nasadit nové soubory, vyberte je a potom klikněte na ikonu šipky pro přenos do vzdálené lokality. Po dokončení přenosu se `Policy.aspx` a `Policy.aspx.vb` soubory existují na místních i vzdálených lokalitách se stavem beze změny.

Spolu se seznamem nových souborů nástroj pro kopírování webu zvýrazní všechny soubory, které se liší mezi místními a vzdálenými lokalitami. Pokud to chcete vidět v akci, vraťte se na stránku `Privacy.aspx` a přidejte několik dalších slov do zásad ochrany osobních údajů. Uložte stránku a pak se vraťte k nástroji pro kopírování webu. Na obrázku 5 se zobrazí stránka `Privacy.aspx` v levém podokně se stavem změněno značící, že není synchronizován se vzdáleným webem.

[![Nástroj pro kopírování webu indikuje, že se změnila stránka &lt;kód&gt;osobních údajů. aspx&lt;/Code&gt;](deploying-your-site-using-visual-studio-vb/_static/image14.png)](deploying-your-site-using-visual-studio-vb/_static/image13.png)

**Obrázek 5**: Nástroj pro kopírování webu indikuje, že došlo ke změně `Privacy.aspx` stránky ([kliknutím zobrazíte obrázek v plné velikosti).](deploying-your-site-using-visual-studio-vb/_static/image15.png)

Nástroj Kopírovat web také indikuje, zda byl soubor od poslední operace kopírování odstraněn. Odstraňte `Privacy.aspx` z místního projektu a obnovte Nástroj pro kopírování webu. Soubory `Privacy.aspx` a `Privacy.aspx.vb` zůstanou uvedeny v levém podokně, ale mají stav odstraněno, což znamená, že byly od poslední operace kopírování odebrány.

## <a name="publishing-a-web-application"></a>Publikování webové aplikace

Další způsob, jak nasadit webovou aplikaci v rámci sady Visual Studio, je použití možnosti publikovat, která je přístupná prostřednictvím nabídky sestavit. Možnost publikovat explicitně zkompiluje aplikaci a pak zkopíruje všechny nezbytné soubory až do zadané vzdálené lokality. Jak vidíte krátce, možnost publikovat je více špičkou než Nástroj pro kopírování webu. Vzhledem k tomu, že nástroj pro kopírování webu umožňuje prozkoumávat soubory na místních a vzdálených lokalitách a umožňuje v případě potřeby nahrávat nebo stahovat jednotlivé soubory, možnost publikování nasadí celou webovou aplikaci.

Kromě kopírování všech potřebných souborů do zadané vzdálené lokality, možnost publikování také explicitně zkompiluje aplikaci. Vzhledem k tomu, že projekty webové aplikace musí být explicitně kompilovány, by měly být neočekávaně zkompilovány, že možnost publikovat je k dispozici pro projekty webových aplikací. Může se jednat o bitovou překvapivé možnost publikování je dostupná také pro webové projekty. Jak je uvedeno v kurzu [*určení toho, které soubory je třeba nasadit*](determining-what-files-need-to-be-deployed-vb.md) , mohou být webové projekty explicitně kompilovány prostřednictvím procesu, který je označován jako *předkompilace*. Tento kurz se zaměřuje na použití možnosti publikovat u projektů webových aplikací; v budoucím kurzu se prozkoumá předkompilace a v tomto bodě se vrátíme k použití možnosti publikovat u webových projektů.

> [!NOTE]
> Přestože je možnost publikovat v aplikaci Visual Studio k dispozici pro webové projekty a projekty webových aplikací, nabízí Visual Web Developer možnost publikování pouze pro projekty webových aplikací.

Pojďme se podívat na nasazení aplikace recenze knih pomocí možnosti Publikovat. Začněte tím, že v aplikaci Visual Studio otevřete BookReviewsWAP (projekt webové aplikace). V nabídce publikovat vyberte projekt sestavení BookReviewsWAP. Tím se zobrazí dialogové okno s výzvou k zadání cílového umístění, a to mimo jiné možnosti konfigurace (viz obrázek 6). Podobně jako u nástroje Kopírovat web můžete zadat umístění, které odkazuje na místní složku, místní web ve službě IIS, vzdálený web, který podporuje rozšíření serveru FrontPage nebo adresu serveru FTP. Můžete zvolit, zda chcete soubory na vzdáleném webovém serveru nahradit nasazenými soubory, nebo odstranit veškerý obsah na vzdáleném webu před publikováním. Můžete taky určit, jestli se mají kopírovat:

- Pouze soubory v projektu potřebné ke spuštění aplikace, což vynechává nepotřebný zdrojový kód a soubory související s projektem.
- Všechny soubory projektu, které zahrnují soubory zdrojového kódu a soubory projektu sady Visual Studio, jako je soubor řešení.
- Všechny soubory ve zdrojové složce projektu, které kopírují všechny soubory ve zdrojové složce projektu bez ohledu na to, zda jsou zahrnuty v projektu.

K dispozici je také možnost nahrát obsah složky `App_Data`.

[![určení cílového webu](deploying-your-site-using-visual-studio-vb/_static/image17.png)](deploying-your-site-using-visual-studio-vb/_static/image16.png)

**Obrázek 6**: určení cílového webu ([kliknutím zobrazíte obrázek v plné velikosti](deploying-your-site-using-visual-studio-vb/_static/image18.png))

Pro aplikaci pro kontrolu knihy obsahuje vzdálená lokalita soubory nasazené při kopírování projektu BookReviewsWSP pomocí nástroje pro kopírování webu. Proto máme možnost publikování začít tím, že odstraníte veškerý existující obsah. Můžeme také pouze zkopírovat potřebné soubory namísto zbytečného provozního prostředí pomocí nepotřebného zdrojového kódu a souborů projektu. Po zadání těchto možností klikněte na tlačítko publikovat. Během několika dalších sekund Visual Studio nasadí potřebné soubory do cílové lokality a zobrazí průběh v okně výstup.

Obrázek 7 zobrazuje soubory na serveru FTP po dokončení operace publikování. Všimněte si, že se nahrály jenom stránky značek a nezbytné soubory podpory na straně serveru a na straně klienta.

[do produkčního prostředí ![jenom potřebné soubory.](deploying-your-site-using-visual-studio-vb/_static/image20.png)](deploying-your-site-using-visual-studio-vb/_static/image19.png)

**Obrázek 7**: do produkčního prostředí se publikovaly jenom potřebné soubory ([kliknutím zobrazíte obrázek v plné velikosti](deploying-your-site-using-visual-studio-vb/_static/image21.png)).

Možnost publikovat je méně odlišit nástroj než Nástroj pro kopírování webu. Vzhledem k tomu, že nástroj pro kopírování webu umožňuje zkontrolovat soubory na místních a vzdálených lokalitách a zjistit, jak se liší, možnost publikování neposkytuje žádné takové rozhraní. Nástroj pro kopírování webu navíc umožňuje provádět jednorázové změny, nahrávat nebo odstraňovat jednotlivé soubory. Možnost publikování nepovoluje takové jemně odstupňované řízení; místo toho publikuje *celou* aplikaci. Toto chování má své specialisty a nevýhody. Na straně plus víte, že při použití možnosti Publikovat nebudete forgetting k nahrání důležitého souboru. Ale zvažte, co se stane, pokud jste provedli malou změnu velmi velkého webu – s možností publikovat nemůžete aktualizovat tuto stránku nebo dvě, které byly upraveny, ale místo toho musíte počkat, až Visual Studio nasadí celý web.

Nejedná se o některé soubory, jejichž obsah se mezi produkčním a vývojovým prostředím liší. Klíčovým příkladem je konfigurační soubor aplikace `Web.config`. Protože možnost publikování po zkopírování nekopíruje soubory webových aplikací, přepíše vlastní konfigurační soubory produkčního prostředí verzí ve vývojovém prostředí. Následující kurz podrobněji prozkoumá toto téma a nabízí tipy pro nasazení webové aplikace, pokud takové rozdíly existují.

## <a name="summary"></a>Souhrn

Nasazení webu zahrnuje kopírování potřebných souborů z vývojového prostředí do provozního prostředí. Předchozí kurz ukázal, jak přenášet soubory pomocí klienta FTP, jako je FileZilly. V tomto kurzu byly prověřeny dva nástroje pro nasazení v aplikaci Visual Studio: Nástroj pro kopírování webu a možnost publikovat. Nástroj pro kopírování webu je podobný klientovi FTP v tom, že má dvoufázové rozhraní se seznamem souborů v místním počítači a v zadaném vzdáleném počítači, který usnadňuje nahrávání nebo stahování souborů mezi dvěma počítači. Možnost publikovat je ještě tupý nástroj, který explicitně zkompiluje projekt a následně nasadí celou aplikaci do zadaného cíle.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Kopírování webu pomocí nástroje pro kopírování webu](https://msdn.microsoft.com/library/1cc82atw.aspx)
- [Postupy: nasazení webu pomocí nástroje pro kopírování](../../../videos/how-do-i/how-do-i-deploy-a-web-site-using-the-copy-web-site-tool.md) webu (video)
- [Postupy: publikování projektů webových aplikací](https://msdn.microsoft.com/library/aa983453.aspx)
- [Postupy: publikování webů](https://msdn.microsoft.com/library/20yh9f1b.aspx)
- [Projekty nastavení a nasazení v aplikaci Visual Studio](https://msdn.microsoft.com/library/wx3b589t.aspx)

> [!div class="step-by-step"]
> [Předchozí](deploying-your-site-using-an-ftp-client-vb.md)
> [Další](common-configuration-differences-between-development-and-production-vb.md)
