---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
title: Začínáme s Entity Framework 4,0 Database First a webovými formuláři ASP.NET 4 – část 2 | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak pomocí Entity Framework vytvořit aplikace webových formulářů ASP.NET. Ukázková aplikace je...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: fb63a326-a4ae-4b0c-a4f5-412327197216
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
msc.type: authoredcontent
ms.openlocfilehash: bd6a2e29e6f0df04e39be29160e2e08cc99c4706
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78566008"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-2"></a>Začínáme s Entity Framework 4,0 Database First a webovými formuláři ASP.NET 4 – část 2

tím, že [Dykstra](https://github.com/tdykstra)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak pomocí Entity Framework 4,0 a sady Visual Studio 2010 vytvářet aplikace webových formulářů ASP.NET. Informace o řadě kurzů najdete v [prvním kurzu v řadě](the-entity-framework-and-aspnet-getting-started-part-1.md) .

## <a name="the-entitydatasource-control"></a>Ovládací prvek EntityDataSource

V předchozím kurzu jste vytvořili web, databázi a datový model. V tomto kurzu pracujete s ovládacím prvkem `EntityDataSource`, který ASP.NET poskytuje, aby bylo snazší pracovat s datovým modelem Entity Framework. Vytvoříte `GridView` ovládací prvek pro zobrazování a úpravu dat studentů, `DetailsView` řízení pro přidávání nových studentů a ovládací prvek `DropDownList` pro výběr oddělení (který budete používat později pro zobrazení přidružených kurzů).

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image1.png)

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image3.png)

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image5.png)

Všimněte si, že v této aplikaci nebudete přidáváni ověřování na stránky, které databázi aktualizují, a některé z zpracování chyb nebudou tak robustní, jak by bylo potřeba v produkční aplikaci. Tím se kurz neustále zaměřuje na Entity Framework a trvá příliš dlouho. Podrobnosti o tom, jak tyto funkce přidat do aplikace, najdete v tématu [ověřování vstupu uživatele na webových stránkách ASP.NET](https://msdn.microsoft.com/library/7kh55542.aspx) a [zpracování chyb na stránkách ASP.NET a aplikacích](https://msdn.microsoft.com/library/w16865z6.aspx).

## <a name="adding-and-configuring-the-entitydatasource-control"></a>Přidání a konfigurace ovládacího prvku EntityDataSource

Začnete konfigurací ovládacího prvku `EntityDataSource` ke čtení `Person` entit ze sady entit `People`.

Ujistěte se, že máte otevřenou aplikaci Visual Studio a že pracujete s projektem, který jste vytvořili v části 1. Pokud jste projekt nevytvořili, protože jste vytvořili datový model nebo když jste jeho poslední změnu provedli, sestavte projekt nyní. Změny datového modelu nejsou zpřístupněny návrháři, dokud není projekt sestaven.

Vytvořte novou webovou stránku pomocí **webového formuláře pomocí šablony stránky předlohy** a pojmenujte ji *students. aspx*.

[![Image23](the-entity-framework-and-aspnet-getting-started-part-2/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image7.png)

Zadejte *Web. Master* jako stránku předlohy. Všechny stránky, které vytvoříte pro tyto kurzy, budou používat tuto stránku předlohy.

[![Image24](the-entity-framework-and-aspnet-getting-started-part-2/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image9.png)

V zobrazení **zdroj** přidejte `h2` záhlaví k ovládacímu prvku `Content` s názvem `Content2`, jak je znázorněno v následujícím příkladu:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample1.aspx)]

Na kartě **data** na **panelu nástrojů**přetáhněte ovládací prvek `EntityDataSource` na stránku, přetáhněte ho pod záhlavím a změňte ID na `StudentsEntityDataSource`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample2.aspx)]

Přepněte do zobrazení **Návrh** , klikněte na inteligentní značku ovládacího prvku zdroje dat a potom kliknutím na **Konfigurovat zdroj dat** spusťte průvodce **konfigurací zdroje dat** .

