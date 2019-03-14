---
ms.openlocfilehash: 939231583679d469d01724cc1a405bd45e46d2c5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57175887"
---
```console
npm run release
```

Tento příkaz provede na straně klienta prostředků ke zpracování při spuštění aplikace. Prostředky jsou umístěné v *wwwroot* složky.

Webpacku dokončit následující úkoly:

* Vymazat obsah *wwwroot* adresáře.
* Převést TypeScript pro JavaScript&mdash;tento proces se označuje jako *transpilation*.
* Pozměnění generovaný JavaScript, který chcete zmenšit velikost souboru&mdash;tento proces se označuje jako *připravenost k minifikaci*.
* Zpracované soubory jazyka JavaScript, CSS a HTML z zkopírovány *src* k *wwwroot* adresáře.
* Vloží do následující prvky *wwwroot/index.html* souboru:
    * A `<link>` označit, odkazující *wwwroot/main.\< Hodnota hash\>.css* souboru. Tato značka je umisťovaný bezprostředně před uzavírací `</head>` značky.
    * A `<script>` značky, odkazující minifikovaný *wwwroot/main.\< Hodnota hash\>js* souboru. Tato značka je umisťovaný bezprostředně před uzavírací `</body>` značky.
