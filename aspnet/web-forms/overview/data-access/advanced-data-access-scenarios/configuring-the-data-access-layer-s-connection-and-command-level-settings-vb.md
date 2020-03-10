---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/configuring-the-data-access-layer-s-connection-and-command-level-settings-vb
title: Konfigurace nastavení úrovně připojení a nastavení na úrovni příkazu (VB) vrstvy přístupu k datům | Microsoft Docs
author: rick-anderson
description: Objekty TableAdapter v rámci typované datové sady se automaticky postará o připojení k databázi, vydávání příkazů a naplnění objektu DataTable výsledky...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: d57dfa2b-d627-45cb-b5b1-abbf3159d770
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/configuring-the-data-access-layer-s-connection-and-command-level-settings-vb
msc.type: authoredcontent
ms.openlocfilehash: fa2868fc0dd8acd76f600b47d92adb984ce8d105
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78551805"
---
# <a name="configuring-the-data-access-layers-connection--and-command-level-settings-vb"></a>Konfigurace připojení vrstvy přístupu k datům a nastavení na úrovni příkazu (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_72_VB.zip) nebo [stažení PDF](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/datatutorial72vb1.pdf)

> Objekty TableAdapter v rámci typované datové sady se automaticky postará o připojení k databázi, vydávání příkazů a naplnění objektu DataTable výsledky. Existují však situace, kdy chceme postarat o tyto podrobnosti dodržovali a v tomto kurzu se dozvíte, jak získat přístup k nastavení na úrovni připojení k databázi a nastavení na úrovni příkazu v TableAdapter.

## <a name="introduction"></a>Úvod

V celé sérii kurzů jsme použili typové datové sady k implementaci vrstvy přístupu k datům a obchodních objektů naší vícevrstvé architektury. Jak je popsáno v [prvním kurzu](../introduction/creating-a-data-access-layer-vb.md), typové datové sady s datovými tabulkami slouží jako úložiště dat, zatímco objekty TableAdapter slouží jako obálky pro komunikaci s databází, aby bylo možné načíst a upravit podkladová data. Objekty TableAdapter zapouzdřuje složitost při práci s databází a ukládá nám kód pro připojení k databázi, vystavení příkazu nebo naplnění výsledků do objektu DataTable.

Existují však situace, kdy musíme Burrow do hloubky TableAdapter a napsat kód, který funguje přímo s objekty ADO.NET. V rámci kurzu pro zabalení se mění v [rámci transakce](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md) , například jsme přidali metody do TableAdapter pro zahájení, potvrzení a vrácení transakcí ADO.NET. Tyto metody používaly vnitřní, ručně vytvořený objekt `SqlTransaction`, který byl přiřazen k objektům `SqlCommand` TableAdapter s.

V tomto kurzu se podíváme na to, jak přistupovat k nastavení na úrovni připojení k databázi a na úrovni příkazového řádku v TableAdapter. Konkrétně přidáváme funkce do `ProductsTableAdapter`, která umožňuje přístup k základnímu připojovacímu řetězci a nastavení časového limitu příkazů.

## <a name="working-with-data-using-adonet"></a>Práce s daty pomocí ADO.NET