[![Image01](the-entity-framework-and-aspnet-getting-started-part-2/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image11.png)

V kroku průvodce **konfigurací objektu ObjectContext** vyberte **SchoolEntities** jako hodnotu pro **pojmenované připojení**a jako hodnotu **DefaultContainerName** vyberte **SchoolEntities** . Pak klikněte na tlačítko **Další**.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-2/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image13.png)

Poznámka: Pokud se v tomto okamžiku zobrazí následující dialogové okno, je třeba projekt sestavit, aby bylo možné pokračovat.

[![Image25](the-entity-framework-and-aspnet-getting-started-part-2/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image15.png)

V kroku **Konfigurace výběru dat** vyberte možnost **lidé** jako hodnotu pro **EntitySetName**. V části **Vybrat**se ujistěte, že je zaškrtnuté políčko **Vyberte** vše. Pak vyberte možnosti pro povolení aktualizace a odstranění. Až skončíte, klikněte na **Dokončit**.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-2/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image17.png)

## <a name="configuring-database-rules-to-allow-deletion"></a>Konfigurace databázových pravidel pro povolení odstranění

Vytvoříte stránku, která umožní uživatelům odstraňovat studenty z `Person` tabulky, která má tři relace s jinými tabulkami (`Course`, `StudentGrade`a `OfficeAssignment`). Ve výchozím nastavení vám databáze zabrání v odstranění řádku v `Person`, pokud v jedné z ostatních tabulek existují související řádky. Nejprve můžete související řádky odstranit, nebo můžete databázi nakonfigurovat tak, aby se automaticky odstranila při odstranění `Person`ho řádku. V případě záznamů studenta v tomto kurzu nakonfigurujete databázi, aby automaticky odstranila související data. Vzhledem k tomu, že studenti mohou mít v tabulce `StudentGrade` pouze související řádky, je nutné nakonfigurovat pouze jednu ze tří vztahů.

Pokud používáte soubor *School. mdf* , který jste stáhli z projektu, který je součástí tohoto kurzu, můžete tuto část přeskočit, protože tyto změny konfigurace již byly provedeny. Pokud jste databázi vytvořili spuštěním skriptu, nakonfigurujte databázi pomocí následujících postupů.

V **Průzkumník serveru**otevřete databázový diagram, který jste vytvořili v části 1. Klikněte pravým tlačítkem na vztah mezi `Person` a `StudentGrade` (čára mezi tabulkami) a pak vyberte **vlastnosti**.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-2/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image19.png)

V okně **vlastnosti** rozbalte položku **Vložit a aktualizovat specifikaci** a nastavte vlastnost **DeleteRule** na hodnotu **Cascade**.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-2/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image21.png)

Uložte a zavřete diagram. Pokud se zobrazí dotaz, zda chcete databázi aktualizovat, klikněte na tlačítko **Ano**.

Abyste se ujistili, že model udržuje entity, které jsou v paměti synchronizované s tím, co databáze dělá, musíte v datovém modelu nastavit odpovídající pravidla. Otevřete *SchoolModel. edmx*, klikněte pravým tlačítkem myši na čáru přidružení mezi `Person` a `StudentGrade`a pak vyberte **vlastnosti**.

