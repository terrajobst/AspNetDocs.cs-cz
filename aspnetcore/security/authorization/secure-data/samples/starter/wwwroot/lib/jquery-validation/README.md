---
ms.openlocfilehash: 83a958fe6a8d61becf9f9062e8ad0ff69108b435
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069115"
---
<a name="jquery-validation-pluginhttpjqueryvalidationorg---form-validation-made-easy"></a><span data-ttu-id="ec60c-101">[Ověření modulu plug-in jQuery](http://jqueryvalidation.org/) -formu ověření snadné</span><span class="sxs-lookup"><span data-stu-id="ec60c-101">[jQuery Validation Plugin](http://jqueryvalidation.org/) - Form validation made easy</span></span>
================================

<span data-ttu-id="ec60c-102">[![Stav sestavení](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency stav](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span><span class="sxs-lookup"><span data-stu-id="ec60c-102">[![Build Status](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency Status](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span></span>

<span data-ttu-id="ec60c-103">Ověření modulu plug-in jQuery poskytuje což ověřování pro vaše stávající formuláře při vytváření všech typů přizpůsobení podle vaší aplikace opravdu snadné.</span><span class="sxs-lookup"><span data-stu-id="ec60c-103">The jQuery Validation Plugin provides drop-in validation for your existing forms, while making all kinds of customizations to fit your application really easy.</span></span>

## <a name="help-the-projecthttppledgiecomcampaigns18159"></a>[<span data-ttu-id="ec60c-104">Nápověda projektu</span><span class="sxs-lookup"><span data-stu-id="ec60c-104">Help the project</span></span>](http://pledgie.com/campaigns/18159)

<span data-ttu-id="ec60c-105">[![Nápověda projektu](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span><span class="sxs-lookup"><span data-stu-id="ec60c-105">[![Help the project](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span></span>

<span data-ttu-id="ec60c-106">Tento projekt je hledáte pomoc!</span><span class="sxs-lookup"><span data-stu-id="ec60c-106">This project is looking for help!</span></span> <span data-ttu-id="ec60c-107">[Můžete poskytovat kampaň probíhající pledgie](http://pledgie.com/campaigns/18159) a šíří slovo.</span><span class="sxs-lookup"><span data-stu-id="ec60c-107">[You can donate to the ongoing pledgie campaign](http://pledgie.com/campaigns/18159) and help spread the word.</span></span> <span data-ttu-id="ec60c-108">Pokud jste použili modul plug-in nebo plánujete použít, zvažte donation – žádné množství pomůže.</span><span class="sxs-lookup"><span data-stu-id="ec60c-108">If you've used the plugin, or plan to use, consider a donation - any amount will help.</span></span>

<span data-ttu-id="ec60c-109">Můžete najít plán o tom, které můžete utratit peníze [pledgie stránky](http://pledgie.com/campaigns/18159).</span><span class="sxs-lookup"><span data-stu-id="ec60c-109">You can find the plan for how to spend the money on the [pledgie page](http://pledgie.com/campaigns/18159).</span></span>

## <a name="getting-started"></a><span data-ttu-id="ec60c-110">Začínáme</span><span class="sxs-lookup"><span data-stu-id="ec60c-110">Getting Started</span></span>

### <a name="downloading-the-prebuilt-files"></a><span data-ttu-id="ec60c-111">Stahování předem připravených souborů</span><span class="sxs-lookup"><span data-stu-id="ec60c-111">Downloading the prebuilt files</span></span>

<span data-ttu-id="ec60c-112">Předkompilované soubory si můžete stáhnout z http://jqueryvalidation.org/</span><span class="sxs-lookup"><span data-stu-id="ec60c-112">Prebuilt files can be downloaded from http://jqueryvalidation.org/</span></span>

### <a name="downloading-the-latest-changes"></a><span data-ttu-id="ec60c-113">Stažení nejnovější změny</span><span class="sxs-lookup"><span data-stu-id="ec60c-113">Downloading the latest changes</span></span>

<span data-ttu-id="ec60c-114">Soubory vývojového nevydané je možné získat:</span><span class="sxs-lookup"><span data-stu-id="ec60c-114">The unreleased development files can be obtained by:</span></span>

 1. <span data-ttu-id="ec60c-115">[Stahování](https://github.com/jzaefferer/jquery-validation/archive/master.zip) nebo rozvětvení tohoto úložiště</span><span class="sxs-lookup"><span data-stu-id="ec60c-115">[Downloading](https://github.com/jzaefferer/jquery-validation/archive/master.zip) or Forking this repository</span></span>
 2. [<span data-ttu-id="ec60c-116">Nastavení sestavení</span><span class="sxs-lookup"><span data-stu-id="ec60c-116">Setup the build</span></span>](CONTRIBUTING.md#build-setup)
 3. <span data-ttu-id="ec60c-117">Spustit `grunt` vytvořit vytvořené soubory v adresáři "dist"</span><span class="sxs-lookup"><span data-stu-id="ec60c-117">Run `grunt` to create the built files in the "dist" directory</span></span>

### <a name="including-it-on-your-page"></a><span data-ttu-id="ec60c-118">Včetně na stránce</span><span class="sxs-lookup"><span data-stu-id="ec60c-118">Including it on your page</span></span>

<span data-ttu-id="ec60c-119">Zahrnout, jQuery a modulu plug-in na stránce.</span><span class="sxs-lookup"><span data-stu-id="ec60c-119">Include jQuery and the plugin on a page.</span></span> <span data-ttu-id="ec60c-120">Vyberte formulář pro ověření a volání `validate` metody.</span><span class="sxs-lookup"><span data-stu-id="ec60c-120">Then select a form to validate and call the `validate` method.</span></span>

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

<span data-ttu-id="ec60c-121">Můžete také zahrnout jQuery a modulu plug-in pomocí requirejs modul.</span><span class="sxs-lookup"><span data-stu-id="ec60c-121">Alternatively include jQuery and the plugin via requirejs in your module.</span></span>

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

<span data-ttu-id="ec60c-122">Další informace o tom, jak nastavit pravidla a přizpůsobení, [dokumentaci](http://jqueryvalidation.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="ec60c-122">For more information on how to setup a rules and customizations, [check the documentation](http://jqueryvalidation.org/documentation/).</span></span>

## <a name="reporting-issues-and-contributing-code"></a><span data-ttu-id="ec60c-123">Hlášení problémů s a přispívání ke kódu</span><span class="sxs-lookup"><span data-stu-id="ec60c-123">Reporting issues and contributing code</span></span>

<span data-ttu-id="ec60c-124">Zobrazit [přispívání pokyny](CONTRIBUTING.md) podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="ec60c-124">See the [Contributing Guidelines](CONTRIBUTING.md) for details.</span></span>

<span data-ttu-id="ec60c-125">**DŮLEŽITÁ POZNÁMKA O OVĚŘENÍ E-MAILEM**.</span><span class="sxs-lookup"><span data-stu-id="ec60c-125">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="ec60c-126">Od verze 1.12.0 Tento modul plug-in používá stejný regulární výraz, který [specifikace HTML5 navrhuje prohlížeče pomocí](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span><span class="sxs-lookup"><span data-stu-id="ec60c-126">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="ec60c-127">Budeme jejich vedením a používat stejnou kontrolu.</span><span class="sxs-lookup"><span data-stu-id="ec60c-127">We will follow their lead and use the same check.</span></span> <span data-ttu-id="ec60c-128">Pokud se domníváte, že specifikace je nesprávná, ohlaste ho prosím na ně.</span><span class="sxs-lookup"><span data-stu-id="ec60c-128">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="ec60c-129">Pokud máte jiné požadavky, zvažte [pomocí vlastní metody](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span><span class="sxs-lookup"><span data-stu-id="ec60c-129">If you have different requirements, consider [using a custom method](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>

## <a name="license"></a><span data-ttu-id="ec60c-130">Licence</span><span class="sxs-lookup"><span data-stu-id="ec60c-130">License</span></span>
<span data-ttu-id="ec60c-131">Copyright &copy; Jörn Zaefferer</span><span class="sxs-lookup"><span data-stu-id="ec60c-131">Copyright &copy; Jörn Zaefferer</span></span><br>
<span data-ttu-id="ec60c-132">Licencované v rámci licence MIT.</span><span class="sxs-lookup"><span data-stu-id="ec60c-132">Licensed under the MIT license.</span></span>
