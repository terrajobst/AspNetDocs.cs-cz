---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
title: 'Iterace #6 – použití vývoje řízeného testy (C#) | Microsoft Docs'
author: microsoft
description: V této šesté iteraci přidáme do naší aplikace nové funkce, a to tak, že nejprve zapíšeme testy jednotek a napíšeme kód na testy jednotek. V této iteraci,...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 013c3c26-7dc3-41d1-8064-f233c86008b5
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
msc.type: authoredcontent
ms.openlocfilehash: aee0ff9d8d7f17e8a00dab12467bd3a3457fbe18
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601799"
---
# <a name="iteration-6--use-test-driven-development-c"></a>Iterace #6 – použití vývoje řízeného testy (C#)

od [Microsoftu](https://github.com/microsoft)

[Stáhnout kód](iteration-6-use-test-driven-development-cs/_static/contactmanager_6_cs1.zip)

> V této šesté iteraci přidáme do naší aplikace nové funkce, a to tak, že nejprve zapíšeme testy jednotek a napíšeme kód na testy jednotek. V této iteraci přidáváme skupiny kontaktů.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>Sestavování aplikace pro správu kontaktů ASP.NETC#MVC ()

V této sérii kurzů sestavíme celou aplikaci pro správu kontaktů od začátku do konce. Aplikace Správce kontaktů umožňuje ukládat kontaktní údaje – jména, telefonní čísla a e-mailové adresy – seznam lidí.

Aplikaci sestavíme přes několik iterací. U každé iterace doporučujeme aplikaci postupně vylepšit. Cílem tohoto vícenásobného přístupu k iteraci je umožnit pochopení příčiny každé změny.

- Iterace #1 – Vytvoření aplikace V první iteraci vytvoříme nejjednodušším způsobem správce kontaktů. Přidáváme podporu základních databázových operací: vytváření, čtení, aktualizace a odstraňování (CRUD).

- Iterace #2 – nastaví vzhled aplikace jako příjemné. V této iteraci Vylepšete vzhled aplikace úpravou výchozí stránky předlohy zobrazení ASP.NET MVC a šablony kaskádových stylů.

- Iterace #3 – Přidání ověření formuláře. Třetí iterace přidá základní ověřování formuláře. Uživatelům bráníme v odesílání formuláře bez nutnosti vyplnit požadovaná pole formuláře. Ověřujeme taky e-mailové adresy a telefonní čísla.

- Iterace #4 – zajistěte, aby byla aplikace volně spojená. V této čtvrté iteraci využijeme několik vzorů návrhu softwaru, které usnadňují údržbu a úpravy aplikace Správce kontaktů. Například refaktorujte naši aplikaci, aby používala vzor úložiště a vzor vkládání závislostí.

- Iterace #5 – vytvoření testů jednotek. V páté iteraci aplikace usnadňuje údržbu a úpravy přidáním jednotkových testů. Pro naše řadiče a logiku ověřování jsme nastavili třídy datového modelu a testy jednotek.

- Iterace #6 – použití vývoje řízeného testem. V této šesté iteraci přidáme do naší aplikace nové funkce, a to tak, že nejprve zapíšeme testy jednotek a napíšeme kód na testy jednotek. V této iteraci přidáváme skupiny kontaktů.

- Iterace #7 – přidání funkce AJAX V sedmé iteraci vylepšit rychlost reakce a výkon naší aplikace přidáním podpory pro AJAX.

## <a name="this-iteration"></a>Tato iterace

V předchozí iteraci aplikace Správce kontaktů jsme vytvořili testy jednotek, které pro náš kód poskytují bezpečnostní síť. Motivace pro vytváření testů jednotek proběhla tak, aby byl náš kód odolný proti změně. V případě testů jednotek můžeme Happily provést jakoukoli změnu našeho kódu a okamžitě zjistit, jestli jsme převedli existující funkce.

V této iteraci používáme testy jednotek pro zcela jiný účel. V této iteraci používáme testy jednotek jako součást filozofie návrhu aplikace označovaného jako *Vývoj řízený testem*. Při vývoji vývoje řízeného testováním napíšete nejprve testy a potom do testů napíšete kód.

Při vyzkoušení vývoje řízeného testy jsou přesnější tři kroky, které jste dokončili při vytváření kódu (červený/zelený/refaktorer):

1. Zapsat test jednotky, který se nezdařil (červený)
2. Napsat kód, který projde testem jednotky (zeleně)
3. Refaktoring kódu (refaktoring)

Nejprve zapište test jednotky. Test jednotek by měl vyjadřovat svůj záměr na to, jak očekáváte, aby se kód choval. Při prvním vytvoření testu jednotek by test jednotek neměl selhat. Test by se nezdařil, protože jste ještě nenapsali žádný kód aplikace, který by splňoval test.

V dalším kroku zapíšete pouze dostatečný kód, aby byl test jednotky splněn. Cílem je napsat kód v laziest, sloppiest a nejrychlejší možný způsob. Neměli byste ztrácet čas při zvažování architektury vaší aplikace. Místo toho byste se měli zaměřit na zápis minimálního množství kódu, který je nezbytný pro splnění záměru vyjádřeného jednotkovým testem.

Nakonec po napsání dostatečného kódu se můžete vrátit zpět a vzít v úvahu celkovou architekturu aplikace. V tomto kroku přepíšete (refaktorujte) kód tím, že využijete výhod vzorů návrhu softwaru, jako je například vzor úložiště, takže váš kód je udržovatelnější. V tomto kroku můžete ucelená přepisovat kód, protože váš kód je pokryt jednotkovým testováním.

Existuje mnoho výhod, které vedou k vyzkoušení vývoje řízeného testem. Nejprve vývojářem řízený test vynutí soustředit se na kód, který je skutečně nutné zapsat. Vzhledem k tomu, že se trvale zaměřujete na pouhé psaní kódu pro předání konkrétního testu, nebudete se moci Wandering do plevelů a zapisují obrovský objem kódu, který nikdy nebudete používat.

Dále metoda "test First" vynutí, abyste napsali kód z perspektivy způsobu použití kódu. Jinými slovy, při praktickém vývoji na základě testů průběžně píšete testy z perspektivy uživatele. Vývoj řízený testováním proto může mít za následek čisticí a lépe pochopitelné rozhraní API.

Nakonec vývojář řízený testováním vynutí napsat testy jednotek v rámci normálního procesu psaní aplikace. Jako blížící se konečný termín projektu je testování obvykle první věc, která se nachází v okně. Při vykonávání vývoje založeného na testu na druhé straně je pravděpodobnější, že budete virtuous o psaní testů jednotek, protože vývoj řízený testováním provádí testování částí až po proces vytváření aplikace.

> [!NOTE] 
> 
> Pokud se chcete dozvědět víc o vývoji řízených pomocí testů, doporučujeme si přečíst knihu Michael peří, která **efektivně funguje s použitím starší verze kódu**.

V této iteraci přidáme novou funkci do naší aplikace Správce kontaktů. Přidáváme podporu pro skupiny kontaktů. Skupiny kontaktů můžete použít k uspořádání kontaktů do kategorií, jako jsou obchodní a přítel skupiny.

Tuto novou funkci přidáme do naší aplikace pomocí procesu vývoje řízeného testováním. Nejdřív zapíšeme naše testy jednotek a my zapíšeme veškerý náš kód na tyto testy.

## <a name="what-gets-tested"></a>Co se testuje

Jak jsme probrali v předchozí iteraci, obvykle nepíšete testy jednotek pro logiku přístupu k datům nebo logiku zobrazení. Nebudete zapisovat testy jednotek pro logiku přístupu k datům, protože přístup k databázi je poměrně pomalá operace. Nebudete zapisovat testy jednotek pro zobrazení logiky, protože přístup k zobrazení vyžaduje rozchod webového serveru, který je poměrně pomalý. Nemusíte psát test jednotek, pokud test nemůžete provést znovu a znovu.

Vzhledem k tomu, že vývoj na základě testů je založený na testech jednotek, důrazně se zaměřte na řadič pro zápis a obchodní logiku. Nemůžeme se dotýkat databáze nebo zobrazení. Neupravujte databázi ani nevytvářejte naše zobrazení do konce tohoto kurzu. Začneme s tím, co se dá testovat.

## <a name="creating-user-stories"></a>Vytváření uživatelských scénářů

Při praktickém vývoji na základě testů vždy začněte zápisem testu. Tím se okamžitě vyvolá otázka: jak se rozhodnout, jaký test se má zapsat jako první? K zodpovězení této otázky byste měli napsat sadu [**uživatelských scénářů**](http://en.wikipedia.org/wiki/User_stories).

Uživatelský scénář je velmi krátká (obvykle jedna věta) popis požadavku na software. Měl by to být netechnický popis požadavku napsaného z perspektivy uživatele.

Tady jsou sady uživatelských scénářů, které popisují funkce požadované funkcemi nové skupiny kontaktů:

1. Uživatel může zobrazit seznam skupin kontaktů.
2. Uživatel může vytvořit novou skupinu kontaktů.
3. Uživatel může odstranit existující skupinu kontaktů.
4. Při vytváření nového kontaktu může uživatel vybrat skupinu kontaktů.
5. Uživatel může při úpravě existujícího kontaktu vybrat skupinu kontaktů.
6. V zobrazení index se zobrazí seznam skupin kontaktů.
7. Když uživatel klikne na skupinu kontaktů, zobrazí se seznam vyhovujících kontaktů.

Všimněte si, že tento seznam uživatelských scénářů je u zákazníka zcela srozumitelný. Neexistují žádné zmínky o technických podrobnostech o implementaci.

Při sestavování aplikace může být sada uživatelských scénářů pružnější. Uživatelský scénář můžete rozdělit do několika scénářů (požadavky). Například se můžete rozhodnout, že vytvoření nové skupiny kontaktů by mělo zahrnovat ověřování. Odeslání skupiny kontaktů bez názvu by mělo vrátit chybu ověřování.

Po vytvoření seznamu uživatelských scénářů jste připraveni napsat první test jednotky. Začneme vytvořením testu jednotek pro zobrazení seznamu skupin kontaktů.

## <a name="listing-contact-groups"></a>Výpis skupin kontaktů

Naším prvním uživatelským scénářem je, že by měl být uživatel schopný zobrazit seznam skupin kontaktů. Tento příběh musíme vyjádřit pomocí testu.

Vytvořte nový test jednotky tak, že kliknete pravým tlačítkem na složku Controllers v projektu ContactManager. Tests, vyberete **Přidat, nový test**a vyberete šablonu **testu jednotek** (viz obrázek 1). Pojmenujte nový test jednotek GroupControllerTest.cs a klikněte na tlačítko **OK** .

[![přidání testu jednotek GroupControllerTest](iteration-6-use-test-driven-development-cs/_static/image1.jpg)](iteration-6-use-test-driven-development-cs/_static/image1.png)

**Obrázek 01**: Přidání testu jednotek GroupControllerTest ([kliknutím zobrazíte obrázek v plné velikosti](iteration-6-use-test-driven-development-cs/_static/image2.png))

Náš první test jednotky je obsažen v seznamu 1. Tento test ověří, zda metoda index () řadiče skupiny vrací sadu skupin. Test ověří, že se v zobrazení dat vrátí kolekce skupin.

**Výpis 1 – Controllers\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample1.cs)]

