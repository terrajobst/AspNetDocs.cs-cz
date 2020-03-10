---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: Vytvoření databáze | Microsoft Docs
author: microsoft
description: Krok 2 ukazuje postup vytvoření databáze obsahující všechna data o večeři a protokolu RSVP pro naši aplikaci NerdDinner.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: b0aa7c8cdf741f44e09ed18e2b2f73fe6bf786ae
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581002"
---
# <a name="create-a-database"></a>Vytvoření databáze

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 2 bezplatného [kurzu aplikace "NerdDinner"](introducing-the-nerddinner-tutorial.md) , který vás provede procesem vytvoření malé, ale dokončené webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 2 ukazuje postup vytvoření databáze obsahující všechna data o večeři a protokolu RSVP pro naši aplikaci NerdDinner.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme vám postupovat podle [Začínáme s kurzy pro](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [hudební úložiště](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) MVC 3 nebo MVC.

## <a name="nerddinner-step-2-creating-the-database"></a>NerdDinner krok 2: vytvoření databáze

K uložení všech dat o večeři a protokolu RSVP pro naši aplikaci NerdDinner budeme používat databázi.

Následující postup ukazuje vytvoření databáze pomocí bezplatné SQL Server Express edice (kterou můžete snadno nainstalovat pomocí verze V2 [Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)). Veškerý kód, který zapíšeme, bude pracovat s SQL Server Express i s úplným SQL Server.

### <a name="creating-a-new-sql-server-express-database"></a>Vytvoření nové databáze SQL Server Express

Začneme tak, že kliknete pravým tlačítkem na náš webový projekt a pak vyberete příkaz nabídky **přidat&gt;nové položky** :

![](create-a-database/_static/image1.png)

Tím se zobrazí dialogové okno Přidat novou položku v aplikaci Visual Studio. Vyfiltrujeme podle kategorie "data" a vyberete šablonu položky "SQL Server Database":

![](create-a-database/_static/image2.png)

Pojmenujte SQL Server Express databázi, kterou chceme vytvořit "NerdDinner. mdf" a stiskněte OK. Visual Studio se pak zeptá, jestli chceme přidat tento soubor do našeho adresáře \app\_dat (což je adresář, který se už nastavil pomocí seznamů ACL pro čtení i zápis):

![](create-a-database/_static/image3.png)

Klikneme na Ano a vytvoří se nová databáze, která se přidá do našich Průzkumník řešení:

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a>Vytváření tabulek v rámci naší databáze

Nyní máme novou prázdnou databázi. Pojďme do ní přidat některé tabulky.

Provedeme to tak, že přejdete na okno karty Průzkumník serveru v rámci sady Visual Studio, které nám umožní spravovat databáze a servery. SQL Server Express databáze uložené ve složce dat\_\app v naší aplikaci se automaticky zobrazí v Průzkumník serveru. Volitelně můžete použít ikonu "připojit k databázi" v horní části okna Průzkumník serveru k přidání dalších databází SQL Server (místní i vzdálené) do seznamu současně:

![](create-a-database/_static/image5.png)

Do naší databáze NerdDinner přidáme dvě tabulky – jednu pro uložení našich večeře a druhou pro sledování přijetí protokolu RSVP do nich. Nové tabulky můžeme vytvořit tak, že kliknete pravým tlačítkem na složku Tables v naší databázi a zvolíte příkaz nabídky Přidat novou tabulku:

![](create-a-database/_static/image6.png)

Otevře se Návrhář tabulky, který nám umožní nakonfigurovat schéma naší tabulky. V tabulce "večeře" přidáme 10 sloupců dat:

![](create-a-database/_static/image7.png)

Chceme, aby sloupec "DinnerID" byl pro tabulku jedinečným primárním klíčem. To můžeme nakonfigurovat tak, že kliknete pravým tlačítkem na sloupec "DinnerID" a vyberete položku nabídky "nastavit primární klíč":

![](create-a-database/_static/image8.png)

Kromě toho, že DinnerID primární klíč, chceme také nakonfigurovat jako sloupec identity, jehož hodnota se automaticky zvyšuje, protože se do tabulky přidají nové řádky dat (to znamená, že první vložená řada večeře bude mít DinnerID 1, druhý vložený řádek. bude mít DinnerIDu 2 atd.

To můžeme udělat tak, že vyberete sloupec "DinnerID" a potom pomocí editoru "vlastnosti sloupce" nastavíte vlastnost "(je identity)" na sloupci na hodnotu "Ano". Použijeme standardní výchozí hodnoty identity (počínaje 1 a přírůstkem 1 na každém novém řádku večeře):

![](create-a-database/_static/image9.png)

Tuto tabulku pak uložíte zadáním kombinace kláves CTRL + S nebo pomocí příkazu **File-&gt;Save** . Tím se zobrazí výzva k pojmenování tabulky. Budeme pojmenovat "večeře":

![](create-a-database/_static/image10.png)

Naše nová tabulka večeře se pak zobrazí v naší databázi v Průzkumníku serveru.

Pak zopakujeme výše uvedené kroky a vytvoříme tabulku "RSVP". Tato tabulka má 3 sloupce. Nastavíme sloupec RsvpID jako primární klíč a zároveň nastavíme sloupec identity:

![](create-a-database/_static/image11.png)

Budeme ho ukládat a dát mu název "RSVP".

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a>Nastavení vztahu cizího klíče mezi tabulkami

Teď máme v naší databázi dvě tabulky. Náš poslední krok pro návrh schématu bude nastavit relaci 1:1 mezi těmito dvěma tabulkami – aby bylo možné přidružit každý řádek večeře k nule nebo více řádkům protokolu RSVP, které se na něj vztahují. To provedeme tak, že nakonfigurujete sloupec "DinnerID" tabulky protokolu RSVP tak, aby měl relaci cizího klíče se sloupcem "DinnerID" v tabulce "večeřes".

Pokud to chcete udělat, otevřete tabulku protokolu RSVP v Návrháři tabulky tak, že na ni dvakrát kliknete v Průzkumníku serveru. Pak vyberete sloupec "DinnerID", klikněte pravým tlačítkem myši a vyberte relaci... příkaz místní nabídky:

![](create-a-database/_static/image12.png)

Zobrazí se dialogové okno, které můžeme použít k nastavení vztahů mezi tabulkami:

![](create-a-database/_static/image13.png)

Kliknutím na tlačítko Přidat přidáte novou relaci do dialogového okna. Po přidání relace rozbalíme uzel "tabulky a specifikace sloupce" stromové zobrazení v mřížce vlastností na pravé straně dialogového okna a potom kliknete na "...". tlačítko napravo od něj:

![](create-a-database/_static/image14.png)

Kliknutí na... tlačítko zobrazí další dialog, který nám umožní určit, které tabulky a sloupce jsou součástí relace, a také nám umožnit pojmenovat relaci.

V tabulce s primárními klíči se změní na "večeře" a jako primární klíč vyberete sloupec "DinnerID" v tabulce večeře. Naše tabulka protokolu RSVP bude tabulka cizího klíče a protokol RSVP. Sloupec DinnerID bude přidružen jako cizí klíč:

![](create-a-database/_static/image15.png)

Každý řádek v tabulce protokolu RSVP se teď přidruží k řádku v tabulce večeře. SQL Server zachovává referenční integritu pro nás – a zabráníme přidání nového řádku protokolu RSVP, pokud neodkazuje na platný řádek večeře. Tím se také zabrání v odstranění řádku večeře, pokud se na něj stále vztahují řádky protokolu RSVP.

### <a name="adding-data-to-our-tables"></a>Přidávání dat do tabulek

Pojďme to dokončit přidáním ukázkových dat do tabulky večeři. Do tabulky můžeme přidat data tak, že na ni kliknete pravým tlačítkem myši v rámci Průzkumník serveru a vyberete příkaz Zobrazit data tabulky:

![](create-a-database/_static/image16.png)

Přidáme pár řádků dat o večeři, které můžeme později použít při zahájení implementace aplikace:

![](create-a-database/_static/image17.png)

### <a name="next-step"></a>Další krok

Dokončili jsme vytváření naší databáze. Nyní vytvoříme třídy modelů, které můžeme použít k dotazování a aktualizaci.

> [!div class="step-by-step"]
> [Předchozí](create-a-new-aspnet-mvc-project.md)
> [Další](build-a-model-with-business-rule-validations.md)
