---
uid: identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
title: 'ASP.NET Identity: použití úložiště MySQL s poskytovatelem EntityFramework MySQL (C#)-ASP.NET 4. x'
author: maumar
description: V tomto kurzu se dozvíte, jak nahradit výchozí mechanismus úložiště dat pro ASP.NET Identity pomocí EntityFramework (poskytovatele klienta SQL) s provid MySQL...
ms.author: riande
ms.date: 12/10/2013
ms.assetid: 15253312-a92c-43ba-908e-b5dacd3d08b8
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
msc.type: authoredcontent
ms.openlocfilehash: e89ed139657c5ce9ddcc56879946c62038919483
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584005"
---
# <a name="aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider-c"></a>ASP.NET Identity: Použití úložiště MySQL zprostředkovatele EntityFramework MySQL (C#)

od [Maurycy Markowski](https://github.com/maumar), [Raquel Soares de Almeida](https://github.com/raquelsa), [Robert blog](https://github.com/rmcmurray)

> V tomto kurzu se dozvíte, jak nahradit výchozí mechanismus úložiště dat pro [**ASP.NET identity**](introduction-to-aspnet-identity.md) pomocí EntityFramework (poskytovatele klienta SQL) s poskytovatelem MySQL.

V tomto kurzu se pokryje následující témata:

- Vytvoření databáze MySQL v Azure
- Vytvoření aplikace MVC pomocí šablony Visual Studio 2013 MVC
- Konfigurace EntityFramework pro práci s poskytovatelem databáze MySQL
- Spuštění aplikace za účelem ověření výsledků

Na konci tohoto kurzu budete mít aplikaci MVC s úložištěm ASP.NET Identity, které používá databázi MySQL hostovanou v Azure.

## <a name="creating-a-mysql-database-instance-on-azure"></a>Vytvoření instance databáze MySQL v Azure

1. Přihlaste se k [webu Azure Portal](https://go.microsoft.com/fwlink/?linkid=529715&amp;clcid=0x409).
2. V dolní části stránky klikněte na **Nový** a vyberte **Uložit**:

    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.png)
3. V průvodci pro **Výběr a přidání** vyberte **ClearDB databáze MySQL**a potom klikněte na šipku **Další** v dolní části snímku:

   [Kliknutím na následující obrázek ho rozbalte. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.png)
4. Nechejte výchozí **bezplatný** plán, změňte **název** na **IdentityMySQLDatabase**, vyberte oblast, která je nejblíže, a potom klikněte na šipku **Další** v dolní části rámečku:

   [Kliknutím na následující obrázek ho rozbalte. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.png)
5. Kliknutím na značku **nákupu** dokončete vytvoření databáze.

   [Kliknutím na následující obrázek ho rozbalte. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.png)
6. Po vytvoření databáze ji můžete spravovat na kartě **Doplňky** na portálu pro správu. Chcete-li načíst informace o připojení pro vaši databázi, klikněte v dolní části stránky na možnost **informace o připojení** :

   [Kliknutím na následující obrázek ho rozbalte. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image10.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image9.png)
7. Zkopírujte připojovací řetězec kliknutím na tlačítko Kopírovat v poli **CONNECTIONSTRING** a uložte ho. Tyto informace použijete později v tomto kurzu pro aplikaci MVC:

   [Kliknutím na následující obrázek ho rozbalte. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image12.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image11.png)

## <a name="creating-an-mvc-application-project"></a>Vytvoření projektu aplikace MVC

K dokončení kroků v této části kurzu budete muset nejdřív nainstalovat [Visual Studio Express 2013 pro web](https://go.microsoft.com/fwlink/?LinkId=299058) nebo [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566). Po instalaci sady Visual Studio použijte následující postup k vytvoření nového projektu aplikace MVC:

1. Otevřete Visual Studio 2103.
2. Na **úvodní** stránce klikněte na **Nový projekt** , nebo můžete kliknout na nabídku **soubor** a potom na **Nový projekt**:

   [Kliknutím na následující obrázek ho rozbalte. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.jpg)
3. Po zobrazení dialogového okna **Nový projekt** rozbalte v seznamu šablon **položku C# vizuál** , potom klikněte na možnost **Web**a vyberte možnost **Webová aplikace ASP.NET**. Pojmenujte projekt **IdentityMySQLDemo** a pak klikněte na **OK**:

   [Kliknutím na následující obrázek ho rozbalte. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image14.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image13.png)
4. V dialogovém okně **Nový projekt ASP.NET** vyberte **MVC** templatewith výchozí možnosti; Tím se jako metoda ověřování nakonfigurují **jednotlivé uživatelské účty** . Klikněte na **OK**:

   [Kliknutím na následující obrázek ho rozbalte. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image16.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image15.png)

## <a name="configure-entityframework-to-work-with-a-mysql-database"></a>Konfigurace EntityFramework pro práci s databází MySQL

### <a name="update-the-entity-framework-assembly-for-your-project"></a>Aktualizace Entity Frameworkho sestavení pro váš projekt

Aplikace MVC, která byla vytvořena pomocí šablony Visual Studio 2013 obsahuje odkaz na balíček [6.0.0 EntityFramework](http://www.nuget.org/packages/EntityFramework) , ale v tomto sestavení byly k dispozici aktualizace, od verze, která obsahuje významná vylepšení výkonu. Chcete-li ve své aplikaci použít nejnovější aktualizace, použijte následující postup.

1. Otevřete projekt MVC v aplikaci Visual Studio.
2. Klikněte na **nástroje**, potom klikněte na **Správce balíčků NuGet**a pak klikněte na **Konzola správce balíčků**:

   [Kliknutím na následující obrázek ho rozbalte. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image18.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image17.png)
3. **Konzola správce balíčků** se zobrazí v dolní části sady Visual Studio. Zadejte &quot;**Update-Package EntityFramework**&quot; a stiskněte klávesu ENTER:

   [Kliknutím na následující obrázek ho rozbalte. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image20.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image19.png)

### <a name="install-the-mysql-provider-for-entityframework"></a>Instalace poskytovatele MySQL pro EntityFramework

Aby se EntityFramework připojení k databázi MySQL, je nutné nainstalovat poskytovatele MySQL. Provedete to tak, že otevřete **konzolu Správce balíčků** a napíšete &quot;**Install-Package MySQL. data. Entity-pre**&quot;a potom stisknete klávesu ENTER.

> [!NOTE]
> Toto je předběžná verze sestavení, která by mohla obsahovat chyby. V produkčním prostředí byste neměli používat předběžnou verzi zprostředkovatele.

[Kliknutím na následující obrázek ho rozbalte.]

[![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image22.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image21.png)

### <a name="making-project-configuration-changes-to-the-webconfig-file-for-your-application"></a>Provádění změn konfigurace projektu v souboru Web. config pro vaši aplikaci

V této části nakonfigurujete Entity Framework pro použití poskytovatele MySQL, který jste právě nainstalovali, zaregistrujete továrnu poskytovatele MySQL a přidáte do Azure připojovací řetězec.

> [!NOTE]
> Následující příklady obsahují specifickou verzi sestavení pro MySql. data. dll. Pokud se verze sestavení změní, budete muset upravit příslušné konfigurační nastavení se správnou verzí.

1. Otevřete soubor Web. config pro váš projekt v Visual Studio 2013.
2. Vyhledejte následující nastavení konfigurace, které definuje výchozího zprostředkovatele databáze a továrnu pro Entity Framework:

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample1.xml)]
3. Tato nastavení konfigurace nahraďte následujícím nastavením, které nakonfiguruje Entity Framework pro použití poskytovatele MySQL:

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample2.xml)]
4. Vyhledejte část &lt;connectionStrings&gt; a nahraďte ji následujícím kódem, který bude definovat připojovací řetězec pro databázi MySQL hostovanou v Azure (Všimněte si, že hodnota providerName se také změnila z původní):

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample3.xml?highlight=3-4)]

