---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: 'Nasazení webu ASP.NET pomocí sady Visual Studio: nasazení aktualizace kódu | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která bude Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: 3881833bfe2a50a38a357614f92f434a04a8ab08
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78567401"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a>Nasazení webu ASP.NET pomocí sady Visual Studio: nasazení aktualizace kódu

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která umožňuje Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí sady Visual Studio 2012 nebo Visual Studio 2010. Informace o řadě najdete v [prvním kurzu v řadě](introduction.md).

## <a name="overview"></a>Přehled

Po počátečním nasazení bude vaše práce s údržbou a vývojem webu pokračovat a ještě dlouho budete chtít nasadit aktualizaci. Tento kurz vás provede procesem nasazení aktualizace kódu vaší aplikace. Aktualizace, kterou implementujete a nasadíte v tomto kurzu, nezahrnuje změnu databáze. v dalším kurzu se dozvíte, jaké jsou různé informace o nasazení změny databáze.

Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje při procházení tohoto kurzu, zkontrolujte [stránku řešení potíží](troubleshooting.md).

## <a name="make-a-code-change"></a>Provedení změny kódu

Jako jednoduchý příklad aktualizace aplikace přidáváte na stránku **instruktoři** seznam kurzů, které probral vybraný instruktor.

Pokud spouštíte stránku **instruktory** , všimnete si, že v mřížce jsou **vybrané** odkazy, ale nedělají nic jiného, než když se pozadí řádku změní na šedé.

![Stránka instruktoři s výběrem](deploying-a-code-update/_static/image1.png)

Nyní přidáte kód, který se spustí, když se klikne na odkaz **Select** , a zobrazí se seznam kurzů, které prochází vybraným instruktorem.

1. V *instruktors. aspx*přidejte následující kód hned za ovládací prvek **ErrorMessageLabel** `Label`:

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. Spusťte stránku a vyberte instruktor. Zobrazí se seznam výukových kurzů, které tento instruktor projedná.

    ![Stránka instruktorů s výukou kurzů](deploying-a-code-update/_static/image2.png)
3. Zavřete prohlížeč.

## <a name="deploy-the-code-update-to-the-test-environment"></a>Nasazení aktualizace kódu do testovacího prostředí

Než budete moct použít svoje profily publikování k nasazení na testování, přípravu a produkční prostředí, musíte změnit možnosti publikování databáze. Už nemusíte spouštět skripty pro udělení a nasazování dat pro databázi členství.

1. Otevřete Průvodce **publikováním webu** kliknutím pravým tlačítkem myši na projekt ContosoUniversity a kliknutím na **publikovat**.
2. V rozevíracím seznamu **profil** klikněte na profil **testu** .
3. Klikněte na kartu **Nastavení**.
4. V části **DefaultConnection** v části **databáze** zrušte zaškrtnutí políčka **aktualizovat databázi** .
5. Klikněte na kartu **profil** a potom v rozevíracím seznamu **profil** klikněte na **pracovní** profil.
6. Když se zobrazí dotaz, zda chcete uložit změny provedené v profilu **testu** , klikněte na tlačítko **Ano**.
7. Udělejte stejnou změnu v pracovním profilu.
8. Zopakováním tohoto postupu provedete stejnou změnu v produkčním profilu.
9. Zavřete průvodce **publikováním webu** .

Nasazení do testovacího prostředí je teď jednoduchou záležitostí opětovného spuštění publikování jedním kliknutím. Chcete-li tento proces urychlit, můžete použít panel nástrojů pro **publikování webu jedním kliknutím** .

1. V nabídce **zobrazení** zvolte **panely nástrojů** a pak vyberte **možnost publikovat na webu jedním kliknutím**.

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. V **Průzkumník řešení**vyberte projekt ContosoUniversity.
3. panel nástrojů pro **publikování webu jedním kliknutím** vyberte profil publikování **testu** a pak klikněte na **Publikovat web** (ikona se šipkami ukazující vlevo a vpravo).

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. Visual Studio nasadí aktualizovanou aplikaci a prohlížeč se automaticky otevře na domovské stránce.
5. Spusťte stránku instruktoři a vyberte instruktora, abyste ověřili, že byla aktualizace úspěšně nasazena.

Obvykle byste také provedli regresní testování (to znamená otestovat zbytek lokality, abyste se ujistili, že nová změna nepřerušila všechny stávající funkce). Pro tento kurz ale tento krok přeskočíte a pokračujte v nasazení aktualizace do pracovních a produkčních prostředí.

Když znovu nasadíte, Nasazení webu automaticky určí, které soubory se změnily, a na server se zkopírují jenom změněné soubory. Ve výchozím nastavení Nasazení webu používá datum poslední změny souborů k určení, které z nich se změnily. Některé systémy správy zdrojového kódu mění data souborů i v případě, že neměníte obsah souboru. V takovém případě můžete chtít nakonfigurovat Nasazení webu, aby používaly kontrolní součty souborů k určení, které soubory se změnily. Další informace najdete v tématu [Proč se všechny moje soubory znovu nasazují, i když jsem nezměnili?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) v nejčastějších dotazech k nasazení ASP.NET.

