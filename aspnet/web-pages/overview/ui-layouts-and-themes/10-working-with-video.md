---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: Zobrazení videa na webu ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tato kapitola vysvětluje, jak zobrazit video na webových stránkách ASP.NET pomocí stránky syntaxe Razor.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 516d46f38ce8910209f4207c474b0404bf012950
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628945"
---
# <a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a>Zobrazení videa na webu ASP.NET Web Pages (Razor)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek vysvětluje, jak pomocí přehrávače videa (Media) na webu ASP.NET Web Pages (Razor) umožnit uživatelům zobrazovat videa, která jsou uložená na webu. Webové stránky ASP.NET s syntaxe Razor vám umožní přehrávat videa Flash ( *. swf*), Media Player ( *. wmv*) a Silverlight ( *. xap*).
> 
> Naučíte se:
> 
> - Jak zvolit přehrávač videa
> - Přidání videa na webovou stránku.
> - Jak nastavit atributy přehrávače videa
> 
> Jedná se o funkce ASP.NET Razor, které jsou představené v článku:
> 
> - Pomocná rutina `Video`
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 2
> - WebMatrix 2
>   
> 
> V tomto kurzu se používá také WebMatrix 3.

## <a name="introduction"></a>Úvod

Možná budete chtít zobrazit na svém webu video. To uděláte tak, že se připojíte k webu, který už video obsahuje, jako je YouTube. Pokud chcete vložit video z těchto webů přímo na vlastní stránky, můžete z webu získat značku HTML a pak ho zkopírovat do své stránky. Například následující příklad ukazuje, jak vložit video na YouTube:

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

Pokud si chcete přehrát video, které je na vašem vlastním webu (ne na veřejném webu pro sdílení videí), nemůžete na něj přímo odkazovat pomocí vloženého kódu, jako je to. Videa z webu však můžete přehrávat pomocí pomocníka `Video`, který vykresluje přehrávač médií přímo na stránce.

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a>Výběr přehrávače videa

Pro videosoubory existuje spousta formátů a každý formát obvykle vyžaduje jiný přehrávač a jiný způsob konfigurace přehrávače. Na stránkách ASP.NET Razor můžete video přehrát na webové stránce pomocí pomocné rutiny `Video`. Pomocná rutina `Video` zjednodušuje proces vkládání videí na webové stránce, protože automaticky generuje `object` a `embed` prvky HTML, které se obvykle používají k přidání videa na stránku.

Pomocná rutina `Video` podporuje následující mediální přehrávače:

- Adobe Flash
- Windows MediaPlayer
- Microsoft Silverlight

### <a name="the-flash-player"></a>Přehrávač Flash

`Flash` přehrávači pomocníka `Video` vám umožní přehrávat videa Flash (soubory *. swf* ) na webové stránce. Je nutné zadat alespoň cestu k souboru videa. Pokud nezadáte nic, ale cesta, přehrávač použije výchozí hodnoty, které jsou nastavené aktuální verzí Flash. Typická výchozí nastavení:

- Video se zobrazí s výchozí šířkou a výškou a bez barvy pozadí.
- Video se automaticky přehraje při načtení stránky.
- Video se nepřetržitě zacykluje, dokud se explicitně nezastaví.
- Video se škáluje tak, aby se zobrazilo celé video, místo oříznutí videa tak, aby odpovídalo konkrétní velikosti.
- Video se přehrává v okně.

### <a name="the-mediaplayer-player"></a>Přehrávač MediaPlayer

`MediaPlayer` hráč pomocníka s `Video` vám umožní přehrávat videa Windows Media (soubory *. wmv* ), Windows Media Audio (soubory *. WMA* ) a MP3 (soubory *. mp3* ) na webové stránce. Je nutné zadat cestu k mediálnímu souboru, který se má přehrát. všechny ostatní parametry jsou volitelné. Pokud zadáte pouze cestu, přehrávač použije výchozí nastavení nastavené aktuální verzí MediaPlayer, například:

- Video se zobrazuje s výchozí šířkou a výškou.
- Video se automaticky přehraje při načtení stránky.
- Video se jednou přehrává (nejedná se o smyčku).
- Přehrávač zobrazuje úplnou sadu ovládacích prvků v uživatelském rozhraní.
- Video se přehrává v okně.

### <a name="the-silverlight-player"></a>Přehrávač Silverlight

`Silverlight` přehrávači pomocníka s `Video` vám umožní přehrát Windows Media Video (soubory *. wmv* ), Windows Media Audio (soubory *. WMA* ) a MP3 (soubory *. mp3* ). Je nutné nastavit parametr cesty tak, aby odkazoval na balíček aplikace založený na programu Silverlight (soubor *. xap* ). Musíte také nastavit parametry Width a Height. Všechny ostatní parametry jsou volitelné. Pokud použijete přehrávač Silverlight pro video, pokud nastavíte pouze požadované parametry, přehrávač Silverlight zobrazí video bez barvy pozadí.

> [!NOTE]
> V případě, že Silverlight ještě neznáte: soubor *. xap* je komprimovaný soubor, který obsahuje pokyny k rozložení v souboru *. XAML* , spravovaný kód v sestaveních a volitelné prostředky. V aplikaci Visual Studio můžete vytvořit soubor *. xap* jako projekt aplikace Silverlight.

