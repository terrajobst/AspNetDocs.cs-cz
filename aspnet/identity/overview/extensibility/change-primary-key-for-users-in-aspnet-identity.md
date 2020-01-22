---
uid: identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
title: Změna primárního klíče pro uživatele v ASP.NET Identity-ASP.NET 4. x
author: Rick-Anderson
description: V Visual Studio 2013 výchozí webová aplikace používá pro klíč pro uživatelské účty řetězcovou hodnotu. ASP.NET Identity umožňuje změnit typ...
ms.author: riande
ms.date: 09/30/2014
ms.assetid: 44925849-5762-4504-a8cd-8f0cd06f6dc3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0afea8eacfc646f1489b87629fdb2d437815d88c
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519138"
---
# <a name="change-primary-key-for-users-in-aspnet-identity"></a>Změna primárního klíče uživatelů v ASP.NET Identity

podle [Tom FitzMacken](https://github.com/tfitzmac)

> V Visual Studio 2013 výchozí webová aplikace používá pro klíč pro uživatelské účty řetězcovou hodnotu. ASP.NET Identity umožňuje změnit typ klíče tak, aby splňoval požadavky na data. Například můžete změnit typ klíče z řetězce na celé číslo.
> 
> V tomto tématu se dozvíte, jak začít s výchozí webovou aplikací a jak změnit klíč uživatelského účtu na celé číslo. Stejné úpravy můžete použít k implementaci libovolného typu klíče v projektu. Ukazuje, jak provést tyto změny ve výchozí webové aplikaci, ale můžete použít podobné změny v přizpůsobené aplikaci. Zobrazuje změny potřebné při práci s MVC nebo webovými formuláři.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Visual Studio 2013 s aktualizací Update 2 (nebo novější)
> - ASP.NET Identity 2,1 nebo novější

K provedení kroků v tomto kurzu musíte mít Visual Studio 2013 Update 2 (nebo novější) a webovou aplikaci vytvořenou v šabloně webové aplikace ASP.NET. Šablona se změnila ve Update 3. V tomto tématu se dozvíte, jak změnit šablonu v Update 2 a Update 3.

Toto téma obsahuje následující oddíly:

- [Změna typu klíče ve třídě uživatele identity](#userclass)
- [Přidat přizpůsobené třídy identity, které používají typ klíče](#customclass)
- [Změna třídy kontextu a Správce uživatelů na použití typu klíče](#context)
- [Změna spouštěcí konfigurace tak, aby používala typ klíče](#startup)
- [V případě MVC s aktualizací Update 2 změňte AccountController tak, aby předával typ klíče.](#mvcupdate2)
- [Pro MVC s aktualizací Update 3 změňte AccountController a ManageController, aby se předal typ klíče.](#mvcupdate3)
- [U webových formulářů s aktualizací Update 2 změňte stránky účtu, aby předávaly typ klíče.](#webformsupdate2)
- [U webových formulářů s aktualizací Update 3 změňte stránky účtu, aby předávaly typ klíče.](#webformsupdate3)
- [Spustit aplikaci](#run)
- [Další materiály](#other)

<a id="userclass"></a>
## <a name="change-the-type-of-the-key-in-the-identity-user-class"></a>Změna typu klíče ve třídě uživatele identity

V projektu vytvořeném pomocí šablony webové aplikace ASP.NET určete, že třída ApplicationUser používá pro klíč uživatelských účtů celé číslo. V IdentityModels.cs změňte třídu ApplicationUser na dědění z IdentityUser, která má typ **int** pro obecný parametr TKey. Také předáte názvy tří přizpůsobených tříd, které ještě nebyly implementovány.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample1.cs?highlight=1-2)]

Změnili jste typ klíče, ale ve výchozím nastavení zbývající část aplikace stále předpokládá, že klíč je řetězec. Je nutné explicitně určit typ klíče v kódu, který předpokládá řetězec.

Ve třídě **ApplicationUser** změňte metodu **GenerateUserIdentityAsync** tak, aby zahrnovala int, jak je znázorněno ve zvýrazněném kódu níže. Tato změna není nutná pro projekty webových formulářů se šablonou Update 3.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample2.cs?highlight=2)]

<a id="customclass"></a>
## <a name="add-customized-identity-classes-that-use-the-key-type"></a>Přidat přizpůsobené třídy identity, které používají typ klíče

Ostatní třídy identity, například IdentityUserRole, IdentityUserClaim, IdentityUserLogin, IdentityRole, UserStore, RoleStore, jsou stále nastaveny tak, aby používaly řetězcový klíč. Vytvořte nové verze těchto tříd, které určují celé číslo pro klíč. V těchto třídách nemusíte poskytovat mnohem implementační kód, primárně je pouze nastavení int jako klíč.

Do souboru IdentityModels.cs přidejte následující třídy.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample3.cs)]

<a id="context"></a>
## <a name="change-the-context-class-and-user-manager-to-use-the-key-type"></a>Změna třídy kontextu a Správce uživatelů na použití typu klíče

V IdentityModels.cs změňte definici třídy **ApplicationDbContext** tak, aby používala vaše nové přizpůsobené třídy a **int** pro klíč, jak je znázorněno ve zvýrazněném kódu.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample4.cs?highlight=1-2)]

Parametr ThrowIfV1Schema již v konstruktoru není platný. Změňte konstruktor tak, aby nepředával hodnotu ThrowIfV1Schema.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample5.cs)]

Otevřete IdentityConfig.cs a změňte třídu **ApplicationUserManger** tak, aby používala novou třídu úložiště uživatele pro trvalá data a **int** pro klíč.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample6.cs?highlight=1,3,12,14,32,37,48)]

