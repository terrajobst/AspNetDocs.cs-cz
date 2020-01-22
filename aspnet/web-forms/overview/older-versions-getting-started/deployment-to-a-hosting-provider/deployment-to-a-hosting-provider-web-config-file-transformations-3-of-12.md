---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12
title: 'Nasazení webové aplikace SQL Server Compact v ASP.NET s využitím sady Visual Studio nebo Visual Web Developer: transformace souboru Web. config-3 z 12 | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 2b0df3d9-450b-4ea6-b315-4c9650722cad
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12
msc.type: authoredcontent
ms.openlocfilehash: 9e7902bcf8a16c154aee1a982824bfaedeea7d9d
ms.sourcegitcommit: 7b1e1784213dd4c301635f9e181764f3e2f94162
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/22/2020
ms.locfileid: "76309233"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-webconfig-file-transformations---3-of-12"></a>Nasazení webové aplikace SQL Server Compact v ASP.NET s využitím sady Visual Studio nebo Visual Web Developer: transformace souboru Web. config-3 z 12

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Studio 2012 RC nebo Visual Studio Express 2012 RC pro web. Můžete také použít Visual Studio 2010, pokud nainstalujete aktualizaci publikování na webu. Úvod k řadě najdete v [prvním kurzu v řadě](deployment-to-a-hosting-provider-introduction-1-of-12.md).
> 
> Kurz, který ukazuje funkce nasazení představené po vydání RC sady Visual Studio 2012, ukazuje, jak nasadit SQL Server edice jiné než SQL Server Compact a ukazuje, jak nasadit na Azure App Service Web Apps, v tématu [nasazení webu ASP.NET pomocí sady Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Přehled

V tomto kurzu se dozvíte, jak automatizovat proces změny souboru *Web. config* při jeho nasazení do různých cílových prostředí. Většina aplikací má nastavení v souboru *Web. config* , které se musí při nasazení aplikace lišit. Automatizace procesu provádění těchto změn vám zajistí, že byste je museli provádět ručně při každém nasazení, což by bylo zdlouhavé a náchylné k chybám.

Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje při procházení tohoto kurzu, zkontrolujte [stránku řešení potíží](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Transformace Web. config oproti Nasazení webum parametrům

Existují dva způsoby automatizace procesu změny nastavení souboru *Web. config* : [transformace Web. config](https://msdn.microsoft.com/library/dd465326.aspx) a [parametry nasazení webu](https://msdn.microsoft.com/library/ff398068.aspx). Transformační soubor *Web. config* obsahuje kód XML, který určuje, jak se má při nasazení změnit soubor *Web. config* . Můžete určit různé změny pro konkrétní konfigurace sestavení a pro konkrétní publikační profily. Výchozí konfigurace sestavení jsou ladění a vydání a můžete vytvořit vlastní konfigurace sestavení. Profil publikování obvykle odpovídá cílovému prostředí. (Další informace o profilech publikování najdete v kurzu [nasazení do služby IIS jako testovací prostředí](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) .)

Parametry Nasazení webu lze použít k určení mnoha různých druhů nastavení, které je třeba konfigurovat během nasazování, včetně nastavení, která jsou nalezena v souborech *Web. config* . Při použití k zadání změn souboru *Web. config* nasazení webu parametry jsou složitější, aby je bylo možné nastavit, ale jsou užitečné, pokud neznáte hodnotu, která má být nastavena, dokud nebudete nasazovat. Například v podnikovém prostředí můžete vytvořit *balíček pro nasazení* a dát mu osobu v oddělení IT, aby se nainstalovala v produkčním prostředí, a tato osoba musí být schopná zadat připojovací řetězce nebo hesla, které neznáte.

Scénář, na který se tento kurz zabývá, najdete v části všechno, co se má udělat v souboru *Web. config* , takže nemusíte používat parametry nasazení webu. Nakonfigurujete některé transformace, které se liší v závislosti na použité konfiguraci sestavení a některé, které se liší v závislosti na použitém profilu publikování.

## <a name="creating-transformation-files-for-publish-profiles"></a>Vytváření transformačních souborů pro profily publikování

V **Průzkumník řešení**rozbalte *Web. config* a zobrazte transformační soubory *Web. Debug. config* a *Web. Release. config* , které jsou vytvořeny ve výchozím nastavení pro dvě výchozí konfigurace sestavení.

![Web.config_transform_files](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image1.png)

Transformační soubory pro vlastní konfigurace sestavení můžete vytvořit tak, že kliknete pravým tlačítkem na soubor Web. config a zvolíte přidat transformované **transformace** z kontextové nabídky, ale pro tento kurz to nemusíte dělat.

Pro konfiguraci změn, které se vztahují k cílovému umístění nasazení, a nikoli ke konfiguraci sestavení, potřebujete dva další transformační soubory. Typický příklad tohoto druhu nastavení je koncový bod WCF, který se liší pro testování a produkci. V novějších kurzech vytvoříte profily publikování s názvem test a produkční, takže budete potřebovat soubor *Web. test. config* a soubor *Web. produkční. config* .

Transformační soubory, které jsou svázané s publikačními profily, je nutné vytvořit ručně. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt ContosoUniversity a vyberte **Otevřít složku v Průzkumníku Windows**.

![Open_folder_in_Windows_Explorer](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image2.png)

V **Průzkumníku Windows**vyberte soubor *Web. Release. config* , zkopírujte soubor a pak vložte dvě kopie. Přejmenujte tyto kopie *Web. produkční. config* a *Web. test. config*a pak zavřete **Průzkumníka Windows**.

V **Průzkumník řešení**kliknutím na **aktualizovat** zobrazíte nové soubory.

Vyberte nové soubory, klikněte pravým tlačítkem myši a potom v místní nabídce klikněte na možnost **zahrnout do projektu** .

![Zahrnutí testovacích a produkčních konfiguračních souborů do projektu](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image3.png)

Chcete-li zabránit nasazení těchto souborů, vyberte je v **Průzkumník řešení**a potom v okně **vlastnosti** změňte vlastnost **Akce sestavení** z **obsahu** na **hodnotu žádné**. (Transformační soubory, které jsou založeny na konfiguracích sestavení, jsou automaticky znemožněny nasazením.)

Nyní jste připraveni zadat transformace *Web. config* do transformačních souborů *Web. config* .

## <a name="limiting-error-log-access-to-administrators"></a>Omezení přístupu k protokolu chyb správcům

Pokud při spuštění aplikace dojde k chybě, aplikace zobrazí obecnou chybovou stránku namísto chybové stránky generované systémem a používá [knihovny elmah balíček NuGet](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) pro protokolování chyb a vytváření sestav. Element `customErrors` v souboru *Web. config* určuje chybovou stránku:

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample1.xml)]

Chcete-li zobrazit chybovou stránku, dočasně změňte atribut `mode` elementu `customErrors` z "RemoteOnly" na "on" a spusťte aplikaci ze sady Visual Studio. Způsobí chybu zadáním neplatné adresy URL, například *Studentsxxx. aspx*. Namísto chybové stránky nenalezené stránky, která je generována službou IIS, se zobrazí stránka *GenericErrorPage. aspx* .

[![Error_page](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image5.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image4.png)

Chcete-li zobrazit protokol chyb, nahraďte vše v adrese URL za číslem portu pomocí *knihovny elmah. axd* (pro příklad na snímku obrazovky `http://localhost:51130/elmah.axd`) a stiskněte klávesu ENTER:

[![Elmah_log_page](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image7.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image6.png)

Po dokončení nezapomeňte nastavit `customErrors` element zpět na režim "RemoteOnly".

Na vašem vývojovém počítači je vhodné zajistit bezplatný přístup ke stránce protokolu chyb, ale v produkčním prostředí by se mohlo jednat o bezpečnostní riziko. V produkčním webu můžete přidat autorizační pravidlo, které omezuje přístup k protokolu chyb jenom správcům, a to tak, že v souboru *Web. produkční. config* nakonfigurujete transformaci.

Otevřete *Web. produkční. config* a přidejte nový prvek `location` hned za otevírací značku `configuration`, jak je znázorněno zde. (Ujistěte se, že přidáte pouze prvek `location` a nikoli okolní kód, který je zde zobrazen pouze k poskytnutí nějakého kontextu.)

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample2.xml?highlight=2-9)]

Hodnota atributu `Transform` příkazu INSERT způsobí, že tento prvek `location` přidat jako položku na stejné úrovni do všech existujících `location` prvků v souboru *Web. config* . (Již existuje jeden `location` element, který určuje autorizační pravidla pro stránku **aktualizace kreditů** .) Při testování produkčního webu po nasazení otestujete test a ověřte, zda je toto autorizační pravidlo platné.

V testovacím prostředí není nutné omezit přístup k protokolu chyb, takže nemusíte přidávat tento kód do souboru *Web. test. config* .

> [!NOTE] 
> 
> **Poznámka k zabezpečení** Nikdy nezobrazuje podrobnosti o chybě pro veřejnost v produkční aplikaci nebo tyto informace ukládejte ve veřejném umístění. Útočníci můžou pomocí informací o chybách zjišťovat ohrožení zabezpečení v lokalitě. Pokud ve své vlastní aplikaci používáte knihovny ELMAH, nezapomeňte prozkoumat způsoby, kterými se knihovny ELMAH dá nakonfigurovat tak, aby se minimalizovala rizika zabezpečení. KNIHOVNY ELMAH příklad v tomto kurzu by se neměl považovat za doporučenou konfiguraci. Je to příklad, který jste zvolili pro ilustraci, jak zpracovat složku, ve které musí být aplikace schopná vytvářet soubory.

## <a name="setting-an-environment-indicator"></a>Nastavení indikátoru prostředí

Běžným scénářem je nastavení souboru *Web. config* , které musí být v každém prostředí, které nasazujete na, odlišné. Například aplikace, která volá službu WCF, může v testovacích a produkčních prostředích potřebovat jiný koncový bod. Aplikace Contoso University obsahuje také nastavení tohoto druhu. Toto nastavení řídí viditelný indikátor na stránkách webu, které vám sdělí, ve kterém prostředí se nacházíte, jako je vývoj, testování nebo produkce. Hodnota nastavení určuje, zda bude aplikace připojovat "(dev)" nebo "(test)" do hlavního nadpisu na stránce hlavního *serveru.* Master:

[![Environment_indicator](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image9.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image8.png)

Indikátor prostředí se vynechá, když aplikace běží v produkčním prostředí.

Webové stránky společnosti Contoso University čtou hodnotu, která je nastavena v `appSettings` v souboru *Web. config* , aby bylo možné určit prostředí, ve kterém je aplikace spuštěná:

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample3.xml)]

