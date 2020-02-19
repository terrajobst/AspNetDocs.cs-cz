---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/improving-the-details-and-delete-methods
title: Vylepšení metod Details a Delete (VB) | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, který je...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: c5c14ef0-c128-4dc1-8c01-7f0fdb09e411
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/improving-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 08d80cac071907e927bb30df53c6f84a28f53156
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456254"
---
# <a name="improving-the-details-and-delete-methods-vb"></a>Vylepšení podrobností a metod Delete (VB)

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, což je bezplatná verze Microsoft Visual Studio. Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže. Všechny z nich můžete nainstalovat kliknutím na následující odkaz: instalace [webové platformy](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Případně můžete požadavky jednotlivě nainstalovat pomocí následujících odkazů:
> 
> - [Požadavky sady Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Aktualizace nástrojů MVC 3 pro ASP.NET](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podpora modulu runtime + nástroje)
> 
> Pokud používáte sadu Visual Studio 2010 místo sady Visual Web Developer 2010, nainstalujte požadavky kliknutím na následující odkaz: sady [Visual studio 2010 požadavky](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Projekt Visual Web Developer s VB.NET zdrojovým kódem je k dispozici pro toto téma. [Stáhněte si verzi VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Pokud dáváte přednost C#, přepněte se na [ C# verzi](../cs/improving-the-details-and-delete-methods.md) tohoto kurzu.

V této části kurzu provedete některá vylepšení automaticky generovaných `Details` a `Delete`ch metod. Tyto změny nejsou vyžadovány, ale pouze s několika malými verzemi kódu, můžete aplikaci snadno vylepšit.

## <a name="improving-the-details-and-delete-methods"></a>Vylepšení metod Details a DELETE

Když jste vygenerovali `Movie` kontroler, ASP.NET MVC vygenerovala kód, který fungoval skvěle, ale který je možné lépe nastavit pomocí několika malých změn.

Otevřete kontroler `Movie` a upravte metodu `Details` vrácením `HttpNotFound`, když se video nenajde. Měli byste také upravit metodu `Details` k nastavení výchozí hodnoty pro ID, které je předáno. (V [části 6](examining-the-edit-methods-and-edit-view.md) tohoto kurzu jste provedli podobné změny metody `Edit`.) Je však třeba změnit návratový typ metody `Details` z `ViewResult` na `ActionResult`, protože metoda `HttpNotFound` nevrací objekt `ViewResult`. Následující příklad ukazuje upravenou metodu `Details`.

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample1.vb)]

Code First usnadňuje hledání dat pomocí metody `Find`. Důležitou funkcí zabezpečení, kterou jsme do metody zavedli, je to, že kód ověřuje, že metoda `Find` našla film předtím, než se kód pokusí s ním něco udělat. Hacker by například mohl do lokality způsobit chyby tím, že změní adresu URL vytvořenou odkazy z `http://localhost:xxxx/Movies/Details/1` na něco jako `http://localhost:xxxx/Movies/Details/12345` (nebo některá jiná hodnota, která nepředstavuje skutečný film). Pokud nekontrolujete film s hodnotou null, může to vést k chybě databáze.

Podobně změňte metody `Delete` a `DeleteConfirmed` a určete výchozí hodnotu parametru ID a vraťte `HttpNotFound`, když se video nenajde. Níže jsou uvedené aktualizované metody `Delete` v řadiči `Movie`.

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample2.vb)]

Všimněte si, že metoda `Delete` neodstraní data. Provádění operace odstranění v reakci na požadavek GET (nebo pro tuto skutečnost, provádění operace Edit, operace vytvoření nebo jakékoli jiné operace, která mění data) otevře bezpečnostní riziko. Další informace najdete v tématu Stephen položky blogu Walther pro [ASP.NET #46 MVC – nepoužívejte odstranění odkazů, protože vytvářejí bezpečnostní otvory](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).

Metoda `HttpPost`, která odstraňuje data, má název `DeleteConfirmed`, který metodě HTTP POST udělí jedinečný podpis nebo název. Níže jsou uvedené signatury dvou metod:

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample3.vb)]

