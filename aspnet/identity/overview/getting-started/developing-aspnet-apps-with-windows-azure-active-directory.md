---
uid: identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory
title: Vývoj aplikací ASP.NET s využitím Azure Active Directory-ASP.NET 4. x
author: Rick-Anderson
description: Microsoft ASP.NET nástroje pro Azure Active Directory usnadňují ověřování pro webové aplikace hostované v Azure. Můžete použít Azure předběžné...
ms.author: riande
ms.date: 08/14/2014
ms.assetid: 457d7eaf-ee76-4ceb-9082-c7c1721435ad
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory
msc.type: authoredcontent
ms.openlocfilehash: 28425ea8d1312dfc6e14df9677396f2cbcf6f16d
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456722"
---
# <a name="developing-aspnet-apps-with-azure-active-directory"></a>Vývoj aplikací ASP.NET s použitím Azure Active Directory

od [Rick Anderson](https://twitter.com/RickAndMSFT)

Microsoft ASP.NET nástroje pro Azure Active Directory zjednodušují povolení ověřování pro webové aplikace hostované v [Azure](https://www.windowsazure.com/home/features/web-sites/). Ověřování Azure můžete použít k ověření uživatelů Office 365 z vaší organizace a firemních účtů synchronizovaných z místní služby Active Directory nebo uživatelů vytvořených ve vlastní Azure Active Directory doméně. Povolení ověřování Windows Azure nakonfiguruje vaši aplikaci tak, aby ověřovala uživatele pomocí jednoho [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) tenanta.

V tomto kurzu se dozvíte, jak vytvořit aplikaci ASP.NET, která je nakonfigurovaná pro přihlašování pomocí [Azure Active Directory](https://msdn.microsoft.com/library/azure/mt168838.aspx) (Azure AD). Naučíte se také, jak volat Graph API a získat informace o aktuálně přihlášeném uživateli a o tom, jak aplikaci nasadit do Azure.

## <a name="prerequisites"></a>Požadavky

1. [Visual Studio Express 2013 pro web](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express) nebo [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).
2. Je třeba zadat [Visual Studio 2013 Update 4](https://www.microsoft.com/download/details.aspx?id=44921) – Update 3 nebo vyšší.
3. Účet Azure. Pokud ještě nemáte účet, [klikněte sem](https://azure.microsoft.com/pricing/free-trial/) pro bezplatnou zkušební verzi.

## <a name="add-a-global-administrator-to-your-active-directory"></a>Přidání globálního správce do Active Directory

1. Přihlaste se k [Azure portál pro správu](https://manage.windowsazure.com/).
2. Všechny účty Azure obsahují **výchozí adresář** – klikněte na něj a potom klikněte na kartu **Uživatelé** v horní části stránky (viz obrázek níže).
3. Klikněte na Přidat uživatele.
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image1.png)
4. Vytvořte nového uživatele s rolí **globálního správce** . V horní nabídce klikněte na **Uživatelé** a potom na panelu příkazů klikněte na tlačítko **Přidat uživatele** .
5. V dialogovém okně **Přidat uživatele** zadejte jméno nového uživatele a klikněte na šipku vpravo.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image2.png)
6. Zadejte uživatelské jméno a nastavte roli na **globální správce**. Globální správci vyžadují alternativní e-mailovou adresu pro účely obnovení hesla. Až budete hotovi, klikněte na šipku doprava.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image3.png)
7. Na další stránce dialogového okna klikněte na **vytvořit**. Pro nového uživatele se vytvoří dočasné heslo, které se zobrazí v dialogovém okně.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image4.png)

   Uložte heslo. po prvním přihlášení budete muset změnit heslo. Následující obrázek ukazuje nový účet správce. K přihlášení do aplikace je nutné použít Azure Active Directory, nikoli účet Microsoft na této stránce.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image5.png)

## <a name="create-an-aspnet-application"></a>Vytvoření aplikace v ASP.NET

Následující kroky používají [Visual Studio Express 2013 pro web](https://www.microsoft.com/download/details.aspx?id=40747)a vyžadují [Visual Studio 2013 Update 3](https://www.microsoft.com/download/details.aspx?id=43721).

1. V aplikaci Visual Studio klikněte na **soubor** a pak na **Nový projekt**. V dialogovém okně **Nový projekt** vyberte v nabídce vlevo C# možnost vizuální webový projekt a klikněte na tlačítko **OK**. Pokud nechcete, aby aplikace byla pro aplikaci k disApplication Insights, můžete také zrušit kontrolu **přidání do projektu** .
2. V dialogovém okně **Nový projekt ASP.NET** vyberte **MVC**a pak klikněte na **změnit ověřování**.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image6.png)
3. V dialogu **změnit ověřování** vyberte **účty organizace**. Tyto možnosti se dají použít k automatické registraci aplikace v Azure AD a také k automatické konfiguraci vaší aplikace pro integraci se službou Azure AD. K registraci a konfiguraci aplikace nemusíte používat dialogové okno **změnit ověřování** , ale to je mnohem jednodušší. Pokud používáte Visual Studio 2012, můžete přesto aplikaci zaregistrovat do Azure Portál pro správu a aktualizovat její konfiguraci pro integraci se službou Azure AD.
   V rozevíracích nabídkách vyberte **cloudová** a **jednotné přihlašování a pak čtěte data adresáře**. Zadejte doménu pro adresář služby Azure AD (například na obrázcích níže) *aricka0yahoo.onmicrosoft.com*a pak klikněte na **OK**. Název domény můžete získat z karty domény pro výchozí adresář na webu Azure Portal (viz další obrázek níže).

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image7.png)

   Následující obrázek ukazuje název domény z Azure Portal.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image8.png)

    > [!NOTE]
    > Volitelně můžete nakonfigurovat identifikátor URI ID aplikace, který se zaregistruje ve službě Azure AD, kliknutím na **Další možnosti**. Identifikátor URI ID aplikace je jedinečný identifikátor pro aplikaci, která je zaregistrovaná v Azure AD a používaná aplikací k identifikaci sebe sama při komunikaci se službou Azure AD. Další informace o identifikátoru URI ID aplikace a dalších vlastnostech registrovaných aplikací najdete v [tomto tématu](https://msdn.microsoft.com/library/azure/dn499820.aspx#BKMK_Registering). Kliknutím na zaškrtávací políčko pod polem identifikátor URI ID aplikace můžete také přepsat existující registraci v Azure AD, která používá stejný identifikátor URI ID aplikace.
4. Po kliknutí na tlačítko **OK**se zobrazí dialogové okno pro přihlášení a bude nutné se přihlásit pomocí účtu globálního správce (nikoli účet Microsoft přidruženého k vašemu předplatnému). Pokud jste dříve vytvořili nový účet správce, budete muset změnit heslo a znovu se přihlásit pomocí nového hesla.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image9.png)
5. Po úspěšném ověření se v dialogovém okně **Nový projekt ASP.NET** zobrazí volba pro ověřování (**organizace** ) a adresář, do kterého se nová aplikace zaregistruje (*aricka0yahoo.onmicrosoft.com* na obrázku níže). Pod těmito informacemi vyberte zaškrtávací políčko s označením **hostitel v cloudu**. Pokud je toto políčko zaškrtnuté, projekt se zřídí jako webová aplikace Azure a bude povolený pro snadné publikování později. Klikněte na tlačítko **OK**.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image10.png)
6. Zobrazí se dialogové okno **Konfigurovat web Azure** s použitím automaticky generovaného názvu a oblasti webu. Všimněte si také, že účet, ke kterému jste právě přihlášení, v dialogovém okně. Chcete se ujistit, že tento účet je ten, ke kterému je vaše předplatné Azure připojené, obvykle účet Microsoft.

    > [!NOTE]
    > Tento projekt vyžaduje databázi. Musíte vybrat jednu ze stávajících databází nebo vytvořit novou. Databáze je povinná, protože projekt už používá místní databázový soubor k uložení malého množství konfiguračních dat ověřování. Když nasadíte aplikaci na web Azure, tato databáze se do nasazení nebalí, takže musíte vybrat takovou přístupnou v cloudu. Klikněte na tlačítko **OK**.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image11.png)
