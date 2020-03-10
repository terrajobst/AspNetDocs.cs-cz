---
uid: web-pages/overview/data/working-with-files
title: Práce se soubory na webu ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tato kapitola vysvětluje, jak číst, zapisovat, přidávat, odstraňovat a nahrávat soubory.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: eee916e4-ba4c-439a-a24e-68df7d45a569
msc.legacyurl: /web-pages/overview/data/working-with-files
msc.type: authoredcontent
ms.openlocfilehash: 684c47a8a8480dc040e5144144577c94c35d39e5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78642364"
---
# <a name="working-with-files-in-an-aspnet-web-pages-razor-site"></a>Práce se soubory na webu ASP.NET Web Pages (Razor)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek vysvětluje, jak číst, zapisovat, přidávat, odstraňovat a nahrávat soubory na webu ASP.NET Web Pages (Razor).
> 
> > [!NOTE]
> > Pokud chcete nahrát obrázky a manipulovat s nimi (například je překlopit nebo změnit jejich velikost), přečtěte si téma [práce s obrázky na webu ASP.NET Web Pages](/aspnet/web-pages/overview/ui-layouts-and-themes/9-working-with-images).
> 
> 
> **Co se naučíte:** 
> 
> - Jak vytvořit textový soubor a zapsat do něj data.
> - Postup připojení dat k existujícímu souboru.
> - Jak číst soubor a zobrazit z něho
> - Odstranění souborů z webu.
> - Jak umožnit uživatelům odeslat jeden soubor nebo více souborů.
> 
> Jedná se o funkce ASP.NET programování, které jsou představené v článku:
> 
> - Objekt `File`, který poskytuje způsob správy souborů.
> - Pomocná rutina `FileUpload`
> - Objekt `Path`, který poskytuje metody, které umožňují pracovat s cestami a názvy souborů.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 2
> - WebMatrix 2
>   
> 
> V tomto kurzu se používá také WebMatrix 3.

<a id="Creating_a_Text_File"></a>
## <a name="creating-a-text-file-and-writing-data-to-it"></a>Vytvoření textového souboru a zápis dat do něj

Kromě používání databáze na webu může pracovat se soubory. Můžete například použít textové soubory jako jednoduchý způsob, jak ukládat data webu. (Textový soubor, který se používá k ukládání dat, se někdy označuje jako *plochý soubor*.) Textové soubory mohou být v různých formátech, například *txt*, *. XML*nebo *. csv* (hodnoty oddělené čárkami).

Pokud chcete ukládat data do textového souboru, můžete použít metodu `File.WriteAllText` k určení souboru, který se má vytvořit, a dat, která se do něj zapisují. V tomto postupu vytvoříte stránku, která obsahuje jednoduchý formulář se třemi `input` prvky (křestní jméno, příjmení a e-mailovou adresu) a tlačítko **Odeslat** . Když uživatel formulář odešle, uloží se vstup uživatele do textového souboru.

