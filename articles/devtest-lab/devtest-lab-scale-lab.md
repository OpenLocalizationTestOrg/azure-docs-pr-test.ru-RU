---
title: "aaaScale квоты и ограничения в лаборатории в Azure DevTest Labs | Документы Microsoft"
description: "Узнайте, как tooscale лаборатории в Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a>Масштабирование квот и ограничений в DevTest Labs
При работе в DevTest Labs, можно заметить, что отсутствуют определенные toosome ограничения по умолчанию ресурсы Azure, что может повлиять на службы DevTest Labs hello. Эти ограничения, который ссылается tooas **квоты**.

> [!NOTE]
> Hello DevTest Labs службы не задать все квоты. Квоты, которые могут возникнуть, ограничения по умолчанию hello в целом Azure подписки.

Каждый ресурс Azure можно использовать, пока не достигнута его квота. Каждая подписка имеет свои квоты, а процесс использования отслеживается отдельно для каждой подписки.

Например, что каждой подписки задана квота по умолчанию в 20 ядер. Таким образом, при создании в лаборатории виртуальных машин, каждая из которых имеет четыре ядра, можно создать только пять виртуальных машин. 

[Azure подписка и ограничения служб](https://docs.microsoft.com/azure/azure-subscription-service-limits) перечислены некоторые наиболее распространенные квот hello для ресурсов Azure. Здравствуйте, ресурсы, которые наиболее часто используются в лабораторной среде и для которой могут возникнуть квоты, включают Виртуальных машинах, общих IP-адресов, сетевого интерфейса, управляемого дисков, назначение роли RBAC и каналы ExpressRoute.

## <a name="view-your-usage-and-quotas"></a>Просмотр сведений об использовании и квотах
Следующие шаги показывают, как tooview hello текущие квоты в вашей подписке для определенных ресурсов Azure и toosee использовали какой процент каждой из квот.

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Выберите **более служб**, а затем выберите **выставления счетов** из списка hello.
1. В колонке hello выставления счетов выберите подписку.
4. Выберите **Использование и квоты**.

   ![Кнопка "Использование и квоты"](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   Здравствуйте, использование + квоты колонке отображается список различных ресурсах, доступных в такой подписки и hello процент квоты hello, который используется для каждого ресурса.

   ![Квоты и использование](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a>Запрос дополнительных ресурсов в подписке
По достижении конца квоты, ограничение по умолчанию hello ресурса в подписке можно увеличить вверх tooa максимальный предел, как описано в [подписка Azure и ограничения служб](https://docs.microsoft.com/azure/azure-subscription-service-limits).

Следующие шаги показывают, как toorequest квоты увеличивать через hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Щелкните **Больше служб**, выберите **Выставление счетов**, а затем — **Использование и квоты**.
1. Здравствуйте, использование + колонке квоты, выберите hello **запросить увеличение** кнопки.

   ![Кнопка "Запросить увеличение"](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. toocomplete и отправить запрос hello, заполните hello необходимые сведения на всех трех вкладках hello **New поддерживает запрос** формы.

   ![Форма запроса на увеличение](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

[Основные сведения о Azure ограничения и увеличивая степень](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) предоставляет дополнительные сведения об обращении в службу поддержки Azure toorequest квоты увеличение.



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>Дальнейшие действия
* Просмотр hello [коллекции шаблонов Azure Resource Manager DevTest Labs QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/Samples).
