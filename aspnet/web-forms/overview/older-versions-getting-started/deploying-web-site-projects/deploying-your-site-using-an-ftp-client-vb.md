---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-an-ftp-client-vb
title: Nasazení webu pomocí klienta FTP (VB) | Microsoft Docs
author: rick-anderson
description: Nejjednodušší způsob, jak nasadit aplikaci ASP.NET, je ručně zkopírovat potřebné soubory z vývojového prostředí do produkčního prostředí. Thi...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 09279194-bcf9-4b59-a09d-c68e5926a758
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-an-ftp-client-vb
msc.type: authoredcontent
ms.openlocfilehash: 7875304c672625d8c0eaaf0fea8ef509bb801a3a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78545505"
---
# <a name="deploying-your-site-using-an-ftp-client-vb"></a>Nasazení webu pomocí klienta FTP (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_03_VB.zip) nebo [stažení PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial03_DeployingViaFTP_vb.pdf)

> Nejjednodušší způsob, jak nasadit aplikaci ASP.NET, je ručně zkopírovat potřebné soubory z vývojového prostředí do produkčního prostředí. V tomto kurzu se dozvíte, jak pomocí klienta FTP získat soubory z vaší plochy do poskytovatele webového hostitele.

## <a name="introduction"></a>Úvod

V předchozím kurzu jsme zavedli jednoduchou ASP.NET webovou aplikaci, která se skládá z několik stránek ASP.NET, hlavní stránky, vlastní základní třídy `Page`, řady obrázků a tří šablon stylů CSS. Nyní jsme připraveni tuto aplikaci nasadit do poskytovatele webového hostitele. v takovém případě bude aplikace přístupná pro kohokoli s připojením k Internetu.

