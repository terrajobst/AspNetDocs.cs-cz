---
uid: web-api/overview/testing-and-debugging/troubleshooting-http-405-errors-after-publishing-web-api-applications
title: Řešení potíží s webovými API2 aplikacemi, které fungují v aplikaci Visual Studio a selžou na provozním serveru služby IIS
author: rmcmurray
description: Řešení potíží s webovými API2 aplikacemi, které fungují v aplikaci Visual Studio a selžou na provozním serveru služby IIS
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 07ec7d37-023f-43ea-b471-60b08ce338f7
msc.legacyurl: /web-api/overview/testing-and-debugging/troubleshooting-http-405-errors-after-publishing-web-api-applications
msc.type: authoredcontent
ms.openlocfilehash: 1b47f1ade3619cfd010260352f6a96985ab3598b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555018"
---
# <a name="troubleshoot-web-api2-apps-that-work-in-visual-studio-and-fail-on-a-production-iis-server"></a>Řešení potíží s webovými API2 aplikacemi, které fungují v aplikaci Visual Studio a selžou na provozním serveru služby IIS

> Tento dokument vysvětluje, jak řešit potíže s webovými API2 aplikacemi, které jsou nasazené na provozní server služby IIS. Řeší běžné chyby HTTP 405 a 501.
> 
> ## <a name="software-used-in-this-tutorial"></a>Software použitý v tomto kurzu
> 
> 
> - [Internetová informační služba (IIS)](https://www.iis.net/) (verze 7 nebo novější)
> - [Webové rozhraní API](../../index.md) 

Webové aplikace API obvykle používají několik příkazů HTTP: GET, POST, PUT, DELETE a někdy PATCH. V takovém případě mohou vývojáři běžet v situacích, kdy jsou tyto operace implementovány jiným modulem IIS na svém provozním serveru služby IIS, což vede k situaci, kdy kontroler webového rozhraní API, který funguje správně v sadě Visual Studio nebo na vývojovém serveru, bude Pokud je nainstalovaná na provozní server IIS, vrátí se chyba HTTP 405.

## <a name="what-causes-http-405-errors"></a>Co způsobuje chyby HTTP 405

Prvním krokem ke studiu potíží s chybami HTTP 405 je pochopení toho, co znamená chyba HTTP 405. Hlavním řídícím dokumentem pro HTTP je [RFC 2616](http://www.ietf.org/rfc/rfc2616.txt), který definuje stavový kód HTTP 405 jako ***metoda není povolený***, a další popis tohoto stavového kódu jako situaci, kdy &quot;metoda zadaná na řádku požadavku není povolená pro prostředek identifikovaný identifikátorem Request-URI.&quot; jinými slovy není pro konkrétní adresu URL, kterou klient HTTP požaduje, povolený příkaz HTTP.

V rámci krátké recenze je tady několik nejpoužívanějších metod HTTP, které jsou definované v dokumentu RFC 2616, RFC 4918 a RFC 5789:

| HTTP – metoda | Popis |
| --- | --- |
| **GET** | Tato metoda se používá k načtení dat z identifikátoru URI a pravděpodobně nejčastěji používané metody HTTP. |
| **ZÁHLAVÍ** | Tato metoda je podobně jako metoda GET, s tím rozdílem, že ve skutečnosti nenačítá data z identifikátoru URI žádosti – jednoduše načte stav HTTP. |
| **POST** | Tato metoda se obvykle používá k posílání nových dat do identifikátoru URI. PŘÍSPĚVEK se často používá k odeslání dat formuláře. |
| **PUT** | Tato metoda se obvykle používá k posílání nezpracovaných dat do identifikátoru URI. PUT se často používá k odesílání dat JSON nebo XML do aplikací webového rozhraní API. |
| **DELETE** | Tato metoda slouží k odebrání dat z identifikátoru URI. |
| **NASTAVENÍ** | Tato metoda se obvykle používá k načtení seznamu metod HTTP, které jsou podporovány pro identifikátor URI. |
| **KOPÍROVAT PŘESUN** | Tyto dvě metody se používají s protokolem WebDAV a jejich účelem je vysvětlivek. |
| **MKCOL** | Tato metoda se používá s protokolem WebDAV a používá se k vytvoření kolekce (například adresáře) na zadaném identifikátoru URI. |
| **PROPFIND PROPPATCH** | Tyto dvě metody se používají s protokolem WebDAV a používají se k dotazování nebo nastavování vlastností pro identifikátor URI. |
| **UZAMKNOUT ODEMKNUTÍ** | Tyto dvě metody se používají s protokolem WebDAV a používají se k uzamčení nebo odemčení prostředku identifikovaného identifikátorem URI požadavku při vytváření obsahu. |
| **POUŽITA** | Tato metoda slouží k úpravě existujícího prostředku HTTP. |

Pokud je jedna z těchto metod HTTP nakonfigurovaná pro použití na serveru, server bude reagovat na stav HTTP a další data, která jsou pro požadavek vhodná. (Například metoda GET může obdržet odpověď HTTP 200 ***OK*** a metoda PUT může obdržet odpověď ***vytvořenou*** protokolem HTTP 201.)

Pokud metoda HTTP není nakonfigurovaná pro použití na serveru, server bude reagovat pomocí chyby HTTP 501, která ***není implementována*** .

Pokud je však metoda HTTP nakonfigurována pro použití na serveru, ale byla zakázána pro daný identifikátor URI, server bude reagovat s metodou HTTP 405 ***není povolena*** chyba.

## <a name="example-http-405-error"></a>Příklad chyby HTTP 405

Následující příklad požadavku HTTP a odpovědi ilustruje situaci, kdy se klient HTTP pokouší o vložení hodnoty do aplikace webového rozhraní API na webovém serveru a server vrátí chybu HTTP, která uvádí, že metoda PUT není povolená:

Požadavek HTTP:

[!code-console[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample1.cmd)]

Odpověď HTTP:

[!code-console[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample2.cmd)]

V tomto příkladu klient HTTP odeslal platnou žádost JSON k adrese URL aplikace webového rozhraní API na webovém serveru, ale server vrátil chybovou zprávu HTTP 405, která indikuje, že metoda PUT není pro tuto adresu URL povolená. Naproti tomu, pokud se identifikátor URI požadavku neshoduje s trasou pro aplikaci webového rozhraní API, Server vrátil chybu HTTP 404 ***Nenalezeno*** .

## <a name="resolve-http-405-errors"></a>Vyřešit chyby HTTP 405

Existuje několik důvodů, proč nemusí být povolen konkrétní příkaz HTTP, ale existuje jeden primární scénář, který je přední příčinou této chyby ve službě IIS: více obslužných rutin je definováno pro stejnou operaci/metodu a jedna z obslužných rutin blokuje očekávanou obslužnou rutinu od zpracování požadavku. Pomocí vysvětlení, služba IIS zpracovává obslužné rutiny od prvního až po poslední na základě záznamů obslužné rutiny Order v souborech *ApplicationHost. config* a *Web. config* , kde se pro zpracování žádosti použije první vyhovující kombinace cest, příkazů, prostředků atd.

Následující příklad je výpis ze souboru *ApplicationHost. config* pro server IIS, který vrátil chybu HTTP 405 při použití metody Put k odesílání dat do aplikace webového rozhraní API. V tomto výňatku je definováno několik obslužných rutin HTTP a každá obslužná rutina má jinou sadu metod HTTP, pro které je nakonfigurována – poslední položka v seznamu je obslužná rutina statického obsahu, což je výchozí obslužná rutina, která se používá po ostatních obslužných rutinách chanc e pro zkontrolování žádosti:

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample3.xml)]

