---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application
title: Maximalizace výkonu pomocí Entity Framework 4,0 ve webové aplikaci ASP.NET 4 | Microsoft Docs
author: tdykstra
description: Tato řada kurzů se sestavuje na webové aplikaci Contoso University, která je vytvořená Začínáme pomocí řady kurzů Entity Framework 4,0. I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 4e43455e-dfa1-42db-83cb-c987703f04b5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application
msc.type: authoredcontent
ms.openlocfilehash: 5630200a1ad1d30f6d89b38e15179f15b699fa9f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78545960"
---
# <a name="maximizing-performance-with-the-entity-framework-40-in-an-aspnet-4-web-application"></a>Maximalizace výkonu pomocí Entity Framework 4,0 ve webové aplikaci ASP.NET 4

tím, že [Dykstra](https://github.com/tdykstra)

> Tato řada kurzů se sestavuje na webové aplikaci Contoso University, která je vytvořená [Začínáme pomocí řady kurzů Entity Framework 4,0](https://asp.net/entity-framework/tutorials#Getting%20Started) . Pokud jste nedokončili předchozí kurzy, jako výchozí bod tohoto kurzu si můžete aplikaci, kterou jste vytvořili, [Stáhnout](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) . Můžete si také [Stáhnout aplikaci](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) , která je vytvořená úplnou řadou kurzů. Pokud máte dotazy k kurzům, můžete je publikovat na [fórum ASP.NET Entity Framework](https://forums.asp.net/1227.aspx).

V předchozím kurzu jste viděli, jak zpracovávat konflikty souběžnosti. V tomto kurzu se zobrazuje možnosti pro zlepšení výkonu webové aplikace v ASP.NET, která používá Entity Framework. Naučíte se několik způsobů, jak maximalizovat výkon nebo diagnostikovat problémy s výkonem.

Informace uvedené v následujících částech jsou pravděpodobně užitečné v nejrůznějších scénářích:

- Efektivně načítat související data.
- Spravovat stav zobrazení.

Informace uvedené v následujících částech můžou být užitečné, pokud máte jednotlivé dotazy, které představují problémy s výkonem:

- Použijte možnost `NoTracking` Merge.
- Předem zkompilujte dotazy LINQ.
- Prověřte příkazy dotazu odeslané do databáze.

Informace uvedené v následující části jsou potenciálně užitečné pro aplikace, které mají extrémně velké datové modely:

- Předem vygenerujte zobrazení.

> [!NOTE]
> Výkon webové aplikace je ovlivněn mnoha faktory, včetně toho, co je velikost požadavků a dat odpovědí, rychlost databázových dotazů, počet požadavků, které server může zařadit do fronty a jak je může obsluhovat, a dokonce efektivitou jakýchkoli knihovny klientských skriptů, které můžete používat. Pokud je výkon v aplikaci kritický nebo pokud testování nebo zkušenosti ukazují, že výkon aplikace není uspokojivý, měli byste dodržovat běžný protokol pro vyladění výkonu. Změřte na míru, kde dochází k kritickým bodům výkonu a pak adresovat oblasti, které budou mít největší dopad na celkový výkon aplikace.
> 
> Toto téma se zaměřuje hlavně na způsoby, kterými můžete potenciálně zlepšit výkon specificky Entity Framework v ASP.NET. Návrhy jsou užitečné, pokud určíte, že přístup k datům je jedním z problémů s výkonem ve vaší aplikaci. V případě, že se zde popsané metody nepovažují za &quot;osvědčené postupy&quot; všeobecně – mnohé z nich jsou vhodné pouze ve výjimečných situacích nebo na řešení velmi specifických druhů kritických bodů výkonu.

Chcete-li spustit kurz, spusťte aplikaci Visual Studio a otevřete webovou aplikaci Contoso University, se kterou jste pracovali v předchozím kurzu.

## <a name="efficiently-loading-related-data"></a>Efektivní načítání souvisejících dat

Existuje několik způsobů, jak může Entity Framework načíst související data do navigačních vlastností entity:

- *Opožděné načítání*. Při prvním načtení entity se nenačte související data. Při prvním pokusu o přístup k navigační vlastnosti je však automaticky načtena data potřebná pro tuto vlastnost navigace. Výsledkem je, že se do databáze pošle víc dotazů – jednu pro samotnou entitu a druhou, a to pokaždé, když se musí načíst související data pro danou entitu. 

    [![Image05](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image2.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image1.png)

*Eager načítání*. Když se entita přečte, načtou se spolu s ní související data. To obvykle vede k tomu, že se vytvoří dotaz s jedním spojením, který načte všechna potřebná data. Eager se načítají pomocí metody `Include`, jak už jste v těchto kurzech viděli.

[![Image07](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image4.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image3.png)

- *Explicitní načítání*. To se podobá opožděnému načítání, s tím rozdílem, že explicitně načtete související data v kódu; k tomu nedochází automaticky při přístupu k navigační vlastnosti. Související data načtoute ručně pomocí metody `Load` vlastnosti navigace pro kolekce nebo použijete metodu `Load` vlastnosti reference pro vlastnosti, které obsahují jeden objekt. (Například zavoláte metodu `PersonReference.Load` pro načtení `Person` navigační vlastnosti entity `Department`.)

    [![Image06](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image6.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image5.png)

Vzhledem k tomu, že ihned nezískají hodnoty vlastností, opožděné načítání a explicitní načítání jsou také označovány jako *odložené načítání*.

Opožděné načítání je výchozím chováním kontextu objektu, který byl vygenerován návrhářem. Pokud otevřete soubor *SchoolModel.Designer.cs* , který definuje třídu kontextu objektu, najdete tři metody konstruktoru a každý z nich obsahuje následující příkaz:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample1.cs)]

Obecně platí, že pokud víte, že potřebujete související data pro každou načtenou entitu, Eager načítání nabízí nejlepší výkon, protože jeden dotaz odeslaný do databáze je obvykle efektivnější než samostatné dotazy pro každou načtenou entitu. Na druhé straně platí, že pokud potřebujete přístup k vlastnostem navigace entity jenom zřídka nebo jenom pro malou sadu entit, opožděné načítání nebo explicitní načítání může být efektivnější, protože Eager načítání by načetlo víc dat, než kolik potřebujete.

V rámci webové aplikace může být opožděné načtení poměrně malé hodnoty, protože akce uživatele, které ovlivňují nutnost souvisejících dat, probíhají v prohlížeči, který nemá žádné připojení k kontextu objektu, který stránku vykreslil. Na druhé straně při vázání ovládacího prvku obvykle víte, jaká data potřebujete, a proto je obecně vhodné zvolit Eager načítání nebo odložené načítání na základě toho, co je vhodné v jednotlivých scénářích.

Kromě toho může ovládací prvek DataBound použít objekt entity poté, co je objekt kontextu vyřazen. V takovém případě by se pokus o opožděné načtení vlastnosti navigace nezdařil. Chybová zpráva, kterou obdržíte, je nejasná: &quot;`The ObjectContext instance has been disposed and can no longer be used for operations that require a connection.`&quot;

Ovládací prvek `EntityDataSource` zakáže opožděné načítání ve výchozím nastavení. Pro ovládací prvek `ObjectDataSource`, který používáte pro aktuální kurz (nebo pokud přistupujete ke kontextu objektu z kódu stránky), existuje několik způsobů, jak můžete ve výchozím nastavení zakázat opožděné načítání. Můžete ho zakázat při vytváření instance kontextu objektu. Například můžete přidat následující řádek do metody konstruktoru třídy `SchoolRepository`:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample2.cs)]

Pro společnost Contoso University se nastaví kontext objektu automaticky při opožděném načítání, takže tuto vlastnost nebude nutné nastavovat pokaždé, když je vytvořena instance kontextu.

Otevřete datový model *SchoolModel. edmx* , klikněte na návrhovou plochu a potom v podokně Vlastnosti nastavte vlastnost **opožděné načítání povoleno** na `False`. Uložte a zavřete datový model.

[![Image04](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image8.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image7.png)

## <a name="managing-view-state"></a>Správa stavu zobrazení

Aby byla zajištěna funkčnost aktualizace, musí webová stránka ASP.NET při vykreslování stránky uchovávat hodnoty původních vlastností entity. Během zpracování zpětného volání může ovládací prvek znovu vytvořit původní stav entity a volat metodu `Attach` entity před použitím změn a voláním metody `SaveChanges`. Ve výchozím nastavení ovládací prvky webových formulářů ASP.NET používají pro ukládání původních hodnot stav zobrazení. Stav zobrazení však může ovlivnit výkon, protože je uložen ve skrytých polích, která mohou podstatně zvětšit velikost stránky odesílané do a z prohlížeče.

Techniky pro správu stavu zobrazení nebo alternativy, jako je například stav relace, nejsou jedinečné pro Entity Framework, takže v tomto kurzu se podrobněji nejedná o toto téma. Další informace najdete na odkazech na konci tohoto kurzu.

Verze 4 pro ASP.NET však poskytuje nový způsob práce se stavem zobrazení, kdy každý ASP.NET vývojář webových formulářů by měl znát: vlastnost `ViewStateMode`. Tuto novou vlastnost lze nastavit na úrovni stránky nebo ovládacího prvku a umožňuje zakázat stav zobrazení ve výchozím nastavení pro stránku a povolit ji pouze pro ovládací prvky, které ji potřebují.

Pro aplikace, kde je výkon kritický, je dobrým zvykem vždy zakázat stav zobrazení na úrovni stránky a povolit ho pouze pro ovládací prvky, které to vyžadují. Tato metoda může podstatně snížit velikost stavu zobrazení na stránkách společnosti Contoso University, ale pokud chcete zjistit, jak to funguje, můžete to udělat na stránce *instruktors. aspx* . Tato stránka obsahuje mnoho ovládacích prvků, včetně ovládacího prvku `Label`, který má zakázaný stav zobrazení. Žádný z ovládacích prvků na této stránce ve skutečnosti nemusí mít povolený stav zobrazení. (Vlastnost `DataKeyNames` ovládacího prvku `GridView` určuje stav, který musí být udržován mezi zpětnými odesláními, ale tyto hodnoty jsou uchovávány ve stavu ovládacího prvku, který není ovlivněn vlastností `ViewStateMode`.)

Direktiva `Page` a označení ovládacího prvku `Label` v současné době se podobá následujícímu příkladu:

[!code-aspx[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample3.aspx)]

Proveďte následující změny:

- Přidejte `ViewStateMode="Disabled"` do direktivy `Page`.
- Odeberte `ViewStateMode="Disabled"` z ovládacího prvku `Label`.

Značka se teď podobá následujícímu příkladu:

[!code-aspx[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample4.aspx)]

Stav zobrazení je nyní zakázán pro všechny ovládací prvky. Pokud později přidáte ovládací prvek, který potřebuje použít stav zobrazení, je vše, co je potřeba udělat, zahrnuje atribut `ViewStateMode="Enabled"` pro tento ovládací prvek.

## <a name="using-the-notracking-merge-option"></a>Použití možnosti sloučení NoTracking

Když kontext objektu načítá řádky databáze a vytváří objekty entit, které je reprezentují, ve výchozím nastavení je také sleduje tyto objekty entit pomocí Správce stavu objektu. Tato data sledování fungují jako mezipaměť a používají se při aktualizaci entity. Vzhledem k tomu, že webová aplikace má obvykle krátkodobé instance kontextu objektu, dotazy často vracejí data, která není nutné sledovat, protože kontext objektu, který je čte, bude odstraněn dříve, než se znovu použije nebo aktualizuje kterákoli z entit, které čte.

V Entity Framework můžete určit, zda kontext objektu sleduje objekty entit nastavením *možnosti sloučení*. Možnost sloučení můžete nastavit pro jednotlivé dotazy nebo pro sady entit. Pokud ho nastavíte pro sadu entit, znamená to, že nastavujete výchozí možnost sloučení pro všechny dotazy, které jsou pro danou sadu entit vytvořené.

Pro společnost Contoso University není sledování nutné pro žádné ze sad entit, ke kterým přistupujete z úložiště, takže můžete nastavit možnost Sloučit na `NoTracking` pro tyto sady entit při vytváření instance kontextu objektu ve třídě úložiště. (Všimněte si, že v tomto kurzu nastavení možnosti sloučení nebude mít znatelný vliv na výkon aplikace. Možnost `NoTracking` se může zvýšit výkon jenom v určitých scénářích s vysokým objemem dat.)

Ve složce DAL otevřete soubor *SchoolRepository.cs* a přidejte metodu konstruktoru, která nastaví možnost sloučení pro sady entit, ke kterým má úložiště přístup:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample5.cs)]

