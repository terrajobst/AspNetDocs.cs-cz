---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs
title: Základní rozdíly mezi službou IIS a vývojovým serverem ASP.NETC#() | Microsoft Docs
author: rick-anderson
description: Při místním testování aplikace ASP.NET je pravděpodobné, že používáte vývojový webový server ASP.NET. Produkční web je ale nejpravděpodobnější po oddálení...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 13a5a423-9235-4dde-b408-2fd10f791d63
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs
msc.type: authoredcontent
ms.openlocfilehash: 7fea3939bd910a052340215c207013e2269f32a2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74617573"
---
# <a name="core-differences-between-iis-and-the-aspnet-development-server-c"></a>Hlavní rozdíly mezi službou IIS a serverem ASP.NET Development Server (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_06_CS.zip) nebo [stažení PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial06_WebServerDiff_cs.pdf)

> Při místním testování aplikace ASP.NET je pravděpodobné, že používáte vývojový webový server ASP.NET. Produkční web je ale pravděpodobně poháněn službou IIS. Existují některé rozdíly mezi tím, jak tyto webové servery zpracovávají požadavky. tyto rozdíly mohou mít důležité důsledky. V tomto kurzu se seznámíte s některými z dalších německých rozdílů.

## <a name="introduction"></a>Úvod

