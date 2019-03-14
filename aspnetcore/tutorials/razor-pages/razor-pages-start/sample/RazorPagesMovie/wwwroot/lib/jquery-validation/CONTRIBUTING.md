---
ms.openlocfilehash: 3b33bb9bcab1aa7e5438c6fe3f2d7ba0833e7756
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076906"
---
--

## <a name="reporting-an-issue"></a>Ohlášení problému

1. Ujistěte se, že problém, který jste adresování reprodukovatelné.
2. Použití http://jsbin.com nebo http://jsfiddle.net poskytnout zkušební stránku.
3. Jaké prohlížeče problém možné reprodukovat v označení. **Poznámka: Nebudou řešit problémy režimu zájmu kompatibility aplikace Internet Explorer. Ujistěte se, že test v skutečný prohlížeč!**
4. Jakou verzi modulu plug-in je problém reprodukovat v. Je to reprodukovatelné po aktualizaci na nejnovější verzi.

Dokumentace ke službě problémy jsou sledovány také na [jQuery ověření](https://github.com/jzaefferer/jquery-validation/issues) sledování problémů.
Žádosti o přijetí změn ke zlepšení dokumenty jsou v uvítání systémem [dokumentace ověřování jQuery](https://github.com/jzaefferer/validation-content) úložiště, i když.

**DŮLEŽITÁ POZNÁMKA O OVĚŘENÍ E-MAILEM**. Od verze 1.12.0 Tento modul plug-in používá stejný regulární výraz, který [specifikace HTML5 navrhuje prohlížeče pomocí](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address). Budeme jejich vedením a používat stejnou kontrolu. Pokud se domníváte, že specifikace je nesprávná, ohlaste ho prosím na ně. Pokud máte jiné požadavky, zvažte [pomocí vlastní metody](http://jqueryvalidation.org/jQuery.validator.addMethod/).

## <a name="contributing-code"></a>Přispívání ke kódu

Děkujeme za přispívání. Tady je pár pokyny, které pomohou váš příspěvek získat dostali.

1. Ujistěte se, že problém, který jste adresování reprodukovatelné. Použít jsbin.com nebo jsfiddle.net k poskytnutí zkušební stránku.
2. Postupujte podle [průvodce správným stylem jQuery](http://contribute.jquery.com/style-guides/js)
3. Přidat nebo aktualizovat testy jednotek spolu s vaší opravy. Spusťte testy jednotek v prohlížeči alespoň jeden (viz níže).
4. Spustit `grunt` (viz níže) kontroluje linting a několik jiných problémů.
5. Popisují změnu v hodnotě zprávy potvrzení a odkaz-the-ticket, následujícím způsobem: "Ukázky: Oprava delegáta chyb pro dynamické součty ukázku. Opravy #51 ". Pokud přidáváte nový soubor lokalizace, použijte vypadat přibližně takto: "Lokalizace: Lokalizace přidání Chorvatština (HR)"

## <a name="build-setup"></a>Vytvoření nastavení

1. Nainstalujte [NodeJS](http://nodejs.org).
2. Nainstalovat spuštěním nainstalujte rozhraní příkazového řádku pro Grunt `npm install -g grunt-cli`. Další podrobnosti jsou dostupné na svém webu http://gruntjs.com/getting-started.
3. Závislosti na NPM nainstalujte spuštěním `npm install`.
4. Sestavení lze volat teď spuštěním `grunt`.

## <a name="creating-a-new-additional-method"></a>Vytváří se nový další – metoda

Pokud jste napsali vlastní metody, které chcete přispívat k dalším-methods.js:

1. Vytvoření větve
2. Přidejte metodu jako nový soubor v `src/additional`
3. (Volitelné) Přidat překlady `src/localization`
4. Odeslat žádost o přijetí změn do hlavní větve.

## <a name="unit-tests"></a>Testy jednotek

Chcete-li spustit testy jednotky, otevřete `test/index.html` ve webovém prohlížeči. Ujistěte se, že jste spustili `npm install` před tak všechny požadované závislosti jsou k dispozici.
Začněte s jeden prohlížeč při vývoji opravu a potom spusťte před ostatními před potvrzením. Obvykle nejnovější Chrome, Firefox, prohlížeč Safari a Opera a několik dokumentu.

## <a name="documentation"></a>Dokumentace

Nahlaste prosím problémy v dokumentaci na [jQuery ověření](https://github.com/jzaefferer/jquery-validation/issues) sledování problémů.
V případě implementuje vaši žádost o přijetí změn nebo změny veřejné rozhraní API by bylo plus by zadejte žádost o přijetí změn před [dokumentace ověřování jQuery](https://github.com/jzaefferer/validation-content) úložiště.

## <a name="linting"></a>Analyzování kódu

Chcete-li spustit JSHint a další nástroje, použijte `grunt`.
