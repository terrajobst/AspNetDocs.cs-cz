---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
title: 'Nasazení webu ASP.NET pomocí sady Visual Studio: nasazování dalších souborů | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která bude Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí usin...
ms.author: riande
ms.date: 03/23/2015
ms.assetid: 1cd91055-84bc-42c6-9d80-646f41429d4d
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
msc.type: authoredcontent
ms.openlocfilehash: eaa3141c22980f0c816e2f33b5597ac9fe69c23c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548410"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-extra-files"></a>Nasazení webu ASP.NET pomocí sady Visual Studio: nasazení dalších souborů

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která umožňuje Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí sady Visual Studio 2012 nebo Visual Studio 2010. Informace o řadě najdete v [prvním kurzu v řadě](introduction.md).

## <a name="overview"></a>Přehled

V tomto kurzu se dozvíte, jak roztáhnout kanál publikování webu sady Visual Studio, aby během nasazení procházel další úkol. Úkolem je zkopírovat další soubory, které nejsou ve složce projektu, na cílový web.

V tomto kurzu zkopírujete jeden soubor navíc: *robots. txt*. Tento soubor chcete nasadit do přípravy, ale ne do produkčního prostředí. V kurzu [nasazení do produkčního](deploying-to-production.md) prostředí jste do projektu přidali tento soubor a nakonfigurovali do něj profil publikování v produkčním prostředí, abyste ho vyloučili. V tomto kurzu se zobrazí alternativní metoda pro zpracování této situace. ta, která bude užitečná pro všechny soubory, které chcete nasadit, ale nechcete je zahrnout do projektu.

## <a name="move-the-robotstxt-file"></a>Přesunout soubor robots. txt

K přípravě na jinou metodu zpracování souboru *robots. txt*v této části kurzu přesunete soubor do složky, která není obsažena v projektu, a odstraníte soubor *robots. txt* z přípravného prostředí. Je nutné odstranit soubor z přípravy, abyste si ověřili, že vaše nová metoda nasazení souboru do tohoto prostředí funguje správně.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na soubor *robots. txt* a klikněte na **vyloučit z projektu**.
2. Pomocí Průzkumníka souborů Windows vytvořte ve složce řešení novou složku a pojmenujte ji *ExtraFiles*.
3. Přesuňte soubor *robots. txt* ze složky projektu *ContosoUniversity* do složky *ExtraFiles* .

    ![ExtraFiles složka](deploying-extra-files/_static/image1.png)
4. Pomocí nástroje FTP odstraňte soubor *robots. txt* z přípravného webu.

    Alternativně můžete vybrat **odebrat další soubory v umístění** v části **Možnosti publikování souboru** na kartě **Nastavení** v profilu publikování a znovu publikovat do přípravy.

## <a name="update-the-publish-profile-file"></a>Aktualizace souboru profilu publikování

Soubor *robots. txt* potřebujete jenom v přípravě, takže jenom profil publikování, který je potřeba aktualizovat, aby ho bylo možné nasadit, je pracovní.

1. V aplikaci Visual Studio otevřete *přípravný. pubxml*.
2. Na konci souboru před uzavírací `</Project>`ovou značkou přidejte následující kód:

    [!code-xml[Main](deploying-extra-files/samples/sample1.xml)]

    Tento kód vytvoří nový *cíl* , který bude shromažďovat další soubory, které mají být nasazeny. Cíl se skládá z jedné nebo více úloh, které spustí nástroj MSBuild na základě podmínek, které zadáte.

    Atribut `Include` určuje, že složka, ve které se mají najít soubory, je *ExtraFiles*, která je umístěná na stejné úrovni jako složka projektu. Nástroj MSBuild bude shromažďovat všechny soubory z této složky a rekurzivně z jakékoli podsložky (dvojitá hvězdička určuje rekurzivní podsložky). Pomocí tohoto kódu můžete umístit více souborů a souborů do podsložek do složky *ExtraFiles* a všechny budou nasazeny.

    Element `DestinationRelativePath` určuje, že složky a soubory by měly být zkopírovány do kořenové složky cílového webu, ve stejném souboru a struktuře složek, které jsou umístěny ve složce *ExtraFiles* . Pokud jste chtěli zkopírovat samotnou složku *ExtraFiles* , hodnota `DestinationRelativePath` by byla *\%ExtraFiles (RecursiveDir)% (filename)% (přípona)* .
