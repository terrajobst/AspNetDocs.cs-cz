---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
title: Použití ASP.NET MVC s různými verzemi služby IIS (VB) | Microsoft Docs
author: microsoft
description: V tomto kurzu se naučíte používat ASP.NET MVC a směrování adres URL s různými verzemi Internetová informační služba. Naučíte se různé strategie...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 1c1283b2-6956-4937-b568-d30de432ce23
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
msc.type: authoredcontent
ms.openlocfilehash: b754175c853c20eec6be3521376b62d62f33106d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581835"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-vb"></a>Použití ASP.NET MVC s různými verzemi služby IIS (VB)

od [Microsoftu](https://github.com/microsoft)

> V tomto kurzu se naučíte používat ASP.NET MVC a směrování adres URL s různými verzemi Internetová informační služba. Naučíte se různé strategie pro používání ASP.NET MVC se službou IIS 7,0 (klasický režim), IIS 6,0 a staršími verzemi služby IIS.

Rozhraní ASP.NET MVC závisí na směrování ASP.NET pro směrování požadavků prohlížeče na akce kontroleru. Aby bylo možné využívat ASP.NET směrování, možná budete muset provést další kroky konfigurace na webovém serveru. To vše závisí na verzi Internetová informační služba (IIS) a režimu zpracování žádostí pro vaši aplikaci.

Tady je souhrn různých verzí služby IIS:

- Služba IIS 7,0 (integrovaný režim) – není nutná žádná zvláštní konfigurace pro použití směrování ASP.NET.
- IIS 7,0 (klasický režim) – pro použití směrování ASP.NET je potřeba provést speciální konfiguraci.
- Služba IIS 6,0 nebo nižší – pro použití směrování ASP.NET je potřeba provést zvláštní konfiguraci.

Nejnovější verze služby IIS je verze 7,5 (v systému Win7). Služba IIS 7 služby IIS je součástí systémů Windows Server 2008 a VISTA/SP1 a vyšší. Službu IIS 7,0 můžete také nainstalovat na libovolnou verzi operačního systému Vista s výjimkou Home Basic (viz [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)).

Služba IIS 7,0 podporuje dva režimy zpracování požadavků. Můžete použít integrovaný režim nebo klasický režim. Pokud používáte IIS 7,0 v integrovaném režimu, nemusíte provádět žádné zvláštní kroky konfigurace. Při použití IIS 7,0 v klasickém režimu ale potřebujete provést další konfiguraci.

Microsoft Windows Server 2003 obsahuje službu IIS 6,0. Pokud používáte operační systém Windows Server 2003, nemůžete upgradovat službu IIS 6,0 na IIS 7,0. Při použití služby IIS 6,0 je nutné provést další kroky konfigurace.

Microsoft Windows XP Professional zahrnuje IIS 5,1. Při použití služby IIS 5,1 je nutné provést další kroky konfigurace.

Microsoft Windows 2000 a Microsoft Windows 2000 Professional zahrnují službu IIS 5,0. Při použití služby IIS 5,0 je nutné provést další kroky konfigurace.

## <a name="integrated-versus-classic-mode"></a>Integrovaný versus klasický režim

Služba IIS 7,0 může zpracovávat požadavky pomocí dvou různých režimů zpracování požadavků: integrovaných a klasických. Integrovaný režim poskytuje lepší výkon a další funkce. Klasický režim je zahrnutý pro zpětnou kompatibilitu s předchozími verzemi služby IIS.

Režim zpracování žádosti je určen fondem aplikací. Můžete určit, který režim zpracování je používán konkrétní webovou aplikací, určením fondu aplikací, který je přidružen k aplikaci. Postupujte následovně:

1. Spustit Správce Internetová informační služba
2. V okně připojení vyberte aplikaci.
3. V okně akce kliknutím na odkaz **základní nastavení** otevřete dialogové okno Upravit aplikaci (viz obrázek 1).
4. Poznamenejte si vybraný fond aplikací.

Ve výchozím nastavení je služba IIS nakonfigurovaná tak, aby podporovala dva fondy aplikací: **DefaultAppPool** a **Classic .NET AppPool**. Pokud je vybraná možnost DefaultAppPool, aplikace běží v režimu integrovaného zpracování požadavků. Pokud je vybrána možnost klasický fond aplikací .NET, aplikace běží v režimu klasických zpracování požadavků.

[![dialogového okna Nový projekt](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)

**Obrázek 1**: zjištění režimu zpracování požadavků ([kliknutím zobrazíte obrázek v plné velikosti](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png))

Všimněte si, že můžete změnit režim zpracování požadavků v dialogovém okně Upravit aplikaci. Klikněte na tlačítko vybrat a změňte fond aplikací přidružený k aplikaci. Mějte na paměti, že při změně aplikace ASP.NET z klasického režimu na integrovaný režim dochází k problémům s kompatibilitou. Další informace najdete v následujících článcích:

- Upgrade ASP.NET 1,1 na IIS 7,0 v systému Windows Vista a Windows Server 2008-- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)

- Integrace ASP.NET se službou IIS 7,0 – [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)

Pokud aplikace ASP.NET používá službu DefaultAppPool, nemusíte provádět žádné další kroky, abyste mohli získat ASP.NET směrování (a tedy ASP.NET MVC), aby fungovala. Pokud je ale aplikace ASP.NET nakonfigurovaná tak, aby používala klasický fond rozhraní .NET .NET, pak budete moct dál číst.

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a>Použití ASP.NET MVC se staršími verzemi služby IIS

Pokud potřebujete použít službu ASP.NET MVC se starší verzí služby IIS, než je IIS 7,0, nebo potřebujete použít IIS 7,0 v klasickém režimu, máte dvě možnosti. Nejprve můžete upravit směrovací tabulku tak, aby používala přípony souborů. Například místo vyžádání adresy URL jako/Store/Details byste si vyžádali adresu URL, jako je/Store.aspx/Details.

Druhou možností je vytvořit něco označovaného jako *Mapa skriptu se zástupnými znaky*. Mapa skriptu se zástupnými znaky umožňuje mapovat všechny požadavky do ASP.NET Frameworku.

Pokud nemáte přístup k webovému serveru (například vaše aplikace ASP.NET MVC je hostována poskytovatelem internetových služeb), budete muset použít první možnost. Pokud nechcete měnit vzhled adres URL a máte přístup k vašemu webovému serveru, můžete použít druhou možnost.

Podrobněji prozkoumáme jednotlivé možnosti v následujících oddílech.

## <a name="adding-extensions-to-the-route-table"></a>Přidání rozšíření do směrovací tabulky

Nejjednodušší způsob, jak získat směrování ASP.NET pro práci se staršími verzemi služby IIS, je upravit tabulku směrování v souboru Global. asax. Výchozí a neupravený soubor Global. asax v seznamu 1 nakonfiguruje jednu trasu s názvem výchozí trasa.

**Výpis 1-Global. asax (nezměněno)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample1.vb)]

