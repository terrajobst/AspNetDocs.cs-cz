---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
title: Ověřují se uživatelé s ověřováním pomocíC#formulářů () | Microsoft Docs
author: microsoft
description: Přečtěte si, jak pomocí atributu [autorizovat] chránit heslem konkrétní stránky v aplikaci MVC. Naučíte se, jak používat správu webu...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 239fd3ca-5630-4b8d-bc4b-2f906b1d3504
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: bed2eafa47fec25ac04cb07e0037f596494bb7d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541508"
---
# <a name="authenticating-users-with-forms-authentication-c"></a>Ověřování uživatelů pomocí formulářů (C#)

od [Microsoftu](https://github.com/microsoft)

> Přečtěte si, jak pomocí atributu [autorizovat] chránit heslem konkrétní stránky v aplikaci MVC. Naučíte se, jak pomocí nástroje pro správu webu vytvářet a spravovat uživatele a role. Naučíte se také, jak nakonfigurovat, kde jsou uložené informace o uživatelském účtu a roli.

Cílem tohoto kurzu je vysvětlit, jak můžete používat ověřování pomocí formulářů k ochraně zobrazení v aplikacích ASP.NET MVC. Naučíte se, jak pomocí nástroje pro správu webu vytvářet uživatele a role. Naučíte se také, jak zabránit neautorizovaným uživatelům v vyvolání akcí kontroleru. Nakonec se dozvíte, jak nakonfigurovat, kde jsou uložená uživatelská jména a hesla.

#### <a name="using-the-web-site-administration-tool"></a>Použití nástroje pro správu webu

Než budeme dělat cokoli jiného, měli byste začít vytvořením některých uživatelů a rolí. Nejjednodušší způsob, jak vytvořit nové uživatele a role, je využít nástroj pro správu webu sady Visual Studio 2008. Tento nástroj můžete spustit výběrem možnosti nabídky **projekt, konfigurace ASP.NET**. Alternativně můžete spustit nástroj pro správu webu kliknutím na ikonu (trochu Scary) kladiva, která se zobrazí v horní části okna Průzkumník řešení (viz obrázek 1).

**Obrázek 1 – spuštění nástroje pro správu webu**

![clip_image002](authenticating-users-with-forms-authentication-cs/_static/image1.jpg)

V nástroji pro správu webu můžete vytvořit nové uživatele a role výběrem karty zabezpečení. Kliknutím na odkaz **vytvořit uživatele** vytvořte nového uživatele s názvem Stephen (viz obrázek 2). Poskytněte Stephen uživateli jakékoli heslo, které chcete (například *tajný klíč*).

**Obrázek 2 – Vytvoření nového uživatele**

![clip_image004](authenticating-users-with-forms-authentication-cs/_static/image2.jpg)

Nové role vytvoříte tak, že nejprve povolíte role a definujete jednu nebo více rolí. Role Povolte kliknutím na odkaz **Povolit role** . Potom vytvořte roli s názvem *Administrators* kliknutím na odkaz **vytvořit nebo spravovat role** (viz obrázek 3).

**Obrázek 3 – vytvoření nové role**

![clip_image006](authenticating-users-with-forms-authentication-cs/_static/image3.jpg)

Nakonec vytvořte nového uživatele s názvem Sally a přidružte Sally k roli Administrators kliknutím na odkaz vytvořit uživatele a výběrem možnosti správci při vytváření Sally (viz obrázek 4).

**Obrázek 4 – Přidání uživatele k roli**

![clip_image008](authenticating-users-with-forms-authentication-cs/_static/image4.jpg)

Když je vše zmíněné a hotové, měli byste mít dva nové uživatele s názvem Stephen a Sally. Měli byste také mít novou roli s názvem Administrators. Sally je členem role Administrators a Stephen není.

#### <a name="requiring-authorization"></a>Vyžadování autorizace

Můžete vyžadovat, aby uživatel byl ověřený předtím, než uživatel vyvolá akci kontroleru přidáním atributu [autorizační] k akci. Můžete použít atribut [autorizovat] na jednotlivé akce kontroleru nebo můžete použít tento atribut na celou třídu kontroleru.

Například kontroler v výpisu 1 zpřístupňuje akci s názvem CompanySecrets (). Vzhledem k tomu, že tato akce je upravena pomocí atributu [autorizovat], tuto akci nelze vyvolat, pokud není uživatel ověřen.

**Výpis 1 – souboru controllers\homecontroller.cs**

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample1.cs)]

