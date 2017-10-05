---
title: "Настройка кластера Azure Service Fabric | Документация Майкрософт"
description: "Краткое руководство о создании кластера Service Fabric для Windows или Linux в Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: ec59450052b377412a28f7eaf55d1f1512b55195
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a>Создание первого кластера Service Fabric в Azure
[Кластер Service Fabric](service-fabric-deploy-anywhere.md) — это подключенный к сети набор виртуальных машин или физических компьютеров, в котором вы развертываете микрослужбы и управляете ими. Используя это краткое руководство, вы сможете за несколько минут создать кластер с пятью узлами под управлением Windows или Linux на [портале Azure](http://portal.azure.com) или с помощью [Azure PowerShell](https://msdn.microsoft.com/library/dn135248).  

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) , прежде чем начинать работу.


## <a name="use-the-azure-portal"></a>Использование портала Azure

Войдите на портал Azure. Для этого перейдите по ссылке [http://portal.azure.com](http://portal.azure.com).

### <a name="create-the-cluster"></a>Создание кластера

1. Щелкните **Создать** в верхнем левом углу портала Azure.
2. Выберите **Среда выполнения приложений** в колонке **Создать**, а затем в колонке **Среда выполнения приложений** выберите **Кластер Service Fabric**.
3. Заполните форму Service Fabric **Основы**. Выберите версию **операционной системы** Windows или Linux для запуска узлов кластера. Имя пользователя и пароль понадобятся для входа на виртуальную машину. Создайте **группу ресурсов**. Группа ресурсов — это логический контейнер, в котором происходит создание ресурсов Azure и коллективное управление ими. По завершении нажмите кнопку **ОК**.

    ![Результат установки кластера][cluster-setup-basics]

4. Заполните форму **Конфигурация кластера**.  Для параметра **Число типа узлов** введите значение "1".

5. Выберите **Node type 1 (Primary)** (Тип узла 1 (первичный)) и заполните форму **Конфигурация типа узла**.  Укажите имя типа узла и задайте для параметра [Уровень устойчивости](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) значение "Бронзовый".  Выберите размер виртуальной машины.

    Типы узлов определяют размер виртуальной машины, их число, пользовательские конечные точки и другие параметры для виртуальных машин этого типа. Каждый определенный тип узла настроен как отдельный масштабируемый набор виртуальных машин, используемый для развертывания виртуальных машин и управления ими в наборе. Каждый тип узла поддерживает возможность независимого масштабирования, имеет разные наборы открытых портов и собственные метрики емкости.  Первый или первичный тип узла определяет размещение системных служб Service Fabric и должен включать от пяти виртуальных машин.

    Для любой рабочей развернутой службы важным шагом является [планирование загрузки](service-fabric-cluster-capacity.md).  Так как в этом кратком руководстве вы не будете выполнять приложения, вы можете выбрать размер виртуальной машины *DS1_v2 Standard*.  Для [уровня надежности](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) задайте значение Silver, а для масштабируемого набора виртуальных машин задайте начальную мощность 5.  

    Пользовательские конечные точки открывают порты в подсистеме балансировщика нагрузки Azure, поэтому вы сможете подключиться к приложениям, выполняющимся в кластере.  Введите "80, 8172", чтобы открыть порты 80 и 8172.

    Не устанавливайте флажок в поле **Настройка дополнительных параметров**, используемом для настройки конечных точек управления протоколами TCP и HTTP, диапазонов порта приложения, [ограничений на размещение](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints) и [свойств емкости](service-fabric-cluster-resource-manager-metrics.md).    

    Нажмите кнопку **ОК**.

6. В форме **Конфигурация кластера** задайте значение **Вкл.** для **диагностики**.  При работе с этим руководством не нужно вводить свойства [настроек структуры](service-fabric-cluster-fabric-settings.md).  В разделе **Версия Fabric** выберите режим **автоматического** обновления, чтобы корпорация Майкрософт автоматически обновляла версию кода Fabric, выполняющегося в кластере.  Если вы хотите [выбирать поддерживаемую версию](service-fabric-cluster-upgrade.md), задайте режим **Вручную**. 

    ![Конфигурация типа узла][node-type-config]

    Нажмите кнопку **ОК**.

7. Заполните форму **Безопасность**.  Для этого руководства выберите **незащищенный** режим.  Учитывая, что любой пользователь может анонимно подключиться к незащищенному кластеру и выполнять различные операции управления, для производственных рабочих нагрузок мы настоятельно рекомендуем создать безопасное подключение к кластеру.  

    Сертификаты используются в Service Fabric, чтобы обеспечить функции аутентификации и шифрования для защиты различных аспектов кластера и его приложений. Дополнительные сведения о том, как сертификаты используются в Service Fabric, см. в статье [Сценарии защиты кластера Service Fabric](service-fabric-cluster-security.md).  Чтобы включить проверку подлинности пользователя с помощью Azure Active Directory или настроить сертификаты для безопасности приложения, [создайте кластер из шаблона Resource Manager](service-fabric-cluster-creation-via-arm.md).

    Нажмите кнопку **ОК**.

8. Проверьте сводные данные.  Если вы хотите скачать шаблон Resource Manager, построенный из введенных вами параметров, выберите **Скачать шаблон и параметры**.  Выберите **Создать**, чтобы создать кластер.

    Ход создания кластера будет отображаться в области уведомлений. (Щелкните значок колокольчика рядом со строкой состояния в правом верхнем углу экрана). Если при создании кластера вы установили флажок **Закрепить на начальной панели**, то на **начальной доске** вы увидите закрепленный элемент **Deploying Service Fabric Cluster** (Развертывание кластера Service Fabric).

### <a name="view-cluster-status"></a>Просмотр сведений о состоянии кластера
После создания кластера его можно просмотреть на портале в колонке **Обзор**. На панели мониторинга отобразятся подробные сведения о кластере, включая общедоступную конечную точку кластера и ссылку на Service Fabric Explorer.

![Состояние кластера][cluster-status]

### <a name="visualize-the-cluster-using-service-fabric-explorer"></a>Визуализация кластера с помощью Service Fabric Explorer
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) — хорошее средство для визуализации кластера и управления приложениями.  Service Fabric Explorer — это служба, выполняющаяся в кластере.  Чтобы получить доступ к этой службе, используйте веб-браузер. Для этого щелкните ссылку **Service Fabric Explorer** на странице **обзора** кластера.  Вы также можете ввести адрес прямо в браузер [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)

