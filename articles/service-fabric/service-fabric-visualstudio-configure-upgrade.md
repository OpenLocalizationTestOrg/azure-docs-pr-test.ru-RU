---
title: "обновление приложения Service Fabric hello aaaConfigure | Документы Microsoft"
description: "Узнайте, как tooconfigure hello параметров обновления приложения Service Fabric с помощью Microsoft Visual Studio."
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a>Настройка обновления hello приложения Service Fabric в Visual Studio
Visual Studio tools для Azure Service Fabric поддерживает обновления публикации toolocal или удаленных кластеров. Существует три сценария, в которых требуется tooupgrade более новой версии приложения tooa вместо замены приложения hello во время тестирования и отладки.

* Данные приложения не были потеряны во время обновления hello.
* Доступность остается высокого уровня, не будет нарушения работы службы во время обновления hello при наличии достаточного числа экземпляров службы распределены по нескольким доменам обновления.
* Тесты для приложения могут запускаться во время его обновления.

## <a name="parameters-needed-tooupgrade"></a>Параметры требуются tooupgrade
Существует два типа развертывания: обычное или обновление. Регулярные развертывания будут удалены все предыдущие сведения о развертывании и данные на кластере hello во время развертывания обновления сохраняет его. При обновлении приложения Service Fabric в Visual Studio требуется параметров обновления приложения tooprovide и проверку политики работоспособности. Обновление приложения, параметры помогают управлять обновления hello при проверку политики работоспособности определить, успешно ли прошло обновление hello. Дополнительные сведения см. в статье [Параметры обновления приложений](service-fabric-application-upgrade-parameters.md).

Существует три режима обновления: *отслеживаемое*, *неотслеживаемое автоматическое* и *неотслеживаемое ручное*.

* Обновление отслеживаемое автоматизирует обновление hello и приложение проверки работоспособности.
* Обновление UnmonitoredAuto автоматизирует обновление hello, но пропускает hello проверки работоспособности приложения.
* При этом обновление UnmonitoredManual необходимо toomanually обновить каждый домен обновления.

Для каждого режима обновления необходим различный набор параметров. В разделе [параметров обновления приложения](service-fabric-application-upgrade-parameters.md) toolearn больше о доступных параметрах обновления hello.

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a>Обновление приложения Service Fabric в Visual Studio
Если вы используете tooupgrade средств Visual Studio Service Fabric hello приложения Service Fabric, можно указать toobe процесс публикации обновления, а не регулярное развертывания путем проверки hello **обновление приложения hello** проверки поле.

### <a name="tooconfigure-hello-upgrade-parameters"></a>Параметры обновления tooconfigure hello
1. Нажмите кнопку hello **параметры** кнопки следующий toohello флажок. Hello **изменение параметров обновления** откроется диалоговое окно. Hello **изменение параметров обновления** диалоговое окно поддерживает режимы hello отслеживаемое, UnmonitoredAuto и UnmonitoredManual обновления.
2. Выберите режим обновления hello toouse а затем заполнить hello сеткой параметров.

    Каждый параметр имеет значения по умолчанию. Необязательный параметр Hello *DefaultServiceTypeHealthPolicy* входные таблицы хэша. Ниже приведен пример входной формат hello хэш-таблицы для *DefaultServiceTypeHealthPolicy*:

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    *ServiceTypeHealthPolicyMap* еще один необязательный параметр, входные таблицы хэша в hello следующий формат:

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    Ниже приведен пример из реальной жизни:

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. Если выбран режим обновления UnmonitoredManual, необходимо вручную запустите toocontinue консоль PowerShell и завершения процесса обновления hello. См. слишком[обновление приложения Service Fabric: Дополнительные разделы](service-fabric-application-upgrade-advanced.md) toolearn вручную обновить works.

## <a name="upgrade-an-application-by-using-powershell"></a>Обновление приложения с помощью PowerShell
Можно использовать командлеты PowerShell tooupgrade приложения Service Fabric. Подробные сведения см. в [руководстве по обновлению приложений Service Fabric](service-fabric-application-upgrade-tutorial.md) и статье, посвященной командлету [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx).

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a>Укажите в файле манифеста приложения hello проверку политики работоспособности
Каждая служба в приложении Service Fabric может иметь собственные параметры политики работоспособности, которые переопределяют значения по умолчанию hello. Можно предоставить значения этих параметров в файле манифеста приложения hello.

Hello следующем примере показано, как tooapply уникальный работоспособности проверьте политику для каждой службы в манифесте приложения hello.

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о развертывании приложений см. в статье [Развертывание гостевого исполняемого файла в Service Fabric](service-fabric-deploy-existing-app.md).