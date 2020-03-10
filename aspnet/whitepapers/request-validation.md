---
uid: whitepapers/request-validation
title: Ověření žádosti – zabránění útokům na skripty | Microsoft Docs
author: rick-anderson
description: Tento dokument popisuje funkci ověření žádosti ASP.NET, kde ve výchozím nastavení aplikace brání v zpracování nekódovaného HTML obsahu Odeslat...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: fa429113-5f8f-4ef4-97c5-5c04900a19fa
msc.legacyurl: /whitepapers/request-validation
msc.type: content
ms.openlocfilehash: 807cccd6fe1acdd6359b014387abd3878840d4cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640845"
---
# <a name="request-validation---preventing-script-attacks"></a>Ověření požadavku – obrana před skriptovými útoky

> Tento dokument popisuje funkci ověření žádosti ASP.NET, kde ve výchozím nastavení aplikace brání zpracování nekódovaného obsahu HTML odeslaného na server. Tuto funkci ověření žádosti lze zakázat, pokud je aplikace navržena tak, aby bezpečně zpracovala data ve formátu HTML.
> 
> Platí pro ASP.NET 1,1 a ASP.NET 2,0.

Žádost o ověření, funkce ASP.NET od verze 1,1, brání serveru v přijetí obsahu obsahujícího nešifrovaný kód HTML. Tato funkce je navržená tak, aby zabránila útokům prostřednictvím injektáže skriptu, přičemž kód skriptu nebo HTML může být nevědomě odeslán na server, uložený a následně prezentovan jiným uživatelům. I když je to vhodné, důrazně doporučujeme ověřit všechna vstupní data a kódování HTML.

Například vytvoříte webovou stránku, která žádá o e-mailovou adresu uživatele a uloží tuto e-mailovou adresu do databáze. Pokud uživatel zadá &lt;upozornění&gt;skriptu ("Hello ze skriptu")&lt;/SCRIPT&gt; namísto platné e-mailové adresy, když se tato data zobrazí, tento skript se dá spustit, pokud obsah není správně kódovaný. Funkce ověření žádosti ASP.NET brání tomu, aby se stalo.

## <a name="why-this-feature-is-useful"></a>Proč je tato funkce užitečná

Mnoho webů neví, že jsou otevřené pro jednoduché útoky prostřednictvím injektáže skriptu. Bez ohledu na to, jestli je účel těchto útoků v lokalitě, zobrazením HTML, nebo na potenciálně spouštěný klientský skript pro přesměrování uživatele na web hackerů, útoky prostřednictvím injektáže skriptu jsou problémy, ke kterým musí soupeří webové vývojáře.

Útoky prostřednictvím injektáže skriptu jsou obavy ze všech webových vývojářů, ať už používají ASP.NET, ASP nebo jiné technologie pro vývoj na webu.

Funkce ověření žádosti ASP.NET proaktivně zabraňuje těmto útokům tím, že nepovolí zpracování nekódovaného obsahu HTML serverem, pokud se nerozhodne vývojář povolit tento obsah.

## <a name="what-to-expect-error-page"></a>Co očekávat: chybová stránka

Níže uvedený snímek obrazovky ukazuje ukázkový kód ASP.NET:

![](request-validation/_static/image1.png)

Výsledkem spuštění tohoto kódu je jednoduchá stránka, která umožňuje zadat nějaký text do textového pole, kliknout na tlačítko a zobrazit text v ovládacím prvku popisek:

![](request-validation/_static/image2.png)

Nicméně byly JavaScripty, například `<script>alert("hello!")</script>` k zadání a odeslání, by se vám zobrazila výjimka:

![](request-validation/_static/image3.png)

Chybová zpráva uvádí, že byla zjištěna hodnota potenciálně nebezpečného nebezpečného požadavku. Form a v popisu je uveden seznam s podrobnostmi o tom, co se stalo a jak změnit chování. Příklad:

Ověření žádosti zjistilo potenciálně nebezpečnou vstupní hodnotu klienta a zpracování žádosti bylo přerušeno. Tato hodnota může znamenat pokus o ohrožení zabezpečení aplikace, jako je například útok na skriptování mezi weby. Ověření žádosti můžete zakázat nastavením `validateRequest=false` v direktivě stránky nebo v konfiguračním oddílu. Důrazně však doporučujeme, aby aplikace v tomto případě explicitně kontrolovala všechny vstupy.

## <a name="disabling-request-validation-on-a-page"></a>Zakázání ověření žádosti na stránce

Chcete-li zakázat ověření žádosti na stránce, je nutné nastavit atribut `validateRequest` direktivy stránky na `false`:

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> Je-li požadavek na ověření zakázán, lze obsah odeslat na stránku. je zodpovědný vývojář stránky, aby zajistil, že je obsah správně kódován nebo zpracován.

## <a name="disabling-request-validation-for-your-application"></a>Zakázání ověření žádosti pro vaši aplikaci

Chcete-li zakázat ověření žádosti pro vaši aplikaci, je nutné upravit nebo vytvořit soubor Web. config pro aplikaci a nastavit atribut validateRequest oddílu `<pages />` na `false`:

[!code-xml[Main](request-validation/samples/sample2.xml)]

Pokud chcete zakázat ověření žádosti pro všechny aplikace na serveru, můžete tuto úpravu provést v souboru Machine. config.

> [!CAUTION]
> Pokud je žádost o ověření zakázána, může být obsah odeslán do aplikace. je zodpovědný za to, že vývojář aplikace zajišťuje správné kódování nebo zpracování obsahu.

Následující kód je upraven pro vypnutí ověřování žádosti:

![](request-validation/_static/image4.png)

Nyní, pokud byl do textového pole zadán následující kód jazyka JavaScript `<script>alert("hello!")</script>` výsledek by byl:

![](request-validation/_static/image5.png)

Aby nedocházelo k tomu, že se ověření žádosti vypnulo, musíme obsah zakódovat ve formátu HTML.

## <a name="how-to-html-encode-content"></a>Jak kódovat obsah HTML

Pokud jste zakázali ověřování žádostí, je vhodné zakódovat obsah HTML, který bude uložen pro budoucí použití. Kódování HTML automaticky nahradí všechny "&lt;" nebo "&gt;" (společně s několika dalšími symboly) odpovídající reprezentaci kódované v HTML. Například '&lt;' nahrazuje '&amp;lt; ' a '&gt;' je nahrazen '&amp;gt; '. Prohlížeče používají tyto speciální kódy k zobrazení&lt;nebo&gt;v prohlížeči.

Obsah může být na serveru snadno kódovaný HTML pomocí rozhraní `Server.HtmlEncode(string)` API. Obsah může být také snadno dekódovat HTML, to znamená vrácení zpět na standardní HTML pomocí metody `Server.HtmlDecode(string)`.

![](request-validation/_static/image6.png)

Výsledek:

![](request-validation/_static/image7.png)