Pokud zavoláte akci CompanySecrets () tak, že zadáte adresu URL/Home/CompanySecrets na adresní řádek v prohlížeči a nejste ověřeným uživatelem, budete přesměrováni na automatické zobrazení přihlášení (viz obrázek 5).

**Obrázek 5 – zobrazení přihlášení**

![clip_image010](authenticating-users-with-forms-authentication-cs/_static/image5.jpg)

Můžete použít zobrazení přihlášení a zadat své uživatelské jméno a heslo. Pokud nejste registrovaný uživatel, můžete kliknout na odkaz **zaregistrovat** a přejít k zobrazení registru (viz obrázek 6). Můžete použít zobrazení registru k vytvoření nového uživatelského účtu.

**Obrázek 6 – zobrazení registrů**

![clip_image012](authenticating-users-with-forms-authentication-cs/_static/image6.jpg)

Po úspěšném přihlášení si můžete prohlédnout zobrazení CompanySecrets (viz obrázek 7). Ve výchozím nastavení budete nadále přihlášeni, dokud nezavřete okno prohlížeče.

**Obrázek 7 – zobrazení CompanySecrets**

![clip_image014](authenticating-users-with-forms-authentication-cs/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a>Autorizace podle uživatelského jména nebo role uživatele

Atribut [autorizovat] můžete použít k omezení přístupu k akci kontroleru na konkrétní skupinu uživatelů nebo konkrétní sadu rolí uživatele. Například upravený domovský řadič v seznamu 2 obsahuje dvě nové akce s názvem StephenSecrets () a AdministratorSecrets ().

**Výpis 2 – souboru controllers\homecontroller.cs**

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample2.cs)]

Akci StephenSecrets () může vyvolat jenom uživatel s uživatelským jménem Stephen. Všichni ostatní uživatelé budou přesměrováni na zobrazení přihlášení. Vlastnost Users přijímá seznam názvů uživatelských účtů oddělených čárkami.

Akci AdministratorSecrets () mohou vyvolat pouze uživatelé v roli správců. Například vzhledem k tomu, že Sally je členem skupiny Administrators, může vyvolat akci AdministratorSecrets (). Všichni ostatní uživatelé budou přesměrováni na zobrazení přihlášení. Vlastnost role přijímá seznam názvů rolí oddělených čárkami.

#### <a name="configuring-authentication"></a>Konfigurace ověřování

V tomto okamžiku se můžete zajímat, kde se ukládají informace o uživatelském účtu a roli. Ve výchozím nastavení jsou informace uložené v databázi SQL Express s názvem ASPNETDB. mdf, která se nachází ve složce aplikace\_dat aplikace MVC. Tato databáze je generována ASP.NET architekturou automaticky, když začnete používat členství.

Chcete-li zobrazit databázi ASPNETDB. mdf v okně Průzkumník řešení, musíte nejprve vybrat možnost projekt možnosti nabídky, Zobrazit všechny soubory.

Použití výchozí databáze SQL Express je při vývoji aplikace přesné. Pravděpodobně ale nebudete chtít používat výchozí databázi ASPNETDB. mdf pro produkční aplikaci. V takovém případě můžete změnit, kde jsou uložené informace o uživatelském účtu, a to provedením následujících dvou kroků:

1. Přidání databázových objektů Aplikační služby do provozní databáze – Změňte připojovací řetězec aplikace tak, aby odkazoval na provozní databázi.

Prvním krokem je přidání všech potřebných databázových objektů (tabulek a uložených procedur) do provozní databáze. Nejjednodušší způsob, jak tyto objekty přidat do nové databáze, je využít průvodce instalací SQL Server ASP.NET (viz obrázek 8). Tento nástroj můžete spustit otevřením příkazového řádku sady Visual Studio 2008 ze skupiny programu Microsoft Visual Studio 2008 a spuštěním následujícího příkazu z příkazového řádku:

