---
uid: visual-studio/overview/2013/using-browser-link
title: Používá se odkaz na prohlížeč v Visual Studio 2013 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/04/2013
ms.assetid: 46cbfe20-b4dc-449b-9016-80657dd44fbe
msc.legacyurl: /visual-studio/overview/2013/using-browser-link
msc.type: authoredcontent
ms.openlocfilehash: 723a38de4569b0bb58817c70aabb84fef8e19591
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622904"
---
# <a name="using-browser-link-in-visual-studio-2013"></a>Použití odkazu prohlížeče v Visual Studio 2013

o [Jan Wasson](https://github.com/MikeWasson)

Odkaz na prohlížeč je nová funkce v Visual Studio 2013, která vytvoří komunikační kanál mezi vývojovým prostředím a jedním nebo více webovými prohlížeči. Odkaz na prohlížeč můžete použít k aktualizaci webové aplikace v několika prohlížečích najednou, což je užitečné pro testování v různých prohlížečích.

- [Aktualizace prohlížeče](#browser-refresh)
- [Zobrazení řídicího panelu pro odkaz na prohlížeč](#dashboard)
- [Povolení odkazu na prohlížeč pro statické soubory HTML](#static-html)
- [Zakazuje se odkaz na prohlížeč.](#disabling)
- [Jak to funguje?](#how-it-works)

<a id="browser-refresh"></a>
## <a name="browser-refresh"></a>Aktualizace prohlížeče

Pomocí aktualizace prohlížeče můžete aktualizovat několik prohlížečů, které jsou připojené k aplikaci Visual Studio prostřednictvím odkazu Browser.

Chcete-li použít aktualizaci prohlížeče, nejprve vytvořte aplikaci ASP.NET pomocí některé z šablon projektu. Ladění aplikace stisknutím klávesy F5 nebo kliknutím na ikonu se šipkou na panelu nástrojů:

![](using-browser-link/_static/image1.png)

Pomocí rozevíracího seznamu můžete také vybrat konkrétní prohlížeč pro ladění.

![](using-browser-link/_static/image2.png)

Chcete-li ladit více prohlížečů, vyberte možnost **Procházet pomocí**. V dialogovém okně **Procházet se** stisknutím klávesy Ctrl vyberte více než jeden prohlížeč. Kliknutím na **Procházet** můžete ladit s vybranými prohlížeči. Odkaz na prohlížeč funguje také v případě, že spustíte prohlížeč mimo aplikaci Visual Studio a přejdete na adresu URL aplikace.

![](using-browser-link/_static/image3.png)

Ovládací prvky Browser Link se nacházejí v rozevíracím seznamu s kulatou ikonou šipky. Ikona šipky je tlačítko **aktualizovat** .

![](using-browser-link/_static/image4.png)

Pokud chcete zjistit, které prohlížeče jsou připojené, najeďte myší na tlačítko **aktualizovat** při ladění. Připojené prohlížeče se zobrazí v okně s popisem.

![](using-browser-link/_static/image5.png)

Chcete-li aktualizovat připojené prohlížeče, klikněte na tlačítko **aktualizovat** nebo stiskněte klávesy CTRL + ALT + ENTER. Například následující snímek obrazovky ukazuje projekt ASP.NET, který byl vytvořen pomocí šablony projektu MVC 5. V horní části můžete vidět aplikaci spuštěnou ve dvou prohlížečích. V dolní části je projekt otevřen v aplikaci Visual Studio.

![](using-browser-link/_static/image6.png)

V aplikaci Visual Studio jsem změnil (a) &lt;H1&gt; nadpis domovské stránky:

![](using-browser-link/_static/image7.png)

Po kliknutí na tlačítko **aktualizovat** se změna objevila v obou oknech prohlížeče:

![](using-browser-link/_static/image8.png)

**Poznámky**

- Chcete-li povolit odkaz na prohlížeč, nastavte `debug=true` v prvku [&lt;kompilace&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx) v souboru Web. config projektu.
- Aplikace musí běžet na místním hostiteli.
- Aplikace musí být cílena na rozhraní .NET 4,0 nebo novější.

<a id="dashboard"></a>
## <a name="viewing-the-browser-link-dashboard"></a>Zobrazení řídicího panelu pro odkaz na prohlížeč

Řídicí panel propojení prohlížeče zobrazuje informace o připojeních odkazů prohlížeče. Chcete-li zobrazit řídicí panel, vyberte rozevírací nabídku odkaz prohlížeče (malou šipku vedle tlačítka **aktualizovat** ). Pak klikněte na **řídicí panel odkaz na prohlížeč**.

![](using-browser-link/_static/image9.png)

Řídicí panel zobrazuje připojené prohlížeče a adresu URL, na které má každý prohlížeč přejít.

![](using-browser-link/_static/image10.png)

V části **požadavky** se zobrazují všechny kroky, které jsou nutné k povolení odkazu na prohlížeč pro daný projekt. Například následující snímek obrazovky ukazuje projekt, ve kterém je "ladění" v souboru Web. config nastaveno na hodnotu false.

![](using-browser-link/_static/image11.png)

<a id="static-html"></a>
## <a name="enabling-browser-link-for-static-html-files"></a>Povolení odkazu na prohlížeč pro statické soubory HTML

Chcete-li povolit odkaz na prohlížeč pro statické soubory HTML, přidejte do souboru Web. config následující text.

[!code-xml[Main](using-browser-link/samples/sample1.xml)]

Z důvodu výkonu odeberte toto nastavení při publikování projektu.

<a id="disabling"></a>
## <a name="disabling-browser-link"></a>Zakazuje se odkaz na prohlížeč.

Odkaz na prohlížeč je ve výchozím nastavení povolený. Je několik způsobů, jak je zakázat:

- V rozevírací nabídce odkaz prohlížeče zrušte **možnost povolit odkaz na prohlížeč**. 

    ![](using-browser-link/_static/image12.png)
- V souboru Web. config přidejte klíč s názvem "vs: EnableBrowserLink" s hodnotou "false" v oddílu appSettings. 

    [!code-xml[Main](using-browser-link/samples/sample2.xml)]
- V souboru Web. config nastavte Debug na false. 

    [!code-xml[Main](using-browser-link/samples/sample3.xml)]

<a id="how-it-works"></a>
## <a name="how-does-it-work"></a>Jak to funguje?

Odkaz na prohlížeč používá [signál](../../../signalr/index.md) k vytvoření komunikačního kanálu mezi Visual Studio a prohlížečem. Je-li povolen odkaz na prohlížeč, aplikace Visual Studio funguje jako server signálu, ke kterému se může připojit více klientů (prohlížečů). Odkaz na prohlížeč také zaregistruje modul HTTP pomocí ASP.NET. Tento modul vloží speciální skript &lt;&gt; odkazuje na každý požadavek stránky ze serveru. Odkazy na skript můžete zobrazit tak, že v prohlížeči vyberete "Zobrazit zdroj".

![](using-browser-link/_static/image13.png)

Vaše zdrojové soubory se nemění. Modul HTTP vloží odkazy skriptu dynamicky.

Vzhledem k tomu, že kód na straně prohlížeče je celý JavaScript, funguje ve všech prohlížečích, které [Signal podporuje](../../../signalr/overview/getting-started/supported-platforms.md), bez vyžadování jakéhokoli modulu plug-in prohlížeče.
