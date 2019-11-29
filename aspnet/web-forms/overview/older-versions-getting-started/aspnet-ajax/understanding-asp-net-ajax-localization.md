---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
title: Porozumění lokalizaci ASP.NET AJAX | Microsoft Docs
author: scottcate
description: Lokalizace je proces navrhování a integrace podpory pro určitý jazyk a jazykovou verzi do aplikace nebo součásti aplikace. Mikrofon...
ms.author: riande
ms.date: 03/14/2008
ms.assetid: c1a35f18-bab9-41f7-8497-15530c37a09d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
msc.type: authoredcontent
ms.openlocfilehash: 003e7939accd7a68dab97441b3d999bca835b85a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600879"
---
# <a name="understanding-aspnet-ajax-localization"></a>Principy lokalizace pomocí technologie ASP.NET AJAX

[Scott Cate](https://github.com/scottcate)

[Stáhnout PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial04_Localization_cs.pdf)

> Lokalizace je proces navrhování a integrace podpory pro určitý jazyk a jazykovou verzi do aplikace nebo součásti aplikace. Platforma Microsoft ASP.NET poskytuje rozsáhlou podporu pro lokalizaci standardních aplikací ASP.NET integrací standardního modelu lokalizace rozhraní .NET. Rozhraní Microsoft AJAX používá integrovaný model pro podporu různých scénářů, ve kterých lze provádět lokalizaci.

## <a name="introduction"></a>Úvod

Technologie Microsoftu pro ASP.NET přináší objektově orientovaný a řízený programovací model a podílí se na nich s výhodami zkompilovaného kódu. Model zpracování na straně serveru má však několik nevýhod, které je součástí technologie, mnohé z nich mohou být řešeny novými funkcemi obsaženými v oboru názvů System. Web. Extensions, který zapouzdřuje služby Microsoft AJAX v .NET Framework 3,5. Tato rozšíření umožňují mnoho bohatých funkcí klienta, které byly dříve k dispozici jako součást rozšíření AJAX ASP.NET 2,0, ale nyní jsou součástí základní knihovny tříd rozhraní. Ovládací prvky a funkce v tomto oboru názvů zahrnují částečné vykreslování stránek bez nutnosti úplného obnovení stránky, možnost přístupu k webovým službám prostřednictvím klientského skriptu (včetně rozhraní API pro profilaci ASP.NET) a rozsáhlé rozhraní API na straně klienta navržené k zrcadlení mnoha z řídicí Schémata zobrazená v sadě ovládacích prvků na straně serveru ASP.NET.

Tento dokument white paper zkoumá funkce lokalizace přítomné v knihovně Microsoft AJAX Framework a Microsoft AJAX Script Library v kontextu potřeby pro podporu lokalizace a kontrolu již integrované podpory pro lokalizaci na webu. aplikace poskytované .NET Framework. Knihovna skriptů Microsoft AJAX používá formát souboru. resx, který již používá aplikace .NET, což poskytuje integrovanou podporu IDE a typ prostředku, který lze sdílet.

Tento dokument White Paper vychází z verze beta 2 Microsoft Visual Studio 2008. Tento dokument White Paper také předpokládá, že budete pracovat se sadou Visual Studio 2008, nikoli s nástrojem Visual Web Developer Express a bude poskytovat návody podle uživatelského rozhraní sady Visual Studio. Některé ukázky kódu budou používat šablony projektů, které nemusí být k dispozici v aplikaci Visual Web Developer Express.

## <a name="the-need-for-localization"></a>*Nutnost lokalizace*

Zejména pro vývojáře v podnikových aplikacích a vývojářích komponent se možnost vytvářet nástroje, které mohou být vědomy rozdílů mezi kulturami a jazyky, se stále stále potřebují. Návrh komponent s možností přizpůsobení národním prostředí klienta zvyšuje produktivitu vývojářů a snižuje množství práce potřebné k globálnímu fungování součásti.

Lokalizace je proces navrhování a integrace podpory pro určitý jazyk a jazykovou verzi do aplikace nebo součásti aplikace. Platforma Microsoft ASP.NET poskytuje rozsáhlou podporu pro lokalizaci standardních aplikací ASP.NET integrací standardního modelu lokalizace rozhraní .NET. Rozhraní Microsoft AJAX používá integrovaný model pro podporu různých scénářů, ve kterých lze provádět lokalizaci. Pomocí rozhraní Microsoft AJAX Framework mohou být skripty buď lokalizovány, nasazeny do satelitních sestavení, nebo pomocí struktury statického systému souborů.

## <a name="embedding-scripts-with-satellite-assemblies"></a>*Vkládání skriptů pomocí satelitních sestavení*

V souladu se standardní .NET Framework strategii lokalizace můžou být prostředky zahrnuté v satelitních sestaveních. Satelitní sestavení poskytují několik výhod oproti tradičnímu zahrnutí prostředků v binárních souborech – každou danou lokalizaci je možné aktualizovat bez aktualizace větší image, další lokalizace je možné nasadit jednoduše instalací satelitních sestavení do složku projektu a satelitní sestavení lze nasadit bez způsob opětovného načtení sestavení hlavního projektu. Zejména v projektech ASP.NET to je užitečné, protože může významně snížit množství systémových prostředků používaných přírůstkovou aktualizací a s minimálním dopadem na využívání webů v produkčním prostředí.

Skripty jsou vloženy do sestavení jejich zahrnutím do spravovaných souborů. resx (nebo kompilovaných. Resources), které jsou zahrnuty do sestavení v době kompilace. Jejich prostředky jsou následně zpřístupněny pro aplikaci skriptu prostřednictvím kódu generovaného modulem runtime jazyka AJAX prostřednictvím atributů na úrovni sestavení.

*Zásady vytváření názvů pro vložené soubory skriptu*

Správa skriptu Microsoft AJAX Framework podporuje různé možnosti pro použití při nasazení a testování skriptů a poskytuje pokyny pro usnadnění těchto možností.

*Pro usnadnění ladění:*

Skripty vydané verze (produkční) by neměly zahrnovat kvalifikátor `.debug` v názvu souboru. Skripty navržené pro ladění by měly zahrnovat `.debug` do souboru filename.

*Pro usnadnění lokalizace:*

Skripty neutrální jazykové verze by neměly obsahovat žádný identifikátor jazykové verze v názvu souboru. Pro skripty obsahující lokalizované prostředky by měl být v názvu souboru uveden kód jazyka ISO. Například `es-CO` představuje španělštinu, Kolumbie.

Následující tabulka shrnuje konvence pojmenovávání souborů s příklady:

| Název souboru | Význam |
| --- | --- |
| Script. js | Skript pro vydanou verzi, který je neutrální pro jazykovou verzi. |
| Script. Debug. js | Skript pro ladění verze, který je neutrální pro jazykovou verzi. |
| Script. en-US. js | Verze pro verzi English, USA skript. |
| Script.debug.es-CO. js | Skript debug-Version španělsky, Kolumbie. |

## <a name="walkthrough-create-an-localized-embedded-script"></a>Návod: vytvoření lokalizovaného vloženého skriptu

*Poznámka: Tento návod vyžaduje použití sady Visual Studio 2008 jako Visual Web Developer Express nezahrnuje šablonu projektu pro projekty knihovny tříd.*

1. Vytvoří nový projekt webu s integrovanými rozšířeními ASP.NET AJAX. Vytvořte další projekt, projekt knihovny tříd v rámci řešení s názvem LocalizingResources.
2. Přidejte soubor JScript s názvem VerifyDeletion. js do projektu LocalizingResources a také soubory prostředků. resx s názvem DeletionResources. resx a DeletionResources. ES. resx. Předchozí bude obsahovat prostředky neutrální jazykové verze; Ta bude obsahovat prostředky španělského jazyka.
3. Do VerifyDeletion. js přidejte následující kód:

[!code-javascript[Main](understanding-asp-net-ajax-localization/samples/sample1.js)]

Pro ty, které nejsou obeznámené s syntaxí regulárního výrazu jazyka JavaScript, text v rámci jednoduchých lomítek (v předchozím příkladu/FILENAME/je příklad) označuje objekt RegExp. Knihovna MSDN obsahuje rozsáhlý odkaz na jazyk JavaScript a prostředky na nativních objektech JavaScriptu lze najít online.

1. Do DeletionResources. resx přidejte následující řetězce prostředků: 

    **VerifyDelete**: jste si jisti, že chcete odstranit název souboru?

    **Odstraněno**: název souboru byl odstraněn.

1. Do DeletionResources. ES. resx přidejte následující řetězce prostředků: 

    **VerifyDelete**: Est Seguro DESEE quitar filename?

    **Odstraněno**: filename se ha quitado.
2. Do souboru AssemblyInfo přidejte následující řádky kódu:

[!code-csharp[Main](understanding-asp-net-ajax-localization/samples/sample2.cs)]

1. Přidejte do projektu LocalizingResources odkazy na System. Web a System. Web. Extensions.
2. Přidejte odkaz na projekt LocalizingResources z projektu webu.
3. V části default. aspx v projektu webu aktualizujte ovládací prvek ScriptManager následujícím dodatečným označením:

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample3.aspx)]

