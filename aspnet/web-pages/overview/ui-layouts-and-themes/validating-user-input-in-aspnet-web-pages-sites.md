---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: Ověřování vstupu uživatele v lokalitách ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tento článek popisuje, jak ověřit informace, které získáte od uživatelů &mdash;, abyste se ujistili, že uživatelé zadávají platné informace ve formulářích HTML v...
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: e6f8e1051d09d11f1756bfada44a73ba7c2a1db2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563502"
---
# <a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a>Ověřování vstupu uživatele na webech ASP.NET Web Pages (Razor)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek popisuje, jak ověřit informace, které dostanete od uživatelů &mdash;, aby se zajistilo, že uživatelé zadávají platné informace ve formulářích HTML na webu ASP.NET Web Pages (Razor).
> 
> Naučíte se:
> 
> - Jak ověřit, jestli vstup uživatele odpovídá ověřovacím kritériím, která definujete.
> - Jak určit, zda všechny ověřovací testy prošly.
> - Jak zobrazit chyby ověřování (a jak je naformátovat).
> - Ověření dat, která nepřicházejí přímo od uživatelů
> 
> Toto jsou koncepty programování ASP.NET představené v článku:
> 
> - Pomocná rutina `Validation`
> - Metody `Html.ValidationSummary` a `Html.ValidationMessage`.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 3
>   
> 
> Tento kurz funguje také s ASP.NET webovými stránkami 2.

Tento článek obsahuje následující oddíly:

