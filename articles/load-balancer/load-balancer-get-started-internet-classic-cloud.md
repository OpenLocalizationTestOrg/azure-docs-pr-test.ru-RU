---
title: "Подсистема балансировки нагрузки aaaCreate из Интернета для облачных служб Azure | Документы Microsoft"
description: "Узнайте, как из Интернета toocreate Подсистема балансировки загрузки в классической модели развертывания для облачных служб"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 0bb16f96-56a6-429f-88f5-0de2d0136756
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d93cf76d417cbfc744cf07ba48c43a63cc14df69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a>Приступая к работе по созданию балансировщика нагрузки для Интернета для облачных служб

> [!div class="op_single_selector"]
> * [классический портал Azure](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Интерфейс командной строки Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [облачных служб Azure](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Перед началом работы с ресурсами Azure, он является важным toounderstand, что Azure в данный момент существуют две модели развертывания: диспетчера ресурсов Azure и классическом. Обязательно изучите [модели и инструменты развертывания](../azure-classic-rm.md) , прежде чем приступить к работе с какими бы то ни было ресурсами Azure. Для просмотра документации hello для различных средств, щелкнув вкладки hello hello верхней части этой статьи. В этой статье рассматриваются hello классической модели развертывания. Вы также можете [Узнайте, как с помощью диспетчера ресурсов Azure подсистемы балансировки нагрузки, toocreate из Интернета](load-balancer-get-started-internet-arm-ps.md).

Облачные службы автоматически настраиваются с подсистемой балансировки нагрузки и можно настроить через модель службы hello.

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a>Создание с помощью файла определения службы hello подсистемы балансировки нагрузки

Вы можете использовать hello Azure SDK для .NET 2,5 tooupdate облачной службы. Параметры конечной точки для облачных служб, выполняемых в hello [службы определение](https://msdn.microsoft.com/library/azure/gg557553.aspx) файл csdef.

Hello следующем примере показано, как настроить файл servicedefinition.csdef для развертывания облака:

Проверка фрагмент кода hello для hello файл csdef, созданный при развертывании облака, вы увидите hello внешней конечной точки, настроенной toouse порты HTTP через порт 10000 10001 и 10002.

```xml
<ServiceDefinition name=“Tenant“>
    <WorkerRole name=“FERole” vmsize=“Small“>
<Endpoints>
    <InputEndpoint name=“FE_External_Http” protocol=“http” port=“10000“ />
    <InputEndpoint name=“FE_External_Tcp“  protocol=“tcp“  port=“10001“ />
    <InputEndpoint name=“FE_External_Udp“  protocol=“udp“  port=“10002“ />

    <InputEndpointname=“HTTP_Probe” protocol=“http” port=“80” loadBalancerProbe=“MyProbe“ />

    <InstanceInputEndpoint name=“InstanceEP” protocol=“tcp” localPort=“80“>
        <AllocatePublicPortFrom>
            <FixedPortRange min=“10110” max=“10120“  />
        </AllocatePublicPortFrom>
    </InstanceInputEndpoint>
    <InternalEndpoint name=“FE_InternalEP_Tcp” protocol=“tcp“ />
</Endpoints>
    </WorkerRole>
</ServiceDefinition>
```

## <a name="check-load-balancer-health-status-for-cloud-services"></a>Проверка состояния работоспособности подсистемы балансировки нагрузки для облачных служб

Hello ниже приведен пример проверки работоспособности:

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

Hello балансировки нагрузки объединяет сведения hello hello конечной точки и hello toocreate hello проверки URL-адреса в форме hello `http://{DIP of VM}:80/Probe.aspx` , может быть используется tooquery hello работоспособности службы hello.

Hello служба обнаруживает периодической проверки из hello же IP-адрес. Это запрос проверки работоспособности hello, поступающих от узла hello узла hello запущенным hello виртуальной машины. Служба Hello имеет toorespond с кодом состояния HTTP 200 для tooassume подсистемы балансировки нагрузки hello, что служба hello находится в работоспособном состоянии. Все другие состояния HTTP код (например 503) напрямую принимает hello виртуальной машины из ротации.

Определение проверки Hello также управляет hello частоту выборки hello. В нашем случае выше hello балансировки нагрузки проверка конечной точки hello каждые 5 секунд. Если нет утвердительный ответ, полученный для 10 секунд (двух интервалов выборки), проверки hello предполагается вниз и hello виртуальной машины берется из ротации. Аналогичным образом Если служба hello из ротации и утвердительный ответ, служба hello помещается обратно toorotation прямо сейчас. Если службы hello нагрузка колеблется между Работоспособная и Неработоспособная, подсистемы балансировки нагрузки hello вправе toodelay hello повторное введение задней toorotation hello службы до работоспособны, чтобы число проб.

Проверьте hello схема определения службы для hello [проверки работоспособности](https://msdn.microsoft.com/library/azure/jj151530.aspx) для получения дополнительной информации.

## <a name="next-steps"></a>Дальнейшие действия

[Приступая к настройке внутренней подсистемы балансировки нагрузки](load-balancer-get-started-ilb-arm-ps.md)

[Настройка режима распределения подсистемы балансировки нагрузки](load-balancer-distribution-mode.md)

[Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md)

