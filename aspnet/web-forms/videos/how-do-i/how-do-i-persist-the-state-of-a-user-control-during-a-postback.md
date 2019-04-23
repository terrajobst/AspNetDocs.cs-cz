---
uid: web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
title: '[How Do I]: Persist the State of a User Control During a Postback | Microsoft Docs'
author: rick-anderson
description: V toto video pixelů na Chris ukazuje, jak k uložení stavu jednoho nebo více objektů do uživatelského ovládacího prvku. Nejprve se vytvoří uživatelský ovládací prvek, který představuje abilit...
ms.author: riande
ms.date: 04/02/2009
ms.assetid: d1bca4c6-838c-40f7-87ec-80bb67e483e5
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
msc.type: video
ms.openlocfilehash: c87bd6c5c993a1bde8f8a84f6d53b431e54541d9
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59414774"
---
# <a name="how-do-i-persist-the-state-of-a-user-control-during-a-postback"></a>[Jak na to]: Zachování stavu uživatelského ovládacího prvku během události zpětného odeslání (postback)
[How Do I]: Persist the State of a User Control During a Postback

<span data-ttu-id="47d26-104">podle [Chris pixelů na](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="47d26-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="47d26-105">V toto video pixelů na Chris ukazuje, jak k uložení stavu jednoho nebo více objektů do uživatelského ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="47d26-105">In this video Chris Pels shows how to persist the state of one or more objects in a user control.</span></span> <span data-ttu-id="47d26-106">Nejprve se vytvoří uživatelský ovládací prvek, který představuje možnost pro uživatele k určení filtrovacích kritérií vyhledávání.</span><span class="sxs-lookup"><span data-stu-id="47d26-106">First, a user control is created that represents the ability for a user to specify filter criteria for a search.</span></span> <span data-ttu-id="47d26-107">Kromě toho doprovodné třídy filtru je vytvořili pro uložení informace o filtru.</span><span class="sxs-lookup"><span data-stu-id="47d26-107">In addition, a companion Filter class is created to store the filter information.</span></span> <span data-ttu-id="47d26-108">Několik prvků uživatelského rozhraní jsou přidány do ovládací prvek filtru spolu s některé metody a vlastnosti, které chcete uložit aktuální informace o filtru ve filtru instance třídy.</span><span class="sxs-lookup"><span data-stu-id="47d26-108">Several user interface elements are added to the filter control along with some methods and properties to store the current filter information in the Filter class instance.</span></span> <span data-ttu-id="47d26-109">Trvalost uživatelského ovládacího prvku v dalším kroku je implementováno pomocí RegisterRequiresControlState metodu a související metody uložit/obnovit.</span><span class="sxs-lookup"><span data-stu-id="47d26-109">Next, the user control persistence is implemented using the RegisterRequiresControlState method and associated Save/Restore methods.</span></span> <span data-ttu-id="47d26-110">Tyto metody ukládání instance třídy filtru a jeho dat během zpětného odeslání stránky.</span><span class="sxs-lookup"><span data-stu-id="47d26-110">These methods store the instance of the filter class and its data during page postbacks.</span></span> <span data-ttu-id="47d26-111">Nakonec je diskusi o tom, jak ukládat více objektů v implementaci stavu ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="47d26-111">Finally, there is a discussion of how to store multiple objects in control state implementation.</span></span>

[<span data-ttu-id="47d26-112">&#9654;Podívejte se na video (23 minut)</span><span class="sxs-lookup"><span data-stu-id="47d26-112">&#9654; Watch video (23 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-persist-the-state-of-a-user-control-during-a-postback)
