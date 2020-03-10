---
uid: web-forms/overview/getting-started/code-editing-in-web-forms-pages
title: Úpravy kódu ASP.NET webové formuláře v Visual Studio 2013 | Microsoft Docs
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: 5344b74e-b888-479a-92bc-601a33bd61a2
msc.legacyurl: /web-forms/overview/getting-started/code-editing-in-web-forms-pages
msc.type: authoredcontent
ms.openlocfilehash: 3473ad476fbbebc58e12586334b4600f57cf17ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78632746"
---
# <a name="code-editing-aspnet-web-forms-in-visual-studio-2013"></a>Úprava kódu webových formulářů ASP.NET v sadě Visual Studio 2013

od [Erik Reitan](https://github.com/Erikre)

V mnoha stránkách webového formuláře ASP.NET můžete psát kód v Visual Basic, C#nebo v jiném jazyce. Editor kódu v aplikaci Visual Studio vám může pomoci při rychlém psaní kódu a pomáhá vyhnout se chybám. Kromě toho Editor poskytuje způsoby, jak vytvořit opakovaně použitelný kód, který vám pomůže snížit množství práce, kterou potřebujete.

Tento názorný postup ukazuje různé funkce editoru kódu sady Visual Studio.

V tomto návodu se naučíte:

- Opravte chyby vloženého kódování.
- Refaktorujte a přejmenujte kód.
- Přejmenujte proměnné a objekty.
- Vložte fragmenty kódu.

## <a name="prerequisites"></a>Předpoklady

Aby bylo možné dokončit tento návod, budete potřebovat:

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) nebo [Microsoft Visual Studio Express 2013 pro web](https://www.microsoft.com/visualstudio/11/downloads#express-web). .NET Framework se nainstaluje automaticky. 

    > [!NOTE] 
    > 
    > Microsoft Visual Studio 2013 a Microsoft Visual Studio Express 2013 pro web se často v této sérii kurzů označují jako Visual Studio.  
    >   
    > Pokud používáte sadu Visual Studio, tento návod předpokládá, že jste vybrali kolekci pro **Vývoj webu** nastavení při prvním spuštění sady Visual Studio. Další informace najdete v tématu [Postupy: výběr nastavení prostředí pro vývoj webu](https://msdn.microsoft.com/library/ff521558.aspx).

## <a name="creating-a-web-application-project-and-a-page"></a>Vytvoření projektu webové aplikace a stránky

<a id="sectionToggle0"></a>

V této části návodu vytvoříte projekt webové aplikace a přidáte do něj novou stránku.

### <a name="to-create-a-web-application-project"></a>Vytvoření projektu webové aplikace

1. Otevřete Microsoft Visual Studio.
2. V nabídce **soubor** vyberte **Nový projekt**.  
    ![nabídky soubor](code-editing-in-web-forms-pages/_static/image1.png)

    Zobrazí se dialogové okno **Nový projekt**.
3. Na levé straně vyberte **šablony** -&gt; skupinu **Web** Templates &gt; **Visual C#**  -.
4. V prostředním sloupci vyberte šablonu **webové aplikace ASP.NET** .
5. Pojmenujte projekt ***BasicWebApp*** a klikněte na tlačítko **OK** .   
Dialogové okno ![nový projekt](code-editing-in-web-forms-pages/_static/image2.png)
6. Potom vyberte šablonu **webové formuláře** a kliknutím na tlačítko **OK** vytvořte projekt.  
Dialogové okno ![nový projekt v ASP.NET](code-editing-in-web-forms-pages/_static/image3.png)  

    Visual Studio vytvoří nový projekt, který obsahuje předem sestavené funkce založené na šabloně webových formulářů.

## <a name="creating-a-new-aspnet-web-forms-page"></a>Vytvoření nové stránky webových formulářů ASP.NET

Když vytvoříte novou aplikaci webového formuláře pomocí šablony projektu **webové aplikace ASP.NET** , Visual Studio přidá stránku ASP.NET (stránku webového formuláře) s názvem *Default. aspx*a také několik dalších souborů a složek. Stránku *Default. aspx* můžete použít jako domovskou stránku webové aplikace. Pro tento návod ale vytvoříte a budete pracovat s novou stránkou.

### <a name="to-add-a-page-to-the-web-application"></a>Přidání stránky do webové aplikace

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na název webové aplikace (v tomto kurzu je název aplikace **BasicWebSite**) a pak klikněte na **Přidat** -&gt; **novou položku**.   
Zobrazí se dialogové okno **Přidat novou položku** .
2. Na levé straně vyberte skupinu **Visual C#**  -&gt; **Web** Templates. Pak v prostředním seznamu vyberte **webový formulář** a pojmenujte ho *FirstWebPage. aspx*.   
    Dialogové okno ![přidat novou položku](code-editing-in-web-forms-pages/_static/image4.png)
3. Kliknutím na tlačítko **Přidat** přidejte stránku webových formulářů do projektu.  
 Visual Studio vytvoří novou stránku a otevře ji.
4. Dále nastavte tuto novou stránku jako výchozí spouštěcí stránku. V **Průzkumník řešení**klikněte pravým tlačítkem myši na novou stránku s názvem *FirstWebPage. aspx* a vyberte možnost **nastavit jako úvodní stránku**. Při příštím spuštění této aplikace k otestování pokroku se tato nová stránka automaticky zobrazí v prohlížeči.

## <a name="correcting-inline-coding-errors"></a>Oprava chyb vloženého kódu

Editor kódu v aplikaci Visual Studio pomáhá vyhnout se chybám při psaní kódu a pokud jste provedli chybu, Editor kódu vám pomůže chybu opravit. V této části návodu napíšete řádek kódu, který ilustruje funkce oprav chyb v editoru.

### <a name="to-correct-simple-coding-errors-in-visual-studio"></a>Oprava chyb jednoduchého kódování v aplikaci Visual Studio

1. V zobrazení **Návrh** dvakrát klikněte na prázdnou stránku a vytvořte obslužnou rutinu pro událost **Load** pro stránku.   
   Obslužnou rutinu události používáte pouze jako místo pro psaní kódu.
2. Uvnitř obslužné rutiny zadejte následující řádek, který obsahuje chybu a stiskněte klávesu **ENTER**:

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample1.cs)]

   Když stisknete klávesu **ENTER**, Editor kódu umístí zelenou a červenou vlnovku (obvykle volání &quot;vlnovkou&quot; čar) v oblasti kódu, u kterých dochází k problémům. Zelené podtržení označuje upozornění. Červené podtržení indikuje chybu, kterou je třeba opravit. 

    Podržením ukazatele myši nad `myStr` zobrazíte popis tlačítka, který vás upozorní. K zobrazení chybové zprávy se také podržíte ukazatel myši na červeném podtržení.

    Následující obrázek ukazuje kód s podtržením.

    ![Uvítací text v zobrazení Návrh](code-editing-in-web-forms-pages/_static/image5.png "Uvítací text v zobrazení Návrh")  
   Chybu je třeba opravit přidáním středníku `;` na konec řádku. Upozornění jednoduše upozorňuje na to, že jste dosud nepoužili `myStr` proměnnou.  

    > [!NOTE] 
    > 
    > Aktuální nastavení formátování kódu v aplikaci Visual Studio si můžete zobrazit tak, že vyberete **nástroje** -&gt; **Možnosti** -&gt; **písma a barvy**.

