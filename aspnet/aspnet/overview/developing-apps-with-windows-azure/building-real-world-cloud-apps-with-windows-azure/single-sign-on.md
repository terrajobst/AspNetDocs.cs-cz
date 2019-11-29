---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
title: Jednotné přihlašování (vytváření skutečných cloudových aplikací s Azure) | Microsoft Docs
author: MikeWasson
description: Vytváření reálných cloudových aplikací pomocí Azure je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které mohou...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 7d82d5e9-0619-4f22-9e03-32a6d52940a5
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
msc.type: authoredcontent
ms.openlocfilehash: 7e32f444dc38132296cffd45ac658f5abf51f314
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585283"
---
# <a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a>Jednotné přihlašování (vytváření skutečných cloudových aplikací s Azure)

[Jan Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Dykstra](https://github.com/tdykstra)

[Stažení opravy projektu IT](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stažení elektronické knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **Vytváření reálných cloudových aplikací pomocí Azure** je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které vám pomůžou úspěšně vyvíjet webové aplikace pro Cloud. Informace o elektronické příručce najdete v [první kapitole](introduction.md).

Při vývoji cloudové aplikace je potřeba vzít v úvahu mnoho problémů se zabezpečením, ale pro tuto řadu se zaměříme jenom na jedno: jednotné přihlašování. Lidé se často dotazují: "Já jsem sestavovat aplikace pro zaměstnance mojí společnosti; Jak můžu hostovat tyto aplikace v cloudu a pořád jim povolit, aby používali stejný model zabezpečení, který mají zaměstnanci vědět a používají v místním prostředí, když běží aplikace, které jsou hostované v bráně firewall? " Jedním z způsobů, jak tento scénář povolit, se říká Azure Active Directory (Azure AD). Azure AD umožňuje zpřístupnit podnikovým podnikovým aplikacím přístup přes Internet a umožňuje zpřístupnit tyto aplikace i obchodním partnerům.

## <a name="introduction-to-azure-ad"></a>Seznámení s Azure AD

[Azure AD](https://docs.microsoft.com/azure/active-directory/) poskytuje [službu Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) v cloudu. Mezi klíčové funkce patří následující:

- Integruje se s místní službou Active Directory.
- Umožňuje jednotné přihlašování s vašimi aplikacemi.
- Podporuje otevřené standardy, jako je [SAML](http://en.wikipedia.org/wiki/SAML_2.0), [WS-dokrmený](http://en.wikipedia.org/wiki/WS-Federation)a [OAuth 2,0](http://oauth.net/2/).
- Podporuje REST API podnikového [grafu](https://msdn.microsoft.com/library/hh974476.aspx).

Předpokládejme, že máte místní prostředí Windows serveru Active Directory, které se používá k tomu, aby se zaměstnanci mohli přihlašovat k intranetovým aplikacím:

![](single-sign-on/_static/image1.png)

To, co Azure AD umožňuje, je vytvořit adresář v cloudu. Je to bezplatná funkce a snadno se nastavuje.

Může být zcela nezávislá na vaší místní službě Active Directory. můžete do něj umístit libovolného někoho a ověřit je v internetových aplikacích.

![Microsoft Azure Active Directory](single-sign-on/_static/image2.png)

Nebo ho můžete integrovat s místní službou AD.

![Integrace AD a WAAD](single-sign-on/_static/image3.png)

Všichni zaměstnanci, kteří se můžou místně ověřovat v místním prostředí, se teď můžou ověřit přes Internet – bez nutnosti otevírat bránu firewall nebo nasazovat nové servery v datovém centru. Můžete dál využívat všechny existující prostředí Active Directory, které znáte a dnes používáte, a poskytnout tak interním aplikacím možnost jednotného přihlašování.

Jakmile provedete toto propojení mezi službami AD a Azure AD, můžete také povolit vašim webovým aplikacím a mobilním zařízením ověřování zaměstnanců v cloudu a povolit aplikace třetích stran, jako je například Office 365, SalesForce.com nebo Google, přijmout vaše přihlašovací údaje zaměstnanců. Pokud používáte Office 365, už jste si nastavili Azure AD, protože Office 365 používá k ověřování a autorizaci službu Azure AD.

![aplikace třetích stran](single-sign-on/_static/image4.png)

Krásy tohoto přístupu je to, že kdykoli vaše organizace přidá nebo odstraní uživatele nebo když uživatel změní heslo, použijete stejný proces, který dnes využijete v místním prostředí. Všechny změny vaší místní služby Active Directory se automaticky rozšíří do cloudového prostředí.

Pokud vaše společnost používá nebo přesouvá sadu Office 365, dobrá zpráva je, že budete mít službu Azure AD nastavenou automaticky, protože sada Office 365 pro ověřování používá službu Azure AD. Takže můžete snadno použít ve svých aplikacích stejné ověřování, které používá sada Office 365.

## <a name="set-up-an-azure-ad-tenant"></a>Nastavení tenanta Azure AD

adresář služby Azure AD se nazývá [tenant](https://technet.microsoft.com/library/jj573650.aspx)Azure AD a nastavení tenanta je poměrně snadné. Ukážeme vám, jak se to provede v Azure Portál pro správu, aby bylo možné ilustrovat koncepty, ale samozřejmě jako jiné funkce portálu to můžete udělat také pomocí skriptu nebo rozhraní API pro správu.

Na portálu pro správu klikněte na kartu Active Directory.

![WAAD na portálu](single-sign-on/_static/image5.png)

Pro svůj účet Azure máte automaticky jednoho tenanta Azure AD a můžete kliknout na tlačítko **Přidat** v dolní části stránky a vytvořit další adresáře. Můžete chtít jeden pro testovací prostředí a jeden pro produkční prostředí, například. Zamyslete se nad tím, co pojmenujte nový adresář. Pokud pro tento adresář použijete své jméno a potom pro jednoho z nich použijete své jméno, může to být matoucí.

![Přidat adresář](single-sign-on/_static/image6.png)

Portál má úplnou podporu pro vytváření, odstraňování a správu uživatelů v rámci tohoto prostředí. Pokud například chcete přidat uživatele, přejděte na kartu **Uživatelé** a klikněte na tlačítko **Přidat uživatele** .

![Tlačítko Přidat uživatele](single-sign-on/_static/image7.png)

![Přidat uživatelský dialog](single-sign-on/_static/image8.png)

Můžete vytvořit nového uživatele, který existuje pouze v tomto adresáři, nebo můžete zaregistrovat účet Microsoft jako uživatele v tomto adresáři nebo zaregistrovat nebo uživatele z jiného adresáře služby Azure AD jako uživatel v tomto adresáři. (Ve skutečném adresáři by se ContosoTest.onmicrosoft.com výchozí doména. Můžete také použít doménu podle vlastního výběru, například contoso.com.)

![Uživatelské typy](single-sign-on/_static/image9.png)

![Přidat uživatelský dialog](single-sign-on/_static/image10.png)

Uživatele můžete přiřadit k roli.

![Profil uživatele](single-sign-on/_static/image11.png)

A účet se vytvoří s dočasným heslem.

![Dočasné heslo](single-sign-on/_static/image12.png)

Uživatelé, které vytváříte tímto způsobem, se můžou ke svým webovým aplikacím přihlašovat hned pomocí tohoto adresáře cloudu.

To je skvělé pro podnikové jednotné přihlašování, ale je to karta **integrace adresáře** :

![Karta integrace adresáře](single-sign-on/_static/image13.png)

Pokud povolíte integraci adresáře a [stáhnete nástroj](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), můžete tento cloudový adresář synchronizovat se stávající místní službou Active Directory, kterou už ve vaší organizaci používáte. Pak se v tomto cloudovém adresáři zobrazí všichni uživatelé, kteří jsou v adresáři. Vaše cloudové aplikace teď můžou ověřit všechny vaše zaměstnance pomocí svých stávajících přihlašovacích údajů služby Active Directory. A všechno je zdarma – jak synchronizační nástroj, tak i služba Azure AD.

Tento nástroj je průvodcem, který se snadno používá, jak můžete vidět z těchto snímků obrazovky. Tyto pokyny nejsou kompletní, jenom příklad, který vám ukáže základní proces. Podrobnější informace o tom, jak to udělat, najdete v odkazech v části [Resources (prostředky](#resources) ) na konci kapitoly.

![Průvodce konfigurací nástroje pro synchronizaci WAAD](single-sign-on/_static/image14.png)

Klikněte na **Další**a potom zadejte přihlašovací údaje Azure Active Directory.

![Průvodce konfigurací nástroje pro synchronizaci WAAD](single-sign-on/_static/image15.png)

Klikněte na **Další**a potom zadejte svoje místní přihlašovací údaje služby AD.

![Průvodce konfigurací nástroje pro synchronizaci WAAD](single-sign-on/_static/image16.png)

Klikněte na **Další**a pak určete, jestli chcete v cloudu ukládat hodnoty hash hesel služby AD.

![Průvodce konfigurací nástroje pro synchronizaci WAAD](single-sign-on/_static/image17.png)

Hodnota hash hesla, kterou můžete uložit v cloudu, je jednosměrná hodnota hash. Skutečná hesla se nikdy neukládají v Azure AD. Pokud se rozhodnete ukládat hodnoty hash v cloudu, budete muset použít [Active Directory Federation Services (AD FS)](https://technet.microsoft.com/library/hh831502.aspx) (ADFS). K dispozici jsou také [Další faktory, které byste měli vzít v úvahu při rozhodování, zda používat službu AD FS](https://technet.microsoft.com/library/jj573653.aspx). Možnost ADFS vyžaduje několik dalších kroků konfigurace.

Pokud se rozhodnete ukládat hodnoty hash do cloudu, jste hotovi a nástroj po kliknutí na **Další**spustí synchronizaci adresářů.

![Průvodce konfigurací nástroje pro synchronizaci WAAD](single-sign-on/_static/image18.png)

A za pár minut jste hotovi.

![Průvodce konfigurací nástroje pro synchronizaci WAAD](single-sign-on/_static/image19.png)

Stačí ho spustit na jednom řadiči domény v organizaci ve Windows 2003 nebo novějším. A není nutné restartovat počítač. Až to budete mít, všichni uživatelé budou v cloudu a můžete provádět jednotné přihlašování z libovolné webové nebo mobilní aplikace, pomocí SAML, OAuth nebo WS-dodávání.

V některých případech se dozvíte, jak se to dělá, protože ho Microsoft používá pro vlastní citlivá firemní data? A odpověď je Ano. Například pokud přejdete na interní web Microsoft SharePointu na adrese [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/), zobrazí se výzva k přihlášení.

![Přihlášení k Office 365](single-sign-on/_static/image20.png)

Společnost Microsoft povolila službu AD FS, takže když zadáte ID Microsoftu, budete přesměrováni na přihlašovací stránku služby AD FS.

![Přihlášení k ADFS](single-sign-on/_static/image21.png)

A když zadáte přihlašovací údaje uložené v interním účtu Microsoft AD, budete mít přístup k této interní aplikaci.

![Web služby SharePoint společnosti Microsoft](single-sign-on/_static/image22.png)

K dispozici je server pro přihlášení k reklamě, protože už jsme nastavili službu AD FS dřív, než se služba Azure AD stala dostupná, ale proces přihlášení projde adresářem služby Azure AD v cloudu. Naše důležité dokumenty, Správa zdrojového kódu, soubory pro správu výkonu, prodejní sestavy a další jsou v cloudu a používají toto přesné řešení k zabezpečení.

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a>Vytvoření aplikace ASP.NET, která používá Azure AD pro jednotné přihlašování

Visual Studio umožňuje opravdu snadno vytvořit aplikaci, která používá Azure AD pro jednotné přihlašování, jak vidíte z několika snímků obrazovky.

Při vytváření nové aplikace ASP.NET, MVC nebo webových formulářů, je výchozí metoda ověřování ASP.NET Identity. Pokud ho chcete změnit na Azure AD, klikněte na tlačítko **změnit ověřování** .

![Změnit ověřování](single-sign-on/_static/image23.png)

Vyberte účty organizace, zadejte název domény a pak vyberte jednotné přihlašování.

![Dialogové okno Konfigurace ověřování](single-sign-on/_static/image24.png)

Můžete taky udělit oprávnění ke čtení nebo čtení a zápisu pro data adresáře aplikace. Pokud to uděláte, může k vyhledání telefonního čísla uživatele použít [REST API Azure Graph](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) , zjistit, jestli jsou v kanceláři, kdy se naposledy přihlásili atd.

To je všechno, co musíte udělat – Visual Studio si vyžádá pověření pro správce vašeho tenanta Azure AD a potom nakonfiguruje projekt i tenanta Azure AD pro novou aplikaci.

Při spuštění projektu se zobrazí přihlašovací stránka a můžete se přihlásit pomocí přihlašovacích údajů uživatele v adresáři služby Azure AD.

![Přihlášení k účtu org](single-sign-on/_static/image25.png)

![Přihlášen](single-sign-on/_static/image26.png)

Když nasadíte aplikaci do Azure, stačí, když zaškrtnete políčko **Povolit ověřování organizace** , a jakmile se Visual Studio bude starat o veškerou konfiguraci za vás.

![Publikování webu](single-sign-on/_static/image27.png)

Tyto snímky obrazovky pocházejí z kompletního podrobného kurzu, který ukazuje, jak vytvořit aplikaci, která používá ověřování Azure AD: [vývoj aplikací ASP.NET pomocí Azure Active Directory](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md).

## <a name="summary"></a>Přehled

V této kapitole jste viděli, že Azure Active Directory, Visual Studio a ASP.NET usnadňují nastavení jednotného přihlašování v internetových aplikacích pro uživatele vaší organizace. Uživatelé se můžou k internetovým aplikacím přihlašovat pomocí stejných přihlašovacích údajů, které používají k přihlášení pomocí služby Active Directory ve vaší interní síti.

[Další kapitola](data-storage-options.md) si vyhledá možnosti úložiště dat dostupné pro cloudovou aplikaci.

<a id="resources"></a>
## <a name="resources"></a>Prostředky

Další informace naleznete v následujících zdrojích:

- [Azure Active Directory dokumentaci](https://docs.microsoft.com/azure/active-directory/). Stránka portálu pro dokumentaci k Azure AD na webu windowsazure.com. Podrobné kurzy najdete v části **vývoj** .
- [Multi-Factor Authentication Azure](https://docs.microsoft.com/azure/multi-factor-authentication/). Stránka portálu pro dokumentaci k Multi-Factor Authentication v Azure.
- [Možnosti ověřování účtu organizace](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions) Vysvětlení možností ověřování Azure AD v dialogovém okně Visual Studio 2013 nový projekt.
- [Vzory a postupy Microsoft – model federované identity](https://msdn.microsoft.com/library/dn589790.aspx).
- [Postupy: Nainstalujte nástroj Azure Active Directory Sync](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx).
- [Mapa obsahu Active Directory Federation Services (AD FS) 2,0](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx) Odkazy na dokumentaci ke službě ADFS 2,0.
- [Ověřování na základě rolí a ACL v aplikaci Windows Azure AD](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1). Ukázková aplikace
- [Azure Active Directory Graph API Blog](https://blogs.msdn.com/b/aadgraphteam/).
- [Access Control v integraci BYOD a adresáře v hybridní infrastruktuře identit](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=). Video o relaci Tech Ed 2014 od Gayana Bagdasaryan.

> [!div class="step-by-step"]
> [Předchozí](web-development-best-practices.md)
> [Další](data-storage-options.md)
