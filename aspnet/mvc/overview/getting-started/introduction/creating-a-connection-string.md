---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: Vytvoření připojovacího řetězce a práce s SQL Server LocalDB | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: 20781ad760d3a0e4559ec4c7e18528f3686dcc02
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456514"
---
# <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="273ac-102">Vytvoření připojovacího řetězce a práce s databází SQL Serveru LocalDB</span><span class="sxs-lookup"><span data-stu-id="273ac-102">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="273ac-103">od [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="273ac-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [Tutorial Note](index.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="273ac-104">Vytvoření připojovacího řetězce a práce s databází SQL Serveru LocalDB</span><span class="sxs-lookup"><span data-stu-id="273ac-104">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="273ac-105">Třída `MovieDBContext`, kterou jste vytvořili, zpracovává úlohu připojení k databázi a mapování objektů `Movie` na záznamy databáze.</span><span class="sxs-lookup"><span data-stu-id="273ac-105">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="273ac-106">Jedna otázka, na kterou se můžete zeptat, ale je, jak určit databázi, ke které se bude připojovat.</span><span class="sxs-lookup"><span data-stu-id="273ac-106">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="273ac-107">Nemusíte ve skutečnosti určovat, která databáze se má použít, Entity Framework výchozí bude používat [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span><span class="sxs-lookup"><span data-stu-id="273ac-107">You don't actually have to specify which database to use, Entity Framework will default to using [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span></span> <span data-ttu-id="273ac-108">V této části výslovně přidáte připojovací řetězec do souboru *Web. config* aplikace.</span><span class="sxs-lookup"><span data-stu-id="273ac-108">In this section we'll explicitly add a connection string in the *Web.config* file of the application.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="273ac-109">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="273ac-109">SQL Server Express LocalDB</span></span>

<span data-ttu-id="273ac-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) je zjednodušená verze databázového stroje SQL Server Express, která se spouští na vyžádání a běží v uživatelském režimu.</span><span class="sxs-lookup"><span data-stu-id="273ac-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) is a lightweight version of the SQL Server Express Database Engine that starts on demand and runs in user mode.</span></span> <span data-ttu-id="273ac-111">LocalDB se spouští ve speciálním režimu provádění SQL Server Express, který umožňuje pracovat s databázemi jako se soubory *. mdf* .</span><span class="sxs-lookup"><span data-stu-id="273ac-111">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="273ac-112">Soubory databáze LocalDB jsou obvykle uloženy ve složce *App\_data* webového projektu.</span><span class="sxs-lookup"><span data-stu-id="273ac-112">Typically, LocalDB database files are kept in the *App\_Data* folder of a web project.</span></span>

<span data-ttu-id="273ac-113">SQL Server Express se nedoporučuje používat v produkčních webových aplikacích.</span><span class="sxs-lookup"><span data-stu-id="273ac-113">SQL Server Express is not recommended for use in production web applications.</span></span> <span data-ttu-id="273ac-114">LocalDB by se neměl používat pro produkční prostředí s webovou aplikací, protože není navržená pro práci se službou IIS.</span><span class="sxs-lookup"><span data-stu-id="273ac-114">LocalDB in particular should not be used for production with a web application because it is not designed to work with IIS.</span></span> <span data-ttu-id="273ac-115">Databázi LocalDB je však možné snadno migrovat do SQL Server nebo SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="273ac-115">However, a LocalDB database can be easily migrated to SQL Server or SQL Azure.</span></span>

<span data-ttu-id="273ac-116">V aplikaci Visual Studio 2017 se LocalDB nainstaluje ve výchozím nastavení pomocí sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="273ac-116">In Visual Studio 2017, LocalDB is installed by default with Visual Studio.</span></span>

