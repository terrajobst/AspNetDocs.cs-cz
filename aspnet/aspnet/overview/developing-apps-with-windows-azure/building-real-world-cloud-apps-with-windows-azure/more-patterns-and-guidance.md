---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/more-patterns-and-guidance
title: Další vzory a pokyny (vytváření skutečných cloudových aplikací s Azure) | Microsoft Docs
author: MikeWasson
description: Vytváření reálných cloudových aplikací pomocí Azure je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které mohou...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 7e97cfc3-d830-4002-8ff7-5790d1ff49e6
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/more-patterns-and-guidance
msc.type: authoredcontent
ms.openlocfilehash: 57e32bf7568ecb0eb22f0f2b585310dcab2d5d43
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457073"
---
# <a name="more-patterns-and-guidance-building-real-world-cloud-apps-with-azure"></a>Další vzory a pokyny (vytváření skutečných cloudových aplikací s Azure)

[Jan Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Dykstra](https://github.com/tdykstra)

[Stažení opravy projektu IT](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stažení elektronické knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **Vytváření reálných cloudových aplikací pomocí Azure** je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které vám pomůžou úspěšně vyvíjet webové aplikace pro Cloud. Informace o elektronické příručce najdete v [první kapitole](introduction.md).

Teď jste viděli 13 vzorů, které poskytují pokyny k úspěšnému provedení v cloud computingu. Toto jsou jenom některé ze vzorů, které platí pro cloudové aplikace. Tady jsou některé další témata týkající se cloud computingu a materiály, které jim pomohou s těmito tématy:

- Migrují se stávající místní aplikace do cloudu. 

    - [Přesun aplikací do cloudu](https://msdn.microsoft.com/library/ff728592.aspx). Elektronická kniha podle vzorů a postupů Microsoftu. K dispozici také jako [tištěné verze pro kopírování](https://www.amazon.com/dp/1621140202).
    - [Migrují se ASP.NET a IIS.NET Microsoftu](https://go.microsoft.com/fwlink/?LinkId=400656). Případová studie Robert blog
    - [Přesunutí 4 &amp; Mayor na weby Azure](http://www.jeff.wilcox.name/2013/04/4thandmayor-azure-websites/). Blogový příspěvek by Jan Wilcox, že jeho činnost přesouvá webovou aplikaci z Amazon Web Services na Web Apps v Azure App Service.
    - [Přesouváte aplikace do Azure: Jaké změny?](https://azure.microsoft.com/documentation/videos/web-sites-internals-and-the-file-system/) Krátké video o Stefan Schackow, vysvětluje přístup k systému souborů v Web Apps v Azure App Service.
    - [Hybridní cloud Azure](https://www.amazon.com/dp/B00EOP4UQW). Hardcopy knihu nebo elektronickou knihu podle Danny Garber, Jamal Malik a Adam Fazio.
- Problémy se zabezpečením, ověřováním a autorizací, které jsou jedinečné pro cloudové aplikace

    - [Pokyny k zabezpečení Azure](https://azure.microsoft.com/blog/2014/02/10/best-practices-windows-azure-websites-waws/)
    - [Vzory a postupy Microsoftu – doprovodné materiály pro Azure](https://msdn.microsoft.com/library/dn568099.aspx) Viz vzor serveru gatekeeper, model federované identity.
    - [Zabezpečení sítě Azure](https://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx). Dokument white paper o Ashin Palekara.

Podívejte se také na další modely a pokyny pro cloud computing na základě [vzorů a postupů Microsoftu – doprovodné materiály pro Azure](https://msdn.microsoft.com/library/dn568099.aspx).

<a id="resources"></a>
## <a name="resources"></a>Prostředky

Každá z kapitol v této elektronické knize obsahuje odkazy na prostředky, kde najdete další informace o tomto konkrétním tématu. Následující seznam obsahuje odkazy na přehledy osvědčených postupů a doporučené vzory pro úspěšný vývoj v cloudu s Azure.

Dokumentace

- [Osvědčené postupy pro návrh rozsáhlých služeb v Azure Cloud Services](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx). Dokument White Paper, který označuje Simms a Michael Thomassy.
- [Failsafe: pokyny pro odolné cloudové architektury](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx). Dokument white paper o matolin Mercuri, Ulrich Homann a Andrew Townhill. Verze webové stránky pro video řady FailSafe
- [Pokyny pro Azure](https://azure.microsoft.com/develop/net/guidance/) Stránka portálu pro oficiální dokumentaci týkající se vývoje aplikací pro Azure.

Videa

- [Vytváření reálných cloudových aplikací s využitím Azure – část 1](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324) a [část 2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325). Video prezentace Scottem Guthrie, na kterém je tato elektronická kniha založená. Uvedené na konferenci Tech Ed Austrálie v září 2013. Na konferenci norských vývojářů se doručila dřívější verze stejné prezentace (NORWEGIAN Developers Conference) v červnu, 2013: [Norwegian Developers Conference část 1](http://vimeo.com/68215538) [Norwegian Developers Conference část 2](http://vimeo.com/68215602).
- [Failsafe: vytváření škálovatelných, odolných Cloud Services](https://channel9.msdn.com/Series/FailSafe). Devět datových řad podle Ulrich Homann, matolin Mercuri a Simms. 400 nabízí přehled o tom, jak architekt cloudových aplikací. Tato série se zaměřuje na teorie a důvody za doporučenými vzory; Další podrobné informace o tom, jak označit Simms, najdete v tématu vytváření velkých řad.
- [Sestavování velkých: lekcí získaných od zákazníků Azure – část 1](https://channel9.msdn.com/Events/Build/2012/3-029) a [část 2](https://channel9.msdn.com/Events/Build/2012/3-030). Série videí po dvou částech Simon Davies a označení Simms, podobně jako u řady FailSafe, ale orientované na praktické implementace.

Ukázka kódu

- [Oprava IT aplikace, která doprovází tuto elektronickou knihu](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4?cdn_id=2013-12-03-002).
- [Základy cloudových služeb v Azure v C# pro Visual Studio 2012](https://aka.ms/csf). Projekt ke stažení na webu Galerie kódu společnosti Microsoft zahrnuje jak kód, tak dokumentaci, kterou vyvinul tým pro odborné poradenství v Microsoftu (CAT). Ukazuje mnoho osvědčených postupů v FailSafe a vytváření velkých grafických řad a FailSafe dokumentu White Paper. Stránka Galerie kódu také odkazuje na rozsáhlou dokumentaci autory projektu – viz téma odkazy na základní informace o [kolekci wiki cloudových služeb](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx) v modrém poli v horní části popisu projektu. Tento projekt a dokumentace jsou stále aktivně vyvíjeny a díky tomu je lepší volbou pro informace o mnoha tématech, než jsou podobné, ale starší dokumenty White Paper.

Knihy pro pevné kopírování

- [Cloud Computing Bible](https://www.amazon.com/dp/0470903562). Od Barrie Sosinsky.
- [Návrh verze IT! a nasazení softwaru připraveného pro produkční](https://www.amazon.com/Release-It-Production-Ready-Pragmatic-Programmers/dp/0978739213)prostředí. Autor: Michael T. Nygard.
- [Vzory architektury cloudu: použití Microsoft Azure](http://shop.oreilly.com/product/0636920023777.do). Podle Bill Wilder
- [Platforma Windows Azure](https://www.amazon.com/dp/1430235632). Od Tejaswiho Redkara.
- [Programovací vzory Windows Azure pro spouštění](https://www.amazon.com/dp/1849685606). Od Riccardo Becker.
- [Microsoft Windows Azure Development kuchařka](https://www.amazon.com/dp/1849682224). Od Neilem Mackenzie.

Nakonec, když začnete vytvářet reálné aplikace a spouštíte je v Azure, dříve nebo později budete potřebovat pomoc od expertů. Můžete klást otázky na webech komunity, jako jsou [fóra Azure nebo StackOverflow](https://azure.microsoft.com/support/forums/), nebo můžete požádat o podporu Azure přímo na Microsoftu. Microsoft nabízí několik úrovní technické podpory Azure: Souhrn a porovnání možností najdete v tématu [Podpora Azure](https://azure.microsoft.com/support/plans/).

<a id="acknowledgments"></a>
## <a name="acknowledgments"></a>Potvrzení

Tento obsah byl napsán Dykstra, Rick Anderson a Mike Wasson. Většina původního obsahu pochází ze [Scott Guthrie](https://weblogs.asp.net/scottgu/)a v materiálech z značky Simms a Microsoft Customer Advisor (CAT).

Mnoho dalších kolegů na Microsoftu bylo zkontrolováno a komentáře k konceptům a kódu:

- Tim Ammann – prověření kapitoly automatizace
- Christopher Bennage – zkontrolováno a testováno opravný kód.
- Ryan – bobulovin – přezkoumání kapitoly CD/CI
- Vittorio Bertocci – zkontrolovala se kapitola jednotného přihlašování.
- Chris Clayton – pomáhá řešit technické problémy ve skriptech PowerShellu.
- Conor Cunningham – revize kapitoly možností úložiště dat
- Carlos Farre – zkontrolováno a testováno opravou kódu pro problémy se zabezpečením.
- Larry Franks – prověření kapitoly telemetrie a monitorování.
- Jonathana Gao – zkontrolované oddíly Hadoop a MapReduce v kapitole možnosti úložiště dat.
- Sidney Higa – zkontrolované všechny kapitoly.
- Gordon Hogenson – zkontrolovala se kapitola správy zdrojového kódu.
- Tamra Myers – možnosti úložiště dat, objekty BLOB a fronty – kapitoly.
- Pranav Rastogi předvádí – zkontrolovala se kapitola jednotného přihlašování.
- Míchačka v červnu Rogers – Přidali jsme zpracování chyb a pomohli skripty pro automatizaci PowerShellu.
- Mani Subramanian – zkontrolovaly všechny kapitoly a vedly proces revize kódu a testování kódu pro opravu IT.
- Shaun Tinline-Petr – prozkoumali jsme kapitolu dělení dat.
- Selcin Tukarslan – zkontrolované kapitoly, které pokrývají SQL Database a SQL Server.
- Edward Wu – poskytuje vzorový kód pro kapitolu SSO.
- Guang vystoupí Yang zapsal skripty PowerShellu pro automatizaci.

Členové [Rady Microsoft Developer Advisor rad](https://aka.ms/DGAC) (DGAC) se také přezkoumávají a v konceptech zakomentováni:

- Jean-Luc Boucho
- Catalin Gheorghiu
- Wouter de KORT
- Carlos dos Santos
- Neilem Mackenzie
- Dennis Persson
- Sunil Saba
- [Aleksey Sinyagin](http://www.linkedin.com/in/sinyagin)
- Wagner fakturace
- Michael dřevo

Ostatní členové DGAC se zkontrolovali a povyjádřili se do předběžného přehledu:

- Damir Arh
- Edward Bakker
- Srdjan Bozovic
- Mingu muž – kanál
- Gianni Rosa Gallina
- Paulo Morgado
- Jason Oliveira
- Alberto Poblacion
- Ryan Riley
- Perez Jones Tsisah
- Roger Whitehead
- Pawel Wilkosz

> [!div class="step-by-step"]
> [Předchozí](queue-centric-work-pattern.md)
> [Další](the-fix-it-sample-application.md)
