---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
title: 'Nasazení webové aplikace v ASP.NET pomocí SQL Server Compact sady Visual Studio nebo Visual Web Developer: nasazení do služby IIS jako testovací prostředí – 5 z 12 | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 493b2a66-816c-485c-8315-952ed1085ccc
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
msc.type: authoredcontent
ms.openlocfilehash: 5d85232ff2cb229d771d517db7173721c9e277bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78635126"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-iis-as-a-test-environment---5-of-12"></a>Nasazení webové aplikace SQL Server Compact v ASP.NET s využitím sady Visual Studio nebo Visual Web Developer: nasazení do služby IIS jako testovací prostředí – 5.12.

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Studio 2012 RC nebo Visual Studio Express 2012 RC pro web. Můžete také použít Visual Studio 2010, pokud nainstalujete aktualizaci publikování na webu. Úvod k řadě najdete v [prvním kurzu v řadě](deployment-to-a-hosting-provider-introduction-1-of-12.md).
> 
> Kurz, který ukazuje funkce nasazení představené po vydání RC sady Visual Studio 2012, ukazuje, jak nasadit SQL Server edice jiné než SQL Server Compact a ukazuje, jak nasadit na Azure App Service Web Apps, v tématu [nasazení webu ASP.NET pomocí sady Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Přehled

V tomto kurzu se dozvíte, jak nasadit webovou aplikaci v ASP.NET do služby IIS v místním počítači.

Když vyvíjíte aplikaci, obecně se otestujete jejich spuštěním v aplikaci Visual Studio. Ve výchozím nastavení to znamená, že používáte vývojový server sady Visual Studio (označovaný také jako Cassini). Vývojový server sady Visual Studio usnadňuje testování během vývoje v aplikaci Visual Studio, ale nefunguje úplně stejně jako služba IIS. V důsledku toho je možné, že aplikace bude správně fungovat při testování v sadě Visual Studio, ale selže při nasazení do služby IIS v hostitelském prostředí.

Aplikaci můžete testovat spolehlivě v těchto ohledech:

1. Při testování v aplikaci Visual Studio během vývoje použijte IIS Express nebo celou službu IIS místo vývojového serveru sady Visual Studio. Tato metoda obecně emuluje přesnější způsob, jakým bude web běžet v rámci služby IIS. Tato metoda však netestuje proces nasazení nebo neověřuje, zda výsledek procesu nasazení bude správně fungovat.
2. Nasaďte aplikaci do služby IIS na svém vývojovém počítači pomocí stejného procesu, který později použijete k jeho nasazení do provozního prostředí. Tato metoda ověřuje i proces nasazení společně s ověřením, že vaše aplikace bude ve službě IIS správně fungovat.
3. Nasaďte aplikaci do testovacího prostředí, které je co nejblíže vašemu provoznímu prostředí. Vzhledem k tomu, že provozní prostředí pro tyto kurzy je poskytovatel hostingu třetí strany, ideální testovací prostředí by představovalo druhý účet u poskytovatele hostingu. Tento druhý účet byste použili jenom pro testování, ale měl by se nastavit stejným způsobem jako provozní účet.

V tomto kurzu se dozvíte o krocích pro možnost 2. Doprovodné materiály k možnosti 3 najdete na konci kurzu [nasazení do provozního prostředí](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) a na konci tohoto kurzu jsou k dispozici odkazy na zdroje pro možnost 1.

Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje při procházení tohoto kurzu, zkontrolujte [stránku řešení potíží](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).

## <a name="configuring-the-application-to-run-in-medium-trust"></a>Konfigurace aplikace tak, aby běžela ve středním vztahu důvěryhodnosti

Než nainstalujete službu IIS a nasadíte do ní, změníte nastavení souboru Web. config tak, aby lokalita běžela podobně jako v typickém hostitelském prostředí.

Poskytovatelé hostingu obvykle spouštějí váš web ve *středním vztahu důvěryhodnosti*, což znamená, že některé věci není povoleno. Například kód aplikace nemůže získat přístup k registru systému Windows a nemůže číst nebo zapisovat soubory, které se nacházejí mimo hierarchii složek vaší aplikace. Ve výchozím nastavení je vaše aplikace spuštěná ve *vysokém vztahu důvěryhodnosti* v místním počítači, což znamená, že aplikace může být schopná provádět věci, které se při nasazení do produkčního prostředí nezdařily. Proto pokud chcete, aby testovací prostředí přesněji odráželo provozní prostředí, nakonfigurujete aplikaci tak, aby běžela ve středním vztahu důvěryhodnosti.

V souboru Web. config aplikace přidejte prvek **Trust** do prvku **System. Web** , jak je znázorněno v tomto příkladu.

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample1.xml?highlight=4)]