Microsoft .NET Framework obsahuje spoustu třídy navržené speciálně pro práci s daty. Tyto třídy, které se nacházejí v [oboru názvů`System.Data`](https://msdn.microsoft.com/library/system.data.aspx), jsou označovány jako třídy *ADO.NET* . Některé třídy v ADO.NET zastřešující jsou vázané na konkrétního *poskytovatele dat*. Poskytovatele dat si můžete představit jako komunikační kanál, který umožňuje tok informací mezi třídami ADO.NET a podkladovým úložištěm dat. Existují zobecnění poskytovatelé, jako jsou OleDb a ODBC, i poskytovatele, kteří jsou speciálně navrženi pro konkrétní databázový systém. Pokud je například možné se připojit k databázi Microsoft SQL Server pomocí poskytovatele OleDb, poskytovatel SqlClient je mnohem efektivnější, protože byl navržený a optimalizovaný speciálně pro SQL Server.

Při programovém přístupu k datům se běžně používá následující vzor:

1. Navažte připojení k databázi.
2. Vydejte příkaz.
3. Pro `SELECT` dotazy Pracujte s výslednými záznamy.

Pro provedení každého z těchto kroků jsou k dispozici samostatné třídy ADO.NET. Pokud se chcete připojit k databázi pomocí poskytovatele SqlClient, použijte například [třídu`SqlConnection`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection(VS.80).aspx). Chcete-li vydat `INSERT`, `UPDATE`, `DELETE`nebo `SELECT` příkaz k databázi, použijte [třídu`SqlCommand`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.aspx).

S výjimkou [úprav v rámci kurzu transakce](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md) jsme nemuseli psát žádné ADO.NET code dodržovali, protože automaticky generovaný kód objekty TableAdapter zahrnuje funkce potřebné pro připojení k databázi, vydávání příkazů, načítání dat a naplnění těchto dat do datových tabulek. Nicméně může nastat situace, kdy potřebujeme přizpůsobit tato nastavení nízké úrovně. V několika dalších krocích prověříme, jak se dá na ADO.NET objekty používané interně objekty TableAdapter.

## <a name="step-1-examining-with-the-connection-property"></a>Krok 1: zkoumání vlastností připojení

Každá třída TableAdapter má vlastnost `Connection`, která určuje informace o připojení databáze. Tento datový typ a `ConnectionString` hodnota jsou určeny výběry provedenými v Průvodci konfigurací TableAdapter. Načtěte si, že když nejdřív přidáte TableAdapter do typové datové sady, tento průvodce požádá o zdroj databáze (viz obrázek 1). Rozevírací seznam v tomto prvním kroku zahrnuje databáze zadané v konfiguračním souboru i všechny další databáze v datových připojeních Průzkumník serveru s. Pokud databáze, kterou chceme použít, v rozevíracím seznamu neexistuje, je možné zadat nové připojení k databázi kliknutím na tlačítko nové připojení a zadáním potřebných informací o připojení.

[![prvním kroku Průvodce konfigurací TableAdapter](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image2.png)](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image1.png)

**Obrázek 1**: první krok průvodce konfigurací TableAdapter ([kliknutím zobrazíte obrázek v plné velikosti](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image3.png))

Počkejte chvilku, než zkontrolujete kód vlastnosti TableAdapter s `Connection`. Jak je uvedeno v kurzu [Vytvoření vrstvy přístupu k datům](../introduction/creating-a-data-access-layer-vb.md) , můžeme zobrazit automaticky generovaný TableAdapter kód tak, že přejdete do okna zobrazení tříd, přejdete do příslušné třídy a dvakrát kliknete na název člena.

Přejděte do okna Zobrazení tříd tak, že přejdete do nabídky Zobrazit a zvolíte Zobrazení tříd (nebo zadáte Ctrl + Shift + C). V horní polovině okna Zobrazení tříd přejděte k podrobnostem k oboru názvů `NorthwindTableAdapters` a vyberte třídu `ProductsTableAdapter`. Tím se zobrazí členové `ProductsTableAdapter` s v dolní polovině Zobrazení tříd, jak je znázorněno na obrázku 2. Dvojím kliknutím na vlastnost `Connection` zobrazíte její kód.

![Dvakrát klikněte na vlastnost připojení v Zobrazení tříd k zobrazení jejího automaticky generovaného kódu.](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image4.png)

**Obrázek 2**: poklikejte na vlastnost Connection v zobrazení tříd k zobrazení jejího automaticky generovaného kódu.

Následuje `Connection` vlastností TableAdapter s a dalším kódem souvisejícím s připojením:

[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample1.vb)]