V předchozím příkladu je pro samostatné seznamy metod HTTP jasně definována obslužná rutina protokolu WebDAV a obslužná rutina adresy URL bez přípony pro ASP.NET (která se používá pro webové rozhraní API). Všimněte si, že je obslužná rutina ISAPI DLL nakonfigurovaná pro všechny metody HTTP, i když tato konfigurace nebude nutně způsobovat chybu. Nastavení konfigurace by se ale mělo zvážit při řešení potíží s chybami HTTP 405.

V předchozím příkladu nedošlo k problému s obslužnou rutinou knihoven DLL ISAPI; ve skutečnosti nebyl problém definovaný v souboru *ApplicationHost. config* pro server IIS – problém byl způsoben záznamem, který byl vytvořen v souboru *Web. config* , když byla aplikace webového rozhraní API vytvořena v aplikaci Visual Studio. Následující úryvek ze souboru *Web. config* aplikace zobrazuje umístění problému:

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample4.xml)]

V tomto výňatku je Předefinovaná obslužná rutina adresy URL bez přípony pro ASP.NET tak, aby zahrnovala další metody HTTP, které budou použity s aplikací webového rozhraní API. Jelikož je však pro obslužnou rutinu protokolu WebDAV definována podobná sada metod HTTP, dojde ke konfliktu. V tomto konkrétním případě je obslužná rutina WebDAV definovaná a načtená službou IIS, a to i v případě, že je protokol WebDAV pro web, který obsahuje aplikaci webového rozhraní API, zakázaný. Při zpracování požadavku HTTP PUT zavolá služba IIS modul WebDAV, protože je definovaný pro operaci PUT. Když se zavolá modul WebDAV, zkontroluje jeho konfiguraci a zjistí, že je zakázaný, takže vrátí metodu HTTP 405, která ***není povolená*** pro všechny žádosti, které se podobá požadavku WebDAV. Chcete-li tento problém vyřešit, odeberte protokol WebDAV ze seznamu modulů HTTP pro web, kde je definována vaše aplikace webového rozhraní API. Následující příklad ukazuje, co může vypadat takto:

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample5.xml)]

