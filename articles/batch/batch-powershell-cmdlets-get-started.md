---
title: "aaaGet работы с PowerShell для пакета Azure | Документы Microsoft"
description: "Краткое введение toohello toomanage ресурсы пакета можно использовать командлеты Azure PowerShell."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: f9ad62c5-27bf-4e6b-a5bf-c5f5914e6199
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3e4d12e9c1e52a5b2db2dd44346edda93b7ef92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a>Управление ресурсами пакетной службы с помощью командлетов PowerShell

С hello командлеты PowerShell Azure пакета, можно выполнять и многие hello скрипт такие же задачи, выполняемые с hello пакетных API, hello портал Azure и hello Azure интерфейс командной строки (CLI). Это краткое введение toohello командлеты можно использовать учетные записи пакетного toomanage и работать с ресурсами пакета пулов, заданий и задач.

Полный список пакета командлетов и синтаксиса подробные командлета см hello [Справочник по командлетам Azure пакета](/powershell/module/azurerm.batch/#batch).

В этой статье описаны командлеты Azure PowerShell 3.0.0. Рекомендуется обновить ваш Azure PowerShell часто tootake преимуществами службы обновления и улучшения.

## <a name="prerequisites"></a>Предварительные требования
Выполните следующие операции toouse Azure PowerShell toomanage hello ресурсы пакета.

* [Установка и настройка Azure PowerShell](/powershell/azure/overview)
* Запустите hello **AzureRmAccount входа** командлет tooconnect tooyour подписки (hello Azure пакетной отгрузки командлеты в модуле Azure Resource Manager hello):
  
    `Login-AzureRmAccount`
* **Зарегистрировать в пространство имен поставщика пакета hello**. Эта операция должна выполнить toobe **один раз для каждой подписки**.
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a>Управление учетными записями пакетной службы и ключами
### <a name="create-a-batch-account"></a>Создание учетной записи Пакетной службы
Командлет **New-AzureRmBatchAccount** создает учетную запись пакетной службы в указанной группе ресурсов. Если у вас еще нет группы ресурсов, создайте его, выполнив hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) командлета. Укажите один из hello Azure областей в hello **расположение** параметр, например «Центральной части США». Например:

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

Создайте учетную запись пакета в группе ресурсов hello, указав имя учетной записи hello в <*account_name*> расположением hello и имя группы ресурсов. Создание учетной записи пакетной hello может занять некоторое время toocomplete. Например:

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> Учетная запись пакетной Hello имя должно быть уникальным toohello регион Azure для группы ресурсов hello, содержать от 3 до 24 символов и использовать только строчные буквы и цифры.
> 
> 

### <a name="get-account-access-keys"></a>Получение ключей доступа к учетной записи
**Get-AzureRmBatchAccountKeys** отображаются hello ключи доступа, связанном с учетной записью пакетной службы Azure. Например выполните следующие tooget hello первичный и вторичный ключи hello учетной записи, которую вы создали hello.

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a>Создание нового ключа доступа
**New-AzureRmBatchAccountKey** создает новый первичный или вторичный ключ учетной записи пакетной службы Azure. В примере toogenerate новый первичный ключ для учетной записи пакета, введите:

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> toogenerate новый вторичный ключ, укажите «Получатель» для hello **KeyType** параметра. У вас tooregenerate hello первичный и вторичный ключи отдельно.
> 
> 

### <a name="delete-a-batch-account"></a>Удаление учетной записи Пакетной службы
**Remove-AzureRmBatchAccount** удаляет учетную запись пакетной службы. Например:

    Remove-AzureRmBatchAccount -AccountName <account_name>

При появлении запроса подтвердите учетную запись tooremove hello. Удаление учетной записи может занять некоторое время toocomplete.

## <a name="create-a-batchaccountcontext-object"></a>Создание объекта BatchAccountContext
с помощью tooauthenticate hello командлеты PowerShell пакета при создании и управлении пакета пулы, заданий, задач, и другие ресурсы, сначала создайте объект BatchAccountContext toostore имя учетной записи и ключи:

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

