---
uid: web-forms/overview/older-versions-security/membership/user-based-authorization-cs
title: Autorizace na základě uživatele (C#) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se podíváme na omezení přístupu ke stránkám a omezení funkcí na úrovni stránek pomocí různých technik.
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 3c815a9e-2296-4b9b-b945-776d54989daa
msc.legacyurl: /web-forms/overview/older-versions-security/membership/user-based-authorization-cs
msc.type: authoredcontent
ms.openlocfilehash: 059dbf42956268884dcfdade696491ac39e32da9
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74614667"
---
# <a name="user-based-authorization-c"></a>Ověřování založené na uživatelích (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_07_CS.zip) nebo [stažení PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial07_UserAuth_cs.pdf)

> V tomto kurzu se podíváme na omezení přístupu ke stránkám a omezení funkcí na úrovni stránek pomocí různých technik.

## <a name="introduction"></a>Úvod

Většina webových aplikací, které nabízejí uživatelské účty, tak, aby bylo jisté, že někteří návštěvníci mají přístup k určitým stránkám v rámci lokality. Ve většině online messageboardch webů jsou například všichni uživatelé – anonymní a ověřené – můžou zobrazit příspěvky Messageboard, ale jenom ověření uživatelé mohou navštívit webovou stránku a vytvořit nový příspěvek. A můžou existovat stránky pro správu, které jsou dostupné jenom pro konkrétního uživatele (nebo konkrétní skupinu uživatelů). Kromě toho se funkce na úrovni stránek můžou v jednotlivých uživatelích lišit. Při zobrazení seznamu příspěvků se ověřeným uživatelům zobrazuje rozhraní pro hodnocení jednotlivých příspěvků, zatímco toto rozhraní není k dispozici pro anonymní návštěvníky.

ASP.NET usnadňuje definování autorizačních pravidel založených na uživatelích. Pouze pomocí bitové značky v `Web.config`lze konkrétní webové stránky nebo celé adresáře uzamknout, aby byly přístupné pouze pro určitou podmnožinu uživatelů. Funkce na úrovni stránky lze zapnout nebo vypnout na základě aktuálně přihlášeného uživatele prostřednictvím programových a deklarativních prostředků.

V tomto kurzu se podíváme na omezení přístupu ke stránkám a omezení funkcí na úrovni stránek pomocí různých technik. Pojďme začít!

## <a name="a-look-at-the-url-authorization-workflow"></a>Podívejte se na pracovní postup autorizace URL.

Jak je popsáno v kurzu [*Přehled ověřování pomocí formulářů*](../introduction/an-overview-of-forms-authentication-cs.md) , když modul runtime ASP.NET zpracuje požadavek na prostředek ASP.NET, žádost během svého životního cyklu vyvolá několik událostí. *Moduly HTTP* jsou spravované třídy, jejichž kód je spuštěn v reakci na konkrétní událost v životním cyklu žádosti. ASP.NET se dodává s několika moduly HTTP, které provádějí zásadní úlohy na pozadí.

Jeden takový modul HTTP je [`FormsAuthenticationModule`](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx). Jak je popsáno v předchozích kurzech, je primární funkcí `FormsAuthenticationModule` určení identity aktuální žádosti. K tomu je možné si prohlédnout lístek ověřování pomocí formulářů, který je umístěný v souboru cookie nebo vložený v rámci adresy URL. Tato identifikace probíhá během [`AuthenticateRequest` události](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx).

Dalším důležitým modulem HTTP je [`UrlAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx), která se vyvolá v reakci na [událost`AuthorizeRequest`](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx) (která se stane po `AuthenticateRequest` události). `UrlAuthorizationModule` prověřuje označení konfigurace v `Web.config` a určí, jestli aktuální identita má oprávnění k návštěvě zadané stránky. Tento proces se nazývá *autorizace adresy URL*.

Podíváme se na syntaxi autorizačních pravidel URL v kroku 1, ale nejprve se podíváme na to, co `UrlAuthorizationModule` v závislosti na tom, jestli je požadavek autorizovaný. Pokud `UrlAuthorizationModule` zjistí, že je žádost autorizována, nedělá nic a požadavek pokračuje v průběhu svého životního cyklu. Pokud ale požadavek *není autorizovaný,* `UrlAuthorizationModule` přeruší životní cyklus a vydá pokyn objektu `Response`, aby vrátil [neautorizovaný stav HTTP 401](http://www.checkupdown.com/status/E401.html) . Pokud používáte ověřování pomocí formulářů, tento stav HTTP 401 se nikdy nevrátí klientovi, protože pokud `FormsAuthenticationModule` zjistí stav HTTP 401, změní se na [přesměrování http 302](http://www.checkupdown.com/status/E302.html) na přihlašovací stránku.

Obrázek 1 znázorňuje pracovní postup ASP.NET kanálu, `FormsAuthenticationModule`a `UrlAuthorizationModule`, když dorazí na neautorizovaný požadavek. Konkrétně obrázek 1 ukazuje žádost anonymního návštěvníka pro `ProtectedPage.aspx`, což je stránka, která odepře přístup anonymním uživatelům. Vzhledem k tomu, že je návštěvník anonymní, `UrlAuthorizationModule` přeruší požadavek a vrátí neautorizovaný stav HTTP 401. `FormsAuthenticationModule` pak převede stav 401 na přihlašovací stránku 302 přesměrování na. Po ověření uživatele prostřednictvím přihlašovací stránky se přesměruje na `ProtectedPage.aspx`. Tentokrát `FormsAuthenticationModule` identifikuje uživatele na základě ověřovacího lístku. Teď, když je návštěvník ověřený, `UrlAuthorizationModule` povoluje přístup k této stránce.

[![ověřování formulářů a pracovní postup pro autorizaci adres URL](user-based-authorization-cs/_static/image2.png)](user-based-authorization-cs/_static/image1.png)

**Obrázek 1**: ověřování formulářů a pracovní postup pro autorizaci adres URL ([kliknutím zobrazíte obrázek v plné velikosti](user-based-authorization-cs/_static/image3.png))

Obrázek 1 znázorňuje interakci, ke které dochází, když se anonymní návštěvník pokusí získat přístup k prostředku, který není k dispozici pro anonymní uživatele. V takovém případě se anonymní návštěvník přesměruje na přihlašovací stránku se stránkou, která se pokusila navštívit určenou v řetězci QueryString. Jakmile se uživatel úspěšně přihlásí, automaticky se přesměruje zpátky na prostředek, který se původně pokoušel o zobrazení.

Když anonymní uživatel neautorizovaný požadavek provede, je tento pracovní postup jednoduchý a může návštěvníkovi pochopit, co se stalo a proč. Mějte ale na paměti, že `FormsAuthenticationModule` *přesměruje* neoprávněného uživatele na přihlašovací stránku, a to i v případě, že žádost provádí ověřený uživatel. To může vést k matoucímu uživatelskému prostředí, pokud se ověřený uživatel pokusí navštívit stránku, pro kterou nemá oprávnění.

Představte si, že náš web měl nakonfigurovaná autorizační pravidla URL tak, aby stránka ASP.NET `OnlyTito.aspx`a accessibly jenom na tito. Nyní si představte, že Sam navštíví lokalitu, přihlásí se a potom se pokusí navštívit `OnlyTito.aspx`. `UrlAuthorizationModule` zastaví životní cyklus požadavků a vrátí neautorizovaný stav HTTP 401, který `FormsAuthenticationModule` detekuje a pak přesměruje Sam na přihlašovací stránku. Vzhledem k tomu, že správce Sam už je přihlášený, může to ale být na to, že se pošle zpátky na přihlašovací stránku. Může to znamenat, že se přihlašovací údaje ztratily nějakým způsobem nebo že zadaly neplatné přihlašovací údaje. Pokud Sam znovu zadá své přihlašovací údaje z přihlašovací stránky, přihlásí se (znovu) a přesměruje na `OnlyTito.aspx`. `UrlAuthorizationModule` zjistí, že se na tuto stránku nemůže navštívit správce Sam, a vrátí se na přihlašovací stránku.

Obrázek 2 znázorňuje toto matoucí pracovní postup.

[![výchozí pracovní postup může vést k matoucímu cyklu](user-based-authorization-cs/_static/image5.png)](user-based-authorization-cs/_static/image4.png)

**Obrázek 2**: výchozí pracovní postup může vést k matoucímu cyklu ([kliknutím zobrazíte obrázek v plné velikosti).](user-based-authorization-cs/_static/image6.png)

Pracovní postup znázorněný na obrázku 2 může rychle befuddle i na nejvíc počítačové návštěvníky. Podíváme se na způsoby, jak zamezit tomuto cyklu nematoucí v kroku 2.

> [!NOTE]
> ASP.NET pomocí dvou mechanismů určuje, zda má aktuální uživatel přístup ke konkrétní webové stránce: ověřování adres URL a autorizace souborů. Autorizace souborů je implementována [`FileAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx), která určuje autoritu v rámci konzultací k požadovaným seznamům ACL souborů. Autorizace souborů se nejčastěji používá při ověřování systému Windows, protože seznamy ACL jsou oprávnění, která platí pro účty systému Windows. Při použití ověřování pomocí formulářů se všechny požadavky na úrovni operačního systému a systému souborů spouští stejným účtem systému Windows, bez ohledu na to, uživatel navštívil web. Vzhledem k tomu, že se série kurzů zaměřuje na ověřování prostřednictvím formulářů, nebudeme se zabývat autorizací souborů.

### <a name="the-scope-of-url-authorization"></a>Rozsah ověřování URL

`UrlAuthorizationModule` je spravovaný kód, který je součástí modulu runtime ASP.NET. Před verzí 7 webového serveru [Internetová informační služba](https://www.iis.net/) od Microsoftu existovala odlišná bariéra mezi KANÁLEM HTTP služby IIS a kanálem běhového prostředí ASP.NET. V krátkém formátu IIS 6 a starší, ASP. `UrlAuthorizationModule` netto se spustí jenom v případě, že je požadavek delegovaný ze služby IIS na modul runtime ASP.NET. Ve výchozím nastavení služba IIS zpracovává statický obsah, jako jsou stránky HTML a šablony stylů CSS, JavaScript a image – a funguje jenom v případě, že se požaduje stránka s rozšířením `.aspx`, `.asmx`nebo `.ashx`.

Služba IIS 7 ale umožňuje integrované kanály IIS a ASP.NET. S několika nastaveními konfigurace můžete nastavit službu IIS 7, aby vyvolala `UrlAuthorizationModule` pro *všechny* požadavky, což znamená, že AUTORIZAČNÍ pravidla URL je možné definovat pro soubory libovolného typu. Kromě toho služba IIS 7 zahrnuje vlastní autorizační modul URL. Další informace o integraci ASP.NET a funkci nativní URL autorizace služby IIS 7 najdete v tématu [Principy ověřování adres URL IIS7](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization). Podrobnější pohled na ASP.NET a integraci služby IIS 7 najdete v části Shahram khosravi Book, *Professional Professional IIS 7 a ASP.NET Integration Programming* (ISBN: 978-0470152539).

V kostce se ve verzích starších než IIS 7 používají autorizační pravidla URL jenom u prostředků zpracovávaných modulem runtime ASP.NET. Ale u služby IIS 7 je možné používat funkci autorizace nativní adresy URL služby IIS nebo integrovat ASP. NET se `UrlAuthorizationModule` do kanálu HTTP služby IIS, čímž se tato funkce rozšíří na všechny požadavky.

> [!NOTE]
> V prostředí ASP je ještě několik drobných rozdílů. Autorizační pravidla pro `UrlAuthorizationModule` a funkce ověřování URL služby IIS 7 zpracovávají autorizační pravidla. V tomto kurzu se nezkoumají funkce autorizace adresy URL služby IIS 7 ani rozdíly v tom, jak analyzují autorizační pravidla ve srovnání s `UrlAuthorizationModule`. Další informace o těchto tématech najdete v dokumentaci ke službě IIS 7 na webu MSDN nebo na adrese [www.IIS.NET](https://www.iis.net/).

## <a name="step-1-defining-url-authorization-rules-inwebconfig"></a>Krok 1: definování autorizačních pravidel URL v`Web.config`

`UrlAuthorizationModule` určuje, jestli udělit nebo odepřít přístup k požadovanému prostředku pro konkrétní identitu na základě autorizačních pravidel URL definovaných v konfiguraci aplikace. Autorizační pravidla jsou zapsána v [prvku`<authorization>`](https://msdn.microsoft.com/library/8d82143t.aspx) ve formě `<allow>` a `<deny>` podřízených prvků. Každý `<allow>` a podřízený element `<deny>` může určovat:

- Konkrétní uživatel
- Seznam uživatelů oddělených čárkami
- Všichni anonymní uživatelé označeni otazníkem (?)
- Všichni uživatelé, označená hvězdičkou (\*)

Následující kód ukazuje, jak používat autorizační pravidla URL k tomu, aby uživatelé tito a Scott a odepřeli všechny ostatní:

[!code-xml[Main](user-based-authorization-cs/samples/sample1.xml)]

Element `<allow>` definuje, co jsou uživatelé povoleni – tito a Scott – zatímco `<deny>` element instruuje, že *Všichni* uživatelé mají odepřený přístup.

> [!NOTE]
> Prvky `<allow>` a `<deny>` mohou také určovat autorizační pravidla pro role. V budoucím kurzu budeme kontrolovat autorizaci na základě rolí.

Následující nastavení udělí přístup komukoli jinému než Sam (včetně anonymních návštěvníků):

[!code-xml[Main](user-based-authorization-cs/samples/sample2.xml)]

Pokud chcete povoleným pouze ověřeným uživatelům, použijte následující konfiguraci, která odepře přístup všem anonymním uživatelům:

[!code-xml[Main](user-based-authorization-cs/samples/sample3.xml)]

Autorizační pravidla jsou definována v rámci prvku `<system.web>` v `Web.config` a platí pro všechny prostředky ASP.NET ve webové aplikaci. Často má aplikace různá autorizační pravidla pro různé oddíly. Například na webu elektronického obchodování mohou všichni návštěvníci posuzuje produkty, zobrazit recenze produktů, Hledat v katalogu a tak dále. Registraci nebo stránky pro správu historie expedice se ale můžou dosáhnout jenom ověřených uživatelů. Kromě toho mohou být k dispozici části webu, které jsou přístupné pouze pro vybrané uživatele, například pro správce webu.

ASP.NET usnadňuje definování různých autorizačních pravidel pro různé soubory a složky v lokalitě nástroje. Autorizační pravidla zadaná v souboru `Web.config` kořenové složky se vztahují na všechny prostředky ASP.NET v lokalitě. Tato výchozí nastavení autorizace se ale dají přepsat pro určitou složku přidáním `Web.config` s oddílem `<authorization>`.

Pojďme aktualizovat náš web tak, aby na stránkách ASP.NET ve složce `Membership` mohli navštívit jenom ověření uživatelé. K tomu musíme přidat soubor `Web.config` do složky `Membership` a nastavit jeho autorizační nastavení tak, aby odepřelo anonymní uživatele. Pravým tlačítkem myši klikněte na složku `Membership` v Průzkumník řešení, vyberte nabídku Přidat novou položku z kontextové nabídky a přidejte nový soubor webové konfigurace s názvem `Web.config`.

[![přidat soubor Web. config do složky členství](user-based-authorization-cs/_static/image8.png)](user-based-authorization-cs/_static/image7.png)

**Obrázek 3**: přidání souboru `Web.config` do složky `Membership` ([kliknutím zobrazíte obrázek v plné velikosti](user-based-authorization-cs/_static/image9.png))

V tomto okamžiku by měl projekt obsahovat dva `Web.config` soubory: jeden v kořenovém adresáři a druhý ve složce `Membership`.

[![by vaše aplikace měla teď obsahovat dva soubory Web. config](user-based-authorization-cs/_static/image11.png)](user-based-authorization-cs/_static/image10.png)

**Obrázek 4**: vaše aplikace by teď měla obsahovat dva soubory `Web.config` ([kliknutím zobrazíte obrázek v plné velikosti).](user-based-authorization-cs/_static/image12.png)

Aktualizujte konfigurační soubor ve složce `Membership` tak, aby zakázal přístup anonymním uživatelům.

[!code-xml[Main](user-based-authorization-cs/samples/sample4.xml)]

A je to!

Pokud chcete tuto změnu vyzkoušet, navštivte domovskou stránku v prohlížeči a ujistěte se, že jste odhlášeni. Vzhledem k tomu, že výchozí chování aplikace ASP.NET je umožnit všem návštěvníkům, a vzhledem k tomu, že jsme neudělali žádné autorizační změny v souboru `Web.config` kořenového adresáře, můžeme navštívit soubory v kořenovém adresáři jako anonymní návštěvník.

Klikněte na odkaz vytvořit uživatelské účty, který se nachází v levém sloupci. Tím přejdete na `~/Membership/CreatingUserAccounts.aspx`. Vzhledem k tomu, že soubor `Web.config` v `Membership` složce definuje autorizační pravidla pro zákaz anonymního přístupu, přeruší požadavek `UrlAuthorizationModule` a vrátí neautorizovaný stav HTTP 401. `FormsAuthenticationModule` tuto hodnotu změní na stav přesměrování 302, který nám posílá na přihlašovací stránku. Všimněte si, že se stránka, ke které se pokoušíte získat přístup (`CreatingUserAccounts.aspx`), předává přihlašovací stránce prostřednictvím parametru `ReturnUrl` QueryString.

[![vzhledem k tomu, že autorizační pravidla URL zakazují anonymní přístup, přesměruje se na přihlašovací stránku.](user-based-authorization-cs/_static/image14.png)](user-based-authorization-cs/_static/image13.png)

**Obrázek 5**: vzhledem k tomu, že AUTORIZAČNÍ pravidla URL zakazují anonymní přístup, přesměrujeme na přihlašovací stránku ([kliknutím zobrazíte obrázek v plné velikosti).](user-based-authorization-cs/_static/image15.png)

Po úspěšném přihlášení se přesměruje na stránku `CreatingUserAccounts.aspx`. Tentokrát `UrlAuthorizationModule` umožňuje přístup k této stránce, protože už nepoužíváme anonymní.

### <a name="applying-url-authorization-rules-to-a-specific-location"></a>Použití autorizačních pravidel URL na konkrétní umístění

Nastavení autorizace definovaná v části `<system.web>` `Web.config` platí pro všechny prostředky ASP.NET v tomto adresáři a v jeho podadresářích (dokud není přepsáno jiným `Web.config` souborem). V některých případech ale můžeme chtít, aby všechny ASP.NET prostředky v daném adresáři měly konkrétní konfiguraci autorizace s výjimkou jedné nebo dvě konkrétní stránky. Toho je možné dosáhnout přidáním prvku `<location>` v `Web.config`, nasměrováním na soubor, jehož autorizační pravidla se liší a definováním jeho jedinečných autorizačních pravidel v něm.

Chcete-li předejít použití prvku `<location>` k přepsání nastavení konfigurace pro konkrétní prostředek, přizpůsobte nastavení autorizace, aby bylo možné navštívit `CreatingUserAccounts.aspx`pouze tito. K tomuto účelu přidejte `<location>` element do souboru `Web.config` `Membership` složky a aktualizujte jeho značky tak, aby vypadala takto:

[!code-xml[Main](user-based-authorization-cs/samples/sample5.xml)]

Element `<authorization>` v `<system.web>` definuje výchozí autorizační pravidla URL pro prostředky ASP.NET ve složce `Membership` a jejích podsložkách. `<location>` element umožňuje potlačit tato pravidla pro konkrétní prostředek. Ve výše uvedeném kódu `<location>` element odkazuje na stránku `CreatingUserAccounts.aspx` a určuje jeho autorizační pravidla, jako je například povolit tito, ale odepřít všem ostatním.

Pokud chcete otestovat tuto změnu autorizace, začněte tím, že navštívíte web jako anonymní uživatel. Pokud se pokusíte navštívit libovolnou stránku ve složce `Membership`, například `UserBasedAuthorization.aspx`, `UrlAuthorizationModule` žádost zamítne a budete přesměrováni na přihlašovací stránku. Jakmile se přihlásíte jako, například Scott, můžete navštívit libovolnou stránku ve složce `Membership` *s výjimkou* `CreatingUserAccounts.aspx`. Pokud se pokusíte navštívit `CreatingUserAccounts.aspx` přihlášeni jako kdokoli, ale tito bude mít za následek neautorizovaný přístup, budete přesměrováni zpět na přihlašovací stránku.

> [!NOTE]
> Element `<location>` musí být mimo prvek `<system.web>` konfigurace. Pro každý prostředek, jehož autorizační nastavení chcete přepsat, je nutné použít samostatný `<location>` element.

### <a name="a-look-at-how-theurlauthorizationmoduleuses-the-authorization-rules-to-grant-or-deny-access"></a>Podívejte se, jak`UrlAuthorizationModule`používá autorizační pravidla k udělení nebo odepření přístupu.

`UrlAuthorizationModule` určuje, jestli se má autorizovat konkrétní identita konkrétní adresy URL, a to tak, že se jednou analyzují autorizační pravidla adresy URL od první a funguje tak, jak je. Jakmile je nalezena shoda, uživateli je udělen nebo odepřen přístup v závislosti na tom, zda byla shoda nalezena v prvku `<allow>` nebo `<deny>`. <strong>Pokud není nalezena žádná shoda, uživateli je udělen přístup.</strong> Proto pokud chcete omezit přístup, je nezbytné použít `<deny>` prvek jako poslední prvek v konfiguraci autorizace adresy URL. <strong>Vynecháte-li</strong> <strong>`<deny>`</strong> <strong>element, budou přístupní všichni uživatelé uděleni.</strong>

Pro lepší pochopení procesu používaného `UrlAuthorizationModule` k určení autority zvažte příklady autorizačních pravidel URL, která jsme si vyhledali dříve v tomto kroku. Prvním pravidlem je `<allow>` prvek, který umožňuje přístup k tito a Scott. Druhá pravidla jsou `<deny>` prvek, který odepírá přístup všem. Pokud se anonymní uživatel navštíví, `UrlAuthorizationModule` začíná dotazem, je anonymní nebo tito? Odpověď, zjevně, je ne, takže pokračuje pro druhé pravidlo. Je anonymní v sadě každého? Vzhledem k tomu, že odpověď je tady Ano, pravidlo `<deny>` je platné a návštěvník se přesměruje na přihlašovací stránku. Podobně platí, `UrlAuthorizationModule` že pokud se Jisun na návštěvu, spouští se dotazování, je Jisun buď Scott, nebo tito? Vzhledem k tomu, že se `UrlAuthorizationModule` pokračuje na druhou otázku, je Jisun v sadě od sebe? Je to proto, že je to také odepřený přístup. Nakonec, pokud jsou tito návštěvy, první otázka, kterou představuje `UrlAuthorizationModule`, je kladná odpověď, takže tito má udělen přístup.

Vzhledem k tomu, že `UrlAuthorizationModule` zpracovává autorizační pravidla shora dolů a zastavuje se v jakémkoli porovnání, je důležité, abyste pocházeli s dalšími konkrétními pravidly před méně specifickými. To znamená, že k definování autorizačních pravidel, která zakazují Jisun a anonymním uživatelům, ale povolíte všem ostatním ověřeným uživatelům, začnete s nejpřesnější pravidly – to znamená, že to bude mít dopad na Jisun – a pak přejít na méně specifická pravidla – to vše umožní ověření uživatelé, ale zamítnutí všech anonymních uživatelů. Následující autorizační pravidla URL implementují tuto zásadu tak, že nejprve odmítnou Jisun a pak odepře anonymního uživatele. Všem ověřeným uživatelům, kteří nejsou Jisun, se udělí přístup, protože žádný z těchto příkazů `<deny>` nebude odpovídat.

[!code-xml[Main](user-based-authorization-cs/samples/sample6.xml)]

## <a name="step-2-fixing-the-workflow-for-unauthorized-authenticated-users"></a>Krok 2: Oprava pracovního postupu pro neautorizované a ověřené uživatele

Jak jsme se už dozvěděli v tomto kurzu v části, kde se podíváme na oddíl autorizační pracovní postup URL, kdykoli se neautorizovaný požadavek vystaví, `UrlAuthorizationModule` přeruší požadavek a vrátí neautorizovaný stav HTTP 401. Tento stav 401 je změněn `FormsAuthenticationModule` do stavu přesměrování 302, který odesílá uživatele do přihlašovací stránky. Tento pracovní postup probíhá na jakékoli neautorizované žádosti, i když je uživatel ověřený.

Vrácení ověřeného uživatele na přihlašovací stránku je pravděpodobně Zaměňujte, protože již bylo přihlášeno k systému. V případě nedostatku práce můžeme tento pracovní postup vylepšit přesměrováním ověřených uživatelů, kteří se pokusili o přístup na stránku s omezeným oprávněním.

Začněte vytvořením nové stránky ASP.NET v kořenové složce webové aplikace s názvem `UnauthorizedAccess.aspx`; Nezapomeňte tuto stránku přidružit k `Site.master` hlavní stránkou. Po vytvoření této stránky odeberte ovládací prvek obsahu, který odkazuje na `LoginContent` ContentPlaceHolder, aby se zobrazil výchozí obsah stránky předlohy. Dále přidejte zprávu, která vysvětluje situaci, a to tak, že se uživatel pokusil získat přístup k chráněnému prostředku. Po přidání takové zprávy by deklarativní označení stránky `UnauthorizedAccess.aspx` mělo vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](user-based-authorization-cs/samples/sample7.aspx)]

Teď je potřeba změnit pracovní postup tak, aby v případě, že ověřený uživatel provádí neautorizovaný požadavek, odesílaly na `UnauthorizedAccess.aspx` stránku místo přihlašovací stránky. Logika, která přesměruje neautorizované požadavky na přihlašovací stránku, je ukryto v rámci soukromé metody třídy `FormsAuthenticationModule`, takže nemůžeme toto chování přizpůsobit. K tomu můžeme přidat vlastní logiku na přihlašovací stránku, která uživatele přesměruje na `UnauthorizedAccess.aspx`(v případě potřeby).

Když `FormsAuthenticationModule` přesměruje neoprávněného návštěvníka na přihlašovací stránku, připojí k řetězci dotazu požadovanou neautorizovanou adresu URL s názvem `ReturnUrl`. Například pokud se neoprávněný uživatel pokusí navštívit `OnlyTito.aspx`, `FormsAuthenticationModule` ho přesměruje na `Login.aspx?ReturnUrl=OnlyTito.aspx`. Proto pokud je přihlašovací stránka dosažitelná ověřeným uživatelem pomocí řetězce dotazu QueryString, který obsahuje parametr `ReturnUrl`, víme, že tento neověřený uživatel se právě pokusil navštívit stránku, která nemá oprávnění k zobrazení. V takovém případě chceme přesměrovat na `UnauthorizedAccess.aspx`.

K tomu je potřeba přidat následující kód k obslužné rutině události `Page_Load` přihlašovací stránky:

[!code-csharp[Main](user-based-authorization-cs/samples/sample8.cs)]

Výše uvedený kód přesměruje ověřené a neoprávněné uživatele na stránku `UnauthorizedAccess.aspx`. Pokud chcete zobrazit tuto logiku v akci, přejděte na web jako anonymní návštěvník a klikněte na odkaz vytvoření uživatelských účtů v levém sloupci. Tím přejdete na stránku `~/Membership/CreatingUserAccounts.aspx`, která v kroku 1 byla nakonfigurována tak, aby povolovala přístup pouze k tito. Vzhledem k tomu, že anonymní uživatelé jsou zakázáni, `FormsAuthenticationModule` přesměrovává zpět na přihlašovací stránku.

V tuto chvíli jsou anonymní, takže `Request.IsAuthenticated` vrátí `false` a nebudeme přesměrováni na `UnauthorizedAccess.aspx`. Místo toho se zobrazí přihlašovací stránka. Přihlaste se jako jiný uživatel než tito, jako je například Bruce. Po zadání příslušných přihlašovacích údajů se na přihlašovací stránce přesměruje zpět na `~/Membership/CreatingUserAccounts.aspx`. Vzhledem k tomu, že je tato stránka dostupná jenom pro tito, nemůžeme ji zobrazit a zobrazí se výzva k jejímu vrácení na přihlašovací stránce. Tentokrát ale `Request.IsAuthenticated` vrátí `true` (a existuje `ReturnUrl` parametr řetězce dotazu), takže jsme přesměrováni na stránku `UnauthorizedAccess.aspx`.

[![ověřeno, neoprávnění uživatelé budou přesměrováni na UnauthorizedAccess. aspx.](user-based-authorization-cs/_static/image17.png)](user-based-authorization-cs/_static/image16.png)

**Obrázek 6**: ověřený, neoprávnění uživatelé jsou přesměrováni na `UnauthorizedAccess.aspx` ([kliknutím zobrazíte obrázek v plné velikosti).](user-based-authorization-cs/_static/image18.png)

Tento přizpůsobený pracovní postup prezentuje více rozumné a uživatelsky jasné uživatelské prostředí na základě krátkého okruhu cyklu znázorněného na obrázku 2.

## <a name="step-3-limiting-functionality-based-on-the-currently-logged-in-user"></a>Krok 3: omezení funkčnosti na základě aktuálně přihlášeného uživatele

Autorizace adres URL usnadňuje zadání hrubých autorizačních pravidel. Jak jsme viděli v kroku 1, s autorizací adresy URL můžeme stručně zjistit, jaké identity jsou povolené a které z nich jsou odepřené zobrazení konkrétní stránky nebo všech stránek ve složce. V některých scénářích ale můžeme chtít, aby všichni uživatelé navštívili stránku, ale omezili funkčnost stránky na základě toho, kdo na ni uživatel navštíví.

Vezměte v úvahu případ webu elektronického obchodování, který umožňuje ověřeným návštěvníkům zkontrolovat své produkty. Když anonymní uživatel navštíví stránku produktu, uvidí jenom informace o produktu a nedostal by příležitost opustit kontrolu. Ověřený uživatel, který navštívil stejnou stránku, ale uvidí rozhraní revize. Pokud ověřený uživatel dosud nezkontroloval tento produkt, rozhraní jim umožní odeslat recenzi. v opačném případě by se jim zobrazila dříve odeslaná revize. Pokud chcete tento scénář provést podrobněji, stránka produktu může zobrazit další informace a nabízet rozšířené funkce pro uživatele, kteří pracují s elektronického obchodováníou společností. Například stránka produktu může obsahovat seznam inventáře v zásobách a možnosti pro úpravu ceny a popisu produktu, když ho zaměstnanec navštíví.

Tato pravidla autorizace jemného zrnitosti lze implementovat deklarativně nebo programově (nebo prostřednictvím některé kombinace dvou). V další části se dozvíte, jak implementovat jemnou autorizaci pomocí ovládacího prvku LoginView. Podle toho budeme zkoumat programové techniky. Než se budeme moct podívat na použití jemných autorizačních pravidel, nejdřív musíme vytvořit stránku, jejíž funkce závisí na uživateli, který ho navštíví.

Pojďme vytvořit stránku, která obsahuje seznam souborů v konkrétním adresáři v prvku GridView. Spolu s výpisem názvu, velikosti a dalších informací o jednotlivých souborech bude prvek GridView obsahovat dva sloupce LinkButtons: jedno zobrazení s názvem a jedna s názvem odstranit. Pokud se klikne na zobrazení LinkButton, zobrazí se obsah vybraného souboru. Pokud kliknete na Odstranit LinkButton, soubor se odstraní. Zpočátku tuto stránku vytvoříme tak, aby její funkce zobrazení a odstranění byla dostupná pro všechny uživatele. V části použití ovládacího prvku LoginView a programově omezeného počtu funkcí se dozvíte, jak povolit nebo zakázat tyto funkce na základě uživatele navštíveného na stránce.

> [!NOTE]
> ASP.NET stránka pro sestavení používá ovládací prvek GridView k zobrazení seznamu souborů. Vzhledem k tomu, že se řada kurzů zaměřuje na ověřování prostřednictvím formulářů, autorizaci, uživatelské účty a role, Nechci strávit příliš mnoho času, který by probral vnitřní práci ovládacího prvku GridView. I když tento kurz obsahuje konkrétní podrobné pokyny pro nastavení této stránky, neuvádí podrobnosti o tom, proč byly určité volby provedeny, nebo jaké konkrétní vlastnosti mají na Vykreslený výstup. Důkladné přezkoumání ovládacího prvku GridView najdete *[v části práce s daty v řadě kurzů ASP.NET 2,0](../../data-access/index.md)* .

Začněte tím, že otevřete soubor `UserBasedAuthorization.aspx` ve složce `Membership` a přidáte ovládací prvek GridView na stránku s názvem `FilesGrid`. Z inteligentní značky GridView klikněte na odkaz Upravit sloupce a otevřete tak dialogové okno pole. Z tohoto místa zrušte zaškrtnutí políčka automaticky generovat pole v levém dolním rohu. Dále přidejte tlačítko vybrat, tlačítko Odstranit a dvě BoundFields z levého horního rohu (tlačítka Vybrat a odstranit lze najít v CommandField typu). Nastavte vlastnost `SelectText` tlačítka pro výběr tak, aby se zobrazila, a první vlastnosti `HeaderText` a `DataField` na název. Nastavte vlastnost `HeaderText` druhé vlastnost BoundField na velikost v bajtech, její vlastnost `DataField` na hodnotu Length, vlastnost `DataFormatString` na {0:N0} a vlastnost `HtmlEncode` na hodnotu false (NEPRAVDA).

Po nakonfigurování sloupců prvku GridView kliknutím na tlačítko OK zavřete dialogové okno pole. Z okno Vlastnosti nastavte vlastnost `DataKeyNames` prvku GridView na `FullName`. V tomto okamžiku by deklarativní označení prvku GridView mělo vypadat takto:

[!code-aspx[Main](user-based-authorization-cs/samples/sample9.aspx)]

S vytvořenými značkami prvku GridView jsme připraveni napsat kód, který načte soubory do konkrétního adresáře a vytvoří jejich vazby na prvek GridView. Přidejte následující kód do obslužné rutiny události `Page_Load` stránky:

[!code-csharp[Main](user-based-authorization-cs/samples/sample10.cs)]

Výše uvedený kód používá [třídu`DirectoryInfo`](https://msdn.microsoft.com/library/system.io.directoryinfo.aspx) k získání seznamu souborů v kořenové složce aplikace. [Metoda`GetFiles()`](https://msdn.microsoft.com/library/system.io.directoryinfo.getfiles.aspx) vrátí všechny soubory v adresáři jako pole [`FileInfo` objektů](https://msdn.microsoft.com/library/system.io.fileinfo.aspx), které jsou následně svázány s prvku GridView. Objekt `FileInfo` má sortiment vlastností, jako jsou `Name`, `Length`a `IsReadOnly`, mimo jiné. Jak vidíte z jeho deklarativní značky, prvek GridView zobrazí pouze vlastnosti `Name` a `Length`.

> [!NOTE]
> Třídy `DirectoryInfo` a `FileInfo` se nacházejí v [oboru názvů`System.IO`](https://msdn.microsoft.com/library/system.io.aspx). Proto bude nutné, aby tyto názvy tříd měly název oboru názvů nebo aby se obor názvů importoval do souboru třídy (prostřednictvím `using System.IO`).

Chvíli počkejte, než navštívíte tuto stránku prostřednictvím prohlížeče. Zobrazí se seznam souborů umístěných v kořenovém adresáři aplikace. Kliknutím na některý z zobrazení nebo odstraněním LinkButtons dojde k postbacku, ale nedojde k žádné akci, protože ještě jsme vytvořili potřebné obslužné rutiny událostí.

[![je v prvku GridView uveden seznam souborů v kořenovém adresáři webové aplikace.](user-based-authorization-cs/_static/image20.png)](user-based-authorization-cs/_static/image19.png)

**Obrázek 7**: v prvku GridView jsou uvedeny soubory v kořenovém adresáři webové aplikace ([kliknutím zobrazíte obrázek v plné velikosti).](user-based-authorization-cs/_static/image21.png)

Pro zobrazení obsahu vybraného souboru potřebujeme prostředky. Vraťte se do sady Visual Studio a přidejte textové pole s názvem `FileContents` nad prvek GridView. Vlastnost `TextMode` nastavte na `MultiLine` a vlastnosti `Columns` a `Rows` na 95% a 10 v uvedeném pořadí.

[!code-aspx[Main](user-based-authorization-cs/samples/sample11.aspx)]

Dále vytvořte obslužnou rutinu události pro [událost`SelectedIndexChanged`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindexchanged.aspx) prvku GridView a přidejte následující kód:

[!code-csharp[Main](user-based-authorization-cs/samples/sample12.cs)]

Tento kód používá vlastnost `SelectedValue` prvku GridView k určení úplného názvu souboru vybraného souboru. Interně se na kolekci `DataKeys` odkazuje, aby získala `SelectedValue`, takže je nutné nastavit vlastnost `DataKeyNames` prvku GridView na název, jak je popsáno výše v tomto kroku. [Třída`File`](https://msdn.microsoft.com/library/system.io.file.aspx) slouží ke čtení obsahu vybraného souboru do řetězce, který je poté přiřazen vlastnosti `Text` textového pole `FileContents` a zobrazuje obsah vybraného souboru na stránce.

[![obsah vybraného souboru se zobrazí v textovém poli.](user-based-authorization-cs/_static/image23.png)](user-based-authorization-cs/_static/image22.png)

**Obrázek 8**: obsah vybraného souboru se zobrazí v textovém poli ([kliknutím zobrazíte obrázek v plné velikosti).](user-based-authorization-cs/_static/image24.png)

> [!NOTE]
> Pokud zobrazíte obsah souboru, který obsahuje kód HTML, a pak se pokusíte zobrazit nebo odstranit soubor, zobrazí se chyba `HttpRequestValidationException`. K tomu dochází z důvodu zpětného odeslání obsahu textového pole zpět na webový server. Ve výchozím nastavení ASP.NET `HttpRequestValidationException` vyvolá chybu při každém zjištění potenciálně nebezpečného obsahu zpětného volání, jako je například kód HTML. Chcete-li zakázat výskyt této chyby, vypněte žádost o ověření stránky přidáním `ValidateRequest="false"` do direktivy `@Page`. Další informace o výhodách ověření požadavků a o tom, jaká preventivní opatření byste měli provést při jeho zakázání, najdete v tématu [ověření žádosti o ověření – předcházení útokům pomocí skriptů](https://asp.net/learn/whitepapers/request-validation/).

Nakonec přidejte obslužnou rutinu události s následujícím kódem pro [událost`RowDeleting`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleting.aspx)prvku GridView:

[!code-csharp[Main](user-based-authorization-cs/samples/sample13.cs)]

Kód jednoduše zobrazí úplný název souboru, který se má odstranit, do textového pole `FileContents`, *aniž by* soubor skutečně odstranil.

[![kliknutí na tlačítko Odstranit soubor ve skutečnosti neodstraní.](user-based-authorization-cs/_static/image26.png)](user-based-authorization-cs/_static/image25.png)

**Obrázek 9**: kliknutím na tlačítko Odstranit soubor ve skutečnosti neodstraníte ([kliknutím zobrazíte obrázek v plné velikosti).](user-based-authorization-cs/_static/image27.png)

V kroku 1 jsme nakonfigurovali autorizační pravidla URL, která uživatelům brání v prohlížení stránek ve složce `Membership`. Aby bylo možné lépe vykazovat ověřování jemných zrn, umožněte anonymním uživatelům navštívit stránku `UserBasedAuthorization.aspx`, ale s omezenými funkcemi. Chcete-li otevřít tuto stránku pro všechny uživatele, přidejte následující prvek `<location>` do souboru `Web.config` ve složce `Membership`:

[!code-xml[Main](user-based-authorization-cs/samples/sample14.xml)]

Po přidání tohoto prvku `<location>` otestujte nová autorizační pravidla adresy URL odhlášením z lokality. Jako anonymní uživatel byste měli mít oprávnění navštívit stránku `UserBasedAuthorization.aspx`.

V současné době může kterýkoli ověřený nebo anonymní uživatel navštívit stránku `UserBasedAuthorization.aspx` a zobrazovat nebo odstraňovat soubory. Pojďme to udělat, aby jenom ověření uživatelé mohli zobrazit obsah souboru a jenom tito může odstranit soubor. Tato pravidla autorizace jemného zrnitosti lze použít deklarativně, programově nebo prostřednictvím kombinace obou metod. Pojďme použít deklarativní přístup k omezení toho, kdo může zobrazit obsah souboru; pomocí programového přístupu můžete omezit, kdo může soubor odstranit.

### <a name="using-the-loginview-control"></a>Použití ovládacího prvku LoginView

Jak jsme viděli v minulých kurzech, ovládací prvek LoginView je užitečný pro zobrazení různých rozhraní pro ověřené a anonymní uživatele a nabízí snadný způsob, jak skrýt funkce, které nejsou přístupné anonymním uživatelům. Vzhledem k tomu, že anonymní uživatelé nemohou soubory zobrazit ani odstranit, je třeba zobrazit textové pole `FileContents` pouze v případě, že stránku navštíví ověřený uživatel. Chcete-li to dosáhnout, přidejte ovládací prvek LoginView na stránku, pojmenujte jej `LoginViewForFileContentsTextBox`a přesuňte deklarativní značku `FileContents` textového pole do `LoggedInTemplate`ovládacího prvku LoginView.

[!code-aspx[Main](user-based-authorization-cs/samples/sample15.aspx)]

Webové ovládací prvky v šablonách prvku LoginView již nejsou přímo přístupné z třídy kódu na pozadí. Například obslužné rutiny `FilesGrid` `SelectedIndexChanged` a `RowDeleting` v prvku GridView aktuálně odkazují na ovládací prvek TextBox `FileContents` s kódem, jako je:

[!code-csharp[Main](user-based-authorization-cs/samples/sample16.cs)]

Tento kód však již není platný. Přesunutím `FileContents` textového pole do `LoggedInTemplate` textového pole nelze získat přímý odkaz. Místo toho je nutné použít metodu `FindControl("controlId")` pro programové odkazování ovládacího prvku. Aktualizujte obslužné rutiny události `FilesGrid` tak, aby odkazovaly na textové pole, například:

[!code-csharp[Main](user-based-authorization-cs/samples/sample17.cs)]

Po přesunutí textového pole do `LoggedInTemplate` prvku LoginView a aktualizace kódu stránky tak, aby odkazovaly na textové pole pomocí vzoru `FindControl("controlId")`, navštivte stránku jako anonymní uživatel. Jak ukazuje obrázek 10, `FileContents` textové pole se nezobrazí. Zobrazení LinkButtoncollection se však stále zobrazuje.

[![ovládací prvek LoginView vykresluje pouze textové pole obsahů pro ověřené uživatele.](user-based-authorization-cs/_static/image29.png)](user-based-authorization-cs/_static/image28.png)

**Obrázek 10**: ovládací prvek LoginView vykresluje pouze textové pole `FileContents` pro ověřené uživatele ([kliknutím zobrazíte obrázek v plné velikosti).](user-based-authorization-cs/_static/image30.png)

Jedním ze způsobů, jak skrýt tlačítko zobrazení pro anonymní uživatele, je převést pole GridView na TemplateField. Tím se vygeneruje šablona, která obsahuje deklarativní označení pro zobrazení LinkButton. Pak můžeme do prvku TemplateField přidat ovládací prvek LoginView a umístit do něj objekt LinkButton v rámci `LoggedInTemplate`LoginView, takže se skryje tlačítko Zobrazit od anonymních návštěvníků. Chcete-li to provést, klikněte na odkaz Upravit sloupce z inteligentní značky GridView pro otevření dialogového okna pole. Potom v seznamu v levém dolním rohu vyberte tlačítko vybrat a potom klikněte na odkaz převést toto pole na odkaz TemplateField. Tím se změní deklarativní označení pole z:

[!code-aspx[Main](user-based-authorization-cs/samples/sample18.aspx)]

 Na: 

[!code-aspx[Main](user-based-authorization-cs/samples/sample19.aspx)]

V tuto chvíli můžeme přidat prvku LoginView do TemplateField. Následující kód zobrazuje zobrazení LinkButton pouze pro ověřené uživatele.

[!code-aspx[Main](user-based-authorization-cs/samples/sample20.aspx)]

Jak ukazuje obrázek 11, není konečný výsledek v podstatě, protože se sloupec zobrazení stále zobrazuje, i když je zobrazení LinkButtons v tomto sloupci skryté. V další části se podíváme na postup skrytí celého sloupce GridView (a ne jenom pro LinkButton).

[![ovládacího prvku LoginView skryje zobrazení LinkButtons pro anonymní návštěvníky.](user-based-authorization-cs/_static/image32.png)](user-based-authorization-cs/_static/image31.png)

**Obrázek 11**: ovládací prvek LoginView skrývá zobrazení LinkButtons pro anonymní návštěvníky ([kliknutím zobrazíte obrázek v plné velikosti](user-based-authorization-cs/_static/image33.png)).

### <a name="programmatically-limiting-functionality"></a>Programově omezené funkce

V některých případech jsou deklarativní techniky nedostatečné na omezení funkčnosti stránky. Například dostupnost určité funkce stránky může být závislá na kritériích, která přesahují, jestli uživatel, který stránku navštívil, je anonymní nebo ověřený. V takových případech lze různé prvky uživatelského rozhraní zobrazit nebo skrýt prostřednictvím programových prostředků.

Aby bylo možné funkce programově omezit, musíme provést dvě úlohy:

1. Určí, zda má uživatel navštěvující stránku přístup k funkcím a
2. Programově změňte uživatelské rozhraní na základě toho, jestli má uživatel přístup k příslušné funkci.

Aby bylo možné předvést použití těchto dvou úloh, umožněte pouze tito odstranit soubory z prvku GridView. Náš první úkol vám pak určí, jestli se tito na stránku. Po určení je potřeba skrýt (nebo zobrazit) odstranění sloupce prvku GridView. Sloupce prvku GridView jsou přístupné prostřednictvím jeho vlastnosti `Columns`; sloupec je vykreslen pouze v případě, že je jeho vlastnost `Visible` nastavena na hodnotu `true` (výchozí).

Přidejte následující kód do obslužné rutiny události `Page_Load` před vytvořením vazby dat do prvku GridView:

[!code-csharp[Main](user-based-authorization-cs/samples/sample21.cs)]

Jak jsme probrali v kurzu [*Přehled ověřování formulářů*](../introduction/an-overview-of-forms-authentication-cs.md) , `User.Identity.Name` vrátí název identity. To odpovídá uživatelskému jménu zadanému v přihlašovacím ovládacím prvku. Pokud se tito na stránku, vlastnost `Visible` druhého sloupce prvku GridView je nastavena na hodnotu `true`; v opačném případě je nastavená na `false`. Výsledkem netto je to, že když někdo jiný než tito navštíví stránku, buď jiného ověřeného uživatele, nebo anonymního uživatele, sloupec odstranění se nevykresluje (viz obrázek 12). Pokud však tito navštíví stránku, je k dispozici sloupec odstranění (viz obrázek 13).

[![sloupec odstranit není vykreslený, když ho navštíví někdo jiný než tito (například Bruce).](user-based-authorization-cs/_static/image35.png)](user-based-authorization-cs/_static/image34.png)

**Obrázek 12**: sloupec pro odstranění se nevykresluje, když ho navštíví někdo jiný než tito (například Bruce) ([kliknutím zobrazíte obrázek v plné velikosti).](user-based-authorization-cs/_static/image36.png)

[Vykreslí se ![odstranění sloupce pro tito.](user-based-authorization-cs/_static/image38.png)](user-based-authorization-cs/_static/image37.png)

**Obrázek 13**: vykreslí se sloupec odstranění pro tito ([kliknutím zobrazíte obrázek v plné velikosti](user-based-authorization-cs/_static/image39.png)).

## <a name="step-4-applying-authorization-rules-to-classes-and-methods"></a>Krok 4: aplikování autorizačních pravidel na třídy a metody

V kroku 3 nepovolujeme anonymním uživatelům zobrazení obsahu souboru a zakázání všech uživatelů, ale tito z odstranění souborů. To bylo provedeno skrytím přidružených prvků uživatelského rozhraní pro neoprávněné návštěvníky prostřednictvím deklarativních a programových techniků. Pro náš jednoduchý příklad byly správně skryty prvky uživatelského rozhraní, ale informace o složitějších lokalitách, kde může být mnoho různých způsobů, jak stejné funkce provádět? V rámci omezení této funkčnosti na neoprávněné uživatele co se stane, když zapomenete skrýt nebo zakázat všechny příslušné prvky uživatelského rozhraní?

Snadný způsob, jak zajistit, že konkrétnímu kusu funkcí nemůžete mít přístup neoprávněným uživatelem, je vytřídit tuto třídu nebo metodu pomocí [atributu`PrincipalPermission`](https://msdn.microsoft.com/library/system.security.permissions.principalpermissionattribute.aspx). Pokud modul runtime .NET používá třídu nebo provede některou z jeho metod, zkontroluje, zda má aktuální kontext zabezpečení oprávnění k použití třídy nebo provedení metody. Atribut `PrincipalPermission` poskytuje mechanismus, pomocí kterého můžeme definovat tato pravidla.

Pojďme pomocí atributu `PrincipalPermission` v prvku GridView `SelectedIndexChanged` a `RowDeleting` obslužné rutiny události zakázat provádění anonymních uživatelů a uživatelů než tito, v uvedeném pořadí. Vše, co je potřeba udělat, je přidat odpovídající atribut základem jednotlivé definice funkce:

[!code-csharp[Main](user-based-authorization-cs/samples/sample22.cs)]

Atribut pro `SelectedIndexChanged` obslužná rutina události Určuje, že obslužná rutina události může spustit pouze ověřený uživatel, kde atribut v obslužné rutině události `RowDeleting` omezuje spuštění na tito.

Pokud by nějaký uživatel jiný než tito se pokusil spustit obslužnou rutinu události `RowDeleting` nebo neověřený uživatel se pokusí spustit obslužnou rutinu události `SelectedIndexChanged`, modul runtime .NET vyvolá `SecurityException`.

[![je-li kontext zabezpečení autorizován pro spuštění metody, je vyvolána výjimka SecurityException](user-based-authorization-cs/_static/image41.png)](user-based-authorization-cs/_static/image40.png)

**Obrázek 14**: Pokud kontext zabezpečení nemá autorizaci ke spuštění metody, je vyvolána `SecurityException` ([kliknutím zobrazíte obrázek v plné velikosti).](user-based-authorization-cs/_static/image42.png)

> [!NOTE]
> Chcete-li více kontextům zabezpečení udělit přístup ke třídě nebo metodě, seupravte třídu nebo metodu pomocí atributu `PrincipalPermission` pro každý kontext zabezpečení. To znamená, že pokud chcete, aby tito i Bruce mohl spustit obslužnou rutinu události `RowDeleting`, přidejte *dva* atributy `PrincipalPermission`:

[!code-csharp[Main](user-based-authorization-cs/samples/sample23.cs)]

Kromě stránek ASP.NET má řada aplikací také architekturu, která zahrnuje různé vrstvy, například obchodní logiku a vrstvy přístupu k datům. Tyto vrstvy jsou obvykle implementovány jako knihovny tříd a třídy nabídky a metody pro provádění obchodní logiky a funkcionality související s daty. Atribut `PrincipalPermission` je užitečný pro použití autorizačních pravidel pro tyto vrstvy.

Další informace o použití atributu `PrincipalPermission` k definování autorizačních pravidel pro třídy a metody najdete v záznamu blogu [Scott Guthrie](https://weblogs.asp.net/scottgu/) [Přidání autorizačních pravidel do obchodních a datových vrstev pomocí `PrincipalPermissionAttributes`](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx).

## <a name="summary"></a>Přehled

V tomto kurzu jsme se podívali na to, jak použít uživatelská pravidla autorizace. Začali jsme s pohledem na ASP. Rozhraní URL pro autorizaci sítě. U každé žádosti `UrlAuthorizationModule` modul ASP.NET zkontroluje autorizační pravidla URL definovaná v konfiguraci aplikace a určí, jestli má identita oprávnění k přístupu k požadovanému prostředku. V krátkém případě autorizace adres URL usnadňuje zadání autorizačních pravidel pro konkrétní stránku nebo pro všechny stránky v konkrétním adresáři.

Autorizační rozhraní URL používá autorizační pravidla pro stránku na základě stránky. V případě autorizace adresy URL je žádost o udělení identity autorizována pro přístup k určitému prostředku, nebo ne. Mnohé z těchto scénářů ale volají pro přesnější pravidla autorizace zrnitosti. Místo toho, aby bylo možné definovat, kdo má oprávnění k přístupu na stránku, může být nutné umožnit všem uživatelům přístup ke stránce, ale k zobrazení různých dat nebo nabídnutí různých funkcí v závislosti na uživateli, který stránku navštívil. Ověřování na úrovni stránky obvykle zahrnuje skrývání specifických prvků uživatelského rozhraní, aby nedocházelo k neautorizovaným uživatelům v přístupu k zakázaným funkcím. Kromě toho je možné použít atributy k omezení přístupu ke třídám a provádění metod pro určité uživatele.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Přidání autorizačních pravidel do obchodních a datových vrstev pomocí `PrincipalPermissionAttributes`](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)
- [Autorizace ASP.NET](https://msdn.microsoft.com/library/wce3kxhd.aspx)
- [Změny mezi službami IIS6 a IIS7 Security](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [Konfigurace konkrétních souborů a podadresářů](https://msdn.microsoft.com/library/6hbkh9s7.aspx)
- [Omezení funkcí pro úpravu dat podle uživatele](../../data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-cs.md)
- [Rychlé starty ovládacího prvku LoginView](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/loginview.aspx)
- [Principy ověřování URL IIS7](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)
- [`UrlAuthorizationModule` technickou dokumentaci](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)
- [Práce s daty v ASP.NET 2,0](../../data-access/index.md)

### <a name="about-the-author"></a>O autorovi

Scott Mitchell, autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je *[Sams naučit se ASP.NET 2,0 za 24 hodin](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* . Scott se dá kontaktovat [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com).

> [!div class="step-by-step"]
> [Předchozí](validating-user-credentials-against-the-membership-user-store-cs.md)
> [Další](storing-additional-user-information-cs.md)