Tento scénář je často k dispozici po publikování aplikace z vývojového prostředí do produkčního prostředí služby IIS a k tomu dochází proto, že seznam obslužných rutin/modulů se mezi vývojovým a produkčním prostředím liší. Například pokud používáte Visual Studio 2012 nebo novější k vývoji aplikace webového rozhraní API, IIS Express je výchozím webovým serverem pro testování. Tento vývojový webový server je verzí úplné funkce služby IIS, která je dodávána v serverovém produktu, a tento vývojový webový server obsahuje několik změn, které byly přidány pro vývojové scénáře. Například modul WebDAV se často instaluje na provozní webový server, na kterém běží plná verze služby IIS, i když se nepoužívá. Vývojová verze služby IIS, (IIS Express), nainstaluje modul WebDAV, ale položky pro modul WebDAV jsou záměrně zakomentovány, takže modul WebDAV se nikdy nenačte do IIS Express, pokud jste konkrétně nezměnili konfiguraci IIS Express. nastavení pro přidání funkce protokolu WebDAV do instalace IIS Express. V důsledku toho může webová aplikace ve vývojovém počítači fungovat správně, ale při publikování aplikace webového rozhraní API na provozní webový server služby IIS se může zobrazit chyba HTTP 405.

## <a name="http-501-errors"></a>Chyby HTTP 501

* Indikuje, že konkrétní funkčnost nebyla na serveru implementována.
* Obvykle znamená, že ve vašich nastaveních IIS není definovaná žádná obslužná rutina, která by odpovídala požadavku HTTP:
  * Pravděpodobně indikuje, že ve službě IIS není správně nainstalována položka nebo
  * Něco upravilo nastavení služby IIS, takže nejsou definované žádné obslužné rutiny, které podporují konkrétní metodu HTTP.

Chcete-li tento problém vyřešit, budete muset přeinstalovat jakoukoli aplikaci, která se pokouší použít metodu HTTP, pro kterou nemá odpovídající definice modulu nebo obslužné rutiny.

## <a name="summary"></a>Souhrn

Chyby protokolu HTTP 405 jsou způsobeny tím, že metoda HTTP není povolena webovým serverem pro požadovanou adresu URL. Tento stav se často zobrazuje, když je pro určitou operaci definována konkrétní obslužná rutina a tato obslužná rutina Přepisuje obslužnou rutinu, kterou očekáváte pro zpracování žádosti.