Když je vytvořena instance třídy TableAdapter, je `_connection` členské proměnné rovna `Nothing`. Když je k vlastnosti `Connection` přistup, nejprve zkontroluje, zda byla vytvořena instance `_connection` členské proměnné. Pokud tomu tak není, je vyvolána metoda `InitConnection`, která vytvoří instanci `_connection` a nastaví její vlastnost `ConnectionString` na hodnotu připojovacího řetězce zadanou v prvním kroku Průvodce konfigurací TableAdapter.

Vlastnost `Connection` lze také přiřadit objektu `SqlConnection`. Tím přidružíte nový objekt `SqlConnection` k jednotlivým objektům `SqlCommand` TableAdapter s.

## <a name="step-2-exposing-connection-level-settings"></a>Krok 2: vystavení nastavení na úrovni připojení

Informace o připojení by měly zůstat zapouzdřeny v rámci TableAdapter a nemohou být přístupné pro jiné vrstvy architektury aplikace. Můžou ale nastat scénáře, kdy informace na úrovni připojení TableAdapter s musí být dostupné nebo přizpůsobitelné pro dotaz, uživatele nebo ASP.NET stránku.

Pomocí této `ProductsTableAdapter` v datové sadě `Northwind` zahrňte vlastnost `ConnectionString`, kterou může použít vrstva obchodní logiky ke čtení nebo změně připojovacího řetězce používaného TableAdapter.

> [!NOTE]
> *Připojovací řetězec* je řetězec, který určuje informace o připojení k databázi, jako je například poskytovatel, který se má použít, umístění databáze, přihlašovací údaje pro ověřování a další nastavení související s databází. Seznam vzorů připojovacích řetězců, které používá celá řada úložišť a poskytovatelů dat, naleznete v tématu [connectionStrings.com](http://www.connectionstrings.com/).

Jak je popsáno v kurzu [Vytvoření vrstvy přístupu k datům](../introduction/creating-a-data-access-layer-vb.md) , lze automaticky generované třídy typu DataSet rozšířit prostřednictvím použití dílčích tříd. Nejprve vytvořte novou podsložku v projektu s názvem `ConnectionAndCommandSettings` pod `~/App_Code/DAL` složky.

![Přidat podsložku s názvem ConnectionAndCommandSettings](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image5.png)

**Obrázek 3**: Přidání podsložky s názvem `ConnectionAndCommandSettings`

Přidejte nový soubor třídy s názvem `ProductsTableAdapter.ConnectionAndCommandSettings.vb` a zadejte následující kód:

[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample2.vb)]

Tato částečná třída přidá vlastnost `Public` s názvem `ConnectionString` do třídy `ProductsTableAdapter`, která umožňuje libovolné vrstvě číst nebo aktualizovat připojovací řetězec pro příslušné připojení TableAdapter s.

S touto částečnou třídou vytvořenou (a uloženou) otevřete třídu `ProductsBLL`. Přejděte na jednu z existujících metod a zadejte `Adapter` a potom stiskněte klávesu tečka, abyste mohli spustit IntelliSense. Měla by se zobrazit nová vlastnost `ConnectionString` dostupná v IntelliSense, což znamená, že můžete programově číst nebo upravovat tuto hodnotu z knihoven BLL.

## <a name="exposing-the-entire-connection-object"></a>Vystavení celého objektu připojení

Tato částečná třída zpřístupňuje jenom jednu vlastnost základního objektu připojení: `ConnectionString`. Pokud chcete, aby byl celý objekt připojení dostupný i nad rámec TableAdapter, můžete alternativně změnit úroveň ochrany vlastností `Connection`. Automaticky generovaný kód, který jsme zkoumali v kroku 1, ukázal, že vlastnost TableAdapter s `Connection` je označená jako `Friend`, což znamená, že k ní lze přistupovat pouze třídy ve stejném sestavení. To však může být změněno prostřednictvím vlastnosti `ConnectionModifier` TableAdapter s.

