---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Programování webových stránek ASP.NET (Razor) pomocí sady Visual Studio | Microsoft Docs
author: Rick-Anderson
description: V tomto dodatku se dozvíte, jak můžete pomocí syntaxe Razor použít Visual Studio 2010 nebo Visual Web Developer 2010 Express k programování webových stránek ASP.NET.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 1a76098779d05912bf7bdf2de5fdce024770752c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78633509"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a>Programování webových stránek ASP.NET (Razor) pomocí sady Visual Studio

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek vysvětluje, jak můžete použít aplikaci Visual Studio nebo Visual Web Developer Express k programování webů ASP.NET Web Pages (Razor).
>
> Co se dozvíte
>
> - Co je potřeba nainstalovat (Pokud cokoli) pro práci s ASP.NET webovými stránkami ve vaší verzi sady Visual Studio.
> - Přidání podpory pro webové stránky ASP.NET do aplikace Visual Web Developer 2010 Express.
> - Jak používat funkce v aplikaci Visual Studio pro práci se stránkami ASP.NET Razor, včetně IntelliSense a ladicího programu.
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
>
>
> - Webové stránky ASP.NET (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>
>
> Tento kurz funguje také s ASP.NET webovými stránkami 2, Visual Studio 2012, Visual Studio 2010 a WebMatrix 2.

ASP.NET webové syntaxe Razor stránky můžete programovat pomocí WebMatrixu nebo mnoha dalších editorů kódu. Můžete také použít Microsoft Visual Studio, což je integrované vývojové prostředí (IDE), které poskytuje výkonnou sadu nástrojů pro vytváření mnoha typů aplikací (nikoli jenom webů). Chcete-li pracovat se ASP.NET Razor Pages, můžete použít [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).

Dvě užitečné funkce, které Visual Studio poskytuje pro programování s webovými stránkami ASP.NET Razor, jsou tyto:

- *IntelliSense*. Funkce IntelliSense integrovaná do sady Visual Studio je komplexnější než IntelliSense ve WebMatrixu.
- *Ladicí program*. Ladicí program vám umožní vyřešit potíže s kódem zastavením programu, který je spuštěný, prozkoumáním proměnných a krokování kódem řádek po řádku.

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a>Použití sady Visual Studio s různými verzemi ASP.NET webových stránek

Chcete-li vyvíjet webové aplikace v ASP.NET v aplikaci Visual Studio 2017, nainstalujte úlohu **vývoje ASP.NET a webu** .

Visual Studio 2012 a Visual Studio 2013 zahrnují podporu pro webové stránky ASP.NET. (Balíčky, které jsou nutné k podpoře webových stránek ASP.NET, se instalují při instalaci sady Visual Studio.)

Visual Studio 2010 ve výchozím nastavení neobsahuje podporu pro webové stránky ASP.NET. Chcete-li používat webové stránky ASP.NET se sadou Visual Studio 2010, je nutné nainstalovat balíček ASP.NET MVC. Pokud chcete získat ASP.NET webové stránky 2, nainstalujte ASP.NET MVC 4.

Následující tabulka shrnuje podporu pro webové stránky ASP.NET v různých verzích sady Visual Studio.

|  | Visual Studio 2010 | Visual Studio 2012 | Visual Studio 2013 |
| --- | --- | --- | --- |
| **ASP.NET webové stránky 2** | Instalace ASP.NET MVC 4 | Obsaženy | Obsaženy |
| **Webové stránky ASP.NET 3** |  | Aktualizace na ASP.NET webové stránky 3 přes NuGet | Obsaženy |

Chcete-li pracovat se sadou Visual Studio 2010, přečtěte si téma [Instalace podpory pro webové stránky ASP.NET v aplikaci Visual studio 2010](#vs2010support).

## <a name="launching-visual-studio-from-webmatrix"></a>Spouští se Visual Studio z WebMatrixu.

Pokud jste spustili projekt ve WebMatrixu a chcete přepnout na Visual Studio, WebMatrix poskytuje tlačítko pro snadné otevření projektu v aplikaci Visual Studio. Aby bylo toto tlačítko povoleno, je nutné mít v počítači nainstalovánu aplikaci Visual Studio. Na následujícím obrázku je znázorněno tlačítko v WebMatrixu.

![Spustit Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

Po kliknutí na tlačítko se projekt otevře v aplikaci Visual Studio. Můžete přepínat mezi webmaticí a Visual Studio bez problémů. Budete upozorněni, pokud se některé soubory změnily v jiném prostředí a potřebujete je znovu načíst, abyste získali nejnovější změny.

## <a name="creating-aspnet-razor-site-in-visual-studio"></a>Vytvoření webu ASP.NET Razor v aplikaci Visual Studio

Vytvoření webu ASP.NET Razor v aplikaci Visual Studio:

1. Otevřete sadu Visual Studio.
2. V nabídce **soubor** klikněte na příkaz **Nový web**.

    ![vytvořit nový web](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. V dialogovém okně **Nový web** vyberte jazyk, který chcete použít (vizuál C# nebo Visual Basic).
4. Vyberte šablonu **web web ASP.NET (Razor)** .

    ![Web Razor](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. Klikněte na tlačítko **OK**.

Nový projekt existuje a je naplněný s některými výchozími webovými stránkami, které vám pomůžou začít.

### <a name="using-intellisense"></a>Používání atributu IntelliSense

Teď, když jste vytvořili lokalitu, uvidíte, jak funguje technologie IntelliSense v sadě Visual Studio.

1. Na webu, který jste právě vytvořili, otevřete stránku *Default. cshtml* .
2. Po `<h3>` značek na stránce zadejte `@ServerInfo.` (včetně tečky). Všimněte si, jak IntelliSense zobrazuje dostupné metody pro pomoc `ServerInfo` v rozevíracím seznamu.

    ![IntelliSense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. V seznamu vyberte metodu `GetHtml` a stiskněte klávesu ENTER. Technologie IntelliSense automaticky vyplní metodu. (Stejně jako u libovolné metody C#v, je nutné přidat `()` znaků za metodou.) Dokončený kód pro metodu `GetHtml` vypadá jako v následujícím příkladu:

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. Stisknutím kombinace kláves CTRL + F5 stránku spusťte. Tato stránka vypadá jako při zobrazení v prohlížeči:

    ![Výchozí stránka v prohlížeči](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. Zavřete prohlížeč.

### <a name="using-the-debugger"></a>Použití ladicího programu

1. V horní části stránky *Default. cshtml* za řádek, který začíná na `Page.Title`, přidejte následující řádek kódu:

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. V levém okraji editoru nalevo od kódu klikněte na tlačítko Další na tento nový řádek, aby bylo možné přidat *zarážku*. Zarážka je značka, která instruuje ladicí program, aby zastavil běh programu v tomto okamžiku, abyste viděli, co se děje.

    ![Nastavit zarážku](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. Odeberte volání metody `ServerInfo.GetHtml` a přidejte volání `@myTime` proměnné na svém místě. Toto volání zobrazí aktuální časovou hodnotu, která je vrácena novým řádkem kódu.
4. Stiskněte klávesu F5 ke spuštění stránky v ladicím programu. Stránka se zastaví na zarážce, kterou jste nastavili. Následující obrázek ukazuje, jak stránka vypadá v editoru se zarážkou (žlutě).

    ![ladit zarážku](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. Na panelu nástrojů ladění kliknutím na tlačítko **Krok do** (nebo stisknutím klávesy F11) spusťte další řádek kódu. Pokaždé, když kliknete na toto tlačítko, budete pokračovat v provádění na další řádek kódu.

    ![Krok do – tlačítko](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. Prozkoumejte hodnotu proměnné `myTime` tím, že podržíte ukazatel myši nad ní nebo zkontrolujete hodnoty zobrazené v oknech **místní** hodnoty a **zásobník volání** . Visual Studio zobrazí hodnotu proměnné.

    ![Zobrazit časovou hodnotu](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. Po kontrole proměnné a krokování prostřednictvím kódu stiskněte klávesu F5 pro pokračování ve spouštění stránky bez zastavení na každém řádku. Až dokončíte krokování se všemi kódy, prohlížeč zobrazí stránku.

Další informace o ladicím programu a o tom, jak ladit kód v aplikaci Visual Studio, naleznete v tématu [Návod: ladění webových stránek ve Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a>Použití Razor v projektech ASP.NET MVC se sadou Visual Studio

Syntaxe Razor se také v projektech ASP.NET MVC používá rozsáhle. MVC je výkonný model založený na vzorcích, který slouží k vytváření dynamických webů. Pokud bude web webových stránek ASP.NET obtížné udržovat, můžete zvážit jeho převod na aplikaci ASP.NET MVC. Příklad vytvoření aplikace MVC najdete v tématu [Začínáme s ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a>Instalace podpory pro webové stránky ASP.NET v aplikaci Visual Studio 2010

V této části se dozvíte, jak nainstalovat Visual Web Developer Express 2010 a nástroje ASP.NET Web Pages pro Visual Studio.

1. Pokud ještě nemáte instalační program webové platformy, Stáhněte si ho z následující adresy URL:

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. Spusťte instalační program webové platformy.
3. Klikněte na kartu **produkty** .

    ![Karta produkty WebPI](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. Vyhledejte **ASP.NET MVC 4** (pro webové stránky ASP.NET 2) a pak klikněte na **Přidat**. Mezi tyto produkty patří nástroje sady Visual Studio pro vytváření webů ASP.NET Razor.

    ![Možnosti instalace WebPi](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. Instalaci dokončíte kliknutím na **instalovat** .
