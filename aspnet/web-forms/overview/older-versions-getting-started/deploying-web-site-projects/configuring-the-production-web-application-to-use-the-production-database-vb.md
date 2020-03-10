---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-the-production-web-application-to-use-the-production-database-vb
title: Konfigurace produkční webové aplikace pro použití provozní databáze (VB) | Microsoft Docs
author: rick-anderson
description: Jak je popsáno v předchozích kurzech, není neobvyklé, aby se konfigurační informace lišily mezi vývojovým a produkčním prostředím. Toto je ES...
ms.author: riande
ms.date: 04/23/2009
ms.assetid: a64a7aa0-6608-449e-83bf-1ef8cceee504
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-the-production-web-application-to-use-the-production-database-vb
msc.type: authoredcontent
ms.openlocfilehash: 7fe4f545a76992ad687827af447d9a9e95bea73f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78636225"
---
# <a name="configuring-the-production-web-application-to-use-the-production-database-vb"></a>Konfigurace produkční webové aplikace pro použití produkční databáze (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_08_VB.zip) nebo [stažení PDF](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial08_DBConfig_vb.pdf)

> Jak je popsáno v předchozích kurzech, není neobvyklé, aby se konfigurační informace lišily mezi vývojovým a produkčním prostředím. To platí zejména pro webové aplikace řízené daty, protože databázové připojovací řetězce se mezi vývojovým a produkčním prostředím liší. V tomto kurzu se seznámíte s možnostmi konfigurace produkčního prostředí tak, aby obsahovalo příslušný připojovací řetězec podrobněji.

## <a name="introduction"></a>Úvod

Datově řízené webové aplikace obvykle používají jinou databázi při vývoji, než je v produkčním prostředí. V případě aplikací hostovaných poskytovatelem webového hostitele a v místním prostředí se vývojová databáze obvykle nachází v počítači s vývojářem s a provozní databáze je hostována na databázovém serveru v zařízení společnosti pro hostování webu. Nasazení webové aplikace řízené daty zahrnuje kopírování vývojové databáze na provozní server databáze. V předchozím kurzu jsme se podívali na způsoby, jak tento krok provést.

Webová aplikace používá informace v *připojovacím řetězci* k navázání spojení s databází. Připojovací řetězec, který je obvykle uložen v `Web.config`, určuje název databázového serveru, název databáze, kontext zabezpečení a další informace. Vzhledem k tomu, že databáze používaná webovou aplikací závisí na tom, jestli je webová aplikace spuštěná ve vývojovém nebo produkčním prostředí, připojovací řetězce se musí mezi těmito dvěma prostředími lišit.

Informace o konfiguraci se mezi vývojovým a produkčním prostředím neobvykle liší. *Běžné rozdíly v konfiguraci mezi výukovým a produkčním* kurzem popisuje techniky pro udržování oddělených konfiguračních informací mezi těmito dvěma prostředími a také stručnou diskusi o připojovacích řetězcích databáze. V tomto kurzu se seznámíte s možnostmi konfigurace produkčního prostředí tak, aby obsahovalo příslušný připojovací řetězec podrobněji.

## <a name="examining-the-connection-string-information"></a>Prozkoumání informací o připojovacím řetězci

Připojovací řetězec používaný v knize recenze webové aplikace je uložený v konfiguračním souboru aplikace s `Web.config`. `Web.config` obsahuje speciální část pro ukládání připojovacích řetězců, aptly s názvem [&lt;connectionstrings&gt;](https://msdn.microsoft.com/library/bf7sd233.aspx). Soubor `Web.config` pro web recenze knih má v této části definovaný jeden připojovací řetězec s názvem `ReviewsConnectionString`:

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample1.xml)]

Připojovací řetězec – zdroj dat = .\SQLEXPRESS; AttachDbFilename = | DataDirectory | \Reviews.mdf; Integrated Security = true; User Instance = true – se skládá z řady možností a hodnot s páry možnosti/hodnota oddělenými středníkem a každou možností a hodnotou oddělenou rovnítkem. V tomto připojovacím řetězci se používají čtyři možnosti:

- `Data Source` – určuje umístění databázového serveru a název instance databázového serveru (pokud existuje). Hodnota, `.\SQLEXPRESS`, je příkladem, kdy je k dispozici databázový server a název instance. Doba určuje, že databázový server je ve stejném počítači jako aplikace. název instance je `SQLEXPRESS`.
- `AttachDbFilename` – určuje umístění databázového souboru. Hodnota obsahuje zástupný `|DataDirectory|`, který se přeloží na úplnou cestu složky `App_Data` aplikace za běhu.
- `Integrated Security` – logická hodnota, která označuje, jestli se má při připojování k databázi použít zadané uživatelské jméno nebo heslo, nebo přihlašovací údaje aktuálního účtu systému Windows (true).
- `User Instance` – možnost konfigurace specifická pro edice SQL Server Express, která označuje, jestli se mají v místním počítači připojovat a připojovat k databázi SQL Server Express edice, které se nepoužívají pro správu. Další informace o tomto nastavení najdete v tématu [SQL Server Express uživatelské instance](https://msdn.microsoft.com/library/ms254504.aspx) .

Možnosti povolujících připojovacích řetězců závisí na databázi, ke které se připojujete, a na použitém poskytovateli databáze [ADO.NET](http://ADO.NET) . Například připojovací řetězec pro připojení k databázi Microsoft SQL Server se liší od serveru používaného pro připojení k databázi Oracle. Podobně připojení k Microsoft SQL Server databázi pomocí poskytovatele SqlClient používá jiný připojovací řetězec než při použití zprostředkovatele OLE DB.

Připojovací řetězec databáze můžete vytvořit ručně s použitím webu, jako je [connectionStrings.com](http://www.connectionstrings.com/) jako prostředku, pro jaké možnosti jsou k dispozici. Jednodušším přístupem je však přidání databáze do Průzkumník serveru v aplikaci Visual Studio a následné připojení řetězce z okno Vlastnosti. Tuto techniku použijte k sestavování připojovacího řetězce k provoznímu databázovému serveru.

Otevřete Visual Studio a potom přejděte do okna Průzkumník serveru (ve Visual Web Developer se toto okno nazývá Průzkumník databáze). Klikněte pravým tlačítkem na možnost datová připojení a v místní nabídce vyberte možnost Přidat připojení. Tím se zobrazí Průvodce na obrázku 1. Vyberte příslušný zdroj dat a klikněte na pokračovat.

[![vyberte, chcete-li přidat novou databázi do Průzkumník serveru](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image2.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image1.jpg) 

**Obrázek 1**: vyberte možnost Přidat novou databázi do Průzkumník serveru ([kliknutím zobrazíte obrázek v plné velikosti).](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image3.jpg)

Dále zadejte různé informace o připojení databáze (viz obrázek 2). Pokud jste se zaregistrovali ve vaší společnosti pro hostování webů, měli byste poskytnout informace o tom, jak se připojit k databázi – název databázového serveru, název databáze, uživatelské jméno a heslo, které se mají použít k připojení k databázi a tak dále. Po zadání těchto informací kliknutím na tlačítko OK dokončete tohoto průvodce a přidejte databázi do Průzkumník serveru.

[![zadat informace o připojení databáze](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image5.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image4.jpg) 

**Obrázek 2**: zadání informací o připojení k databázi ([kliknutím zobrazíte obrázek v plné velikosti](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image6.jpg))

Databáze produkčního prostředí by teď měla být uvedená v Průzkumník serveru. Vyberte databázi z Průzkumník serveru a přejít na okno Vlastnosti. V této části najdete vlastnost s názvem připojovací řetězec s připojovacím řetězcem databáze s. Za předpokladu, že používáte databázi Microsoft SQL Server v produkčním prostředí a poskytovatel SqlClient by měl váš připojovací řetězec vypadat podobně jako v následujícím příkladu:

<strong>Zdroj dat =<em>servername</em>; Počáteční katalog =<em>DatabaseName</em>; Zachovat informace o zabezpečení = pravda; ID uživatele =<em>uživatelské jméno</em>; Heslo =*heslo</strong>*

Kde *servername*, *DatabaseName*, *username*a *Password* jsou hodnoty pro název databázového serveru, název databáze a uživatelské jméno a heslo, které jste zadali vaší webovou hostitelskou společností.

## <a name="deploying-the-book-reviews-web-application"></a>Nasazení webové aplikace recenze knih

Předchozí kurz se věnuje kopírování vývojové databáze do produkčního prostředí, ale nezkoumala jsme nasazení aplikace řízené daty. V tomto okamžiku provozní prostředí obsahuje databázi, ale používá verzi recenze aplikace se statickými recenzemi. Musíme na provozní server nasadit novou aplikaci založenou na datech a aktualizované informace o konfiguraci.

Nasaďte aplikaci řízenou daty z vývojového prostředí do produkčního prostředí, chvíli počkejte. Tento proces se podrobněji pokryl v předchozích kurzech. Pokud potřebujete aktualizační program, přečtěte si téma *nasazení webu pomocí klienta FTP* nebo *nasazení webu pomocí kurzů sady Visual Studio* . Je potřeba zajistit, aby byl připojovací řetězec produkční databáze ten, který se používá v produkčním prostředí, což znamená, že musí být nasazený alternativní `Web.config` soubor. Konkrétně tento změněný `Web.config` prvek `<connectionStrings>` souboru musí obsahovat připojovací řetězec produkční databáze a měl by vypadat nějak takto:

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample2.xml)]

Všimněte si, že připojovací řetězec v elementu `<connectionStrings>` se nazývá stejný (`ReviewsConnectionString`), ale nyní obsahuje připojovací řetězec provozní databáze namísto připojovacího řetězce vývojové databáze.

Pokud nemáte podrobnější pracovní postup nasazení, buď ručně upravte soubor `Web.config` tak, aby používal připojovací řetězec provozní databáze předtím, než se nasadí (zapamatuje se zpět na použití připojovacího řetězce pro vývojovou databázi), nebo Udržujte samostatný `Web.config` soubor s informacemi o konfiguraci produkčního prostředí, které se nahrají do provozního prostředí v rámci procesu nasazení.

> [!NOTE]
> Pokud omylem nasadíte `Web.config` soubor, který obsahuje připojovací řetězec pro vývojovou databázi, dojde k chybě, když se aplikace v produkčním prostředí pokusí připojit k databázi. Tato chyba se projevuje jako `SqlException` se zprávou, že server nebyl nalezen nebo nebyl přístupný.

Po nasazení lokality do produkčního prostředí navštivte provozní web prostřednictvím prohlížeče. Měli byste vidět a využívat stejné uživatelské prostředí jako při místním spuštění aplikace řízené daty. Když navštívíte web na produkčním webu, používá ho provozní databázový server, zatímco při návštěvě webu ve vývojovém prostředí se používá databáze ve vývoji. Obrázek 3 ukazuje, jak si na webu v produkčním prostředí *ASP.NET 3,5* na stránce s informacemi o tom, jak se na webu v provozním prostředí (adresa URL v adresním řádku prohlížeče) zobrazuje.

[![aplikace řízená daty je teď k dispozici v produkčním prostředí.](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image8.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image7.jpg) 

**Obrázek 3**: aplikace řízená daty je teď k dispozici v produkčním prostředí. ([Kliknutím zobrazíte obrázek v plné velikosti.](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image9.jpg))

### <a name="storing-connection-strings-in-a-separate-configuration-file"></a>Ukládání připojovacích řetězců do samostatného konfiguračního souboru

Běžnou technikou pro správu oddělených informací o konfiguraci vývojových a produkčních prostředí je mít dvě verze `Web.config`: jeden pro vývojové prostředí a jeden pro produkci. V době nasazení se dá odpovídající verze `Web.config` zkopírovat do produkčního prostředí. V ideálním případě bude tento proces automatizován jako součást pracovního postupu nasazení.

Místo udržování dvou samostatných souborů `Web.config` můžete volitelně zadat i přesnější rozdíly. Prvky, které tvoří soubor `Web.config`, lze definovat v externích konfiguračních souborech, které jsou následně odkazovány v souboru `Web.config`. V kostce můžete mít jeden soubor `Web.config` pro obě prostředí, která odkazují na soubor databaseConnectionStrings. config, který by obsahoval připojovací řetězce používané aplikací a by byl pro každé prostředí jedinečný. Zjistím, že rozdělující různé informace o konfiguraci do samostatných souborů poskytuje tidier a jednodušší soubor `Web.config` a podrobněji popisuje rozdíly v konfiguraci mezi vývojovým a produkčním prostředím.

Chcete-li použít tuto techniku, Začněte vytvořením nové složky ve webové aplikaci s názvem `ConfigSections`. V dalším kroku přidejte do této nové složky s názvem databaseConnectionStrings. dev. config a databaseConnectionStrings. produkční. config dva soubory. Dále zkopírujte prvek `<connectionStrings>` z `Web.config` do souborů databaseConnectionStrings. dev. config a databaseConnectionStrings. produkční. config a pak upravte připojovací řetězec v souboru databaseConnectionStrings. produkčního. config tak, aby určoval připojovací řetězec provozní databáze. Například soubor databaseConnectionStrings. dev. config by měl obsahovat pouze prvek `<connectionStrings>` s připojovacím řetězcem, který odkazuje na vývojovou databázi:

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample3.xml)]

Podobně soubor databaseConnectionStrings. produkčního. config by měl obsahovat pouze prvek `<connectionStrings>`, ale ten, který má připojovací řetězec provozní databáze.

Vytvořte kopii souboru databaseConnectionStrings. dev. config a pojmenujte ho databaseConnectionStrings. config.

> [!NOTE]
> Konfigurační soubor můžete pojmenovat jiným způsobem než databaseConnectionStrings. config, pokud chcete, například `connectionStrings.config` nebo `dbInfo.config`. Nezapomeňte ale pojmenovat soubor s příponou `.config` jako `.config` soubory ve výchozím nastavení nejsou obsluhovány modulem ASP.NET. Pokud zadáte název souboru něco jiného, například `connectionStrings.txt`, uživatel by mohl nasměrovat svůj prohlížeč na [www.yoursite.com/ConfigSettings/connectionStrings.txt](http://www.yoursite.com/ConfigSettings/connectionStrings.txt) a zobrazit obsah souboru.

V tomto okamžiku by měla složka `ConfigSections` obsahovat tři soubory (viz obrázek 4). Soubory databaseConnectionStrings. dev. config a databaseConnectionStrings. produkční. config obsahují připojovací řetězce pro vývojová a produkční prostředí, v uvedeném pořadí. Soubor databaseConnectionStrings. config obsahuje informace připojovacího řetězce, který bude webová aplikace používat za běhu. V důsledku toho by soubor databaseConnectionStrings. config měl být stejný jako soubor databaseConnectionStrings. dev. config ve vývojovém prostředí, zatímco v produkčním souboru databaseConnectionStrings. config by měl být stejný jako databaseConnectionStrings. produkční. config.

[![ConfigSections](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image11.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image10.jpg) 

**Obrázek 4**: ConfigSections ([kliknutím zobrazíte obrázek v plné velikosti](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image12.jpg))

Teď je potřeba dát `Web.config`, aby pro své úložiště připojovacích řetězců používal soubor databaseConnectionStrings. config. Otevřete `Web.config` a nahraďte existující prvek `<connectionStrings>` následujícím způsobem:

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample4.xml)]

Atribut `configSource` určuje fyzickou cestu relativní k souboru `Web.config`. Pokud je soubor externí `.config` ve stejném adresáři jako `Web.config` pak nastavte tento atribut na název souboru `.config` souboru. Pokud je v podadresáři, stejně jako v případě databaseConnectionStrings. config, určete podsložku pomocí zpětného lomítka pro vymezení názvu složky a souboru, jako je ConfigSections\databaseConnectionStrings.config.

V rámci této úpravy obsahují vývojové a produkční prostředí stejný soubor `Web.config`. Teď jediným rozdílem je soubor databaseConnectionStrings. config. Zkopírujte soubor databaseConnectionStrings. produkční. config do produkčního prostředí a přejmenujte ho na databaseConnectionStrings. config. Pokud v budoucnu dojde ke změnám v připojovacím řetězci k produkční databázi, budete je muset udělat v souboru databaseConnectionStrings. produkční. config a pak ho nahrát do produkčního prostředí a přejmenovat ho na databaseConnectionStrings. config.

> [!NOTE]
> Můžete zadat informace pro jakýkoli `Web.config` element v samostatném souboru a použít atribut `configSource` pro odkazování na tento soubor z `Web.config`.

## <a name="summary"></a>Souhrn

Aplikace řízené daty obvykle používají různé databáze ve vývojovém a produkčním prostředí. V důsledku toho musí být připojovací řetězce databáze uložené v konfiguraci webové aplikace jedinečné pro každé prostředí. V tomto kurzu jsme se podívali na to, jak určit připojovací řetězec provozní databáze a jak udržovat jedinečné informace o připojovacím řetězci v obou prostředích.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Připojovací řetězce a konfigurační soubory](https://msdn.microsoft.com/library/ms254494.aspx)
- [Informace o řetězcích konfigurace databáze @ ConnectionStrings.com](http://www.connectionstrings.com/)
- [Přesunout nastavení ze souboru Web. config](http://www.asp101.com/tips/index.asp?id=154)
- [Technická dokumentace pro&gt; element &lt;connectionStrings](https://msdn.microsoft.com/library/bf7sd233.aspx)

> [!div class="step-by-step"]
> [Předchozí](deploying-a-database-vb.md)
> [Další](configuring-a-website-that-uses-application-services-vb.md)