V našich diskusích o [*tom, jaké soubory je potřeba nasadit*](determining-what-files-need-to-be-deployed-vb.md) , víme, co je potřeba zkopírovat soubory do poskytovatele webového hostitele. (Odvolání, které soubory jsou zkopírovány závisí na tom, zda je aplikace explicitně nebo automaticky zkompilována.) Jak ale získáme soubory z vývojového prostředí (z našeho počítače) až do produkčního prostředí (webový server spravovaný poskytovatelem webového hostitele)? Soubor [ **F** . **T** ransfer **P** rotocol (FTP)](http://en.wikipedia.org/wiki/File_Transfer_Protocol) je běžně používaný protokol pro kopírování souborů z jednoho počítače do druhého přes síť. Další možností je rozšíření FPSE (FrontPage Server Extensions). Tento kurz se zaměřuje na použití samostatného klientského softwaru FTP k nasazení potřebných souborů z vývojového prostředí do provozního prostředí.

> [!NOTE]
> Visual Studio obsahuje nástroje pro publikování webů přes FTP. Tyto nástroje, jakož i zobrazení nástrojů využívajících rozšíření FPSE, jsou uvedené v dalším kurzu.

K kopírování souborů pomocí FTP potřebujeme *klienta FTP* ve vývojovém prostředí. Klient FTP je aplikace, která je navržena ke kopírování souborů z počítače, který je nainstalován, do počítače, na kterém je spuštěn *Server FTP*. (Pokud poskytovatel webového hostitele podporuje přenosy souborů přes FTP, a to co nejvíc, pak je na webových serverech spuštěný FTP server.) K dispozici je několik klientských aplikací FTP. Webový prohlížeč může být dokonce dvojnásobný jako klient FTP. Můj oblíbený klient FTP a ten, který bude používat pro tento kurz, je [FileZilly](http://filezilla-project.org/), bezplatný Open Source klient FTP, který je k dispozici pro Windows, Linux a Mac. Jakýkoli klient FTP bude fungovat, ale nebudete si moct používat libovolného klienta, se kterým se vám bude líbit.

Pokud budete sledovat, budete muset před dokončením tohoto kurzu nebo následným vytvořením účtu vytvořit účet s poskytovatelem webového hostitele. Jak je uvedeno v předchozím kurzu, je Gaggle společnostem poskytovatele webového hostitele s velkým spektrem cen, funkcí a kvality služeb. V této sérii kurzů používáme jako poskytovatele webového hostitele [slevový ASP.NET](http://discountasp.net) , ale můžete postupovat spolu s libovolným poskytovatelem webového hostitele, pokud podporují verzi ASP.NET, ve které je váš web vyvinutý. (Tyto kurzy byly vytvořeny pomocí ASP.NET 3,5.) Také proto, že budeme soubory kopírovat do poskytovatele webového hostitele pomocí FTP v tomto kurzu a v budoucnu, je nezbytné, aby poskytovatel webového hostitele podporoval přístup FTP k webovým serverům. Tato funkce nabízí prakticky všichni poskytovatelé webového hostitele, ale před registrací byste měli ještě před registrací kontrolu.

## <a name="deploying-the-book-review-web-application-project"></a>Nasazení projektu webové aplikace revize knihy

Načtěte si, že existují dvě verze webové aplikace recenze pro knihu: jeden implementovaný pomocí modelu projektu webové aplikace (BookReviewsWAP) a druhý pomocí modelu webu projektu (BookReviewsWSP). Typ projektu ovlivňuje, zda je web kompilován automaticky nebo explicitně a že model kompilace určuje, které soubory je třeba nasadit. V důsledku toho budeme posuzovat nasazení projektů BookReviewsWAP a BookReviewsWSP odděleně od BookReviewsWAP. Pokud jste to ještě neudělali, chvíli Stáhněte tyto dvě ASP.NET aplikace.

Spusťte projekt BookReviewsWAP tak, že přejdete do složky `BookReviewsWAP` a dvakrát kliknete na `BookReviewsWAP.sln` soubor. Před nasazením projektu je důležité ho sestavit, aby se zajistilo, že všechny změny ve zdrojovém kódu jsou součástí zkompilovaného sestavení. Chcete-li sestavit projekt, přejděte do nabídky sestavení a vyberte možnost nabídky sestavit BookReviewsWAP. Tím se zkompiluje zdrojový kód v projektu do jednoho sestavení, `BookReviewsWAP.dll`, který je umístěn ve složce `Bin`.

Nyní jsme připraveni nasadit potřebné soubory. Spusťte klienta FTP a připojte se k webovému serveru u svého poskytovatele webového hostitele. (Pokud se přihlásíte k webové hostingové společnosti, budou vás e-mailem o připojení k serveru FTP zasílat. to zahrnuje adresu serveru FTP a také uživatelské jméno a heslo.)

Zkopírujte následující soubory z plochy do kořenové složky webu u svého poskytovatele webového hostitele. Když FTP na webový server u poskytovatele webového hostitele máte pravděpodobně v kořenovém adresáři webu. Někteří poskytovatelé webového hostitele ale mají podsložku s názvem `www` nebo `wwwroot`, která slouží jako kořenová složka pro vaše soubory webu. Nakonec při FTPing souborů může být nutné vytvořit odpovídající strukturu složky v produkčním prostředí – složku `Bin`, složku `Fiction`, složku `Images` atd.

- `~/Default.aspx`
- `~/About.aspx`
- `~/Site.master`
- `~/Web.config`
- `~/Web.sitemap`
- Úplný obsah složky `Styles`
- Úplný obsah složky `Images` (a její podsložka `BookCovers`)
- `~/Fiction/Default.aspx`
- `~/Fiction/Blaze.aspx`
- `~/Tech/Default.aspx`
- `~/Tech/CYOW.aspx`
- `~/Tech/TYASP35.aspx`
- `~/Bin/BookReviewsWAP.dll`

Obrázek 1 zobrazuje FileZilly po zkopírování potřebných souborů. FileZilly zobrazí soubory na místním počítači vlevo a na pravé straně soubory na vzdáleném počítači. Jak ukazuje obrázek 1, soubory zdrojového kódu ASP.NET, například `About.aspx.vb`, jsou v místním počítači (vývojové prostředí), ale nebyly zkopírovány do poskytovatele webového hostitele (produkční prostředí), protože soubory kódu není nutné při použití explicitní kompilace nasazovat.

> [!NOTE]
> Na provozním serveru není nijak poškozeno soubory zdrojového kódu, protože jsou ignorovány. ASP.NET zakazuje požadavky HTTP na soubory se zdrojovým kódem ve výchozím nastavení, takže i když se soubory zdrojového kódu nacházejí na provozním serveru, jsou pro návštěvníky webu nedostupné. (To znamená, že pokud se uživatel pokusí navštívit `http://www.yoursite.com/Default.aspx.vb` zobrazí se chybová stránka s vysvětlením, že tyto typy souborů `.vb` jsou zakázané.)

[![použít klienta FTP ke zkopírování potřebných souborů z plochy na webový server u poskytovatele webového hostitele.](deploying-your-site-using-an-ftp-client-vb/_static/image2.png)](deploying-your-site-using-an-ftp-client-vb/_static/image1.png)

**Obrázek 1**: použijte klienta FTP ke zkopírování potřebných souborů z plochy na webový server u poskytovatele webového hostitele ([kliknutím zobrazíte obrázek v plné velikosti).](deploying-your-site-using-an-ftp-client-vb/_static/image3.png)

Po nasazení lokality chvíli otestuje lokalitu. Pokud jste si zakoupili název domény a správně nakonfigurovali nastavení DNS, můžete navštívit web zadáním názvu domény. Další možností je, že váš poskytovatel webového hostitele by vám dodal adresu URL vašeho webu, který bude vypadat nějak jako *účet Account*. *webhostprovider*. com nebo *webhostprovider*. com/*account*. Například adresa URL pro můj účet na zlevněné ASP.NET je: `http://httpruntime.web703.discountasp.net`.

Na obrázku 2 vidíte nasazený web recenze knih. Všimněte si, že se zobrazuje na slevě ASP. Servery sítě, na `http://httpruntime.web703.discountasp.net`. V tomto okamžiku může kdokoli s připojením k Internetu zobrazit můj web! Jak očekáváme, lokalita vypadá a chová se stejně jako při testování ve vývojovém prostředí.

> [!NOTE]
> Pokud se zobrazí chyba při zobrazení vaší aplikace, zajistěte, abyste nasadili správnou sadu souborů. V dalším kroku zkontrolujte chybovou zprávu a zjistěte, jestli se v problému objevila nějaká upozornění. Následující postup vám umožní zapnout Helpdesk vaší webové hostitelské společnosti nebo odeslat svůj dotaz na příslušné fórum na [fórech ASP.NET](https://forums.asp.net/).

[![web recenze webu je teď přístupný pro kohokoli s připojením k Internetu.](deploying-your-site-using-an-ftp-client-vb/_static/image5.png)](deploying-your-site-using-an-ftp-client-vb/_static/image4.png)

**Obrázek 2**: web recenze knih je teď přístupný pro kohokoli s připojením k Internetu ([kliknutím zobrazíte obrázek v plné velikosti).](deploying-your-site-using-an-ftp-client-vb/_static/image6.png)

## <a name="deploying-the-book-review-web-site-project"></a>Nasazení projektu webu revize knihy

Při nasazování aplikace ASP.NET, která používá automatickou kompilaci, jako je například projekt webu BookReviewsWSP, není ve složce `Bin` žádné zkompilované sestavení. V důsledku toho musí být soubory zdrojového kódu webové aplikace nasazeny do provozního prostředí. Pojďme si projít tento proces.

Stejně jako u projektu webové aplikace je vhodné nejdřív aplikaci sestavit, než ji nasadíte. Při sestavování projektu webu nevytváří sestavení, kontroluje všechny chyby při kompilaci na stránce. Lepší vyhledání těchto chyb teď, než když návštěvník na web zjistíte.

Po úspěšném sestavení projektu pomocí klienta FTP zkopírujte následující soubory do kořenové složky webu u svého poskytovatele webového hostitele. Možná budete muset vytvořit odpovídající strukturu složek v produkčním prostředí.

> [!NOTE]
> Pokud jste již nasadili projekt BookReviewsWAP, ale přesto chcete zkusit nasadit projekt BookReviewsWSP, nejprve odstraňte všechny soubory na webovém serveru, které byly nahrány při nasazování BookReviewsWAP, a potom soubory nasaďte pro BookReviewsWSP.

- `~/Default.aspx`
- `~/Default.aspx.vb`
- `~/About.aspx`
- `~/About.aspx.vb`
- `~/Site.master`
- `~/Site.master.vb`
- `~/Web.config`
- `~/Web.sitemap`
- Úplný obsah složky `Styles`
- Úplný obsah složky `Images` (a její podsložka `BookCovers`)
- `~/App_Code/BasePage.vb`
- `~/Fiction/Default.aspx`
- `~/Fiction/Default.aspx.vb`
- `~/Fiction/Blaze.aspx`
- `~/Fiction/Blaze.aspx.vb`
- `~/Tech/Default.aspx`
- `~/Tech/Default.aspx.vb`
- `~/Tech/CYOW.aspx`
- `~/Tech/CYOW.aspx.vb`
- `~/Tech/TYASP35.aspx`
- `~/Tech/TYASP35.aspx.vb`

Obrázek 3 ukazuje FileZilly po zkopírování potřebných souborů. Jak vidíte, soubory ASP.NET zdrojového kódu, jako je například `About.aspx.vb`, jsou přítomny v místním počítači (vývojovém prostředí) a poskytovateli webového hostitele (produkční prostředí), protože soubory kódu musí být nasazeny při použití automatické kompilace.

[![použít klienta FTP ke zkopírování potřebných souborů z plochy na webový server u poskytovatele webového hostitele](deploying-your-site-using-an-ftp-client-vb/_static/image8.png)](deploying-your-site-using-an-ftp-client-vb/_static/image7.png)

**Obrázek 3**: použijte klienta FTP ke zkopírování potřebných souborů z plochy na webový server u poskytovatele webového hostitele ([kliknutím zobrazíte obrázek v plné velikosti).](deploying-your-site-using-an-ftp-client-vb/_static/image9.png)

Prostředí uživatele není ovlivněno modelem kompilace aplikace. Stejné stránky ASP.NET jsou přístupné a vypadají a chovají se stejně, ať už byl web vytvořen pomocí modelu projektu webové aplikace nebo modelu projektu webu.

## <a name="updating-a-web-application-on-production"></a>Aktualizace webové aplikace v produkčním prostředí

Vývoj webových aplikací a nasazení nejsou jednorázovým procesem. Například při vytváření stránky recenze webu jsem vytvořili různé stránky a napsali jste doprovodné kód na osobním počítači (vývojové prostředí). Po dosažení určitého stabilního stavu nasadím aplikaci, aby ostatní mohli navštívit web a číst moje recenze. Nasazení ale neoznačuje konec vývoje na tomto webu. Můžu přidat další recenze knih nebo implementovat nové funkce, jako je například umožnění návštěvníkům v hodnocení knih nebo ponechání vlastních komentářů. Taková vylepšení by se vyvinula ve vývojovém prostředí a po dokončení by se musela nasadit. Vývoj a nasazování jsou proto cyklicky. Vyvíjíte aplikaci a potom ji nasadíte. I když je web v provozu a v produkčním prostředí, přidají se nové funkce a v průběhu času se opravují chyby, které vyžadují opětovné nasazení aplikace. A tak dále.

Jak můžete očekávat, když znovu nasadíte webovou aplikaci, stačí zkopírovat jenom nové a změněné soubory. Není nutné znovu nasazovat nezměněné stránky nebo soubory podpory na straně serveru nebo klienta (i když to není nijak poškozeno).

> [!NOTE]
> Mějte na paměti, že při použití explicitní kompilace je potřeba vzít v úvahu, že kdykoli do projektu přidáte novou ASP.NET stránku nebo když provedete jakékoli změny kódu, musíte projekt znovu sestavit, který aktualizuje sestavení ve složce `Bin`. V důsledku toho budete muset zkopírovat toto aktualizované sestavení do produkčního prostředí při aktualizaci webové aplikace v produkčním prostředí (společně s jiným novým a aktualizovaným obsahem).

Také je třeba pochopit, že jakékoli změny `Web.config` nebo soubory v adresáři `Bin` zastaví a restartuje fond aplikací webu. Pokud je stav relace uložený pomocí režimu `InProc` (výchozí nastavení), budou návštěvníci vaší lokality přijít o stav relace, kdykoli budou tyto soubory změněny. Chcete-li se tomuto Pitfall vyhnout, zvažte uložení relace pomocí režimů `StateServer` nebo `SQLServer`. Další informace o tomto tématu najdete v článku [režimy stavu relace](https://msdn.microsoft.com/library/ms178586.aspx).

Nakonec mějte na paměti, že opětovné nasazení aplikace může trvat pár sekund až několik minut, a to v závislosti na počtu a velikosti souborů, které je potřeba zkopírovat do provozního prostředí. Během této doby mohou uživatelé, kteří navštíví váš web, zaznamenat chyby nebo liché chování. Můžete "vypnout celou aplikaci" přidáním stránky s názvem `App_Offline.htm` do kořenového adresáře vaší aplikace, který vysvětluje uživatele, že lokalita je mimo provoz pro údržbu (nebo cokoli) a bude brzy zálohována. Když je přítomen soubor `App_Offline.htm`, modul runtime ASP.NET přesměruje všechny příchozí požadavky na tuto stránku.

## <a name="summary"></a>Souhrn

Nasazení webové aplikace zahrnuje kopírování potřebných souborů z vývojového prostředí do provozního prostředí. Nejběžnějším způsobem, kterým se soubory přenáší přes síť, je protokol FTP (File Transfer Protocol) (FTP) a většina poskytovatelů webového hostitele podporuje přístup FTP na své webové servery. V tomto kurzu jsme zjistili, jak použít klienta FTP k nasazení potřebných souborů na webový server. Po nasazení může web navštívit kdokoli, kdo má připojení k Internetu.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Aplikace\_offline. htm a funguje s funkcí "přívětivé chyby IE".](https://weblogs.asp.net/scottgu/App_5F00_Offline.htm-and-working-around-the-_2200_IE-Friendly-Errors_2200_-feature)
- [Režimy stavu relace](https://msdn.microsoft.com/library/ms178586.aspx)

> [!div class="step-by-step"]
> [Předchozí](determining-what-files-need-to-be-deployed-vb.md)
> [Další](deploying-your-site-using-visual-studio-vb.md)