Při prvním zadání kódu v seznamu 1 v aplikaci Visual Studio získáte spoustu červených klikatých čar. Nevytvořili jsme třídy GroupController nebo Group.

V tuto chvíli můžeme dokonce sestavit naši aplikaci, abychom mohli spustit náš první test jednotek. To je dobré. Počítá se jako neúspěšný test. Proto máme oprávnění ke spuštění psaní kódu aplikace. Abychom mohli spustit náš test, musíme napsat dostatečný kód.

Třída řadiče skupiny v seznamu 2 obsahuje minimální kód potřebný k předání testu jednotky. Akce index () vrátí staticky kódovaný seznam skupin (třída skupiny je definována v seznamu 3).

**Výpis 2 – Controllers\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample2.cs)]

**Výpis 3 – Models\Group.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample3.cs)]

Až do našeho projektu přidáme třídy GroupController a Group, náš první test jednotky se úspěšně dokončí (viz obrázek 2). Dokončili jsme minimální práci nutnou k předání testu. Je čas na oslavu.

[![úspěch!](iteration-6-use-test-driven-development-cs/_static/image2.jpg)](iteration-6-use-test-driven-development-cs/_static/image3.png)

**Obrázek 02**: úspěch! ([Kliknutím zobrazíte obrázek v plné velikosti.](iteration-6-use-test-driven-development-cs/_static/image4.png))

