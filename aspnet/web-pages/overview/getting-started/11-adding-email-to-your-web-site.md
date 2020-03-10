---
uid: web-pages/overview/getting-started/11-adding-email-to-your-web-site
title: Odesílání e-mailů z webu ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tato kapitola vysvětluje, jak odeslat automatizovanou e-mailovou zprávu z webu.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: fc49bcb9-f1a9-4048-8c3f-b60951853200
msc.legacyurl: /web-pages/overview/getting-started/11-adding-email-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 23e9717329525fb5a0ed505c9dc94505d4f9dbbe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634713"
---
# <a name="sending-email-from-an-aspnet-web-pages-razor-site"></a>Odesílání e-mailů z webu ASP.NET Web Pages (Razor)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek vysvětluje, jak odeslat e-mailovou zprávu z webu při použití webových stránek ASP.NET (Razor).
> 
> Naučíte se:
> 
> - Jak odeslat e-mailovou zprávu z webu
> - Jak připojit soubor k e-mailové zprávě
> 
> Toto je funkce ASP.NET představená v článku:
> 
> - Pomocná rutina `WebMail`
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 3
>   
> 
> Tento kurz funguje také s ASP.NET webovými stránkami 2.

<a id="Sending_Email_Messages"></a>
## <a name="sending-email-messages-from-your-website"></a>Posílání e-mailových zpráv z webu

K dispozici jsou nejrůznější důvody, proč možná budete potřebovat poslat e-mailovou adresu z webu. Můžete odesílat uživatelům potvrzovací zprávy nebo vám můžou poslat oznámení sami (například to, že se zaregistroval nový uživatel). Pomocná rutina `WebMail` vám usnadňuje odesílání e-mailů.

Chcete-li použít pomocníka `WebMail`, musíte mít přístup k serveru SMTP. (SMTP představuje *protokol Simple Mail Transfer*.) Server SMTP je e-mailový server, který přesměruje zprávy na server &#8212; příjemce, že se jedná o odchozí stranu e-mailu. Pokud pro svůj web použijete poskytovatele hostingu, nastavili jste se na něj e-mail a můžou vám sdělit, co váš název serveru SMTP. Pokud pracujete v podnikové síti, může vám správce nebo oddělení IT obvykle poskytnout informace o serveru SMTP, který můžete použít. Pokud pracujete doma, možná budete moct testovat pomocí svého běžného poskytovatele e-mailu, který vám může sdělit název serveru SMTP. Obvykle potřebujete:

- Název serveru SMTP.
- Číslo portu. To je téměř vždy 25. Poskytovatel internetových služeb ale může vyžadovat, abyste používali port 587. Pokud k e-mailu používáte protokol SSL (Secure Sockets Layer), budete možná potřebovat jiný port. Obraťte se na poskytovatele e-mailu.
- Přihlašovací údaje (uživatelské jméno, heslo).

V tomto postupu vytvoříte dvě stránky. První stránka obsahuje formulář, který umožňuje uživatelům zadat popis, jako by byl vyplněný formulářem technické podpory. První stránka odesílá informace do druhé stránky. Na druhé stránce kód extrahuje informace o uživateli a pošle e-mailovou zprávu. Také se zobrazí zpráva potvrzující, že byla přijata zpráva o problému.

![obrazu](11-adding-email-to-your-web-site/_static/image1.jpg)

> [!NOTE]
> Aby byl tento příklad jednoduchý, kód inicializuje `WebMail` pomocný pomocník na stránce, kde ho používáte. Pro reálné weby je však vhodnější umístit inicializační kód jako v globálním souboru, aby bylo možné inicializovat pomoc `WebMail` pro všechny soubory na webu. Další informace najdete v tématu [přizpůsobení chování na úrovni webu pro webové stránky ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers).

1. Vytvoří nový web.
2. Přidejte novou stránku s názvem *EmailRequest. cshtml* a přidejte následující kód: 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample1.html)]

    Všimněte si, že atribut `action` prvku Form byl nastaven na hodnotu *ProcessRequest. cshtml*. To znamená, že formulář bude odeslán do této stránky místo zpět na aktuální stránku.