[![Image21](the-entity-framework-and-aspnet-getting-started-part-2/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image23.png)

V okně **vlastnosti** nastavte End1- **Delete** na **Cascade**.

[![Image22](the-entity-framework-and-aspnet-getting-started-part-2/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image25.png)

Uložte a zavřete soubor *SchoolModel. edmx* a pak znovu sestavte projekt.

Obecně platí, že když se databáze změní, máte několik možností, jak synchronizovat model:

- U určitých druhů změn (například přidávání nebo obnovování tabulek, zobrazení nebo uložených procedur), klikněte pravým tlačítkem myši v návrháři a vyberte **aktualizovat model z databáze** , aby se tento Návrhář automaticky provedl.
- Znovu vygenerujte datový model.
- Proveďte ruční aktualizace, jako je tato.

V tomto případě jste mohli model znovu vygenerovat nebo aktualizovat tabulky ovlivněné změnou vztahu, ale pak byste museli změnit název pole-název (od `FirstName` do `FirstMidName`).

## <a name="using-a-gridview-control-to-read-and-update-entities"></a>Použití ovládacího prvku GridView ke čtení a aktualizaci entit

V této části použijete `GridView` ovládací prvek pro zobrazení, aktualizaci nebo odstranění studentů.

Otevřete nebo přejděte na *studenty. aspx* a přepněte se do zobrazení **Návrh** . Na kartě **data** na **panelu nástrojů**přetáhněte ovládací prvek `GridView` napravo od ovládacího prvku `EntityDataSource`, pojmenujte jej `StudentsGridView`, klikněte na inteligentní značku a pak jako zdroj dat vyberte **StudentsEntityDataSource** .

[![Image06](the-entity-framework-and-aspnet-getting-started-part-2/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image27.png)

Klikněte na **Aktualizovat schéma** (Pokud se zobrazí výzva k potvrzení), klikněte na tlačítko **Ano** , pak na **Povolit stránkování**, povolit **řazení**, **Povolit úpravy**a **Povolit odstranění**.

Klikněte na tlačítko **Upravit sloupce**.

[![Image10](the-entity-framework-and-aspnet-getting-started-part-2/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image29.png)

V poli **Vybraná pole** odstraňte **PersonID**, **LastName**a **HireDate**. Obvykle nezobrazujete klíč záznamu uživatelům, datum přijetí není relevantní pro studenty a do jednoho pole umístíte obě části názvu, takže budete potřebovat jenom jedno z polí s názvem.)

[![Image11](the-entity-framework-and-aspnet-getting-started-part-2/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image31.png)

Vyberte pole **FirstMidName** a pak klikněte na **převést toto pole na TemplateField**.

Totéž udělejte pro **EnrollmentDate**.

[![Image13](the-entity-framework-and-aspnet-getting-started-part-2/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image33.png)

Klikněte na **OK** a pak přepněte do zobrazení **zdroje** . Zbývající změny budou snazší přímo v kódu. Značka ovládacího prvku `GridView` nyní vypadá jako v následujícím příkladu.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample3.aspx)]

První sloupec za polem příkazu je pole šablony, ve kterém se aktuálně zobrazuje křestní jméno. Změňte označení pro toto pole šablony tak, aby vypadalo jako v následujícím příkladu:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample4.aspx)]

V režimu zobrazení se dva ovládací prvky `Label` zobrazují jako jméno a příjmení. V režimu úprav jsou k dispozici dvě textová pole, abyste mohli změnit jméno a příjmení. Stejně jako u ovládacích prvků `Label` v režimu zobrazení používáte `Bind` a `Eval` výrazy přesně tak, jak byste měli ASP.NET ovládací prvky zdroje dat, které se připojují přímo k databázím. Jediným rozdílem je, že zadáváte vlastnosti entity místo databázových sloupců.

Poslední sloupec je pole šablony, které zobrazuje datum zápisu. Změňte označení tohoto pole tak, aby vypadalo jako v následujícím příkladu:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample5.aspx)]

V režimu zobrazení i úprav formátový řetězec {0, d} způsobí, že se datum zobrazí ve formátu "short data". (Váš počítač může být nakonfigurovaný tak, aby se tento formát zobrazoval jinak než obrázky obrazovky zobrazené v tomto kurzu.)

