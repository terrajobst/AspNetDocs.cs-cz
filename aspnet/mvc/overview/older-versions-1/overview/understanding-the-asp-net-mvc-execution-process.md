---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: Principy procesu provádění ASP.NET MVC | Microsoft Docs
author: microsoft
description: Přečtěte si, jak rozhraní ASP.NET MVC zpracovává požadavky prohlížeče krok za krokem.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 28940947253e0af43886cf1231f8aaf4615526cc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541515"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a>Principy procesu spuštění ASP.NET MVC

od [Microsoftu](https://github.com/microsoft)

> Přečtěte si, jak rozhraní ASP.NET MVC zpracovává požadavky prohlížeče krok za krokem.

Požadavky na webovou aplikaci založenou na ASP.NET MVC se nejdřív procházejí objektem **UrlRoutingModule** , který je modulem http. Tento modul analyzuje požadavek a provede výběr směrování. Objekt **UrlRoutingModule** vybere první objekt směrování, který odpovídá aktuálnímu požadavku. (Objekt směrování je třída, která implementuje **RouteBase**a je obvykle instancí třídy **Směrování** .) Pokud se žádné trasy neshodují, objekt **UrlRoutingModule** neprovede žádnou akci a umožní, aby se požadavek vrátil do normálního zpracování žádosti ASP.NET nebo služby IIS.

Z vybraného objektu **Směrování** Získá objekt **UrlRoutingModule** objekt **IRouteHandler** , který je spojen s objektem **Směrování** . Obvykle se v aplikaci MVC jedná o instanci **MvcRouteHandler**. Instance **IRouteHandler** vytvoří objekt **IHttpHandler** a předá ho objektu **IHttpContext** . Ve výchozím nastavení je instance **IHttpHandler** pro MVC objektem **MvcHandler** . Objekt **MvcHandler** pak vybere kontroler, který požadavek nakonec zpracuje.

> [!NOTE]
> Když webová aplikace MVC v ASP.NET běží ve službě IIS 7,0, není pro projekty MVC potřeba žádná přípona názvu souboru. Ve službě IIS 6,0 však obslužná rutina vyžaduje mapování názvu souboru. Mvc na knihovnu DLL ASP.NET ISAPI.

Modul a obslužná rutina jsou vstupními body rozhraní ASP.NET MVC. Provádějí tyto akce:

- Vyberte příslušný kontroler ve webové aplikaci MVC.
- Získat konkrétní instanci kontroleru.
- Zavolejte metodu **Execute** řadiče.

Následující seznam obsahuje fáze provádění pro webový projekt MVC:

- Přijetí první žádosti o aplikaci 

    - V souboru Global. asax jsou objekty **Směrování** přidány do objektu **Route** .
- Provést směrování 

    - Modul **UrlRoutingModule** používá první vyhovující objekt **Směrování** **v kolekci metody** pro vytvoření objektu **parametr RouteData** , který potom používá k vytvoření objektu **Třída requestContext** (**IHttpContext**).
- Obslužná rutina žádosti o vytvoření MVC 

    - Objekt **MvcRouteHandler** vytvoří instanci třídy **MvcHandler** a předá ji instanci **Třída requestContext** .
- Vytvořit kontroler 

    - Objekt **MvcHandler** používá instanci **Třída requestContext** k identifikaci objektu **IControllerFactory** (obvykle instancí třídy **DefaultControllerFactory** ) k vytvoření instance kontroleru pomocí.
- Spustit kontroler – instance **MvcHandler** volá metodu **Execute** příkazu Controller. |
- Vyvolat akci 

    - Většina řadičů dědí ze základní třídy **řadiče** . Pro řadiče, které to dělají, určí objekt **ControllerActionInvoker** , který je přidružen k řadiči, metodu Action třídy Controller, která má být volána, a poté zavolá tuto metodu.
- Výsledek provedení 

    - Typická metoda Action může obdržet uživatelský vstup, připravit příslušná data odpovědi a pak výsledek spustit vrácením typu výsledku. Předdefinované typy výsledků, které lze provést, zahrnují následující: **ViewResult** (který vykresluje zobrazení a je nejčastěji používaný výsledný typ), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**a **EmptyResult**.
