---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 'Nasazení webu ASP.NET pomocí sady Visual Studio: nasazení příkazového řádku | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která bude Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13cfe4492398b59f2c80394689cc113ccb218c60
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78630919"
---
# <a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a>Nasazení webu ASP.NET pomocí sady Visual Studio: nasazení z příkazového řádku

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která umožňuje Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí sady Visual Studio 2012 nebo Visual Studio 2010. Informace o řadě najdete v [prvním kurzu v řadě](introduction.md).

## <a name="overview"></a>Přehled

V tomto kurzu se dozvíte, jak vyvolat kanál publikování webu sady Visual Studio z příkazového řádku. To je užitečné ve scénářích, kde chcete [automatizovat proces nasazení](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) místo ručního provedení v aplikaci Visual Studio, obvykle pomocí [systému správy verzí zdrojového kódu](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md).

## <a name="make-a-change-to-deploy"></a>Provedení změny nasazení

V současné době stránka o produktu zobrazuje kód šablony.

![Stránka s kódem šablony](command-line-deployment/_static/image1.png)

Nahradíte ho kódem, který zobrazuje souhrn registrace studenta.

Otevřete stránku *About. aspx* , odstraňte všechny značky uvnitř elementu `MainContent` `Content` a vložte následující kód do svého umístění:

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

Spusťte projekt a vyberte stránku **o produktu** .

