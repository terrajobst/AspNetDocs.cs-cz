---
uid: signalr/overview/security/introduction-to-security
title: Seznámení se zabezpečením signalizace | Microsoft Docs
author: bradygaster
description: Popisuje problémy se zabezpečením, které je nutné vzít v úvahu při vývoji aplikace pro signalizaci.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ed562717-8591-4936-8e10-c7e63dcb570a
msc.legacyurl: /signalr/overview/security/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 24ce20b45543468de28ad017ba62d2f6e5a00f3b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558574"
---
# <a name="introduction-to-signalr-security"></a>Úvod do zabezpečení knihovnou SignalR

autorem [Fletcher](https://github.com/pfletcher), který [FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Tento článek popisuje problémy se zabezpečením, které je nutné vzít v úvahu při vývoji aplikace pro signalizaci.
>
> ## <a name="software-versions-used-in-this-topic"></a>Verze softwaru používané v tomto tématu
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - Signal – verze 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Předchozí verze tohoto tématu
>
> Informace o dřívějších verzích nástroje Signal najdete v části [Signal – starší verze](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Dotazy a komentáře
>
> Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky. Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>Přehled

Tento dokument obsahuje následující části:

- [Koncepce zabezpečení signálů](#concepts)

    - [Ověřování a autorizace](#authentication)
    - [Token připojení](#connectiontoken)
    - [Opětovné připojení skupin při opakovaném připojování](#rejoingroup)
- [Jak signál zabraňuje padělání požadavků mezi weby](#csrf)
- [Doporučení pro zabezpečení signálů](#recommendations)

    - [Protokol SSL (Secure Socket Layer)](#ssl)
    - [Nepoužívejte skupiny jako bezpečnostní mechanismus.](#groupsecurity)
    - [Bezpečné zpracování vstupu od klientů](#input)
    - [Sjednocování změny stavu uživatele s aktivním připojením](#reconcile)
    - [Automaticky generované soubory proxy JavaScriptu](#autogen)
    - [Výjimky](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a>Koncepce zabezpečení signálů

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a>Ověřování a autorizace

Signál neposkytuje žádné funkce pro ověřování uživatelů. Místo toho se funkce signalizace integrují do existující struktury ověřování pro aplikaci. Uživatele ověříte tak, jak byste v aplikaci normálně pracovali, a s výsledky ověřování v kódu vašeho signálu. Můžete například ověřit uživatele s ověřováním pomocí formulářů ASP.NET a potom v centru vynutili, kteří uživatelé nebo role jsou oprávněni volat metodu. V centru můžete k klientovi předat taky ověřovací informace, jako je uživatelské jméno nebo uživatel, který patří do role.

Signál poskytuje [autorizačnímu atributu oprávnění](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) k určení uživatelů, kteří mají přístup k rozbočovači nebo metodě. Atribut autorizovat aplikujete buď na centrum, nebo na konkrétní metody v centru. Bez atributu autorizovat jsou všechny veřejné metody v centru k dispozici klientovi, který je připojen k centru. Další informace o centrech najdete v tématu [ověřování a autorizace pro centra signálu](hub-authorization.md).

Atribut `Authorize` použijete pro centra, ale ne na trvalá připojení. Pokud chcete vynutilit autorizační pravidla při použití `PersistentConnection`, musíte přepsat metodu `AuthorizeRequest`. Další informace o trvalých připojeních najdete v tématu [ověřování a autorizace pro trvalá připojení k signalizaci](persistent-connection-authorization.md).

<a id="connectiontoken"></a>

### <a name="connection-token"></a>Token připojení

Signalizace snižuje riziko provádění škodlivých příkazů tím, že ověřuje identitu odesilatele. U každého požadavku klient a server předají token připojení, který obsahuje ID připojení a uživatelské jméno pro ověřené uživatele. ID připojení jednoznačně identifikuje každého připojeného klienta. Server náhodně generuje ID připojení při vytvoření nového připojení a uchovává toto ID po dobu trvání připojení. Ověřovací mechanismus pro webovou aplikaci poskytuje uživatelské jméno. Signál používá k ochraně tokenu připojení šifrování a digitální podpis.

![](introduction-to-security/_static/image2.png)

Pro každý požadavek Server ověří obsah tokenu, aby bylo zajištěno, že požadavek pochází od zadaného uživatele. Uživatelské jméno musí odpovídat ID připojení. Ověřením ID připojení i uživatelského jména může útočník zabránit uživateli se zlými úmysly v snadném zosobnění jiného uživatele. Pokud server nemůže ověřit token připojení, požadavek se nezdařil.

![](introduction-to-security/_static/image4.png)

Vzhledem k tomu, že ID připojení je součástí procesu ověřování, neměli byste ID připojení jednoho uživatele odhalit jiným uživatelům nebo ukládat hodnoty na klienta, například v souboru cookie.

#### <a name="connection-tokens-vs-other-token-types"></a>Tokeny připojení vs. jiné typy tokenů

Tokeny připojení jsou občas označeny pomocí nástrojů zabezpečení, protože se jeví jako tokeny relace nebo ověřovací tokeny, které představují riziko, pokud je vystaveno.

Token připojení signálu není ověřovací token. Slouží k potvrzení, že uživatel, který vytváří tuto žádost, je stejný jako ten, který vytvořil připojení. Token připojení je nezbytný, protože signál ASP.NET umožňuje připojení k pohybu mezi servery. Token přidruží připojení ke konkrétnímu uživateli, ale neuplatňuje identitu uživatele, který požadavek odeslal. Aby požadavek na signál byl správně ověřen, musí mít jiný token, který vyhodnotí identitu uživatele, jako je soubor cookie nebo nosný token. Samotný token připojení ale neprovede žádnou deklaraci identity, kterou tento požadavek provedl, protože k tomuto uživateli je přidruženo ID připojení obsažené v tokenu.

Vzhledem k tomu, že token připojení neposkytuje vlastní žádost o ověření, není považován za "relaci" nebo "ověřovací" token. Převzetí tokenu připojení daného uživatele a jeho opětovné přehrání v žádosti ověřené jako jiný uživatel (nebo neověřená žádost) selže, protože identita uživatele žádosti a identita uložená v tokenu se neshodují.

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a>Opětovné připojení skupin při opakovaném připojování

Ve výchozím nastavení aplikace signalizace automaticky znovu přiřadí uživatele do příslušných skupin při opětovném připojení k dočasnému přerušení, například při přerušení připojení a opětovném navázání před vypršením časového limitu připojení. Po opětovném připojení klient předává token skupiny, který obsahuje ID připojení a přiřazené skupiny. Token skupiny je digitálně podepsaný a zašifrovaný. Po opětovném připojení klient zachová stejné ID připojení; Proto ID připojení předané z připojeného klienta musí odpovídat předchozímu ID připojení používanému klientem. Toto ověření brání uživateli se zlými úmysly v předávání požadavků na připojení neautorizovaných skupin při opětovném připojení.

Je ale důležité si uvědomit, že vyprší platnost tokenu skupiny. Pokud uživatel patřil do skupiny v minulosti, ale byl zakázán z této skupiny, může být tento uživatel schopný napodobovat token skupiny, který obsahuje zakázanou skupinu. Pokud potřebujete zabezpečeně spravovat, kteří uživatelé patří do kterých skupin, je třeba tato data uložit na server, například do databáze. Pak přidejte do své aplikace logiku, která ověří na serveru, jestli uživatel patří do skupiny. Příklad ověření členství ve skupině najdete v tématu [práce se skupinami](../guide-to-the-api/working-with-groups.md).

Automatické opětovné připojení skupin se použije jenom v případě, že se připojení znovu připojí po dočasném přerušení. Pokud se uživatel odpojí tím, že přejde pryč z aplikace nebo restartuje aplikaci, musí aplikace zpracovat, jak tohoto uživatele přidat do správných skupin. Další informace najdete v tématu [práce se skupinami](../guide-to-the-api/working-with-groups.md).

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a>Jak signál zabraňuje padělání požadavků mezi weby

Padělání žádostí mezi weby (CSRF) je útok, kdy škodlivý web pošle požadavek na ohrožený web, ve kterém je aktuálně přihlášený uživatel. Signalizace brání CSRF, protože by škodlivý web mohl vytvořit platnou žádost pro vaši aplikaci signalizace.

### <a name="description-of-csrf-attack"></a>Popis útoku CSRF

Tady je příklad útoku CSRF:

1. Uživatel se do www.example.com přihlašuje pomocí ověřování pomocí formulářů.
2. Server ověřuje uživatele. Odpověď ze serveru obsahuje soubor cookie ověřování.
3. Uživatel navštíví škodlivý web, aniž by se odhlásil. Tento škodlivý web obsahuje následující formulář HTML:

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   Všimněte si, že akce formuláře provede příspěvky na ohrožený web, nikoli na škodlivý web. Toto je součást CSRF (pro různé lokality).
4. Uživatel klikne na tlačítko Odeslat. Prohlížeč zahrnuje ověřovací soubor cookie s požadavkem.
5. Požadavek běží na serveru example.com s kontextem ověřování uživatele a může provádět cokoli, co může ověřený uživatel dělat.

I když tento příklad vyžaduje, aby uživatel klikne na tlačítko formulář, škodlivá stránka by mohla jednoduše spustit skript, který odešle požadavek AJAX do vaší aplikace signalizace. Použití protokolu SSL navíc nebrání útoku CSRF, protože škodlivý web může odeslat žádost "https://".

Obvykle jsou útoky CSRF na weby, které používají soubory cookie pro ověřování, protože prohlížeče odesílají všechny relevantní soubory cookie do cílového webu. Nicméně útoky CSRF nejsou omezené na zneužití souborů cookie. Například základní ověřování a ověřování algoritmem Digest je také zranitelné. Když se uživatel přihlásí pomocí základního ověřování nebo ověřování hodnotou hash, prohlížeč automaticky pošle přihlašovací údaje, dokud relace neskončí.

### <a name="csrf-mitigations-taken-by-signalr"></a>CSRF zmírnění útoků prostřednictvím signalizace

Signalizace provede následující kroky, které zabrání škodlivému webu v vytváření platných požadavků do vaší aplikace. Signalizace provede následující kroky ve výchozím nastavení, není nutné provádět žádnou akci ve vašem kódu.

- **Zakázat různé požadavky na doménu** Návěstí zakáže mezidoménové požadavky, aby uživatelé nemohli volat koncový bod signalizace z externí domény. Signál považuje za neplatný požadavek z externí domény na neplatný a zablokuje požadavek. Doporučujeme, abyste zachovali toto výchozí chování; v opačném případě by škodlivý web mohl přesvědčit uživatele o odeslání příkazů do vašeho webu. Pokud potřebujete použít mezidoménové požadavky, přečtěte si téma [jak navázat připojení mezi doménami](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) .
- **Předat token připojení v řetězci dotazu, nikoli v souboru cookie** Signalizace předá token připojení jako hodnotu řetězce dotazu, nikoli jako soubor cookie. Uložení tokenu připojení v souboru cookie je nebezpečné, protože prohlížeč může neúmyslně přesměrovat token připojení, když dojde k výskytu škodlivého kódu. Předávání tokenu připojení v řetězci dotazu také brání tomu, aby token připojení trval nad rámec aktuálního připojení. Uživatel se zlými úmysly proto nemůže podat žádost v rámci ověřovacích přihlašovacích údajů jiného uživatele.
- **Ověřit token připojení** Jak je popsáno v části [token připojení](#connectiontoken) , server ví, které ID připojení je přidruženo ke každému ověřenému uživateli. Server nezpracovává žádné požadavky z ID připojení, které se neshoduje s uživatelským jménem. Je pravděpodobné, že uživatel se zlými úmysly může odhadnout platný požadavek, protože uživatel se zlými úmysly by musel znát uživatelské jméno a aktuální náhodně generované ID připojení. Toto ID připojení je neplatné, jakmile se připojení ukončí. Anonymní uživatelé by neměli mít přístup k žádným citlivým informacím.

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>Doporučení pro zabezpečení signálů

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a>Protokol SSL (Secure Socket Layer)

Protokol SSL používá šifrování k zabezpečení přenosu dat mezi klientem a serverem. Pokud vaše aplikace Signaler přenáší citlivé informace mezi klientem a serverem, použijte k přenosu protokol SSL. Další informace o nastavení SSL najdete v tématu [jak nastavit SSL na IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>Nepoužívejte skupiny jako bezpečnostní mechanismus.

Skupiny představují pohodlný způsob shromažďování souvisejících uživatelů, ale nejedná se o zabezpečený mechanismus pro omezení přístupu k citlivým informacím. To platí hlavně v případě, že se uživatelé můžou při opětovném připojení automaticky znovu připojit ke skupinám. Místo toho zvažte přidání privilegovaných uživatelů do role a omezení přístupu k metodě centra jenom na členy této role. Příklad omezení přístupu na základě role najdete v tématu [ověřování a autorizace pro centra signálu](hub-authorization.md). Příklad kontroly přístupu uživatelů ke skupinám při opětovném připojení najdete v tématu [práce se skupinami](../guide-to-the-api/working-with-groups.md).

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>Bezpečné zpracování vstupu od klientů

Chcete-li zajistit, že uživatel se zlými úmysly neodesílá skript jiným uživatelům, je nutné zakódovat všechny vstupy z klientů, kteří jsou určeni pro všesměrové vysílání ostatním klientům. Měli byste kódovat zprávy na přijímajících klientech, nikoli na serveru, protože vaše aplikace Signaler může mít mnoho různých typů klientů. Proto funkce kódování HTML funguje pro webového klienta, ale ne pro jiné typy klientů. Například metoda webového klienta pro zobrazení zprávy chatu by mohla bezpečně zpracovat uživatelské jméno a zprávu voláním funkce `html()`.

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a>Sjednocování změny stavu uživatele s aktivním připojením

Změní-li se stav ověření uživatele, když existuje aktivní připojení, uživateli se zobrazí chyba oznamující, že identita uživatele se během aktivního připojení k signalizaci nemůže změnit. V takovém případě by se vaše aplikace měla znovu připojit k serveru, aby bylo zajištěno, že je ID připojení a uživatelské jméno koordinováno. Pokud například vaše aplikace umožňuje uživateli odhlásit se v době, kdy existuje aktivní připojení, uživatelské jméno pro připojení se už nebude shodovat s názvem, který se předává pro další požadavek. Před odhlášením uživatele budete chtít zastavit připojení a pak ho znovu spustit.

Je ale důležité si uvědomit, že většina aplikací nebude muset ručně zastavit a spustit připojení. Pokud vaše aplikace přesměruje uživatele na samostatnou stránku po odhlášení, jako je například výchozí chování v aplikaci webových formulářů nebo aplikace MVC, nebo aktualizuje aktuální stránku po odhlášení, je aktivní připojení automaticky odpojeno a není vyžaduje jakoukoli další akci.

Následující příklad ukazuje, jak zastavit a spustit připojení, když se změní stav uživatele.

[!code-html[Main](introduction-to-security/samples/sample3.html)]

Nebo se může změnit stav ověřování uživatele, pokud vaše lokalita používá klouzavé vypršení platnosti s ověřováním pomocí formulářů a neexistuje žádná aktivita, která by soubor cookie pro ověřování zůstal platný. V takovém případě se uživatel odhlásí a uživatelské jméno se už nebude shodovat s uživatelským jménem v tokenu připojení. Tento problém můžete vyřešit tak, že přidáte nějaký skript, který pravidelně vyžádá prostředek na webovém serveru, aby byl soubor cookie ověřování platný. Následující příklad ukazuje, jak vyžádat prostředek každých 30 minut.

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a>Automaticky generované soubory proxy JavaScriptu

Pokud nechcete zahrnout všechna centra a metody v souboru proxy JavaScriptu pro každého uživatele, můžete zakázat automatické generování souboru. Tuto možnost si můžete vybrat, pokud máte více Center a metod, ale nechcete, aby každý uživatel měl vědět o všech metodách. Automatickou generaci zakážete nastavením **EnableJavaScriptProxies** na **false**.

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

Další informace o souborech proxy JavaScript najdete v tématu [vygenerovaný proxy server a co pro vás](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy). <a id="exceptions"></a>

### <a name="exceptions"></a>Výjimky

Měli byste se vyhnout předávání objektů výjimek klientům, protože objekty mohou klientům zobrazit citlivé informace. Místo toho zavolejte metodu na straně klienta, která zobrazí příslušnou chybovou zprávu.

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