3. Přidejte do webu novou stránku s názvem *ProcessRequest. cshtml* a přidejte následující kód a značku:   

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample2.cshtml)]

    V kódu získáte hodnoty polí formuláře, které byly odeslány na stránku. Pak zavoláte metodu `Send` pomocné rutiny `WebMail` k vytvoření a odeslání e-mailové zprávy. V tomto případě jsou hodnoty, které se mají použít, tvořeny textem, který je zřetězený s hodnotami, které byly odeslány z formuláře.

    Kód této stránky je uvnitř `try/catch`ho bloku. Pokud z nějakého důvodu pokus o odeslání e-mailu nefunguje (například nastavení nejsou pravá), kód v `catch`ovém bloku se spustí a nastaví proměnnou `errorMessage` na chybu, ke které došlo. (Další informace o `try/catch` blocích nebo značce `<text>` naleznete v tématu [Úvod do programování webových stránek ASP.NET pomocí syntaxe Razor](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors).)

    Pokud je proměnná `errorMessage` v těle stránky prázdná (výchozí nastavení), uživateli se zobrazí zpráva, že e-mailová zpráva byla odeslána. Pokud je proměnná `errorMessage` nastavená na hodnotu true, uživateli se zobrazí zpráva, že při odesílání zprávy došlo k potížím.

    Všimněte si, že v části stránky, která zobrazuje chybovou zprávu, existuje další test: `if(debuggingFlag)`. Toto je proměnná, kterou můžete nastavit na hodnotu true, pokud máte potíže při odesílání e-mailů. Pokud má `debuggingFlag` hodnotu true a pokud dojde k potížím při posílání e-mailu, zobrazí se další chybová zpráva s informacemi o tom, že ASP.NET při pokusu o odeslání e-mailové zprávy nahlásila jakákoli. Poctivé upozornění: chybové zprávy, které ASP.NET zprávy, když nelze odeslat e-mailovou zprávu, mohou být obecné. Pokud například ASP.NET nemůže kontaktovat server SMTP (například proto, že jste v názvu serveru provedli chybu), zobrazí se chyba `Failure sending mail`.

    > [!NOTE] 
    > 
    > **Důležité** informace Když obdržíte chybovou zprávu z objektu výjimky (`ex` v kódu), neprovádějte *rutině tuto zprávu* uživatelům. Objekty výjimek často obsahují informace, které by uživatelé neměli vidět a které mohou být dokonce ohrožením zabezpečení. Proto tento kód zahrnuje proměnnou `debuggingFlag`, která se používá jako přepínač k zobrazení chybové zprávy a proč je proměnná ve výchozím nastavení nastavena na hodnotu false. Tuto proměnnou byste měli nastavit na hodnotu true (a proto zobrazit chybovou zprávu) *pouze* v případě, že máte problém s odesíláním e-mailů a potřebujete ladit. Po dokončení řešení potíží nastavte `debuggingFlag` zpět na false.

    Upravte následující nastavení související s e-maily v kódu:

   - Nastavte `your-SMTP-host` na název serveru SMTP, ke kterému máte přístup.
   - Nastavte `your-user-name-here` na uživatelské jméno pro svůj účet serveru SMTP.
   - Nastavte `your-account-password` na heslo pro svůj účet serveru SMTP.
   - Nastavte `your-email-address-here` na vlastní e-mailovou adresu. Toto je e-mailová adresa, ze které se zpráva odesílá. (Někteří poskytovatelé e-mailu neumožňují zadat jinou adresu `From` a vaše uživatelské jméno bude používat jako `From`ová adresa.)

     > [!TIP] 
     > 
     > <a id="configuring_email_settings"></a>
     > ### <a name="configuring-email-settings"></a>Konfigurace nastavení e-mailu
     > 
     > V některých případech se může jednat o výzvu, abyste se ujistili, že máte správná nastavení pro server SMTP, číslo portu atd. Tady je několik tipů:
     > 
     > - Název serveru SMTP je často podobný jako `smtp.provider.com` nebo `smtp.provider.net`. Pokud ale publikujete lokalitu pro poskytovatele hostingu, může být název serveru SMTP v tomto okamžiku `localhost`. Důvodem je to, že po publikování a spuštění webu na serveru zprostředkovatele může být e-mailový server místní z perspektivy vaší aplikace. Tato změna v názvech serverů může znamenat, že je třeba změnit název serveru SMTP v rámci procesu publikování.
     > - Číslo portu je obvykle 25. Někteří poskytovatelé ale vyžadují, abyste používali port 587 nebo jiný port.
     > - Ujistěte se, že používáte správné přihlašovací údaje. Pokud jste web publikovali pro poskytovatele hostingu, použijte přihlašovací údaje, které poskytovatel konkrétně označil, k e-mailu. Ty se můžou lišit od přihlašovacích údajů, které používáte k publikování.
     > - Někdy nepotřebujete vůbec přihlašovací údaje. Pokud posíláte e-mail pomocí osobního poskytovatele internetových služeb, váš poskytovatel e-mailu už může znát vaše přihlašovací údaje. Po publikování může být nutné použít jiné přihlašovací údaje než při testování na místním počítači.
     > - Pokud poskytovatel e-mailu používá šifrování, musíte nastavit `WebMail.EnableSsl` na `true`.
