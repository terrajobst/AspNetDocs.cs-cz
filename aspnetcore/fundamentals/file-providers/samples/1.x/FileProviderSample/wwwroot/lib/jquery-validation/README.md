---
ms.openlocfilehash: 24c36493284988aa45b15c78e2577c0ef96aba56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067609"
---
<a name="jquery-validation-pluginhttpsjqueryvalidationorg---form-validation-made-easy"></a><span data-ttu-id="9b25f-101">[Ověření modulu plug-in jQuery](https://jqueryvalidation.org/) -formu ověření snadné</span><span class="sxs-lookup"><span data-stu-id="9b25f-101">[jQuery Validation Plugin](https://jqueryvalidation.org/) - Form validation made easy</span></span>
================================

<span data-ttu-id="9b25f-102">[![Stav sestavení](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![devDependency stav](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)</span><span class="sxs-lookup"><span data-stu-id="9b25f-102">[![Build Status](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![devDependency Status](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)</span></span>

<span data-ttu-id="9b25f-103">Ověření modulu plug-in jQuery poskytuje což ověřování pro vaše stávající formuláře při vytváření všech typů přizpůsobení podle vaší aplikace opravdu snadné.</span><span class="sxs-lookup"><span data-stu-id="9b25f-103">The jQuery Validation Plugin provides drop-in validation for your existing forms, while making all kinds of customizations to fit your application really easy.</span></span>

## <a name="getting-started"></a><span data-ttu-id="9b25f-104">Začínáme</span><span class="sxs-lookup"><span data-stu-id="9b25f-104">Getting Started</span></span>

### <a name="downloading-the-prebuilt-files"></a><span data-ttu-id="9b25f-105">Stahování předem připravených souborů</span><span class="sxs-lookup"><span data-stu-id="9b25f-105">Downloading the prebuilt files</span></span>

<span data-ttu-id="9b25f-106">Předkompilované soubory si můžete stáhnout z https://jqueryvalidation.org/</span><span class="sxs-lookup"><span data-stu-id="9b25f-106">Prebuilt files can be downloaded from https://jqueryvalidation.org/</span></span>

### <a name="downloading-the-latest-changes"></a><span data-ttu-id="9b25f-107">Stažení nejnovější změny</span><span class="sxs-lookup"><span data-stu-id="9b25f-107">Downloading the latest changes</span></span>

<span data-ttu-id="9b25f-108">Soubory vývojového nevydané je možné získat:</span><span class="sxs-lookup"><span data-stu-id="9b25f-108">The unreleased development files can be obtained by:</span></span>

 1. <span data-ttu-id="9b25f-109">[Stahování](https://github.com/jquery-validation/jquery-validation/archive/master.zip) nebo rozvětvení tohoto úložiště</span><span class="sxs-lookup"><span data-stu-id="9b25f-109">[Downloading](https://github.com/jquery-validation/jquery-validation/archive/master.zip) or Forking this repository</span></span>
 2. [<span data-ttu-id="9b25f-110">Nastavení sestavení</span><span class="sxs-lookup"><span data-stu-id="9b25f-110">Setup the build</span></span>](CONTRIBUTING.md#build-setup)
 3. <span data-ttu-id="9b25f-111">Spustit `grunt` vytvořit vytvořené soubory v adresáři "dist"</span><span class="sxs-lookup"><span data-stu-id="9b25f-111">Run `grunt` to create the built files in the "dist" directory</span></span>

### <a name="including-it-on-your-page"></a><span data-ttu-id="9b25f-112">Včetně na stránce</span><span class="sxs-lookup"><span data-stu-id="9b25f-112">Including it on your page</span></span>

<span data-ttu-id="9b25f-113">Zahrnout, jQuery a modulu plug-in na stránce.</span><span class="sxs-lookup"><span data-stu-id="9b25f-113">Include jQuery and the plugin on a page.</span></span> <span data-ttu-id="9b25f-114">Vyberte formulář pro ověření a volání `validate` metody.</span><span class="sxs-lookup"><span data-stu-id="9b25f-114">Then select a form to validate and call the `validate` method.</span></span>

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

<span data-ttu-id="9b25f-115">Můžete také zahrnout jQuery a modulu plug-in pomocí requirejs modul.</span><span class="sxs-lookup"><span data-stu-id="9b25f-115">Alternatively include jQuery and the plugin via requirejs in your module.</span></span>

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

<span data-ttu-id="9b25f-116">Další informace o tom, jak nastavit pravidla a přizpůsobení, [dokumentaci](https://jqueryvalidation.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="9b25f-116">For more information on how to setup a rules and customizations, [check the documentation](https://jqueryvalidation.org/documentation/).</span></span>

## <a name="reporting-issues-and-contributing-code"></a><span data-ttu-id="9b25f-117">Hlášení problémů s a přispívání ke kódu</span><span class="sxs-lookup"><span data-stu-id="9b25f-117">Reporting issues and contributing code</span></span>

<span data-ttu-id="9b25f-118">Zobrazit [přispívání pokyny](CONTRIBUTING.md) podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="9b25f-118">See the [Contributing Guidelines](CONTRIBUTING.md) for details.</span></span>

<span data-ttu-id="9b25f-119">**DŮLEŽITÁ POZNÁMKA O OVĚŘENÍ E-MAILEM**.</span><span class="sxs-lookup"><span data-stu-id="9b25f-119">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="9b25f-120">Od verze 1.12.0 Tento modul plug-in používá stejný regulární výraz, který [specifikace HTML5 navrhuje prohlížeče pomocí](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span><span class="sxs-lookup"><span data-stu-id="9b25f-120">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="9b25f-121">Budeme jejich vedením a používat stejnou kontrolu.</span><span class="sxs-lookup"><span data-stu-id="9b25f-121">We will follow their lead and use the same check.</span></span> <span data-ttu-id="9b25f-122">Pokud se domníváte, že specifikace je nesprávná, ohlaste ho prosím na ně.</span><span class="sxs-lookup"><span data-stu-id="9b25f-122">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="9b25f-123">Pokud máte jiné požadavky, zvažte [pomocí vlastní metody](https://jqueryvalidation.org/jQuery.validator.addMethod/).</span><span class="sxs-lookup"><span data-stu-id="9b25f-123">If you have different requirements, consider [using a custom method](https://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>
<span data-ttu-id="9b25f-124">V případě, že budete muset upravit ověření integrované vzory regulárních výrazů, prosím [postupujte podle dokumentace](https://jqueryvalidation.org/jQuery.validator.methods/).</span><span class="sxs-lookup"><span data-stu-id="9b25f-124">In case you need to adjust the built-in validation regular expression patterns, please [follow the documentation](https://jqueryvalidation.org/jQuery.validator.methods/).</span></span>

<span data-ttu-id="9b25f-125">**DŮLEŽITÁ POZNÁMKA O METODĚ POVINNÉ**.</span><span class="sxs-lookup"><span data-stu-id="9b25f-125">**IMPORTANT NOTE ABOUT REQUIRED METHOD**.</span></span> <span data-ttu-id="9b25f-126">Od verze 1.14.0 zastaví tento modul plug-in oříznutí mezery z hodnoty elementu připojené.</span><span class="sxs-lookup"><span data-stu-id="9b25f-126">As of version 1.14.0 this plugin stops trimming white spaces from the value of the attached element.</span></span> <span data-ttu-id="9b25f-127">Pokud chcete k dosažení stejného výsledku, můžete použít [ `normalizer` ](https://jqueryvalidation.org/normalizer/) , který je možné převést hodnotu prvku před ověření.</span><span class="sxs-lookup"><span data-stu-id="9b25f-127">If you want to achieve the same result, you can use the [`normalizer`](https://jqueryvalidation.org/normalizer/) that can be used to transform the value of an element before validation.</span></span> <span data-ttu-id="9b25f-128">Tato funkce byla k dispozici od `v1.15.0`.</span><span class="sxs-lookup"><span data-stu-id="9b25f-128">This feature was available since `v1.15.0`.</span></span> <span data-ttu-id="9b25f-129">Jinými slovy můžete provést vypadat přibližně takto:</span><span class="sxs-lookup"><span data-stu-id="9b25f-129">In other words, you can do something like this:</span></span>
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

## <a name="license"></a><span data-ttu-id="9b25f-130">Licence</span><span class="sxs-lookup"><span data-stu-id="9b25f-130">License</span></span>
<span data-ttu-id="9b25f-131">Copyright &copy; Jörn Zaefferer</span><span class="sxs-lookup"><span data-stu-id="9b25f-131">Copyright &copy; Jörn Zaefferer</span></span><br>
<span data-ttu-id="9b25f-132">Licencované v rámci licence MIT.</span><span class="sxs-lookup"><span data-stu-id="9b25f-132">Licensed under the MIT license.</span></span>
