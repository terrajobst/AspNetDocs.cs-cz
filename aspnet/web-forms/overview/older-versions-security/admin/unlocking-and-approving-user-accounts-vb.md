---
uid: web-forms/overview/older-versions-security/admin/unlocking-and-approving-user-accounts-vb
title: Odemknutí a schválení uživatelských účtů (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se dozvíte, jak vytvořit webovou stránku pro správce ke správě stavů uzamčených a schválených uživatelů. Také se dozvíte, jak schvalovat nové uživatele o...
ms.author: riande
ms.date: 04/01/2008
ms.assetid: 041854a5-ea8c-4de0-82f1-121ba6cb2893
msc.legacyurl: /web-forms/overview/older-versions-security/admin/unlocking-and-approving-user-accounts-vb
msc.type: authoredcontent
ms.openlocfilehash: 4a7474676b8f502c583e226678de2b275e0ea3c7
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74590706"
---
# <a name="unlocking-and-approving-user-accounts-vb"></a>Odemykání a schvalování uživatelských účtů (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.14.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial14_UnlockAndApprove_vb.pdf)

> V tomto kurzu se dozvíte, jak vytvořit webovou stránku pro správce ke správě stavů uzamčených a schválených uživatelů. Také se dozvíte, jak schvalovat nové uživatele až po ověření své e-mailové adresy.

## <a name="introduction"></a>Úvod

Spolu s uživatelským jménem, heslem a e-mailem mají každý uživatelský účet dvě pole stavu, která určují, jestli se uživatel může přihlásit k webu: uzamčený a schválený. Uživatel se automaticky uzamkne, pokud zadá neplatné přihlašovací údaje během zadaného počtu minut (výchozí nastavení zamkne uživatele po 5 neplatných pokusů o přihlášení během 10 minut). Schválený stav je užitečný ve scénářích, kdy se musí některá akce stát, než se nový uživatel bude moci přihlásit k webu. Uživatel například může potřebovat nejdřív ověřit e-mailovou adresu nebo ho před přihlášením schválit správce.

Vzhledem k tomu, že se uzamčený nebo neschválený uživatel nemůže přihlásit, je přirozený jenom to, jak se tyto stavy dají resetovat. ASP.NET neobsahuje žádné integrované funkce ani webové ovládací prvky pro správu stavů uzamčených a schválených uživatelů v části, protože tato rozhodnutí je potřeba zpracovat na základě lokality. Některé lokality mohou automaticky schvalovat všechny nové uživatelské účty (výchozí chování). Jiní správci mají schvalovat nové účty nebo neschvalovat uživatele, dokud nenavštíví odkaz odeslaný na e-mailovou adresu, kterou jste zadali při registraci. Podobně některé weby můžou uživatele uzamknout, až správce resetuje stav, zatímco ostatní weby odešlou e-mailem uzamčenému uživateli e-mail s adresou URL, kterou můžou navštívit k odemknutí svého účtu.

V tomto kurzu se dozvíte, jak vytvořit webovou stránku pro správce ke správě stavů uzamčených a schválených uživatelů. Také se dozvíte, jak schvalovat nové uživatele až po ověření své e-mailové adresy.

## <a name="step-1-managing-users-locked-out-and-approved-statuses"></a>Krok 1: Správa stavů uzamčených a schválených uživatelů

<a id="Tutorial12"> </a>V [*sestavování rozhraní pro výběr jednoho uživatelského účtu z mnoha*](building-an-interface-to-select-one-user-account-from-many-vb.md) kurzů jsme sestavili stránku, která uvádí jednotlivé uživatelské účty na stránkovaném a filtrovaném prvku GridView. V mřížce jsou uvedena jména a e-maily jednotlivých uživatelů, jejich schválené a uzamčené stavy, ať už jsou online, a jakékoli komentáře k uživateli. Pokud chcete spravovat stavy schválené a uzamčené pro uživatele, můžeme tuto mřížku upravit. Chcete-li změnit stav schváleného uživatele, správce nejprve vyhledá uživatelský účet a pak upraví odpovídající řádek prvku GridView zaškrtnutím nebo zrušením zaškrtnutí políčka schváleno. Případně můžeme spravovat stavy schválené a uzamčené prostřednictvím samostatné stránky ASP.NET.

V tomto kurzu budeme používat dvě stránky ASP.NET: `ManageUsers.aspx` a `UserInformation.aspx`. Tady je postup, když `ManageUsers.aspx` zobrazuje seznam uživatelských účtů v systému, zatímco `UserInformation.aspx` umožňuje správci spravovat stav schválené a uzamčené pro konkrétního uživatele. Naším prvním pořadím podnikání je rozšíření prvku GridView v `ManageUsers.aspx` tak, aby zahrnovalo HyperLinkField, které se vykresluje jako sloupec odkazů. Chceme, aby každý odkaz odkazoval na `UserInformation.aspx?user=UserName`, kde *username* je jméno uživatele, který chcete upravit.

> [!NOTE]
> Pokud jste si stáhli kód pro <a id="Tutorial13"> </a>kurz [*obnovování a změny hesel*](recovering-and-changing-passwords-vb.md) , možná jste si všimli, že `ManageUsers.aspx` stránka už obsahuje sadu odkazů "spravovat" a stránka `UserInformation.aspx` poskytuje rozhraní pro změnu hesla vybraného uživatele. Rozhodli jste se Nereplikovat tuto funkci v kódu přidruženém k tomuto kurzu, protože fungovalo obcházením rozhraní API pro členství a provozování přímo s databází SQL Server pro změnu hesla uživatele. V tomto kurzu začnete od začátku na stránce `UserInformation.aspx`.

### <a name="adding-manage-links-to-theuseraccountsgridview"></a>Přidání odkazů "spravovat" do`UserAccounts`GridView

Otevřete stránku `ManageUsers.aspx` a přidejte HyperLinkField do `UserAccounts` GridView. Nastavte vlastnost `Text` HyperLinkField na "spravovat" a její `DataNavigateUrlFields` a `DataNavigateUrlFormatString` vlastnosti na `UserName` a "UserInformation. aspx? User ={0}" (v uvedeném pořadí). Tato nastavení konfigurují HyperLinkField tak, aby všechny hypertextové odkazy zobrazovaly text "spravovat", ale každý odkaz předává do řetězce QueryString hodnotu odpovídající *uživatelskému jménu* .

Po přidání HyperLinkField do prvku GridView chvíli počkejte, než se zobrazí stránka `ManageUsers.aspx` v prohlížeči. Jak ukazuje obrázek 1, každý řádek prvku GridView nyní obsahuje odkaz "spravovat". Odkaz "spravovat" pro Bruce odkazuje na `UserInformation.aspx?user=Bruce`, zatímco odkaz "Správa" pro Dave odkazuje na `UserInformation.aspx?user=Dave`.

[![HyperLinkField přidá](unlocking-and-approving-user-accounts-vb/_static/image2.png)](unlocking-and-approving-user-accounts-vb/_static/image1.png)

**Obrázek 1**: HyperLinkField přidá do každého uživatelského účtu odkaz "spravovat" ([kliknutím zobrazíte obrázek v plné velikosti).](unlocking-and-approving-user-accounts-vb/_static/image3.png)

V průběhu chvilky vytvoříme uživatelské rozhraní a kód pro `UserInformation.aspx` stránku, ale nejdřív si nechte mluvit o tom, jak programově změnit stav uzamčeného a schváleného uživatele. [Třída`MembershipUser`](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx) má vlastnosti [`IsLockedOut`](https://msdn.microsoft.com/library/system.web.security.membershipuser.islockedout.aspx) a [`IsApproved`](https://msdn.microsoft.com/library/system.web.security.membershipuser.isapproved.aspx). Vlastnost `IsLockedOut` je určena jen pro čtení. Neexistuje žádný mechanismus pro programové uzamykání uživatele. Chcete-li odemknout uživatele, použijte [metodu`UnlockUser`](https://msdn.microsoft.com/library/system.web.security.membershipuser.unlockuser.aspx)třídy `MembershipUser`. Vlastnost `IsApproved` je čitelná a zapisovatelná. Chcete-li uložit všechny změny této vlastnosti, musíme volat [metodu`UpdateUser`](https://msdn.microsoft.com/library/system.web.security.membership.updateuser.aspx)třídy `Membership`, předejte upravený `MembershipUser` objekt.

Vzhledem k tomu, že vlastnost `IsApproved` je čitelná a zapisovatelná, ovládací prvek CheckBox je pravděpodobně nejlepším prvkem uživatelského rozhraní pro konfiguraci této vlastnosti. Nicméně zaškrtávací políčko nebude pro vlastnost `IsLockedOut` fungovat, protože správce nemůže uživatele uzamknout, může odemknout pouze uživatele. Vhodným uživatelským rozhraním pro vlastnost `IsLockedOut` je tlačítko, které po kliknutí na něj odemkne uživatelský účet. Toto tlačítko by mělo být povoleno pouze v případě, že je uživatel uzamčen.

### <a name="creating-theuserinformationaspxpage"></a>Vytvoření stránky`UserInformation.aspx`

Nyní je připraven k implementaci uživatelského rozhraní v `UserInformation.aspx`. Otevřete tuto stránku a přidejte následující webové ovládací prvky:

- Ovládací prvek hypertextový odkaz, který po kliknutí vrátí správce na stránku `ManageUsers.aspx`.
- Webový ovládací prvek popisku pro zobrazení jména vybraného uživatele. Nastavte `ID` tohoto popisku na `UserNameLabel` a vymažte jeho vlastnost text.
- Ovládací prvek CheckBox s názvem `IsApproved`. Vlastnost `AutoPostBack` nastavte na `True`.
- Ovládací prvek popisku pro zobrazení posledního uzamčeného data uživatele Pojmenujte tento popisek `LastLockedOutDateLabel` a vymažte jeho vlastnost `Text`.
- Tlačítko pro odemknutí uživatele Pojmenujte toto tlačítko `UnlockUserButton` a nastavte jeho vlastnost `Text` na "odemknout uživatele".
- Ovládací prvek popisek pro zobrazení stavových zpráv, například "stav schválení uživatele" byl aktualizován. " Pojmenujte tento ovládací prvek `StatusMessage`, vymažte jeho vlastnost `Text` a nastavte jeho vlastnost `CssClass` na `Important`. (`Important` Třída CSS je definována v souboru šablony stylů `Styles.css`; zobrazuje odpovídající text ve velkém červeném písmu.)

Po přidání těchto ovládacích prvků by zobrazení Návrh v aplikaci Visual Studio mělo vypadat podobně jako snímek obrazovky na obrázku 2.

[![vytvořit uživatelské rozhraní pro UserInformation. aspx](unlocking-and-approving-user-accounts-vb/_static/image5.png)](unlocking-and-approving-user-accounts-vb/_static/image4.png)

**Obrázek 2**: vytvoření uživatelského rozhraní pro `UserInformation.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](unlocking-and-approving-user-accounts-vb/_static/image6.png))

Po dokončení uživatelského rozhraní je naším dalším úkolem nastavení zaškrtávacího políčka `IsApproved` a dalších ovládacích prvků na základě informací vybraného uživatele. Vytvořte obslužnou rutinu události pro událost `Load` stránky a přidejte následující kód:

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample1.vb)]

Výše uvedený kód začíná tím, že zajistí, že se jedná o první návštěvu stránky, nikoli následné zpětné odeslání. Pak přečte uživatelské jméno předané v poli `user` QueryString a načte informace o tomto uživatelském účtu pomocí metody `Membership.GetUser(username)`. Pokud nebylo zadáno uživatelské jméno prostřednictvím řetězce dotazu nebo pokud nebylo nalezeno konkrétního uživatele, správce se pošle zpátky na stránku `ManageUsers.aspx`.

Hodnota `UserName` objektu `MembershipUser` se pak zobrazí v `UserNameLabel` a zaškrtávací políčko `IsApproved` se kontroluje na základě hodnoty vlastnosti `IsApproved`.

[Vlastnost`LastLockoutDate`](https://msdn.microsoft.com/library/system.web.security.membershipuser.lastlockoutdate.aspx) objektu `MembershipUser` vrací hodnotu `DateTime`, která indikuje, kdy byl uživatel naposledy uzamčen. Pokud uživatel nikdy neuzamkl, vrácená hodnota závisí na zprostředkovateli členství. Při vytvoření nového účtu `SqlMembershipProvider` nastaví `LastLockoutDate` pole `aspnet_Membership` tabulky na `1754-01-01 12:00:00 AM`. Výše uvedený kód zobrazuje prázdný řetězec v `LastLockoutDateLabel`, pokud se vlastnost `LastLockoutDate` vyskytne před rokem 2000; v opačném případě se v popisku zobrazí část data vlastnosti `LastLockoutDate`. Vlastnost `Enabled` `UnlockUserButton`je nastavena na stav uzamčeno uživatele, což znamená, že toto tlačítko bude povoleno pouze v případě, že je uživatel uzamčen.

Vyzkoušení stránky `UserInformation.aspx` pomocí prohlížeče chvíli počkejte. Samozřejmě budete muset začít `ManageUsers.aspx` a vybrat uživatelský účet, který chcete spravovat. Po přijetí na `UserInformation.aspx`si všimněte, že zaškrtávací políčko `IsApproved` je zaškrtnuto pouze v případě, že je uživatel schválen. Pokud uživatel byl někdy uzamčený, zobrazí se jeho poslední datum uzamčení. Tlačítko Odemknout uživatele je povoleno pouze v případě, že je uživatel aktuálně uzamčen. Zaškrtnutím nebo zrušením zaškrtnutí políčka `IsApproved` nebo kliknutím na tlačítko Odemknout uživatele dojde k postbacku, ale v uživatelském účtu se neprovádí žádné úpravy, protože ještě jsme pro tyto události vytvořili obslužné rutiny událostí.

Vraťte se do sady Visual Studio a vytvořte obslužné rutiny událostí pro událost `CheckedChanged` `IsApproved` zaškrtávací políčko a událost `Click` tlačítka `UnlockUser`. V obslužné rutině události `CheckedChanged` nastavte vlastnost `IsApproved` uživatele na vlastnost `Checked` zaškrtávacího políčka a poté změny uložte prostřednictvím volání `Membership.UpdateUser`. V obslužné rutině události `Click` jednoduše zavolejte metodu `UnlockUser` `MembershipUser` objektu. V obou obslužných rutinách události se zobrazí vhodná zpráva v popisku `StatusMessage`.

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample2.vb)]

### <a name="testing-theuserinformationaspxpage"></a>Testování stránky`UserInformation.aspx`

Pomocí těchto obslužných rutin událostí znovu přejděte na stránku a neschváleného uživatele. Jak ukazuje obrázek 3, na stránce by se měla zobrazit Stručná zpráva oznamující, že se vlastnost `IsApproved` uživatele úspěšně změnila.

[![pracovník Novotný byl neschválen](unlocking-and-approving-user-accounts-vb/_static/image8.png)](unlocking-and-approving-user-accounts-vb/_static/image7.png)

**Obrázek 3**: pracovník Novotný byl neschválen ([kliknutím zobrazíte obrázek v plné velikosti).](unlocking-and-approving-user-accounts-vb/_static/image9.png)

Potom odhlaste se a zkuste se přihlásit jako uživatel, jehož účet jste právě neschválili. Vzhledem k tomu, že uživatel není schválený, nemůže se přihlásit. Ve výchozím nastavení zobrazí ovládací prvek přihlášení stejnou zprávu, pokud se uživatel nemůže přihlásit, bez ohledu na důvod. Ale při <a id="Tutorial6"> </a> [*ověřování přihlašovacích údajů uživatele proti uživatelskému obchodu s uživatelským jménem*](../membership/validating-user-credentials-against-the-membership-user-store-vb.md) jsme prohlédli rozšíření přihlašovacího ovládacího prvku, aby se zobrazila vhodnější zpráva. Obrázek 4 znázorňuje, že se na pracovníkovi zobrazuje zpráva, že se nemůže přihlásit, protože jeho účet ještě není schválený.

[![Chris se nemůže přihlásit, protože jeho účet není schválený.](unlocking-and-approving-user-accounts-vb/_static/image11.png)](unlocking-and-approving-user-accounts-vb/_static/image10.png)

**Obrázek 4**: Chris se nemůže přihlásit, protože jeho účet není schválený ([kliknutím zobrazíte obrázek v plné velikosti).](unlocking-and-approving-user-accounts-vb/_static/image12.png)

Chcete-li otestovat funkci uzamčení, zkuste se přihlásit jako schválený uživatel, ale použijte nesprávné heslo. Opakujte tento postup a počkejte, než se účet uživatele zamkne. Přihlašovací ovládací prvek byl aktualizován také, aby při pokusu o přihlášení z uzamčeného účtu zobrazoval vlastní zprávu. Víte, že účet byl uzamčen po zahájení zobrazení následující zprávy na přihlašovací stránce: "váš účet byl uzamčen z důvodu příliš velkého počtu neplatných pokusů o přihlášení". Kontaktujte prosím správce, aby váš účet byl odemčený. "

Vraťte se na stránku `ManageUsers.aspx` a klikněte na odkaz Správa pro uzamčeného uživatele. Na obrázku 5 vidíte, že by se měla zobrazit hodnota na stránce `LastLockedOutDateLabel` tlačítko Odemknout uživatele by mělo být povolené. Kliknutím na tlačítko Odemknout uživatele odemkněte uživatelský účet. Po odemčení uživatele se budou moct znovu přihlásit.

[![Dave byl uzamčený ze systému](unlocking-and-approving-user-accounts-vb/_static/image14.png)](unlocking-and-approving-user-accounts-vb/_static/image13.png)

**Obrázek 5**: Dave byl uzamčen ze systému ([kliknutím zobrazíte obrázek v plné velikosti](unlocking-and-approving-user-accounts-vb/_static/image15.png)).

## <a name="step-2-specifying-new-users-approved-status"></a>Krok 2: určení stavu schválení nových uživatelů

Schválený stav je užitečný ve scénářích, kdy chcete provést určitou akci předtím, než se nový uživatel bude moci přihlásit a získat přístup k funkcím, které jsou specifické pro uživatele. Například může být spuštěn soukromý web, kde jsou všechny stránky kromě přihlašovacích a registračních stránek přístupné pouze ověřeným uživatelům. Ale co se stane, když cizí web dosáhne vaší webové stránky, najde registrační stránku a vytvoří účet? Aby k tomu nedocházelo, můžete přesunout přihlašovací stránku do složky `Administration` a vyžadovat, aby si správce ručně vytvořil každý účet. Případně můžete všem uživatelům povolit registraci, ale zakázat přístup k webu, dokud správce neschválí uživatelský účet.

Ve výchozím nastavení schválí ovládací prvek ovládacím CreateUserWizard nové účty. Toto chování můžete nakonfigurovat pomocí [vlastnosti`DisableCreatedUser`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.disablecreateduser.aspx)ovládacího prvku. Nastavte tuto vlastnost na `True`, aby neschvalovala nové uživatelské účty.

> [!NOTE]
> Ve výchozím nastavení se ovládací prvek ovládacím CreateUserWizard automaticky přihlásí k novému uživatelskému účtu. Toto chování je řízeno [vlastností`LoginCreatedUser`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.logincreateduser.aspx)ovládacího prvku. Vzhledem k tomu, že neschválení uživatelé se nemohou přihlásit k webu, když `DisableCreatedUser` `True` nový uživatelský účet není přihlášen k webu, bez ohledu na hodnotu vlastnosti `LoginCreatedUser`.

Pokud vytváříte nové uživatelské účty prostřednictvím metody `Membership.CreateUser` a chcete vytvořit neschválený uživatelský účet, použijte jedno z přetížení, které přijímají hodnotu vlastnosti `IsApproved` nového uživatele jako vstupní parametr.

## <a name="step-3-approving-users-by-verifying-their-email-address"></a>Krok 3: schválení uživatelů ověřením jejich e-mailové adresy

Mnoho webů, které podporují uživatelské účty, neschvaluje nové uživatele, dokud neověří e-mailovou adresu, kterou zadal při registraci. Tento proces ověření se běžně používá k vzdorujeí robotyí, odesilatelům nevyžádané pošty a dalších ne'er-jamk, protože vyžaduje jedinečnou, ověřenou e-mailovou adresu a v procesu registrace přidá další krok. Když se v tomto modelu přihlásí nový uživatel, pošle se vám e-mailová zpráva s odkazem na ověřovací stránku. Tím, že uživatel prochází odkazem, který zjistil, že e-mail přijal a proto, že zadaná e-mailová adresa je platná. Stránka pro ověření zodpovídá za schválení uživatele. K tomu může dojít automaticky, což schválí všechny uživatele, kteří dosáhnou této stránky, nebo jenom po tom, co uživatel zadá nějaké další informace, jako je třeba [CAPTCHA](http://en.wikipedia.org/wiki/Captcha).

Abychom tento pracovní postup přizpůsobili, musíme nejdřív aktualizovat stránku pro vytvoření účtu, aby noví uživatelé neschválili. Otevřete stránku `EnhancedCreateUserWizard.aspx` ve složce `Membership` a nastavte vlastnost `DisableCreatedUser` ovládacího prvku ovládacím CreateUserWizard na `True`.

Dále je potřeba nakonfigurovat ovládací prvek ovládacím CreateUserWizard, aby odesílal novému uživateli e-mail s pokyny, jak ověřit jejich účet. Konkrétně budeme do e-mailu začlenit odkaz na stránku `Verification.aspx` (kterou jsme ještě vytvořili) a předáním `UserId` nového uživatele pomocí řetězce dotazu QueryString. Stránka `Verification.aspx` vyhledá zadaného uživatele a označí je jako schválená.

### <a name="sending-a-verification-email-to-new-users"></a>Posílání ověřovacího e-mailu novým uživatelům

K odeslání e-mailu z ovládacího prvku ovládacím CreateUserWizard nakonfigurujte jeho vlastnost `MailDefinition` odpovídajícím způsobem. Jak je popsáno v <a id="Tutorial13"> </a> [předchozím kurzu](recovering-and-changing-passwords-vb.md), ovládací prvky ChangePassword a PasswordRecovery obsahují [vlastnost`MailDefinition`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.maildefinition.aspx) , která funguje stejným způsobem jako ovládací prvek ovládacím CreateUserWizard.

> [!NOTE]
> Chcete-li použít vlastnost `MailDefinition`, je třeba zadat možnosti doručování pošty v `Web.config`. Další informace najdete [v tématu posílání e-mailů v ASP.NET](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx).

Začněte vytvořením nové e-mailové šablony s názvem `CreateUserWizard.txt` ve složce `EmailTemplates`. Pro šablonu použijte následující text:

[!code-aspx[Main](unlocking-and-approving-user-accounts-vb/samples/sample3.aspx)]

Nastavte vlastnost `BodyFileName` `MailDefinition`na ~/EmailTemplates/CreateUserWizard.txt a jeho vlastnost `Subject` na Vítejte na mém webu! Aktivujte prosím svůj účet.

Všimněte si, že `CreateUserWizard.txt` e-mailová šablona obsahuje zástupný text `<%VerificationUrl%>`. Tady se umístí adresa URL stránky `Verification.aspx`. Ovládacím CreateUserWizard automaticky nahradí `<%UserName%>` a `<%Password%>` zástupné symboly pomocí uživatelského jména a hesla nového účtu, ale není k dispozici žádný vestavěný zástupný symbol `<%VerificationUrl%>`. Je potřeba ji ručně nahradit odpovídající ověřovací adresou URL.

K tomuto účelu vytvořte obslužnou rutinu události pro [událost`SendingMail`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.sendingmail.aspx) ovládacím CreateUserWizard a přidejte následující kód:

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample4.vb)]

Událost `SendingMail` aktivuje se po `CreatedUser` události, což znamená, že v době, kdy výše uvedená obslužná rutina události spustí, byl nový uživatelský účet již vytvořen. K hodnotě `UserId` nového uživatele se dostanete tak, že zavoláte metodu `Membership.GetUser` a předáte do ovládacího prvku ovládacím CreateUserWizard, který předává `UserName`. V dalším kroku se vytvoří adresa URL pro ověření. Příkaz `Request.Url.GetLeftPart(UriPartial.Authority)` vrátí část `http://yourserver.com` adresy URL; `Request.ApplicationPath` vrátí cestu, kde je aplikace rootovaná. Adresa URL pro ověření se pak definuje jako `Verification.aspx?ID=userId`. Tyto dva řetězce se pak zřetězí tak, aby tvořily úplnou adresu URL. Text e-mailové zprávy (`e.Message.Body`) obsahuje také všechny výskyty `<%VerificationUrl%>` nahrazené úplnou adresou URL.

Čistý efekt znamená, že noví uživatelé jsou neschváleni, což znamená, že se nemohou přihlásit k webu. Kromě toho se automaticky odesílají e-maily s odkazem na adresu URL pro ověření (viz obrázek 6).

[![nový uživatel obdrží E-mail s odkazem na adresu URL pro ověření.](unlocking-and-approving-user-accounts-vb/_static/image17.png)](unlocking-and-approving-user-accounts-vb/_static/image16.png)

**Obrázek 6**: nový uživatel obdrží E-mail s odkazem na adresu URL pro ověření ([kliknutím zobrazíte obrázek v plné velikosti).](unlocking-and-approving-user-accounts-vb/_static/image18.png)

> [!NOTE]
> Výchozí krok ovládacím CreateUserWizard ovládacího prvku ovládacím CreateUserWizard zobrazí zprávu informující o tom, že byl vytvořen účet uživatele, a zobrazí tlačítko pro pokračování. Kliknutím převezme uživatel adresu URL určenou vlastností `ContinueDestinationPageUrl` ovládacího prvku. Ovládacím CreateUserWizard v `EnhancedCreateUserWizard.aspx` je nakonfigurován tak, aby odesílala nové uživatele do `~/Membership/AdditionalUserInfo.aspx`, která uživatele vyzve k zadání svého rodištěu, adresy URL domovské stránky a podpisu. Vzhledem k tomu, že tyto informace mohou být přidány pouze přihlášeným uživatelům, má smysl tuto vlastnost aktualizovat, aby bylo možné odesílat uživatele zpět na domovskou stránku webu (`~/Default.aspx`). Kromě toho by měla být stránka `EnhancedCreateUserWizard.aspx` nebo krok ovládacím CreateUserWizard rozšířena tak, aby informovala uživatele o tom, že byl odeslán ověřovací e-mail, a jejich účet nebude aktivován, dokud nepostupuje podle pokynů v tomto e-mailu. Tyto úpravy opouštíme jako cvičení pro čtenáře.

### <a name="creating-the-verification-page"></a>Vytvoření ověřovací stránky

Náš konečný úkol je vytvořit stránku `Verification.aspx`. Přidejte tuto stránku do kořenové složky a přiřadíte ji k `Site.master` hlavní stránku. Vzhledem k tomu, že jsme provedli většinu předchozích stránek obsahu přidaných do webu, odeberte ovládací prvek obsahu, který odkazuje na `LoginContent` ContentPlaceHolder, aby stránka obsahu používala výchozí obsah stránky předlohy.

Přidejte ovládací prvek web Label na stránku `Verification.aspx`, nastavte jeho `ID` na `StatusMessage` a vymažte jeho vlastnost text. Dále vytvořte obslužnou rutinu události `Page_Load` a přidejte následující kód:

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample5.vb)]