7. Projekt se vytvoří a možnosti ověřování a možnosti webové aplikace se automaticky nakonfigurují s projektem. Po dokončení tohoto procesu spusťte projekt místně stisknutím **^ F5**. Budete se muset přihlásit pomocí účtu organizace. Zadejte uživatelské jméno a heslo pro účet, který jste vytvořili dříve, a klikněte na tlačítko **Přihlásit**.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image12.png)
8. Po úspěšném přihlášení se na webu ASP.NET zobrazí, že jste ověřili zobrazením uživatelského jména v pravém horním rohu stránky.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image13.png)

   Pokud se zobrazí chyba: hodnota nemůže být null nebo prázdná. Název parametru: linkText ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image14.png)

   Viz část [ladění](#dbg) na konci tohoto kurzu.

## <a name="basics-of-the-graph-api"></a>Základy Graph API

[Graph API](https://msdn.microsoft.com/library/azure/hh974476.aspx) je programové rozhraní používané k provádění CRUD a dalších operací s objekty v adresáři služby Azure AD. Pokud vyberete možnost účtu organizace pro ověřování při vytváření nového projektu v Visual Studio 2013, bude aplikace již nakonfigurována pro volání Graph API. V této části se stručně ukáže, jak Graph API funguje.

1. V běžící aplikaci klikněte na jméno přihlášeného uživatele v pravém horním rohu stránky. Tím přejdete na stránku profil uživatele, což je akce na domovském řadiči. Všimněte si, že tabulka obsahuje uživatelské informace o účtu správce, který jste vytvořili dříve. Tyto informace jsou uloženy ve vašem adresáři a je volána Graph API, aby byly tyto informace načteny při načtení stránky.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image15.png)
2. Vraťte se do sady Visual Studio a rozbalte složku **řadiče** a otevřete soubor **HomeController.cs** . Zobrazí se akce **USERPROFILE ()** , která obsahuje kód pro načtení tokenu, a volání Graph API. Tento kód je duplikován níže:

    [!code-csharp[Main](developing-aspnet-apps-with-windows-azure-active-directory/samples/sample1.cs?highlight=22)]

    Chcete-li volat Graph API, je nejprve nutné načíst token. Po načtení tokenu musí být jeho řetězcová hodnota připojena do autorizační hlavičky pro všechny následné požadavky na Graph API. Většina výše uvedeného kódu zpracovává podrobnosti ověřování ve službě Azure AD, aby získal token, pomocí tokenu k volání Graph API a pak transformuje odpověď, aby mohla být prezentována v zobrazení.

    Nejrelevantnější část pro diskuzi je následující zvýrazněný řádek: `UserProfile profile = JsonConvert.DeserializeObject<UserProfile>(responseString);`. Tento řádek představuje jméno uživatele, které bylo deserializováno z odpovědi JSON a je prezentováno v zobrazení.

    Graph API můžete volat pomocí HttpClient a zpracovávat nezpracovaná data sami, ale jednodušším způsobem je použití [klientské knihovny grafů, která je k dispozici prostřednictvím NuGet](http://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient/). Klientská knihovna zpracovává nezpracované požadavky HTTP a transformaci vrácených dat za vás a výrazně usnadňuje práci s Graph API v prostředí .NET. Podívejte se na související ukázky Graph API kódu na [GitHubu.](https://github.com/AzureADSamples)

## <a name="deploy-the-application-to-azure"></a>Nasazení aplikace do Azure

Následující postup vám ukáže, jak nasadit aplikaci do Azure. V předchozích krocích jste připojili nový projekt pomocí webové aplikace v Azure, takže je připravený k publikování v několika krocích.

1. V aplikaci Visual Studio klikněte pravým tlačítkem na projekt a vyberte **publikovat**. Dialog **Publikovat web** se zobrazí se všemi nastaveními, která jsou už nakonfigurovaná. Kliknutím na tlačítko **Další** přejdete na stránku **Nastavení** . Může se zobrazit výzva k ověření. Ujistěte se, že se ověřujete pomocí účtu předplatného Azure (obvykle účet Microsoft), nikoli účtu organizace, který jste vytvořili dříve.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image16.png)
2. Zaškrtněte možnost **Povolit ověřování organizace** . Do pole **doména** zadejte doménu pro svůj adresář. V rozevíracím seznamu **úroveň přístupu** vyberte **jednotné přihlašování, číst data adresáře**. Všimněte si, že předchozí databáze, kterou jste použili, je již vyplněna v části **databáze** . Klikněte na **Publikovat**.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image17.png)
3. Visual Studio začne nasazovat web a zobrazí se nové okno prohlížeče. Může se zobrazit výzva k opětovnému ověření adresáře. Po ověření budete přesměrováni na nově publikovaný web v Azure.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image18.png)

