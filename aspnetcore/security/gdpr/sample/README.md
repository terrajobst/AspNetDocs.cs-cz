---
ms.openlocfilehash: 96cd8c78178b02ad3eb4a471540950b4581af583
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57068632"
---
# <a name="gdpr-sample"></a>Ukázka GDPR

* V *appsettings.json*, nastavte `CheckNotConsentNeeded` k `false` vyžadovat souhlas; v opačném případě nastavte na hodnotu true nebo vynechejte. Testování aplikace s `CheckNotConsentNeeded` nastavena na `false` a nastavte na `true`.
* Vytvoření základní a které není nezbytné soubory cookie s každou změnu `CheckConsentNeeded` a udělit souhlas.
* Registrace uživatele.
* Odstranění souborů cookie.