Otevřete `Northwind` datovou sadu, klikněte na `ProductsTableAdapter` v návrháři a přejděte na okno Vlastnosti. Zobrazí se `ConnectionModifier` nastavená na výchozí hodnotu `Assembly`. Chcete-li zpřístupnit vlastnost `Connection` mimo typové sestavení DataSet s, změňte vlastnost `ConnectionModifier` na `Public`.

[![úroveň přístupnosti vlastností připojení lze nakonfigurovat prostřednictvím vlastnosti ConnectionModifier](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image7.png)](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image6.png)

**Obrázek 4**: úroveň přístupnosti vlastností `Connection` se dá nakonfigurovat přes vlastnost `ConnectionModifier` ([kliknutím zobrazíte obrázek v plné velikosti).](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image8.png)

Uložte datovou sadu a vraťte se do třídy `ProductsBLL`. Stejně jako dřív přejděte na jednu z existujících metod a zadejte `Adapter` a potom stiskněte klávesu tečka pro zobrazení IntelliSense. Seznam by měl obsahovat `Connection` vlastnost, což znamená, že teď můžete programově číst nebo přiřazovat nastavení na úrovni připojení z knihoven BLL.

## <a name="step-3-examining-the-command-related-properties"></a>Krok 3: prozkoumání vlastností souvisejících s příkazy

TableAdapter se skládá z hlavního dotazu, který ve výchozím nastavení obsahuje automaticky generované `INSERT`, `UPDATE`a `DELETE` příkazy. Tento hlavní dotaz s `INSERT`, `UPDATE`a `DELETE` příkazy jsou implementovány v kódu TableAdapter s jako objekt ADO.NET data Adapter prostřednictvím vlastnosti `Adapter`. Podobně jako u vlastnosti `Connection` se datový typ `Adapter` vlastnosti s určuje podle použitého poskytovatele dat. Vzhledem k tomu, že tyto kurzy používají poskytovatele SqlClient, vlastnost `Adapter` je typu [`SqlDataAdapter`](https://msdn.microsoft.com/library/system.data.sqlclient.sqldataadapter(VS.80).aspx).

Vlastnost TableAdapter s `Adapter` má tři vlastnosti typu `SqlCommand`, které používá k vystavení příkazů `INSERT`, `UPDATE`a `DELETE`:

- `InsertCommand`
- `UpdateCommand`
- `DeleteCommand`

Objekt `SqlCommand` zodpovídá za odeslání konkrétního dotazu do databáze a má vlastnosti jako: [`CommandText`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.commandtext.aspx), který obsahuje příkaz SQL ad hoc nebo uloženou proceduru, která má být provedena. a [`Parameters`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.parameters.aspx), což je kolekce objektů `SqlParameter`. Jak jsme se mohli vrátit do kurzu [Vytvoření vrstvy přístupu k datům](../introduction/creating-a-data-access-layer-vb.md) , tyto objekty příkazů je možné přizpůsobit pomocí okno Vlastnosti.

Kromě hlavního dotazu může TableAdapter zahrnovat proměnlivý počet metod, které při vyvolání odesílají zadaný příkaz do databáze. Hlavní objekt příkazu dotazu s a objekty příkazu pro všechny další metody jsou uloženy ve vlastnosti TableAdapter s `CommandCollection`.

Počkejte, než se podíváme na kód vygenerovaný `ProductsTableAdapter` v datové sadě `Northwind` pro tyto dvě vlastnosti a jejich podpůrné členské proměnné a pomocné metody:

[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample3.vb)]

Kód pro `Adapter` a vlastnosti `CommandCollection` úzce napodobuje vlastnost `Connection`. Existují proměnné členů, které obsahují objekty používané vlastnostmi. Vlastnosti přístupových objektů `Get` jsou spouštěny zaškrtnutím a zjistíte, zda je odpovídající členská proměnná `Nothing`. Pokud ano, je volána inicializační metoda, která vytvoří instanci členské proměnné a přiřadí základní vlastnosti související s příkazy.

