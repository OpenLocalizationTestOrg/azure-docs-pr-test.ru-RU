---
title: "aaaSet кластера Azure Service Fabric | Документы Microsoft"
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
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a>Создание первого кластера Service Fabric в Azure
[Кластер Service Fabric](service-fabric-deploy-anywhere.md) — это подключенный к сети набор виртуальных машин или физических компьютеров, в котором вы развертываете микрослужбы и управляете ими. Это краткое руководство поможет вам toocreate пяти кластера из узла, ОС Windows или Linux, через hello [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) или [портал Azure](http://portal.azure.com) через несколько минут.  

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.


## <a name="use-hello-azure-portal"></a>Использовать hello портал Azure

Вход toohello портал Azure по адресу [http://portal.azure.com](http://portal.azure.com).

### <a name="create-hello-cluster"></a>Создание кластера hello

1. Нажмите кнопку hello **New** кнопка найдена в верхнем левом углу hello hello портал Azure.
2. Выберите **вычислений** из hello **New** и затем выберите **кластера Service Fabric** из hello **вычислений** колонку.
3. Заполните hello Service Fabric **основы** формы. Для **операционной системы**выберите hello версией Windows или Linux, нужно hello toorun узлов кластера. Hello имя пользователя и пароль, введенный здесь — используется toolog toohello виртуальной машине. Создайте **группу ресурсов**. Группа ресурсов — это логический контейнер, в котором происходит создание ресурсов Azure и коллективное управление ими. По завершении нажмите кнопку **ОК**.

    ![Результат установки кластера][cluster-setup-basics]

4. Заполните hello **конфигурации кластера** формы.  Для параметра **Число типа узлов** введите значение "1".

5. Выберите **тип узла (первичный) 1** и заполнить hello **конфигурации узла типа** формы.  Укажите имя типа узла и установите hello [уровень устойчивости](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) слишком «бронзового.»  Выберите размер виртуальной машины.

    Размер виртуальной Машины hello, количество виртуальных машин, пользовательские конечные точки определяют типы узлов и других параметров для hello виртуальных машин данного типа. Каждый определенный тип узел настроен как набор масштабирования отдельной виртуальной машине — как набор используемых toodeploy и управляемых виртуальных машин. Каждый тип узла поддерживает возможность независимого масштабирования, имеет разные наборы открытых портов и собственные метрики емкости.  Hello первой или основной, тип узла — где размещаются Service Fabric системных служб и должен иметь пять или более виртуальных машин.

    Для любой рабочей развернутой службы важным шагом является [планирование загрузки](service-fabric-cluster-capacity.md).  Так как в этом кратком руководстве вы не будете выполнять приложения, вы можете выбрать размер виртуальной машины *DS1_v2 Standard*.  Выберите «Серебряный» для hello [уровень надежности](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) и начального набора масштабирования виртуальных машин емкость 5.  

    Пользовательские конечные точки открыть порты в подсистеме балансировки нагрузки Azure hello, что позволяет подключаться с приложениями, работающими на кластере hello.  Введите «80, 8172» tooopen порты 80 и 8172.

    Не устанавливайте hello **Настройка дополнительных параметров** поле, которое используется для настройки конечных точек управления TCP или HTTP, диапазонов портов приложения, [ограничения размещения](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), и [емкости свойства](service-fabric-cluster-resource-manager-metrics.md).    

    Нажмите кнопку **ОК**.

6. В hello **конфигурации кластера** задайте **диагностики** слишком**на**.  Для краткого руководства, нет необходимости tooenter любое [структуры параметр](service-fabric-cluster-fabric-settings.md) свойства.  В **версия Fabric**выберите **автоматического** режим обновления, чтобы корпорация Майкрософт автоматически обновляет версию hello hello структуры работающего кластера hello.  Установить режим hello слишком**вручную** Если требуется слишком[выберите поддерживаемую версию](service-fabric-cluster-upgrade.md) tooupgrade для. 

    ![Конфигурация типа узла][node-type-config]

    Нажмите кнопку **ОК**.

7. Заполните hello **безопасности** формы.  Для этого руководства выберите **незащищенный** режим.  Это настоятельно рекомендуется toocreate безопасного кластера для рабочих нагрузок, тем не менее, поскольку любой пользователь может анонимно подключения tooan небезопасные кластера и выполнять операции управления.  

    Сертификаты используются в Service Fabric tooprovide проверки подлинности и шифрования toosecure различные аспекты кластера и его применения. Дополнительные сведения о том, как сертификаты используются в Service Fabric, см. в статье [Сценарии защиты кластера Service Fabric](service-fabric-cluster-security.md).  Использование Azure Active Directory или tooset сертификаты для обеспечения безопасности приложения, проверка подлинности пользователя tooenable [создания кластера из шаблона диспетчера ресурсов](service-fabric-cluster-creation-via-arm.md).

    Нажмите кнопку **ОК**.

8. Просмотрите hello сводки.  Если вы хотите toodownload введено шаблона диспетчера ресурсов, построенная hello параметры, выберите **загрузки шаблона и параметров**.  Выберите **создать** toocreate hello кластера.

    Вы увидите ход создания hello в уведомлениях hello. (Щелкните значок колокольчика «hello» рядом с hello строку состояния в hello верхнем правом углу экрана.) Если вы нажали кнопку **tooStartboard ПИН-код** при создании кластера hello, см **развертывание кластера Service Fabric** закрепленные toohello **запустить** доски.

### <a name="view-cluster-status"></a>Просмотр сведений о состоянии кластера
После создания кластера можно проверить кластер на hello **Обзор** колонке hello портала. Теперь можно просмотреть сведения hello кластера на панели мониторинга hello, включая общедоступную конечную точку кластера hello и ссылка tooService Fabric Explorer.

![Состояние кластера][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>Визуализация hello кластера с помощью обозревателя Service Fabric
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) — хорошее средство для визуализации кластера и управления приложениями.  Обозреватель Service Fabric — это служба, запускаемую в кластере hello.  Доступ к ним через веб-браузер, нажав кнопку hello **Service Fabric Explorer** связь кластера hello **Обзор** портале hello.  Можно также ввести адрес hello непосредственно в браузер hello: [http://quickstartcluster.westus.cloudapp.azure.com:19080/обозреватель](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)

панели мониторинга кластера Hello Обзор кластера, в том числе сводную приложения и состояние работоспособности узла. представление узла Hello отображает hello физическую структуру hello кластера. Для каждого узла можно просмотреть, какие приложения были развернуты на этом узле

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a>Подключите кластер toohello с помощью PowerShell
Убедитесь, что данный кластер hello выполняется путем подключения с помощью PowerShell.  Hello модуля ServiceFabric PowerShell устанавливается вместе с hello [пакет Service Fabric SDK](service-fabric-get-started.md).  Hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлет устанавливает toohello подключения кластера.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
В разделе [кластера безопасное подключение tooa](service-fabric-connect-to-secure-cluster.md) другие примеры соединения tooa кластера. После подключения кластера toohello, используйте hello [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay командлет список узлов в hello сведения о кластере и состоянии для каждого узла. **Состояние работоспособности** каждого узла должно иметь значение *ОК*.

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

### <a name="remove-hello-cluster"></a>Удаление кластера hello
Кластер Service Fabric состоит из других ресурсов Azure в дополнение к этому toohello сам ресурс кластера. Поэтому toocompletely Удаление кластера Service Fabric требуется также toodelete Здравствуйте, все ресурсы, которые оно состоит из. Hello простейший способ toodelete hello кластера и все ресурсы hello, которые он использует является группой ресурсов toodelete hello. Для других способов toodelete кластера или toodelete некоторых (но не всех) hello ресурсы в группе ресурсов см. [удалить кластер](service-fabric-cluster-delete.md)

Удаление группы ресурсов в hello портала Azure:
1. Переход кластера Service Fabric toohello требуется toodelete.
2. Нажмите кнопку hello **группы ресурсов** имя на странице essentials hello кластера.
3. В hello **Essentials группы ресурсов** щелкните **удалить группу ресурсов** и следуйте появляющимся hello на этой странице toocomplete hello удаления группы ресурсов hello.
    ![Удаление группы ресурсов hello][cluster-delete]


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a>Использование Azure Powershell toodeploy безопасности кластера
1. Загрузите hello [Azure Powershell 4.0 или более поздней версии модуля](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) на компьютере.

2. Откройте окно Windows PowerShell, hello выполнить следующую команду. 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    Должны появиться следующие выходные данные как toohello.

    ![Список PowerShell][ps-list]

3. TooAzure входа и toocreate hello кластеру toowhich подписки выберите hello

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. Выполнения hello, следующая команда toonow создания безопасного кластера. Не забудьте toocustomize hello параметров. 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    Команда Hello может занять от toocomplete минут too30 10 минут hello конец, вы должны получить следующие выходные данные как toohello. сведения о сертификате hello, hello KeyVault, где был загружен, и hello локальную папку, куда копируется сертификат hello Hello вывода. 

    ![Результат PowerShell][ps-out]

5. Копировать все выходные данные hello и сохраните текстовый файл tooa образом toorefer tooit. Запишите следующие сведения из выходных данных hello hello. 

    - **CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx
    - **CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10
    - **ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080
    - **ClientConnectionEndpointPort** : 19000

### <a name="install-hello-certificate-on-your-local-machine"></a>Установите сертификат hello на локальном компьютере
  
кластер toohello tooconnect, потребуется tooinstall hello сертификат в хранилище персональных (Мои) hello hello текущего пользователя. 

Запустите следующие PowerShell hello

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

Теперь вы находитесь кластера безопасных готовы tooconnect tooyour.

### <a name="connect-tooa-secure-cluster"></a>Подключите кластер безопасного tooa 

Запустите следующие hello PowerShell команды tooconnect tooa безопасности кластера. сведения о сертификате Hello должно соответствовать сертификат, который был используется tooset hello кластера. 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


Следующий пример показывает hello Hello завершено параметров: 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Запустите hello, выполнив команду toocheck, что вы подключены и hello кластера находится в работоспособном состоянии.

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a>Публикация кластера tooyour приложения из Visual Studio

Теперь, когда вы настроили кластер Azure, можно опубликовать tooit вашего приложения из Visual Studio по следующей hello [кластера tooan публикации](service-fabric-publish-app-remote-cluster.md) документа. 

### <a name="remove-hello-cluster"></a>Удаление кластера hello
Кластер состоит из других ресурсов Azure в дополнение к этому toohello сам ресурс кластера. Hello простейший способ toodelete hello кластера и все ресурсы hello, которые он использует является группой ресурсов toodelete hello. 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы настроили кластеру разработки, попробуйте hello следующее:
* [Создание безопасного кластера на портале hello](service-fabric-cluster-creation-via-portal.md)
* [Create a cluster from a template](service-fabric-cluster-creation-via-arm.md) (Создание кластера из шаблона) 
* [Разверните приложения с помощью PowerShell](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