## <a name="creating-contact-groups"></a>Vytváření skupin kontaktů

Nyní můžeme přejít k druhému uživatelskému scénáři. Musíme být schopni vytvořit nové skupiny kontaktů. Abychom tento záměr vyjádřili s testem.

Test v seznamu 4 ověřuje, že volání metody Create () s novou skupinou přidá skupinu do seznamu skupin vrácených metodou index (). Jinými slovy, pokud vytvořím novou skupinu, pak by měla být schopna získat novou skupinu zpátky ze seznamu skupin vrácených metodou index ().

**Výpis 4 – Controllers\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample4.cs)]

Test v seznamu 4 volá metodu Create () řadiče skupiny s novou skupinou kontaktů. V dalším kroku test ověří, že voláním metody index řadiče skupiny () vrátí novou skupinu v zobrazení dat.

Změněný řadič skupiny v seznamu 5 obsahuje minimální změny potřebné k předání nového testu.

**Výpis 5 – Controllers\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample5.cs)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a>Řadič skupiny v seznamu 5 má novou akci vytvořit (). Tato akce přidá skupinu do kolekce skupin. Všimněte si, že akce index () byla změněna tak, aby vracela obsah kolekce skupin.

Znovu jsme provedli minimální množství práce potřebné k předání testu jednotky. Až tyto změny provedeme u řadiče skupiny, všechny testy jednotek proběhnou znovu.

