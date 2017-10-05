---
title: "Устранение неполадок в предварительной версии Microsoft Power BI Embedded"
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
ms.openlocfilehash: f406d23e578acc825514aa5bd9eabcbf160bf9ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a>Устранение неполадок в предварительной версии Microsoft Power BI Embedded
В этой статье содержатся сведения об устранении неполадок в **Power BI Embedded**.

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a>Настройка строк подключения SQL Server
Чтобы задать строку подключения SQL Server, необходимо следовать определенному формату. Ниже приведен пример строки подключения для SQL Server.

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

Дополнительные сведения о строках подключения SQL Server см. в следующих статьях:

* [Строки подключения SQL Server](https://msdn.microsoft.com/library/jj653752.aspx)
* [SqlConnection.ConnectionString](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a>Настройка учетных данных
При наличии учетных данных для среды разработки или промежуточной среды, например имени пользователя и пароля, может потребоваться изменить учетные данные в соответствии с рабочим решением.

## <a name="see-also"></a>См. также
* [Приступая к работе с примером Microsoft Power BI Embedded](power-bi-embedded-get-started-sample.md)
* [Что такое Microsoft Power BI Embedded](power-bi-embedded-what-is-power-bi-embedded.md)