## <a name="refactoring-and-renaming"></a>Refaktoring a přejmenování

Refaktoring je softwarová metodologie, která zahrnuje restrukturalizaci kódu, aby bylo snazší pochopit a udržovat, a současně zachovat jeho funkčnost. Jednoduchým příkladem může být, že napíšete kód v obslužné rutině události pro získání dat z databáze. Při vývoji stránky zjistíte, že potřebujete přístup k datům z několika různých obslužných rutin. Proto refaktorujte kód stránky vytvořením metody přístupu k datům na stránce a vložením volání do metody v obslužných rutinách.

Editor kódu obsahuje nástroje, které vám pomůžou provádět různé úlohy refaktoringu. V tomto návodu budete pracovat se dvěma technikami refaktoringu: přejmenování proměnných a extrahování metod. Mezi další možnosti refaktoringu patří zapouzdření polí, zvýšení úrovně místních proměnných na parametry metody a Správa parametrů metod. Dostupnost těchto možností refaktoringu závisí na umístění v kódu.

### <a name="refactoring-code"></a>Refaktoring kódu

Běžným scénářem refaktoringu je vytvoření (extrakce) metody z kódu, který je uvnitř jiného člena, jako je například metoda. Tím se zmenší velikost původního členu a bude extrahování kódu znovu použitelné.

V této části návodu napíšete nějaký jednoduchý kód a potom z něj extrahujete metodu. Refaktoring se podporuje pro C#, takže vytvoříte stránku, která bude používat C# jako svůj programovací jazyk.

### <a name="to-extract-a-method-in-a-c-page"></a>Extrakce metody na C# stránce

1. Přepněte do zobrazení **návrhu** .
2. Na **panelu nástrojů**na kartě **standardní** přetáhněte na stránku ovládací prvek [tlačítko](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) .
3. Dvakrát klikněte na ovládací prvek **tlačítko** a vytvořte obslužnou rutinu události [kliknutí](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) a pak přidejte následující zvýrazněný kód:

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample2.cs?highlight=3-16)]

   Kód vytvoří objekt **ArrayList** , používá smyčku k načtení s hodnotami a poté používá další smyčku k zobrazení obsahu objektu **ArrayList** .
