---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
title: 'ASP.NET nasazení webu pomocí sady Visual Studio: nasazení do produkčního prostředí | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která bude Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 416438a1-3b2f-4d27-bf53-6b76223c33bf
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
msc.type: authoredcontent
ms.openlocfilehash: ddc3d15f0436c4c3a24491cf0377111768da67df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78632781"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-production"></a>ASP.NET nasazení webu pomocí sady Visual Studio: nasazení do produkčního prostředí

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která umožňuje Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí sady Visual Studio 2012 nebo Visual Studio 2010. Informace o řadě najdete v [prvním kurzu v řadě](introduction.md).

## <a name="overview"></a>Přehled

V tomto kurzu nastavíte Microsoft Azure účet, vytvoříte pracovní a produkční prostředí a nasadíte webovou aplikaci v ASP.NET do pracovního a produkčního prostředí pomocí funkce publikování jedním kliknutím sady Visual Studio.

Pokud chcete, můžete nasadit poskytovatele hostingu třetí strany. Většina postupů popsaných v tomto kurzu je stejná pro poskytovatele hostingu nebo pro Azure, s tím rozdílem, že každý zprostředkovatel má vlastní uživatelské rozhraní pro účet a správu webu. Poskytovatele hostingu můžete najít v [galerii poskytovatelů](https://www.microsoft.com/web/hosting) na webu Microsoft.com.

Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje při procházení kurzu, nezapomeňte na stránce věnované řešení potíží v této sérii kurzů.

## <a name="get-a-microsoft-azure-account"></a>Získat účet Microsoft Azure

Pokud ještě nemáte účet Azure, můžete si během několika minut vytvořit bezplatný zkušební účet. Podrobnosti najdete v tématu [Bezplatná zkušební verze Azure](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).

## <a name="create-a-staging-environment"></a>Vytvoření přípravného prostředí

> [!NOTE]
> Od napsání tohoto kurzu Azure App Service přidat novou funkci pro automatizaci mnoha procesů pro vytváření pracovních a produkčních prostředí. Viz [Nastavení přípravného prostředí pro webové aplikace v Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-staged-publishing/).

Jak je vysvětleno v [kurzu nasazení do testovacího prostředí](deploying-to-iis.md), nejspolehlivější testovací prostředí je web na poskytovateli hostingu, který je stejně jako produkční Web. U mnoha poskytovatelů hostingu byste si museli zvážit výhody těchto výhod s významnými dodatečnými náklady, ale v Azure můžete vytvořit další bezplatnou webovou aplikaci jako svou pracovní aplikaci. Potřebujete také databázi a další výdaje za to, že náklady na provozní databázi budou být buď žádné, nebo minimální. V Azure platíte za velikost databázového úložiště, které místo pro každou databázi použijete, a množství dalšího úložiště, které budete používat v pracovním prostoru, bude minimální.

Jak je vysvětleno v [kurzu nasazení do testovacího prostředí](deploying-to-iis.md), v části fázování a výroba budete nasazovat své dvě databáze do jedné databáze. Pokud jste si chtěli ponechat oddělení oddělené, proces bude stejný s tím rozdílem, že byste pro každé prostředí vytvořili další databázi a při vytváření profilu publikování vyberete správný cílový řetězec pro každou databázi.

V této části kurzu vytvoříte webovou aplikaci a databázi pro použití v přípravném prostředí a před vytvořením a nasazením do provozního prostředí nasadíte do přípravy a otestování.

> [!NOTE]
> Následující kroky ukazují, jak vytvořit webovou aplikaci v Azure App Service pomocí portálu pro správu Azure. V nejnovější verzi sady Azure SDK můžete to provést také bez nutnosti opustit sadu Visual Studio pomocí Průzkumník serveru. V Visual Studio 2013 můžete také vytvořit webovou aplikaci přímo z dialogového okna publikovat. Další informace najdete v tématu [Vytvoření webové aplikace v ASP.NET v Azure App Service.](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)

1. V [portál pro správu Azure](https://manage.windowsazure.com/)klikněte na **weby**a pak klikněte na **Nový**.
2. Klikněte na **Web**a potom na **vlastní vytvořit**.

    **Nový web – otevře se Průvodce vytvořením vlastního webu** . **Vlastní Průvodce vytvořením** umožňuje vytvořit web a databázi ve stejnou dobu.
3. V kroku průvodce **vytvořit web** zadejte do pole **Adresa URL** řetězec, který chcete použít jako jedinečnou adresu URL přípravného prostředí vaší aplikace. Například zadejte ContosoUniversity-staging123 (včetně náhodných čísel na konci, aby byl jedinečný v případě, že je provedena ContosoUniversity – fázování).

    Úplná adresa URL bude obsahovat informace o tom, co zadáte, a příponu, která se zobrazí vedle textového pole.
4. V rozevíracím seznamu **oblast** vyberte oblast, která je pro vás nejblíže.

    Toto nastavení určuje, v jakém datovém centru bude webová aplikace běžet.
5. V rozevíracím seznamu **databáze** vyberte **vytvořit novou databázi SQL**.
6. V poli **název připojovacího řetězce databáze** ponechte výchozí hodnotu *DefaultConnection*.
7. Klikněte na šipku, která odkazuje na pravou stranu v poli.

    Následující ilustrace znázorňuje dialog **vytvořit web** s ukázkovými hodnotami v něm. Adresa URL a oblast, které jste zadali, se liší.

    ![Vytvořit krok webu](deploying-to-production/_static/image1.png)

    Průvodce přejde na krok **zadat nastavení databáze** .
8. Do pole **název** zadejte *ContosoUniversity* a náhodné číslo, které má být jedinečné, například *ContosoUniversity123*.
9. V poli **Server** vyberte **Nový SQL Database Server**.
10. Zadejte jméno správce a heslo.

    Sem nezadáváte existující jméno a heslo. Zadáváte nový název a heslo, které teď definujete pro pozdější použití, až budete chtít získat přístup k databázi.
11. V poli **oblast** vyberte stejnou oblast, kterou jste zvolili pro webovou aplikaci.

    Zachování webového serveru a databázového serveru ve stejné oblasti vám dává nejlepší výkon a minimalizuje náklady.
12. Kliknutím na značku zaškrtnutí v dolní části pole označíte, že jste hotovi.

    Následující ilustrace znázorňuje dialog **zadat nastavení databáze** s ukázkovými hodnotami v něm. Hodnoty, které jste zadali, se můžou lišit.

    ![Krok nastavení databáze nového webu – Průvodce vytvořením databáze](deploying-to-production/_static/image2.png)

    Portál pro správu se vrátí na stránku websites a ve sloupci **stav** se zobrazí, že se webová aplikace vytváří. Po delší dobu (obvykle méně než minutu) se ve sloupci **stav** zobrazí, že se webová aplikace úspěšně vytvořila. V navigačním panelu vlevo se počet webových aplikací, které máte ve vašem účtu, zobrazuje vedle ikony **websites** a počet databází se zobrazí vedle ikony **databáze SQL** .

    ![Stránka webů Portál pro správu, vytvořený web](deploying-to-production/_static/image3.png)

    Název vaší webové aplikace se bude lišit od ukázkové aplikace na obrázku.

## <a name="deploy-the-application-to-staging"></a>Nasazení aplikace do přípravy

Teď, když jste vytvořili webovou aplikaci a databázi pro testovací prostředí, můžete do ní nasadit projekt.

> [!NOTE]
> Tyto pokyny ukazují, jak vytvořit profil publikování stažením souboru *. publishsettings* , který funguje nejen pro Azure, ale také pro poskytovatele hostingu třetích stran. Nejnovější sada Azure SDK také umožňuje přímo se připojit k Azure ze sady Visual Studio a vybírat ze seznamu webových aplikací, které máte ve vašem účtu Azure. V Visual Studio 2013 se můžete přihlásit k Azure z dialogového okna **publikování na webu** nebo z okna **Průzkumník serveru** . Další informace najdete v tématu [Vytvoření webové aplikace v ASP.NET v Azure App Service](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).

### <a name="download-the-publishsettings-file"></a>Stažení souboru. publishsettings

1. Klikněte na název webové aplikace, kterou jste právě vytvořili.

    ![Kliknutím na lokalitu přejdete na řídicí panel.](deploying-to-production/_static/image4.png)
2. V části **rychlý přehled** na kartě **řídicí panel** klikněte na **Stáhnout profil publikování**.

    ![Stáhnout odkaz na profil publikování](deploying-to-production/_static/image5.png)

    Tento krok stáhne soubor, který obsahuje všechna nastavení, která potřebujete k nasazení aplikace do vaší webové aplikace. Tento soubor naimportujete do sady Visual Studio, takže tyto informace nebudete muset zadávat ručně.
3. Uložte soubor *. publishsettings* do složky, ke které máte přístup ze sady Visual Studio.

    ![ukládání souboru. publishsettings](deploying-to-production/_static/image6.png)

    > [!WARNING]
    > Zabezpečení – soubor *. publishsettings* obsahuje vaše přihlašovací údaje (nekódované), které se používají ke správě předplatných a služeb Azure. Osvědčeným postupem zabezpečení pro tento soubor je uložit ho dočasně mimo vaše zdrojové adresáře (například ve složce Libraries\Documents) a po dokončení importu ho odstranit. Uživatel se zlými úmysly, který získá přístup k souboru *. publishsettings* , může upravit, vytvořit a odstranit vaše služby Azure.

### <a name="create-a-publish-profile"></a>Vytvořit profil publikování

1. V aplikaci Visual Studio klikněte pravým tlačítkem na projekt ContosoUniversity v **Průzkumník řešení** a v místní nabídce vyberte **publikovat** .

    Otevře se průvodce **publikováním webu** .
2. Klikněte na kartu **profil** .
3. Klikněte na **Importovat**.
4. Přejděte do souboru *. publishsettings* , který jste stáhli dříve, a pak klikněte na **otevřít**.

    ![Dialogové okno Importovat nastavení publikování](deploying-to-production/_static/image7.png)
5. Na kartě **připojení** klikněte na **ověřit připojení** a ujistěte se, že jsou nastavení správná.

    Po ověření připojení se zobrazí zelená značka zaškrtnutí vedle tlačítka **ověřit připojení** .

    U některých poskytovatelů hostingu se po kliknutí na **ověřit připojení**může zobrazit dialogové okno s **chybou certifikátu** . Pokud tak učiníte, ověřte, že název serveru je očekávaný. Pokud je název serveru správný, vyberte **Uložit tento certifikát pro budoucí relace sady Visual Studio** a klikněte na **přijmout**. (Tato chyba znamená, že se poskytovatel hostingu rozhodl vyhnout se nákladům na nákup certifikátu SSL pro adresu URL, na kterou nasazujete. Pokud dáváte přednost navázání zabezpečeného připojení pomocí platného certifikátu, obraťte se na svého poskytovatele hostingu.)
6. Klikněte na **Další**.

    ![ikona úspěšného připojení a tlačítko Další na kartě připojení](deploying-to-production/_static/image8.png)
7. Na kartě **Nastavení** rozbalte **možnost publikování souboru**a pak vyberte **vyloučit soubory ze složky\_dat aplikace**.

    Informace o dalších možnostech v části **Možnosti publikování souborů**najdete v kurzu [nasazení do služby IIS](deploying-to-iis.md) . Snímek obrazovky, který ukazuje výsledek tohoto kroku, a následující kroky konfigurace databáze jsou na konci kroků konfigurace databáze.
8. V části **DefaultConnection** v části **databáze** nakonfigurujte nasazení databáze pro databázi členství.
9. 1. Vyberte **aktualizovat databázi**.

        Pole **řetězce vzdáleného připojení** přímo pod **DefaultConnection** se vyplní připojovacím řetězcem ze souboru. publishsettings. Připojovací řetězec obsahuje SQL Server přihlašovací údaje, které jsou uloženy v prostém textu v souboru *. pubxml* . Pokud nechcete, aby byly trvale uloženy, můžete je odebrat z profilu publikování po nasazení databáze a jejich uložení v Azure. Další informace najdete v tématu [jak zajistit zabezpečení připojovacích řetězců ASP.NET Database při nasazení do Azure ze zdroje](http://www.hanselman.com/blog/HowToKeepYourASPNETDatabaseConnectionStringsSecureWhenDeployingToAzureFromSource.aspx) na blogu Scott Hanselman.
      2. Klikněte na **Konfigurovat aktualizace databáze**.
      3. V dialogovém okně **Konfigurovat aktualizace databáze** klikněte na **Přidat skript SQL**.
      4. V poli **Přidat skript SQL** přejděte na skript *ASPNET-data-prod. SQL* , který jste předtím uložili ve složce řešení, a pak klikněte na **otevřít**.
      5. Zavřete dialogové okno **Konfigurovat aktualizace databáze** .
10. V části **SchoolContext** v části **databáze** vyberte **Spustit migrace Code First (spouští se při spuštění aplikace)** .

    Visual Studio zobrazí příkaz **Execute migrace Code First** namísto **aktualizační databáze** pro `DbContext` třídy. Pokud chcete poskytovatele dbDacFx použít místo migrace k nasazení databáze, ke které máte přístup pomocí třídy `DbContext`, přečtěte si téma [návody nasazení Code First databáze bez migrace?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) v tématu Nejčastější dotazy k nasazení webu pro Visual Studio a ASP.NET na webu MSDN.

    Karta **Nastavení** teď vypadá jako v následujícím příkladu:

    ![Karta nastavení pro přípravu](deploying-to-production/_static/image9.png)
11. Chcete-li uložit profil a přejmenovat ho do *pracovního*postupu, proveďte následující kroky:

    1. Klikněte na kartu **profil** a potom klikněte na možnost **Spravovat profily**.
    2. Import vytvořil dva nové profily, jeden pro FTP a druhý pro Nasazení webu. Nakonfigurovali jste profil Nasazení webu: Přejmenujte tento profil na *fázování*.

        ![Přejmenovat profil na pracovní](deploying-to-production/_static/image10.png)
    3. Zavřete dialogové okno **Upravit profily publikování webu** .
    4. Zavřete průvodce **publikováním webu** .

### <a name="configure-a-publish-profile-transform-for-the-environment-indicator"></a>Konfigurace transformace profilu publikování pro indikátor prostředí

> [!NOTE]
> V této části se dozvíte, jak nastavit transformaci Web. config pro indikátor prostředí. Vzhledem k tomu, že indikátor je v prvku `<appSettings>`, máte další alternativu pro zadání transformace při nasazení do Azure App Service. Další informace najdete v tématu [Určení nastavení souboru Web. config v Azure](web-config-transformations.md#watransforms).

1. V **Průzkumník řešení**rozbalte položku **vlastnosti**a potom rozbalte **PublishProfiles**.
2. Klikněte pravým tlačítkem na *fázování. pubxml*a pak klikněte na **přidat konfigurační transformaci**.

    ![Přidat transformaci konfigurace pro přípravu](deploying-to-production/_static/image11.png)

    Visual Studio vytvoří transformační soubor *Web. staging. config* a otevře ho.
3. V transformačním souboru *Web. staging. config* vložte následující kód hned za úvodní značku `configuration`.

    [!code-xml[Main](deploying-to-production/samples/sample1.xml)]

    Když použijete přípravný profil publikování, tato transformace nastaví indikátor prostředí na "prod". V nasazené webové aplikaci se po nadpisu "contoso University" H1 nezobrazí žádná přípona, například "(dev)" nebo "(test)".
4. Klikněte pravým tlačítkem myši na soubor *Web. staging. config* a klikněte na **Náhled transformovat** , aby se zajistilo, že transformace, kterou jste zakódujete, vytvoří očekávané změny.

    V okně **Náhled Web. config** se zobrazí výsledek použití transformací *Web. Release. config* a transformací *Web. staging. config* .

### <a name="prevent-public-use-of-the-test-app"></a>Zabránit veřejnému použití testovací aplikace

Důležitým aspektem pro pracovní aplikaci je to, že bude živý na internetu, ale nechcete, aby ji veřejnost používala. K minimalizaci pravděpodobnosti, že ji lidé uvidí a používají, můžete použít jednu nebo více z následujících metod:

- Nastavte pravidla brány firewall, která umožňují přístup k pracovní aplikaci jenom z IP adres, které používáte k testování přípravy.
- Použijte zašifrované URL, které by nebylo možné odhadnout.
- Vytvořte soubor *robots. txt* , abyste zajistili, že vyhledávací weby nebudou procházet testovací aplikaci a na ni budou odkazy ve výsledcích hledání.

První z těchto metod je nejúčinnější, ale není pokrytá v tomto kurzu, protože by to vyžadovalo nasazení do cloudové služby Azure místo Azure App Service. Další informace o Cloud Services a omezeních IP adres v Azure najdete v tématu [možnosti hostování služby COMPUTE poskytované Azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me) a [zablokování konkrétních IP adres pro přístup k webové roli](https://msdn.microsoft.com/library/windowsazure/jj154098.aspx). Pokud nasazujete pro poskytovatele hostingu třetí strany, obraťte se na poskytovatele, kde zjistíte, jak implementovat omezení IP adres.

V tomto kurzu vytvoříte soubor *robots. txt* .

1. V **Průzkumník řešení**klikněte pravým tlačítkem na projekt ContosoUniversity a klikněte na **Přidat novou položku**.
2. Vytvořte nový **textový soubor** s názvem *robots. txt*a vložte do něj následující text:

    [!code-console[Main](deploying-to-production/samples/sample2.cmd)]

    `User-agent` řádek oznamuje vyhledávacím modulům, že se pravidla v souboru vztahují na všechny webové prohledávací moduly (roboty) a `Disallow` řádek určuje, že by neměly být procházeny žádné stránky na webu.

    Chcete, aby vyhledávací weby mohly zařadit do katalogu produkční aplikace, takže je potřeba tento soubor vyloučit z produkčního nasazení. Uděláte to tak, že nakonfigurujete nastavení v produkčním publikačním profilu při jeho vytváření.

### <a name="deploy-to-staging"></a>Nasazení do přípravného prostředí

1. Otevřete Průvodce **publikováním webu** tak, že kliknete pravým tlačítkem na projekt contoso University a kliknete na **publikovat**.
2. Ujistěte se, že je vybraný **pracovní** profil.
3. Klikněte na **Publikovat**.

    Okno **výstup** zobrazuje, jaké akce nasazení byly provedeny, a oznamuje úspěšné dokončení nasazení. Výchozí prohlížeč se automaticky otevře na adresu URL nasazené webové aplikace.

## <a name="test-in-the-staging-environment"></a>Testování v přípravném prostředí

Všimněte si, že indikátor prostředí chybí (není k dispozici "(test)" nebo "(dev)" za nadpisem H1, který ukazuje, že transformace *Web. config* pro indikátor prostředí byla úspěšná.

![Příprava domovské stránky](deploying-to-production/_static/image12.png)

Spusťte stránku **Students** a ověřte, zda nasazená databáze nemá žádné studenty.

Spuštěním stránky **instruktory** ověřte, zda Code First dosazení databáze s daty instruktory:

Vyberte **Přidat studenty** z nabídky **Students** , přidejte studenta a potom zobrazte nového studenta na stránce **Students** , abyste ověřili, že můžete úspěšně zapisovat do databáze.

Na stránce **kurzy** klikněte na **aktualizovat kredity**. Stránka **aktualizovat kredity** vyžaduje oprávnění správce, aby se zobrazila stránka pro **přihlášení** . Zadejte přihlašovací údaje účtu správce, které jste vytvořili dříve ("admin" a "prodpwd"). Zobrazí se stránka **aktualizace kredity** , která ověřuje, že účet správce, který jste vytvořili v předchozím kurzu, byl správně nasazen do testovacího prostředí.

Požádejte o neplatnou adresu URL, aby došlo k chybě, kterou bude knihovny ELMAH sledovat, a pak požádejte o zprávu o chybě knihovny ELMAH. Pokud nasazujete pro poskytovatele hostingu třetí strany, pravděpodobně zjistíte, že sestava je prázdná ze stejného důvodu, že byla v předchozím kurzu prázdná. Abyste mohli knihovny ELMAH zapisovat do složky protokolu, budete muset pomocí nástrojů pro správu účtu poskytovatele hostingu nakonfigurovat oprávnění ke složkám.

Aplikace, kterou jste vytvořili, je teď spuštěná v cloudu ve webové aplikaci, která je stejně jako to, co budete používat pro produkční prostředí. Vzhledem k tomu, že vše funguje správně, je dalším krokem nasazení do produkčního prostředí.

## <a name="deploy-to-production"></a>Nasazení do produkčního prostředí

Proces vytvoření provozní webové aplikace a nasazení do produkčního prostředí je stejný jako pro přípravu, s tím rozdílem, že je potřeba z nasazení vyloučit soubor *robots. txt* . Uděláte to tak, že upravíte soubor profilu publikování.

### <a name="create-the-production-environment-and-the-production-publish-profile"></a>Vytvoření produkčního prostředí a produkčního profilu pro publikování

1. Vytvořte provozní webovou aplikaci a databázi v Azure stejným způsobem, jaký jste použili pro přípravu.

    Když vytváříte databázi, můžete ji umístit na stejný server, který jste vytvořili dříve, nebo vytvořit nový server.
2. Stáhněte soubor *. publishsettings* .
3. Vytvořte profil publikování importem souboru produkčního *. publishsettings* , a to za stejným postupem, který jste použili pro přípravu.

    Nezapomeňte konfigurovat skript nasazení dat v části **DefaultConnection** v části **databáze** na kartě **Nastavení** .
4. Přejmenujte profil publikování na *produkční*prostředí.
5. Nakonfigurujte transformaci profilu publikování pro indikátor prostředí za stejným postupem, který jste použili pro přípravu.

### <a name="edit-the-pubxml-file-to-exclude-robotstxt"></a>Upravit soubor. pubxml pro vyloučení souboru robots. txt

Soubory profilu publikování jsou pojmenovány &lt;pronázev&gt; *. pubxml* a nacházejí se ve složce *PublishProfiles* . Složka *PublishProfiles* je ve složce *Properties (vlastnosti* ) projektu C# webové aplikace ve složce *můj projekt* v projektu webové aplikace VB nebo ve složce *aplikace\_data* v projektu webové aplikace. Každý soubor *. pubxml* obsahuje nastavení, která se vztahují na jeden profil publikování. Hodnoty, které zadáte v průvodci publikovat web, jsou uloženy v těchto souborech a lze je upravit pro vytvoření nebo změnu nastavení, která nejsou k dispozici v uživatelském rozhraní sady Visual Studio.

Ve výchozím nastavení jsou soubory *. pubxml* zahrnuty do projektu při vytváření profilu publikování, ale můžete je vyloučit z projektu a Visual Studio je stále bude používat. Visual Studio hledá soubory *. pubxml* ve složce *PublishProfiles* bez ohledu na to, jestli jsou zahrnuté v projektu.

Pro každý soubor *. pubxml* je soubor *. pubxml. User* . Pokud jste vybrali možnost **Uložit heslo** a ve výchozím nastavení je vyloučený z projektu, soubor *. pubxml. User* obsahuje šifrované heslo.

Soubor *. pubxml* obsahuje nastavení, která se týkají konkrétního publikačního profilu. Pokud chcete konfigurovat nastavení, která se vztahují na všechny profily, můžete vytvořit soubor *. WPP. targets* . Proces sestavení importuje tyto soubory do souboru projektu *. csproj* nebo *. vbproj* , takže většinu nastavení, které lze konfigurovat v souboru projektu, lze nakonfigurovat v těchto souborech. Další informace o souborech *. pubxml* a *. WPP. targets* naleznete v tématu [How to: Edit settings Deployment in Publish profiles (. pubxml) files and the. WPP. targets in Visual Studio Web Projects](https://msdn.microsoft.com/library/ff398069.aspx).

1. V **Průzkumník řešení**rozbalte **vlastnosti** a rozbalte **PublishProfiles**.
2. Klikněte pravým tlačítkem na *produkční. pubxml* a klikněte na **otevřít**.

    ![Otevřete soubor. pubxml](deploying-to-production/_static/image13.png)
3. Klikněte pravým tlačítkem na *produkční. pubxml* a klikněte na **otevřít**.
4. Přidejte následující řádky těsně před uzavírací `PropertyGroup` element:

    [!code-xml[Main](deploying-to-production/samples/sample3.xml)]

    Soubor. pubxml se teď zdá jako v následujícím příkladu:

    [!code-xml[Main](deploying-to-production/samples/sample4.xml?highlight=18-20)]

    Další informace o tom, jak vyloučit soubory a složky, najdete v tématu Jak [mohu vyloučit konkrétní soubory nebo složky z nasazení?](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment) v tématu **Nejčastější dotazy k nasazení webu pro Visual Studio a ASP.NET** na webu MSDN.

### <a name="deploy-to-production"></a>Nasazení do produkčního prostředí

1. Otevřete Průvodce **publikováním webu** se ujistěte, že **je vybraný profil publikování na** webu, a pak klikněte na **Spustit náhled** na kartě **Náhled** a ověřte, jestli se soubor *robots. txt* nezkopíruje do produkční aplikace.

    ![Náhled souborů, které se mají publikovat do produkčního prostředí](deploying-to-production/_static/image14.png)

    Zkontrolujte seznam souborů, které se zkopírují. Uvidíte, že všechny soubory *. cs* , včetně souborů *. aspx.cs*, *. aspx.Designer.cs*, *Master.cs*a *Master.Designer.cs* , jsou vynechány. Veškerý tento kód byl zkompilován do souborů *ContosoUniversity. dll* a *ContosoUniversity. pdb* , které najdete ve složce *bin* . Vzhledem k tomu, že je ke spuštění aplikace nutná pouze *Knihovna DLL* , a zadali jste dříve, že by měly být nasazeny pouze soubory potřebné ke spuštění aplikace, nebyly do cílového prostředí zkopírovány žádné soubory *. cs* . Složka *obj* a soubory *ContosoUniversity. csproj* a *. csproj. User* jsou vynechány ze stejného důvodu.

    Kliknutím na **publikovat** nasadíte do produkčního prostředí.
2. Otestujte v produkčním prostředí podle stejného postupu, který jste použili pro přípravu.

    Vše je stejné jako u přípravy s výjimkou adresy URL a chybějícího souboru *robots. txt* .

## <a name="summary"></a>Souhrn

Teď jste úspěšně nasadili a otestovali webovou aplikaci, která je veřejně dostupná přes Internet.

![Výroba domovské stránky](deploying-to-production/_static/image15.png)

V dalším kurzu aktualizujete kód aplikace a nasadíte změnu do testovacích, pracovních a produkčních prostředí.

> [!NOTE]
> I když se vaše aplikace používá v produkčním prostředí, měli byste implementovat plán obnovení. To znamená, že byste měli pravidelně zálohovat vaše databáze z produkční aplikace do zabezpečeného úložiště a měli byste uchovávat několik generací takových záloh. Při aktualizaci databáze byste měli vytvořit záložní kopii hned před změnou. Pak pokud uděláte chybu a nezjistíte ji, dokud ji nenainstalujete do produkčního prostředí, budete moct databázi obnovit do stavu, ve kterém byla, než se nastala poškozená. Další informace najdete v tématu [Zálohování a obnovení služby Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/jj650016.aspx).
> 
> 
> [!NOTE]
> V tomto kurzu SQL Server edice, do které nasazujete, Azure SQL Database. I když je proces nasazení podobný jiným verzím SQL Server, skutečná produkční aplikace může vyžadovat speciální kód pro Azure SQL Database v některých scénářích. Další informace najdete v tématu [práce s Azure SQL Database](../../../../whitepapers/aspnet-data-access-content-map.md#ssdb) a [Výběr mezi SQL Server a Azure SQL Database](../../../../whitepapers/aspnet-data-access-content-map.md#ssdbchoosing).
> 
> [!div class="step-by-step"]
> [Předchozí](setting-folder-permissions.md)
> [Další](deploying-a-code-update.md)
