---
uid: web-api/overview/security/working-with-ssl-in-web-api
title: Práce s protokolem SSL ve webovém rozhraní API | Microsoft Docs
author: MikeWasson
description: Ukazuje, jak používat protokol SSL s webovým rozhraním API ASP.NET, včetně použití klientských certifikátů SSL.
ms.author: riande
ms.date: 02/22/2019
ms.assetid: 97f6164f-59cf-45c0-b820-e4aa29b45396
msc.legacyurl: /web-api/overview/security/working-with-ssl-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 31589b3713b1f1a9b98d12906bfef81f8bf5e3f9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598635"
---
# <a name="working-with-ssl-in-web-api"></a><span data-ttu-id="2f23d-103">Práce s protokolem SSL v rozhraní Web API</span><span class="sxs-lookup"><span data-stu-id="2f23d-103">Working with SSL in Web API</span></span>

<span data-ttu-id="2f23d-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2f23d-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2f23d-105">Několik běžných schémat ověřování není v případě obyčejného protokolu HTTP zabezpečené.</span><span class="sxs-lookup"><span data-stu-id="2f23d-105">Several common authentication schemes are not secure over plain HTTP.</span></span> <span data-ttu-id="2f23d-106">Konkrétně základní ověřování a ověřování formulářů odesílají nezašifrované přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="2f23d-106">In particular, Basic authentication and forms authentication send unencrypted credentials.</span></span> <span data-ttu-id="2f23d-107">Aby bylo zajištěno zabezpečení, *musí* tato schémata ověřování používat protokol SSL.</span><span class="sxs-lookup"><span data-stu-id="2f23d-107">To be secure, these authentication schemes *must* use SSL.</span></span> <span data-ttu-id="2f23d-108">K ověřování klientů se navíc dají použít klientské certifikáty SSL.</span><span class="sxs-lookup"><span data-stu-id="2f23d-108">In addition, SSL client certificates can be used to authenticate clients.</span></span>

## <a name="enabling-ssl-on-the-server"></a><span data-ttu-id="2f23d-109">Povolení protokolu SSL na serveru</span><span class="sxs-lookup"><span data-stu-id="2f23d-109">Enabling SSL on the Server</span></span>

<span data-ttu-id="2f23d-110">Nastavení SSL v IIS 7 nebo novějším:</span><span class="sxs-lookup"><span data-stu-id="2f23d-110">To set up SSL in IIS 7 or later:</span></span>

- <span data-ttu-id="2f23d-111">Vytvořte nebo Získejte certifikát.</span><span class="sxs-lookup"><span data-stu-id="2f23d-111">Create or get a certificate.</span></span> <span data-ttu-id="2f23d-112">Pro účely testování můžete vytvořit certifikát podepsaný svým držitelem.</span><span class="sxs-lookup"><span data-stu-id="2f23d-112">For testing, you can create a self-signed certificate.</span></span>
- <span data-ttu-id="2f23d-113">Přidejte vazbu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2f23d-113">Add an HTTPS binding.</span></span>

<span data-ttu-id="2f23d-114">Podrobnosti najdete v tématu [jak nastavit SSL na IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).</span><span class="sxs-lookup"><span data-stu-id="2f23d-114">For details, see [How to Set Up SSL on IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).</span></span>

<span data-ttu-id="2f23d-115">V případě místního testování můžete povolit protokol SSL v IIS Express ze sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2f23d-115">For local testing, you can enable SSL in IIS Express from Visual Studio.</span></span> <span data-ttu-id="2f23d-116">V okno Vlastnosti nastavte možnost **SSL povoleno** na **hodnotu true**.</span><span class="sxs-lookup"><span data-stu-id="2f23d-116">In the Properties window, set **SSL Enabled** to **True**.</span></span> <span data-ttu-id="2f23d-117">Poznamenejte si hodnotu **URL SSL**; tuto adresu URL použijte pro testování připojení HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2f23d-117">Note the value of **SSL URL**; use this URL for testing HTTPS connections.</span></span>

![](working-with-ssl-in-web-api/_static/image1.png)

### <a name="enforcing-ssl-in-a-web-api-controller"></a><span data-ttu-id="2f23d-118">Vynucování SSL v kontroleru webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="2f23d-118">Enforcing SSL in a Web API Controller</span></span>

