---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
title: 'ASP.NET nasazení webu pomocí sady Visual Studio: nasazení do testu | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která bude Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí usin...
ms.author: riande
ms.date: 01/16/2019
ms.assetid: 8bf2c4fb-4ee5-4841-bfc2-03462c1f7a7a
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
msc.type: authoredcontent
ms.openlocfilehash: 738318cce442fdc5d58dd1e4c992d4941be2487e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74591243"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-test"></a>ASP.NET nasazení webu pomocí sady Visual Studio: nasazení do testování

tím, že [Dykstra](https://github.com/tdykstra)

V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která bude Azure App Service Web Apps nebo poskytovateli hostování třetí strany pomocí sady Visual Studio 2017. Informace o řadě najdete v [prvním kurzu v řadě](introduction.md).

Aktuální verzi nasazení do Azure najdete v tématu [Vytvoření webové aplikace v ASP.NET Core v Azure](/azure/app-service/app-service-web-get-started-dotnet).

## <a name="overview"></a>Přehled

V tomto kurzu nasadíte webovou aplikaci v ASP.NET do služby Internet Information Server (IIS) na místním počítači.

Obecně platí, že když vyvíjíte aplikaci, spustíte ji a otestujete ji v aplikaci Visual Studio. Ve výchozím nastavení používají projekty webové aplikace v aplikaci Visual Studio 2017 IIS Express jako vývojový webový server. IIS Express se chová podobně jako plná služba IIS, než vývojový server sady Visual Studio (označovaný také jako Cassini), který Visual Studio 2017 používá ve výchozím nastavení. Ale vývoj webového serveru nefunguje úplně stejně jako služba IIS. V důsledku toho může aplikace správně běžet a testovat v aplikaci Visual Studio, ale při nasazení do služby IIS dojde k chybě.

Můžete spolehlivě testovat aplikaci dvěma způsoby:

1. Nasaďte aplikaci do služby IIS na svém vývojovém počítači pomocí stejného procesu, který později použijete k jeho nasazení do provozního prostředí.

   Aplikaci Visual Studio můžete nakonfigurovat tak, aby používala službu IIS při spuštění webového projektu, ale to by nemohlo testovat proces nasazení. Tato metoda ověří váš proces nasazení a aplikace správně funguje v rámci služby IIS.

2. Nasaďte aplikaci do testovacího prostředí podobného vašemu provoznímu prostředí. 
 
   Provozní prostředí pro tyto kurzy je Web Apps v Azure App Service. Ideální testovací prostředí je další webová aplikace vytvořená ve službě Azure. I když by byl nastavený stejným způsobem jako produkční webová aplikace, měli byste ho použít jenom pro testování.

Možnost 2 je nejspolehlivější způsob testování. Pokud použijete možnost 2, nemusíte nutně používat možnost 1. Pokud však nasazujete pro poskytovatele hostingu třetí strany, možnost 2 nemusí být vhodná nebo může být náročná, takže v této sérii kurzů se zobrazují obě metody. Pokyny k možnosti 2 jsou k dispozici v kurzu [nasazení do provozního prostředí](deploying-to-production.md) .

Další informace o používání webových serverů v aplikaci Visual Studio naleznete v tématu [webové servery v aplikaci Visual Studio pro webové projekty ASP.NET](https://msdn.microsoft.com/library/58wxa9w5.aspx).

Připomenutí: Pokud obdržíte chybovou zprávu nebo něco nefunguje při procházení tohoto kurzu, zkontrolujte [stránku Poradce při potížích](troubleshooting.md).

## <a name="download-the-contoso-university-starter-project"></a>Stáhnout projekt contoso University Starter

Stáhněte a nainstalujte si řešení a projekt společnosti Contoso University Visual Studio Start. Toto řešení obsahuje dokončený kurz. 

[Stáhnout počáteční projekt](https://go.microsoft.com/fwlink/p/?LinkId=282627)

## <a name="install-iis"></a>Instalace služby IIS

Pokud chcete nasadit službu IIS na svém vývojovém počítači, zkontrolujte, že je nainstalovaná služba IIS a Nasazení webu. Ve výchozím nastavení Visual Studio nainstaluje Nasazení webu, ale služba IIS není zahrnutá ve výchozí konfiguraci Windows 10, Windows 8 nebo Windows 7. Pokud jste už službu IIS nainstalovali a výchozí fond aplikací už je nastavený na .NET 4, přejděte k [Další části](#sqlexpress).

1. Pro instalaci služby IIS a Nasazení webu doporučujeme použít [instalační program webové platformy (pracovního procesu)](https://www.microsoft.com/web/downloads/platform.aspx) . V případě potřeby nainstaluje služba pracovního procesu osvědčenou konfiguraci služby IIS, která zahrnuje požadavky služby IIS a Nasazení webu.

   Pokud jste již nainstalovali službu IIS, Nasazení webu nebo kteroukoli z požadovaných součástí, nainstaluje požadavek na instalaci pouze to, co chybí.

   * Pomocí instalačního programu webové platformy nainstalujte službu IIS a Nasazení webu:
    
     ![Instalace služby IIS pomocí procesu pracovního procesu](deploying-to-iis/_static/image30.png)

     ![Instalace Nasazení webu pomocí procesu pracovního procesu](deploying-to-iis/_static/image31.png)

     Zobrazí se zpráva oznamující, že se nainstaluje služba IIS 7. Odkaz funguje pro IIS 8 ve Windows 8; u systému Windows 8 a novějších verzí ale Projděte následující kroky, abyste se ujistili, že je nainstalovaná ASP.NET 4,7:

   * Otevřete **Ovládací panely** > **programy** > **programy a funkce** > **zapnout nebo vypnout funkce systému Windows**.

   * Rozbalte **Internetová informační služba**, **webové služby**a **funkce pro vývoj aplikací**.
   
   * Potvrďte, že je vybraná možnost **ASP.NET 4,7** .

     ![Vyberte ASP.NET 4,7](deploying-to-iis/_static/image1a.png)

   * Ověřte, zda je vybrána možnost **webové služby** a **Konzola pro správu služby IIS** . Tím se nainstaluje služba IIS a správce služby IIS.
    
     ![Vybrat webové služby](deploying-to-iis/_static/image24.png)    
  
   * Vyberte **OK**. Zobrazí se zprávy s dialogovým oknem, které indikují instalaci.

Po instalaci služby IIS spusťte **Správce služby IIS** , abyste se ujistili, že se k výchozímu fondu aplikací přiřadí .NET Framework verze 4.

1. Kliknutím na tlačítko WINDOWS + R otevřete dialogové okno **spuštění** .

   (V systému Windows 8 nebo novějším zadejte na **úvodní** stránce "Run" (spustit). V systému Windows 7 vyberte v nabídce **Start** možnost **Spustit** . Pokud příkaz **Spustit** není v nabídce **Start** , klikněte pravým tlačítkem myši na hlavní panel, vyberte možnost **vlastnosti**, vyberte kartu **Nabídka Start** , vyberte možnost **přizpůsobit**a vyberte možnost **Spustit příkaz**.)

2. Zadejte "inetmgr" a vyberte **OK**.

3. V podokně **připojení** rozbalte uzel server a vyberte **fondy aplikací**. V podokně **fondy aplikací** , pokud je aplikace **DefaultAppPool** přiřazena k rozhraní .NET Framework verze 4, jak je znázorněno na následujícím obrázku, přejděte k další části.

   ![Inetmgr_showing_4.0_app_pools](deploying-to-iis/_static/image5a.png)

4. Pokud vidíte pouze dva fondy aplikací a obě jsou nastaveny na .NET Framework 2,0, nainstalujte ASP.NET 4 do služby IIS.

   V systému Windows 8 nebo novějším se podívejte na předchozí část s pokyny pro zajištění, že je nainstalovaná verze ASP.NET 4,7, nebo si přečtěte, [Jak nainstalovat ASP.NET 4,5 v systému Windows 8 a Windows Server 2012](https://support.microsoft.com/kb/2736284). V případě systému Windows 7 otevřete okno příkazového řádku kliknutím pravým tlačítkem myši na **příkazový řádek** v nabídce **Start** systému Windows a výběrem možnosti **Spustit jako správce**. Spuštěním příkazu [aspnet\_regiis. exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx) nainstalujete ASP.NET 4 do služby IIS pomocí následujících příkazů. (V 32 systémech nahraďte "Framework64" rozhraním "Framework".)

   [!code-console[Main](deploying-to-iis/samples/sample1.cmd)]

   Tento příkaz vytvoří nové fondy aplikací pro .NET Framework 4, výchozí fond aplikací však zůstane nastaven na 2,0. Nasazujete aplikaci, která se zaměřuje na rozhraní .NET 4, do tohoto fondu aplikací, takže změňte fond aplikací na .NET 4.

5. Pokud jste **Správce služby IIS**zavřeli, spusťte ho znovu, rozbalte uzel serveru a vyberte **fondy aplikací**.

6. V podokně **fondy aplikací** vyberte možnost **DefaultAppPool**. V podokně **Akce** vyberte **základní nastavení**.

   ![Inetmgr_selecting_Basic_Settings_for_app_pool](deploying-to-iis/_static/image25.png)

7. V dialogovém okně **Upravit fond aplikací** změňte **verzi .NET CLR** na **.NET CLR v 4.0.30319**. Vyberte **OK**.

   ![Selecting_. NET_4_for_DefaultAppPool](deploying-to-iis/_static/image6a.png)

Nyní jste připraveni publikovat webovou aplikaci do služby IIS. Nejprve však vytvořte databáze pro testování.

<a id="sqlexpress"></a>

## <a name="install-sql-server-express"></a>Nainstalovat SQL Server Express

LocalDB není navržený tak, aby fungoval ve službě IIS, takže vaše testovací prostředí musí mít nainstalovaný SQL Server Express. Pokud používáte Visual Studio 2010 SQL Server Express, je již ve výchozím nastavení nainstalován. Pokud používáte Visual Studio 2012 nebo novější, nainstalujte SQL Server Express.

Pokud chcete nainstalovat SQL Server Express, Stáhněte si ho a nainstalujte si ho z [webu Download Center: Microsoft SQL Server 2017 Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express). 

Na první stránce centra instalace SQL Server vyberte **nový SQL Server samostatnou instalaci nebo přidejte funkce do existující instalace** a postupujte podle pokynů pro přijetí výchozích možností. V Průvodci instalací přijměte výchozí nastavení. Další informace o možnostech instalace najdete v tématu [instalace SQL Server v Průvodci instalací (nastavení)](https://msdn.microsoft.com/library/ms143219.aspx).

## <a name="create-sql-server-express-databases-for-the-test-environment"></a>Vytvoření databází SQL Server Express pro testovací prostředí

Aplikace Contoso University má dvě databáze: 

1. Databáze členství 
2. Aplikační databáze 

Tyto databáze můžete nasadit do dvou samostatných databází nebo do jediné databáze. Jejich kombinování usnadňuje spojení s databází. 

Pokud nasazujete pro poskytovatele hostingu třetí strany, váš plán hostování vám také může poskytnout důvod, jak je kombinovat. Zprostředkovatel může například účtovat více databází více nebo nemusí dokonce umožňovat více než jednu databázi.

V tomto kurzu nasadíte do dvou databází v testovacím prostředí a do jedné databáze v pracovním prostředí a v produkčním prostředí.

V nabídce **zobrazení** v aplikaci Visual Studio vyberte možnost **Průzkumník serveru** (**Průzkumník databáze** v aplikaci Visual Web Developer). Klikněte pravým tlačítkem na **datová připojení** a vyberte **vytvořit novou SQL Server databázi**.

![Selecting_Create_New_SQL_Server_Database](deploying-to-iis/_static/image8.png)

V dialogovém okně **vytvořit novou databázi SQL Server** do pole **název serveru** zadejte ".\SQLEXPRESS" a do pole **název nové databáze** zadejte "ASPNET-ContosoUniversity". Vyberte **OK**.

![Vytvoření ASPNET-ContosoUniversity](deploying-to-iis/_static/image9.png)

Použijte stejný postup k vytvoření nové databáze SQL Server Express School s názvem `ContosoUniversity`.

**Průzkumník serveru** zobrazí dvě nové databáze.

![Nové databáze v Průzkumník serveru](deploying-to-iis/_static/image10.png)

## <a name="create-a-grant-script-for-the-new-databases"></a>Vytvoření skriptu udělení pro nové databáze

Když je aplikace spuštěna ve službě IIS ve vývojovém počítači, aplikace používá k přístupu k databázi výchozí přihlašovací údaje fondu aplikací. Ve výchozím nastavení ale fond aplikací nemá oprávnění k otevření databází. To znamená, že pro udělení tohoto oprávnění musíte spustit skript. V této části vytvoříte skript a spustíte ho později, abyste se ujistili, že aplikace může otevírat databáze při spuštění ve službě IIS.

V textovém editoru zkopírujte následující příkazy SQL do nového souboru a uložte ho jako *grant. SQL*. 

[!code-sql[Main](deploying-to-iis/samples/sample2.sql)]

V aplikaci Visual Studio otevřete řešení contoso University. Klikněte pravým tlačítkem na řešení (ne na jeden z projektů) a vyberte **Přidat**. Vyberte možnost **existující položka**, přejděte k položce *grant. SQL*a otevřete ji.

> [!NOTE]
> Tento skript je navržený tak, aby fungoval s SQL Server Express 2012 nebo novějším a s nastavením služby IIS ve Windows 10, Windows 8 nebo Windows 7, jak jsou uvedeny v tomto kurzu. Pokud používáte jinou verzi SQL Server nebo Windows nebo pokud jste v počítači nastavili službu IIS odlišně, může se stát, že se budou vyžadovat změny v tomto skriptu. Další informace o SQL Server skriptů naleznete v tématu [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511).

> [!NOTE] 
> **Poznámka k zabezpečení** Tento skript poskytuje `db_owner` oprávnění uživateli, který přistupuje k databázi v době běhu, což je to, co budete mít v produkčním prostředí. V některých scénářích můžete chtít zadat uživatele, který má úplná oprávnění aktualizace schématu databáze jenom pro nasazení, a určit pro dobu běhu jiného uživatele, který má oprávnění jenom pro čtení a zápis dat. Další informace najdete v tématu [Kontrola automatických změn souboru Web. config pro migrace Code First](#reviewingmigrations) dále v tomto kurzu.

<a id="publish"></a>

## <a name="run-the-grant-script-in-the-application-database"></a>Spuštění skriptu udělení v aplikační databázi

Profil publikování můžete nakonfigurovat tak, aby během nasazení spouštěl skript grant v databázi členství, protože toto nasazení databáze používá poskytovatele [dbDacFx](https://docs.microsoft.com/iis/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing) . Během nasazování Migrace Code First nemůžete spouštět skripty, což je způsob nasazení aplikační databáze. To znamená, že před nasazením v aplikační databázi musíte ručně spustit skript.

1. V aplikaci Visual Studio otevřete soubor *grant. SQL* , který jste vytvořili dříve.

2. Vyberte **připojit**. 

    ![Tlačítko připojit](deploying-to-iis/_static/image11.png)

3. V dialogovém okně **připojit k serveru** jako **název serveru**zadejte *.\SQLEXPRESS* . Vyberte **připojit**.

4. V rozevíracím seznamu databáze vyberte **ContosoUniversity**. Vyberte **provést**. 

   ![](deploying-to-iis/_static/image12.png)

Výchozí identita fondu aplikací nyní má dostatečná oprávnění v databázi aplikace, aby bylo možné Migrace Code First vytvořit tabulky databáze při spuštění aplikace.

## <a name="publish-to-iis"></a>Publikování ve službě IIS

Existuje několik způsobů, jak můžete nasadit do služby IIS pomocí sady Visual Studio a Nasazení webu:

* Použijte možnost publikování jedním kliknutím v aplikaci Visual Studio.
* Publikování z příkazového řádku.
* Vytvořte balíček pro nasazení a nainstalujte ho pomocí Správce služby IIS. Balíček má soubor. zip se všemi soubory a metadaty, které jsou potřeba k instalaci lokality ve službě IIS.
* Vytvořte balíček pro nasazení a nainstalujte ho pomocí příkazového řádku.

Proces, který jste provedli v předchozích kurzech k nastavení sady Visual Studio pro automatizaci úloh nasazení, se vztahuje na všechny tyto metody. V těchto kurzech použijete první dvě metody. Informace o použití balíčků pro nasazení najdete v tématu [nasazení webové aplikace vytvořením a instalací balíčku pro nasazení](https://go.microsoft.com/fwlink/p/?LinkId=282413#package) webu v mapě obsahu nasazení webu pro Visual Studio a ASP.NET.

Před publikováním se ujistěte, že používáte aplikaci Visual Studio v režimu správce. Pokud v záhlaví nevidíte **(správce)** , zavřete Visual Studio. Na **úvodní** stránce Windows 8 (nebo novější) nebo v nabídce **Start** systému Windows 7 klikněte pravým tlačítkem myši na ikonu sady Visual Studio a vyberte možnost **Spustit jako správce**. Režim správce je vyžadován pouze k publikování při publikování do služby IIS v místním počítači.

### <a name="create-the-publish-profile"></a>Vytvořit profil publikování

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt **ContosoUniversity** (ne na projekt **ContosoUniversity. dal** ). Vyberte **publikovat**. Zobrazí se stránka **publikování** .

2. Vyberte **Nový profil**. Zobrazí se dialogové okno **vybrat cíl publikování** .

3. Vyberte **IIS, FTP atd**. Vyberte **vytvořit profil**. Zobrazí se průvodce **publikováním** .

   ![Karta profil Průvodce publikováním webu](deploying-to-iis/_static/image26.png)

4. V rozevírací nabídce **Metoda publikování** vyberte možnost **nasazení webu**.

5. Jako **Server**zadejte *localhost*.

6. Jako **název lokality**zadejte *Default Web site/ContosoUniversity*.

7. Jako **cílovou adresu URL**zadejte *http://localhost/ContosoUniversity* .

   Nastavení **cílové adresy URL** není vyžadováno. Když Visual Studio dokončí nasazení aplikace, automaticky otevře výchozí prohlížeč na této adrese URL. Pokud nechcete, aby se prohlížeč po nasazení otevřel automaticky, nechejte toto pole prázdné.

8. Vyberte **ověřit připojení** , abyste ověřili, že jsou nastavení správná, a můžete se připojit ke službě IIS v místním počítači.

   Zelená značka zaškrtnutí ověří, že připojení proběhlo úspěšně.

   ![Karta pro připojení Průvodce publikováním webu](deploying-to-iis/_static/image27.png)

9. Kliknutím na tlačítko **Další** přejdete na kartu **Nastavení** .

10. Rozevírací seznam **Konfigurace** určuje konfiguraci sestavení, která se má nasadit. Nechte nastavenou na výchozí hodnotu **vydaná verze**. V tomto kurzu nebudete nasazovat sestavení pro ladění.

11. Rozbalte položku **Možnosti publikování souboru**. Vyberte **vyloučit soubory ze složky\_dat aplikace**.

    V testovacím prostředí aplikace přistupuje k databázím, které jste vytvořili v místní instanci SQL Server Express, nikoli v souborech MDF ve složce *App\_data* .

12. Nechte **předkompilovat během publikování** a zrušte zaškrtnutí políček **odebrat další soubory v cílovém umístění** .

    ![Možnosti publikování souboru na kartě nastavení](deploying-to-iis/_static/image15a.png)

    Předkompilace je možnost, která je užitečná hlavně pro velké weby. Může zkrátit čas spuštění při prvním vyžádání stránky po publikování webu.

    Nemusíte odebírat další soubory, protože se jedná o vaše první nasazení a zatím neexistují žádné soubory v cílové složce.

    > [!NOTE] 
    > Pokud pro následné nasazení na stejnou lokalitu vyberete možnost **odebrat další soubory v cíli** , ujistěte se, že jste používali funkci Preview, abyste viděli, které soubory se před nasazením odstraní. Očekávané chování je, že Nasazení webu odstraní soubory na cílovém serveru, který jste odstranili v projektu. Porovnává se ale celá struktura složek ve zdrojové a cílové složce. a v některých případech může Nasazení webu odstranit soubory, které nechcete odstranit.
    > 
    > Například pokud máte webovou aplikaci v podsložce na serveru, když nasadíte projekt do kořenové složky, podsložka bude odstraněna. Můžete mít jeden projekt pro hlavní web na contoso.com a jiný projekt pro blog na contoso.com/blog. Aplikace blogu je v podsložce. Pokud při nasazení hlavní lokality vyberete možnost **odebrat další soubory v cíli** , aplikace blogu se odstraní.
    > 
    > Pro jiný příklad se může stát, že se vaše aplikace\_datovou složku neočekávaně odstranila. Některé databáze, například soubory databáze SQL Server Compact Store ve složce App\_data. Po počátečním nasazení nechcete uchovávat soubory databáze v následných nasazeních, takže vyberete **vyloučit aplikace\_data** na kartě Balení/publikování webu. Pokud jste vybrali možnost **odebrat další soubory v cílovém umístění** , vaše soubory databáze a aplikace\_data samotné se odstraní při příštím publikování.

### <a name="configure-deployment-for-the-membership-database"></a>Konfigurace nasazení pro databázi členství

Následující postup platí pro databázi **DefaultConnection** v části **databáze** dialogového okna.

1. Do pole **řetězec vzdáleného připojení** zadejte následující připojovací řetězec, který odkazuje na novou SQL Server Express databázi členství.

   [!code-console[Main](deploying-to-iis/samples/sample3.cmd)]

   Proces nasazení vloží tento připojovací řetězec do nasazeného souboru Web. config, protože je vybrán **použít tento připojovací řetězec za běhu** .

    Připojovací řetězec můžete také získat z **Průzkumník serveru**. V **Průzkumník serveru**rozbalte **datová připojení** a vyberte **&lt;nazev_pocitace&gt;\SQLExpress.ASPNET-ContosoUniversity** databázi a potom v okně **vlastnosti** Zkopírujte hodnotu **připojovacího řetězce** . Tento připojovací řetězec bude mít jedno další nastavení, které můžete odstranit: `Pooling=False`.

2. Vyberte **aktualizovat databázi**.

   Tím dojde k vytvoření schématu databáze v cílové databázi během nasazování. V části Další kroky zadáte další skripty, které je třeba spustit: jeden pro udělení přístupu k databázi výchozímu fondu aplikací a jeden pro nasazení dat.

3. Vyberte **Konfigurovat aktualizace databáze**.
 
4. V dialogovém okně **Konfigurovat aktualizace databáze** vyberte **Přidat skript SQL**. Přejděte do skriptu *grant. SQL* , který jste předtím uložili ve složce řešení.

5. Opakujte postup pro přidání skriptu *ASPNET-data-dev. SQL* .

   ![Konfigurace aktualizací databáze pro databázi členství](deploying-to-iis/_static/image16.png)

6. Vyberte **Zavřít**.

### <a name="configure-deployment-for-the-application-database"></a>Konfigurace nasazení pro databázi aplikace

Když aplikace Visual Studio zjistí třídu Entity Framework `DbContext`, vytvoří položku v sekci **databáze** , která má zaškrtávací políčko **Spustit migrace Code First** místo zaškrtávacího políčka **databáze aktualizace** . V tomto kurzu použijete toto zaškrtávací políčko k určení Migrace Code Firstho nasazení.

V některých scénářích můžete použít databázi `DbContext`, ale chcete použít poskytovatele dbDacFx místo migrace k nasazení databáze. V takovém případě si přečtěte téma [návody nasazení Code First databáze bez migrace?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) v nejčastějších dotazech k nasazení webu ASP.NET na webu MSDN.

Následující postup platí pro databázi **SchoolContext** v části **databáze** dialogového okna.

1. Do pole **řetězec vzdáleného připojení** zadejte následující připojovací řetězec, který odkazuje na novou SQL Server Express aplikační databázi.

   [!code-console[Main](deploying-to-iis/samples/sample4.cmd)]

   Proces nasazení vloží tento připojovací řetězec do nasazeného souboru Web. config, protože je vybrán **použít tento připojovací řetězec za běhu** .

   Připojovací řetězec aplikační databáze můžete také získat z **Průzkumník serveru** stejným způsobem jako připojovací řetězec databáze členství.

2. Vyberte **Execute migrace Code First (spouští se při spuštění aplikace)** .

   Tato možnost způsobí, že proces nasazení nakonfiguruje nasazený soubor Web. config a určí `MigrateDatabaseToLatestVersion` inicializátor. Tento inicializátor automaticky aktualizuje databázi na nejnovější verzi, když aplikace přistupuje k databázi poprvé po nasazení.

### <a name="configure-publish-profile-transforms"></a>Konfigurace transformací profilů publikování

1. Vyberte **Zavřít**. Když se zobrazí dotaz, jestli chcete změny uložit, vyberte **Ano** .

2. V **Průzkumník řešení**rozbalte položku **vlastnosti**a pak rozbalte **PublishProfiles**.

3. Klikněte pravým tlačítkem na *CustomProfile. pubxml* a přejmenujte ho *test. pubxml*.

4. Klikněte pravým tlačítkem na *test. pubxml*. Vyberte **přidat konfigurační transformaci**.

   ![Přidat konfigurační nabídku pro transformaci](deploying-to-iis/_static/image17.png)

   Visual Studio vytvoří transformační soubor *Web. test. config* a otevře jej.

5. V transformačním souboru *Web. test. config* vložte následující kód hned za úvodní značku konfigurace.

   [!code-xml[Main](deploying-to-iis/samples/sample5.xml)]

    Když použijete profil publikování testu, tato transformace nastaví indikátor prostředí na "test". V nasazeném webu uvidíte "(test)" za nadpisem "contoso University" H1.

6. Soubor uložte a zavřete.

7. Klikněte pravým tlačítkem myši na soubor *Web. test. config* a vyberte možnost **Náhled transformace** , abyste se ujistili, že transformace, kterou jste zakódujete, poskytuje očekávané změny.

    V okně **Náhled Web. config** se zobrazí výsledek použití transformací *Web. Release. config* a transformací *Web. test. config* .

### <a name="preview-the-deployment-updates"></a>Náhled aktualizací nasazení

1. Znovu spusťte průvodce **publikováním webu** (klikněte pravým tlačítkem myši na projekt ContosoUniversity, vyberte **publikovat**a pak na **Náhled**).

2. V dialogovém okně **Náhled** vyberte možnost **Spustit náhled** , chcete-li zobrazit seznam souborů, které budou zkopírovány. 

   ![Publikování náhledu](deploying-to-iis/_static/image29.png)

   Můžete také vybrat odkaz **databáze verze Preview** a zobrazit skripty, které se spustí v databázi členství. (Nejsou spouštěny žádné skripty pro nasazení Migrace Code First, takže není k dispozici žádné zobrazení databáze aplikace.)

3. Vyberte **publikovat**.

   Pokud Visual Studio není v režimu správce, může se zobrazit chybová zpráva s oprávněním. V takovém případě zavřete Visual Studio, otevřete ho v režimu správce a zkuste publikování znovu.

   Pokud je Visual Studio v režimu správce, okno **výstup** sestavy úspěšné sestavení a publikování.

   ![Output_window_publish_Test](deploying-to-iis/_static/image20.png)

   Pokud jste zadali adresu URL do pole **cílová adresa URL** na kartě **připojení** profilu publikování, prohlížeč se automaticky otevře na domovské stránce společnosti Contoso University běžící ve službě IIS na vašem počítači.

## <a name="test-in-the-test-environment"></a>Testování v testovacím prostředí

Všimněte si, že indikátor prostředí zobrazuje "(test)" místo "(dev)", což ukazuje, že transformace *Web. config* pro indikátor prostředí byla úspěšná.

Spuštěním stránky **instruktory** ověřte, zda Code First dosazení databáze s daty instruktory. Když vyberete tuto stránku, může trvat několik minut, než se načtou, protože Code First vytvoří databázi a potom spustí metodu `Seed`. (Neudělal to, když jste na domovské stránce, protože aplikace se ještě nepokoušela o přístup k databázi.)

Vyberte kartu **studenti** a ověřte, zda nasazená databáze nemá žádné studenty.

V nabídce **Students** vyberte **Přidat studenty** . Přidejte studenta a pak na stránce **Students** Zobrazte nového studenta. Tím ověříte, že můžete úspěšně zapisovat do databáze.

V nabídce **kurzy** vyberte **aktualizovat kredity**. Stránka **aktualizovat kredity** vyžaduje oprávnění správce, aby se zobrazila stránka pro **přihlášení** . Zadejte přihlašovací údaje účtu správce, které jste vytvořili dříve ("admin" a "devpwd"). Zobrazí se stránka **aktualizovat kredity** . Tím ověříte, že účet správce, který jste vytvořili v předchozím kurzu, byl správně nasazen do testovacího prostředí.

Ověřte, že složka *knihovny elmah* ve složce *c:\inetpub\wwwroot\ContosoUniversity* existuje pouze s zástupným souborem.

<a id="reviewingmigrations"></a>

## <a name="review-the-automatic-webconfig-changes-for-code-first-migrations"></a>Zkontrolujte automatické změny souboru Web. config pro Migrace Code First

Otevřete soubor *Web. config* v nasazené aplikaci na adrese *C:\inetpub\wwwroot\ContosoUniversity* a můžete zjistit, kde se proces nasazení nakonfiguroval migrace Code First k automatické aktualizaci databáze na nejnovější verzi.

![](deploying-to-iis/_static/image21.png)

Proces nasazení také vytvořil nový připojovací řetězec pro Migrace Code First pro použití výhradně pro aktualizaci schématu databáze:

![Připojovací řetězec Database_Publish](deploying-to-iis/_static/image22.png)

Tento dodatečný připojovací řetězec umožňuje zadat jeden uživatelský účet pro aktualizace schématu databáze a jiný uživatelský účet pro přístup k datům aplikací. Můžete například přiřadit roli **vlastníka databáze\_** migrace Code First a **DB\_DataReader** s DB\_rolemi **datawrite** do aplikace. Jedná se o běžný způsob obrany, který brání potenciálně škodlivému kódu v aplikaci ve změně schématu databáze. (K tomu může dojít například při úspěšném útoku injektáže SQL.) Tyto kurzy tento model nepoužívají. K implementaci tohoto modelu ve vašem scénáři proveďte tyto kroky:

1. V průvodci **publikování webu** na kartě **Nastavení** zadejte připojovací řetězec, který určuje uživatele s úplnými oprávněními pro aktualizaci schématu databáze. Zrušte zaškrtnutí políčka **použít tento připojovací řetězec za běhu** . V nasazeném souboru Web. config se jedná o `DatabasePublish` připojovací řetězec.

2. Vytvořte transformaci souboru Web. config pro připojovací řetězec, který má aplikace používat v době běhu.

## <a name="summary"></a>Přehled

Nyní jste nasadili aplikaci do služby IIS na vývojovém počítači a otestovali ji.

![Domovská stránka v testu](deploying-to-iis/_static/image23.png)

Tím se ověří, že proces nasazení zkopíroval obsah aplikace do správného umístění (kromě souborů, které jste nechtěli nasadit), a taky to, že Nasazení webu nakonfigurovaná služba IIS během nasazení správně. V dalším kurzu spustíte ještě jeden test, který najde úlohu nasazení, která ještě není hotová: nastavení oprávnění složky ve složce *Elm Ah* .

## <a name="more-information"></a>Další informace

Informace o spuštění služby IIS nebo IIS Express v aplikaci Visual Studio naleznete v následujících zdrojích informací:

- [IIS Express přehledu](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) na webu IIS.NET.
- [Představujeme IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) na blogu Scottu Guthrie.
- [Webové servery v aplikaci Visual Studio pro webové projekty ASP.NET](https://msdn.microsoft.com/library/58wxa9w5.aspx).
- [Základní rozdíly mezi službou IIS a vývojovým serverem ASP.NET](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) na webu ASP.NET

Informace o tom, jaké problémy mohou nastat, když vaše aplikace běží ve středním vztahu důvěryhodnosti, najdete v tématu [hostování aplikací ASP.NET ve středním vztahu důvěryhodnosti](http://www.4guysfromrolla.com/articles/100307-1.aspx) na čtyřech kyberbezpečnosti z webu Rolla.

> [!div class="step-by-step"]
> [Předchozí](project-properties.md)
> [Další](setting-folder-permissions.md)