## <a name="adding-validation"></a>Přidání ověření

Tento požadavek nebyl výslovně uveden v uživatelském scénáři. Je však vhodné vyžadovat, aby skupina měla název. Jinak organizace kontaktů do skupin nebude velmi užitečná.

Výpis 6 obsahuje nový test, který tento záměr vyjadřuje. Tento test ověřuje, že při pokusu o vytvoření skupiny bez poskytnutí názvu dojde k chybě ověřovací zprávy ve stavu modelu.

**Výpis 6 – Controllers\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample6.cs)]

Aby bylo možné tento test splnit, musíme do třídy skupiny přidat vlastnost Name (viz výpis 7). Kromě toho je potřeba přidat do akce vytvořit () řadiče skupiny nepatrnou bitovou logiku ověřování (viz výpis 8).

**Výpis 7 – Models\Group.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample7.cs)]

**Výpis 8 – Controllers\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample8.cs)]

Všimněte si, že akce vytvořit řadič skupiny () nyní obsahuje ověřování i databázovou logiku. Databáze, kterou používá řadič skupiny, se v současné době skládá z toho, že není nic víc než kolekce v paměti.

## <a name="time-to-refactor"></a>Čas do refaktoru

Třetí krok červené/zelené/refaktoru je refaktorická součást. V tuto chvíli Musíme přejít zpátky z našeho kódu a vzít v úvahu, jak můžeme Refaktorovat naši aplikaci, aby vylepšila její návrh. Refaktoring fáze je fáze, na které si myslíme, že je nejlepší způsob, jak implementovat zásady a vzory návrhu softwaru.

