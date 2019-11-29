---
uid: web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
title: 'Nasazení webu ASP.NET pomocí sady Visual Studio: nastavení oprávnění složky | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která bude Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9715a121-fa55-4f1b-a5d2-fb3f6cd8be8f
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
msc.type: authoredcontent
ms.openlocfilehash: 410525bb2e3f6e5a0be6d7d6b33fb3a40509041a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74614942"
---
# <a name="aspnet-web-deployment-using-visual-studio-setting-folder-permissions"></a>Nasazení webu ASP.NET pomocí sady Visual Studio: nastavení oprávnění složky

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která umožňuje Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí sady Visual Studio 2012 nebo Visual Studio 2010. Informace o řadě najdete v [prvním kurzu v řadě](introduction.md).

## <a name="overview"></a>Přehled

V tomto kurzu nastavíte oprávnění složky pro složku *knihovny elmah* na nasazeném webu tak, aby aplikace mohla v této složce vytvářet soubory protokolů.

Při testování webové aplikace v aplikaci Visual Studio pomocí vývojového serveru sady Visual Studio (Cassini) nebo IIS Express aplikace běží pod vaší identitou. Pravděpodobně jste správcem vašeho vývojového počítače a máte plnou autoritu, abyste mohli cokoli dělat s jakýmkoli souborem v jakékoli složce. V případě, že je aplikace spuštěna v rámci služby IIS, je spuštěna pod identitou definovanou pro fond aplikací, ke kterému je lokalita přiřazena. Obvykle se jedná o účet definovaný systémem, který má omezená oprávnění. Ve výchozím nastavení má oprávnění číst a spustit pro soubory a složky webové aplikace, ale nemá přístup pro zápis.

Dojde k problému, pokud vaše aplikace vytvoří nebo aktualizuje soubory, což je běžné nutnost ve webových aplikacích. V aplikaci Contoso University knihovny elmah vytvoří ve složce *knihovny elmah* soubory XML, aby se uložily podrobnosti o chybách. I když nepoužíváte něco jako knihovny elmah, může váš web umožnit uživatelům nahrávat soubory nebo provádět jiné úkoly, které zapisují data do složky ve vaší lokalitě.

Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje při procházení tohoto kurzu, zkontrolujte [stránku řešení potíží](troubleshooting.md).

## <a name="test-error-logging-and-reporting"></a>Protokolování a vytváření sestav chyb testu

Chcete-li zjistit, jak aplikace nefunguje správně ve službě IIS (i když to bylo při testování v aplikaci Visual Studio), můžete způsobit chybu, která by normálně byla protokolována nástrojem knihovny elmah, a potom otevřít protokol chyb knihovny elmah a zobrazit podrobnosti. Pokud knihovny elmah nemohl vytvořit soubor XML a uložit podrobnosti o chybě, zobrazí se prázdná zpráva o chybě.

Otevřete prohlížeč a klikněte na `http://localhost/ContosoUniversity`a pak si vyžádejte neplatnou adresu URL, jako je *Studentsxxx. aspx*. Namísto stránky *GenericErrorPage. aspx* se zobrazí systémem generovaná chybová stránka, protože nastavení `customErrors` v souboru Web. config je "remoteonly" a místní služba IIS je spuštěna:

![Chybová stránka HTTP 404](setting-folder-permissions/_static/image1.png)

Nyní spusťte *knihovny elmah. axd* , aby se zobrazila zpráva o chybách. Po přihlášení pomocí přihlašovacích údajů účtu správce (&quot;správce&quot; a &quot;devpwd&quot;) se zobrazí prázdná stránka protokolu chyb, protože knihovny elmah se nepodařilo vytvořit soubor XML ve složce *knihovny elmah* :

![Prázdný protokol chyb](setting-folder-permissions/_static/image2.png)

## <a name="set-write-permission-on-the-elmah-folder"></a>Nastavení oprávnění k zápisu ve složce knihovny elmah

Oprávnění ke složkám můžete nastavit ručně nebo ji můžete nastavit jako automatickou součást procesu nasazení. Díky tomu, že automatické vyžaduje komplexní kód MSBuild a že je potřeba to udělat jenom při prvním nasazení, se v následujících krocích provede ruční postup. (Informace o tom, jak provést tuto část procesu nasazení, najdete v tématu [Nastavení oprávnění složky na webu publikování](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) na blogu Sayed Hashimi.)

1. V **Průzkumníku souborů**přejděte na *C:\inetpub\wwwroot\ContosoUniversity*. Klikněte pravým tlačítkem na složku *knihovny elmah* , vyberte **vlastnosti**a pak vyberte kartu **zabezpečení** .
2. Klikněte na **Upravit**.
3. V dialogovém okně **oprávnění pro knihovny elmah** vyberte **DefaultAppPool**a potom zaškrtněte políčko **zapsat** ve sloupci **povoleno** .

    ![Oprávnění pro složku knihovny ELMAH](setting-folder-permissions/_static/image3.png)

    (Pokud v seznamu **název skupiny nebo jméno uživatele** nevidíte **DefaultAppPool** , pravděpodobně jste v tomto kurzu nastavili službu IIS a ASP.NET 4 pomocí jiné metody než ta, kterou jste zadali v tomto kurzu. V takovém případě Zjistěte, jakou identitu používá fond aplikací přiřazený k aplikaci Contoso University, a udělte této identitě oprávnění k zápisu. Viz odkazy na identity fondu aplikací na konci tohoto kurzu.) V obou dialogových oknech klikněte na **OK** .

## <a name="retest-error-logging-and-reporting"></a>Přezkoušet protokolování chyb a vytváření sestav

Otestujte tak, že znovu zavedete chybu, a to tak, že vyžádáte špatnou adresu URL a spustíte stránku **protokolu chyb** . Tentokrát se chyba zobrazí na stránce.

![Stránka protokolu chyb knihovny ELMAH](setting-folder-permissions/_static/image4.png)

## <a name="summary"></a>Přehled

Nyní jste dokončili všechny úlohy, které jsou potřebné k zajištění správného fungování společnosti Contoso ve službě IIS na místním počítači. V dalším kurzu zpřístupníte web veřejně k dispozici tím, že ho nasadíte do Azure.

## <a name="more-information"></a>Další informace

V tomto příkladu je důvod, proč knihovny elmah nemohl uložit soubory protokolu, byl poměrně zřejmý. Trasování služby IIS můžete použít v případech, kdy příčina problému není tak zřejmá; Přečtěte si téma [řešení potíží s neúspěšnými žádostmi pomocí trasování ve službě IIS 7](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) na webu IIS.NET.

Další informace o tom, jak udělit oprávnění identitám fondu aplikací, najdete v tématu [identity fondu aplikací](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) a [zabezpečený obsah ve službě IIS prostřednictvím seznamů ACL pro systém souborů](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) na webu IIS.NET.

> [!div class="step-by-step"]
> [Předchozí](deploying-to-iis.md)
> [Další](deploying-to-production.md)
