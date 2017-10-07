---
title: "кластер Service Fabric aaaCreate в Azure | Документы Microsoft"
description: "Узнайте, как toocreate Windows или Linux Service Fabric кластер в Azure с помощью PowerShell."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a>Создание безопасного кластера в Azure с помощью PowerShell
В этом учебнике показано, как toocreate Service Fabric кластера (Windows или Linux) в Azure. После завершения имеется кластер, работающими в облаке hello, можно развернуть приложение.

Из этого руководства вы узнаете, как выполнять такие задачи:

> [!div class="checklist"]
> * Создание защищенного кластера Service Fabric в Azure с помощью PowerShell
> * Безопасный hello кластера с помощью сертификата X.509
> * Подключите кластер toohello с помощью PowerShell
> * Удаление кластера

## <a name="prerequisites"></a>Предварительные требования
Перед началом работы с этим руководством выполните следующие действия:
- Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- Установка hello [модуля Service Fabric SDK и PowerShell](service-fabric-get-started.md)
- Установка hello [Azure Powershell версии 4.1 или более поздней версии модуля](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)

После процедуры Hello создает Предварительный просмотр (одной виртуальной машины) для одного узла кластера Service Fabric. кластер Hello защищен самозаверяющий сертификат, который получает создан вместе с кластера hello и затем помещается в хранилище ключей. Кластеры с одним узлом, не может быть масштабирована за одну виртуальную машину и предварительного просмотра кластеров не может быть toonewer обновленной версии.

