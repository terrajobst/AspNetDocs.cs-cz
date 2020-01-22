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
ms.openlocfilehash: d3c6e736c5dcf4a3615e3c72cfc033effc7cc8e6
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519307"
---
# <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>Vytvoření připojovacího řetězce a práce s databází SQL Serveru LocalDB

od [Rick Anderson]((https://twitter.com/RickAndMSFT))

[!INCLUDE [Tutorial Note](index.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>Vytvoření připojovacího řetězce a práce s databází SQL Serveru LocalDB

Třída `MovieDBContext`, kterou jste vytvořili, zpracovává úlohu připojení k databázi a mapování objektů `Movie` na záznamy databáze. Jedna otázka, na kterou se můžete zeptat, ale je, jak určit databázi, ke které se bude připojovat. Nemusíte ve skutečnosti určovat, která databáze se má použít, Entity Framework výchozí bude používat [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb). V této části výslovně přidáte připojovací řetězec do souboru *Web. config* aplikace.

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) je zjednodušená verze databázového stroje SQL Server Express, která se spouští na vyžádání a běží v uživatelském režimu. LocalDB se spouští ve speciálním režimu provádění SQL Server Express, který umožňuje pracovat s databázemi jako se soubory *. mdf* . Soubory databáze LocalDB jsou obvykle uloženy ve složce *App\_data* webového projektu.

SQL Server Express se nedoporučuje používat v produkčních webových aplikacích. LocalDB by se neměl používat pro produkční prostředí s webovou aplikací, protože není navržená pro práci se službou IIS. Databázi LocalDB je však možné snadno migrovat do SQL Server nebo SQL Azure.

V aplikaci Visual Studio 2017 se LocalDB nainstaluje ve výchozím nastavení pomocí sady Visual Studio.

Ve výchozím nastavení Entity Framework vyhledá připojovací řetězec s názvem stejný jako třída kontextu objektu (`MovieDBContext` pro tento projekt). Další informace najdete v tématu [SQL Server připojovacích řetězců pro webové aplikace ASP.NET](https://msdn.microsoft.com/library/jj653752.aspx).

Otevřete soubor *Web. config* v kořenovém adresáři aplikace. (Ne soubor *Web. config* ve složce *views* .)

![](creating-a-connection-string/_static/image1.png)

Vyhledejte prvek `<connectionStrings>`:

![](creating-a-connection-string/_static/image2.png)

Přidejte následující připojovací řetězec do prvku `<connectionStrings>` v souboru *Web. config* .

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

Následující příklad ukazuje část souboru *Web. config* s přidaným novým připojovacím řetězcem:

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

Dva připojovací řetězce jsou velmi podobné. První připojovací řetězec má název `DefaultConnection` a slouží pro databázi členství k řízení toho, kdo má přístup k aplikaci. Připojovací řetězec, který jste přidali, určuje databázi LocalDB s názvem *film. mdf* umístěnou ve složce *App\_data* . V tomto kurzu nebudeme používat databázi členství. Další informace o členství, ověřování a zabezpečení najdete v části můj kurz [Vytvoření aplikace ASP.NET MVC s ověřováním a SQL DB a nasazením do Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).

Název připojovacího řetězce se musí shodovat s názvem třídy [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) .

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

Nemusíte ve skutečnosti přidávat připojovací řetězec `MovieDBContext`. Pokud nezadáte připojovací řetězec, Entity Framework vytvoří databázi LocalDB v adresáři Users s plně kvalifikovaným názvem třídy [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) (v tomto případě `MvcMovie.Models.MovieDBContext`). Databázi můžete pojmenovat cokoli, co chcete, pokud má *.* Přípona MDF. Například můžeme pojmenovat databázi *MyFilms. mdf*.

V dalším kroku vytvoříte novou třídu `MoviesController`, kterou můžete použít k zobrazení dat filmu a umožníte uživatelům vytvářet nové seznamy filmů.

> [!div class="step-by-step"]
> [Předchozí](adding-a-model.md)
> [Další](accessing-your-models-data-from-a-controller.md)
