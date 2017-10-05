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
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="d5175-103">Устранение неполадок в предварительной версии Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="d5175-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="d5175-104">В этой статье содержатся сведения об устранении неполадок в **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="d5175-104">This article provides answers for how  to troubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="d5175-105">Настройка строк подключения SQL Server</span><span class="sxs-lookup"><span data-stu-id="d5175-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="d5175-106">Чтобы задать строку подключения SQL Server, необходимо следовать определенному формату.</span><span class="sxs-lookup"><span data-stu-id="d5175-106">To set a SQL Server connecting string, you need to follow a specific format.</span></span> <span data-ttu-id="d5175-107">Ниже приведен пример строки подключения для SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d5175-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="d5175-108">Дополнительные сведения о строках подключения SQL Server см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="d5175-108">To learn more about SQL Server connection strings, see the following articles:</span></span>

* [<span data-ttu-id="d5175-109">Строки подключения SQL Server</span><span class="sxs-lookup"><span data-stu-id="d5175-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="d5175-110">SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="d5175-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="d5175-111">Настройка учетных данных</span><span class="sxs-lookup"><span data-stu-id="d5175-111">Setting credentials</span></span>
<span data-ttu-id="d5175-112">При наличии учетных данных для среды разработки или промежуточной среды, например имени пользователя и пароля, может потребоваться изменить учетные данные в соответствии с рабочим решением.</span><span class="sxs-lookup"><span data-stu-id="d5175-112">In the case where you have credentials for a development or staging environment, such as user name and password, you might need to update credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="d5175-113">См. также</span><span class="sxs-lookup"><span data-stu-id="d5175-113">See Also</span></span>
* [<span data-ttu-id="d5175-114">Приступая к работе с примером Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="d5175-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="d5175-115">Что такое Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="d5175-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)

