---
title: "Выставление счетов и о гибком управлении ресурсами в Azure стек aaaCustomer | Документы Microsoft"
description: "Узнайте, как сведения об использовании ресурсов tooretrieve из стека Azure."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: a9afc7b6-43da-437b-a853-aab73ff14113
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2016
ms.author: alfredop
ms.openlocfilehash: d92caac2874e5364870b29a38515b579ab059991
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="usage-and-billing-in-azure-stack"></a>Использование и выставление счетов в стек Azure

Использование представляет hello количество ресурсов, потребляемых пользователем. Стек Azure собирает сведения об использовании для каждого пользователя и использует их toobill их. Эта статья описывает, каким образом пользователи стек Azure взимается плата за использование ресурсов, и способ доступа к hello сведений о выставлении счетов для аналитики, гибкого управления ресурсами, и т. д.

Стек Azure содержит toocollect инфраструктуры hello и собирать данные об использовании для всех ресурсов. Доступ к этим данным и экспортировать tooa система выставления счетов с помощью адаптера выставления счетов или экспортировать его средство tooa бизнес-аналитики, такие как Microsoft Power BI. После экспорта, это сведения об оплате используется для аналитики или передаваться tooa системы о гибком управлении ресурсами.

![Концептуальная модель для подключения Azure стека tooa адаптер выставления счетов выставления счетов для приложения](media/azure-stack-billing-and-chargeback/image1.png)

## <a name="what-usage-information-can-i-find-and-how"></a>Какие сведения об использовании можно найти и как?

Azure поставщиков ресурсов стека, например вычислений, хранения и сети, создают данные об использовании через часовые интервалы для каждой подписки. Hello данные об использовании содержит сведения о ресурсе hello, например, имя ресурса, индикатор имя, идентификатор отслеживать количество использованные toolearn т. д. о ресурсах идентификатор hello метрах см. в toohello [API часто задаваемые вопросы об использовании](azure-stack-usage-related-faq.md) статьи. 

После сбора данных об использовании hello — [сообщил tooAzure](azure-stack-usage-reporting.md) toogenerate счета, который можно просмотреть с помощью hello Azure портале выставления счетов. Hello Azure портале выставления счетов выводятся данные об использовании hello только для ресурсов оплачивается hello. В дополнение к этому toohello оплачивается ресурсы, стек Azure записывает данные об использовании для более широкому набору ресурсов, которые можно использовать в среде Azure стека через API-интерфейс REST или PowerShell. Администраторов облака Azure стека можно получить данные об использовании hello для всех пользовательских подписок, в то время как пользователь сможет получить только свои сведения об использовании.

## <a name="retrieve-usage-information"></a>Получить сведения об использовании

данные об использовании toogenerate hello, должен иметь ресурсы, которые запущена и активно используете hello системы. Если вы не знаете ли какие либо ресурсы в Azure Marketplace стека, развертывание виртуальной машины (VM) и проверить hello ВМ мониторинга колонке toomake убедиться, что она выполняет. Используйте следующие данные об использовании hello tooview командлеты PowerShell hello.

1. [Установка PowerShell Azure стека.](azure-stack-powershell-install.md)
2. * [Настройка пользователя Azure стека hello](azure-stack-powershell-configure-user.md) или hello [стека Azure оператор](azure-stack-powershell-configure-admin.md) среды PowerShell 
3. данные об использовании tooretrieve hello, использовать hello [Get UsageAggregates](/powershell/module/azurerm.usageaggregates/get-usageaggregates) командлета PowerShell:
   ```PowerShell
   Get-UsageAggregates -ReportedStartTime "<Start time for usage reporting>" -ReportedEndTime "<end time for usage reporting>" -AggregationGranularity <Hourly or Daily>
   ```

   Если данные об использовании недоступны, возвращается в как показано на следующий снимок экрана приветствия: 
   
   ![Использование статистических выражений](media/azure-stack-billing-and-chargeback/image2.png)
   
   PowerShell возвращает 1 000 строк использование каждого вызова. Можно использовать параметр tooretrieve hello продолжения более 1000 строк

## <a name="next-steps"></a>Дальнейшие действия

[Отчет tooAzure данных об использовании стек Azure](azure-stack-usage-reporting.md)

[Использование поставщика ресурсов API](azure-stack-provider-resource-api.md)

[Использование ресурсов API клиента](azure-stack-tenant-resource-usage-api.md)

[Часто задаваемые вопросы, относящиеся к использованию](azure-stack-usage-related-faq.md)

