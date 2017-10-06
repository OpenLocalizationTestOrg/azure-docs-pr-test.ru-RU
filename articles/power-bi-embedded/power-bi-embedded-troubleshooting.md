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
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="e50df-103">Устранение неполадок в предварительной версии Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="e50df-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="e50df-104">Эта статья содержит ответы как tootroubleshoot **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="e50df-104">This article provides answers for how  tootroubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="e50df-105">Настройка строк подключения SQL Server</span><span class="sxs-lookup"><span data-stu-id="e50df-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="e50df-106">tooset строку подключения SQL Server, необходимо toofollow определенный формат.</span><span class="sxs-lookup"><span data-stu-id="e50df-106">tooset a SQL Server connecting string, you need toofollow a specific format.</span></span> <span data-ttu-id="e50df-107">Ниже приведен пример строки подключения для SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e50df-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="e50df-108">toolearn Дополнительные сведения о строки подключения SQL Server, см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="e50df-108">toolearn more about SQL Server connection strings, see hello following articles:</span></span>

* [<span data-ttu-id="e50df-109">Строки подключения SQL Server</span><span class="sxs-lookup"><span data-stu-id="e50df-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="e50df-110">SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="e50df-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="e50df-111">Настройка учетных данных</span><span class="sxs-lookup"><span data-stu-id="e50df-111">Setting credentials</span></span>
<span data-ttu-id="e50df-112">В случае hello, где имеются учетные данные для разработки или промежуточной среде, например имя пользователя и пароль может потребоваться tooupdate учетные данные, соответствующие решения производства.</span><span class="sxs-lookup"><span data-stu-id="e50df-112">In hello case where you have credentials for a development or staging environment, such as user name and password, you might need tooupdate credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="e50df-113">См. также</span><span class="sxs-lookup"><span data-stu-id="e50df-113">See Also</span></span>
* [<span data-ttu-id="e50df-114">Приступая к работе с примером Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="e50df-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="e50df-115">Что такое Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="e50df-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)

