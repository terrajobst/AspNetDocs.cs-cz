---
ms.openlocfilehash: 24c36493284988aa45b15c78e2577c0ef96aba56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067609"
---
<a name="jquery-validation-pluginhttpsjqueryvalidationorg---form-validation-made-easy"></a>[Ověření modulu plug-in jQuery](https://jqueryvalidation.org/) -formu ověření snadné
================================

[![Stav sestavení](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![devDependency stav](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)

Ověření modulu plug-in jQuery poskytuje což ověřování pro vaše stávající formuláře při vytváření všech typů přizpůsobení podle vaší aplikace opravdu snadné.

## <a name="getting-started"></a>Začínáme

### <a name="downloading-the-prebuilt-files"></a>Stahování předem připravených souborů

Předkompilované soubory si můžete stáhnout z https://jqueryvalidation.org/

### <a name="downloading-the-latest-changes"></a>Stažení nejnovější změny

Soubory vývojového nevydané je možné získat:

 1. [Stahování](https://github.com/jquery-validation/jquery-validation/archive/master.zip) nebo rozvětvení tohoto úložiště
 2. [Nastavení sestavení](CONTRIBUTING.md#build-setup)
 3. Spustit `grunt` vytvořit vytvořené soubory v adresáři "dist"

### <a name="including-it-on-your-page"></a>Včetně na stránce

Zahrnout, jQuery a modulu plug-in na stránce. Vyberte formulář pro ověření a volání `validate` metody.

```html
<form>
    <input required>
</form>
<script src="jquery.js"></script>
<script src="jquery.validate.js"></script>
<script>
$("form").validate();
</script>
```

Můžete také zahrnout jQuery a modulu plug-in pomocí requirejs modul.

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

Další informace o tom, jak nastavit pravidla a přizpůsobení, [dokumentaci](https://jqueryvalidation.org/documentation/).

## <a name="reporting-issues-and-contributing-code"></a>Hlášení problémů s a přispívání ke kódu

Zobrazit [přispívání pokyny](CONTRIBUTING.md) podrobnosti.

**DŮLEŽITÁ POZNÁMKA O OVĚŘENÍ E-MAILEM**. Od verze 1.12.0 Tento modul plug-in používá stejný regulární výraz, který [specifikace HTML5 navrhuje prohlížeče pomocí](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address). Budeme jejich vedením a používat stejnou kontrolu. Pokud se domníváte, že specifikace je nesprávná, ohlaste ho prosím na ně. Pokud máte jiné požadavky, zvažte [pomocí vlastní metody](https://jqueryvalidation.org/jQuery.validator.addMethod/).
V případě, že budete muset upravit ověření integrované vzory regulárních výrazů, prosím [postupujte podle dokumentace](https://jqueryvalidation.org/jQuery.validator.methods/).

**DŮLEŽITÁ POZNÁMKA O METODĚ POVINNÉ**. Od verze 1.14.0 zastaví tento modul plug-in oříznutí mezery z hodnoty elementu připojené. Pokud chcete k dosažení stejného výsledku, můžete použít [ `normalizer` ](https://jqueryvalidation.org/normalizer/) , který je možné převést hodnotu prvku před ověření. Tato funkce byla k dispozici od `v1.15.0`. Jinými slovy můžete provést vypadat přibližně takto:
``` js
$("#myForm").validate({
    rules: {
        username: {
            required: true,
            // Using the normalizer to trim the value of the element
            // before validating it.
            //
            // The value of `this` inside the `normalizer` is the corresponding
            // DOMElement. In this example, `this` references the `username` element.
            normalizer: function(value) {
                return $.trim(value);
            }
        }
    }
});
```

## <a name="license"></a>Licence
Copyright &copy; Jörn Zaefferer<br>
Licencované v rámci licence MIT.
