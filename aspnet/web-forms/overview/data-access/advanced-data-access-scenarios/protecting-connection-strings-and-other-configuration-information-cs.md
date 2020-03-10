---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/protecting-connection-strings-and-other-configuration-information-cs
title: Ochrana připojovacích řetězců a dalších konfiguračních údajůC#() | Microsoft Docs
author: rick-anderson
description: Aplikace ASP.NET obvykle ukládá informace o konfiguraci do souboru Web. config. Některé z těchto informací jsou citlivé a opravňují ochranu. Podle definice...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: ad8dd396-30f7-4abe-ac02-a0b84422e5be
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/protecting-connection-strings-and-other-configuration-information-cs
msc.type: authoredcontent
ms.openlocfilehash: 15970bee1e990d3a139673efe12486e08f79814c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78524736"
---
# <a name="protecting-connection-strings-and-other-configuration-information-c"></a>Ochrana připojovacích řetězců a dalších konfiguračních údajů (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_73_CS.zip) nebo [stažení PDF](protecting-connection-strings-and-other-configuration-information-cs/_static/datatutorial73cs1.pdf)

> Aplikace ASP.NET obvykle ukládá informace o konfiguraci do souboru Web. config. Některé z těchto informací jsou citlivé a opravňují ochranu. Ve výchozím nastavení se tento soubor neobsluhuje návštěvníkovi webu, ale správce nebo počítačový podvodník může získat přístup k systému souborů webového serveru a zobrazit obsah souboru. V tomto kurzu se naučíme, že ASP.NET 2,0 umožňuje chránit citlivé informace tím, že šifruje oddíly souboru Web. config.

## <a name="introduction"></a>Úvod

Informace o konfiguraci pro aplikace ASP.NET se běžně ukládají do souboru XML s názvem `Web.config`. V průběhu těchto kurzů jsme aktualizovali `Web.config` několik. Při vytváření `Northwind` typované datové sady v [prvním kurzu](../introduction/creating-a-data-access-layer-cs.md), například informace o připojovacím řetězci byly automaticky přidány do `Web.config` v části `<connectionStrings>`. Později v kurzu [stránky předlohy a navigace na webu](../introduction/master-pages-and-site-navigation-cs.md) ručně aktualizujeme `Web.config`a přidáte `<pages>` element, což znamená, že všechny stránky ASP.NET v našem projektu by měly používat motiv `DataWebControls`.

Vzhledem k tomu, že `Web.config` může obsahovat citlivá data, jako jsou připojovací řetězce, je důležité, aby obsah `Web.config` byl zabezpečený a skrytý proti neoprávněným divákům. Ve výchozím nastavení jsou všechny požadavky HTTP na soubor s rozšířením `.config` zpracovávány modulem ASP.NET, který vrací *Tento typ stránky není obsluhován* na obrázku 1. To znamená, že Návštěvníci nemůžou zobrazit obsah souborů `Web.config`, a to pouhým zadáním http://www.YourServer.com/Web.config do svého panelu Adresa v prohlížeči.

