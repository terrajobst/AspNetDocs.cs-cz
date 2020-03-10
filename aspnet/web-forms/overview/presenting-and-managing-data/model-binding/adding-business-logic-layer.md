---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: Přidání vrstvy obchodní logiky do projektu, který používá vazby modelu a webové formuláře | Microsoft Docs
author: Rick-Anderson
description: Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET. Vazba modelu umožňuje interakci dat více-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: a824d06d3781e11706f2a48d44ea3ad89bdb7c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634832"
---
# <a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a>Přidání vrstvy obchodní logiky do projektu, který používá vazby modelu a webové formuláře

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET. Vazba modelu umožňuje, aby data byla v interakci s více přímým přesměrováním než při práci s objekty zdroje dat (například ObjectDataSource nebo SqlDataSource). Tato série začíná úvodním materiálem a v pozdějších kurzech přechází na pokročilejší koncepty.
> 
> V tomto kurzu se dozvíte, jak použít vazbu modelu s vrstvou obchodní logiky. Nastavíte člena OnCallingDataMethods k určení, že k volání metod dat se používá jiný objekt než aktuální stránka.
> 
> Tento kurz sestaví na projektu vytvořeném v [předchozích](retrieving-data.md) částech řady.
> 
> Můžete [si stáhnout](https://go.microsoft.com/fwlink/?LinkId=286116) celý projekt v C# nebo VB. Kód ke stažení funguje buď se sadou Visual Studio 2012 nebo Visual Studio 2013. Používá šablonu sady Visual Studio 2012, která se mírně liší od Visual Studio 2013 šablony zobrazené v tomto kurzu.

## <a name="what-youll-build"></a>Co sestavíte

Vazba modelu umožňuje vložit kód interakce dat do souboru kódu na pozadí webové stránky nebo samostatné třídy obchodní logiky. Předchozí kurzy ukázaly, jak používat soubory kódu na pozadí pro kód interakce dat. Tento přístup funguje pro malé weby, ale může vést k opakování kódu a většímu obtížnosti při údržbě velkého webu. Může být také velmi obtížné programově testovat kód, který se nachází v souboru kódu na pozadí, protože není k dispozici žádná abstraktní vrstva.

Chcete-li centralizovat kód interakce dat, můžete vytvořit vrstvu obchodní logiky, která obsahuje veškerou logiku pro interakci s daty. Pak zavoláte vrstvu obchodní logiky z webových stránek. V tomto kurzu se dozvíte, jak přesunout celý kód, který jste napsali v předchozích kurzech, do vrstvy obchodní logiky a potom použít tento kód ze stránek.

V tomto kurzu:

1. Přesunout kód ze souborů kódu na pozadí do vrstvy obchodní logiky
2. Změna ovládacích prvků vázaných na data pro volání metod ve vrstvě obchodní logiky

## <a name="create-business-logic-layer"></a>Vytvoření vrstvy obchodní logiky

Nyní vytvoříte třídu, která je volána z webových stránek. Metody v této třídě vypadají podobně jako metody, které jste použili v předchozích kurzech, a obsahují atributy zprostředkovatele hodnoty.

Nejprve přidejte novou složku s názvem **knihoven BLL**.

![Přidat složku](adding-business-logic-layer/_static/image1.png)

Ve složce knihoven BLL vytvořte novou třídu s názvem **SchoolBL.cs**. Bude obsahovat všechny operace s daty, které byly původně uloženy v souborech kódu na pozadí. Metody jsou skoro stejné jako metody v souboru kódu na pozadí, ale budou zahrnovat nějaké změny.

Nejdůležitější změnou poznámky je, že již nespouštíte kód z instance třídy **Page** . Třída Page obsahuje metodu **TryUpdateModel** a vlastnost **ModelState** . Když je tento kód přesunut do vrstvy obchodní logiky, nebudete již mít instanci třídy Page, která by tyto členy volala. Chcete-li se tomuto problému vyhnout, je nutné přidat parametr **ModelMethodContext** k jakékoli metodě, která přistupuje k TryUpdateModel nebo ModelState. Tento parametr ModelMethodContext můžete použít k volání TryUpdateModel nebo načtení ModelState. Pro tento nový parametr není nutné měnit cokoli na webové stránce.

Nahraďte kód v SchoolBL.cs následujícím kódem.

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a>Revidovat existující stránky a načíst data z vrstvy obchodní logiky

Nakonec budete převádět stránky students. aspx, AddStudent. aspx a kurzy. aspx z použití dotazů v souboru kódu na pozadí pro použití vrstvy obchodní logiky.

V souborech s kódem na pozadí pro studenty, AddStudent a kurzy odstraňte nebo odkomentujte následující metody dotazů:

- studentsGrid\_GetData
- studentsGrid\_UpdateItem
- studentsGrid\_DeleteItem
- addStudentForm\_InsertItem
- coursesGrid\_GetData

V souboru kódu na pozadí teď nemusíte mít žádný kód, který se týká operací s daty.

Obslužná rutina události **OnCallingDataMethods** umožňuje určit objekt, který se má použít pro metody dat. V části studenty. aspx přidejte hodnotu pro tuto obslužnou rutinu události a změňte názvy metod dat na názvy metod ve třídě obchodní logiky.

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

V souboru kódu na pozadí pro studenty. aspx Definujte obslužnou rutinu události pro událost CallingDataMethods. V této obslužné rutině události zadáte třídu obchodní logiky pro datové operace.

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

V AddStudent. aspx udělejte podobné změny.

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

V kurzů. aspx udělejte podobné změny.

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

Spusťte aplikaci a Všimněte si, že všechny stránky fungují stejně jako dříve. Logika ověřování funguje také správně.

## <a name="conclusion"></a>Závěr

V tomto kurzu znovu rozřadíte aplikaci tak, aby používala vrstvu pro přístup k datům a vrstvu obchodní logiky. Určili jste, že datové ovládací prvky používají objekt, který není aktuální stránkou pro datové operace.

> [!div class="step-by-step"]
> [Předchozí](using-query-string-values-to-retrieve-data.md)
