---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-cs
title: Běžné rozdíly v konfiguraci mezi vývojem aC#výrobou () | Microsoft Docs
author: rick-anderson
description: V předchozích kurzech jsme nasadili náš web kopírováním všech relevantních souborů z vývojového prostředí do provozního prostředí. Ale i...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 721a5c37-7e21-48e0-832e-535c6351dcae
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-cs
msc.type: authoredcontent
ms.openlocfilehash: 60379c87a8cf58b89066a6070ac659e65930b4fa
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74620422"
---
# <a name="common-configuration-differences-between-development-and-production-c"></a>Nejčastější rozdíly mezi vývojovou a provozní konfigurací (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial05_ConfigDifferences_cs.pdf)

> V předchozích kurzech jsme nasadili náš web kopírováním všech relevantních souborů z vývojového prostředí do provozního prostředí. Nejedná se ale o rozdíl mezi tím, že existují rozdíly v konfiguraci mezi prostředími, což vyžaduje, aby každé prostředí mělo jedinečný soubor Web. config. V tomto kurzu se podíváme na typické rozdíly v konfiguraci a vyhledáte strategie pro udržování samostatných informací o konfiguraci.

## <a name="introduction"></a>Úvod

Poslední dva kurzy vás provedl prostřednictvím nasazení jednoduché webové aplikace. Kurz [*nasazení webu pomocí klienta FTP*](deploying-your-site-using-an-ftp-client-cs.md) ukázal použití samostatného klienta FTP ke zkopírování potřebných souborů z vývojového prostředí až po produkční prostředí. V předchozím kurzu, [*nasazení webu pomocí sady Visual Studio*](deploying-your-site-using-visual-studio-cs.md), prohlédlo se do nasazení pomocí nástroje pro kopírování webu sady Visual Studio a možnosti publikování. V obou kurzech byl každý soubor v produkčním prostředí kopií souboru ve vývojovém prostředí. Není to ale běžné pro konfigurační soubory v produkčním prostředí, aby se lišily od těch ve vývojovém prostředí. Konfigurace webové aplikace je uložena v souboru `Web.config` a obvykle obsahuje informace o externích prostředcích, jako jsou databáze, webové a e-mailové servery. Také naplní chování aplikace v určitých situacích, například v případě, že je třeba provést akci, když dojde k neošetřené výjimce.

Při nasazení webové aplikace je důležité, aby byly správné informace o konfiguraci v produkčním prostředí. Ve většině případů se `Web.config` soubor ve vývojovém prostředí nedá zkopírovat do produkčního prostředí tak, jak je. Místo toho je potřeba nahrát přizpůsobenou verzi `Web.config` do produkčního prostředí. V tomto kurzu se krátce posuzuje některé z častých rozdílů v konfiguraci. shrnuje také některé techniky pro zachování různých konfiguračních informací mezi prostředími.

## <a name="typical-configuration-differences-between-the-development-and-production-environments"></a>Typické rozdíly v konfiguraci mezi vývojovým a produkčním prostředím

`Web.config` soubor obsahuje řadu informací o konfiguraci pro ASP.NET aplikaci. Některé z těchto informací o konfiguraci jsou stejné bez ohledu na prostředí. Například nastavení ověřování a autorizační pravidla URL, která jsou popsaná v `<authentication>` `Web.config` souboru a `<authorization>` prvky jsou obvykle stejné bez ohledu na prostředí. Jiné konfigurační informace, například informace o externích prostředcích, se obvykle liší v závislosti na prostředí.

