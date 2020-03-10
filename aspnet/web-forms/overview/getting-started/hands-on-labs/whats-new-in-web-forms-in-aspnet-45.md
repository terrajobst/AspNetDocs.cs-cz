---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
title: Co je nového ve webových formulářích v ASP.NET 4,5 | Microsoft Docs
author: rick-anderson
description: Nová verze webových formulářů ASP.NET zavádí řadu vylepšení, která se zaměřují na vylepšení uživatelského prostředí při práci s daty. V předchozích verzích...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 0a1f88bd-97da-4ed1-86f1-605199dc75a4
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: 301af8ed877b58624e419c04f605c41f27dbdd0c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525730"
---
# <a name="whats-new-in-web-forms-in-aspnet-45"></a>Novinky webových formulářů v ASP.NET 4.5

podle [týmu webového Campy](https://twitter.com/webcamps)

> Nová verze webových formulářů ASP.NET zavádí řadu vylepšení, která se zaměřují na vylepšení uživatelského prostředí při práci s daty.
> 
> V předchozích verzích webových formulářů při použití datové vazby k vygenerování hodnoty člena objektu jste použili výrazy vázání dat Bind () nebo Eval (). V nové verzi ASP.NET můžete deklarovat, na jaký typ dat se ovládací prvek bude vázat, pomocí nové vlastnosti ItemType. Nastavení této vlastnosti vám umožní použít proměnnou silného typu k získání všech výhod prostředí pro vývoj sady Visual Studio, jako je IntelliSense, navigace členů a kontrola doby kompilace.
> 
> Pomocí ovládacích prvků vázaných na data můžete nyní také zadat vlastní metody pro výběr, aktualizaci, odstranění a vložení dat, což zjednodušuje interakci mezi ovládacími prvky stránky a logikou aplikace. Kromě toho byly přidány funkce vazby modelu do ASP.NET, což znamená, že data lze namapovat přímo do parametrů typu metody.
> 
> Ověřování vstupu uživatele by mělo být také snazší s nejnovější verzí webových formulářů. Nyní můžete opatřit třídy modelu pomocí atributů ověřování z oboru názvů **System. ComponentModel. DataAnnotations** a požádat, aby všechny ovládací prvky vaší lokality ověřovaly vstup uživatele pomocí těchto informací. Ověřování na straně klienta ve webových formulářích je teď integrované s jQuery, které poskytuje čisticí kód na straně klienta a nepřináší funkce JavaScriptu.
> 
> V oblasti ověření žádosti jsme udělali vylepšení, která usnadňují selektivní vypnutí žádostí o ověření pro konkrétní části vašich aplikací nebo čtení dat neověřených žádostí.
> 
> Některá vylepšení byla provedena v ovládacích prvcích webového formuláře Server, aby bylo možné využívat nové funkce HTML5:
> 
> - Vlastnost TextMode ovládacího prvku TextBox byla aktualizována tak, aby podporovala nové typy vstupu HTML5, jako je e-mail, DateTime a tak dále.
> - Ovládací prvek nahrání souboru teď podporuje více nahrávání souborů z prohlížečů, které podporují tuto funkci HTML5.
> - Ovládací prvky validátoru nyní podporují ověřování prvků jazyka HTML5.
> - Nové prvky HTML5 obsahující atributy, které reprezentují adresu URL, teď podporují runat =&quot;Server&quot;. V důsledku toho můžete použít konvence ASP.NET v cestách URL, jako je například operátor ~ představující kořen aplikace (například &lt;video runat =&quot;Server&quot; src =&quot;~/myVideo.wmv&quot;&gt;&lt;/video&gt;).
> - Ovládací prvek UpdatePanel byl vyřešen pro podporu při odesílání vstupních polí HTML5.
> 
> Na oficiálním portálu ASP.NET najdete další příklady nových funkcí v ASP.NET webformách 4,5: [co je nového v ASP.NET 4,5 a Visual Studio 2012](../../../../whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012.md#_Toc318097385) .
> 
> Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici na adrese [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).

<a id="Objectives"></a>
### <a name="objectives"></a>Cíle

V této praktické laboratorní laboratoři se dozvíte, jak:

- Použití výrazů pro datovou vazbu silně typovaného typu
- Použití nových funkcí vazby modelu ve webových formulářích
- Použití zprostředkovatelů hodnot pro mapování dat stránky na metody kódu na pozadí
- Použití datových poznámek pro ověřování vstupu uživatele
- Využijte nenáročné ověřování na straně klienta pomocí jQuery ve webových formulářích
- Implementace podrobného ověřování žádostí
- Implementace asynchronního zpracování stránky ve webových formulářích

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Předpoklady

K dokončení tohoto testovacího prostředí musíte mít následující položky:

- [Microsoft Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) nebo nadřazený seznam (pokyny k instalaci najdete v [příloze a](#AppendixA) ).

<a id="Setup"></a>
### <a name="setup"></a>Nastavení

**Instalace fragmentů kódu**

Pro usnadnění práce je většina kódu, který budete spravovat v tomto testovacím prostředí, k dispozici jako fragmenty kódu sady Visual Studio. Chcete-li nainstalovat fragmenty kódu, spusťte soubor **.\Source\Setup\CodeSnippets.vsi** .

Pokud nejste obeznámeni s fragmentem Visual Studio Code a chcete se dozvědět, jak je používat, můžete odkazovat na přílohu z tohoto dokumentu &quot;[příloze C: použití fragmentů kódu](#AppendixC)&quot;.

<a id="Exercises"></a>
## <a name="exercises"></a>Cvičení

Tato praktická cvičení zahrnují následující cvičení:

1. [Cvičení 1: vazba modelu ve webových formulářích ASP.NET](#Exercise1)
2. [Cvičení 2: ověření dat](#Exercise2)
3. [Cvičení 3: asynchronní zpracování stránky ve webových formulářích ASP.NET](#Exercise3)

> [!NOTE]
> Každé cvičení doprovází **koncovou** složku obsahující výsledné řešení, které byste měli získat po dokončení cvičení. Pokud potřebujete další nápovědu k práci prostřednictvím cvičení, můžete toto řešení použít jako vodítko.

Odhadovaný čas dokončení tohoto testovacího prostředí: **60 minut**.

<a id="Exercise1"></a>

<a id="Exercise_1_Model_Binding_in_ASPNET_Web_Forms"></a>
### <a name="exercise-1-model-binding-in-aspnet-web-forms"></a>Cvičení 1: vazba modelu ve webových formulářích ASP.NET

Nová verze webových formulářů ASP.NET zavádí řadu vylepšení, která se zaměřují na zlepšení prostředí při práci s daty. V průběhu tohoto cvičení se dozvíte o ovládacích prvcích dat a vázání modelů se silnými typy.

<a id="Task_1_-_Using_Strongly-Typed_Data-Bindings"></a>
#### <a name="task-1---using-strongly-typed-data-bindings"></a>Úloha 1 – použití datových vazeb silného typu

V této úloze zjistíte nové vazby silného typu, které jsou k dispozici v ASP.NET 4,5.

1. Otevřete řešení **zahájit** , které se nachází ve složce **source/EX1-ModelBinding/Begin/** Folder.

   1. Než budete pokračovat, budete muset stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
2. Otevřete stránku **Customers. aspx** . Umístěte nečíselný seznam do hlavního ovládacího prvku a zahrňte do výpisu každého zákazníka ovládací prvek Repeater. Nastavte název Repeater na **customersRepeater** , jak je znázorněno v následujícím kódu.

    V předchozích verzích webových formulářů při použití datové vazby k vygenerování hodnoty člena na objektu, na který datovou vazbu vytváříte, byste použili výraz vazby dat spolu s voláním metody Eval a předáním názvu člena jako řetězce.

    V době běhu tato volání Eval použijí reflexi proti aktuálně vázanému objektu pro čtení hodnoty člena se zadaným názvem a zobrazení výsledku v HTML. Díky tomuto přístupu je vazba dat velmi jednoduchá proti libovolným neobrazovým datům.

    Bohužel ztratíte spoustu skvělých funkcí prostředí pro vývoj v prostředí Visual Studio, včetně IntelliSense pro názvy členů, podporu navigace (například přejít k definici) a kontrolu doby kompilace.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample1.aspx)]
3. Otevřete soubor **Customers.aspx.cs** .
4. Přidejte následující příkaz using.

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample2.cs)]
5. Na **stránce\_metoda Load** přidejte kód pro naplnění tohoto opakovače seznamem zákazníků.

    (Fragment kódu- *webové formuláře Lab – Ex01 – zdroj dat pro zákazníky BIND*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample3.cs)]

    Řešení používá EntityFramework společně s CodeFirst k vytvoření a přístup k databázi. V následujícím kódu je customersRepeater vázán na materializující dotaz, který vrátí všechny zákazníky z databáze.
6. Stisknutím klávesy **F5** spusťte řešení a přejděte na stránku **Customers (zákazníci** ), aby se zobrazila akce Repeater v akci. Jak řešení používá CodeFirst, databáze se vytvoří a naplní v místní instanci SQL Express při spuštění aplikace.

    ![Výpis zákazníků s použitím Repeater](whats-new-in-web-forms-in-aspnet-45/_static/image1.png "Výpis zákazníků s použitím Repeater")

    *Výpis zákazníků s použitím Repeater*

    > [!NOTE]
    > V aplikaci Visual Studio 2012 je IIS Express výchozím webovým serverem pro vývoj.
7. Zavřete prohlížeč a vraťte se do sady Visual Studio.
8. Teď nahraďte implementaci, aby používala vazby silného typu. Otevřete stránku **Customers. aspx** a pomocí nového atributu **ItemType** v Repeater nastavte typ **zákazníka** jako typ vazby.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample4.aspx)]

    Vlastnost ItemType umožňuje deklarovat, na který typ dat bude ovládací prvek vázán, a umožňuje použít vazbu silného typu uvnitř ovládacího prvku vázaného na data.
9. Obsah ItemTemplate nahraďte následujícím kódem.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample5.aspx)]

    Jedním z Nevýhodou s výše uvedenými přístupy je to, že volání Eval () a BIND () jsou v pozdní vazbě, což znamená, že předáte řetězce, které představují názvy vlastností. To znamená, že nezískáte IntelliSense pro názvy členů, podporu navigace v kódu (například přejít k definici) ani podporu kontroly při kompilaci.

    Nastavením vlastnosti ItemType dojde k vygenerování dvou nových typových proměnných v rozsahu výrazů datové vazby: **Item** a **položku BindItem**. Tyto silně typované proměnné můžete použít ve výrazech datové vazby a získat kompletní výhody prostředí pro vývoj v aplikaci Visual Studio.

    &quot; **:** &quot; použitá ve výrazu automaticky zakóduje výstup do HTML, aby nedocházelo k problémům se zabezpečením (například k útokům prostřednictvím skriptování mezi weby). Tento zápis byl k dispozici od rozhraní .NET 4 pro zápis odpovědí, ale nyní je také k dispozici ve výrazech datové vazby.

    > [!NOTE]
    > Člen položky funguje jako jednosměrná vazba. Pokud chcete provést obousměrnou vazbu, použijte člen **položku BindItem** .

    ![Podpora technologie IntelliSense ve vazbách silného typu](whats-new-in-web-forms-in-aspnet-45/_static/image2.png "Podpora technologie IntelliSense ve vazbách silného typu")

    *Podpora technologie IntelliSense ve vazbách silného typu*
10. Stisknutím klávesy **F5** spusťte řešení a přejděte na stránku Customers (zákazníci) a ujistěte se, že změny fungují podle očekávání.

    ![Výpis podrobností o zákaznících](whats-new-in-web-forms-in-aspnet-45/_static/image3.png "Výpis podrobností o zákaznících")

    *Výpis podrobností o zákaznících*
11. Zavřete prohlížeč a vraťte se do sady Visual Studio.

<a id="Task_2_-_Introducing_Model_Binding_in_Web_Forms"></a>
#### <a name="task-2---introducing-model-binding-in-web-forms"></a>Úloha 2 – zavedení vazby modelu ve webových formulářích

V předchozích verzích webových formulářů ASP.NET, pokud jste chtěli provést obousměrnou datovou vazbu, načítají a aktualizují data, je třeba použít objekt zdroje dat. Může to být zdroj dat objektu, zdroj dat SQL, zdroj dat LINQ atd. Pokud ale váš scénář požaduje vlastní kód pro zpracování dat, je potřeba použít zdroj dat objektu a tím se napravily nějaké nevýhody. Například je třeba se vyhnout složitým typům a při provádění logiky ověřování potřebujete zpracovat výjimky.

V nové verzi webových formulářů ASP.NET podporují ovládací prvky vázané na data vazbu modelu. To znamená, že můžete zadat metody Select, Update, INSERT a DELETE přímo v ovládacím prvku vázaného na data pro volání logiky ze souboru kódu na pozadí nebo z jiné třídy.

Pokud se o to chcete dozvědět, použijte prvek GridView k vypsání kategorií produktů pomocí nového atributu **SelectMethod** . Tento atribut umožňuje zadat metodu pro načtení dat GridView.

1. Otevřete stránku **Products. aspx** a přidejte **prvek GridView**. Nakonfigurujte prvek GridView tak, jak je znázorněno níže, aby bylo možné použít vazby silného typu a Povolit řazení a stránkování.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample6.aspx)]
2. Použijte nový atribut **SelectMethod** ke konfiguraci prvku GridView pro volání metody **GetCategories** pro výběr dat.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample7.aspx)]
3. Otevřete soubor kódu na pozadí **Products.aspx.cs** a přidejte následující příkazy using.

    (Fragment kódu – *webové formuláře Lab-Ex01-Namespaces*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample8.cs)]
4. Přidejte do třídy **Products** privátního člena a přiřaďte novou instanci **ProductsContext**. Tato vlastnost uloží datový kontext Entity Framework, který vám umožní připojit se k databázi.

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample9.cs)]
5. Vytvořte metodu **GetCategories** pro načtení seznamu kategorií pomocí LINQ. Dotaz bude obsahovat vlastnost **Products** , aby prvek GridView mohl zobrazit množství produktů pro každou kategorii. Všimněte si, že metoda vrátí nezpracovaný objekt IQueryable, který představuje dotaz, který má být proveden později v životním cyklu stránky.

    (Fragment kódu- *webové formuláře Lab-Ex01-GetCategories*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample10.cs)]

    > [!NOTE]
    > V předchozích verzích webových formulářů ASP.NET umožňuje řazení a stránkování pomocí vlastní logiky úložiště v rámci kontextu zdroje dat objektu, který je vyžadován pro zápis vlastního kódu a příjem všech potřebných parametrů. Nyní, protože metody vázání dat mohou vracet IQueryable a to představuje dotaz, který má být spuštěn, ASP.NET se může postarat o změnu dotazu pro přidání správných parametrů řazení a stránkování.
6. Stisknutím klávesy **F5** spusťte ladění webu a přejděte na stránku produkty. Měli byste vidět, že je prvek GridView naplněn kategoriemi vrácenými metodou GetCategories.

    ![Naplnění prvku GridView pomocí vazby modelu](whats-new-in-web-forms-in-aspnet-45/_static/image4.png "Naplnění prvku GridView pomocí vazby modelu")

    *Naplnění prvku GridView pomocí vazby modelu*
7. Stiskněte **SHIFT**+**F5** zastavit ladění.

<a id="Task_3_-_Value_Providers_in_Model_Binding"></a>
#### <a name="task-3---value-providers-in-model-binding"></a>Zprostředkovatelé úlohy 3-hodnota ve vazbě modelu

Vazba modelu umožňuje zadat vlastní metody pro práci s daty přímo v ovládacím prvku vázaného na data, ale také umožňuje mapovat data ze stránky na parametry z těchto metod. V parametru metody můžete použít atributy zprostředkovatele hodnoty k určení zdroje dat hodnoty. Příklad:

- Ovládací prvky na stránce
- Hodnoty řetězce dotazu
- Zobrazení dat
- Stav relace
- Soubory cookie
- Odeslaná data formuláře
- Stav zobrazení
- Podporují se i vlastní zprostředkovatelé hodnot.

Pokud jste použili ASP.NET MVC 4, budete si všimnout, že je podpora vazeb modelů podobná. Tyto funkce byly skutečně pořízeny z ASP.NET MVC a přesunuty do sestavení **System. Web** , aby je bylo možné použít i ve webových formulářích.

V této úloze aktualizujete prvek GridView tak, aby vyfiltroval výsledky podle množství produktů pro každou kategorii, a přijímá parametr filtru s vazbou modelu.

1. Vraťte se na stránku **Products. aspx** .
2. V horní části prvku GridView přidejte **popisek** a **pole se seznamem** pro výběr počtu produktů pro každou kategorii, jak je znázorněno níže.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample11.aspx)]
3. Do prvku GridView přidejte **šablonu EmptyDataTemplate** , aby se zobrazila zpráva, když neexistují žádné kategorie s vybraným počtem produktů.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample12.aspx)]
4. Otevřete **Products.aspx.cs** kód na pozadí a přidejte následující příkaz using.

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample13.cs)]
5. Upravte metodu **GetCategories** pro příjem celočíselného argumentu **minProductsCount** a filtrování vrácených výsledků. Chcete-li to provést, nahraďte metodu následujícím kódem.

    (Fragment kódu- *webové formuláře Lab-Ex01-getkategorie 2*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample14.cs)]

    Nový atribut **[Control]** v argumentu **minProductsCount** umožní ASP.NET, že jeho hodnota musí být naplněna pomocí ovládacího prvku na stránce. ASP.NET bude hledat všechny ovládací prvky, které odpovídají názvu argumentu (minProductsCount), a provést potřebné mapování a převod pro vyplnění parametru hodnotou ovládacího prvku.

    Alternativně atribut poskytuje přetížený konstruktor, který umožňuje určit ovládací prvek, ze kterého se má získat hodnota.

    > [!NOTE]
    > Jedním z cílů funkcí datové vazby je snížení množství kódu, který je nutné zapsat pro interakci stránky. Kromě poskytovatele hodnot [Control] můžete použít jiné poskytovatele vazeb modelů v parametrech metody. Některé z nich jsou uvedené v úvodu k úloze.
6. Stisknutím klávesy **F5** spusťte ladění webu a přejděte na stránku produkty. V rozevíracím seznamu vyberte počet produktů a Všimněte si, jak je prvek GridView nyní aktualizován.

    ![Filtrování prvku GridView s hodnotou rozevíracího seznamu](whats-new-in-web-forms-in-aspnet-45/_static/image5.png "Filtrování prvku GridView s hodnotou rozevíracího seznamu")

    *Filtrování prvku GridView s hodnotou rozevíracího seznamu*
7. Zastavit ladění.

<a id="Task_4_-_Using_Model_Binding_for_Filtering"></a>
#### <a name="task-4---using-model-binding-for-filtering"></a>Úloha 4 – použití vazby modelu pro filtrování

V této úloze přidáte druhý podřízený prvek GridView k zobrazení produktů v rámci vybrané kategorie.

1. Otevřete stránku **Products. aspx** a aktualizujte pole GridView kategorií tak, aby automaticky vygenerovalo tlačítko pro výběr.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample15.aspx)]
2. V dolní části přidejte druhý **prvek GridView** s názvem **productsGrid** . Nastavte typ **ItemType** na **WebFormsLab. model. Product**, **DataKeyNames** na **ProductID** a vlastnost **SelectMethod** na **GetProducts**. Nastavte **AutoGenerateColumns** na **false** a přidejte sloupce pro ProductID, ProductName, Description a UnitPrice.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample16.aspx)]
3. Otevřete soubor kódu na pozadí **Products.aspx.cs** . Implementací metody **GetProducts** můžete získat ID kategorie z prvku GridView kategorie a filtrovat produkty. Vazba modelu nastaví hodnotu parametru pomocí vybraného řádku v **categoriesGrid**. Vzhledem k tomu, že název argumentu a název ovládacího prvku se neshodují, měli byste zadat název ovládacího prvku ve zprostředkovateli hodnoty ovládacího prvku.

    (Fragment kódu – *webové formuláře Lab-Ex01-GetProducts*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample17.cs)]

    > [!NOTE]
    > Tento přístup usnadňuje testování částí těchto metod. V kontextu testování částí, kdy webové formuláře nejsou spuštěny, atribut [Control] neprovede žádnou konkrétní akci.
4. Otevřete stránku **Products. aspx** a vyhledejte prvek GridView Products. Aktualizujte prvek GridView pro produkty, aby se zobrazil odkaz pro úpravu vybraného produktu.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample18.aspx)]
5. Otevřete stránku **ProductDetails. aspx** s kódem na pozadí a nahraďte metodu **SelectProduct** následujícím kódem.

    (Fragment kódu- *webové formuláře Lab-Ex01-SelectProduct*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample19.cs)]

    > [!NOTE]
    > Všimněte si, že atribut **[QueryString]** je použit k vyplnění parametru metody z parametru ProductID v řetězci dotazu.
6. Stisknutím klávesy **F5** spusťte ladění webu a přejděte na stránku produkty. V prvku GridView kategorie vyberte libovolnou kategorii a Všimněte si, že jsou aktualizovány informace v prvku GridView.

    ![Zobrazení produktů z vybrané kategorie](whats-new-in-web-forms-in-aspnet-45/_static/image6.png "Zobrazení produktů z vybrané kategorie")

    *Zobrazení produktů z vybrané kategorie*
7. Kliknutím na odkaz **zobrazení** na produkt otevřete stránku ProductDetails. aspx.

    Všimněte si, že stránka načítá produkt s metodou SelectMethod pomocí parametru productId z řetězce dotazu.

    ![Zobrazení podrobností o produktu](whats-new-in-web-forms-in-aspnet-45/_static/image7.png "Zobrazení podrobností o produktu")

    *Zobrazení podrobností o produktu*

    > [!NOTE]
    > Možnost napsat popis HTML bude implementována při dalším cvičení.

<a id="Task_5_-_Using_Model_Binding_for_Update_Operations"></a>
#### <a name="task-5---using-model-binding-for-update-operations"></a>Úloha 5 – použití vazby modelu pro operace aktualizace

V předchozím úkolu jste použili vazbu modelu hlavně pro výběr dat. v tomto úkolu se naučíte používat vazbu modelu v operacích aktualizace.

Aktualizujete prvek GridView kategorie, aby uživatel mohl aktualizovat kategorie.

1. Otevřete stránku **Products. aspx** a aktualizujte pole GridView kategorií tak, aby automaticky vygenerovalo tlačítko Upravit, a pomocí nového atributu **UpdateMethod** určete metodu **UpdateCategory** pro aktualizaci vybrané položky.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample20.aspx)]

    Atribut DataKeyNames v prvku GridView definuje, které jsou členy, kteří jedinečně identifikují objekt vázaný na model, a proto jsou parametry, které by metoda Update měla aspoň přijmout.
2. Otevřete soubor kódu na pozadí **Products.aspx.cs** a Implementujte metodu **UpdateCategory** . Metoda by měla získat ID kategorie, aby se načetla aktuální kategorie, naplňte hodnoty z prvku GridView a pak kategorii aktualizovat.

    (Fragment kódu – *webové formuláře Lab-Ex01-UpdateCategory*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample21.cs)]

    Nová metoda **TryUpdateModel** v třídě Page zodpovídá za naplnění objektu modelu pomocí hodnot z ovládacích prvků na stránce. V tomto případě nahradí aktualizované hodnoty z aktuálního řádku GridView upravovaného do objektu **Category** .

    > [!NOTE]
    > Další cvičení Vysvětlete použití ModelState. IsValid pro ověřování dat zadaných uživatelem při úpravách objektu.
3. Spusťte web a přejdete na stránku produkty. Upravte kategorii. Zadejte nový název a kliknutím na **aktualizovat** zachovejte změny.

    ![Úpravy kategorií](whats-new-in-web-forms-in-aspnet-45/_static/image8.png "Úpravy kategorií")

    *Úpravy kategorií*

<a id="Exercise2"></a>

<a id="Exercise_2_Data_Validation"></a>
### <a name="exercise-2-data-validation"></a>Cvičení 2: ověření dat

V tomto cvičení se dozvíte o nových funkcích ověřování dat v ASP.NET 4,5. Ve webových formulářích se dozvíte o nových nenápadných funkcích ověřování. Pro ověření vstupu uživatele použijete datové poznámky v třídách aplikačního modelu a nakonec se dozvíte, jak na stránce zapnout nebo vypnout ověřování žádosti na jednotlivé ovládací prvky.

<a id="Task_1_-_Unobtrusive_Validation"></a>
#### <a name="task-1---unobtrusive-validation"></a>Úloha 1 – nenáročná ověření

Formuláře obsahující složitá data, včetně validátorů, obvykle generují příliš mnoho kódů JavaScriptu na stránce, což může představovat přibližně 60% kódu. Když je povolené nenáročné ověřování, váš kód HTML bude vypadat jako čistič a tidier.

V této části povolíte nenáročné ověřování v ASP.NET k porovnání kódu HTML generovaného oběma konfiguracemi.

1. Otevřete **Visual Studio 2012** a otevřete řešení **Spustit** ve složce **Source\Ex2-Validation\Begin** tohoto testovacího prostředí. Případně můžete pokračovat v práci na stávajícím řešení z předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. To provedete tak, že v Průzkumník řešení kliknete na projekt **WebFormsLab** **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
2. Stisknutím klávesy **F5** spusťte webovou aplikaci. Přejděte na stránku Customers (zákazníci) a klikněte na odkaz **Přidat nového zákazníka** .
3. Klikněte pravým tlačítkem na stránku prohlížeče a výběrem možnosti **Zobrazit zdroj** otevřete kód HTML generovaný aplikací.

    ![Zobrazení kódu HTML stránky](whats-new-in-web-forms-in-aspnet-45/_static/image9.png "Zobrazení kódu HTML stránky")

    *Zobrazení kódu HTML stránky*
4. Posuňte se na zdrojový kód stránky a Všimněte si, že ASP.NET vložil kód JavaScriptu a validátory dat na stránce, aby provedla ověření a zobrazila seznam chyb.

    ![Kód JavaScript ověřování na stránce CustomerDetails](whats-new-in-web-forms-in-aspnet-45/_static/image10.png "Kód JavaScript ověřování na stránce CustomerDetails")

    *Kód JavaScript ověřování na stránce CustomerDetails*
5. Zavřete prohlížeč a vraťte se do sady Visual Studio.
6. Nyní povolíte nenáročné ověřování. Otevřete soubor **Web. config** a vyhledejte v části **appSettings** klíč **ValidationSettings: UnobtrusiveValidationMode** **.** Nastavte hodnotu klíče na **WebForms**.

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample22.xml)]

    > [!NOTE]
    > Tuto vlastnost můžete také nastavit na **stránce &quot;\_událost Load**&quot; pro případ, že chcete povolit nenáročná ověřování pouze pro některé stránky.
7. Otevřete **CustomerDetails. aspx** a stisknutím klávesy **F5** spusťte webovou aplikaci.
8. Stisknutím klávesy F12 otevřete nástroje pro vývojáře IE. Po otevření nástrojů pro vývojáře vyberte kartu skript. z nabídky vyberte **CustomerDetails. aspx** a Všimněte si, že skripty potřebné ke spuštění jQuery na stránce byly načteny do prohlížeče z místní lokality.

    ![Načítání souborů JavaScriptu jQuery přímo z místního serveru služby IIS](whats-new-in-web-forms-in-aspnet-45/_static/image11.png "Načítání souborů JavaScriptu jQuery přímo z místního serveru služby IIS")

    *Načítání souborů JavaScriptu jQuery přímo z místního serveru služby IIS*
9. Zavřete prohlížeč a vraťte se do sady Visual Studio. Znovu otevřete soubor **Web. Master** a vyhledejte **ScriptManager**. Přidejte vlastnost **EnableCdn** atributu s hodnotou **true**. Vynutí se tak, aby jQuery bylo načteno z adresy URL online, nikoli z adresy URL místního webu.
10. Otevřete **CustomerDetails. aspx** v aplikaci Visual Studio. Stisknutím klávesy F5 spusťte Web. Po otevření Internet Exploreru stiskněte klávesu F12 a otevřete nástroje pro vývojáře. Vyberte kartu **skript** a potom se podívejte na rozevírací seznam. Všimněte si, že se už nenačítá soubory JavaScriptu pro JavaScript z místní lokality, ale místo z online jQuery CDN.

    ![Načítání souborů JavaScriptu jQuery z CDN](whats-new-in-web-forms-in-aspnet-45/_static/image12.png "Načítání souborů JavaScriptu jQuery z CDN")

    *Načítání souborů JavaScriptu jQuery z CDN*
11. Znovu otevřete zdrojový kód stránky HTML pomocí možnosti zobrazit zdroj v prohlížeči. Všimněte si, že povolením nenáročného ověřování ASP.NET nahradili vložený kód jazyka JavaScript pomocí atributů \*dat.

    ![Nenápadný ověřovací kód](whats-new-in-web-forms-in-aspnet-45/_static/image13.png "Nenápadný ověřovací kód")

    *Nenápadný ověřovací kód*

    > [!NOTE]
    > V tomto příkladu jste viděli, jak se souhrn ověření s poznámkami k datům zjednodušil jenom na několik řádků HTML a JavaScript. Dříve, bez neúspěšného ověření, bude lepší ovládací prvky ověřování, které přidáte, tím větší bude růst kód pro ověření JavaScriptu.

<a id="Task_2_-_Validating_the_Model_with_Data_Annotations"></a>
#### <a name="task-2---validating-the-model-with-data-annotations"></a>Úloha 2 – ověření modelu pomocí datových poznámek

ASP.NET 4,5 zavádí pro webové formuláře ověřování datových poznámek. Místo toho, abyste měli ovládací prvek ověřování u každého vstupu, teď můžete definovat omezení v třídách modelu a používat je napříč všemi vašimi webovými aplikacemi. V této části se dozvíte, jak používat datové poznámky k ověření formuláře pro nový/upravit zákazníka.

1. Otevřete stránku **CustomerDetail. aspx** . Všimněte si, že křestní jméno zákazníka a druhý název v sekcích **EditItemTemplate** a **Šablona InsertItemTemplate** se ověřují pomocí ovládacích prvků RequiredFieldValidator. Každý validátor je přidružen ke konkrétní podmínce, takže musíte zahrnout tolik validátorů jako podmínky kontroly.
2. Přidejte datové poznámky pro ověření třídy modelu zákazníka. Otevřete třídu **Customer.cs** ve složce **modelu** a *naupravte* jednotlivé vlastnosti pomocí atributů datových poznámek.

    (Fragment kódu – *webové formuláře Lab – Ex02 – datové poznámky*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample23.cs)]

    > [!NOTE]
    > .NET Framework 4,5 rozšířil existující kolekci poznámek k datům. Tady jsou některé poznámky k datům, které můžete použít: [CreditCard], [telefon], [EmailAddress], [rozsah], [Compare], [URL], [přípony a rozšíření], [povinné], [klíč], [RegularExpression].
    > 
    > Některé příklady použití:
    > 
    > [Klíč]: Specifies that an attribute is the unique identifier
    > 
    > [Range(0.4, 0.5, ErrorMessage=&quot;{Write an error message}&quot;]: Double range
    > 
    > [EmailAddress(ErrorMessage=&quot;Invalid Email&quot;), MaxLength(56)]: Two annotations in the same line.
    > 
    > V rámci každého atributu můžete také definovat vlastní chybové zprávy.
3. Otevřete **CustomerDetails. aspx** a odeberte všechny RequiredFieldValidators pro pole jméno a příjmení v částech EditItemTemplate a šablona InsertItemTemplate ovládacího prvku FormView.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample24.aspx)]

    > [!NOTE]
    > Jednou z výhod použití datových poznámek je, že logika ověřování není na stránkách aplikace duplikována. V modelu je nadefinujete a použijete ji na všech stránkách aplikace, které pracují s daty.
4. Otevřete **CustomerDetails. aspx** Code a vyhledejte metodu SaveCustomer. Tato metoda je volána při vkládání nového zákazníka a přijímá parametr zákazníka z hodnot ovládacího prvku FormView. Když dojde k mapování mezi ovládacími prvky stránky a objektem parametru, ASP.NET spustí ověřování modelu proti všem atributům datových poznámek a vyplní slovník ModelState o zjištěné chyby, pokud existují.

    ModelState. IsValid vrátí hodnotu true pouze v případě, že všechna pole v modelu jsou po provedení ověření platná.

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample25.cs)]
5. Na konec stránky CustomerDetails přidejte ovládací prvek **ovládací souhrnu ověření** , který zobrazí seznam chyb modelu.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample26.aspx)]

    **ShowModelStateErrors** je nová vlastnost v ovládacím prvku ovládací souhrnu ověření, která Pokud je nastavena na **hodnotu true**, ovládací prvek zobrazí chyby ze slovníku ModelState. Tyto chyby pocházejí z ověřování datových poznámek.
6. Stisknutím klávesy **F5** spusťte webovou aplikaci. Vyplňte formulář s některými chybnými hodnotami a kliknutím na **Uložit** spusťte ověřování. Všimněte si souhrnu chyb v dolní části.

    ![Ověřování pomocí datových poznámek](whats-new-in-web-forms-in-aspnet-45/_static/image14.png "Ověřování pomocí datových poznámek")

    *Ověřování pomocí datových poznámek*

<a id="Task_3_-_Handling_Custom_Database_Errors_with_ModelState"></a>
#### <a name="task-3---handling-custom-database-errors-with-modelstate"></a>Úloha 3 – zpracování chyb vlastních databází pomocí ModelState

V předchozí verzi webových formulářů zpracování chyb databáze, jako je příliš dlouhý řetězec nebo porušení jedinečného klíče, může zahrnovat vyvolání výjimek v kódu úložiště a následné zpracování výjimek v kódu na pozadí, aby se zobrazila chyba. K tomu je potřeba Skvělé množství kódu, abyste mohli něco poměrně snadno udělat.

Ve webových formulářích 4,5 lze objekt ModelState použít k zobrazení chyb na stránce, a to buď z modelu, nebo z databáze, konzistentním způsobem.

V této úloze přidáte kód pro správné zpracování výjimek databáze a zobrazíte příslušnou zprávu uživateli pomocí objektu ModelState.

1. I když je aplikace stále spuštěná, zkuste aktualizovat název kategorie pomocí duplicitní hodnoty.

    ![Aktualizace kategorie s duplicitním názvem](whats-new-in-web-forms-in-aspnet-45/_static/image15.png "Aktualizace kategorie s duplicitním názvem")

    *Aktualizace kategorie s duplicitním názvem*

    Všimněte si, že výjimka je vyvolána z důvodu &quot;jedinečné omezení&quot; sloupce **NázevKategorie** .

    ![Výjimka pro duplicitní názvy kategorií](whats-new-in-web-forms-in-aspnet-45/_static/image16.png "Výjimka pro duplicitní názvy kategorií")

    *Výjimka pro duplicitní názvy kategorií*
2. Zastavit ladění. V souboru kódu na pozadí **Products.aspx.cs** aktualizujte metodu **UpdateCategory** pro zpracování výjimek vyvolaných databází. Metoda SaveChanges () volá a přidá chybu do objektu **ModelState** .

    Nová metoda **TryUpdateModel** aktualizuje objekt kategorie načtený z databáze pomocí dat formuláře zadaného uživatelem.

    (Fragment kódu – *webové formuláře Lab-Ex02-UpdateCategory chyby zpracování*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample27.cs)]

    > [!NOTE]
    > V ideálním případě by bylo nutné určit příčinu DbUpdateException a ověřit, zda je hlavní příčinou porušení omezení jedinečného klíče.
3. Otevřete **Products. aspx** a přidejte ovládací prvek **ovládací souhrnu ověření** pod položku kategorie GridView, aby se zobrazil seznam chyb modelu.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample28.aspx)]
4. Spusťte web a přejdete na stránku produkty. Zkuste aktualizovat název kategorie pomocí duplicitní hodnoty.

    Všimněte si, že výjimka byla zpracována a chybová zpráva se zobrazí v ovládacím prvku **ovládací souhrnu ověření** .

    ![Chyba duplicitní kategorie](whats-new-in-web-forms-in-aspnet-45/_static/image17.png "Chyba duplicitní kategorie")

    *Chyba duplicitní kategorie*

<a id="Task_4_-_Request_Validation_in_ASPNET_Web_Forms_45"></a>
#### <a name="task-4---request-validation-in-aspnet-web-forms-45"></a>Úloha 4 – požadavek na ověření ve webových formulářích ASP.NET 4,5

Funkce ověření žádosti v ASP.NET poskytuje určitou úroveň výchozí ochrany proti útokům prostřednictvím skriptování mezi weby (XSS). V předchozích verzích ASP.NET bylo ověření žádosti ve výchozím nastavení povolené a bylo možné ho zakázat jenom pro celou stránku. S novou verzí webových formulářů ASP.NET teď můžete zakázat ověření žádosti pro jeden ovládací prvek, provést ověřování opožděným požadavkem nebo získat přístup k neověřeným datům žádostí (Buďte opatrní, pokud to uděláte!).

1. Stisknutím **kombinace kláves CTRL + F5** web spusťte bez ladění a přejděte na stránku produkty. Vyberte kategorii a pak klikněte na odkaz **Upravit** na libovolném z produktů.
2. Zadejte popis, který obsahuje potenciálně nebezpečný obsah, například značky HTML. Vezměte v úvahu výjimku vyvolanou v důsledku ověření žádosti.

    ![Úprava produktu s potenciálně nebezpečným obsahem](whats-new-in-web-forms-in-aspnet-45/_static/image18.png "Úprava produktu s potenciálně nebezpečným obsahem")

    *Úprava produktu s potenciálně nebezpečným obsahem*

    ![Vyvolaná výjimka kvůli ověření žádosti](whats-new-in-web-forms-in-aspnet-45/_static/image19.png "Vyvolaná výjimka kvůli ověření žádosti")

    *Vyvolaná výjimka kvůli ověření žádosti*
3. Zavřete stránku a v aplikaci Visual Studio stisknutím kláves **SHIFT + F5** Zastavte ladění.
4. Otevřete stránku **ProductDetails. aspx** a vyhledejte textové pole **Popis** .
5. Do textového pole přidejte novou vlastnost **ValidateRequestMode** a nastavte její hodnotu na **disabled (zakázáno**).

    Nový atribut **ValidateRequestMode** vám umožňuje v každém ovládacím prvku zablokovat podrobné ověřování požadavků. To je užitečné, pokud chcete použít vstup, který může obdržet kód HTML, ale chcete, aby ověřování fungovalo pro zbytek stránky.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample29.aspx)]
6. Stisknutím klávesy **F5** spusťte webovou aplikaci. Otevřete znovu stránku Upravit produkt a dokončete Popis produktu včetně značek HTML. Všimněte si, že teď můžete do popisu přidat obsah HTML.

    ![Požadavek na ověření pro popis produktu zakázán](whats-new-in-web-forms-in-aspnet-45/_static/image20.png "Požadavek na ověření pro popis produktu zakázán")

    *Požadavek na ověření pro popis produktu zakázán*

    > [!NOTE]
    > V produkční aplikaci byste měli upravit kód HTML zadaný uživatelem, aby se zajistilo, že se zadají jenom bezpečné značky HTML (například nejsou k dispozici žádné &lt;značky&gt; skriptu). K tomu můžete použít [knihovnu Microsoft Web Protection Library](https://www.nuget.org/packages/AntiXSS).
7. Upravte produkt znovu. Do pole název zadejte kód HTML a klikněte na **Uložit**. Všimněte si, že žádosti o ověření jsou zakázané jenom pro pole Popis a zbývající pole se znovu ověřují proti potenciálně nebezpečnému obsahu.

    ![Žádost o ověření povolena ve zbývajících polích](whats-new-in-web-forms-in-aspnet-45/_static/image21.png "Žádost o ověření povolena ve zbývajících polích")

    *Žádost o ověření povolena ve zbývajících polích*

    Webové formuláře ASP.NET 4,5 obsahují nový režim ověřování žádostí, který provede ověření žádosti laxně vytvářená. V případě, že je v režimu ověření žádosti nastavena na **4,5**, je-li část kódu přistupuje k *žádosti. formulář [&quot;Key&quot;]* , ověření žádosti ASP.NET 4.5 spustí pouze ověření žádosti pro tento konkrétní prvek v kolekci formulářů.

    Kromě toho ASP.NET 4,5 teď obsahuje základní rutiny kódování z knihovny Microsoft Anti-XSS Library v 4.0. Rutiny kódování anti-XSS jsou implementované novým typem *AntiXssEncoder* , který najdete v oboru názvů New **System. Web. Security. AntiXSS** . S parametrem **encoderType** nakonfigurovaným pro použití *AntiXssEncoder*, všechna výstupní kódování v rámci ASP.NET automaticky používá nové rutiny kódování.
8. Ověření žádosti ASP.NET 4,5 také podporuje neověřený přístup k žádostem o data. ASP.NET 4,5 přidá novou vlastnost kolekce do objektu **HttpRequest** s názvem **unvalidateed**. Když přejdete do **HttpRequest. Neověřeno** máte přístup ke všem běžným datům požadavků, včetně formulářů, querystrings, souborů cookie, adres URL a tak dále.

    ![Request. unvalidateed – objekt](whats-new-in-web-forms-in-aspnet-45/_static/image22.png "Request. unvalidateed – objekt")

    *Request. unvalidateed – objekt*

    > [!NOTE]
    > **Použijte prosím vlastnost HttpRequest. unvalidateed s opatrností!** Ujistěte se, že jste pečlivě provedli vlastní ověření u nezpracovaných dat požadavků, abyste zajistili, že netripý text nebudete zaokrouhlit na nepodezřelé zákazníky.

<a id="Exercise3"></a>

<a id="Exercise_3_Asynchronous_Page_Processing_in_ASPNET_Web_Forms"></a>
### <a name="exercise-3-asynchronous-page-processing-in-aspnet-web-forms"></a>Cvičení 3: asynchronní zpracování stránky ve webových formulářích ASP.NET

V tomto cvičení se zavedete na nové funkce asynchronního zpracování stránky ve webových formulářích ASP.NET.

<a id="Task_1_-_Updating_the_Product_Details_Page_to_Upload_and_Show_Images"></a>
#### <a name="task-1---updating-the-product-details-page-to-upload-and-show-images"></a>Úloha 1 – aktualizace stránky s podrobnostmi o produktu pro nahrávání a zobrazování imagí

V této úloze aktualizujete stránku s podrobnostmi o produktu, aby uživatel mohl zadat adresu URL obrázku pro daný produkt a zobrazit ho v zobrazení jen pro čtení. Místní kopii zadané image vytvoříte tak, že ji stáhnete synchronně. V další úloze aktualizujete tuto implementaci, aby fungovala asynchronně.

1. Otevřete **Visual Studio 2012** a z této složky testovacího prostředí načtěte řešení **Begin** , které najdete v **Source\Ex3-Async\Begin** . Případně můžete pokračovat v práci na stávajícím řešení z předchozích cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že v Průzkumník řešení kliknete na projekt **WebFormsLab** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
2. Otevřete zdroj stránky **ProductDetails. aspx** a přidejte pole do šablony ItemTemplate třídy FormView, kde zobrazíte obrázek produktu.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample30.aspx)]
3. Přidejte pole k určení adresy URL obrázku v EditTemplate třídy FormView.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample31.aspx)]
4. Otevřete soubor kódu na pozadí **ProductDetails.aspx.cs** a přidejte následující direktivy oboru názvů.

    (Fragment kódu – *webové formuláře Lab-Ex03-Namespaces*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample32.cs)]
5. Vytvořte metodu **UpdateProductImage** pro ukládání vzdálených imagí do složky místních **imagí** a aktualizujte entitu produkt o novou hodnotu umístění bitové kopie.

    (Fragment kódu – *webové formuláře Lab-Ex03-UpdateProductImage*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample33.cs)]
6. Aktualizujte metodu **UpdateProduct** pro volání metody **UpdateProductImage** .

    (Fragment kódu – *webové formuláře Lab – Ex03 – volání UpdateProductImage*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample34.cs)]
7. Spusťte aplikaci a pokuste se odeslat obrázek pro produkt. Například můžete použít následující adresu URL obrázku z Office Clip umění: [ [http://officeimg.vo.msecnd.net/images/MB900437099.jpg](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)

    ![Nastavení obrázku pro produkt](whats-new-in-web-forms-in-aspnet-45/_static/image23.png "Nastavení obrázku pro produkt")

    *Nastavení obrázku pro produkt*

<a id="Task_2_-_Adding_Asynchronous_Processing_to_the_Product_Details_Page"></a>
#### <a name="task-2---adding-asynchronous-processing-to-the-product-details-page"></a>Úloha 2 – Přidání asynchronního zpracování na stránku s podrobnostmi o produktu

V této úloze aktualizujete stránku s podrobnostmi o produktu, abyste ji mohli asynchronně pracovat. Pomocí asynchronního zpracování stránky ASP.NET 4,5 vylepšíte dlouho běžící úlohu – proces stahování obrazu.

Asynchronní metody ve webových aplikacích lze použít k optimalizaci způsobu použití fondů vláken ASP.NET. V ASP.NET existuje omezený počet vláken ve fondu vláken pro účast požadavků, takže pokud jsou všechna vlákna zaneprázdněná, ASP.NET začne zamítnout nové žádosti, odesílá chybové zprávy aplikace a zpřístupňuje váš web jako nedostupný.

Časově náročné operace na webu jsou skvělé kandidáty na asynchronní programování, protože zabírají přiřazené vlákno po dlouhou dobu. To zahrnuje dlouho běžící požadavky, stránky s velkým množstvím různých prvků a stránek, které vyžadují offline operace, jako je dotazování databáze nebo přístup k externímu webovému serveru. Výhoda spočívá v tom, že pokud použijete asynchronní metody pro tyto operace, zatímco stránka je zpracovávána, vlákno je uvolněno a vráceno do fondu vláken a lze je použít k účasti na nové žádosti stránky. To znamená, že se stránka začne zpracovávat v jednom vlákně z fondu vláken a po dokončení asynchronního zpracování může dokončit zpracování v jiném z nich.

1. Otevřete stránku **ProductDetails. aspx** . Přidejte atribut **Async** do elementu **Page** a nastavte jej na **hodnotu true**. Tento atribut určuje, že ASP.NET implementuje rozhraní IHttpAsyncHandler.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample35.aspx)]
2. Přidáním popisku v dolní části stránky zobrazíte podrobnosti o vláknech, na kterých je stránka spuštěna.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample36.aspx)]
3. Otevřete **ProductDetails.aspx.cs** a přidejte následující direktivy oboru názvů.

    (Fragment kódu- *webové formuláře Lab-Ex03-Namespaces 2*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample37.cs)]
4. Upravte metodu **UpdateProductImage** a stáhněte bitovou kopii pomocí asynchronní úlohy. Metodu **WebClient** **DownloadFile** nahradíte metodou **DownloadFileTaskAsync** a zahrnete klíčové slovo **await** .

    (Fragment kódu- *webové formuláře Lab-Ex03-UpdateProductImage Async*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample38.cs)]

    RegisterAsyncTask registruje novou stránku asynchronní úlohu, která se má spustit v jiném vlákně. Přijímá výraz lambda s úkolem (t), který má být proveden. Klíčové slovo **await** v metodě **DownloadFileTaskAsync** převede zbytek metody do zpětného volání, které je vyvoláno asynchronně po dokončení metody **DownloadFileTaskAsync** . ASP.NET bude pokračovat v provádění metody tím, že automaticky zachovává všechny původní hodnoty požadavku HTTP. Nový asynchronní programovací model v rozhraní .NET 4,5 umožňuje psát asynchronní kód, který vypadá velmi podobně jako synchronní kód, a nechat kompilátorem zpracovat komplikace funkcí zpětného volání nebo kódu pokračování.
    > [!NOTE]
    > RegisterAsyncTask a ExecuteInParallel byly již k dispozici od .NET 2,0. Klíčové slovo await je nového z asynchronního programovacího modelu .NET 4,5 a lze jej použít spolu s novými metodami TaskAsync z objektu rozhraní .NET WebClient.
5. Přidejte kód pro zobrazení vláken, na kterých byl kód spuštěn a dokončen. Chcete-li to provést, aktualizujte metodu **UpdateProductImage** pomocí následujícího kódu.

    (Fragment kódu – *webové formuláře Lab-Ex03-Zobrazit vlákna*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample39.cs)]
6. Otevřete soubor **Web. config** webu. Přidejte následující proměnnou appSetting.

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample40.xml)]
7. Stisknutím klávesy **F5** spusťte aplikaci a Nahrajte obrázek pro daný produkt. Všimněte si ID vláken, kde byl kód spuštěn a dokončen, se může lišit. Důvodem je to, že asynchronní úlohy jsou spouštěny v samostatném vlákně z fondu vláken ASP.NET. Po dokončení úlohy ASP.NET vloží úlohu zpátky do fronty a přiřadí libovolné dostupné vlákna.

    ![Asynchronní stahování obrazu](whats-new-in-web-forms-in-aspnet-45/_static/image24.png "Asynchronní stahování obrazu")

    *Asynchronní stahování obrazu*

> [!NOTE]
> Kromě toho můžete tuto aplikaci nasadit do Azure podle [dodatku B: publikování aplikace ASP.NET MVC 4 pomocí nasazení webu](#AppendixB).

---

<a id="Summary"></a>
## <a name="summary"></a>Souhrn

V této praktické laboratorní laboratoři jsme vyřešili a ukázali následující koncepty:

- Použití výrazů pro datovou vazbu silně typovaného typu
- Použití nových funkcí vazby modelu ve webových formulářích
- Použití zprostředkovatelů hodnot pro mapování dat stránky na metody kódu na pozadí
- Použití datových poznámek pro ověřování vstupu uživatele
- Využijte nenáročné ověřování na straně klienta pomocí jQuery ve webových formulářích
- Implementace podrobného ověřování žádostí
- Implementace asynchronního zpracování stránky ve webových formulářích

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Příloha A: instalace Visual Studio Express 2012 pro web

**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** . Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.

1. Přejít na [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169). Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;<em>Visual Studio Express 2012 pro web pomocí sady Azure SDK</em>&quot;.
2. Klikněte na **nainstalovat hned**. Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.
3. Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.

    ![Nainstalovat Visual Studio Express](whats-new-in-web-forms-in-aspnet-45/_static/image25.png "Nainstalovat Visual Studio Express")

    *Nainstalovat Visual Studio Express*
4. Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**

    ![Přijetí licenčních podmínek](whats-new-in-web-forms-in-aspnet-45/_static/image26.png)

    *Přijetí licenčních podmínek*
5. Počkejte na dokončení procesu stahování a instalace.

    ![Průběh instalace](whats-new-in-web-forms-in-aspnet-45/_static/image27.png)

    *Průběh instalace*
6. Po dokončení instalace klikněte na **Dokončit**.

    ![Instalace dokončena](whats-new-in-web-forms-in-aspnet-45/_static/image28.png)

    *Instalace dokončena*
7. Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.
8. Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .

    ![Dlaždice VS Express for Web](whats-new-in-web-forms-in-aspnet-45/_static/image29.png)

    *Dlaždice VS Express for Web*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Příloha B: publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu

V tomto dodatku se dozvíte, jak vytvořit nový web z webu Azure Portal a publikovat aplikaci, kterou jste získali, pomocí testovacího prostředí s využitím funkce publikování Nasazení webu, kterou poskytuje Azure.

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a>Úloha 1 – Vytvoření nového webu z webu Azure Portal

1. Přejít na [portál pro správu Azure](https://manage.windowsazure.com/) a přihlaste se pomocí přihlašovacích údajů Microsoftu přidružených k vašemu předplatnému.

    > [!NOTE]
    > S Azure můžete hostovat 10 ASP.NET webů zdarma a pak škálovat podle nárůstu provozu. [Tady](https://aka.ms/aspnet-hol-azure)se můžete zaregistrovat.

    ![Přihlaste se k Windows Azure Portal](whats-new-in-web-forms-in-aspnet-45/_static/image30.png "Přihlaste se k Windows Azure Portal")

    *Přihlášení k portálu*
2. Na panelu příkazů klikněte na **Nový** .

    ![Vytvoření nového webu](whats-new-in-web-forms-in-aspnet-45/_static/image31.png "Vytvoření nového webu")

    *Vytvoření nového webu*
3. Klikněte na **compute** | **Web**. Pak vyberte možnost **rychlé vytvoření** . Zadejte dostupnou adresu URL pro nový web a klikněte na **vytvořit web**.

    > [!NOTE]
    > Azure je hostitelem webové aplikace běžící v cloudu, kterou můžete řídit a spravovat. Možnost rychle vytvořit umožňuje nasadit dokončenou webovou aplikaci do Azure z webu mimo portál. Nezahrnuje kroky pro nastavení databáze.

    ![Vytvoření nového webu pomocí rychlého vytvoření](whats-new-in-web-forms-in-aspnet-45/_static/image32.png "Vytvoření nového webu pomocí rychlého vytvoření")

    *Vytvoření nového webu pomocí rychlého vytvoření*
4. Počkejte, než se nový **Web** vytvoří.
5. Po vytvoření webu klikněte na odkaz ve sloupci **Adresa URL** . Ověřte, zda nový web funguje.

    ![Procházení na nový web](whats-new-in-web-forms-in-aspnet-45/_static/image33.png "Procházení na nový web")

    *Procházení na nový web*

    ![Běžící Web](whats-new-in-web-forms-in-aspnet-45/_static/image34.png "Běžící Web")

    *Běžící Web*
6. Vraťte se na portál a kliknutím na název webu pod sloupcem **název** zobrazíte stránky pro správu.

    ![Otevření stránek správy webu](whats-new-in-web-forms-in-aspnet-45/_static/image35.png "Otevření stránek správy webu")

    *Otevření stránek správy webu*
7. Na stránce **řídicí panel** klikněte v části **rychlý přehled** na odkaz **Stáhnout profil publikování** .

    > [!NOTE]
    > *Profil publikování* obsahuje všechny informace potřebné k publikování webové aplikace do Azure pro každou povolenou metodu publikace. Profil publikování obsahuje adresy URL, přihlašovací údaje uživatele a databázové řetězce potřebné k připojení a ověření proti jednotlivým koncovým bodům, pro které je povolena metoda publikace. **Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** a **Microsoft Visual Studio 2012** podporují čtení profilů publikování pro automatizaci konfigurace těchto programů pro publikování webových aplikací do Azure.

    ![Stahuje se publikační profil webu.](whats-new-in-web-forms-in-aspnet-45/_static/image36.png "Stahuje se publikační profil webu.")

    *Stahuje se publikační profil webu.*
8. Stáhněte si soubor profilu publikování do známého umístění. V tomto cvičení se dozvíte, jak tento soubor použít k publikování webové aplikace do Azure ze sady Visual Studio.

    ![Ukládání souboru profilu publikování](whats-new-in-web-forms-in-aspnet-45/_static/image37.png "Ukládá se publikační profil.")

    *Ukládání souboru profilu publikování*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>Úloha 2 – Konfigurace databázového serveru

Pokud vaše aplikace využívá SQL Server databází, budete muset vytvořit SQL Database Server. Pokud chcete nasadit jednoduchou aplikaci, která nepoužívá SQL Server, můžete tuto úlohu přeskočit.

1. Pro uložení aplikační databáze budete potřebovat server SQL Database. SQL Database servery můžete zobrazit z předplatného na portálu pro správu Azure na stránce **databáze SQL** | **serverech** | **řídicím panelu serveru**. Pokud nemáte vytvořený server, můžete ho vytvořit pomocí tlačítka **Přidat** na panelu příkazů. Poznamenejte si **název serveru a adresu URL, přihlašovací jméno a heslo správce**, jak je budete používat v dalších úlohách. Databázi ještě nevytvářejte, protože bude vytvořená v pozdější fázi.

    ![Řídicí panel serveru SQL Database](whats-new-in-web-forms-in-aspnet-45/_static/image38.png "Řídicí panel serveru SQL Database")

    *Řídicí panel serveru SQL Database*
2. V další úloze budete testovat připojení k databázi ze sady Visual Studio, z tohoto důvodu je třeba zahrnout místní IP adresu do seznamu **povolených IP adres**serveru. Chcete-li to provést, klikněte na tlačítko **Konfigurovat**, vyberte IP adresu z **aktuální IP adresy klienta** a vložte ji do textového pole **Počáteční IP adresa** a **koncová IP adresa** a klikněte na tlačítko ![přidat-Client-IP-Address-OK-tlačítko](whats-new-in-web-forms-in-aspnet-45/_static/image39.png).

    ![Přidává se IP adresa klienta.](whats-new-in-web-forms-in-aspnet-45/_static/image40.png)

    *Přidává se IP adresa klienta.*
3. Jakmile se **IP adresa klienta** přidá do seznamu povolených IP adres, potvrďte změny kliknutím na **Uložit** .

    ![Potvrdit změny](whats-new-in-web-forms-in-aspnet-45/_static/image41.png)

    *Potvrdit změny*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Úloha 3 – publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu

1. Vraťte se do řešení ASP.NET MVC 4. V **Průzkumník řešení**klikněte pravým tlačítkem myši na webový projekt a vyberte **publikovat**.

    ![Publikování aplikace](whats-new-in-web-forms-in-aspnet-45/_static/image42.png "Publikování aplikace")

    *Publikování webu*
2. Importujte profil publikování, který jste uložili v prvním úkolu.

    ![Import profilu publikování](whats-new-in-web-forms-in-aspnet-45/_static/image43.png "Import profilu publikování")

    *Importuje se publikační profil.*
3. Klikněte na **ověřit připojení**. Po dokončení ověřování klikněte na **Další**.

    > [!NOTE]
    > Ověření je dokončeno, jakmile se zobrazí zelená značka zaškrtnutí vedle tlačítka ověřit připojení.

    ![Ověřování připojení](whats-new-in-web-forms-in-aspnet-45/_static/image44.png "Ověřování připojení")

    *Ověřování připojení*
4. Na stránce **Nastavení** v části **databáze** klikněte na tlačítko vedle textového pole připojení k databázi (tj. **DefaultConnection**).

    ![Konfigurace nasazení webu](whats-new-in-web-forms-in-aspnet-45/_static/image45.png "Konfigurace nasazení webu")

    *Konfigurace nasazení webu*
5. Připojení k databázi nakonfigurujte následujícím způsobem:

   - Do pole **název serveru** zadejte adresu URL serveru SQL Database pomocí předpony *TCP:* .
   - V **uživatelské jméno** zadejte přihlašovací jméno správce serveru.
   - V **heslo** zadejte přihlašovací heslo správce serveru.
   - Zadejte nový název databáze.

     ![Konfigurace cílového připojovacího řetězce](whats-new-in-web-forms-in-aspnet-45/_static/image46.png "Konfigurace cílového připojovacího řetězce")

     *Konfigurace cílového připojovacího řetězce*
6. Pak klikněte na **OK**. Po zobrazení výzvy k vytvoření databáze klikněte na **Ano**.

    ![Vytvoření databáze](whats-new-in-web-forms-in-aspnet-45/_static/image47.png "Vytváří se řetězec databáze.")

    *Vytvoření databáze*
7. Připojovací řetězec, který budete používat pro připojení k SQL Database v Azure, se zobrazí ve výchozím textovém poli připojení. Pak klikněte na tlačítko **Další**.

    ![Připojovací řetězec ukazující na SQL Database](whats-new-in-web-forms-in-aspnet-45/_static/image48.png "Připojovací řetězec ukazující na SQL Database")

    *Připojovací řetězec ukazující na SQL Database*
8. Na stránce **Náhled** klikněte na **publikovat**.

    ![Publikování webové aplikace](whats-new-in-web-forms-in-aspnet-45/_static/image49.png "Publikování webové aplikace")

    *Publikování webové aplikace*
9. Jakmile se proces publikování dokončí, otevře se ve výchozím prohlížeči publikovaný web.

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>Příloha C: používání fragmentů kódu

S fragmenty kódu máte veškerý kód, který potřebujete, na dosah ruky. Dokument testovacího prostředí vás přesně upozorní, když ho můžete používat, jak je znázorněno na následujícím obrázku.

![Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio](whats-new-in-web-forms-in-aspnet-45/_static/image50.png "Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio")

*Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio*

***Přidání fragmentu kódu pomocí klávesnice (C# pouze)***

1. Umístěte kurzor na místo, kam chcete vložit kód.
2. Začněte psát název fragmentu (bez mezer a spojovníků).
3. Sledujte, jak IntelliSense zobrazuje stejné názvy fragmentů kódu.
4. Vyberte správný fragment kódu (nebo pokračujte v psaní, dokud není vybrán celý název tohoto fragmentu kódu).
5. Dvojím stisknutím klávesy TAB vložte fragment kódu do umístění kurzoru.

![Začněte psát název fragmentu.](whats-new-in-web-forms-in-aspnet-45/_static/image51.png "Začněte psát název fragmentu.")

*Začněte psát název fragmentu.*

![Stisknutím klávesy TAB vyberte zvýrazněný fragment.](whats-new-in-web-forms-in-aspnet-45/_static/image52.png "Stisknutím klávesy TAB vyberte zvýrazněný fragment.")

*Stisknutím klávesy TAB vyberte zvýrazněný fragment.*

![Stiskněte znovu TAB a fragment kódu se rozšíří.](whats-new-in-web-forms-in-aspnet-45/_static/image53.png "Stiskněte znovu TAB a fragment kódu se rozšíří.")

*Stiskněte znovu TAB a fragment kódu se rozšíří.*

***Přidání fragmentu kódu pomocí myši (C#, Visual Basic a XML)*** první. Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.

1. Vyberte **Vložit fragment** a potom **Moje fragmenty kódu**.
2. Kliknutím na něj ze seznamu vyberte příslušný fragment kódu.

![Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.](whats-new-in-web-forms-in-aspnet-45/_static/image54.png "Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.")

*Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.*

![Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.](whats-new-in-web-forms-in-aspnet-45/_static/image55.png "Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.")

*Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.*