<span data-ttu-id="2f23d-119">Pokud máte vazbu HTTPS i HTTP, klienti stále můžou k přístupu k webu používat protokol HTTP.</span><span class="sxs-lookup"><span data-stu-id="2f23d-119">If you have both an HTTPS and an HTTP binding, clients can still use HTTP to access the site.</span></span> <span data-ttu-id="2f23d-120">Může být možné, že některé prostředky budou k dispozici prostřednictvím protokolu HTTP, zatímco jiné prostředky vyžadují protokol SSL.</span><span class="sxs-lookup"><span data-stu-id="2f23d-120">You might allow some resources to be available through HTTP, while other resources require SSL.</span></span> <span data-ttu-id="2f23d-121">V takovém případě použijte filtr akcí pro vyžadování protokolu SSL pro chráněné prostředky.</span><span class="sxs-lookup"><span data-stu-id="2f23d-121">In that case, use an action filter to require SSL for the protected resources.</span></span> <span data-ttu-id="2f23d-122">Následující kód ukazuje filtr ověřování webového rozhraní API, který kontroluje protokol SSL:</span><span class="sxs-lookup"><span data-stu-id="2f23d-122">The following code shows a Web API authentication filter that checks for SSL:</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample1.cs)]

<span data-ttu-id="2f23d-123">Přidejte tento filtr do všech akcí webového rozhraní API, které vyžadují protokol SSL:</span><span class="sxs-lookup"><span data-stu-id="2f23d-123">Add this filter to any Web API actions that require SSL:</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample2.cs)]

## <a name="ssl-client-certificates"></a><span data-ttu-id="2f23d-124">Klientské certifikáty SSL</span><span class="sxs-lookup"><span data-stu-id="2f23d-124">SSL Client Certificates</span></span>

<span data-ttu-id="2f23d-125">SSL zajišťuje ověřování pomocí certifikátů infrastruktury veřejných klíčů.</span><span class="sxs-lookup"><span data-stu-id="2f23d-125">SSL provides authentication by using Public Key Infrastructure certificates.</span></span> <span data-ttu-id="2f23d-126">Server musí poskytovat certifikát, který ověřuje server pro klienta.</span><span class="sxs-lookup"><span data-stu-id="2f23d-126">The server must provide a certificate that authenticates the server to the client.</span></span> <span data-ttu-id="2f23d-127">Je méně běžné, že klient poskytuje certifikát serveru, ale jedná se o jednu možnost ověřování klientů.</span><span class="sxs-lookup"><span data-stu-id="2f23d-127">It is less common for the client to provide a certificate to the server, but this is one option for authenticating clients.</span></span> <span data-ttu-id="2f23d-128">Pokud chcete používat klientské certifikáty s protokolem SSL, budete potřebovat způsob distribuce podepsaných certifikátů uživatelům.</span><span class="sxs-lookup"><span data-stu-id="2f23d-128">To use client certificates with SSL, you need a way to distribute signed certificates to your users.</span></span> <span data-ttu-id="2f23d-129">Pro mnoho typů aplikací to nebude dobrým uživatelským prostředím, ale v některých prostředích (například v podniku) může být proveditelné.</span><span class="sxs-lookup"><span data-stu-id="2f23d-129">For many application types, this will not be a good user experience, but in some environments (for example, enterprise) it may be feasible.</span></span>

| <span data-ttu-id="2f23d-130">Výhody</span><span class="sxs-lookup"><span data-stu-id="2f23d-130">Advantages</span></span> | <span data-ttu-id="2f23d-131">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="2f23d-131">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="2f23d-132">-Přihlašovací údaje certifikátu jsou silnější než uživatelské jméno a heslo.</span><span class="sxs-lookup"><span data-stu-id="2f23d-132">- Certificate credentials are stronger than username/password.</span></span> <span data-ttu-id="2f23d-133">-SSL poskytuje kompletní zabezpečený kanál s ověřováním, integritou zpráv a šifrováním zpráv.</span><span class="sxs-lookup"><span data-stu-id="2f23d-133">- SSL provides a complete secure channel, with authentication, message integrity, and message encryption.</span></span> | <span data-ttu-id="2f23d-134">– Musíte získat a spravovat certifikáty PKI.</span><span class="sxs-lookup"><span data-stu-id="2f23d-134">- You must obtain and manage PKI certificates.</span></span> <span data-ttu-id="2f23d-135">-Klientská platforma musí podporovat klientské certifikáty SSL.</span><span class="sxs-lookup"><span data-stu-id="2f23d-135">- The client platform must support SSL client certificates.</span></span> |