Hromadný z výše uvedeného kódu ověřuje, že ID uživatele zadané pomocí řetězce dotazu existuje, že se jedná o platnou `Guid` hodnotu a že odkazuje na existující uživatelský účet. Pokud všechny tyto kontroly proběhnou, je uživatelský účet schválen. v opačném případě se zobrazí vhodná stavová zpráva.

Obrázek 7 ukazuje stránku `Verification.aspx`, když se navštíví přes prohlížeč.

[![účet nového uživatele je teď schválený.](unlocking-and-approving-user-accounts-vb/_static/image20.png)](unlocking-and-approving-user-accounts-vb/_static/image19.png)

**Obrázek 7**: účet nového uživatele je teď schválený ([kliknutím zobrazíte obrázek v plné velikosti](unlocking-and-approving-user-accounts-vb/_static/image21.png)).

## <a name="summary"></a>Přehled

Všechny uživatelské účty členů mají dva stavy, které určují, jestli se uživatel může přihlásit k webu: `IsLockedOut` a `IsApproved`. Obě tyto vlastnosti musí být `True`, aby se uživatel mohl přihlásit.

Stav uzamčeného uživatele se používá jako bezpečnostní opatření ke snížení pravděpodobnosti narušení hackerů v lokalitě prostřednictvím metod hrubou silou. Konkrétně je uživatel uzamčen, pokud v určitém časovém období dojde k určitému počtu neplatných pokusů o přihlášení. Tyto hranice lze konfigurovat prostřednictvím nastavení zprostředkovatele členství v `Web.config`.

Schválený stav se běžně používá jako prostředek k zakázání přihlášení nových uživatelů, dokud některá akce neuplyne. Lokalita možná vyžaduje, aby nové účty nejdřív schválil správce nebo, jak jsme viděli v kroku 3 ověřením jejich e-mailové adresy.

Šťastné programování!

### <a name="about-the-author"></a>O autorovi

Scott Mitchell, autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je *[Sams naučit se ASP.NET 2,0 za 24 hodin](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* . Scott se dá kontaktovat [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky...

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](recovering-and-changing-passwords-vb.md)
