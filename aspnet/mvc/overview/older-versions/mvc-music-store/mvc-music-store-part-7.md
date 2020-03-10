---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: '7\. část: členství a autorizace | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 7 pokrývá členství a autorizaci.
ms.author: riande
ms.date: 10/13/2010
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: a6a1a936e0ea29ea36721ba78f35845401f74c01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539198"
---
# <a name="part-7-membership-and-authorization"></a>7\. část: Členství a ověřování

o [Jan Galloway](https://github.com/jongalloway)

> Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.  
>   
> Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.  
>   
> V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 7 pokrývá členství a autorizaci.

Náš kontroler Správce úložiště je momentálně přístupný pro každého navštívení našeho webu. Pojďme to změnit, aby se omezilo oprávnění správců webu.

## <a name="adding-the-accountcontroller-and-views"></a>Přidání AccountController a zobrazení

Jeden rozdíl mezi celou šablonou webové aplikace ASP.NET MVC 3 a šablonou prázdné webové aplikace ASP.NET MVC 3 je, že prázdná šablona neobsahuje kontroler účtu. Přidáme řadič účtu zkopírováním několika souborů z nové aplikace ASP.NET MVC vytvořené z úplné šablony webové aplikace ASP.NET MVC 3.

Vytvořte novou aplikaci ASP.NET MVC pomocí úplné šablony webové aplikace ASP.NET MVC 3 a zkopírujte následující soubory do stejných adresářů v našem projektu:

1. Kopírování AccountController.cs do adresáře Controllers
2. Kopírování AccountModels do adresáře modelů
3. Vytvořte adresář účtu v adresáři zobrazení a zkopírujte všechna čtyři zobrazení v

Změňte obor názvů pro třídy Controller a model tak, aby začínaly na MvcMusicStore. Třída AccountController by měla používat obor názvů MvcMusicStore. Controllers a třída AccountModels by měla používat obor názvů MvcMusicStore. Models.

*Poznámka: tyto soubory jsou také k dispozici ve stažení MvcMusicStore-Assets. zip, ze kterého jsme zkopírovali soubory návrhu webu na začátku tohoto kurzu. Soubory členství jsou umístěny v adresáři kódu.*

Aktualizované řešení by mělo vypadat takto:

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a>Přidání administrativního uživatele s lokalitou konfigurace ASP.NET

Než budeme vyžadovat autorizaci na našem webu, bude nutné vytvořit uživatele s přístupem. Nejjednodušší způsob, jak vytvořit uživatele, je použít vestavěný web ASP.NET Configuration.

Spusťte web ASP.NET Configuration kliknutím na ikonu v Průzkumník řešení.

![](mvc-music-store-part-7/_static/image2.png)

Tím se spustí konfigurační Web. Klikněte na kartu zabezpečení na domovské obrazovce a potom klikněte na odkaz Povolit role v centru obrazovky.

![](mvc-music-store-part-7/_static/image3.png)

Klikněte na odkaz vytvořit nebo spravovat role.

![](mvc-music-store-part-7/_static/image4.png)

Jako název role zadejte "Administrator" a stiskněte tlačítko Přidat roli.

![](mvc-music-store-part-7/_static/image5.png)

Klikněte na tlačítko zpět a potom klikněte na odkaz vytvořit uživatele na levé straně.

![](mvc-music-store-part-7/_static/image6.png)

Vyplňte pole informace o uživateli vlevo pomocí následujících informací:

| **Pole** | **Hodnota** |
| --- | --- |
| **Uživatelské jméno** | Správce |
| **Heslo** | password123! |
| **Potvrzení hesla** | password123! |
| **E-mail** | (bude fungovat libovolná e-mailová adresa) |
| **Bezpečnostní otázka** | (bez ohledu na to, co chcete) |
| **Bezpečnostní odpověď** | (bez ohledu na to, co chcete) |

*Poznámka: můžete samozřejmě použít jakékoli heslo, které chcete. Výchozí nastavení zabezpečení hesla vyžaduje heslo, které je delší než 7 znaků a obsahuje jeden nealfanumerický znak.*

Vyberte roli správce pro tohoto uživatele a klikněte na tlačítko vytvořit uživatele.

![](mvc-music-store-part-7/_static/image7.png)

V tomto okamžiku by se měla zobrazit zpráva oznamující, že uživatel byl úspěšně vytvořen.

![](mvc-music-store-part-7/_static/image8.png)

Nyní můžete zavřít okno prohlížeče.

## <a name="role-based-authorization"></a>Autorizace na základě rolí

Nyní můžeme omezit přístup k StoreManagerController pomocí atributu [autorizovat], který určuje, že uživatel musí být v roli správce pro přístup k jakékoli akci kontroleru ve třídě.

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

*Poznámka: atribut [autorizační] lze umístit na konkrétní metody akce i na úrovni třídy řadiče.*

Když teď přejdete na/StoreManager, zobrazí se dialogové okno pro přihlášení:

![](mvc-music-store-part-7/_static/image9.png)

Až se přihlásíte pomocí našeho nového účtu správce, můžeme přejít na obrazovku pro úpravy alba stejně jako dřív.

> [!div class="step-by-step"]
> [Předchozí](mvc-music-store-part-6.md)
> [Další](mvc-music-store-part-8.md)
