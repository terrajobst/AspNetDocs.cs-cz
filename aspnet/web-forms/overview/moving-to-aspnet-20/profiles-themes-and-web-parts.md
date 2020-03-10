---
uid: web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
title: Profily, motivy a Webové části | Microsoft Docs
author: microsoft
description: Konfigurace a instrumentace v ASP.NET 2,0 jsou významné změny. Nové rozhraní API konfigurace ASP.NET umožňuje provádět změny konfigurace...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 92df4051-77c6-492c-bd34-23d24189cea4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
msc.type: authoredcontent
ms.openlocfilehash: cf5c45781be6d003d28c6aa27efa08032579a6dd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78587232"
---
# <a name="profiles-themes-and-web-parts"></a>Profily, motivy a webové části

od [Microsoftu](https://github.com/microsoft)

> Konfigurace a instrumentace v ASP.NET 2,0 jsou významné změny. Nové rozhraní API konfigurace ASP.NET umožňuje provádět změny konfigurace prostřednictvím kódu programu. Kromě toho existuje mnoho nových nastavení konfigurace umožňujících nové konfigurace a instrumentaci.

ASP.NET 2,0 představuje podstatné zlepšení v oblasti individuálních webů. Kromě funkcí členství, které jsme již pokryli, ASP.NET profily, motivy a webové části významně zvyšují přizpůsobení webů.

## <a name="aspnet-profiles"></a>Profily ASP.NET

Profily ASP.NET se podobají relacím. Rozdílem je, že profil je trvalý, zatímco při zavření prohlížeče dojde ke ztrátě relace. Dalším velkým rozdílem mezi relacemi a profily je, že profily jsou silného typu, takže během procesu vývoje poskytují technologii IntelliSense.

Profil je definován buď v konfiguračním souboru počítačů, nebo v souboru Web. config pro aplikaci. (Profil nemůžete definovat v souboru Web. config v podadresářích.) Následující kód definuje profil pro uložení návštěvníků webu jméno a příjmení.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample1.xml)]

Výchozí datový typ pro vlastnost profilu je System. String. V předchozím příkladu není zadán žádný datový typ. Proto jsou vlastnosti FirstName a LastName oba typu řetězce. Jak už jsme uvedli, vlastnosti profilu jsou silného typu. Následující kód přidá novou vlastnost pro věk typu Int32.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample2.xml)]

Profily se obecně používají při ověřování pomocí formulářů ASP.NET. Při použití v kombinaci s ověřováním pomocí formulářů má každý uživatel samostatný profil přidružený k jejich ID uživatele. Je ale také možné umožnit používání profilů v anonymní aplikaci pomocí &lt;anonymousIdentification&gt; elementu v konfiguračním souboru spolu s atributem **AllowAnonymous** , jak je znázorněno níže:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample3.xml)]

Když tento web prochází anonymní uživatel, ASP.NET vytvoří pro uživatele instanci **ProfileCommon** . Tento profil používá jedinečné ID uložené v souboru cookie v prohlížeči k identifikaci uživatele jako jedinečného návštěvníka. Tímto způsobem můžete ukládat informace o profilu pro uživatele, kteří se prohlížejí anonymně.

## <a name="profile-groups"></a>Skupiny profilů

Je možné seskupit vlastnosti profilů. Seskupením vlastností lze simulovat více profilů pro konkrétní aplikaci.

Následující konfigurace nakonfiguruje vlastnost FirstName a LastName pro dvě skupiny; Kupující a potenciální zákazníci.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample4.xml)]

Pak je možné nastavit vlastnosti v určité skupině následujícím způsobem:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample5.cs)]

## <a name="storing-complex-objects"></a>Ukládání složitých objektů

Zde uvedené příklady obsahují v profilu uložené jednoduché datové typy. V profilu je také možné ukládat komplexní datové typy zadáním metody serializace pomocí atributu **SerializeAs** následujícím způsobem:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample6.xml)]

V tomto případě je typ PurchaseInvoice. Třída PurchaseInvoice musí být označena jako serializovatelný a může obsahovat libovolný počet vlastností. Například pokud má PurchaseInvoice vlastnost s názvem **NumItemsPurchased**, můžete odkazovat na tuto vlastnost v kódu následujícím způsobem:

[!code-css[Main](profiles-themes-and-web-parts/samples/sample7.css)]

## <a name="profile-inheritance"></a>Dědičnost profilu

Je možné vytvořit profil pro použití ve více aplikacích. Vytvořením třídy profilu, která je odvozena z ProfileBase, můžete znovu použít profil v několika aplikacích pomocí atributu **Inherits** , jak je uvedeno níže:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample8.xml)]

V takovém případě by třída **PurchasingProfile** vypadala takto:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample9.cs)]

## <a name="profile-providers"></a>Poskytovatelé profilu

ASP.NET profily používají model poskytovatele. Výchozí zprostředkovatel ukládá informace v databázi SQL Server Express ve složce App\_data webové aplikace pomocí poskytovatele SqlProfileProvider. Pokud databáze neexistuje, ASP.NET se automaticky vytvoří, když se profil pokusí uložit informace.

V některých případech však můžete chtít vyvinout vlastního poskytovatele profilu. Funkce profilu ASP.NET vám umožňuje snadno používat různé poskytovatele.

Vlastního poskytovatele profilu vytvoříte v těchto případech:

- Je nutné uložit informace o profilu ve zdroji dat, například v databázi FoxPro nebo v databázi Oracle, které nejsou podporovány poskytovateli profilu, kteří jsou součástí .NET Framework.
- Musíte spravovat informace o profilu pomocí schématu databáze, které se liší od schématu databáze používaného poskytovateli, kteří jsou součástí .NET Framework. Běžným příkladem je, že chcete integrovat informace o profilu s uživatelskými daty v existující databázi SQL Server.

### <a name="required-classes"></a>Požadované třídy

Chcete-li implementovat poskytovatele profilu, vytvořte třídu, která dědí z abstraktní třídy System. Web. Profile. ProfileProvider. Abstraktní třída **ProfileProvider** zase dědí abstraktní třídu System. Configuration. modulu SettingsProvider, která dědí abstraktní třídu System. Configuration. Provider. ProviderBase. Z důvodu tohoto řetězce dědičnosti kromě požadovaných členů třídy **ProfileProvider** je nutné implementovat požadované členy tříd **modulu SettingsProvider** a **ProviderBase** .

Následující tabulky popisují vlastnosti a metody, které je nutné implementovat z abstraktních tříd **ProviderBase**, **modulu SettingsProvider**a **ProfileProvider** .

### <a name="providerbase-members"></a>ProviderBase členové

| **Člen** | **Popis** |
| --- | --- |
| Initialize – metoda | Jako vstup bere název instance poskytovatele a kolekce NameValueCollection nastavení konfigurace. Slouží k nastavení možností a hodnot vlastností pro instanci zprostředkovatele, včetně hodnot specifických pro implementaci a možností zadaných v konfiguraci počítače nebo souboru Web. config. |

### <a name="settingsprovider-members"></a>Modulu SettingsProvider členové