## <a name="pre-compiling-linq-queries"></a>Předběžné kompilování dotazů LINQ

Když Entity Framework spustí dotaz Entity SQL během životního cyklu dané `ObjectContext` instance, bude kompilace dotazu nějakou dobu trvat. Výsledek kompilace je uložen do mezipaměti, což znamená, že další spuštění dotazu jsou mnohem rychlejší. Dotazy LINQ následují podobně jako s tím rozdílem, že některé práce potřebné ke kompilaci dotazu se provádí pokaždé, když je dotaz proveden. Jinými slovy, pro dotazy LINQ ve výchozím nastavení nejsou všechny výsledky kompilace ukládány do mezipaměti.

Pokud máte dotaz LINQ, který očekáváte, že opakovaně spouštíte v rámci životního kontextu objektu, můžete napsat kód, který způsobí, že všechny výsledky kompilace budou uloženy do mezipaměti při prvním spuštění dotazu LINQ.

Jako ilustraci to provedete pro dvě `Get` metody ve třídě `SchoolRepository`, jedna z nich nepřijímá žádné parametry (metoda `GetInstructorNames`) a jedna, která vyžaduje parametr (metoda `GetDepartmentsByAdministrator`). Tyto metody, protože jsou nyní ještě nemusejí být kompilovány, protože nejsou dotazy LINQ:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample6.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample7.cs)]