Можно передать объект BatchAccountContext hello в командлеты, используйте hello **BatchContext** параметра.

> [!NOTE]
> По умолчанию учетная запись hello первичный ключ используется для проверки подлинности, однако можно явно выбрать hello ключа toouse путем изменения объекта BatchAccountContext **KeyInUse** свойство: `$context.KeyInUse = "Secondary"`.
> 
> 

## <a name="create-and-modify-batch-resources"></a>Создание и изменение ресурсов пакетной службы
Использовать командлеты, такие как **New AzureBatchPool**, **New AzureBatchJob**, и **New AzureBatchTask** toocreate ресурсами под учетной записью пакета. Существуют соответствующие **Get -** и **Set -** командлеты tooupdate hello свойств существующих ресурсов и **Remove -** командлеты tooremove ресурсы учетной записи пакета.

При использовании многие из этих командлетов в дополнение toopassing BatchContext объекта, необходима toocreate или передать объекты, содержащие параметры подробные ресурсов, как показано в следующий пример hello. В разделе hello подробную справку по каждому командлету Дополнительные примеры.

### <a name="create-a-batch-pool"></a>Создание пула пакетной службы
При создании или обновлении пула пакета, выберите конфигурацию hello облачной службы или конфигурации виртуальной машины hello для hello операционной системы на hello вычислительных узлов (в разделе [Обзор возможностей пакетной](batch-api-basics.md#pool)). При указании hello конфигурацию облачной службы с одним hello записи образа вычислительных узлов [выпусками гостевых ОС Azure](../cloud-services/cloud-services-guestos-update-matrix.md#releases). При указании hello конфигурации виртуальной машины, можно указать одно из hello поддерживается Linux или виртуальной Машины Windows изображений в hello [виртуальных машин Azure Marketplace][vm_marketplace], или предоставить пользовательский изображение, которое вы подготовили.

При запуске **New AzureBatchPool**, передав объект PSCloudServiceConfiguration или PSVirtualMachineConfiguration hello параметры операционной системы. Например hello следующий командлет создает новый пул пакета с небольших вычислительных узлов размера в hello конфигурацию облачной службы, восстановленных из образа с последней версией операционной системы hello семейства 3 (Windows Server 2012). Здравствуйте, **CloudServiceConfiguration** указывает hello *$configuration* переменной как объект PSCloudServiceConfiguration hello. Hello **BatchContext** параметр указывает, ранее определенную переменную *$context* как объект BatchAccountContext hello.

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

Hello целевое количество вычислительных узлов в новый пул hello определяется по формуле автоматического масштабирования. В этом случае hello формула является просто **$TargetDedicated = 4**, количеству hello вычислительных узлов в пуле hello не более: 4.

## <a name="query-for-pools-jobs-tasks-and-other-details"></a>Запрос на получение сведений о пулах, заданиях, задачах и другой информации
Используйте командлеты, такие как **Get AzureBatchPool**, **Get AzureBatchJob**, и **Get AzureBatchTask** tooquery для сущности, созданные в учетной записи пакета.

### <a name="query-for-data"></a>Запрос данных
Например, используйте **Get AzureBatchPools** toofind пулов. По умолчанию это запросы для всех пулов в рамках учетной записи, при условии, что вы уже хранимые hello объекта BatchAccountContext в *$context*:

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a>Использование фильтра OData
Можно указать фильтр OData с помощью hello **фильтра** toofind параметр hello только объекты, которые вас интересуют. Например, можно найти все пулы с идентификаторами, начинающимися с myPool:

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

Этот способ не такой гибкий, как использование "Where-Object" в локальном конвейере. Однако hello отправку запроса toohello пакетной службы непосредственно, чтобы все Фильтрация происходит на серверной стороне hello, экономя пропускную способность Интернета.

### <a name="use-hello-id-parameter"></a>Используйте параметр идентификатора hello
Фильтр OData альтернативных tooan — toouse hello **идентификатор** параметра. tooquery для конкретного пула с myPool «идентификатор»:

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

Hello **идентификатор** параметр поддерживает поиск полного кода, не подстановочные знаки или OData стиль фильтры.

### <a name="use-hello-maxcount-parameter"></a>Использование параметра MaxCount hello
По умолчанию каждый командлет возвращает максимум 1000 объектов. Если этот предел достигнут, уточнить ваш фильтр toobring обратно меньше объектов либо явно задать максимальное использование hello **MaxCount** параметра. Например:

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

задать верхнюю границу hello tooremove, **MaxCount** too0 или меньше.

### <a name="use-hello-powershell-pipeline"></a>Использовать конвейер PowerShell hello
Командлеты пакета можно использовать hello PowerShell конвейера toosend данных между командлетами. Это имеет тот же эффект, что и при указании параметра, но упрощает работу с несколькими сущностями проще hello.

Например, поиск и вывод всех задач в учетной записи:

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

Перезапуск (перезагрузка) каждого вычислительного узла в пуле:

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a>Управление пакетами приложений
Пакеты приложений предоставляют упрощенный способ toohello приложений toodeploy вычислительных узлов в пулов. Hello командлеты PowerShell для пакета можно отправить и управлять пакетами приложений в вашей учетной записи пакета и развертывание узлов toocompute версии пакета.

**Создайте** приложение:

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

**Добавьте** пакет приложения:

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

Набор hello **версия по умолчанию** для приложения hello:

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

**Выведите список** пакетов приложения:

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

**Удалите** пакет приложения:

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

**Удалите** приложение:

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> Все версии пакета приложения для приложения необходимо удалить перед удалением приложения hello. При попытке toodelete приложение, которое в настоящее время имеет пакетов приложений, вы получите ошибку «Конфликт».
> 
> 

### <a name="deploy-an-application-package"></a>Развертывание пакета приложения
Вы можете указать один или несколько пакетов приложений для развертывания при создании пула. При указании пакета во время создания пула это развернутой tooeach узел в качестве пула соединений hello узла. Кроме того, развертывание пакетов выполняется при перезагрузке узла или пересоздании образа узла.

Укажите hello `-ApplicationPackageReference` параметр при создании пула приложений пакета toohello узлов toodeploy пул, как они присоединиться к пулу hello. Сначала создайте **PSApplicationPackageReference** и настройте его с hello идентификатор и пакета версии приложения необходимо toodeploy toohello пул вычислительных узлов:

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

Теперь создайте пул hello и указать ссылку объекта hello пакета, как hello аргумент toohello `ApplicationPackageReferences` параметр:

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

Можно найти дополнительные сведения о пакетах приложения в [развертывания приложений toocompute узлов с пакетами приложения пакета](batch-application-packages.md).

> [!IMPORTANT]
> Вы должны [связать учетную запись хранилища Azure](#linked-storage-account-autostorage) tooyour пакетной учетной записи toouse пакетов приложений.
> 
> 

### <a name="update-a-pools-application-packages"></a>Обновление пакетов приложений пула
tooupdate приложения hello, назначенные tooan существующий пул, сначала создайте объект PSApplicationPackageReference hello требуемого свойства (Id и пакета версии приложения):

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

Затем получить пул hello из пакета, очистить все существующие пакеты, добавлять нашей новой ссылки на пакет и обновлять hello пакетная служба с новыми настройками пула hello:

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

Теперь вы обновили свойства пула hello в пакетной службе hello. tooactually развертывание hello новый пакет toocompute узлов приложения в пуле hello, тем не менее, необходимо перезапустить или повторного создания образа этих узлов. Чтобы перезапустить каждый узел в пуле, используйте следующую команду:

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> Можно развернуть несколько вычислительных узлов toohello приложения пакеты в пуле. Если вы хотите слишком*добавить* пакета приложения вместо замены hello развернутые пакеты, пропустите hello `$pool.ApplicationPackageReferences.Clear()` строку выше.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
* Подробные сведения о синтаксисе командлетов и их примеры см. в [справке по командлетам пакетной службы Azure](/powershell/module/azurerm.batch/#batch).
* Дополнительные сведения о приложениях и пакеты приложений в пакете см. в разделе [развертывания приложений toocompute узлов с пакетами приложения пакета](batch-application-packages.md).

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/