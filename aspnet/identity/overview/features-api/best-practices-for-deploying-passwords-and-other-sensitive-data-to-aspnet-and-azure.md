---
uid: identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
title: Nasazení hesel a dalších citlivých dat do ASP.NET a Azure App Service-ASP.NET 4. x
author: Rick-Anderson
description: V tomto kurzu se dozvíte, jak může váš kód bezpečně ukládat a přistupovat k zabezpečeným informacím. Nejdůležitějším bodem je, že nikdy nebudete ukládat hesla ani jiné...
ms.author: riande
ms.date: 05/21/2015
ms.assetid: 97902c66-cb61-4d11-be52-73f962f2db0a
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
msc.type: authoredcontent
ms.openlocfilehash: 8356a90611f791779cc4ff4730038d82cd76242f
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457047"
---
# <a name="best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure-app-service"></a>Doporučené postupy nasazení hesel a dalších citlivých dat do ASP.NET a služby Azure App Service

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> V tomto kurzu se dozvíte, jak může váš kód bezpečně ukládat a přistupovat k zabezpečeným informacím. Nejdůležitějším bodem je, že byste nikdy neměli ukládat hesla ani další citlivá data ve zdrojovém kódu a neměli byste používat provozní tajemství v režimu vývoje a testování.
> 
> Vzorový kód je jednoduchá Konzolová aplikace WebJob a aplikace ASP.NET MVC, které potřebují přístup k heslům připojovacího řetězce databáze, Twilio, Google a SendGrid Secure Keys.
> 
> Na místních nastaveních se také zmiňuje i PHP.

- [Práce s hesly ve vývojovém prostředí](#pwd)
- [Práce s připojovacími řetězci ve vývojovém prostředí](#con)
- [Konzolové aplikace WebJobs](#wj)
- [Nasazení tajných klíčů do Azure](#da)
- [Poznámky pro místní a PHP](#not)
- [Další zdroje](#addRes)

<a id="pwd"></a>
## <a name="working-with-passwords-in-the-development-environment"></a>Práce s hesly ve vývojovém prostředí

Kurzy často znázorňují citlivá data ve zdrojovém kódu a snad s upozorněním, že byste nikdy neměli ukládat citlivá data ve zdrojovém kódu. Například moje [aplikace ASP.NET MVC 5 s kurzem SMS a e-mailem 2FA](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md) zobrazuje v souboru *Web. config* následující:

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample1.xml)]

Soubor *Web. config* je zdrojový kód, takže tyto tajné klíče by nikdy neměly být uloženy v tomto souboru. Naštěstí `<appSettings>` element má atribut `file`, který umožňuje určit externí soubor, který obsahuje nastavení konfigurace citlivých aplikací. Všechna vaše tajná klíčová okna můžete přesunout do externího souboru, pokud se externí soubor nevrátí do zdrojového stromu. Například v následujícím kódu soubor *AppSettingsSecrets. config* obsahuje všechny tajné klíče aplikace:

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample2.xml)]

Označení v externím souboru (*AppSettingsSecrets. config* v této ukázce) je stejný kód, který se nachází v souboru *Web. config* :

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample3.xml)]

Modul runtime ASP.NET sloučí obsah externího souboru s označením ve &lt;appSettings&gt; elementu. Pokud zadaný soubor nelze nalézt, modul runtime atribut souboru ignoruje.