Můžeme upravit náš kód jakýmkoli způsobem, který jsme zvolili pro zlepšení návrhu kódu. Máme bezpečnostní sítě pro testování částí, které nám zabraňují v přerušení stávajících funkcí.

V současné době je náš řadič skupiny v perspektivě dobré softwarového návrhu. Řadič skupiny obsahuje zamotáníou část ověřování a kódu pro přístup k datům. Aby nedošlo k porušení zásady jedné zodpovědnosti, musíme tyto aspekty oddělit do různých tříd.

Naše třída řadiče skupiny refaktoringu je obsažena v seznamu 9. Kontroler byl upraven, aby používal vrstvu služby ContactManager. Jedná se o stejnou vrstvu služby, kterou používáme u kontroleru kontaktů.

Výpis 10 obsahuje nové metody přidané do vrstvy služby ContactManager, které podporují ověřování, výpis a vytváření skupin. Rozhraní IContactManagerService bylo aktualizováno, aby zahrnovalo nové metody.

Výpis 11 obsahuje novou třídu FakeContactManagerRepository, která implementuje rozhraní IContactManagerRepository. Na rozdíl od třídy EntityContactManagerRepository, která také implementuje rozhraní IContactManagerRepository, naše nová třída FakeContactManagerRepository nekomunikuje s databází. Třída FakeContactManagerRepository používá kolekci v paměti jako proxy pro databázi. Tuto třídu použijeme v našich testech jednotek jako na falešnou vrstvu úložiště.

**Výpis 9 – Controllers\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample9.cs)]

**Výpis 10 – Controllers\ContactManagerService.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample10.cs)]

**Výpis 11 – Controllers\FakeContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample11.cs)]

Změna rozhraní IContactManagerRepository vyžaduje použití k implementaci metod Create () a ListGroups () ve třídě EntityContactManagerRepository. Laziest a nejrychlejší způsob, jak to provést, je přidat metody se zástupnými procedurami, které vypadají takto:   

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample12.cs)]

Nakonec tyto změny návrhu naší aplikace vyžadují, abychom provedli některé úpravy našich testů jednotek. Teď je potřeba při provádění testů jednotek používat FakeContactManagerRepository. Aktualizovaná třída GroupControllerTest je obsažena v seznamu 12.

**Výpis 12 – Controllers\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample13.cs)]

Po opětovném provedení všech těchto změn všechny testy jednotek proběhnou znovu. Dokončili jsme celý cyklus červené/zelené/refaktoru. Implementovali jsme první dva uživatelské scénáře. Nyní máme podporu jednotkových testů pro požadavky vyjádřené v uživatelských scénářích. Implementace zbývajících uživatelských scénářů zahrnuje opakování stejného cyklu červené/zelené/refaktoru.

## <a name="modifying-our-database"></a>Úprava naší databáze

Omlouváme se, i když jsme splnili všechny požadavky vyjádřené našimi testy jednotek, ale naše práce se nedokončila. Pořád potřebujeme upravit naši databázi.

Musíme vytvořit novou tabulku databáze skupiny. Postupujte následovně:

1. V okně Průzkumník serveru klikněte pravým tlačítkem myši na složku tabulky a vyberte možnost nabídky **Přidat novou tabulku**.
2. Zadejte dva sloupce popsané níže v Návrháři tabulky.
3. Označte sloupec ID jako primární klíč a sloupec identity.
4. Kliknutím na ikonu této diskety uložte novou tabulku se skupinami názvů.

<a id="0.11_table01"></a>

| **Název sloupce** | **Datový typ** | **Povoluje hodnoty null.** |
| --- | --- | --- |
| ID | int | False |
| Název | nvarchar (50) | False |

Dál musíme odstranit všechna data z tabulky Contacts (jinak nebudeme moct vytvořit relaci mezi tabulkami kontaktů a skupin). Postupujte následovně:

1. Klikněte pravým tlačítkem myši na tabulku kontaktů a vyberte možnost nabídky **Zobrazit data tabulky**.
2. Odstraní všechny řádky.