![O stránce](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a>Nasazení na test pomocí příkazového řádku

Nebudete nasazovat jinou změnu databáze, takže zakážete nasazení databáze dbDacFx pro databázi ASPNET-ContosoUniversity. Otevřete Průvodce **publikováním webu** a v každém ze tří profilů publikování zrušte zaškrtnutí políčka **aktualizovat databázi** na kartě **Nastavení** .

Na úvodní stránce Windows 8 vyhledejte **Developer Command Prompt pro VS2012**.

Klikněte pravým tlačítkem na ikonu **Developer Command Prompt pro VS2012** a klikněte na **Spustit jako správce**.

Na příkazovém řádku zadejte následující příkaz, který nahradí cestu k souboru řešení cestou k souboru řešení:

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

Nástroj MSBuild sestaví řešení a nasadí ho do testovacího prostředí.

![Výstup příkazového řádku](command-line-deployment/_static/image3.png)

Otevřete prohlížeč a přejděte na `http://localhost/ContosoUniversity`a kliknutím na stránku **o** ověřte, že nasazení proběhlo úspěšně.

Pokud jste nevytvořili žádné studenty v testu, zobrazí se v záhlaví **Statistika těla studenta** prázdná stránka. Přejděte na stránku **Students** , klikněte na **Přidat studenta**a přidejte nějaké studenty a pak se vraťte na stránku **o produktu** a podívejte se na téma o statistice studenta.

![O stránce v testovacím prostředí](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a>Možnosti příkazového řádku pro klávesu

Příkaz, který jste zadali, předali cestu k souboru řešení a dvěma vlastnostem na MSBuild:

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a>Nasazení řešení vs. nasazení jednotlivých projektů

Zadáním souboru řešení dojde k sestavení všech projektů v tomto řešení. Pokud máte v řešení více webových projektů, platí následující chování nástroje MSBuild:

- Vlastnosti, které zadáte v příkazovém řádku, jsou předány do každého projektu. Proto každý webový projekt musí mít profil publikování s názvem, který zadáte. Zadáte-li `/p:PublishProfile=Test`, musí mít každý webový projekt profil publikování s názvem *test*.
- Jeden projekt může být úspěšně publikován, i když jiný není sestaven. Další informace naleznete v tématu StackOverflow vlákno [MSBuild se nezdařila se dvěma balíčky](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages).

Pokud zadáte samostatný projekt namísto řešení, je nutné přidat parametr, který určuje verzi sady Visual Studio. Pokud používáte Visual Studio 2012, příkazový řádek by byl podobný následujícímu příkladu:

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

Číslo verze sady Visual Studio 2010 je 10,0. Další informace najdete v tématu [Kompatibilita projektů v aplikaci Visual Studio a VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) na blogu Sayed Hashimi.

### <a name="specifying-the-publish-profile"></a>Zadání profilu publikování

Můžete zadat profil publikování podle názvu nebo úplnou cestou k souboru *. pubxml* , jak je znázorněno v následujícím příkladu:

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a>Metody publikování na webu podporované pro publikování z příkazového řádku

Pro publikování na příkazovém řádku jsou podporované tři metody publikování:

- `MSDeploy` – publikování pomocí Nasazení webu.
- `Package` – publikování vytvořením balíčku Nasazení webu. Balíček je nutné nainstalovat samostatně z příkazu MSBuild, který ho vytvoří.
- `FileSystem` – publikování kopírováním souborů do zadané složky.

### <a name="specifying-the-build-configuration-and-platform"></a>Zadání konfigurace sestavení a platformy

Konfigurace sestavení a platforma musí být nastavená v sadě Visual Studio nebo na příkazovém řádku. Profily publikování zahrnují vlastnosti, které jsou pojmenovány `LastUsedBuildConfiguration` a `LastUsedPlatform`, ale tyto vlastnosti nelze nastavit, aby bylo možné určit, jak je projekt sestaven. Další informace najdete v tématu [MSBuild: jak nastavit vlastnost konfigurace](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) na blogu Sayed Hashimi.

## <a name="deploy-to-staging"></a>Nasazení do přípravného prostředí

K nasazení do Azure je nutné přidat heslo do příkazového řádku. Pokud jste heslo uložili v profilu publikování v aplikaci Visual Studio, bylo uloženo v šifrované podobě v souboru *. pubxml. User* . Tento soubor není nástrojem MSBuild k dispozici při nasazení příkazového řádku, takže je nutné předat heslo v parametru příkazového řádku.

1. Zkopírujte heslo, které potřebujete, ze souboru *. publishsettings* , který jste si stáhli dříve pro pracovní web. Heslo je hodnota atributu `userPWD` prvku Nasazení webu `publishProfile`.

    ![Nasazení webu heslo](command-line-deployment/_static/image5.png)
2. Na úvodní stránce Windows 8 vyhledejte **Developer Command Prompt pro VS2012**a kliknutím na ikonu otevřete příkazový řádek. (Nemusíte ho otevírat jako správce, protože neprovádíte nasazení do služby IIS v místním počítači.)
3. Na příkazovém řádku zadejte následující příkaz, který nahradí cestu k souboru řešení cestou k souboru řešení a heslo s vaším heslem:

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    Všimněte si, že tento příkazový řádek obsahuje další parametr: `/p:AllowUntrustedCertificate=true`. Při psaní tohoto kurzu musí být vlastnost `AllowUntrustedCertificate` nastavena při publikování do Azure z příkazového řádku. Po vydání opravy pro tuto chybu nebudete potřebovat parametr.
4. Otevřete prohlížeč a přejděte na adresu URL vašeho přípravného webu a kliknutím na stránku **o** ověřte, že nasazení proběhlo úspěšně.

    Jak jste viděli dříve pro testovací prostředí, možná budete muset vytvořit nějaké studenty, aby viděli statistiku na stránce **o produktu** .

## <a name="deploy-to-production"></a>Nasazení do produkčního prostředí

Proces pro nasazení do produkčního prostředí je podobný procesu pro přípravu.

1. Zkopírujte heslo, které potřebujete, ze souboru *. publishsettings* , který jste si stáhli dříve pro produkční Web.
2. Otevřete **Developer Command Prompt pro VS2012**.
3. Na příkazovém řádku zadejte následující příkaz, který nahradí cestu k souboru řešení cestou k souboru řešení a heslo s vaším heslem:

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    V případě skutečného produkčního webu, pokud došlo ke změně databáze, byste obvykle zkopírovali *aplikaci\_offline souboru. htm* do lokality před nasazením a po úspěšném nasazení ho odstraníte.
4. Otevřete prohlížeč a přejděte na adresu URL vašeho přípravného webu a kliknutím na stránku **o** ověřte, že nasazení proběhlo úspěšně.

## <a name="summary"></a>Souhrn

Nyní jste nasadili aktualizaci aplikace pomocí příkazového řádku.

![O stránce v testovacím prostředí](command-line-deployment/_static/image6.png)

V dalším kurzu se zobrazí příklad rozšiřování kanálu publikování na webu. V tomto příkladu se dozvíte, jak nasadit soubory, které nejsou zahrnuty v projektu.

> [!div class="step-by-step"]
> [Předchozí](deploying-a-database-update.md)
> [Další](deploying-extra-files.md)