| **Člen** | **Popis** |
| --- | --- |
| ApplicationName – vlastnost | Název aplikace, který je uložený spolu s každým profilem. Poskytovatel profilu používá název aplikace k ukládání informací o profilu samostatně pro každou aplikaci. To umožňuje více aplikacím ASP.NET používat stejný zdroj dat bez konfliktu, pokud se stejné uživatelské jméno vytvoří v různých aplikacích. Alternativně může více aplikací ASP.NET sdílet profilový zdroj dat zadáním stejného názvu aplikace. |
| GetPropertyValues – metoda | Přijímá jako vstup objekt SettingsContext a objekt SettingsPropertyCollection. **SettingsContext** poskytuje informace o uživateli. Tyto informace můžete použít jako primární klíč k načtení informací o vlastnostech profilu pro uživatele. Použijte objekt **SettingsContext** k získání uživatelského jména a uživatele, zda je ověřen nebo anonymní. **SettingsPropertyCollection** obsahuje kolekci objektů SettingsProperty. Každý objekt **SettingsProperty** poskytuje název a typ vlastnosti a také další informace, jako je například výchozí hodnota vlastnosti a určuje, zda je vlastnost určena pouze pro čtení. Metoda **GetPropertyValues** naplní SettingsPropertyValueCollection objekty SettingsPropertyValue na základě objektů **SettingsProperty** poskytovaných jako vstup. Hodnoty ze zdroje dat pro zadaného uživatele jsou přiřazeny k vlastnostem PropertyValue pro každý objekt **SettingsPropertyValue** a je vrácena celá kolekce. Volání metody také aktualizuje hodnotu LastActivityDate pro zadaný uživatelský profil na aktuální datum a čas. |
| Metoda SetPropertyValues | Přijímá jako vstup objekt **SettingsContext** a objekt **SettingsPropertyValueCollection** . **SettingsContext** poskytuje informace o uživateli. Tyto informace můžete použít jako primární klíč k načtení informací o vlastnostech profilu pro uživatele. Použijte objekt **SettingsContext** k získání uživatelského jména a uživatele, zda je ověřen nebo anonymní. **SettingsPropertyValueCollection** obsahuje kolekci objektů **SettingsPropertyValue** . Každý objekt **SettingsPropertyValue** poskytuje název, typ a hodnotu vlastnosti a také další informace, jako je například výchozí hodnota vlastnosti a určuje, zda je vlastnost určena pouze pro čtení. Metoda **SetPropertyValues** aktualizuje hodnoty vlastností profilu ve zdroji dat pro zadaného uživatele. Volání metody také aktualizuje hodnoty **LastActivityDate** a LastUpdatedDate pro zadaný profil uživatele na aktuální datum a čas. |

### <a name="profileprovider-members"></a>ProfileProvider členové

| **Člen** | **Popis** |
| --- | --- |
| Metoda DeleteProfiles | Přijímá jako vstup pole řetězců pro uživatelská jména a odstraní je ze zdroje dat všechny informace o profilu a hodnot vlastností pro zadané názvy, kde název aplikace odpovídá hodnotě vlastnosti **ApplicationName** . Pokud váš zdroj dat podporuje transakce, doporučujeme zahrnout všechny operace odstranění v transakci a vrátit zpět transakci a vyvolat výjimku, pokud dojde k chybě jakékoli operace odstranění. |
| Metoda DeleteProfiles | Přijímá jako vstup kolekci objektů ProfileInfo a odstraní je ze zdroje dat všechny informace o profilu a hodnoty vlastností pro každý profil, kde název aplikace odpovídá hodnotě vlastnosti **ApplicationName** . Pokud váš zdroj dat podporuje transakce, je doporučeno zahrnout všechny operace odstranění v transakci a vrátit transakci zpět a vyvolat výjimku, pokud dojde k chybě jakékoli operace odstranění. |
| Metoda DeleteInactiveProfiles | Přijímá jako vstup hodnotu ProfileAuthenticationOption a objekt DateTime a odstraní je ze zdroje dat všechny informace o profilu a hodnoty vlastností, kde je datum poslední aktivity menší nebo rovno zadanému datu a času a kde se název aplikace shoduje s hodnotou vlastnosti **ApplicationName** . Parametr **ProfileAuthenticationOption** určuje, zda mají být odstraněny pouze anonymní profily, pouze ověřené profily nebo všechny profily. Pokud váš zdroj dat podporuje transakce, je doporučeno zahrnout všechny operace odstranění v transakci a vrátit transakci zpět a vyvolat výjimku, pokud dojde k chybě jakékoli operace odstranění. |
| Metoda GetAllProfiles | Přijímá jako vstup hodnotu **ProfileAuthenticationOption** , celé číslo, které určuje index stránky, celé číslo, které určuje velikost stránky, a odkaz na celé číslo, které bude nastaveno na celkový počet profilů. Vrátí ProfileInfoCollection, který obsahuje objekty **ProfileInfo** pro všechny profily ve zdroji dat, kde název aplikace odpovídá hodnotě vlastnosti **ApplicationName** . Parametr **ProfileAuthenticationOption** určuje, zda mají být vráceny pouze anonymní profily, pouze ověřené profily nebo všechny profily. Výsledky vrácené metodou **GetAllProfiles** jsou omezeny hodnotami indexu stránky a velikostí stránky. Hodnota velikosti stránky určuje maximální počet **ProfileInfo** objektů, které se mají vrátit v **ProfileInfoCollection**. Hodnota index stránky určuje, kterou stránku výsledků mají vracet, přičemž 1 identifikuje první stránku. Parametr pro celkový počet záznamů je výstupní parametr (v Visual Basic můžete použít **ByRef** ), který je nastavený na celkový počet profilů. Pokud například úložiště dat obsahuje 13 profilů pro aplikaci a hodnota indexu stránky je 2 s velikostí stránky 5, vrácený **ProfileInfoCollection** obsahuje šest až desáté profily. Hodnota celkem záznamů je nastavená na 13, když se metoda vrátí. |
| Metoda GetAllInactiveProfiles | Přijímá jako vstup hodnotu **ProfileAuthenticationOption** , objekt **DateTime** , celé číslo, které určuje index stránky, celé číslo, které určuje velikost stránky, a odkaz na celé číslo, které bude nastaveno na celkový počet profilů. Vrátí **ProfileInfoCollection** , který obsahuje objekty **ProfileInfo** pro všechny profily ve zdroji dat, kde je datum poslední aktivity menší nebo rovno zadané hodnotě **DateTime** a kde se název aplikace shoduje s hodnotou vlastnosti **ApplicationName** . Parametr **ProfileAuthenticationOption** určuje, zda mají být vráceny pouze anonymní profily, pouze ověřené profily nebo všechny profily. Výsledky vrácené metodou **GetAllInactiveProfiles** jsou omezeny hodnotami indexu stránky a velikostí stránky. Hodnota velikosti stránky určuje maximální počet **ProfileInfo** objektů, které se mají vrátit v **ProfileInfoCollection**. Hodnota index stránky určuje, kterou stránku výsledků mají vracet, přičemž 1 identifikuje první stránku. Parametr pro celkový počet záznamů je výstupní parametr (v Visual Basic můžete použít **ByRef** ), který je nastavený na celkový počet profilů. Pokud například úložiště dat obsahuje 13 profilů pro aplikaci a hodnota indexu stránky je 2 s velikostí stránky 5, vrácený **ProfileInfoCollection** obsahuje šest až desáté profily. Hodnota celkem záznamů je nastavená na 13, když se metoda vrátí. |
| Metoda FindProfilesByUserName | Přijímá jako vstup hodnotu **ProfileAuthenticationOption** , řetězec obsahující uživatelské jméno, celé číslo, které určuje index stránky, celé číslo, které určuje velikost stránky, a odkaz na celé číslo, které bude nastaveno na celkový počet profilů. Vrátí **ProfileInfoCollection** , který obsahuje objekty **ProfileInfo** pro všechny profily ve zdroji dat, kde uživatelské jméno odpovídá zadanému uživatelskému jménu a název aplikace se shoduje s hodnotou vlastnosti **ApplicationName** . Parametr **ProfileAuthenticationOption** určuje, zda mají být vráceny pouze anonymní profily, pouze ověřené profily nebo všechny profily. Pokud váš zdroj dat podporuje další možnosti vyhledávání, například zástupné znaky, můžete pro uživatelská jména poskytnout rozsáhlejší možnosti vyhledávání. Výsledky vrácené metodou **FindProfilesByUserName** jsou omezeny hodnotami indexu stránky a velikostí stránky. Hodnota velikosti stránky určuje maximální počet **ProfileInfo** objektů, které se mají vrátit v **ProfileInfoCollection**. Hodnota index stránky určuje, kterou stránku výsledků mají vracet, přičemž 1 identifikuje první stránku. Parametr pro celkový počet záznamů je výstupní parametr (v Visual Basic můžete použít **ByRef** ), který je nastavený na celkový počet profilů. Pokud například úložiště dat obsahuje 13 profilů pro aplikaci a hodnota indexu stránky je 2 s velikostí stránky 5, vrácený **ProfileInfoCollection** obsahuje šest až desáté profily. Hodnota celkem záznamů je nastavená na 13, když se metoda vrátí. |
| FindInactiveProfilesByUserName method | Přijímá jako vstup hodnotu **ProfileAuthenticationOption** , řetězec obsahující uživatelské jméno, objekt **DateTime** , celé číslo, které určuje index stránky, celé číslo, které určuje velikost stránky, a odkaz na celé číslo, které bude nastaveno na celkový počet profilů. Vrátí **ProfileInfoCollection** , který obsahuje **objekty ProfileInfo** pro všechny profily ve zdroji dat, kde uživatelské jméno odpovídá zadanému uživatelskému jménu, kde je datum poslední aktivity menší nebo rovno **zadanému**datu a kde se název aplikace shoduje s hodnotou vlastnosti **ApplicationName** . Parametr **ProfileAuthenticationOption** určuje, zda mají být vráceny pouze anonymní profily, pouze ověřené profily nebo všechny profily. Pokud váš zdroj dat podporuje další možnosti vyhledávání, například zástupné znaky, můžete pro uživatelská jména poskytnout rozsáhlejší možnosti vyhledávání. Výsledky vrácené metodou **FindInactiveProfilesByUserName** jsou omezeny hodnotami indexu stránky a velikostí stránky. Hodnota velikosti stránky určuje maximální počet **ProfileInfo** objektů, které se mají vrátit v **ProfileInfoCollection**. Hodnota index stránky určuje, kterou stránku výsledků mají vracet, přičemž 1 identifikuje první stránku. Parametr pro celkový počet záznamů je výstupní parametr (v Visual Basic můžete použít **ByRef** ), který je nastavený na celkový počet profilů. Pokud například úložiště dat obsahuje 13 profilů pro aplikaci a hodnota indexu stránky je 2 s velikostí stránky 5, vrácený **ProfileInfoCollection** obsahuje šest až desáté profily. Hodnota celkem záznamů je nastavená na 13, když se metoda vrátí. |
| Metoda GetNumberOfInActiveProfiles | Přijímá jako vstup hodnotu **ProfileAuthenticationOption** a objekt **DateTime** a vrátí počet všech profilů ve zdroji dat, kde je datum poslední aktivity menší nebo rovno zadanému **datu a kde** se název aplikace shoduje s hodnotou vlastnosti **ApplicationName** . Parametr **ProfileAuthenticationOption** určuje, zda se mají počítat pouze anonymní profily, pouze ověřené profily nebo všechny profily. |