### <a name="adding-custom-migrationhistory-context"></a>Přidání vlastního kontextu MigrationHistory

Entity Framework Code First používá tabulku **MigrationHistory** k udržení přehledu o změnách modelu a k zajištění konzistence mezi schématem databáze a koncepčním schématem. Tato tabulka ale ve výchozím nastavení pro MySQL nefunguje, protože primární klíč je moc velký. Chcete-li tuto situaci napravit, bude nutné zmenšit velikost klíče pro tuto tabulku. Chcete-li tak učinit, proveďte následující kroky:

1. Informace o schématu pro tuto tabulku jsou zachyceny v **HistoryContext**, který lze upravit jako jakékoli jiné **DbContext**. Chcete-li to provést, přidejte do projektu nový soubor třídy s názvem **MySqlHistoryContext.cs** a nahraďte jeho obsah následujícím kódem:

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample4.cs)]
2. Dále bude nutné nakonfigurovat Entity Framework pro použití upraveného **HistoryContext**namísto výchozího. To lze provést pomocí funkcí konfigurace na základě kódu. Provedete to tak, že do svého projektu přidáte nový soubor třídy s názvem **MySqlConfiguration.cs** a nahradíte jeho obsah:

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample5.cs)]

### <a name="creating-a-custom-entityframework-initializer-for-applicationdbcontext"></a>Vytvoření vlastního inicializátoru EntityFramework pro ApplicationDbContext