Všimněte si, že v každé z těchto polí šablony Návrhář ve výchozím nastavení použil výraz `Bind`, ale změnili jste jej na výraz `Eval` v elementech `ItemTemplate`. Výraz `Bind` zpřístupňuje dostupná data v `GridView` vlastnosti ovládacího prvku pro případ, že budete potřebovat přístup k datům v kódu. Na této stránce nepotřebujete přístup k těmto datům v kódu, takže můžete použít `Eval`, což je efektivnější. Další informace najdete v tématu věnovaném [získání dat z ovládacích prvků pro](https://weblogs.asp.net/davidfowler/archive/2008/12/12/getting-your-data-out-of-the-data-controls.aspx)data.

## <a name="revising-entitydatasource-control-markup-to-improve-performance"></a>Revize značek ovládacího prvku EntityDataSource pro zlepšení výkonu

V označení ovládacího prvku `EntityDataSource` odeberte atributy `ConnectionString` a `DefaultContainerName` a nahraďte je atributem `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"`. Toto je změna, kterou byste měli udělat při každém vytvoření ovládacího prvku `EntityDataSource`, pokud nepotřebujete použít připojení, které se liší od toho, který je pevně kódovaný ve třídě kontextu objektu. Použití atributu `ContextTypeName` přináší následující výhody:

- Lepší výkon. Když ovládací prvek `EntityDataSource` inicializuje datový model pomocí atributů `ConnectionString` a `DefaultContainerName`, provede další práci pro načtení metadat pro každý požadavek. To není nutné, pokud zadáte atribut `ContextTypeName`.
- Opožděné načítání je ve výchozím nastavení zapnuté v třídách kontextu generovaných objektů (například `SchoolEntities` v tomto kurzu) v Entity Framework 4,0. To znamená, že navigační vlastnosti jsou v případě potřeby načítány se souvisejícími daty automaticky. Opožděné načítání je podrobněji vysvětleno dále v tomto kurzu.
- Všechna vlastní nastavení, která jste použili u třídy kontextu objektu (v tomto případě `SchoolEntities` třídy), budou k dispozici pro ovládací prvky, které používají ovládací prvek `EntityDataSource`. Přizpůsobení třídy kontextu objektu je pokročilé téma, které není zahrnuto v této sérii kurzů. Další informace naleznete v tématu [rozšíření Entity Framework generovaných typů](https://msdn.microsoft.com/library/dd456844.aspx).

Značka se teď bude podobat následujícímu příkladu (pořadí vlastností se může lišit):

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample6.aspx)]

Atribut `EnableFlattening` odkazuje na funkci, která byla vyžadována v dřívějších verzích Entity Framework, protože sloupce cizího klíče nebyly zveřejněny jako vlastnosti entity. Aktuální verze umožňuje použít *přidružení cizího klíče*, což znamená, že vlastnosti cizího klíče jsou zpřístupněny pro všechna přiřazení, ale u přidružení typu m:n. Pokud vaše Entity obsahují vlastnosti cizího klíče a žádné [komplexní typy](https://msdn.microsoft.com/library/bb738472.aspx), můžete ponechat tento atribut nastavený na `False`. Neodstraňujte atribut ze značky, protože výchozí hodnota je `True`. Další informace najdete v tématu věnovaném [sloučení objektů (EntityDataSource)](https://msdn.microsoft.com/library/ee404746.aspx).

Spusťte stránku a zobrazí se seznam studentů a zaměstnanců (v dalším kurzu budete filtrovat jenom studenty). Křestní jméno a příjmení se zobrazí společně.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-2/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image35.png)

Pokud chcete zobrazení seřadit, klikněte na název sloupce.

V libovolném řádku klikněte na **Upravit** . Textová pole se zobrazí, kde můžete změnit jméno a příjmení.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-2/_static/image38.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image37.png)

Tlačítko **Odstranit** také funguje. Klikněte na tlačítko Odstranit pro řádek, který má datum registrace, a řádek zmizí. (Řádky bez data registrace reprezentují instruktory a může se zobrazit chyba referenční integrity. V dalším kurzu tento seznam vyfiltrujete tak, aby zahrnoval jenom studenty.)

## <a name="displaying-data-from-a-navigation-property"></a>Zobrazení dat z navigační vlastnosti

