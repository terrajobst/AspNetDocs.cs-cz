---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
title: Principy ověřování a Aplikační služby profilu ASP.NET AJAX | Microsoft Docs
author: scottcate
description: Ověřovací služba umožňuje uživatelům poskytnout přihlašovací údaje, aby mohli získat ověřovací soubor cookie a že služba brány povoluje vlastního uživatele...
ms.author: riande
ms.date: 03/14/2008
ms.assetid: 6ab4efb6-aab6-45ac-ad2c-bdec5848ef9e
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
msc.type: authoredcontent
ms.openlocfilehash: cab9acb1ffd75cca87f6c575a6abdd000235828e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640530"
---
# <a name="understanding-aspnet-ajax-authentication-and-profile-application-services"></a>Principy služeb ověřování a používání profilu technologie ASP.NET AJAX

[Scott Cate](https://github.com/scottcate)

[Stáhnout PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial03_MSAjax_ASP.NET_Services_cs.pdf)

> Ověřovací služba umožňuje uživatelům poskytnout přihlašovací údaje, aby mohli získat ověřovací soubor cookie, a je služba brány, která umožňuje vlastní profily uživatelů, které poskytuje ASP.NET. Použití ověřovací služby ASP.NET AJAX je kompatibilní s ověřováním Standard ASP.NET Forms, takže aplikace, které aktuálně používají ověřování pomocí formulářů (například s ovládacím prvkem přihlášení), nebudou při upgradu na ověřovací službu AJAX přerušeny.

## <a name="introduction"></a>Úvod

V rámci .NET Framework 3,5 Společnost Microsoft přináší upgrade prostředí s proměnlivým rozšířením. k dispozici je pouze nové vývojové prostředí, ale jsou k dispozici nové funkce LINQ (Language-Integrated Query) a další jazykové vylepšení. Kromě toho jsou zahrnuty některé známé funkce jiných sad nástrojů, zejména rozšíření ASP.NET AJAX, jako členy první třídy .NET Framework základní knihovny tříd. Tato rozšíření umožňují mnoho nových bohatých funkcí klienta, včetně částečného vykreslování stránek bez nutnosti úplné aktualizace stránky, možnosti přístupu k webovým službám prostřednictvím klientského skriptu (včetně rozhraní API pro profilaci ASP.NET) a rozsáhlého rozhraní API na straně klienta. Navrženo pro zrcadlení mnoha řídicích schémat, které jsou vidět v ASP.NET sadě ovládacích prvků na straně serveru.

Tento dokument White Paper prohlíží implementaci a používání služby ASP.NET profilování a ověřování pomocí formulářů, protože jsou zpřístupněny rozšířeními AJAX ExtensionsThe AJAX, což usnadňuje podporu ověřování Microsoft ASP.NET pomocí formulářů, jako je (a také Služba profilace) je vystavena prostřednictvím skriptu proxy webové služby. Rozšíření AJAX podporují také vlastní ověřování prostřednictvím třídy AuthenticationServiceManager.

Tento dokument White Paper vychází z verze beta 2 sady Visual Studio 2008 a .NET Framework 3,5. Tento dokument White Paper také předpokládá, že budete pracovat se sadou Visual Studio 2008 Beta 2, ne Visual Web Developer Express a bude poskytovat návody podle uživatelského rozhraní sady Visual Studio. Některé ukázky kódu mohou využívat šablony projektu nedostupné v aplikaci Visual Web Developer Express.

## <a name="profiles-and-authentication"></a>*Profily a ověřování*

Microsoft ASP.NET profilů a ověřovacích služeb poskytuje systém ověřování ASP.NET Forms a jsou standardními komponentami ASP.NET. Rozšíření ASP.NET AJAX poskytují přístup k těmto službám prostřednictvím skriptů prostřednictvím proxy serverů prostřednictvím poměrně jasného modelu pod oborem názvů Sys. Services klientské knihovny AJAX.

Ověřovací služba umožňuje uživatelům poskytnout přihlašovací údaje, aby mohli získat ověřovací soubor cookie, a je služba brány, která umožňuje vlastní profily uživatelů, které poskytuje ASP.NET. Použití ověřovací služby ASP.NET AJAX je kompatibilní s ověřováním Standard ASP.NET Forms, takže aplikace, které aktuálně používají ověřování pomocí formulářů (například s ovládacím prvkem přihlášení), nebudou při upgradu na ověřovací službu AJAX přerušeny.

Profilová služba umožňuje automatickou integraci a ukládání uživatelských dat na základě členství poskytované ověřovací službou. Uložená data jsou určena souborem Web. config a různí poskytovatelé služby profilování zpracovává správu dat. Stejně jako u ověřovací služby je služba profilů AJAX kompatibilní se standardní profilovou službou ASP.NET, takže stránky aktuálně obsahující funkce služby profilů ASP.NET by se neměly rušit, protože podporují podporu AJAX.

Začlenění ASP.NET ověřování a profilování samotných služeb do aplikace je mimo rámec tohoto dokumentu White Paper. Další informace o tomto tématu najdete v článku referenční materiály knihovny MSDN Správa uživatelů pomocí členství na [https://msdn.microsoft.com/library/tw292whz.aspx](https://msdn.microsoft.com/library/tw292whz.aspx). ASP.NET také obsahuje nástroj pro automatické nastavení členství pomocí SQL Server, který je výchozím poskytovatelem ověřovací služby pro členství v ASP.NET. Další informace naleznete v článku Nástroj ASP.NET SQL Server Registration Tool (ASPNET\_regsql. exe) na [https://msdn.microsoft.com/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/library/ms229862(vs.80).aspx).

## <a name="using-the-aspnet-ajax-authentication-service"></a>*Použití ověřovací služby ASP.NET AJAX*

V souboru Web. config musí být povolená ověřovací služba ASP.NET AJAX:

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample1.xml)]

