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
ms.openlocfilehash: 0e720b3e4c5d3b8f779afe3a6e2b47baa86eec4c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74592711"
---
# <a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a>Sestavování kapitol ke stažení pro kurzy EF 5 MVC 4

Od [Rick Anderson]((https://twitter.com/RickAndMSFT))

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio 2012. Informace o řadě kurzů najdete v [prvním kurzu v řadě](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

## <a name="building-the-chapter-downloads"></a>Stažení jednotlivých kapitol

1. Stáhněte a rozbalte soubor zip s ukázkovým projektem. V balíčku pro stažení souborů k extrahování najdete další soubory zip, jednu pro dokončení každé kapitoly.
2. Klikněte pravým tlačítkem na požadovaný soubor zip, klikněte na **vlastnosti**a pak klikněte na tlačítko **odblokovat** .  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. Rozbalte soubor.
4. Dvojím kliknutím na soubor *CUx. sln* spustíte Visual Studio.
5. V nabídce **nástroje** klikněte na **Správce balíčků NuGet**a pak na **Konzola správce balíčků**.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. V konzole správce balíčků (PMC) klikněte na **obnovit**.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. Ukončete aplikaci Visual Studio.
8. Restartujte Visual Studio a otevřete soubor řešení, který jste uzavřeli v předchozím kroku.
9. V konzole správce balíčků (PMC) zadejte příkaz `Update-Database`:  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > Pokud se zobrazí následující chyba:  
    >   
    >  *Termín "aktualizace databáze" nebyl rozpoznán jako název rutiny, funkce, souboru skriptu nebo spustitelného programu. Zkontrolujte pravopis názvu, nebo pokud byla vložena cesta, ověřte, zda je cesta správná, a akci opakujte.*  
    > Ukončete a restartujte Visual Studio.

    Každá migrace se spustí a pak se spustí metoda počáteční hodnoty. Teď můžete aplikaci spustit.

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> [Předchozí](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