### <a name="applicationname"></a>ApplicationName

Vzhledem k tomu, že poskytovatelé profilu ukládají informace o profilu samostatně pro každou aplikaci, je nutné zajistit, aby vaše schéma dat zahrnovalo název aplikace a aby dotazy a aktualizace zahrnovaly také název aplikace. Například následující příkaz slouží k načtení hodnoty vlastnosti z databáze na základě uživatelského jména a toho, zda je profil anonymní, a zajišťuje, že je hodnota **ApplicationName** obsažena v dotazu.

[!code-sql[Main](profiles-themes-and-web-parts/samples/sample10.sql)]

## <a name="aspnet-themes"></a>ASP.NET motivy

## <a name="what-are-aspnet-20-themes"></a>Co jsou motivy ASP.NET 2,0?

Jedním z nejdůležitějších aspektů webové aplikace je konzistentní vzhled a chování napříč lokalitou. Vývojáři ASP.NET 1. x obvykle používají šablony stylů CSS (CSS) k implementaci konzistentního vzhledu a chování. Motivy ASP.NET 2,0 se podstatně zlepšují na základě šablony stylů CSS, protože dávají vývojářovi ASP.NET možnost definovat vzhled ovládacích prvků ASP.NET serveru i HTML elementy. Motivy ASP.NET lze použít pro jednotlivé ovládací prvky, konkrétní webové stránky nebo celou webovou aplikaci. Motivy používají kombinaci souborů CSS, volitelného souboru skinu a volitelného adresáře obrázků, pokud jsou potřebné obrázky. Soubor skinu ovládá vzhled ovládacích prvků ASP.NET serveru.

## <a name="where-are-themes-stored"></a>Kde jsou motivy uloženy?

Umístění, kde se motivy ukládají, se liší v závislosti na jejich oboru. Motivy, které lze použít pro libovolnou aplikaci, jsou uloženy v následující složce:

`C:\WINDOWS\Microsoft.NET\Framework\v2.x.xxxxx\ASP.NETClientFiles\Themes\<Theme_Name>`

Motiv, který je specifický pro konkrétní aplikaci, je uložený v adresáři `App\_Themes\<Theme\_Name>` v kořenu webu.

> [!NOTE]
> Soubor skinu by měl upravovat jenom vlastnosti serverového ovládacího prvku, které mají vliv na vzhled.

Globální motiv je motiv, který se dá použít pro libovolnou aplikaci nebo web běžící na webovém serveru. Tyto motivy jsou ve výchozím nastavení uloženy v adresáři ASP. NETClientfiles\Themes, který se nachází uvnitř adresáře v2. x. xxxxx. Případně můžete soubory motivů přesunout do složky ASPNET\_Client/System\_web/[verze]/Themes/[motiv\_název] v kořenovém adresáři webu.

Motivy specifické pro aplikaci lze použít pouze pro aplikaci, ve které jsou umístěny soubory. Tyto soubory jsou uloženy v adresáři `App\_Themes/<theme\_name>` v kořenové složce webu.

## <a name="the-components-of-a-theme"></a>Komponenty motivu

Motiv se skládá z jednoho nebo více souborů CSS, volitelného souboru vzhledu a volitelné složky imagí. Soubory CSS můžou být libovolný název, který si přejete (například default. CSS nebo Theme. CSS atd.) a musí být v kořenovém adresáři složky themes. Soubory CSS slouží k definování běžných tříd a atributů šablon stylů CSS pro konkrétní selektory. Chcete-li použít jednu z tříd CSS na prvek stránky, je použita vlastnost **CSSClass** .

Soubor skinu je soubor XML, který obsahuje definice vlastností pro serverové ovládací prvky ASP.NET. Níže uvedený kód je ukázkový soubor skinu.

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample11.aspx)]

**Obrázek 1** níže ukazuje malou stránku ASP.NET s procházením bez použití motivu. **Obrázek 2** ukazuje stejný soubor s použitým motivem. Barva pozadí a barva textu jsou konfigurovány pomocí souboru CSS. Vzhled tlačítka a textového pole se konfiguruje pomocí souboru skinu uvedeného výše.

![Žádný motiv](profiles-themes-and-web-parts/_static/image1.gif)

**Obrázek 1**: žádný motiv

![Motiv použit](profiles-themes-and-web-parts/_static/image2.gif)

**Obrázek 2**: použit motiv

Soubor skinu uvedený výše definuje výchozí vzhled pro všechny ovládací prvky TextBox a ovládací prvky tlačítek. To znamená, že každý ovládací prvek TextBox a ovládací prvek tlačítko vložený na stránce bude pobírat tento vzhled. Můžete také definovat Skin, který lze použít na konkrétní instance těchto ovládacích prvků pomocí vlastnosti **SkinID** ovládacího prvku.

Následující kód definuje vzhled ovládacího prvku tlačítko. Pouze ovládací prvky tlačítka s vlastností **SkinID** třídy **goButton** budou přebírat vzhled vzhledu.

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample12.aspx)]

Můžete mít jenom jeden výchozí vzhled pro každý typ ovládacího prvku serveru. Pokud požadujete další vzhledy, měli byste použít vlastnost SkinID.

## <a name="applying-themes-to-pages"></a>Použití motivů na stránkách

Motiv lze použít pomocí kterékoli z následujících metod:

