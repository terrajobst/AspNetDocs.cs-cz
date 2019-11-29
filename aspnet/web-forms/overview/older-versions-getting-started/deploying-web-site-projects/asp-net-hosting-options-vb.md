---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/asp-net-hosting-options-vb
title: Možnosti hostování ASP.NET (VB) | Microsoft Docs
author: rick-anderson
description: Webové aplikace v ASP.NET se obvykle navrhují, vytvářejí a testují v místním vývojovém prostředí a je potřeba je nasadit do provozního prostředí...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 492f5ae2-bad7-4107-89a9-f04a9525dee7
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/asp-net-hosting-options-vb
msc.type: authoredcontent
ms.openlocfilehash: 4293114002aee15ddace1a3f19c240f35e6065f5
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74620763"
---
# <a name="aspnet-hosting-options-vb"></a>Možnosti hostování v technologii ASP.NET (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial01_Basics_vb.pdf)

> Webové aplikace v ASP.NET se obvykle navrhují, vytvářejí a testují v místním vývojovém prostředí a je potřeba je nasadit do provozního prostředí, jakmile bude připravené k vydání. Tento kurz poskytuje podrobný přehled procesu nasazení a slouží jako úvod do této série kurzů.

## <a name="introduction"></a>Úvod

Webové aplikace jsou obvykle navrženy, vytvořeny a testovány ve vývojovém prostředí, které je přístupné pouze programátorům pracujícím na webu. Jakmile je aplikace připravená k uvolnění, přesune se do produkčního prostředí, kde k webu může přistupovat kdokoli na internetu. Tento proces nasazení přináší řadu problémů:

- Aby bylo možné nasadit aplikaci ASP.NET, musí existovat produkční prostředí a musí být správně nastavené. Kromě toho musí být provozní prostředí udržováno v aktuálním stavu pomocí nejnovějších oprav zabezpečení.
- Správná sada souborů označení, soubory kódu a podpůrné soubory musí být zkopírovány z vývojového prostředí do produkčního prostředí. Pro aplikace založené na datech může to vyžadovat také kopírování schématu databáze nebo dat.
- Mezi těmito dvěma prostředími můžou být rozdíly v konfiguraci. Připojovací řetězec databáze nebo e-mailový server, který se používá ve vývojovém prostředí, se pravděpodobně liší od produkčního prostředí. A co víc, chování aplikace může záviset na prostředí. Například pokud při vývoji dojde k chybě, může se zobrazit na obrazovce, ale pokud dojde k chybě v produkčním prostředí, zobrazí se místo toho uživatelsky přívětivá chybová stránka, která bude obsahovat podrobnosti o chybě e-mailem vývojářům.

Aby se předešlo prvnímu výzvě – nastavení a udržování produkčního prostředí – mnoho jednotlivců a firem externí vlastní produkční prostředí pro *poskytovatele hostingu webů*. Poskytovatel hostování webů je společnost, která spravuje provozní prostředí vaším jménem. Existují poskytovatelé webového hostitele dlouhé, každý s různými cenami a úrovněmi služeb; Tipy k nalezení takového poskytovatele služeb najdete v části Vyhledání poskytovatele webového hostitele.

Toto je první v řadě kurzů, které se týkají kroků v části nasazení webové aplikace v ASP.NET do produkčního prostředí spravovaného poskytovatelem webového hostitele. V průběhu těchto kurzů prověříme:

- Jaké soubory je třeba nasadit do poskytovatele webového hostitele.
- Nástroje pro zjednodušení procesu nasazení.
- Jak nasadit databázi.
- Tipy pro nasazení databáze, která používá [členství a zprostředkovatele rolí založené na SQL](../../older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs.md), spolu s způsoby, jak napodobovat Nástroj pro správu webu v produkčním prostředí.
- Strategie pro hladkou aktualizaci databáze v produkčním prostředí se změnami provedenými během vývoje.
- Techniky pro protokolování chyb, ke kterým dochází v produkci, a způsoby, jak informovat vývojáře, když dojde k chybě.

Tyto kurzy jsou stručné a poskytují podrobné pokyny s mnoha snímky obrazovky, které vás provedou procesem vizuálně. Tento kurz konference poskytuje přehled procesu nasazení ASP.NET a Rady ohledně hledání poskytovatele hostování webů. Pojďme začít!

## <a name="an-overview-of-the-aspnet-deployment-process"></a>Přehled procesu nasazení ASP.NET