1. Pokud ještě neexistuje, vytvořte novou složku s názvem *App\_data*.
2. V kořenovém adresáři webu vytvořte nový soubor s názvem *UserData. cshtml*.
3. Existující obsah nahraďte následujícím: 

    [!code-cshtml[Main](working-with-files/samples/sample1.cshtml)]

    Kód HTML vytvoří formulář se třemi textovými poli. V kódu pomocí vlastnosti `IsPost` určíte, zda byla stránka odeslána před zahájením zpracování.

    Prvním úkolem je získat vstup uživatele a přiřadit ho k proměnným. Kód pak zřetězí hodnoty samostatných proměnných do jednoho řetězce s oddělovači, který je pak uložen v jiné proměnné. Všimněte si, že oddělovač čárky je řetězec obsažený v uvozovkách (","), protože do velkého řetězce, který vytváříte, nebudete dělit čárkami. Na konci dat, která zřetězete společně, přidáte `Environment.NewLine`. Tím se přidá konec řádku (znak nového řádku). To, co vytváříte se všemi zřetězením, je řetězec, který vypadá takto:

    [!code-css[Main](working-with-files/samples/sample2.css)]

    (Na konci neviditelného konce řádku.)

    Pak vytvoříte proměnnou (`dataFile`), která obsahuje umístění a název souboru, do kterého se budou ukládat data. Nastavení umístění vyžaduje speciální zpracování. V rámci webů je to špatný postup, jak odkazovat v kódu na absolutní cesty, jako je *C:\Folder\File.txt* pro soubory na webovém serveru. Pokud se web přesune, absolutní cesta bude špatná. Kromě toho pro hostovanou lokalitu (na rozdíl od na vašem počítači) obvykle neznáte, co je správná cesta při psaní kódu.

    Ale v některých případech (stejně jako při psaní souboru) potřebujete úplnou cestu. Řešením je použití metody `MapPath` objektu `Server`. Tím se vrátí úplná cesta k vašemu webu. Chcete-li získat cestu k kořenovému adresáři webu, uživatel `~` operátor (aby represen virtuální kořenový adresář webu) k `MapPath`. (Do této podsložky můžete také předat název podsložky, například *~/App\_data/* , abyste získali cestu k této podsložce.) Pak můžete zřetězit Další informace do jakékoli metody, která se vrátí, aby bylo možné vytvořit úplnou cestu. V tomto příkladu přidáte název souboru. (Další informace o tom, jak pracovat s cestami k souborům a složkám v tématu [Úvod k ASP.NET programování webových stránek pomocí syntaxe Razor](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths), si můžete přečíst.)

    Soubor se uloží do složky *Data\_aplikace* . Tato složka je speciální složkou v ASP.NET, která se používá k ukládání datových souborů, jak je popsáno v tématu [Úvod k práci s databází na webech webových stránek ASP.NET](https://go.microsoft.com/fwlink/?LinkId=195209).

    Metoda `WriteAllText` objektu `File` zapisuje data do souboru. Tato metoda přijímá dva parametry: název (s cestou) souboru, do kterého se má zapisovat, a skutečná data, která mají být zapsána. Všimněte si, že název prvního parametru má `@` znak jako předponu. To oznamuje ASP.NET, že zadáváte doslovné řetězcový literál a že znaky jako "/" by neměly být interpretovány zvláštním způsobem. (Další informace najdete v tématu [Úvod do webového programování ASP.NET pomocí syntaxe Razor](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)

    > [!NOTE]
    > Aby váš kód ukládal soubory do složky *\_dat aplikace* , potřebuje aplikace oprávnění ke čtení i zápisu pro tuto složku. Ve vývojovém počítači to není obvykle problém. Když ale publikujete web na webový server poskytovatele hostingu, možná budete muset tato oprávnění výslovně nastavit. Pokud spustíte tento kód na serveru poskytovatele hostingu a získáte chyby, obraťte se na poskytovatele hostingu a zjistěte, jak tato oprávnění nastavit.

- Spusťte stránku v prohlížeči. 

    ![](working-with-files/_static/image1.jpg)
- Do polí zadejte hodnoty a pak klikněte na **Odeslat**.
- Zavřete prohlížeč.
- Vraťte se do projektu a aktualizujte zobrazení.
- Otevřete soubor *data. txt* . Data, která jste odeslali ve formuláři, jsou v souboru. 

    ![obrazu](working-with-files/_static/image2.jpg)
- Zavřete soubor *data. txt* .

<a id="Appending_Data"></a>
## <a name="appending-data-to-an-existing-file"></a>Připojení dat k existujícímu souboru

V předchozím příkladu jste pomocí `WriteAllText` vytvořili textový soubor, který je v něm jenom jedna část dat. Pokud zavoláte metodu znovu a předáte stejný název souboru, existující soubor bude zcela přepsán. Po vytvoření souboru však budete často chtít přidat nová data na konec souboru. To lze provést pomocí metody `AppendAllText` objektu `File`.

1. Na webu vytvořte kopii souboru *UserData. cshtml* a pojmenujte kopii *UserDataMultiple. cshtml*.
2. Před otevírací `<!DOCTYPE html>`ovou značkou nahraďte blok kódu následujícím blokem kódu: 

    [!code-cshtml[Main](working-with-files/samples/sample3.cshtml)]

    Tento kód v předchozím příkladu obsahuje jednu změnu. Místo použití `WriteAllText`používá metodu `the AppendAllText`. Metody jsou podobné, s tím rozdílem, že `AppendAllText` přidává data na konec souboru. Stejně jako u `WriteAllText``AppendAllText` vytvoří soubor, pokud ještě neexistuje.
3. Spusťte stránku v prohlížeči.
4. Zadejte hodnoty pro pole a pak klikněte na **Odeslat**.
5. Přidejte další data a odešlete formulář znovu.
6. Vraťte se do projektu, klikněte pravým tlačítkem na složku projektu a pak klikněte na **aktualizovat**.
7. Otevřete soubor *data. txt* . Nyní obsahuje nová data, která jste právě zadali. 

    ![obrazu](working-with-files/_static/image3.jpg)

<a id="Reading_and_Displaying_Data"></a>
## <a name="reading-and-displaying-data-from-a-file"></a>Čtení a zobrazování dat ze souboru

I v případě, že nepotřebujete zapisovat data do textového souboru, pravděpodobně někdy budete potřebovat číst data z jedné. K tomu můžete znovu použít objekt `File`. Objekt `File` můžete použít ke čtení každého řádku samostatně (odděleného zalomením řádku) nebo ke čtení jednotlivých položek bez ohledu na to, jak jsou oddělené.

Tento postup ukazuje, jak číst a zobrazit data, která jste vytvořili v předchozím příkladu.

1. V kořenovém adresáři webu vytvořte nový soubor s názvem *úloha displayData. cshtml*.
2. Existující obsah nahraďte následujícím: 

    [!code-cshtml[Main](working-with-files/samples/sample4.cshtml)]

    Kód začíná čtením souboru, který jste vytvořili v předchozím příkladu, do proměnné s názvem `userData`pomocí tohoto volání metody:

    [!code-css[Main](working-with-files/samples/sample5.css)]

    Kód, který se má provést, je uvnitř příkazu `if`. Pokud chcete číst soubor, je vhodné použít metodu `File.Exists` k určení toho, zda je soubor k dispozici. Kód také kontroluje, zda je soubor prázdný.

    Tělo stránky obsahuje dvě `foreach` smyčky, jedna vnořená uvnitř druhé. Vnější smyčka `foreach` získá z datového souboru vždy jeden řádek. V tomto případě jsou řádky definovány pomocí konců řádků v souboru &#8212; , kde je každá datová položka na vlastním řádku. Vnější smyčka vytvoří novou položku (`<li>` element) uvnitř seřazeného seznamu (`<ol>` elementu).

    Vnitřní smyčka rozdělí jednotlivé datové řádky na položky (pole) pomocí čárky jako oddělovače. (Na základě předchozího příkladu to znamená, že každý řádek obsahuje tři pole &#8212; jméno, příjmení a e-mailovou adresu, každou oddělenou čárkou.) Vnitřní smyčka také vytvoří seznam `<ul>` a zobrazí jednu položku seznamu pro každé pole v datovém řádku.

    Kód ukazuje, jak použít dva datové typy, pole a `char` datový typ. Pole je povinné, protože metoda `File.ReadAllLines` vrací data jako pole. `char` datový typ je vyžadován, protože metoda `Split` vrací `array`, ve kterém každý prvek je typu `char`. (Informace o polích naleznete v tématu [Úvod do ASP.NET webového programování pomocí syntaxe Razor](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects).)
3. Spusťte stránku v prohlížeči. Zobrazí se data, která jste zadali pro předchozí příklady. 

    ![obrazu](working-with-files/_static/image4.jpg)

> [!TIP] 
> 
> **Zobrazení dat z textového souboru s oddělovači v aplikaci Microsoft Excel**
> 
> Pomocí aplikace Microsoft Excel můžete uložit data obsažená v tabulce jako textový soubor s oddělovači (soubor *. csv* ). Když to uděláte, soubor se uloží jako prostý text, ne ve formátu aplikace Excel. Každý řádek v tabulce je oddělen zalomením řádku v textovém souboru a každá datová položka je oddělená čárkou. Pomocí kódu zobrazeného v předchozím příkladu si můžete přečíst soubor s oddělovači v Excelu jenom změnou názvu datového souboru ve vašem kódu.

<a id="Deleting_Files"></a>
## <a name="deleting-files"></a>Odstraňování souborů

Chcete-li odstranit soubory z webu, můžete použít metodu `File.Delete`. Tento postup ukazuje, jak umožnit uživatelům odstranit obrázek (soubor *. jpg* ) ze složky *imagí* , pokud znají název souboru.

> [!NOTE] 
> 
> **Důležité** informace Na produkčním webu je obvykle možné omezit, kdo může provádět změny dat. Informace o tom, jak nastavit členství a způsoby, jak autorizovat uživatele k provádění úloh na webu, najdete v tématu věnovaném [Přidání zabezpečení a členství na web webových stránek ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202904).

1. Na webu vytvořte podsložku s názvem *Image*.
2. Zkopírujte jeden nebo více souborů *. jpg* do složky *imagí* .
3. V kořenovém adresáři webu vytvořte nový soubor s názvem *. Delete. cshtml*.
4. Existující obsah nahraďte následujícím: 

    [!code-cshtml[Main](working-with-files/samples/sample6.cshtml)]

    Tato stránka obsahuje formulář, kde mohou uživatelé zadat název souboru obrázku. Nevstupují do přípony názvu souboru *. jpg* ; tím, že omezíte název souboru tímto způsobem, pomůžete uživatelům zabránit ve odstraňování libovolných souborů na vašem webu.

    Kód přečte název souboru, který uživatel zadal, a pak vytvoří úplnou cestu. Chcete-li vytvořit cestu, kód používá aktuální cestu k webu (vrácený metodou `Server.MapPath`), název složky *images* , název, který uživatel zadal, a ". jpg" jako řetězec literálu.

    Chcete-li odstranit soubor, kód volá metodu `File.Delete` a předá jí úplnou cestu, kterou jste právě nastavili. Na konci značky zobrazí kód potvrzovací zprávu, že soubor byl odstraněn.
5. Spusťte stránku v prohlížeči. 

    ![obrazu](working-with-files/_static/image5.jpg)
6. Zadejte název souboru, který se má odstranit, a klikněte na **Odeslat**. Pokud byl soubor odstraněn, zobrazí se v dolní části stránky název souboru.

<a id="Letting_Users_Upload_a_File"></a>
## <a name="letting-users-upload-a-file"></a>Umožnění uživatelům odeslat soubor

Pomoc s `FileUpload` umožňuje uživatelům nahrávat soubory na web. Následující postup ukazuje, jak umožnit uživatelům odeslat jeden soubor.

1. Přidejte knihovnu webových pomocníků ASP.NET na web, jak je popsáno v [tématu Instalace pomocníků na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste ho ještě nepřidali.
2. Ve složce *Data\_aplikace* vytvořte novou složku a pojmenujte ji *UploadedFiles*.
3. V kořenovém adresáři vytvořte nový soubor s názvem *FileUpload. cshtml*.
4. Stávající obsah stránky nahraďte následujícím způsobem: 

    [!code-cshtml[Main](working-with-files/samples/sample7.cshtml)]

    Tělo stránky používá pomocnou část `FileUpload` k vytvoření pole pro odeslání a tlačítek, které jste pravděpodobně obeznámeni s:

    ![obrazu](working-with-files/_static/image6.jpg)

    Vlastnosti, které jste nastavili pro pomocnou pomůcku `FileUpload` určete, že chcete, aby se soubor nahrál, a že se má tlačítko Odeslat **načíst.** (Další pole přidáte později v článku.)

    Když uživatel klikne na **Odeslat**, kód v horní části stránky získá soubor a uloží ho. Objekt `Request`, který obvykle používáte k získání hodnot z polí formuláře, má také pole `Files` obsahující soubor (nebo soubory), které byly odeslány. Jednotlivé soubory můžete v poli &#8212; získat mimo konkrétní pozice, například k získání prvního nahraného souboru, získáte `Request.Files[0]`, abyste získali druhý soubor, získáte `Request.Files[1]`a tak dále. (Nezapomeňte, že při programování se počítá obvykle od nuly.)

    Při načítání nahraného souboru jej umístíte do proměnné (`uploadedFile`), abyste se mohli manipulovat. Chcete-li určit název nahraného souboru, stačí získat jeho vlastnost `FileName`. Když však uživatel nahraje soubor, `FileName` obsahuje původní název uživatele, který obsahuje celou cestu. Může to vypadat takto:

    *C:\Users\Public\Sample.txt*

    Nechcete všechny informace o této cestě, ale, protože to je cesta k počítači uživatele, ne pro váš server. Přejete si jenom skutečný název souboru (*Sample. txt*). Pomocí metody `Path.GetFileName` můžete prokládat pouze soubor z cesty, například takto:

    [!code-csharp[Main](working-with-files/samples/sample8.cs)]

    Objekt `Path` je nástroj, který má několik metod, jako je to, které lze použít k rozložení cest, kombinování cest a tak dále.

    Až se vám zobrazí název nahraného souboru, můžete vytvořit novou cestu, kam chcete nahrát nahraný soubor na svůj web. V tomto případě zkombinujete `Server.MapPath`, názvy složek (*App\_data/UploadedFiles*) a nově vytvořený název souboru pro vytvoření nové cesty. Potom můžete zavolat metodu `SaveAs` nahraného souboru a soubor skutečně uložit.
5. Spusťte stránku v prohlížeči. 

    ![obrazu](working-with-files/_static/image7.jpg)
6. Klikněte na **Procházet** a vyberte soubor, který se má nahrát. 

    ![obrazu](working-with-files/_static/image8.jpg)

    Textové pole vedle tlačítka **Procházet** bude obsahovat cestu a umístění souboru.

    ![obrazu](working-with-files/_static/image9.jpg)
7. Klikněte na **Odeslat**.
8. Na webu klikněte pravým tlačítkem na složku projektu a pak klikněte na **aktualizovat**.
9. Otevřete složku *UploadedFiles* . Soubor, který jste nahráli, je ve složce. 

    ![obrazu](working-with-files/_static/image10.jpg)

<a id="Letting_Users_Upload_Multiple_Files"></a>
## <a name="letting-users-upload-multiple-files"></a>Umožnění uživatelům nahrávat více souborů

V předchozím příkladu umožníte uživatelům odeslat jeden soubor. Můžete ale použít pomocníka `FileUpload` k nahrání více souborů najednou. To je užitečné pro scénáře, jako je nahrávání fotek, kde je nahrávání jednoho souboru v čase zdlouhavé. (Můžete si přečíst informace o nahrávání fotek při [práci s obrázky na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202897).) Tento příklad ukazuje, jak umožnit uživatelům nahrávání dvou souborů najednou, i když můžete stejný postup použít k nahrání více než.

1. Přidejte knihovnu webových pomocníků ASP.NET na web, jak je popsáno v [tématu Instalace pomocníků na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste to ještě neudělali.
2. Vytvořte novou stránku s názvem *FileUploadMultiple. cshtml*.
3. Stávající obsah stránky nahraďte následujícím způsobem:  

    [!code-cshtml[Main](working-with-files/samples/sample9.cshtml)]

    V tomto příkladu je pomocná Nápověda `FileUpload` v těle stránky nakonfigurovaná tak, aby uživatelé mohli ve výchozím nastavení nahrávat dva soubory. Vzhledem k tomu, že `allowMoreFilesToBeAdded` je nastavená na `true`, pomoc vykreslí odkaz, který uživateli umožňuje přidat další pole pro nahrávání:

    ![obrazu](working-with-files/_static/image11.jpg)

    Chcete-li zpracovat soubory, které uživatel nahraje, kód používá stejnou základní techniku, jakou jste použili v předchozím příkladu &#8212; , načte soubor z `Request.Files` a pak ho uloží. (Včetně různých věcí, které musíte udělat, abyste získali správný název a cestu k souboru.) Inovace tohoto času je v tom, že uživatel může nahrávat více souborů a vy neznáte mnoho. Chcete-li zjistit, můžete získat `Request.Files.Count`.

    S tímto číslem můžete cyklicky procházet `Request.Files`, načítat jednotlivé soubory a ukládat je. Pokud chcete pomocí kolekce procyklovat známý počet opakování, můžete použít smyčku `for`, například:

    [!code-csharp[Main](working-with-files/samples/sample10.cs)]

    Proměnná `i` je pouze dočasný čítač, který bude přecházet od nuly k libovolnému hornímu limitu, který jste nastavili. V tomto případě je horní limit počet souborů. Vzhledem k tomu, že čítač začíná nulou, protože je typický pro počítání scénářů v ASP.NET, je horní limit ve skutečnosti nižší než počet souborů. (Pokud se nahrají tři soubory, je počet nula až 2.)

    Proměnná `uploadedCount` vyhodnotí všechny soubory, které se úspěšně nahrály a uložily. Tyto účty kódu pro možnost, že očekávaný soubor nemusí být možné nahrát.
4. Spusťte stránku v prohlížeči. Prohlížeč zobrazí stránku a její dvě pole pro odeslání.
5. Vyberte dva soubory k nahrání.
6. Klikněte na **Přidat další soubor**. Na stránce se zobrazí nové pole pro odeslání. 

    ![obrazu](working-with-files/_static/image12.jpg)
7. Klikněte na **Odeslat**.
8. Na webu klikněte pravým tlačítkem na složku projektu a pak klikněte na **aktualizovat**.
9. Otevřete složku *UploadedFiles* , abyste viděli úspěšně nahrané soubory.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Další prostředky

[Práce s obrázky na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202897)

[Export do souboru CSV](https://msdn.microsoft.com/library/ms155919.aspx)
