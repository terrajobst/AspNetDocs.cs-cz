---
uid: web-pages/overview/testing-and-debugging/introduction-to-debugging
title: Úvod do ladění webů ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Ladění je proces vyhledávání a odstraňování chyb na vašich kódových stránkách. V této kapitole se dozvíte o některých nástrojích a technikách, které můžete použít k ladění a Analyz...
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 68de4326-7611-4b9b-b5f6-79b7adc3069f
msc.legacyurl: /web-pages/overview/testing-and-debugging/introduction-to-debugging
msc.type: authoredcontent
ms.openlocfilehash: ae7d871e56326610c043dc20fe6e0919e1b4ac89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624367"
---
# <a name="introduction-to-debugging-aspnet-web-pages-razor-sites"></a>Úvod do ladění webů ASP.NET Web Pages (Razor)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek popisuje různé způsoby, jak ladit stránky na webu ASP.NET Web Pages (Razor). Ladění je proces vyhledávání a odstraňování chyb na vašich kódových stránkách.
>
> **Co se naučíte:**
>
> - Jak zobrazit informace, které pomáhají analyzovat a ladit stránky.
> - Jak používat ladicí nástroje v aplikaci Visual Studio.
>
>
> Jedná se o funkce ASP.NET, které jsou představené v článku:
>
> - Pomocná rutina `ServerInfo`
> - Pomocná `ObjectInfo`
>
>
> ## <a name="software-versions"></a>Verze softwaru
>
>
> - Webové stránky ASP.NET (Razor) 3
> - Visual Studio 2013
>
>
> Tento kurz funguje také s ASP.NET webovými stránkami 2. Můžete použít WebMatrix 3, ale integrovaný ladicí program není podporován.

