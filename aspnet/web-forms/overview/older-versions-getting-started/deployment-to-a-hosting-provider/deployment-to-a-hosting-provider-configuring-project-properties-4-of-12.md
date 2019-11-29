---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-configuring-project-properties-4-of-12
title: 'Nasazení webové aplikace v ASP.NET pomocí SQL Server Compact sady Visual Studio nebo Visual Web Developer: Konfigurace vlastností projektu – 4 z 12 | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 8b013630-842c-4d44-a6fc-c6be43e7210f
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-configuring-project-properties-4-of-12
msc.type: authoredcontent
ms.openlocfilehash: 6e63e75dca3d776fb9a1bd7e420ef48891daac69
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74569810"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-configuring-project-properties---4-of-12"></a>Nasazení webové aplikace v ASP.NET pomocí SQL Server Compact sady Visual Studio nebo Visual Web Developer: Konfigurace vlastností projektu – 4 z 12

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Studio 2012 RC nebo Visual Studio Express 2012 RC pro web. Můžete také použít Visual Studio 2010, pokud nainstalujete aktualizaci publikování na webu. Úvod k řadě najdete v [prvním kurzu v řadě](deployment-to-a-hosting-provider-introduction-1-of-12.md).
> 
> Kurz, který ukazuje funkce nasazení představené po vydání RC sady Visual Studio 2012, ukazuje, jak nasadit SQL Server edice jiné než SQL Server Compact a ukazuje, jak nasadit na Azure App Service Web Apps, v tématu [nasazení webu ASP.NET pomocí sady Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Přehled

Některé možnosti nasazení jsou nakonfigurovány ve vlastnostech projektu, které jsou uloženy v souboru projektu (soubor *. csproj* nebo *. vbproj* ). Ve většině případů jsou výchozí hodnoty těchto nastavení vhodné, ale můžete použít **Vlastnosti projektu** integrované do sady Visual Studio pro práci s těmito nastaveními, pokud je třeba je změnit. V tomto kurzu si prohlédnete nastavení nasazení ve **vlastnostech projektu**. Také vytvoříte zástupný soubor, který způsobí nasazení prázdné složky.

## <a name="configuring-deployment-settings-in-the-project-properties-window"></a>Konfigurace nastavení nasazení v okně vlastností projektu

Většina nastavení, která mají vliv na to, co se stane během nasazení, jsou součástí profilu publikování, jak vidíte v následujících kurzech. Několik nastavení, o kterých byste měli vědět, se nachází na kartách **balení a publikování** okna **vlastností projektu** . Tato nastavení jsou určena pro každou konfiguraci sestavení – to znamená, že můžete mít různá nastavení pro sestavení pro vydání, než pro sestavení pro ladění.

V **Průzkumník řešení**klikněte pravým tlačítkem na projekt **ContosoUniversity** , vyberte **vlastnosti**a pak vyberte kartu **balíček/publikovat web** .

![Package_Publish_Web_tab](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image1.png)

Po zobrazení okna se ve výchozím nastavení zobrazí nastavení pro každou konfiguraci sestavení, která je pro toto řešení aktuálně aktivní. Pokud pole **Konfigurace** neuvádí možnost **aktivní (vydání)** , vyberte **verze** , aby se zobrazila nastavení pro konfiguraci sestavení pro vydání. Nasadíte sestavení vydaných verzí do testovacího i produkčního prostředí.

![Package_Publish_Web_tab_selecting_Release](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image2.png)

Když vyberete možnost **aktivní (vydaná verze)** nebo **vydaná verze** , zobrazí se hodnoty, které jsou platné při nasazení pomocí konfigurace sestavení verze:

- V poli **položky k nasazení** se vybere **pouze soubory potřebné ke spuštění aplikace** . Další možnosti jsou **všechny soubory v tomto projektu** nebo **všechny soubory v této složce projektu**. Když necháte výchozí výběr beze změny, nebudete například nasazovat soubory zdrojového kódu. Toto nastavení je důvod, proč se složky obsahující SQL Server Compact binární soubory měly zahrnout do projektu. Další informace o tomto nastavení najdete v tématu **Proč se nepovedlo nasadit všechny soubory ve složce projektu?** v tématu [Nejčastější dotazy k nasazení projektu webové aplikace ASP.NET](https://msdn.microsoft.com/library/ee942158.aspx).
- Je vybraná možnost **vyloučit vygenerované symboly ladění** . Při použití této konfigurace sestavení nebudete ladit.
- Nevybrali jste možnost **vyloučit soubory ze složky App\_data** . Soubor SQL Server Compact pro databázi členství je v této složce a je nutné ji nasadit. Když nasadíte aktualizace, které neobsahují změny v databázi, zaškrtnete toto políčko.
- **Před publikováním tuto aplikaci předem zkompilujte** . Ve většině scénářů není nutné předem kompilovat projekty webových aplikací. Další informace o této možnosti najdete v dialogovém okně [Balení/publikování webu, vlastnosti projektu](https://msdn.microsoft.com/library/dd410108(v=vs.110).aspx) a [Rozšířené nastavení předkompilace](https://msdn.microsoft.com/library/hh475319(v=vs.110).aspx).
- Je vybraná možnost **Zahrnout všechny databáze nakonfigurované na kartě Balení/publikování SQL** , ale tato možnost nemá žádný vliv, protože nekonfigurujete kartu **Package/Publish SQL** . Tato karta je určena pro starší metodu nasazení databáze, která se používá jako jediná možnost pro nasazení SQL Serverch databází. V kurzu [migrace do SQL Server](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md) použijete kartu **Package/Publish SQL** .
- Oddíl **nastavení balíčku pro nasazení webu** neplatí, protože v těchto kurzech používáte publikování jedním kliknutím.

Změnou rozevíracího seznamu **Konfigurace** na ladit zobrazíte výchozí nastavení pro sestavení pro ladění. Hodnoty jsou stejné, s výjimkou **vyloučených vygenerovaných symbolů ladění** je vymazáno, aby bylo možné ladit při nasazení sestavení ladění.

## <a name="making-sure-that-the-elmah-folder-gets-deployed"></a>Zajištění nasazení složky knihovny elmah

Jak jste viděli v předchozím kurzu, [balíček NuGet knihovny elmah](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) poskytuje funkce pro protokolování chyb a vytváření sestav. Ve složce s názvem *knihovny elmah*je v aplikaci Contoso University knihovny elmah nakonfigurovaná tak, aby ukládala podrobnosti o chybách:

![Knihovny elmah složka](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image3.png)

Běžným požadavkem je vyloučení určitých souborů nebo složek z nasazení. Dalším příkladem může být složka, do které můžou uživatelé nahrávat soubory. Nechcete nasadit soubory protokolu ani nahrané soubory, které byly vytvořeny ve vašem vývojovém prostředí, do produkčního prostředí. A pokud nasazujete aktualizaci do produkčního prostředí, nechcete, aby proces nasazení odstranil soubory, které existují v produkčním prostředí. (V závislosti na nastavení možnosti nasazení, pokud soubor existuje v cílové lokalitě, ale ne ve zdrojové lokalitě při nasazení, Nasazení webu ho odstraní z cílového umístění.)

Jak jste viděli dříve v tomto kurzu, možnost **položky k nasazení** na kartě **balení nebo publikování webu** je nastavena **pouze na soubory potřebné ke spuštění této aplikace**. V důsledku toho nebudou nasazeny soubory protokolu vytvořené nástrojem knihovny elmah ve vývoji, což je to, co chcete udělat. (Aby bylo možné je nasadit, museli by být zahrnuti do projektu a vlastnost **Akce sestavení** by musel být nastavena na **obsah**. Další informace najdete v tématu **Proč se nepovedlo nasadit všechny soubory ve složce projektu?** v tématu [Nejčastější dotazy k nasazení projektu webové aplikace ASP.NET](https://msdn.microsoft.com/library/ee942158.aspx). Nasazení webu však nevytvoří složku v cílové lokalitě, pokud k ní není k dispozici alespoň jeden soubor. Proto do složky přidáte soubor *. txt* , který bude fungovat jako zástupný symbol, aby se složka zkopírovala.

V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku *knihovny elmah* , vyberte možnost **Přidat novou položku**a vytvořte soubor s názvem *zástupný text. txt*. Vložte do něj následující text: "Jedná se o zástupný soubor, aby bylo zajištěno, že se složka bude nasazovat". a uložte soubor. To je všechno, co musíte udělat, aby se zajistilo, že Visual Studio nasadí tento soubor a složku, ve které je, protože vlastnost **Akce sestavení** souborů *. txt* je ve výchozím nastavení nastavená na **obsah** .

Nyní jste dokončili všechny úlohy nastavování nasazení. V dalším kurzu nasadíte web společnosti Contoso University do testovacího prostředí a otestujete ho.

> [!div class="step-by-step"]
> [Předchozí](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
> [Další](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)