Hodnota by měla být "test" v testovacím prostředí a "prod" v produkčním prostředí.

Otevřete *Web. produkční. config* a přidejte `appSettings` prvek těsně před počáteční značku `location` elementu, který jste přidali dříve:

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample4.xml)]

Hodnota atributu `xdt:Transform` "Setattributess" značí, že účelem této transformace je změnit hodnoty atributu stávajícího prvku v souboru *Web. config* . Hodnota atributu `xdt:Locator` Match (Key) označuje, že prvek, který má být změněn, je ten, jehož atribut `key` odpovídá atributu `key`, který je zde uveden. Jediný atribut prvku `add` je `value`a to je to, co se v nasazeném souboru *Web. config* změní. Tento kód způsobí, že atribut `value` elementu `Environment` `appSettings` má být v souboru *Web. config* , který je nasazen do produkčního prostředí, nastaven na "prod".

Dále použijte stejnou změnu v souboru *Web. test. config* , kromě nastavení `value` na "test" místo "prod". Po dokončení bude oddíl `appSettings` v *souboru Web. test. config* vypadat jako v následujícím příkladu:

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample5.xml)]

## <a name="disabling-debug-mode"></a>Zakazování režimu ladění

Pro sestavení pro vydání nechcete povolit ladění bez ohledu na to, které prostředí nasazujete do nástroje. Ve výchozím nastavení se transformační soubor *Web. Release. config* automaticky vytvoří s kódem, který odebere atribut `debug` z `compilation` elementu:

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample6.xml)]

