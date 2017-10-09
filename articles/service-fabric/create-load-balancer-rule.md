---
title: "aaaCreate правило балансировки нагрузки Azure для кластера"
description: "Настройте порты tooopen подсистемы балансировки нагрузки Azure для кластера Azure Service Fabric."
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a>Открытие портов для кластера Service Fabric

Hello подсистемы балансировки нагрузки развернуты вместе с Azure Service Fabric кластера направляет трафик tooyour приложение, работающее на узле. При изменении вашего приложения toouse другой порт, предоставлять этот порт (или маршрутизации другой порт) в hello подсистемы балансировки нагрузки Azure.

При развертывании вашей tooAzure кластера service fabric подсистемы балансировки нагрузки была автоматически создана для вас. Если у вас нет подсистемы балансировки нагрузки, ознакомьтесь с разделом [Создание балансировщика нагрузки для Интернета на портале Azure](..\load-balancer\load-balancer-get-started-internet-portal.md).

## <a name="configure-service-fabric"></a>Настройка Service Fabric

Приложение Service Fabric **ServiceManifest.xml** файл конфигурации определяет конечные точки hello toouse ожидает приложение. После того, файл конфигурации hello была обновленные toodefine конечной точки, балансировки нагрузки hello должно быть обновленные tooexpose, (или другой) порт. Дополнительные сведения о как toocreate hello конечной точки службы fabric. в разделе [установки конечной точки](service-fabric-service-manifest-resources.md).

## <a name="create-a-load-balancer-rule"></a>Создание правила балансировщика нагрузки

Правило подсистемы балансировки нагрузки открывает порт с выходом в Интернет и перенаправляет трафик toohello внутреннего узла порт, используемый вашим приложением. Если у вас нет подсистемы балансировки нагрузки, ознакомьтесь с разделом [Создание балансировщика нагрузки для Интернета на портале Azure](..\load-balancer\load-balancer-get-started-internet-portal.md).

toocreate правило балансировки нагрузки, требуется hello toocollect следующую информацию:

- имя подсистемы балансировки нагрузки;
- Группа ресурсов для hello Подсистема балансировки нагрузки и кластера service fabric.
- внешний порт;
- внутренний порт.

## <a name="azure-cli"></a>Инфраструктура CLI Azure
>[!NOTE]
>Если требуется имя hello toodetermine подсистемы балансировки нагрузки hello используйте tooquickly этой команды get список всех подсистем балансировки нагрузки и hello связанных групп ресурсов.
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

Он принимает только toocreate отдельную команду правило подсистемы балансировки нагрузки с hello **Azure CLI**. Необходимо просто tooknow hello, вызывающую нагрузки hello балансировки и ресурсов toocreate группы новое правило.

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

Hello Azure CLI команда имеет несколько параметров, описанных в следующей таблице hello.

| Параметр | Описание |
| --------- | ----------- |
| `--backend-port`  | приложение hello service fabric для Hello порт прослушивания. |
| `--frontend-port` | порт hello Hello загрузить предоставляет балансировки для внешних соединений. |
| `-lb-name` | Имя Hello hello загрузить toochange балансировки. |
| `-g`       | Группа ресурсов Hello hello балансировки нагрузки и кластера service fabric. |
| `-n`       | Здравствуйте, выбрать имя правила hello. |


>[!NOTE]
>Дополнительные сведения о toocreate балансировки нагрузки с hello Azure CLI. в статье [создать подсистемы балансировки нагрузки с hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).

## <a name="powershell"></a>PowerShell

>[!NOTE]
>Если вам требуется toodetermine hello имя подсистемы балансировки нагрузки hello, используйте tooquickly этой команды get список всех подсистем балансировки нагрузки и группы связанных ресурсов.
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

PowerShell немного сложнее, чем hello Azure CLI. По существу выполните следующие шаги toocreate hello правило.

1. Получите hello балансировки нагрузки Azure.
2. Создайте правило.
3. Добавьте правило для hello toohello подсистемы балансировки нагрузки.
4. Обновление подсистемы балансировки нагрузки hello.

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

О hello `New-AzureRmLoadBalancerRuleConfig` команды hello `-FrontendPort` подсистемы балансировки нагрузки представляет hello порт hello предоставляет внешние подключения и hello `-BackendPort` прослушивают структуры представляет hello порт hello службы приложений.

>[!NOTE]
>Дополнительные сведения о toocreate балансировки нагрузки с помощью PowerShell, в статье [создание подсистемы балансировки нагрузки с помощью PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).

