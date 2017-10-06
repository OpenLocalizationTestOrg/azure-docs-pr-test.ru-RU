---
title: "проблемы, связанные с aaaDeployment облачной службы Microsoft Azure часто задаваемые вопросы о | Документы Microsoft"
description: "В этой статье перечислены hello часто задаваемые вопросы о развертывания для облачных служб Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 8d67e36aa87fb5794d358e5cc235123ac7286028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Проблемы развертывания для облачных служб Azure. Вопросы и ответы (FAQ)

В этой статье приведены часто задаваемые вопросы по проблемам развертывания для [облачных служб Microsoft Azure](https://azure.microsoft.com/services/cloud-services). Кроме того, можно обратиться к hello [страницы размер виртуальной Машины облачных служб](cloud-services-sizes-specs.md) для сведений о размере.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-does-deploying-a-cloud-service-toohello-staging-slot-sometimes-fail-with-a-resource-allocation-error-if-there-is-already-an-existing-deployment-in-hello-production-slot"></a>Почему развертывание облачной службы toohello иногда промежуточных слотах не с ошибкой выделения ресурсов Если существующее развертывание в производственный слот hello?
Если развертывание облачной службы в любой ячейке, hello всей облачной службы является закрепленных tooa конкретному кластеру. Это означает, что если развертывания уже существует в производственный слот hello, новое промежуточное развертывание может быть размещена только в hello же кластера в качестве hello производственный слот.

Ошибки при выделении возникать, когда hello кластера, где находится облачной службы не имеет достаточно физические вычислительные ресурсы toosatisfy запроса на развертывание.

Статья [Сбой выделения ресурсов для облачной службы: решения](cloud-services-allocation-failures.md#solutions) поможет устранить такие ошибки выделения.

## <a name="why-does-scaling-up-or-scaling-out-a-cloud-service-deployment-sometimes-result-in-allocation-failure"></a>Почему масштабирование развертывания облачной службы иногда приводит к сбою выделения?
При развертывании облачной службы, обычно получает закрепленных tooa конкретному кластеру. Это означает, что вертикальное масштабирование/out существующей облачной службы необходимо выделения новых экземпляров hello одного кластера. Если кластер hello почти заполнена или hello требуемого ВМ размер и тип недоступен, hello запрос может завершиться неудачно.

Статья [Сбой выделения ресурсов для облачной службы: решения](cloud-services-allocation-failures.md#solutions) поможет устранить такие ошибки выделения.

## <a name="why-does-deploying-a-cloud-service-into-an-affinity-group-sometimes-result-in-allocation-failure"></a>Почему развертывание облачной службы в территориальной группе иногда приводит к появлению ошибки выделения?
Новый пустой облачной службе tooan развертывания может быть выделен структуры hello в любой кластер в этой области, если hello облачная служба — закрепленных tooan территориальную группу. Toohello развертываний же территориальная группа будет предпринята в hello одного кластера. Если кластер hello почти заполнена, hello запрос может завершиться ошибкой.

Статья [Сбой выделения ресурсов для облачной службы: решения](cloud-services-allocation-failures.md#solutions) поможет устранить такие ошибки выделения.

## <a name="why-does-changing-vm-size-or-adding-a-new-vm-tooan-existing-cloud-service-sometimes-result-in-allocation-failure"></a>Почему изменение размера виртуальной Машины или добавлении новой виртуальной Машины tooan существующей облачной службе иногда приводит к появлению ошибки выделения?
Hello кластеров в центре обработки данных может иметь собственную конфигурацию машины типов (например, ряда, Av2 рядов, серии D, серии Dv2, серии G, H рядов, и т. д.). Однако не все кластеры hello всегда будет иметь все виды hello виртуальных машин. Например при попытке tooadd серии D ВМ tooa облачная служба, которая уже развернуто в кластере типа только для ряда, будет возникать ошибки выделения. Это также происходит при попытке что toochange ВМ SKU, чей размер (например, при переключении из серии tooa D серии A).

Статья [Сбой выделения ресурсов для облачной службы: решения](cloud-services-allocation-failures.md#solutions) поможет устранить такие ошибки выделения.

toocheck hello размеры, доступные в вашем регионе. в разделе [Microsoft Azure: продукты, доступные по регионам](https://azure.microsoft.com/regions/services).

## <a name="why-does-deploying-a-cloud-service-sometime-fail-due-toolimitsquotasconstraints-on-my-subscription-or-service"></a>Почему выполняет развертывание облачной службы иногда сбой из-за toolimits/квоты и ограничения для моей подписки или службы?
Развертывание для облачной службы может завершиться ошибкой, если hello ресурсы, необходимые toobe выделенной превышают по умолчанию hello или максимальная квота разрешено для вашей службы на уровне hello регионе и центре обработки данных. Дополнительные сведения см. в статье [Ограничения облачных служб](../azure-subscription-service-limits.md#cloud-services-limits).

Можно также отслеживать hello текущего или квоты на использование для вашей подписки на портале hello: портал Azure = > подписок = > \<соответствующие подписки > = > «Использование + квоты».

Также можно получить сведения и потребление-, относящиеся к использованию ресурсов через API-интерфейсов выставления счетов Azure hello. См. раздел [API использования ресурсов Azure (предварительная версия)](../billing/billing-usage-rate-card-overview.md#azure-resource-usage-api-preview).

## <a name="how-can-i-change-hello-size-of-a-deployed-cloud-service-vm-without-redeploying-it"></a>Как изменить размер hello развернутую облачную службу виртуальной Машины без ее повторного развертывания?
Невозможно изменить размер виртуальной Машины hello развернутую облачную службу без ее повторного развертывания. Hello размер виртуальной Машины встроен в hello CSDEF, которое может быть обновлено только с повторного развертывания.

Дополнительные сведения см. в разделе [как tooupdate облачной службы](cloud-services-update-azure-service.md).

 