3. Na konci souboru před uzavírací `</Project>`ovou značkou přidejte následující kód, který určuje, kdy se má spustit nový cíl.

    [!code-xml[Main](deploying-extra-files/samples/sample2.xml)]

    Tento kód způsobí, že se nový `CustomCollectFiles` cíl spustí vždy, když se spustí cíl, který kopíruje soubory do cílové složky. Při vytváření balíčku pro publikování a nasazení došlo k samostatnému cíli a nový cíl se vloží do obou cílů pro případ, že se rozhodnete nasadit pomocí balíčku pro nasazení místo publikování.

    Soubor *. pubxml* se teď zdá jako v následujícím příkladu:

    [!code-xml[Main](deploying-extra-files/samples/sample3.xml?highlight=53-71)]
4. Uložte a zavřete soubor *staging. pubxml* .

## <a name="publish-to-staging"></a>Publikovat do přípravy

Pomocí publikování jedním kliknutím nebo příkazového řádku publikujte aplikaci pomocí pracovního profilu.

Pokud používáte publikování jedním kliknutím, můžete ověřit v okně **náhledu** , které budou zkopírovány *robot. txt* . V opačném případě pomocí nástroje FTP ověřte, zda je soubor *robots. txt* v kořenové složce webu po nasazení.

## <a name="summary"></a>Souhrn

Tím se dokončí Tato série kurzů pro nasazení webové aplikace v ASP.NET k poskytovateli hostingu třetí strany. Další informace o všech tématech popsaných v těchto kurzech najdete v tématu [Mapa obsahu nasazení ASP.NET](https://go.microsoft.com/fwlink/p/?LinkId=282413).

## <a name="more-information"></a>Další informace

Pokud víte, jak pracovat se soubory MSBuild, můžete automatizovat mnoho dalších úloh nasazení pomocí psaní kódu v souborech *. pubxml* (pro úlohy specifické pro profilování) nebo souboru Project *. WPP. targets* (pro úlohy, které platí pro všechny profily). Další informace o souborech *. pubxml* a *. WPP. targets* naleznete v tématu [How to: Edit settings Deployment in Publish profiles (. pubxml) files and the. WPP. targets in Visual Studio Web Projects](https://msdn.microsoft.com/library/ff398069). Základní informace o nástroji MSBuild Code najdete v části **anatomie souboru projektu** v [podnikovém nasazení série: principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md). Informace o tom, jak pracovat se soubory MSBuild pro provádění úloh pro vlastní scénáře, naleznete v této knize: [uvnitř Microsoft Build Engine: použití nástroje MSBuild a Team Foundation Build](http://msbuildbook.com) pomocí Sayed Ibraham Hashimi a William Bartholomew.

## <a name="acknowledgements"></a>Poděkování

Chci nás zasílat na následující lidi, kteří významně přispěli k obsahu této série kurzů:

- [Alberto Poblacion, MVP &amp; MCT, Španělsko](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- Jarod Ferguson, MVP pro vývoj datových platforem, USA
- Harsh Mittal, Microsoft
- [Jan Galloway](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))
- [Kristina Olson, Microsoft](https://blogs.iis.net/krolson/default.aspx)
- [Mike Pope, Microsoft](http://www.mikepope.com/blog/DisplayBlog.aspx)
- Mohit Srivastava, Microsoft
- [Raffaele Rialdi, Itálie](http://www.iamraf.net/)
- [Rick Anderson, Microsoft](https://blogs.msdn.com/b/rickandy/)
- [Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))
- [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))
- [Scott Hunterem, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))
- [Srđan Božović, Srbsko](http://msforge.net/blogs/zmajcek/)
- [Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))

> [!div class="step-by-step"]
> [Předchozí](command-line-deployment.md)
> [Další](troubleshooting.md)
