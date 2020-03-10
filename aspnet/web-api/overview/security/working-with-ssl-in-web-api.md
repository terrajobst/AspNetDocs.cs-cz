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
# <a name="working-with-ssl-in-web-api"></a>Práce s protokolem SSL v rozhraní Web API

o [Jan Wasson](https://github.com/MikeWasson)

Několik běžných schémat ověřování není v případě obyčejného protokolu HTTP zabezpečené. Konkrétně základní ověřování a ověřování formulářů odesílají nezašifrované přihlašovací údaje. Aby bylo zajištěno zabezpečení, *musí* tato schémata ověřování používat protokol SSL. K ověřování klientů se navíc dají použít klientské certifikáty SSL.

## <a name="enabling-ssl-on-the-server"></a>Povolení protokolu SSL na serveru

Nastavení SSL v IIS 7 nebo novějším:

- Vytvořte nebo Získejte certifikát. Pro účely testování můžete vytvořit certifikát podepsaný svým držitelem.
- Přidejte vazbu HTTPS.

Podrobnosti najdete v tématu [jak nastavit SSL na IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).

V případě místního testování můžete povolit protokol SSL v IIS Express ze sady Visual Studio. V okno Vlastnosti nastavte možnost **SSL povoleno** na **hodnotu true**. Poznamenejte si hodnotu **URL SSL**; tuto adresu URL použijte pro testování připojení HTTPS.

![](working-with-ssl-in-web-api/_static/image1.png)

### <a name="enforcing-ssl-in-a-web-api-controller"></a>Vynucování SSL v kontroleru webového rozhraní API

Pokud máte vazbu HTTPS i HTTP, klienti stále můžou k přístupu k webu používat protokol HTTP. Může být možné, že některé prostředky budou k dispozici prostřednictvím protokolu HTTP, zatímco jiné prostředky vyžadují protokol SSL. V takovém případě použijte filtr akcí pro vyžadování protokolu SSL pro chráněné prostředky. Následující kód ukazuje filtr ověřování webového rozhraní API, který kontroluje protokol SSL:

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample1.cs)]

Přidejte tento filtr do všech akcí webového rozhraní API, které vyžadují protokol SSL:

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample2.cs)]

## <a name="ssl-client-certificates"></a>Klientské certifikáty SSL

SSL zajišťuje ověřování pomocí certifikátů infrastruktury veřejných klíčů. Server musí poskytovat certifikát, který ověřuje server pro klienta. Je méně běžné, že klient poskytuje certifikát serveru, ale jedná se o jednu možnost ověřování klientů. Pokud chcete používat klientské certifikáty s protokolem SSL, budete potřebovat způsob distribuce podepsaných certifikátů uživatelům. Pro mnoho typů aplikací to nebude dobrým uživatelským prostředím, ale v některých prostředích (například v podniku) může být proveditelné.

| Výhody | Nevýhody |
| --- | --- |
| -Přihlašovací údaje certifikátu jsou silnější než uživatelské jméno a heslo. -SSL poskytuje kompletní zabezpečený kanál s ověřováním, integritou zpráv a šifrováním zpráv. | – Musíte získat a spravovat certifikáty PKI. -Klientská platforma musí podporovat klientské certifikáty SSL. |

Chcete-li nakonfigurovat službu IIS tak, aby přijímala klientské certifikáty, otevřete Správce služby IIS a proveďte následující kroky:

1. Ve stromovém zobrazení klikněte na uzel lokalita.
2. Dvakrát klikněte na funkci **Nastavení SSL** v prostředním podokně.
3. V části **klientské certifikáty**vyberte jednu z následujících možností: 

    - **Přijmout**: Internetová informační služba bude přijímat certifikát od klienta, ale nevyžaduje jednu z nich.
    - **Vyžadovat**: vyžadování klientského certifikátu. (Pokud chcete povolit tuto možnost, musíte taky vybrat "vyžadovat SSL".)

Můžete také nastavit tyto možnosti v souboru ApplicationHost. config:

[!code-xml[Main](working-with-ssl-in-web-api/samples/sample3.xml)]

Příznak **SslNegotiateCert** znamená, že služba IIS přijme certifikát od klienta, ale nevyžaduje jeden (ekvivalent možnosti "přijmout" ve Správci služby IIS). Pro vyžadování certifikátu nastavte příznak **SslRequireCert** . Pro testování můžete také nastavit tyto možnosti v IIS Express v místním hostiteli aplikace. Konfigurační soubor umístěný v části "Documents\IISExpress\config".

### <a name="creating-a-client-certificate-for-testing"></a>Vytvoření klientského certifikátu pro testování

Pro účely testování můžete použít nástroj [Makecert. exe](/windows/desktop/SecCrypto/makecert) k vytvoření klientského certifikátu. Nejdřív vytvořte kořenovou autoritu testu:

[!code-console[Main](working-with-ssl-in-web-api/samples/sample4.cmd)]

Makecert zobrazí výzvu k zadání hesla pro privátní klíč.

Dále přidejte certifikát do úložiště Důvěryhodné kořenové certifikační autority testovacího serveru následujícím způsobem:

1. Otevřete konzolu MMC.
2. V části **soubor**vyberte **Přidat nebo odebrat modul snap-in**.
3. Vyberte možnost **účet počítače**.
4. Vyberte **místní počítač** a dokončete průvodce.
5. V navigačním podokně rozbalte uzel důvěryhodné kořenové certifikační autority.
6. V nabídce **Akce** přejděte na **všechny úlohy**a potom kliknutím na **importovat** spusťte Průvodce importem certifikátu.
7. Vyhledejte soubor certifikátu TempCA. cer.
8. Klikněte na **otevřít**a potom na **Další** a dokončete průvodce. (Budete vyzváni k zadání hesla znovu.)

Nyní vytvořte certifikát klienta, který je podepsán prvním certifikátem:

[!code-console[Main](working-with-ssl-in-web-api/samples/sample5.cmd)]

### <a name="using-client-certificates-in-web-api"></a>Použití klientských certifikátů ve webovém rozhraní API

Na straně serveru můžete získat certifikát klienta voláním [GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx) ve zprávě požadavku. Metoda vrátí hodnotu null, pokud není k dispozici klientský certifikát. V opačném případě vrátí instanci **X509Certificate2** . Pomocí tohoto objektu můžete získat informace z certifikátu, jako je například Vystavitel a předmět. Pak můžete tyto informace použít k ověřování a/nebo autorizaci.

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample6.cs)]