## <a name="step-4-exposing-command-level-settings"></a>Krok 4: vystavení nastavení na úrovni příkazu

V ideálním případě by informace na úrovni příkazu měly zůstat zapouzdřeny v rámci vrstvy přístupu k datům. Tyto informace by se měly provádět v jiných vrstvách architektury, ale můžou být vystavené prostřednictvím částečné třídy, stejně jako u nastavení na úrovni připojení.

Vzhledem k tomu, že TableAdapter má pouze jednu vlastnost `Connection`, kód pro vystavení nastavení na úrovni připojení je poměrně jednoduchý. Věci jsou trochu složitější při změně nastavení na úrovni příkazu, protože TableAdapter může mít více objektů příkazu – `InsertCommand`, `UpdateCommand`a `DeleteCommand`, spolu s proměnným počtem objektů příkazů ve vlastnosti `CommandCollection`. Při aktualizaci nastavení na úrovni příkazu bude nutné tato nastavení rozšířit na všechny objekty příkazu.

Představte si například, že byly některé dotazy v TableAdapter, které trvaly mimořádnou dobu od času spuštění. Když použijete TableAdapter k provedení jednoho z těchto dotazů, můžeme zvětšit objekt Command [`CommandTimeout` Property](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.commandtimeout.aspx). Tato vlastnost určuje počet sekund, po které se má počkat, než se příkaz spustí, a použije se výchozí hodnota 30.

Chcete-li, aby vlastnost `CommandTimeout` mohla být upravena pomocí knihoven BLL, přidejte následující metodu `Public` do `ProductsDataTable` pomocí souboru dílčí třídy vytvořeného v kroku 2 (`ProductsTableAdapter.ConnectionAndCommandSettings.vb`):

[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample4.vb)]

Tuto metodu lze vyvolat z knihoven BLL nebo prezentační vrstvy pro nastavení časového limitu příkazů pro všechny problémy s příkazy, které instance TableAdapter.

> [!NOTE]
> Vlastnosti `Adapter` a `CommandCollection` jsou označeny jako `Private`, což znamená, že mohou být k dispozici pouze z kódu v rámci TableAdapter. Na rozdíl od vlastnosti `Connection` se tyto modifikátory přístupu nedají konfigurovat. Proto pokud potřebujete vystavit vlastnosti na úrovni příkazu jiným vrstvám v architektuře, je nutné použít předchozí přístup ke třídě popsané výše a poskytnout `Public` metodu nebo vlastnost, která čte nebo zapisuje do `Private` objektů příkazů.

## <a name="summary"></a>Souhrn

Objekty TableAdapter v rámci typové datové sady slouží k zapouzdření podrobností a složitosti přístupu k datům. Pomocí objekty TableAdapter se nemusíte starat o zápis kódu ADO.NET pro připojení k databázi, vystavení příkazu nebo naplnění výsledků do objektu DataTable. Vše se zpracovává automaticky pro nás.

Mohou však nastat situace, kdy potřebujeme upravit ADO.NET specifiky nízké úrovně, jako je například změna připojovacího řetězce nebo výchozí připojení nebo hodnoty časového limitu příkazu. TableAdapter má automaticky generované vlastnosti `Connection`, `Adapter`a `CommandCollection`, ale ve výchozím nastavení jsou to `Friend` nebo `Private`. Tyto vnitřní informace mohou být zpřístupněny rozšířením TableAdapter pomocí dílčích tříd pro zahrnutí `Public`ch metod nebo vlastností. Alternativně lze modifikátor přístupu k vlastnosti TableAdapter s `Connection` nakonfigurovat prostřednictvím vlastnosti TableAdapter s `ConnectionModifier`.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Recenzenti potenciálních zákazníků pro tento kurz byly Burnadette Leigh, S Ren Jacob Lauritsen, Teresa Murphy a Hilton Geisenow. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](working-with-computed-columns-vb.md)
> [Další](protecting-connection-strings-and-other-configuration-information-vb.md)
