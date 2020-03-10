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
# <a name="aspnet-web-pages-razor-troubleshooting-guide"></a><span data-ttu-id="1d507-104">Webové stránky ASP.NET (Razor) – průvodce řešením potíží</span><span class="sxs-lookup"><span data-stu-id="1d507-104">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>

<span data-ttu-id="1d507-105">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="1d507-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="1d507-106">Tento článek popisuje problémy, které mohou nastat při práci s webovými stránkami ASP.NET (Razor) a s některými navrhovanými řešeními.</span><span class="sxs-lookup"><span data-stu-id="1d507-106">This article describes issues that you might have when working with ASP.NET Web Pages (Razor) and some suggested solutions.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="1d507-107">Verze softwaru</span><span class="sxs-lookup"><span data-stu-id="1d507-107">Software versions</span></span>
> 
> 
> - <span data-ttu-id="1d507-108">Webové stránky ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="1d507-108">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="1d507-109">Tento kurz funguje také s ASP.NET webovými stránkami 2 a ASP.NET Web Pages 1,0.</span><span class="sxs-lookup"><span data-stu-id="1d507-109">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0.</span></span>

<span data-ttu-id="1d507-110">Toto téma obsahuje následující oddíly:</span><span class="sxs-lookup"><span data-stu-id="1d507-110">This topic contains the following sections:</span></span>