[![návštěvě souboru Web. config prostřednictvím prohlížeče vrátí tento typ stránky zprávu o tom, že není obsluhován.](protecting-connection-strings-and-other-configuration-information-cs/_static/image2.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image1.png)

**Obrázek 1**: navštívení `Web.config` prostřednictvím prohlížeče vrátí tento typ stránky neobsluhuje zprávu ([kliknutím zobrazíte obrázek v plné velikosti).](protecting-connection-strings-and-other-configuration-information-cs/_static/image3.png)

Ale co když útočník dokáže najít nějaký jiný způsob zneužití, který mu umožní zobrazit obsah souborů `Web.config`? Co by útočník mohl s těmito informacemi dělat a jaké kroky je možné provést k další ochraně citlivých informací v rámci `Web.config`? Naštěstí většina sekcí v `Web.config` neobsahuje citlivé informace. Jaká škoda může útočník napadnout, pokud zná název výchozího motivu používaného vašimi ASP.NET stránkami?

Některé `Web.config` ale obsahují citlivé informace, které mohou obsahovat připojovací řetězce, uživatelská jména, hesla, názvy serverů, šifrovací klíče a tak dále. Tyto informace se většinou nacházejí v následujících částech `Web.config`:

- `<appSettings>`
- `<connectionStrings>`
- `<identity>`
- `<sessionState>`

V tomto kurzu se podíváme na techniky ochrany takových citlivých informací o konfiguraci. Jak uvidíme, .NET Framework verze 2,0 obsahuje chráněný systém konfigurace, který umožňuje programově šifrovat a dešifrovat vybrané konfigurační oddíly a Breeze.

> [!NOTE]
> Tento kurz se uzavírá s doporučeními Microsoftu pro připojení k databázi z aplikace ASP.NET. Kromě šifrování připojovacích řetězců můžete zvýšit zabezpečení systému tím, že zajistíte, že se k databázi připojíte zabezpečeným způsobem.

## <a name="step-1-exploring-aspnet-20-s-protected-configuration-options"></a>Krok 1: prozkoumání možností chráněné konfigurace ASP.NET 2,0 s

ASP.NET 2,0 obsahuje chráněný konfigurační systém pro šifrování a dešifrování informací o konfiguraci. To zahrnuje metody v .NET Framework, které lze použít k programovému šifrování nebo dešifrování informací o konfiguraci. Chráněný konfigurační systém používá [model poskytovatele](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx), který vývojářům umožňuje vybrat, jaká kryptografická implementace se použije.

.NET Framework se dodává se dvěma poskytovateli Protected Configuration:

- [`RSAProtectedConfigurationProvider`](https://msdn.microsoft.com/library/system.configuration.rsaprotectedconfigurationprovider.aspx) – používá asymetrický [algoritmus RSA](http://en.wikipedia.org/wiki/Rsa) pro šifrování a dešifrování.
- [`DPAPIProtectedConfigurationProvider`](https://msdn.microsoft.com/system.configuration.dpapiprotectedconfigurationprovider.aspx) – používá pro šifrování a dešifrování Windows [Data Protection API (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx) .

Vzhledem k tomu, že systém chráněné konfigurace implementuje vzor návrhu poskytovatele, je možné vytvořit vlastního poskytovatele chráněné konfigurace a připojit ho k aplikaci. Další informace o tomto procesu najdete v tématu [implementace zprostředkovatele chráněné konfigurace](https://msdn.microsoft.com/library/wfc2t3az(VS.80).aspx) .

Zprostředkovatelé RSA a DPAPI používají klíče pro své šifrovací a dešifrovací rutiny a tyto klíče je možné uložit na úrovni počítače nebo uživatele. Klíče na úrovni počítače jsou ideální pro scénáře, ve kterých se webová aplikace spouští na vlastním vyhrazeném serveru, nebo pokud na serveru existuje víc aplikací, které potřebují sdílet šifrované informace. Klíče na úrovni uživatele jsou bezpečnější možností ve sdílených hostitelských prostředích, kde jiné aplikace na stejném serveru by neměly mít možnost dešifrovat oddíly chráněné konfigurace aplikace.

V tomto kurzu budou v našem příkladu použity klíče zprostředkovatele DPAPI a na úrovni počítače. Konkrétně se podíváme na šifrování oddílu `<connectionStrings>` v `Web.config`, i když chráněný konfigurační systém lze použít k šifrování většiny `Web.config` oddílu. Informace o použití klíčů na úrovni uživatele nebo pomocí poskytovatele RSA najdete v části zdroje informací v části Další informace na konci tohoto kurzu.

> [!NOTE]
> Poskytovatelé `RSAProtectedConfigurationProvider` a `DPAPIProtectedConfigurationProvider` jsou registrováni v `machine.config` souboru s názvy zprostředkovatelů `RsaProtectedConfigurationProvider` a `DataProtectionConfigurationProvider`. Při šifrování nebo dešifrování informací o konfiguraci bude potřeba zadat příslušný název poskytovatele (`RsaProtectedConfigurationProvider` nebo `DataProtectionConfigurationProvider`) místo skutečného názvu typu (`RSAProtectedConfigurationProvider` a `DPAPIProtectedConfigurationProvider`). Soubor `machine.config` můžete najít ve složce `$WINDOWS$\Microsoft.NET\Framework\version\CONFIG`.

## <a name="step-2-programmatically-encrypting-and-decrypting-configuration-sections"></a>Krok 2: šifrování a dešifrování konfiguračních oddílů prostřednictvím kódu programu

Pomocí několika řádků kódu můžeme šifrovat nebo dešifrovat konkrétní konfigurační oddíl pomocí zadaného zprostředkovatele. Kód, jak uvidíme krátce, stačí programově odkazovat na příslušný konfigurační oddíl, zavolat jeho `ProtectSection` nebo `UnprotectSection` metodu a pak zavolat metodu `Save`, aby se změny zachovaly. Kromě toho .NET Framework obsahuje užitečný nástroj příkazového řádku, který může šifrovat a dešifrovat informace o konfiguraci. Tento nástroj příkazového řádku budeme prozkoumat v kroku 3.

Pro ilustraci ochrany informací o konfiguraci pomocí programu vytvoříme stránku ASP.NET, která obsahuje tlačítka pro šifrování a dešifrování `Web.config``<connectionStrings>` v části.

Začněte tím, že otevřete stránku `EncryptingConfigSections.aspx` ve složce `AdvancedDAL`. Přetáhněte ovládací prvek TextBox z panelu nástrojů do návrháře, nastavte jeho vlastnost `ID` na `WebConfigContents`, jeho vlastnost `TextMode` na `MultiLine`a jeho `Width` a `Rows` vlastnosti na 95% a 15 v uvedeném pořadí. V tomto ovládacím prvku TextBox se zobrazí obsah `Web.config`, který nám umožní rychle zjistit, jestli je obsah zašifrovaný. Samozřejmě v reálné aplikaci byste nikdy neměli chtít zobrazit obsah `Web.config`.

Pod textovým polem přidejte dva ovládací prvky tlačítko s názvem `EncryptConnStrings` a `DecryptConnStrings`. Nastavte jejich vlastnosti textu pro šifrování připojovacích řetězců a dešifrování připojovacích řetězců.

V tuto chvíli by vaše obrazovka měla vypadat podobně jako na obrázku 2.

[![přidat webové ovládací prvky TextBox a dva tlačítka na stránku](protecting-connection-strings-and-other-configuration-information-cs/_static/image5.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image4.png)

**Obrázek 2**: Přidání ovládacího prvku TextBox a dva webové ovládací prvky tlačítka na stránku ([kliknutím zobrazíte obrázek v plné velikosti](protecting-connection-strings-and-other-configuration-information-cs/_static/image6.png))

Dále je potřeba napsat kód, který načte a zobrazí obsah `Web.config` v textovém poli `WebConfigContents` při prvním načtení stránky. Přidejte následující kód do třídy stránky s kódem na pozadí. Tento kód přidá metodu nazvanou `DisplayWebConfig` a zavolá ji z obslužné rutiny události `Page_Load`, pokud je `Page.IsPostBack` `false`:

[!code-csharp[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample1.cs)]

Metoda `DisplayWebConfig` používá [třídu`File`](https://msdn.microsoft.com/library/system.io.file.aspx) k otevření souboru `Web.config` aplikace, [třídy`StreamReader`](https://msdn.microsoft.com/library/system.io.streamreader.aspx) ke čtení jeho obsahu do řetězce a [třídu`Path`](https://msdn.microsoft.com/library/system.io.path.aspx) pro vygenerování fyzické cesty k souboru `Web.config`. Tyto tři třídy jsou všechny nalezeny v [oboru názvů`System.IO`](https://msdn.microsoft.com/library/system.io.aspx). V důsledku toho budete muset přidat `using` `System.IO` příkaz do horní části třídy s kódem na pozadí, případně můžete předpony těchto názvů tříd pomocí `System.IO.`.

Dále je potřeba přidat obslužné rutiny událostí pro dvě ovládací prvky tlačítka `Click` události a přidat potřebný kód pro šifrování a dešifrování `<connectionStrings>` oddílu pomocí klíče na úrovni počítače se zprostředkovatelem rozhraní DPAPI. V Návrháři dvakrát klikněte na každé tlačítko a přidejte `Click` obslužnou rutinu události do třídy kódu na pozadí a poté přidejte následující kód:

[!code-csharp[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample2.cs)]

Kód použitý ve dvou obslužných rutinách událostí je téměř identický. Začínají tím, že získávají informace o aktuálním souboru aplikace `Web.config` pomocí metody [`WebConfigurationManager` třídy](https://msdn.microsoft.com/library/system.web.configuration.webconfigurationmanager.aspx) s [`OpenWebConfiguration`](https://msdn.microsoft.com/library/system.web.configuration.webconfigurationmanager.openwebconfiguration.aspx). Tato metoda vrací konfigurační soubor webu pro zadanou virtuální cestu. V dalším kroku se k `<connectionStrings>` oddílu `Web.config` soubory přistupují prostřednictvím metody [`Configuration` třídy](https://msdn.microsoft.com/library/system.configuration.configuration.aspx) s [`GetSection(sectionName)`](https://msdn.microsoft.com/library/system.configuration.configuration.getsection.aspx), která vrací objekt [`ConfigurationSection`](https://msdn.microsoft.com/library/system.configuration.configurationsection.aspx) .

Objekt `ConfigurationSection` obsahuje [vlastnost`SectionInformation`](https://msdn.microsoft.com/library/system.configuration.configurationsection.sectioninformation.aspx) , která poskytuje další informace a funkce týkající se konfiguračního oddílu. Jak vidíte výše uvedený kód, můžeme zjistit, jestli je konfigurační oddíl zašifrovaný, kontrolou vlastnosti `SectionInformation` vlastností s `IsProtected`. Oddíl je navíc možné šifrovat nebo dešifrovat prostřednictvím `SectionInformation` vlastností s `ProtectSection(provider)` a `UnprotectSection`mi metodami.

Metoda `ProtectSection(provider)` akceptuje jako vstup řetězec, který určuje název poskytovatele chráněné konfigurace, který se má použít při šifrování. V obslužné rutině tlačítka `EncryptConnString` tlačítko s předáte DataProtectionConfigurationProvider do metody `ProtectSection(provider)`, aby se použil poskytovatel rozhraní DPAPI. Metoda `UnprotectSection` může určit zprostředkovatele, který se použil k zašifrování konfiguračního oddílu, a proto nevyžaduje žádné vstupní parametry.

Po volání metody `ProtectSection(provider)` nebo `UnprotectSection` je nutné volat metodu `Configuration` objektu s [`Save`](https://msdn.microsoft.com/library/system.configuration.configuration.save.aspx) , aby se změny zachovaly. Po zašifrování nebo dešifrování informací o konfiguraci a uložení změn zavoláme `DisplayWebConfig` pro načtení aktualizovaného obsahu `Web.config` do ovládacího prvku TextBox.

Po zadání výše uvedeného kódu ho testujte na stránce `EncryptingConfigSections.aspx` v prohlížeči. Zpočátku byste měli vidět stránku, která obsahuje obsah `Web.config` s oddílem `<connectionStrings>` zobrazeným v prostém textu (viz obrázek 3).

[![přidat webové ovládací prvky TextBox a dva tlačítka na stránku](protecting-connection-strings-and-other-configuration-information-cs/_static/image8.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image7.png)

**Obrázek 3**: Přidání ovládacího prvku TextBox a dva webové ovládací prvky tlačítka na stránku ([kliknutím zobrazíte obrázek v plné velikosti](protecting-connection-strings-and-other-configuration-information-cs/_static/image9.png))

Nyní klikněte na tlačítko šifrovat připojovací řetězce. Pokud je povoleno ověřování žádosti, značka odeslaná zpátky z `WebConfigContents`ho textového pole vytvoří `HttpRequestValidationException`, která zobrazí zprávu, potenciálně nebezpečná `Request.Form` hodnota byla zjištěna z klienta. Požadavek na ověření, který je ve výchozím nastavení povolený v ASP.NET 2,0, zakáže zpětné odeslání, které zahrnuje nekódované HTML, a je navržený tak, aby se zabránilo útokům prostřednictvím injektáže skriptu. Tuto kontrolu je možné zakázat na úrovni stránky nebo aplikace. Pro vypnutí této stránky nastavte `ValidateRequest` nastavení na `false` v direktivě `@Page`. Direktiva `@Page` se nachází v horní části deklarativního označení stránky.

[!code-aspx[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample3.aspx)]

Další informace o ověření žádosti, jeho účelu, způsobu jeho zakázání na úrovni stránky a aplikace a o tom, jak kódovat kód HTML, najdete v tématu [ověření žádosti – předcházení útokům pomocí skriptů](../../../../whitepapers/request-validation.md).

Po zakázání žádosti o ověření pro stránku zkuste znovu kliknout na tlačítko šifrovat připojovací řetězce. Při zpětném odeslání se k konfiguračnímu souboru dostanete a jeho `<connectionStrings>` oddíl zašifrovaný pomocí poskytovatele rozhraní DPAPI. Textové pole se pak aktualizuje, aby se zobrazil nový `Web.config` obsah. Jak ukazuje obrázek 4, informace o `<connectionStrings>` jsou teď zašifrované.

[![kliknutím na tlačítko šifrovat připojovací řetězce zašifrujete oddíl &lt;connectionString&gt;.](protecting-connection-strings-and-other-configuration-information-cs/_static/image11.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image10.png)

**Obrázek 4**: kliknutím na tlačítko šifrovat připojovací řetězce zašifrujete `<connectionString>` oddíl ([kliknutím zobrazíte obrázek v plné velikosti).](protecting-connection-strings-and-other-configuration-information-cs/_static/image12.png)

Následuje následující oddíl šifrované `<connectionStrings>` vygenerovaný na mém počítači, i když byl pro zkrácení odebraný nějaký obsah v `<CipherData>` elementu:

[!code-xml[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample4.xml)]

> [!NOTE]
> Element `<connectionStrings>` Určuje zprostředkovatele, který se používá k šifrování (`DataProtectionConfigurationProvider`). Tyto informace používá metoda `UnprotectSection` při kliknutí na tlačítko dešifrování připojovacích řetězců.

Pokud jsou k informacím připojovacího řetězce přistupované z `Web.config` – buď pomocí kódu, který zapisujeme, z ovládacího prvku SqlDataSource, nebo automaticky generovaného kódu z objekty TableAdapter v našich typových datových sadách – automaticky se dešifruje. V krátkém případě není nutné přidávat žádný další kód nebo logiku k dešifrování šifrovaného `<connectionString>` oddílu. Provedete to tak, že v tuto chvíli navštívíte jeden z předchozích kurzů, jako je například jednoduchý úvodní kurz ze základní části vytváření sestav (`~/BasicReporting/SimpleDisplay.aspx`). Jak je znázorněno na obrázku 5, kurz funguje přesně tak, jak byste očekávali, což značí, že informace o šifrovaném připojovacím řetězci jsou automaticky dešifrovány stránkou ASP.NET.

[![vrstva přístupu k datům automaticky dešifruje informace o připojovacím řetězci.](protecting-connection-strings-and-other-configuration-information-cs/_static/image14.png)](protecting-connection-strings-and-other-configuration-information-cs/_static/image13.png)

**Obrázek 5**: Vrstva přístupu k datům automaticky dešifruje informace o připojovacím řetězci ([kliknutím zobrazíte obrázek v plné velikosti).](protecting-connection-strings-and-other-configuration-information-cs/_static/image15.png)

Chcete-li vrátit část `<connectionStrings>` zpět do její reprezentace ve formátu prostého textu, klikněte na tlačítko dešifrovat připojovací řetězce. Při zpětném odeslání byste viděli připojovací řetězce v `Web.config` v prostém textu. V tuto chvíli by vaše obrazovka měla vypadat jako při první návštěvě této stránky (viz obrázek 3).

## <a name="step-3-encrypting-configuration-sections-usingaspnet_regiisexe"></a>Krok 3: šifrování konfiguračních oddílů pomocí`aspnet_regiis.exe`

.NET Framework obsahuje řadu nástrojů příkazového řádku ve složce `$WINDOWS$\Microsoft.NET\Framework\version\`. V kurzu [použití závislostí mezipaměti SQL](../caching-data/using-sql-cache-dependencies-cs.md) jste si například vyhledali použití nástroje příkazového řádku `aspnet_regsql.exe` k přidání infrastruktury potřebné pro závislosti mezipaměti SQL. Dalším užitečným nástrojem příkazového řádku v této složce je [Nástroj pro registraci ASP.NET služby IIS (`aspnet_regiis.exe`)](https://msdn.microsoft.com/library/k6h9cz8h(VS.80).aspx). Jak je uvedeno, ASP.NET registrační nástroj služby IIS se primárně používá k registraci aplikace ASP.NET 2,0 s webovým serverem Microsoft s Professional na úrovni služby IIS. Kromě funkcí souvisejících se službou IIS se dá registrační nástroj ASP.NET služby IIS použít taky k šifrování nebo dešifrování zadaných konfiguračních oddílů v `Web.config`.

Následující příkaz ukazuje obecnou syntaxi použitou k zašifrování konfiguračního oddílu pomocí nástroje `aspnet_regiis.exe`ho příkazového řádku:

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample5.cmd)]

*oddíl* je konfigurační oddíl pro šifrování (jako connectionstringy), *fyzický\_adresář* je úplná, fyzická cesta k kořenovému adresáři webové aplikace s a *poskytovatelem* je název poskytovatele chráněné konfigurace, který se má použít (například DataProtectionConfigurationProvider). Případně, pokud je webová aplikace registrována ve službě IIS, můžete místo fyzické cesty zadat virtuální cestu pomocí následující syntaxe:

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample6.cmd)]

Následující příklad `aspnet_regiis.exe` šifruje oddíl `<connectionStrings>` pomocí poskytovatele DPAPI s klíčem na úrovni počítače:

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample7.cmd)]

Podobně je možné použít nástroj příkazového řádku `aspnet_regiis.exe` k dešifrování konfiguračních oddílů. Místo použití přepínače `-pef` použijte `-pdf` (nebo místo `-pe`použijte `-pd`). Všimněte si také, že při dešifrování není potřebný název poskytovatele.

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-cs/samples/sample8.cmd)]

> [!NOTE]
> Vzhledem k tomu, že používáme poskytovatele rozhraní DPAPI, který používá klíče specifické pro počítač, musíte spustit `aspnet_regiis.exe` ze stejného počítače, ze kterého jsou webové stránky obsluhovány. Pokud například spustíte tento program příkazového řádku z místního vývojového počítače a potom nahrajete zašifrovaný soubor Web. config na provozní server, nebude se v tomto provozním serveru moci dešifrovat informace o připojovacím řetězci, protože byl zašifrovaný. použití klíčů specifických pro váš vývojový počítač. Poskytovatel RSA nemá toto omezení, protože je možné exportovat klíče RSA na jiný počítač.

## <a name="understanding-database-authentication-options"></a>Principy možností ověřování databáze

Předtím, než může kterákoli aplikace vystavit `SELECT`, `INSERT`, `UPDATE`nebo `DELETE` dotazy do databáze Microsoft SQL Server, musí databáze nejprve určit žadatele. Tento proces se označuje jako *ověřování* a SQL Server poskytuje dvě metody ověřování:

- **Ověřování systému Windows** – proces, ve kterém je aplikace spuštěná, slouží ke komunikaci s databází. Při spuštění aplikace ASP.NET prostřednictvím vývojového serveru sady Visual Studio 2005 s ASP.NET předpokládá aplikace ASP.NET identitu aktuálně přihlášeného uživatele. Pro aplikace ASP.NET na serveru Microsoft Internet Information Server (IIS) ASP.NET aplikace obvykle předpokládají identitu `domainName``\MachineName` nebo `domainName``\NETWORK SERVICE`, i když je lze přizpůsobit.
- **Ověřování SQL** – hodnoty ID a hesla uživatele jsou zadány jako přihlašovací údaje pro ověřování. S ověřováním SQL je v připojovacím řetězci zadáno ID uživatele a heslo.

Ověřování systému Windows je upřednostňováno při ověřování SQL, protože je bezpečnější. Při ověřování systému Windows je připojovací řetězec bezplatný od uživatelského jména a hesla, a pokud se webový server a databázový server nacházejí ve dvou různých počítačích, přihlašovací údaje se neodesílají přes síť v prostém textu. Při ověřování SQL se ale přihlašovací údaje pro ověřování zakódují do připojovacího řetězce a přenesou se z webového serveru do databázového serveru v prostém textu.

Tyto kurzy používaly ověřování systému Windows. Můžete určit, jaký režim ověřování se používá, kontrolou připojovacího řetězce. Připojovací řetězec v `Web.config` pro naše kurzy byl:

`Data Source=.\SQLEXPRESS; AttachDbFilename=|DataDirectory|\NORTHWND.MDF; Integrated Security=True; User Instance=True`

Integrované zabezpečení = true a chybějící uživatelské jméno a heslo označují, že se používá ověřování systému Windows. V některých připojovacích řetězcích se pojem důvěryhodné připojení = Yes nebo Integrated Security = SSPI používá namísto integrovaného zabezpečení = true, ale všechny tři označují použití ověřování systému Windows.

Následující příklad ukazuje připojovací řetězec, který používá ověřování SQL. Poznamenejte si přihlašovací údaje vložené v připojovacím řetězci:

`Server=serverName; Database=Northwind; uid=userID; pwd=password`

Představte si, že útočník může zobrazit soubor s `Web.config` vaší aplikace. Pokud používáte ověřování SQL pro připojení k databázi, která je přístupná přes Internet, útočník může tento připojovací řetězec použít k připojení k vaší databázi prostřednictvím SQL Management Studio nebo na stránkách ASP.NET na svém vlastním webu. Chcete-li snížit riziko této hrozby, zašifrujte informace připojovacího řetězce v `Web.config` pomocí chráněného konfiguračního systému.

> [!NOTE]
> Další informace o různých typech ověřování dostupných v SQL Server najdete v tématu [sestavování zabezpečených aplikací ASP.NET: ověřování, autorizace a zabezpečená komunikace](https://msdn.microsoft.com/library/aa302392.aspx). Další příklady připojovacích řetězců, které ilustrují rozdíly mezi syntaxí ověřování Windows a SQL, najdete v tématu [connectionStrings.com](http://www.connectionstrings.com/).

## <a name="summary"></a>Souhrn

Ve výchozím nastavení se k souborům s rozšířením `.config` v aplikaci ASP.NET nelze dostat prostřednictvím prohlížeče. Tyto typy souborů nejsou vraceny, protože mohou obsahovat citlivé informace, například připojovací řetězce databáze, uživatelská jména a hesla atd. Chráněný konfigurační systém v rozhraní .NET 2,0 pomáhá chránit citlivé informace tím, že umožňuje šifrovat zadané konfigurační oddíly. Existují dva předdefinované poskytovatele chráněných konfigurací: jeden, který používá algoritmus RSA a druhý používá rozhraní Windows Data Protection API (DPAPI).

V tomto kurzu jsme se podívali na to, jak šifrovat a dešifrovat nastavení konfigurace pomocí poskytovatele rozhraní DPAPI. To je možné provést programově, jak jsme viděli v kroku 2, a také prostřednictvím nástroje příkazového řádku `aspnet_regiis.exe`, který byl popsaný v kroku 3. Další informace o použití klíčů na úrovni uživatele nebo o použití poskytovatele RSA najdete v tématu prostředky v části Další informace o čtení.

Šťastné programování!

## <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Sestavování zabezpečené aplikace ASP.NET: ověřování, autorizace a zabezpečená komunikace](https://msdn.microsoft.com/library/aa302392.aspx)
- [Šifrování informací o konfiguraci v aplikacích ASP.NET 2,0](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)
- [Šifrování hodnot `Web.config` v ASP.NET 2,0](https://weblogs.asp.net/scottgu/archive/2006/01/09/434893.aspx)
- [Postupy: šifrování konfiguračních oddílů v ASP.NET 2,0 pomocí DPAPI](https://msdn.microsoft.com/library/ms998280.aspx)
- [Postupy: šifrování konfiguračních oddílů v ASP.NET 2,0 pomocí RSA](https://msdn.microsoft.com/library/ms998283.aspx)
- [Rozhraní API pro konfiguraci v rozhraní .NET 2,0](http://www.odetocode.com/Articles/418.aspx)
- [Ochrana dat systému Windows](https://msdn.microsoft.com/library/ms995355.aspx)

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Teresa Murphy a Randy Schmidt. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs.md)
> [Další](debugging-stored-procedures-cs.md)
