---
ms.openlocfilehash: 96cd8c78178b02ad3eb4a471540950b4581af583
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57068632"
---
# <a name="gdpr-sample"></a><span data-ttu-id="909b1-101">Ukázka GDPR</span><span class="sxs-lookup"><span data-stu-id="909b1-101">GDPR Sample</span></span>

* <span data-ttu-id="909b1-102">V *appsettings.json*, nastavte `CheckNotConsentNeeded` k `false` vyžadovat souhlas; v opačném případě nastavte na hodnotu true nebo vynechejte.</span><span class="sxs-lookup"><span data-stu-id="909b1-102">In *appsettings.json*, set `CheckNotConsentNeeded` to `false` to require consent; otherwise set to true or omit.</span></span> <span data-ttu-id="909b1-103">Testování aplikace s `CheckNotConsentNeeded` nastavena na `false` a nastavte na `true`.</span><span class="sxs-lookup"><span data-stu-id="909b1-103">Test the app with `CheckNotConsentNeeded` set to `false` and set to `true`.</span></span>
* <span data-ttu-id="909b1-104">Vytvoření základní a které není nezbytné soubory cookie s každou změnu `CheckConsentNeeded` a udělit souhlas.</span><span class="sxs-lookup"><span data-stu-id="909b1-104">Create essential and non-essential cookies with each variation of `CheckConsentNeeded` and consent granted.</span></span>
* <span data-ttu-id="909b1-105">Registrace uživatele.</span><span class="sxs-lookup"><span data-stu-id="909b1-105">Register a user.</span></span>
* <span data-ttu-id="909b1-106">Odstranění souborů cookie.</span><span class="sxs-lookup"><span data-stu-id="909b1-106">Delete cookies.</span></span>