Atribut `Transform` způsobí, že atribut `debug` bude vynechán z nasazeného souboru *Web. config* při každém nasazení sestavení pro vydání.

Tato stejná transformace je v souborových transformačních a produkčních převodech, protože jste je vytvořili zkopírováním transformačního souboru verze. Nebudete je muset duplikovat, proto otevřete každý z těchto souborů, odeberte **kompilační** prvek a uložte a zavřete jednotlivé soubory.

## <a name="setting-connection-strings"></a>Nastavení připojovacích řetězců

Ve většině případů není nutné nastavovat transformace připojovacích řetězců, protože v profilu publikování můžete zadat připojovací řetězce. Ale při nasazování databáze SQL Server Compact existuje výjimka a používáte Migrace Entity Framework Code First k aktualizaci databáze na cílovém serveru. V tomto scénáři je nutné zadat další připojovací řetězec, který bude použit na serveru pro aktualizaci schématu databáze. Chcete-li nastavit tuto transformaci, přidejte **&gt;elementu&lt;connectionStrings** hned po úvodní značce **&gt;&lt;konfigurace** v souboru *Web. test. config* a v transformačních souborech *Web. produkční. config* :

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample7.xml)]

Atribut `Transform` určuje, zda bude tento připojovací řetězec přidán do elementu *connectionStrings* v nasazeném souboru *Web. config* . (Proces publikování automaticky vytvoří tento další připojovací řetězec, pokud neexistuje, ale ve výchozím nastavení je atribut **ProviderName** nastaven na `System.Data.SqlClient`, který nefunguje pro SQL Server Compact. Přidáním připojovacího řetězce ručně zachováte proces nasazení z vytváření elementu připojovacího řetězce s nesprávným názvem poskytovatele.)

Nyní jste zadali všechny transformace *Web. config* , které potřebujete pro nasazení aplikace Contoso University na testování a produkci. V následujícím kurzu se postará o úlohy nastavení nasazení, které vyžadují nastavení vlastností projektu.

## <a name="more-information"></a>Další informace

Další informace o tématech popsaných v tomto kurzu najdete v tématu scénář transformace Web. config v [mapě obsahu nasazení ASP.NET](https://msdn.microsoft.com/library/bb386521.aspx).

> [!div class="step-by-step"]
> [Předchozí](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
> [Další](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
