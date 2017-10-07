---
title: "узлы кластера HPC Pack aaaAutoscale | Документы Microsoft"
description: "Автоматически увеличиваться и уменьшаться hello число вычислительными узлами кластера HPC Pack в Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a>Автоматически увеличиваться и уменьшаться hello ресурсы кластера HPC Pack в Azure, в соответствии с toohello рабочая нагрузка кластера
Если выполняется развертывание узлов «Повышения» Azure в кластере HPC Pack или создать кластер пакета HPC на виртуальных машинах Azure, вы можете способ автоматического увеличения или сжатия hello ресурсы кластера, например узлов или ядер согласно hello рабочей нагрузки в кластере hello. Масштабирование ресурсов кластера hello таким образом позволяет toouse ресурсам Azure более эффективно и управлять их стоимостью.

В этой статье показано два способа HPC Pack предоставляет tooautoscale вычислительные ресурсы:

* Свойство кластера HPC Pack Hello **AutoGrowShrink**

* Hello **AzureAutoGrowShrink.ps1** скрипт HPC PowerShell

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

В настоящее время можно автоматически увеличивать и сжимать только вычислительные узлы пакета HPC под управлением ОС Windows Server.


## <a name="set-hello-autogrowshrink-cluster-property"></a>Задайте для свойства кластера AutoGrowShrink hello
### <a name="prerequisites"></a>Предварительные требования

