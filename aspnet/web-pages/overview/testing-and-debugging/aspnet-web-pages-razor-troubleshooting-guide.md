---
uid: web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
title: Průvodce odstraňováním potíží s webovými stránkami (Razor) ASP.NET | Microsoft Docs
author: Rick-Anderson
description: Tento článek popisuje problémy, které mohou nastat při práci s webovými stránkami ASP.NET (Razor) a s některými navrhovanými řešeními. Verze softwaru ASP.NET Web Úvo...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 2a2c1833-0bfe-4e2e-9cc0-341b52c7b121
msc.legacyurl: /web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
msc.type: authoredcontent
ms.openlocfilehash: fc03767c16f46c1e282d24ee3a7df2409a7c38bb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78585762"
---
# <a name="aspnet-web-pages-razor-troubleshooting-guide"></a>Webové stránky ASP.NET (Razor) – průvodce řešením potíží

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek popisuje problémy, které mohou nastat při práci s webovými stránkami ASP.NET (Razor) a s některými navrhovanými řešeními.
> 
> ## <a name="software-versions"></a>Verze softwaru
> 
> 
> - Webové stránky ASP.NET (Razor) 3
>   
> 
> Tento kurz funguje také s ASP.NET webovými stránkami 2 a ASP.NET Web Pages 1,0.

Toto téma obsahuje následující oddíly:

- [Problémy se spuštěnými stránkami](#Issues_Running_.cshtml_Pages)
- [Problémy s kódem Razor](#IssuesWithRazorCode)
- [Problémy se zabezpečením a členstvím](#membership)
- [Problémy s odesíláním e-mailů](#email)
- [Další zdroje](#AdditionalResources)

Obecné otázky najdete v tématu [Nejčastější dotazy k webovým stránkám ASP.NET (Razor)](https://go.microsoft.com/fwlink/?LinkId=253000).

<a id="Issues_Running_.cshtml_Pages"></a>
## <a name="issues-with-running-pages"></a>Problémy se spuštěnými stránkami

Celá řada problémů může zabránit správnému fungování stránek *. cshtml* a *. vbhtml* . V této části jsou uvedené běžné chybové zprávy a pravděpodobná příčiny.

### <a name="http-error-403---forbidden-access-is-denied"></a>Chyba protokolu HTTP 403 – zakázáno: přístup byl odepřen

*Nemáte oprávnění k zobrazení tohoto adresáře nebo stránky pomocí zadaných přihlašovacích údajů.*

K této chybě může dojít, pokud na serveru není spuštěná správná verze .NET Framework. Ujistěte se, že počítač, na kterém běží server (místně nebo vzdáleně), má nainstalovanou aspoň .NET Framework 4. Také se ujistěte, že je aplikace sama nakonfigurovaná tak, aby spouštěla správnou verzi.

Pokud se tento problém zobrazuje místně při práci s webmatrixem, klikněte na pracovní prostor **webu** a potom v ovládacím prvku TreeView klikněte na **Nastavení**. V seznamu **vybrat verzi .NET Framework** vyberte **.NET 4 (integrovaný režim)** . Pokud je tato verze již nastavená, zkuste spustit WebMatrix jako správce.

Ujistěte se, že v kořenovém adresáři webu je alespoň jeden soubor *. cshtml* .

Pokud se zobrazí tato chyba, když je webový server na vzdáleném serveru, obraťte se na správce serveru. Ujistěte se, že na serveru je nainstalovaná .NET Framework 4 nebo novější. Také se ujistěte, že aplikace běží ve fondu aplikací, který je nakonfigurován pro použití této verze the.NET Framework.

Pokud máte kontrolu nad serverem, ujistěte se, že je spuštěná správná verze .NET Framework. Můžete také zkusit opravit instalaci spuštěním příkazu `aspnet_regiis -iru`. (Pokud například nainstalujete službu IIS po instalaci .NET Framework, služba IIS nebude správně nakonfigurována tak, aby spouštěla stránky ASP.NET.) Další informace najdete v tématu [registrační nástroj ASP.NET služby IIS (Aspnet\_regiis. exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx).

### <a name="http-error-40314---forbidden"></a>Chyba protokolu HTTP 403,14 – zakázáno

*Webový server je nakonfigurován tak, aby neobsahoval seznam obsahu tohoto adresáře.*

K této chybě může dojít, pokud požadujete prostředek, který je chráněný (například soubor *Web. config* ), nebo který je ve složce, která je chráněná (například *aplikace\_data* nebo *\_kódu aplikace*).

### <a name="http-error-40417---not-found"></a>Chyba protokolu HTTP 404,17 – nenalezeno

*Požadovaný obsah vypadá jako skript a nebude obsluhován obslužnou rutinou statického souboru.*

K této chybě může dojít, pokud server není správně nakonfigurován tak, aby používal .NET Framework 4 nebo novější, a proto nerozpoznal kód v blocích `@{ }`. Podívejte se na popis uvedený výše pro *chybu protokolu HTTP 403 – zakázáno: přístup byl odepřen*.

### <a name="http-error-4047---not-found"></a>Chyba protokolu HTTP 404,7 – Nenalezeno

*Modul filtrování požadavků je nakonfigurován tak, aby odepřel příponu souboru.*

K této chybě může dojít, pokud byla na serveru explicitně zablokována rozšíření *. cshtml* nebo *. vbhtml* . Příznak tohoto problému je, že adresy URL fungují, když neobsahují rozšíření, ale adresy URL, které obsahují *. cshtml* nebo *. vbhtml* , nefungují. Možným řešením je znovu povolit rozšíření v souboru *Web. config* tohoto webu. Následující příklad ukazuje, jak povolit rozšíření *. cshtml* .

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample1.xml?highlight=5-6)]

### <a name="http-error-4048---not-found"></a>Chyba protokolu HTTP 404,8 – Nenalezeno

*Modul filtrování požadavků je nakonfigurován tak, aby odepřel cestu v adrese URL, která obsahuje oddíl hiddenSegment.*

K této chybě může dojít, pokud požadujete prostředek, který je chráněný (například soubor *Web. config* ), nebo který je ve složce, která je chráněná (například *aplikace\_data* nebo *\_kódu aplikace*).

### <a name="this-type-of-page-is-not-served-server-error-in--application"></a>Tento typ stránky není obsluhován (chyba serveru v/aplikaci)

Podívejte se na popis předchozí chyby protokolu HTTP 404,17.

<a id="IssuesWithRazorCode"></a>
## <a name="issues-with-razor-code"></a>Problémy s kódem Razor

### <a name="the-name-class-does-not-exist-in-the-current-context"></a>Název*Class*v aktuálním kontextu neexistuje.

Příčinou této chyby je často, že `class` odkazuje na pomoc, ale pomocník není nainstalován. Pokud se například pokusíte použít pomocníka, ale pokud jste balíček nenainstalovali z nástroje NuGet, zobrazí se tato chyba. K vyhledání a instalaci pomocné rutiny použijte Galerii WebMatrix.

Pokud je nainstalovaná pomoc, ale stránka ji ještě nerozezná, zkuste do kódu přidat příkaz `using`. V příkazu `using` odkazují na obor názvů, který obsahuje nápovědu. Například základní pomocníky, které jsou v balíčku webových pomocníků ASP.NET, jsou v oboru názvů `System.Web.Helpers`. V horní části stránky, kde chcete použít pomocníka, přidejte tento řádek:

`@using Microsoft.Web.Helpers;`

<a id="membership"></a>
## <a name="issues-with-security-and-membership"></a>Problémy se zabezpečením a členstvím

Pokud používáte vestavěný systém zabezpečení (členství) na webových stránkách ASP.NET (Razor), může dojít k následujícím potížím.

### <a name="to-call-this-method-the-membershipprovider-property-must-be-an-instance-of-extendedmembershipprovider"></a>Pro volání této metody musí být vlastnost Membership. Provider instancí třídy "ExtendedMembershipProvider".

Tato chyba může znamenat, že není nakonfigurovaná žádná `AspNetSqlMembershipProvider` třída. (Příznakem je, že lokalita funguje místně, ale vyvolá tuto chybu, když ji publikujete na server poskytovatele hostingu.) Jedním z oprav tohoto problému je explicitní povolení jednoduchého členství přidáním následujícího do souboru *Web. config* webu:

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample2.xml?highlight=6)]

<a id="email"></a>
## <a name="issues-with-sending-email"></a>Problémy s odesíláním e-mailů

Problémy s odesíláním e-mailů můžou být náročné na ladění. K počátečnímu problému může dojít, když se nemůžete připojit k serveru SMTP. Pokud je připojení úspěšné, ASP.NET zprávu do serveru SMTP. Mohou však nastat problémy se zprávou, která brání serveru SMTP v jeho odeslání.

Pokud vaše aplikace úspěšně neposílá e-mail, zkuste následující:

- Název serveru SMTP je často podobný jako `smtp.provider.com` nebo `smtp.provider.net`. Pokud ale publikujete lokalitu pro poskytovatele hostingu, může být název serveru SMTP v tomto okamžiku `localhost`. K této situaci dochází, protože po publikování a spuštění webu na serveru zprostředkovatele může být server SMTP místní z perspektivy vaší aplikace. Tato změna v názvech serverů může znamenat, že je třeba změnit název serveru SMTP v rámci procesu publikování.
- Číslo portu je obvykle 25. Někteří poskytovatelé ale vyžadují, abyste používali port 587 nebo jiný port. U vlastníka serveru SMTP ověřte, jaké číslo portu očekáváte použít.
- Ujistěte se, že používáte správné přihlašovací údaje. Pokud jste web publikovali pro poskytovatele hostingu, použijte přihlašovací údaje, které poskytovatel konkrétně označil, k e-mailu. Tyto přihlašovací údaje se můžou lišit od přihlašovacích údajů, které používáte k publikování.
- Někdy nepotřebujete vůbec přihlašovací údaje. Pokud posíláte e-mail pomocí osobního poskytovatele internetových služeb, váš poskytovatel e-mailu už může znát vaše přihlašovací údaje. Po publikování může být nutné použít jiné přihlašovací údaje než při testování na místním počítači.
- Pokud poskytovatel e-mailu používá šifrování, nastavte `WebMail.EnableSsl` na `true`.

Pokud při odesílání e-mailů dojde k chybě, může se zobrazit standardní chybová zpráva ASP.NET, která vypadá takto:

![ASP.NET chybová zpráva, když dojde k problému s e-mailem](aspnet-web-pages-razor-troubleshooting-guide/_static/image1.png)

Problémy s posíláním e-mailu můžete také ladit pomocí `try-catch`ho bloku, jak je uvedeno v následujícím příkladu. Když použijete blok `try-catch`, nezobrazuje ASP.NET standardní chybové zprávy. Místo toho můžete zachytit chybu v `catch` části bloku.

[!code-cshtml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample3.cshtml)]

Nahraďte příslušné hodnoty pro `your-SMTP-server-name`a tak dále. Mezi chybové zprávy, které vidíte tímto způsobem, patří následující:

- *Odeslání e-mailu se nezdařilo.*

    -nebo-

    *Pokus o připojení se nezdařil, protože připojená strana nereagovala po určitém časovém intervalu správně nebo navázáno připojení selhalo, protože se nepovedlo odpovědět připojeného hostitele.*

    Tato chyba obvykle znamená, že se aplikace nemohla připojit k serveru SMTP. Ověřte název serveru a číslo portu.
- *Poštovní schránka není k dispozici. Odpověď serveru byla: 5.1.0 &lt;someuser@invaliddomain&gt; odesilatel byl odmítnut: Neplatná doména odesílatele.*

    Tato zpráva může značit, že adresa `From` není správná nebo chybí.
- *Zadaný řetězec není ve formátu vyžadovaném pro e-mailovou adresu.*

    Tato chyba může znamenat, že hodnota `To` nebo `From` vlastností není rozpoznána jako e-mailové adresy. (ASP.NET nemůže ověřit, zda je e-mailová adresa platná, zda je ve správném formátu, například *name@domain.com* .)

> [!NOTE]
> Před publikováním stránky na živém webu odeberte kód, který zobrazí chybu (`@errorMessage`). Není vhodné, aby uživatelé viděli chybové zprávy, které získáte ze serveru.

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>Další prostředky

[Webové stránky ASP.NET (Razor) – časté otázky](https://go.microsoft.com/fwlink/?LinkId=253000)

Fórum [webových stránek WebMatrix a ASP.NET](https://forums.asp.net/1224.aspx/1?WebMatrix) na webu ASP.NET
