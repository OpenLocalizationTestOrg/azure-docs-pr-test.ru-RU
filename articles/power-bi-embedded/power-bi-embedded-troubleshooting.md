---
title: "Устранение неполадок предварительной версией Power BI Embedded aaaMicrosoft"
description: "Устранение неполадок в предварительной версии Microsoft Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: c8aee652-ed8b-4c66-9c63-f798b7a655b4
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: a0a25cd73977c0ea0bd6b7c82e215412245771bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a>Устранение неполадок в предварительной версии Microsoft Power BI Embedded
Эта статья содержит ответы как tootroubleshoot **Power BI Embedded**.

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a>Настройка строк подключения SQL Server
tooset строку подключения SQL Server, необходимо toofollow определенный формат. Ниже приведен пример строки подключения для SQL Server.

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

toolearn Дополнительные сведения о строки подключения SQL Server, см. следующие статьи hello:

* [Строки подключения SQL Server](https://msdn.microsoft.com/library/jj653752.aspx)
* [SqlConnection.ConnectionString](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a>Настройка учетных данных
В случае hello, где имеются учетные данные для разработки или промежуточной среде, например имя пользователя и пароль может потребоваться tooupdate учетные данные, соответствующие решения производства.

## <a name="see-also"></a>См. также
* [Приступая к работе с примером Microsoft Power BI Embedded](power-bi-embedded-get-started-sample.md)
* [Что такое Microsoft Power BI Embedded](power-bi-embedded-what-is-power-bi-embedded.md)