4. Spusťte stránku *EmailRequest. cshtml* v prohlížeči. (Před spuštěním se ujistěte, že je stránka vybraná v pracovním prostoru **soubory** .)
5. Zadejte své jméno a popis problému a pak klikněte na tlačítko **Odeslat** . Budete přesměrováni na stránku *ProcessRequest. cshtml* , která potvrdí vaši zprávu a pošle vám e-mailovou zprávu. 

    ![obrazu](11-adding-email-to-your-web-site/_static/image2.jpg)

<a id="Sending_a_File"></a>
## <a name="sending-a-file-using-email"></a>Odeslání souboru pomocí e-mailu

Můžete také odesílat soubory, které jsou připojeny k e-mailovým zprávám. V tomto postupu vytvoříte textový soubor a dvě stránky HTML. Textový soubor použijete jako přílohu e-mailu.

1. Na webu přidejte nový textový soubor a pojmenujte ho *MyFile. txt*.
2. Zkopírujte následující text a vložte ho do souboru: 

    `Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.`
3. Vytvořte stránku s názvem *SendFile. cshtml* a přidejte následující kód: 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample3.html)]
4. Vytvořte stránku s názvem *ProcessFile. cshtml* a přidejte následující kód: 

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample4.cshtml)]
5. V kódu upravte následující nastavení související s e-maily v tomto příkladu:

    - Nastavte `your-SMTP-host` na název serveru SMTP, ke kterému máte přístup.
    - Nastavte `your-user-name-here` na uživatelské jméno pro svůj účet serveru SMTP.
    - Nastavte `your-email-address-here` na vlastní e-mailovou adresu. Toto je e-mailová adresa, ze které se zpráva odesílá.
    - Nastavte `your-account-password` na heslo pro svůj účet serveru SMTP.
    - Nastavte `target-email-address-here` na vlastní e-mailovou adresu. (Stejně jako dřív jste normálně poslali e-mail někomu jinému, ale pro testování ho můžete poslat sami.)
6. Spusťte stránku *SendFile. cshtml* v prohlížeči.
7. Zadejte své jméno, řádek předmětu a název textového souboru, který chcete připojit (*MyFile. txt*).
8. Klikněte na tlačítko `Submit`. Stejně jako dřív budete přesměrováni na stránku *ProcessFile. cshtml* , která potvrdí vaši zprávu a pošle vám e-mailovou zprávu s připojeným souborem.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Další prostředky

- [Webové stránky ASP.NET (Razor) – průvodce řešením potíží](https://go.microsoft.com/fwlink/?LinkId=253001)
- [Protokol SMTP (Simple Mail Transfer Protocol)](https://msdn.microsoft.com/library/aa480435.aspx)
- [Přizpůsobení chování na úrovni webu pro webové stránky v ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202906)