- [Přehled ověřování vstupu uživatele](#Overview_of_User_Input_Validation)
- [Ověřování vstupu uživatele](#Validating_User_Input)
- [Přidání ověřování na straně klienta](#Adding_Client-Side_Validation)
- [Chyby ověřování formátování](#Formatting_Validation_Errors)
- [Ověřování dat, která nepřicházejí přímo od uživatelů](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a>Přehled ověřování vstupu uživatele

Pokud požádáte uživatele, aby zadali informace na stránce, například do formuláře, je důležité se ujistit, že hodnoty, které vstoupí, jsou platné. Nechcete například zpracovat formulář, který neobsahuje důležité informace.

Když uživatelé zadávají hodnoty do formuláře HTML, hodnoty, které vstupují, jsou řetězce. V mnoha případech jsou hodnoty, které potřebujete, některými jinými datovými typy, jako jsou celá čísla nebo kalendářní data. Proto musíte také zajistit, aby hodnoty, které uživatel zadal, mohly být správně převedeny na příslušné datové typy.

U těchto hodnot můžete mít také určitá omezení. I když uživatelé správně zadají celé číslo, může být třeba se ujistit, že hodnota spadá do určitého rozsahu.

![Chyby ověřování, které používají třídy stylů CSS](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> **Důležité** informace Ověřování vstupu uživatele je také důležité pro zabezpečení. Pokud omezíte hodnoty, které mohou uživatelé zadat do formulářů, snížíte pravděpodobnost, že může někdo zadat hodnotu, která může ohrozit zabezpečení vašeho webu.

<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a>Ověřování vstupu uživatele

V ASP.NET webové stránky 2 můžete použít pomocníka `Validator` pro testování vstupu uživatele. Základní postup je následující:

1. Určete, které vstupní prvky (pole) chcete ověřit.

    Hodnoty jsou obvykle ověřeny ve `<input>` prvky ve formuláři. Je však dobrým zvykem ověřit všechny vstupy, dokonce i vstupy, které pocházejí z omezeného prvku, jako je například seznam `<select>`. To pomáhá zajistit, že uživatelé neobejde ovládací prvky na stránce a odešlou formulář.
2. V kódu stránky přidejte jednotlivé kontroly ověřování pro každý element input pomocí metod pomocné rutiny `Validation`.

    Chcete-li vyhledat požadovaná pole, použijte `Validation.RequireField(field, [error message])` (pro jednotlivá pole) nebo `Validation.RequireFields(field1, field2, ...))` (pro seznam polí). Pro jiné typy ověřování použijte `Validation.Add(field, ValidationType)`. Pro `ValidationType`můžete použít tyto možnosti:

    `Validator.DateTime ([error message])`  
   `Validator.Decimal([error message])`  
   `Validator.EqualsTo(otherField [, error message])`  
   `Validator.Float([error message])`  
   `Validator.Integer([error message])`  
   `Validator.Range(min, max [, error message])`  
   `Validator.RegEx(pattern [, error message])`  
   `Validator.Required([error message])`  
   `Validator.StringLength(length)`  
   `Validator.Url([error message])`
3. Po odeslání stránky ověřte, zda ověření proběhlo zaškrtnutím `Validation.IsValid`:

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    Pokud dojde k chybám ověřování, přeskočíte normální zpracování stránky. Například pokud účelem stránky je aktualizovat databázi, neuděláte to, dokud nebudou opraveny všechny chyby ověřování.
4. Pokud dojde k chybám ověření, zobrazí se chybové zprávy v kódu stránky pomocí `Html.ValidationSummary` nebo `Html.ValidationMessage`nebo obojího.

Následující příklad ukazuje stránku, která znázorňuje tyto kroky.

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

Pokud chcete zjistit, jak ověřování funguje, spusťte tuto stránku a záměrně udělejte chyby. Tady je příklad, jak stránka vypadá, když zapomenete zadat název kurzu, pokud zadáte a zadáte neplatné datum:

![Chyby ověřování na vykreslené stránce](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a>Přidání ověřování na straně klienta

Ve výchozím nastavení se uživatelský vstup ověří poté, co uživatel stránku odešle – to znamená, že ověření proběhne v kódu serveru. Nevýhodou tohoto přístupu je, že uživatelé nevědí, že udělali chybu až po odeslání stránky. V případě, že je formulář dlouhý nebo složitý, mohou být chyby zasílání zpráv pouze po odeslání stránky pro uživatele nepohodlné.

Můžete přidat podporu, která provádí ověřování v klientském skriptu. V takovém případě se ověřování provádí, protože uživatelé pracují v prohlížeči. Předpokládejme například, že zadáte, že hodnota by měla být celé číslo. Pokud uživatel zadá hodnotu, která není celočíselná, zobrazí se chyba, jakmile uživatel opustí pole pro zadání. Uživatelé získají okamžitou zpětnou vazbu, která je pro ně vhodná. Ověřování na základě klienta může také snížit počet pokusů, které uživatel musí odeslat formuláři, aby opravil více chyb.

> [!NOTE]
> I když používáte ověřování na straně klienta, ověřování se vždy provádí také v kódu serveru. Ověřování v kódu serveru je bezpečnostní opatření pro případ, že uživatelé obcházejí ověřování na základě klienta.

1. Zaregistrujte následující knihovny JavaScriptu na stránce:  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

   Dvě knihovny jsou spustitelný ze služby Content Delivery Network (CDN), takže je nemusíte nutně mít na počítači nebo na serveru. Je však nutné mít místní kopii *jQuery. Validate. nenáročná. js*. Pokud ještě nepracujete se šablonou WebMatrix (jako je **startovní web** ), která obsahuje knihovnu, vytvořte web webové stránky, který je založen na **počátečním webu**. Pak zkopírujte soubor *. js* na aktuální web.
2. V označení pro každý prvek, který budete ověřovat, přidejte volání `Validation.For(field)`. Tato metoda generuje atributy, které se používají při ověřování na straně klienta. (Místo toho, aby vygeneroval skutečný kód JavaScriptu, metoda vygeneruje atributy jako `data-val-...`. Tyto atributy podporují nenápadné ověření klienta, které používá jQuery k provedení práce.)

Následující stránka ukazuje, jak přidat funkce ověřování klientů do výše uvedeného příkladu.

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample4.cshtml?highlight=35-39,51,61,71)]

Ne všechny ověřovací kontroly jsou spuštěny na klientovi. Konkrétně ověřování typu dat (celé číslo, datum atd.) neběží na klientovi. Následující kontroly fungují na straně klienta i serveru:

- `Required`
- `Range(minValue, maxValue)`
- `StringLength(maxLength[, minLength])`
- `Regex(pattern)`
- `EqualsTo(otherField)`

V tomto příkladu test pro platné datum nebude fungovat v klientském kódu. Test se ale provede v kódu serveru.

<a id="Formatting_Validation_Errors"></a>
## <a name="formatting-validation-errors"></a>Chyby ověřování formátování

Můžete řídit, jak se zobrazují chyby ověřování tím, že definujete třídy CSS, které mají následující rezervované názvy:

- `field-validation-error`. Definuje výstup metody `Html.ValidationMessage`, když se zobrazuje chyba.
- `field-validation-valid`. Definuje výstup metody `Html.ValidationMessage`, pokud není k dispozici žádná chyba.
- `input-validation-error`. Definuje, jak se vykreslují prvky `<input>`, když dojde k chybě. (Například můžete použít tuto třídu k nastavení barvy pozadí &lt;vstupní&gt; elementu na jinou barvu, je-li její hodnota neplatná.) Tato třída CSS se používá pouze během ověřování klienta (na webových stránkách ASP.NET 2).
- `input-validation-valid`. Definuje vzhled `<input>` prvků v případě, že není k dispozici žádná chyba.
- `validation-summary-errors`. Definuje výstup metody `Html.ValidationSummary` zobrazuje seznam chyb.
- `validation-summary-valid`. Definuje výstup metody `Html.ValidationSummary`, pokud není k dispozici žádná chyba.

Následující blok `<style>` obsahuje pravidla pro chybové podmínky.

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

Pokud tento blok stylu zadáte na vzorových stránkách výše v článku, zobrazí se chyba, která bude vypadat jako na následujícím obrázku:

![Chyby ověřování, které používají třídy stylů CSS](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> Pokud nepoužíváte ověřování klienta v ASP.NET webové stránky 2, třídy CSS pro prvky `<input>` (`input-validation-error` a `input-validation-valid` nemají žádný vliv.

### <a name="static-and-dynamic-error-display"></a>Zobrazení statické a dynamické chyby

Pravidla šablony stylů CSS jsou uvedena ve dvojicích, například `validation-summary-errors` a `validation-summary-valid`. Tyto páry umožňují definovat pravidla pro obě podmínky: chybový stav a podmínku "normální" (nejedná se o chyba). Je důležité pochopit, že značky pro zobrazení chyb jsou vždy vykresleny, i když nejsou k dispozici žádné chyby. Například pokud má stránka jako metodu `Html.ValidationSummary` v kódu, bude zdroj stránky obsahovat následující kód, i když je stránka vyžadovaná poprvé:

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

Jinými slovy, metoda `Html.ValidationSummary` vždy vykresluje `<div>` prvek a seznam, a to i v případě, že seznam chyb je prázdný. Podobně metoda `Html.ValidationMessage` vždy vykresluje `<span>` prvek jako zástupný symbol pro chybu jednotlivých polí, a to i v případě, že nedošlo k chybě.

V některých situacích může zobrazování chybové zprávy způsobit přetečení stránky a může způsobit, že se prvky na stránce pohybují. Pravidla šablony stylů CSS, která končí `-valid` umožňují definovat rozložení, které vám může zabránit tomuto problému. Můžete například definovat `field-validation-error` a `field-validation-valid` mají stejnou pevnou velikost. Tímto způsobem je oblast zobrazení pro pole statická a při zobrazení chybové zprávy se tok stránky nezmění.

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a>Ověřování dat, která nepřicházejí přímo od uživatelů

Někdy je nutné ověřit informace, které nepocházejí přímo z formuláře HTML. Typickým příkladem je stránka, kde je hodnota předána v řetězci dotazu, jako v následujícím příkladu:

`http://server/myapp/EditClassInformation?classid=1022`

V takovém případě se chcete ujistit, že hodnota, která je předána stránce (zde 1022 pro hodnotu `classid`), je platná. K provedení tohoto ověřování nemůžete přímo použít pomocníka `Validation`. Můžete však použít jiné funkce systému ověřování, například možnost zobrazit chybové zprávy ověřování.

> [!NOTE] 
> 
> **Důležité** informace Vždy ověří hodnoty, které získáte z *libovolného* zdroje, včetně hodnot polí formuláře, hodnot řetězce dotazu a hodnot souborů cookie. Lidé můžou tyto hodnoty změnit (třeba pro škodlivé účely). Aby bylo možné aplikaci chránit, je nutné tyto hodnoty ověřit.

Následující příklad ukazuje, jak můžete ověřit hodnotu, která je předána do řetězce dotazu. Kód testuje, že hodnota není prázdná a že se jedná o celé číslo.

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

Všimněte si, že test je proveden, pokud žádost není odesláním formuláře (`if(!IsPost)`). Tento test by byl splněn při prvním vyžádání stránky, ale ne v případě, kdy je žádost odeslána formuláři.

Chcete-li zobrazit tuto chybu, můžete přidat chybu do seznamu chyb ověřování voláním `Validation.AddFormError("message")`. Pokud stránka obsahuje volání metody `Html.ValidationSummary`, zobrazí se chyba podobně jako při ověřování vstupu uživatele.

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>Další prostředky

[Práce s formuláři HTML na webech webových stránek ASP.NET](https://go.microsoft.com/fwlink/?LinkID=202892)
