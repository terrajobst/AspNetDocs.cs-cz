---
uid: mvc/overview/advanced/custom-mvc-templates
title: Vlastní šablona MVC | Microsoft Docs
author: joeloff
description: Vytvořte šablonu jako rozšíření VSIX.
ms.author: riande
ms.date: 12/10/2012
ms.assetid: b0a214c7-2f38-4dbc-b47f-bd7bd9df97bd
msc.legacyurl: /mvc/overview/advanced/custom-mvc-templates
msc.type: authoredcontent
ms.openlocfilehash: 0603bc24e070e223551813f66a75889a2e46fd35
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616352"
---
# <a name="custom-mvc-template"></a>Vlastní šablona MVC

od [Jacques Eloff](https://github.com/joeloff)

Vydání aktualizace nástrojů MVC 3 Tools for Visual Studio 2010 představilo samostatného Průvodce projektem pro projekty MVC. Tato změna byla řízena dvěma faktory. Nejprve zavedení nových šablon v MVC 3 a podpora dalších zobrazovacích modulů, jako je například Razor, vedlo k přeplnění dialogového okna Nový projekt v aplikaci Visual Studio. V druhé době si zákazníci požádali o body rozšiřitelnosti a nový průvodce projektem MVC vám poskytne možnost reagovat na tyto žádosti.

Přidání vlastních šablon bylo namáhavý proces, který se spoléhat na použití registru, aby se nové šablony zobrazovaly v Průvodci projektem MVC. Autor nové šablony musel zabalit ho do MSI, aby se zajistilo, že se v době instalace vytvoří potřebné položky registru. Alternativou bylo vytvoření souboru ZIP obsahujícího šablonu, která bude mít koncovému uživateli k dispozici požadované položky registru ručně.

Žádná ze zmíněných přístupů není ideální, takže jsme se rozhodli využít některou ze stávajících infrastruktur poskytovaných rozšířeními [VSIX](https://msdn.microsoft.com/library/ff363239.aspx) , aby bylo snazší vytvářet, distribuovat a instalovat vlastní šablony MVC počínaje MVC 4 pro Visual Studio 2012. Mezi výhody, které poskytuje tento přístup, patří:

- Rozšíření VSIX může obsahovat více šablon, které podporují různé jazyky (C# a Visual Basic) a několik zobrazovacích modulů (aspx a Razor).
- Rozšíření VSIX může cílit na více SKU sady Visual Studio včetně SKU Express.
- [Galerie sady Visual Studio](https://visualstudiogallery.msdn.microsoft.com/) usnadňuje distribuci rozšíření pro velkou cílovou skupinu.
- Rozšíření VSIX je možné upgradovat, aby bylo snazší vytvářet opravy a aktualizace vlastních šablon.

## <a name="prerequisites"></a>Předpoklady

- Uživatelé musí být obeznámeni s vytvářením šablon projektů, včetně požadovaných značek pro vstemplate soubory atd.
- Uživatelé budou muset mít nainstalované Visual Studio Professional a novější. Expresní SKU nepodporují vytváření projektů VSIX.
- Je nainstalovaná [Sada Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668) .

## <a name="example"></a>Příklad

Prvním krokem je vytvoření nového projektu VSIX pomocí C# nebo Visual Basic. Vyberte **soubor > nový projekt**, klikněte na **rozšiřitelnost** v levém podokně a vyberte **projekt VSIX**.

![Nový projekt](custom-mvc-templates/_static/image1.jpg)

Po vytvoření projektu bude otevřen Návrhář VSIX.

![Metadata Návrháře projektu](custom-mvc-templates/_static/image2.jpg)

Návrhář lze použít k úpravě některých obecných vlastností rozšíření, které se uživatelům zobrazí při instalaci rozšíření nebo po prohledání nainstalovaných rozšíření v aplikaci Visual Studio (**nástroje > rozšíření a aktualizace**). Až dokončíte Obecné informace, klikněte na **kartu cíle instalace**.

![Cíle instalace Návrháře projektu](custom-mvc-templates/_static/image3.jpg)

Tato karta slouží k určení SKU a verzí sady Visual Studio, které jsou podporovány vaším rozšířením. Zaškrtněte políčko pro **Tento VSIX je nainstalováno pro všechny uživatele** , aby bylo možné instalovat VSIX pro jednotlivé počítače. Kliknutím na tlačítko **Nový** na pravé straně přidejte další SKU, jako je například Web Developer Express (souboru vwd).

![Přidat nový cíl instalace](custom-mvc-templates/_static/image4.jpg)

Pokud máte v úmyslu podporovat všechny skladové položky Professional a vyšší (Professional, Premium a Ultimate), stačí pouze vybrat minimální SKLADOVOU položku v rodině, **Microsoft.VisualStudio.pro**. Až dokončíte cíle instalace, nezapomeňte uložit všechny změny.

![Cíle instalace Návrháře projektu](custom-mvc-templates/_static/image5.jpg)

Karta **assets (prostředky** ) slouží k přidání všech souborů obsahu do VSIX. Vzhledem k tomu, že MVC vyžaduje vlastní metadata, budete upravovat nezpracovaný soubor XML souboru manifestu VSIX namísto použití karty **assets** pro přidání obsahu. Začněte přidáním obsahu šablony do projektu VSIX. Je důležité, aby struktura složky a obsahu zrcadlíte rozložení projektu. Níže uvedený příklad obsahuje čtyři šablony projektu, které byly odvozeny ze šablony projektu základní MVC. Zajistěte, aby všechny soubory, které tvoří šablonu projektu (vše pod složkou ProjectTemplates), byly přidány do skupiny položek **obsahu** v souboru projektu VSIX a že každá položka obsahuje sadu metadat **CopyToOutputDirectory** a **IncludeInVsix** , jak je znázorněno v následujícím příkladu.

&lt;obsahu include =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;

&lt;CopyToOutputDirectory&gt;vždy&lt;/CopyToOutputDirectory&gt;

&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;

&lt;/Content&gt;

V takovém případě se IDE pokusí kompilovat obsah šablony při sestavení VSIX a pravděpodobně se zobrazí chyba. Soubory kódu v šablonách často obsahují speciální [parametry šablony](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx) používané v aplikaci Visual Studio, když je vytvořena instance šablony projektu, a proto nemůže být zkompilována v INTEGROVANÉm vývojovém prostředí.

![Průzkumník řešení](custom-mvc-templates/_static/image6.jpg)

Zavřete návrháře VSIX a pak klikněte pravým tlačítkem na soubor **source. extension. manifest** v **Průzkumník řešení** a vyberte **otevřít s** a zvolte možnost **Editor XML (text)** .

![Otevřít v dialogovém okně](custom-mvc-templates/_static/image7.jpg)

Vytvořte **&lt;assets&gt;** element a přidejte **&lt;element Asset&gt;** pro každý soubor, který musí být součástí VSIX. Atribut **Type** pro každý **&lt;&gt;elementu assetu** musí být nastaven na **Microsoft. VisualStudio. Mvc. template**. Toto je vlastní obor názvů, který je srozumitelný pouze v Průvodci projektem MVC. Další informace o struktuře a rozložení souboru manifestu najdete v dokumentaci ke schématu VSIX 2,0.

Pouze přidávání souborů do VSIX není dostačující k registraci šablon pomocí Průvodce MVC. V průvodci MVC musíte zadat informace, jako je název šablony, popis, podporované moduly zobrazení a programovací jazyk. Tyto informace se přenesou do vlastních atributů přidružených k elementu **&lt;Asset&gt;** pro každý soubor **vstemplate** .

&lt;Asset d:VsixSubPath =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;

Type =&quot;Microsoft. VisualStudio. Mvc. template&quot;

d:Source =&quot;soubor&quot;

Path =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;

ProjectType =&quot;MVC&quot;

Jazyk =&quot;C#&quot;

ViewEngine =&quot;aspx&quot;

TemplateId =&quot;MyMvcApplication&quot;

Title =&quot;vlastní základní webová aplikace&quot;

Description =&quot;vlastní šablonu odvozenou ze základní webové aplikace MVC (Razor)&quot;

Verze =&quot;4,0&quot;/&gt;

Níže je uveden popis vlastních atributů, které musí být k dispozici:

- **ProjectType** musí být nastavené na MVC.
- **Jazyk** určuje vývojový jazyk podporovaný šablonou. Platné hodnoty jsou buď C# nebo VB.
- **ViewEngine** určuje modul zobrazení podporovaný šablonou, jako je například aspx nebo Razor. Pro toto pole můžete zadat vlastní hodnotu.
- **TemplateID** se používá k seskupování šablon. Pokud se hodnota shoduje s existujícím ID šablony, bude přepsat šablony, které byly dříve registrovány pomocí Průvodce MVC.
- **Title** Určuje krátký popis zobrazený v průvodci MVC pod každou šablonou projektu.
- **Popis** určuje podrobnější popis šablony.

Po přidání všech souborů do manifestu a jejich uložení si všimněte, že se na kartě **assets (prostředky** ) v Návrháři zobrazí všechny soubory, ale ne vlastní atributy, které jste přidali do **&lt;Asset&gt;** elementy pro soubory **vstemplate** .

![Prostředky Návrháře projektu](custom-mvc-templates/_static/image8.jpg)

Vše, co teď zbývá, je zkompilovat projekt VSIX a nainstalovat ho.

Ujistěte se, že jsou všechny instance sady Visual Studio uzavřeny v počítači, kde chcete otestovat rozšíření VSIX. Visual Studio vyhledává nová rozšíření během spouštění, takže pokud je IDE otevřené při instalaci VSIX, budete muset restartovat Visual Studio. V Průzkumníkovi poklikejte na soubor VSIX a spusťte **instalační program VSIX**, klikněte na **nainstalovat** a potom spusťte Visual Studio.

![Instalační program VSIX](custom-mvc-templates/_static/image9.jpg)

V nabídce vyberte **nástroje > rozšíření a aktualizace a** potvrďte tak, že bylo rozšíření nainstalováno. Pokud instalační program VSIX oznámil při instalaci rozšíření nějaké chyby, můžete zobrazit další informace v protokolu VSIX Installer. Protokol je obvykle vytvořen ve složce **% TEMP%** uživatele, který rozšíření nainstaloval, například **C:\Users\Bob\AppData\Local\Temp**.

![Rozšíření a aktualizace](custom-mvc-templates/_static/image10.jpg)

Po zavření okna můžete vytvořit projekt MVC 4, abyste viděli, jestli jsou vaše nové šablony zobrazené v průvodci MVC.

![Nový projekt ASP.NET MVC 4](custom-mvc-templates/_static/image11.jpg)

## <a name="limitations"></a>Omezení

1. Průvodce MVC nepodporuje lokalizované vlastní šablony.
2. Průvodce nebude hlásit žádné chyby, pokud se nepovede najít vlastní šablony. Pokud některý z požadovaných vlastních atributů chybí, šablona bude jednoduše vyloučena z průvodce.