Ověřovací služba vyžaduje, aby bylo povoleno ověřování pomocí formulářů ASP.NET a aby bylo možné povolit soubory cookie v klientském prohlížeči (skript nemůže povolit relaci bez souborů cookie, protože relace bez souborů cookie vyžadují parametry adresy URL).

Jakmile je povolená a nakonfigurovaná ověřovací služba AJAX, může klientský skript ihned využít výhod objektu Sys. Services. AuthenticationService. Primárně klientský skript bude chtít využít výhod `login` metody a `isLoggedIn`. Existuje několik vlastností, které poskytují výchozí hodnoty pro metodu přihlašování, která může přijímat velký počet parametrů.

*Členové sys. Services. AuthenticationService*

*Metoda přihlašování:*

Metoda Login () zahájí požadavek na ověření přihlašovacích údajů uživatele. Tato metoda je asynchronní a neblokuje provádění.

*Ukazatelů*

| **Název parametru** | **Význam** |
| --- | --- |
| userName | Povinná hodnota. Uživatelské jméno, které se má ověřit |
| heslo | Volitelné (výchozí hodnota je null). Heslo uživatele. |
| Trvalé | Volitelné (výchozí hodnota je false). Určuje, zda má být soubor cookie ověřování uživatele uchován v rámci relací. Pokud je hodnota false, uživatel se odhlásí při zavření prohlížeče nebo vypršení platnosti relace. |
| redirectUrl | Volitelné (výchozí hodnota je null). Adresa URL pro přesměrování prohlížeče po úspěšném ověření. Pokud má tento parametr hodnotu null nebo prázdný řetězec, nedojde k žádnému přesměrování. |
| customInfo | Volitelné (výchozí hodnota je null). Tento parametr se aktuálně nepoužívá a je vyhrazený pro budoucí použití. |
| loginCompletedCallback | Volitelné (výchozí hodnota je null). Funkce, která se má zavolat po úspěšném dokončení přihlášení Je-li tento parametr zadán, přepíše vlastnost defaultLoginCompleted. |
| failedCallback | Volitelné (výchozí hodnota je null). Funkce, která má být volána, když Přihlášení selhalo. Je-li tento parametr zadán, přepíše vlastnost defaultFailedCallback. |
| userContext | Volitelné (výchozí hodnota je null). Vlastní uživatelská kontextová data, která by měla být předána funkcím zpětného volání. |

*Návratová hodnota:*

Tato funkce nezahrnuje návratovou hodnotu. Po dokončení volání této funkce je však k dispozici několik chování:

