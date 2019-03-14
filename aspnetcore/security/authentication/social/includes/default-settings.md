---
ms.openlocfilehash: a7be92adffc06ac0f25b84ea15d1a8c4896f4f9d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57168625"
---
<!--Don't update this for 2.2, use the 2.2 version --> Volání [AddIdentity](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionuiextensions.adddefaultidentity) nakonfiguruje výchozí nastavení schéma. [AddAuthentication(String)](/dotnet/api/microsoft.extensions.dependencyinjection.authenticationservicecollectionextensions.addauthentication#Microsoft_Extensions_DependencyInjection_AuthenticationServiceCollectionExtensions_AddAuthentication_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_String_) přetížení sad [DefaultScheme](/dotnet/api/microsoft.aspnetcore.authentication.authenticationoptions.defaultscheme) vlastnost. [AddAuthentication (akce&lt;AuthenticationOptions&gt;)](/dotnet/api/microsoft.extensions.dependencyinjection.authenticationservicecollectionextensions.addauthentication#Microsoft_Extensions_DependencyInjection_AuthenticationServiceCollectionExtensions_AddAuthentication_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_Action_Microsoft_AspNetCore_Authentication_AuthenticationOptions__) přetížení umožňuje konfigurovat možnosti ověřování, které je možné použít k nastavení výchozí schémata ověřování pro různé účely. Následující volání `AddAuthentication` přepsání, které jste dříve nakonfigurovali [AuthenticationOptions](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions) vlastnosti.

[AuthenticationBuilder](/dotnet/api/microsoft.aspnetcore.authentication.authenticationbuilder) rozšiřující metody, které se zaregistrovat obslužnou rutinu ověřování může být volána pouze jednou za schéma ověřování. Existují přetížení, které umožňují konfiguraci vlastností schéma, název schématu a zobrazovaný název.