Důležitým aspektem potíží s chybami a problémy v kódu je vyhnout se tomu na prvním místě. To lze provést tak, že zadáte části kódu, které mohou způsobit chyby v `try/catch` blocích. Další informace najdete v části týkající se zpracování chyb v [úvodu do ASP.NET webového programování pomocí syntaxe Razor](https://go.microsoft.com/fwlink/?LinkId=202890).

Pomocník pro `ServerInfo` je diagnostický nástroj, který poskytuje přehled informací o prostředí webového serveru, které je hostitelem vaší stránky. Zobrazuje také informace o požadavcích HTTP, které jsou odeslány, když prohlížeč požaduje stránku. Pomocná rutina `ServerInfo` zobrazí aktuální identitu uživatele, typ prohlížeče, který požadavek odeslal, a tak dále. Tento druh informací vám může pomoct při řešení běžných problémů.

1. Vytvořte novou webovou stránku s názvem *serverinfo. cshtml*.
2. Na konci stránky těsně před uzavírací značku `</body>` přidejte `@ServerInfo.GetHtml()`:

    [!code-cshtml[Main](introduction-to-debugging/samples/sample1.cshtml)]

    Kód `ServerInfo` můžete přidat kdekoli na stránce. Ale při jeho přidání na konci zůstane výstup oddělený od dalšího obsahu stránky, což usnadňuje čtení.

    > [!NOTE]
    >
    > **Důležité** informace Před přesunutím webových stránek na provozní server byste měli odebrat veškerý diagnostický kód z webových stránek. To platí pro pomocnou nápovědu `ServerInfo` a také pro další diagnostické techniky v tomto článku, které zahrnují přidávání kódu na stránku. Nechcete, aby návštěvníci webu viděli informace o názvu serveru, uživatelských jménech, cestách na serveru a podobných podrobnostech, protože tento typ informací může být užitečný pro lidi se škodlivým záměrem.
3. Uložte stránku a spusťte ji v prohlížeči.

    ![Ladění – 1](introduction-to-debugging/_static/image1.jpg)

    Pomocník pro `ServerInfo` zobrazí na stránce čtyři tabulky s informacemi:

   - Konfigurace serveru. Tato část obsahuje informace o hostujícím webovém serveru, včetně názvu počítače, verze ASP.NET, kterou používáte, názvu domény a času serveru.
   - Proměnné serveru ASP.NET V této části najdete podrobné informace o mnoha podrobnostech protokolu HTTP (nazývaných proměnné HTTP) a hodnotách, které jsou součástí jednotlivých požadavků na webovou stránku.
   - Informace o běhu HTTP. V této části najdete podrobné informace o verzi Microsoft .NET Framework, pod kterou běží vaše webová stránka, o cestě, podrobnostech o mezipaměti atd. (Jak jste se naučili v [úvodu k webovému programování v ASP.NET pomocí syntaxe Razor](https://go.microsoft.com/fwlink/?LinkId=202890), webové stránky ASP.NET, které používají syntaxe Razor, jsou postavené na technologii ASP.NET webového serveru společnosti Microsoft, která je sama o sobě postavená na obsáhlé knihovně pro vývoj softwaru nazvané .NET Framework.)
   - Proměnné prostředí. V této části najdete seznam všech proměnných místního prostředí a jejich hodnot na webovém serveru.

     Úplný popis všech informací o serveru a požadavku je nad rámec tohoto článku, ale vidíte, že pomocník pro `ServerInfo` vrátí spoustu diagnostických informací. Další informace o hodnotách, které `ServerInfo` vrací, najdete v tématu [rozpoznané proměnné prostředí](https://technet.microsoft.com/library/dd560744(WS.10).aspx) na webu Microsoft TechNet a v [proměnných serveru služby IIS](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) na webu MSDN.

## <a name="embedding-output-expressions-to-display-page-values"></a>Vložení výstupních výrazů pro zobrazení hodnot stránky

Dalším způsobem, jak zjistit, co se děje ve vašem kódu, je vložit výstupní výrazy na stránku. Jak víte, můžete přímo vytvořit výstup hodnoty proměnné tak, že na stránku přidáte něco jako `@myVariable` nebo `@(subTotal * 12)`. Pro ladění můžete tyto výrazy výstupu umístit do strategických bodů v kódu. To vám umožní zobrazit hodnotu klíčových proměnných nebo výsledek výpočtů při spuštění stránky. Až budete hotovi s laděním, můžete odebrat výrazy nebo je opatřit poznámkami. Tento postup znázorňuje typický způsob, jak použít vložené výrazy, které vám pomůžou ladit stránku.

1. Vytvořte novou stránku WebMatrix s názvem *OutputExpression. cshtml*.
2. Obsah stránky nahraďte následujícím:

    [!code-html[Main](introduction-to-debugging/samples/sample2.html)]

    V příkladu se používá příkaz `switch` pro kontrolu hodnoty `weekday` proměnné a poté zobrazení jiné výstupní zprávy v závislosti na dnu dne v týdnu. V příkladu blok `if` v rámci prvního bloku kódu libovolně změní den v týdnu přidáním jednoho dne do aktuální hodnoty v týdnu. Toto je chyba zavedená pro ilustraci.
3. Uložte stránku a spusťte ji v prohlížeči.

    Na stránce se zobrazí zpráva pro nesprávný den v týdnu. Libovolný den v týdnu, ve kterém se ve skutečnosti zobrazuje, zobrazí se zpráva po dobu jednoho dne později. I když v tomto případě víte, proč je zpráva vypnutá (vzhledem k tomu, že kód záměrně nastaví nesprávnou hodnotu dne), je v realitě často obtížné zjistit, kde v kódu dochází k chybám. Chcete-li ladit, je třeba zjistit, co se děje s hodnotou klíčových objektů a proměnných, jako je například `weekday`.
4. Přidejte výstupní výrazy vložením `@weekday`, jak je znázorněno na dvou místech označených komentáři v kódu. Tyto výrazy výstupu zobrazí hodnoty proměnné v tomto okamžiku při provádění kódu.

    [!code-csharp[Main](introduction-to-debugging/samples/sample3.cs?highlight=2-3,15-16)]
5. Uložte a spusťte stránku v prohlížeči.

    Stránka zobrazuje první den v týdnu, potom aktualizovaný den v týdnu, který je výsledkem přidání jednoho dne a pak výslednou zprávu z příkazu `switch`. Výstup ze dvou výrazů proměnné (`@weekday`) nemá žádné mezery mezi dny, protože jste do výstupu nepřidali žádné značky `<p>` HTML. výrazy jsou pouze pro testování.

    ![Ladění – 2](introduction-to-debugging/_static/image2.jpg)

    Teď vidíte, kde se chyba nachází. Při prvním zobrazení `weekday` proměnné v kódu se zobrazuje správný den. Když ho zobrazíte podruhé, po `if` bloku v kódu, den je od jednoho. Takže víte, že mezi prvním a druhým vzhledem k proměnné pracovního dne došlo k nějakému problému. Pokud se jednalo o skutečnou chybu, tento druh přístupu vám může přispět k zúžení umístění kódu, který způsobuje problém.
6. Opravte kód na stránce odebráním dvou výstupních výrazů, které jste přidali, a odebráním kódu, který změní den v týdnu. Zbývající, úplný blok kódu vypadá jako v následujícím příkladu:

    [!code-cshtml[Main](introduction-to-debugging/samples/sample4.cshtml)]
7. Spusťte stránku v prohlížeči. Tentokrát se zobrazí správná zpráva pro skutečný den v týdnu.

## <a name="using-the-objectinfo-helper-to-display-object-values"></a>Použití pomocníka ObjectInfo k zobrazení hodnot objektu

Pomocník `ObjectInfo` zobrazí typ a hodnotu každého objektu, který do něj předáte. Můžete ji použít k zobrazení hodnoty proměnných a objektů v kódu (stejně jako u výstupních výrazů v předchozím příkladu), a navíc můžete zobrazit informace o datovém typu objektu.

1. Otevřete soubor s názvem *OutputExpression. cshtml* , který jste vytvořili dříve.
2. Nahraďte veškerý kód na stránce následujícím blokem kódu:

    [!code-html[Main](introduction-to-debugging/samples/sample5.html)]
3. Uložte a spusťte stránku v prohlížeči.

    ![Ladění – 4](introduction-to-debugging/_static/image3.jpg)

    V tomto příkladu pomocník `ObjectInfo` zobrazí dvě položky:

   - Typ Pro první proměnnou je typ `DayOfWeek`. Pro druhou proměnnou je typ `String`.
   - Hodnota V takovém případě, protože již na stránce je zobrazena hodnota proměnné pozdravu, hodnota se zobrazí znovu, když předáte proměnnou do `ObjectInfo`.

     U složitějších objektů může pomocník pro `ObjectInfo` Zobrazit více informací &#8212; v podstatě, může zobrazit typy a hodnoty všech vlastností objektu.

## <a name="using-debugging-tools-in-visual-studio"></a>Používání ladicích nástrojů v aplikaci Visual Studio

Pro komplexnější prostředí ladění použijte [Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017). V sadě Visual Studio můžete nastavit zarážku v kódu na řádku, který chcete zkontrolovat.

![Nastavit zarážku](introduction-to-debugging/_static/image1.png)

Při testování webu je spuštěný Kód zastaven na zarážce.

![dosažení zarážky](introduction-to-debugging/_static/image2.png)

Můžete kontrolovat aktuální hodnoty proměnných a krokovat kód řádek po řádku.

![Zobrazit hodnoty](introduction-to-debugging/_static/image3.png)

Informace o použití integrovaného ladicího programu v aplikaci Visual Studio k ladění stránek ASP.NET Razor naleznete v tématu [Programming ASP.NET Web Pages (Razor) pomocí sady Visual Studio](https://go.microsoft.com/fwlink/?LinkId=205854).

## <a name="additional-resources"></a>Další prostředky

- [Programování webových stránek ASP.NET (Razor) pomocí sady Visual Studio](https://go.microsoft.com/fwlink/?LinkId=205854)
- [Serverové proměnné IIS](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) (MSDN)
- [Rozpoznané proměnné prostředí](https://technet.microsoft.com/library/dd560744(WS.10).aspx) (TechNet)