V kostce nasazení aplikace ASP.NET zahrnuje následující tři kroky:

1. Konfigurace webové aplikace, webového serveru a databáze v produkčním prostředí.
2. Synchronizuje stránky ASP.NET, soubory kódu, sestavení ve složce `Bin` a podpůrné soubory HTML, jako jsou soubory CSS a JavaScript.
3. Synchronizujte schéma databáze a data.

Informace o konfiguraci webové aplikace se obvykle nacházejí v souboru `Web.config` a zahrnují databázové připojovací řetězce, kritéria zpracování chyb, pravidla pro přepis adres URL a informace o e-mailovém serveru. Často tyto informace se liší pro aplikaci ve vývoji a stejnou aplikaci v produkčním prostředí. Například při vývoji aplikace je nejvhodnější použít vývojovou databázi, takže nebudete testováni na provozní databázi. V důsledku toho se databázové připojovací řetězce obvykle liší mezi vývojem a provozními aplikacemi. Vzhledem k těmto rozdílům zahrnuje součást nasazení změny informací o konfiguraci webové aplikace.

Kromě změn konfigurace webové aplikace může krok 1 také zahrnovat konfiguraci webového serveru a databáze. Pokud například stránka ASP.NET vytvoří nebo odstraní soubory z adresáře na webovém serveru, je nutné nakonfigurovat webový server tak, aby povoloval tyto změny systému souborů. Podobně může být k dispozici oprávnění nebo nastavení ověřování, které je třeba provést v databázi.

Krok 2 zahrnuje synchronizaci sady důležitých stránek ASP.NET a podpůrných souborů mezi vývojovým a produkčním prostředím. Konkrétní sada souborů souvisejících s ASP.NET, které je třeba synchronizovat mezi těmito dvěma prostředími, závisí na typu projektu, který jste vytvořili v aplikaci Visual Studio, a je diskuze v dalším kurzu <em>[určení, které soubory je třeba nasadit](determining-what-files-need-to-be-deployed-vb.md)</em>. Třetí a čtvrté kurzy – <em>[nasazení lokality pomocí FTP](deploying-your-site-using-an-ftp-client-vb.md)</em>a <em>[nasazení webu pomocí sady Visual Studio](deploying-your-site-using-visual-studio-vb.md)</em> – Projděte si různé nástroje a techniky pro synchronizaci těchto souborů.

Při sestavování datově řízených aplikací se obvykle používají dvě databáze: jednu pro vývoj a jednu v produkčním prostředí. Během vývoje může být schéma vývojové databáze upraveno tak, aby zahrnovalo nové tabulky, sloupce, uložené procedury a triggery, nebo může být upraveno pro odebrání nebo přejmenování existujících databázových objektů. Mezi časem provedení těchto změn a časem nasazení aplikace do produkčního prostředí se databáze pro vývoj a provoz nesynchronizují. Tento asynchronii se musí během procesu nasazování opravit. Tyto výzvy budou přezkoumány v budoucích kurzech.

## <a name="finding-a-web-host-provider"></a>Hledání poskytovatele webového hostitele

Aplikace ASP.NET se dají nasadit na jakýkoli webový server, na kterém je nainstalovaná služba .NET Framework a Internetová informační služba (IIS). Lokalitu můžete hostovat z osobního počítače za předpokladu, že jste měli širokopásmové připojení k Internetu a víte, jak směrovač nakonfigurovat tak, aby povoloval příchozí webové požadavky. Lokalitu můžete také hostovat z počítače v intranetu, ale i mnoho společností. Zaměřte se na tyto kurzy, ale na hostování vašeho webu u poskytovatele webového hostitele.