Aplikace se teď v IIS spustí ve středním vztahu důvěryhodnosti i na místním počítači. Toto nastavení umožňuje zachytit co nejdříve všechny pokusy pomocí kódu aplikace a udělat tak něco, co by selhalo v produkčním prostředí.

> [!NOTE]
> Pokud používáte Migrace Entity Framework Code First, ujistěte se, že máte nainstalovanou verzi 5,0 nebo novější. V Entity Framework verze 4,3 vyžaduje migrace úplný vztah důvěryhodnosti, aby bylo možné aktualizovat schéma databáze.

## <a name="installing-iis-and-web-deploy"></a>Instalace služby IIS a Nasazení webu

Chcete-li nasadit službu IIS na vývojovém počítači, je nutné, aby byla nainstalována služba IIS a Nasazení webu. Nejsou zahrnuty ve výchozí konfiguraci systému Windows 7. Pokud jste již nainstalovali službu IIS i Nasazení webu, přejděte k další části.

Použití [instalačního programu webové platformy](https://www.microsoft.com/web/downloads/platform.aspx) je preferovaný způsob, jak nainstalovat službu iis a nasazení webu, protože instalační program webové platformy nainstaluje doporučenou konfiguraci služby IIS a automaticky nainstaluje požadavky pro službu IIS a v případě potřeby také nasazení webu.

Chcete-li spustit instalační program webové platformy pro instalaci služby IIS a Nasazení webu, použijte následující odkaz. Pokud jste již nainstalovali službu IIS, Nasazení webu nebo některou z požadovaných součástí, nainstaluje instalační program webové platformy pouze ty, co chybí.

- [Instalace služby IIS a Nasazení webu pomocí WebPI](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=IIS7;ASPNET;NETFramework4;WDeploy)

## <a name="setting-the-default-application-pool-to-net-4"></a>Nastavení výchozího fondu aplikací na .NET 4

Po instalaci služby IIS spusťte **Správce služby IIS** , abyste se ujistili, že se k výchozímu fondu aplikací přiřadí .NET Framework verze 4.

V nabídce **Start** systému Windows vyberte možnost **Spustit**, zadejte příkaz "inetmgr" a pak klikněte na tlačítko **OK**. (Pokud příkaz **Spustit** není v nabídce **Start** , můžete stisknout klávesu Windows a R, abyste ho otevřeli. Nebo klikněte pravým tlačítkem myši na hlavní panel, klikněte na **vlastnosti**, vyberte kartu **nabídky Start** , klikněte na **přizpůsobit**a vyberte **Spustit příkaz**.)

V podokně **připojení** rozbalte uzel server a vyberte **fondy aplikací**. V podokně **fondy aplikací** , pokud je aplikace **DefaultAppPool** přiřazena k rozhraní .NET Framework verze 4, jak je znázorněno na následujícím obrázku, přejděte k další části.

[![Inetmgr_showing_4.0_app_pools](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image1.png)

Pokud vidíte pouze dva fondy aplikací a obě jsou nastaveny na .NET Framework 2,0, je nutné nainstalovat ASP.NET 4 do služby IIS:

- Otevřete okno příkazového řádku kliknutím pravým tlačítkem myši na **příkazový řádek** v nabídce **Start** systému Windows a výběrem možnosti **Spustit jako správce**. Pak spuštěním příkazu [aspnet\_regiis. exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx) nainstalujte ASP.NET 4 ve službě IIS pomocí následujících příkazů. (V 64 systémech nahraďte "Framework" "Framework64".)

    [!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample2.cmd)]

    [![aspnet_regiis_installing_ASP. NET_4](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image3.png)

    Tento příkaz vytvoří nové fondy aplikací pro .NET Framework 4, ale výchozí fond aplikací bude stále nastaven na 2,0. Nasadíte aplikaci, která cílí na rozhraní .NET 4, do tohoto fondu aplikací, takže musíte změnit fond aplikací na .NET 4.

Pokud jste zavřeli **Správce služby IIS**, spusťte ho znovu, rozbalte uzel serveru a kliknutím na **fondy aplikací** zobrazte znovu podokno **fondy aplikací** .

V podokně **fondy aplikací** klikněte na **DefaultAppPool**a potom v podokně **Akce** klikněte na **základní nastavení**.

[![Inetmgr_selecting_Basic_Settings_for_app_pool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image5.png)

V dialogovém okně **Upravit fond aplikací** změňte **.NET Framework verze** na **.NET Framework v 4.0.30319** a klikněte na **OK**.

[![Selecting_. NET_4_for_DefaultAppPool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image7.png)

Nyní jste připraveni publikovat do služby IIS.

## <a name="publishing-to-iis"></a>Publikování do služby IIS

Existuje několik způsobů, jak můžete nasadit pomocí sady Visual Studio 2010 a Nasazení webu:

- Použijte možnost publikování jedním kliknutím v aplikaci Visual Studio.
- Vytvořte *balíček pro nasazení* a nainstalujte ho pomocí uživatelského rozhraní Správce služby IIS. Balíček pro nasazení se skládá ze souboru *. zip* , který obsahuje všechny soubory a metadata potřebná k instalaci lokality ve službě IIS.
- Vytvořte balíček pro nasazení a nainstalujte ho pomocí příkazového řádku.

Proces, který jste provedli v předchozích kurzech k nastavení sady Visual Studio pro automatizaci úloh nasazení, se vztahuje na všechny tyto tři metody. V těchto kurzech použijete první z těchto metod. Informace o použití balíčků nasazení najdete v tématu [Mapa obsahu nasazení ASP.NET](https://msdn.microsoft.com/library/bb386521.aspx).

Před publikováním se ujistěte, že používáte aplikaci Visual Studio v režimu správce. (V nabídce **Start** ve Windows 7 klikněte pravým tlačítkem na ikonu pro verzi sady Visual Studio, kterou používáte, a vyberte **Spustit jako správce**.) Režim správce je vyžadován pro publikování pouze v případě, že publikujete do služby IIS v místním počítači.

V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt ContosoUniversity (ne na projekt CONTOSOUNIVERSITY. dal) a vyberte **publikovat**.

Zobrazí se průvodce **publikováním webu** .

![Publish_Web_wizard_Profile_tab](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image9.png)

V rozevíracím seznamu vyberte **&lt;nový...&gt;** .

V dialogovém okně **Nový profil** zadejte "test" a pak klikněte na **OK**.

![New_Profile_dialog_box](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image10.png)

Tento název je stejný jako prostřední uzel transformačního souboru Web. test. config, který jste vytvořili dříve. Tato korespondence vede k tomu, že při publikování pomocí tohoto profilu způsobí použití transformací Web. test. config.

Průvodce se automaticky přesune na kartu **připojení** .

Do pole **Adresa URL služby** zadejte *localhost*.

Do pole **Web/aplikace** zadejte *Default Web site/ContosoUniversity*.

Do pole **cílová adresa URL** zadejte `http://localhost/ContosoUniversity`.

Nastavení **cílové adresy URL** není vyžadováno. Když Visual Studio dokončí nasazení aplikace, automaticky otevře výchozí prohlížeč na této adrese URL. Pokud nechcete, aby se prohlížeč po nasazení otevřel automaticky, nechejte toto pole prázdné.

![Publish_Web_wizard_Connection_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image11.png)

Klikněte na **ověřit připojení** , abyste ověřili, že jsou nastavení správná, a můžete se připojit ke službě IIS v místním počítači.

Zelená značka zaškrtnutí ověří, že připojení proběhlo úspěšně.

![Publish_Web_wizard_Connection_tab_validated](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image12.png)

Kliknutím na tlačítko **Další** přejdete na kartu **Nastavení** .

Rozevírací seznam **Konfigurace** určuje konfiguraci sestavení, která se má nasadit. Výchozí hodnota je Release, což je to, co chcete.

Zrušte zaškrtnutí políčka **odebrat další soubory v cílovém umístění** . Vzhledem k tomu, že se jedná o vaše první nasazení, neexistují zatím žádné soubory v cílové složce.

V části **databáze** zadejte do pole Připojovací řetězec pro **SchoolContext**následující hodnotu:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample3.cmd)]

Proces nasazení vloží tento připojovací řetězec do nasazeného souboru Web. config, protože je vybrán **použít tento připojovací řetězec za běhu** .

Také v části **SchoolContext**vyberte **použít migrace Code First**. Tato možnost způsobí, že proces nasazení nakonfiguruje nasazený soubor Web. config a určí `MigrateDatabaseToLatestVersion` inicializátor. Tento inicializátor automaticky aktualizuje databázi na nejnovější verzi, když aplikace přistupuje k databázi poprvé po nasazení.

Do pole Připojovací řetězec pro **DefaultConnection**zadejte následující hodnotu:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample4.cmd)]

Ponechte vymazané **aktualizaci databáze** . Databáze členství bude nasazena zkopírováním souboru. SDF do aplikace\_data a nechcete, aby proces nasazení v této databázi udělal něco jiného.

![Publish_Web_wizard_Settings_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image13.png)

Kliknutím na tlačítko **Další** přejdete na kartu **Náhled** .

Na kartě **Náhled** klikněte na možnost **Spustit náhled** . zobrazí se seznam souborů, které budou zkopírovány.

![Publish_Web_wizard_Preview_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image14.png)

![Publish_Web_wizard_Preview_tab_Test_with_file_list](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image15.png)

Klikněte na **Publikovat**.

Pokud Visual Studio není v režimu správce, může se zobrazit chybová zpráva, která indikuje chybu oprávnění. V takovém případě zavřete Visual Studio, otevřete ho v režimu správce a zkuste publikování znovu.

Pokud je Visual Studio v režimu správce, okno **výstup** sestavy úspěšné sestavení a publikování.

![Output_window_publish_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image16.png)

Prohlížeč se automaticky otevře na domovské stránce společnosti Contoso University běžící ve službě IIS na místním počítači.

[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image17.png)

## <a name="testing-in-the-test-environment"></a>Testování v testovacím prostředí

Všimněte si, že indikátor prostředí zobrazuje "(test)" místo "(dev)", které ukazuje, že transformace *Web. config* pro indikátor prostředí byla úspěšná.

[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image19.png)

Spusťte stránku **Students** a ověřte, zda nasazená databáze nemá žádné studenty. Když vyberete tuto stránku, může trvat několik minut, než se načte, protože Code First vytvoří databázi a potom spustí metodu `Seed`. (Neudělal to, když jste na domovské stránce, protože aplikace se ještě nepokoušela o přístup k databázi.)

[![Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image21.png)

Spuštěním stránky **instruktory** ověřte, zda Code First dosazení databáze s daty instruktory:

[![Instructors_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image23.png)

Vyberte **Přidat studenty** z nabídky **Students** , přidejte studenta a potom zobrazte nového studenta na stránce **Students** , abyste ověřili, že můžete úspěšně zapisovat do databáze:

[![Add_Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image26.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image25.png)

[![Students_page_with_new_student_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image28.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image27.png)

V nabídce **kurzy** vyberte **aktualizovat kredity**. Stránka **aktualizovat kredity** vyžaduje oprávnění správce, aby se zobrazila stránka pro **přihlášení** . Zadejte přihlašovací údaje účtu správce, které jste vytvořili dříve ("admin" a "pas $ W0rd"). Zobrazí se stránka **aktualizace kredity** , která ověřuje, že účet správce, který jste vytvořili v předchozím kurzu, byl správně nasazen do testovacího prostředí.

[![Log_In_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image30.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image29.png)

[![Update_Credits_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image32.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image31.png)

Ověřte, zda existuje složka *knihovny elmah* s pouze zástupným souborem.

[![Elmah_folder_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image34.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image33.png)

<a id="efcfmigrations"></a>

## <a name="reviewing-the-automatic-webconfig-changes-for-code-first-migrations"></a>Probíhá kontrola automatických změn souboru Web. config pro Migrace Code First

Otevřete soubor *Web. config* v nasazené aplikaci na adrese *C:\inetpub\wwwroot\ContosoUniversity* a můžete zjistit, kde se proces nasazení nakonfiguroval migrace Code First k automatické aktualizaci databáze na nejnovější verzi.

![](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image35.png)

Proces nasazení také vytvořil nový připojovací řetězec pro Migrace Code First pro použití výhradně pro aktualizaci schématu databáze:

![DatabasePublish_connection_string](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image36.png)

Tento dodatečný připojovací řetězec umožňuje zadat jeden uživatelský účet pro aktualizace schématu databáze a jiný uživatelský účet pro přístup k datům aplikací. Můžete například přiřadit roli vlastníka databáze\_k Migrace Code First a k aplikaci DB\_DataReader a DB\_role datawrite. Jedná se o běžný způsob obrany, který brání potenciálně škodlivému kódu v aplikaci ve změně schématu databáze. (K tomu může dojít například při úspěšném útoku injektáže SQL.) Tento model tyto kurzy nepoužívá. Nevztahuje se na SQL Server Compact a neplatí při migraci na SQL Server v pozdějším kurzu v této sérii. Cytanium web nabízí jenom jeden uživatelský účet pro přístup k databázi SQL Server, kterou vytvoříte na Cytanium. Pokud ve svém scénáři máte možnost implementovat tento model, můžete to provést pomocí následujících kroků:

1. Na kartě **Nastavení** v průvodci **Publikovat web** zadejte připojovací řetězec, který určuje uživatele s úplnými oprávněními pro aktualizaci schématu databáze, a zrušte zaškrtnutí políčka **použít tento připojovací řetězec za běhu** . V nasazeném souboru Web. config se jedná o `DatabasePublish` připojovací řetězec.
2. Vytvořte transformaci souboru Web. config pro připojovací řetězec, který má aplikace používat v době běhu.

Nyní jste nasadili aplikaci do služby IIS na vývojovém počítači a otestovali ji. Tím se ověří, že proces nasazení zkopíroval obsah aplikace do správného umístění (kromě souborů, které jste nechtěli nasadit), a taky to, že Nasazení webu nakonfigurovaná služba IIS během nasazení správně. V dalším kurzu spustíte ještě jeden test, který najde úlohu nasazení, která ještě není hotová: nastavení oprávnění složky ve složce *knihovny elmah* .

## <a name="more-information"></a>Další informace

Informace o spuštění služby IIS nebo IIS Express v aplikaci Visual Studio naleznete v následujících zdrojích informací:

- [IIS Express přehledu](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) na webu IIS.NET.
- [Představujeme IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) na blogu Scottu Guthrie.
- [Postupy: určení webového serveru pro webové projekty v aplikaci Visual Studio](https://msdn.microsoft.com/library/ms178108.aspx).
- [Základní rozdíly mezi službou IIS a vývojovým serverem ASP.NET](../deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) na webu ASP.NET
- [Otestujte svoji ASP.NET MVC nebo aplikaci webových formulářů na IIS 7 za 30 sekund](https://blogs.msdn.com/b/rickandy/archive/2011/04/22/test-you-asp-net-mvc-or-webforms-application-on-iis-7-in-30-seconds.aspx) na blogu Rick Anderson. Tato položka poskytuje příklady, proč testování pomocí Cassini (Visual Studio Development Server) není tak spolehlivé jako testování v IIS Express a proč testování v IIS Express není tak spolehlivé jako testování ve službě IIS.

Informace o tom, jaké problémy mohou nastat, když vaše aplikace běží ve středním vztahu důvěryhodnosti, najdete v tématu [hostování aplikací ASP.NET ve středním vztahu důvěryhodnosti](http://www.4guysfromrolla.com/articles/100307-1.aspx) na 4 kyberbezpečnosti z webu Rolla.

> [!div class="step-by-step"]
> [Předchozí](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
> [Další](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
