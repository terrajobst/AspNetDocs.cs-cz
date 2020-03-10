---
uid: whitepapers/ms03-32-issue
title: Po použití aktualizace zabezpečení pro IE | opravit chybu nedostupná aplikace serveru Microsoft Docs
author: rick-anderson
description: Tento dokument popisuje opravu, která řeší problém s aktualizací zabezpečení MS03-32 pro Internet Explorer, která má vliv na aplikace ASP.NET 1,0 běžící na Wi...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 1365eebb-bdf7-4a05-8d18-7f200531be55
msc.legacyurl: /whitepapers/ms03-32-issue
msc.type: content
ms.openlocfilehash: e0b6776cbfe22e341ac7105f03daac5074b480fc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574184"
---
# <a name="fix-for-server-application-unavailable-error-after-applying-security-update-for-ie"></a>Oprava chyby „Serverová aplikace není k dispozici“ po použití aktualizace zabezpečení pro IE

> Tento dokument popisuje opravu, která řeší problém s aktualizací zabezpečení MS03-32 pro Internet Explorer, která má vliv na aplikace ASP.NET 1,0 běžící v systému Windows XP Professional.
> 
> Platí pro ASP.NET 1,0 a Windows XP Professional.

Společnost Microsoft zjistila problém s aktualizací zabezpečení MS03-32 pro Internet Explorer a ASP.NET 1,0 spuštěnou v systému Windows XP. Tuto opravu můžete nainstalovat ručně nebo získat nedávné důležité aktualizace z web Windows Update webu.

K tomuto problému dochází, když po instalaci opravy na počítač se systémem Windows XP všechny požadavky na aplikace ASP.NET spuštěné na místním webovém serveru služby IIS 5,1 vytvoří chybová zpráva oznamující, že "serverová aplikace není k dispozici". Žádosti na vzdálené webové servery nejsou ovlivněny.

Tento problém má vliv jenom na instalace, na kterých běží ASP.NET 1,0 v systému Windows XP. Nemá vliv na počítače se systémem Windows 2000 nebo Windows Server 2003. Nemá to vliv na počítače se systémem Windows XP s nainstalovanou ASP.NET 1,1.

Upozorňujeme, že **Tento problém není** chybou zabezpečení s ASP.NET. Neotevírá **ani** neumožňuje žádné škodlivé útoky proti ASP.NET aplikaci nebo serveru. Místo toho je to čistě funkční chyba způsobená samotnou opravou.

Pracujeme na trvalém řešení tohoto problému. Do té doby můžete jako alternativní řešení problému spustit následující dávkový soubor. Dávkový soubor provede následující akce:

1. Zastaví služby IIS a ASP.NET State.
2. Odstraní a znovu vytvoří účet ASPNET se známým dočasným heslem.
3. Používá příkaz Windows `runas` ke spuštění spustitelného souboru, který vytvoří uživatelský profil ASPNET.
4. Znovu zaregistruje ASP.NET. Tím se vytvoří nové náhodné heslo pro účet a použije se výchozí nastavení řízení přístupu ASP.NET.
5. Restartuje službu IIS.

Dávkový soubor obsahuje pevně zakódované dočasné heslo "<strong>1pass\@Word</strong>", který budete při spuštění dávkového souboru vyzváni k zadání příkazu runas. Po dokončení příkazu runas se heslo účtu ASPNET znovu vytvoří se silnou náhodnou hodnotou. Všimněte si, že dávkový soubor může selhat, pokud heslo pevně zakódované nesplňuje požadavky na složitost hesla ve vašem prostředí. V takovém případě ji můžete změnit na jinou hodnotu, která je vhodná pro vaše prostředí.

*> [!IMPORTANT]* Pokud jste přidali vlastní nastavení řízení přístupu nebo oprávnění účtu databáze pro účet ASPNET, bude nutné po dokončení tohoto dávkového souboru znovu vytvořit. Důvodem je to, že při opětovném vytvoření účtu se zobrazí nový identifikátor zabezpečení (SID).

*> [!IMPORTANT]* Pokud spouštíte pracovní proces ASP.NET s vlastním účtem, který je jiný než účet ASPNET, neměli byste tento dávkový soubor spouštět. Místo toho byste se měli interaktivně přihlašovat nebo použít příkaz runas s tímto účtem, který vytvoří pro tento účet profil uživatele.

Dávkový soubor je součástí archivního archivu níže. Pokud ho chcete použít:

1. Musíte být spuštěni jako účet s oprávněními správce.
2. [Stažení a otevření samorozbalovacího spustitelného souboru](ms03-32-issue/_static/fixup1.exe)
3. Extrahujte obsah do c:\
4. Vyberte spustit... v nabídce Start zadejte `cmd.exe`
5. Do okna Otevřít příkaz zadejte `c:\fixup.cmd`.
6. Po zobrazení výzvy zadejte jako heslo <strong>1pass\@Word</strong> .
7. Pokud máte dříve vlastní nastavení řízení přístupu nebo oprávnění účtu databáze pro účet ASPNET, budete muset znovu použít tato nastavení.

Mnoho omluv za nepříjemnosti, které to způsobilo. Budeme publikovat další informace, jakmile budou k dispozici.

Následující tabulka podrobně popisuje platformy a verze, na které se tento problém týká.

| .NET Framework | Platforma | Ovlivněn |
| --- | --- | --- |
| Verze 1,0 | Windows 2000 Professional | Ne |
| Verze 1,0 | Windows 2000 Server | Ne |
| Verze 1,0 | Windows XP Professional | Ano |
| Verze 1,0 | Windows Server 2003 | Ne |
| Verze 1,0 | Windows XP Home s Cassini | Ne |
| Verze 1,1 | Windows 2000 Professional | Ne |
| Verze 1,1 | Windows 2000 Server | Ne |
| Verze 1,1 | Windows XP Professional | Ne |
| Verze 1,1 | Windows Server 2003 | Ne |
| Verze 1,1 | Windows XP Home s Cassini | Ne |

S pozdravem   
 Tým ASP.NET