- Aktuální stránka se buď aktualizuje, nebo se změní, pokud parametr `redirectUrl` nevrátil hodnotu null, ani prázdný řetězec.
- Pokud však parametr měl hodnotu null nebo prázdný řetězec, je volána parametr `loginCompletedCallback` nebo vlastnost `defaultLoginCompletedCallback`.
- Pokud volání webové služby dojde k chybě, je volána parametr `failedCallback` vlastnosti `defaultFailedCallback`.

*Metoda odhlášení:*

Metoda logout () odstraní soubor cookie s přihlašovacími údaji a odhlásí aktuálního uživatele z webové aplikace.

*Ukazatelů*

| **Název parametru** | **Význam** |
| --- | --- |
| redirectUrl | Volitelné (výchozí hodnota je null). Adresa URL pro přesměrování prohlížeče po úspěšném ověření. Pokud má tento parametr hodnotu null nebo prázdný řetězec, nedojde k žádnému přesměrování. |
| logoutCompletedCallback | Volitelné (výchozí hodnota je null). Funkce, která má být volána po úspěšném dokončení odhlášení. Je-li tento parametr zadán, přepíše vlastnost defaultLogoutCompleted. |
| failedCallback | Volitelné (výchozí hodnota je null). Funkce, která má být volána, když Přihlášení selhalo. Je-li tento parametr zadán, přepíše vlastnost defaultFailedCallback. |
| userContext | Volitelné (výchozí hodnota je null). Vlastní uživatelská kontextová data, která by měla být předána funkcím zpětného volání. |

*Návratová hodnota:*

Tato funkce nezahrnuje návratovou hodnotu. Po dokončení volání této funkce je však k dispozici několik chování:

- Aktuální stránka se buď aktualizuje, nebo se změní, pokud parametr `redirectUrl` nevrátil hodnotu null, ani prázdný řetězec.
- Pokud však parametr měl hodnotu null nebo prázdný řetězec, je volána parametr `logoutCompletedCallback` nebo vlastnost `defaultLogoutCompletedCallback`.
- Pokud volání webové služby dojde k chybě, je volána parametr `failedCallback` vlastnosti `defaultFailedCallback`.

*defaultFailedCallback – vlastnost (Get, set):*

Tato vlastnost určuje funkci, která by měla být volána, pokud dojde k selhání komunikace s webovou službou. Měl by získat delegáta (nebo odkaz na funkci).

Odkaz na funkci určený touto vlastností by měl mít následující signaturu:

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample2.js)]

*Ukazatelů*

| **Název parametru** | **Význam** |
| --- | --- |
| error | Určuje informace o chybě. |
| userContext | Určuje informace o kontextu uživatele zadané při volání funkce přihlášení nebo odhlášení. |
| MethodName | Název volající metody. |

*vlastnost defaultLoginCompletedCallback (Get, set):*

Tato vlastnost určuje funkci, která by měla být volána, když bylo volání přihlašovací webové služby dokončeno. Měl by získat delegáta (nebo odkaz na funkci).

Odkaz na funkci určený touto vlastností by měl mít následující signaturu:

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample3.js)]

*Ukazatelů*

| **Název parametru** | **Význam** |
| --- | --- |
| validCredentials | Určuje, jestli uživatel zadal platné přihlašovací údaje. `true`, pokud se uživatel úspěšně přihlásil. jinak `false`. |
| userContext | Určuje informace o kontextu uživatele zadané při volání funkce Login. |
| MethodName | Název volající metody. |

*vlastnost defaultLogoutCompletedCallback (Get, set):*

Tato vlastnost určuje funkci, která by měla být volána, když bylo dokončeno volání odhlašovací webové služby. Měl by získat delegáta (nebo odkaz na funkci).

Odkaz na funkci určený touto vlastností by měl mít následující signaturu:

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample4.js)]

*Ukazatelů*

| **Název parametru** | **Význam** |
| --- | --- |
| výsledek | Tento parametr bude vždy `null`; je vyhrazený pro budoucí použití. |
| userContext | Určuje informace o kontextu uživatele zadané při volání funkce Login. |
| MethodName | Název volající metody. |

*vlastnost isLoggedIn (Get):*

Tato vlastnost získá aktuální stav ověřování uživatele. je nastavena objektem ScriptManager během žádosti stránky.

Tato vlastnost vrátí `true`, pokud je uživatel aktuálně přihlášený. v opačném případě vrátí `false`.