<span data-ttu-id="2f23d-136">Chcete-li nakonfigurovat službu IIS tak, aby přijímala klientské certifikáty, otevřete Správce služby IIS a proveďte následující kroky:</span><span class="sxs-lookup"><span data-stu-id="2f23d-136">To configure IIS to accept client certificates, open IIS Manager and perform the following steps:</span></span>

1. <span data-ttu-id="2f23d-137">Ve stromovém zobrazení klikněte na uzel lokalita.</span><span class="sxs-lookup"><span data-stu-id="2f23d-137">Click the site node in the tree view.</span></span>
2. <span data-ttu-id="2f23d-138">Dvakrát klikněte na funkci **Nastavení SSL** v prostředním podokně.</span><span class="sxs-lookup"><span data-stu-id="2f23d-138">Double-click the **SSL Settings** feature in the middle pane.</span></span>
3. <span data-ttu-id="2f23d-139">V části **klientské certifikáty**vyberte jednu z následujících možností:</span><span class="sxs-lookup"><span data-stu-id="2f23d-139">Under **Client Certificates**, select one of these options:</span></span> 

    - <span data-ttu-id="2f23d-140">**Přijmout**: Internetová informační služba bude přijímat certifikát od klienta, ale nevyžaduje jednu z nich.</span><span class="sxs-lookup"><span data-stu-id="2f23d-140">**Accept**: IIS will accept a certificate from the client, but does not require one.</span></span>
    - <span data-ttu-id="2f23d-141">**Vyžadovat**: vyžadování klientského certifikátu.</span><span class="sxs-lookup"><span data-stu-id="2f23d-141">**Require**: Require a client certificate.</span></span> <span data-ttu-id="2f23d-142">(Pokud chcete povolit tuto možnost, musíte taky vybrat "vyžadovat SSL".)</span><span class="sxs-lookup"><span data-stu-id="2f23d-142">(To enable this option, you must also select "Require SSL")</span></span>

<span data-ttu-id="2f23d-143">Můžete také nastavit tyto možnosti v souboru ApplicationHost. config:</span><span class="sxs-lookup"><span data-stu-id="2f23d-143">You can also set these options in the ApplicationHost.config file:</span></span>

[!code-xml[Main](working-with-ssl-in-web-api/samples/sample3.xml)]

<span data-ttu-id="2f23d-144">Příznak **SslNegotiateCert** znamená, že služba IIS přijme certifikát od klienta, ale nevyžaduje jeden (ekvivalent možnosti "přijmout" ve Správci služby IIS).</span><span class="sxs-lookup"><span data-stu-id="2f23d-144">The **SslNegotiateCert** flag means IIS will accept a certificate from the client, but does not require one (equivalent to the "Accept" option in IIS Manager).</span></span> <span data-ttu-id="2f23d-145">Pro vyžadování certifikátu nastavte příznak **SslRequireCert** .</span><span class="sxs-lookup"><span data-stu-id="2f23d-145">To require a certificate, set the **SslRequireCert** flag.</span></span> <span data-ttu-id="2f23d-146">Pro testování můžete také nastavit tyto možnosti v IIS Express v místním hostiteli aplikace. Konfigurační soubor umístěný v části "Documents\IISExpress\config".</span><span class="sxs-lookup"><span data-stu-id="2f23d-146">For testing, you can also set these options in IIS Express, in the local applicationhost.Config file, located in "Documents\IISExpress\config".</span></span>

### <a name="creating-a-client-certificate-for-testing"></a><span data-ttu-id="2f23d-147">Vytvoření klientského certifikátu pro testování</span><span class="sxs-lookup"><span data-stu-id="2f23d-147">Creating a Client Certificate for Testing</span></span>

<span data-ttu-id="2f23d-148">Pro účely testování můžete použít nástroj [Makecert. exe](/windows/desktop/SecCrypto/makecert) k vytvoření klientského certifikátu.</span><span class="sxs-lookup"><span data-stu-id="2f23d-148">For testing purposes, you can use [MakeCert.exe](/windows/desktop/SecCrypto/makecert) to create a client certificate.</span></span> <span data-ttu-id="2f23d-149">Nejdřív vytvořte kořenovou autoritu testu:</span><span class="sxs-lookup"><span data-stu-id="2f23d-149">First, create a test root authority:</span></span>

[!code-console[Main](working-with-ssl-in-web-api/samples/sample4.cmd)]

<span data-ttu-id="2f23d-150">Makecert zobrazí výzvu k zadání hesla pro privátní klíč.</span><span class="sxs-lookup"><span data-stu-id="2f23d-150">Makecert will prompt you to enter a password for the private key.</span></span>