На панели мониторинга кластера представлены общие сведения о кластере, включая общие сведения о приложении и работоспособности узла кластера. В представлении "Узлы" отображается физическая структура кластера. Для каждого узла можно просмотреть, какие приложения были развернуты на этом узле

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-to-the-cluster-using-powershell"></a>Подключение к кластеру с помощью PowerShell
Убедитесь, что кластер работает, подключившись к нему с помощью PowerShell.  Модуль PowerShell ServiceFabric установлен вместе с [пакетом SDK для Service Fabric](service-fabric-get-started.md).  Подключитесь к кластеру, используя командлет [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps).   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
Примеры других способов подключения к кластеру см. в статье о [безопасном подключении к кластеру](service-fabric-connect-to-secure-cluster.md). После подключения к кластеру используйте командлет [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps), чтобы отобразить список узлов в кластере и сведения о состоянии каждого узла. **Состояние работоспособности** каждого узла должно иметь значение *ОК*.

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-the-cluster"></a>Удаление кластера
Кластер Service Fabric состоит из многих других ресурсов Azure помимо собственно ресурса кластера. Чтобы полностью удалить кластер Service Fabric, необходимо также удалить все ресурсы, из которых он состоит. Чтобы удалить кластер и все ресурсы, который он использует, проще всего удалить группу ресурсов. Чтобы узнать о других способах удаления кластера и некоторых (не всех) ресурсов в группе ресурсов, см. сведения об [удалении кластера](service-fabric-cluster-delete.md).

Удаление группы ресурсов на портале Azure
1. Перейдите к нужному кластеру Service Fabric.
2. Щелкните имя **группы ресурсов** на странице основных компонентов кластера.
3. На странице **основных компонентов группы ресурсов** щелкните **Удалить группу ресурсов** и выполните приведенные далее инструкции, чтобы завершить удаление группы ресурсов.
    ![Удаление группы ресурсов][cluster-delete]


## <a name="use-azure-powershell-to-deploy-a-secure-cluster"></a>Развертывание защищенного кластера с помощью Azure PowerShell
1. Скачайте [модуль Azure PowerShell 4.0 или более поздней версии](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) на компьютер.

2. Откройте окно Windows PowerShell и выполните следующую команду: 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    Должен отобразиться похожий результат:

    ![Список PowerShell][ps-list]

3. Войдите в Azure и выберите подписку, в которой вы хотите создать кластер.

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. Чтобы создать защищенный кластер, выполните следующую команду. Не забудьте настроить параметры. 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also the name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    Команда может выполняться 10–30 минут. Когда она выполнится, отобразятся похожие выходные данные: Они содержат сведения о сертификате, хранилище ключей, в которое он передан, и локальной папке, в которую он скопирован. 

    ![Результат PowerShell][ps-out]

5. Скопируйте все выходные данные и сохраните их в текстовый файл, так как позднее вам понадобится сослаться на него. Запишите следующие сведения из выходных данных. 

    - **CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx
    - **CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10
    - **ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080
    - **ClientConnectionEndpointPort** : 19000

### <a name="install-the-certificate-on-your-local-machine"></a>Установка сертификата на локальном компьютере
  
Чтобы подключиться к кластеру, необходимо установить сертификат в личное хранилище (Мое хранилище) текущего пользователя. 

Выполните эту команду PowerShell:

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\the name of the cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

Теперь все готово для подключения к защищенному кластеру.

### <a name="connect-to-a-secure-cluster"></a>Безопасное подключение к кластеру 

Для подключения к защищенному кластеру выполните следующую команду PowerShell: Сведения о сертификате должны совпадать со сведениями сертификата, с помощью которого настраивался кластер. 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


В следующем примере показано, как настроить параметры: 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Выполните следующую команду, чтобы проверить подключение к кластеру и убедиться, что кластер работает:

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-to-your-cluster-from-visual-studio"></a>Публикация приложений из Visual Studio в кластер

После настройки кластера Azure можно опубликовать приложение из Visual Studio в Azure, следуя инструкциям из статьи о [публикации в кластер Azure](service-fabric-publish-app-remote-cluster.md). 

### <a name="remove-the-cluster"></a>Удаление кластера
Помимо собственных ресурсов кластер содержит другие ресурсы Azure. Чтобы удалить кластер и все ресурсы, который он использует, проще всего удалить группу ресурсов. 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы настроили кластер разработки, перейдите к следующим шагам.
* [Create a secure cluster in the portal](service-fabric-cluster-creation-via-portal.md) (Создание безопасного кластера на портале)
* [Create a cluster from a template](service-fabric-cluster-creation-via-arm.md) (Создание кластера из шаблона) 
* [Разверните приложения с помощью PowerShell](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
