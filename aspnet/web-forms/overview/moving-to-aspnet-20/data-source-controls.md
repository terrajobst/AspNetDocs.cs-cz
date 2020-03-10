---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: Ovládací prvky zdroje dat | Microsoft Docs
author: microsoft
description: Ovládací prvek DataGrid v ASP.NET 1. x označil Skvělé zlepšení přístupu k datům ve webových aplikacích. Není to ale uživatelsky přívětivé, jak by bylo možné....
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: a2e2cfbec3e5aebf42a2de30bab7d45b4b610298
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639410"
---
# <a name="data-source-controls"></a>Ovládací prvky zdroje dat

od [Microsoftu](https://github.com/microsoft)

> Ovládací prvek DataGrid v ASP.NET 1. x označil Skvělé zlepšení přístupu k datům ve webových aplikacích. Není to ale uživatelsky přívětivé, jak by bylo možné. Stále se vyžaduje značné množství kódu, aby bylo možné získat z něho mnohem užitečnou funkčnost. Jedná se o model všech přístupů k datům budoucna v 1. x.

Ovládací prvek DataGrid v ASP.NET 1. x označil Skvělé zlepšení přístupu k datům ve webových aplikacích. Není to ale uživatelsky přívětivé, jak by bylo možné. Stále se vyžaduje značné množství kódu, aby bylo možné získat z něho mnohem užitečnou funkčnost. Jedná se o model všech přístupů k datům budoucna v 1. x.

ASP.NET 2,0 Tento údaj řeší v rámci ovládacích prvků zdroje dat. Ovládací prvky zdroje dat v ASP.NET 2,0 poskytují vývojářům deklarativní model pro načítání dat, zobrazování dat a upravování dat. Účelem ovládacích prvků zdroje dat je poskytnout konzistentní reprezentace dat pro ovládací prvky vázané na data bez ohledu na zdroj těchto dat. Na srdce ovládacího prvku zdroje dat v ASP.NET 2,0 je abstraktní třída DataSourceControl. Třída DataSourceControl poskytuje základní implementaci rozhraní IDataSource a rozhraní IListSource, což je ten, který umožňuje přiřadit ovládací prvek zdroje dat jako zdroj dat ovládacího prvku vázaného na data (prostřednictvím nové vlastnosti DataSourceId. prodiskutováni později) a vystavte si data v seznamu. Každý seznam dat z ovládacího prvku zdroje dat je vystaven jako objekt DataSourceView. Přístup k instancím DataSourceView zajišťuje rozhraní IDataSource. Například metoda GetViewNames vrací rozhraní ICollection, které umožňuje vytvořit výčet objektů DataSourceView přidružených ke konkrétnímu ovládacímu prvku zdroje dat a metoda GetView umožňuje přístup ke konkrétní instanci třídy DataSourceView podle názvu.

Ovládací prvky zdroje dat nemají žádné uživatelské rozhraní. Jsou implementovány jako serverové ovládací prvky, aby mohly podporovat deklarativní syntaxi a tak, že mají přístup ke stavu stránky, pokud je to požadováno. Ovládací prvky zdroje dat nevykreslují žádné značky HTML klientovi.

> [!NOTE]
> Jak uvidíte později, existují i výhody ukládání do mezipaměti získané pomocí ovládacích prvků zdroje dat.

## <a name="storing-connection-strings"></a>Ukládání připojovacích řetězců

Předtím, než se podíváme na to, jak nakonfigurovat ovládací prvky zdroje dat, doporučujeme pro připojovací řetězce využít novou funkci v ASP.NET 2,0. ASP.NET 2,0 zavádí nový oddíl v konfiguračním souboru, který umožňuje snadno ukládat připojovací řetězce, které se dají dynamicky číst za běhu. Část &lt;connectionStrings&gt; umožňuje snadno ukládat připojovací řetězce.

Následující fragment kódu přidá nový připojovací řetězec.

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> Stejně jako v části &lt;appSettings&gt; se sekce &lt;connectionStrings&gt; zobrazí mimo oddíl &lt;System. Web&gt; konfiguračního souboru.

Chcete-li použít tento připojovací řetězec, můžete použít následující syntaxi při nastavování atributu ConnectionString ovládacího prvku serveru.

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

&gt; oddílu &lt;connectionStrings lze také šifrovat, aby citlivé informace nebyly vystaveny. Tato možnost bude zahrnuta v pozdějším modulu.

## <a name="caching-data-sources"></a>Ukládání zdrojů dat do mezipaměti

Každý DataSourceControl poskytuje čtyři vlastnosti pro konfiguraci ukládání do mezipaměti. EnableCaching, CacheDuration, CacheExpirationPolicy a CacheKeyDependency.

## <a name="enablecaching"></a>EnableCaching

EnableCaching je logická vlastnost, která určuje, zda je povoleno ukládání do mezipaměti pro ovládací prvek zdroje dat.

## <a name="cacheduration-property"></a>Vlastnost CacheDuration

Vlastnost CacheDuration nastaví počet sekund, po které mezipaměť zůstává platná. Nastavení této vlastnosti na **hodnotu 0** způsobí, že mezipaměť zůstane platná, dokud není explicitně zrušena její platnost.

## <a name="cacheexpirationpolicy-property"></a>Vlastnost CacheExpirationPolicy

Vlastnost CacheExpirationPolicy lze nastavit buď jako **absolutní** , nebo jako **posuvnou**. Nastavení na absolutní znamená, že maximální doba, po kterou budou data ukládána do mezipaměti, je počet sekund zadaný vlastností CacheDuration. Nastavením na klouzavé je čas vypršení platnosti obnoven při provedení každé operace.

## <a name="cachekeydependency-property"></a>CacheKeyDependency Property

Pokud je pro vlastnost CacheKeyDependency zadána řetězcová hodnota, ASP.NET nastaví novou závislost mezipaměti založenou na tomto řetězci. To umožňuje explicitně zrušit platnost mezipaměti tím, že jednoduše změníte nebo odeberete CacheKeyDependency.

**Důležité**: Pokud je povolené zosobnění a přístup ke zdroji dat nebo obsahu dat je založený na identitě klienta, doporučuje se ukládání do mezipaměti zakázat nastavením EnableCaching na hodnotu false. Pokud je v tomto scénáři povoleno ukládání do mezipaměti a uživatel jiný než uživatel, který původně požadoval, aby data vystavoval požadavek, autorizace pro zdroj dat není vynutila. Data budou jednoduše obsluhována z mezipaměti.

## <a name="the-sqldatasource-control"></a>Ovládací prvek SqlDataSource

Ovládací prvek SqlDataSource umožňuje vývojáři získat přístup k datům uloženým v libovolné relační databázi, která podporuje ADO.NET. Může použít poskytovatele System. data. SqlClient pro přístup k databázi SQL Server, poskytovateli System. data. OleDb, zprostředkovateli System. data. ODBC nebo poskytovateli System. data. OracleClient pro přístup k Oracle. Proto se třída SqlDataSource nepoužívá jenom pro přístup k datům v databázi SQL Server.

Aby bylo možné použít SqlDataSource, stačí zadat hodnotu vlastnosti ConnectionString a zadat příkaz SQL nebo uloženou proceduru. Ovládací prvek SqlDataSource má za starosti práci s podkladovou architekturou ADO.NET. Otevře připojení, odešle dotaz na zdroj dat nebo spustí uloženou proceduru, vrátí data a pak připojení ukončí.

> [!NOTE]
> Vzhledem k tomu, že třída DataSourceControl automaticky ukončí připojení za vás, měla by snížit počet volání zákazníků vygenerovaných nevracením databázových připojení.

Fragment kódu níže váže ovládací prvek DropDownList k ovládacímu prvku SqlDataSource pomocí připojovacího řetězce, který je uložen v konfiguračním souboru, jak je uvedeno výše.

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

Jak je znázorněno výše, vlastnost DataSourceMode třídy SqlDataSource určuje režim zdroje dat. V předchozím příkladu je vlastnost DataSourceMode nastavena na hodnotu DataSourceMode. V takovém případě třída SqlDataSource vrátí objekt rozhraní IDataReader pomocí kurzoru určeného pouze pro čtení. Zadaný typ objektu, který je vrácen, je řízen poskytovatelem, který je použit. V tomto případě používáme poskytovatele System. data. SqlClient, jak je uvedeno v části &lt;connectionStrings&gt; souboru Web. config. Proto vrácený objekt bude typu SqlDataReader. Zadáním hodnoty DataSourceMode datové sady můžete data uložit do datové sady na serveru. Tento režim umožňuje přidat funkce, jako je například řazení, stránkování atd. Pokud mám datovou vazbu třídy SqlDataSource k ovládacímu prvku GridView, chtěl jsem si zvolit režim DataSet. V případě ovládacího prvkem DropDownList je však režim DataReader správnou volbou.

> [!NOTE]
> Při ukládání do mezipaměti třídy SqlDataSource nebo prvku AccessDataSource musí být vlastnost DataSourceMode nastavena na hodnotu DataSet. K výjimce dojde v případě, že povolíte ukládání do mezipaměti s datasourcemodí objektu DataSourceMode.

## <a name="sqldatasource-properties"></a>Vlastnosti SqlDataSource

Níže jsou uvedeny některé vlastnosti ovládacího prvku SqlDataSource.

### <a name="cancelselectonnullparameter"></a>CancelSelectOnNullParameter

Logická hodnota určující, zda je příkaz SELECT zrušen, pokud jeden z parametrů má hodnotu null. Ve výchozím nastavení true.

### <a name="conflictdetection"></a>ConflictDetection

V situaci, kdy více uživatelů může aktualizovat zdroj dat ve stejnou dobu, vlastnost ConflictDetection určuje chování ovládacího prvku SqlDataSource. Tato vlastnost je vyhodnocena jako jedna z hodnot výčtu ConflictOptions. Tyto hodnoty jsou **CompareAllValues** a **hodnotu OverwriteChanges**. Pokud je nastavená na hodnotu OverwriteChanges, poslední osoba, která zapíše data do zdroje dat, přepíše všechny předchozí změny. Pokud je však vlastnost ConflictDetection nastavena na hodnotu CompareAllValues, jsou vytvořeny také parametry pro sloupce vrácené vlastností SelectCommand a Parameters pro uložení původních hodnot v každém z těchto sloupců, které umožňují třídě SqlDataSource zobrazit Určete, zda se hodnoty od spuštění vlastnosti SelectCommand změnily.

### <a name="deletecommand"></a>Vlastnost

Nastaví nebo získá řetězec SQL, který se použije při odstraňování řádků z databáze. Může to být buď dotaz SQL, nebo název uložené procedury.

### <a name="deletecommandtype"></a>DeleteCommandType

Nastaví nebo získá typ příkazu DELETE, buď dotaz SQL (text), nebo uloženou proceduru (StoredProcedure).

### <a name="deleteparameters"></a>DeleteParameters

Vrátí parametry, které jsou používány pomocí události DeleteCommand objektu SqlDataSourceView přidruženého k ovládacímu prvku SqlDataSource.

### <a name="oldvaluesparameterformatstring"></a>OldValuesParameterFormatString

Tato vlastnost slouží k určení formátu původních parametrů hodnot v případech, kdy je vlastnost ConflictDetection nastavena na hodnotu CompareAllValues. Výchozí hodnota je {0} to znamená, že parametry původních hodnot budou mít stejný název jako původní parametr. Jinými slovy, pokud je název pole EmployeeID, původní parametr hodnoty by byl @EmployeeID.

### <a name="selectcommand"></a>SelectCommand

Nastaví nebo získá řetězec SQL, který se používá k načtení dat z databáze. Může to být buď dotaz SQL, nebo název uložené procedury.

### <a name="selectcommandtype"></a>SelectCommandType

Nastaví nebo získá typ příkazu SELECT, buď dotaz SQL (text), nebo uloženou proceduru (StoredProcedure).

### <a name="selectparameters"></a>SelectParameters

Vrátí parametry, které jsou používány pomocí vlastnosti SelectCommand objektu SqlDataSourceView přidruženého k ovládacímu prvku SqlDataSource.

### <a name="sortparametername"></a>SortParameterName

Získá nebo nastaví název parametru uložené procedury, který se používá při řazení dat načtených pomocí ovládacího prvku zdroje dat. Platí pouze v případě, že je SelectCommandType nastaveno na StoredProcedure.

### <a name="sqlcachedependency"></a>SqlCacheDependency

Středníkem oddělený řetězec určující databáze a tabulky používané v závislosti na SQL Server cache. (Závislosti mezipaměti SQL budou popsány v pozdějším modulu.)

### <a name="updatecommand"></a>Událost

Nastaví nebo získá řetězec SQL, který se používá při aktualizaci dat v databázi. Může to být buď dotaz SQL, nebo název uložené procedury.

### <a name="updatecommandtype"></a>UpdateCommandType

Nastaví nebo získá typ příkazu Update, buď dotaz SQL (text), nebo uloženou proceduru (StoredProcedure).

### <a name="updateparameters"></a>UpdateParameters

Vrátí parametry, které jsou používány událostmi UpdateCommand objektu SqlDataSourceView přidruženého k ovládacímu prvku SqlDataSource.

## <a name="the-accessdatasource-control"></a>Ovládací prvek AccessDataSource

Ovládací prvek AccessDataSource je odvozen z třídy SqlDataSource a je použit pro datovou vazby k databázi aplikace Microsoft Access. Vlastnost ConnectionString ovládacího prvku AccessDataSource je vlastnost jen pro čtení. Místo použití vlastnosti ConnectionString se vlastnost DataFile používá k odkazování na databázi Access, jak je znázorněno níže.

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

AccessDataSource vždy nastaví ProviderName (ProviderName) základní třídy SqlDataSource na System. data. OleDb a připojí se k databázi pomocí poskytovatele OLE DB Microsoft. Jet. OLEDB. 4.0. Ovládací prvek AccessDataSource nelze použít pro připojení k databázi s přístupem chráněným heslem. Pokud je nutné se připojit k databázi chráněné heslem, měli byste použít ovládací prvek SqlDataSource.

> [!NOTE]
> Přístup k databázím uloženým v rámci webu by měl být umístěn v adresáři App\_data. ASP.NET nepovoluje procházení souborů v tomto adresáři. Při použití databází Access bude třeba udělit účtu procesu oprávnění ke čtení a zápisu do aplikace\_datový adresář.

## <a name="the-xmldatasource-control"></a>Ovládací prvek XmlDataSource

Prvek XmlDataSource se používá k vázání dat XML do ovládacích prvků vázaných na data. Můžete vytvořit propojení se souborem XML pomocí vlastnosti DataFile nebo můžete vytvořit propojení s řetězcem XML pomocí vlastnosti data. XmlDataSource zpřístupňuje atributy XML jako pole s možností vazby. V případech, kdy potřebujete vytvořit vazby na hodnoty, které nejsou reprezentované jako atributy, budete muset použít transformaci XSL. Můžete také použít výrazy XPath k filtrování dat XML.

Vezměte v úvahu následující soubor XML:

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

Všimněte si, že XmlDataSource používá vlastnost XPath *persons/person* k filtrování pouze těch&gt; uzlů &lt;osoba. Vlastnost DropDownList potom vytvoří vázání dat k atributu LastName pomocí vlastnosti DataTextField.

I když je ovládací prvek XmlDataSource primárně použit pro datovou vazby k datům XML jen pro čtení, je možné upravit datový soubor XML. Všimněte si, že v takových případech automatické vkládání, aktualizace a odstraňování informací v souboru XML neprobíhá automaticky stejně jako jiné ovládací prvky zdroje dat. Místo toho budete muset napsat kód pro ruční úpravu dat pomocí následujících metod ovládacího prvku XmlDataSource.

### <a name="getxmldocument"></a>GetXmlDocument

Načte objekt XmlDocument obsahující kód XML, který získá XmlDataSource.

### <a name="save"></a>Uložení

Uloží z paměti XmlDocument zpátky do zdroje dat.

Je důležité si uvědomit, že metoda Save bude fungovat jenom v případě, že jsou splněné tyto dvě podmínky:

1. XmlDataSource používá vlastnost DataFile pro svázání se souborem XML namísto vlastnosti data pro svázání s daty XML v paměti.
2. Pomocí vlastnosti Transform nebo TransformFile není určena žádná transformace.

Všimněte si také, že metoda Save může vracet neočekávané výsledky při volání více uživatelů současně.

## <a name="the-objectdatasource-control"></a>Ovládací prvek ObjectDataSource

Ovládací prvky zdroje dat, které jsme pokryli do tohoto bodu, jsou vynikajícími volbami pro dvě vícevrstvé aplikace, kde ovládací prvek zdroje dat komunikuje přímo s úložištěm dat. Mnohé z reálných aplikací však jsou vícevrstvé aplikace, ve kterých může být potřeba, aby ovládací prvek zdroje dat komunikoval s podnikovým objektem, který zase komunikuje s datovou vrstvou. V těchto situacích prvek ObjectDataSource vyplní vyúčtování jako nejúhledné. Prvek ObjectDataSource pracuje ve spojení se zdrojovým objektem. Ovládací prvek ObjectDataSource vytvoří instanci zdrojového objektu, volá zadanou metodu a odstraní instanci objektu All v rámci jednoho požadavku, pokud objekt obsahuje metody instance místo statických metod (sdílené v Visual Basic). Proto musí být objekt bezstavový. To znamená, že váš objekt by měl získat a uvolnit všechny požadované prostředky v rozsahu jediné žádosti. Způsob vytvoření zdrojového objektu lze řídit zpracováním události ObjectCreating ovládacího prvku ObjectDataSource. Můžete vytvořit instanci zdrojového objektu a potom nastavit vlastnost ObjectInstance třídy ObjectDataSourceEventArgs na tuto instanci. Ovládací prvek ObjectDataSource použije instanci, která je vytvořena v události ObjectCreating místo vytvoření vlastní instance.

Pokud zdrojový objekt ovládacího prvku ObjectDataSource zveřejňuje veřejné statické metody (sdílené v Visual Basic), které lze volat pro načtení a úpravu dat, ovládací prvek ObjectDataSource bude volat tyto metody přímo. Pokud ovládací prvek ObjectDataSource musí vytvořit instanci zdrojového objektu, aby bylo možné provést volání metody, objekt musí obsahovat veřejný konstruktor, který nepřijímá žádné parametry. Ovládací prvek ObjectDataSource vyvolá tento konstruktor při vytvoření nové instance zdrojového objektu.

Pokud zdrojový objekt neobsahuje veřejný konstruktor bez parametrů, můžete vytvořit instanci zdrojového objektu, který bude použit ovládacím prvkem ObjectDataSource v události ObjectCreating.

## <a name="specifying-object-methods"></a>Určení metod objektu

Zdrojový objekt ovládacího prvku ObjectDataSource může obsahovat libovolný počet metod, které se používají k výběru, vložení, aktualizaci nebo odstranění dat. Tyto metody jsou volány ovládacím prvkem ObjectDataSource na základě názvu metody, jak je určeno pomocí vlastnosti SelectMethod, určena metoda InsertMethod, UpdateMethod nebo DeleteMethod ovládacího prvku ObjectDataSource. Zdrojový objekt může také zahrnovat volitelnou metodu SelectCount, která je identifikována ovládacím prvkem ObjectDataSource pomocí vlastnosti SelectCountMethod, která vrací počet celkového počtu objektů ve zdroji dat. Ovládací prvek ObjectDataSource zavolá metodu SelectCount poté, co byla volána metoda Select, aby získala celkový počet záznamů ve zdroji dat pro použití při stránkování.

## <a name="lab-using-data-source-controls"></a>Testovací prostředí využívající ovládací prvky zdroje dat

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a>Cvičení 1 – zobrazení dat pomocí ovládacího prvku SqlDataSource

Následující cvičení používá ovládací prvek SqlDataSource pro připojení k databázi Northwind. Předpokládá, že máte přístup k databázi Northwind na instanci SQL Server 2000.

1. Vytvořte nový web ASP.NET.
2. Přidejte nový soubor Web. config.

    1. Klikněte pravým tlačítkem na projekt v Průzkumník řešení a klikněte na Přidat novou položku.
    2. V seznamu šablon vyberte soubor webové konfigurace a klikněte na Přidat.
3. Upravte &lt;&gt;ch connectionStrings v části následujícím způsobem: 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. Přepněte do zobrazení kódu a přidejte atribut ConnectionString a atribut SelectCommand do &lt;ASP: SqlDataSource&gt; ovládací prvek následujícím způsobem: 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. Z zobrazení Návrh přidejte nový ovládací prvek GridView.
6. V rozevíracím seznamu zvolit zdroj dat v nabídce Úkoly GridView vyberte možnost SqlDataSource1.
7. Klikněte pravým tlačítkem na Default. aspx a v nabídce vyberte Zobrazit v prohlížeči. Po zobrazení výzvy k uložení klikněte na Ano.
8. Prvek GridView zobrazí data z tabulky Products.

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a>Cvičení 2 – Úprava dat pomocí ovládacího prvku SqlDataSource

Následující cvičení ukazuje, jak vytvořit datovou vazby ovládacího prvku DropDownList pomocí deklarativní syntaxe a umožňuje upravit data zobrazená v ovládacím prvku DropDownList.

1. V zobrazení Návrh odstraňte ovládací prvek GridView z default. aspx. 

    **Důležité**: ponechejte ovládací prvek SqlDataSource na stránce.
2. Přidejte ovládací prvek DropDownList na Default. aspx.
3. Přepněte do zobrazení zdroje.
4. Přidejte atribut DataSourceId, DataTextField a DataValueField do &lt;ASP: DropDownList&gt; ovládací prvek následujícím způsobem: 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. Uložte default. aspx a zobrazte ho v prohlížeči. Všimněte si, že DropDownList obsahuje všechny produkty z databáze Northwind.
6. Zavřete prohlížeč.
7. V zobrazení zdroje default. aspx přidejte do ovládacího prvku DropDownList nový ovládací prvek TextBox. Změňte vlastnost ID textového pole na txtProductName.
8. Do ovládacího prvku TextBox přidejte ovládací prvek tlačítko Nový. Změňte vlastnost ID tlačítka na btnUpdate a vlastnost text na hodnotu **aktualizovat název produktu**.
9. V zobrazení zdrojového kódu default. aspx přidejte do tagu SqlDataSource vlastnost UpdateCommand a dvě nové UpdateParameters, jak je znázorněno níže: 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > Všimněte si, že v tomto kódu jsou přidány dva parametry aktualizace (ProductName a ProductID). Tyto parametry jsou namapovány na vlastnost text v textovém poli txtProductName a na vlastnost SelectedValue třídy ddlProducts DropDownList.
10. Přepněte na zobrazení Návrh a dvakrát klikněte na ovládací prvek tlačítko a přidejte obslužnou rutinu události.
11. Přidejte následující kód do btnUpdate\_klikněte na kód: 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. Klikněte pravým tlačítkem na Default. aspx a vyberte ho k zobrazení v prohlížeči. Po zobrazení výzvy k uložení všech změn klikněte na tlačítko Ano.
13. Částečné třídy ASP.NET 2,0 umožňují kompilaci za běhu. Aby se projevily změny v kódu, není nutné vytvářet aplikaci.
14. Vyberte produkt z DropDownList.
15. Do textového pole zadejte nový název pro vybraný produkt a pak klikněte na tlačítko Aktualizovat.
16. V databázi se aktualizuje název produktu.

## <a name="exercise-3-using-the-objectdatasource-control"></a>Cvičení 3 pomocí ovládacího prvku ObjectDataSource

Toto cvičení demonstruje použití ovládacího prvku ObjectDataSource a zdrojového objektu pro interakci s databází Northwind.

1. Klikněte pravým tlačítkem na projekt v Průzkumník řešení a klikněte na Přidat novou položku.
2. V seznamu šablon vyberte možnost webový formulář. Změňte název na Object. aspx a klikněte na Přidat.
3. Klikněte pravým tlačítkem na projekt v Průzkumník řešení a klikněte na Přidat novou položku.
4. V seznamu šablony vyberte třída. Změňte název třídy na NorthwindData.cs a klikněte na Přidat.
5. Po zobrazení výzvy k přidání třídy do složky\_kódu aplikace klikněte na Ano.
6. Do souboru NorthwindData.cs přidejte následující kód: 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. Do zobrazení zdroje objektu Object. aspx přidejte následující kód: 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. Uložte všechny soubory a procházení Object. aspx.
9. Interakce s rozhraním zobrazením podrobností, úpravou zaměstnanců, přidáním zaměstnanců a odstraňováním zaměstnanců.