- Na stránkách &lt;&gt; elementu souboru Web. config
- V direktivě @Page stránky
- Prostřednictvím kódu programu

## <a name="applying-a-theme-in-the-configuration-file"></a>Použití motivu v konfiguračním souboru

Chcete-li použít motiv v konfiguračním souboru aplikace, použijte následující syntaxi:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample13.xml)]

Název motivu, který je zde zadaný, musí odpovídat názvu složky themes. Tato složka může existovat buď v jednom z umístění uvedených výše v tomto kurzu. Pokud se pokusíte použít motiv, který neexistuje, dojde k chybě konfigurace.

## <a name="applying-a-theme-in-the-page-directive"></a>Použití motivu v direktivě Page

Motiv můžete použít také v direktivě @ Page. Tato metoda umožňuje použít motiv pro konkrétní stránku.

Chcete-li použít motiv v direktivě @Page, použijte následující syntaxi:

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample14.aspx)]

Níže uvedený motiv se musí shodovat se složkou motivu, jak je uvedeno výše. Pokud se pokusíte použít motiv, který neexistuje, dojde k selhání sestavení. Visual Studio také zvýrazní atribut a upozorní vás, že žádný takový motiv neexistuje.

## <a name="applying-a-theme-programmatically"></a>Programové použití motivu

Chcete-li použít motiv programově, je nutné zadat vlastnost **Theme** stránky na **stránce\_předinicializační** metoda.

Chcete-li použít motiv programově, použijte následující syntaxi:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample15.cs)]

Je nutné použít motiv v metodě předinit z důvodu životního cyklu stránky. Pokud ji použijete po tomto okamžiku, motiv stránky již byl použit modulem runtime a změna v tomto okamžiku je příliš pozdě v životním cyklu. Pokud použijete motiv, který neexistuje, dojde k **HttpException –** . Pokud je motiv použit programově, bude k dispozici upozornění sestavení, pokud kterýkoli serverový ovládací prvek má zadanou vlastnost SkinID. Toto upozornění je určeno k tomu, aby vám informovalo, že žádný motiv není deklarativně použit a může být ignorován.

## <a name="exercise-1--applying-a-theme"></a>Cvičení 1: použití motivu

V tomto cvičení použijete motiv ASP.NET na webu.

> [!IMPORTANT]
> Pokud k zadání informací do souboru Skin používáte Microsoft Word, ujistěte se, že nenahrazujete běžné uvozovky pomocí inteligentních uvozovek. Inteligentní uvozovky způsobí problémy se soubory skinu.

1. Vytvořte nový web ASP.NET.
2. V Průzkumník řešení klikněte pravým tlačítkem na projekt a vyberte možnost Přidat novou položku.
3. V seznamu souborů vyberte možnost soubor webové konfigurace a klikněte na tlačítko Přidat.
4. V Průzkumník řešení klikněte pravým tlačítkem na projekt a vyberte možnost Přidat novou položku.
5. Vyberte soubor skinu a klikněte na Přidat.
6. Po zobrazení výzvy klikněte na tlačítko Ano, pokud chcete umístit soubor do složky\_ch motivů aplikace.
7. Klikněte pravým tlačítkem myši na složku SkinFile ve složce\_aplikace v Průzkumník řešení a vyberte možnost Přidat novou položku.
8. V seznamu souborů vyberte šablonu stylů a klikněte na Přidat. Nyní máte všechny soubory nezbytné k implementaci nového motivu. Sada Visual Studio však má název složky Themes SkinFile. Klikněte pravým tlačítkem na tuto složku a změňte její název na CoolTheme.
9. Otevřete soubor SkinFile. Skin a přidejte následující kód na konec souboru: 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample16.aspx)]
10. Uložte soubor SkinFile. Skin.
11. Otevřete šablonu stylů. CSS.
12. Celý text v něm nahraďte následujícím textem: 

    [!code-css[Main](profiles-themes-and-web-parts/samples/sample17.css)]
13. Uložte soubor StyleSheet. CSS.
14. Otevřete stránku Default. aspx.
15. Přidejte ovládací prvek TextBox a ovládací prvek tlačítko.
16. Uložte stránku. Teď přejděte na stránku Default. aspx. Měl by se zobrazit jako normální webový formulář.
17. Otevřete soubor Web. config.
18. Přímo pod otevírací značku `<system.web>` přidejte následující: 

    [!code-xml[Main](profiles-themes-and-web-parts/samples/sample18.xml)]
19. Uložte soubor Web. config. Teď přejděte na stránku Default. aspx. Měl by se zobrazit s použitým motivem.
20. Pokud ještě není otevřený, otevřete stránku Default. aspx v aplikaci Visual Studio.
21. Vyberte tlačítko.
22. Změňte vlastnost **SkinID** na goButton. Všimněte si, že Visual Studio poskytuje rozevírací seznam s platnými SkinID hodnotami pro ovládací prvek tlačítko.
23. Uložte stránku. Teď zobrazte náhled stránky v prohlížeči znovu. Tlačítko by nyní mělo vyslovit "Přejít" a mělo by být širší vzhledem.

Pomocí vlastnosti **SkinID** můžete snadno nakonfigurovat různé vzhledy pro různé instance konkrétního typu serverového ovládacího prvku.

## <a name="the-stylesheettheme-property"></a>Vlastnost StyleSheetTheme

Zatím jsme mluvili jenom o použití motivů pomocí vlastnosti Theme. Při použití vlastnosti Theme přepíše soubor Skin všechna deklarativní nastavení pro serverové ovládací prvky. Například v cvičení 1 jste zadali SkinID "goButton" pro ovládací prvek tlačítko a změnili jste text tlačítka na "Přejít". Možná jste si všimli, že vlastnost text tlačítka v Návrháři byla nastavena na tlačítko "tlačítko", ale motiv overrode. Motiv vždy přepíše všechna nastavení vlastností v návrháři.

Pokud byste chtěli mít možnost přepsat vlastnosti definované v souboru skinu motivu pomocí vlastností zadaných v návrháři, můžete místo vlastnosti Theme použít vlastnost **StyleSheetTheme** . Vlastnost StyleSheetTheme je stejná jako vlastnost Theme s tím rozdílem, že nepřepisuje všechna explicitní nastavení vlastností, jako je vlastnost Theme.

Chcete-li se podívat v akci, otevřete soubor Web. config z projektu v cvičení 1 a změňte `<pages>` element na následující:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample19.xml)]

Teď přejděte na stránku Default. aspx a uvidíte, že ovládací prvek tlačítko má vlastnost text pro tlačítko "tlačítko". Důvodem je, že nastavení explicitní vlastnosti v Návrháři Přepisuje vlastnost text nastavenou vlastností goButton SkinID.

## <a name="overriding-themes"></a>Přepsání motivů

Globální motiv se dá přepsat použitím motivu se stejným názvem ve složce\_ch motivů aplikace. Motiv však není aplikován ve scénáři true override. Pokud modul runtime nalezne soubory motivů ve složce App\_Themes, použije motiv s použitím těchto souborů a bude globální motiv ignorovat.

Vlastnost StyleSheetTheme je přepsatelné a lze ji přepsat v kódu následujícím způsobem:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample20.cs)]

## <a name="web-parts"></a>Webové části

ASP.NET Webové části je integrovaná sada ovládacích prvků pro vytváření webů, které umožňují koncovým uživatelům upravovat obsah, vzhled a chování webových stránek přímo z prohlížeče. Změny lze použít pro všechny uživatele na webu nebo pro jednotlivé uživatele. Když uživatelé upravují stránky a ovládací prvky, můžete nastavení uložit, abyste zachovali osobní preference uživatele v budoucích relacích prohlížeče, což je funkce s názvem přizpůsobení. Tyto Webové části funkce znamenají, že vývojáři můžou uživatelům umožnit, aby se webové aplikace přizpůsobili dynamicky bez zásahu vývojářů nebo správců.

Pomocí sady ovládacích prvků Webové části můžete jako vývojář umožnit koncovým uživatelům:

- Přizpůsobení obsahu stránky. Uživatelé mohou přidat nové ovládací prvky Webové části na stránku, odebrat je, skrýt nebo minimalizovat, jako jsou běžná okna.
- Přizpůsobení rozložení stránky. Uživatelé mohou přetáhnout ovládací prvek Webové části do jiné zóny na stránce nebo změnit jeho vzhled, vlastnosti a chování.
- Exportovat a importovat ovládací prvky. Uživatelé mohou importovat nebo exportovat nastavení řízení Webové části pro použití na jiných stránkách nebo webech, zachovat vlastnosti, vzhled a dokonce i data v ovládacích prvcích. Tím se sníží požadavky na zadání dat a konfiguraci pro koncové uživatele.
- Vytvořte připojení. Uživatelé mohou navázat spojení mezi ovládacími prvky tak, aby například ovládací prvek grafu mohl zobrazit graf pro data v burzovním ovládacím prvku. Uživatelé mohou přizpůsobit nejen samotné připojení, ale vzhled a podrobnosti o tom, jak ovládací prvek grafu zobrazuje data.
- Umožňuje spravovat a přizpůsobovat nastavení na úrovni webu. Autorizovaní uživatelé mohou konfigurovat nastavení na úrovni webu, určit, kdo má přístup k webu nebo stránce, nastavit přístup založený na rolích k ovládacím prvkům a tak dále. Uživatel v roli správce například může nastavit, aby byl ovládací prvek Webové části sdílen všemi uživateli, a zabránit uživatelům, kteří nejsou správci, přizpůsobení sdíleného ovládacího prvku.

Obvykle budete pracovat s Webové části jedním ze tří způsobů: vytváření stránek, které používají ovládací prvky Webové části, vytváření individuálních ovládacích prvků Webové části nebo vytváření kompletních a přizpůsobitelných webových aplikací, jako je například portál.

## <a name="page-development"></a>Vývoj stránky

Vývojáři stránky mohou pomocí nástrojů pro vizuální návrh, jako je například Microsoft Visual Studio 2005, vytvářet stránky, které používají Webové části. Jednou z výhod použití nástroje, jako je například Visual Studio, je, že sada ovládacích prvků Webové části poskytuje funkce pro vytváření a konfiguraci Webové části ovládacích prvků ve vizuálním návrháři. Můžete například použít návrháře k přetažení Webové části zóny nebo ovládacího prvku editoru Webové části na návrhovou plochu a následně nakonfigurovat ovládací prvek vpravo v Návrháři pomocí uživatelského rozhraní poskytnutého sadou ovládacího prvku Webové části. To může urychlit vývoj aplikací Webové části a snížit množství kódu, který musíte napsat.

## <a name="control-development"></a>Vývoj ovládacích prvků

Můžete použít jakýkoli existující ovládací prvek ASP.NET jako ovládací prvek pro Webové části, včetně standardních ovládacích prvků webového serveru, vlastních serverových ovládacích prvků a uživatelských ovládacích prvků. Pro maximální programové řízení vašeho prostředí můžete také vytvořit vlastní Webové části ovládací prvky, které jsou odvozeny z třídy WebPart. Pro individuální vývoj ovládacích prvků Webové části obvykle buď vytvoříte uživatelský ovládací prvek a použijete ho jako ovládací prvek Webové části, nebo můžete vyvinout vlastní ovládací prvek Webové části.

Jako příklad vývoje vlastního ovládacího prvku Webové části můžete vytvořit ovládací prvek, který poskytuje kteroukoli z funkcí poskytovaných jinými ovládacími prvky serveru ASP.NET, které mohou být užitečné pro balení jako přizpůsobitelný Webové části ovládací prvek: kalendáře, seznamy, finanční informace, Novinky, kalkulačky, ovládací prvky formátovaného textu pro aktualizaci obsahu, upravitelné mřížky, které se připojují k databázím, grafů, které dynamicky aktualizují své displeje, nebo počasí a cestovní informace. Pokud přidáváte vizuálního návrháře s vaším ovládacím prvkem, pak libovolný vývojář stránky, který používá Visual Studio, může jednoduše přetáhnout ovládací prvek do zóny Webové části a nakonfigurovat ho v době návrhu bez nutnosti psát další kód.

Přizpůsobení je základem funkce Webové části. Umožňuje uživatelům upravit nebo přizpůsobit – rozložení, vzhled a chování Webové částich ovládacích prvků na stránce. Individuální nastavení jsou dlouhodobá: jsou trvalá nejen během aktuální relace prohlížeče (jako u stavu zobrazení), ale také v dlouhodobém úložišti, aby se nastavení uživatele ukládalo i pro budoucí relace prohlížeče. Přizpůsobení je ve výchozím nastavení povoleno pro Webové části stránky.

Strukturální komponenty uživatelského rozhraní spoléhají na přizpůsobení a poskytují základní strukturu a služby potřebné pro všechny Webové části ovládací prvky. Jedna součást konstrukce uživatelského rozhraní požadovaná na každé stránce Webové části je ovládací prvek WebPartManager. I když nikdy nevidí, má tento ovládací prvek kritickou úlohu koordinace všech Webové částich ovládacích prvků na stránce. Například sleduje všechny jednotlivé ovládací prvky Webové části. Spravuje Webové části zóny (oblasti, které obsahují ovládací prvky Webové části na stránce) a na kterých ovládacích prvcích se nacházejí. Také sleduje a ovládá různé režimy zobrazení, ve kterých může být stránka, jako je například procházení, připojení, úpravy nebo režim katalogu, a to, zda se změny přizpůsobení vztahují na všechny uživatele nebo na jednotlivé uživatele. Nakonec Inicializuje a sleduje připojení a komunikaci mezi ovládacími prvky Webové části.

Druhý druh strukturální komponenty uživatelského rozhraní je zóna. Zóny slouží jako správci rozložení na stránce Webové části. Obsahují a organizují ovládací prvky, které jsou odvozeny z třídy součásti (ovládací prvky části), a poskytují možnost vytvářet modulární rozložení stránky buď ve vodorovném nebo svislém směru. Zóny také nabízí společné a konzistentní prvky uživatelského rozhraní (například styl záhlaví a zápatí, název, styl ohraničení, tlačítka akcí atd.) pro každý ovládací prvek, který obsahují. Tyto společné prvky jsou označovány jako okolí ovládacího prvku. V různých režimech zobrazení a s různými ovládacími prvky se používá několik specializovaných typů zón. Různé typy zón jsou popsány v části Webové části základní ovládací prvky níže.

Webové části ovládací prvky uživatelského rozhraní, které jsou odvozeny z třídy **součásti** , tvořené primárním uživatelským rozhraním stránky webové části. Sada ovládacích prvků Webové části je flexibilní a zahrnutá v možnostech, které vám dává možnost vytvářet ovládací prvky částí. Kromě vytváření vlastních ovládacích prvků Webové části můžete také použít stávající ovládací prvky serveru ASP.NET, uživatelské ovládací prvky nebo vlastní serverové ovládací prvky jako Webové části ovládací prvky. Základní ovládací prvky, které jsou nejčastěji používány pro vytváření Webové části stránek, jsou popsány v následující části.

## <a name="web-parts-essential-controls"></a>Webové části základní ovládací prvky

Sada ovládacích prvků Webové části je rozsáhlá, ale některé ovládací prvky jsou nezbytné, protože jsou nutné k tomu, aby Webové části fungovaly, nebo protože se jedná o ovládací prvky nejčastěji používané na Webové části stránkách. Když začnete používat Webové části a vytváříte základní Webové části stránky, je užitečné znát základní Webové části ovládací prvky popsané v následující tabulce.

