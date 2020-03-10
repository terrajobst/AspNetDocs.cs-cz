---
uid: web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
title: '[How Do I]: Persist the State of a User Control During a Postback | Microsoft Docs'
author: rick-anderson
description: V tomto videu Chris pixelů na ukazuje, jak zachovat stav jednoho nebo více objektů v uživatelském ovládacím prvku. Nejprve je vytvořen uživatelský ovládací prvek, který představuje abilit...
ms.author: riande
ms.date: 04/02/2009
ms.assetid: d1bca4c6-838c-40f7-87ec-80bb67e483e5
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
msc.type: video
ms.openlocfilehash: c87bd6c5c993a1bde8f8a84f6d53b431e54541d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78635819"
---
# <a name="how-do-i-persist-the-state-of-a-user-control-during-a-postback"></a>[Jak mám]: zachovat stav uživatelského ovládacího prvku během postbacku
[How Do I]: Persist the State of a User Control During a Postback

<span data-ttu-id="e9cef-104">autor – [Chris pixelů na](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="e9cef-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="e9cef-105">V tomto videu Chris pixelů na ukazuje, jak zachovat stav jednoho nebo více objektů v uživatelském ovládacím prvku.</span><span class="sxs-lookup"><span data-stu-id="e9cef-105">In this video Chris Pels shows how to persist the state of one or more objects in a user control.</span></span> <span data-ttu-id="e9cef-106">Nejprve je vytvořen uživatelský ovládací prvek, který představuje schopnost uživateli zadat kritéria filtru pro hledání.</span><span class="sxs-lookup"><span data-stu-id="e9cef-106">First, a user control is created that represents the ability for a user to specify filter criteria for a search.</span></span> <span data-ttu-id="e9cef-107">Kromě toho je vytvořena třída doprovodného filtru pro ukládání informací o filtru.</span><span class="sxs-lookup"><span data-stu-id="e9cef-107">In addition, a companion Filter class is created to store the filter information.</span></span> <span data-ttu-id="e9cef-108">Několik prvků uživatelského rozhraní je přidáno do ovládacího prvku filtru spolu s některými metodami a vlastnostmi pro uložení aktuálních informací o filtru v instanci třídy filtru.</span><span class="sxs-lookup"><span data-stu-id="e9cef-108">Several user interface elements are added to the filter control along with some methods and properties to store the current filter information in the Filter class instance.</span></span> <span data-ttu-id="e9cef-109">V dalším kroku je trvalost uživatelského ovládacího prvku implementováno pomocí metody RegisterRequiresControlState a přidružených metod Save/Restore.</span><span class="sxs-lookup"><span data-stu-id="e9cef-109">Next, the user control persistence is implemented using the RegisterRequiresControlState method and associated Save/Restore methods.</span></span> <span data-ttu-id="e9cef-110">Tyto metody ukládají instanci třídy Filter a její data během postbacků stránky.</span><span class="sxs-lookup"><span data-stu-id="e9cef-110">These methods store the instance of the filter class and its data during page postbacks.</span></span> <span data-ttu-id="e9cef-111">Nakonec existuje diskuze o tom, jak uložit více objektů v implementaci stavu ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="e9cef-111">Finally, there is a discussion of how to store multiple objects in control state implementation.</span></span>

[<span data-ttu-id="e9cef-112">&#9654;Přehrát video (23 minut)</span><span class="sxs-lookup"><span data-stu-id="e9cef-112">&#9654; Watch video (23 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-persist-the-state-of-a-user-control-during-a-postback)
