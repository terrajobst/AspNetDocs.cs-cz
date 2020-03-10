---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: Vylepšení v aplikaci Visual Studio 2005 | Microsoft Docs
author: microsoft
description: Visual Studio 2005 poskytuje vývojářům webových aplikací dlouhý seznam vylepšení a vylepšení webových projektů.
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: 64215d556ded0850537a13856fe69b094116ebca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78575577"
---
# <a name="improvements-in-visual-studio-2005"></a>Vylepšení v sadě Visual Studio 2005

od [Microsoftu](https://github.com/microsoft)

> Visual Studio 2005 poskytuje vývojářům webových aplikací dlouhý seznam vylepšení a vylepšení webových projektů.

Visual Studio 2005 poskytuje vývojářům webových aplikací dlouhý seznam vylepšení a vylepšení webových projektů. Stejně jako v případě sady Visual Studio .NET 2002 a 2003 existuje mnoho stížností ve způsobu, jakým byly zpracovány webové projekty. Visual Studio 2005 přidává k těmto stížnostem velký počet nových funkcí, aby bylo možné tyto stížnosti vyřešit. Pro ty, kteří dávají přednost způsobu, jakým aplikace Visual Studio .NET 2003 zpracovala kompilaci webových aplikací, naleznete v tématu [projekty webových aplikací](https://go.microsoft.com/fwlink/?LinkId=57870).

V tomto modulu se dobře pokryje vylepšení vytváření, správy a vývoje webového projektu. V pozdějším modulu je dobré se zabývat vylepšeními při sestavování webových projektů a jejich nasazení.

## <a name="frontpage-server-extensions"></a>Rozšíření serveru FrontPage

Aby bylo možné vytvářet nebo sestavovat webové projekty, musí být v poli Visual Studio .NET 2002 a 2003 požadována rozšíření serveru FrontPage. Vývojáři mají možnost volit mezi dvěma různými režimy přístupu (rozšíření serveru FrontPage nebo režim přístupu k souborům), jak se používají rozšíření FrontPage Server Extensions k provádění úloh, jako je například nastavení kořenového adresáře aplikace ve službě IIS atd.

Visual Studio 2005 odstraňuje závislosti na rozšířeních serveru FrontPage pro místní projekty. Visual Studio 2005 teď přistupuje k metabázi služby IIS přímo místo pomocí rozšíření serveru FrontPage. Visual Studio 2005 také přidává podporu pro FTP, která umožňuje vzdálený přístup k projektu bez nutnosti rozšíření serveru FrontPage.

Pro vývojáře, kteří chtějí používat rozšíření FrontPage Server Extensions v jejich projektech, je tato možnost stále k dispozici. V závislosti na silné zpětné vazbě od komunity vývojářů ASP.NET to ale není potřeba.

> [!NOTE]
> Rozšíření serveru FrontPage jsou stále vyžadována pro vzdálené vytváření projektů, otevírání atd.

## <a name="aspnet-development-server"></a>Vývojový server ASP.NET

Visual Studio 2005 se dodává s novým webovým serverem s názvem ASP.NET Development Server. (Tento webový server se dřív nazýval Cassini.)

Vývojového serveru ASP.NET je několik výhod.

- Pro vývoj a ladění na webovém serveru je teď možné, že nejsou správci.
- ASP.NET Development Server dynamicky mapuje virtuální adresáře na libovolné místo v systému souborů, což umožňuje flexibilní umístění projektu.
- Uživatelé v systému Windows XP Professional, kteří již používají službu IIS, nyní budou moci vytvářet nové webové aplikace, které nebudou mít vliv na strukturu souboru nebo složky jejich výchozího webu ve službě IIS.

Pro využití vývojového serveru ASP.NET není potřeba žádná zvláštní konfigurace. Pokud je webový projekt, který je hostován v systému souborů, laděn nebo procházen, Visual Studio 2005 automaticky spustí instanci ASP.NET vývojového serveru na náhodném portu pro obsluhu žádosti.

Další informace najdete na vývojovém serveru ASP.NET dále v tomto modulu.

## <a name="improved-file-management"></a>Vylepšená správa souborů

V aplikacích Visual Studio 2002 a 2003 je soubor projektu (. vbproj pro VB.NET a. csproj pro C#) uložený ve všech souborech ve webové aplikaci. Průzkumník řešení zobrazení je založeno na informacích o souboru v souboru projektu. Z tohoto důvodu Průzkumník řešení často zobrazovat nepřesné informace v případech, kdy byly použity externí editory. Sady Visual Studio 2002 a 2003 by často přepsaly změny souboru nebo nezobrazovaly nejaktuálnější verze souborů.

Visual Studio 2005 se souborem projektu. Místo toho přečte informace o souborech a složkách přímo z disku. Výsledkem je přesné zobrazení souborů v projektu. Vzhledem k tomu, že složka odkazy v aplikaci Visual Studio 2002 a 2003 nepředstavuje skutečnou složku ve vaší webové aplikaci, aplikace Visual Studio 2005 také odebere složku odkazy z Průzkumník řešení. Pro přístup k odkazům pro váš projekt v aplikaci Visual Studio 2005 byste měli použít stránky vlastností projektu.

## <a name="creating-web-projects"></a>Vytváření webových projektů

Vývojáři webu mají k dispozici mnoho nových možností pro vytváření projektů v aplikaci Visual Studio 2005. Weby se teď dají vytvářet kdekoli v systému souborů a pak je můžete ladit nebo procházet pomocí nového ASP.NET vývojového serveru. Vývojáři mohou vytvářet nové weby také pomocí protokolu FTP.

Kliknutím sem si můžete zobrazit video s návodem k vytváření webových projektů v aplikaci Visual Studio 2005.

![](improvements-in-visual-studio-2005/_static/image1.png)

[Otevření videa na celé obrazovce](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)

### <a name="file-system-projects"></a>Projekty systému souborů

Jak jste viděli v návodu k videu, můžete zvolit vytvoření webů v systému souborů buď na místním počítači, nebo na vzdáleném umístění přes sdílenou složku. Weby, které jsou vytvořené v systému souborů, se procházejí a ladí pomocí ASP.NET vývojového serveru.

> [!NOTE]
> ASP.NET vývojový server může pro zákazníky způsobit nějaký nejasnost. Pokud je webový projekt vytvořen v systému souborů ve struktuře adresáře IISs (tj. c:/Inetpub/wwwroot), web bude i nadále procházen prostřednictvím vývojového serveru ASP.NET při spuštění z aplikace Visual Studio 2005. Proto se žádná konfigurace služby IIS (tj. metody ověřování) nedá použít.

Výchozí webový projekt také odstraní velkou režii, protože obsahuje jenom stránku Default. aspx, soubor default.cs a složku App/_Data. Soubor Web. config a speciální složky (tj. app/_code) jsou přidány, jak jsou potřeba. Váš webový projekt obsahuje pouze soubory a složky, které potřebujete.

### <a name="http-projects"></a>Projekty HTTP

Projekty HTTP mohou být buď projekty, které jsou vytvořeny na místním webu služby IIS nebo na vzdáleném webu. Výchozí umístění projektu je `http://localhost`. Pokud kliknete na tlačítko Procházet, jsou k dispozici dvě možnosti protokolu HTTP: místní služba IIS a vzdálený web. Hlavní rozdíl v těchto dvou možnostech je způsob, jakým se v dialogovém okně Vybrat umístění zobrazují informace o webu a jak se zkopírují soubory na webový server.

Možnost místní služby IIS čte informace o lokalitě z metabáze v místním počítači a soubory jsou zkopírovány pomocí systému souborů. Možnost Vzdálená lokalita používá rozšíření serveru FrontPage a informace o lokalitě a soubory jsou zkopírovány pomocí volání RPC protokolu HTTP a rozšíření serveru FrontPage.

> [!NOTE]
> Soubor vs # # #/_tmp. htm a Get/_aspx/_ver. aspx se již nepoužívají k určení informací o verzi.

Výchozí možnost HTTP je místní služba IIS. Tato možnost přečte metabázi služby IIS a určí, které lokality jsou k dispozici, a umístění, ve kterém má být vytvořen obsah. Můžete vybrat jinou složku nebo virtuální adresář tím, že ji vyberete ve stromovém zobrazení. Můžete také vytvořit nový virtuální adresář, označit složky jako aplikace a také odstranit existující virtuální adresáře z tohoto dialogového okna.

![Dialog zvolit umístění](improvements-in-visual-studio-2005/_static/image1.gif)

**Obrázek 1**: dialogové okno zvolit umístění

Na rozdíl od dřívějších verzí sady Visual Studio, pokud zaškrtnete políčko **použít SSL (Secure Sockets Layer)** a certifikát SSL se neshoduje s adresou URL, kterou prohlížíte, zobrazí se dialogové okno výstraha zabezpečení s dotazem, jestli chcete pokračovat. Pokud certifikát nesouhlasí s použitím sady Visual Studio .NET 2003, vytvoření projektu by nebylo úspěšné.

![Výstraha zabezpečení týkající se certifikátu SSL](improvements-in-visual-studio-2005/_static/image2.gif)

**Obrázek 2**: výstraha zabezpečení týkající se certifikátu SSL

### <a name="note-on-host-headers"></a>Poznámka k hlavičkám hostitele

Pokud vytváříte webovou aplikaci na webu vázaném na konkrétní IP adresu, budete muset zajistit, aby byla nakonfigurována Hlavička hostitele. V opačném případě Visual Studio vytvoří web na adrese `http://localhost`, ale IP adresa se nebude správně přeložit, pokud je lokalita procházena nebo Laděna v rámci rozhraní IDE.

Pokud vyberete možnost Vzdálená lokalita, dialogové okno se změní a umožní vám zadat cílovou adresu URL nového webu. Tato adresa URL musí být na serveru s povolenými rozšířeními FrontPage serveru. Pokud chcete pracovat s místním webovým serverem pomocí rozšíření serveru FrontPage, můžete použít možnost Vzdálená lokalita a zadat místní adresu URL.

![Vytvoření webu na vzdáleném serveru](improvements-in-visual-studio-2005/_static/image1.jpg)

**Obrázek 3**: vytvoření webu na vzdáleném serveru

Pokud se při vytváření aplikace na vzdálené lokalitě přes SSL neshoduje certifikát SSL, dialogové okno pro potvrzení se mírně liší od dialogu, který se zobrazuje při použití možnosti místní služba IIS.

![Výstraha zabezpečení vzdálené lokality](improvements-in-visual-studio-2005/_static/image3.gif)

**Obrázek 4**: výstraha zabezpečení vzdálené lokality

<a id="_Toc116100243"></a>

#### <a name="ftp"></a>FTP

Visual Studio 2005 zavádí možnost vytvářet weby prostřednictvím FTP. Když použijete tuto možnost, rozhraní IDE vytvoří soubory místně v dočasné složce uživatelů a pak pomocí protokolu FTP přesune soubory do umístění FTP.

> [!NOTE]
> Umístění složky Temp je c:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;název aplikace&gt;

Při použití možnosti FTP se zobrazí dialogové okno zvolit umístění. Do tohoto dialogu zadáte požadované informace o připojení FTP, jak je znázorněno níže.

![Dialog zvolit umístění pro FTP](improvements-in-visual-studio-2005/_static/image2.jpg)

**Obrázek 5**: dialogové okno zvolit umístění pro FTP

## <a name="lab-setup-ftp-site-and-create-a-project"></a>Testovací prostředí: nastavení serveru FTP a vytvoření projektu

Následující postup slouží ke konfiguraci serveru FTP tak, aby měl uživatel umístění, do kterého může nahrávat jenom přes FTP.

### <a name="install-the-ftp-service"></a>Instalace služby FTP

1. Otevřete panel Přidat nebo odebrat programy, vyberte možnost Přidat nebo odebrat součásti systému Windows.
2. Vyberte možnost Internetová informační služba (aplikační server ve Windows 2003) a klikněte na tlačítko **Podrobnosti**.
3. Zaškrtněte **službu Protokol FTP (File Transfer Protocol) (FTP)** a klikněte na **OK**.
4. Kliknutím na **Další** nainstalujete službu FTP.

### <a name="create-a-new-folder-for-content"></a>Vytvoření nové složky pro obsah

1. V Průzkumníku Windows vytvořte novou složku s názvem **Uživatel1** uvnitř c:/Inetpub/Wwwroot.

#### <a name="configure-folders-and-permissions-on-folders"></a>Nakonfigurujte složky a oprávnění pro složky.

1. Otevřete modul snap-in Internetová informační služba z nástrojů pro správu. Nyní budete mít složku servery FTP pod uzlem název počítače.
2. Rozbalte položku **servery FTP**.
3. Klikněte pravým tlačítkem na **výchozí server FTP**, vyberte **Nový**, pak **virtuální adresář**a pak klikněte na **Další**.
4. Jako název virtuálního adresáře zadejte **Uživatel1** a klikněte na **Další**.
5. Jako cestu zadejte **c:/Inetpub/wwwroot/uživatel1** a klikněte na **Další**.
6. Klikněte na tlačítko **Další** a **dokončete Průvodce** .
7. Klikněte pravým tlačítkem na virtuální adresář **user1** ve výchozím serveru FTP a vyberte **vlastnosti**.
8. Zaškrtněte políčko pro **zápis** a kliknutím na tlačítko **OK** zavřete dialogové okno.
9. Klikněte pravým tlačítkem na **výchozí server FTP** a vyberte **vlastnosti**.
10. Na kartě **účty zabezpečení** zrušte **povolení anonymních připojení**.
11. Klikněte na **Ano** v dialogovém okně s dotazem, jestli chcete pokračovat.
12. Kliknutím na tlačítko **OK** zavřete dialogové okno.
13. V uzlu **weby** rozbalte **výchozí webový server** .
14. Klikněte pravým tlačítkem na adresář **user1** a vyberte **vlastnosti** .
15. V části **nastavení aplikace** klikněte na **vytvořit** , aby se složka označila jako aplikace.
16. Kliknutím na tlačítko **OK** zavřete dialogové okno.
17. Zavřete modul snap-in Internetová informační služba.

### <a name="create-web-project"></a>Vytvořit webový projekt

1. Otevřete Visual Studio 2005.
2. V nabídce **soubor** klikněte na položku **Nový web**.
3. V rozevíracím seznamu **umístění** vyberte **FTP**.
4. Klikněte na **Browse** (Procházet).
5. Do textového pole **serveru** zadejte **localhost** .
6. Do textového pole adresáře zadejte **Uživatel1** .
7. Klikněte na **Otevřít**. Umístění FTP bude zadáno do dialogového okna Nový web.
8. Klikněte na tlačítko **OK**.
9. Zrušte kontrolu **anonymního přihlášení** v dialogovém okně přihlášení k FTP, zadejte své přihlašovací údaje a klikněte na **OK**.
10. Jaká je adresa URL projektu? (Adresa URL projektu se zobrazí v Průzkumník řešení.)
11. V nabídce **sestavení** vyberte možnost **Sestavit web** nebo **Sestavit řešení**.
12. V Průzkumník řešení klikněte pravým tlačítkem na Default. aspx a vyberte **Zobrazit v prohlížeči**.
13. V dialogovém okně požadovaná adresa URL webu zadejte pro adresu URL `http://localhost/user1` a klikněte na **OK**.

> [!NOTE]
> Pokud se zobrazí chyba upozorňující na neschopnost načíst typ nebo _Default, ujistěte se, že na vašem webu běží ASP.NET 2,0, a ne na starší verzi. To můžete provést na kartě ASP.NET v Internetová informační služba.

## <a name="opening-web-projects"></a>Otevírání webových projektů

Otevírání webových projektů se podobá vytváření projektů. V následujících částech jsou vyvolány oblasti a při práci v rámci integrovaného vývojového prostředí (IDE) si ponechte nějaké oči. Zahrnuje také práci s webovými projekty pomocí protokolu HTTP a FTP.

Chcete-li otevřít webový projekt, v nabídce soubor vyberte možnost otevřít web. Zobrazí se výzva se stejným dialogovým oknem zvolit umístění dříve a máte k dispozici stejné čtyři možnosti: systém souborů, místní služba IIS, FTP a vzdálená lokalita.

<a id="_Toc116100245"></a>

## <a name="file-system"></a>Systém souborů

Jak bylo uvedeno dříve v tomto modulu, Visual Studio již nepoužívá soubor projektu. Proto pokud se rozhodnete otevřít web ze systému souborů, máte ve skutečnosti možnost výběru libovolné složky, kterou chcete, a to i v případě, že se složka, kterou jste zvolili, nevytvořila jako webový projekt na začátku v aplikaci Visual Studio. Můžete například zvolit otevření složky dokumenty jako webu a aplikace Visual Studio bude Happily otevřít a zobrazit soubory, jak je uvedeno níže.

![Dokumenty otevřené jako web](improvements-in-visual-studio-2005/_static/image3.jpg)

**Obrázek 6**: *Moje dokumenty* otevřené jako web

Vzhledem k tomu, že Visual Studio v případě potřeby vytvoří pouze další soubory a složky, do umístění, které jste otevřeli, se nepřidaly žádné další soubory ani složky. Vedlejším účinkem této architektury je, že vám zabrání v vnořování webů do systému souborů. Zvažte například následující adresářovou strukturu.

Webový projekt na adrese C:/MyWebSite

Další webový projekt v C:/MyWebSite/Nested

Při otevření webu na adrese c:/MyWebSite se vnořená složka zobrazí jako podsložku této aplikace.

<a id="_Toc116100246"></a>

## <a name="http"></a>HTTP

Při otevírání webů prostřednictvím protokolu HTTP jsou nastavení čtena z metabáze služby IIS (místní IIS) nebo pomocí rozšíření FrontPage Server Extensions (vzdálené lokality). Pokud jsou k dispozici vnořené webové aplikace, zobrazí se i ikona, která je identifikuje jako aplikace. Pokud jste obeznámeni s používáním webových aplikací v aplikaci FrontPage, chování v sadě Visual Studio 2005 je podobné.

I když aplikace Visual Studio zobrazí ikonu pro aplikace, které jsou vnořené pod aplikací, která je aktuálně otevřena v rámci rozhraní IDE, neumožní vám jejich rozbalením zobrazit jejich obsah. Můžete je však otevřít dvojitým kliknutím na ně. Když to uděláte, zobrazí se dialogové okno s výzvou k otevření webové aplikace (a nahrazení aktuálně otevřeného řešení) nebo přidání webové aplikace do aktuálního řešení.

![Dvojitým kliknutím na ikonu vnořené aplikace zobrazíte tento dialog.](improvements-in-visual-studio-2005/_static/image4.jpg)

**Obrázek 7**: dvojitým kliknutím na ikonu vnořené aplikace zobrazíte tento dialog.

<a id="_Toc116100247"></a>

## <a name="ftp-site"></a>Server FTP

Když otevřete web prostřednictvím FTP, soubory se zkopírují místně do složky Temp. Úplná cesta k umístění místního úložiště se zobrazí v podokně Vlastnosti projektu a vytvoří se v následujícím formátu.

C:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;název aplikace&gt;

Při použití FTP bude Visual Studio muset zadat základní adresu URL pro váš projekt, abyste ho mohli procházet, jak je znázorněno níže. Pokud nezadáte základní adresu URL, aplikace Visual Studio vás na ni požádá při prvním pokusu o procházení stránky na webu.

![Určení základní adresy URL pro servery FTP](improvements-in-visual-studio-2005/_static/image5.jpg)

**Obrázek 8**: určení základní adresy URL pro servery FTP

## <a name="improvements-in-compilation"></a>Vylepšení kompilace

Práce s webovými aplikacemi v aplikaci Visual Studio 2005 je výrazně rychlejší než v předchozích verzích. To je způsobeno neomezenou částí pro změny v architektuře kompilace.

V aplikacích Visual Studio 2002 a 2003 byly webové aplikace kompilovány do jednoho primárního sestavení umístěného ve složce/bin. V aplikaci Visual Studio 2005 byla přidána složka aplikace nebo _Code. Třídy a jiný kód, který není uživatelským rozhraním, se přidají do složky App/_Code. Když Visual Studio sestaví projekt, všechny soubory ve složce App/_Code jsou kompilovány do jediného souboru App/_Code. dll. Výsledkem této změny je, že následné sestavení jsou mnohem rychlejší než v předchozích verzích.

> [!NOTE]
> Nástroj příkazového řádku MSBuild lze použít také k sestavení webových aplikací ASP.NET. Tento nástroj bude popsaný v modulu 9.

Další vylepšení kompilace je nová možnost stránky sestavení v nabídce sestavení. Tato funkce umožňuje vývojářům znovu sestavit pouze aktuální stránku (spolu s průběhem a závislostmi), aby se změny mohly kompilovat rychleji. Protože C# nástroj nenabízí kompilaci na pozadí pro účely aktualizace technologie IntelliSense atd., bude výhodou nesmírně z této funkce, protože umožní rychlé aktualizace technologie IntelliSense pouhým vytvořením jediné stránky.

Vlastnosti sestavení pro projekt umožňují konfigurovat typ sestavení, který proběhne před spuštěním úvodní stránky. Vývojáři mohou vytvořit pouze aktuální stránku, aby mohla aplikace Visual Studio začít ladit aplikace rychleji po změnách kódu.

![Úvodní akce stránky sestavení](improvements-in-visual-studio-2005/_static/image6.jpg)

**Obrázek 9**: akce zahájení stránky sestavení

Další skvělé vylepšení sady Visual Studio a architektury ASP.NET je v oblasti úprav a pokračování. V aplikaci Visual Studio 2005 mohou vývojáři spustit ladění projektu a provádět změny kódu v projektu bez odpojení ladicího programu. Ve skutečnosti můžete začít ladit projekt, přidat novou třídu, přidat do této třídy kód, přidat kód na stránku, která vytvoří novou instanci této třídy, a provést metodu třídy, a to vše bez odpojení ladicího programu. Spuštění nového kódu je doslova stejně snadné jako aktualizace prohlížeče.

Kliknutím sem zobrazíte podrobný návod k funkci upravit a pokračovat v aplikaci Visual Studio 2005.

![](improvements-in-visual-studio-2005/_static/image2.png)

[Otevření videa na celé obrazovce](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)

Robustní funkce úprav a pokračování v ASP.NET 2,0 a Visual Studio 2005 je způsobena změnou architektury pro ASP.NET aplikace. V ASP.NET 1. x byly aplikace vytvořené v aplikaci Visual Studio 2002/2003 zkompilovány do primárního sestavení, které bylo uloženo ve složce/bin. Všechny třídy, stránky atd. pro aplikaci byly zkompilovány do této jedné knihovny DLL. Pak za běhu ASP.NET zkompiluje všechny ovládací prvky, značky a ASP.NET kód v rámci stránek a zkopíruje tyto knihovny DLL do dočasné složky ASP.NET.

V aplikaci Visual Studio 2005 s použitím ASP.NET 2,0 jsou výše uvedené dva modely kompilace (jeden pro Visual Studio a jeden pro ASP.NET za běhu) byly sloučeny do jednoho společného kompilačního modelu. To znamená, že všechny problémy při kompilaci jsou nyní zachyceny během fáze vývoje místo za běhu. Umožňuje také podporu návrháře a IntelliSense pro funkce, jako jsou uživatelské ovládací prvky a stránky předlohy.

Kliknutím sem si můžete zobrazit video s návodem k podpoře návrháře pro uživatelské ovládací prvky.

![](improvements-in-visual-studio-2005/_static/image3.png)

[Otevření videa na celé obrazovce](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)

> [!NOTE]
> Při odebrání uživatelského ovládacího prvku ze stránky zůstane direktiva @Register ve značce a měla by být odebrána ručně, aby se předešlo chybám při analýze, pokud je uživatelský ovládací prvek odstraněn z webu.

Dalším vylepšením modelu kompilace sady Visual Studio je funkce Publikovat web. Vzhledem k tomu, že funkce publikování předkompiluje web, mohou vývojáři využít přizpůsobený výkon, který není nutné kompilovat na vyžádání. Také předkompiluje všechny zdrojové kódy ve složce App/_Code do knihovny DLL, takže není nutné nasadit zdrojový kód.

![Dialog publikovat web](improvements-in-visual-studio-2005/_static/image7.jpg)

**Obrázek 10**: dialog publikovat web

> [!NOTE]
> Nástroj ASPNET/_compile. exe lze také použít k předkompilování webové aplikace ASP.NET. Tento nástroj bude popsaný v modulu 9.

Při publikování webu jsou předkompilované soubory uloženy ve složce dočasných souborů ASP.NET, jak je znázorněno níže. Soubory s příponou *. Compiled* souboru jsou soubory XML, které definují závislosti pro konkrétní knihovny DLL. Všechny webové formuláře nebo uživatelské ovládací prvky jsou kompilovány do náhodných knihoven DLL, které začínají na *App/_Web/_* .

Pokud ponecháte zaškrtnuté políčko *Povolit tomuto předkompilovanému webu možnost aktualizovat* , značky uvnitř webových formulářů a uživatelských ovládacích prvků nebudou zkompilovány do knihovny DLL, což vám umožní provádět změny po nasazení. Pokud dáváte přednost zamčení značky, takže změny nasazeného obsahu nejsou povoleny, zrušte toto políčko.

Zaškrtávací políčko *použít pevné pojmenování a jedno stránky sestavení* vám umožní zakázat dávkovou kompilaci, aby každá stránka byla zkompilována do sestavení s pevným názvem. Když toto políčko nezaškrtnete, budete moct využít dávkovou kompilaci.

Zaškrtávací políčko *Povolit silné pojmenování v předkompilovaných sestaveních* umožňuje sestavit předkompilované sestavení pomocí silného názvu.

> [!NOTE]
> V ASP.NET 1. x musí být sestavení se silným názvem nainstalována do globální mezipaměti sestavení (GAC). V ASP.NET 2,0 není nutné instalovat sestavení se silným názvem do globální mezipaměti sestavení (GAC).

![Předkompilované soubory aplikací ASP.NET](improvements-in-visual-studio-2005/_static/image8.jpg)

**Obrázek 11**: předem kompilované soubory aplikací ASP.NET

> [!NOTE]
> V aplikaci výše nebyl nalezen žádný soubor Web. config. V případě, že by existoval, byl po procesu publikování webu volán *PrecompiledApp. config* .

## <a name="improvements-in-deployment"></a>Vylepšení nasazení

Stejně jako u sady Visual Studio 2002 a 2003 nabízí Visual Studio 2005 funkci kopírování projektu. Tato funkce je však v systému Visual Studio 2005 v dochovu a nyní se nazývá kopírování webu.

Dialog Kopírovat webovou stránku je rozdělen do levého a pravého rámce. Levý rámec se nazývá zdrojový web a pravý rámec se nazývá vzdálený web. Jednou z věcí, které mohou Zaměňujte některé vývojáře, je, že lokalita zobrazená v pravém rámci nemusí nutně být vzdáleným webem. Může to být web v místním systému souborů nebo místní instance služby IIS. Kromě toho lokalita zobrazená v levém snímku není nutně zdrojový web, protože dialogové okno vám umožňuje publikovat ze vzdáleného webu *na* zdrojový web.

Pokud kopírujete projekt na vzdálený webový server, musí mít tato lokalita nainstalované rozšíření serveru FrontPage. Pokud tomu tak není, budete se muset připojit pomocí FTP. Na druhé straně platí, že pokud kopírujete projekt do místní instance služby IIS, rozšíření serveru FrontPage se nevyžadují.

> [!NOTE]
> Pokud se pokusíte vytvořit nový web v místní instanci služby IIS a nainstalujete rozšíření serveru FrontPage 2002, zobrazí se chybová zpráva s oznámením, že vytváření webů není na serveru SharePoint podporováno. V takovém případě máte možnost nainstalovat rozšíření serveru FrontPage 2000 nebo odebrat rozšíření serveru FrontPage.

Kliknutím sem zobrazíte podrobný návod pro funkci kopírování webu.

![](improvements-in-visual-studio-2005/_static/image4.png)

[Otevření videa na celé obrazovce](improvements-in-visual-studio-2005/_static/copysite1.wmv)

## <a name="improvements-in-debugging"></a>Vylepšení ladění

V aplikaci Visual Studio 2005 jsou k dispozici čtyři klíčová vylepšení ladění.

- Ladění lokálně, jako není správce, je možné vymezit.
- Atribut debug elementu compilation je nyní ve výchozím nastavení false.
- Nastavení vzdáleného ladění a konfigurace je snazší než předtím.
- Nyní můžete ladit web otevřený přes FTP umístění.

## <a name="debugging-as-a-non-administrator"></a>Ladění jako správce bez oprávnění správce

Přidání ASP.NET vývojového serveru umožňuje správcům bez oprávnění snadno ladit aplikace ASP.NET přímo ze seznamu. Když je laděna aplikace ASP.NET spuštěná v místním systému souborů, Visual Studio spustí vývojový server ASP.NET v kontextu přihlášeného uživatele. Tento uživatel pak může tuto aplikaci ladit bez jakékoli další konfigurace.

## <a name="debug-is-false-by-default"></a>Ladění má ve výchozím nastavení hodnotu false.

V ASP.NET 1. x byl atribut *Debug* v elementu *compilation* v souboru Web. config ve výchozím nastavení nastaven na *hodnotu true* . Před nasazením aplikace do produkčního prostředí vždycky doporučujeme, aby vývojáři nastavili tento atribut na *false* , ale vzhledem k tomu, že většina vývojářů plně nerozumí důsledkům, kdy je atribut debug nastaven na hodnotu true, jednoduše ho odešlou tak, jak je.

Nejzávažnějším problémem s atributem Debug nastaveným na hodnotu true je, že zakáže rozhraní ASP. sítě model dávkové kompilace. Proto každá stránka je zkompilována do samostatné knihovny DLL. Pokud se webová aplikace skládá z tisíců stránek (bez nevyslechnutí jakýmkoli způsobem), znamená to, že tato aplikace vytvoří několik tisíc malých knihoven DLL. I když mají tyto knihovny DLL malou velikost, nejsou načteny do žádného konkrétního umístění v paměti. Proto způsobují fragmentaci v systémové paměti a můžou přispívat k OutOfMemoryExceptioným výskytům.

V ASP.NET 2,0 je ve výchozím nastavení atribut debug nastaven na hodnotu false. Jak už jste viděli, když vývojář ladit aplikaci ASP.NET v aplikaci Visual Studio 2005, zobrazí se výzva k přidání souboru Web. config s povoleným laděním. Tím dojde ke stejným nevýhodám, které byly přítomny v ASP.NET 1. x, ale nyní vývojář jasně varuje, že by měl být před přesunutím aplikace do produkčního atributu obnoven na hodnotu false.

## <a name="remote-debugging-setup-and-configuration"></a>Nastavení a konfigurace vzdáleného ladění

V aplikaci Visual Studio 2002/2003 se vzdálené ladění spoléhalo na Machine Debug Manager (MDM. exe) a v procesu Vs7jit. exe. Z toho důvodu řešení potíží se vzdáleným laděním bylo pro zákazníky často černým polem a často není mnohem lepší pro službu PSS.

Visual Studio 2005 odstraňuje závislosti na procesech MDM. exe a Vs7jit. exe. Místo toho teď používá službu Remote Debug Monitor Service (Msvsmon. exe).

Požadavek na ladění v aplikaci Visual Studio 2005 vzdáleně je poměrně jednoduchý. Před laděním musíte spustit msvsmon. exe na vzdáleném serveru. Sledování vzdáleného ladění můžete nainstalovat z disku CD sady Visual Studio nebo můžete jednoduše spustit msvsmon. exe ze sdílené složky bez nutnosti na webovém serveru vůbec nainstalovat cokoli.

Když spustíte msvsmon. exe, je pravděpodobný, že bude vytěžovat porty blokované pro vzdálené ladění. Naštěstí můžete porty snadno odblokovat přímo v dialogovém okně s upozorněním, jak je znázorněno níže.

![Oznámení, že brána Windows Firewall blokuje vzdálené ladění](improvements-in-visual-studio-2005/_static/image9.jpg)

**Obrázek 12**: oznámení, že brána Windows Firewall blokuje vzdálené ladění

Po odblokování portů potřebných pro ladění se zobrazí Sledování vzdáleného ladění, jak je znázorněno níže. Z tohoto rozhraní můžete snadno monitorovat připojení a měnit oprávnění k ladění.

![Sledování vzdáleného ladění](improvements-in-visual-studio-2005/_static/image10.jpg)

**Obrázek 13**: sledování vzdáleného ladění

Je také možné vzdáleně ladit webové aplikace otevřené prostřednictvím FTP. Postup je stejný jako dříve popsaný. Budete ale muset zadat základní adresu URL pro procházení projektu FTP, jak je uvedeno dříve v tomto modulu.

## <a name="lab-2"></a>Testovací prostředí 2

## <a name="remote-debugging-with-visual-studio-2005"></a>Vzdálené ladění pomocí sady Visual Studio 2005

Tato laboratoř vás provede vzdáleným laděním pomocí sady Visual Studio 2005.

Kliknutím sem zobrazíte návod k videu tohoto testovacího prostředí.

![](improvements-in-visual-studio-2005/_static/image5.png)

[Otevření videa na celé obrazovce](improvements-in-visual-studio-2005/_static/remdebug1.wmv)

Toto testovací prostředí vyžaduje, abyste měli dva počítače, jeden se systémem Visual Studio 2005 a další běžící IIS 5 nebo novější.

1. Otevřete Visual Studio 2005 a vytvořte nový web na vzdáleném serveru.

> [!NOTE]
> Web můžete vytvořit na vzdálené instanci služby IIS nebo přes FTP.

1. Na vzdáleném webovém serveru vyhledejte ve vývojovém počítači msvsmon. exe s použitím cesty UNC a spusťte ji.  
 Výchozím umístěním pro msvsmon. exe je//server/c $/Program Files/Microsoft Visual Studio 8/Common7/IDE/Remote Debugger/x86.
2. Pokud se zobrazí výzva k odblokování portů pro vzdálené ladění, udělejte to.
3. Z vývojového počítače otevřete kód na pozadí pro default. aspx a nastavte zarážku v metodě Page/_Load.
4. Spusťte ladění z vývojového počítače.

Zarážka by měla být dosaženo podle očekávání.

## <a name="aspnet-development-server"></a>Vývojový server ASP.NET

Jak už jsme probrali, Visual Studio 2005 se dodává s webovým serverem s názvem ASP.NET Development Server. (Vývojový server ASP.NET se někdy označuje jako Cassini.) Tento webový server je pohodlný způsob, jak procházet a ladit webové aplikace běžící v systému souborů.

ASP.NET Development Server je webový server s omezeným přístupem. Nepovoluje vzdálená připojení, neumožňuje žádné žádosti od jiného uživatele, než je uživatel, který spustil webový server. Nemá taky možnost obsluhovat stránky ASP. Budou obsluhovány pouze prostředky ASP.NET a HTML (včetně obrázků, souborů CSS atd.).

Vývojový server ASP.NET se dá spustit prostřednictvím příkazového řádku spuštěním souboru WebDev. webServer. exe, který se nachází v c:/Windows/Microsoft. NET/Framework/v 2.0./ */* / */* /*. Následující dialog zobrazuje dostupné parametry.

![](improvements-in-visual-studio-2005/_static/image11.jpg)

**Obrázek 14**

> [!NOTE]
> Server ASP.NET Development není podporován při explicitním spuštění prostřednictvím příkazového řádku.