<span data-ttu-id="2f23d-151">Dále přidejte certifikát do úložiště Důvěryhodné kořenové certifikační autority testovacího serveru následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="2f23d-151">Next, add the certificate to the test server's "Trusted Root Certification Authorities" store, as follows:</span></span>

1. <span data-ttu-id="2f23d-152">Otevřete konzolu MMC.</span><span class="sxs-lookup"><span data-stu-id="2f23d-152">Open MMC.</span></span>
2. <span data-ttu-id="2f23d-153">V části **soubor**vyberte **Přidat nebo odebrat modul snap-in**.</span><span class="sxs-lookup"><span data-stu-id="2f23d-153">Under **File**, select **Add/Remove Snap-In**.</span></span>
3. <span data-ttu-id="2f23d-154">Vyberte možnost **účet počítače**.</span><span class="sxs-lookup"><span data-stu-id="2f23d-154">Select **Computer Account**.</span></span>
4. <span data-ttu-id="2f23d-155">Vyberte **místní počítač** a dokončete průvodce.</span><span class="sxs-lookup"><span data-stu-id="2f23d-155">Select **Local computer** and complete the wizard.</span></span>
5. <span data-ttu-id="2f23d-156">V navigačním podokně rozbalte uzel důvěryhodné kořenové certifikační autority.</span><span class="sxs-lookup"><span data-stu-id="2f23d-156">Under the navigation pane, expand the "Trusted Root Certification Authorities" node.</span></span>
6. <span data-ttu-id="2f23d-157">V nabídce **Akce** přejděte na **všechny úlohy**a potom kliknutím na **importovat** spusťte Průvodce importem certifikátu.</span><span class="sxs-lookup"><span data-stu-id="2f23d-157">On the **Action** menu, point to **All Tasks**, and then click **Import** to start the Certificate Import Wizard.</span></span>
7. <span data-ttu-id="2f23d-158">Vyhledejte soubor certifikátu TempCA. cer.</span><span class="sxs-lookup"><span data-stu-id="2f23d-158">Browse to the certificate file, TempCA.cer.</span></span>
8. <span data-ttu-id="2f23d-159">Klikněte na **otevřít**a potom na **Další** a dokončete průvodce.</span><span class="sxs-lookup"><span data-stu-id="2f23d-159">Click **Open**, then click **Next** and complete the wizard.</span></span> <span data-ttu-id="2f23d-160">(Budete vyzváni k zadání hesla znovu.)</span><span class="sxs-lookup"><span data-stu-id="2f23d-160">(You will be prompted to re-enter the password.)</span></span>

<span data-ttu-id="2f23d-161">Nyní vytvořte certifikát klienta, který je podepsán prvním certifikátem:</span><span class="sxs-lookup"><span data-stu-id="2f23d-161">Now create a client certificate that is signed by the first certificate:</span></span>

[!code-console[Main](working-with-ssl-in-web-api/samples/sample5.cmd)]

### <a name="using-client-certificates-in-web-api"></a><span data-ttu-id="2f23d-162">Použití klientských certifikátů ve webovém rozhraní API</span><span class="sxs-lookup"><span data-stu-id="2f23d-162">Using Client Certificates in Web API</span></span>

<span data-ttu-id="2f23d-163">Na straně serveru můžete získat certifikát klienta voláním [GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx) ve zprávě požadavku.</span><span class="sxs-lookup"><span data-stu-id="2f23d-163">On the server side, you can get the client certificate by calling [GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx) on the request message.</span></span> <span data-ttu-id="2f23d-164">Metoda vrátí hodnotu null, pokud není k dispozici klientský certifikát.</span><span class="sxs-lookup"><span data-stu-id="2f23d-164">The method returns null if there is no client certificate.</span></span> <span data-ttu-id="2f23d-165">V opačném případě vrátí instanci **X509Certificate2** .</span><span class="sxs-lookup"><span data-stu-id="2f23d-165">Otherwise, it returns an **X509Certificate2** instance.</span></span> <span data-ttu-id="2f23d-166">Pomocí tohoto objektu můžete získat informace z certifikátu, jako je například Vystavitel a předmět.</span><span class="sxs-lookup"><span data-stu-id="2f23d-166">Use this object to get information from the certificate, such as the issuer and subject.</span></span> <span data-ttu-id="2f23d-167">Pak můžete tyto informace použít k ověřování a/nebo autorizaci.</span><span class="sxs-lookup"><span data-stu-id="2f23d-167">Then you can use this information for authentication and/or authorization.</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample6.cs)]
