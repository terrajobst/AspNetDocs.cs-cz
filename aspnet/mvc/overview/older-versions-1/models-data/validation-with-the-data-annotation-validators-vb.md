---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: Ověřování pomocí validátorů datových poznámek (VB) | Microsoft Docs
author: microsoft
description: Využijte výhod modelu datových poznámek, abyste mohli provádět ověřování v rámci aplikace ASP.NET MVC. Naučte se používat různé typy validátoru...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: 00150575baabc659f7dd0c07349cde52105f6c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542082"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a>Ověřování validátory datových poznámek (VB)

od [Microsoftu](https://github.com/microsoft)

> Využijte výhod modelu datových poznámek, abyste mohli provádět ověřování v rámci aplikace ASP.NET MVC. Naučte se používat různé typy atributů validátoru a pracovat s nimi v Microsoft Entity Framework.

V tomto kurzu se naučíte, jak pomocí validátorů datových poznámek provádět ověřování v aplikaci ASP.NET MVC. Výhodou použití validátorů datových poznámek je, že vám umožňují provádět ověřování jednoduše přidáním jednoho nebo více atributů, jako je například povinný nebo StringLength atribut – na vlastnost třídy.

Předtím, než budete moci použít validátory datových poznámek, je nutné stáhnout pořadač modelů datových poznámek. Ukázku pořadače datových poznámek si můžete stáhnout z webu CodePlex kliknutím [sem](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).

Je důležité si uvědomit, že pořadač pro datové poznámky není oficiální součástí rozhraní Microsoft ASP.NET MVC. I když je pořadač modelů datových poznámek vytvořený týmem Microsoft ASP.NET MVC, Microsoft nenabízí oficiální podporu produktu pro model datových poznámek s popisem a použitý v tomto kurzu.

## <a name="using-the-data-annotation-model-binder"></a>Použití pořadače modelů datových poznámek

Aby bylo možné použít Bindery modelu datových poznámek v aplikaci ASP.NET MVC, musíte nejprve přidat odkaz na sestavení Microsoft. Web. Mvc. DataAnnotations. dll a sestavení System. ComponentModel. DataAnnotations. dll. Vyberte projekt možnosti nabídky **, přidat odkaz**. Potom klikněte na kartu **Procházet** a přejděte do umístění, kam jste stáhli (a odeberou) ukázku pořadače datových poznámek (viz **Obrázek 1**).

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

**Obrázek 1**: Přidání odkazu na pořadač modelů datových poznámek ([kliknutím zobrazíte obrázek v plné velikosti](validation-with-the-data-annotation-validators-vb/_static/image3.png))

Vyberte sestavení Microsoft. Web. Mvc. DataAnnotations. dll a System. ComponentModel. DataAnnotations. dll a klikněte na tlačítko **OK** .

Sestavení System. ComponentModel. DataAnnotations. dll, které je součástí .NET Framework Service Pack 1, nelze použít u pořadače modelů datových poznámek. Je nutné použít verzi sestavení System. ComponentModel. DataAnnotations. dll zahrnuté v ukázce stažení modelu datových poznámek.

Nakonec je nutné zaregistrovat pořadač modelu DataAnnotations v souboru Global. asax. Přidejte následující řádek kódu do obslužné rutiny události aplikace\_Start (), aby metoda Application\_Start () vypadala takto:

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

Tento řádek kódu registruje DataAnnotationsModelBinder jako výchozí modelový pořadač pro celou aplikaci ASP.NET MVC.

## <a name="using-the-data-annotation-validator-attributes"></a>Používání atributů validátoru datových poznámek

Při použití pořadače datových poznámek pomocí atributů validátoru provedete ověření. Obor názvů System. ComponentModel. DataAnnotations obsahuje následující atributy validátoru:

- Rozsah – umožňuje ověřit, zda hodnota vlastnosti spadá mezi zadaný rozsah hodnot.
- RegularExpression – umožňuje ověřit, zda hodnota vlastnosti odpovídá zadanému vzoru regulárního výrazu.
- Požadováno – umožňuje označit vlastnost jako povinnou.
- StringLength – umožňuje zadat maximální délku řetězcové vlastnosti.
- Ověření – základní třída pro všechny atributy validátoru.

> [!NOTE] 
> 
> Pokud vaše požadavky na ověření nejsou splněné pomocí žádného ze standardních validátorů, budete mít vždy možnost vytvořit vlastní atribut validátoru děděním nového atributu validátoru z atributu základní ověření.

Třída Product v **seznamu 1** ukazuje, jak používat tyto atributy validátoru. Vlastnosti název, popis a JednotkováCena jsou označeny jako povinné. Vlastnost Name musí mít délku řetězce, který je kratší než 10 znaků. Nakonec musí vlastnost UnitPrice odpovídat vzoru regulárního výrazu, který představuje částku měny.

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

**Výpis 1**: Models\Product.vb

Třída Product ukazuje, jak použít jeden další atribut: atribut DisplayName. Atribut DisplayName umožňuje upravit název vlastnosti, když je vlastnost zobrazena v chybové zprávě. Místo zobrazení chybové zprávy "povinné pole UnitPrice" můžete zobrazit chybovou zprávu "pole Cena je povinné".

> [!NOTE] 
> 
> Pokud chcete úplně přizpůsobit chybovou zprávu zobrazované validátorem, můžete k vlastnosti ErrorMessage validátoru přiřadit vlastní chybovou zprávu, například: `<Required(ErrorMessage:="This field needs a value!")>`

Můžete použít třídu Product v **seznamu 1** s akcí kontroleru vytvořit () v **seznamu 2**. Tato akce kontroleru znovu zobrazí zobrazení pro vytváření, pokud stav modelu obsahuje nějaké chyby.

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

**Výpis 2**: Controllers\ProductController.vb

Nakonec můžete vytvořit zobrazení v **seznamu 3** kliknutím pravým tlačítkem myši na akci vytvořit () a výběrem možnosti nabídky **Přidat zobrazení**. Vytvořte zobrazení silného typu s třídou Product jako třídu modelu. V rozevíracím seznamu zobrazit obsah vyberte **vytvořit** (viz **Obrázek 2**).

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

**Obrázek 2**: Přidání zobrazení pro vytvoření

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

**Výpis 3**: Views\Product\Create.aspx

> [!NOTE] 
> 
> Odeberte pole ID z formuláře vytvořit generovaného pomocí možnosti nabídky **Přidat zobrazení** . Vzhledem k tomu, že pole ID odpovídá sloupci identity, nechcete uživatelům povolit zadání hodnoty do tohoto pole.

Pokud odešlete formulář pro vytvoření produktu a nezadáte hodnoty pro požadovaná pole, zobrazí se chybové zprávy ověření na **obrázku 3** .

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

**Obrázek 3**: Chybí povinná pole

Pokud zadáte neplatnou hodnotu měny, zobrazí se chybová zpráva na **obrázku 4** .

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

**Obrázek 4**: Neplatná částka měny

## <a name="using-data-annotation-validators-with-the-entity-framework"></a>Použití validátorů datových poznámek pomocí Entity Framework

Pokud používáte Microsoft Entity Framework k vygenerování tříd datového modelu, nemůžete použít atributy validátoru přímo na vaše třídy. Vzhledem k tomu, že Entity Framework Designer generuje třídy modelu, všechny změny, které provedete v třídách modelu, budou při příštím provedení změn v Návrháři přepsány.

Chcete-li použít validátory s třídami generovanými Entity Framework pak je třeba vytvořit metaznačky datových tříd. Validátory lze použít pro třídu meta data namísto použití validátorů na skutečnou třídu.

Představte si například, že jste vytvořili třídu filmů pomocí Entity Framework (viz **Obrázek 5**). Představte si, že chcete, aby název filmu a vlastnosti režiséra byly povinné. V takovém případě můžete vytvořit částečnou třídu a třídu meta data v **seznamu 4**.

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

**Obrázek 5**: třída filmu vygenerovaná Entity Framework

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

**Výpis 4**: Models\Movie.vb

Soubor v **seznamu 4** obsahuje dvě třídy s názvem video a MovieMetaData. Třída Movie je částečnou třídou. Odpovídá částečné třídě generované Entity Framework, která je obsažena v souboru datamode. Designer. vb.

V současné době rozhraní .NET Framework nepodporuje částečné vlastnosti. Proto neexistuje způsob, jak použít atributy validátoru na vlastnosti třídy filmu definované v souboru datamode. Designer. vb použitím atributů validátoru na vlastnosti třídy filmu definované v souboru v **seznamu 4**.

Všimněte si, že částečná třída videa je upravena atributem MetadataType, který odkazuje na třídu MovieMetaData. Třída MovieMetaData obsahuje vlastnosti proxy serveru pro vlastnosti třídy video.

Atributy validátoru jsou aplikovány na vlastnosti třídy MovieMetaData. Vlastnosti název, ředitel a DateReleased jsou všechny označené jako požadované vlastnosti. Vlastnosti režiséra musí být přiřazen řetězec, který obsahuje méně než 5 znaků. Nakonec se atribut DisplayName aplikuje na vlastnost DateReleased, aby se zobrazila chybová zpráva, například pole Datum uvolnění je povinné. místo chyby "pole DateReleased je povinné."

> [!NOTE] 
> 
> Všimněte si, že vlastnosti proxy v třídě MovieMetaData nemusejí představovat stejné typy jako odpovídající vlastnosti ve třídě Movie. Například vlastnost Director je vlastnost řetězce ve třídě Movie a vlastnost objektu ve třídě MovieMetaData.

Stránka na **obrázku 6** znázorňuje chybové zprávy vrácené při zadání neplatných hodnot vlastností videa.

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

**Obrázek 6**: použití validátorů s entity frameworkem ([kliknutím zobrazíte obrázek v plné velikosti](validation-with-the-data-annotation-validators-vb/_static/image14.png))

## <a name="summary"></a>Souhrn

V tomto kurzu jste zjistili, jak můžete pomocí pořadače modelu datové poznámky využít k ověřování v rámci aplikace ASP.NET MVC. Zjistili jste, jak používat různé typy atributů validátoru, jako jsou povinné a StringLength atributy. Zjistili jste také, jak tyto atributy použít při práci s Entity Frameworkem Microsoft.

> [!div class="step-by-step"]
> [Předchozí](validating-with-a-service-layer-vb.md)
