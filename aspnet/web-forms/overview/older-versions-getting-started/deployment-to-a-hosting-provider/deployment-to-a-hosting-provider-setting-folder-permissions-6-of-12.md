---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12
title: 'Nasazení webové aplikace v ASP.NET pomocí SQL Server Compact sady Visual Studio nebo Visual Web Developer: nastavení oprávnění složky – 6 z 12 | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: cd03a188-e947-4f55-9bda-b8bce201d8c6
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12
msc.type: authoredcontent
ms.openlocfilehash: 85a77a196cf3458bbb2e6308838a846936cd070b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74633535"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-setting-folder-permissions---6-of-12"></a>Nasazení webové aplikace v ASP.NET pomocí SQL Server Compact sady Visual Studio nebo Visual Web Developer: nastavení oprávnění složky – 6 z 12

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Studio 2012 RC nebo Visual Studio Express 2012 RC pro web. Můžete také použít Visual Studio 2010, pokud nainstalujete aktualizaci publikování na webu. Úvod k řadě najdete v [prvním kurzu v řadě](deployment-to-a-hosting-provider-introduction-1-of-12.md).
> 
> Kurz, který ukazuje funkce nasazení představené po vydání RC sady Visual Studio 2012, ukazuje, jak nasadit SQL Server edice jiné než SQL Server Compact a ukazuje, jak nasadit na Azure App Service Web Apps, v tématu [nasazení webu ASP.NET pomocí sady Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Přehled

V tomto kurzu nastavíte oprávnění složky pro složku *knihovny elmah* na nasazeném webu tak, aby aplikace mohla v této složce vytvářet soubory protokolů.

Při testování webové aplikace v aplikaci Visual Studio pomocí vývojového serveru sady Visual Studio (Cassini) se aplikace spustí v rámci vaší identity. Pravděpodobně jste správcem vašeho vývojového počítače a máte plnou autoritu, abyste mohli cokoli dělat s jakýmkoli souborem v jakékoli složce. V případě, že je aplikace spuštěna v rámci služby IIS, je spuštěna pod identitou definovanou pro fond aplikací, ke kterému je lokalita přiřazena. Obvykle se jedná o účet definovaný systémem, který má omezená oprávnění. Ve výchozím nastavení má oprávnění číst a spustit pro soubory a složky webové aplikace, ale nemá přístup pro zápis.

Dojde k problému, pokud vaše aplikace vytvoří nebo aktualizuje soubory, což je běžné nutnost ve webových aplikacích. V aplikaci Contoso University knihovny elmah vytvoří ve složce *knihovny elmah* soubory XML, aby se uložily podrobnosti o chybách. I když nepoužíváte něco jako knihovny elmah, může váš web umožnit uživatelům nahrávat soubory nebo provádět jiné úkoly, které zapisují data do složky ve vaší lokalitě.

Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje při procházení tohoto kurzu, zkontrolujte [stránku řešení potíží](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).

## <a name="testing-error-logging-and-reporting"></a>Testování protokolování chyb a vytváření sestav

Chcete-li zjistit, jak aplikace nefunguje správně ve službě IIS (i když to bylo při testování v aplikaci Visual Studio), můžete způsobit chybu, která by normálně byla protokolována nástrojem knihovny elmah, a potom otevřít protokol chyb knihovny elmah a zobrazit podrobnosti. Pokud knihovny elmah nemohl vytvořit soubor XML a uložit podrobnosti o chybě, zobrazí se prázdná zpráva o chybě.

Otevřete prohlížeč a klikněte na `http://localhost/ContosoUniversity`a pak si vyžádejte neplatnou adresu URL, jako je *Studentsxxx. aspx*. Namísto stránky *GenericErrorPage. aspx* se zobrazí systémem generovaná chybová stránka, protože nastavení `customErrors` v souboru Web. config je "remoteonly" a místní služba IIS je spuštěna:

[![Error_page_Test](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image2.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image1.png)

Nyní spusťte *knihovny elmah. axd* , aby se zobrazila zpráva o chybách. Zobrazí se prázdná stránka protokolu chyb, protože knihovny elmah se nepovedlo vytvořit soubor XML ve složce *knihovny elmah* :

[![Error_log_page_empty](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image4.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image3.png)

## <a name="setting-write-permission-on-the-elmah-folder"></a>Nastavení oprávnění k zápisu ve složce knihovny elmah

Oprávnění ke složkám můžete nastavit ručně nebo ji můžete nastavit jako automatickou součást procesu nasazení. Díky tomu, že automatické vyžaduje komplexní kód MSBuild a protože je potřeba to udělat jenom při prvním nasazení, tento kurz ukazuje, jak to provést ručně. (Informace o tom, jak provést tuto část procesu nasazení, najdete v tématu [Nastavení oprávnění složky na webu publikování](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) na blogu Sayed Hashimi.)

V **Průzkumníku Windows**přejděte na *C:\inetpub\wwwroot\ContosoUniversity*. Klikněte pravým tlačítkem na složku *knihovny elmah* , vyberte **vlastnosti**a pak vyberte kartu **zabezpečení** .

[![Elmah_folder_Properties_Security_tab](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image6.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image5.png)

(Pokud v seznamu **název skupiny nebo jméno uživatele** nevidíte **DefaultAppPool** , pravděpodobně jste v tomto kurzu nastavili službu IIS a ASP.NET 4 pomocí jiné metody než ta, kterou jste zadali v tomto kurzu. V takovém případě Zjistěte, jakou identitu používá fond aplikací přiřazený k aplikaci Contoso University, a udělte této identitě oprávnění k zápisu. Viz odkazy na identity fondu aplikací na konci tohoto kurzu.)

Klikněte na **Upravit**. V dialogovém okně **oprávnění pro knihovny elmah** vyberte **DefaultAppPool**a potom zaškrtněte políčko **zapsat** ve sloupci **povoleno** .

[![Permissions_for_Elmah_dialog_box](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image8.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image7.png)

V obou dialogových oknech klikněte na **OK** .

## <a name="retesting-error-logging-and-reporting"></a>Přezkoušení protokolování chyb a vytváření sestav

Otestujte tak, že znovu zavedete chybu, a to tak, že vyžádáte špatnou adresu URL a spustíte stránku **protokolu chyb** . Tentokrát se chyba zobrazí na stránce.

[![Elmah_Error_Log_page_Test](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image10.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image9.png)

Také budete potřebovat oprávnění k zápisu do složky *Data\_aplikace* , protože v této složce máte SQL Server Compact soubory databáze a chcete být schopni aktualizovat data v těchto databázích. V takovém případě však nemusíte nic dalšího dělat, protože proces nasazení automaticky nastaví oprávnění k zápisu do složky *\_dat aplikace* .

Nyní jste dokončili všechny úlohy, které jsou potřebné k zajištění správného fungování společnosti Contoso ve službě IIS na místním počítači. V dalším kurzu zpřístupníte web veřejně k dispozici tím, že ho nasadíte do poskytovatele hostingu.

## <a name="more-information"></a>Další informace

V tomto příkladu je důvod, proč knihovny elmah nemohl uložit soubory protokolu, byl poměrně zřejmý. Trasování služby IIS můžete použít v případech, kdy příčina problému není tak zřejmá; Přečtěte si téma [řešení potíží s neúspěšnými žádostmi pomocí trasování ve službě IIS 7](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) na webu IIS.NET.

Další informace o tom, jak udělit oprávnění identitám fondu aplikací, najdete v tématu [identity fondu aplikací](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) a [zabezpečený obsah ve službě IIS prostřednictvím seznamů ACL pro systém souborů](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) na webu IIS.NET.

> [!div class="step-by-step"]
> [Předchozí](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)
> [Další](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
