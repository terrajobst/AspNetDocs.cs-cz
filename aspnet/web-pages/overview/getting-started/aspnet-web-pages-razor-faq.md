---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: Nejčastější dotazy k webovým stránkám ASP.NET (Razor) | Microsoft Docs
author: Rick-Anderson
description: V tomto článku jsou uvedené některé nejčastější dotazy týkající se webových stránek ASP.NET (Razor) a WebMatrix. Verze softwaru používané v kurzu ASP.NET webové stránky (R...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: 6fa1b668e915af856a693e79eafb7180ed504dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640929"
---
# <a name="aspnet-web-pages-razor-faq"></a>Webové stránky ASP.NET (Razor) – časté otázky

tím, že [FitzMacken](https://github.com/tfitzmac)

> > [!NOTE] 
> > WebMatrix se už nedoporučuje jako integrované vývojové prostředí pro webové stránky ASP.NET. Použijte [Visual Studio](xref:aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) nebo [Visual Studio Code](https://code.visualstudio.com/).
>
> V tomto článku jsou uvedené některé nejčastější dotazy týkající se webových stránek ASP.NET (Razor) a WebMatrix.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>   
> 
> Tento kurz funguje také s ASP.NET webovými stránkami 2, WebMatrix 2 a Visual Studio 2012.

- [Jaký je rozdíl mezi ASP.NET webovými stránkami, webovými formuláři ASP.NET a ASP.NET MVC?](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [Potřebuji pro práci s webovými stránkami WebMatrix?](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [Můžu na stránce webových stránek použít ovládací prvky webových formulářů ASP.NET?](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [Můžu nasadit web webových stránek ASP.NET bez použití WebMatrixu?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [Musím pro podporu přihlášení použít pomocníka WebSecurity?](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [Podporuje webové stránky ASP.NET HTML5?](#Does_ASP.NET_Web_Pages_support_HTML5)
- [Můžu použít JavaScript a jQuery s webovými stránkami?](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [Další zdroje](#AdditionalResources)

Dotazy týkající se chyb a dalších problémů najdete v [Průvodci odstraňováním potíží s webovými stránkami ASP.NET (Razor)](https://go.microsoft.com/fwlink/?LinkId=253001).

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a>Jaký je rozdíl mezi ASP.NET webovými stránkami, webovými formuláři ASP.NET a ASP.NET MVC?

Všechny tři jsou ASP.NET technologie pro vytváření dynamických webových aplikací:

- Webové stránky ASP.NET se zaměřují na Přidání dynamického kódu (na straně serveru) a přístupu k databázi na stránky HTML a funkce jednoduché a zjednodušené syntaxe.
- Webové formuláře ASP.NET jsou založené na modelu objektu stránky a tradičních ovládacích prvcích typu okno (tlačítka, seznamy atd.). Webové formuláře využívají model založený na událostech, které jsou známé pro ty, kteří pracovali s vývojem na základě klientů (Windows Forms).
- ASP.NET MVC implementuje vzor pro ASP.NET modelu model-View-Controller. Důraz se týká oddělení potíží (zpracování, data a vrstvy uživatelského rozhraní).

Všechny tři architektury jsou plně podporované a i nadále jsou vyvíjené týmem ASP.NET. Obecně platí, že volba rozhraní, které se použije, závisí na pozadí a zkušenostech s ASP.NET.

Konkrétní webové stránky ASP.NET byly navrženy tak, aby pro uživatele, kteří již znají kód HTML, mohli přidat zpracování serveru na své stránky. Je dobrou volbou pro studenty, nadšence a lidi, kteří jsou obecně noví v programování. Může to být také dobrou volbou pro vývojáře, kteří mají zkušenosti s non-ASP.NET webovými technologiemi.

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a>Potřebuji pro práci s webovými stránkami WebMatrix?

Ne. WebMatrix se už nedoporučuje jako integrované vývojové prostředí pro webové stránky ASP.NET. Použijte [Visual Studio](program-asp-net-web-pages-in-visual-studio.md) nebo [Visual Studio Code](https://code.visualstudio.com/).

Pokud nechcete používat aplikaci Visual Studio ani Visual Studio Code, můžete nainstalovat součásti produktu jednotlivě pomocí [Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx). Potřebujete následující produkty:

- Microsoft .NET Framework 4.5
- ASP.NET MVC 5 (který nainstaluje i rozhraní Web Pages ASP.NET)
- IIS Express (webový server)
- Microsoft SQL Server Compact 4,0 (databáze)

Textový editor lze použít k úpravám stránek *. cshtml* (nebo *. vbhtml*).

Správa databází SQL Server Compact (soubory *. sdf* ) bez nástroje je trochu obtížnější. Nástroje Visual Studio containds pro správu databází *. sdf* . Můžete také spustit příkazy SQL v kódu, abyste mohli provádět mnoho úloh správy SQL Server.

Chcete-li testovat stránky *. cshtml* bez použití integrovaného vývojového prostředí (IDE), můžete je nasadit na živý Server. (Viz [Jak můžu nasadit web webových stránek ASP.NET bez použití WebMatrixu?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix))

### <a name="running-iis-express-without-using-an-ide"></a>Spouštění IIS Express bez použití rozhraní IDE

Pokud nainstalujete IIS Express do počítače jako webový server, můžete je použít k otestování stránek. Můžete spustit IIS Express z příkazového řádku a přidružit ho k určitému číslu portu. Pak tento port určíte, když vyžádáte soubory *. cshtml* v prohlížeči.

V systému Windows otevřete příkazový řádek s oprávněními správce a změňte umístění *C:\Program Files\IIS Express.* (Pro 64 bitové systémy použijte složku *C:\Program Files (x86) \IIS Express.)* Potom zadejte následující příkaz, který použije skutečnou cestu k webu:

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

Můžete použít jakékoli číslo portu, které již není vyhrazeno jiným procesem. (Čísla portů nad 1024 jsou obvykle zadarmo.) Pro hodnotu `path` použijte cestu ke složce webu, kde jsou soubory *. cshtml* .

Po spuštění tohoto příkazu pro nastavení IIS Express pro obsluhu vašich stránek můžete otevřít prohlížeč a přejít k souboru *. cshtml* . Použijte adresu URL podobnou následující:

`http://localhost:35896/default.cshtml`

Nápovědu k IIS Express možností příkazového řádku získáte tak, že do příkazového řádku zadáte `iisexpress.exe /?`.

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a>Můžu na stránce webových stránek použít ovládací prvky webových formulářů ASP.NET?

Ne. Ovládací prvky webových formulářů, jako je ovládací prvek [CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) , [ovládací prvky ověřování](https://msdn.microsoft.com/library/bwd43d0x)a ovládací prvek [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) fungují pouze na stránkách webových formulářů (soubory *. aspx* ). Tyto ovládací prvky vyžadují rozhraní stránky webového formuláře.

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a>Můžu nasadit web webových stránek ASP.NET bez použití WebMatrixu?

Ano. Soubory webů můžete ručně zkopírovat na server (obvykle pomocí FTP). Pokud provádíte ruční kopírování, budete také muset zkopírovat soubory, které podporují SQL Server Compact (databáze). Podrobnosti najdete v blogu [nasazování aplikací webové stránky bez nástroje](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317).

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a>Musím pro podporu přihlášení použít pomocníka WebSecurity?

Ne. Jedním z možností je poskytovatel `SimpleMembership`, který je součástí webových stránek ASP.NET. K dispozici jsou taky poskytovatelé zabezpečení, kteří jsou součástí ASP.NET (které můžete použít k práci ve webových formulářích). Ověřování pomocí formulářů můžete například použít na webových stránkách ASP.NET stejně jako v webových formulářích. Příklad použití ověřování pomocí formulářů naleznete v podpora Microsoftu článku [jak implementovat ověřování založené na formulářích ve vaší aplikaci ASP.NET pomocí C#.NET](https://support.microsoft.com/kb/301240). Pokud si chcete stáhnout jednoduchý příklad, přečtěte si téma [ASP.NET verze "přihlašovací &amp; heslo](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm).

Informace o tom, jak používat ověřování systému Windows, najdete v blogovém příspěvku [s ověřováním systému Windows na webových stránkách ASP.NET](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298).

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a>Podporuje webové stránky ASP.NET HTML5?

Ano. Stránky, které vytvoříte pomocí webových stránek ASP.NET (stránky *. cshtml* nebo *. vbhtml* ), jsou v podstatě stránky HTML, které obsahují také kód, který běží na serveru, před vykreslením stránky. Dokud prohlížeč uživatele podporuje HTML5, můžete použít prvky HTML5 na stránce *. cshtml* nebo *. vbhtml* .

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a>Můžu použít JavaScript a jQuery s webovými stránkami?

Jistě. Stránky, které vytvoříte pomocí webových stránek ASP.NET (stránky *. cshtml* nebo *. vbhtml* ), jsou v nich jenom stránky HTML s kódem serveru. Proto cokoli, co můžete provádět na normální stránce HTML pomocí JavaScriptu nebo jQuery, můžete provést také na stránce *. cshtml* nebo *. vbhtml* .

**Úvodní šablona webu** v WebMatrixu obsahuje řadu knihoven jQuery. Pokud vytvoříte lokalitu pomocí této šablony, složka *skripty* obsahuje knihovnu jQuery Core (*jQuery 1.6.2. js)* a knihovny pro ověření jQuery (*jQuery. Validate. js*atd.).

Tady jsou některé blogové příspěvky, které ilustrují způsoby použití jQuery s ASP.NET webovými stránkami:

- [Přidání dobrých funkcí jQuery k ASP.NET webovým stránkám pomocí WebMatrixu](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) Rachel Appel
- [5 min: WebMatrix + JQUERY UI + JSON + šablony jQuery](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) pomocí Jonas Eriksson
- [Formuláře WebMatrix a jQuery](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms) pomocí Jan slaného

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>Další prostředky

[Webové stránky ASP.NET (Razor) – průvodce řešením potíží](https://go.microsoft.com/fwlink/?LinkId=253001)

[Fórum webových stránek WebMatrix a ASP.NET](https://forums.asp.net/1224.aspx/1?WebMatrix) na webu ASP.NET