| **Ovládací prvek Webové části** | **Popis** |
| --- | --- |
| WebPartManager | Spravuje všechny Webové části ovládací prvky na stránce. Pro každou Webové části stránku je vyžadován pouze jeden ovládací prvek **WebPartManager** (a pouze jeden). |
| CatalogZone | Obsahuje ovládací prvky CatalogPart. Pomocí této zóny můžete vytvořit katalog Webové částich ovládacích prvků, ze kterých mohou uživatelé vybírat ovládací prvky pro přidání na stránku. |
| EditorZone | Obsahuje ovládací prvky EditorPart. Pomocí této zóny můžete uživatelům umožnit úpravy a přizpůsobení Webové části ovládacích prvků na stránce. |
| Prvku | Obsahuje a poskytuje celkové rozložení pro ovládací prvky webové části, které tvoří hlavní uživatelské rozhraní stránky. Tuto zónu použijte vždy, když vytvoříte stránky s ovládacími prvky Webové části. Stránky mohou obsahovat jednu nebo více zón. |
| ConnectionsZone | Obsahuje ovládací prvky WebPartConnection a poskytuje uživatelské rozhraní pro správu připojení. |
| WebPart (GenericWebPart) | Vykreslí primární uživatelské rozhraní. do této kategorie patří většina Webové části ovládacích prvků uživatelského rozhraní. Pro maximální programové řízení můžete vytvořit vlastní Webové části ovládací prvky, které jsou odvozeny ze základního ovládacího prvku **WebPart** . Můžete také použít existující ovládací prvky serveru, uživatelské ovládací prvky nebo vlastní ovládací prvky jako ovládací prvky Webové části. Pokaždé, když jsou některé z těchto ovládacích prvků umístěny v zóně, ovládací prvek **WebPartManager** je automaticky zalomí s ovládacími prvky **GenericWebPart** za běhu, takže je lze použít s funkcí webové části. |
| Prvku | Obsahuje seznam dostupných Webové částich ovládacích prvků, které mohou uživatelé přidat na stránku. |
| WebPartConnection | Vytvoří propojení mezi dvěma ovládacími prvky Webové části na stránce. Připojení definuje jeden z ovládacích prvků Webové části jako zprostředkovatele (data) a druhý jako příjemce. |
| EditorPart | Slouží jako základní třída pro specializované ovládací prvky editoru. |
| Ovládací prvky EditorPart (AppearanceEditorPart, LayoutEditorPart, BehaviorEditorPart a PropertyGridEditorPart) | Umožňuje uživatelům přizpůsobit různé aspekty Webové části ovládacích prvků uživatelského rozhraní na stránce. |

## <a name="lab-create-a-web-part-page"></a>Testovací prostředí: Vytvoření stránky webové části

V tomto testovacím prostředí vytvoříte stránku webové části, která bude uchovávat informace prostřednictvím profilů ASP.NET.

### <a name="creating-a-simple-page-with-web-parts"></a>Vytvoření jednoduché stránky pomocí Webové části

V této části návodu vytvoříte stránku, která používá ovládací prvky Webové části k zobrazení statického obsahu. Prvním krokem při práci s Webové části je vytvořit stránku se dvěma požadovanými strukturálními prvky. Nejprve stránka webové části potřebuje ovládací prvek WebPartManager pro sledování a koordinaci všech Webové částich ovládacích prvků. Druhý Webové části stránka vyžaduje jednu nebo více zón, což jsou složené ovládací prvky, které obsahují WebPart nebo jiné serverové ovládací prvky a zabírají určenou oblast stránky.

> [!NOTE]
> K povolení Webové částiho přizpůsobení není nutné provádět žádné akce. Tato možnost je ve výchozím nastavení povolená pro sadu ovládacích prvků Webové části. Když na webu poprvé spustíte Webové části stránku, ASP.NET nastaví výchozího poskytovatele individuálního nastavení pro ukládání uživatelských nastavení přizpůsobení. Další informace o individuálním nastavení najdete v tématu Přehled přizpůsobení Webové části.

### <a name="to-create-a-page-for-containing-web-parts-controls"></a>Vytvoření stránky pro obsahující Webové části ovládací prvky

1. Zavřete výchozí stránku a přidejte novou stránku do webu s názvem WebPartsDemo. aspx.
2. Přepněte do zobrazení **návrhu** .
3. V nabídce **zobrazení** se ujistěte, že jsou vybrány možnosti **nevizuálních ovládacích prvků** a **podrobností** , takže můžete zobrazit značky rozložení a ovládací prvky, které nemají uživatelské rozhraní.
4. Umístěte kurzor před značky `<div>` na návrhové ploše a stisknutím klávesy ENTER přidejte nový řádek. Umístěte kurzor před znakem nového řádku, v nabídce klikněte na ovládací prvek rozevíracího seznamu **Formát bloku** a vyberte možnost **Nadpis 1** . Do nadpisu přidejte **ukázkovou stránku text webové části**.
5. Z karty **WebParts** na panelu nástrojů přetáhněte ovládací prvek **WebPartManager** na stránku a umístěte ho hned za znak nového řádku a před `<div>`značky.   
  
   Ovládací prvek **WebPartManager** nevykresluje žádný výstup, takže se zobrazí jako šedé pole na návrhové ploše.
6. Umístěte kurzor do značek `<div>`.
7. V nabídce **rozložení** klikněte na možnost **Vložit tabulku**a vytvořte novou tabulku, která má jeden řádek a tři sloupce. Klikněte na tlačítko **Vlastnosti buňky** , v rozevíracím seznamu **svislé zarovnání** vyberte **nahoře** , klikněte na **OK**a znovu klikněte na **OK** a vytvořte tabulku.
8. Přetáhněte ovládací prvek WebPartZone do levého sloupce tabulky. Klikněte pravým tlačítkem myši na ovládací prvek **WebPartZone** , vyberte možnost **vlastnosti**a nastavte následující vlastnosti:   
  
   ID: SidebarZone   
  
   HeaderText: postranní panel
9. Přetáhněte druhý ovládací prvek **WebPartZone WebPartZone** do sloupce prostřední tabulky a nastavte následující vlastnosti:   
  
   ID: MainZone   
  
   HeaderText: Main
10. Uložte soubor.

Vaše stránka má teď dvě odlišné zóny, které můžete řídit samostatně. Nicméně žádná zóna neobsahuje žádný obsah, takže vytvoření obsahu je dalším krokem. V tomto návodu pracujete s Webové části ovládacími prvky, které zobrazují pouze statický obsah.

Rozložení Webové části zóny je určeno prvkem &lt;ZoneTemplate&gt;. V šabloně zóny můžete přidat libovolný ovládací prvek ASP.NET, bez ohledu na to, zda se jedná o vlastní ovládací prvek Webové části, uživatelský ovládací prvek nebo existující serverový ovládací prvek. Všimněte si, že tady používáte ovládací prvek popisek a že jednoduše přidáte statický text. Když umístíte běžný serverový ovládací prvek do zóny **WebPartZone** , ASP.NET zachází s ovládacím prvkem jako webové části ovládacího prvku za běhu, což umožňuje webové části funkcí na ovládacím prvku.

**Vytvoření obsahu pro hlavní zónu**

1. V zobrazení **Návrh** přetáhněte ovládací prvek **popisek** z karty **Standard** panelu nástrojů do oblasti obsahu v zóně, jejíž vlastnost **ID** je nastavená na MainZone.
2. Přepněte do zobrazení **zdroje** . Všimněte si, že byl přidán prvek &lt;ZoneTemplate&gt; pro zabalení ovládacího prvku **Label** do MainZone.
3. Přidejte atribut s názvem **title** do &lt;ASP: Label&gt; element a nastavte jeho hodnotu na Content. Odeberte atribut text = Label z &lt;ASP: Label&gt; elementu. Mezi otevíracími a ukončovacími značkami prvku &lt;ASP: Label&gt; přidejte nějaký text, jako je například **Vítejte na domovské stránce, na** základě páru &lt;H2&gt; tagů elementu. Váš kód by měl vypadat takto. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample21.aspx)]
4. Uložte soubor.

Dále vytvořte uživatelský ovládací prvek, který lze také přidat na stránku jako ovládací prvek Webové části.