1. Ve službě default. aspx kdekoli na stránce vložte tento kód:

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample4.aspx)]

1. Stiskněte klávesu F5. Pokud se zobrazí výzva, povolte ladění. Po načtení stránky stiskněte tlačítko Odstranit. Všimněte si, že se zobrazí výzva k zadání angličtiny (Pokud Váš počítač není ve výchozím nastavení preferovaný pro prostředky španělštiny) pro potvrzení.
2. Zavřete okno prohlížeče a vraťte se na Default. aspx. V direktivě @Page Header nahraďte auto pro Culture a UICulture pomocí ES-ES. Opětovným stisknutím klávesy F5 znovu spusťte webovou aplikaci v prohlížeči. Tentokrát si všimněte, že se zobrazí výzva k odstranění souboru v španělštině:

[![](understanding-asp-net-ajax-localization/_static/image2.png)](understanding-asp-net-ajax-localization/_static/image1.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-localization/_static/image3.png))

[![](understanding-asp-net-ajax-localization/_static/image5.png)](understanding-asp-net-ajax-localization/_static/image4.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-localization/_static/image6.png))

Všimněte si, že existuje několik variant tohoto Názorného postupu. Například skripty mohou být registrovány s ovládacím prvkem ScriptManager programově během načítání stránky.