*cesta – vlastnost (Get, set):*

Tato vlastnost programově určuje umístění webové služby ověřování. Dá se použít k přepsání výchozího zprostředkovatele ověřování a zároveň jedné sady, která je deklarativně ve vlastnosti cesta podřízeného uzlu AuthenticationService ovládacího prvku ScriptManager (Další informace najdete v tématu použití vlastního zprostředkovatele ověřovací služby). níže v tématu).

Všimněte si, že umístění výchozí ověřovací služby se nemění. ASP.NET AJAX však umožňuje zadat umístění webové služby, která poskytuje stejné rozhraní třídy jako proxy ověřovací služby ASP.NET AJAX.

Všimněte si také, že tato vlastnost by neměla být nastavena na hodnotu, která přesměruje požadavek skriptu mimo aktuální web. Vzhledem k tomu, že aktuální aplikace by neobdržela přihlašovací údaje pro ověření, by byla nepoužitelná; také technologie AJAX, která je základem AJAX, by neměla vystavovat požadavky mezi weby a může vygenerovat výjimku zabezpečení v klientském prohlížeči.

Tato vlastnost je objekt `String` reprezentující cestu k ověřovací webové službě.

*Timeout – vlastnost (Get, set):*

Tato vlastnost určuje dobu, po kterou se má čekat na ověřovací službu před tím, než se žádost o přihlášení nezdařila. Pokud časový limit vyprší během čekání na dokončení volání, bude voláno zpětné volání s neúspěšným požadavkem a volání nebude dokončeno.

Tato vlastnost je objekt `Number`, který představuje počet milisekund, po které se má čekat na výsledky od ověřovací služby.

*Ukázka kódu: přihlášení k ověřovací službě*

Následující kód je příklad stránky ASP.NET s jednoduchým voláním skriptu pro metody Login a Logout třídy AuthenticationService.

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample5.aspx)]

## <a name="accessing-aspnet-profiling-data-via-ajax"></a>Přístup k datům profilování ASP.NET prostřednictvím AJAX

Služba profilace ASP.NET je také zpřístupněna prostřednictvím rozšíření AJAX ASP.NET. Vzhledem k tomu, že služba profilace ASP.NET poskytuje bohatě podrobnější rozhraní API, pomocí kterého se ukládají a načítají data uživatelů, může to být vynikající nástroj pro zvýšení produktivity.

Služba profilů musí být povolená v souboru Web. config; není ve výchozím nastavení. Chcete-li to provést, zajistěte, aby byl podřízený element `profileService` v souboru Web. config povolen = true a zda jste určili, které vlastnosti mohou být čteny nebo zapsány následujícím způsobem:

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample6.xml)]

Je taky potřeba nakonfigurovat profilovou službu. I když konfigurace služby profilování je mimo rozsah tohoto dokumentu White Paper, je vhodné si uvědomit, že skupiny definované v nastavení konfigurace profilu budou přístupné jako dílčí vlastnosti názvu skupiny. Například při zadání následující části profilu:

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample7.xml)]

Klientský skript by měl mít přístup k názvu, Address. řádek1, Address. řádek2, Address. City, Address. State, Address. zip a BackgroundColor jako k vlastnostem pole vlastnosti třídy ProfileService.

Po nakonfigurování služby profilace AJAX bude okamžitě k dispozici na stránkách. před použitím ale bude nutné ho načíst.

*Členové sys. Services. ProfileService*

*pole vlastností:*

Pole vlastnosti zpřístupňuje všechna nakonfigurovaná data profilu jako podřízené vlastnosti, na které může odkazovat konvence tečka-operátor-Name. Vlastnosti, které jsou podřízenými položkami skupin vlastností, jsou označovány jako název_skupiny. PropertyName. Pokud chcete získat stav uživatele, můžete v ukázkové konfiguraci profilu uvedeného výše použít následující identifikátor:

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample8.cs)]

*Metoda load:*

Načte vybraný seznam nebo všechny vlastnosti ze serveru.

*Ukazatelů*

