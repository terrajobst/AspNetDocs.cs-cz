---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 'Nasazení webové aplikace SQL Server Compact v ASP.NET s využitím sady Visual Studio nebo Visual Web Developer: nasazení aktualizace pouze kódu – 8 z 12 | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: e4d094ef84a747c36ce05ddb0e3d1ce0391d5605
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74572719"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a>Nasazení webové aplikace v ASP.NET pomocí SQL Server Compact sady Visual Studio nebo Visual Web Developer: nasazení aktualizace pouze kódu – 8 z 12

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Studio 2012 RC nebo Visual Studio Express 2012 RC pro web. Můžete také použít Visual Studio 2010, pokud nainstalujete aktualizaci publikování na webu. Úvod k řadě najdete v [prvním kurzu v řadě](deployment-to-a-hosting-provider-introduction-1-of-12.md).
> 
> Kurz, který ukazuje funkce nasazení představené po vydání RC sady Visual Studio 2012, ukazuje, jak nasadit SQL Server edice jiné než SQL Server Compact a ukazuje, jak nasadit na Azure App Service Web Apps, v tématu [nasazení webu ASP.NET pomocí sady Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Přehled

Po počátečním nasazení bude vaše práce s údržbou a vývojem webu pokračovat a ještě dlouho budete chtít nasadit aktualizaci. Tento kurz vás provede procesem nasazení aktualizace kódu vaší aplikace. Tato aktualizace nezahrnuje změnu databáze. v dalším kurzu se dozvíte, jaké jsou různé informace o nasazení změny databáze.

Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje při procházení tohoto kurzu, zkontrolujte [stránku řešení potíží](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).

## <a name="making-a-code-change"></a>Provedení změny kódu

Jako jednoduchý příklad aktualizace aplikace přidáváte na stránku **instruktoři** seznam kurzů, které probral vybraný instruktor.

Pokud spouštíte stránku **instruktory** , všimnete si, že v mřížce jsou **vybrané** odkazy, ale nedělají nic jiného, než když se pozadí řádku změní na šedé.

[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)

Nyní přidáte kód, který se spustí, když se klikne na odkaz **Select** , a zobrazí se seznam kurzů, které prochází vybraným instruktorem.

V *instruktors. aspx*přidejte následující kód hned za ovládací prvek **ErrorMessageLabel** `Label`:

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

Spusťte stránku a vyberte instruktor. Zobrazí se seznam výukových kurzů, které tento instruktor projedná.

[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)

## <a name="deploying-the-code-update-to-the-test-environment"></a>Nasazení aktualizace kódu do testovacího prostředí

Nasazení do testovacího prostředí je jednoduché pro opětovné spuštění publikování jedním kliknutím. Chcete-li tento proces urychlit, můžete použít panel nástrojů pro **publikování webu jedním kliknutím** .

V nabídce **zobrazení** zvolte **panely nástrojů** a pak vyberte **možnost publikovat na webu jedním kliknutím**.

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

V **Průzkumník řešení**vyberte projekt ContosoUniversity.

panel nástrojů pro **publikování webu jedním kliknutím** vyberte profil publikování **testu** a pak klikněte na **Publikovat web** (ikona se šipkami ukazující vlevo a vpravo).

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

Visual Studio nasadí aktualizovanou aplikaci a prohlížeč se automaticky otevře na domovské stránce. Spusťte stránku instruktoři a vyberte instruktora, abyste ověřili, že byla aktualizace úspěšně nasazena.

[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)

Obvykle byste také provedli regresní testování (to znamená otestovat zbytek lokality, abyste se ujistili, že nová změna nepřerušila všechny stávající funkce). Pro tento kurz ale tento krok přeskočíte a pokračujte v nasazení aktualizace do produkčního prostředí.

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a>Prevence opětovného nasazení počátečního stavu databáze do produkčního prostředí

V reálné aplikaci uživatelé při počátečním nasazení komunikují s produkčním webem a databáze se naplní živými daty. Proto nebudete chtít znovu nasadit databázi členství v původním stavu, což by mělo vymazat všechna živá data. Vzhledem k tomu, že databáze SQL Server Compact jsou soubory ve složce *App\_data* , je nutné zabránit tomu tím, že změníte nastavení nasazení tak, aby soubory ve složce *aplikace\_data* nebyly nasazeny.

Otevřete okno **Vlastnosti projektu** pro projekt ContosoUniversity a vyberte kartu **balíček/publikovat web** . Ujistěte se, že je rozevírací seznam **Konfigurace** buď **aktivní (vydaná verze)** , nebo **vydaná verze** , vyberte možnost **vyloučit soubory ze složky App\_data**.

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

V případě, že se rozhodnete nasadit sestavení pro ladění v budoucnu, je vhodné provést stejnou změnu konfigurace sestavení ladění: změnit **konfiguraci** pro **ladění** a pak vybrat **vyloučit soubory ze složky App\_data**.

Uložte a zavřete kartu **balíček/publikovat web** .

> [!NOTE] 
> 
> [!IMPORTANT]
> Ujistěte se, že v profilech publikování není vybraná možnost **odebrat další soubory v cílovém umístění** . Vyberete-li tuto možnost, proces nasazení odstraní databáze, které máte v aplikaci\_data v nasazeném webu, a odstraní složku aplikace\_data.

## <a name="preventing-user-access-to-the-production-site-during-update"></a>Brání uživateli v průběhu aktualizace přístup k produkčnímu webu.

Změna, kterou právě nasazujete, je jednoduchá změna na jednu stránku. Někdy ale nasadíte větší změny a v takovém případě se lokalita může chovat nezvyklě, pokud uživatel požádá o stránku před dokončením nasazení. Abyste tomu předešli, můžete použít *aplikaci\_offline souboru. htm* . Když umístíte soubor s názvem *app\_v režimu offline. htm* do kořenové složky vaší aplikace, služba IIS automaticky zobrazí tento soubor místo spuštění aplikace. Takže pokud chcete během nasazování zabránit v přístupu, vložte *aplikaci\_do režimu offline. htm* v kořenové složce, spusťte proces nasazení a pak *\_offline. htm*odeberte aplikaci.

V **Průzkumník řešení**klikněte pravým tlačítkem na řešení (ne na jeden z projektů) a vyberte **Nová složka řešení**.

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

Pojmenujte složku *SolutionFiles*.

V nové složce vytvořte stránku HTML s názvem *app\_offline. htm*. Existující obsah nahraďte následujícím kódem:

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

Aplikaci můžete zkopírovat *\_offline souboru. htm* do lokality pomocí připojení FTP nebo nástroje **Správce souborů** v ovládacím panelu poskytovatele hostingu. V tomto kurzu použijete **Správce souborů**.

Otevřete ovládací panely a v kurzu [nasazení do provozního prostředí](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) vyberte **Správce souborů** . Vyberte **contosouniversity.com** a potom **wwwroot** , abyste se dostali do kořenové složky vaší aplikace, a pak klikněte na **nahrát**.

[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)

V dialogovém okně **nahrát soubor** vyberte *aplikaci\_offline. htm* a pak klikněte na **nahrát**.

[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)

Přejděte na adresu URL vašeho webu. Uvidíte, že se teď místo domovské stránky zobrazuje stránka *aplikace\_offline. htm* .

[![App_offline. htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)

Teď můžete začít s nasazením do produkčního prostředí.

## <a name="deploying-the-code-update-to-the-production-environment"></a>Nasazení aktualizace kódu do provozního prostředí

Na panelu nástrojů **publikování webu jedním kliknutím** vyberte profil publikování v **produkci** a pak klikněte na **Publikovat web**.

Visual Studio nasadí aktualizovanou aplikaci a otevře prohlížeč na domovské stránce webu. Zobrazí se soubor *\_offline. htm aplikace* . Než budete moct otestovat ověření úspěšného nasazení, musíte *aplikaci odebrat\_offline souboru. htm* .

Vraťte se do aplikace **Správce souborů** v Ovládacích panelech. Vyberte **contosouniversity.com** a **wwwroot**, vyberte **aplikace\_offline. htm**a pak klikněte na **Odstranit**.

[![Deleting_app_offline. htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)

V prohlížeči otevřete stránku instruktoři ve veřejné lokalitě a vyberte instruktora, abyste ověřili, že byla aktualizace úspěšně nasazena.

[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)

Nyní jste nasadili aktualizaci aplikace, která nezahrnuje změnu databáze. V dalším kurzu se dozvíte, jak nasadit změnu databáze.

> [!div class="step-by-step"]
> [Předchozí](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [Další](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