toocalculate расходы, выполнив кластера Service Fabric в Azure используйте hello [калькулятор цен Azure](https://azure.microsoft.com/pricing/calculator/).
Дополнительные сведения о создании кластеров Service Fabric см. в статье [Создание кластера Service Fabric в Azure с помощью Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).

## <a name="create-hello-cluster-using-azure-powershell"></a>Создание кластера hello, с помощью Azure PowerShell
1. Загрузить локальную копию шаблона Azure Resource Manager hello и файл параметров hello hello [шаблона Azure Resource Manager для Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) репозитории GitHub.  *azuredeploy.JSON* — шаблон hello Azure Resource Manager, который определяет кластер Service Fabric. *azuredeploy.Parameters.JSON* — это файл параметров для вас toocustomize hello кластерном развертывании.

2. Настроить следующие параметры в hello hello *azuredeploy.parameters.json* файл параметров:

   | Параметр       | Описание | Рекомендуемое значение |
   | --------------- | ----------- | --------------- |
   | clusterLocation | кластер hello toodeploy toowhich регион Azure Hello. | *Например, westeurope, eastasia, eastus* |
   | clusterName     | Имя кластера hello требуется toocreate. | *Например, bobs-sfpreviewcluster* |
   | adminUserName   | Hello учетная запись локального администратора на виртуальных машинах hello кластера. | *Любое допустимое имя пользователя Windows Server* |
   | adminPassword   | Пароль учетной записи локального администратора hello на виртуальных машинах hello кластера. | *Любой допустимый пароль Windows Server* |
   | clusterCodeVersion | toorun версии Service Fabric Hello. (255.255.X.255 — предварительные версии). | **255.255.5718.255** |
   | vmInstanceCount | Hello количество виртуальных машин в кластере (может быть 1 или 3-99). | **1** | *Для предварительной версии кластера укажите только одну виртуальную машину* |

3. Откройте консоль PowerShell, tooAzure входа и выберите hello подписку, которую требуется toodeploy hello кластера в:

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. Создайте и зашифровать пароль для сертификата toobe hello, используемые Service Fabric.

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. Создание кластера hello и свой сертификат, выполнив следующую команду hello.

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   >Hello `-CertificateSubjectName` параметра должны быть выровнены с параметром Имя_кластера hello, указанный в файле параметров hello, также как hello toohello домена привязан регион Azure вы выбрали, например: `clustername.eastus.cloudapp.azure.com`.

После завершения настройки hello, он выводит сведения о кластере hello, созданные в Azure. Также он копирует каталог hello кластера сертификат toohello - CertificateOutputFolder на hello путь, заданный для этого параметра. Необходимо, чтобы этот сертификат tooaccess Service Fabric Explorer и представление hello работоспособности кластера.

Запишите hello URL-адрес для кластера, который может быть примерно toohello URL-адреса: *https://mycluster.westeurope.cloudapp.azure.com:19080*

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a>& Изменить сертификат hello доступ обозреватель Service Fabric ##

1. Дважды щелкните hello tooopen hello сертификатов мастера импорта сертификатов.

2. Использовать параметры по умолчанию, но убедитесь, что hello toocheck **Пометить ключ как экспортируемый.** флажок в hello **защиты закрытого ключа** шаг. Visual Studio требуется tooexport hello сертификат при настройке проверки подлинности кластера Fabric tooService реестра контейнера Azure далее в этом учебнике.

3. Теперь можно открыть обозреватель Service Fabric в браузере. toodo таким образом, перейдите toohello **ManagementEndpoint** URL-адрес для кластера с помощью веб-браузер и hello выберите сертификат, который был сохранен на компьютере.

>[!NOTE]
>При открытии обозревателя Service Fabric появится сообщение об ошибке сертификата, так как используется самозаверяющий сертификат. В Edge, у вас есть tooclick *сведения* и затем hello *перейдите на веб-странице toohello* ссылку. В браузере Chrome, у вас есть tooclick *Дополнительно* и затем hello *Продолжить* ссылку.

>[!NOTE]
>Если происходит сбой создания кластера hello, всегда можно повторно hello команду, которая обновляет hello ресурсов, уже развернутых. Если сертификат был создан в ходе развертывания не удалось hello, создается новый. Создание кластера tootroubleshoot, в разделе [создание кластера Service Fabric с помощью диспетчера ресурсов Azure](service-fabric-cluster-creation-via-arm.md).

## <a name="connect-toohello-secure-cluster"></a>Подключите кластер безопасного toohello
Подключите кластер toohello с помощью модуля Service Fabric PowerShell hello, установленные с hello Service Fabric SDK.  Во-первых установите hello сертификат в хранилище персональных (Мои) hello hello текущего пользователя на компьютере.  Выполните следующую команду PowerShell hello.

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

Теперь вы находитесь кластера безопасных готовы tooconnect tooyour.

Hello **Service Fabric** модуль PowerShell предоставляет многие командлеты для управления кластерами, приложениями и службами Service Fabric.  Используйте hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) командлет tooconnect toohello безопасности кластера. Здравствуйте, отпечаток сертификата и сведений о конечной точке соединения находятся в выходной hello из предыдущего шага.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Убедитесь, что вы подключены, и hello кластера находится в работоспособном состоянии, с помощью hello [Get ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) командлета.

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a>Очистка ресурсов

Кластер состоит из других ресурсов Azure в дополнение к этому toohello сам ресурс кластера. Hello простейший способ toodelete hello кластера и все ресурсы hello, которые он использует является группой ресурсов toodelete hello.

Войдите в tooAzure и выберите hello идентификатор подписки, с которой необходимо tooremove hello кластера.  Идентификатор подписки можно найти в систему в toohello [портал Azure](http://portal.azure.com). Удалите группу ресурсов hello и все ресурсы кластера hello, с помощью hello [командлет Remove-AzureRMResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a>Дальнейшие действия
Из этого руководства вы узнали, как выполнять такие задачи:

> [!div class="checklist"]
> * Создание кластера Service Fabric в Azure
> * Безопасный hello кластера с помощью сертификата X.509
> * Подключите кластер toohello с помощью PowerShell
> * Удаление кластера

Затем переместить следующие учебника toolearn как toohello toodeploy существующего приложения.
> [!div class="nextstepaction"]
> [Развертывание существующего приложения .NET с помощью Docker Compose](service-fabric-host-app-in-a-container.md)
