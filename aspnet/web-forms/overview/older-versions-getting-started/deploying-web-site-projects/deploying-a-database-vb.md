---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-a-database-vb
title: Nasazení databáze (VB) | Microsoft Docs
author: rick-anderson
description: Nasazení webové aplikace v ASP.NET zahrnuje získání potřebných souborů a prostředků z vývojového prostředí do provozního prostředí. Pro da...
ms.author: riande
ms.date: 04/23/2009
ms.assetid: 96ac3e69-04c7-4917-ad06-5f8968c3fbf1
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-a-database-vb
msc.type: authoredcontent
ms.openlocfilehash: 8221025bec06e052016070f74deabb3e6d936045
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74643546"
---
# <a name="deploying-a-database-vb"></a>Nasazení databáze (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_07_VB.zip) nebo [stažení PDF](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial07_DeployDB_vb.pdf)

> Nasazení webové aplikace v ASP.NET zahrnuje získání potřebných souborů a prostředků z vývojového prostředí do provozního prostředí. Pro webové aplikace řízené daty to zahrnuje schéma databáze a data. Tento kurz je první v řadě, který prozkoumá kroky potřebné k úspěšnému nasazení databáze z vývojového prostředí do produkčního prostředí.

### <a name="introduction"></a>Úvod

Nasazení webové aplikace v ASP.NET zahrnuje získání potřebných souborů a prostředků z vývojového prostředí do provozního prostředí. V průběhu posledních šesti kurzů jsme se podívali na nasazení jednoduché recenze webové aplikace. Tato ukázková lokalita se skládá z několika prostředků na straně serveru – ASP.NET stránek, konfiguračních souborů, souborů `Web.sitemap` a tak dále s prostředky na straně klienta, jako jsou obrázky a soubory CSS. Ale co jsou webové aplikace řízené daty? Jaké další kroky je potřeba provést k nasazení webové aplikace, která používá databázi?

V dalších několika kurzech budeme řešit kroky potřebné k nasazení webové aplikace řízené daty. Tento kurz se spustí tím, že se podíváme, jak získat schéma a obsah databáze z vývojového prostředí do provozního prostředí, zatímco v dalším kurzu se zobrazí potřebné změny konfigurace. Po prozkoumání výzev k nasazení databáze, která používá Aplikační služby (členství, role, profil atd.).

## <a name="examining-the-updated-book-reviews-web-application"></a>Kontrola aktualizovaných webových aplikací pro recenze knih

Aby bylo možné předvést nasazení webové aplikace řízené daty, aktualizovala mi Web Application recenze z jednoduchého, statického webu na jeden řízený daty. Stejně jako dřív existují dvě verze aplikace v tomto kurzu stažení: jeden, který používá model projektu webové aplikace a jeden, který používá model projektu webu.