Dále je potřeba definovat relaci mezi tabulkou databáze skupiny a existující tabulkou databáze kontaktů. Postupujte následovně:

1. Dvojitým kliknutím na tabulku kontaktů v okně Průzkumník serveru otevřete Návrháře tabulky.
2. Přidejte nový sloupec typu Integer do tabulky kontaktů s názvem GroupId.
3. Kliknutím na tlačítko vztah otevřete dialogové okno relace cizího klíče (viz obrázek 3).
4. Klikněte na tlačítko Přidat.
5. Klikněte na tlačítko se třemi tečkami vedle tlačítka specifikace tabulky a sloupců.
6. V dialogovém okně tabulky a sloupce vyberte skupiny jako primární klíč tabulka a ID jako sloupec primárního klíče. Jako sloupec cizího klíče vyberte kontakty jako tabulku cizího klíče (viz obrázek 4). Klikněte na tlačítko OK.
7. V části **Vložit a aktualizovat specifikaci**vyberte **kaskádovou** hodnotu pro **pravidlo odstranit**.
8. Kliknutím na tlačítko Zavřít zavřete dialogové okno relace cizího klíče.
9. Kliknutím na tlačítko Uložit uložte změny v tabulce Contacts.

[![vytvoření relace databázové tabulky](iteration-6-use-test-driven-development-cs/_static/image3.jpg)](iteration-6-use-test-driven-development-cs/_static/image5.png)

**Obrázek 03**: Vytvoření vztahu databázové tabulky ([kliknutím zobrazíte obrázek v plné velikosti](iteration-6-use-test-driven-development-cs/_static/image6.png))

[![určení relací mezi tabulkami](iteration-6-use-test-driven-development-cs/_static/image4.jpg)](iteration-6-use-test-driven-development-cs/_static/image7.png)

**Obrázek 04**: zadání relací mezi tabulkami ([kliknutím zobrazíte obrázek v plné velikosti](iteration-6-use-test-driven-development-cs/_static/image8.png))

### <a name="updating-our-data-model"></a>Aktualizuje se náš datový model.

Dál je potřeba aktualizovat náš datový model tak, aby představoval novou databázovou tabulku. Postupujte následovně:

1. Dvojím kliknutím na soubor ContactManagerModel. edmx ve složce modely otevřete Entity Designer.
2. Klikněte pravým tlačítkem myši na plochu návrháře a vyberte možnost nabídky **aktualizovat model z databáze**.
3. V Průvodci aktualizací vyberte tabulku skupiny a klikněte na tlačítko Dokončit (viz obrázek 5).
4. Klikněte pravým tlačítkem na entitu skupiny a vyberte možnost nabídky **Přejmenovat**. Změňte název entity *Groups* na *Group* (jednotné).
5. Klikněte pravým tlačítkem na navigační vlastnost skupiny, která se zobrazí v dolní části entity kontakt. Změňte název *skupiny* navigační vlastnost na *Group* (jednotné).

[![aktualizace modelu Entity Framework z databáze](iteration-6-use-test-driven-development-cs/_static/image5.jpg)](iteration-6-use-test-driven-development-cs/_static/image9.png)

**Obrázek 05**: aktualizace modelu Entity Framework z databáze ([kliknutím zobrazíte obrázek v plné velikosti](iteration-6-use-test-driven-development-cs/_static/image10.png))

Po dokončení tohoto postupu bude datový model představovat tabulky kontaktů a skupin. Entity Designer by měl zobrazovat obě entity (viz obrázek 6).

[![Entity Designer zobrazování skupin a kontaktů](iteration-6-use-test-driven-development-cs/_static/image6.jpg)](iteration-6-use-test-driven-development-cs/_static/image11.png)

**Obrázek 6**: Entity Designer zobrazení skupiny a kontaktu ([kliknutím zobrazíte obrázek v plné velikosti](iteration-6-use-test-driven-development-cs/_static/image12.png))

### <a name="creating-our-repository-classes"></a>Vytváření tříd úložišť