* **HPC Pack 2012 R2 с обновлением 2 или более поздней версии кластера** -hello головной узел кластера может быть развернут локально или на виртуальной Машине Azure. В разделе [Настройка гибридного кластера с помощью пакета HPC](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget работы с локальной головного узла и узлы «Повышения» Azure. В разделе hello [скрипт развертывания IaaS пакета HPC](hpcpack-cluster-powershell-script.md) tooquickly развертывание кластера HPC Pack на виртуальных машинах Azure.

* **Для кластера с головным узлом в Azure (модель развертывания Resource Manager)**. Начиная с версии пакета HPC 2016 аутентификация сертификата в приложении Azure Active Directory используется для автоматического увеличения и сжатия виртуальных машин кластера, развернутых с помощью Azure Resource Manager. Настройте сертификат следующим образом:

  1. После развертывания кластера подключитесь с удаленного рабочего стола tooone головного узла.

  2. Отправка hello сертификата (в формате PFX с закрытым ключом) tooeach головного узла и установите tooCert:\LocalMachine\My и Cert: \LocalMachine\Root.

  3. Запустите Azure PowerShell с правами администратора и выполните следующие команды на один головной узел hello:

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    Если ваша учетная запись находится в более чем одного клиента Azure Active Directory или подписки Azure, можно запустить следующие hello команд tooselect hello правильный клиента и подписки:
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    Запустите следующие команды tooview hello hello выбранного клиента и подписки:
    
    ```powershell
        Get-AzureRMContext
    ```

  4. Запустите следующий сценарий hello

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    где:

    **DisplayName** — отображаемое имя активного приложения Azure. Если приложение hello не существует, он создается в Azure Active Directory.

    **Домашняя страница** -hello Домашняя страница приложения hello. Вы можете настроить пустой URL-адрес, как предшествующий пример hello.

    **IdentifierUri** -идентификатор приложения hello. Вы можете настроить пустой URL-адрес, как предшествующий пример hello.

    **CertificateThumbprint** -отпечаток сертификата hello установлен на головном узле hello в шаге 1.

    **TenantId** — идентификатор клиента каталога Azure Active Directory. Hello идентификатор клиента можно получить с портала Azure Active Directory hello **свойства** страницы.

    Чтобы получить дополнительные сведения о **ConfigARMAutoGrowShrinkCert.ps1**, выполните `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.


* **Для кластера с головного узла в Azure (классической модели развертывания)** — Если используется кластер hello toocreate скрипт развертывания hello IaaS пакета HPC в hello классической модели развертывания, включите hello **AutoGrowShrink** кластера свойство, задав параметр AutoGrowShrink hello в файле конфигурации кластера hello. Дополнительные сведения см. в разделе документации hello hello [сценарий загрузки](https://www.microsoft.com/download/details.aspx?id=44949).

    Кроме того, включите hello **AutoGrowShrink** свойство кластера после развертывания hello кластера с помощью HPC PowerShell команд, описанных в следующем разделе hello. tooprepare для этого первого полного hello следующие шаги:

  1. Настройка сертификата управления Azure на головном узле hello и hello подписки Azure. Для тестирования развертывания можно использовать самозаверяющий сертификат по умолчанию Microsoft HPC Azure hello, который устанавливает пакета HPC на головном узле hello и затем отправьте этот сертификат tooyour подписки Azure. Параметры и инструкции см. в разделе hello [библиотеки TechNet рекомендации](https://technet.microsoft.com/library/gg481759.aspx).

  2. Запустите **regedit** на головном узле hello перейдите tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo и добавьте строковое значение. Задайте имя значения hello слишком «Отпечаток» и значение данных toohello отпечаток сертификата hello в шаге 1.

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a>Свойства AutoGrowShrink hello tooset команды HPC PowerShell
Ниже приведены образец HPC PowerShell команды tooset **AutoGrowShrink** и tootune его поведения, используя дополнительные параметры. В разделе [AutoGrowShrink параметры](#AutoGrowShrink-parameters) далее в этой статье для hello полный список параметров.

toorun эти команды, запустите HPC PowerShell на головном узле кластера hello с правами администратора.

**hello tooenable AutoGrowShrink свойство**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

**hello toodisable AutoGrowShrink свойство**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

**toochange hello расти интервал в минутах**

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

**toochange hello уменьшить интервал в минутах**

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

**tooview hello AutoGrowShrink в текущей конфигурации**

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

**группы узлов tooexclude из AutoGrowShrink**

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> Этот параметр поддерживается, начиная с версии пакета HPC 2016.
>

### <a name="autogrowshrink-parameters"></a>Параметры AutoGrowShrink
Hello ниже приведены параметры AutoGrowShrink, которые можно изменить с помощью hello **HpcClusterProperty набора** команды.

* **EnableGrowShrink** - переключение tooenable или отключить hello **AutoGrowShrink** свойство.
* **ParamSweepTasksPerCore** -количество параметрической очистки задач toogrow одного ядра. по умолчанию Hello — одно ядро toogrow каждой задачи.

  > [!NOTE]
  > Изменения HPC Pack QFE KB3134307 **ParamSweepTasksPerCore** слишком**TasksPerResourceUnit**. Он основан на типе ресурса задания hello и может быть узел, сокета или core.
  >
  >
* **GrowThreshold** -пороговое значение автоматического увеличения tootrigger задач в очереди. по умолчанию Hello-1, это означает, что если 1 или более задач в hello в очереди состояний, автоматически увеличивать размер узлов.
* **GrowInterval** -интервал в минутах tootrigger автоматическое приращение. Интервал по умолчанию Hello составляет 5 минут.
* **ShrinkInterval** -интервал в минутах tootrigger автоматическое сжатие. Интервал по умолчанию Hello составляет 5 минут. |
* **ShrinkIdleTimes** -количество непрерывных проверок tooshrink tooindicate hello узлов бездействуют. по умолчанию Hello-3 раза. Например, если hello **ShrinkInterval** 5 минут, пакет HPC проверяет, является ли узел hello простоя каждые 5 минут. Если узлы hello в состояние бездействия hello после 3 непрерывных проверок (15 минут), пакет HPC сжимает этого узла.
* **ExtraNodesGrowRatio** -дополнительных процент toogrow узлы для заданий интерфейса передачи сообщений (MPI). значение по умолчанию Hello-1, означающее HPC Pack роста узлы % 1 для заданий MPI.
* **GrowByMin** -переключение tooindicate ли политика автоматического увеличения hello основан на hello минимальные ресурсы, необходимые для задания hello. по умолчанию Hello равно false, что означает, что пакет HPC увеличился узлов для задания в соответствии с hello максимальное ресурсы, необходимые для задания hello.
* **SoaJobGrowThreshold** -пороговое значение входящих SOA запросов tootrigger hello автоматическое увеличение процесса. значение по умолчанию Hello — 50 000.

  > [!NOTE]
  > Этот параметр поддерживается, начиная с версии пакета HPC 2012 R2 с обновлением 3.
  >
  >
* **SoaRequestsPerCore** -количество входящих SOA запросов toogrow одного ядра. значение по умолчанию Hello — 20000.

  > [!NOTE]
  > Этот параметр поддерживается, начиная с версии пакета HPC 2012 R2 с обновлением 3.
  >
* **ExcludeNodeGroups** — узлы в hello указаны группы узлов автоматически увеличиваться и уменьшаться.
  
  > [!NOTE]
  > Этот параметр поддерживается, начиная с версии пакета HPC 2016.
  >

### <a name="mpi-example"></a>Пример MPI
По умолчанию пакет HPC увеличивается на 1% дополнительные узлы для заданий MPI (**ExtraNodesGrowRatio** имеет значение too1). Hello причина заключается в том, что MPI может потребоваться несколько узлов и hello задание можно запустить только в том случае, когда готовы все узлы. При запуске узлов Azure иногда одного узла могут потребоваться дополнительные toostart времени, чем другие, вызывая другие узлы toobe простоя во время ожидания для этого узла tooget готовности. Увеличивая размер дополнительных узлов, пакет HPC сокращает это время ожидания ресурса и потенциально сокращает расходы. Процент hello tooincrease дополнительных узлов для заданий MPI (например, too10%), выполнить команду, аналогичную

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a>Пример SOA
По умолчанию **SoaJobGrowThreshold** задано too50000 и **SoaRequestsPerCore** имеет значение too200000. Если отправить одно задание SOA с 70 000 запросов, будет существовать одна задача, поставленная в очередь, и 70 000 входящих запросов. В этом случае пакет HPC роста 1 ядро hello в очереди задач, и для входящих запросов увеличивается (70000 50000) или в общее роста 2 ядра, для этого задания SOA 20000 = 1 core.

## <a name="run-hello-azureautogrowshrinkps1-script"></a>Запустите сценарий AzureAutoGrowShrink.ps1 hello
### <a name="prerequisites"></a>Предварительные требования

* **HPC Pack 2012 R2 с обновлением 1 или более поздней версии кластера** - hello **AzureAutoGrowShrink.ps1** скрипта установлен в папке hello % CCP_HOME % bin. Hello головной узел кластера может быть развернут локально или на виртуальной Машине Azure. В разделе [Настройка гибридного кластера с помощью пакета HPC](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget работы с локальной головного узла и узлы «Повышения» Azure. . В разделе hello [скрипт развертывания IaaS пакета HPC](hpcpack-cluster-powershell-script.md) tooquickly развертывание кластера HPC Pack на виртуальных машинах Azure или используйте [шаблона Azure краткое руководство](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).
* **Azure PowerShell 1.4.0** -скрипт hello в настоящее время зависит от этой конкретной версии Azure PowerShell.
* **Для кластера с помощью Azure burst узлы** -скрипт hello на клиентском компьютере с установленным пакетом HPC или на головном узле hello. Если выполняется на клиентском компьютере, убедитесь, что вы hello переменной $env: CCP_SCHEDULER toopoint toohello головного узла. Hello узлы «Повышения» Azure должны быть добавлены toohello кластера, но они могут быть в hello не развернутом состоянии.
* **Для кластера, развернутых в виртуальных машинах Azure (модели развертывания диспетчера ресурсов)** -кластер виртуальных машин Azure, развернутых в модели развертывания диспетчера ресурсов hello, скрипт hello поддерживает два метода для проверки подлинности Azure: вход tooyour учетная запись Azure сценарий hello toorun каждый раз (путем запуска `Login-AzureRmAccount`, или настройте tooauthenticate участника службы с сертификатом. Пакет HPC предоставляет сценарий hello **ConfigARMAutoGrowShrinkCert.ps** toocreate участника службы с сертификатом. Hello сценарий создает приложение Azure Active Directory (Azure AD) и субъекта-службы и назначает участника службы toohello роль участника hello. сценарий toorun hello, запустите Azure PowerShell от имени администратора и выполните hello, следующие команды:

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    Чтобы получить дополнительные сведения о **ConfigARMAutoGrowShrinkCert.ps1**, выполните `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.

* **Для кластера, развернутых в виртуальных машинах Azure (классической модели развертывания)** -скрипт hello на hello ВМ головного узла, так как он зависит от hello **Start-HpcIaaSNode.ps1** и **Stop-HpcIaaSNode.ps1**сценарии, которые установлены на ней. Кроме того, эти сценарии требуют сертификат управления Azure или файл параметров публикации (см. статью [Управление вычислительными узлами в кластере на основе пакета HPC в Azure](hpcpack-cluster-node-manage.md)). Убедитесь, что все hello вычислений узел виртуальных машин, необходимо уже добавлены toohello кластера. Они могут находиться в остановленном состоянии hello.



### <a name="syntax"></a>Синтаксис
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a>Параметры
* **NodeTemplates** -имена toodefine шаблоны узла hello hello область для узлов toogrow hello и сжатия. Если не указан (имеет значение по умолчанию hello @()), все узлы в hello **AzureNodes** узел группы находятся в области, если **NodeType** имеет значение AzureNodes, и все узлы в hello **ComputeNodes** узел группы находятся в области, когда **NodeType** имеет значение ComputeNodes.
* **JobTemplates** -имена hello задания области hello toodefine шаблоны для узлов toogrow hello.
* **NodeType** — тип узла toogrow hello и сжатия. Поддерживаемые значения:

  * **AzureNodes** — для (расширительных) узлов PaaS Azure в локальной среде или в кластере IaaS Azure.
  * **ComputeNodes** — для виртуальных машин вычислительных узлов только в кластере IaaS Azure.

* **NumOfQueuedJobsPerNodeToGrow** -количество заданий в очереди, необходимых toogrow один узел.
* **NumOfQueuedJobsToGrowThreshold** -hello пороговое значение числа заданий в очереди toostart hello увеличиваться процесса.
* **NumOfActiveQueuedTasksPerNodeToGrow** -hello количество активных задач в очереди, необходимых toogrow один узел. Если для **NumOfQueuedJobsPerNodeToGrow** указано значение больше 0, этот параметр пропускается.
* **NumOfActiveQueuedTasksToGrowThreshold** -hello пороговое число активных задач в очереди toostart hello увеличиваться процесса.
* **NumOfInitialNodesToGrow** - hello первоначального минимальное число узлов toogrow, если все узлы hello в области находятся **не развернуто** или **остановлена (освобождена)**.
* **GrowCheckIntervalMins** -hello интервал в минутах между проверяет toogrow.
* **ShrinkCheckIntervalMins** -hello интервал в минутах между проверяет tooshrink.
* **ShrinkCheckIdleTimes** -hello количество проверок непрерывного сжатия (разделенные **ShrinkCheckIntervalMins**) узлов hello tooindicate бездействуют.
* **UseLastConfigurations** -hello предыдущие конфигурации, сохраненные в файле параметров hello.
* **ArgFile**- hello имя toosave файл, используемый аргумент hello и hello конфигураций toorun hello скрипт обновления.
* **LogFilePrefix** -hello префикс имени файла журнала hello. Можно указать путь. По умолчанию hello журнала является письменного toohello текущий рабочий каталог.

### <a name="example-1"></a>Пример 1
Hello следующий пример настраивает hello Azure пакета развертывания с шаблоном AzureNode по умолчанию toogrow узлов и автоматически уменьшается. Если все узлы изначально находятся в hello **не развернуто** состоянии, по крайней мере 3 узлы запущены. Если hello количество заданий в очереди превышает 8, hello сценарий запускает узлы, пока их количество не превышает отношение hello заданий в очереди для **NumOfQueuedJobsPerNodeToGrow**. Если узел найден toobe простоя в 3 раз подряд, он останавливается.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a>Пример 2
Hello следующий пример настраивает hello Azure ВМ вычислительных узлов развернут с toogrow шаблоном ComputeNode по умолчанию hello и автоматически уменьшается.
Hello задания, настроенные с шаблона задания по умолчанию hello определить область hello рабочей нагрузки в кластере hello. Если все узлы hello изначально были остановлены, запускаются по крайней мере 5 узлов. Если hello число активных задач в очереди превышает 15, hello сценарий запускает узлы, пока их количество не превышает отношение активных задач в очереди hello слишком**NumOfActiveQueuedTasksPerNodeToGrow**. Если узел найден toobe бездействия в 10 раз подряд, он останавливается.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