ASPNET\_regsql

**Obrázek 8 – Průvodce instalací SQL Server ASP.NET**

![clip_image016](authenticating-users-with-forms-authentication-cs/_static/image8.jpg)

Průvodce instalací SQL Server ASP.NET umožňuje vybrat databázi SQL Server v síti a nainstalovat všechny databázové objekty, které vyžadují aplikační služby ASP.NET. Databázový server není nutné umístit na místní počítač.

> [!NOTE] 
> 
> Pokud nechcete použít Průvodce instalací SQL Server ASP.NET, můžete najít skripty SQL pro přidání databázových objektů služby Application Services do následující složky:
> 
> > C:\Windows\Microsoft.NET\Framework\v2.0.50727

Po vytvoření potřebných databázových objektů je nutné upravit připojení k databázi, které používá aplikace MVC. Upravte připojovací řetězec ApplicationServices v souboru webové konfigurace (Web. config) tak, aby odkazoval na provozní databázi. Například upravené připojení v seznamu 3 odkazuje na databázi s názvem MyProductionDB (původní připojovací řetězec ApplicationServices byl zakomentován).

**Výpis 3 – Web. config**

[!code-xml[Main](authenticating-users-with-forms-authentication-cs/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a>Konfigurace oprávnění databáze

Použijete-li integrované zabezpečení pro připojení k databázi, budete muset přidat správný uživatelský účet systému Windows jako přihlašovací jméno k databázi. Správný účet závisí na tom, zda používáte vývojový server ASP.NET nebo Internetová informační služba jako webový server. Správný uživatelský účet závisí také na vašem operačním systému.

Pokud používáte vývojový server ASP.NET (výchozí webový server používaný aplikací Visual Studio), aplikace se spustí v kontextu uživatelského účtu systému Windows. V takovém případě je nutné přidat uživatelský účet systému Windows jako přihlášení k databázovému serveru.

Případně, pokud používáte Internetová informační služba pak musíte přidat účet ASPNET nebo účet služby NT/NETWORK SERVICE jako přihlášení k databázovému serveru. Pokud používáte systém Windows XP, přidejte účet ASPNET jako přihlašovací údaje do vaší databáze. Pokud používáte novější operační systém, například Windows Vista nebo Windows Server 2008, přidejte účet AUTORITy NT/síťová služba jako přihlašovací jméno databáze.

Nový uživatelský účet můžete do databáze přidat pomocí Microsoft SQL Server Management Studio (viz obrázek 9).

**Obrázek 9 – vytvoření nového Microsoft SQL Serverho přihlášení**

![clip_image018](authenticating-users-with-forms-authentication-cs/_static/image9.jpg)

Po vytvoření požadovaného přihlašovacího jména musíte mapovat přihlášení k uživateli databáze se správnými databázovými rolemi. Dvakrát klikněte na přihlášení a vyberte kartu mapování uživatele. Vyberte jednu nebo více databázových rolí služby Application Services. Chcete-li například ověřit uživatele, je třeba povolit roli databáze ASPNET\_Membership\_BasicAccess. Aby bylo možné vytvářet nové uživatele, je nutné povolit roli FullAccess členství v\_ASPNET\_a databázi (viz obrázek 10).

**Obrázek 10 – přidávání rolí Aplikační služby databáze**

![clip_image020](authenticating-users-with-forms-authentication-cs/_static/image10.jpg)

#### <a name="summary"></a>Souhrn

V tomto kurzu jste zjistili, jak používat ověřování pomocí formulářů při sestavování aplikace ASP.NET MVC. Nejprve jste zjistili, jak vytvořit nové uživatele a role pomocí nástroje pro správu webu. V dalším kroku jste zjistili, jak použít atribut [autorizovat] k tomu, aby se zabránilo neautorizovaným uživatelům v vyvolání herních akcí. Nakonec jste zjistili, jak nakonfigurovat aplikaci MVC tak, aby ukládala informace o uživatelích a rolích do provozní databáze.

> [!div class="step-by-step"]
> [Next](authenticating-users-with-windows-authentication-cs.md)