Nicméně, aby bylo možné vyzkoušet zkompilované dotazy, budete pokračovat, jako by byly napsány jako následující dotazy LINQ:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample8.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample9.cs)]

Můžete změnit kód v těchto metodách na to, co je uvedeno výše, a spustit aplikaci, abyste ověřili, že funguje před pokračováním. Následující pokyny se však přímo procházejí při vytváření předem kompilovaných verzí.

Vytvořte soubor třídy ve složce *dal* , pojmenujte ji *SchoolEntities.cs*a stávající kód nahraďte následujícím kódem:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample10.cs)]

Tento kód vytvoří částečnou třídu, která rozšiřuje automaticky generovanou třídu kontextu objektu. Částečná třída obsahuje dva zkompilované dotazy LINQ pomocí metody `Compile` třídy `CompiledQuery`. Vytvoří také metody, které lze použít pro volání dotazů. Uložte a zavřete tento soubor.

Dále v *SchoolRepository.cs*změňte existující `GetInstructorNames` a `GetDepartmentsByAdministrator` metody ve třídě úložiště tak, aby volaly zkompilované dotazy:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample11.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample12.cs)]

Spusťte stránku *oddělení. aspx* a ověřte, zda funguje stejně jako dříve. Metoda `GetInstructorNames` je volána pro naplnění rozevíracího seznamu správce a metoda `GetDepartmentsByAdministrator` je volána, když kliknete na tlačítko **aktualizovat** , aby se ověřilo, že žádný instruktor není správcem více než jednoho oddělení.