## <a name="take-the-application-offline-during-deployment"></a>Při nasazení převést aplikaci do offline režimu

Změna, kterou právě nasazujete, je jednoduchá změna na jednu stránku. Někdy ale nasadíte větší změny nebo nasadíte změny kódu i databáze a lokalita se může chovat nesprávně, pokud uživatel požádá o stránku před dokončením nasazení. Pokud chcete zabránit uživatelům v přístupu k webu, když probíhá nasazení, můžete použít *aplikaci\_offline souboru. htm* . Když umístíte soubor s názvem *app\_v režimu offline. htm* do kořenové složky vaší aplikace, služba IIS automaticky zobrazí tento soubor místo spuštění aplikace. Pokud tedy chcete během nasazení zabránit přístupu, vložte *aplikaci\_do režimu offline. htm* v kořenové složce, spusťte proces nasazení a po úspěšném nasazení odeberte *aplikaci\_offline. htm* .

Nasazení webu můžete nakonfigurovat tak, aby při zahájení nasazování automaticky umístila výchozí *aplikaci\_offline soubor. htm* na server, a po dokončení ho odebere. Chcete-li provést vše, co musíte udělat, přidejte do souboru publikačního profilu (. pubxml) následující element XML:

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

V tomto kurzu se dozvíte, jak vytvořit a použít vlastní *aplikaci\_offline souboru. htm* .

Použití *aplikace\_offline. htm* v pracovní lokalitě není vyžadováno, protože nemáte přístup k pracovnímu webu. Je ale vhodné použít fázování k otestování všech způsobů, jak plánujete nasazení v produkčním prostředí.

### <a name="create-app_offlinehtm"></a>Vytvoření aplikace\_offline. htm

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na řešení, klikněte na tlačítko **Přidat**a poté klikněte na položku **Nová položka**.
2. Vytvořte **stránku HTML** s názvem *App\_offline. htm* (odstraňte poslední "l" v rozšíření *. html* , které Visual Studio vytvoří ve výchozím nastavení).
3. Nahraďte kód šablony následujícím kódem:

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. Uložte soubor a zavřete ho.

### <a name="copy-app_offlinehtm-to-the-root-folder-of-the-web-site"></a>Zkopírujte aplikaci\_offline. htm do kořenové složky webu.