> [!WARNING]
> Zabezpečení – nepřidejte svůj soubor *tajných klíčů. config* do projektu nebo jej vraťte do správy zdrojového kódu. Ve výchozím nastavení sada Visual Studio nastaví `Build Action` na `Content`, což znamená, že soubor je nasazený. Další informace najdete v tématu [Proč se nepovedlo nasadit všechny soubory ve složce projektu?](https://msdn.microsoft.com/library/ee942158(v=vs.110).aspx#can_i_exclude_specific_files_or_folders_from_deployment) I když můžete použít jakékoli rozšíření souboru *tajných kódů. config* , je vhodné uchovávat soubor *. config*, protože konfigurační soubory nejsou obsluhovány službou IIS. Všimněte si také, že soubor *AppSettingsSecrets. config* je ze souboru *Web. config* ze dvou adresářových úrovní, takže je zcela z adresáře řešení. Přesunutím souboru z adresáře řešení &quot;git add \*&quot; ho do úložiště přidat.

<a id="con"></a>
## <a name="working-with-connection-strings-in-the-development-environment"></a>Práce s připojovacími řetězci ve vývojovém prostředí

Visual Studio vytvoří nové projekty ASP.NET, které používají [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx). LocalDB byl vytvořen speciálně pro vývojové prostředí. Nevyžaduje heslo, takže nemusíte nic dělat, abyste zabránili tomu, aby se tajné kódy kontrolovaly do zdrojového kódu. Některé vývojové týmy používají plné verze SQL Server (nebo jiného systému DBMS), které vyžadují heslo.

Atribut `configSource` lze použít k nahrazení celého kódu `<connectionStrings>`. Na rozdíl od atributu `<appSettings>` `file`, který sloučí značku, atribut `configSource` nahradí značku. Následující kód ukazuje atribut `configSource` v souboru *Web. config* :

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample4.xml?highlight=1)]

> [!NOTE]
> Použijete-li atribut `configSource`, jak je uvedeno výše, přesunete připojovací řetězce do externího souboru a ponecháte si aplikaci Visual Studio vytvořit nový web, nebudete schopni zjistit, že používáte databázi, a při publikování do Azure ze sady Visual Studio nezískáme možnost konfigurace databáze. Pokud používáte atribut `configSource`, můžete použít PowerShell k vytvoření a nasazení vašeho webu a databáze, nebo můžete vytvořit web a databázi na portálu před publikováním. Skript [New-AzureWebsitewithDB. ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) vytvoří nový web a databázi.

> [!WARNING]
> Zabezpečení – na rozdíl od souboru *AppSettingsSecrets. config* musí být soubor externích připojovacích řetězců ve stejném adresáři jako kořenový soubor *Web. config* , takže budete muset vzít v úvahu bezpečnostní opatření, abyste se ujistili, že je nebudete kontrolovat do zdrojového úložiště.

> [!NOTE]
> **Upozornění zabezpečení v souboru tajných kódů:** Osvědčeným postupem je nepoužívat provozní tajemství v rámci testování a vývoje. Používáním produkčních hesel v testu nebo v jejich vývoji nevrací tyto tajné kódy.

<a id="wj"></a>
## <a name="webjobs-console-apps"></a>Konzolové aplikace WebJobs

Soubor *App. config* používaný konzolovou aplikací nepodporuje relativní cesty, ale podporuje absolutní cesty. K přesunutí tajných kódů z adresáře projektu můžete použít absolutní cestu. Následující kód ukazuje tajné klíče v souboru *C:\secrets\AppSettingsSecrets.config* a data v souboru *App. config* , která nejsou citlivá.

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample5.xml?highlight=2)]

<a id="da"></a>
## <a name="deploying-secrets-to-azure"></a>Nasazení tajných klíčů do Azure

Když nasadíte webovou aplikaci do Azure, soubor *AppSettingsSecrets. config* se nesadí (to je to, co chcete). Můžete přejít na [portál pro správu Azure](https://azure.microsoft.com/services/management-portal/) a nastavit je ručně, abyste to provedli:

1. Přejít na [https://portal.azure.com](https://portal.azure.com)a přihlaste se pomocí přihlašovacích údajů Azure.
2. Klikněte na **procházet &gt; Web Apps**a pak klikněte na název vaší webové aplikace.
3. Klikněte na **všechna nastavení &gt; nastavení aplikace**.

**Nastavení aplikace** a hodnoty **připojovacích řetězců** přepíšou stejné nastavení v souboru *Web. config* . V našem příkladu jsme tato nastavení do Azure nasadili, ale pokud byly tyto klíče v souboru *Web. config* , bude mít přednost nastavení zobrazená na portálu.

Osvědčeným postupem je postupovat podle [pracovního postupu DevOps](../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything.md) a pomocí [Azure PowerShell](https://azure.microsoft.com/documentation/articles/install-configure-powershell/) (nebo jiné [architektury, jako je například](http://www.opscode.com/chef/) tovární nebo [Puppet](http://puppetlabs.com/puppet/what-is-puppet)), automatizovat nastavení těchto hodnot v Azure. Následující skript PowerShellu používá [Export-CLIXML](http://www.powershellcookbook.com/recipe/PukO/securely-store-credentials-on-disk) k exportu šifrovaných tajných klíčů na disk:

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample6.ps1)]

Ve skriptu výše je ' název ' název tajného klíče, například '&quot;Arial\_AppSecret&quot; nebo "TwitterSecret". Soubor. Credential vytvořený skriptem můžete zobrazit v prohlížeči. Fragment kódu níže testuje všechny soubory přihlašovacích údajů a nastavuje tajné klíče pro pojmenovanou webovou aplikaci:

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample7.ps1)]