| **Název parametru** | **Význam** |
| --- | --- |
| propertyNames | Volitelné (výchozí hodnota je null). Vlastnosti, které mají být načteny ze serveru. |
| loadCompletedCallback | Volitelné (výchozí hodnota je null). Funkce, která se má volat po dokončení načítání |
| failedCallback | Volitelné (výchozí hodnota je null). Funkce, která se má volat, pokud dojde k chybě |
| userContext | Volitelné (výchozí hodnota je null). Kontextové informace, které mají být předány funkci zpětného volání. |

Funkce Load neobsahuje návratovou hodnotu. Pokud bylo volání úspěšně dokončeno, bude volána buď parametr `loadCompletedCallback`, nebo vlastnost `defaultLoadCompletedCallback`. Pokud se volání nezdařilo nebo vypršel časový limit, bude volána buď parametr `failedCallback`, nebo vlastnost `defaultFailedCallback`.

Pokud není zadán parametr `propertyNames`, jsou ze serveru načteny všechny vlastnosti nakonfigurované pro čtení.

*Uložit metodu:*

Metoda Save () uloží zadaný seznam vlastností (nebo všechny vlastnosti) do profilu ASP.NET uživatele.

*Ukazatelů*

| **Název parametru** | **Význam** |
| --- | --- |
| propertyNames | Volitelné (výchozí hodnota je null). Vlastnosti, které mají být uloženy na server. |
| saveCompletedCallback | Volitelné (výchozí hodnota je null). Funkce, která se má volat po dokončení ukládání. |
| failedCallback | Volitelné (výchozí hodnota je null). Funkce, která se má volat, pokud dojde k chybě |
| userContext | Volitelné (výchozí hodnota je null). Kontextové informace, které mají být předány funkci zpětného volání. |

Funkce Save neobsahuje návratovou hodnotu. Pokud se volání úspěšně dokončí, bude volat buď parametr `saveCompletedCallback`, nebo vlastnost `defaultSaveCompletedCallback`. Pokud se volání nezdařilo nebo vypršel časový limit, bude volána buď vlastnost `failedCallback`, nebo `defaultFailedCallback`.

Pokud má parametr `propertyNames` hodnotu null, všechny vlastnosti profilu budou odeslány na server a server se rozhodne, které vlastnosti mohou být uloženy a které nemohou.

*defaultFailedCallback – vlastnost (Get, set):*

Tato vlastnost určuje funkci, která by měla být volána, pokud dojde k selhání komunikace s webovou službou. Měl by získat delegáta (nebo odkaz na funkci).

Odkaz na funkci určený touto vlastností by měl mít následující signaturu:

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample9.js)]

*Ukazatelů*

| **Název parametru** | **Význam** |
| --- | --- |
| Chyba | Určuje informace o chybě. |
| userContext | Určuje informace o kontextu uživatele zadané při volání funkce Load nebo Save. |
| MethodName | Název volající metody. |

*vlastnost defaultSaveCompleted (Get, set):*

Tato vlastnost určuje funkci, která by měla být volána po dokončení ukládání dat profilu uživatele. Měl by získat delegáta (nebo odkaz na funkci).

Odkaz na funkci určený touto vlastností by měl mít následující signaturu:

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample10.js)]

*Ukazatelů*

| **Název parametru** | **Význam** |
| --- | --- |
| numPropsSaved | Určuje počet uložených vlastností. |
| userContext | Určuje informace o kontextu uživatele zadané při volání funkce Load nebo Save. |
| MethodName | Název volající metody. |

*vlastnost defaultLoadCompleted (Get, set):*

Tato vlastnost určuje funkci, která by měla být volána po dokončení načítání dat profilu uživatele. Měl by získat delegáta (nebo odkaz na funkci).

Odkaz na funkci určený touto vlastností by měl mít následující signaturu:

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample11.js)]

*Ukazatelů*

| **Název parametru** | **Význam** |
| --- | --- |
| numPropsLoaded | Určuje počet načtených vlastností. |
| userContext | Určuje informace o kontextu uživatele zadané při volání funkce Load nebo Save. |
| MethodName | Název volající metody. |

*cesta – vlastnost (Get, set):*

Tato vlastnost programově určuje umístění webové služby Profile. Dá se použít k přepsání výchozího poskytovatele služby profilů i jedné sady deklarativně ve vlastnosti cesta podřízeného uzlu ProfileService ovládacího prvku ScriptManager.