- [<span data-ttu-id="1d507-111">Problémy se spuštěnými stránkami</span><span class="sxs-lookup"><span data-stu-id="1d507-111">Issues with Running Pages</span></span>](#Issues_Running_.cshtml_Pages)
- [<span data-ttu-id="1d507-112">Problémy s kódem Razor</span><span class="sxs-lookup"><span data-stu-id="1d507-112">Issues with Razor Code</span></span>](#IssuesWithRazorCode)
- [<span data-ttu-id="1d507-113">Problémy se zabezpečením a členstvím</span><span class="sxs-lookup"><span data-stu-id="1d507-113">Issues with Security and Membership</span></span>](#membership)
- [<span data-ttu-id="1d507-114">Problémy s odesíláním e-mailů</span><span class="sxs-lookup"><span data-stu-id="1d507-114">Issues with Sending Email</span></span>](#email)
- [<span data-ttu-id="1d507-115">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="1d507-115">Additional Resources</span></span>](#AdditionalResources)

<span data-ttu-id="1d507-116">Obecné otázky najdete v tématu [Nejčastější dotazy k webovým stránkám ASP.NET (Razor)](https://go.microsoft.com/fwlink/?LinkId=253000).</span><span class="sxs-lookup"><span data-stu-id="1d507-116">For general questions, see [ASP.NET Web Pages (Razor) FAQ](https://go.microsoft.com/fwlink/?LinkId=253000).</span></span>

<a id="Issues_Running_.cshtml_Pages"></a>
## <a name="issues-with-running-pages"></a><span data-ttu-id="1d507-117">Problémy se spuštěnými stránkami</span><span class="sxs-lookup"><span data-stu-id="1d507-117">Issues with Running Pages</span></span>

<span data-ttu-id="1d507-118">Celá řada problémů může zabránit správnému fungování stránek *. cshtml* a *. vbhtml* .</span><span class="sxs-lookup"><span data-stu-id="1d507-118">A variety of issues can prevent *.cshtml* and *.vbhtml* pages from running properly.</span></span> <span data-ttu-id="1d507-119">V této části jsou uvedené běžné chybové zprávy a pravděpodobná příčiny.</span><span class="sxs-lookup"><span data-stu-id="1d507-119">This section lists common error messages and likely causes.</span></span>

### <a name="http-error-403---forbidden-access-is-denied"></a><span data-ttu-id="1d507-120">Chyba protokolu HTTP 403 – zakázáno: přístup byl odepřen</span><span class="sxs-lookup"><span data-stu-id="1d507-120">HTTP Error 403 - Forbidden: Access is denied</span></span>

<span data-ttu-id="1d507-121">*Nemáte oprávnění k zobrazení tohoto adresáře nebo stránky pomocí zadaných přihlašovacích údajů.*</span><span class="sxs-lookup"><span data-stu-id="1d507-121">*You do not have permission to view this directory or page using the credentials that you supplied.*</span></span>

<span data-ttu-id="1d507-122">K této chybě může dojít, pokud na serveru není spuštěná správná verze .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="1d507-122">This error can occur if the server is not running the correct version of the .NET Framework.</span></span> <span data-ttu-id="1d507-123">Ujistěte se, že počítač, na kterém běží server (místně nebo vzdáleně), má nainstalovanou aspoň .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="1d507-123">Make sure that the computer that's running the server (locally or remotely) has at least the .NET Framework 4 installed.</span></span> <span data-ttu-id="1d507-124">Také se ujistěte, že je aplikace sama nakonfigurovaná tak, aby spouštěla správnou verzi.</span><span class="sxs-lookup"><span data-stu-id="1d507-124">Also make sure that the application itself is configured to run the right version.</span></span>

<span data-ttu-id="1d507-125">Pokud se tento problém zobrazuje místně při práci s webmatrixem, klikněte na pracovní prostor **webu** a potom v ovládacím prvku TreeView klikněte na **Nastavení**.</span><span class="sxs-lookup"><span data-stu-id="1d507-125">If you see this problem locally while working in WebMatrix, click the **Site** workspace, and then in the treeview click **Settings**.</span></span> <span data-ttu-id="1d507-126">V seznamu **vybrat verzi .NET Framework** vyberte **.NET 4 (integrovaný režim)** .</span><span class="sxs-lookup"><span data-stu-id="1d507-126">In the **Select .NET Framework Version** list, select **.NET 4 (Integrated)**.</span></span> <span data-ttu-id="1d507-127">Pokud je tato verze již nastavená, zkuste spustit WebMatrix jako správce.</span><span class="sxs-lookup"><span data-stu-id="1d507-127">If this version is already set, try running WebMatrix as an administrator.</span></span>

<span data-ttu-id="1d507-128">Ujistěte se, že v kořenovém adresáři webu je alespoň jeden soubor *. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="1d507-128">Make sure that the root of your website has at least one *.cshtml* file in it.</span></span>

<span data-ttu-id="1d507-129">Pokud se zobrazí tato chyba, když je webový server na vzdáleném serveru, obraťte se na správce serveru.</span><span class="sxs-lookup"><span data-stu-id="1d507-129">If you see this error when the web server is on a remote server, contact the server administrator.</span></span> <span data-ttu-id="1d507-130">Ujistěte se, že na serveru je nainstalovaná .NET Framework 4 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="1d507-130">Make sure that the server has the .NET Framework 4 or later installed.</span></span> <span data-ttu-id="1d507-131">Také se ujistěte, že aplikace běží ve fondu aplikací, který je nakonfigurován pro použití této verze the.NET Framework.</span><span class="sxs-lookup"><span data-stu-id="1d507-131">Also make sure that the application is running in an application pool that's configured to use that version of the.NET Framework.</span></span>

<span data-ttu-id="1d507-132">Pokud máte kontrolu nad serverem, ujistěte se, že je spuštěná správná verze .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="1d507-132">If you have control over the server, make sure it's running the correct version of the .NET Framework.</span></span> <span data-ttu-id="1d507-133">Můžete také zkusit opravit instalaci spuštěním příkazu `aspnet_regiis -iru`.</span><span class="sxs-lookup"><span data-stu-id="1d507-133">You might also try repairing the installation by running the `aspnet_regiis -iru` command.</span></span> <span data-ttu-id="1d507-134">(Pokud například nainstalujete službu IIS po instalaci .NET Framework, služba IIS nebude správně nakonfigurována tak, aby spouštěla stránky ASP.NET.) Další informace najdete v tématu [registrační nástroj ASP.NET služby IIS (Aspnet\_regiis. exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="1d507-134">(For example, if you install IIS after you install the .NET Framework, IIS will not be correctly configured to run ASP.NET pages.) For more information, see [ASP.NET IIS Registration Tool (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx).</span></span>

### <a name="http-error-40314---forbidden"></a><span data-ttu-id="1d507-135">Chyba protokolu HTTP 403,14 – zakázáno</span><span class="sxs-lookup"><span data-stu-id="1d507-135">HTTP Error 403.14 - Forbidden</span></span>

<span data-ttu-id="1d507-136">*Webový server je nakonfigurován tak, aby neobsahoval seznam obsahu tohoto adresáře.*</span><span class="sxs-lookup"><span data-stu-id="1d507-136">*The Web server is configured to not list the contents of this directory.*</span></span>

<span data-ttu-id="1d507-137">K této chybě může dojít, pokud požadujete prostředek, který je chráněný (například soubor *Web. config* ), nebo který je ve složce, která je chráněná (například *aplikace\_data* nebo *\_kódu aplikace*).</span><span class="sxs-lookup"><span data-stu-id="1d507-137">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="http-error-40417---not-found"></a><span data-ttu-id="1d507-138">Chyba protokolu HTTP 404,17 – nenalezeno</span><span class="sxs-lookup"><span data-stu-id="1d507-138">HTTP Error 404.17 - Not Found</span></span>

<span data-ttu-id="1d507-139">*Požadovaný obsah vypadá jako skript a nebude obsluhován obslužnou rutinou statického souboru.*</span><span class="sxs-lookup"><span data-stu-id="1d507-139">*The requested content appears to be script and will not be served by the static file handler.*</span></span>

<span data-ttu-id="1d507-140">K této chybě může dojít, pokud server není správně nakonfigurován tak, aby používal .NET Framework 4 nebo novější, a proto nerozpoznal kód v blocích `@{ }`.</span><span class="sxs-lookup"><span data-stu-id="1d507-140">This error can occur if the server is not configured correctly to use the .NET Framework 4 or later, and therefore does not recognize the code in `@{ }` blocks.</span></span> <span data-ttu-id="1d507-141">Podívejte se na popis uvedený výše pro *chybu protokolu HTTP 403 – zakázáno: přístup byl odepřen*.</span><span class="sxs-lookup"><span data-stu-id="1d507-141">See the description earlier for *HTTP Error 403 - Forbidden: Access is denied*.</span></span>

### <a name="http-error-4047---not-found"></a><span data-ttu-id="1d507-142">Chyba protokolu HTTP 404,7 – Nenalezeno</span><span class="sxs-lookup"><span data-stu-id="1d507-142">HTTP Error 404.7 - Not Found</span></span>

<span data-ttu-id="1d507-143">*Modul filtrování požadavků je nakonfigurován tak, aby odepřel příponu souboru.*</span><span class="sxs-lookup"><span data-stu-id="1d507-143">*The request filtering module is configured to deny the file extension*</span></span>

<span data-ttu-id="1d507-144">K této chybě může dojít, pokud byla na serveru explicitně zablokována rozšíření *. cshtml* nebo *. vbhtml* .</span><span class="sxs-lookup"><span data-stu-id="1d507-144">This error can occur if *.cshtml* or *.vbhtml* extensions have been explicitly blocked on the server.</span></span> <span data-ttu-id="1d507-145">Příznak tohoto problému je, že adresy URL fungují, když neobsahují rozšíření, ale adresy URL, které obsahují *. cshtml* nebo *. vbhtml* , nefungují.</span><span class="sxs-lookup"><span data-stu-id="1d507-145">A symptom of this problem is that URLs work when they do not include the extension, but URLs that include *.cshtml* or *.vbhtml* do not work.</span></span> <span data-ttu-id="1d507-146">Možným řešením je znovu povolit rozšíření v souboru *Web. config* tohoto webu.</span><span class="sxs-lookup"><span data-stu-id="1d507-146">A possible solution is to re-enable the extensions in the site's *Web.config* file.</span></span> <span data-ttu-id="1d507-147">Následující příklad ukazuje, jak povolit rozšíření *. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="1d507-147">The following example shows how to enable the *.cshtml* extension.</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample1.xml?highlight=5-6)]

### <a name="http-error-4048---not-found"></a><span data-ttu-id="1d507-148">Chyba protokolu HTTP 404,8 – Nenalezeno</span><span class="sxs-lookup"><span data-stu-id="1d507-148">HTTP Error 404.8 - Not Found</span></span>

<span data-ttu-id="1d507-149">*Modul filtrování požadavků je nakonfigurován tak, aby odepřel cestu v adrese URL, která obsahuje oddíl hiddenSegment.*</span><span class="sxs-lookup"><span data-stu-id="1d507-149">*The request filtering module is configured to deny a path in the URL that contains a hiddenSegment section.*</span></span>

<span data-ttu-id="1d507-150">K této chybě může dojít, pokud požadujete prostředek, který je chráněný (například soubor *Web. config* ), nebo který je ve složce, která je chráněná (například *aplikace\_data* nebo *\_kódu aplikace*).</span><span class="sxs-lookup"><span data-stu-id="1d507-150">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="this-type-of-page-is-not-served-server-error-in--application"></a><span data-ttu-id="1d507-151">Tento typ stránky není obsluhován (chyba serveru v/aplikaci)</span><span class="sxs-lookup"><span data-stu-id="1d507-151">This type of page is not served (Server Error in '/' Application)</span></span>

<span data-ttu-id="1d507-152">Podívejte se na popis předchozí chyby protokolu HTTP 404,17.</span><span class="sxs-lookup"><span data-stu-id="1d507-152">See the description earlier for HTTP Error 404.17.</span></span>

<a id="IssuesWithRazorCode"></a>
## <a name="issues-with-razor-code"></a><span data-ttu-id="1d507-153">Problémy s kódem Razor</span><span class="sxs-lookup"><span data-stu-id="1d507-153">Issues with Razor code</span></span>

### <a name="the-name-class-does-not-exist-in-the-current-context"></a><span data-ttu-id="1d507-154">Název*Class*v aktuálním kontextu neexistuje.</span><span class="sxs-lookup"><span data-stu-id="1d507-154">The name '*class*' does not exist in the current context</span></span>

<span data-ttu-id="1d507-155">Příčinou této chyby je často, že `class` odkazuje na pomoc, ale pomocník není nainstalován.</span><span class="sxs-lookup"><span data-stu-id="1d507-155">Often, a reason you see this error is that `class` references a helper, but the helper is not installed.</span></span> <span data-ttu-id="1d507-156">Pokud se například pokusíte použít pomocníka, ale pokud jste balíček nenainstalovali z nástroje NuGet, zobrazí se tato chyba.</span><span class="sxs-lookup"><span data-stu-id="1d507-156">For example, if you try to use a helper, but if you haven't installed the package from NuGet, you'll see this error.</span></span> <span data-ttu-id="1d507-157">K vyhledání a instalaci pomocné rutiny použijte Galerii WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="1d507-157">Use the Gallery in WebMatrix to find and install the helper.</span></span>

<span data-ttu-id="1d507-158">Pokud je nainstalovaná pomoc, ale stránka ji ještě nerozezná, zkuste do kódu přidat příkaz `using`.</span><span class="sxs-lookup"><span data-stu-id="1d507-158">If the helper is installed, but the page still doesn't recognize it, try adding add a `using` statement to the code.</span></span> <span data-ttu-id="1d507-159">V příkazu `using` odkazují na obor názvů, který obsahuje nápovědu.</span><span class="sxs-lookup"><span data-stu-id="1d507-159">In the `using` statement, reference the namespace that includes the helper.</span></span> <span data-ttu-id="1d507-160">Například základní pomocníky, které jsou v balíčku webových pomocníků ASP.NET, jsou v oboru názvů `System.Web.Helpers`.</span><span class="sxs-lookup"><span data-stu-id="1d507-160">For example, the basic helpers that are in the ASP.NET Web Helpers package are in the `System.Web.Helpers` namespace.</span></span> <span data-ttu-id="1d507-161">V horní části stránky, kde chcete použít pomocníka, přidejte tento řádek:</span><span class="sxs-lookup"><span data-stu-id="1d507-161">At the top of the page where you want to use the helper, add this line:</span></span>

`@using Microsoft.Web.Helpers;`

<a id="membership"></a>
## <a name="issues-with-security-and-membership"></a><span data-ttu-id="1d507-162">Problémy se zabezpečením a členstvím</span><span class="sxs-lookup"><span data-stu-id="1d507-162">Issues with Security and Membership</span></span>

<span data-ttu-id="1d507-163">Pokud používáte vestavěný systém zabezpečení (členství) na webových stránkách ASP.NET (Razor), může dojít k následujícím potížím.</span><span class="sxs-lookup"><span data-stu-id="1d507-163">If you are using the built-in security (membership) system in ASP.NET Web Pages (Razor), you might encounter the following issues.</span></span>

### <a name="to-call-this-method-the-membershipprovider-property-must-be-an-instance-of-extendedmembershipprovider"></a><span data-ttu-id="1d507-164">Pro volání této metody musí být vlastnost Membership. Provider instancí třídy "ExtendedMembershipProvider".</span><span class="sxs-lookup"><span data-stu-id="1d507-164">To call this method, the "Membership.Provider" property must be an instance of "ExtendedMembershipProvider"</span></span>

<span data-ttu-id="1d507-165">Tato chyba může znamenat, že není nakonfigurovaná žádná `AspNetSqlMembershipProvider` třída.</span><span class="sxs-lookup"><span data-stu-id="1d507-165">This error can indicate that no `AspNetSqlMembershipProvider` class is configured.</span></span> <span data-ttu-id="1d507-166">(Příznakem je, že lokalita funguje místně, ale vyvolá tuto chybu, když ji publikujete na server poskytovatele hostingu.) Jedním z oprav tohoto problému je explicitní povolení jednoduchého členství přidáním následujícího do souboru *Web. config* webu:</span><span class="sxs-lookup"><span data-stu-id="1d507-166">(A symptom is that the site works fine locally but throws this error when you publish it to a hosting provider's server.) One fix for this problem is to explicitly enable simple membership by adding the following to the site's *Web.config* file:</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample2.xml?highlight=6)]

<a id="email"></a>
## <a name="issues-with-sending-email"></a><span data-ttu-id="1d507-167">Problémy s odesíláním e-mailů</span><span class="sxs-lookup"><span data-stu-id="1d507-167">Issues with Sending Email</span></span>

<span data-ttu-id="1d507-168">Problémy s odesíláním e-mailů můžou být náročné na ladění.</span><span class="sxs-lookup"><span data-stu-id="1d507-168">Problems with sending email can be challenging to debug.</span></span> <span data-ttu-id="1d507-169">K počátečnímu problému může dojít, když se nemůžete připojit k serveru SMTP.</span><span class="sxs-lookup"><span data-stu-id="1d507-169">An initial problem can be that you can't connect to the SMTP server.</span></span> <span data-ttu-id="1d507-170">Pokud je připojení úspěšné, ASP.NET zprávu do serveru SMTP.</span><span class="sxs-lookup"><span data-stu-id="1d507-170">If the connection is successful, ASP.NET hands the message off to the SMTP server.</span></span> <span data-ttu-id="1d507-171">Mohou však nastat problémy se zprávou, která brání serveru SMTP v jeho odeslání.</span><span class="sxs-lookup"><span data-stu-id="1d507-171">However, there can be problems with the message itself that prevents the SMTP server from sending it.</span></span>

<span data-ttu-id="1d507-172">Pokud vaše aplikace úspěšně neposílá e-mail, zkuste následující:</span><span class="sxs-lookup"><span data-stu-id="1d507-172">If your application does not successfully send email, try the following:</span></span>

- <span data-ttu-id="1d507-173">Název serveru SMTP je často podobný jako `smtp.provider.com` nebo `smtp.provider.net`.</span><span class="sxs-lookup"><span data-stu-id="1d507-173">The SMTP server name is often something like `smtp.provider.com` or `smtp.provider.net`.</span></span> <span data-ttu-id="1d507-174">Pokud ale publikujete lokalitu pro poskytovatele hostingu, může být název serveru SMTP v tomto okamžiku `localhost`.</span><span class="sxs-lookup"><span data-stu-id="1d507-174">However, if you publish your site to a hosting provider, the SMTP server name at that point might be `localhost`.</span></span> <span data-ttu-id="1d507-175">K této situaci dochází, protože po publikování a spuštění webu na serveru zprostředkovatele může být server SMTP místní z perspektivy vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="1d507-175">This situation occurs because after you've published and your site is running on the provider's server, the SMTP server might be local from the perspective of your application.</span></span> <span data-ttu-id="1d507-176">Tato změna v názvech serverů může znamenat, že je třeba změnit název serveru SMTP v rámci procesu publikování.</span><span class="sxs-lookup"><span data-stu-id="1d507-176">This change in server names might mean that you have to change the SMTP server name as part of your publishing process.</span></span>
- <span data-ttu-id="1d507-177">Číslo portu je obvykle 25.</span><span class="sxs-lookup"><span data-stu-id="1d507-177">The port number is usually 25.</span></span> <span data-ttu-id="1d507-178">Někteří poskytovatelé ale vyžadují, abyste používali port 587 nebo jiný port.</span><span class="sxs-lookup"><span data-stu-id="1d507-178">However, some providers require you to use port 587 or some other port.</span></span> <span data-ttu-id="1d507-179">U vlastníka serveru SMTP ověřte, jaké číslo portu očekáváte použít.</span><span class="sxs-lookup"><span data-stu-id="1d507-179">Check with the owner of the SMTP server what port number they expect you to use.</span></span>
- <span data-ttu-id="1d507-180">Ujistěte se, že používáte správné přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="1d507-180">Make sure that you use the right credentials.</span></span> <span data-ttu-id="1d507-181">Pokud jste web publikovali pro poskytovatele hostingu, použijte přihlašovací údaje, které poskytovatel konkrétně označil, k e-mailu.</span><span class="sxs-lookup"><span data-stu-id="1d507-181">If you've published your site to a hosting provider, use the credentials that the provider has specifically indicated are for email.</span></span> <span data-ttu-id="1d507-182">Tyto přihlašovací údaje se můžou lišit od přihlašovacích údajů, které používáte k publikování.</span><span class="sxs-lookup"><span data-stu-id="1d507-182">These credentials might be different from the credentials you use to publish.</span></span>
- <span data-ttu-id="1d507-183">Někdy nepotřebujete vůbec přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="1d507-183">Sometimes you don't need credentials at all.</span></span> <span data-ttu-id="1d507-184">Pokud posíláte e-mail pomocí osobního poskytovatele internetových služeb, váš poskytovatel e-mailu už může znát vaše přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="1d507-184">If you're sending email by using your personal ISP, your email provider might already know your credentials.</span></span> <span data-ttu-id="1d507-185">Po publikování může být nutné použít jiné přihlašovací údaje než při testování na místním počítači.</span><span class="sxs-lookup"><span data-stu-id="1d507-185">After you publish, you might need to use different credentials than when you test on your local computer.</span></span>
- <span data-ttu-id="1d507-186">Pokud poskytovatel e-mailu používá šifrování, nastavte `WebMail.EnableSsl` na `true`.</span><span class="sxs-lookup"><span data-stu-id="1d507-186">If your email provider uses encryption, set `WebMail.EnableSsl` to `true`.</span></span>

<span data-ttu-id="1d507-187">Pokud při odesílání e-mailů dojde k chybě, může se zobrazit standardní chybová zpráva ASP.NET, která vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="1d507-187">If there is an error sending email, you might see a standard ASP.NET error message, which looks like this:</span></span>

![ASP.NET chybová zpráva, když dojde k problému s e-mailem](aspnet-web-pages-razor-troubleshooting-guide/_static/image1.png)

<span data-ttu-id="1d507-189">Problémy s posíláním e-mailu můžete také ladit pomocí `try-catch`ho bloku, jak je uvedeno v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="1d507-189">You can also debug problems with sending email by using a `try-catch` block, as in the following example.</span></span> <span data-ttu-id="1d507-190">Když použijete blok `try-catch`, nezobrazuje ASP.NET standardní chybové zprávy.</span><span class="sxs-lookup"><span data-stu-id="1d507-190">When you use a `try-catch` block, ASP.NET does not display its standard error messages.</span></span> <span data-ttu-id="1d507-191">Místo toho můžete zachytit chybu v `catch` části bloku.</span><span class="sxs-lookup"><span data-stu-id="1d507-191">Instead, you can capture the error in the `catch` portion of the block.</span></span>

[!code-cshtml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample3.cshtml)]

<span data-ttu-id="1d507-192">Nahraďte příslušné hodnoty pro `your-SMTP-server-name`a tak dále.</span><span class="sxs-lookup"><span data-stu-id="1d507-192">Substitute the appropriate values for `your-SMTP-server-name`, and so on.</span></span> <span data-ttu-id="1d507-193">Mezi chybové zprávy, které vidíte tímto způsobem, patří následující:</span><span class="sxs-lookup"><span data-stu-id="1d507-193">Some of the error messages you might see this way include the following:</span></span>

- <span data-ttu-id="1d507-194">*Odeslání e-mailu se nezdařilo.*</span><span class="sxs-lookup"><span data-stu-id="1d507-194">*Failure sending mail.*</span></span>

    <span data-ttu-id="1d507-195">-nebo-</span><span class="sxs-lookup"><span data-stu-id="1d507-195">-or-</span></span>

    <span data-ttu-id="1d507-196">*Pokus o připojení se nezdařil, protože připojená strana nereagovala po určitém časovém intervalu správně nebo navázáno připojení selhalo, protože se nepovedlo odpovědět připojeného hostitele.*</span><span class="sxs-lookup"><span data-stu-id="1d507-196">*A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond*</span></span>

    <span data-ttu-id="1d507-197">Tato chyba obvykle znamená, že se aplikace nemohla připojit k serveru SMTP.</span><span class="sxs-lookup"><span data-stu-id="1d507-197">This error usually means that the application could not connect to the SMTP server.</span></span> <span data-ttu-id="1d507-198">Ověřte název serveru a číslo portu.</span><span class="sxs-lookup"><span data-stu-id="1d507-198">Check the server name and port number.</span></span>
- <span data-ttu-id="1d507-199">*Poštovní schránka není k dispozici. Odpověď serveru byla: 5.1.0 &lt;someuser@invaliddomain&gt; odesilatel byl odmítnut: Neplatná doména odesílatele.*</span><span class="sxs-lookup"><span data-stu-id="1d507-199">*Mailbox unavailable. The server response was: 5.1.0 &lt;someuser@invaliddomain&gt; sender rejected : invalid sender domain*</span></span>

    <span data-ttu-id="1d507-200">Tato zpráva může značit, že adresa `From` není správná nebo chybí.</span><span class="sxs-lookup"><span data-stu-id="1d507-200">This message can indicate that the `From` address is not correct or is missing.</span></span>
- <span data-ttu-id="1d507-201">*Zadaný řetězec není ve formátu vyžadovaném pro e-mailovou adresu.*</span><span class="sxs-lookup"><span data-stu-id="1d507-201">*The specified string is not in the form required for an email address.*</span></span>

    <span data-ttu-id="1d507-202">Tato chyba může znamenat, že hodnota `To` nebo `From` vlastností není rozpoznána jako e-mailové adresy.</span><span class="sxs-lookup"><span data-stu-id="1d507-202">This error might indicate that the value of the `To` or `From` properties are not recognized as email addresses.</span></span> <span data-ttu-id="1d507-203">(ASP.NET nemůže ověřit, zda je e-mailová adresa platná, zda je ve správném formátu, například *name@domain.com* .)</span><span class="sxs-lookup"><span data-stu-id="1d507-203">(ASP.NET cannot check that the email address is valid, only that it's in the correct format, like *name@domain.com*.)</span></span>

> [!NOTE]
> <span data-ttu-id="1d507-204">Před publikováním stránky na živém webu odeberte kód, který zobrazí chybu (`@errorMessage`).</span><span class="sxs-lookup"><span data-stu-id="1d507-204">Remove the markup that displays the error (`@errorMessage`) before you publish the page to a live site.</span></span> <span data-ttu-id="1d507-205">Není vhodné, aby uživatelé viděli chybové zprávy, které získáte ze serveru.</span><span class="sxs-lookup"><span data-stu-id="1d507-205">It's not a good idea to let users see error messages that you get from a server.</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="1d507-206">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="1d507-206">Additional Resources</span></span>

[<span data-ttu-id="1d507-207">Webové stránky ASP.NET (Razor) – časté otázky</span><span class="sxs-lookup"><span data-stu-id="1d507-207">ASP.NET Web Pages (Razor) FAQ</span></span>](https://go.microsoft.com/fwlink/?LinkId=253000)

<span data-ttu-id="1d507-208">Fórum [webových stránek WebMatrix a ASP.NET](https://forums.asp.net/1224.aspx/1?WebMatrix) na webu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1d507-208">[WebMatrix and ASP.NET Web Pages](https://forums.asp.net/1224.aspx/1?WebMatrix) forum on the ASP.NET website</span></span>