[![Image03](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image10.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image9.png)

Předem kompilované dotazy v aplikaci Contoso University jsou pouze k tomu, abyste viděli, jak to udělat, ne, protože by bylo možné měřit výkon. Předkompilace dotazů LINQ umožňuje přidat do kódu úroveň složitosti, takže se ujistěte, že ji provedete pouze pro dotazy, které ve skutečnosti představují kritické body výkonu ve vaší aplikaci.

## <a name="examining-queries-sent-to-the-database"></a>Zkoumání dotazů odeslaných do databáze

Pokud zkoumáte problémy s výkonem, někdy je užitečné znát přesné příkazy SQL, které Entity Framework posílá do databáze. Pokud pracujete s objektem `IQueryable`, jedním ze způsobů, jak to provést, je použít metodu `ToTraceString`.

V *SchoolRepository.cs*změňte kód v metodě `GetDepartmentsByName` tak, aby odpovídal následujícímu příkladu:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample13.cs)]

Proměnná `departments` musí být přetypování na typ `ObjectQuery`, protože metoda `Where` na konci předchozího řádku vytvoří objekt `IQueryable`; bez `Where` metoda přetypování by nebylo nutné.

Nastavte zarážku na řádku `return` a potom v ladicím programu spusťte stránku *oddělení. aspx* . Když zaškrtnete zarážku, prověřte `commandText` proměnnou v okně **místní** hodnoty a použijte Vizualizér textu (zvětšení skla ve sloupci **hodnota** ) a zobrazte její hodnotu v okně **Vizualizér textu** . Můžete zobrazit celý příkaz SQL, který je výsledkem tohoto kódu:

[![Image08](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image12.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image11.png)

Alternativně funkce IntelliTrace v Visual Studio Ultimate poskytuje způsob, jak zobrazit příkazy SQL generované Entity Framework, které nevyžadují změnu kódu nebo dokonce nastavení zarážky.

> [!NOTE]
> Následující postupy můžete provádět pouze v případě, že máte Visual Studio Ultimate.

Obnovte původní kód v metodě `GetDepartmentsByName` a potom v ladicím programu spusťte stránku *oddělení. aspx* .

V aplikaci Visual Studio vyberte nabídku **ladění** , pak **IntelliTrace**a pak **IntelliTrace události**.

[![Image11](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image14.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image13.png)

V okně **IntelliTrace** klikněte na možnost **rozdělit vše**.

[![Image12](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image16.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image15.png)

Okno **IntelliTrace** zobrazí seznam posledních událostí:

[![Image09](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image18.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image17.png)

Klikněte na **ADO.NET** řádek. Rozbalí se, aby se zobrazil text příkazu:

[![Image10](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image20.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image19.png)

Celý textový řetězec příkazu můžete zkopírovat do schránky z okna **místní** hodnoty.

Předpokládejme, že jste pracovali s databází s více tabulkami, relacemi a sloupci, než je jednoduchá databáze `School`. Může se stát, že dotaz, který shromažďuje všechny informace, které potřebujete v jednom `Select` příkazu, který obsahuje více klauzulí `Join`, bude příliš složitý pro efektivní práci. V takovém případě můžete přepnout z Eager načítání na explicitní načítání pro zjednodušení dotazu.

Například zkuste změnit kód v metodě `GetDepartmentsByName` v *SchoolRepository.cs*. V současnosti v této metodě máte dotaz na objekt, který má `Include` metody pro vlastnosti `Person` a `Courses` navigace. Nahraďte příkaz `return` kódem, který provádí explicitní načítání, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample14.cs)]

Spusťte v ladicím programu stránku *departments. aspx* a znovu se vraťte do okna **IntelliTrace** . Teď, když se dřív jednalo o jeden dotaz, se zobrazí dlouhé pořadí.

[![Image13](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image22.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image21.png)

Klikněte na první **ADO.NET** řádek, abyste viděli, co se stalo se složitým dotazem, který jste zobrazili dříve.

[![Image14](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image24.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image23.png)

Dotaz z oddělení se stal jednoduchým `Select` dotazem bez klauzule `Join`, ale následuje samostatné dotazy, které načítají související kurzy a správce, pomocí sady dvou dotazů pro každé oddělení vrácené původním dotazem.

> [!NOTE]
> Pokud necháte povolené opožděné načítání, vzor, který tady vidíte, se stejným dotazem se opakuje mnohokrát, může být výsledkem opožděného načítání. Vzor, který obvykle chcete zabránit, je opožděně načítána související data pro každý řádek primární tabulky. Pokud jste neověřili, že je dotaz typu Single JOIN příliš složitý, aby byl účinný, je obvykle možné v takových případech zvýšit výkon tak, že změníte primární dotaz na použití Eager načítání.

## <a name="pre-generating-views"></a>Předběžná generování zobrazení

Při prvním vytvoření objektu `ObjectContext` v nové doméně aplikace Entity Framework vygeneruje sadu tříd, které používá pro přístup k databázi. Tyto třídy se nazývají *zobrazení*a pokud máte velmi rozsáhlý datový model, generování těchto zobrazení může zpozdit reakci webu na první požadavek na stránku po inicializaci nové domény aplikace. Tuto prodlevu prvního požadavku můžete zkrátit vytvořením zobrazení v době kompilace, nikoli v době běhu.

> [!NOTE]
> Pokud vaše aplikace nemá extrémně velký datový model nebo pokud má velký datový model, ale nemáte obavy o problém s výkonem, který má vliv pouze na první požadavek na stránku po recyklaci služby IIS, můžete tuto část přeskočit. Vytváření zobrazení se neprovádí při každém vytvoření instance objektu `ObjectContext`, protože zobrazení jsou uložena do mezipaměti v doméně aplikace. Proto, pokud nebudete často recyklovat aplikaci ve službě IIS, velmi málo žádostí o stránky by mělo těžit z předem vygenerovaných zobrazení.

Zobrazení můžete předem generovat pomocí nástroje příkazového řádku *EdmGen. exe* nebo pomocí šablony *textové šablony Transformation Toolkit* (T4). V tomto kurzu použijete šablonu T4.

Ve složce *dal* přidejte soubor pomocí šablony **textové šablony** (je pod uzlem **Obecné** v seznamu **nainstalovaných šablon** ) a pojmenujte ho *SchoolModel.views.TT*. Nahraďte existující kód v souboru následujícím kódem:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample15.cs)]

Tento kód generuje zobrazení pro soubor *. edmx* , který je umístěn ve stejné složce jako šablona a který má stejný název jako soubor šablony. Například pokud má soubor šablony název *SchoolModel.views.TT*, bude vyhledán soubor datového modelu s názvem *SchoolModel. edmx*.

Uložte soubor, klikněte pravým tlačítkem na soubor v **Průzkumník řešení** a vyberte **Spustit vlastní nástroj**.

[![Image02](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image26.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image25.png)

Visual Studio vygeneruje soubor kódu, který vytvoří zobrazení s názvem *SchoolModel.views.cs* na základě šablony. (Možná jste si všimli, že se soubor s kódem generuje, i před tím, než vyberete možnost **Spustit vlastní nástroj**, jakmile soubor šablony uložíte.)

[![Image01](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image28.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image27.png)

Nyní můžete spustit aplikaci a ověřit, zda funguje stejně jako dříve.

Další informace o předem vygenerovaných zobrazeních najdete v následujících zdrojích informací:

- [Postupy: předběžné generování zobrazení pro zlepšení výkonu dotazů](https://msdn.microsoft.com/library/bb896240.aspx) na webu MSDN. Vysvětluje, jak použít nástroj příkazového řádku `EdmGen.exe` pro předběžné generování zobrazení.
- [Izolace výkonu s předkompilovanými nebo předem vygenerovanými zobrazeními v Entity Framework 4](https://blogs.msdn.com/b/appfabriccat/archive/2010/08/06/isolating-performance-with-precompiled-pre-generated-views-in-the-entity-framework-4.aspx) na blogu zákaznického týmu s Windows serverem AppFabric.

Tím se dokončí Úvod ke zlepšení výkonu ve webové aplikaci v ASP.NET, která používá Entity Framework. Další informace najdete v následujících zdrojích:

- [Požadavky na výkon (Entity Framework)](https://msdn.microsoft.com/library/cc853327.aspx) na webu MSDN.
- [Příspěvky související s výkonem na blogu týmu Entity Framework](https://blogs.msdn.com/b/adonet/archive/tags/performance/).
- [Možnosti sloučení EF a zkompilované dotazy](https://blogs.msdn.com/b/dsimmons/archive/2010/01/12/ef-merge-options-and-compiled-queries.aspx) Blogový příspěvek, který vysvětluje neočekávané chování kompilovaných dotazů a možností sloučení, například `NoTracking`. Pokud máte v úmyslu použít zkompilované dotazy nebo manipulovat s nastaveními možností sloučení v aplikaci, přečtěte si toto první.
- [Příspěvky týkající se Entity Framework na blogu pro zákazníka poradenského týmu pro data a modelování](https://blogs.msdn.com/b/dmcat/archive/tags/entity+framework/). Zahrnuje příspěvky na zkompilované dotazy a použití profileru sady Visual Studio 2010 k odhalení problémů s výkonem.
- [Entity Framework vlákno fóra s radami pro zlepšení výkonu vysoce složitých dotazů](https://social.msdn.microsoft.com/Forums/adodotnetentityframework/thread/ffe8b2ab-c5b5-4331-8988-33a872d0b5f6).
- [ASP.NET doporučení pro správu stavu](https://msdn.microsoft.com/library/z1hkazw7.aspx).
- [Pomocí Entity Framework a prvku ObjectDataSource: vlastní stránkování](http://geekswithblogs.net/Frez/articles/using-the-entity-framework-and-the-objectdatasource-custom-paging.aspx). Blogový příspěvek, který sestaví na aplikaci ContosoUniversity vytvořené v těchto kurzech, a vysvětluje, jak implementovat stránkování na stránce *oddělení. aspx* .

V dalším kurzu se posuzuje některá z důležitých vylepšení Entity Framework, která jsou ve verzi 4 novinkou.

> [!div class="step-by-step"]
> [Předchozí](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)
> [Další](what-s-new-in-the-entity-framework-4.md)