Výchozí trasa nakonfigurovaná v seznamu 1 vám umožní směrovat adresy URL, které vypadají takto:

/Home/Index

/Product/Details/3

/Product

Starší verze služby IIS bohužel tyto požadavky nepředá rozhraní ASP.NET Framework. Proto se tyto požadavky nebudou směrovat do kontroleru. Pokud například vytvoříte požadavek prohlížeče na adresu URL/Home/Index, zobrazí se chybová stránka na obrázku 2.

[![dialogového okna Nový projekt](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)

**Obrázek 2**: příjem Chyby nenalezení 404 ([kliknutím zobrazíte obrázek v plné velikosti](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png))

Starší verze služby IIS mapují pouze některé požadavky na ASP.NET Framework. Požadavek musí být adresa URL se správnou příponou souboru. Například požadavek na/SomePage.aspx se mapuje na rozhraní ASP.NET. Nicméně požadavek na/SomePage.htm není.

Proto je potřeba upravit výchozí trasu tak, aby se ASP.NET směrování, aby obsahovalo příponu souboru, která je namapovaná na ASP.NET Framework.

To se provádí pomocí skriptu s názvem `registermvc.wsf`. Byla součástí verze ASP.NET MVC 1 v `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`, ale od ASP.NET 2 se tento skript přesunul do ASP.NET futures, který je k dispozici na adrese [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978).

Spuštění tohoto skriptu zaregistruje nové rozšíření. Mvc se službou IIS. Po registraci rozšíření. Mvc můžete v souboru Global. asax změnit trasy tak, aby trasy používaly rozšíření. Mvc.

Upravený soubor Global. asax v seznamu 2 funguje se staršími verzemi služby IIS.

**Výpis 2 – Global. asax (upraveno s rozšířeními)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample2.vb)]

