---
uid: web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-cs
title: Obnovování a změna hesel (C#) | Microsoft Docs
author: rick-anderson
description: ASP.NET obsahuje dva webové ovládací prvky pro pomoc s obnovováním a změnou hesel. Ovládací prvek PasswordRecovery umožňuje návštěvníkovi obnovit ztracený PA...
ms.author: riande
ms.date: 04/01/2008
ms.assetid: 19c4d042-4e34-4b44-9f1d-6bf2253ba366
msc.legacyurl: /web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-cs
msc.type: authoredcontent
ms.openlocfilehash: 8c07b8a3c36e4863c6d2d356b8483544ac4cafeb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74576718"
---
# <a name="recovering-and-changing-passwords-c"></a>Obnovení a změna hesel (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/CS.13.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial13_ChangingPasswords_cs.pdf)

> ASP.NET obsahuje dva webové ovládací prvky pro pomoc s obnovováním a změnou hesel. Ovládací prvek PasswordRecovery umožňuje návštěvníkovi obnovit ztracené heslo. Ovládací prvek ChangePassword umožňuje uživateli aktualizovat heslo. Stejně jako ostatní webové ovládací prvky související s přihlášením, které jsme viděli v této sérii kurzů, ovládací prvky PasswordRecovery a ChangePassword fungují s rámec členství na pozadí pro resetování nebo změnu hesel uživatelů.

## <a name="introduction"></a>Úvod

Mezi weby pro moji banku, programovou firmu, telefonní firmu, e-mailové účty a přizpůsobené webové portály mají spoustu různých hesel, které si zapamatují. Díky tolika přihlašovacím údajům, aby se nepamatují tyto dny, není neobvyklé, že by uživatelé zapomněli heslo. Pro účely tohoto účtu musí weby, které nabízejí uživatelské účty, obsahovat způsob, jak může uživatel obnovit heslo. Tento proces obvykle zahrnuje generování nového a náhodného hesla a odeslání e-mailu e-mailové adrese uživatele v souboru. Po přijetí nového hesla se většina uživatelů vrátí na lokalitu a změní heslo z náhodně generovaného hesla, aby je bylo možné popamatovat.

ASP.NET obsahuje dva webové ovládací prvky pro pomoc s obnovováním a změnou hesel. Ovládací prvek PasswordRecovery umožňuje návštěvníkovi obnovit ztracené heslo. Ovládací prvek ChangePassword umožňuje uživateli aktualizovat heslo. Stejně jako ostatní webové ovládací prvky související s přihlášením, které jsme viděli v této sérii kurzů, ovládací prvky PasswordRecovery a ChangePassword fungují s rámec členství na pozadí pro resetování nebo změnu hesel uživatelů.

V tomto kurzu prověříme tyto dva ovládací prvky. Také se dozvíte, jak programově měnit a resetovat heslo uživatele prostřednictvím metod `ChangePassword` a `ResetPassword` třídy `MembershipUser`.

## <a name="step-1-helping-users-recover-lost-passwords"></a>Krok 1: pomoc uživatelům při obnovování ztracených hesel

Všechny weby, které podporují uživatelské účty, musí uživatelům poskytnout nějaký mechanismus pro obnovování zapomenutých hesel. Dobrá zpráva je, že implementace takových funkcí v ASP.NET je Breeze díky webovému ovládacímu prvku PasswordRecovery. Ovládací prvek PasswordRecovery vykreslí rozhraní, které vyzve uživatele k zadání uživatelského jména a v případě potřeby odpoví na své bezpečnostní otázky. Pak e-mailem uživatele zaznamená heslo.

> [!NOTE]
> Vzhledem k tomu, že se e-mailové zprávy přenáší prostřednictvím sítě v prostém textu, dochází k bezpečnostním rizikům při posílání hesla uživatele e-mailem.

Ovládací prvek PasswordRecovery se skládá ze tří zobrazení:

- **Username** – vyzve návštěvníka k zadání uživatelského jména. Toto je počáteční zobrazení.
- **Otázka**– zobrazí uživatelské jméno a bezpečnostní otázku jako text spolu s textovým polem pro uživatele, aby zadal odpověď na svoji bezpečnostní otázku.
- **Success**– zobrazí zprávu s informací o uživateli, že heslo bylo e-mailem.

Zobrazená zobrazení a akce provedené ovládacím prvkem PasswordRecovery závisejí na následujícím nastavení konfigurace členství:

- `RequiresQuestionAndAnswer`
- `EnablePasswordRetrieval`
- `EnablePasswordReset`

Nastavení `RequiresQuestionAndAnswer` architektury pro členství určuje, jestli musí uživatelé při registraci účtu zadat bezpečnostní otázku a odpověď. Jak je popsáno v <a id="_msoanchor_1"> </a>kurzu [*vytváření uživatelských účtů*](../membership/creating-user-accounts-cs.md) , pokud je `RequiresQuestionAndAnswer` true (výchozí nastavení), rozhraní ovládacím CreateUserWizard obsahuje ovládací prvky TextBox pro bezpečnostní otázku a odpověď nového uživatele. Pokud je `RequiresQuestionAndAnswer` false, žádné takové informace se nebudou shromažďovat. Podobně, pokud `RequiresQuestionAndAnswer` má hodnotu true, ovládací prvek PasswordRecovery zobrazí zobrazení otázky poté, co uživatel zadá své uživatelské jméno. heslo se obnoví pouze v případě, že uživatel zadá správnou bezpečnostní otázku. Pokud je `RequiresQuestionAndAnswer` false, ovládací prvek PasswordRecovery se přesune přímo ze zobrazení uživatelské jméno do zobrazení úspěšné.

Když uživatel zadá své uživatelské jméno nebo uživatelské jméno a bezpečnostní odpověď, pokud `RequiresQuestionAndAnswer` true – PasswordRecovery pošle uživateli heslo. Pokud je možnost `EnablePasswordRetrieval` nastavená na hodnotu true, uživatel bude e-mailem poslat svoje aktuální heslo. Pokud je nastavena na hodnotu false a `EnablePasswordReset` je nastavena na hodnotu true, pak ovládací prvek PasswordRecovery vygeneruje nové náhodné heslo pro uživatele a pošle mu toto nové heslo e-mailem. Pokud jsou `EnablePasswordRetrieval` i `EnablePasswordReset` false, vyvolá ovládací prvek PasswordRecovery výjimku.

> [!NOTE]
> Odvolání, že `SqlMembershipProvider` ukládá hesla uživatelů v jednom ze tří formátů: Clear, hash (výchozí) nebo šifrovaná. Použitý mechanismus úložiště závisí na nastavení konfigurace členství; Ukázková aplikace používá formát hesla s algoritmem hash. Při použití formátu hesla s algoritmem hash musí být parametr `EnablePasswordRetrieval` nastaven na hodnotu false, protože systém nemůže určit skutečné heslo uživatele z verze s hodnotou hash uloženou v databázi.

Obrázek 1 ukazuje, jak je rozhraní PasswordRecovery a chování ovlivněno konfigurací členství.

[![RequiresQuestionAndAnswer, EnablePasswordRetrieval a EnablePasswordReset ovlivňují vzhled a chování ovládacího prvku PasswordRecovery.](recovering-and-changing-passwords-cs/_static/image2.png)](recovering-and-changing-passwords-cs/_static/image1.png)

**Obrázek 1**: `RequiresQuestionAndAnswer`, `EnablePasswordRetrieval`a `EnablePasswordReset` ovlivňují vzhled a chování ovládacího prvku PasswordRecovery ([kliknutím zobrazíte obrázek v plné velikosti).](recovering-and-changing-passwords-cs/_static/image3.png)

> [!NOTE]
> <a id="_msoanchor_2"> </a>V kurzu [*vytváření schématu členství v SQL Server*](../membership/creating-the-membership-schema-in-sql-server-cs.md) jsme nakonfigurovali poskytovatele členství nastavením `RequiresQuestionAndAnswer` na hodnotu true, `EnablePasswordRetrieval` na hodnotu false a `EnablePasswordReset` na hodnotu true.

### <a name="using-the-passwordrecovery-control"></a>Použití ovládacího prvku PasswordRecovery

Pojďme se podívat na použití ovládacího prvku PasswordRecovery na stránce ASP.NET. Otevřete `RecoverPassword.aspx` a přetáhněte ovládací prvek PasswordRecovery z panelu nástrojů na Návrhář. nastavte jeho `ID` na `RecoverPwd`. Podobně jako webové ovládací prvky login a ovládacím CreateUserWizard vykreslí zobrazení ovládacího prvku PasswordRecovery bohatě složené rozhraní, které obsahuje popisky, textová pole, tlačítka a ověřovací ovládací prvky. Můžete přizpůsobit vzhled zobrazení prostřednictvím vlastností stylu ovládacího prvku nebo převodem zobrazení do šablon. Ponechám se to jako cvičení pro zúčastněný čtenář.

Když uživatel navštíví tuto stránku, zadá její uživatelské jméno a klikne na tlačítko Odeslat. Vzhledem k tomu, že v našem nastavení konfigurace členství jsme nastavili vlastnost `RequiresQuestionAndAnswer` na hodnotu true, pak bude ovládací prvek PasswordRecovery zobrazovat otázky. Poté, co uživatel zadá správnou odpověď zabezpečení a klikne na tlačítko Odeslat, ovládací prvek PasswordRecovery aktualizuje heslo uživatele na náhodně generovaný a pošle toto heslo na e-mailovou adresu v souboru. To vše je možné, aniž byste museli psát jediný řádek kódu!

Než otestujete tuto stránku, budete mít k dispozici jednu poslední část konfigurace, která je v úmyslu: musíme zadat nastavení doručování pošty v `Web.config`. Ovládací prvek PasswordRecovery spoléhá na tato nastavení pro odeslání e-mailu.

Konfigurace doručování pošty je určena prostřednictvím [elementu`<mailSettings>`](https://msdn.microsoft.com/library/w355a94k.aspx)elementu [`<system.net>`](https://msdn.microsoft.com/library/6484zdc1.aspx). Pomocí [elementu`<smtp>`](https://msdn.microsoft.com/library/ms164240.aspx) určete způsob doručení a výchozí hodnotu z adresy. Následující kód konfiguruje nastavení pošty pro použití síťového serveru SMTP s názvem `smtp.example.com` na portu 25 a přihlašovací údaje uživatelského jména a hesla uživatelského jména a hesla.

> [!NOTE]
> `<system.net>` je podřízeným prvkem kořenového elementu `<configuration>` a na stejné úrovni jako `<system.web>`. Proto neumísťujte element `<system.net>` v rámci elementu `<system.web>`; místo toho ho umístěte na stejnou úroveň.

[!code-xml[Main](recovering-and-changing-passwords-cs/samples/sample1.xml)]

Kromě používání serveru SMTP v síti můžete případně zadat výstupní adresář, kam se mají ukládat e-mailové zprávy, které se mají odeslat.

Po nakonfigurování nastavení SMTP navštivte stránku `RecoverPassword.aspx` v prohlížeči. Nejdřív zkuste zadat uživatelské jméno, které v úložišti uživatelů neexistuje. Jak ukazuje obrázek 2, ovládací prvek PasswordRecovery zobrazí zprávu oznamující, že nelze získat informace o uživateli. Text zprávy lze přizpůsobit pomocí [vlastnosti`UserNameFailureText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.usernamefailuretext.aspx)ovládacího prvku.

[Při zadání neplatného uživatelského jména se zobrazí ![chybová zpráva.](recovering-and-changing-passwords-cs/_static/image5.png)](recovering-and-changing-passwords-cs/_static/image4.png)

**Obrázek 2**: Pokud je zadáno neplatné uživatelské jméno ([kliknutím zobrazíte obrázek v plné velikosti),](recovering-and-changing-passwords-cs/_static/image6.png)zobrazí se chybová zpráva.

Teď zadejte uživatelské jméno. Použijte uživatelské jméno účtu v systému s e-mailovou adresou, na kterou máte přístup, a jejíž bezpečnostní odpověď víte. Po zadání uživatelského jména a kliknutí na Odeslat zobrazí ovládací prvek PasswordRecovery zobrazení dotazu. Stejně jako u zobrazení uživatelského jména, pokud zadáte nesprávnou odpověď, ovládací prvek PasswordRecovery zobrazí chybovou zprávu (viz obrázek 3). K přizpůsobení této chybové zprávy použijte [vlastnost`QuestionFailureText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.questionfailuretext.aspx) .

[![se zobrazí chybová zpráva, pokud uživatel zadá neplatnou bezpečnostní odpověď](recovering-and-changing-passwords-cs/_static/image8.png)](recovering-and-changing-passwords-cs/_static/image7.png)

**Obrázek 3**: Pokud uživatel zadá neplatnou bezpečnostní odpověď ([kliknutím zobrazíte obrázek v plné velikosti](recovering-and-changing-passwords-cs/_static/image9.png)), zobrazí se chybová zpráva.

Nakonec zadejte správnou odpověď zabezpečení a klikněte na Odeslat. Na pozadí ovládací prvek PasswordRecovery vygeneruje náhodné heslo, přiřadí ho k uživatelskému účtu, pošle e-mail s oznámením uživatele o svém novém heslu (viz obrázek 4) a pak zobrazí zobrazení úspěšnosti.

[![se uživateli pošle E-mail s jeho novým heslem.](recovering-and-changing-passwords-cs/_static/image11.png)](recovering-and-changing-passwords-cs/_static/image10.png)

**Obrázek 4**: uživateli se pošle E-mail s jeho novým heslem ([kliknutím zobrazíte obrázek v plné velikosti](recovering-and-changing-passwords-cs/_static/image12.png)).

### <a name="customizing-the-email"></a>Přizpůsobení e-mailu

Výchozí e-mail odeslaný ovládacím prvkem PasswordRecovery je spíše matný (viz obrázek 4). Zpráva se odešle z účtu zadaného v atributu `from` `<smtp>` elementu s heslem předmětu a tělo textu v prostém textu:

Vraťte se prosím na web a přihlaste se pomocí následujících informací.

Uživatelské jméno: *uživatelské* jméno

Heslo: *heslo*

Tuto zprávu lze přizpůsobit programově prostřednictvím obslužné rutiny události pro [událost`SendingMail`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.sendingmail.aspx)ovládacího prvku PasswordRecovery nebo deklarativně prostřednictvím [vlastnosti`MailDefinition`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.maildefinition.aspx). Pojďme prozkoumat obě tyto možnosti.

Událost `SendingMail` je aktivována před odesláním e-mailové zprávy a je poslední možností, jak tuto e-mailovou zprávu programově upravit. Při vyvolání této události je obslužné rutině události předán objekt typu [`MailMessageEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.mailmessageeventargs.aspx), jehož vlastnost `Message` obsahuje odkaz na e-mail, který se má odeslat.

Vytvořte obslužnou rutinu události pro událost `SendingMail` a přidejte následující kód, který programově přidá `webmaster@example.com` do seznamu kopie.

[!code-csharp[Main](recovering-and-changing-passwords-cs/samples/sample2.cs)]

E-mailová zpráva se dá nakonfigurovat taky prostřednictvím deklarativních prostředků. Vlastnost `MailDefinition` ovládacího prvku PasswordRecovery je objekt typu [`MailDefinition`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.aspx). Třída `MailDefinition` nabízí hostitele vlastností souvisejících s e-maily, včetně `From`, `CC`, `Priority`, `Subject`, `IsBodyHtml`, `BodyFileName`a dalších. U starts nastavte [vlastnost`Subject`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.subject.aspx) na něco výstižnější než ta, která se používá ve výchozím nastavení (heslo), například heslo bylo resetováno...

K přizpůsobení těla e-mailové zprávy musíme vytvořit samostatný soubor šablony e-mailu, který obsahuje obsah těla. Začněte vytvořením nové složky na webu s názvem `EmailTemplates`. Potom do této složky přidejte nový textový soubor s názvem `PasswordRecovery.txt` a přidejte následující obsah:

[!code-aspx[Main](recovering-and-changing-passwords-cs/samples/sample3.aspx)]

Všimněte si použití zástupných symbolů `<%UserName%>` a `<%Password%>`. Ovládací prvek PasswordRecovery automaticky nahradí tyto dva zástupné symboly uživatelským jménem a obnoveným heslem před odesláním e-mailu.

Nakonec nastavte [vlastnost `MailDefinition``BodyFileName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx) na šablonu e-mailu, kterou jsme právě vytvořili (`~/EmailTemplates/PasswordRecovery.txt`).

Po provedení těchto změn přejděte na stránku `RecoverPassword.aspx` a zadejte své uživatelské jméno a odpověď na zabezpečení. Obdržíte e-mail, který vypadá jako na obrázku 5. Všimněte si, že `webmaster@example.com` byl CC a předmět a tělo byly aktualizovány.

[![se aktualizoval předmět, text a seznam kopií.](recovering-and-changing-passwords-cs/_static/image14.png)](recovering-and-changing-passwords-cs/_static/image13.png)

**Obrázek 5**: aktualizoval se seznam předmět, tělo a kopie ([kliknutím zobrazíte obrázek v plné velikosti](recovering-and-changing-passwords-cs/_static/image15.png)).

K odeslání e-mailové sady ve formátu HTML [`IsBodyHtml`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.isbodyhtml.aspx) na hodnotu true (výchozí hodnota je false) a aktualizace e-mailové šablony tak, aby OBSAHOVALA kód HTML.

Vlastnost `MailDefinition` není jedinečná pro třídu PasswordRecovery. Jak uvidíme v kroku 2, ovládací prvek ChangePassword také nabízí vlastnost `MailDefinition`. Kromě toho ovládací prvek ovládacím CreateUserWizard zahrnuje takovou vlastnost, kterou můžete nakonfigurovat tak, aby automaticky odesílala uvítací e-mailovou zprávu novým uživatelům.

> [!NOTE]
> V současné době nejsou v levém navigačním panelu k dispozici žádná propojení pro dosažení stránky `RecoverPassword.aspx`. Uživatel by se na tuto stránku musel zajímat jenom v případě, že se mu nepovedlo úspěšně přihlásit k webu. Proto aktualizujte stránku `Login.aspx` tak, aby obsahovala odkaz na stránku `RecoverPassword.aspx`.

### <a name="programmatically-resetting-a-users-password"></a>Programové obnovení hesla uživatele

Při resetování hesla uživatele ovládací prvek PasswordRecovery volá [metodu`ResetPassword`](https://msdn.microsoft.com/library/system.web.security.membershipuser.resetpassword.aspx)objektu `MembershipUser`. Tato metoda má dvě přetížení:

- **[`ResetPassword`](https://msdn.microsoft.com/library/d94bdzz2.aspx)** – resetuje heslo uživatele. Toto přetížení použijte, pokud je `RequiresQuestionAndAnswer` false.
- **[`ResetPassword(securityAnswer)`](https://msdn.microsoft.com/library/d90zte4w.aspx)** – obnoví heslo uživatele pouze v případě, že je zadané *securityAnswer* správné. Toto přetížení použijte, pokud je `RequiresQuestionAndAnswer` true.

Obě přetížení vrátí nové náhodně generované heslo.

Podobně jako u jiných metod v rozhraní členství, `ResetPassword` metoda se deleguje nakonfigurovanému zprostředkovateli. `SqlMembershipProvider` vyvolá uloženou proceduru `aspnet_Membership_ResetPassword`, která předává uživatelské jméno, nové heslo a dodanou odpověď na heslo, mimo jiné pole. Uložená procedura zajišťuje, že odpověď na heslo odpovídá a pak aktualizuje heslo uživatele.

Pár poznámek k implementaci nízké úrovně:

- Uzamčený uživatel nemůže resetovat své heslo. Je však možné, že neschváleného uživatele. V kurzu <a id="_msoanchor_3"> </a> [*odblokování a schválení uživatelských*](unlocking-and-approving-user-accounts-cs.md) účtů se podíváme na uzamčené a schválené stavy podrobněji.
- Pokud je odpověď hesla nesprávná, zvýší se počet neúspěšných pokusů o přijetí hesla uživatele. Pokud se v zadaném časovém období vyskytne zadaný počet neplatných bezpečnostních odpovědí, uživatel je uzamčen.

### <a name="a-word-on-how-the-random-passwords-are-generated"></a>Slovo, jak se generují náhodná hesla

Náhodně generovaná hesla zobrazená v e-mailových zprávách na obrázcích 4 a 5 se vytvoří pomocí [metody`GeneratePassword`](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)třídy členství. Tato metoda přijímá dva celočíselné vstupy datového- *Length* a *numberOfNonAlphanumericCharacters* -a vrací řetězec s minimální *délkou* znaků dlouhých alespoň *numberOfNonAlphanumericCharacters* počet nealfanumerických znaků. Pokud je tato metoda volána v rámci tříd členství nebo webových ovládacích prvků souvisejících s přihlášením, hodnoty pro tyto dva parametry jsou určeny `MinRequiredPasswordLength` a `MinRequiredNonalphanumericCharacters` vlastností konfigurace členství, které jsme nastavili na 7 a 1 v uvedeném pořadí.

Metoda `GeneratePassword` používá kryptograficky silné generátory náhodných čísel, aby se zajistilo, že není k dispozici žádný posun při výběru náhodných znaků. Kromě toho je `GeneratePassword` `public`, což znamená, že ho můžete použít přímo z aplikace ASP.NET, pokud potřebujete Generovat náhodné řetězce nebo hesla.

> [!NOTE]
> Třída `SqlMembershipProvider` vždy generuje náhodné heslo alespoň o délce 14 znaků, takže pokud je `MinRequiredPasswordLength` menší než 14, je jeho hodnota ignorována.

## <a name="step-2-changing-passwords"></a>Krok 2: změna hesel

Náhodně vygenerovaná hesla je obtížné pamatovat. Vezměte v úvahu heslo uvedené na obrázku 4: `WWGUZv(f2yM:Bd`. Zkuste potvrzování paměti. Nemusíte říct, že když se uživateli pošle náhodně generované heslo tohoto řazení, bude chtít změnit heslo na něco, co je zapamatovatelné.

Pomocí ovládacího prvku ChangePassword vytvořte rozhraní, které bude uživatel moci změnit jeho heslo. Podobně jako u ovládacího prvku PasswordRecovery se ovládací prvek ChangePassword skládá ze dvou zobrazení: změnit heslo a úspěch. Zobrazení změnit heslo vyzve uživatele ke starému a novému heslu. Po poskytnutí správného starého hesla a nového hesla, které splňuje požadavky na minimální délku a nealfanumerické znaky, ovládací prvek ChangePassword aktualizuje heslo uživatele a zobrazí zobrazení úspěšnosti.

> [!NOTE]
> Ovládací prvek ChangePassword mění heslo uživatele vyvoláním [metody`ChangePassword`](https://msdn.microsoft.com/library/system.web.security.membershipuser.changepassword.aspx)`MembershipUser`ho objektu. Metoda ChangePassword přijímá dva `string` vstupní parametry – *oldPassword* a *nové_heslo*– a aktualizuje účet uživatele pomocí parametru *nové_heslo*za předpokladu, že zadaný *oldPassword* je správný.

Otevřete stránku `ChangePassword.aspx` a přidejte na ni ovládací prvek ChangePassword a pojmenujte ho `ChangePwd`. V tomto okamžiku by zobrazení Návrh měla zobrazit zobrazení Změna hesla (viz obrázek 6). Podobně jako u ovládacího prvku PasswordRecovery lze přepínat mezi zobrazeními prostřednictvím inteligentní značky ovládacího prvku. Tyto pohledy jsou navíc přizpůsobitelné přes vlastnosti stylu roztříděné nebo je převedené na šablonu.

[![přidání ovládacího prvku ChangePassword na stránku](recovering-and-changing-passwords-cs/_static/image17.png)](recovering-and-changing-passwords-cs/_static/image16.png)

**Obrázek 6**: Přidání ovládacího prvku ChangePassword na stránku ([kliknutím zobrazíte obrázek v plné velikosti](recovering-and-changing-passwords-cs/_static/image18.png))

Ovládací prvek ChangePassword může aktualizovat heslo aktuálně přihlášeného uživatele *nebo* heslo jiného zadaného uživatele. Jak ukazuje obrázek 6, výchozí zobrazení Změna hesla vykresluje pouze tři ovládací prvky TextBox: jednu pro původní heslo a dvě pro nové heslo. Toto výchozí rozhraní se používá k aktualizaci hesla aktuálně přihlášeného uživatele.

Chcete-li použít ovládací prvek ChangePassword k aktualizaci hesla jiného uživatele, nastavte [vlastnost`DisplayUserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.changepassword.displayusername.aspx) ovládacího prvku na hodnotu true. Tím se na stránku přidá čtvrté textové pole s výzvou k zadání uživatelského jména uživatele, jehož heslo se má změnit.

Nastavení `DisplayUserName` na hodnotu true je užitečné, pokud chcete nechat odhlášeného uživatele, aniž byste se museli přihlašovat. Z vlastního hlediska si myslíme, že nedošlo k chybě, která vyžaduje, aby se uživatel přihlásil před tím, než mu umožní změnit své heslo. Proto ponechte `DisplayUserName` nastavenou na hodnotu false (výchozí). V tomto rozhodnutí ale v podstatě nebudeme mít přístup k této stránce anonymním uživatelům. Aktualizujte autorizační pravidla URL webu tak, aby se zabránilo anonymním uživatelům v návštěvě `ChangePassword.aspx`. Pokud potřebujete aktualizovat paměť v syntaxi autorizačního pravidla URL, přečtěte si kurz k <a id="_msoanchor_4"> </a> [*autorizaci na základě uživatele*](../membership/user-based-authorization-cs.md) .

> [!NOTE]
> Může se zdát, že vlastnost `DisplayUserName` je užitečná, když chcete správcům umožnit měnit hesla jiných uživatelů. I když je však `DisplayUserName` nastaveno na hodnotu true, musí být známo a zadáno správné staré heslo. Budeme pohovořit o technikách, které správcům umožňují měnit hesla uživatelů v kroku 3.

Přejděte na stránku `ChangePassword.aspx` v prohlížeči a změňte heslo. Všimněte si, že se zobrazí chybová zpráva, pokud zadáte nové heslo, které nesplňuje požadavky na délku hesla a jiné než alfanumerické znaky zadané v konfiguraci členství (viz obrázek 7).

[![přidání ovládacího prvku ChangePassword na stránku](recovering-and-changing-passwords-cs/_static/image20.png)](recovering-and-changing-passwords-cs/_static/image19.png)

**Obrázek 7**: Přidání ovládacího prvku ChangePassword na stránku ([kliknutím zobrazíte obrázek v plné velikosti](recovering-and-changing-passwords-cs/_static/image21.png))

Po zadání správného starého hesla a platného nového hesla se změní heslo přihlášeného uživatele a zobrazí se zobrazení úspěšné.

### <a name="sending-a-confirmation-email"></a>Posílá se potvrzovací E-mail.

Ve výchozím nastavení ovládací prvek ChangePassword nepošle e-mailovou zprávu uživateli, jehož heslo bylo právě aktualizováno. Pokud chcete odeslat e-mail, stačí nakonfigurovat vlastnost `MailDefinition` ovládacího prvku. Pojďme nakonfigurovat ovládací prvek ChangePassword tak, aby uživateli byl odeslán e-mail ve formátu HTML, který obsahuje nové heslo.

Začněte vytvořením nového souboru ve složce `EmailTemplates` s názvem `ChangePassword.htm`. Přidejte následující kód:

[!code-html[Main](recovering-and-changing-passwords-cs/samples/sample4.html)]

V dalším kroku nastavte vlastnosti `MailDefinition` `BodyFileName`, `IsBodyHtml`a `Subject` vlastností ovládacího prvku ChangePassword na ~/EmailTemplates/ChangePassword.htm, true a vaše heslo se změnilo!

Po provedení těchto změn znovu navštivte stránku a znovu změňte heslo. Tentokrát ovládací prvek ChangePassword pošle e-mailovou adresu uživatele v souboru přizpůsobený e-mail ve formátu HTML (viz obrázek 8).

[![e-mailové zprávy informující o tom, že se změnilo heslo](recovering-and-changing-passwords-cs/_static/image23.png)](recovering-and-changing-passwords-cs/_static/image22.png)

**Obrázek 8**: e-mailová zpráva informuje uživatele o tom, že se změnilo heslo ([kliknutím zobrazíte obrázek v plné velikosti).](recovering-and-changing-passwords-cs/_static/image24.png)

## <a name="step-3-allowing-administrators-to-change-users-passwords"></a>Krok 3: povolení správců měnit hesla uživatelů

Běžnou funkcí v aplikacích, které podporují uživatelské účty, je možnost, aby administrativní uživatel mohl měnit hesla jiných uživatelů. Tato funkce se někdy vyžaduje, protože systém nemá možnost měnit hesla uživatelů. V takovém případě může být jediným způsobem, jak by uživatel obnovil zapomenuté heslo, být správce, aby jim přidělil nové heslo. Pomocí ovládacích prvků PasswordRecovery a ChangePassword se však administrativní uživatelé nemusí sami rušit a měnit hesla uživatelů, protože je uživatelé můžou sám provádět.

Ale co dělat v případě, že váš klient bude mít možnost měnit hesla jiných uživatelů, aby měli administrativní uživatelé? Přidání této funkce může být trochu práce. Chcete-li změnit heslo uživatele, je nutné zadat staré i nové heslo do metody `ChangePassword` `MembershipUser` objektu, ale správce by neměl znát heslo uživatele, aby jej bylo možné upravit.

Jedním z možných řešení je nejdřív resetovat heslo uživatele a pak ho změnit na nové heslo pomocí kódu podobného následujícímu:

[!code-aspx[Main](recovering-and-changing-passwords-cs/samples/sample5.aspx)]

Tento kód začíná načtením informací o uživatelském *jménu*, což je uživatel, jehož heslo si chce správce změnit. Dále je vyvolána metoda `ResetPassword`, která přiřadí a uživateli nové náhodné heslo. Toto náhodně generované heslo je vráceno metodou a uložené v proměnné `resetPwd`. Teď, když znáte heslo uživatele, můžeme ho změnit prostřednictvím volání `ChangePassword`.

Tento kód funguje pouze v případě, že je konfigurace systému členství nastavena tak, že `RequiresQuestionAndAnswer` hodnota false. Pokud `RequiresQuestionAndAnswer` má hodnotu true, stejně jako v naší aplikaci, musí být metoda `ResetPassword` předána bezpečnostní odpovědi, jinak vyvolá výjimku.

Pokud je architektura členství nakonfigurovaná tak, aby vyžadovala bezpečnostní otázku a odpověď, a přesto váš klient naruší, že správci budou moct měnit hesla uživatelů, máte tři možnosti:

- Vyvolejte svoji práci ve vzduchu a sdělte klientovi, že to je jenom jedna věc, kterou nejde udělat.
- Nastavte `RequiresQuestionAndAnswer` na false. Výsledkem je méně zabezpečená aplikace. Představte si, že uživatel nekalé získal přístup k e-mailové schránce jiného uživatele. Je možné, že ohrožený uživatel opustil svůj stůl, aby přešel na oběd a nezamkl svoji pracovní stanici nebo mohl získat e-mail z veřejného terminálu a odhlásil se. V obou případech může uživatel nekalé navštívit stránku `RecoverPassword.aspx` a zadat uživatelské jméno. Systém pak pošle obnovené heslo e-mailem bez výzvy k zadání bezpečnostní odpovědi.
- Obejít vrstvu abstrakce vytvořenou rozhraním členství a pracovat přímo s databází SQL Server. Schéma členství zahrnuje uloženou proceduru s názvem `aspnet_Membership_SetPassword`, která nastavuje heslo uživatele a nevyžaduje odpověď zabezpečení nebo původní heslo, aby bylo možné provést jeho úlohu.

Žádná z těchto možností nezpůsobuje zvláště odvolání, ale to je způsob, jakým se v některých případech stane doba, kterou vývojář spouští.

Jsem napřed a implementoval třetí přístup, psaní kódu, který obchází `Membership` a `MembershipUser` třídy a funguje přímo proti databázi `SecurityTutorials`.

> [!NOTE]
> Když pracujete přímo s databází, zapouzdření poskytované rozhraním členství je Shattered. Toto rozhodnutí spojuje s `SqlMembershipProvider`, takže náš kód je méně přenosný. Kromě toho tento kód nemusí fungovat podle očekávání v budoucích verzích ASP.NET, pokud se změní schéma členství. Tento přístup je alternativním řešením a podobně jako u většiny alternativních řešení není Příkladem osvědčených postupů.

Kód obsahuje některé neatraktivní bity a je poměrně dlouhý. Proto nechci, aby tento kurz byl v podrobném zkoumání. Pokud vás zajímá více informací, Stáhněte si kód pro tento kurz a navštivte stránku `~/Administration/ManageUsers.aspx`. Tato stránka, kterou jsme vytvořili v <a id="_msoanchor_5"> </a> [předchozím kurzu](building-an-interface-to-select-one-user-account-from-many-cs.md), uvádí jednotlivé uživatele. Aktualizoval (a) jsem prvek GridView, aby zahrnoval odkaz na stránku `UserInformation.aspx` a předává uživatelské jméno vybraného uživatele pomocí řetězce dotazu QueryString. Stránka `UserInformation.aspx` zobrazuje informace o vybraném uživateli a textová pole pro změnu hesla (viz obrázek 9).

Až zadáte nové heslo, potvrďte ho ve druhém textovém poli a klikněte na tlačítko Aktualizovat uživatele a vyvolá se `aspnet_Membership_SetPassword` uložená procedura a aktualizuje se heslo uživatele. Doporučujeme, aby se čtenáři, na které se tato funkce dozvěděly, seznámili s kódem a pokusili se rozšířit funkci, aby zahrnovala odeslání e-mailu uživateli, jehož heslo bylo změněno.

[![může správce změnit heslo uživatele.](recovering-and-changing-passwords-cs/_static/image26.png)](recovering-and-changing-passwords-cs/_static/image25.png)

**Obrázek 9**: Správce může změnit heslo uživatele ([kliknutím zobrazíte obrázek v plné velikosti](recovering-and-changing-passwords-cs/_static/image27.png)).

> [!NOTE]
> Stránka `UserInformation.aspx` aktuálně funguje pouze v případě, že je rozhraní členství nakonfigurováno pro ukládání hesel ve formátu Clear nebo hash. Chybí kód k zašifrování nového hesla, i když jste pozváni k přidání této funkce. Způsob, jakým je nutné přidat potřebný kód, je použít Decompiler jako [reflektor](http://www.aisto.com/roeder/dotnet/) k prohlédnutí zdrojového kódu pro metody v .NET Framework; Začněte kontrolou `ChangePassword` metody `SqlMembershipProvider` třídy. Toto je metoda, kterou jste použili k zápisu kódu pro vytvoření hodnoty hash hesla.

## <a name="summary"></a>Přehled

ASP.NET nabízí dva ovládací prvky, které uživatelům pomůžou spravovat jejich heslo. Ovládací prvek PasswordRecovery je vhodný pro uživatele, kteří zapomněli svá hesla. V závislosti na konfiguraci rozhraní členství má uživatel buď e-mailem své stávající heslo, nebo nové náhodně generované heslo. Ovládací prvek ChangePassword umožňuje uživateli aktualizovat heslo.

Podobně jako ovládací prvky login a ovládacím CreateUserWizard, ovládací prvky PasswordRecovery a ChangePassword vykreslují bohatou uživatelské rozhraní bez nutnosti psát Lick deklarativního kódu nebo řádku kódu. Pokud výchozí uživatelské rozhraní nevyhovuje vašim potřebám, můžete ho přizpůsobit pomocí nejrůznějších vlastností stylu. Alternativně lze rozhraní ovládacích prvků převést na šablony, a to i pro jemnější stupeň řízení. Na pozadí tyto ovládací prvky používají rozhraní API pro členství, vyvolává metody `ResetPassword` a `ChangePassword` objektu `MembershipUser`.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Rychlé starty ovládacího prvku ChangePassword](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/changepassword.aspx)
- [Rychlé starty ovládacího prvku PasswordRecovery](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/passwordrecovery.aspx)
- [Odesílání e-mailů v ASP.NET](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [Nejčastější dotazy k `System.Net.Mail`](http://www.systemnetmail.com/)

### <a name="about-the-author"></a>O autorovi

Scott Mitchell, autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je *[Sams naučit se ASP.NET 2,0 za 24 hodin](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* . Scott se dá kontaktovat [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu zahrnují Michael Emmings a Banerjee. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](building-an-interface-to-select-one-user-account-from-many-cs.md)
> [Další](unlocking-and-approving-user-accounts-cs.md)