Modul CLR (Common Language Runtime) vyžaduje, aby přetížené metody měly jedinečný podpis (stejný název, jiný seznam parametrů). Tady ale budete potřebovat dvě metody odstranění – jednu pro GET a jednu pro POST--to vyžaduje stejnou signaturu. (Obě musí přijmout jedno celé číslo jako parametr.)

Pokud je chcete seřadit, můžete provést několik věcí. Jedním z nich je poskytnout metody různé názvy. To je v předchozím příkladu. To však přináší malý problém: ASP.NET mapuje segmenty adresy URL na metody akcí podle názvu a Pokud přejmenujete metodu, směrování normálně nedokáže tuto metodu najít. Řešení je to, co vidíte v příkladu, což je přidání atributu `ActionName("Delete")` do metody `DeleteConfirmed`. To efektivně provádí mapování pro systém směrování tak, aby adresa URL, která obsahuje <em>/Delete/</em>pro požadavek post, mohla najít metodu `DeleteConfirmed`.

Dalším způsobem, jak se vyhnout problému s metodami, které mají stejný název a signatury, je umělá změna signatury metody POST tak, aby zahrnovala nepoužitý parametr. Například někteří vývojáři přidávají typ parametru `FormCollection`, který je předán metodě POST, a pak jednoduše nepoužívejte parametr:

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample4.vb)]

## <a name="wrapping-up"></a>Zabalení

Nyní máte úplnou aplikaci ASP.NET MVC, která ukládá data do databáze SQL Server Compact. Můžete vytvářet, číst, aktualizovat, odstraňovat a hledat filmy.

![](improving-the-details-and-delete-methods/_static/image1.png)

Tento základní kurz vám umožní začít vytvářet řadiče, přidružit je k zobrazením a předávat je s využitím pevně zakódovaných dat. Pak jste vytvořili a navrhli datový model. Entity Framework Code First vytvořila databáze z datového modelu za běhu a systém generování uživatelského rozhraní ASP.NET MVC automaticky vygeneroval metody a zobrazení akcí pro základní operace CRUD. Pak jste přidali vyhledávací formulář, který umožní uživatelům hledat v databázi. Změnili jste databázi tak, aby obsahovala nový sloupec dat, a poté aktualizovala dvě stránky, aby bylo možné vytvořit a zobrazit tato nová data. Přidaní jste ověřování pomocí označení datového modelu pomocí atributů z oboru názvů `DataAnnotations`. Výsledné ověřování běží na klientovi a na serveru.

Pokud chcete aplikaci nasadit, je vhodné nejdřív otestovat aplikaci na místním serveru služby IIS 7. Pomocí tohoto odkazu [Instalace webové platformy](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=ASPNET;) můžete povolit nastavení služby IIS pro aplikace ASP.NET. Podívejte se na následující odkazy na nasazení:

- [Mapa obsahu nasazení ASP.NET](https://msdn.microsoft.com/library/dd394698.aspx)
- [Povolení služby IIS 7. x](https://blogs.msdn.com/b/rickandy/archive/2011/03/14/enabling-iis-7-x-on-windows-7-vista-sp1-windows-2008-windows-2008-r2.aspx)
- [Nasazení projektů webové aplikace](https://msdn.microsoft.com/library/dd394698.aspx)

Teď vám pomůžeme přejít na naši mezilehlou škálu [Entity Framework datový model pro aplikace ASP.NET MVC](../../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) a kurzy pro [hudební úložiště MVC](../../mvc-music-store/mvc-music-store-part-1.md) , abyste si prozkoumali [články ASP.NET na webu MSDN](https://msdn.microsoft.com/library/gg416514(VS.98).aspx)a provedli si více videí a prostředků na [https://asp.net/mvc](https://asp.net/mvc) , abyste se dozvěděli ještě víc o ASP.NET MVC! [Fóra ASP.NET MVC](https://forums.asp.net/1146.aspx) jsou skvělým místem pro pokladení otázek.

Užijte si ji!

– Scott Hanselman ([http://hanselman.com](http://hanselman.com) a [@shanselman](http://twitter.com/shanselman) na Twitteru) a Rick Anderson [blogs.MSDN.com/rickAndy](https://blogs.msdn.com/rickAndy)

> [!div class="step-by-step"]
> [Předchozí](adding-validation-to-the-model.md)
