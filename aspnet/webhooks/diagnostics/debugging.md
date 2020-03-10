---
uid: webhooks/diagnostics/debugging
title: Ladění webhooků ASP.NET | Microsoft Docs
author: rick-anderson
description: Jak ladit Webhooky ASP.NET
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 517d282fc22703b5861b748aea51023fa0a12a26
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640866"
---
# <a name="aspnet-webhooks-debugging"></a>Ladění webhooků ASP.NET  

## <a name="debugging-in-azure"></a>Ladění v Azure

Chcete-li ladit webovou aplikaci při spuštění v Azure, přečtěte si kurz [řešení potíží s webovou aplikací v Azure App Service pomocí sady Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).

## <a name="debugging-with-source-and-symbols"></a>Ladění pomocí zdrojů a symbolů

Kromě ladění vlastního kódu je možné provést ladění přímo do Microsoft ASP.NET webhooků a ve skutečnosti na rozhraní .NET. To funguje bez ohledu na to, zda je místní nebo vzdálené ladění. Nejdřív nakonfigurujte Visual Studio tak, aby bylo možné najít zdroj a symboly, a to tak, že kliknete na **ladění** a pak na **Možnosti a nastavení**. Nastavte následující možnosti:

![Možnosti a nastavení](_static/SourceSymbols.png)

Pak přidejte odkaz na [symbolsource.org](http://symbolsource.org) pro stažení zdroje a symbolů. Přejděte na kartu **symboly** v nabídce výše a přidejte následující jako umístění symbolu:

```
http://srv.symbolsource.org/pdb/Public
```

Kromě toho se ujistěte, že adresář mezipaměti má krátký název; jinak názvy souborů mohou být příliš dlouhé, což způsobí, že symboly nebudou načteny. Vzorová cesta:

```
C:\SymCache
```

Nastavení by mělo vypadat podobně jako toto:

![Možnosti příklad umístění souboru se symboly](_static/SymSource.png)