Dál musíme implementovat naši třídu úložiště. V průběhu této iterace jsme do rozhraní IContactManagerRepository přidali několik nových metod při psaní kódu pro splnění našich testů jednotek. Konečná verze rozhraní IContactManagerRepository je obsažena v seznamu 14.

**Výpis 14 – Models\IContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample14.cs)]

Neimplementovali jsme žádnou z metod, které se týkají práce se skupinami kontaktů. V současné době má třída EntityContactManagerRepository zástupné procedury pro každou metodu skupiny kontaktů uvedenou v rozhraní IContactManagerRepository. Například metoda ListGroups () v tuto chvíli vypadá takto:

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample15.cs)]

Metody zástupné procedury nám umožnily kompilovat naši aplikaci a předávat testy jednotek. Nyní je však čas na to, aby tyto metody byly skutečně implementovány. Konečná verze třídy EntityContactManagerRepository je obsažena v seznamu 13.

**Výpis 13 – Models\EntityContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample16.cs)]

### <a name="creating-the-views"></a>Vytváření zobrazení

ASP.NET aplikace MVC při použití výchozího modulu zobrazení ASP.NET. Takže nebudete vytvářet zobrazení v reakci na určitý test jednotek. Vzhledem k tomu, že by byla aplikace nepoužitelná bez zobrazení, můžeme tuto iteraci dokončit bez vytváření a úprav zobrazení obsažených v aplikaci Správce kontaktů.

Pro správu skupin kontaktů musíme vytvořit následující nová zobrazení (viz obrázek 7):

- Views\Group\Index.aspx – zobrazí seznam skupin kontaktů.
- Views\Group\Delete.aspx – zobrazí potvrzovací formulář pro odstranění skupiny kontaktů.

[![zobrazení index skupiny](iteration-6-use-test-driven-development-cs/_static/image7.jpg)](iteration-6-use-test-driven-development-cs/_static/image13.png)

**Obrázek 07**: zobrazení index skupiny ([kliknutím zobrazíte obrázek v plné velikosti](iteration-6-use-test-driven-development-cs/_static/image14.png))

Musíme upravit následující existující zobrazení tak, aby zahrnovala skupiny kontaktů:

- Views\Home\Create.aspx
- Views\Home\Edit.aspx
- Views\Home\Index.aspx

Upravená zobrazení si můžete prohlédnout v aplikaci Visual Studio, která doprovází tento kurz. Například obrázek 8 znázorňuje zobrazení indexu kontaktu.

[![zobrazení indexu kontaktu](iteration-6-use-test-driven-development-cs/_static/image8.jpg)](iteration-6-use-test-driven-development-cs/_static/image15.png)

**Obrázek 08**: Zobrazení indexu kontaktů ([kliknutím zobrazíte obrázek v plné velikosti](iteration-6-use-test-driven-development-cs/_static/image16.png))

## <a name="summary"></a>Souhrn

V této iteraci jsme do naší aplikace Správce kontaktů přidali novou funkčnost pomocí metodologie návrhu vývojové aplikace řízené testem. Začali jsme vytvořením sady uživatelských scénářů. Vytvořili jsme sadu testů jednotek, které odpovídají požadavkům vyjádřeným uživatelskými příběhy. Nakonec jsme napsali dostatečný kód pro splnění požadavků, které vyjadřují testy jednotek.

Po dokončení zápisu dostatečného kódu pro splnění požadavků, které jsou vyjádřeny testy jednotek, jsme aktualizovali naši databázi a zobrazení. Do naší databáze jsme přidali novou tabulku skupin a aktualizovali jsme náš Entity Framework datový model. Také jsme vytvořili a upravili sadu zobrazení.

V další iteraci – finální iterací – přepište naši aplikaci, aby využila AJAX. Když využijete technologii AJAX, vylepšit rychlost odezvy a výkon aplikace Správce kontaktů.

> [!div class="step-by-step"]
> [Předchozí](iteration-5-create-unit-tests-cs.md)
> [Další](iteration-7-add-ajax-functionality-cs.md)