V šabloně Update 3 je třeba změnit třídu ApplicationSignInManager.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample7.cs?highlight=1)]

<a id="startup"></a>
## <a name="change-start-up-configuration-to-use-the-key-type"></a>Změna spouštěcí konfigurace tak, aby používala typ klíče

V Startup.Auth.cs nahraďte kód OnValidateIdentity, jak je zvýrazněno níže. Všimněte si, že definice getUserIdCallback analyzuje řetězcovou hodnotu na celé číslo.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample8.cs?highlight=7-12)]

Pokud váš projekt nerozpozná obecnou implementaci metody **GetUserID** , budete možná muset aktualizovat balíček NuGet ASP.NET identity na verzi 2,1.

Vytvořili jste spoustu změn tříd infrastruktury, které používá ASP.NET Identity. Pokud se pokusíte zkompilovat projekt, všimnete si velkého množství chyb. Naštěstí jsou všechny zbývající chyby podobné. Třída identity očekává pro klíč celé číslo, ale kontroler (nebo webový formulář) předává řetězcovou hodnotu. V každém případě je nutné převést řetězec na celé číslo a voláním metody **GetUserID&lt;int&gt;** . Můžete buď pracovat se seznamem chyb z kompilace, nebo provést následující změny.

Zbývající změny závisí na typu vytvářeného projektu a na aktualizaci, kterou jste nainstalovali v aplikaci Visual Studio. Pomocí následujících odkazů můžete přejít přímo k příslušné části

- [V případě MVC s aktualizací Update 2 změňte AccountController tak, aby předával typ klíče.](#mvcupdate2)
- [Pro MVC s aktualizací Update 3 změňte AccountController a ManageController, aby se předal typ klíče.](#mvcupdate3)
- [U webových formulářů s aktualizací Update 2 změňte stránky účtu, aby předávaly typ klíče.](#webformsupdate2)
- [U webových formulářů s aktualizací Update 3 změňte stránky účtu, aby předávaly typ klíče.](#webformsupdate3)

<a id="mvcupdate2"></a>
## <a name="for-mvc-with-update-2-change-the-accountcontroller-to-pass-the-key-type"></a>V případě MVC s aktualizací Update 2 změňte AccountController tak, aby předával typ klíče.

Otevřete soubor AccountController.cs. Je potřeba změnit následující metody.

Metoda **ConfirmEmail**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample9.cs?highlight=1,3)]

**Zrušit přidružení** metody

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample10.cs?highlight=5,9)]

**Manage (ManageUserViewModel)** – metoda

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample11.cs?highlight=11,17,41)]

Metoda **LinkLoginCallback**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample12.cs?highlight=10)]

Metoda **RemoveAccountList**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample13.cs?highlight=3)]

Metoda **HasPassword**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample14.cs?highlight=3)]

Nyní můžete [Spustit aplikaci](#run) a zaregistrovat nového uživatele.

<a id="mvcupdate3"></a>
## <a name="for-mvc-with-update-3-change-the-accountcontroller-and-managecontroller-to-pass-the-key-type"></a>Pro MVC s aktualizací Update 3 změňte AccountController a ManageController, aby se předal typ klíče.

Otevřete soubor AccountController.cs. Je třeba změnit následující metodu.

Metoda **ConfirmEmail**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample15.cs?highlight=1,3)]

