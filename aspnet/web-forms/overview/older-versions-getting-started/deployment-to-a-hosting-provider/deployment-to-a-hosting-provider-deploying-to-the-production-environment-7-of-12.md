---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12
title: 'Nasazení webové aplikace SQL Server Compact v ASP.NET s využitím sady Visual Studio nebo Visual Web Developer: nasazení do provozního prostředí – 7 z 12 | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: b83ab819-2b05-4776-b7b4-79ef78d457a5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12
msc.type: authoredcontent
ms.openlocfilehash: db838633accdedd7c0693b126a007e254ca681e4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74627294"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-the-production-environment---7-of-12"></a>Nasazení webové aplikace v ASP.NET pomocí SQL Server Compact sady Visual Studio nebo Visual Web Developer: nasazení do provozního prostředí – 7.12.

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Studio 2012 RC nebo Visual Studio Express 2012 RC pro web. Můžete také použít Visual Studio 2010, pokud nainstalujete aktualizaci publikování na webu. Úvod k řadě najdete v [prvním kurzu v řadě](deployment-to-a-hosting-provider-introduction-1-of-12.md).
> 
> Kurz, který ukazuje funkce nasazení představené po vydání RC sady Visual Studio 2012, ukazuje, jak nasadit SQL Server edice jiné než SQL Server Compact a ukazuje, jak nasadit na Azure App Service Web Apps, v tématu [nasazení webu ASP.NET pomocí sady Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Přehled

V tomto kurzu nastavíte účet s poskytovatelem hostingu a nasadíte webovou aplikaci v ASP.NET do provozního prostředí pomocí funkce publikování jedním kliknutím sady Visual Studio.

Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje při procházení tohoto kurzu, zkontrolujte [stránku řešení potíží](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).

## <a name="selecting-a-hosting-provider"></a>Výběr poskytovatele hostingu

Pro aplikaci Contoso University a pro tuto řadu kurzů potřebujete poskytovatele, který podporuje ASP.NET 4 a Nasazení webu. Zvolili jste konkrétní hostingovou společnost, která by kurzy mohla Ukázat na ucelené možnosti nasazení na živý Web. Každá hostující společnost poskytuje různé funkce a prostředí nasazení na jejich servery se trochu liší. Proces popsaný v tomto kurzu je ale typický pro celý proces. Poskytovatel hostingu, který se používá pro účely tohoto kurzu, Cytanium.com, je jedním z mnoha dostupných a jeho použití v tomto kurzu nepředstavuje potvrzení ani doporučení.

Až budete připraveni vybrat vlastního poskytovatele hostingu, můžete porovnat funkce a ceny v [galerii poskytovatelů](https://www.microsoft.com/web/hosting) na webu Microsoft.com/web.

## <a name="creating-an-account"></a>Vytváření účtu

Vytvořte účet na vybraném poskytovateli. Pokud je podpora pro kompletní SQL Server databáze přidána jako další, nemusíte ji pro tento kurz vybírat, ale budete ji potřebovat pro [migraci na SQL Server](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md) kurz později v této sérii.

Pro tyto kurzy nemusíte registrovat nový název domény. Můžete otestovat pro ověření úspěšného nasazení pomocí dočasné adresy URL přiřazené k lokalitě zprostředkovatelem.

Po vytvoření účtu obdržíte obvykle uvítací e-mail, který obsahuje všechny informace, které potřebujete k nasazení a správě vašeho webu. Informace, které váš poskytovatel hostingu odesílá, se podobá tomu, co se tady zobrazuje. Uvítací e-mail Cytanium, který se pošle vlastníkům nového účtu, zahrnuje tyto informace:

- Adresa URL webu ovládacího panelu poskytovatele, kde můžete spravovat nastavení webu. ID a heslo, které jste zadali, jsou zahrnuté v této části uvítacího e-mailu pro snadné reference. (Obě se změnily na ukázku hodnoty pro tento obrázek.)

    [![Welcome_Email_Control_Panel_URL](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image1.png)
- Výchozí .NET Framework verze a informace o tom, jak je změnit. Mnoho hostitelských webů je standardně 2,0, což spolupracuje s aplikacemi ASP.NET, které cílí na .NET Framework 2,0, 3,0 nebo 3,5. Společnost Contoso University je však aplikací .NET Framework 4, takže je nutné toto nastavení změnit. (Pro aplikaci ASP.NET 4,5 byste měli použít nastavení .NET 4,0.)

    [![Welcome_Email_Framework_Version](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image3.png)
- Dočasná adresa URL, kterou můžete použít pro přístup k webu. Po vytvoření tohoto účtu se jako stávající název domény zadal "contosouniversity.com". Proto je dočasná adresa URL `http://contosouniversity.com.vserver01.cytanium.com`.

    [![Welcome_Email_Temporary_URL](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image5.png)
- Informace o tom, jak nastavit databáze a připojovací řetězce, které potřebujete pro přístup k nim:

    [![Welcome_Email_Database_Info](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image7.png)
- Informace o nástrojích a nastaveních pro nasazení webu. (E-mail z Cytanium také zmiňuje WebMatrix, který je tady vynechán.)

    [![Welcome_Email_Deploy_info](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image10.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image9.png)

## <a name="setting-the-net-framework-version"></a>Nastavení verze .NET Framework

Uvítací e-mail Cytanium obsahuje odkaz na pokyny, jak změnit verzi .NET Framework. Tyto pokyny vysvětlují, jak to lze provést prostřednictvím ovládacího panelu Cytanium. Jiní poskytovatelé mají weby v Ovládacích panelech, které vypadají jinak, nebo vás k tomu můžou dát jiným způsobem.

Přejít na adresu URL ovládacího panelu. Po přihlášení pomocí uživatelského jména a hesla se zobrazí ovládací panely.

[![Cytanium_Control_Panel](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image11.png)

V poli **hostující prostory** umístěte ukazatel myši na ikonu webu a v nabídce vyberte možnost **webové servery** .

[![Cytanium_Control_Panel_selecting_Web_Sites](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image13.png)

V poli **weby** klikněte na **contosouniversity.com** (název webu, který jste použili při vytváření účtu).

[![Cytanium_Control_Panel_selecting_contosouniversity](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image15.png)

V poli **Vlastnosti webového serveru** vyberte kartu **rozšíření** .

[![Cytanium_Control_Panel_Extensions_tab](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image17.png)

Změňte ASP.NET z **integrovaného kanálu 2,0** na **4,0 (integrovaný kanál)** a pak klikněte na **aktualizovat**.

## <a name="publishing-to-the-hosting-provider"></a>Publikování pro poskytovatele hostingu

Uvítací e-mail od poskytovatele hostingu zahrnuje všechna nastavení, která potřebujete k publikování projektu, a tyto informace můžete zadat ručně do profilu publikování. Při konfiguraci nasazení na zprostředkovatele ale budete používat jednodušší a méně chybově náchylnější způsob: stahujete soubor *. publishsettings* a naimportujete ho do publikačního profilu.

V prohlížeči přejdete na ovládací panel Cytanium a vyberte **Web** a pak vyberte **weby.**

![Ovládací panely pro výběr webů](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image19.png)

Vyberte web **contosouniversity.com** .

![Ovládací panely pro výběr contosouniversity.com](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image20.png)

Vyberte kartu **publikování na webu** .

![Karta publikování na webu v Ovládacích panelech](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image21.png)

Vytvořte přihlašovací údaje, které se použijí pro publikování na webu, a to zadáním uživatelského jména a hesla. Můžete zadat stejné přihlašovací údaje, které používáte pro přihlášení k ovládacímu panelu. Pak klikněte na **Povolit**.

![Ovládací panel vytvoření přihlašovacích údajů pro publikování](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image22.png)

Klikněte na **Stáhnout profil publikování pro tento web**.

![Řídicí panel – stáhnout profil publikování](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image23.png)

Až se zobrazí výzva k otevření nebo uložení souboru, uložte ho.

![Uložit soubor profilu publikování](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image24.png)

V **Průzkumník řešení** v aplikaci Visual Studio klikněte pravým tlačítkem na projekt ContosoUniversity a vyberte **publikovat**. Dialogové okno **Publikovat web** se otevře na kartě **Náhled** s vybraným **testovacím** profilem, protože to je poslední profil, který jste použili.

Vyberte kartu **profil** a pak klikněte na **importovat**.

![Tlačítko pro import webového Průvodce publikování](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image25.png)

V dialogovém okně **importovat nastavení publikování** vyberte soubor *. publishsettings* , který jste stáhli, a klikněte na **otevřít**. Průvodce přejde na kartu připojení se všemi vyplněnými poli.

![Karta pro připojení Průvodce publikováním webu](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image26.png)

Soubor. publishsettings umístí do pole Cílová adresa URL plánovanou trvalou adresu URL pro web, ale pokud jste tuto doménu ještě nekoupili, nahraďte tuto hodnotu dočasnou adresou URL. V tomto příkladu je adresa URL  *[http://contosouniversity.com.vserver01.cytanium.com](http://contosouniversity.com.vserver01.cytanium.com).* Jediným účelem tohoto pole je určit, jakou adresu URL bude prohlížeč po úspěšném nasazení automaticky po úspěšném nasazení. Pokud ponecháte pole prázdné, jediným z nich je, že se prohlížeč po nasazení automaticky nespustí.

Klikněte na **ověřit připojení** , abyste ověřili, že jsou nastavení správná, a můžete se připojit k serveru. Jak jste viděli dříve, zelená značka zaškrtnutí ověří, že připojení proběhlo úspěšně.

Když kliknete na ověřit připojení, může se zobrazit dialogové okno s **chybou certifikátu** . Pokud tak učiníte, ověřte, že název serveru je očekávaný. Pokud je, vyberte **Uložit tento certifikát pro budoucí relace sady Visual Studio** a klikněte na **přijmout**. (Tato chyba znamená, že se poskytovatel hostingu rozhodl vyhnout se nákladům na nákup certifikátu SSL pro adresu URL, na kterou nasazujete. Pokud dáváte přednost navázání zabezpečeného připojení pomocí platného certifikátu, obraťte se na svého poskytovatele hostingu.)

![Chyba certifikátu](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image27.png)

Klikněte na tlačítko **Další**.

V části **databáze** na kartě **Nastavení** zadejte stejné hodnoty, které jste zadali pro testovací profil publikování. Připojovací řetězce, které potřebujete, najdete v rozevíracích seznamech.

- V poli připojovací řetězec pro **SchoolContext** vyberte `Data Source=|DataDirectory|School-Prod.sdf`
- V části **SchoolContext**vyberte **použít migrace Code First**.
- V poli připojovací řetězec pro **DefaultConnection**vyberte `Data Source=|DataDirectory|aspnet-Prod.sdf`
- V části **DefaultConnection**ponechte zrušenou **aktualizaci databáze** .

![Karta nastavení Průvodce publikováním webu](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image28.png)

Klikněte na tlačítko **Další**.

Na kartě **Náhled** klikněte na možnost **Spustit náhled** . zobrazí se seznam souborů, které budou zkopírovány. Uvidíte stejný seznam, který jste viděli dříve při nasazení do služby IIS v místním počítači.

Před publikováním změňte název profilu tak, aby se používal transformační soubor Web. produkční. config. Vyberte kartu **profil** a klikněte na **Spravovat profily**.

![Průvodce publikováním webu Správa profilů](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image29.png)

V dialogovém okně **Upravit profily publikování na webu** vyberte profil výroby, klikněte na **Přejmenovat**a změňte název profilu na produkční. Pak klikněte na **Zavřít**.

![Dialogové okno Upravit profily publikování webu](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image30.png)

Klikněte na **publikovat**.

Aplikace je publikovaná pro poskytovatele hostingu. Výsledek se zobrazí v okně **výstup** .

![Okno výstup po nasazení](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image31.png)

Prohlížeč se automaticky otevře na adresu URL, kterou jste zadali v poli **cílová adresa URL** na kartě **připojení** v průvodci **publikování webu** . Stejná Domovská stránka se zobrazí jako při spuštění webu v aplikaci Visual Studio, s tím rozdílem, že v záhlaví není nyní žádný indikátor prostředí "(test)" nebo "(dev)". To znamená, že transformace *Web. config* indikátoru prostředí fungovala správně.

> [!NOTE]
> Pokud se v záhlaví stále zobrazuje "(test)", odstraňte ze projektu ContosoUniversity složku *obj* a znovu ji nasaďte. V předběžných verzích softwaru se může dřív použité transformační soubor (Web. test. config) použít znovu, i když používáte produkční profil.

[![Home_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image33.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image32.png)

Než spustíte stránku, která způsobí přístup k databázi, ujistěte se, že knihovny elmah bude moci protokolovat všechny chyby, ke kterým dojde.

## <a name="setting-folder-permissions-for-elmah"></a>Nastavení oprávnění složky pro knihovny elmah

Jak si pamatujete z předchozího kurzu v této sérii, musíte se ujistit, že aplikace má oprávnění k zápisu do složky ve vaší aplikaci, kde knihovny elmah ukládá soubory protokolu chyb. Pokud jste nasadili službu IIS místně na počítači, nastavili jste tato oprávnění ručně. V této části se dozvíte, jak nastavit oprávnění na Cytanium. (Někteří poskytovatelé hostingu to nemůžou povolit, můžou nabízet jednu nebo více předdefinovaných složek s oprávněním k zápisu. V takovém případě byste museli aplikaci upravit, aby používala zadané složky.)

Oprávnění ke složkám lze nastavit v Ovládacích panelech Cytanium. V části Adresa URL ovládacího panelu vyberte **Správce souborů**.

[![Cytanium_Control_Panel_with_File_Manager_selected](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image35.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image34.png)

V poli **Správce souborů** vyberte **contosouniversity.com** a potom **wwwroot** , aby se zobrazila kořenová složka aplikace. Klikněte na ikonu visacího zámku nezobrazuje vedle **knihovny elmah**.

[![Cytanium_Control_Panel_File_Manager_at_root_folder](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image37.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image36.png)

V okně **oprávnění složky**/**souboru** zaškrtněte políčka **pro čtení** a **zápis** pro **contosouniversity.com** a klikněte na **nastavit oprávnění**.

[![Cytanium_Control_Panel_File_Folder_Permissions_Elmah](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image39.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image38.png)

Zajistěte, aby knihovny elmah měl přístup pro zápis do složky *knihovny elmah* tím, že vyvolá chybu a pak zobrazí zprávu o chybách knihovny elmah. Žádost o neplatnou adresu URL, jako je *Studentsxxx. aspx*. Stejně jako dřív se zobrazí stránka *GenericErrorPage. aspx* . Klikněte na odkaz **Odhlásit** se a potom spusťte *knihovny elmah. axd*. Nejdřív získáte **přihlašovací** stránku, která ověří, že transformace *Web. config* úspěšně přidala autorizaci knihovny elmah. Po přihlášení se zobrazí sestava znázorňující chybu, kterou jste právě způsobili.

[![knihovny elmah. axd_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image41.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image40.png)

## <a name="testing-in-the-production-environment"></a>Testování v produkčním prostředí

Spusťte stránku **Students** . Aplikace se při prvním pokusu o přístup do školní databáze pokusí o vytvoření databáze, která spustí Migrace Code First. Když se stránka zobrazí po chvíli zpoždění, ukáže to, že neexistují studenti.

[![Students_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image43.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image42.png)

Spuštěním stránky **instruktory** ověříte, že data počátečních dat byla do databáze úspěšně vložena.

[![Instructors_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image45.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image44.png)

Stejně jako v testovacím prostředí chcete ověřit, jestli aktualizace databáze fungují v produkčním prostředí, ale obvykle nechcete zadávat testovací data do provozní databáze. V tomto kurzu použijete stejnou metodu, kterou jste provedli v testu. Ale v reálné aplikaci byste mohli chtít najít metodu, která ověřuje, jestli jsou aktualizace databáze úspěšné, aniž byste museli zavádět testovací data do provozní databáze. V některých aplikacích může být praktické přidat něco a pak je odstranit.

Přidejte studenta a potom zobrazte data, která jste zadali na stránce **Students** , abyste ověřili, že můžete aktualizovat data v databázi.

[![Add_Students_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image47.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image46.png)

[![Students_page_with_new_student_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image49.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image48.png)

Kliknutím na **aktualizovat kredity** v nabídce **kurzy** ověřte, jestli autorizační pravidla fungují správně. Zobrazí se **přihlašovací** stránka. Zadejte přihlašovací údaje účtu správce, klikněte na **Přihlásit**se a zobrazí se stránka **aktualizovat kredity** .

[![Log_In_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image51.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image50.png)

Pokud je přihlášení úspěšné, zobrazí se stránka **aktualizace kredity** . To znamená, že se úspěšně nasadila databáze členství ASP.NET (s jediným účtem správce).

[![Update_Credits_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image53.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image52.png)

Teď jste úspěšně nasadili a otestovali lokalitu, která je veřejně dostupná přes Internet.

## <a name="creating-a-more-reliable-test-environment"></a>Vytvoření spolehlivější testovací prostředí

Jak je vysvětleno v kurzu [nasazení do testovacího prostředí](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) , nejspolehlivější testovací prostředí by představovalo druhý účet u poskytovatele hostingu, který je stejně jako produkční účet. Tento postup by byl dražší než použití místní služby IIS jako testovacího prostředí, protože byste se museli zaregistrovat k druhému hostitelskému účtu. Pokud ale zabrání chybám produkčního serveru nebo výpadkům, můžete se rozhodnout, že stojí za cenu.

Většina procesu pro vytvoření a nasazení testovacího účtu je podobná tomu, co jste už provedli při nasazení do produkčního prostředí:

- Vytvořte transformační soubor *Web. config* .
- Vytvořte účet u poskytovatele hostingu.
- Vytvořte nový profil publikování a nasaďte ho do testovacího účtu.

### <a name="preventing-public-access-to-the-test-site"></a>Zabránění veřejnému přístupu k testovacímu webu

Důležitým aspektem testovacího účtu je to, že bude živý na internetu, ale nechcete, aby ho veřejnost používali. Pro zachování privátní lokality můžete použít jednu nebo několik následujících metod:

- Řekněte poskytovateli hostingu, aby nastavil pravidla brány firewall, která umožňují přístup k testovací lokalitě jenom z IP adres, které používáte pro testování.
- Zamaskujte adresu URL tak, aby se nepodobá adrese URL veřejné lokality.
- Pomocí souboru *robots. txt* zajistěte, aby vyhledávací weby neprošly testovací lokalitou a odkazy na ni ve výsledcích hledání.

První z těchto metod je zjevnější, ale procedura pro to je specifická pro každého poskytovatele hostingu a nebude zahrnuta v tomto kurzu. Pokud zadáte vašemu poskytovateli hostingu, abyste povolili pouze vaši IP adresu pro procházení na adresu URL testovacího účtu, nemusíte si dělat starosti se vyhledáváním v procházecích provyhledávačích. Ale i v takovém případě je nasazení souboru *robots. txt* vhodné jako záloha pro případ, že je pravidlo brány firewall někdy náhodně vypnuté.

Soubor *robots. txt* přejde do složky projektu a měl by mít následující text:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/samples/sample1.cmd)]

`User-agent` řádek oznamuje vyhledávacím modulům, že se pravidla v souboru vztahují na všechny webové prohledávací moduly (roboty) a `Disallow` řádek určuje, že by neměly být procházeny žádné stránky na webu.

Pravděpodobně budete chtít, aby vyhledávací weby mohly zařadit do katalogu produkčního webu, takže tento soubor musíte vyloučit z produkčního nasazení. Chcete-li to provést, přečtěte si téma Jak mohu **vyloučit konkrétní soubory nebo složky z nasazení?** v tématu [Nejčastější dotazy k nasazení projektu webové aplikace ASP.NET](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment). Ujistěte se, že zadáváte vyloučení jenom pro produkční profil publikování.

Vytvoření druhého hostitelského účtu je přístup k práci s testovacím prostředím, které se nevyžaduje, ale může se jednat o přidané náklady. V následujících kurzech budete dál používat službu IIS jako testovací prostředí.

V dalším kurzu aktualizujete kód aplikace a nasadíte svou změnu do testovacích a produkčních prostředí.

> [!div class="step-by-step"]
> [Předchozí](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
> [Další](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