Důležité: nezapomeňte znovu sestavit aplikaci ASP.NET MVC po změně souboru Global. asax.

Existují dvě důležité změny v souboru Global. asax v seznamu 2. V Global. asax jsou nyní definovány dvě trasy. Vzor adresy URL výchozí trasy, první trasy, teď vypadá takto:

{Controller}. Mvc/{Action}/{ID}

Přidání rozšíření. Mvc změní typ souborů, které modul směrování ASP.NET zachycuje. V této změně aplikace ASP.NET MVC nyní směruje požadavky jako následující:

/Home.mvc/Index/

/Product.mvc/Details/3

/Product.mvc/

Druhá trasa, kořenová trasa, je nová. Tento vzor adresy URL pro kořenovou trasu je prázdný řetězec. Tato trasa je nezbytná pro porovnání požadavků provedených vůči kořenovému adresáři vaší aplikace. Například kořenová trasa bude odpovídat žádosti, která vypadá takto:

[http://www.YourApplication.com/](http://www.YourApplication.com/)

Po provedení těchto úprav v tabulce směrování budete muset zajistit, aby všechny odkazy v aplikaci byly kompatibilní s těmito novými vzory adres URL. Jinými slovy, zajistěte, aby všechny vaše odkazy zahrnovaly příponu. Mvc. Použijete-li k vygenerování odkazů pomocnou metodu HTML. ActionLink (), neměli byste provádět žádné změny.

Namísto použití skriptu registermvc. WCF můžete přidat nové rozšíření služby IIS, které je namapováno na ASP.NET Framework ručně. Když přidáváte nové rozšíření sami, ujistěte se, že políčko **ověřit, že soubor existuje** , není zaškrtnuté.

## <a name="hosted-server"></a>Hostovaný Server

Nemáte vždycky přístup k vašemu webovému serveru. Pokud například hostete aplikaci MVC ASP.NET pomocí poskytovatele internetového hostování, pak nebudete nutně mít přístup ke službě IIS.

V takovém případě byste měli použít jednu z existujících přípon souborů, které jsou namapovány na ASP.NET Framework. Mezi přípony souborů namapované na ASP.NET patří například rozšíření. aspx,. axd a. ashx.

Například upravený soubor Global. asax v seznamu 3 používá příponu. aspx místo rozšíření. Mvc.

**Výpis 3 – Global. asax (upraveno s příponami. aspx)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample3.vb)]

Soubor Global. asax v seznamu 3 je přesně stejný jako předchozí soubor Global. asax s výjimkou toho, že používá příponu. aspx místo rozšíření. Mvc. Není nutné provádět žádné nastavení na vzdáleném webovém serveru, aby bylo možné použít příponu. aspx.

## <a name="creating-a-wildcard-script-map"></a>Vytvoření mapy skriptů se zástupnými znaky

Pokud nechcete měnit adresy URL pro aplikaci ASP.NET MVC a máte přístup k vašemu webovému serveru, máte další možnost. Můžete vytvořit mapu skriptů se zástupnými znaky, která mapuje všechny požadavky na webový server do ASP.NET architektury. Tímto způsobem můžete použít výchozí směrovací tabulku ASP.NET MVC se službou IIS 7,0 (v klasickém režimu) nebo IIS 6,0.

Uvědomte si, že tato možnost způsobí, že služba IIS zachycuje všechny požadavky vytvořené na webovém serveru. To zahrnuje požadavky na image, klasické stránky ASP a HTML stránky. Proto povolení mapy skriptů se zástupnými znaky pro ASP.NET má vliv na výkon.