Nyní předpokládejme, že chcete zjistit, kolik kurzů má každý student zaregistrovaný. Entity Framework poskytuje tyto informace v `StudentGrades` navigační vlastnosti entity `Person`. Vzhledem k tomu, že návrh databáze neumožňuje, aby se student zaregistroval v rámci kurzu, aniž by se mu přiřadila vaše třídy, můžete předpokládat, že řádek v řádku `StudentGrade` tabulky, který je spojený s kurzem, je stejný jako zápis do kurzu. (Navigační vlastnost `Courses` je určena pouze pro instruktory.)

Použijete-li atribut `ContextTypeName` ovládacího prvku `EntityDataSource`, Entity Framework při přístupu k této vlastnosti automaticky načte informace pro navigační vlastnost. Tato metoda se nazývá *opožděné načítání*. To však může být neefektivní, protože má za následek samostatné volání databáze pokaždé, když jsou potřeba další informace. Pokud potřebujete data z vlastnosti navigace pro každou entitu vrácenou ovládacím prvkem `EntityDataSource`, je efektivnější načíst související data společně s entitou v jednom volání do databáze. To se říká *Eager načítání*a zadáte Eager načítání pro navigační vlastnost nastavením vlastnosti `Include` ovládacího prvku `EntityDataSource`.

Ve službě *students. aspx*chcete zobrazit počet kurzů pro každého studenta, takže Eager načítání je nejlepší volbou. Pokud jste zobrazili všechny studenty, ale zobrazuje se počet kurzů jenom pro několik z nich (což by vyžadovalo psaní kódu navíc k označení), může být opožděné načítání lepší volbou.

Otevřete nebo přejděte na *studenty. aspx*, přepněte do zobrazení **návrh** , vyberte `StudentsEntityDataSource`a v okně **vlastnosti** nastavte vlastnost **include** na **StudentGrades**. (Pokud jste chtěli získat více vlastností navigace, mohli byste zadat jejich názvy oddělené čárkami, například **StudentGrades, kurzy**).

[![Image19](the-entity-framework-and-aspnet-getting-started-part-2/_static/image40.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image39.png)

Přepněte do zobrazení **zdroje** . V ovládacím prvku `StudentsGridView` za poslední prvek `asp:TemplateField` přidejte následující nové pole šablony:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample7.aspx)]

Ve výrazu `Eval` můžete odkazovat na vlastnost navigace `StudentGrades`. Vzhledem k tomu, že tato vlastnost obsahuje kolekci, má vlastnost `Count`, kterou můžete použít k zobrazení počtu kurzů, ve kterých je student zaregistrovaný. V pozdějším kurzu uvidíte, jak zobrazit data z navigačních vlastností, které obsahují jednotlivé entity místo kolekcí. (Všimněte si, že nemůžete použít prvky `BoundField` k zobrazení dat z vlastností navigace.)

Spusťte stránku a teď uvidíte, kolik kurzů jednotlivého studenta jsou zaregistrované v.

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image42.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image41.png)

## <a name="using-a-detailsview-control-to-insert-entities"></a>Použití ovládacího prvku DetailsView pro vložení entit

Dalším krokem je vytvoření stránky s `DetailsView` ovládacím prvkem, který vám umožní přidat nové studenty. Zavřete prohlížeč a pak vytvořte novou webovou stránku pomocí stránky předlohy *Web. Master* . Pojmenujte stránku *StudentsAdd. aspx*a pak přepněte do zobrazení **zdroje** .

