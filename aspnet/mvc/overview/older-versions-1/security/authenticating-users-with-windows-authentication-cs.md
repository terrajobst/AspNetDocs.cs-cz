---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
title: Ověřování uživatelů pomocí ověřování systému Windows (C#) | Microsoft Docs
author: microsoft
description: Naučte se používat ověřování systému Windows v kontextu aplikace MVC. Naučíte se, jak povolit ověřování Windows v rámci webu vaší aplikace co...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 418bb07e-f369-4119-b4b0-08f890f7abb2
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: bb3909bff2791c15a8737fc12cac69f79b55733f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624122"
---
# <a name="authenticating-users-with-windows-authentication-c"></a>Ověřování uživatelů pomocí ověřování systému Windows (C#)

od [Microsoftu](https://github.com/microsoft)

> Naučte se používat ověřování systému Windows v kontextu aplikace MVC. Naučíte se, jak povolit ověřování Windows v konfiguračním souboru webu vaší aplikace a jak nakonfigurovat ověřování pomocí služby IIS. Nakonec se naučíte, jak použít atribut [autorizovat] k omezení přístupu k akcím kontroleru na konkrétní uživatele nebo skupiny systému Windows.

Cílem tohoto kurzu je vysvětlit, jak můžete využít funkce zabezpečení integrované do Internetová informační služba k ochraně zobrazení v aplikacích MVC. Naučíte se, jak můžete, aby se akce kontroleru vyvolaly jenom konkrétním uživatelům nebo uživatelům systému Windows, kteří jsou členy určitých skupin systému Windows.

Použití ověřování systému Windows dává smysl při vytváření interního webu společnosti (intranetový server) a chcete, aby uživatelé mohli při přístupu k webu používat standardní uživatelská jména a hesla systému Windows. Pokud vytváříte web na webu (internetový web), zvažte místo toho použití ověřování pomocí formulářů.

#### <a name="enabling-windows-authentication"></a>Povoluje se ověřování systému Windows.

Při vytváření nové aplikace ASP.NET MVC není ověřování systému Windows ve výchozím nastavení povoleno. Ověřování prostřednictvím formulářů je výchozí typ ověřování povolený pro aplikace MVC. Ověřování systému Windows je nutné povolit úpravou konfiguračního souboru webové konfigurace aplikace MVC (Web. config). Vyhledejte&gt; &lt;ověřování a upravte ho tak, aby místo ověřování pomocí formuláře používal Windows:

[!code-xml[Main](authenticating-users-with-windows-authentication-cs/samples/sample1.xml)]

Když povolíte ověřování systému Windows, váš webový server bude zodpovědný za ověřování uživatelů. Obvykle existují dva různé typy webových serverů, které používáte při vytváření a nasazování aplikace ASP.NET MVC.

Nejdřív při vývoji aplikace MVC použijete vývojový webový server ASP.NET, který je součástí sady Visual Studio. Ve výchozím nastavení se webový server ASP.NET Development spouští všechny stránky v kontextu aktuálního účtu systému Windows (libovolný účet, který jste použili k přihlášení do systému Windows).

Webový server pro vývoj ASP.NET také podporuje ověřování NTLM. Ověřování NTLM můžete povolit tak, že kliknete pravým tlačítkem na název projektu v okně Průzkumník řešení a vyberete vlastnosti. Potom vyberte kartu Web a zaškrtněte políčko NTLM (viz obrázek 1).

**Obrázek 1 – povolení ověřování NTLM pro webový server ASP.NET Development**

![clip_image002](authenticating-users-with-windows-authentication-cs/_static/image1.jpg)

V případě produkční webové aplikace můžete službu IIS používat jako webový server. Služba IIS podporuje několik typů ověřování, včetně:

- Základní ověřování – definováno jako součást protokolu HTTP 1,0. Odesílá uživatelská jména a hesla v nešifrovaném textu (kódovaný v kódování Base64) napříč internetem. – Ověřování algoritmem Digest – pošle místo samotného hesla hodnotu hash hesla, a to přes Internet. – Ověřování pomocí protokolu NTLM (Integrated Windows) – nejlepší typ ověřování, které se má použít v intranetových prostředích používajících systém Windows. -Ověřování certifikátů – povolí ověřování pomocí certifikátu na straně klienta. Certifikát se mapuje na uživatelský účet systému Windows.

> [!NOTE] 
> 
> Podrobnější přehled těchto různých typů ověřování najdete v tématu [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx).

K povolení konkrétního typu ověřování můžete použít Správce Internetová informační služba. Mějte na paměti, že všechny typy ověřování nejsou v případě každého operačního systému k dispozici. Pokud navíc používáte službu IIS 7,0 se systémem Windows Vista, budete muset před zobrazením ve Správci Internetová informační služba povolit různé typy ověřování systému Windows. Otevřete **Ovládací panely, programy, programy a funkce, zapněte nebo vypněte funkce systému Windows**a rozbalte uzel Internetová informační služba (viz obrázek 2).

**Obrázek 2 – povolení funkcí služby IIS systému Windows**

![clip_image004](authenticating-users-with-windows-authentication-cs/_static/image2.jpg)

Pomocí Internetová informační služba můžete povolit nebo zakázat různé typy ověřování. Obrázek 3 například znázorňuje zakázání anonymního ověřování a povolení ověřování pomocí integrovaného systému Windows (NTLM) při použití IIS 7,0.

**Obrázek 3 – povolení integrovaného ověřování systému Windows**

![clip_image006](authenticating-users-with-windows-authentication-cs/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a>Autorizace uživatelů a skupin systému Windows

Po povolení ověřování systému Windows můžete použít atribut [autorizovat] k řízení přístupu k řadičům nebo k akcím kontroleru. Tento atribut lze použít pro celý kontroler MVC nebo pro konkrétní akci kontroleru.

Například domovský řadič v seznamu 1 zveřejňuje tři akce s názvem index (), CompanySecrets () a StephenSecrets (). Kdokoli může vyvolat akci index (). Akci CompanySecrets () však mohou vyvolat pouze členové skupiny místních správců systému Windows. Nakonec může akci StephenSecrets () vyvolat jenom uživatel domény Windows s názvem Stephen (v doméně Redmond).

**Výpis 1 – souboru controllers\homecontroller.cs**

[!code-csharp[Main](authenticating-users-with-windows-authentication-cs/samples/sample2.cs)]

> [!NOTE] 
> 
> Vzhledem k tomu, že nástroj řízení uživatelských účtů systému Windows (UAC) pracuje se systémem Windows Vista nebo Windows Server 2008, místní skupina správců se bude chovat jinak než jiné skupiny. Pokud nezměníte nastavení nástroje řízení uživatelských účtů v počítači, atribut [autorizovat] správně rozpoznává člena místní skupiny Administrators.

K tomu, co se stane, když se pokusíte vyvolat akci kontroleru bez správných oprávnění, záleží na typu povoleného ověřování. Ve výchozím nastavení se při použití vývojového serveru ASP.NET jednoduše zobrazí prázdná stránka. Stránka je dodávána s **401 neautorizovaným** stavem odpovědi HTTP.

Pokud na druhé straně používáte službu IIS se zakázaným anonymním ověřováním a je povolené základní ověřování, pak se při každém požadavku na chráněnou stránku zobrazí výzva k zadání přihlašovacího dialogového okna (viz obrázek 4).

**Obrázek 4 – dialogové okno pro přihlášení k základnímu ověření**

![clip_image008](authenticating-users-with-windows-authentication-cs/_static/image4.jpg)

#### <a name="summary"></a>Souhrn

V tomto kurzu se vysvětluje, jak můžete používat ověřování Windows v kontextu aplikace ASP.NET MVC. Zjistili jste, jak povolit ověřování systému Windows v rámci konfiguračního souboru webové aplikace a jak nakonfigurovat ověřování pomocí služby IIS. Nakonec jste zjistili, jak použít atribut [autorizovat] k omezení přístupu k akcím kontroleru na konkrétní uživatele nebo skupiny systému Windows.

> [!div class="step-by-step"]
> [Předchozí](authenticating-users-with-forms-authentication-cs.md)
> [Další](preventing-javascript-injection-attacks-cs.md)
