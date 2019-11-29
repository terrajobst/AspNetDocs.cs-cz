---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 'ASP.NET nasazení webu pomocí sady Visual Studio: transformace souboru Web. config | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která bude Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a9d39547c94a63003442ba6fe1257693dde24b05
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621791"
---
# <a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a>ASP.NET nasazení webu pomocí sady Visual Studio: transformace souborů Web. config

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která umožňuje Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí sady Visual Studio 2012 nebo Visual Studio 2010. Informace o řadě najdete v [prvním kurzu v řadě](introduction.md).

## <a name="overview"></a>Přehled

V tomto kurzu se dozvíte, jak automatizovat proces změny souboru *Web. config* při jeho nasazení do různých cílových prostředí. Většina aplikací má nastavení v souboru *Web. config* , které se musí při nasazení aplikace lišit. Automatizace procesu provádění těchto změn vám zajistí, že byste je museli provádět ručně při každém nasazení, což by bylo zdlouhavé a náchylné k chybám.

Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje při procházení tohoto kurzu, zkontrolujte [stránku řešení potíží](troubleshooting.md).

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Transformace Web. config oproti Nasazení webum parametrům

Existují dva způsoby automatizace procesu změny nastavení souboru *Web. config* : [transformace Web. config](https://msdn.microsoft.com/library/dd465326.aspx) a [parametry nasazení webu](https://msdn.microsoft.com/library/ff398068.aspx). Transformační soubor *Web. config* obsahuje kód XML, který určuje, jak se má při nasazení změnit soubor *Web. config* . Můžete určit různé změny pro konkrétní konfigurace sestavení a pro konkrétní publikační profily. Výchozí konfigurace sestavení jsou ladění a vydání a můžete vytvořit vlastní konfigurace sestavení. Profil publikování obvykle odpovídá cílovému prostředí. (Další informace o profilech publikování najdete v kurzu [nasazení do služby IIS jako testovací prostředí](deploying-to-iis.md) .)

Parametry Nasazení webu lze použít k určení mnoha různých druhů nastavení, které je třeba konfigurovat během nasazování, včetně nastavení, která jsou nalezena v souborech *Web. config* . Při použití k zadání změn souboru *Web. config* nasazení webu parametry jsou složitější, aby je bylo možné nastavit, ale jsou užitečné, pokud neznáte hodnotu, která má být nastavena, dokud nebudete nasazovat. Například v podnikovém prostředí můžete vytvořit *balíček pro nasazení* a dát mu osobu v oddělení IT, aby se nainstalovala v produkčním prostředí, a tato osoba musí být schopná zadat připojovací řetězce nebo hesla, které neznáte.

V případě scénáře, ve kterém se tato řada kurzů zabývá, si poznáte všechno, co se má udělat v souboru *Web. config* , takže nemusíte používat nasazení webu parametry. Nakonfigurujete některé transformace, které se liší v závislosti na použité konfiguraci sestavení a některé, které se liší v závislosti na použitém profilu publikování.

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a>Zadání nastavení Web. config v Azure

Pokud je nastavení souboru *Web. config* , které chcete změnit, v `<connectionStrings>` nebo `<appSettings>`m prvku a pokud nasazujete do Web Apps v Azure App Service, máte další možnost pro automatizaci změn během nasazení. Nastavení, která chcete uplatnit v Azure, můžete zadat na kartě **Konfigurovat** na stránce portálu pro správu vaší webové aplikace (přejděte dolů k části **nastavení aplikace** a **připojovací řetězce** ). Při nasazení projektu Azure automaticky aplikuje změny. Další informace najdete v tématu [Weby Windows Azure: jak fungují řetězce aplikace a připojovací řetězce](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).

## <a name="default-transformation-files"></a>Výchozí transformační soubory

V **Průzkumník řešení**rozbalte *Web. config* a zobrazte transformační soubory *Web. Debug. config* a *Web. Release. config* , které jsou vytvořeny ve výchozím nastavení pro dvě výchozí konfigurace sestavení.

![Web. config_transform_files](web-config-transformations/_static/image1.png)

Transformační soubory pro vlastní konfigurace sestavení lze vytvořit kliknutím pravým tlačítkem myši na soubor Web. config a výběrem možnosti **Přidat transformace konfigurace** z místní nabídky. V tomto kurzu to nemusíte dělat a možnost nabídky je zakázaná, protože jste nevytvořili žádné vlastní konfigurace sestavení.

Později vytvoříte tři další transformační soubory, jednu z nich pro profily publikování testů, přípravy a výroby. Typický příklad nastavení, které byste zpracovali v transformačním souboru profilu publikování, protože závisí na cílovém prostředí je koncový bod WCF, který se liší pro testování a produkci. Transformační soubory profilu publikování vytvoříte v pozdějších kurzech po vytvoření profilů publikování, se kterými se budou nacházet.

## <a name="disable-debug-mode"></a>Zakázat režim ladění

Příkladem nastavení, které závisí na konfiguraci sestavení místo cílového prostředí, je atribut `debug`. Pro sestavení pro vydání vydaných verzí se obvykle požaduje ladění zakázané bez ohledu na to, ve kterém prostředí nasazujete. Proto ve výchozím nastavení šablony projektu sady Visual Studio vytvoří transformační soubory *Web. Release. config* s kódem, který odebere atribut `debug` z `compilation` elementu. Toto je výchozí *Web. Release. config*: Kromě některého ukázkového transformačního kódu, který je označen jako komentář, obsahuje kód v prvku `compilation`, který odebere `debug` atribut:

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

Atribut `xdt:Transform="RemoveAttributes(debug)"` určuje, zda chcete odebrat atribut `debug` z `system.web/compilation` elementu v nasazeném souboru *Web. config* . To se provede pokaždé, když nasadíte sestavení pro vydání.

## <a name="limit-error-log-access-to-administrators"></a>Omezit přístup k protokolu chyb správcům

Pokud při spuštění aplikace dojde k chybě, aplikace zobrazí obecnou chybovou stránku místo chybové stránky generované systémem a k protokolování chyb a vytváření sestav používá [balíček NuGet knihovny elmah](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) . Element `customErrors` v souboru *Web. config* aplikace určuje chybovou stránku:

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

Chcete-li zobrazit chybovou stránku, dočasně změňte atribut `mode` elementu `customErrors` z "RemoteOnly" na "on" a spusťte aplikaci ze sady Visual Studio. Způsobí chybu zadáním neplatné adresy URL, například *Studentsxxx. aspx*. Namísto chybové stránky vygenerované službou IIS "prostředek nelze nalézt" se zobrazí stránka *GenericErrorPage. aspx* .

![Chybová stránka](web-config-transformations/_static/image2.png)

Chcete-li zobrazit protokol chyb, nahraďte vše v adrese URL za číslem portu pomocí *knihovny elmah. axd* (například `http://localhost:51130/elmah.axd`) a stiskněte klávesu ENTER:

![Stránka knihovny ELMAH](web-config-transformations/_static/image3.png)

Po dokončení nezapomeňte nastavit `customErrors` element zpět na režim "RemoteOnly".

Na vašem vývojovém počítači je vhodné zajistit bezplatný přístup ke stránce protokolu chyb, ale v produkčním prostředí by se mohlo jednat o bezpečnostní riziko. V produkčním webu chcete přidat autorizační pravidlo, které omezuje přístup k protokolu chyb správcům, a zajistit, aby omezení fungovalo i v testu a v přípravě. Proto se jedná o další změnu, kterou chcete implementovat při každém nasazení sestavení pro vydání, a proto patří do souboru *Web. Release. config* .

Otevřete *Web. Release. config* a přidejte nový prvek `location` bezprostředně před uzavírací značku `configuration`, jak je znázorněno zde.

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

Hodnota atributu `Transform` příkazu INSERT způsobí, že tento prvek `location` přidat jako položku na stejné úrovni do všech existujících `location` prvků v souboru *Web. config* . (Již existuje jeden `location` element, který určuje autorizační pravidla pro stránku **aktualizace kreditů** .)

Nyní můžete zobrazit náhled transformace a ujistit se, že je správně kódována.

V **Průzkumník řešení**klikněte pravým tlačítkem na *Web. Release. config* a klikněte na **Náhled transformovat**.

![Náhled nabídky transformace](web-config-transformations/_static/image4.png)

Otevře se stránka s vývojovým souborem *Web. config* na levé straně a informace o tom, jak bude nasazený soubor *Web. config* vypadat na pravé straně, se zvýrazněnými změnami.

![Náhled transformace ladění](web-config-transformations/_static/image5.png)

![Náhled transformace umístění](web-config-transformations/_static/image6.png)

(Ve verzi Preview si můžete všimnout některých dalších změn, u kterých jste nenapsali transformace: typicky se to týká odebrání prázdných znaků, které neovlivňují funkčnost.)

Když po nasazení otestujete lokalitu, otestujete také, abyste ověřili, že autorizační pravidlo je platné.

> [!NOTE] 
> 
> **Poznámka k zabezpečení** Nikdy nezobrazuje podrobnosti o chybě pro veřejnost v produkční aplikaci nebo tyto informace ukládejte ve veřejném umístění. Útočníci můžou pomocí informací o chybách zjišťovat ohrožení zabezpečení v lokalitě. Pokud používáte knihovny ELMAH ve vlastní aplikaci, nakonfigurujte knihovny ELMAH tak, aby se minimalizovala rizika zabezpečení. KNIHOVNY ELMAH příklad v tomto kurzu by se neměl považovat za doporučenou konfiguraci. Je to příklad, který jste zvolili pro ilustraci, jak zpracovat složku, ve které musí být aplikace schopná vytvářet soubory. Další informace najdete v tématu [zabezpečení koncového bodu knihovny elmah](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages).

## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a>Nastavení, které budete zpracovávat v transformačních souborech profilu publikování

Běžným scénářem je nastavení souboru *Web. config* , které musí být v každém prostředí, které nasazujete na, odlišné. Například aplikace, která volá službu WCF, může v testovacích a produkčních prostředích potřebovat jiný koncový bod. Aplikace Contoso University obsahuje také nastavení tohoto druhu. Toto nastavení řídí viditelný indikátor na stránkách webu, které vám sdělí, ve kterém prostředí se nacházíte, jako je vývoj, testování nebo produkce. Hodnota nastavení určuje, zda bude aplikace připojovat "(dev)" nebo "(test)" do hlavního nadpisu na stránce hlavního *serveru.* Master:

![Indikátor prostředí](web-config-transformations/_static/image7.png)

Indikátor prostředí je vynechán, když aplikace běží v pracovním nebo produkčním prostředí.

Webové stránky společnosti Contoso University čtou hodnotu, která je nastavena v `appSettings` v souboru *Web. config* , aby bylo možné určit prostředí, ve kterém je aplikace spuštěná:

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

Hodnota by měla být "test" v testovacím prostředí a "prod" pro přípravu a výrobu.

Následující kód v transformačním souboru bude implementovat tuto transformaci:

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

Hodnota atributu `xdt:Transform` "Setattributess" značí, že účelem této transformace je změnit hodnoty atributu stávajícího prvku v souboru *Web. config* . Hodnota atributu `xdt:Locator` Match (Key) označuje, že prvek, který má být změněn, je ten, jehož atribut `key` odpovídá atributu `key`, který je zde uveden. Jediný atribut prvku `add` je `value`a to je to, co se v nasazeném souboru *Web. config* změní. Zde zobrazený kód způsobí, že atribut `value` elementu `Environment` `appSettings` v souboru *Web. config* , který je nasazený, bude nastaven na "test".

Tato transformace patří do transformačních souborů profilu publikování, které jste ještě nevytvořili. Při vytváření profilů publikování pro testovací, testovací a produkční prostředí vytvoříte a aktualizujete transformační soubory, které tuto změnu implementují. Uděláte to tak, že ve [službě IIS](deploying-to-iis.md) nasadíte a [nasadíte do produkčních](deploying-to-production.md) kurzů.

> [!NOTE]
> Vzhledem k tomu, že toto nastavení je v prvku `<appSettings>`, máte další alternativu k určení transformace při nasazení do Web Apps v Azure App Service v části [Určení nastavení souboru Web. config v Azure](#watransforms) výše v tomto tématu.

## <a name="setting-connection-strings"></a>Nastavení připojovacích řetězců

I když výchozí transformační soubor obsahuje příklad, který ukazuje, jak aktualizovat připojovací řetězec, ve většině případů nemusíte nastavovat transformace připojovacích řetězců, protože můžete zadat připojovací řetězce v profilu publikování. Uděláte to tak, že ve [službě IIS](deploying-to-iis.md) nasadíte a [nasadíte do produkčních](deploying-to-production.md) kurzů.

## <a name="summary"></a>Přehled

Nyní máte k dispozici tolik, kolik máte s transformací *Web. config* před vytvořením profilů publikování a zobrazili jste náhled toho, co se nachází v nasazeném souboru Web. config.

![Náhled transformace umístění](web-config-transformations/_static/image8.png)

V následujícím kurzu se postará o úlohy nastavení nasazení, které vyžadují nastavení vlastností projektu.

## <a name="more-information"></a>Další informace

Další informace o tématech popsaných v tomto kurzu najdete v tématu [Použití transformací Web. config ke změně nastavení v cílovém souboru Web. config nebo App. config během nasazování](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms) v mapě obsahu nasazení webu pro Visual Studio a ASP.NET.

> [!div class="step-by-step"]
> [Předchozí](preparing-databases.md)
> [Další](project-properties.md)