<a id="dbg"></a>
## <a name="debugging-the-app"></a>Ladění aplikace

Pokud se zobrazí následující chyba: hodnota nemůže být null nebo prázdná. Název parametru: linkText

![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image19.png)

Nahraďte kód v souboru *Views\Shared\\_LoginPartial. cshtml* následujícím způsobem:

[!code-cshtml[Main](developing-aspnet-apps-with-windows-azure-active-directory/samples/sample2.cshtml?highlight=1-8,15-16)]

Pokud se přihlášený uživatel po spuštění aplikace zobrazí jako "null uživatel", odhlaste se a znovu se přihlaste pomocí účtu služby Active Directory, který jste vytvořili dříve.

Skvělým kurzem, který je potřeba provést, je Rick Rainey [podrobně: Azure websites a organizace ověřování pomocí Azure AD](http://rickrainey.com/2014/08/19/deep-dive-azure-websites-and-organizational-authentication-using-azure-ad/).

## <a name="more-information"></a>Další informace

- [Hluboká podrobně: Azure websites a ověřování organizace pomocí Azure AD](http://rickrainey.com/2014/08/19/deep-dive-azure-websites-and-organizational-authentication-using-azure-ad/)
- [Přehled služby Azure AD Graph API](https://msdn.microsoft.com/library/azure/hh974476.aspx)
- [Scénáře ověřování ve službě Azure AD](https://msdn.microsoft.com/library/azure/dn499820.aspx)
- [Ukázky kódu Azure AD na GitHubu](https://github.com/AzureADSamples)
