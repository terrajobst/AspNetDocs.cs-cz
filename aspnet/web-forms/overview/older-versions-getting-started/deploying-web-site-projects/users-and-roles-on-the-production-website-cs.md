---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs
title: Uživatelé a role na provozním webu (C#) | Microsoft Docs
author: rick-anderson
description: Nástroj pro správu webu ASP.NET (WSAT) poskytuje webové uživatelské rozhraní pro konfiguraci nastavení členství a rolí a pro vytváření, úpravy a...
ms.author: riande
ms.date: 06/09/2009
ms.assetid: dbc54313-5d05-4285-98b3-726edea6d0c9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs
msc.type: authoredcontent
ms.openlocfilehash: c47bd2c1661f129dd8856916de04b8ba459fbfec
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548242"
---
# <a name="users-and-roles-on-the-production-website-c"></a>Uživatelé a role na provozním webu (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout PDF](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial16_CustomAWAT_cs.pdf)

> Nástroj pro správu webu ASP.NET (WSAT) poskytuje webové uživatelské rozhraní pro konfiguraci nastavení členství a rolí a pro vytváření, úpravy a odstraňování uživatelů a rolí. WSAT bohužel funguje jenom v případě, že se navštíví z místního hostitele, což znamená, že nebudete mít přístup k nástroji pro správu produkčního webu přes prohlížeč. Dobrá zpráva je, že existují alternativní řešení, díky kterým je možné spravovat uživatele a role v produkčním prostředí. V tomto kurzu se podíváme na Tato alternativní řešení a další.

## <a name="introduction"></a>Úvod

ASP.NET 2,0 představil řadu *aplikačních služeb*, které jsou sadou stavebních blokových služeb, které můžete přidat do své webové aplikace. Do webu recenze webů jsme přidali služby pro členství a role zpátky v části [ *Konfigurace webu, který používá aplikační služby* kurzu](configuring-a-website-that-uses-application-services-cs.md). Služba členství usnadňuje vytváření a správu uživatelských účtů; Služba role nabízí rozhraní API pro kategorizaci uživatelů do skupin. Web recenze obsahuje tři uživatelské účty – Scott, Jisun a Alice – a jednu roli, správce s Scottem a Jisun v roli správce.

Formátu. Aplikační služby netto nejsou vázané na konkrétní implementaci. Místo toho dejte aplikačním službám pokyn, aby používaly konkrétního *poskytovatele*, a tento poskytovatel implementuje službu pomocí konkrétní technologie. Nakonfigurovali jsme webovou aplikaci recenze pro knihu, aby používala poskytovatele `SqlMembershipProvider` a `SqlRoleProvider` pro služby členství a rolí. Tito dva poskytovatelé uchovávají informace o uživatelském účtu a roli v SQL Server databázi a jsou nejčastěji používanými poskytovateli pro internetové webové aplikace hostované na společnosti pro hostování na webu.

Běžnou výzvou pro vývojáře, kteří používají služby členství a rolí, je Správa uživatelů a rolí v produkčním prostředí. Jak odstranit uživatelský účet z produkčního webu, přidat novou roli nebo přidat existujícího uživatele do existující role? V tomto kurzu se seznámíte s různými technikami správy uživatelů a rolí na produkčním webu.

## <a name="using-the-aspnet-web-site-administration-tool"></a>Použití nástroje pro správu webu ASP.NET

ASP.NET zahrnuje [Nástroj pro správu](https://msdn.microsoft.com/library/yy40ytx0.aspx) webu (WSAT), který usnadňuje vytváření a správu uživatelských účtů a rolí a určuje autorizační pravidla založená na uživatelích a rolích. Chcete-li použít WSAT, klikněte na ikonu konfigurace ASP.NET v Průzkumník řešení nebo přejděte na web nebo v nabídce projekt a vyberte možnost konfigurace ASP.NET. Buď se přiblíží, spustí se webový prohlížeč a navede na něj WSAT na adrese, jako je: `http://localhost:portNumber/asp.netwebadminfiles/default.aspx?applicationPhysicalPath=pathToApplication`

WSAT je rozdělen na tři části:

- **Zabezpečení** – Správa uživatelů, rolí a autorizačních pravidel.
- **ApplicationConfiguration** – tady můžete spravovat &lt;appSettings&gt; a nastavení SMTP. Můžete také převést aplikaci do offline režimu a spravovat nastavení ladění a trasování a také určit výchozí vlastní chybovou stránku.
- **ProviderConfiguration** – nakonfigurujte zprostředkovatele používané aplikačními službami.

Oddíl zabezpečení (znázorněný na **obrázku 1**) obsahuje odkazy pro vytváření nových uživatelů, správu uživatelů, vytváření a správu rolí a vytváření a správu pravidel přístupu. Z tohoto místa můžete přidat novou roli do systému, odstranit stávajícího uživatele nebo přidat nebo odebrat role z konkrétního uživatelského účtu.

[![](users-and-roles-on-the-production-website-cs/_static/image2.png)](users-and-roles-on-the-production-website-cs/_static/image1.png)

**Obrázek 1**: oddíl zabezpečení WSAT zahrnuje možnosti správy uživatelů a rolí.  
([Kliknutím zobrazíte obrázek v plné velikosti.](users-and-roles-on-the-production-website-cs/_static/image3.png))

WSAT je však k dispozici pouze místně. WSAT na vzdáleném produkčním webu nemůžete navštívit. Pokud navštívíte `www.yoursite.com/asp.netwebadminfiles/default.aspx` dostanete odpověď na 404, která nebyla nalezena. Kód, který využívá WSAT, používá třídy `Membership` a `Roles` v .NET Framework k vytváření, úpravám a odstraňování uživatelů a rolí. Tyto třídy projednávají informace o konfiguraci webové aplikace a určí, co má poskytovatel použít; zpátky v části [ *Konfigurace webu, který používá aplikační služby* kurzu](configuring-a-website-that-uses-application-services-cs.md) nastavíme web recenze pro použití poskytovatele `SqlMembershipProvider` a `SqlRoleProvider`. To má za následek přidání oddílů `<membership>` a `<roleManager>` do `Web.config`.

[!code-xml[Main](users-and-roles-on-the-production-website-cs/samples/sample1.xml)]

Všimněte si, že oddíly `<membership>` a `<roleManager>` odkazují na poskytovatele `SqlMembershipProvider` a `SqlRoleProvider` v jejich atributu `type` v uvedeném pořadí. Tito poskytovatelé ukládají informace o uživateli a roli do zadané SQL Server databáze. Databáze používaná těmito zprostředkovateli je určena atributem `connectionStringName` `ReviewsConnectionString`, který je definován v souboru `~/ConfigSections/databaseConnectionStrings.config`. Odvolání, že soubor `databaseConnectionStrings.config` ve vývojovém prostředí obsahuje připojovací řetězec k vývojové databázi, zatímco `databaseConnectionStrings.config` soubor v produkci obsahuje připojovací řetězec do provozní databáze.

V kostce musí být WSAT k dispozici místně prostřednictvím vývojového prostředí a bude pracovat s informacemi o uživatelích a rolích v databázi určené v souboru `databaseConnectionStrings.config`. V důsledku toho, pokud změníme informace připojovacího řetězce v `databaseConnectionStrings.config` souboru ve vývojovém prostředí, můžeme místní WSAT použít pro správu uživatelů a rolí v produkčním prostředí.

K ilustraci této funkce otevřete soubor `databaseConnectionStrings.config` v aplikaci Visual Studio ve vývojovém prostředí a nahraďte připojovací řetězec vývojové databáze pomocí připojovacího řetězce produkční databáze. Pak spusťte WSAT, otevřete kartu zabezpečení a přidejte nového uživatele s názvem Sam s heslem heslo. (menší uvozovky). **Obrázek 2** ukazuje obrazovku WSAT při vytváření tohoto účtu.

[![](users-and-roles-on-the-production-website-cs/_static/image5.png)](users-and-roles-on-the-production-website-cs/_static/image4.png)

**Obrázek 2**: vytvoření nového uživatele s názvem Sam v produkčním prostředí  
([Kliknutím zobrazíte obrázek v plné velikosti.](users-and-roles-on-the-production-website-cs/_static/image6.png))

Vzhledem k tomu, že jsme změnili připojovací řetězec v `databaseConnectionStrings.config` tak, aby odkazoval na provozní server databáze, správce Sam byl přidán jako uživatel v produkčním prostředí. Pokud to chcete ověřit, změňte připojovací řetězec v souboru `databaseConnectionStrings.config` zpátky do vývojové databáze a potom navštivte stránku `Login.aspx` ve vývojovém prostředí. Zkuste se přihlásit jako Sam (viz **Obrázek 3**).

[![](users-and-roles-on-the-production-website-cs/_static/image8.png)](users-and-roles-on-the-production-website-cs/_static/image7.png)

**Obrázek 3**: nemůžete se přihlásit jako Sam ve vývojovém prostředí.  
([Kliknutím zobrazíte obrázek v plné velikosti.](users-and-roles-on-the-production-website-cs/_static/image9.png))

Nemůžete se přihlásit jako Sam ve vývojovém prostředí, protože informace o uživatelském účtu v místní databázi neexistují. Místo toho se přidala do provozní databáze. Pokud to chcete ověřit, Prohlédněte si obsah `aspnet_Users` tabulky ve vývojových i produkčních databázích. Ve vývojovém prostředí by měly existovat pouze tři záznamy pro uživatele Scott, Jisun a Alice. Tabulka `aspnet_Users` v provozní databázi ale obsahuje čtyři záznamy: Scott, Jisun, Alice a Sam. V důsledku toho se Sam může přihlásit prostřednictvím webu v produkčním prostředí, ale ne prostřednictvím vývojového prostředí.

[![](users-and-roles-on-the-production-website-cs/_static/image11.png)](users-and-roles-on-the-production-website-cs/_static/image10.png)

**Obrázek 4**: Sam se může přihlásit na produkčním webu  
([Kliknutím zobrazíte obrázek v plné velikosti.](users-and-roles-on-the-production-website-cs/_static/image12.png))

> [!NOTE]
> Nezapomeňte změnit připojovací řetězec v `databaseConnectionStrings.config` souboru zpátky na řetězec připojení pro vývojovou databázi, když jste hotovi s WSAT, jinak budete při testování lokality přes vývojové prostředí pracovat s provozními daty. Pamatujte na to, že zatímco technika, kterou jsme právě provedli, nám umožňuje používat WSAT pro vzdálenou správu uživatelů a rolí, změny kterékoli další možnosti konfigurace WSAT (pravidla přístupu, nastavení SMTP, nastavení ladění a trasování atd.) upravte soubor `Web.config`. V důsledku toho se všechny změny provedené v nastavení vztahují na vývojové prostředí a nikoli na produkční prostředí.

## <a name="creating-custom-user-and-role-management-web-pages"></a>Vytváření vlastních webových stránek a uživatelů pro správu rolí

WSAT poskytuje předem připravený systém pro správu uživatelů a rolí, ale dá se spustit jenom místně a vyžaduje provedení změn informací o připojovacím řetězci, aby bylo možné spravovat uživatele a role v produkčním prostředí. Většina webů, které podporují uživatelské účty, zahrnuje také řadu webových stránek pro správu uživatelů a rolí, které správcům umožňují spravovat uživatele a role ze stránek v rámci lokality. Tyto webové stránky pro správu usnadňují správu uživatelů a rolí a jsou nezbytné pro weby, kde mohou existovat mnoho správců nebo správců, kteří nemají přístup k aplikaci nebo technickému pozadí pro použití sady Visual Studio ke spuštění WSAT.

ASP.NET zahrnuje řadu integrovaných webových ovládacích prvků souvisejících s přihlášením, které provádějí implementaci mnoha z těchto webových stránek jako snadno přetahování. Můžete například vytvořit stránku pro správce a vytvořit nový uživatelský účet přetažením ovládacího prvku ovládacím CreateUserWizard na stránku a nastavením několika vlastností. Ve skutečnosti stránka pro vytváření uživatelů v WSAT znázorněná na **obrázku 2** používá stejný ovládací prvek ovládacím CreateUserWizard, který můžete přidat na své stránky. Kromě toho jsou funkce členství a rolí k dispozici programově prostřednictvím `Membership` a `Roles` třídy v .NET Framework. Pomocí těchto tříd můžete napsat kód k vytváření, úpravám a odstraňování uživatelů a rolí a také k přidávání nebo odebírání uživatelů rolí, k určení toho, kteří uživatelé jsou v rolích a k provádění dalších úloh souvisejících s uživateli a rolemi.

V části [ *Konfigurace webu, který používá aplikační služby* kurzu](configuring-a-website-that-uses-application-services-cs.md) jsem přidal stránku do `Admin` složky s názvem `CreateAccount.aspx`. Tato stránka umožňuje správci přidat nový uživatelský účet k lokalitě a určit, zda byl nově vytvořený uživatel v roli správce (viz **Obrázek 5**).

[![](users-and-roles-on-the-production-website-cs/_static/image14.png)](users-and-roles-on-the-production-website-cs/_static/image13.png)

**Obrázek 5**: Správci můžou vytvářet nové uživatelské účty.  
([Kliknutím zobrazíte obrázek v plné velikosti.](users-and-roles-on-the-production-website-cs/_static/image15.png))

Podrobnější informace o vytváření stránek pro správu uživatelů a rolí spolu s podrobnými pokyny k používání tříd `Membership` a `Roles` a webových ovládacích prvků ASP.NET souvisejících s přihlášením najdete v tématu [kurzy zabezpečení webu](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md). Najdete zde Rady, jak vytvářet webové stránky pro vytváření nových účtů, vytváření a správu rolí, přiřazování uživatelů k rolím a další běžné úlohy správy.

K implementaci WSAT podobných funkcím na produkčním webu můžete vždy vytvořit vlastní řadu webových stránek, které implementují funkce WSAT. Pokud chcete začít, podívejte se na zdrojový kód WSAT, který je umístěný ve složce `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\ASP.NETWebAdminFiles`. Další možností je použít alternativu clem Dan WSAT, kterou sdílí v jejím článku, a to s využitím [vlastního nástroje pro správu](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)webu. Dan provede čtenáře procesem vytvoření vlastního nástroje podobného WSAT, zahrnuje zdrojový kód aplikace ke stažení (v C#) a poskytuje podrobné pokyny pro přidání vlastního WSATu na hostovaný Web.

## <a name="summary"></a>Souhrn

Nástroj pro správu webu ASP.NET (WSAT) je možné použít společně s aplikacemi pro členství a role, které slouží ke správě informací o uživatelích a rolích pro váš web. WSAT je ale přístupný jenom místně a nedá se navštívit z produkčního webu. Změnou připojovacího řetězce ve vývojovém prostředí tak, aby odkazoval na produkční databázi, můžete použít WSAT ke správě uživatelů a rolí na produkčním webu.

I když přístup WSAT nabízí rychlý a snadný způsob, jak spravovat uživatele a role, vyžaduje spuštění WSAT ze sady Visual Studio a také dočasné změny informací o připojovacím řetězci. WSAT nabízí rychlý způsob, jak spravovat uživatele a role v produkčním prostředí, ale je nenáročný a nefunguje dobře pro weby s více správci nebo s správci, kteří nemají nebo nejsou obeznámeni se sadou Visual Studio a WSAT. Z těchto důvodů většina webů, které podporují uživatelské účty, zahrnuje sadu webových stránek pro správu. Taková sada webových stránek eliminuje nutnost WSAT a používá různé administrativní uživatele z libovolného počítače.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Prozkoumává se ASP. Členství v síti, role a profil](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [Postup při zavedení vlastního nástroje pro správu webu](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [Přehled nástroje pro správu webu](https://msdn.microsoft.com/library/yy40ytx0.aspx)
- [Kurzy zabezpečení webu](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> [Předchozí](precompiling-your-website-cs.md)
> [Další](asp-net-hosting-options-vb.md)