> [!NOTE]
> [Služba IIS](https://www.iis.net/) je webový server společnosti Microsoft na podnikové úrovni. Dodává se s edicemi systému Windows, které nejsou doma, například Windows Server 2008 a některé edice systému Windows Vista. Nemusíte instalovat službu IIS, aby sloužila aplikacím ASP.NET ve vývojovém prostředí, protože Visual Studio zahrnuje vývojový webový server ASP.NET. Vývojový webový server ASP.NET ale přijímá jenom místní připojení, takže se nedá použít v produkčním prostředí.

Než budete moct nasadit svůj web do poskytovatele webového hostitele, musíte se nejdřív rozhodnout, kde společnost má dělat firmy. Na webu Marketplace existují dlouhé společnosti pro hostování webů; hledání "společnosti pro hostování na webu" vrací více než 5 000 000 výsledků. Jak najdete tu, která je pro vás ta pravá? Oblíbený vyhledávací web je dobrým počátečním místem, jako jsou weby jako [TopHosts](http://www.tophosts.com/) a [HostCritique](http://www.hostcritique.net/), které porovnávají a kontrastují různé hostitelské služby. Také doporučujeme požádat své kolegy a spolupracovníky na všechna doporučení; doporučení můžete také požádat o doporučení pro [hostování otevřeného fóra](https://forums.asp.net/158.aspx) v [ASP.NET fórech](https://forums.asp.net/).

Společnosti pro hostování webů typicky nabízejí sdílené hostitelské plány a vyhrazené plány hostování. Se sdíleným hostováním jednoho webového serveru hostuje desítky, pokud ne stovky různých webů. S vyhrazeným hostováním zapůjčujete počítač od společnosti, která poskytuje váš web i web samostatně. Sdílený plán hostování může zahrnovat podporu pro stránky ASP.NET, schopnost pracovat s databázemi aplikace Microsoft Access, 5 GB místa na disku a 100 GB propustnosti měsíčního provozu pro $9,95 za měsíc. Jiný sdílený plán hostování může zahrnovat podporu pro stránky ASP.NET, přístup k databázovému serveru Microsoft SQL Server 2008, 10 GB místa na disku a 250 GB provozu na šířku pásma pro $19,95 za měsíc. Vyhrazené hostitelské plány jsou obvykle mnohem dražší a účtují více než 100 dolarů za měsíc, ale nabízejí lepší výkon a větší kontrolu než možnosti sdíleného hostování. Plán, který zvolíte, závisí na vašem rozpočtu, na množství dat, které váš web obdrží, a na vámi předpokládaných funkcích budete potřebovat.

Mezi dva důležité důležité informace při výběru poskytovatele webového hostitele jsou služby zákazníkům a kvalita služeb. Pokud máte nějaký dotaz nebo problém s konfigurací, jak dlouho trvá odeslání problému do helpdesku webového hostitele, dokud nedostanete odpověď? Jak spolehlivé jsou služby společnosti? Mají často výpadky databáze? Jak často má jejich e-mailový server přejít do režimu offline? Vždy si můžete položit společnost, aby poskytovala podrobné informace o jejich provozní době a dotazování na jejich zákaznickou zásadu, ale ještě více surefire způsob, jak vyžádat zpětnou vazbu stávajících a minulých zákazníků, které můžete provádět prostřednictvím online fór, diskusních skupin a e-mailových listservs. .

> [!NOTE]
> Některé společnosti pro hostování webů zaměřují svou firmu na konkrétní technologický zásobník, jako je .NET nebo [lampa](http://en.wikipedia.org/wiki/LAMP_stack) (**L** Inux **, Pache** , **M** ySQL a **P** HP), takže se ujistěte, že společnost, kterou vyberete, hostuje ASP.NET aplikace. Také zkontrolujte, zda podporují verzi ASP.NET, kterou používáte k sestavení aplikace. A pokud vytváříte aplikaci založenou na datech, ujistěte se, že webový hostitel nabízí stejný databázový server a verzi, kterou používáte.

## <a name="summary"></a>Přehled

Webové aplikace ASP.NET jsou obvykle navrženy, vytvořeny a testovány v místním vývojovém prostředí. Jakmile je verze připravena k vydání, bude přesunuta do produkčního prostředí. I když je možné hostovat ASP.NET weby na vašem osobním počítači nebo na serverech v rámci vaší společnosti, mnoho podniků a jednotlivců si zvolí jako poskytovatele webového hostitele vlastní hostování.

V této sérii kurzů se prozkoumá postup nasazení aplikace ASP.NET do poskytovatele webového hostitele a prozkoumá běžné problémy. V tomto kurzu jste si nabídli základní přehled procesu nasazení ASP.NET a poskytli tipy pro vyhledání vhodného poskytovatele webového hostitele. V dalším kurzu se zobrazí informace o tom, jaké soubory související s ASP.NET je nutné při nasazování webu zkopírovat do produkčního prostředí.

Šťastné programování!

### <a name="special-thanks-to"></a>Zvláštní díky...

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Teresa Murphy. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com).

> [!div class="step-by-step"]
> [Předchozí](users-and-roles-on-the-production-website-cs.md)
> [Další](determining-what-files-need-to-be-deployed-vb.md)