Metoda **SendCode**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample16.cs?highlight=4)]

Otevřete soubor ManageController.cs. Je potřeba změnit následující metody.

**Index** – metoda

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample17.cs?highlight=15-17)]

Metody **RemoveLogin**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample18.cs?highlight=3,13,17)]

Metoda **AddPhoneNumber**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample19.cs?highlight=9)]

Metoda **EnableTwoFactorAuthentication**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample20.cs?highlight=3-4)]

Metoda **DisableTwoFactorAuthentication**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample21.cs?highlight=3-4)]

Metody **VerifyPhoneNumber**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample22.cs?highlight=4,18,21)]

Metoda **RemovePhoneNumber**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample23.cs?highlight=3,8)]

**ChangePassword** – metoda

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample24.cs?highlight=10,13)]

Metoda **SetPassword**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample25.cs?highlight=5,8)]

Metoda **ManageLogins**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample26.cs?highlight=7,12)]

Metoda **LinkLoginCallback**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample27.cs?highlight=8)]

Metoda **HasPassword**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample28.cs?highlight=3)]

Metoda **HasPhoneNumber**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample29.cs?highlight=3)]

Nyní můžete [Spustit aplikaci](#run) a zaregistrovat nového uživatele.

<a id="webformsupdate2"></a>
## <a name="for-web-forms-with-update-2-change-account-pages-to-pass-the-key-type"></a>U webových formulářů s aktualizací Update 2 změňte stránky účtu, aby předávaly typ klíče.

U webových formulářů s aktualizací Update 2 je třeba změnit následující stránky.

**Confirm.aspx.cx**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample30.cs?highlight=8)]

**RegisterExternalLogin.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample31.cs?highlight=36)]

**Manage.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample32.cs?highlight=3,22,47,52,69,85,93,98)]

Nyní můžete [Spustit aplikaci](#run) a zaregistrovat nového uživatele.

<a id="webformsupdate3"></a>
## <a name="for-web-forms-with-update-3-change-account-pages-to-pass-the-key-type"></a>U webových formulářů s aktualizací Update 3 změňte stránky účtu, aby předávaly typ klíče.

U webových formulářů s aktualizací Update 3 je třeba změnit následující stránky.

**Confirm.aspx.cx**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample33.cs?highlight=8)]

**RegisterExternalLogin.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample34.cs?highlight=36)]

**Manage.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample35.cs?highlight=11,27,32,34,82,87,99,108)]

**VerifyPhoneNumber.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample36.cs?highlight=8,23,27)]

**AddPhoneNumber.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample37.cs?highlight=7)]

**ManagePassword.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample38.cs?highlight=11,47,50,68)]

**ManageLogins.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample39.cs?highlight=16,23,32,41,45)]

**TwoFactorAuthenticationSignIn.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample40.cs?highlight=14-15,29,53)]

<a id="run"></a>
## <a name="run-application"></a>Spustit aplikaci

Dokončili jste všechny požadované změny v šabloně výchozí webové aplikace. Spusťte aplikaci a zaregistrujte nového uživatele. Po registraci uživatele si všimněte, že tabulka AspNetUsers má sloupec ID, který je celé číslo.

![nový primární klíč](change-primary-key-for-users-in-aspnet-identity/_static/image1.png)

Pokud jste již dříve vytvořili ASP.NET Identity tabulky s jiným primárním klíčem, je nutné provést další změny. Pokud je to možné, stačí odstranit stávající databázi. Databáze bude znovu vytvořena se správným návrhem při spuštění webové aplikace a přidání nového uživatele. Pokud není možné odstranit, spusťte migraci Code First pro změnu tabulek. Nový celočíselný primární klíč ale nebude nastaven jako vlastnost IDENTITY SQL v databázi. Sloupec ID je nutné ručně nastavit jako IDENTITU.

<a id="other"></a>
## <a name="other-resources"></a>Další zdroje

- [Přehled poskytovatelů vlastního úložiště pro ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md)
- [Migrace stávajícího webu z členství SQL na ASP.NET Identity](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [Migrace dat Universal Provider pro členství a profily uživatelů do ASP.NET Identity](../migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity.md)
- [Ukázková aplikace](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK) se změněným primárním klíčem