## <a name="including-a-static-script-file-structure"></a>*Zahrnutí struktury souborů statického skriptu*

Při použití statických souborů skriptu pro nasazení přijdete o některé výhody použití schématu lokalizace rozhraní .NET. Primárně se zobrazuje, že ztratíte automatický typ vygenerovaný ze zahrnutí souborů prostředků skriptu; v předchozím návodu byl například prostředek vystavený automaticky generovaným typem s názvem zpráva z ovládacího prvku ScriptManager.

Existují však některé výhody použití struktury statických souborů skriptu. Aktualizace lze provádět bez nutnosti opětovné kompilace a opětovného nasazení satelitních sestavení a použití statické struktury souborů lze také použít k přepsání vloženého skriptu pro integraci menšího množství funkcí, které nemusí být dodávány s komponentou.

Společnost Microsoft doporučuje zabránit problémům s řízením verzí tím, že během kompilace projektu automaticky generuje vaše prostředky skriptu. Když zachováváte rozsáhlý základ kódu skriptu, může být stále obtížné zajistit, aby se změny kódu projevily v každém lokalizovaném skriptu. Jako alternativu můžete jednoduše zachovat jeden skript logiky a více lokalizačních skriptů a sloučit soubory při sestavování projektu.

Vzhledem k tomu, že nejsou k dispozici prostředky pro deklarativní zahrnutí, by měly být statické soubory skriptu odkazovány buď přidáním `<asp:ScriptElement>` prvků jako podřízených `<Scripts>` značky ovládacího prvku ScriptManager, nebo přidáním `ScriptReference` objektů do vlastnosti `Scripts` ovládacího prvku `ScriptManager` na stránce za běhu.

## <a name="the-scriptmanager-and-its-role-in-localization"></a>*ScriptManager a jeho role v lokalizaci*

ScriptManager umožňuje několik automatických chování lokalizovaných aplikací:

- Automaticky vyhledává soubory skriptu na základě nastavení a konvencí pojmenování. například načte skripty s podporou ladění v režimu ladění a načte lokalizované skripty na základě výběru uživatelského rozhraní v prohlížeči.
- Umožňuje definici kultur, včetně vlastních jazykových verzí.
- Umožňuje kompresi souborů skriptu přes protokol HTTP.
- Ukládá do mezipaměti skripty pro efektivní správu mnoha požadavků.
- Přidá vrstvu dereference do skriptů jejich provedením pomocí šifrované adresy URL.

Odkazy na skripty mohou být přidány do ovládacího prvku ScriptManager buď prostřednictvím kódu programu, nebo deklarativním označením. Deklarativní označení je zvláště užitečné, pokud pracujete se skripty vloženými v jiných sestaveních než na samotném projektu webu, protože název skriptu se nejspíš nemění, protože revize se provedou.

## <a name="summary"></a>Přehled

Protože webové aplikace se dosahují větší cílové skupiny, je potřeba mít přístup k širším kulturám a komunitám, které se stávají jádrem obchodního modelu. webové aplikace elektronického obchodování musí být schopné řešit cizí měny, systémy správy obsahu musí být schopné nejen prezentovat svůj obsah, ale také jejich doporučení k navigaci a pole formuláře v jiných jazycích a společnosti musí znát, že tato nutnost je snadno.

.NET Framework vnitřně podporuje bohatou architekturu lokalizace, pomocí satelitních sestavení a souborů prostředků XML (. resx) k dispozici jednotného způsobu vyhledávání řetězců prostředků a obrázků. Rozšíření ASP.NET AJAX, včetně knihovny Microsoft AJAX Framework a Microsoft AJAX Script Library, poskytují podporu pro tento programovací model v kódu na straně klienta a umožňují snadné vyhledávání řetězců prostředků. Satelitní sestavení podporují automatické zahrnutí prostředků skriptů (skutečné soubory. js) prostřednictvím ScriptResource. axd, pokud názvy souborů následují po daném schématu pojmenování. Díky této podpoře ASP.NET rozšíření AJAX zjednodušují lokalizaci skriptů a globalizace aplikací.

## <a name="bio"></a>*Dostupnost*

Scott Cate spolupracuje s webovými technologiemi Microsoftu od 1997 a je prezidentem myKB.com ([www.myKB.com](http://www.myKB.com)), kde se specializuje při psaní aplikací založených na ASP.NET zaměřené na softwarová řešení ve znalostní bázi Knowledge Base. Scott se dá kontaktovat e-mailem na [scott.cate@myKB.com](mailto:scott.cate@myKB.com) nebo jeho blogu na [ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [Předchozí](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
> [Další](understanding-asp-net-ajax-web-services.md)