Aktualizovaná webová aplikace recenze knih používá databázi [edice SQL Server 2008 Express](https://www.microsoft.com/express/sql/default.aspx) , která je uložena ve složce `App_Data` webu (`~/App_Data/Reviews.mdf`). Pokud máte v počítači nainstalovanou SQL Server 2008, měla by se ukázka spustit bez chyby. Pokud máte starší verzi SQL Server můžete buď nainstalovat bezplatnou edici SQL Server 2008 Express, nebo můžete pomocí databázových skriptů dostupných v tomto kurzu stáhnout vytvořit databázi sami.

Databáze `Reviews.mdf` obsahuje čtyři tabulky:

- `Genres` – obsahuje záznam pro každý žánr, například technologie, fiktivní a obchodní.
- `Books` – obsahuje záznam pro každou kontrolu, ve kterém jsou sloupce jako `Title`, `GenreId`, `ReviewDate`a `Review`mimo jiné.
- `Authors` – obsahuje informace o každém autorovi, který přispěl k revidované knize.
- `BooksAuthors` – tabulka JOIN typu m:n, která určuje, co autoři napsali jako knihy.

Obrázek 1 znázorňuje diagram ER těchto čtyř tabulek.

[![se databáze webových aplikací s recenzemi knih skládá ze čtyř tabulek](deploying-a-database-vb/_static/image2.jpg)](deploying-a-database-vb/_static/image1.jpg) 

**Obrázek 1**: databáze webových aplikací recenze knih se skládá ze čtyř tabulek ([kliknutím zobrazíte obrázek v plné velikosti).](deploying-a-database-vb/_static/image3.jpg)

Předchozí verze webu Recenze knih měla pro každou knihu samostatnou ASP.NET stránku. Například se objevila Stránka s názvem `~/Tech/TYASP35.aspx`, která obsahuje revizi *ASP.NET 3,5 za 24 hodin*. Tato nová webová verze na základě dat obsahuje recenze uložené v databázi a na jednu stránku ASP.NET, Projděte si. aspx? ID =*bookId*, ve kterém se zobrazí revize pro určenou knihu. Podobně existuje stránka Žánr. aspx? ID =*genreId* , ve které jsou uvedeny revidované knihy v zadaném žánru.

Na obrázcích 2 a 3 se zobrazuje `Genre.aspx` a `Review.aspx` stránky v akci. Poznamenejte si adresu URL v adresním řádku jednotlivých stránek. Na obrázku 2 je to s žánrem. aspx? ID = 85d164ba-1123-4c47-82a0-c8ec75de7e0e. Vzhledem k tomu, že 85d164ba-1123-4c47-82a0-c8ec75de7e0e je hodnota `GenreId` pro technologický Žánr, nadpis stránky s čte "recenze technologie" a seznam s odrážkami vypíše tyto recenze na webu, který spadají do tohoto žánru.

[![stránky žánru technologie](deploying-a-database-vb/_static/image5.jpg)](deploying-a-database-vb/_static/image4.jpg) 

**Obrázek 2**: stránka Žánr technologie ([kliknutím zobrazíte obrázek v plné velikosti](deploying-a-database-vb/_static/image6.jpg))

[![recenze pro učení sami ASP.NET 3,5 za 24 hodin](deploying-a-database-vb/_static/image8.jpg)](deploying-a-database-vb/_static/image7.jpg) 

**Obrázek 3**: recenze pro *učení ASP.NET 3,5 za 24 hodin* ([kliknutím zobrazíte obrázek v plné velikosti](deploying-a-database-vb/_static/image9.jpg))

Webová aplikace recenze obsahuje také oddíl pro správu, ve kterém můžou správci přidávat, upravovat a odstraňovat žánry, recenze a informace o autorech. V současné době má každý návštěvník přístup k části pro správu. V budoucím kurzu přidáváme podporu pro uživatelské účty a na stránkách pro správu se povolují jenom autorizovaní uživatelé.

Pokud si stáhnete aplikaci recenze v knize, nezapomeňte si uvědomit, že její účelem je Ukázat nasazení aplikace řízené daty. Neprojevuje osvědčené postupy, pokud jde o návrh aplikace. Například neexistuje žádná samostatná vrstva přístupu k datům (DAL); stránky ASP.NET komunikují přímo s databází prostřednictvím ovládacího prvku SqlDataSource nebo kódu ADO.NET ve třídách kódu na pozadí. Podrobnější informace o vytváření aplikací založených na datech pomocí vrstvené architektury najdete v tématu moje [ *práce s datovými* kurzy](../../data-access/index.md).

## <a name="databases-on-development-versus-production"></a>Databáze na vývoji versus produkci

Při zahájení vývoje webové aplikace řízené daty je nutné zadat připojovací řetězec databáze, který poskytuje informace o tom, jak se připojit k databázi aplikace. Tento připojovací řetězec Určuje mimo jiné databázový server, název databáze a informace o zabezpečení. Nejčastěji se databáze, kterou aplikace používá během vývoje, liší od databáze použité v produkčním prostředí. Existuje mnoho výhod používání různých databází pro vývoj a produkci. Když máte jinou databázi ve vývoji, znamená to, že si nemusíte dělat obavy o náhodné úpravy nebo odstraňování živých dat. Umožňuje také vkládat fiktivní testovací data nebo provádět změny v datovém modelu, aniž byste se museli starat o účinky na aplikaci v produkčním prostředí. Nevýhodou s jinou databází ve vývojovém a produkčním prostředí je, že když aplikaci nasadíte databázi a všechny relevantní změny schématu databáze nebo dat, musí být nasazeny i.

Před prvním nasazením je k dispozici pouze jedna instance databáze a tato instance je ve vývojovém prostředí. Při prvním nasazení aplikace do produkčního prostředí není nutné kopírovat pouze nezbytné soubory na straně serveru a na straně klienta, ale také zkopírovat databázi z vývojového prostředí do provozního prostředí. Tady teď máme hned s webovou aplikací recenze knih. databáze se nachází ve složce `App_Data` ve vývojovém prostředí, ale ještě nebyla vložená do provozního prostředí.

Po nasazení aplikace jsou k dispozici dvě kopie databáze. Vzhledem k tomu, že je aplikace vyspělá, mohou být přidány nové funkce, které vyžadují změnu v datovém modelu (například přidávání nových sloupců do existujících tabulek, provádění změn ve stávajících sloupcích, přidávání nových tabulek atd.). Po nasazení webové aplikace se změny použité v databázi ve vývojovém prostředí od posledního nasazení musí použít na provozní databázi. Některé strategie správy tohoto procesu jsou popsány v budoucím kurzu. Tento kurz se zaměřuje na nasazení celé databáze z vývojového prostředí do produkčního prostředí.

## <a name="deploying-the-database-to-the-production-environment"></a>Nasazení databáze do provozního prostředí

Zbývající část tohoto kurzu se zabývá tím, jak nasadit databázi z vývojového prostředí do provozního prostředí. Pokud potřebujete, ujistěte se, že váš účet s vaším poskytovatelem webového hostitele zahrnuje Microsoft SQL Server podporu databáze. Také budete muset mít nějaké informace, konkrétně název databázového serveru, název databáze a uživatelské jméno a heslo použité pro připojení k databázi.

Jak bylo popsáno dříve v tomto kurzu, aplikace recenze webu zkontroluje, že databáze web s SQL Server 2008 Express je uložená ve `App_Data` složce. Důvodem by bylo, že nasazení takové databáze by bylo jednoduché jako kopírování `App_Data` složky z vývojového prostředí do provozního prostředí. Většina poskytovatelů webových hostitelů ale v důsledku bezpečnostních důvodů nepodporuje hostování databází ve složce `App_Data`. Místo toho webové hostitele poskytují účet na SQL Server databázový server v rámci svého prostředí. Nasazení databáze z vývojového prostředí do provozního prostředí vyžaduje, aby byla vaše databáze zaregistrovaná na databázovém serveru webového hostitele s.

Jak tedy získáte databázi z vývojového prostředí do provozního prostředí? To lze provést několika způsoby v závislosti na tom, jaké služby webový hostitel nabízí. U některých hostitelů, jako je například DiscountASP.NET, můžete FTP zálohovat databázi nebo vlastní soubor `.mdf` na svůj web a potom v Ovládacích panelech obnovit záložní soubor nebo připojit soubor `.mdf` k SQL Server databázovému serveru. Díky tomu, že tyto nástroje nasazují databázi, jsou stejně jednoduché jako kopírování složky `App_Data` do provozního prostředí a její připojení prostřednictvím ovládacích panelů. To je pravděpodobně nejjednodušší a nejrychlejší způsob, jak databázi poprvé publikovat.

Dalším postupem je použití Průvodce publikováním databáze. Průvodce publikováním databáze je desktopová aplikace pro Windows, která vygeneruje příkazy SQL pro vytvoření schématu databáze s, tabulek, uložených procedur, zobrazení, uživatelsky definovaných funkcí a tak dále, a volitelně i dat ve svých tabulkách. Pak se můžete připojit k databázovému serveru poskytovatele webového hostitele s prostřednictvím SQL Server Management Studio a potom tento skript spustit pro duplikaci databáze v produkčním prostředí. Ještě lepší, pokud váš poskytovatel webového hostitele podporuje [služby publikování databáze](http://www.codeplex.com/sqlhost/Wiki/View.aspx?title=Database%20Publishing%20Services&amp;referringTitle=Home) Microsoft s, můžete mít skript vygenerovaný průvodcem publikováním databáze automaticky spuštěný na databázovém serveru vaším jménem. Vzhledem k tomu, že Průvodce publikováním databáze vygeneruje skript, který vytvoří schéma databáze a data, bude fungovat bez ohledu na to, jestli váš poskytovatel webového hostitele nabízí funkce, jako je připojení nahraného `.mdf` souboru.

### <a name="generating-the-sql-commands-to-create-the-database-schema-and-data-using-the-database-publishing-wizard"></a>Generování příkazů SQL pro vytvoření schématu databáze a dat pomocí Průvodce publikováním databáze

Pojďme pomocí Průvodce publikováním databáze nasadit knihu recenze databáze do produkčního prostředí. Pokud používáte Visual Studio 2008 nebo novější, Průvodce publikováním databáze je již nainstalován. Pokud používáte Visual Studio 2005, budete muset nejdřív [Stáhnout a nainstalovat](https://www.microsoft.com/downloads/details.aspx?familyid=56E5B1C5-BF17-42E0-A410-371A838E570A&amp;displaylang=en) průvodce.

Otevřete Visual Studio a přejděte do databáze `Reviews.mdf`. Pokud používáte aplikaci Visual Web Developer, přečtěte si v Průzkumníkovi databáze. Pokud používáte aplikaci Visual Studio, použijte Průzkumník serveru. Obrázek 4 ukazuje databázi `Reviews.mdf` v Průzkumníku databáze v aplikaci Visual Web Developer. Jak ukazuje obrázek 4, `Reviews.mdf` databáze se skládá ze čtyř tabulek, tří uložených procedur a uživatelsky definované funkce.

[![vyhledejte databázi v Průzkumníku databáze nebo Průzkumník serveru](deploying-a-database-vb/_static/image11.jpg)](deploying-a-database-vb/_static/image10.jpg) 

**Obrázek 4**: vyhledejte databázi v Průzkumníku databáze nebo Průzkumník serveru ([kliknutím zobrazíte obrázek v plné velikosti](deploying-a-database-vb/_static/image12.jpg)).

Klikněte pravým tlačítkem na název databáze a v místní nabídce vyberte možnost publikovat do poskytovatele. Tím se spustí Průvodce publikováním databáze (viz obrázek 5). Kliknutím na tlačítko Další přejdete na úvodní obrazovku.

[![úvodní obrazovku průvodce publikováním databáze](deploying-a-database-vb/_static/image14.jpg)](deploying-a-database-vb/_static/image13.jpg) 

**Obrázek 5**: Úvodní obrazovka Průvodce publikováním databáze ([kliknutím zobrazíte obrázek v plné velikosti](deploying-a-database-vb/_static/image15.jpg))

Druhá obrazovka v průvodci uvádí databáze dostupné pro Průvodce publikováním databáze a umožňuje zvolit, zda se má skriptovat všechny objekty ve vybrané databázi nebo vybrat objekty, které se mají skriptovat. Vyberte příslušnou databázi a ponechte zaškrtnuté políčko "skripty všechny objekty v vybrané databázi".

> [!NOTE]
> Pokud se zobrazí chyba " *v databázi databáze pro typy* , které jsou v tomto průvodci, nejsou žádné žádné objekty". "při kliknutí na tlačítko Další na obrazovce zobrazené na obrázku 6 se ujistěte, že cesta k souboru databáze není delší dobu. Jak je uvedeno v [této položce diskuze](http://www.codeplex.com/sqlhost/Thread/View.aspx?ThreadId=11014) na stránce projektu průvodce publikováním databáze, k této chybě může dojít, pokud je cesta k souboru databáze moc dlouhá.

[![úvodní obrazovku průvodce publikováním databáze](deploying-a-database-vb/_static/image17.jpg)](deploying-a-database-vb/_static/image16.jpg) 

**Obrázek 6**: Úvodní obrazovka Průvodce publikováním databáze ([kliknutím zobrazíte obrázek v plné velikosti](deploying-a-database-vb/_static/image18.jpg))

Na další obrazovce můžete vygenerovat soubor skriptu, nebo pokud ho webový hostitel podporuje, publikujte databázi přímo na databázovém serveru poskytovatele webového hostitele. Jak ukazuje obrázek 7, mám skript napsaný do souboru `C:\REVIEWS.MDF.sql`.

[![skriptovat databázi do souboru nebo ji publikovat přímo pro poskytovatele webového hostitele](deploying-a-database-vb/_static/image20.jpg)](deploying-a-database-vb/_static/image19.jpg) 

**Obrázek 7**: Vytvoření skriptu databáze do souboru nebo jeho publikování přímo na poskytovatele webového hostitele ([kliknutím zobrazíte obrázek v plné velikosti](deploying-a-database-vb/_static/image21.jpg))

Na následující obrazovce se zobrazí výzva k zadání celé řady možností skriptování. Můžete určit, zda má skript obsahovat příkazy drop pro odebrání těchto existujících objektů. Výchozí hodnota je true, což je při prvním nasazení databáze velmi přesné. Můžete také určit, zda je cílová databáze SQL Server 2000, SQL Server 2005 nebo SQL Server 2008. Nakonec můžete určit, jestli se má skriptovat schéma a data, jenom data, nebo jenom schéma. Schéma je kolekce databázových objektů, tabulek, uložených procedur, zobrazení a tak dále. Data jsou informace nacházející se v tabulkách.

Jak ukazuje obrázek 8, mám průvodce nakonfigurovaný tak, aby vynechal existující databázové objekty, aby vygeneroval skript pro databázi SQL Server 2008 a publikoval jak schéma, tak data.

[![zadat možnosti publikování](deploying-a-database-vb/_static/image23.jpg)](deploying-a-database-vb/_static/image22.jpg) 

**Obrázek 8**: zadání možností publikování ([kliknutím zobrazíte obrázek v plné velikosti](deploying-a-database-vb/_static/image24.jpg))

Poslední dvě obrazovky shrnují akce, které se mají provést, a pak zobrazí stav skriptování. Čistým výsledkem spuštění Průvodce je, že máme soubor skriptu, který obsahuje příkazy SQL potřebné k vytvoření databáze v produkčním prostředí a naplnit je stejnými daty jako při vývoji.

### <a name="executing-the-sql-commands-on-the-production-environment-database"></a>Spuštění příkazů SQL v databázi produkčního prostředí

Teď, když máme skript, který obsahuje příkazy SQL pro vytvoření databáze a její data, která zůstávají, je spuštění skriptu v provozní databázi. Někteří poskytovatelé webového hostitele nabízejí textové pole v Ovládacích panelech, kde můžete zadat příkazy SQL, které mají být provedeny v databázi. Pokud máte velmi velký soubor skriptu, tato možnost nemusí fungovat (`REVIEWS.MDF.sql` soubor skriptu má velikost větší než 425 KB).

Lepším řešením je připojit se přímo k provoznímu databázovému serveru pomocí SQL Server Management Studio (SSMS). Pokud máte v počítači nainstalovanou needici SQL Server, pravděpodobně už máte nainstalovanou verzi SSMS. V opačném případě si můžete [Stáhnout a nainstalovat](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en) bezplatnou kopii SQL Server Management Studio Express Edition.

Spusťte SSMS a připojte se k databázovému serveru webového hostitele s pomocí informací poskytnutých vaším poskytovatelem webového hostitele.

[![se připojit k serveru databáze poskytovatele webového hostitele s](deploying-a-database-vb/_static/image26.jpg)](deploying-a-database-vb/_static/image25.jpg) 

**Obrázek 9**: připojení k databázovému serveru poskytovatele webového hostitele s ([kliknutím zobrazíte obrázek v plné velikosti](deploying-a-database-vb/_static/image27.jpg))

Rozbalte kartu databáze a vyhledejte svou databázi. Klikněte na tlačítko Nový dotaz v levém horním rohu panelu nástrojů, vložte příkazy SQL ze souboru skriptu vytvořeného průvodcem publikováním databáze a kliknutím na tlačítko Spustit spusťte tyto příkazy na provozním databázovém serveru. Pokud je soubor skriptu obzvláště velký, může několik minut trvat, než se příkazy spustí.

[![se připojit k serveru databáze poskytovatele webového hostitele s](deploying-a-database-vb/_static/image29.jpg)](deploying-a-database-vb/_static/image28.jpg) 

**Obrázek 10**: připojení k databázovému serveru poskytovatele webového hostitele s ([kliknutím zobrazíte obrázek v plné velikosti](deploying-a-database-vb/_static/image30.jpg))

To všechno je! V tomto okamžiku je vývojová databáze duplikována do produkčního prostředí. Pokud aktualizujete databázi v SSMS, měli byste vidět nové databázové objekty. Obrázek 11 znázorňuje provozní databáze s tabulkami, uložené procedury a uživatelsky definované funkce, které zrcadlí na vývojové databázi. A vzhledem k tomu, že Průvodce publikováním databáze vydal pokyn k publikování dat, tabulky provozní databáze s mají stejná data jako tabulky vývojových databází v době, kdy byl průvodce spuštěn. Obrázek 12 zobrazuje data v tabulce `Books` v provozní databázi.

[![databázových objektů byly duplikovány do provozní databáze.](deploying-a-database-vb/_static/image32.jpg)](deploying-a-database-vb/_static/image31.jpg) 

**Obrázek 11**: objekty databáze byly duplikovány do provozní databáze ([kliknutím zobrazíte obrázek v plné velikosti).](deploying-a-database-vb/_static/image33.jpg)

[![provozní databáze obsahuje stejná data jako na vývojové databázi.](deploying-a-database-vb/_static/image35.jpg)](deploying-a-database-vb/_static/image34.jpg) 

**Obrázek 12**: provozní databáze obsahuje stejná data jako na vývojové databázi ([kliknutím zobrazíte obrázek v plné velikosti).](deploying-a-database-vb/_static/image36.jpg)

V tuto chvíli jsme nasadili pouze vývojovou databázi do produkčního prostředí. Ještě jsme se nepodívali na nasazení samotné webové aplikace ani nezkoumali, jaké změny konfigurace jsou potřeba k tomu, aby aplikace v produkčním prostředí používala provozní databázi. Tyto problémy pokryjeme v dalším kurzu.

## <a name="summary"></a>Přehled

Nasazení webové aplikace řízené daty vyžaduje kopírování databáze používané během vývoje do provozního prostředí. Mnoho poskytovatelů webových hostitelů nabízí nástroje, které zjednodušují proces nasazení databáze. Například pomocí DiscountASP.NET můžete FTP soubor databáze `.mdf` (nebo zálohu) a pak připojit databázi k databázovému serveru z ovládacích panelů. Další možnost, která funguje bez ohledu na to, jaké funkce váš poskytovatel webového hostitele nabízí, je nástroj Průvodce publikováním databáze od Microsoftu, který generuje skript příkazů SQL pro vytvoření schématu a dat vývojových databází. Po vygenerování tohoto skriptu ho můžete spustit v provozní databázi.

Teď, když je v knize v produkčním prostředí recenze databáze webové aplikace, můžeme aplikaci nasadit. Konfigurační informace webové aplikace s však určují připojovací řetězec k databázi a tento připojovací řetězec odkazuje na vývojovou databázi. Při nasazování lokality do produkčního prostředí musíme tyto informace o připojovacím řetězci aktualizovat. V dalším kurzu se dozvíte o těchto rozdílech v konfiguraci a provedou kroky potřebné k publikování knihy řízené daty do produkčního prostředí.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Stažení průvodce publikováním databáze Microsoft SQL Server 1,1](https://www.microsoft.com/downloads/details.aspx?familyid=56E5B1C5-BF17-42E0-A410-371A838E570A&amp;displaylang=en)
- [Stáhnout edici Microsoft SQL Server Management Studio Express](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)

> [!div class="step-by-step"]
> [Předchozí](core-differences-between-iis-and-the-asp-net-development-server-vb.md)
> [Další](configuring-the-production-web-application-to-use-the-production-database-vb.md)
