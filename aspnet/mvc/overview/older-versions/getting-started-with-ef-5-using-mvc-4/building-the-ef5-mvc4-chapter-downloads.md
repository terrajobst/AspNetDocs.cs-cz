---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
title: Sestavování kapitol ke stažení pro kurzy EF 5 MVC 4 | Microsoft Docs
author: Rick-Anderson
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: d0a89089-eed8-4f61-a478-c5ffa30186f5
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
msc.type: authoredcontent
ms.openlocfilehash: 10237af40e3914b65e5181f17555697e86adea4b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457853"
---
# <a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a><span data-ttu-id="82f2e-103">Sestavování kapitol ke stažení pro kurzy EF 5 MVC 4</span><span class="sxs-lookup"><span data-stu-id="82f2e-103">Building the Chapter Downloads for the EF 5 MVC 4 Tutorials</span></span>

<span data-ttu-id="82f2e-104">od [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="82f2e-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[<span data-ttu-id="82f2e-105">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="82f2e-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="82f2e-106">Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="82f2e-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="82f2e-107">Informace o řadě kurzů najdete v [prvním kurzu v řadě](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="82f2e-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

## <a name="building-the-chapter-downloads"></a><span data-ttu-id="82f2e-108">Stažení jednotlivých kapitol</span><span class="sxs-lookup"><span data-stu-id="82f2e-108">Building the Chapter Downloads</span></span>

1. <span data-ttu-id="82f2e-109">Stáhněte a rozbalte soubor zip s ukázkovým projektem.</span><span class="sxs-lookup"><span data-stu-id="82f2e-109">Download and unzip the  project sample zip file.</span></span> <span data-ttu-id="82f2e-110">V balíčku pro stažení souborů k extrahování najdete další soubory zip, jednu pro dokončení každé kapitoly.</span><span class="sxs-lookup"><span data-stu-id="82f2e-110">In the unzipped download package, you will find additional zip files, one for the completion of each chapter.</span></span>
2. <span data-ttu-id="82f2e-111">Klikněte pravým tlačítkem na požadovaný soubor zip, klikněte na **vlastnosti**a pak klikněte na tlačítko **odblokovat** .</span><span class="sxs-lookup"><span data-stu-id="82f2e-111">Right click on the desired zip file, click **Properties**, and click the **Unblock** button.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. <span data-ttu-id="82f2e-112">Rozbalte soubor.</span><span class="sxs-lookup"><span data-stu-id="82f2e-112">Unzip the file.</span></span>
4. <span data-ttu-id="82f2e-113">Dvojím kliknutím na soubor *CUx. sln* spustíte Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82f2e-113">Double-click the *CUx.sln* file to launch Visual Studio.</span></span>
5. <span data-ttu-id="82f2e-114">V nabídce **nástroje** klikněte na **Správce balíčků NuGet**a pak na **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="82f2e-114">From the **Tools** menu, click **NuGet Package Manager**, then **Package Manager Console**.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. <span data-ttu-id="82f2e-115">V konzole správce balíčků (PMC) klikněte na **obnovit**.</span><span class="sxs-lookup"><span data-stu-id="82f2e-115">In the Package Manager Console (PMC), click **Restore**.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. <span data-ttu-id="82f2e-116">Ukončete aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82f2e-116">Exit Visual Studio.</span></span>
8. <span data-ttu-id="82f2e-117">Restartujte Visual Studio a otevřete soubor řešení, který jste uzavřeli v předchozím kroku.</span><span class="sxs-lookup"><span data-stu-id="82f2e-117">Restart Visual Studio, opening the solution file you closed in the step above.</span></span>
9. <span data-ttu-id="82f2e-118">V konzole správce balíčků (PMC) zadejte příkaz `Update-Database`:</span><span class="sxs-lookup"><span data-stu-id="82f2e-118">In the Package Manager Console (PMC), enter the `Update-Database` command:</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > <span data-ttu-id="82f2e-119">Pokud se zobrazí následující chyba:</span><span class="sxs-lookup"><span data-stu-id="82f2e-119">If you get the following error:</span></span>  
    >   
    >  <span data-ttu-id="82f2e-120">*Termín "aktualizace databáze" nebyl rozpoznán jako název rutiny, funkce, souboru skriptu nebo spustitelného programu. Zkontrolujte pravopis názvu, nebo pokud byla vložena cesta, ověřte, zda je cesta správná, a akci opakujte.*</span><span class="sxs-lookup"><span data-stu-id="82f2e-120">*The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.*</span></span>  
    > <span data-ttu-id="82f2e-121">Ukončete a restartujte Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82f2e-121">Exit and restart Visual Studio.</span></span>

    <span data-ttu-id="82f2e-122">Každá migrace se spustí a pak se spustí metoda počáteční hodnoty.</span><span class="sxs-lookup"><span data-stu-id="82f2e-122">Each migration will run, then the seed method will run.</span></span> <span data-ttu-id="82f2e-123">Teď můžete aplikaci spustit.</span><span class="sxs-lookup"><span data-stu-id="82f2e-123">You can now run the app.</span></span>

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> [<span data-ttu-id="82f2e-124">Předchozí</span><span class="sxs-lookup"><span data-stu-id="82f2e-124">Previous</span></span>](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