Všimněte si, že umístění výchozí profilové služby se nemění. ASP.NET AJAX však umožňuje zadat umístění webové služby, která poskytuje stejné rozhraní třídy jako proxy ověřovací služby ASP.NET AJAX.

Všimněte si také, že tato vlastnost by neměla být nastavena na hodnotu, která přesměruje požadavek skriptu mimo aktuální web. Technologie AJAX, která je základem AJAX, by neměla vystavovat požadavky mezi weby a může vygenerovat výjimku zabezpečení v prohlížeči klienta.

Tato vlastnost je objekt `String`, který představuje cestu k webové službě profilu.

*Timeout – vlastnost (Get, set):*

Tato vlastnost určuje dobu, po kterou se má na službu profilů čekat, než se nezdařila žádost o načtení nebo uložení. Pokud časový limit vyprší během čekání na dokončení volání, bude voláno zpětné volání s neúspěšným požadavkem a volání nebude dokončeno.

Tato vlastnost je objekt `Number`, který představuje počet milisekund, po které se má čekat na výsledky z profilové služby.

*Ukázka kódu: načtení dat profilu při načtení stránky*

Následující kód zkontroluje, jestli je uživatel ověřený, a pokud ano, načte jako stránku upřednostňovanou barvu pozadí uživatele.

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample12.js)]

## <a name="using-a-custom-authentication-service-provider"></a>*Použití vlastního zprostředkovatele ověřovací služby*

Rozšíření ASP.NET AJAX umožňují vytvořit vlastního poskytovatele ověřovací služby pro skripty vyvoláním funkce prostřednictvím vlastní webové služby. Aby bylo možné použít, Webová služba musí vystavit dvě metody `Login` a `Logout`; a tyto metody musí být zadány se stejnými signaturami metody jako výchozí webová služba ověřování ASP.NET AJAX.

Po vytvoření vlastní webové služby budete muset na stránce zadat cestu, a to buď deklarativně na stránce, programově v kódu, nebo prostřednictvím skriptu klienta.

*Postup při deklarativním nastavení cesty:*

Chcete-li nastavit cestu deklarativně, zahrňte do stránky ASP.NET podřízenou položku AuthenticationService objektu ScriptManager:

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample13.aspx)]

*Nastavení cesty v kódu:*

Pokud chcete cestu nastavit programově, zadejte cestu přes instanci správce skriptů:

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample14.cs)]

*Postup při nastavení cesty ve skriptu:*

Chcete-li nastavit cestu programově ve skriptu, využijte vlastnost `path` třídy AuthenticationService:

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample15.js)]

*Ukázková webová služba pro vlastní ověřování*

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample16.aspx)]

## <a name="summary"></a>Souhrn

ASP.NET Services – konkrétně profilování, členství a ověřovací služby – jsou snadno zpřístupněny JavaScriptu v klientském prohlížeči. To umožňuje vývojářům integrovat kód na straně klienta s mechanismem ověřování bez problémů, aniž by v závislosti na ovládacích prvcích, jako je například UpdatePanel, procházeli těžkou zdvihání. Data profilu je možné chránit i z klienta, a to díky využití nastavení konfigurace webu. ve výchozím nastavení nejsou k dispozici žádná data a vývojáři musí souhlasit s vlastnostmi profilu.

Díky vytváření zjednodušených implementací webových služeb s ekvivalentními signaturami metod můžou vývojáři vytvářet vlastní poskytovatele skriptů pro tyto vnitřní služby ASP.NET Services. Podpora těchto technik zjednodušuje vývoj bohatých klientských aplikací a současně poskytuje vývojářům širokou škálu flexibility, které splňují konkrétní potřeby.

## <a name="bio"></a>*Dostupnost*

Scott Cate spolupracuje s webovými technologiemi Microsoftu od 1997 a je prezidentem myKB.com ([www.myKB.com](http://www.myKB.com)), kde se specializuje při psaní aplikací založených na ASP.NET zaměřené na softwarová řešení ve znalostní bázi Knowledge Base. Scott se dá kontaktovat e-mailem na [scott.cate@myKB.com](mailto:scott.cate@myKB.com) nebo jeho blogu na [ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [Předchozí](understanding-asp-net-ajax-updatepanel-triggers.md)
> [Další](understanding-asp-net-ajax-localization.md)
