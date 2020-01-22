---
uid: visual-studio/overview/2013/creating-web-projects-in-visual-studio
title: Vytváření ASP.NET webových projektů v Visual Studio 2013 | Microsoft Docs
author: tdykstra
description: Toto téma vysvětluje možnosti pro vytváření ASP.NET webových projektů v Visual Studio 2013 s aktualizací Update 3 zde jsou některé nové funkce pro vývoj webů c...
ms.author: riande
ms.date: 12/01/2014
ms.assetid: 61941e64-0c0d-4996-9270-cb8ccfd0cabc
msc.legacyurl: /visual-studio/overview/2013/creating-web-projects-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: fbb4cd7afa2506879d47bce980bf0164aad40c2c
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519268"
---
# <a name="creating-aspnet-web-projects-in-visual-studio-2013"></a>Vytváření webových projektů ASP.NET v sadě Visual Studio 2013

tím, že [Dykstra](https://github.com/tdykstra)

> Toto téma vysvětluje možnosti pro vytváření webových projektů v ASP.NET v Visual Studio 2013 s aktualizací Update 3.
> 
> Zde jsou některé nové funkce pro vývoj webu v porovnání s předchozími verzemi sady Visual Studio:
> 
> - Jednoduché uživatelské rozhraní pro vytváření projektů, které nabízí [podporu pro víc ASP.NETch platforem](#add) (webové formuláře, MVC a webové rozhraní API).
> - [ASP.NET identity](#indauth)nový systém členství v ASP.NET, který funguje stejně ve všech ASP.NET architekturách a pracuje s jiným softwarem pro hostování webů, než je služba IIS.
> - Použití funkce [bootstrap](#bootstrap) k zajištění reakce na návrh a možnosti.
> - Nové funkce pro webové formuláře, které slouží k nabídnutí pouze pro MVC, jako je například [Automatické vytváření projektů testů](#testproj) a [Šablona intranetového webu](#winauth).
> 
> Informace o tom, jak vytvořit webové projekty pro Azure Cloud Services nebo Azure Mobile Services, najdete v tématu Začínáme [s azure Cloud Services a ASP.NET](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/) a [Vytvoření aplikace tabulek výsledků pomocí back-endu .net pro Azure Mobile Services](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/).

<a id="prerequisites"></a>
## <a name="prerequisites"></a>Požadavky

Tento článek se týká [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) s nainstalovanou [aktualizací Update 3](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409) .

<a id="wap"></a>
## <a name="web-application-projects-versus-web-site-projects"></a>Projekty webové aplikace versus webové projekty

ASP.NET nabízí možnost volby mezi dvěma druhy webových projektů: *projekty webové aplikace* a *projekty*webu. Doporučujeme projekty webové aplikace pro nový vývoj a tento článek se vztahuje pouze na projekty webové aplikace. Další informace naleznete v tématu [projekty webové aplikace versus webové projekty v aplikaci Visual Studio](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx) na webu MSDN.

<a id="overview"></a>
## <a name="overview-of-web-application-project-creation"></a>Přehled vytvoření projektu webové aplikace

Následující kroky ukazují, jak vytvořit webový projekt:

1. Na **úvodní** stránce nebo v nabídce **soubor** klikněte na **Nový projekt** .
2. V dialogovém okně **Nový projekt** klikněte v levém podokně na **Web** a **ASP.NET webová aplikace** v prostředním podokně.

    ![Dialogové okno nového projektu](creating-web-projects-in-visual-studio/_static/image1.png)

    V levém podokně můžete vybrat **Cloud** a vytvořit [cloudovou službu Azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy), [mobilní službu Azure](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx)nebo [webovou úlohu Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs). Toto téma se nevztahuje na tyto šablony.
3. V pravém podokně zaškrtněte políčko **přidat Application Insights do projektu** , pokud chcete pro svou aplikaci sledovat stav a využití. Další informace najdete v tématu [monitorování výkonu ve webových aplikacích](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/).
4. Zadejte **název**projektu, **umístění**a další možnosti a pak klikněte na **OK**.

    Zobrazí se dialogové okno **Nový projekt ASP.NET** .

    ![Dialogové okno nového projektu](creating-web-projects-in-visual-studio/_static/image2.png)
5. Klikněte na šablonu.

    ![Vyberte šablonu](creating-web-projects-in-visual-studio/_static/image3.png)
6. Pokud chcete přidat podporu pro další architektury, které nejsou součástí šablony, zaškrtněte příslušné políčko. (V zobrazeném příkladu můžete přidat MVC nebo webové rozhraní API do projektu webových formulářů.)

    ![Přidat rozhraní](creating-web-projects-in-visual-studio/_static/image4.png)
7. <a id="testproj"></a>Chcete-li přidat projekt testování částí, klikněte na možnost **Přidat testy jednotek**.

    ![Přidat testy jednotek](creating-web-projects-in-visual-studio/_static/image5.png)
8. Pokud chcete jinou metodu ověřování, než jakou šablona ve výchozím nastavení poskytuje, klikněte na **změnit ověřování**.

    ![Tlačítko konfigurovat ověřování](creating-web-projects-in-visual-studio/_static/image6.png)

    ![Dialogové okno Konfigurace ověřování](creating-web-projects-in-visual-studio/_static/image7.png)

<a id="azurenewproj"></a>
### <a name="create-a-web-app-or-virtual-machine-in-azure"></a>Vytvoření webové aplikace nebo virtuálního počítače v Azure

Visual Studio obsahuje funkce, které usnadňují práci se službami Azure pro hostování webových aplikací. V integrovaném vývojovém prostředí sady Visual Studio můžete například provést všechna následující práva:

- Vytvářejte a spravujte webové aplikace nebo virtuální počítače, které zpřístupňují vaši aplikaci přes Internet.
- Zobrazit protokoly vytvořené aplikací při spuštění v cloudu.
- Spouštějte v režimu ladění vzdáleně při spuštění aplikace v cloudu.
- Umožňuje zobrazit a spravovat další služby Azure, jako jsou databáze SQL.

Můžete [vytvořit účet Azure](https://www.windowsazure.com/pricing/free-trial/) , který zahrnuje základní služby, jako jsou třeba webové aplikace, a pokud jste předplatitelem MSDN, můžete [aktivovat výhody](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/) , které vám poskytnou měsíční kredit na další služby Azure. 

Ve výchozím nastavení se v dialogovém okně **Nový projekt ASP.NET** umožňuje vytvořit webovou aplikaci nebo virtuální počítač pro nový webový projekt. Pokud nechcete vytvořit novou webovou aplikaci nebo virtuální počítač, zrušte zaškrtnutí políčka **hostitel v cloudu** .

![Vytvoření vzdálených prostředků](creating-web-projects-in-visual-studio/_static/image8.png)

Popisek zaškrtávacího políčka může být **hostitel v cloudu** nebo **vytvářet vzdálené prostředky**a v obou případech je efekt stejný. Pokud ponecháte zaškrtnuté políčko, Visual Studio ve výchozím nastavení vytvoří webovou aplikaci ve Azure App Service. Pokud chcete, můžete to změnit na **virtuální počítač** pomocí rozevíracího seznamu. Pokud ještě nejste přihlášení k Azure, budete vyzváni k zadání přihlašovacích údajů Azure. Po přihlášení vám dialogové okno umožní nakonfigurovat prostředky, které Visual Studio vytvoří pro váš projekt. Následující ilustrace znázorňuje dialog webové aplikace. Pokud se rozhodnete vytvořit virtuální počítač, zobrazí se různé možnosti.

![Konfigurace nastavení aplikace Azure](creating-web-projects-in-visual-studio/_static/image9.png)

Další informace o tom, jak tento postup použít při vytváření prostředků Azure, najdete v tématech [Začínáme s Azure a ASP.NET](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) a [Vytvoření virtuálního počítače pro web pomocí sady Visual Studio](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/).

Zbývající část tohoto článku poskytuje další informace o dostupných šablonách a jejich možnostech. Článek také zavádí Bootstrap, rozložení a rozhraní pro použití v šablonách.

<a id="vs2013"></a>
## <a name="visual-studio-2013-web-project-templates"></a>Šablony Visual Studio 2013 webového projektu

Visual Studio používá šablony pro vytváření webových projektů. Šablona projektu může vytvořit soubory a složky v novém projektu, nainstalovat balíčky NuGet a poskytnout vzorový kód pro základní funkční aplikaci. Šablony implementují nejnovější webové standardy a jsou určené k předvedení osvědčených postupů pro používání technologií ASP.NET a také vám poskytnou odkaz na začátek vytváření vlastní aplikace.

Visual Studio 2013 poskytuje následující možnosti pro šablony webového projektu pro projekty, které cílí na .NET 4,5 nebo novější verze rozhraní .NET Framework:

- [Prázdná šablona](#empty)
- [Šablona webových formulářů](#wf)
- [Šablona MVC](#mvc)
- [Šablona webového rozhraní API](#webapi)
- [Jedna stránka – šablona aplikace](#spa)
- [Šablona mobilní služby Azure](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)
- [Šablony sady Visual Studio 2012](#vs2012)

Můžete také nainstalovat rozšíření sady Visual Studio, které poskytuje [šablonu Facebooku](#facebook).

Informace o vytváření projektů cílených na rozhraní .NET 4 naleznete v tématu [šablony sady Visual Studio 2012](#vs2012) dále v tomto tématu.

Informace o tom, jak vytvářet ASP.NET aplikace pro mobilní klienty, najdete [v tématu mobilní podpora v ASP.NET](../../../mobile/overview.md).

<a id="empty"></a>
### <a name="empty-template"></a>Prázdná šablona

Prázdná šablona poskytuje minimální složky a soubory pro webovou aplikaci ASP.NET, jako je soubor projektu ( *. csproj* nebo. *vbproj*) a soubor *Web. config* . Podporu webových formulářů, MVC a/nebo webového rozhraní API můžete přidat pomocí zaškrtávacích políček v části **Přidat složky a základní odkazy pro:** Label.

Pro prázdnou šablonu nejsou k dispozici žádné možnosti ověřování. Funkce ověřování je implementována v ukázkových aplikacích a prázdná šablona nevytváří ukázkovou aplikaci.

<a id="wf"></a>
### <a name="web-forms-template"></a>Šablona webových formulářů

Rozhraní Web Forms Framework nabízí následující funkce, které vám umožní rychle vytvářet weby, které jsou bohatě v uživatelském rozhraní a funkcích pro přístup k datům:

- Návrhář WYSIWYG v aplikaci Visual Studio.
- Serverové ovládací prvky, které vykreslují HTML a které lze přizpůsobit nastavením vlastností a stylů.
- Bohatě se seznam ovládacích prvků pro přístup k datům a zobrazení dat.
- Model událostí, který zpřístupňuje události, které lze programovat jako program aplikace klienta, jako je například WPF.
- Automatické uchovávání stavů (dat) mezi požadavky HTTP.

Obecně platí, že vytvoření aplikace webových formulářů vyžaduje méně programovací úsilí než vytváření stejné aplikace pomocí architektury ASP.NET MVC. Webové formuláře ale nestačí jenom pro rychlý vývoj aplikací. K dispozici je celá řada složitých komerčních aplikací a platforem postavených nad webovými formuláři.

Vzhledem k tomu, že stránka webového formuláře a ovládací prvky na stránce automaticky generují většinu značek, které se odesílají do prohlížeče, nebudete mít k dispozici detailní kontrolu nad kódem HTML, který ASP.NET MVC nabízí. Deklarativní model pro konfiguraci stránek a ovládacích prvků minimalizuje množství kódu, který musíte napsat, ale skrývá některé chování HTML a HTTP. Například není vždy možné přesně určit, jaký kód může být generován ovládacím prvkem.

Rozhraní Web Forms se samoně neposkytuje jako ASP.NET MVC na vzory vývoje založené na vzorech, jako je [Vývoj řízený testy](http://en.wikipedia.org/wiki/Test-driven_development), [oddělení obav](http://en.wikipedia.org/wiki/Separation_of_concerns), [inverze řízení](http://en.wikipedia.org/wiki/Inversion_of_control)a [vkládání závislostí](http://en.wikipedia.org/wiki/Dependency_injection). Pokud chcete napsat kód, který je tímto způsobem vytvořen, můžete; Nejedná se pouze o automatické, protože je v rozhraní ASP.NET MVC. Projekt [MVP pro webové formuláře ASP.NET](http://webformsmvp.com/) znázorňuje přístup, který usnadňuje oddělení obav a možností testování a zároveň udržuje rychlý vývoj, který webové formuláře vytvořily. Služba Microsoft SharePoint je postavená na MVP pro webové formuláře.

Šablona webových formulářů vytvoří ukázkovou aplikaci webových formulářů, která pomocí [bootstrap](#bootstrap) zajišťuje reakce na návrh a funkce. Na následujícím obrázku je znázorněna Domovská stránka.

![Domovská stránka webové formuláře aplikace](creating-web-projects-in-visual-studio/_static/image10.png)

Další informace o webových formulářích naleznete v tématu [ASP.NET Web Forms](https://asp.net/web-forms). Informace o tom, co šablona webových formulářů pro vás dělá, najdete v tématu [Vytvoření základní aplikace webového formuláře pomocí Visual Studio 2013](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx).

<a id="mvc"></a>
### <a name="mvc-template"></a>Šablona MVC

Služba ASP.NET MVC byla navržena tak, aby usnadnila vývojové postupy založené na vzorech, jako je [Vývoj řízený testy](http://en.wikipedia.org/wiki/Test-driven_development), [oddělení obav](http://en.wikipedia.org/wiki/Separation_of_concerns), [inverze řízení](http://en.wikipedia.org/wiki/Inversion_of_control)a [vkládání závislostí](http://en.wikipedia.org/wiki/Dependency_injection). Rozhraní podporuje oddělení vrstvy obchodní logiky webové aplikace od své prezentační vrstvy. Díky rozdělení aplikace do modelů (M), zobrazení (V) a řadičů (C) může ASP.NET MVC usnadnit správu složitosti ve větších aplikacích.

S ASP.NET MVC pracujete přímo s HTML a HTTP než ve webových formulářích. Například webové formuláře mohou automaticky zachovávat stav mezi požadavky HTTP, ale je nutné kód, který je explicitně v MVC. Výhodou modelu MVC je to, že umožňuje převzít úplnou kontrolu nad přesně tím, co vaše aplikace dělá a jak se chová ve webovém prostředí. Nevýhodou je, že musíte napsat více kódu.

Služba MVC byla navržena tak, aby byla rozšiřitelná a poskytovala vývojářům možnost přizpůsobit si rámec pro potřeby svých aplikací. Kromě toho je zdrojový kód ASP.NET MVC k dispozici v rámci licence OSI.

Šablona MVC vytvoří ukázkovou aplikaci MVC 5, která pomocí [bootstrap](#bootstrap) zajišťuje reakce na návrh a funkce. Na následujícím obrázku je znázorněna Domovská stránka.

![Ukázková aplikace MVC](creating-web-projects-in-visual-studio/_static/image11.png)

Další informace o MVC najdete v tématu [ASP.NET MVC](https://asp.net/mvc). Informace o tom, jak vybrat šablonu MVC 4, najdete v tématu [šablony sady Visual Studio 2012](#vs2012) dále v tomto článku.

<a id="webapi"></a>
### <a name="web-api-template"></a>Šablona webového rozhraní API

Šablona webového rozhraní API vytvoří ukázkovou webovou službu založenou na webovém rozhraní API, včetně stránek s nápovědě k rozhraní API založených na MVC.

Rozhraní ASP.NET Web API usnadňuje sestavování služeb HTTP, které jsou poskytovány širokému spektru klientů, včetně prohlížečů a mobilních zařízení. Webové rozhraní API ASP.NET je ideální platformou pro vytváření služeb RESTful na .NET Framework.

Šablona webového rozhraní API vytvoří ukázkovou webovou službu. Na následujících obrázcích je znázorněno, jak zobrazit stránky s ukázkou.

![Stránka s webovou pomocí rozhraní API](creating-web-projects-in-visual-studio/_static/image12.png)

![Stránka Nápověda k webovému rozhraní API pro rozhraní GET API](creating-web-projects-in-visual-studio/_static/image13.png)

Další informace o webovém rozhraní API najdete v tématu [webové rozhraní](https://asp.net/web-api)api pro ASP.NET.

<a id="spa"></a>
### <a name="single-page-application-template"></a>Šablona jednostránkové aplikace

Šablona jednostránkové aplikace (SPA) vytvoří ukázkovou aplikaci, která používá JavaScript, HTML 5 a [KnockoutJS](http://knockoutjs.com/) na straně klienta a webové rozhraní API na serveru ASP.NET.

Jedinou možností ověřování pro šablonu SPA jsou [jednotlivé uživatelské účty](#indauth).

Následující ilustrace znázorňuje počáteční stav ukázkové aplikace, kterou vytváří šablona SPA.

![Ukázková aplikace SPA](creating-web-projects-in-visual-studio/_static/image14.png)

Informace o tom, jak vytvořit aplikaci pomocí šablony SPA, najdete v tématu [webové rozhraní API – externí ověřování služby](../../../web-api/overview/security/external-authentication-services.md).

Další informace o aplikacích ASP.NET Single Page a o dalších šablonách SPA, které používají rozhraní JavaScript jiné než KnockoutJS, najdete v následujících zdrojích informací:

- [ASP.NET aplikace s jednou stránkou](../../../single-page-application/index.md)
- [Principy funkcí zabezpečení v šabloně SPA pro VS2013 RC](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)
- [Jednostránkové aplikace: Sestavujte moderní, reagující Web Apps s ASP.NET](https://msdn.microsoft.com/magazine/dn463786.aspx)

<a id="facebook"></a>
### <a name="facebook-template"></a>Šablona Facebooku

Můžete nainstalovat rozšíření sady [Visual Studio, které poskytuje šablonu Facebooku](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409). Tato šablona vytvoří ukázkovou aplikaci, která je navržena pro běh na webu Facebook. Vychází z ASP.NET MVC a využívá webové rozhraní API pro funkce aktualizace v reálném čase.

Pro šablonu Facebooku nejsou k dispozici žádné možnosti ověřování, protože aplikace na Facebooku běží na webu Facebook a spoléhají na ověřování Facebooku.

Další informace o aplikacích ASP.NET Facebook najdete v tématu [aktualizace rozhraní API Facebooku pro MVC](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx).

<a id="vs2012"></a>
### <a name="visual-studio-2012-templates"></a>Šablony sady Visual Studio 2012

Dialog pro vytvoření webového projektu Visual Studio 2013 neposkytuje přístup k některým šablonám, které byly k dispozici v aplikaci Visual Studio 2012. Pokud chcete použít jednu z těchto šablon, můžete kliknout na uzel sady Visual Studio 2012 v levém podokně dialogového okna Nový projekt aplikace Visual Studio.

![Šablony sady Visual Studio 2012](creating-web-projects-in-visual-studio/_static/image15.png)

Uzel sady **Visual Studio 2012** umožňuje vybrat následující webové šablony, ke kterým nemáte přístup, ve výchozím seznamu šablon pro Visual Studio 2013:

- Webová aplikace ASP.NET MVC 4
- Webová aplikace ASP.NET s dynamickými datovými entitami
- Serverový ovládací prvek ASP.NET AJAX
- ASP.NET AJAX Server Control Extender
- Serverový ovládací prvek ASP.NET

<a id="bootstrap"></a>
## <a name="bootstrap-in-the-visual-studio-2013-web-project-templates"></a>Zavedení v šablonách webového projektu Visual Studio 2013

Šablony projektu Visual Studio 2013 používají [bootstrap](http://getbootstrap.com/), rozložení a rozhraní pro vytváření na Twitteru. Bootstrap používá CSS3 k tomu, aby poskytovala reagující návrh, což znamená, že rozložení se můžou dynamicky přizpůsobovat různým velikostem oken prohlížeče. Například v pravém okně prohlížeče je Domovská stránka vytvořená šablonou webových formulářů vypadat jako na následujícím obrázku:

![Domovská stránka webové formuláře aplikace](creating-web-projects-in-visual-studio/_static/image16.png)

Udělejte zúžení okna a vodorovně uspořádané sloupce se přesunou do vertikálního uspořádání:

![Spouštěcí uspořádání vertikálních sloupců](creating-web-projects-in-visual-studio/_static/image17.png)

Zúžení okna o něco dalšího a vodorovná horní nabídka se změní na ikonu, kterou můžete kliknutím rozbalit do vertikálně orientované nabídky:

![Ikona nabídky Bootstrap](creating-web-projects-in-visual-studio/_static/image18.png)

![Počáteční nabídka spustit svisle](creating-web-projects-in-visual-studio/_static/image19.png)

Můžete také použít funkci zaváděcí rutiny Bootstrap, která umožňuje snadno změnit vzhled a chování aplikace. Můžete například změnit motiv tak, že provedete následující kroky.

1. V prohlížeči přejděte na [http://Bootswatch.com](http://Bootswatch.com), zvolte motiv a pak klikněte na **Stáhnout**. (Ve výchozím nastavení se ke stažení načítá *. min. CSS.* Pokud si chcete prohlédnout kód CSS, Získejte místo verze minifikovaného *bootstrap. CSS* .)
2. Zkopírujte obsah staženého souboru CSS.
3. V aplikaci Visual Studio vytvořte nový soubor **šablony stylů** s názvem *bootstrap-Theme. CSS* ve složce *obsahu* a vložte do něj stažený kód CSS.
4. Otevřete *App\_Start/komplet. config* a změňte *bootstrap. CSS* na *bootstrap-Theme. CSS*.

Spusťte projekt znovu a aplikace má nový vzhled. Následující obrázek ukazuje efekt motivu Amelia:

![Spouštěcí motiv Amelia](creating-web-projects-in-visual-studio/_static/image20.png)

K dispozici je spousta spouštěcích motivů, verze Free i Premium. Bootstrap také nabízí širokou škálu součástí uživatelského rozhraní, jako jsou [rozevírací nabídky](http://twitter.github.io/bootstrap/components.html#dropdowns), [skupiny tlačítek](http://twitter.github.io/bootstrap/components.html#buttonGroups)a [ikony](http://twitter.github.io/bootstrap/base-css.html#images). Další informace o Bootstrap najdete v části [bootstrap webu](http://twitter.github.io/bootstrap/).

Použijete-li návrháře webových formulářů v aplikaci Visual Studio, Všimněte si, že Návrhář nepodporuje CSS3, takže nezobrazuje přesně všechny účinky spouštěcích motivů nebo reagující změny v rozložení. Stránky webových formulářů se ale při prohlížení v prohlížeči zobrazí správně.

<a id="add"></a>
## <a name="adding-support-for-additional-frameworks"></a>Přidání podpory pro další architektury

Když vyberete šablonu, bude automaticky vybráno zaškrtávací políčko pro rozhraní používané šablonou. Pokud například vyberete šablonu **webových formulářů** , je zaškrtnuté políčko **webové formuláře** a nemůžete ho vymazat.

![Vyberte šablonu](creating-web-projects-in-visual-studio/_static/image21.png)

![Přidat rozhraní](creating-web-projects-in-visual-studio/_static/image22.png)

Můžete zaškrtnout políčko pro rozhraní, které není součástí šablony, aby bylo možné přidat podporu pro tuto architekturu při vytvoření projektu. Chcete-li například povolit použití stránek Web Forms *. aspx* po výběru šablony MVC, zaškrtněte políčko **webové formuláře** . Nebo pokud chcete povolit MVC při použití šablony webových formulářů, klikněte na zaškrtávací políčko **MVC** . Přidání rozhraní umožňuje povolit i dobu návrhu a podporu za běhu. Například pokud přidáte podporu MVC do projektu webových formulářů, budete moci zobrazit řadiče a zobrazení uživatelského rozhraní.

Pokud kombinujete webové formuláře a MVC v projektu a povolíte [popisné adresy URL](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx) webových formulářů, může dojít k neočekávaným potížím s směrováním, kde jedna adresa URL má více možných cílů. Trasy, které jsou definovány jako první, budou mít přednost. Například pokud máte řadič `Home` a stránku *Home. aspx* , bude adresa URL `http://contoso.com/home` přejít na *Home. aspx* při volání metody `EnableFriendlyUrls` před voláním metody `MapRoute` v *RouteConfig.cs*, nebo stejná adresa URL přejde do výchozího zobrazení pro váš řadič `Home`, pokud voláte `MapRoute` před `EnableFriendlyUrls`.

Přidáním rozhraní se nepřidá žádná ukázková funkce aplikace. Pokud například přidáte podporu webových formulářů v případě, že jste vybrali šablonu MVC, není vytvořen žádný soubor *Default. aspx* domovské stránky. Přidávají se pouze složky, soubory a odkazy, které jsou vyžadovány pro podporu rozhraní. Z tohoto důvodu přidávání rozhraní nemění možnosti ověřování, které jsou implementovány kódem v ukázkových aplikacích vytvořených šablonami. Pokud například vyberete prázdnou šablonu a přidáte webové formuláře nebo podporu MVC, bude tlačítko **Konfigurovat ověřování** stále zakázáno.

Následující části popisují stručný vliv každého zaškrtávacího políčka.

### <a name="add-web-forms-support"></a>Přidat podporu webových formulářů

Vytvoří prázdnou *aplikaci\_* složky s daty a *modely* a soubor *Global. asax* . Tyto položky jsou již vytvořeny všemi šablonami, které jsou jiné než prázdná šablona, takže zaškrtnutí políčka webové formuláře nevede k žádným rozdílům pro jiné šablony.

Šablona webových formulářů umožňuje ve výchozím nastavení zadat popisné adresy URL, ale když přidáte podporu webových formulářů do jiných šablon, zaškrtněte políčko webové formuláře popisné adresy URL nejsou automaticky povoleny.

### <a name="add-mvc-support"></a>Přidat podporu MVC

Nainstaluje balíčky NuGet, Razor a webpages, vytvoří prázdnou *aplikaci\_data*, *řadiče*, *modely*a složky *zobrazení* , vytvoří *aplikaci\_spouštěcí* složku se souborem *RouteConfig.cs* a vytvoří soubor *Global. asax* .

### <a name="add-web-api-support"></a>Přidat podporu webového rozhraní API

Nainstaluje balíčky NuGet WebApi a Newtonsoft. JSON, vytvoří prázdnou *aplikaci\_data*, *řadiče*a složky *modelů* , vytvoří *aplikaci\_spouštěcí* složku se souborem *WebApiConfig.cs* a vytvoří soubor *Global. asax* .

<a id="auth"></a>
## <a name="authentication-methods"></a>Metody ověřování

Visual Studio 2013 nabízí několik možností ověřování pro webové formuláře, MVC a šablony webového rozhraní API:

- [Bez ověřování](#noauth)
- [Jednotlivé uživatelské účty](#indauth) (ASP.NET identity dřív označované jako členství v ASP.NET)
- [Účty organizace](#orgauth) (Windows Server Active Directory nebo Azure Active Directory)
- [Ověřování systému Windows](#winauth) (intranet)

![Dialogové okno Konfigurace ověřování](creating-web-projects-in-visual-studio/_static/image23.png)

<a id="noauth"></a>

### <a name="no-authentication"></a>Bez ověřování

Pokud nevyberete **žádné ověření**, ukázková aplikace nebude obsahovat žádné webové stránky pro přihlášení, žádné uživatelské rozhraní, které indikuje, kdo není přihlášen, žádné třídy entit pro databázi členství a žádný připojovací řetězec pro databázi členství.

<a id="indauth"></a>
### <a name="individual-user-accounts"></a>Jednotlivé uživatelské účty

Když vyberete **jednotlivé uživatelské účty**, ukázková aplikace se nakonfiguruje tak, aby používala ASP.NET identity (dřív označovaná jako členství v ASP.NET) pro ověřování uživatelů. ASP.NET Identity umožňuje uživateli zaregistrovat účet, a to vytvořením uživatelského jména a hesla na webu nebo přihlášením pomocí poskytovatelů sociálních sítí, jako je Facebook, Google, účet Microsoft nebo Twitter. Výchozím úložištěm dat pro profily uživatelů v ASP.NET Identity je databáze SQL Server LocalDB, kterou můžete nasadit do SQL Server nebo Azure SQL Database pro produkční lokalitu.

V Visual Studio 2013 tyto funkce jsou stejné jako v aplikaci Visual Studio 2012, ale podkladový kód pro systém členství v ASP.NET byl přepsán. Mezi výhody nového základu kódu patří následující:

- Nový systém členství je založený na [Owin](http://owin.org/) namísto modulu ověřování ASP.NET Forms. To znamená, že můžete použít stejný ověřovací mechanismus bez ohledu na to, jestli používáte webové formuláře nebo MVC ve službě IIS, nebo jste samoobslužně hostující webové rozhraní API nebo signál.
- Nová databáze členství je spravována pomocí Entity Framework Code First a všechny tabulky jsou reprezentovány třídami entit, které lze upravit. To znamená, že můžete snadno přizpůsobit schéma databáze a webové uživatelské rozhraní související s profilem tak, aby vyhovovalo vašim potřebám, a můžete snadno nasadit své aktualizace pomocí Migrace Code First.

Nový systém členství je implementován automaticky v nových šablonách a může být implementován ručně v jakémkoli projektu, který cílí na rozhraní .NET 4,5 nebo novější.

ASP.NET Identity je dobrá volba, pokud vytváříte internetový web, který je převážně pro externí zákazníky. Pokud vaše organizace používá službu Active Directory nebo Office 365 a chcete vytvořit projekt, který umožňuje jednotné přihlašování pro zaměstnance a obchodní partnery, může být vhodnější volbou možnosti **účty organizace** .

Další informace o možnostech jednotlivých uživatelských účtů najdete v následujících zdrojích informací:

- [www.asp.net/identity](../../../identity/index.md). Dokumentace k ASP.NET Identity na webu ASP.NET.
- [Vytvořte aplikaci ASP.NET MVC 5 s aplikacemi Facebook a Google OAuth2 a OpenID Signing](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md). Také ukazuje, jak přizpůsobit data profilu uživatele.
- [Webové rozhraní API – externí ověřovací služby](../../../web-api/overview/security/external-authentication-services.md)
- [Přidání externích přihlášení do aplikace ASP.NET v Visual Studio 2013](https://blogs.msdn.com/b/webdev/archive/2013/06/27/adding-external-logins-to-your-asp-net-application-in-visual-studio-2013.aspx)

<a id="orgauth"></a>
### <a name="organizational-accounts"></a>Účty organizace

Pokud vyberete **účty organizace**, ukázková aplikace se nakonfiguruje tak, aby používala Windows Identity Foundation (WIF) k ověřování na základě uživatelských účtů ve službě Azure Active Directory (Azure AD, která zahrnuje Office 365) nebo Windows Server Active Directory. Další informace najdete v části [Možnosti ověřování účtu organizace](#orgauthoptions) dále v tomto tématu.

<a id="winauth"></a>
### <a name="windows-authentication"></a>Ověřování Windows

Pokud vyberete **ověřování systému Windows**, bude ukázková aplikace nakonfigurována tak, aby pro ověřování používala modul IIS ověřování systému Windows. Aplikace zobrazí doménu a ID uživatele účtu služby Active Directory nebo místního počítače, který je přihlášený k systému Windows, ale nezahrnuje registraci uživatele nebo uživatelské rozhraní pro přihlášení. Tato možnost je určená pro intranetové weby.

Případně můžete vytvořit intranetový web, který používá ověřování AD, a to tak, že v [části účty organizace vyberete možnost](#orgauthonprem)místní. Místní možnost používá Windows Identity Foundation (WIF) místo modulu ověřování systému Windows. Aby bylo možné nastavit místní možnost, je nutné provést některé další kroky, ale WIF umožňuje funkce, které nejsou k dispozici v modulu ověřování systému Windows. Pomocí WIF můžete například nakonfigurovat přístup k aplikacím ve službě Active Directory a data adresáře dotazů.

<a id="orgauthoptions"></a>
## <a name="organizational-account-authentication-options"></a>Možnosti ověřování účtu organizace

V dialogovém okně **Konfigurace ověřování** získáte několik možností Azure Active Directory (Azure AD, které zahrnují Office 365) nebo ověřování účtu služby Active Directory (AD) Windows serveru.

- [Cloudová organizace](#orgauthsingle) (Azure AD nebo AD s použitím integrace adresáře s Azure AD)
- [Cloud – víc organizací](#orgauthmulti) (Azure AD nebo AD pomocí integrace adresářů s Azure AD)
- [Místní](#orgauthonprem) (AD)

Pokud si chcete vyzkoušet jednu z možností Azure AD, ale ještě nemáte účet, [klikněte sem, abyste se mohli zaregistrovat k účtu Azure AD](https://go.microsoft.com/fwlink/?LinkId=309942).

> [!NOTE]
> Pokud zvolíte jednu z možností Azure AD, projekt vyžaduje databázi a musíte se přihlásit ke globálnímu účtu správce pro vašeho tenanta Azure AD. Zadejte jméno a heslo pro účet organizace (například admin@contoso.onmicrosoft.com), který má oprávnění správce pro vašeho tenanta Azure AD.
> 
> **Nezadávejte přihlašovací údaje pro účet Microsoft (například contoso@hotmail.com) v dialogovém okně přihlášení.**

<a id="orgauthsingle"></a>
### <a name="cloud---single-organization-authentication"></a>Ověřování v cloudu s jednou organizací

![Ověřování jedné organizace](creating-web-projects-in-visual-studio/_static/image24.png)

Tuto možnost vyberte, pokud chcete povolit ověřování u uživatelských účtů, které jsou definované v jednom [tenantovi](https://technet.microsoft.com/library/jj573650.aspx)služby Azure AD. Například lokalita je contoso.com a bude zpřístupněna zaměstnancům společnosti Contoso, kteří jsou v tenantovi contoso.onmicrosoft.com. Nebudete moct nakonfigurovat službu Azure AD, aby uživatelům z jiných tenantů povolil přístup k aplikaci.

#### <a name="domain"></a>Doména

Zadejte doménu služby Azure AD, ve které chcete nastavit aplikaci, například: `contoso.onmicrosoft.com`. Pokud máte [vlastní doménu](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/), například `contoso.com` místo `contoso.onmicrosoft.com`, můžete sem zadat.

#### <a name="access-level"></a>Úroveň přístupu

Pokud aplikace potřebuje dotazovat nebo aktualizovat informace v adresáři pomocí Graph API, vyberte možnost **jednotné přihlašování, čtení dat adresáře** nebo **jednotné přihlašování, čtení a zápis dat adresáře**. V opačném případě vyberte **jednotné přihlašování**. Další informace najdete v tématu [úrovně přístupu k aplikacím](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels) a [použití Graph API k dotazování služby Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx).

#### <a name="application-id-uri"></a>Identifikátor URI ID aplikace

Ve výchozím nastavení šablona vytvoří identifikátor URI ID aplikace za vás připojením názvu projektu k doméně služby Azure AD. Například pokud je název projektu `Example` a doména je `contoso.onmicrosoft.com`, identifikátor URI ID aplikace se bude `https://contoso.onmicrosoft.com/Example`. Pokud chcete identifikátor URI ID aplikace zadat ručně, rozbalte část **Další možnosti** a zadejte identifikátor URI ID aplikace do textového pole. Identifikátor URI ID aplikace musí začínat `https://`.

Ve výchozím nastavení platí, že pokud aplikace, která je již zřízená ve službě Azure AD, má stejný identifikátor URI ID aplikace jako ten, který aplikace Visual Studio používá pro projekt, projekt bude připojen k existující aplikaci místo zřízení nového. Pokud chcete v takovém případě zřídit novou aplikaci, zrušte zaškrtnutí políčka **Přepsat položku aplikace, pokud už jedna se STEJNÝM ID existuje** .

Pokud není zaškrtnuté políčko **přepsat** , a Visual Studio najde existující aplikaci se stejným identifikátorem URI ID aplikace, vytvoří nový identifikátor URI připojením čísla k identifikátoru URI, který se bude používat. Předpokládejme například, že název projektu je `Example`, necháte textové pole prázdné, zrušíte zaškrtnutí políčka **přepsat** a tenant služby Azure AD již obsahuje aplikaci s identifikátorem URI `https://contoso.onmicrosoft.com/Example`. V takovém případě bude nová aplikace zřízena s identifikátorem URI ID aplikace, jako `https://contoso.onmicrosoft.com/Example_20130619330903`.

#### <a name="provisioning-the-application-in-azure-ad"></a>Zřizování aplikace v Azure AD

Aby bylo možné zřídit aplikaci ve službě Azure AD nebo připojit projekt k existující aplikaci, aplikace Visual Studio potřebuje přihlašovací údaje globálního správce domény. Po kliknutí na tlačítko **OK** v dialogovém okně **Konfigurace ověřování** se zobrazí výzva k zadání uživatelského jména a hesla globálního správce pro doménu, kterou jste zadali. Později když v dialogovém okně **Nový projekt ASP.NET** kliknete na **vytvořit projekt** , Visual Studio zřídí aplikaci ve službě Azure AD. Všimněte si, že v rámci tohoto procesu Visual Studio vloží hodnoty tajného klíče klienta do souboru Web. config, který po vytvoření vyprší jeden rok.

Informace o tom, jak vytvářet aplikace, které používají ověřování pomocí **cloudu** , najdete v následujících zdrojích informací:

- [Ověřování Azure](../2012/windows-azure-authentication.md)
- [Přidání přihlašování do webové aplikace pomocí Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151790.aspx)
- [Vývoj aplikací ASP.NET s použitím Azure Active Directory](../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)
- [Zabezpečení webového rozhraní API ASP.NET pomocí komponent Azure AD a Microsoft OWIN](https://msdn.microsoft.com/magazine/dn463788.aspx)

Kurzy ještě nejsou aktualizované pro Visual Studio 2013. Některé z těchto kurzů, které přímo provedete, jsou v Visual Studio 2013 automatizované.

<a id="orgauthmulti"></a>
### <a name="cloud---multi-organization-authentication"></a>Cloud – ověřování více organizací

![Ověřování více organizací](creating-web-projects-in-visual-studio/_static/image25.png)

Tuto možnost vyberte, pokud chcete povolit ověřování u uživatelských účtů, které jsou definované ve více [klientech](https://technet.microsoft.com/library/jj573650.aspx)Azure AD. Například lokalita je contoso.com a bude zpřístupněna zaměstnancům společnosti Contoso, kteří jsou v tenantovi contoso.onmicrosoft.com, a zaměstnanci společnosti Fabrikam, kteří jsou v tenantovi fabrikam.onmicrosoft.com.

Nastavení, která zadáte, a krok zřizování aplikací jsou podobné [ověřování jedné organizace](#orgauthsingle).

Informace o tom, jak vytvářet aplikace, které používají ověřování pomocí **cloudu pro více organizací** , najdete v následujících zdrojích informací:

- [Snadná integrace webových aplikací s Azure Active Directory ASP.NET &amp; sady Visual Studio](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx) na blogu týmu Active Directory.
- [Vývoj webových aplikací s více klienty pomocí kurzu Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx) . Tento kurz se ještě neaktualizoval pro Visual Studio 2013. Některé z toho, co je kurz, který vás provede ručně, je automatizovaně v Visual Studio 2013.
- Abyste se [mohli přihlásit, musíte se zaregistrovat pomocí své aplikace ASP.NET pro více organizací](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/). Blog Vittorio Bertocci, který vysvětluje, jak vyřešit běžné problémy, ke kterým dochází při vytváření projektu, který používá ověřování s více organizacemi.

<a id="orgauthonprem"></a>
### <a name="on-premises-organizational-authentication"></a>Místní ověřování organizace

![Místní ověřování organizace](creating-web-projects-in-visual-studio/_static/image26.png)

Tuto možnost vyberte, pokud chcete povolit ověřování u uživatelských účtů, které jsou definované ve službě Active Directory (AD) Windows serveru, a nechcete používat Azure AD. Tuto možnost můžete použít k vytvoření intranetového webu nebo webu na internetu. Pro internetový web použijte službu Active Directory Federation Services (AD FS) (ADFS) k poskytnutí přístupu ke službě AD. Další informace najdete v tématu [použití možnosti místní ověřování organizace (ADFS) s ASP.NET v Visual Studio 2013](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/).

Pro intranetový web můžete jako alternativu zvolit [ověřování systému Windows](#winauth) namísto této možnosti. Pro možnost ověřování systému Windows nemusíte zadávat adresu URL dokumentu metadat. Ověřování systému Windows ale neposkytuje možnost řídit přístup k aplikacím ve službě Active Directory nebo dotazovat se na data adresáře.

#### <a name="on-premises-authority"></a>Místní autorita

Zadejte adresu URL, která odkazuje na dokument metadat. Dokument metadat obsahuje souřadnice autority. Aplikace bude tyto souřadnice používat k řízení toku webového přihlášení.

#### <a name="application-id-uri"></a>Identifikátor URI ID aplikace

Zadejte jedinečný identifikátor URI, který může služba AD použít k identifikaci této aplikace, nebo necháte prázdné, aby ji Visual Studio vytvořila.

<a id="nextsteps"></a>
## <a name="next-steps"></a>Další kroky

Tento dokument obsahuje základní nápovědu pro vytvoření nového webového projektu v ASP.NET v Visual Studio 2013. Další informace o použití sady Visual Studio pro vývoj webu najdete v tématu [https://www.asp.net/visual-studio/](../../index.md).