> [!WARNING]
> Zabezpečení – Nezahrnovat hesla ani jiné tajné klíče do skriptu PowerShellu, takže by se tak přesadil účel použití skriptu PowerShellu k nasazení citlivých dat. Rutina [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) poskytuje zabezpečený mechanismus pro získání hesla. Použití výzvy uživatelského rozhraní může zabránit úniku hesla.

### <a name="deploying-db-connection-strings"></a>Nasazení připojovacích řetězců databáze

Připojovací řetězce databáze jsou zpracovávány podobně jako nastavení aplikace. Pokud nasadíte webovou aplikaci ze sady Visual Studio, připojovací řetězec bude nakonfigurován za vás. To můžete ověřit na portálu. Doporučený způsob, jak nastavit připojovací řetězec, je PowerShell. Příklad skriptu PowerShellu: vytvoří web a databázi a nastaví připojovací řetězec na webu, Stáhněte si [New-AzureWebsitewithDB. ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) z [knihovny skriptů Azure](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure).

<a id="not"></a>
## <a name="notes-for-php"></a>Poznámky pro PHP

Vzhledem k tomu, že páry klíč-hodnota pro obě **nastavení aplikace** i **připojovací řetězce** jsou uloženy v proměnných prostředí v Azure App Service, můžou tyto hodnoty snadno načíst vývojáři, kteří používají libovolné architektury webových aplikací (například php). Viz [webové stránky Windows Azure v Stefan Schackow: jak řetězce aplikace a připojovací řetězce fungují](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) na blogovém příspěvku, který ukazuje fragment php pro čtení nastavení aplikace a připojovacích řetězců.

## <a name="notes-for-on-premises-servers"></a>Poznámky pro místní servery

Pokud nasazujete na místní webové servery, můžete zajistit zabezpečení tajných klíčů [šifrováním konfiguračních oddílů konfiguračních souborů](https://msdn.microsoft.com/library/ff647398.aspx). Jako alternativu můžete použít stejný přístup doporučený pro Azure websites: zachovat nastavení vývoje v konfiguračních souborech a použít hodnoty proměnných prostředí pro nastavení produkčního prostředí. V takovém případě je však nutné napsat kód aplikace pro funkce, které jsou automaticky na webu Azure websites: načíst nastavení z proměnných prostředí a použít tyto hodnoty místo nastavení konfiguračního souboru nebo použít nastavení konfiguračního souboru, když proměnné prostředí se nenašly.

<a id="addRes"></a>
## <a name="additional-resources"></a>Další materiály a zdroje informací

Příklad skriptu PowerShellu, který vytvoří webovou aplikaci a databázi, nastaví připojovací řetězec + nastavení aplikace. Stáhněte si [New-AzureWebsitewithDB. ps1](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) z [knihovny skriptů Azure](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure). 

Viz [webové stránky Windows Azure v Stefan Schackow: jak fungují řetězce aplikace a připojovací řetězce.](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)

Zvláštní díky Barryho Dorrans ( [@blowdart](https://twitter.com/blowdart) ) a Carlos Farre pro kontrolu.