`Silverlight` přehrávač videa používá nastavení, která zadáte pro přehrávač, a nastavení, která jsou k dispozici v souboru *. xap* .

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a>Typy MIME
> 
> Když prohlížeč stáhne soubor, prohlížeč zajistí, že typ souboru odpovídá typu MIME, který je zadaný pro dokument, který je vykreslený. Typ MIME je typ obsahu nebo typ média souboru. Pomoc `Video` používá následující typy MIME:
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`

<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a>Přehrávání videí pro Flash (. swf)

Tento postup ukazuje, jak přehrát video Flash s názvem *Sample. swf*. Procedura předpokládá, že máte na svém webu složku s názvem *Media* a že soubor *. swf* je v této složce.

1. Přidejte knihovnu webových pomocníků ASP.NET na web, jak je popsáno v [tématu Instalace pomocníků na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste ho ještě nepřidali.
2. Na webu přidejte stránku a pojmenujte ji *FlashVideo. cshtml*.
3. Přidejte na stránku následující kód: 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. Spusťte stránku v prohlížeči. (Před spuštěním se ujistěte, že je stránka vybraná v pracovním prostoru **soubory** .) Stránka se zobrazí a video se automaticky přehraje. 

    ![obrazu](10-working-with-video/_static/image1.jpg "ch08_video -1. jpg")

Můžete nastavit parametr `quality` pro video Flash na `low`, `autolow`, `autohigh`, `medium`, `high`a `best`:

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

Video Flash můžete změnit tak, aby se v konkrétní velikosti hrálo pomocí parametru `scale`, který můžete nastavit na následující:

- `showall`. Tím se zajistí, že se celé video zobrazí při zachování původního poměru stran. Můžete ale končit ohraničením na každé straně.
- `noorder`. Tím se zmenší video a zachová se původní poměr stran, ale může se oříznout.
- `exactfit`. Díky tomu se celé video zobrazí bez zachování původního poměru stran, ale může dojít k narušení.

Pokud nezadáte parametr `scale`, bude viditelné celé video a původní poměr stran bude udržován bez oříznutí. Následující příklad ukazuje, jak použít parametr `scale`:

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

Přehrávač Flash podporuje nastavení grafického režimu s názvem `windowMode`. Tuto možnost můžete nastavit na `window`, `opaque`a `transparent`. Ve výchozím nastavení je `windowMode` nastaveno na `window`, které zobrazí video v samostatném okně na webové stránce. Nastavení `opaque` skrývá vše za videem na webové stránce. Nastavení `transparent` umožňuje zobrazit pozadí webové stránky pomocí videa za předpokladu, že část videa je průhledná.

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a>Přehrávání videí MediaPlayer ( *. wmv*)

Následující postup ukazuje, jak přehrát mediální video v okně s názvem *Sample. wmv* , které je ve složce *média* .

1. Přidejte knihovnu webových pomocníků ASP.NET na web, jak je popsáno v [tématu Instalace pomocníků na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste to ještě neudělali.
2. Vytvořte novou stránku s názvem *MediaPlayerVideo. cshtml*.
3. Přidejte na stránku následující kód: 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. Spusťte stránku v prohlížeči. Video se načte a automaticky přehraje. 

    ![obrazu](10-working-with-video/_static/image2.jpg "ch08_video -2. jpg")

Můžete nastavit `playCount` na celé číslo, které určuje, kolikrát se má video automaticky přehrát:

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

Parametr `uiMode` umožňuje určit, které ovládací prvky se zobrazí v uživatelském rozhraní. `uiMode` můžete nastavit na `invisible`, `none`, `mini`nebo `full`. Pokud nezadáte parametr `uiMode`, bude se video zobrazovat spolu s oknem stav, panel hledání, řídicími tlačítky a ovládacími prvky hlasitosti kromě okna videa. Tyto ovládací prvky se zobrazí také v případě, že přehrávač použijete k přehrání zvukového souboru. Tady je příklad, jak použít parametr `uiMode`:

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

Zvuk je ve výchozím nastavení zapnutý, když video přehrává. Zvuk můžete ztlumit nastavením parametru `mute` na hodnotu true:

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

Úroveň zvuku MediaPlayer videa můžete řídit nastavením parametru `volume` na hodnotu mezi 0 a 100. Výchozí hodnota je 50. Tady je příklad:

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a>Přehrávání videí Silverlight

Tento postup ukazuje, jak přehrát video obsažené na stránce Silverlight *. xap* nacházející se ve složce s názvem *Media*.

1. Přidejte knihovnu webových pomocníků ASP.NET na web, jak je popsáno v [tématu Instalace pomocníků na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste to ještě neudělali.
2. Vytvořte novou stránku s názvem *SilverlightVideo. cshtml*.
3. Přidejte na stránku následující kód: 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. Spusťte stránku v prohlížeči. 

    ![obrazu](10-working-with-video/_static/image3.jpg "ch08_video -3. jpg")

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Další prostředky

[Přehled programu Silverlight](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)

[Atributy značek objektu Flash a vložení](http://kb2.adobe.com/cps/127/tn_12701.html)

[Windows Media Player 11 – značky parametrů sady SDK](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)