4. Stisknutím **kombinace kláves CTRL + F5** spusťte stránku a potom klikněte na **tlačítko** a ujistěte se, že se zobrazí následující výstup:   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample3.html)]
5. Vraťte se do editoru kódu a potom v obslužné rutině události vyberte následující řádky.   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample4.html)]
6. Klikněte pravým tlačítkem myši na výběr, klikněte na **Refaktorovat**a pak zvolte **Extrahovat metodu**. 

    Zobrazí se dialogové okno **Extrahovat metodu** .
7. Do pole **název nové metody** zadejte **DisplayArray**a pak klikněte na **OK**. 

    Editor kódu vytvoří novou metodu s názvem `DisplayArray`a vloží volání nové metody v obslužné rutině **Click** , kde byla smyčka původně.

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample5.cs?highlight=12)]
8. Stisknutím **kombinace kláves CTRL + F5** znovu spusťte stránku a klikněte na **tlačítko**.

    Stránka funguje stejně jako dříve. Metoda `DisplayArray` nyní může být volána odkudkoli ve třídě Page.

## <a name="renaming-variables"></a>Přejmenování proměnných

Když pracujete s proměnnými a také objekty, můžete je chtít přejmenovat poté, co již jsou odkazovány v kódu. Přejmenování proměnných a objektů může ale způsobit, že se kód přeruší, pokud jste převedli přejmenování jednoho z odkazů. Proto můžete použít refaktoring k provedení přejmenování.

### <a name="to-use-refactoring-to-rename-a-variable"></a>Použití refaktoringu k přejmenování proměnné

1. V obslužné rutině události **Click** vyhledejte následující řádek:

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample6.cs)]
2. Klikněte pravým tlačítkem myši na název proměnné `alist`, zvolte **Refaktorovat**a pak zvolte **Přejmenovat**.

    Zobrazí se dialogové okno **Přejmenovat** .
3. Do pole **nový název** zadejte **ArrayList1** a ujistěte se, že je zaškrtnuté políčko **Náhled změn odkazu** . Pak klikněte na **OK**.

    Zobrazí se dialogové okno **Náhled změn** a zobrazí strom obsahující všechny odkazy na proměnnou, kterou přejmenováváte.
4. Kliknutím na **použít** zavřete dialogové okno **Náhled změn** .

    Proměnné, které odkazují konkrétně na instanci, kterou jste vybrali, se přejmenují. Všimněte si však, že proměnná `alist` na následujícím řádku není přejmenována.

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample7.cs)]

    Proměnná `alist` na tomto řádku není přejmenována, protože nepředstavuje stejnou hodnotu jako proměnná `alist`, kterou jste přejmenovali. Proměnná `alist` v deklaraci `DisplayArray` je místní proměnná pro tuto metodu. To ukazuje, že použití refaktoringu k přejmenování proměnných se liší od pouhého provedení akce Find-and-nahrazování v editoru; refaktoring přejmenuje proměnné se znalostí sémantiky proměnné, se kterou pracuje.

## <a name="inserting-snippets"></a>Vkládání fragmentů kódu

Vzhledem k tomu, že existuje mnoho úloh kódování, které vývojáři webových formulářů často potřebují, poskytuje editor kódu knihovnu fragmentů nebo bloků předpsaného kódu. Tyto fragmenty kódu můžete vložit do své stránky.

Každý jazyk, který používáte v aplikaci Visual Studio, obsahuje mírné rozdíly ve způsobu vkládání fragmentů kódu. Informace o vkládání fragmentů naleznete v tématu [Visual Basic fragmenty kódu technologie IntelliSense](https://msdn.microsoft.com/library/18yz4be4.aspx). Informace o vkládání fragmentů kódu v jazyce C#Visual naleznete v tématu [Visual C# Code fragmenty](https://msdn.microsoft.com/library/z41h7fat.aspx).

## <a name="next-steps"></a>Další kroky

Tento návod znázornil základní funkce editoru kódu sady Visual Studio 2010 pro opravy chyb v kódu, refaktoring kódu, přejmenování proměnných a vkládání fragmentů kódu do kódu. Další funkce v editoru umožňují vývoj aplikací rychle a snadno. Můžete například potřebovat:

- Přečtěte si další informace o funkcích technologie IntelliSense, jako je například změna možností technologie IntelliSense, Správa fragmentů kódu a hledání fragmentů kódu online. Další informace najdete v tématu [použití technologie IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx).
- Naučte se vytvářet vlastní fragmenty kódu. Další informace najdete v tématu [vytváření a používání fragmentů kódu technologie IntelliSense](https://msdn.microsoft.com/library/ms165392.aspx) .
- Přečtěte si další informace o funkcích Visual Basic specifických pro fragmenty kódu technologie IntelliSense, jako je například přizpůsobení fragmentů kódu a řešení potíží. Další informace najdete v tématu [Visual Basic fragmentů kódu technologie IntelliSense](https://msdn.microsoft.com/library/18yz4be4.aspx) .
- Přečtěte si další C#informace o funkcích technologie IntelliSense, jako je refaktoring a fragmenty kódu. Další informace najdete v tématu [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx).
