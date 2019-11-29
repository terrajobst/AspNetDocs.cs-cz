---
uid: web-forms/overview/deployment/visual-studio-web-deployment/project-properties
title: 'Nasazení webu ASP.NET pomocí sady Visual Studio: vlastnosti projektu | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která bude Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: ec1cec4c-a75f-47af-a2ba-b1e2f971d24b
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/project-properties
msc.type: authoredcontent
ms.openlocfilehash: b2811791a897c9166f6222c23dddc6921e5267ab
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74614943"
---
# <a name="aspnet-web-deployment-using-visual-studio-project-properties"></a>Nasazení webu ASP.NET pomocí sady Visual Studio: vlastnosti projektu

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která umožňuje Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí sady Visual Studio 2012 nebo Visual Studio 2010. Informace o řadě najdete v [prvním kurzu v řadě](introduction.md).

## <a name="overview"></a>Přehled

Některé možnosti nasazení jsou nakonfigurovány ve vlastnostech projektu, které jsou uloženy v souboru projektu (soubor *. csproj* nebo *. vbproj* ). Ve většině případů jsou výchozí hodnoty těchto nastavení vhodné, ale můžete použít **Vlastnosti projektu** integrované do sady Visual Studio pro práci s těmito nastaveními, pokud je třeba je změnit. V tomto kurzu si prohlédnete nastavení nasazení ve **vlastnostech projektu**. Také vytvoříte zástupný soubor, který způsobí nasazení prázdné složky.

## <a name="configure-deployment-settings-in-the-project-properties-window"></a>Konfigurace nastavení nasazení v okně vlastností projektu

Většina nastavení, která mají vliv na to, co se stane během nasazení, jsou součástí profilu publikování, jak vidíte v následujících kurzech. Několik nastavení, o kterých byste měli vědět, se nachází na kartách **balení a publikování** okna **vlastností projektu** . Tato nastavení jsou určena pro každou konfiguraci sestavení – to znamená, že můžete mít různá nastavení pro sestavení pro vydání, než pro sestavení pro ladění.

V **Průzkumník řešení**klikněte pravým tlačítkem na projekt **ContosoUniversity** , vyberte **vlastnosti**a pak vyberte kartu **balíček/publikovat web** .

![Karta Balení/publikování webu](project-properties/_static/image1.png)

Po zobrazení okna se ve výchozím nastavení zobrazí nastavení pro každou konfiguraci sestavení, která je pro toto řešení aktuálně aktivní. Pokud pole **Konfigurace** neuvádí možnost **aktivní (vydání)** , vyberte **verze** , aby se zobrazila nastavení pro konfiguraci sestavení pro vydání. Nasadíte sestavení vydaných verzí do testovacího i produkčního prostředí.

![Výběr konfigurace sestavení pro vydání](project-properties/_static/image2.png)

Když vyberete možnost **aktivní (vydaná verze)** nebo **vydaná verze** , zobrazí se hodnoty, které jsou platné při nasazení pomocí konfigurace sestavení verze:

