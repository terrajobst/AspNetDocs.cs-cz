---
ms.openlocfilehash: 1b563a8c0674d51f893415221ca8fab574b78265
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57068503"
---
<a name="--"></a>--
================================

<span data-ttu-id="3c296-101">[![Stav sestavení](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency stav](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span><span class="sxs-lookup"><span data-stu-id="3c296-101">[![Build Status](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency Status](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span></span>

<span data-ttu-id="3c296-102">Ověření modulu plug-in jQuery poskytuje což ověřování pro vaše stávající formuláře při vytváření všech typů přizpůsobení podle vaší aplikace opravdu snadné.</span><span class="sxs-lookup"><span data-stu-id="3c296-102">The jQuery Validation Plugin provides drop-in validation for your existing forms, while making all kinds of customizations to fit your application really easy.</span></span>

## <a name="help-the-projecthttppledgiecomcampaigns18159"></a>[<span data-ttu-id="3c296-103">Nápověda projektu</span><span class="sxs-lookup"><span data-stu-id="3c296-103">Help the project</span></span>](http://pledgie.com/campaigns/18159)

<span data-ttu-id="3c296-104">[![Nápověda projektu](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span><span class="sxs-lookup"><span data-stu-id="3c296-104">[![Help the project](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span></span>

<span data-ttu-id="3c296-105">Tento projekt je hledáte pomoc!</span><span class="sxs-lookup"><span data-stu-id="3c296-105">This project is looking for help!</span></span> <span data-ttu-id="3c296-106">[Můžete poskytovat kampaň probíhající pledgie](http://pledgie.com/campaigns/18159) a šíří slovo.</span><span class="sxs-lookup"><span data-stu-id="3c296-106">[You can donate to the ongoing pledgie campaign](http://pledgie.com/campaigns/18159) and help spread the word.</span></span> <span data-ttu-id="3c296-107">Pokud jste použili modul plug-in nebo plánujete použít, zvažte donation – žádné množství pomůže.</span><span class="sxs-lookup"><span data-stu-id="3c296-107">If you've used the plugin, or plan to use, consider a donation - any amount will help.</span></span>

<span data-ttu-id="3c296-108">Můžete najít plán o tom, které můžete utratit peníze [pledgie stránky](http://pledgie.com/campaigns/18159).</span><span class="sxs-lookup"><span data-stu-id="3c296-108">You can find the plan for how to spend the money on the [pledgie page](http://pledgie.com/campaigns/18159).</span></span>

## <a name="get-started"></a><span data-ttu-id="3c296-109">Začínáme</span><span class="sxs-lookup"><span data-stu-id="3c296-109">Get Started</span></span>

### <a name="downloading-the-prebuilt-files"></a><span data-ttu-id="3c296-110">Stahování předem připravených souborů</span><span class="sxs-lookup"><span data-stu-id="3c296-110">Downloading the prebuilt files</span></span>

<span data-ttu-id="3c296-111">Předkompilované soubory si můžete stáhnout z http://jqueryvalidation.org/</span><span class="sxs-lookup"><span data-stu-id="3c296-111">Prebuilt files can be downloaded from http://jqueryvalidation.org/</span></span>

### <a name="downloading-the-latest-changes"></a><span data-ttu-id="3c296-112">Stažení nejnovější změny</span><span class="sxs-lookup"><span data-stu-id="3c296-112">Downloading the latest changes</span></span>

<span data-ttu-id="3c296-113">Soubory vývojového nevydané je možné získat:</span><span class="sxs-lookup"><span data-stu-id="3c296-113">The unreleased development files can be obtained by:</span></span>

 1. <span data-ttu-id="3c296-114">[Stahování](https://github.com/jzaefferer/jquery-validation/archive/master.zip) nebo rozvětvení tohoto úložiště</span><span class="sxs-lookup"><span data-stu-id="3c296-114">[Downloading](https://github.com/jzaefferer/jquery-validation/archive/master.zip) or Forking this repository</span></span>
 2. [<span data-ttu-id="3c296-115">Nastavení sestavení</span><span class="sxs-lookup"><span data-stu-id="3c296-115">Setup the build</span></span>](CONTRIBUTING.md#build-setup)
 3. <span data-ttu-id="3c296-116">Spustit `grunt` vytvořit vytvořené soubory v adresáři "dist"</span><span class="sxs-lookup"><span data-stu-id="3c296-116">Run `grunt` to create the built files in the "dist" directory</span></span>

### <a name="including-it-on-your-page"></a><span data-ttu-id="3c296-117">Včetně na stránce</span><span class="sxs-lookup"><span data-stu-id="3c296-117">Including it on your page</span></span>

<span data-ttu-id="3c296-118">Zahrnout, jQuery a modulu plug-in na stránce.</span><span class="sxs-lookup"><span data-stu-id="3c296-118">Include jQuery and the plugin on a page.</span></span> <span data-ttu-id="3c296-119">Vyberte formulář pro ověření a volání `validate` metody.</span><span class="sxs-lookup"><span data-stu-id="3c296-119">Then select a form to validate and call the `validate` method.</span></span>

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

<span data-ttu-id="3c296-120">Můžete také zahrnout jQuery a modulu plug-in pomocí requirejs modul.</span><span class="sxs-lookup"><span data-stu-id="3c296-120">Alternatively include jQuery and the plugin via requirejs in your module.</span></span>

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

<span data-ttu-id="3c296-121">Další informace o tom, jak nastavit pravidla a přizpůsobení, [dokumentaci](http://jqueryvalidation.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="3c296-121">For more information on how to setup a rules and customizations, [check the documentation](http://jqueryvalidation.org/documentation/).</span></span>

## <a name="reporting-issues-and-contributing-code"></a><span data-ttu-id="3c296-122">Hlášení problémů s a přispívání ke kódu</span><span class="sxs-lookup"><span data-stu-id="3c296-122">Reporting issues and contributing code</span></span>

<span data-ttu-id="3c296-123">Zobrazit [přispívání pokyny](CONTRIBUTING.md) podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="3c296-123">See the [Contributing Guidelines](CONTRIBUTING.md) for details.</span></span>

<span data-ttu-id="3c296-124">**DŮLEŽITÁ POZNÁMKA O OVĚŘENÍ E-MAILEM**.</span><span class="sxs-lookup"><span data-stu-id="3c296-124">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="3c296-125">Od verze 1.12.0 Tento modul plug-in používá stejný regulární výraz, který [specifikace HTML5 navrhuje prohlížeče pomocí](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span><span class="sxs-lookup"><span data-stu-id="3c296-125">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="3c296-126">Budeme jejich vedením a používat stejnou kontrolu.</span><span class="sxs-lookup"><span data-stu-id="3c296-126">We will follow their lead and use the same check.</span></span> <span data-ttu-id="3c296-127">Pokud se domníváte, že specifikace je nesprávná, ohlaste ho prosím na ně.</span><span class="sxs-lookup"><span data-stu-id="3c296-127">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="3c296-128">Pokud máte jiné požadavky, zvažte [pomocí vlastní metody](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span><span class="sxs-lookup"><span data-stu-id="3c296-128">If you have different requirements, consider [using a custom method](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>

## <a name="license"></a><span data-ttu-id="3c296-129">Licence</span><span class="sxs-lookup"><span data-stu-id="3c296-129">License</span></span>
<span data-ttu-id="3c296-130">Copyright &copy; Jörn Zaefferer</span><span class="sxs-lookup"><span data-stu-id="3c296-130">Copyright &copy; Jörn Zaefferer</span></span><br>
<span data-ttu-id="3c296-131">Licencované v rámci licence MIT.</span><span class="sxs-lookup"><span data-stu-id="3c296-131">Licensed under the MIT license.</span></span>
