---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: 'Nasazení webové aplikace SQL Server Compact v ASP.NET s využitím sady Visual Studio nebo Visual Web Developer: nasazení SQL Server aktualizace databáze-11 z 12 | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: 0894c0ac24737e66b6960ef3d48aa17f78c6aa1d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78528124"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a>Nasazení webové aplikace SQL Server Compact v ASP.NET s využitím sady Visual Studio nebo Visual Web Developer: nasazení SQL Server aktualizace databáze-11 z 12

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Studio 2012 RC nebo Visual Studio Express 2012 RC pro web. Můžete také použít Visual Studio 2010, pokud nainstalujete aktualizaci publikování na webu. Úvod k řadě najdete v [prvním kurzu v řadě](deployment-to-a-hosting-provider-introduction-1-of-12.md).
> 
> Kurz, který ukazuje funkce nasazení představené po vydání RC sady Visual Studio 2012, ukazuje, jak nasadit jiné edice SQL Server než SQL Server Compact a ukazuje, jak nasadit na weby Windows Azure najdete v tématu [nasazení webu ASP.NET pomocí sady Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Přehled

V tomto kurzu se dozvíte, jak nasadit aktualizaci databáze do úplné SQL Server databáze. Vzhledem k tomu, že Migrace Code First provádí veškerou práci s aktualizací databáze, proces je téměř shodný s tím, co jste provedli pro SQL Server Compact v kurzu [nasazení aktualizace databáze](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) .

Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje při procházení tohoto kurzu, zkontrolujte [stránku řešení potíží](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).

## <a name="adding-a-new-column-to-a-table"></a>Přidání nového sloupce do tabulky

V této části kurzu provedete změnu v databázi a odpovídající změny kódu a pak je otestujete v aplikaci Visual Studio v článku Příprava pro jejich nasazení do testovacích a produkčních prostředí. Tato změna zahrnuje přidání sloupce `OfficeHours` k entitě `Instructor` a zobrazení nových informací na webové stránce **instruktoři** .

V projektu ContosoUniversity. DAL otevřete *Instructor.cs* a přidejte následující vlastnost mezi `HireDate` a `Courses` vlastnosti:

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

Aktualizujte třídu inicializátoru tak, aby vyzkoušela nový sloupec s testovacími daty. Otevřete *Migrations\Configuration.cs* a nahraďte blok kódu, který začíná `var instructors = new List<Instructor>` s následujícím blokem kódu, který obsahuje nový sloupec:

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

V projektu ContosoUniversity otevřete *instruktory. aspx* a přidejte nové pole šablony pro pracovní dobu Office těsně před uzavírací `</Columns>` značku v prvním `GridView`m ovládacím prvku:

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

Sestavte řešení.

Otevřete okno **konzoly Správce balíčků** a jako **výchozí projekt**vyberte ContosoUniversity. dal.

Zadejte následující příkazy:

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

Spusťte aplikaci a vyberte stránku **instruktoři** . Načtení stránky trvá trochu déle než obvykle, protože Entity Framework znovu vytvoří databázi a semena s testovacími daty.

[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)

## <a name="deploying-the-database-update-to-the-test-environment"></a>Nasazení aktualizace databáze do testovacího prostředí

Při použití Migrace Code First je metoda nasazení změny databáze do SQL Server stejná jako u SQL Server Compact. Je však nutné změnit profil publikování testu, protože je stále nastaven na migraci z SQL Server Compact na SQL Server.

Prvním krokem je odebrání transformací připojovacích řetězců, které jste vytvořili v předchozím kurzu. Ty už nejsou potřeba, protože v profilu publikování zadáte transformace připojovacích řetězců, jak jste předtím nakonfigurovali kartu **balíček/publikování SQL** pro migraci na SQL Server.

Otevřete soubor *Web. test. config* a odeberte `connectionStrings` element. Jedinou zbývající transformací v souboru *Web. test. config* je hodnota `Environment` v elementu `appSettings`.

Nyní můžete aktualizovat profil publikování a publikovat do testovacího prostředí.

Otevřete Průvodce **publikováním webu** a poté přepněte na kartu **profil** .

Vyberte profil publikování **testu** .

Vyberte kartu **Nastavení** .

Klikněte na **Povolit nová vylepšení publikování databáze**.

Do pole Připojovací řetězec pro **SchoolContext**zadejte stejnou hodnotu, jakou jste použili v transformačním souboru *Web. test. config* v předchozím kurzu:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

Vyberte **Execute migrace Code First (spouští se při spuštění aplikace)** . (Ve vaší verzi sady Visual Studio může být zaškrtávací políčko označeno jako **migrace Code First**.)

Do pole Připojovací řetězec pro **DefaultConnection**zadejte stejnou hodnotu, jakou jste použili v transformačním souboru *Web. test. config* v předchozím kurzu:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

Ponechte vymazané **aktualizaci databáze** .

Klikněte na **Publikovat**.

Visual Studio nasadí změny kódu do testovacího prostředí a otevře prohlížeč na domovské stránce společnosti Contoso University.

Vyberte stránku instruktoři.

Když aplikace tuto stránku spustí, pokusí se získat přístup k databázi. Migrace Code First zkontroluje, jestli je databáze aktuální, a zjistí, že se zatím nepoužila poslední migrace. Migrace Code First aplikuje nejnovější migraci, spustí metodu `Seed` a pak se stránka normálně spustí. Zobrazí se sloupec nové hodiny Office s dosazením dat.

[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)

## <a name="deploying-the-database-update-to-the-production-environment"></a>Nasazení aktualizace databáze do provozního prostředí

Je třeba změnit profil publikování také pro produkční prostředí. V takovém případě odeberete stávající profil a vytvoříte nový pomocí importu aktualizovaného souboru. publishsettings. Aktualizovaný soubor bude obsahovat připojovací řetězec pro databázi SQL Server na adrese Cytanium.

Jak bylo zobrazeno, když jste nasadili do testovacího prostředí, již nepotřebujete transformaci připojovacího řetězce v transformačním souboru *Web. produkční. config* . Otevřete tento soubor a odeberte `connectionStrings` element. Zbývající transformace jsou pro hodnotu `Environment` v elementu `appSettings` a element `location`, který omezuje přístup k knihovny elmah zpráv o chybách.

Před vytvořením nového publikačního profilu pro produkci si stáhněte aktualizovaný soubor. publishsettings stejným způsobem jako dříve v kurzu [nasazení do provozního prostředí](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) . (V ovládacím panelu Cytanium klikněte na **weby**a pak klikněte na web **contosouniversity.com** . Vyberte kartu **publikování na webu** a pak klikněte na **Stáhnout profil publikování pro tento web**.) Důvodem je, že je třeba v souboru. publishsettings vybrat připojovací řetězec databáze. Připojovací řetězec nebyl při prvním stažení souboru k dispozici, protože jste stále používali SQL Server Compact a jste vytvořili databázi SQL Server na Cytanium.

Teď můžete aktualizovat profil publikování a publikovat ho v produkčním prostředí.

Otevřete Průvodce **publikováním webu** a poté přepněte na kartu **profil** .

Klikněte na **Spravovat profily**a pak odstraňte produkční profil.

Zavřete průvodce **publikováním webu** a uložte tuto změnu.

Spusťte průvodce **publikováním webu** znovu a pak klikněte na **importovat**.

Na kartě **připojení** změňte **cílovou adresu URL** na odpovídající hodnotu, pokud používáte dočasnou adresu URL.

Klikněte na **Další**.

Na kartě **Nastavení** klikněte na **Povolit nová vylepšení publikování databáze**.

V rozevíracím seznamu připojovací řetězec pro **SchoolContext**vyberte připojovací řetězec Cytanium.

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

Vyberte možnost **spustit Code First migrace (spouští se při spuštění aplikace)** .

V rozevíracím seznamu připojovací řetězec pro **DefaultConnection**vyberte připojovací řetězec Cytanium.

Vyberte kartu **profil** , klikněte na **Spravovat profily**a přejmenujte profil z "contosouniversity.com-nasazení webu" na "produkční".

Zavřete profil publikování a uložte změnu a pak znovu otevřete.

Klikněte na **Publikovat**. (Pro skutečný produkční web byste aplikaci zkopírovali *\_offline. htm* do produkčního prostředí a před publikováním ji uložte do složky projektu a pak ji po dokončení nasazení odebrat.)

Visual Studio nasadí změny kódu do testovacího prostředí a otevře prohlížeč na domovské stránce společnosti Contoso University.

Vyberte stránku instruktoři.

Migrace Code First aktualizuje databázi stejným způsobem jako v testovacím prostředí. Zobrazí se sloupec nové hodiny Office s dosazením dat.

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

Nyní jste úspěšně nasadili aktualizaci aplikace, která zahrnovala změnu databáze, pomocí SQL Server databáze.

## <a name="more-information"></a>Další informace

Tím se dokončí Tato série kurzů pro nasazení webové aplikace v ASP.NET k poskytovateli hostingu třetí strany. Další informace o všech tématech popsaných v těchto kurzech naleznete v části [Mapa obsahu nasazení ASP.NET](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) na webu MSDN.

## <a name="acknowledgements"></a>Poděkování

Chci nás zasílat na následující lidi, kteří významně přispěli k obsahu této série kurzů:

- [Alberto Poblacion, MVP &amp; MCT, Španělsko](https://mvp.support.microsoft.com/profile/Alberto)
- Jarod Ferguson, MVP pro vývoj datových platforem, USA
- Harsh Mittal, Microsoft
- [Kristina Olson, Microsoft](https://blogs.iis.net/krolson/default.aspx)
- [Mike Pope, Microsoft](http://www.mikepope.com/blog/DisplayBlog.aspx)
- Mohit Srivastava, Microsoft
- [Raffaele Rialdi, Itálie](http://www.iamraf.net/)
- [Rick Anderson, Microsoft](https://blogs.msdn.com/b/rickandy/)
- [Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))
- [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))
- [Scott Hunterem, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))
- [Srđan Božović, Srbsko](http://msforge.net/blogs/zmajcek/)
- [Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))

> [!div class="step-by-step"]
> [Předchozí](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
> [Další](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)