Přidejte následující kód, který nahradí existující značku ovládacího prvku `Content` s názvem `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample8.aspx)]

Tento kód vytvoří ovládací prvek `EntityDataSource`, který se podobá tomu, který jste vytvořili ve službě *students. aspx*, s výjimkou toho, že umožňuje vkládání. Stejně jako u ovládacího prvku `GridView` jsou vázaná pole ovládacího prvku `DetailsView` kódována přesně stejně, jako by byla pro ovládací prvek dat, který se připojuje přímo k databázi, s výjimkou toho, že odkazují na vlastnosti entit. V tomto případě se `DetailsView` ovládací prvek používá pouze pro vložení řádků, takže jste nastavili výchozí režim na `Insert`.

Spusťte stránku a přidejte nového studenta.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image44.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image43.png)

Po vložení nového studenta se nic nestane, ale pokud teď spustíte *studenty. aspx*, zobrazí se informace o novém studentovi.

## <a name="displaying-data-in-a-drop-down-list"></a>Zobrazení dat v rozevíracím seznamu

V následujících krocích provedete vázání ovládacího prvku `DropDownList` do sady entit pomocí ovládacího prvku `EntityDataSource`. V této části kurzu nebudete s tímto seznamem mnohem dělat. V následujících částech ale pomocí seznamu umožníte uživatelům vybrat oddělení k zobrazení kurzů přidružených k danému oddělení.

Vytvořte novou webovou stránku s názvem *kurzy. aspx*. V zobrazení **zdroj** přidejte záhlaví do ovládacího prvku `Content` s názvem `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample9.aspx)]

V zobrazení **Návrh** přidejte ovládací prvek `EntityDataSource` do stránky stejně jako předtím, s výjimkou tohoto názvu `DepartmentsEntityDataSource`. Jako hodnotu **EntitySetName** vyberte **oddělení** a vyberte jenom vlastnosti **DepartmentID** a **Name** .

[![Image15](the-entity-framework-and-aspnet-getting-started-part-2/_static/image46.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image45.png)

Z karty **standardní** na **panelu nástrojů**přetáhněte ovládací prvek `DropDownList` na stránku, pojmenujte ho `DepartmentsDropDownList`, klikněte na inteligentní značku a výběrem **Možnosti zvolit zdroj dat** spusťte **Průvodce konfigurací zdroje**dat.

[![Image16](the-entity-framework-and-aspnet-getting-started-part-2/_static/image48.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image47.png)

V kroku **Zvolte zdroj dat** vyberte **DepartmentsEntityDataSource** jako zdroj dat, klikněte na **Aktualizovat schéma**a pak vyberte **název** jako datové pole, které chcete zobrazit a **DepartmentID** jako pole data hodnoty. Klikněte na tlačítko **OK**.

[![Image17](the-entity-framework-and-aspnet-getting-started-part-2/_static/image50.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image49.png)

Metoda, kterou použijete k vázání ovládacího prvku pomocí Entity Framework, je stejná jako u jiných ovládacích prvků zdroje dat ASP.NET s výjimkou, že zadáváte vlastnosti entit a entit.

Přepněte do zobrazení **zdroje** a přidejte "vybrat oddělení:" těsně před ovládací prvek `DropDownList`.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample10.aspx)]

Jako připomenutí změňte značku ovládacího prvku `EntityDataSource` v tomto okamžiku nahrazením atributů `ConnectionString` a `DefaultContainerName` atributem `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"`. Je často vhodné počkat až po vytvoření ovládacího prvku vázaného na data, který je propojen s ovládacím prvkem zdroje dat před změnou značky ovládacího prvku `EntityDataSource`, protože po provedení změny Návrhář neposkytne možnost **Aktualizovat schéma** v ovládacím prvku vázaného na data.

Spusťte stránku a v rozevíracím seznamu můžete vybrat oddělení.

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image52.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image51.png)

Tím se dokončí Úvod k použití ovládacího prvku `EntityDataSource`. Práce s tímto ovládacím prvkem se obecně neliší od práce s jinými ovládacími prvky zdroje dat ASP.NET s tím rozdílem, že místo tabulek a sloupců odkazujete na entity a vlastnosti. Jedinou výjimkou je, když chcete získat přístup k vlastnostem navigace. V dalším kurzu uvidíte, že syntaxe, kterou používáte s ovládacím prvkem `EntityDataSource`, se může lišit od jiných ovládacích prvků zdroje dat při filtrování, seskupování a řazení dat.

> [!div class="step-by-step"]
> [Předchozí](the-entity-framework-and-aspnet-getting-started-part-1.md)
> [Další](the-entity-framework-and-aspnet-getting-started-part-3.md)