### <a name="to-create-a-user-control"></a>Vytvoření uživatelského ovládacího prvku

1. Přidejte do svého webu nový webový uživatelský ovládací prvek, který bude sloužit jako ovládací prvek hledání. Zrušte výběr možnosti **umístit zdrojový kód do samostatného souboru**. Přidejte ji do stejného adresáře jako stránku WebPartsDemo. aspx a pojmenujte ji SearchUserControl. ascx.   
  
    > [!NOTE]
    > Uživatelský ovládací prvek pro tento návod neimplementuje skutečné funkce vyhledávání; slouží pouze k předvedení Webové částich funkcí.
2. Přepněte do zobrazení **návrhu** . Z karty **standardní** na panelu nástrojů přetáhněte ovládací prvek TextBox na stránku.
3. Umístěte kurzor za textové pole, které jste právě přidali, a stisknutím klávesy ENTER přidejte nový řádek.
4. Přetáhněte ovládací prvek tlačítko na stránku na novém řádku pod textové pole, které jste právě přidali.
5. Přepněte do zobrazení **zdroje** . Ujistěte se, že zdrojový kód uživatelského ovládacího prvku vypadá podobně jako v následujícím příkladu. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample22.aspx)]
6. Uložte soubor a zavřete ho.

Nyní můžete přidat ovládací prvky Webové části do zóny postranního panelu. Přidáváte dva ovládací prvky do zóny postranního panelu, jeden obsahující seznam odkazů a druhý, který je uživatelským ovládacím prvkem, který jste vytvořili v předchozím postupu. Odkazy jsou přidány jako ovládací prvek standardní **popisek** serveru podobný způsobu, jakým jste vytvořili statický text pro hlavní zónu. Nicméně i když jednotlivé serverové ovládací prvky obsažené v uživatelském ovládacím prvku mohou být obsaženy přímo v zóně (například ovládací prvek popisek), v tomto případě nejsou. Místo toho jsou součástí uživatelského ovládacího prvku, který jste vytvořili v předchozím postupu. To ukazuje běžný způsob, jak zabalit jakékoli ovládací prvky a další funkce, které chcete v uživatelském ovládacím prvku, a pak na tento ovládací prvek odkazovat v zóně jako Webové části ovládací prvek.

V době běhu sada ovládacích prvků Webové části zalomí oba ovládací prvky s ovládacími prvky GenericWebPart. Když ovládací prvek **GenericWebPart** zalomí ovládací prvek webového serveru, ovládací prvek obecné části je nadřazený ovládací prvek a přístup k ovládacímu prvku serveru můžete získat prostřednictvím vlastnosti ChildControl nadřazeného ovládacího prvku. Toto použití obecných součástí ovládacích prvků umožňuje, aby standardní ovládací prvky webového serveru měly stejné základní chování a atributy jako Webové části ovládací prvky, které jsou odvozeny od třídy **WebPart** .

### <a name="to-add-web-parts-controls-to-the-sidebar-zone"></a>Přidání ovládacích prvků Webové části do zóny postranního panelu

1. Otevřete stránku WebPartsDemo. aspx.
2. Přepněte do zobrazení **návrhu** .
3. Přetáhněte stránku uživatelského ovládacího prvku, kterou jste vytvořili, SearchUserControl. ascx, ze **Průzkumník řešení** do zóny, jejíž vlastnost **ID** je nastavená na SidebarZone, a přetáhněte ji tam.
4. Uložte stránku WebPartsDemo. aspx.
5. Přepněte do zobrazení **zdroje** .
6. V prvku &lt;ASP: WebPartZone&gt; pro SidebarZone těsně nad odkaz na uživatelský ovládací prvek přidejte &lt;ASP: Label&gt; element s obsaženými odkazy, jak je znázorněno v následujícím příkladu. Přidejte také atribut **title** do značky uživatelského ovládacího prvku s hodnotou **hledání**, jak je znázorněno na obrázku. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample23.aspx)]
7. Uložte soubor a zavřete ho.

Teď můžete stránku otestovat tak, že v prohlížeči přejdete do ní. Na stránce se zobrazí dvě zóny. Na následujícím snímku obrazovky vidíte stránku.

**Ukázková stránka Webové části se dvěma zónami**

![Webové části VS – návod 1 snímek obrazovky](profiles-themes-and-web-parts/_static/image3.gif)

**Obrázek 3**: webové části VS – návod 1 snímek obrazovky

V záhlaví každého ovládacího prvku je šipka dolů, která poskytuje přístup k nabídce příkazů dostupných akcí, které můžete provádět na ovládacím prvku. Klikněte na nabídku příkazy pro jeden z ovládacích prvků a pak klikněte na příkaz **minimalizovat** a Všimněte si, že je ovládací prvek minimalizován. V nabídce Akce klikněte na možnost **obnovit**a ovládací prvek se vrátí do jeho normální velikosti.

### <a name="enabling-users-to-edit-pages-and-change-layout"></a>Povolení uživatelům upravovat stránky a měnit rozložení

Webové části poskytuje uživatelům možnost změnit rozložení Webové části ovládacích prvků přetažením z jedné zóny do druhé. Kromě toho, aby uživatelé mohli přesouvat ovládací prvky **WebPart** z jedné zóny do jiné, můžete uživatelům povolit úpravy různých vlastností ovládacích prvků, včetně jejich vzhledu, rozložení a chování. Sada ovládacího prvku Webové části poskytuje základní funkce pro úpravu ovládacích prvků **webové části** . I když v tomto návodu to neuděláte, můžete také vytvořit vlastní ovládací prvky editoru, které umožní uživatelům upravovat funkce ovládacích prvků **WebPart** . Stejně jako u změny umístění ovládacího prvku **WebPart** spoléhá úprava vlastností ovládacího prvku na přizpůsobení ASP.NET pro uložení změn, které uživatelé provedou.

V této části návodu přidáte uživatelům možnost upravovat základní charakteristiky libovolného ovládacího prvku **webové části** na stránce. Chcete-li povolit tyto funkce, přidejte do stránky další vlastní uživatelský ovládací prvek společně s &lt;ASP: EditorZone&gt; element a dva ovládací prvky pro úpravy.

### <a name="to-create-a-user-control-that-enables-changing-page-layout"></a>Vytvoření uživatelského ovládacího prvku, který umožňuje změnu rozložení stránky

1. V aplikaci Visual Studio v nabídce **soubor** vyberte **novou** podnabídku a klikněte na možnost **soubor** .
2. V dialogovém okně **Přidat novou položku** vyberte **Webový uživatelský ovládací prvek**. Pojmenujte nový soubor DisplayModeMenu. ascx. Zrušte výběr možnosti **umístit zdrojový kód do samostatného souboru**.
3. Kliknutím na tlačítko Přidat vytvořte nový ovládací prvek.
4. Přepněte do zobrazení **zdroje** .
5. Odstraňte veškerý existující kód v novém souboru a vložte následující kód. Tento kód uživatelského ovládacího prvku používá funkce sady ovládacích prvků Webové části, které umožňují stránce změnit její zobrazení nebo režim zobrazení, a také umožňuje změnit fyzický vzhled a rozložení stránky, když jste v určitých režimech zobrazení. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample24.aspx)]
6. Uložte soubor kliknutím na ikonu Uložit na panelu nástrojů nebo výběrem možnosti **Uložit** v nabídce **soubor** .

### <a name="to-enable-users-to-change-the-layout"></a>Umožnění uživatelům měnit rozložení