Řetězce připojení databáze představují základní příklad informací o konfiguraci, které se liší v závislosti na prostředí. Když webová aplikace komunikuje s databázovým serverem, musí nejdřív navázat připojení a dosáhnout pomocí [připojovacího řetězce](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string). Přestože je možné pevný kód databázového připojovacího řetězce přímo na webových stránkách nebo v kódu, který se připojuje k databázi, je nejlepší umístit `Web.config`[`<connectionStrings>` prvek](https://msdn.microsoft.com/library/bf7sd233.aspx) tak, aby informace o připojovacím řetězci byly v jediném, centralizovaném umístění. Často se během vývoje používá jiná databáze, než se používá v produkčním prostředí. v důsledku toho musí být informace o připojovacím řetězci jedinečné pro každé prostředí.

> [!NOTE]
> V budoucích kurzech se dozvíte, jak nasazovat aplikace řízené daty. v tomto okamžiku se podrobně do konkrétních údajů o tom, jak se databázové připojovací řetězce ukládají do konfiguračního souboru.

Zamýšlené chování vývojových a produkčních prostředí se podstatně liší. Webová aplikace ve vývojovém prostředí je vytvářena, testována a Laděna malou skupinou vývojářů. V produkčním prostředí je stejná aplikace navštívená mnoha různými souběžnými uživateli. ASP.NET obsahuje řadu funkcí, které vývojářům pomůžou při testování a ladění aplikace, ale tyto funkce by se měly zakázat z důvodů výkonu a zabezpečení v produkčním prostředí. Pojďme se podívat na několik takových nastavení konfigurace.

### <a name="configuration-settings-that-impact-performance"></a>Nastavení konfigurace, která mají vliv na výkon

Pokud je stránka ASP.NET navštívena poprvé (nebo při prvním provedení změny), je nutné její deklarativní označení převést na třídu a tato třída musí být zkompilována. Pokud webová aplikace používá automatickou kompilaci, musí být zkompilována také třída kódu na pozadí stránky. Můžete nakonfigurovat sortiment možností kompilace prostřednictvím [`<compilation>` elementu](https://msdn.microsoft.com/library/s10awwz0.aspx)`Web.config` souboru.

Atribut debug je jedním z nejdůležitějších atributů v prvku `<compilation>`. Pokud je atribut `debug` nastaven na hodnotu "true", zkompilované sestavení obsahují symboly ladění, které jsou potřeba při ladění aplikace v sadě Visual Studio. Ale symboly ladění zvyšují velikost sestavení a při spuštění kódu nastavují další požadavky na paměť. Pokud je navíc atribut `debug` nastaven na hodnotu "true", jakýkoli obsah vrácený `WebResource.axd` není uložen do mezipaměti, což znamená, že pokaždé, když uživatel navštíví stránku, bude muset znovu stáhnout statický obsah vrácený `WebResource.axd`.

> [!NOTE]
> `WebResource.axd` je vestavěná obslužná rutina protokolu HTTP představená v ASP.NET 2,0, kterou serverové ovládací prvky používají k načtení integrovaných prostředků, jako jsou soubory skriptu, obrázky, soubory CSS a další obsah. Další informace o tom, jak `WebResource.axd` funguje a jak je můžete použít pro přístup k vloženým prostředkům z vlastních serverových ovládacích prvků, najdete v tématu [přístup k integrovaným prostředkům přes adresu URL pomocí `WebResource.axd`](http://aspnet.4guysfromrolla.com/articles/080906-1.aspx).

Atribut `debug` elementu `<compilation>` je obvykle ve vývojovém prostředí nastaven na hodnotu "true". Ve skutečnosti musí být tento atribut nastaven na hodnotu "true", aby bylo možné ladit webovou aplikaci. Pokud se pokusíte ladit aplikaci ASP.NET ze sady Visual Studio a atribut `debug` je nastaven na hodnotu "false", sada Visual Studio zobrazí zprávu s vysvětlením, že aplikaci nelze ladit, dokud není atribut `debug` nastaven na hodnotu "true" a nabídne tuto změnu pro vás.

V produkčním prostředí by **nikdy** neměl být atribut `debug` nastaven na hodnotu "true", protože má vliv na výkon. Podrobnější diskusi k tomuto tématu najdete v blogovém příspěvku [Scott Guthrie](https://weblogs.asp.net/scottgu/). [nespouštějte produkční aplikace ASP.NET s povoleným `debug="true"`](https://weblogs.asp.net/scottgu/442448).

### <a name="custom-errors-and-tracing"></a>Vlastní chyby a trasování

V případě, že dojde k neošetřené výjimce v aplikaci ASP.NET, zobrazí se s modulem runtime až do doby, kdy se stane jedna ze tří věcí:

- Zobrazí se obecná chybová zpráva modulu runtime. Tato stránka informuje uživatele o tom, že došlo k chybě za běhu, ale neposkytuje žádné podrobnosti o této chybě.
- Zobrazí se zpráva s podrobnostmi o výjimce, která obsahuje informace o výjimce, která byla právě vyvolána.
- Zobrazí se vlastní chybová stránka, což je ASP.NET stránka, kterou vytvoříte, která zobrazuje jakoukoli zprávu, kterou si přejete.

Co se stane na tváři neošetřené výjimky, závisí na [`<customErrors>` oddílu](https://msdn.microsoft.com/library/h0hfz6fc.aspx)`Web.config` souboru.

Při vývoji a testování aplikace pomáhá zobrazit podrobnosti o jakékoli výjimce v prohlížeči. Zobrazení podrobností o výjimce v aplikaci v produkčním prostředí je však potenciální bezpečnostní riziko. Navíc je unflattering a váš web vypadá neprofesionálně. V ideálním případě v případě neošetřené výjimky zobrazí webová aplikace ve vývojovém prostředí podrobnosti o výjimce, zatímco stejná aplikace v produkčním prostředí zobrazí vlastní chybovou stránku.

> [!NOTE]
> Výchozí nastavení oddílu `<customErrors>` zobrazuje zprávu o podrobnostech výjimky pouze v případě, že stránka je navštívena prostřednictvím místního hostitele, a v opačném případě zobrazuje chybovou stránku Obecné za běhu. To není ideální, ale zajišťuje, že výchozí chování neodhalí podrobnosti o výjimce nemístním návštěvníkům. Budoucí kurz podrobněji prověřuje část `<customErrors>` podrobněji a ukazuje, jak mít vlastní chybovou stránku zobrazenou v případě, že dojde k chybě v produkčním prostředí.

Další funkcí ASP.NET, která je užitečná při vývoji, je trasování. Trasování, pokud je povoleno, zaznamenává informace o jednotlivých příchozích žádostech a poskytuje speciální webovou stránku `Trace.axd`pro zobrazení posledních podrobností žádosti. Trasování můžete zapnout a nakonfigurovat pomocí [elementu`<trace>`](https://msdn.microsoft.com/library/6915t83k.aspx) v `Web.config`.

Pokud povolíte trasování, ujistěte se, že je v produkčním prostředí zakázané. Vzhledem k tomu, že informace o trasování zahrnují soubory cookie, data relace a další potenciálně citlivé informace, je důležité zakázat trasování v produkčním prostředí. Dobrá zpráva je, že ve výchozím nastavení je trasování zakázané a `Trace.axd` soubor je dostupný jenom přes localhost. Pokud toto výchozí nastavení změníte při vývoji, ujistěte se, že jsou v produkčním prostředí zase vypnuté.

## <a name="techniques-for-maintaining-separate-configuration-information"></a>Techniky správy oddělených informací o konfiguraci

Různá nastavení konfigurace ve vývojovém a produkčním prostředí ztěžuje proces nasazení. V předchozích dvou kurzech se během procesu nasazení zkopírovaly všechny nezbytné soubory z vývoje do produkčního prostředí, ale tento přístup funguje jenom v případě, že konfigurační informace jsou v obou prostředích stejné. Existuje řada technik pro nasazení aplikace s různými konfiguračními informacemi. Pojďme tyto možnosti zařadit do katalogu pro hostované webové aplikace.

### <a name="manually-deploying-the-production-environment-configuration-file"></a>Ruční nasazení konfiguračního souboru produkčního prostředí

Nejjednodušším přístupem je udržovat dvě verze `Web.config` souboru: jeden pro vývojové prostředí a jeden pro produkční prostředí. Nasazení lokality do provozu zahrnuje kopírování všech souborů na provozní server ve vývojovém prostředí *s výjimkou* `Web.config` souboru. Místo toho se do produkčního souboru zkopíruje soubor `Web.config` specifický pro produkční prostředí.

Tento přístup není příliš složitý, ale je možné jej snadno implementovat, protože informace o konfiguraci se nečasto mění. Funguje nejlépe pro aplikace s malým vývojovým týmem, který je hostovaný na jednom webovém serveru a jehož konfigurační informace se zřídka mění. Při ručním nasazování souborů aplikace pomocí samostatného klienta FTP se jedná o většinu Tenable. Když použijete nástroj pro kopírování webu sady Visual Studio nebo možnost publikování, budete muset před nasazením nejprve vyměňovat soubor `Web.config` specifický pro nasazení s konkrétní výrobou a pak je po dokončení nasazení znovu zaměnit.

### <a name="change-the-configuration-during-the-build-or-deployment-process"></a>Změna konfigurace během procesu sestavení nebo nasazení

V dosavadních diskuzích se předpokládá proces sestavení a nasazení ad hoc. Mnoho větších softwarových projektů má více formálních procesů, které využívají open source nástroje nebo nástroje třetích stran. V takových projektech si pravděpodobně můžete přizpůsobit proces sestavení nebo nasazení a odpovídajícím způsobem upravit informace o konfiguraci před jejich odesláním do produkčního prostředí. Pokud sestavíte webovou aplikaci pomocí nástroje [MSBuild](http://en.wikipedia.org/wiki/MSBuild), [NAnt](http://nant.sourceforge.net/)nebo nějakého jiného nástroje sestavení, můžete přidat krok sestavení, který upraví soubor `Web.config` tak, aby zahrnoval nastavení specifické pro určitou provozní hodnotu. Pracovní postup nasazení by se mohl programově připojit k serveru správy zdrojového kódu a načíst příslušný soubor `Web.config`.

Skutečný přístup k tomu, aby se informace o konfiguraci do provozu získaly, se výrazně liší v závislosti na vašich nástrojích a pracovním postupu. V takovém případě nebudeme dál do tohoto tématu dohlížet. Pokud používáte oblíbený nástroj sestavení, jako je MSBuild nebo NAnt, můžete najít články týkající se nasazení a kurzy specifické pro tyto nástroje prostřednictvím vyhledávání na webu.

### <a name="managing-configuration-differences-via-the-web-deployment-project-add-in"></a>Správa rozdílů v konfiguraci prostřednictvím doplňku projektu nasazení webu

V 2006 společnost Microsoft vydala doplněk projektu pro vývoj webu pro Visual Studio 2005. Doplněk pro Visual Studio 2008 byl vydaný v 2008. Tento doplněk umožňuje vývojářům v ASP.NET vytvořit samostatný projekt webového nasazení společně se svým projektem webové aplikace, který při sestavení explicitně zkompiluje webovou aplikaci a zkopíruje soubory pro nasazení do místního výstupního adresáře. Projekt webové aplikace používá MSBuild na pozadí.

Ve výchozím nastavení je soubor `Web.config` vývojového prostředí zkopírován do výstupního adresáře, ale můžete nastavit projekt nasazení webu pro přizpůsobení

informace o konfiguraci, které se zkopírují do tohoto adresáře, následujícími způsoby:

- Pomocí `Web.config` nahrazení oddílu souboru, ve kterém zadáte oddíl, který se má nahradit, a soubor XML, který obsahuje nahrazující text.
- Zadáním cesty k externímu zdrojovému souboru konfigurace. Když je tato možnost vybraná, projekt nasazení webu zkopíruje určitý soubor `Web.config` do výstupního adresáře (místo `Web.config` souboru používaného ve vývojovém prostředí).
- Přidáním vlastních pravidel do souboru MSBuild používaného projektem nasazení webu.

Chcete-li nasadit webovou aplikaci, sestavte projekt nasazení webu a potom zkopírujte soubory z výstupní složky projektu do produkčního prostředí.

Další informace o používání projektu nasazení webu najdete v [tomto článku o projektech nasazení webu](https://msdn.microsoft.com/magazine/cc163448.aspx) od vydání 2007. dubna na [webu MSDN Magazine](https://msdn.microsoft.com/magazine/default.aspx)nebo si Projděte odkazy v části Další informace na konci tohoto kurzu.

> [!NOTE]
> Projekt nasazení webu se sadou Visual Web Developer nelze použít, protože projekt nasazení webu je implementován jako doplněk sady Visual Studio a edice Visual Studio Express (včetně aplikace Visual Web Developer) nepodporují doplňky.

## <a name="summary"></a>Přehled

Externí prostředky a chování webové aplikace ve vývoji se obvykle liší od situace, kdy je stejná aplikace v produkčním prostředí. Například databázové připojovací řetězce, možnosti kompilace a chování, když dojde k neošetřené výjimce, se obvykle liší mezi prostředími. Proces nasazení musí vyhovovat těmto rozdílům. Jak je popsáno v tomto kurzu, nejjednodušší způsob je ruční zkopírování alternativního konfiguračního souboru do produkčního prostředí. Při použití doplňku projektu nasazení webu nebo s více formálními procesy sestavení nebo nasazení, které mohou přizpůsobit taková přizpůsobení, jsou k dispozici další elegantní řešení.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Vysvětlení připojovacích řetězců](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)
- [Připojovací řetězce databáze @ ConnectionStrings.com](http://www.connectionstrings.com/)
- [Nespouštějte produkční aplikace v ASP.NET s povoleným `debug="true"`](https://weblogs.asp.net/scottgu/Don_1920_t-run-production-ASP.NET-Applications-with-debug_3D001D20_true_1D20_-enabled)
- [Řádné reakce na neošetřené výjimky – zobrazení uživatelsky přívětivých chybových stránek](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [Jak můžu: použít projekt nasazení webu sady Visual Studio 2008?](../../../videos/how-do-i/how-do-i-use-a-visual-studio-2008-web-deployment-project.md)
- [Nastavení konfigurace klíče při nasazení databáze](http://aspnet.4guysfromrolla.com/articles/121008-1.aspx)
- [Projekty nasazení webu sady Visual studio 2008 stáhnout](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en) | [projekty nasazení sady Visual Studio 2005 stáhnout](https://download.microsoft.com/download/9/4/9/9496adc4-574e-4043-bb70-bc841e27f13c/WebDeploymentSetup.msi)
- [Projekty nasazení webu vs 2008](https://weblogs.asp.net/scottgu/archive/2005/11/06/429723.aspx) | [a podpora projektů nasazení webu vs 2008](https://weblogs.asp.net/scottgu/archive/2008/01/28/vs-2008-web-deployment-project-support-released.aspx)
- [Projekty nasazení webu](https://msdn.microsoft.com/magazine/cc163448.aspx)

> [!div class="step-by-step"]
> [Předchozí](deploying-your-site-using-visual-studio-cs.md)
> [Další](core-differences-between-iis-and-the-asp-net-development-server-cs.md)