Pokaždé, když uživatel navštíví aplikaci ASP.NET, její prohlížeč odešle požadavek na web. Tento požadavek vybral software webového serveru, který koordinuje modul ASP.NET runtime, který vygeneruje a vrátí obsah pro požadovaný prostředek. [ Nternetový **i** nformation **S** ervices (IIS)](http://en.wikipedia.org/wiki/Internet_Information_Services) představují sadu služeb, které poskytují běžné internetové funkce pro servery Windows. Služba IIS je nejčastěji používaný webový server pro aplikace ASP.NET v produkčních prostředích. je nejpravděpodobnější, že software webového serveru používaný vaším poskytovatelem webového hostitele slouží k obsluze vaší aplikace ASP.NET. Službu IIS je také možné použít jako software webového serveru ve vývojovém prostředí, i když to zahrnuje instalaci služby IIS a správnou konfiguraci.

ASP.NET Development Server je alternativou možností webového serveru pro vývojové prostředí; dodává se s a je integrována do sady Visual Studio. Pokud webová aplikace není nakonfigurovaná na používání služby IIS, vývojový server ASP.NET se automaticky spustí a použije se jako webový server při první návštěvě webové stránky z aplikace Visual Studio. Ukázková webová aplikace, kterou jsme vytvořili zpátky v části [*určení toho, jaké soubory je potřeba nasadit*](determining-what-files-need-to-be-deployed-cs.md) , byly webové aplikace založené na systému souborů, které nebyly nakonfigurovány na používání služby IIS. Proto při návštěvě některé z těchto webů z aplikace Visual Studio se používá vývojový server ASP.NET.

V ideálním světě by prostředí pro vývoj a produkci bylo stejné. Jak jsme však probrali v předchozím kurzu, není to pro prostředí neobvyklé, protože by se lišilo nastavení konfigurace. Použití jiného softwaru webového serveru v prostředích přidává další proměnnou, která se musí vzít v úvahu při nasazování aplikace. Tento kurz se zabývá klíčovými rozdíly mezi službou IIS a vývojovým serverem ASP.NET. Z důvodu těchto rozdílů existují scénáře, kdy kód, který spouští bezchybně ve vývojovém prostředí, vyvolá výjimku nebo se při spuštění v produkčním prostředí chová jinak.

## <a name="security-context-differences"></a>Rozdíly v kontextu zabezpečení

Pokaždé, když software webového serveru zpracuje příchozí požadavek, který přidruží tuto žádost k určitému kontextu zabezpečení. Tyto informace o kontextu zabezpečení se používají v operačním systému k určení akcí, které je možné požadovat. Například stránka ASP.NET může obsahovat kód, který protokoluje určitou zprávu do souboru na disku. Aby tato stránka ASP.NET běžela bez chyby, musí mít kontext zabezpečení příslušná oprávnění na úrovni systému souborů, konkrétně oprávnění k zápisu do tohoto souboru.

ASP.NET Development Server přidruží příchozí požadavky k kontextu zabezpečení aktuálně přihlášeného uživatele. Pokud jste k počítači přihlášeni jako správce, budou stránky ASP.NET obsluhované vývojovým serverem ASP.NET mít stejná přístupová práva jako správce. Požadavky ASP.NET zpracovávané službou IIS jsou však přidruženy k určitému účtu počítače. Ve výchozím nastavení se účet počítače síťové služby používá ve verzích 6 a 7, i když váš poskytovatel webového hostitele může nakonfigurovat jedinečný účet pro každého zákazníka. A co víc, váš poskytovatel webového hostitele nejspíš udělil omezená oprávnění k tomuto účtu počítače. Výsledkem je, že můžete mít webové stránky, které se spouštějí bez chyb ve vývojovém prostředí, ale vygenerujete výjimky související s autorizací při hostování v produkčním prostředí.

Chcete-li zobrazit tento typ chyby v akci, kterou jsem vytvořili na webu Recenze knihy, která vytvoří soubor na disku, kde je uložen nejnovější datum a čas, který si někdo prohlížel v *ASP.NET 3,5 během 24 hodin* . Pokud chcete postup sledovat, otevřete stránku `~/Tech/TYASP35.aspx` a přidejte následující kód do obslužné rutiny události `Page_Load`:

[!code-csharp[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample1.cs)]

> [!NOTE]
> [Metoda`File.WriteAllText`](https://msdn.microsoft.com/library/system.io.file.writealltext.aspx) vytvoří nový soubor, pokud neexistuje, a zapíše do něj zadaný obsah. Pokud soubor již existuje, je existující obsah přepsán.

V dalším kroku si Projděte příručku *ASP.NET 3,5 ve 24 hodinách* stránky recenze ve vývojovém prostředí pomocí vývojového serveru ASP.NET. Za předpokladu, že jste přihlášeni k počítači pomocí účtu, který má odpovídající oprávnění k vytvoření a úpravě textového souboru v kořenovém adresáři webové aplikace, bude recenze knihy stejná jako předtím, ale pokaždé, když se stránka navštíví, je data a čas a IP adresa uživatele uloženy v souboru `LastTYASP35Access.txt`. Nasměrujte svůj prohlížeč na tento soubor; měla by se zobrazit zpráva podobná té, která je znázorněna na obrázku 1.

[![textový soubor obsahuje poslední datum a čas, kdy byla recenze knihy navštívena.](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image2.png)](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image1.png)

**Obrázek 1**: textový soubor obsahuje poslední datum a čas, kdy se provedla revize knihy ([kliknutím zobrazíte obrázek v plné velikosti).](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image3.png)

Nasaďte webovou aplikaci do produkčního prostředí a potom navštivte hostovanou *výuku sami ASP.NET 3,5 na* stránce recenze na 24 hodin. V tomto okamžiku byste měli vidět stránku recenze knihy jako normální nebo chybovou zprávu zobrazenou na obrázku 2. Někteří poskytovatelé webového hostitele udělují oprávnění k zápisu na účet anonymního ASP.NET počítače. v takovém případě bude stránka fungovat bez chyby. Pokud ale poskytovatel webového hostitele zakáže přístup k zápisu pro anonymní účet, vyvolá se [výjimka`UnauthorizedAccessException`](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) , když se stránka `TYASP35.aspx` pokusí zapsat aktuální datum a čas do souboru `LastTYASP35Access.txt`.

[![výchozí účet počítače používaný službou IIS nemá oprávnění k zápisu do systému souborů.](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image5.png)](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image4.png)

**Obrázek 2**: výchozí účet počítače používaný službou IIS nemá oprávnění k zápisu do systému souborů ([kliknutím zobrazíte obrázek v plné velikosti).](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image6.png)

Dobrá zpráva je, že většina poskytovatelů webových hostitelů má nějaký nástroj pro řazení oprávnění, který umožňuje určit na svém webu oprávnění systému souborů. Udělte účtu Anonymous ASP.NET přístup pro zápis do kořenového adresáře a pak znovu navštivte stránku recenze knihy. (V případě potřeby se obraťte na svého poskytovatele webového hostitele, kde najdete informace o tom, jak udělit výchozímu účtu ASP.NET oprávnění k zápisu.) Tentokrát by se stránka měla načíst bez chyby a soubor `LastTYASP35Access.txt` by měl být úspěšně vytvořen.

Tady je to, že protože vývojový server ASP.NET funguje v jiném kontextu zabezpečení než IIS, je možné, že stránky ASP.NET, které čtou nebo zapisují do systému souborů, čtou nebo zapisují do protokolu událostí systému Windows nebo čtou nebo zapisují do Windows.  Registr bude fungovat podle očekávání při vývoji, ale vygeneruje výjimky při výrobě. Při sestavování webové aplikace, která bude nasazena do sdíleného prostředí pro hostování webů, nečtěte ani nezapište do protokolu událostí ani do registru systému Windows. Také si poznamenejte všechny ASP.NET stránky, které čtou nebo zapisují do systému souborů, protože možná budete muset udělit oprávnění ke čtení a zápisu pro příslušné složky v produkčním prostředí.

## <a name="differences-on-serving-static-content"></a>Rozdíly v zachovávání statického obsahu

Dalším základním rozdílem mezi službou IIS a vývojovým serverem ASP.NET je způsob, jakým zpracovávají požadavky na statický obsah. Každý požadavek, který přichází do vývojového serveru ASP.NET, ať už se jedná o stránku ASP.NET, obrázek nebo soubor JavaScriptu, se zpracovává modulem runtime ASP.NET. Služba IIS ve výchozím nastavení vyvolá modul runtime ASP.NET jenom v případě, že žádost přichází pro prostředek ASP.NET, jako je například webová stránka ASP.NET, Webová služba a tak dále. Požadavky na statický obsah – obrázky, soubory CSS, soubory JavaScriptu, soubory PDF, soubory ZIP a podobné – jsou načítány službou IIS bez účasti modulu runtime ASP.NET. (Pro další informace můžete službě IIS dát pokyn, aby fungovala s modulem runtime ASP.NET. Další informace najdete v části provádění ověřování založeného na formulářích a ověřování URL ve statických souborech pomocí IIS 7 v tomto kurzu.)

Modul runtime ASP.NET provádí několik kroků k vygenerování požadovaného obsahu, včetně ověřování (Identifikace žadatele) a autorizaci (určení, jestli žadatel má oprávnění k zobrazení požadovaného obsahu). Oblíbená forma ověřování je ověřování pomocí *formulářů*, ve kterém je uživatel identifikovaný zadáním přihlašovacích údajů – obvykle uživatelské jméno a heslo – do textových polí na webové stránce. Při ověřování svých přihlašovacích údajů web ukládá do prohlížeče uživatele soubor cookie *ověřovacího lístku* , který se pošle s každým dalším požadavkem na web a slouží k ověření uživatele. Kromě toho je možné zadat autorizační pravidla *URL* , která určují, co uživatelé můžou nebo nemají přístup k určité složce. Mnoho webů ASP.NET používá ověřování pomocí formulářů a autorizaci adres URL pro podporu uživatelských účtů a k definování částí webu, které jsou přístupné pouze ověřeným uživatelům nebo uživatelům patřícím do určité role.

> [!NOTE]
> Pro důkladné vyhodnocení ASP. Ověřování založené na formulářích, autorizace adres URL a další funkce související s uživatelským účtem, najdete v [kurzech zabezpečení webu](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md).

Vezměte v úvahu web, který podporuje uživatelské účty pomocí ověřování na základě formulářů, a má složku, která používá autorizaci adresy URL, aby povolovala pouze ověřené uživatele. Představte si, že tato složka obsahuje stránky ASP.NET a soubory PDF a že je záměrem zobrazit tyto soubory PDF pouze ověření uživatelé.

Co se stane, když se návštěvník pokusí zobrazit jeden z těchto souborů PDF, a to zadáním adresy URL přímo v adresním řádku prohlížeče? Chcete-li zjistit, vytvořte novou složku na webu recenze webů, přidejte nějaké soubory PDF a nakonfigurujte lokalitu, aby používala autorizaci adresy URL, aby bylo zakázáno anonymním uživatelům v návštěvě této složky. Pokud si stáhnete ukázkovou aplikaci, uvidíte, že jsem vytvořila složku s názvem `PrivateDocs` a přidala PDF z [kurzů zabezpečení webu](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md) (jak to funguje). Složka `PrivateDocs` obsahuje taky `Web.config` soubor, který určuje autorizační pravidla URL pro odepření anonymních uživatelů:

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample2.xml)]

