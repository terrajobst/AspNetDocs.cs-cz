---
title: Neměnnost klíče a nastavení klíče v ASP.NET Core
author: rick-anderson
description: Přečtěte si podrobnosti implementace neměnnost klíče na ochranu dat ASP.NET Core API.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/implementation/key-immutability
ms.openlocfilehash: 7796cb102c0f6f03809704016fd36b28c7a82438
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069397"
---
# <a name="key-immutability-and-key-settings-in-aspnet-core"></a>Neměnnost klíče a nastavení klíče v ASP.NET Core

Po trvalém uložení objektu do záložního úložiště je její znázornění vyřešen navždy. Nová data mohou být přidány do záložního úložiště, ale existující data může nikdy být mutována. Chcete-li zabránit poškození dat je primárním účelem toto chování.

Důsledkem tohoto chování je, že jakmile klíč je zapsán do záložního úložiště, je neměnný. Jeho vytvoření, aktivace a datum vypršení platnosti může nikdy být změněn, i když můžete odvolat pomocí `IKeyManager`. Kromě toho jeho základní informace o vylepšením, materiál hlavního klíče a šifrování na zbývající vlastnosti jsou také neměnné.

Pokud vývojář změní nastavení, která ovlivňuje trvalost klíče, tyto změny se projeví až při příštím klíč generován, buď prostřednictvím explicitní volání konstruktoru `IKeyManager.CreateNewKey` nebo přes data protection systému vlastní [automatické klíč generování](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) chování. Nastavení, které ovlivňují trvalost klíče jsou následující:

* [Výchozí doba platnosti klíče](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)

* [Šifrování klíčů v mechanismu rest](xref:security/data-protection/implementation/key-encryption-at-rest)

* [Vylepšením informací, které obsahuje daný klíč](xref:security/data-protection/configuration/overview#changing-algorithms-with-usecryptographicalgorithms)

Pokud budete potřebovat tato nastavení se rozjíždí dříve než Další automatické klíč času se zajištěním provozu, zvažte explicitní volání konstruktoru `IKeyManager.CreateNewKey` k vytvoření nového klíče. Nezapomeňte zadat datem explicitní aktivace ({nyní + 2 dny} je základním pravidlem na nějakou dobu počkat, změnit na dokončení propagace) a datum vypršení platnosti ve volání.

>[!TIP]
> Všechny aplikace stisknutím úložiště by měl určit stejné nastavení s `IDataProtectionBuilder` metody rozšíření. Vlastnosti trvalý klíč, jinak bude závisí na konkrétní aplikaci, která vyvolá rutiny generování klíčů.
