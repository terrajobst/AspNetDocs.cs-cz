---
ms.openlocfilehash: 56ee26dd77bb1b678b54b6776741f6547889fa08
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072613"
---
<a name="1140--2015-06-30"></a>1.14.0 / 2015-06-30
==================

## <a name="core"></a>Jádro
  * Odebrat nepoužité removeAttrs – metoda
  * Nahraďte regulární výraz pro adresu url – metoda
  * Odebrat chybný parametr adresy url v $.ajax, přepíše $.extend
  * Správně zpracovat tlačítka pro odeslání vnořené Storno
  * Oprava odsazení
  * Refaktorovat attributeRules a dataRules sdílet noramlizer
  * Metoda dataRules se převést hodnotu na číslo pro číselné vstupy
  * Aktualizovat adresu url metodu povolit pro protokol relativní adresy URL
  * Odebrat nepoužívané .format zástupný symbol $
  * Použít jQuery 1.7 a vyšší zapnuto/vypnuto, přidejte destroy – metoda
  * Kompatibilita aplikaci Internet Explorer 8 změnil .indexOf na $.inArray
  * Přetypování NaN hodnoty atributů, které mají nedefinovaný Opera Mini
  * Zastavit oříznutí hodnotu uvnitř požadovanou metodu
  * Použití: zakázáno selektor tak, aby odpovídaly zakázané elementy
  * Vyloučit některé kláves, aby se zabránilo opětovném pole
  * Není prohledána celá modelu DOM pro přepínač/zaškrtne políčko elementy
  * Vyvolat lepší chyby pro chybný pravidlo metody
  * Oprava čísla chyby ověření
  * Opravte odkaz na whatwg specifikace
  * Neplatný element fokus při ověřování vlastní sadu vstupů
  * Při použití metody vlastní zvýraznění resetování styly – element
  * Řídicí znak dolaru v id chyby
  * Vrátit "Ignorovat jen pro čtení, stejně jako pole zakázáno."
  * Aktualizovat odkaz v komentáři pro algoritmus luhnovým algoritmem

## <a name="additionals"></a>Additionals
  * Aktualizovat dateITA problém adresu časové pásmo
  * Oprava metodu rozšíření k pouze období – metoda
  * Oprava přijmout metodu tak, aby odpovídaly pouze období
  * Metoda čas aktualizace umožňující latence v řádu hodin
  * Chybný zkouška spotřebního pro notEqualTo – metoda
  * Přidat notEqualTo – metoda
  * Použijte odkaz na správnou jQuery prostřednictvím `$`
  * Odebrat zbytečné regulární výraz kontroly v metodě iban
  * Brazilský CPF číslo

## <a name="localization"></a>Lokalizace
  * Update messages_tr.js
  * Update messages_sr_lat.js
  * Přidání Perú Španělština (ES PE)
  * Přidání Gruzínština (ქართული, ge)
  * Oprava překlep v Katalánština překladu
  * Zlepšení překlad Finština (fi)
  * Přidat národní prostředí Arménština (hy_AM)
  * Rozšíření italština (it) překlad metodou měny
  * Přidat bn_BD národní prostředí
  * Aktualizovat zh národního prostředí
  * Odebrat znakem tečky na konci italské zprávy

<a name="1131--2014-10-14"></a>1.13.1 / 2014-10-14
==================

## <a name="core"></a>Jádro
  * Povolit 0 jako hodnota autoCreateRanges
  * Použít nastavení pro všechny prvky validationTargetFor ignorovat
  * Hodnota v metodách minimální/maximální/rangelength není trim
  * Před použitím jako výběr v errorsFor řídicí id nebo název
  * Explicitní výchozí nastavení pro možnost focusCleanup
  * Opravte nesprávné regexp pro describedby předávaný
  * Ignorovat jen pro čtení, jakož i zakázané pole
  * Zlepšení id uvozovací znaky, úložiště id v describedby uvozeny řídicími znaky.
  * Používat návratovou hodnotu submitHandler povolit nebo zakázat odeslání formuláře

## <a name="additionals"></a>Additionals
  * Přidat postalcodeBR – metoda
  * Pokud parametr je řetězec opravit vzor – metoda


<a name="1130--2014-07-01"></a>1.13.0 / 2014-07-01
==================

## <a name="all"></a>Všechny
* Přidat modul plug-in UMD obálky

## <a name="core"></a>Jádro
* Respektujeme bez chyb aria-describedby a prázdný skryté chyby
* Zlepšení dateISO RegExp
* Přidání přepínačů/zaškrtne políčko delegovat událost click
* Použití aria-describedby pro elementy bez popisku
* Registrovat focusin, focusout a keyup také na přepínač/zaškrtávací políčko
* Oprava normalizace pro hodnotu atributu rangelength
* Metoda elementValue vypořádat s typem aktualizace = "number" pole
* CharAt – použijte místo zápisu pole na řetězce pro podporu IE8(?)

## <a name="localization"></a>Lokalizace
* Oprava sk překlad rangelength – metoda
* Přidejte metody finština
* Oprava ověřovací zpráva číslo GL
* Oprava ES číslo ověřovací zprávu – metoda
* Přidání Galicijština (HK)
* Oprava francouzské zprávy pro minimální a maximální metody

## <a name="additionals"></a>Additionals
* Přidat statesUS – metoda
* Oprava metoda dateITA řešit chyby letního času
* Přidejte metodu perský datum
* Přidat postalCodeCA – metoda
* Přidat postalcodeIT – metoda

<a name="1120--2014-04-01"></a>1.12.0 / 2014-04-01
==================