<span data-ttu-id="273ac-117">Ve výchozím nastavení Entity Framework vyhledá připojovací řetězec s názvem stejný jako třída kontextu objektu (`MovieDBContext` pro tento projekt).</span><span class="sxs-lookup"><span data-stu-id="273ac-117">By default, the Entity Framework looks for a connection string named the same as the object context class (`MovieDBContext` for this project).</span></span> <span data-ttu-id="273ac-118">Další informace najdete v tématu [SQL Server připojovacích řetězců pro webové aplikace ASP.NET](https://msdn.microsoft.com/library/jj653752.aspx).</span><span class="sxs-lookup"><span data-stu-id="273ac-118">For more information see [SQL Server Connection Strings for ASP.NET Web Applications](https://msdn.microsoft.com/library/jj653752.aspx).</span></span>

<span data-ttu-id="273ac-119">Otevřete soubor *Web. config* v kořenovém adresáři aplikace.</span><span class="sxs-lookup"><span data-stu-id="273ac-119">Open the application root *Web.config* file shown below.</span></span> <span data-ttu-id="273ac-120">(Ne soubor *Web. config* ve složce *views* .)</span><span class="sxs-lookup"><span data-stu-id="273ac-120">(Not the *Web.config* file in the *Views* folder.)</span></span>

![](creating-a-connection-string/_static/image1.png)

<span data-ttu-id="273ac-121">Vyhledejte prvek `<connectionStrings>`:</span><span class="sxs-lookup"><span data-stu-id="273ac-121">Find the `<connectionStrings>` element:</span></span>

![](creating-a-connection-string/_static/image2.png)

<span data-ttu-id="273ac-122">Přidejte následující připojovací řetězec do prvku `<connectionStrings>` v souboru *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="273ac-122">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

<span data-ttu-id="273ac-123">Následující příklad ukazuje část souboru *Web. config* s přidaným novým připojovacím řetězcem:</span><span class="sxs-lookup"><span data-stu-id="273ac-123">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

<span data-ttu-id="273ac-124">Dva připojovací řetězce jsou velmi podobné.</span><span class="sxs-lookup"><span data-stu-id="273ac-124">The two connection strings are very similar.</span></span> <span data-ttu-id="273ac-125">První připojovací řetězec má název `DefaultConnection` a slouží pro databázi členství k řízení toho, kdo má přístup k aplikaci.</span><span class="sxs-lookup"><span data-stu-id="273ac-125">The first connection string is named `DefaultConnection` and is used for the membership database to control who can access the application.</span></span> <span data-ttu-id="273ac-126">Připojovací řetězec, který jste přidali, určuje databázi LocalDB s názvem *film. mdf* umístěnou ve složce *App\_data* .</span><span class="sxs-lookup"><span data-stu-id="273ac-126">The connection string you've added specifies a LocalDB database named *Movie.mdf* located in the *App\_Data* folder.</span></span> <span data-ttu-id="273ac-127">V tomto kurzu nebudeme používat databázi členství. Další informace o členství, ověřování a zabezpečení najdete v části můj kurz [Vytvoření aplikace ASP.NET MVC s ověřováním a SQL DB a nasazením do Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="273ac-127">We won't use the membership database in this tutorial, for more information on membership, authentication and security, see my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>

<span data-ttu-id="273ac-128">Název připojovacího řetězce se musí shodovat s názvem třídy [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) .</span><span class="sxs-lookup"><span data-stu-id="273ac-128">The name of the connection string must match the name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class.</span></span>

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

<span data-ttu-id="273ac-129">Nemusíte ve skutečnosti přidávat připojovací řetězec `MovieDBContext`.</span><span class="sxs-lookup"><span data-stu-id="273ac-129">You don't actually need to add the `MovieDBContext` connection string.</span></span> <span data-ttu-id="273ac-130">Pokud nezadáte připojovací řetězec, Entity Framework vytvoří databázi LocalDB v adresáři Users s plně kvalifikovaným názvem třídy [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) (v tomto případě `MvcMovie.Models.MovieDBContext`).</span><span class="sxs-lookup"><span data-stu-id="273ac-130">If you don't specify a connection string, Entity Framework will create a LocalDB database in the users directory with the fully qualified name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class (in this case `MvcMovie.Models.MovieDBContext`).</span></span> <span data-ttu-id="273ac-131">Databázi můžete pojmenovat cokoli, co chcete, pokud má *.* Přípona MDF.</span><span class="sxs-lookup"><span data-stu-id="273ac-131">You can name the database anything you like, as long as it has the *.MDF* suffix.</span></span> <span data-ttu-id="273ac-132">Například můžeme pojmenovat databázi *MyFilms. mdf*.</span><span class="sxs-lookup"><span data-stu-id="273ac-132">For example, we could name the database *MyFilms.mdf*.</span></span>

<span data-ttu-id="273ac-133">V dalším kroku vytvoříte novou třídu `MoviesController`, kterou můžete použít k zobrazení dat filmu a umožníte uživatelům vytvářet nové seznamy filmů.</span><span class="sxs-lookup"><span data-stu-id="273ac-133">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="273ac-134">[Předchozí](adding-a-model.md)
> [Další](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="273ac-134">[Previous](adding-a-model.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