- V poli **položky k nasazení** se vybere **pouze soubory potřebné ke spuštění aplikace** . Další možnosti jsou **všechny soubory v tomto projektu** nebo **všechny soubory v této složce projektu**. Když necháte výchozí výběr beze změny, nebudete například nasazovat soubory zdrojového kódu. Toto nastavení je důvod, proč se složky obsahující SQL Server Compact binární soubory měly zahrnout do projektu. Další informace o tomto nastavení najdete v tématu **Proč se nepovedlo nasadit všechny soubory ve složce projektu?** v tématu [Nejčastější dotazy k nasazení projektu webové aplikace ASP.NET](https://msdn.microsoft.com/library/ee942158.aspx).
- Je vybraná možnost **vyloučit vygenerované symboly ladění** . Při použití této konfigurace sestavení nebudete ladit.
- Je vybraná možnost **Zahrnout všechny databáze nakonfigurované na kartě Balení/publikování SQL** . Určuje, zda bude Visual Studio nasazovat databáze i soubory. I když popisek zaškrtávacího políčka zmiňuje kartu **Package/Publishing SQL** , zrušení zaškrtnutí tohoto políčka také zakáže nasazení databáze, které je nakonfigurováno v profilu publikování. Budete to provádět později, takže zaškrtávací políčko musí zůstat zaškrtnuté. Karta **Balení/publikování kódu SQL** se používá pro metodu publikování starší databáze, kterou v těchto kurzech nebudete používat.
- Oddíl **nastavení balíčku pro nasazení webu** neplatí, protože v těchto kurzech používáte publikování jedním kliknutím.

Změnou rozevíracího seznamu **Konfigurace** na ladit zobrazíte výchozí nastavení pro sestavení pro ladění. Hodnoty jsou stejné, s výjimkou **vyloučených vygenerovaných symbolů ladění** je vymazáno, aby bylo možné ladit při nasazení sestavení ladění.

## <a name="make-sure-that-the-elmah-folder-gets-deployed"></a>Ujistěte se, že se nasadí složka knihovny elmah.

Jak jste viděli v předchozím kurzu, [balíček NuGet knihovny elmah](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) poskytuje funkce pro protokolování chyb a vytváření sestav. Ve složce s názvem *knihovny elmah*je v aplikaci Contoso University knihovny elmah nakonfigurovaná tak, aby ukládala podrobnosti o chybách:

![Knihovny elmah složka](project-properties/_static/image3.png)

Běžným požadavkem je vyloučení určitých souborů nebo složek z nasazení. Dalším příkladem může být složka, do které můžou uživatelé nahrávat soubory. Nechcete nasadit soubory protokolu ani nahrané soubory, které byly vytvořeny ve vašem vývojovém prostředí, do produkčního prostředí. A pokud nasazujete aktualizaci do produkčního prostředí, nechcete, aby proces nasazení odstranil soubory, které existují v produkčním prostředí. (V závislosti na nastavení možnosti nasazení, pokud soubor existuje v cílové lokalitě, ale ne ve zdrojové lokalitě při nasazení, Nasazení webu ho odstraní z cílového umístění.)

Jak jste viděli dříve v tomto kurzu, možnost **položky k nasazení** na kartě **balení nebo publikování webu** je nastavena **pouze na soubory potřebné ke spuštění této aplikace**. V důsledku toho nebudou nasazeny soubory protokolu vytvořené nástrojem knihovny elmah ve vývoji, což je to, co chcete udělat. (Aby bylo možné je nasadit, museli by být zahrnuti do projektu a vlastnost **Akce sestavení** by musel být nastavena na **obsah**. Další informace najdete v tématu **Proč se nepovedlo nasadit všechny soubory ve složce projektu?** v tématu [Nejčastější dotazy k nasazení projektu webové aplikace ASP.NET](https://msdn.microsoft.com/library/ee942158.aspx). Nasazení webu však nevytvoří složku v cílové lokalitě, pokud k ní není k dispozici alespoň jeden soubor. Proto do složky přidáte soubor *. txt* , který bude fungovat jako zástupný symbol, aby se složka zkopírovala.

V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku *knihovny elmah* , vyberte možnost **Přidat novou položku**a vytvořte textový soubor s názvem *zástupný text. txt*. Vložte do něj následující text: "Jedná se o zástupný soubor, aby bylo zajištěno, že se složka bude nasazovat". a uložte soubor. To je všechno, co musíte udělat, aby se zajistilo, že Visual Studio nasadí tento soubor a složku, ve které je, protože vlastnost **Akce sestavení** souborů *. txt* je ve výchozím nastavení nastavená na **obsah** .

## <a name="summary"></a>Přehled

Nyní jste dokončili všechny úlohy nastavování nasazení. V dalším kurzu nasadíte web společnosti Contoso University do testovacího prostředí a otestujete ho.

> [!div class="step-by-step"]
> [Předchozí](web-config-transformations.md)
> [Další](deploying-to-iis.md)