K kopírování souborů na web můžete použít libovolný nástroj FTP. [FileZilly](http://filezilla-project.org/) je oblíbený nástroj FTP, který se zobrazuje ve snímkůch obrazovky.

Chcete-li použít nástroj FTP, budete potřebovat tři věci: adresu URL serveru FTP, uživatelské jméno a heslo.

Adresa URL se zobrazí na stránce řídicí panel webu v Azure Portál pro správu a uživatelské jméno a heslo pro FTP najdete v souboru *. publishsettings* , který jste si stáhli dříve. Následující kroky ukazují, jak tyto hodnoty získat.

1. V Portál pro správu Azure klikněte na kartu **webové servery** a potom klikněte na pracovní web.
2. Na stránce **řídicí panel** přejděte dolů a vyhledejte název hostitele FTP v části **rychlý přehled** .

    ![Název hostitele FTP](deploying-a-code-update/_static/image5.png)
3. V programu Poznámkový blok nebo jiném textovém editoru otevřete soubor staging *. publishsettings* .
4. Vyhledejte prvek `publishProfile` pro profil FTP.
5. Zkopírujte hodnoty `userName` a `userPWD`.

    ![Přihlašovací údaje FTP](deploying-a-code-update/_static/image6.png)
6. Otevřete nástroj FTP a přihlaste se k adrese URL serveru FTP.
7. Zkopírujte *aplikaci\_offline. htm* ze složky řešení do složky */site/wwwroot* v přípravném webu.

    ![Kopírovat app_offline](deploying-a-code-update/_static/image7.png)
8. Přejděte na adresu URL vašeho pracovního webu. Uvidíte, že se teď místo domovské stránky zobrazuje stránka *aplikace\_offline. htm* .

    ![app_offline. htm v okně prohlížeče](deploying-a-code-update/_static/image8.png)

Nyní jste připraveni na nasazení do přípravy.

## <a name="deploy-the-code-update-to-staging-and-production"></a>Nasazení aktualizace kódu do pracovního a produkčního prostředí

1. Na panelu nástrojů **publikování webu jedním kliknutím** vyberte profil pro **přípravu** a pak klikněte na **Publikovat web**.

    Visual Studio nasadí aktualizovanou aplikaci a otevře prohlížeč na domovské stránce webu. Zobrazí se soubor *\_offline. htm aplikace* . Než budete moct otestovat ověření úspěšného nasazení, musíte *aplikaci odebrat\_offline souboru. htm* .
2. Vraťte se do nástroje FTP a odstraňte **aplikaci\_offline. htm** z přípravného webu.
3. V prohlížeči otevřete stránku instruktoři v přípravném webu a vyberte instruktora, abyste ověřili, že byla aktualizace úspěšně nasazena.
4. Pro produkční prostředí použijte stejný postup jako při přípravě.

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a>Kontrola změn a nasazení určitých souborů

Visual Studio 2012 také umožňuje nasazovat jednotlivé soubory. Pro vybraný soubor můžete zobrazit rozdíly mezi místní a nasazenou verzí, nasadit soubor do cílového prostředí nebo zkopírovat soubor z cílového prostředí do místního projektu. V této části kurzu zjistíte, jak tyto funkce používat.

### <a name="make-a-change-to-deploy"></a>Provedení změny nasazení

1. Otevřete *Content/Web. CSS*a najděte blok značky `body`.
2. Změňte hodnotu `background-color` z `#fff` na `darkblue`.

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a>Zobrazení změny v okně Publikovat náhled

Když použijete průvodce **Publikovat web** k publikování projektu, můžete zjistit, jaké změny budou publikovány Poklikáním na soubor v okně **náhledu** .

1. Klikněte pravým tlačítkem na projekt ContosoUniversity a klikněte na **publikovat**.
2. V rozevíracím seznamu **profil** vyberte profil publikování **testu** .
3. Klikněte na **Náhled**a pak na **Spustit náhled**.
4. V podokně **náhledu** poklikejte na **site. CSS**.

    ![Poklikejte na web. CSS.](deploying-a-code-update/_static/image9.png)

    V dialogovém okně **Náhled změn** se zobrazí náhled změn, které budou nasazeny.

    ![Zobrazit náhled změn v site. CSS](deploying-a-code-update/_static/image10.png)

    Pokud dvakrát kliknete na soubor *Web. config* , zobrazí dialogové okno **Náhled změn** efekt transformací konfigurace sestavení a publikování profilů. V tomto okamžiku jste neudělali nic, co by mohlo způsobit změnu souboru *Web. config* na serveru, takže očekáváte, že se nezobrazí žádné změny. Okno **Náhled změn** ale nesprávně zobrazuje dvě změny. Vypadá to, že se odeberou dva prvky XML. Tyto prvky jsou přidány procesem publikování, když vyberete možnost **spustit migrace Code First při spuštění aplikace** pro třídu kontextu Code First. Porovnání je provedeno před tím, než proces publikování přidá tyto prvky, takže vypadá, že jsou odebírány, i když nebudou odebrány. Tato chyba bude opravena v budoucí verzi.
5. Klikněte na **Zavřít**.
6. Klikněte na **Publikovat**.
7. Po otevření prohlížeče na domovské stránce testovacího webu stiskněte klávesy CTRL + F5, čímž se zobrazí efekt změny šablony stylů CSS.

    ![Účinek změny šablony stylů CSS](deploying-a-code-update/_static/image11.png)
8. Zavřete prohlížeč.

### <a name="publish-specific-files-from-solution-explorer"></a>Publikovat konkrétní soubory z Průzkumník řešení

Předpokládejme, že se vám nelíbí modré pozadí a chcete se vrátit k původní barvě. V této části obnovíte původní nastavení publikováním konkrétního souboru přímo z **Průzkumník řešení**.

1. Otevřete *Content/Web. CSS* a obnovte nastavení `background-color` pro `#fff`.
2. V **Průzkumník řešení**klikněte pravým tlačítkem myši na soubor *Content/Web. CSS* .

    Místní nabídka obsahuje tři možnosti publikování.

    ![Publikování možností z Průzkumník řešení](deploying-a-code-update/_static/image12.png)
3. Klikněte na **Náhled změn v site. CSS**.

    Otevře se okno, ve kterém se zobrazí rozdíly mezi místním souborem a jeho verzí v cílovém prostředí.

    ![Diff-Content/Site.css](deploying-a-code-update/_static/image13.png)
4. V **Průzkumník řešení**klikněte znovu pravým tlačítkem na **site. CSS** a pak klikněte na **Publikovat web. CSS**.

    V okně **aktivity publikování na webu** se zobrazí, že soubor byl publikován.

    ![Okno aktivity publikování na webu](deploying-a-code-update/_static/image14.png)
5. Otevřete prohlížeč na adrese URL `http://localhost/contosouniversity` a potom stisknutím kombinace kláves CTRL + F5 zobrazte efekt změny šablony stylů CSS.

    ![Domovská stránka s normální šablonou stylů CSS](deploying-a-code-update/_static/image15.png)
6. Zavřete prohlížeč.

## <a name="summary"></a>Souhrn

Nyní jste viděli několik způsobů, jak nasadit aktualizaci aplikace, která nezahrnuje změnu databáze a jste viděli, jak zobrazit náhled změn, abyste ověřili, jestli se má aktualizovat, a to, co očekáváte. Stránka instruktoři má teď oddíl **výukových kurzů** .

![Stránka instruktorů s výukou kurzů](deploying-a-code-update/_static/image16.png)

V dalším kurzu se dozvíte, jak nasadit změnu databáze: přidáte pole DatumNarození do databáze a na stránku instruktoři.

> [!div class="step-by-step"]
> [Předchozí](deploying-to-production.md)
> [Další](deploying-a-database-update.md)