Nakonec jsem nakonfigurovali webovou aplikaci tak, aby používala ověřování založené na formulářích, a to tak, že aktualizuje soubor `Web.config` v kořenovém adresáři. nahrazuje:

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample3.xml)]

Řetězce

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample4.xml)]

Pomocí vývojového serveru ASP.NET přejděte na web a zadejte přímou adresu URL k jednomu ze souborů PDF v adresním řádku prohlížeče. Pokud jste si stáhli web přidružený k tomuto kurzu, adresa URL by měla vypadat nějak takto: `http://localhost:portNumber/PrivateDocs/aspnet_tutorial01_Basics_vb.pdf`

Když zadáte tuto adresu URL do adresního řádku, prohlížeč pošle požadavek na ASP.NET vývojový server pro daný soubor. Vývojový server ASP.NET předá požadavek na modul runtime ASP.NET ke zpracování. Vzhledem k tomu, že jsme se ještě přihlásili, a protože `Web.config` ve `PrivateDocs` složce je nakonfigurovaná tak, aby odepřela anonymní přístup, modul runtime ASP.NET automaticky přesměruje nás na přihlašovací stránku `Login.aspx` (viz obrázek 3). Při přesměrování uživatele na přihlašovací stránku zahrnuje ASP.NET parametr `ReturnUrl` QueryString, který indikuje stránku, kterou se uživatel pokusil zobrazit. Po úspěšném přihlášení uživatele se může tato stránka vrátit.