Tady je postup, jak povolit mapu skriptů se zástupnými znaky pro IIS 7,0:

1. Výběr aplikace v okně připojení
2. Ujistěte se, že je vybraná možnost zobrazení **funkcí** .
3. Dvakrát klikněte na tlačítko **mapování obslužných rutin** .
4. Klikněte na odkaz **Přidat mapu skriptů se zástupnými znaky** (viz obrázek 3).
5. Zadejte cestu k souboru ASPNET\_ISAPI. dll (tuto cestu můžete zkopírovat z mapy skriptů PageHandlerFactory).
6. Zadejte název MVC.
7. Klikněte na tlačítko **OK** .

[![dialogového okna Nový projekt](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)

**Obrázek 3**: vytvoření mapy skriptů se zástupnými znaky pomocí IIS 7,0 ([kliknutím zobrazíte obrázek v plné velikosti](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png))

Pomocí těchto kroků vytvořte mapu skriptů se zástupnými znaky se službou IIS 6,0:

1. Klikněte pravým tlačítkem na web a vyberte vlastnosti.
2. Výběr karty **domovského adresáře**
3. Klikněte na tlačítko **Konfigurace** .
4. Výběr karty **mapování**
5. Klikněte na tlačítko **Vložit** (viz obrázek 4).
6. Vložte cestu k souboru ASPNET\_ISAPI. dll do spustitelného pole (tuto cestu můžete zkopírovat z mapy skriptu pro soubory. aspx).
7. Zrušte zaškrtnutí políčka s označením **ověřit, zda soubor existuje** .
8. Klikněte na tlačítko **OK** .

[![dialogového okna Nový projekt](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)

**Obrázek 4**: vytvoření mapy skriptů se zástupnými znaky pomocí služby IIS 6,0 ([kliknutím zobrazíte obrázek v plné velikosti](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png))

Po povolení mapování skriptů se zástupnými znaky je nutné upravit směrovací tabulku v souboru Global. asax tak, aby zahrnovala kořenovou trasu. V opačném případě se zobrazí chybová stránka na obrázku 5 při vytváření žádosti o kořenovou stránku aplikace. V seznamu 4 můžete použít upravený soubor Global. asax.

[![dialogového okna Nový projekt](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)

**Obrázek 5**: chybějící chyba kořenové trasy ([kliknutím zobrazíte obrázek v plné velikosti](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png))

**Výpis 4 – Global. asax (upraveno s kořenovou trasou)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample4.vb)]

Po povolení mapování skriptů se zástupnými znaky pro IIS 7,0 nebo IIS 6,0 můžete vytvořit žádosti, které budou fungovat s výchozí směrovací tabulkou, která bude vypadat takto:

/

/Home/Index

/Product/Details/3

/Product

## <a name="summary"></a>Souhrn

Cílem tohoto kurzu je vysvětlit, jak můžete použít ASP.NET MVC při použití starší verze služby IIS (nebo IIS 7,0 v klasickém režimu). Provedli jsme dvě metody získání ASP.NET směrování pro práci se staršími verzemi služby IIS: Upravte výchozí směrovací tabulku nebo vytvořte mapu skriptů se zástupnými znaky.

První možnost vyžaduje, abyste upravili adresy URL používané ve vaší aplikaci ASP.NET MVC. Jednou z výhod této první možnosti je, že nepotřebujete přístup k webovému serveru, abyste mohli upravit směrovací tabulku. To znamená, že můžete použít tuto první možnost i při hostování aplikace ASP.NET MVC s internetovou hostingovou společností.

Druhou možností je vytvořit mapu skriptů se zástupnými znaky. Výhodou této druhé možnosti je, že nemusíte měnit adresy URL. Nevýhodou této druhé možnosti je, že může ovlivnit výkon aplikace ASP.NET MVC.

> [!div class="step-by-step"]
> [Předchozí](using-asp-net-mvc-with-different-versions-of-iis-cs.md)