1. Otevřete stránku WebPartsDemo. aspx a přepněte do zobrazení **Návrh** .
2. Umístěte kurzor do zobrazení **Návrh** hned za ovládací prvek **WebPartManager** , který jste přidali dříve. Přidejte pevný návrat za text tak, aby po ovládacím prvku **WebPartManager** byl prázdný řádek. Umístěte kurzor na prázdný řádek.
3. Přetáhněte uživatelský ovládací prvek, který jste právě vytvořili (soubor má název DisplayModeMenu. ascx) na stránku WebPartsDemo. aspx a umístěte jej na prázdný řádek.
4. Přetáhněte ovládací prvek EditorZone z části **WebParts** v sadě nástrojů na zbývající buňku otevřít tabulku na stránce WebPartsDemo. aspx.
5. Z části **WebParts** v sadě nástrojů přetáhněte ovládací prvek AppearanceEditorPart a ovládací prvek LayoutEditorPart do ovládacího prvku **EditorZone** .
6. Přepněte do zobrazení **zdroje** . Výsledný kód v buňce tabulky by měl vypadat podobně jako následující kód. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample25.aspx)]
7. Uložte soubor WebPartsDemo. aspx. Vytvořili jste uživatelský ovládací prvek, který umožňuje změnit režimy zobrazení a změnit rozložení stránky a na primární webovou stránku jste odkazovali na ovládací prvek.

Nyní můžete testovat schopnost upravovat stránky a měnit rozložení.

### <a name="to-test-layout-changes"></a>Testování změn rozložení

1. Načtěte stránku v prohlížeči.
2. Klikněte na rozevírací nabídku **režim zobrazení** a vyberte **Upravit**. Zobrazí se názvy zón.
3. Přetáhněte ovládací prvek **moje odkazy** podle jeho záhlaví z oblasti postranního panelu do dolní části hlavní zóny. Stránka by měla vypadat jako na následujícím snímku obrazovky.

### <a name="web-parts-demo-page-with-my-links-control-moved"></a>Stránka ukázky Webové části se přesunutým ovládacím prvkem moje odkazy

![Snímek obrazovky Webové části VS – návod 2](profiles-themes-and-web-parts/_static/image4.gif)

**Obrázek 4**: snímek obrazovky webové části VS – návod 2

1. Klikněte na rozevírací nabídku **režim zobrazení** a vyberte **Procházet**. Stránka se aktualizuje, názvy zón zmizí a ovládací prvek **moje odkazy** zůstane tam, kde jste ho umístili.
2. Chcete-li Ukázat, že přizpůsobení funguje, zavřete prohlížeč a pak znovu načtěte stránku. Změny, které jste provedli, budou uloženy pro budoucí relace prohlížeče.
3. V nabídce **režim zobrazení** vyberte **Upravit**.   
  
   Každý ovládací prvek na stránce se nyní zobrazuje se šipkou dolů v záhlaví, které obsahuje rozevírací nabídku příkazy.
4. Kliknutím na šipku zobrazíte nabídku příkazy v ovládacím prvku **moje odkazy** . Klikněte na příkaz **Upravit** .   
  
   Zobrazí se ovládací prvek **EditorZone** zobrazující ovládací prvky EditorPart, které jste přidali.
5. V části **vzhled** v ovládacím prvku pro úpravy změňte **název** na moje oblíbené, v rozevíracím seznamu **typ Chrome** vyberte **pouze nadpis**a pak klikněte na **použít**. Následující snímek obrazovky ukazuje stránku v režimu úprav.

### <a name="web-parts-demo-page-in-edit-mode"></a>Ukázková stránka Webové části v režimu úprav

![Webové části VS – návod 3 – snímek obrazovky](profiles-themes-and-web-parts/_static/image5.gif)

**Obrázek 5**: snímek obrazovky webové části VS – návod 3

1. Klikněte na nabídku **režim zobrazení** a vyberte **Procházet** a vraťte se do režimu procházení.
2. Ovládací prvek má nyní aktualizovaný název a bez ohraničení, jak je znázorněno na následujícím snímku obrazovky.

### <a name="edited-web-parts-demo-page"></a>Upravená ukázková Webové částiová stránka

![Snímek obrazovky Webové části VS – návod 4](profiles-themes-and-web-parts/_static/image6.gif)

**Obrázek 4**: snímek obrazovky webové části vs – Návod 4

### <a name="adding-web-parts-at-run-time"></a>Přidání Webové části v době běhu

Můžete také uživatelům dovolit, aby během běhu do své stránky přidali ovládací prvky Webové části. Provedete to tak, že nakonfigurujete stránku pomocí katalogu Webové části, který obsahuje seznam Webové části ovládacích prvků, které chcete zpřístupnit uživatelům.

**Chcete-li uživatelům dovolit přidat Webové části v době běhu**

1. Otevřete stránku WebPartsDemo. aspx a přepněte do zobrazení **Návrh** .
2. Z karty **WebParts** v sadě nástrojů přetáhněte ovládací prvek CatalogZone do pravého sloupce tabulky pod ovládací prvek **EditorZone** .   
  
   Oba ovládací prvky mohou být ve stejné buňce tabulky, protože nebudou zobrazeny ve stejnou dobu.
3. V podokně vlastnosti přiřaďte řetězec **přidat webové části** k vlastnosti HeaderText ovládacího prvku **CatalogZone** .
4. Z části **WebParts** v sadě nástrojů přetáhněte ovládací prvek DeclarativeCatalogPart do oblasti obsahu ovládacího prvku **CatalogZone** .
5. Klikněte na šipku v pravém horním rohu ovládacího prvku **DeclarativeCatalogPart** a zpřístupněte nabídku úlohy a pak vyberte **Upravit šablony**.
6. V části **standardní** v sadě nástrojů přetáhněte ovládací prvek **nahrání souborů** a ovládací prvek **Kalendář** do části **WebPartsTemplate** ovládacího prvku **DeclarativeCatalogPart** .
7. Přepněte do zobrazení **zdroje** . Zkontrolujte zdrojový kód prvku &lt;ASP: CatalogZone&gt;. Všimněte si, že ovládací prvek **DeclarativeCatalogPart** obsahuje&gt; prvek &lt;WebPartsTemplate se dvěma uzavřenými serverovými ovládacími prvky, které budete moci přidat na stránku z katalogu.
8. Přidejte vlastnost **title** do každého ovládacího prvku, který jste přidali do katalogu, pomocí hodnoty řetězce zobrazeného pro každý název v následujícím příkladu kódu. I když název není vlastnost, kterou můžete normálně nastavit na těchto dvou ovládacích prvcích serveru v době návrhu, pokud uživatel přidá tyto ovládací prvky do zóny **WebPartZone** z katalogu za běhu, jsou všechny zabaleny pomocí ovládacího prvku **GenericWebPart** . To jim umožní působit jako Webové části ovládací prvky, takže budou moci zobrazovat nadpisy.   
  
   Kód pro dva ovládací prvky obsažené v ovládacím prvku **DeclarativeCatalogPart** by měl vypadat takto. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample26.aspx)]
9. Uložte stránku.

Katalog teď můžete testovat.

### <a name="to-test-the-web-parts-catalog"></a>Otestování katalogu Webové části

1. Načtěte stránku v prohlížeči.
2. Klikněte na rozevírací nabídku **režim zobrazení** a vyberte **katalog**.   
  
   Zobrazí se katalog s názvem **přidat webové části** .
3. Přetáhněte ovládací prvek **Moje oblíbené položky** z hlavní zóny zpátky na horní část zóny bočního panelu a přetáhněte ji tam.
4. V části **přidat webové části** Catalog zaškrtněte obě políčka a v rozevíracím seznamu vyberte **hlavní** , který obsahuje dostupné zóny.
5. V katalogu klikněte na **Přidat** . Ovládací prvky jsou přidány do hlavní zóny. Pokud chcete, můžete přidat více instancí ovládacích prvků z katalogu na stránku.   
  
   Následující snímek obrazovky ukazuje stránku s ovládacím prvkem pro nahrání souboru a kalendářem v hlavní zóně. 

![Ovládací prvky přidané do hlavní zóny z katalogu](profiles-themes-and-web-parts/_static/image7.gif)

    **Figure 5**: Controls added to Main zone from the catalog
6. Klikněte na rozevírací nabídku **režim zobrazení** a vyberte **Procházet**. Katalog zmizí a stránka se aktualizuje.
7. Zavřete prohlížeč. Načtěte stránku znovu. Změny, které jste udělali, se chovají.