[![neoprávněným uživatelům budou automaticky přesměrováni na přihlašovací stránku](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image8.png)](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image7.png)

**Obrázek 3**: neoprávnění uživatelé se automaticky přesměrují na přihlašovací stránku ([kliknutím zobrazíte obrázek v plné velikosti).](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image9.png)

Teď se podívejme na to, jak se to chová v produkčním prostředí. Nasaďte aplikaci a zadejte přímou adresu URL k jednomu z souborů PDF ve složce `PrivateDocs` v produkčním prostředí. Tím se zobrazí výzva prohlížeče, aby se odeslal požadavek na soubor služby IIS. Vzhledem k tomu, že je požadován statický soubor, služba IIS načte a vrátí soubor bez vyvolání modulu runtime ASP.NET. V důsledku toho se neprováděla žádná kontrolní autorizace adresy URL. obsah souboru s přímým přístupem je k dispozici všem, kdo zná přímo adresu URL souboru.

[![anonymní uživatelé mohou stahovat soukromé soubory PDF zadáním přímé adresy URL do souboru.](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image11.png)](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image10.png)

**Obrázek 4**: anonymní uživatelé můžou stahovat soukromé soubory PDF zadáním přímé adresy URL souboru ([kliknutím zobrazíte obrázek v plné velikosti).](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image12.png)