* Přidat ARIA testování ([3d5658e](https://github.com/jzaefferer/jquery-validation/commit/3d5658e9e4825fab27198c256beed86f0bd12577))
* Přidání zpráv es AR lokalizace. ([7b30beb](https://github.com/jzaefferer/jquery-validation/commit/7b30beb8ebd218c38a55d26a63d529e16035c7a2))
* Přidat chybějící tečky "es" a "es_AR" zprávy. ([a2a653c](https://github.com/jzaefferer/jquery-validation/commit/a2a653cb68926ca034b4b09d742d275db934d040))
* Přidání lokalizace indonéská (ID) ([1d348bd](https://github.com/jzaefferer/jquery-validation/commit/1d348bdcb65807c71da8d0bfc13a97663631cd3a))
* Přidání ověření čísla dokumenty NPOKUD, NIE a španělština CIF ([#830](https://github.com/jzaefferer/jquery-validation/issues/830), [317c20f](https://github.com/jzaefferer/jquery-validation/commit/317c20fa9bb772770bb9b70d46c7081d7cfc6545))
* Přidat aktuálního formuláře do kontextu vzdálený požadavek ajax ([0a18ae6](https://github.com/jzaefferer/jquery-validation/commit/0a18ae65b9b6d877e3d15650a5c2617a9d2b11d5))
* Additionals: Aktualizovat IBAN metodu trim koncové prázdné znaky ([#970](https://github.com/jzaefferer/jquery-validation/issues/970), [347b04a](https://github.com/jzaefferer/jquery-validation/commit/347b04a7d4e798227405246a5de3fc57451d52e1))
* Metoda BIC: Zlepšení regulárního výrazu, {1} vždy je redundantní. Zavře gv-744 ([5cad6b4](https://github.com/jzaefferer/jquery-validation/commit/5cad6b493575e8a9a82470d17e0900c881130873))
* Bower: Přidání Bower.json pro registrační balíček ([e86ccb0](https://github.com/jzaefferer/jquery-validation/commit/e86ccb06e301613172d472cf15dd4011ff71b398))
* Změní dolar odkazy na "jQuery" kompatibility s jQuery.noConflict. Zavře gv-754 ([2049afe](https://github.com/jzaefferer/jquery-validation/commit/2049afe46c1be7b3b89b1d9f0690f5bebf4fbf68))
* Jádro: Chyba položka seznamu, přidejte pole "method" ([89a15c7](https://github.com/jzaefferer/jquery-validation/commit/89a15c7a4b17fa2caaf4ff817f09b04c094c3884))
* Jádro: Přidání podpory pro obecné zprávy přes data msg atribut ([5bebaa5](https://github.com/jzaefferer/jquery-validation/commit/5bebaa5c55c73f457c0e0181ec4e3b0c409e2a9d))
* Jádro: Povolit atributy, které mají mít nulovou hodnotu (např. min = '0') ([#854](https://github.com/jzaefferer/jquery-validation/issues/854), [9dc0d1d](https://github.com/jzaefferer/jquery-validation/commit/9dc0d1dd946b2c6178991fb16df0223c76162579))
* Jádro: Zakázat zastaralé $.format ([#755](https://github.com/jzaefferer/jquery-validation/issues/755), [bf3b350](https://github.com/jzaefferer/jquery-validation/commit/bf3b3509140ea8ab5d83d3ec58fd9f1d7822efc5))
* Jádro: Podpora víc tříd chyby opravit ([c1f0baf](https://github.com/jzaefferer/jquery-validation/commit/c1f0baf36c21ca175bbc05fb9345e5b44b094821))
* Jádro: Ignorovat události na prvcích ignorované ([#700](https://github.com/jzaefferer/jquery-validation/issues/700), [a864211](https://github.com/jzaefferer/jquery-validation/commit/a86421131ea69786ee9e0d23a68a54a7658ccdbf))
* Jádro: Zlepšení elementValue – metoda ([6c041ed](https://github.com/jzaefferer/jquery-validation/commit/6c041edd21af1425d12d06cdd1e6e32a78263e82))
* Jádro: Ujistěte se, prvky popisovač ignoruje element() správně. ([3f464a8](https://github.com/jzaefferer/jquery-validation/commit/3f464a8da49dbb0e4881ada04165668e4a63cecb))
* Jádro: Přepnout dataRules parsování stylu specifikace W3C HTML5 ([460fd22](https://github.com/jzaefferer/jquery-validation/commit/460fd22b6c84a74c825ce1fa860c0a9da20b56bb))
* Jádro: Aktivovat úspěch na volitelný, ale mají jiné úspěšné validátory ([#851](https://github.com/jzaefferer/jquery-validation/issues/851), [f93e1de](https://github.com/jzaefferer/jquery-validation/commit/f93e1deb48ec8b3a8a54e946a37db2de42d3aa2a))
* Jádro: Použití plain element místo zrušení obálky elementu znovu ([03cd4c9](https://github.com/jzaefferer/jquery-validation/commit/03cd4c93069674db5415a0bf174a5870da47e5d2))
* Core: Ujistěte se, že poslední spuštění vzdálené ([#711](https://github.com/jzaefferer/jquery-validation/issues/711), [ad91b6f](https://github.com/jzaefferer/jquery-validation/commit/ad91b6f388b7fdfb03b74e78554cbab9fd8fca6f))
* Ukázka: Správná volba v ukázce vícedílné zprávy standardu. ([#1025](https://github.com/jzaefferer/jquery-validation/issues/1025), [070edc7](https://github.com/jzaefferer/jquery-validation/commit/070edc7be4de564cb74cfa9ee4e3f40b6b70b76f))
* Opravte $/ jQuery využití v dalších metod. Opravy #839 ([#839](https://github.com/jzaefferer/jquery-validation/issues/839), [59bc899](https://github.com/jzaefferer/jquery-validation/commit/59bc899e4586255a4251903712e813c21d25b3e1))
* Vylepšete překlady čínštině ([1a0bfe3](https://github.com/jzaefferer/jquery-validation/commit/1a0bfe32b16f8912ddb57388882aa880fab04ffe))
* Počáteční implementace vyžaduje ARIA ([bf3cfb2](https://github.com/jzaefferer/jquery-validation/commit/bf3cfb234ede2891d3f7e19df02894797dd7ba5e))
* Lokalizace: Změna přijmout hodnoty do rozšíření aplikace. Opravy #771, gv-793 se zavře. ([#771](https://github.com/jzaefferer/jquery-validation/issues/771), [12edec6](https://github.com/jzaefferer/jquery-validation/commit/12edec66eb30dc7e86756222d455d49b34016f65))
* Zprávy: Přidat islandském lokalizace ([dc88575](https://github.com/jzaefferer/jquery-validation/commit/dc885753c8872044b0eaa1713cecd94c19d4c73d))
* Zprávy: Přidejte chybějící tečky "bg", "fr" a "sr" zpráv. ([adbc636](https://github.com/jzaefferer/jquery-validation/commit/adbc6361c377bf6b74c35df9782479b1115fbad7))
* Zprávy: Create messages_sr_lat.js ([f2f9007](https://github.com/jzaefferer/jquery-validation/commit/f2f90076518014d98495c2a9afb9a35d45d184e6))
* Zprávy: Create messages_tj.js ([de830b3](https://github.com/jzaefferer/jquery-validation/commit/de830b3fd8689a7384656c17565ee92c2878d8a5))
* Zprávy: Oprava sr_lat překladu, přidejte chybějící prostor ([880ba1c](https://github.com/jzaefferer/jquery-validation/commit/880ba1ca545903a41d8c5332fc4038a7e9a580bd))
* Zprávy: Aktualizovat messages_sr.js, opravte chybějící místa ([10313f4](https://github.com/jzaefferer/jquery-validation/commit/10313f418c18ea75f385248468c2d3600f136cfb))
* Metody: Přidat další metodu měny ([1a981b4](https://github.com/jzaefferer/jquery-validation/commit/1a981b440346620964c87ebdd0fa03246348390e))
* Metody: Přidání inteligentní uvozovky k odebrání stripHTML na interpunkční znaménka ([aa0d624](https://github.com/jzaefferer/jquery-validation/commit/aa0d6241c3ea04663edc1e45ed6e6134630bdd2f))
* Metody: Oprava metody dateITA vyhnout chybám léto ([279b932](https://github.com/jzaefferer/jquery-validation/commit/279b932c1267b7238e6652880b7846ba3bbd2084))
* Metody: Lokalizované metody pro Chilské jazykovou verzi (es +/ CL) ([cf36b93](https://github.com/jzaefferer/jquery-validation/commit/cf36b933499e435196d951401221d533a4811810))
* Metody: Aktualizace e-mailu použijte regulární výraz HTML5, odeberte email2 – metoda ([#828](https://github.com/jzaefferer/jquery-validation/issues/828), [dd162ae](https://github.com/jzaefferer/jquery-validation/commit/dd162ae360639f73edd2dcf7a256710b2f5a4e64))
* Metoda vzoru: Oddělovače, odeberte, protože implementace HTML5 těchto buď nezadávejte. ([37992c1](https://github.com/jzaefferer/jquery-validation/commit/37992c1c9e2e0be8b315ccccc2acb74863439d3e))
* Omezení ověření platební karty zahrnout kontrola délky. Zavře gv-772 ([f5f47c5](https://github.com/jzaefferer/jquery-validation/commit/f5f47c5c661da5b0c0c6d59d169e82230928a804))
* Aktualizace messages_ko.js – zavře gv-715 ([5da3085](https://github.com/jzaefferer/jquery-validation/commit/5da3085ff02e0e6ecc955a8bfc3bb9a8d220581b))
* Update messages_pt_BR.js. Zavře gv-782 ([4bf813b](https://github.com/jzaefferer/jquery-validation/commit/4bf813b751ce34fac3c04eaa2e80f75da3461124))
* Aktualizovat phonesUK a mobileUK tak, aby přijímal nové předpony. Zavře gv-750 ([d447b41](https://github.com/jzaefferer/jquery-validation/commit/d447b41b830dee984be21d8281ec7b87a852001d))
* Ověřte devět číslic PSČ. Zavře gv-726 ([165005d](https://github.com/jzaefferer/jquery-validation/commit/165005d4b5780e22d13d13189d107940c622a76f))
* phoneUS: Přidáte N11 vyloučení. Zavře gv-861 ([519bbc6](https://github.com/jzaefferer/jquery-validation/commit/519bbc656bcb26e8aae5166d7b2e000014e0d12a))
* resetForm měli vymazat všechny hodnoty aria neplatné ([4f8a631](https://github.com/jzaefferer/jquery-validation/commit/4f8a631cbe84f496ec66260ada52db2aa0bb3733))
* valid(): Zkontrolujte všechny elementy. Opravy #791 - valid() ověří pouze první prvek (neplatný) ([#791](https://github.com/jzaefferer/jquery-validation/issues/791), [6f26803](https://github.com/jzaefferer/jquery-validation/commit/6f268031afaf4e155424ee74dd11f6c47fbb8553))

<a name="1111--2013-03-22"></a>1.11.1 / 2013-03-22
==================

  * Vrátit také převádění parametrů metody rozsahu na čísla. Zavře gv-702
  * Většina použití PHP nahraďte mockjax obslužné rutiny. Si udělat trochu pořádek ukázku stejně, aktualizovat na novější modul plug-in zadávání maskovány. Zachovat test captcha. ukázka v jazyce PHP. Opravy #662
  * Odstranit vložený kód zvýraznění mléka ukázku. Zobrazit zdroj funguje správně.
  * Ukázka dynamické součty vyřešit oříznutí mezery z hodnoty obsah šablony před předáním konstruktoru jQuery
  * Opravte minimální/maximální ověření. Zavře gv-666. Opravy #648
  * Opravili jsme "zprávy" chystá se zpravidla a způsobí výjimku po aktualizaci prostřednictvím rules("add"). Zavření 670 gv, řeší #624
  * Přidáte lokalizace korejština (ko). Zavře gv-671
  * Vylepšili jsme metodu UK poštovní směrovací číslo k filtrování další postcodes neplatný. Zavře #682
  * Aktualizujte messages_sv.js. Zavře #683
  * Změna grunt odkaz na web projektu. Zavře #684
  * Vzdálené metody dolů seznamem, aby se poslední, spustit po všechny metody, která se použije k poli. Opravy #679
  * Popis plugin.json aktualizace, by měl obsahovat slovo "ověřit"
  * Oprava překlepů
  * Opravte jQuery zavaděč použít cestu sebe sama. Vnořené ukázky opravy.
  * Aktualizovat grunt qunit contrib chcete používat verzi 1.8 PhantomJS po instalaci přes modul uzel "phantomjs.
  * Ujistěte se, valid() vrátit logickou hodnotu místo 0 nebo 1. Opravy #109 - valid() nevrací logická hodnota

<a name="1110--2013-02-04"></a>1.11.0 / 2013-02-04
==================

  * Odebrat vymazání jako čísla `min`, `max` a `range` pravidla. Opravuje #455. Zavře gv-528.
  * Aktualizace stávající popisky – opravy #430 zavře gv-436
  * Oprava $. validator.format, aby se zabránilo interpolace skupiny, kde je alespoň nahrazuje aplikaci Internet Explorer 8 a 9 - bash se shodou. Opravy #614
  * Oprava mimetype regulární výraz
  * Přidat modul plug-in manifestu a aktualizovat hlavičky právě licencí MIT, vyřaďte zbytečné dual licencování (jako je jQuery).
  * Hebrejský zprávy: Odebrané tečky na konci věty - gv-568 opravy
  * Francouzské překlad pro require_from_group ověření. Gv-573 opravy.
  * Povolit skupiny, které se bude pole nebo řetězec - opravy 479 #
  * Odebrané prostory s více typy MIME
  * Oprava některých datum ověření, chyby syntaxe JS.
  * Odebrat podporu pro metadata modulu plug-in, nahraďte msg pravidlo dat a data-(přidáno v 907467e8) vlastnosti.
  * Přidání sftp jako platný vzor adresy url
  * Přidat Malajština (Moje) lokalizace
  * Aktualizace localization/messages_hu.js
  * Odeberte focusin/focusout kód. Opravy #542 – zahrnutí jquery.validate interfers s focusin a focusout události v IE9
  * Lokalizace: Oprava překlep v finština překladu
  * Oprava ukázku RTM a zobrazit neplatnou ikonu při přechodu z platné zpět na neplatný
  * Oprava předčasné vrácení vzdálené funkce, která zabránila volání jazyka ajax z prováděné v případě, že vstup bylo zadáno příliš rychle. Zajišťuje, že vzdálené ověření vždy ověřuje nejnovější hodnoty.
  * Oprava pro #244 zpět. Opravuje #521 – aktivuje ověření e-mailu se okamžitě, pokud je text v poli.

<a name="1100--2012-09-07"></a>1.10.0 / 2012-09-07
===================

  * Opravit francouzské řetězce pro nowhitespace, phoneUS, phoneUK a mobileUK na základě názorů komunity.
  * Přejmenujte soubory pro language_REGION podle standardní ISO_3166-1 (http://en.wikipedia.org/wiki/ISO_3166-1), pro Tchaj-wan tha jazyk je čínština (zh) a oblasti je Tchaj-wan (tradiční Čínština)
  * Optimalizujte vzorce regulárního výrazu, zvláště pro Velká Británie telefonních čísel.
  * Přidat název jazyka pro každý soubor, přejmenujte kód jazyka podle standard ISO 639 pro estonština, Gruzie, ukrajinština a čínština)http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)
  * Přidání lokalizace Chorvatština (hodina)
  * Byly upravovat existující francouzské překlady a francouzské překlady pro další metody byly přidány.
  * Sloučit změny pro určení vlastní chybové zprávy v atributy dat.
  * Aktualizované UK mobilní telefonní číslo regulární výraz pro nová čísla. Opravy #154
  * Přidáte element do volání úspěch s testem. Opravy #60
  * Oprava regex pro další metodu čas. Opravy #131
  * resetForm nyní vymaže stará previousValue prvků formuláře. Opravy #312
  * Přidání zaškrtávacího políčka testování require_from_group a změněných require_from_group elementValue používat. Opravy #359
  * Opravili jsme elementu dataFilter odpovědi problémů jQuery 1.5.2+. Opravy #405
  * Přidání jQuery Mobile demo. Opravy #249
  * Deoptimize findByName správnost. Opravy #82 - $. validator.prototype.findByName přestane fungovat v aplikace Internet Explorer 7
  * Přidání podpory PSČ USA a testování. Opravy #90
  * Změněné lastElement k lastActive v keyup, přeskočit ověření na kartě nebo prázdný element. Opravy #244
  * Odstraňování z stripHtml odebrané číslo. Opravy #2
  * Oprava neplatný počet na platný vzdálené ověření není platná. Opravy #286
  * Přidání odkazu na file_input ukázku indexu
  * Přesunout staré accept – metoda rozšíření další metody, přidání přijmout nové metody pro zpracování standardního prohlížeče mimetype filtrování. Opravy #287 a nahrazuje #369
  * Zakáže rozostření událost v případě onfocusout je nastavena na hodnotu false. Přidat test.
  * Oprava potíží hodnotu pro přepínací tlačítka a zaškrtávací políčka. Opravy #363
  * Přidání testů pro rangeWords a oprava regulárního výrazu a hranice v metodě. Opravy #308
  * Opravili jsme ukázka tinymce pro tvorbu a přidán odkaz na ukázku stránce. Opravy #382
  * Zpráva změněné lokalizace pro min/max. Opravy #273
  * Přidat pseudo selektor pro vstupní typ textu opravu problému s výchozí prázdný typ atributu. Přidání testů a některé testovací kód. Opravy #217
  * Oprava delegáta chyb pro dynamické součty ukázku. Opravy #51
  * Oprava nesprávná zpráva alfanumerické program pro ověření
  * Odebrat nesprávná false kontrolu na požadovaný atribut
  * požadovaný atribut opravili prohlížeče bez html5. Opravy #301
  * Přidání metody "require_from_group" a "skip_or_fill_minimum"
  * Použijte správnou iso kód pro švédština
  * Soubory aktualizované ukázkové HTML HTML5 doctype
  * Oprava potíží regulární výraz pro desetinná čísla bez počátečních nul. Přidání nové metody testu. Opravy #41
  * Zavést elementValue metodu, která normalizuje jenom řetězcové hodnoty (don't touch pole hodnota vícenásobný výběr). Opravy #116
  * Podpora pro odeslání dynamicky přidaných tlačítek a aktualizované testovacího případu. Používá validateDelegate. Kódu z žádosti o přijetí změn #9
  * Opravte chybný dvojité uvozovky v testovací zařízení
  * Opravte maxWords metoda zahrnout horní mez, není vyloučit. Opravy #284
  * Oprava chyby gramatika v německé rozsah program pro ověření zprávy. Opravy #315
  * Oprava zpracování více názvů tříd pro errorClass možnost. Otestujte Max Lynch. Opravy #280
  * Oprava využití jQuery.format, by měly být $. validator.format. Opravy #329
  * Metody pro 'vše' telefonní čísla Velká Británie + postcodes Velká Británie
  * Metoda vzoru: Převeďte řetězec param RegExp. #223 vydání opravy
  * Gramatika Chyba v souboru německé lokalizace
  * Přidání Estonská lokalizace pro zprávy
  * Zlepšení zpracování na ukázku themerollered popisu tlačítka
  * Přidat typ = "text" na vstupní pole bez atributu typu prosím podmínky
  * Aktualizujte themerollered ukázku, abyste pomocí popisku můžete zobrazit chyby jako překrytí.
  * Aktualizujte themerollered ukázku a použít nejnovější uživatelské rozhraní jQuery (spolu s novější verzí jQuery). Přesuňte kód přibližně pro urychlení načítání stránky.
  * Oprava min chybovou zprávu v japonštině fungovat.
  * Aktualizace modulu plug-in formuláře na nejnovější verzi. Vylepšete ajaxSubmit ukázku.
  * Přetáhněte metody dateDE a numberDE z classRuleSettings zbylé získat přechodem do lokalizované metody
  * Předávání odeslat událost submitHandler zpětného volání
  * Oprava #219 – oprava valid() u elementů s zpětného volání závislostí nebo výraz závislosti.
  * Vylepšení sestavení odebrat dist dir zajistit, že zazipujete pouze aktuální verze

<a name="190"></a>1.9.0
---
* Přidání lokalizace Baskičtina (EU)
* Přidání lokalizace Slovinština (SL)
* Oprava potíží #127 – finština překlady jeden má: místo z;
* Oprava ruština lokalizace, podverze syntaktický problém
* Přidá podporu pro HTML5 vstupní typy, opravy #97
* Vylepšená podpora HTML5 podle nastavení novalidate atributu ve formuláři a čtení atribut typu.
* Oprava showLabel() odebírá všechny třídy z chyba elementu. Odeberte pouze settings.validClass. #151 opravy.
* Přidat do další metody k ověření proti libovolného regulární výrazy "vzor".
* Metoda Vylepšená e-mailu, aby tečky na konci (platné v dokumentu RFC, ale tady nežádoucí). Opravy #143
* Oprava švédská a Norská překlady, je teď přepnout min/max zprávy. Opravy #181
* Oprava #184 - resetForm: by měl zrušit nastavení lastElement
* Oprava #71 – vylepšení stávajících time – metoda a přidejte metodu time12h pro formát času am/pm 12h
* Oprava 177 # – ověření opravy jednoho přepínače nebo zaškrtávacího políčka vstup
* Oprava #189 -: ve výchozím nastavení jsou nyní ignorovány skryté prvky
* Oprava 194 # - vyžaduje jako atribut selže, pokud jQuery > = 1.6 – použití .prop místo .attr
* Oprava 47 #, #39, #32 - čísla povolené platebních karet obsahuje mezery, jakož i pomlčky (mezery jsou běžně zásah uživatele).

<a name="181"></a>1.8.1
---
* Přidání lokalizace Thajština (tou), opravy #85
* Přidání vietnamský (VI) lokalizace díky Ngoc
* Oprava potíží #78. Chyba/platit stylů se vztahuje na všechny přepínače stejné skupiny pro požadované ověřovací.
* Nepoužívejte form.elements, který není podporován jQuery 1.6 zobrazovat. Jeho buggy jako a tím zlepšují přesto (IE6 – 8: form.elements === formuláře).

<a name="180"></a>1.8.0
---
* Vylepšené (NL lokalizace http://plugins.jquery.com/node/14120)
* Přidání Gruzínština (GE) lokalizace díky Avtandil Kikabidze
* Díky Aleksandar Milovac přidání lokalizace Srbština (SR)
* Přidání ipv4 a ipv6 na další metody, díky Natal Ngétal
* Bryan Meyerovich díky přidání lokalizace japonština (Japonsko)
* Přidání lokalizace Katalánština (CA), díky Xavier de Pedro
* Oprava chybějící var příkazů v rámci smyčky for v
* Oprava pro vzdálené ověření, kde máte formátovaných zpráv pokazili)https://github.com/jzaefferer/jquery-validation/issues/11)
* Opravy chyb pro kompatibilitu s jQuery 1.5.1, při zachování zpětné kompatibility

<a name="17"></a>1.7
---
* Přidání lokalizace Litevština (Litva)
* Přidání lokalizace (řečtina (EL)http://plugins.jquery.com/node/12319)
* Přidání (lokalizace Lotyština (LV)http://plugins.jquery.com/node/12349)
* Přidání lokalizace (Hebrejština (HE)http://plugins.jquery.com/node/12039)
* Oprava lokalizace (španělština (ES)http://plugins.jquery.com/node/12696)
* Přidání jQuery UI themerolled ukázku
* Odebrané cmxform.js
* Oprava čtyři chybí středníky ()http://plugins.jquery.com/node/12639)
* Přejmenované metody telefon v dalších methods.js phoneUS
* Přidání phoneUK a mobileUK metody pro další methods.js)http://plugins.jquery.com/node/12359)
* Podrobné Rozšiřte možnosti neměli upravovat více formulářů, při použití na jeden prvek (pravidla – metoda http://plugins.jquery.com/node/12411)
* Opravy chyb pro kompatibilitu s jQuery 1.4.2, při zachování zpětné kompatibility

<a name="16"></a>1.6
---
* Přidání Arabština (AR), portugalština (PTPT), perský (IM), finština (FI) a lokalizace Bulharština (Brazílie)
* Aktualizované lokalizace Švédština (SE) (některé chybějící iso znaků html)
* Oprava $. validator.addMethod správně zpracovat prázdný řetězec oproti undefined argumentu zpráva
* Oprava dvě náhodného globální proměnné
* Vylepšené minimální/maximální/rangeWords (v dalších methods.js) pro odstranění html před počítání; vhodné při počítání slova v editoru richtext
* Přidat lokalizované metody pro Německo, Nizozemsko a PT, odebrání metody dateDE a numberDE (použijte messages_de.js a methods_de.js pomocí metod číslo a datum)
* Oprava vzdálené formuláře odeslat synchronizace, pochvalné hodnocení na Matas Petrikas
* Vylepšené interaktivní vyberte ověření nyní také ověřování na kliknutím (pomocí možností nebo vyberte konzistentní napříč prohlížeči); nefunguje v prohlížeči Safari, které neaktivuje událost click vůbec na vybrané prvky; opravy http://plugins.jquery.com/node/11520
* Aktualizovat na nejnovější modul plug-in formuláře (hodnotu 2,36), opravy http://plugins.jquery.com/node/11487
* Vytvoření vazby k rozostření událost pro equalTo cíl, aby odhlášením při, jejichž cílem změny, opravy http://plugins.jquery.com/node/11450
* Zjednodušené vyberte ověření delegování metody val() jQuery vyberte hodnotu; by mělo vyřešit http://plugins.jquery.com/node/11239
* Pevná výchozí zprávu pro číslice)http://plugins.jquery.com/node/9853)
* Opravili jsme problém se vzdálenou zprávu. v mezipaměti (http://plugins.jquery.com/node/11029 a http://plugins.jquery.com/node/9351)
* Chybí středník opraveny v další methods.js)http://plugins.jquery.com/node/9233)
* Přidání automatické zjišťování substitučních parametrů ve zprávách, eliminuje nutnost k určení formátu funkce)http://plugins.jquery.com/node/11195)
* Opravili jsme problém s: vyplněné /: prázdný poněkud způsobené hrané (http://plugins.jquery.com/node/11144)
* Přidat metodu celé číslo (Další methods.js http://plugins.jquery.com/node/9612)
* Metoda dlouhodobého errorsFor kde pro – atribut obsahuje znaky, které je třeba uvození platný uvnitř (selektor http://plugins.jquery.com/node/9611)

<a name="155"></a>1.5.5
---
* Oprava pro http://plugins.jquery.com/node/8659
* Oprava koncovou čárkou v messages_cs.js

<a name="154"></a>1.5.4
---
* Oprava vzdálené metody chyb)http://plugins.jquery.com/node/8658)

<a name="153"></a>1.5.3
---
* Je opravená chyba souvisí možnost obálky, kde všech nadřazených elementů, které odpovídají obálky – možnost kde vybrané ()http://plugins.jquery.com/node/7624)
* Aktualizované s více částmi ukázku a použijte nejnovější accordion uživatelské rozhraní jQuery
* Přidání metody dateNL a čas additionalMethods.js
* Přidání tradiční čínština (Tchaj-wan, tw) a lokalizaci Kazachstán (KK)
* Přesunout jQuery.format (dříve String.format) do jQuery.validator.format, jQuery.format je zastaralý a už v 1.6 (viz http://code.google.com/p/jquery-utils/issues/detail?id=15 podrobnosti)
* Vyčištění messages_pl.js a messages_ptbr.js (stále definované zprávy pro minimální/maximální/rangeValue, které byly odebrány 1.4)
* Oprava chybný logický operátor v platné modulu plug-in – metody pro více elementů; nyní všechny elementy musí být platná pro výsledek logickou hodnotu true (http://plugins.jquery.com/node/8481)
* Vylepšení $. validator.addMethod: Třetí Nedefinovaná zpráva argument nepřepíše existující (zpráva http://plugins.jquery.com/node/8443)
* Vylepšení submitHandler možnost: Při použití, klikněte na události na odeslání jsou zachyceny tlačítka a tlačítka odesílání je vložen do formuláře před voláním submitHandler a odebrat později; ponechá beze změny (odeslání tlačítka http://plugins.jquery.com/node/7183#comment-3585)
* Možnost přidání validClass výchozí "platné", který přidá tuto třídu pro všechny platné prvky po ověření (http://dev.jquery.com/ticket/2205)
* Přidání creditcardtypes metodu additionalMethods.js, včetně testů (prostřednictvím http://dev.jquery.com/ticket/3635)
* Vylepšené vzdálené metody umožňující serverside zprávy jako řetězec, nebo hodnotu true pro platné, nebo hodnotu false pro neplatný (zpráv na straně klienta, definována pomocí http://dev.jquery.com/ticket/3807)
* Vylepšené přijmout metoda také přijímat Drupal – vizuální styl čárkou oddělený seznam hodnot ()http://plugins.jquery.com/node/8580)

<a name="152"></a>1.5.2
---
* Oprava zprávy v dalších methods.js maxWords, minWords a rangeWords zahrnout volání $.format
* Pevné hodnoty předané do metod, které chcete vyloučit návrat vozíku (\r), nemá stejný jako val() jQuery.
* Přidání lokalizace Slovenština (sk)
* Přidání ukázky pro integraci s kartami uživatelské rozhraní jQuery
* Přidání příkladu vybere seskupení na karty ukázka (viz druhý karty, datum narození pole)

<a name="151"></a>1.5.1
---
* Aktualizovat marketo ukázku nahrazujícím invalidHandler možnost vazba neplatná formuláře události
* Přidání integrace příkladu tinymce pro tvorbu
* Přidání lokalizace Ukrajinština (uživatelský agent)
* Ověření pevné délky pro práci s zkrácená hodnota (regrese z 1.5, ve kterém byl odebrán obecné oříznutí před ověření)
* Různé malé opravy pro kompatibilitu s 1.2.6 a 1.3

<a name="15"></a>1,5
---
* Vylepšené základní Ukázka ověření pole pro potvrzení hesla po změně hesla
* Pevná základní ověření předat nezastřiženými vstupní hodnotu jako první parametr metody ověřování, změnit vyžaduje. přeruší stávající vlastní metodu, která závisí na ořezávání
* Přidání Norština (no), italština (it), maďarština (hu) a lokalizace Rumunština (ro)
* Oprava #3195: Dvě chyby v Švédská lokalizace
* Oprava 3503 #: Rozšířené rules("add") tak, aby přijímal vlastnost zprávy: použijte k určení přidat vlastní zprávy na prvek prostřednictvím pravidel ("Přidat", {zprávy: {vyžaduje: "Required! " } });
* Oprava 3356 #: Regrese z #2908 při použití možností metadat
* Oprava 3370 #: Pomáhá přidání ignoreTitle možností, nastavenou pro přeskočení čtení zpráv z název atributu, aby se zabránilo problémům s panelem nástrojů Google; Výchozí hodnota je false pro kompatibilitu
* Oprava #3516: Aktivační událost tvaru neplatný i v případě, že se jedná o vzdálené ověření
* Přidat možnost invalidHandler jako zástupce pro vazbu ("Neplatná formuláře" function() {})
* Oprava potíží Safari pro načítání ukazatel v ajaxSubmit integrace demo (nejdřív připojit k textu a skrýt)
* Přidání testů pro ověření creditcard a vylepšené výchozí zprávu
* Rozšířeného vzdáleného ověření možnosti pro průchozí $.ajax jako parametr přijímá (řetězce adresy url nebo možnosti, včetně vlastnost adresa url plus všechno ostatní podporuje tento .ajax $)

<a name="14"></a>1.4
---
* Oprava #2931 ověření prvky v pořadí dokumentů a ignorovat typ = image vstupy
* Oprava využití proměnné $ a jQuery, nyní plně kompatibilní s všechny varianty noConflict využití
* Implementovat #2908 povolení vlastních zpráv prostřednictvím třídy metadat ala = "{požadované: hodnotu true, zprávy: {požadované: 'povinné pole.}}", přidali ukázku/custom zprávy – metadat – demo.html
* Odebrat nepoužívané metody minValue (min), hodnota maxValue (max.), prvků rangeValue (prvků rangevalue), (minlength) minLength, maxLength (maxlength) rangeLength (rangelength)
* Oprava regrese #2215: Volání unhighlight pouze pro aktuální prvky, Ne vše, co
* Implementováno #2989 povolení Obrázkové tlačítko pro zrušení ověření
* Opravili jsme chybu, pokud IE nesprávně ověřuje maxlength = 0
* Přidání lokalizace Čeština (cs)
* Resetovat validator.submitted na validator.resetForm() povolení úplné obnovení v případě potřeby
* Oprava 3035 # přeskočí všechny falsy atributy při čtení pravidla (0, nedefinovaný, prázdný řetězec), odebrat součást řešení maxlength (pro uživatele 0)
* Přidání Nizozemská lokalizace (nl) (#3201)

<a name="13"></a>1.3
---
* Oprava události neplatný formulář nyní pouze aktivuje v případě formulář je neplatný
* Přidání Španělština (es), ruština (ru), brazilská portugalština (ptbr), turečtina (tr) a lokalizace Polština (pl)
* Modul plug-in přidání removeAttrs usnadňuje přidávání a odebírání více atributů
* Přidání skupiny možnosti se zobrazí jedna zpráva pro více prvků, pomocí skupin: {arbitraryGroupName: "Názevpole1 Název_pole2 [, fieldNameN"}
* Vylepšené rules() pro přidávání a odebírání (statická) pravidla: pravidla ("Přidání", "– metoda1 [, methodN]" / {method1:param [, method_n:param]}) a pravidel ("remove" ["– metoda1 [, method_n]")
* Vylepšené možnost pravidla, přijímá oddělených mezerami řetězec seznam metod, např. {Datum narození: "required datum"}
* Ověření skupiny pevné zaškrtávacího políčka s pravidly inline: Tak dlouho, dokud pravidla jsou určeny na první prvek, skupině je teď správně ověřují při kliknutí
* Oprava #2473 ignoruje všechna pravidla s parametrem explicitní logickou hodnotu false, např. povinné: false je stejné jako bez zadání vyžaduje vůbec (byla zpracována podle potřeby: true, pokud)
* Oprava 2424 #, s upravenou opravu z #2473: Metody vracející neshodou závislost nepřestávejte další pravidla z právě vyhodnocuje už; stále úspěch se nepoužije pro nepovinné pole
* Oprava adresy url a e-mailová ověření nechcete použít oříznutý hodnoty
* Oprava creditcard ověření tak, aby přijímal pouze číslice a pomlčky ("asdf" není platný creditcard číslo)
* Povolit tlačítko a vstupní prvky pro stornovací tlačítka (prostřednictvím třídy = "Storno")
* Oprava #2215: Oprava zpráva displej tak, aby volání unhighlight jako část zobrazení a skrytí zprávy žádné další visual vedlejší účinky při kontrole, jestli elementu a extrahované validator.checkForm ověření formulář bez sideeffects uživatelského rozhraní
* Rewrote vlastní selektory (: prázdné,: vyplněné,: unchecked) s funkcemi pro kompatibilitu s AIR

<a name="121"></a>1.2.1
-----

* Modul plug-in delegáta jako součást balíčku s modulu plug-in – vždy vyžaduje ověření přesto
* Vylepšení vzdáleného ověření zahrnout součásti z modulu plug-in ajaxQueue správné synchronizace (žádný další modul plugin nezbytné)
* Oprava stopRequest, aby se zabránilo pendingRequest < 0
* Vlastnost přidání jQuery.validator.autoCreateRanges, výchozí hodnota je false, povolit pro převod na rozsah a minlength nebo maxlength rangelength; min/max to v podstatě řeší problém zavedené automaticky vytváření oblastí v 1.2
* Oprava volitelné methods zvýrazněte není nic vůbec Pokud je toto pole prázdné, není tedy aktivovat úspěch
* Povolit hodnotu false a null pro zvýraznění/unhighlight možnosti místo vynucení úkolů-nothing-zpětné volání, i v případě, že není třeba nic zvýrazněny
* Oprava validate() volání bez prvků vybrali, vrací nedefinované namísto vyvolání k chybě
* Vylepšené ukázku metadat nahrazení tříd a atributů k určení pravidel
* Oprava chyby, pokud žádná vlastní zpráva se používá pro vzdálené ověření
* Změny e-mailu a adresy url ověřování tak, aby vyžadovala popisek domény a horního popisku
* Oprava adresy url a e-mailová ověření tak, aby vyžadovala TLD (skutečně potřeba popisek domény); 1.2 verze (TLD je volitelný) je přesunuta do dodatky jako url2 a email2
* Oprava dynamické součty ukázku v aplikacích IE6/7 a vylepšené šablony, použití textarea k uložení víceřádkové šablony a interpolace řetězců
* Příklad form přidané přihlášení s odkaz "Heslo e-mailu", který je volitelné pole pro heslo
* Ukázka rozšířené dynamické součty s příkladem pro dvě pole do jedné zprávy

<a name="12"></a>1.2
---

* Přidání příkladu ověřování AJAX captcha (na základě http://psyrens.com/captcha/)
* Přidání mějte na paměti the mléka demo (díky týmu oprávnění RTM!)
* Přidání služby marketo-demo (Děkujeme Glen Lipka.)
* Přidání podpory pro ověření ajax, viz metoda "vzdálené"; serverside vrací JSON true pro platné prvky, false nebo řetězec pro neplatný řetězec se používá jako zprávy
* Přidání zvýrazňování a unhighlight možnosti ve výchozím nastavení přepíná errorClass u elementu, umožňuje vlastní zvýraznění
* Přidat modul plug-in metoda valid() snadno programové kontroly formulářů a polí, aniž byste museli používat ověřování rozhraní API
* Přidání metody pluginu rules() ke čtení a zápisu pravidel pro daný element (aktuálně jen pro čtení)
* Nahrazené regulární výraz pro e-mailu metoda díky příspěvek Scotta Gonzalez, naleznete v tématu http://projects.scottsplayground.com/email_address_validation/
* Rozdělí události architekturou a nespoléhejte pouze na delegování, vylepšení výkonu i snadné použití pro vývojáře (vyžaduje jquery.delegate.js)
* Přesunuto z vložené do dokumentace ke službě http://docs.jquery.com/Plugins/Validation – včetně interaktivní příklady pro všechny metody
* Odebrané validator.refresh() ověření je nyní zcela dynamický
* Přejmenované minValue min, maxValue do max a prvků rangeValue do rozsahu a ukončení podpory pro předchozí názvy (jenž budou odebrány 1.3)
* Přejmenované minLength minlength, maxLength maxlength a rangeLength k rangelength ukončení podpory pro předchozí názvy (jenž budou odebrány 1.3)
* Přidání funkce sloučení min a max do a být v rozsahu a minlength a maxlength do rangelength
* Přidání podpory pro dynamické pravidlo parametry, povolení k určení funkce jako parametr např. pro minlength volá se při ověřování elementu
* Povolí možnost zadat hodnotu null nebo prázdný řetězec jako zprávu zobrazíte nic (viz ukázka marketo)
* Pravidla renovovaného: Možnost pravidla, metadat, atributů (Nový), a třídy (nové) teď podporuje kombinaci rules() podrobnosti naleznete v tématu

<a name="112"></a>1.1.2
---

* Nahrazené regulární výraz pro adresu URL metoda díky příspěvek Scotta Gonzalez naleznete v tématu http://projects.scottsplayground.com/iri/
* Metoda Vylepšená e-mailu pro lepší zpracování znaků unicode
* Oprava chyby kontejneru skryje, když všechny prvky jsou platné, ne jenom na odeslání formuláře
* Oprava String.format k jQuery.format (Přesun do oboru názvů, jQuery)
* Oprava přijmout metodu tak, aby přijímal rozšíření malá a velká písmena
* Oprava validate() modulu plug-in metoda vždy vrátí jednu instanci (vyhnete vazby události více než jednou) a vytvořte pouze jednu instanci program pro ověření pro daný formulář
* Změnit režim ladění protokolu konzoly z "Chyba" na "varování" úroveň

<a name="111"></a>1.1.1
-----

* Oprava neplatné XHTML, brání Chyba vytváření popisků v Internet Exploreru od jQuery 1.1.4
* Oprava a vylepšené String.format: Globální vyhledávání a nahrazení, lepší zpracování argumentů pole
* Oprava tlačítko Storno zpracování použití objektu validátor pro ukládání stavu místo element formuláře
* Opravili jsme název selektory pro zpracování "pokročilý" názvy, např. obsahující hranaté závorky ("list[]")
* Přidání tlačítka a zakázané prvky, které chcete vyloučit z ověření
* Přesunout obslužné rutiny událostí element ho obnovit, abyste mohli přidat obslužné rutiny pro nové prvky
* Oprava e-mailová ověření umožňující dlouho domén nejvyšší úrovně (např.) ".travel")
* Přesunutý showErrors() z valid() k form()
* Přidání validator.size(): Vrátí počet aktuálních chyb
* Volání submitHandler s validátoru jako obor pro snadnější přístup z jeho metod, např. najít chyby popisky pomocí errorsFor(Element)
* Kompatibilní s jQuery 1.1.x a 1.2.x

<a name="11"></a>1.1
---

* Přidání ověřování na rozostření keyup a klikněte na tlačítko (pro zaškrtávací políčka a radiobutton). Nahrazuje možnost události.
* Oprava resetForm
* Pevné vlastní metody – ukázka

<a name="10"></a>1.0
---

* Vylepšené číslo a numberDE metody ke kontrole správné desetinná čísla s oddělovači
* Pouze prvky, které mají pravidla jsou kontrolovány (jinak úspěch možnost použity na všechny prvky)
* Přidání creditcard číslo – metoda (díky Brian Klug)
* Přidání možnosti Ignorovat, např. Ignorovat: "[@type= skryté]", použití tento výraz k vyloučení prvků k ověření. Výchozí hodnota: žádná, i když odešlete a resetování tlačítka jsou vždy ignorovány.
* Silně rozšířené funkce jako zprávy tím, že poskytuje flexibilní String.format pomocné rutiny
* Přijímají funkce jako zprávy poskytující zpráv vlastního modulu runtime
* Oprava vyloučení prvků bez pravidel z successList
* Pevné vlastní metoda demo, nahradí výstrahy se zpráva zobrazující počet chyb
* Oprava formuláře – odeslání-ochrany před únikem informací při použití submitHandler
* Úplně odebrat závislost na ID prvku, když (Pokud je k dispozici) se stále používají k propojení chyba popisky na vstupy. Můžete dosáhnout použitím pole s {name, zprávy, element} namísto objekt s id: zpráva páry pro interní errorList.
* Přidání podpory pro zadání jednoduchého pravidla jako jednoduchý řetězce, např. "povinné" je ekvivalentní k {požadované: true}
* Funkce: Přidání errorClass do nadřazeného elementu neplatné pole s, což usnadňuje stylu kontejneru popisek či pole nebo popisku pole.
* Funkce: focusCleanup – Pokud je povoleno, zruší errorClass neplatné elementy a pokaždé, když se zaměřuje prvek skryje všechny chybové zprávy.
* Přidat možnost úspěšné, zobrazí pole byla úspěšně ověřena.
* Oprava Opera vyberte potíží (předcházení kolizi atribut)
* Oprava problémů s zaměření skrytých elementů v Internet Exploreru
* Přidání funkce pro přeskočení ověření pro tlačítka pro odeslání dat pomocí třídy "Storno"
* Oprava možné problémy s Google nástrojů podle preferují modulu plug-in možnost zprávy přes atribut nadpisu
* submitHandler je volána, pouze když skutečný odeslat událost byla zpracována, validator.form() vrátí hodnotu false pouze pro neplatný formuláře
* Neplatné elementy jsou nyní zaměřené pouze na odeslání nebo prostřednictvím validator.focusInvalid(), jak se vyhnout všechny problémy s fokus na rozostření
* IE6 Chyba kontejneru rozložení problém je vyřešen.
* Přizpůsobení elementu chyby prostřednictvím errorElement možnost
* Přidání validator.refresh() najít nové vstupů ve formuláři
* Přidání přijmout metoda ověření přípon souborů kontroly
* Vylepšené závislosti funkce přidáním dvou vlastních výrazů: ": prázdné" k výběru elementů s prázdnou hodnotu a: plného k výběru elementů s hodnotou, oba s výjimkou prázdné znaky
* Metoda resetForm() přidán do validátoru: Vynuluje každý prvek formuláře (pomocí modulu plug-in formuláře, pokud je k dispozici), odebere třídy na neplatné elementy a skryje všechny chybové zprávy
* Oprava dokumentace pro validator.showErrors()
* Oprava vytvoření popisku chyba, vždy používali html() místo text(), umožňuje libovolný kód HTML předaný jako zprávy
* Oprava vytvoření popisku pomocí zadané chybové třídy
* Funkce přidání závislosti: Vyžaduje metoda přijímá jako argument řetězec (jQuery výrazy) a funkce
* Vylepšené silně přizpůsobení chybových zpráv: Použijte normální zprávy a zobrazit/skrýt další kontejneru; Zobrazení zpráv zcela nahraďte vlastní mechanismus (při zachování delegovat výchozí obslužnou rutinu; Přizpůsobení umístění generované popisky (namísto výchozí pod – element)
* Dva hlavní chyby opravené v Internet Exploreru (Chyba kontejnerů) a Opera (metadata)
* Upravit metody ověřování tak, aby přijímal prázdná pole jako platný (výjimka: kurz vyžaduje, a také equalTo metod)
* Přejmenovat "min" do "minLength", "max" k "maxLength", "délka" k "rangeLength"
* Přidání "minValue", "maxValue" a "prvků rangeValue"
* Zjednodušené rozhraní API pro podporu různých událostí. Výchozí nastavení, odeslat, je možné zakázat. Pokud libovolná událost není zadána, která je použita na každý prvek (ne celý formulář). Kombinování keyup ověření s odeslání ověřování je teď velice snadné nastavení
* Přidání podpory pro jeden – zpráva podle pravidla při definování zprávy přes nastavení modulu plug-in
* Přidání podpory pro obtékání metadat v některých nadřazeného elementu. Užitečné, pokud metadat se používá pro jiné moduly plug-in příliš.
* Refaktorovaný testy a ukázky: Menší soubory lepší ukázky
* Vylepšené dokumentace: Další příklady pro metody více referenčních texty s vysvětlením, některé základní informace
