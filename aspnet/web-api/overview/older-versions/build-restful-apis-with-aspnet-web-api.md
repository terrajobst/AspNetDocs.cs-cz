---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: Sestavení rozhraní API RESTful s webovým rozhraním API ASP.NET – ASP.NET 4. x
author: rick-anderson
description: 'Praktická cvičení: k vytvoření jednoduchého REST API pro aplikaci Správce kontaktů použijte webové rozhraní API v ASP.NET 4. x.'
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 35b115d6b4f84084e78e429bbb4842670e57bba4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78621812"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a>Sestavení rozhraní API RESTful s webovým rozhraním API ASP.NET

podle [týmu webového Campy](https://twitter.com/webcamps)

> Praktická cvičení: k vytvoření jednoduchého REST API pro aplikaci Správce kontaktů použijte webové rozhraní API v ASP.NET 4. x. Také vytvoříte klienta pro využívání rozhraní API.

V posledních letech se stala jasné, že HTTP není jenom pro obsluhu stránek HTML. Je to také výkonná platforma pro vytváření webových rozhraní API pomocí několik příkazů (GET, POST a tak dále) a několika jednoduchých konceptů, jako jsou *identifikátory URI* a *hlavičky*. Webové rozhraní API ASP.NET je sada komponent, které zjednodušují programování HTTP. Vzhledem k tomu, že je postaven na ASP.NET MVC runtime, webové rozhraní API automaticky zpracovává podrobnosti o přenosech nízké úrovně HTTP. Zároveň webové rozhraní API přirozeně zpřístupňuje model programování HTTP. Jedním z cílů webového rozhraní API je fakt, že se *nejedná o* realitu protokolu HTTP. V důsledku toho je webové rozhraní API flexibilní a snadno širší.  Styl architektury REST byl ověřen jako efektivní způsob, jak využít protokol HTTP, přestože není určitě jediným platným přístupem k HTTP. Správce kontaktů zveřejní RESTful pro výpis, přidávání a odebírání kontaktů, a to i mimo jiné. 

Toto testovací prostředí vyžaduje základní znalost protokolu HTTP, REST a předpokládá, že máte základní znalosti o jazycích HTML, JavaScript a jQuery.
> 
> > [!NOTE]
> > Web ASP.NET má v [https://asp.net/web-api](https://asp.net/web-api)oblast vyhrazenou pro rozhraní Web API pro ASP.NET. Tato lokalita bude dál poskytovat nejnovější informace, ukázky a novinky související s webovým rozhraním API, proto je pravidelně kontrolovat, pokud byste chtěli vytvořit vlastní webová rozhraní API, která jsou dostupná prakticky pro zařízení nebo vývojové rozhraní.
> > 
> > Webové rozhraní API ASP.NET, podobně jako ASP.NET MVC 4, má skvělou flexibilitu v podobě oddělení vrstvy služeb od řadičů, což vám umožní využít několik dostupných rozhraní pro vkládání závislostí poměrně snadno. Na webu MSDN je dobrá ukázka, která ukazuje, jak používat Ninject pro vkládání závislostí v projektu webového rozhraní API ASP.NET, který si můžete stáhnout [tady](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7).
> 
> 
> Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici na adrese [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).

<a id="Objectives"></a>
### <a name="objectives"></a>Cíle

V této praktické laboratorní laboratoři se dozvíte, jak:

- Implementace webového rozhraní API RESTful
- Volání rozhraní API z klienta HTML

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Předpoklady

Následující postup je nutný k dokončení tohoto praktického laboratorního prostředí:

- [Microsoft Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) nebo nejvyšší (pokyny k instalaci najdete v [příloze B](#AppendixB) ).

<a id="Setup"></a>
### <a name="setup"></a>Nastavení

**Instalace fragmentů kódu**

Pro usnadnění práce je většina kódu, který budete spravovat v tomto testovacím prostředí, k dispozici jako fragmenty kódu sady Visual Studio. Chcete-li nainstalovat fragmenty kódu, spusťte soubor **.\Source\Setup\CodeSnippets.vsi** .

Pokud nejste obeznámeni s fragmentem Visual Studio Code a chcete se dozvědět, jak je používat, můžete odkazovat na přílohu z tohoto dokumentu &quot;[příloze A: používání fragmentů kódu](#AppendixA)&quot;.

<a id="Exercises"></a>
## <a name="exercises"></a>Cvičení

Tato praktická cvičení zahrnuje následující cvičení:

1. [Cvičení 1: Vytvoření webového rozhraní API jen pro čtení](#Exercise1)
2. [Cvičení 2: Vytvoření webového rozhraní API pro čtení i zápis](#Exercise2)
3. [Cvičení 3: využívání webového rozhraní API z klienta HTML](#Exercise3)

> [!NOTE]
> Každé cvičení doprovází **koncovou** složku obsahující výsledné řešení, které byste měli získat po dokončení cvičení. Pokud potřebujete další nápovědu k práci prostřednictvím cvičení, můžete toto řešení použít jako vodítko.

Odhadovaný čas dokončení tohoto testovacího prostředí: **60 minut**.

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a>Cvičení 1: Vytvoření webového rozhraní API jen pro čtení

V tomto cvičení budete implementovat metody GET jen pro čtení pro správce kontaktů.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a>Úloha 1 – Vytvoření projektu rozhraní API

V této úloze použijete nové šablony webového projektu ASP.NET k vytvoření webové aplikace webového rozhraní API.

1. Spusťte **Visual Studio 2012 Express for Web**. to uděláte tak, že přejdete na **Start** a zadáte **vs Express for Web** a pak stisknete **ENTER**.
2. V nabídce **soubor** vyberte možnost **Nový projekt**. Vyberte **vizuál C# | Typ webového** projektu ze stromového zobrazení typu projektu a pak vyberte typ projektu **webové aplikace ASP.NET MVC 4** . Nastavte **název** projektu na *ContactManager* a *začněte* **název řešení** a potom klikněte na **OK**.

    ![Vytvoření nového projektu webové aplikace ASP.NET MVC 4,0](build-restful-apis-with-aspnet-web-api/_static/image1.png "Vytvoření nového projektu webové aplikace ASP.NET MVC 4,0")

    *Vytvoření nového projektu webové aplikace ASP.NET MVC 4,0*
3. V dialogovém okně ASP.NET MVC 4 – typ projektu vyberte typ projektu **webové rozhraní API** . Klikněte na tlačítko **OK**.

    ![Určení typu projektu webového rozhraní API](build-restful-apis-with-aspnet-web-api/_static/image2.png "Určení typu projektu webového rozhraní API")

    *Určení typu projektu webového rozhraní API*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a>Úloha 2 – vytvoření řadičů rozhraní API pro správce kontaktů

V této úloze vytvoříte třídy kontroleru, ve kterých se budou nacházet metody rozhraní API.

1. Odstraňte soubor s názvem **ValuesController.cs** v rámci složky **Controllers** z projektu.
2. Klikněte pravým tlačítkem na složku **řadiče** v projektu a vyberte **Přidat | Kontroler** z kontextové nabídky

    ![Přidání nového kontroleru do projektu](build-restful-apis-with-aspnet-web-api/_static/image3.png "Přidání nového kontroleru do projektu")

    *Přidání nového kontroleru do projektu*
3. V dialogovém okně **Přidat řadič** , které se zobrazí, v nabídce šablona vyberte **prázdný kontroler rozhraní API** . Pojmenujte třídu Controller **ContactController**. Pak klikněte na tlačítko **Přidat.**

    ![Použití dialogového okna přidat řadič k vytvoření nového kontroleru webového rozhraní API](build-restful-apis-with-aspnet-web-api/_static/image4.png "Použití dialogového okna přidat řadič k vytvoření nového kontroleru webového rozhraní API")

    *Použití dialogového okna přidat řadič k vytvoření nového kontroleru webového rozhraní API*
4. Do **ContactController**přidejte následující kód.

    (Fragment kódu – *Web API Lab – Ex01-get – metoda rozhraní API*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. Stisknutím klávesy **F5** spusťte ladění aplikace. Měla by se zobrazit výchozí domovská stránka projektu webového rozhraní API.

    ![Výchozí domovská stránka aplikace webového rozhraní API ASP.NET](build-restful-apis-with-aspnet-web-api/_static/image5.png "Výchozí domovská stránka aplikace webového rozhraní API ASP.NET")

    *Výchozí domovská stránka aplikace webového rozhraní API ASP.NET*
6. V okně Internet Exploreru stisknutím klávesy **F12** otevřete okno **vývojářské nástroje** . Klikněte na kartu **síť** a potom kliknutím na tlačítko **Spustit digitalizaci** zahajte zachytávání síťového provozu do okna.

    ![Otevření karty síť a inicializace síťového zachytávání](build-restful-apis-with-aspnet-web-api/_static/image6.png "Otevření karty síť a inicializace síťového zachytávání")

    *Otevření karty síť a inicializace síťového zachytávání*
7. Přidejte adresu URL do panelu Adresa v prohlížeči pomocí **/API/Contact** a stiskněte klávesu ENTER. Podrobnosti o přenosu se zobrazí v okně zachytávání sítě. Všimněte si, že typ MIME odpovědi je **Application/JSON**. Ukazuje, jak výchozí výstupní formát je JSON.

    ![Zobrazení výstupu požadavku webového rozhraní API v zobrazení sítě](build-restful-apis-with-aspnet-web-api/_static/image7.png "Zobrazení výstupu požadavku webového rozhraní API v zobrazení sítě")

    *Zobrazení výstupu požadavku webového rozhraní API v zobrazení sítě*

    > [!NOTE]
    > Výchozí chování aplikace Internet Explorer 10 v tomto okamžiku bude dotázáno, zda by uživatel chtěl uložit nebo otevřít datový proud, který je výsledkem volání webového rozhraní API. Výstupem bude textový soubor, který obsahuje výsledek JSON volání adresy URL webového rozhraní API. Nezavírejte dialog, aby bylo možné sledovat obsah odpovědi prostřednictvím okna nástrojů pro vývojáře.
8. Kliknutím na tlačítko **Přejít k podrobnému zobrazení** zobrazíte další podrobnosti o odezvě tohoto volání rozhraní API.

    ![Přepnout do podrobného zobrazení](build-restful-apis-with-aspnet-web-api/_static/image8.png "Přepnout na zobrazení podrobností")

    *Přepnout do podrobného zobrazení*
9. Chcete-li zobrazit skutečný text odpovědi JSON, klikněte na kartu **tělo odpovědi** .

    ![Zobrazení výstupního textu JSON v monitorování sítě](build-restful-apis-with-aspnet-web-api/_static/image9.png "Zobrazení výstupního textu JSON v monitorování sítě")

    *Zobrazení výstupního textu JSON v monitorování sítě*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a>Úloha 3 – vytvoření modelů kontaktů a rozšíření Správce kontaktů

V této úloze vytvoříte třídy kontroleru, ve kterých se budou nacházet metody rozhraní API.

1. Klikněte pravým tlačítkem na složku **modely** a vyberte **Přidat | Třída...** z místní nabídky.

    ![Přidání nového modelu do webové aplikace](build-restful-apis-with-aspnet-web-api/_static/image10.png "Přidání nového modelu do webové aplikace")

    *Přidání nového modelu do webové aplikace*
2. V dialogovém okně **Přidat novou položku** pojmenujte nový soubor **Contact.cs** a klikněte na **Přidat.**

    ![Vytváření nového souboru třídy kontaktů](build-restful-apis-with-aspnet-web-api/_static/image11.png "Vytváření nového souboru třídy kontaktů")

    *Vytváření nového souboru třídy kontaktů*
3. Do třídy **Contact** přidejte následující zvýrazněný kód.

    (Fragment kódu – *Web API Lab-Ex01-Contact Class*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. Ve třídě **ContactController** vyberte textový **řetězec** v definici metody metody **Get** a zadejte *kontaktní*text. Po zadání slova se na začátku **kontaktu**slov zobrazí indikátor. Buď podržte stisknutou klávesu **CTRL** , stiskněte klávesu tečka (.), nebo klikněte na ikonu pomocí myši. otevře se dialogové okno pomoc v editoru kódu pro automatické vyplňování direktivy **using** pro obor názvů modelů.

    ![Použití pomoci IntelliSense pro deklarace oboru názvů](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    *Použití pomoci IntelliSense pro deklarace oboru názvů*
5. Upravte kód metody **Get** tak, aby vracel pole instancí modelu kontaktu.

    (Fragment kódu – *Web API Lab – Ex01 – vrácení seznamu kontaktů*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. Stiskněte klávesu **F5** pro ladění webové aplikace v prohlížeči. Chcete-li zobrazit změny provedené ve výstupu rozhraní API, proveďte následující kroky.

   1. Po otevření prohlížeče stiskněte klávesu **F12** , pokud vývojářské nástroje ještě nejsou otevřené.
   2. Klikněte na kartu **síť** .
   3. Stiskněte tlačítko **Spustit záznam** .
   4. Přidejte příponu URL **/API/Contact** k adrese URL v adresním řádku a stiskněte klávesu **ENTER** .
   5. Stiskněte tlačítko **Přejít na podrobné zobrazení** .
   6. Vyberte kartu **text odpovědi** . Měl by se zobrazit řetězec JSON představující serializovanou formu pole instancí kontaktů.

      ![Serializovaný výstup pro komplexní volání metody webového rozhraní API](build-restful-apis-with-aspnet-web-api/_static/image13.png "Serializovaný výstup pro komplexní volání metody webového rozhraní API")

      *Serializovaný výstup pro komplexní volání metody webového rozhraní API*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a>Úloha 4 – extrakce funkcí do vrstvy služeb

Tato úloha demonstruje, jak extrahovat funkce do vrstvy služeb, aby vývojáři mohli snadno oddělit své funkce služby od vrstvy kontroleru, a tím umožnit opětovné použití služeb, které skutečně dělají.

1. Vytvořte novou složku v kořenovém adresáři řešení a pojmenujte ji IT **služby**. Provedete to tak, že kliknete pravým tlačítkem na projekt **ContactManager** , vyberete **Přidat** | **novou složku**a pojmenujte IT *služby*.

    ![Vytváření složky služeb](build-restful-apis-with-aspnet-web-api/_static/image14.png "Vytváření složky služeb")

    *Vytváření složky služeb*
2. Klikněte pravým tlačítkem na složku **služby** a vyberte **Přidat | Třída...** z místní nabídky.

    ![Přidání nové třídy do složky služby](build-restful-apis-with-aspnet-web-api/_static/image15.png "Přidání nové třídy do složky služby")

    *Přidání nové třídy do složky služby*
3. Jakmile se zobrazí dialogové okno **Přidat novou položku** , pojmenujte novou třídu **ContactRepository** a klikněte na **Přidat**.

    ![Vytvoření souboru třídy, který bude obsahovat kód pro vrstvu služby úložiště kontaktů](build-restful-apis-with-aspnet-web-api/_static/image16.png "Vytvoření souboru třídy, který bude obsahovat kód pro vrstvu služby úložiště kontaktů")

    *Vytvoření souboru třídy, který bude obsahovat kód pro vrstvu služby úložiště kontaktů*
4. Přidejte do souboru **ContactRepository.cs** direktivu using, aby zahrnovala obor názvů Models.

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. Do souboru **ContactRepository.cs** přidejte následující zvýrazněný kód, který implementuje metodu GetAllContacts.

    (Fragment kódu – *Web API Lab – Ex01 – úložiště kontaktů*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. Otevřete soubor **ContactController.cs** , pokud ještě není otevřený.
7. Do oddílu deklarace oboru názvů souboru přidejte následující příkaz using.

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. Přidejte do třídy **ContactController.cs** následující zvýrazněný kód pro přidání soukromého pole reprezentujícího instanci úložiště, aby zbytek členů třídy mohl využít implementaci služby.

    (Fragment kódu – *Web API Lab-Ex01-Controller kontaktů*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. Změňte metodu **Get** tak, aby používala službu úložiště kontaktů.

    (Fragment kódu – *Web API Lab – Ex01 – vrácení seznamu kontaktů přes úložiště*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. Vložte zarážku do definice metody **Get** **ContactController**.

   ![Přidání zarážek do kontroleru kontaktů](build-restful-apis-with-aspnet-web-api/_static/image17.png "Přidání zarážek do kontroleru kontaktů")

   *Přidání zarážek do kontroleru kontaktů*
11. Stisknutím klávesy **F5** spusťte aplikaci.
12. Po otevření prohlížeče stiskněte klávesu **F12** a otevřete nástroje pro vývojáře.
13. Klikněte na kartu **síť** .
14. Klikněte na tlačítko **Spustit zachycení** .
15. Připojením adresy URL v adresním řádku s příponou **/API/Contact** a stisknutím klávesy **ENTER** NAČTĚTE kontroler rozhraní API.
16. Po zahájení provádění metody **Get** by aplikace Visual Studio 2012 měla provést přerušení.

   ![Přerušení v rámci metody Get](build-restful-apis-with-aspnet-web-api/_static/image18.png "Přerušení v rámci metody Get")

   *Přerušení v rámci metody Get*
17. Pokračujte stisknutím **F5**.
18. Vraťte se do aplikace Internet Explorer, pokud ještě není aktivní. Poznamenejte si okno zachycení sítě.

    ![Zobrazení sítě v aplikaci Internet Explorer zobrazující výsledky volání webového rozhraní API](build-restful-apis-with-aspnet-web-api/_static/image19.png "Zobrazení sítě v aplikaci Internet Explorer zobrazující výsledky volání webového rozhraní API")

    *Zobrazení sítě v aplikaci Internet Explorer zobrazující výsledky volání webového rozhraní API*
19. Klikněte na tlačítko **Přejít k podrobnému zobrazení** .
20. Klikněte na kartu **tělo odpovědi** . Všimněte si výstupu JSON volání rozhraní API a způsobu, jakým představuje dva kontakty načtené vrstvou služby.

    ![Zobrazení výstupu JSON z webového rozhraní API v okně vývojářské nástroje](build-restful-apis-with-aspnet-web-api/_static/image20.png "Zobrazení výstupu JSON z webového rozhraní API v okně vývojářské nástroje")

    *Zobrazení výstupu JSON z webového rozhraní API v okně vývojářské nástroje*

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a>Cvičení 2: Vytvoření webového rozhraní API pro čtení i zápis

V tomto cvičení budete implementovat metody POST a PUT pro správce kontaktů a povolit tak funkce pro úpravy dat.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a>Úloha 1 – otevření projektu webového rozhraní API

V této úloze se připravíte na vylepšení projektu webového rozhraní API vytvořeného v cvičení 1 tak, aby mohl přijímat vstupy uživatele.

1. Spusťte **Visual Studio 2012 Express for Web**. to uděláte tak, že přejdete na **Start** a zadáte **vs Express for Web** a pak stisknete **ENTER**.
2. Otevřete řešení **zahájit** , které se nachází ve složce **source/Ex02-ReadWriteWebAPI/Begin/** Folder. V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
3. Otevřete soubor **Services/ContactRepository. cs** .

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a>Úloha 2 – Přidání funkcí pro trvalost dat do implementace úložiště kontaktů

V této úloze budete rozšiřovat třídu ContactRepository projektu webového rozhraní API vytvořeného v cvičení 1 tak, aby mohl zachovávat a přijímat uživatelské vstupy a nové instance kontaktů.

1. Přidejte následující konstantu do třídy **ContactRepository** , která bude reprezentovat název klíče položky mezipaměti webového serveru později v tomto cvičení.

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. Přidejte do **ContactRepository** konstruktor obsahující následující kód.

    (Fragment kódu – *Web API Lab – Ex02 – konstruktor úložiště kontaktů*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. Upravte kód metody **GetAllContacts** , jak je znázorněno níže.

    (Fragment kódu – *Web API Lab-Ex02-get all Contacts*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > Tento příklad je určen pro demonstrační účely a použije mezipaměť webového serveru jako paměťové médium, aby byly hodnoty k dispozici pro více klientů současně, nikoli pro použití mechanismu úložiště relace nebo životnosti úložiště požadavků. Jedním z nich může být místo mezipaměti webového serveru použití Entity Framework, úložiště XML nebo jakékoli jiné odrůdy.
4. Implementací nové metody s názvem **SaveContact** do třídy **ContactRepository** provedete práci s uložením kontaktu. Metoda **SaveContact** by měla mít jeden parametr **kontaktu** a vracet logickou hodnotu, která označuje úspěch nebo neúspěch.

    (Fragment kódu – *Web API Lab-Ex02-implementace metody SaveContact*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a>Cvičení 3: využívání webového rozhraní API z klienta HTML

V tomto cvičení vytvoříte klienta HTML, který bude volat webové rozhraní API. Tento klient usnadňuje výměnu dat pomocí webového rozhraní API pomocí JavaScriptu a zobrazí výsledky ve webovém prohlížeči pomocí značek HTML.

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a>Úloha 1 – Změna zobrazení indexu, která poskytuje grafické uživatelské rozhraní pro zobrazování kontaktů

V této úloze upravíte výchozí zobrazení indexu webové aplikace tak, aby podporovalo požadavek zobrazení seznamu existujících kontaktů v prohlížeči HTML.

1. Otevřete **Visual Studio 2012 Express for Web** , pokud ještě není otevřený.
2. Otevřete řešení **zahájit** , které se nachází ve složce **source/Ex03-ConsumingWebAPI/Begin/** Folder. V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
3. Otevřete soubor **index. cshtml** umístěný v **zobrazeních nebo v domovské** složce.
4. Nahraďte kód HTML v prvku div **textem** ID, aby vypadal jako následující kód.

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. Přidáním následujícího kódu jazyka JavaScript do dolní části souboru proveďte požadavek HTTP na webové rozhraní API.

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. Otevřete soubor **ContactController.cs** , pokud ještě není otevřený.
7. Umístěte zarážku na metodu **Get** třídy **ContactController** .

    ![Umístění zarážky na metodu Get kontroleru rozhraní API](build-restful-apis-with-aspnet-web-api/_static/image21.png "Umístění zarážky na metodu Get kontroleru rozhraní API")

    *Umístění zarážky na metodu Get kontroleru rozhraní API*
8. Stisknutím klávesy **F5** spusťte projekt. Prohlížeč načte dokument HTML.

    > [!NOTE]
    > Ujistěte se, že procházíte na kořenovou adresu URL vaší aplikace.
9. Jakmile se stránka načte a spustí se JavaScript, zarážka se vykoná a spuštění kódu se v kontroleru zastaví.

    ![Ladění volání webového rozhraní API pomocí VS Express for Web](build-restful-apis-with-aspnet-web-api/_static/image22.png "Ladění volání webového rozhraní API pomocí VS Express for Web")

    *Ladění do volání webového rozhraní API pomocí sady Visual Studio 2012 Express for Web*
10. Chcete-li pokračovat v načítání zobrazení v prohlížeči, odeberte zarážku a stiskněte klávesu **F5** nebo tlačítko **Přejít** na panel nástrojů ladění. Po dokončení volání webového rozhraní API byste měli vidět kontakty vrácené z volání webového rozhraní API zobrazené jako položky seznamu v prohlížeči.

    ![Výsledky volání rozhraní API zobrazeného v prohlížeči jako položky seznamu](build-restful-apis-with-aspnet-web-api/_static/image23.png "Výsledky volání rozhraní API zobrazeného v prohlížeči jako položky seznamu")

    *Výsledky volání rozhraní API zobrazeného v prohlížeči jako položky seznamu*
11. Zastavit ladění.

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a>Úloha 2 – Změna zobrazení indexu pro poskytování uživatelského rozhraní pro vytváření kontaktů

V této úloze budete pokračovat v úpravách zobrazení indexu aplikace MVC. Formulář se přidá do stránky HTML, která zachytí uživatelský vstup a pošle ho do webového rozhraní API a vytvoří nový kontakt. Nová metoda webového rozhraní API se pak vytvoří ke shromáždění data z grafického uživatelského rozhraní.

1. Otevřete soubor **ContactController.cs** .
2. Přidejte novou metodu do třídy Controller s názvem **post** , jak je znázorněno v následujícím kódu.

    (Fragment kódu – *Web API Lab-Ex03-post*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. Otevřete soubor **index. cshtml** v aplikaci Visual Studio, pokud ještě není otevřený.
4. Přidejte kód HTML níže do souboru hned po neuspořádaném seznamu, který jste přidali v předchozím úkolu.

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. Do elementu script v dolní části dokumentu přidejte následující zvýrazněný kód, který bude zpracovávat události kliknutí tlačítkem, které budou odesílat data do webového rozhraní API pomocí volání HTTP POST.

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. V **ContactController.cs**umístěte zarážku na metodu **post** .
7. Stisknutím klávesy **F5** spusťte aplikaci v prohlížeči.
8. Jakmile se stránka načte do prohlížeče, zadejte nové jméno a ID kontaktu a klikněte na tlačítko **Uložit** .

    ![Dokument HTML klienta načtený v prohlížeči](build-restful-apis-with-aspnet-web-api/_static/image24.png "Dokument HTML klienta načtený v prohlížeči")

    *Dokument HTML klienta načtený v prohlížeči*
9. Po přerušení okna ladicího programu v metodě **post** se podíváme na vlastnosti parametru **kontakt** . Hodnoty by se měly shodovat s daty, která jste zadali ve formuláři.

    ![Objekt kontaktu, který se odesílá do webového rozhraní API z klienta](build-restful-apis-with-aspnet-web-api/_static/image25.png "Objekt kontaktu, který se odesílá do webového rozhraní API z klienta")

    *Objekt kontaktu, který se odesílá do webového rozhraní API z klienta*
10. Projděte metodu v ladicím programu, dokud není vytvořena proměnná **odpovědi** . Po kontrole v okně **místní** hodnoty v ladicím programu uvidíte, že byly nastaveny všechny vlastnosti.

   ![Odpověď po vytvoření v ladicím programu](build-restful-apis-with-aspnet-web-api/_static/image26.png "Odpověď po vytvoření v ladicím programu")

   *Odpověď po vytvoření v ladicím programu*
11. Pokud stisknete klávesu **F5** nebo kliknete na **pokračovat** v ladicím programu, požadavek se dokončí. Po přepnutí zpátky do prohlížeče se nový kontakt přidal do seznamu kontaktů uložených implementací **ContactRepository** .

   ![Prohlížeč odráží úspěšné vytvoření nové instance kontaktu.](build-restful-apis-with-aspnet-web-api/_static/image27.png "Prohlížeč odráží úspěšné vytvoření nové instance kontaktu.")

   *Prohlížeč odráží úspěšné vytvoření nové instance kontaktu.*

> [!NOTE]
> Kromě toho můžete tuto aplikaci nasadit do Azure podle [dodatku C: publikování aplikace ASP.NET MVC 4 pomocí nasazení webu](#AppendixC).

---

<a id="Summary"></a>
## <a name="summary"></a>Souhrn

Toto testovací prostředí vás zavedlo k novému webovému rozhraní API ASP.NET a implementaci RESTful webových rozhraní API pomocí rozhraní. Z tohoto místa můžete vytvořit nové úložiště, které usnadňuje Trvalost dat pomocí libovolného počtu mechanismů a kabelů, které jsou v tomto testovacím prostředí k dispozici, a nikoli jednoduchého typu. Webové rozhraní API podporuje řadu dalších funkcí, například povolení komunikace od klientů, kteří nejsou ve formátu HTML, napsaných v jakémkoli jazyce, který podporuje protokoly HTTP a JSON nebo XML. Možnost hostovat webové rozhraní API mimo typickou webovou aplikaci je také možné, stejně jako možnost vytvářet vlastní formáty serializace.

Web ASP.NET má v [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api)oblast vyhrazenou pro rozhraní Web API pro ASP.NET. Tato lokalita bude dál poskytovat nejnovější informace, ukázky a novinky související s webovým rozhraním API, proto je pravidelně kontrolovat, pokud byste chtěli vytvořit vlastní webová rozhraní API, která jsou dostupná prakticky pro zařízení nebo vývojové rozhraní.

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a>Příloha A: používání fragmentů kódu

S fragmenty kódu máte veškerý kód, který potřebujete, na dosah ruky. Dokument testovacího prostředí vás přesně upozorní, když ho můžete používat, jak je znázorněno na následujícím obrázku.

![Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio](build-restful-apis-with-aspnet-web-api/_static/image28.png "Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio")

*Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio*

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a>Přidání fragmentu kódu pomocí klávesnice (C# pouze)

1. Umístěte kurzor na místo, kam chcete vložit kód.
2. Začněte psát název fragmentu (bez mezer a spojovníků).
3. Sledujte, jak IntelliSense zobrazuje stejné názvy fragmentů kódu.
4. Vyberte správný fragment kódu (nebo pokračujte v psaní, dokud není vybrán celý název tohoto fragmentu kódu).
5. Dvojím stisknutím klávesy TAB vložte fragment kódu do umístění kurzoru.

    ![Začněte psát název fragmentu.](build-restful-apis-with-aspnet-web-api/_static/image29.png "Začněte psát název fragmentu.")

    *Začněte psát název fragmentu.*

    ![Stisknutím klávesy TAB vyberte zvýrazněný fragment.](build-restful-apis-with-aspnet-web-api/_static/image30.png "Stisknutím klávesy TAB vyberte zvýrazněný fragment.")

    *Stisknutím klávesy TAB vyberte zvýrazněný fragment.*

    ![Stiskněte znovu TAB a fragment kódu se rozšíří.](build-restful-apis-with-aspnet-web-api/_static/image31.png "Stiskněte znovu TAB a fragment kódu se rozšíří.")

    *Stiskněte znovu TAB a fragment kódu se rozšíří.*

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a>Přidání fragmentu kódu pomocí myši (C#, Visual Basic a XML)

1. Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.
2. Vyberte **Vložit fragment** a potom **Moje fragmenty kódu**.
3. Kliknutím na něj ze seznamu vyberte příslušný fragment kódu.

    ![Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.](build-restful-apis-with-aspnet-web-api/_static/image32.png "Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.")

    *Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.*

    ![Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.](build-restful-apis-with-aspnet-web-api/_static/image33.png "Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.")

    *Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a>Příloha B: instalace Visual Studio Express 2012 pro web

**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** . Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.

1. Přejít na [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169). Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;<em>Visual Studio Express 2012 pro web pomocí sady Azure SDK</em>&quot;.
2. Klikněte na **nainstalovat hned**. Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.
3. Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.

    ![Nainstalovat Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "Nainstalovat Visual Studio Express")

    *Nainstalovat Visual Studio Express*
4. Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**

    ![Přijetí licenčních podmínek](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    *Přijetí licenčních podmínek*
5. Počkejte na dokončení procesu stahování a instalace.

    ![Průběh instalace](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    *Průběh instalace*
6. Po dokončení instalace klikněte na **Dokončit**.

    ![Instalace dokončena](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    *Instalace dokončena*
7. Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.
8. Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .

    ![Dlaždice VS Express for Web](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    *Dlaždice VS Express for Web*

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Příloha C: publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu

V tomto dodatku se dozvíte, jak vytvořit nový web z webu Azure Portal a publikovat aplikaci, kterou jste získali, pomocí testovacího prostředí s využitím funkce publikování Nasazení webu, kterou poskytuje Azure.

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a>Úloha 1 – Vytvoření nového webu z webu Azure Portal

1. Přejít na [portál pro správu Azure](https://manage.windowsazure.com/) a přihlaste se pomocí přihlašovacích údajů Microsoftu přidružených k vašemu předplatnému.

    > [!NOTE]
    > S Azure můžete hostovat 10 ASP.NET webů zdarma a pak škálovat podle nárůstu provozu. [Tady](https://aka.ms/aspnet-hol-azure)se můžete zaregistrovat.

    ![Přihlaste se k Windows Azure Portal](build-restful-apis-with-aspnet-web-api/_static/image39.png "Přihlaste se k Windows Azure Portal")

    *Přihlášení k portálu*
2. Na panelu příkazů klikněte na **Nový** .

    ![Vytvoření nového webu](build-restful-apis-with-aspnet-web-api/_static/image40.png "Vytvoření nového webu")

    *Vytvoření nového webu*
3. Klikněte na **compute** | **Web**. Pak vyberte možnost **rychlé vytvoření** . Zadejte dostupnou adresu URL pro nový web a klikněte na **vytvořit web**.

    > [!NOTE]
    > Azure je hostitelem webové aplikace běžící v cloudu, kterou můžete řídit a spravovat. Možnost rychle vytvořit umožňuje nasadit dokončenou webovou aplikaci do Azure z webu mimo portál. Nezahrnuje kroky pro nastavení databáze.

    ![Vytvoření nového webu pomocí rychlého vytvoření](build-restful-apis-with-aspnet-web-api/_static/image41.png "Vytvoření nového webu pomocí rychlého vytvoření")

    *Vytvoření nového webu pomocí rychlého vytvoření*
4. Počkejte, než se nový **Web** vytvoří.
5. Po vytvoření webu klikněte na odkaz ve sloupci **Adresa URL** . Ověřte, zda nový web funguje.

    ![Procházení na nový web](build-restful-apis-with-aspnet-web-api/_static/image42.png "Procházení na nový web")

    *Procházení na nový web*

    ![Běžící Web](build-restful-apis-with-aspnet-web-api/_static/image43.png "Běžící Web")

    *Běžící Web*
6. Vraťte se na portál a kliknutím na název webu pod sloupcem **název** zobrazíte stránky pro správu.

    ![Otevření stránek správy webu](build-restful-apis-with-aspnet-web-api/_static/image44.png "Otevření stránek správy webu")

    *Otevření stránek správy webu*
7. Na stránce **řídicí panel** klikněte v části **rychlý přehled** na odkaz **Stáhnout profil publikování** .

    > [!NOTE]
    > *Profil publikování* obsahuje všechny informace potřebné k publikování webové aplikace do Azure pro každou povolenou metodu publikování. Profil publikování obsahuje adresy URL, přihlašovací údaje uživatele a databázové řetězce potřebné k připojení a ověření proti jednotlivým koncovým bodům, pro které je povolena metoda publikace. **Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** a **Microsoft Visual Studio 2012** podporují čtení profilů publikování pro automatizaci konfigurace těchto programů pro publikování webových aplikací do Azure.

    ![Stahuje se publikační profil webu.](build-restful-apis-with-aspnet-web-api/_static/image45.png "Stahuje se publikační profil webu.")

    *Stahuje se publikační profil webu.*
8. Stáhněte si soubor profilu publikování do známého umístění. V tomto cvičení se dozvíte, jak tento soubor použít k publikování webové aplikace do Azure ze sady Visual Studio.

    ![Ukládání souboru profilu publikování](build-restful-apis-with-aspnet-web-api/_static/image46.png "Ukládá se publikační profil.")

    *Ukládání souboru profilu publikování*

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>Úloha 2 – Konfigurace databázového serveru

Pokud vaše aplikace využívá SQL Server databází, budete muset vytvořit SQL Database Server. Pokud chcete nasadit jednoduchou aplikaci, která nepoužívá SQL Server, můžete tuto úlohu přeskočit.

1. Pro uložení aplikační databáze budete potřebovat server SQL Database. SQL Database servery můžete zobrazit z předplatného na portálu pro správu Azure na stránce **databáze SQL** | **serverech** | **řídicím panelu serveru**. Pokud nemáte vytvořený server, můžete ho vytvořit pomocí tlačítka **Přidat** na panelu příkazů. Poznamenejte si **název serveru a adresu URL, přihlašovací jméno a heslo správce**, jak je budete používat v dalších úlohách. Databázi ještě nevytvářejte, protože bude vytvořená v pozdější fázi.

    ![Řídicí panel serveru SQL Database](build-restful-apis-with-aspnet-web-api/_static/image47.png "Řídicí panel serveru SQL Database")

    *Řídicí panel serveru SQL Database*
2. V další úloze budete testovat připojení k databázi ze sady Visual Studio, z tohoto důvodu je třeba zahrnout místní IP adresu do seznamu **povolených IP adres**serveru. Chcete-li to provést, klikněte na tlačítko **Konfigurovat**, vyberte IP adresu z **aktuální IP adresy klienta** a vložte ji do textového pole **Počáteční IP adresa** a **koncová IP adresa** a klikněte na tlačítko ![přidat-Client-IP-Address-OK-tlačítko](build-restful-apis-with-aspnet-web-api/_static/image48.png).

    ![Přidává se IP adresa klienta.](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    *Přidává se IP adresa klienta.*
3. Jakmile se **IP adresa klienta** přidá do seznamu povolených IP adres, potvrďte změny kliknutím na **Uložit** .

    ![Potvrdit změny](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    *Potvrdit změny*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Úloha 3 – publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu

1. Vraťte se do řešení ASP.NET MVC 4. V **Průzkumník řešení**klikněte pravým tlačítkem myši na webový projekt a vyberte **publikovat**.

    ![Publikování aplikace](build-restful-apis-with-aspnet-web-api/_static/image51.png "Publikování aplikace")

    *Publikování webu*
2. Importujte profil publikování, který jste uložili v prvním úkolu.

    ![Import profilu publikování](build-restful-apis-with-aspnet-web-api/_static/image52.png "Import profilu publikování")

    *Importuje se publikační profil.*
3. Klikněte na **ověřit připojení**. Po dokončení ověřování klikněte na **Další**.

    > [!NOTE]
    > Ověření je dokončeno, jakmile se zobrazí zelená značka zaškrtnutí vedle tlačítka ověřit připojení.

    ![Ověřování připojení](build-restful-apis-with-aspnet-web-api/_static/image53.png "Ověřování připojení")

    *Ověřování připojení*
4. Na stránce **Nastavení** v části **databáze** klikněte na tlačítko vedle textového pole připojení k databázi (tj. **DefaultConnection**).

    ![Konfigurace nasazení webu](build-restful-apis-with-aspnet-web-api/_static/image54.png "Konfigurace nasazení webu")

    *Konfigurace nasazení webu*
5. Připojení k databázi nakonfigurujte následujícím způsobem:

   - Do pole **název serveru** zadejte adresu URL serveru SQL Database pomocí předpony *TCP:* .
   - V **uživatelské jméno** zadejte přihlašovací jméno správce serveru.
   - V **heslo** zadejte přihlašovací heslo správce serveru.
   - Zadejte nový název databáze, například: *MVC4SampleDB*.

     ![Konfigurace cílového připojovacího řetězce](build-restful-apis-with-aspnet-web-api/_static/image55.png "Konfigurace cílového připojovacího řetězce")

     *Konfigurace cílového připojovacího řetězce*
6. Pak klikněte na **OK**. Po zobrazení výzvy k vytvoření databáze klikněte na **Ano**.

    ![Vytvoření databáze](build-restful-apis-with-aspnet-web-api/_static/image56.png "Vytváří se řetězec databáze.")

    *Vytvoření databáze*
7. Připojovací řetězec, který budete používat pro připojení k SQL Database ve Windows Azure, se zobrazí ve výchozím textovém poli připojení. Pak klikněte na tlačítko **Další**.

    ![Připojovací řetězec ukazující na SQL Database](build-restful-apis-with-aspnet-web-api/_static/image57.png "Připojovací řetězec ukazující na SQL Database")

    *Připojovací řetězec ukazující na SQL Database*
8. Na stránce **Náhled** klikněte na **publikovat**.

    ![Publikování webové aplikace](build-restful-apis-with-aspnet-web-api/_static/image58.png "Publikování webové aplikace")

    *Publikování webové aplikace*
9. Jakmile se proces publikování dokončí, otevře se ve výchozím prohlížeči publikovaný web.

    ![Aplikace byla publikována na platformě Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "Aplikace byla publikována na platformě Windows Azure")

    *Aplikace byla publikována do Azure*