Poskytovatel MySQL, který je vybraný v tomto kurzu, v současné době nepodporuje Entity Framework migrace, takže budete muset použít inicializátory modelu, aby se mohli připojit k databázi. Vzhledem k tomu, že tento kurz používá instanci MySQL v Azure, budete muset vytvořit vlastní inicializátor Entity Framework.

> [!NOTE]
> Tento krok není nutný, pokud se připojujete k instanci SQL Server v Azure nebo používáte databázi, která je hostovaná místně.

Chcete-li vytvořit vlastní inicializátor Entity Framework pro MySQL, použijte následující postup:

1. Přidejte do projektu nový soubor třídy s názvem **MySqlInitializer.cs** a nahraďte jeho obsah následujícím kódem:

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample6.cs?highlight=23)]
2. Otevřete soubor **IdentityModels.cs** pro váš projekt, který je umístěn v adresáři **modelů** , a nahraďte jeho obsah následujícím způsobem:

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample7.cs)]

## <a name="running-the-application-and-verifying-the-database"></a>Spuštění aplikace a ověření databáze

Po dokončení kroků v předchozích částech byste měli otestovat databázi. Chcete-li tak učinit, proveďte následující kroky:

1. Stisknutím **kombinace kláves CTRL + F5** Sestavte a spusťte webovou aplikaci.
2. Klikněte na kartu **registr** v horní části stránky:

   [Kliknutím na následující obrázek ho rozbalte. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.jpg)
3. Zadejte nové uživatelské jméno a heslo a potom klikněte na **zaregistrovat**:

   [Kliknutím na následující obrázek ho rozbalte. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image24.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image23.png)
4. V tomto okamžiku se ASP.NET Identity tabulky vytvoří v databázi MySQL a uživatel je zaregistrován a přihlášen do aplikace:

   [Kliknutím na následující obrázek ho rozbalte. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.jpg)

### <a name="installing-mysql-workbench-tool-to-verify-the-data"></a>Probíhá instalace nástroje MySQL Workbench pro ověření dat

1. Instalace nástroje **MySQL Workbench** ze stránky pro [Stažení souborů MySQL](http://dev.mysql.com/downloads/windows/installer/)
2. V Průvodci instalací: karta **Výběr funkce** vyberte **MySQL Workbench** v části **aplikace** .
3. Spusťte aplikaci a přidejte nové připojení pomocí dat připojovacího řetězce z databáze Azure MySQL, kterou jste vytvořili v BEGGING tohoto kurzu.
4. Po navázání připojení zkontrolujte **ASP.NET identity** tabulky vytvořené v **IdentityMySQLDatabase.**
5. Uvidíte, že jsou vytvořeny všechny ASP.NET Identity požadované tabulky, jak je znázorněno na následujícím obrázku:

   [Kliknutím na následující obrázek ho rozbalte. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.jpg)
6. Zkontrolujte, jestli je v tabulce **aspnetusers** třeba vyhledat položky při registraci nových uživatelů.

   [Kliknutím na následující obrázek ho rozbalte. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image26.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image25.png)
