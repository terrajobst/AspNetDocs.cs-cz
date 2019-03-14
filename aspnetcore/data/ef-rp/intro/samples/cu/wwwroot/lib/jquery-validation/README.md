---
ms.openlocfilehash: 83a958fe6a8d61becf9f9062e8ad0ff69108b435
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077920"
---
<a name="jquery-validation-pluginhttpjqueryvalidationorg---form-validation-made-easy"></a>[Ověření modulu plug-in jQuery](http://jqueryvalidation.org/) -formu ověření snadné
================================

[![Stav sestavení](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency stav](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)

Ověření modulu plug-in jQuery poskytuje což ověřování pro vaše stávající formuláře při vytváření všech typů přizpůsobení podle vaší aplikace opravdu snadné.

## <a name="help-the-projecthttppledgiecomcampaigns18159"></a>[Nápověda projektu](http://pledgie.com/campaigns/18159)

[![Nápověda projektu](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)

Tento projekt je hledáte pomoc! [Můžete poskytovat kampaň probíhající pledgie](http://pledgie.com/campaigns/18159) a šíří slovo. Pokud jste použili modul plug-in nebo plánujete použít, zvažte donation – žádné množství pomůže.

Můžete najít plán o tom, které můžete utratit peníze [pledgie stránky](http://pledgie.com/campaigns/18159).

## <a name="getting-started"></a>Začínáme

### <a name="downloading-the-prebuilt-files"></a>Stahování předem připravených souborů

Předkompilované soubory si můžete stáhnout z http://jqueryvalidation.org/

### <a name="downloading-the-latest-changes"></a>Stažení nejnovější změny

Soubory vývojového nevydané je možné získat:

 1. [Stahování](https://github.com/jzaefferer/jquery-validation/archive/master.zip) nebo rozvětvení tohoto úložiště
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

Další informace o tom, jak nastavit pravidla a přizpůsobení, [dokumentaci](http://jqueryvalidation.org/documentation/).

## <a name="reporting-issues-and-contributing-code"></a>Hlášení problémů s a přispívání ke kódu

Zobrazit [přispívání pokyny](CONTRIBUTING.md) podrobnosti.

**DŮLEŽITÁ POZNÁMKA O OVĚŘENÍ E-MAILEM**. Od verze 1.12.0 Tento modul plug-in používá stejný regulární výraz, který [specifikace HTML5 navrhuje prohlížeče pomocí](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address). Budeme jejich vedením a používat stejnou kontrolu. Pokud se domníváte, že specifikace je nesprávná, ohlaste ho prosím na ně. Pokud máte jiné požadavky, zvažte [pomocí vlastní metody](http://jqueryvalidation.org/jQuery.validator.addMethod/).

## <a name="license"></a>Licence
Copyright &copy; Jörn Zaefferer<br>
Licencované v rámci licence MIT.