### <a name="performing-forms-based-authentication-and-url-authentication-on-static-files-with-iis-7"></a>Provádění ověřování pomocí formulářů a ověřování adres URL ve statických souborech se službou IIS 7

Existuje několik postupů, které můžete použít k ochraně statického obsahu před neoprávněnými uživateli. Služba IIS 7 představila *Integrovaný kanál*, který manželství pracovní postup služby IIS pomocí pracovního postupu modulu runtime ASP.NET. V kostce můžete službě IIS dát pokyn, aby vyvolala moduly ověřování a autorizace modulu runtime ASP.NET všechny příchozí požadavky (včetně statických obsahu, jako jsou soubory PDF). Obraťte se na poskytovatele webového hostitele, kde zjistíte, jak nakonfigurovat web tak, aby používal integrovaný kanál.

Jakmile je služba IIS nakonfigurovaná tak, aby používala integrovaný kanál, přidejte následující kód do souboru `Web.config` v kořenovém adresáři:

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample5.xml)]

Tento kód instruuje službu IIS 7, aby používala moduly ověřování a autorizace založené na ASP.NET. Znovu nasaďte aplikaci a pak znovu navštivte soubor PDF. Tentokrát, když služba IIS zpracuje požadavek, poskytne logice pro ověřování a autorizaci modulu runtime ASP.NET možnost zkontrolovat požadavek. Vzhledem k tomu, že pouze ověření uživatelé mají oprávnění k zobrazení obsahu ve složce `PrivateDocs`, anonymní návštěvník se automaticky přesměruje na stránku pro přihlášení (odkaz zpět na obrázek 3).

> [!NOTE]
> Pokud váš poskytovatel webového hostitele stále používá službu IIS 6, nemůžete použít funkci integrovaného kanálu. Jedním z možných řešení je umístit soukromé dokumenty do složky, která zakáže přístup k protokolu HTTP (například `App_Data`), a pak vytvořit stránku, která bude obsluhovat tyto dokumenty. Tato stránka může být volána `GetPDF.aspx`a je předána název souboru PDF prostřednictvím parametru QueryString. Stránka `GetPDF.aspx` nejdříve ověří, zda má uživatel oprávnění k zobrazení souboru, a pokud ano, použije metodu [`Response.WriteFile(filePath)`](https://msdn.microsoft.com/library/system.web.httpresponse.writefile.aspx) k odeslání obsahu požadovaného souboru PDF zpět žádajícímu klientovi. Tento postup by taky mohl fungovat pro IIS 7, pokud jste nechtěli povolit integrovaný kanál.

## <a name="summary"></a>Přehled

Webové aplikace v produkčním prostředí jsou hostovány pomocí softwaru webového serveru služby IIS společnosti Microsoft. Ve vývojovém prostředí se ale aplikace může hostovat pomocí služby IIS nebo vývojového serveru ASP.NET. V ideálním případě by se měl stejný software webového serveru používat v obou prostředích, protože při použití jiného softwaru se v kombinaci přidá další proměnná. Nicméně snadné použití vývojového serveru ASP.NET umožňuje atraktivní výběr ve vývojovém prostředí. Dobrá zpráva je, že existuje jenom několik základních rozdílů mezi službou IIS a vývojovým serverem ASP.NET a pokud si o těchto rozdílech víte, jak zajistit, aby aplikace fungovala a fungovala stejným způsobem bez ohledu na hlediska.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Integrace ASP.NET se službou IIS 7,0](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)
- [Použití ověřování pomocí fór ASP.NET se všemi typy obsahu ve službě IIS 7](https://blogs.iis.net/bills/archive/2007/05/19/using-asp-net-forms-authentication-with-all-types-of-content-with-iis7-video.aspx) (video)
- [Webové servery v aplikaci Visual Web Developer](https://msdn.microsoft.com/library/58wxa9w5.aspx)

> [!div class="step-by-step"]
> [Předchozí](common-configuration-differences-between-development-and-production-cs.md)
> [Další](deploying-a-database-cs.md)
