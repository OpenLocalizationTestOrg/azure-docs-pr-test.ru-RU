---
title: "пакеты приложений aaaInstall на вычислительных узлах - пакетной службы Azure | Документы Microsoft"
description: "Использовать приложение hello пакеты возможность пакетной службы Azure tooeasily управлять несколькими приложениями и версии для установки пакета вычислительных узлов."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a>Развертывание приложений toocompute узлов с пакетами приложения пакета

компонент пакеты приложения Hello пакетной службы Azure предоставляет удобное управление задач приложений и их развертывания toohello вычислительных узлов в пуле. С помощью пакетов приложений можно загрузить и управления несколькими версиями приложения hello запуска задач, включая их вспомогательные файлы. Затем можно автоматически развернуть один или несколько из этих приложений toohello вычислительных узлов в пуле.

В этой статье вы узнаете, как tooupload пакетов приложений в hello портал Azure и управления ими. Затем будет рассмотрено, каким образом tooinstall их в пуле вычислительных узлов с hello [пакета .NET] [ api_net] библиотеки.

> [!NOTE]
> 
> Пакеты приложений поддерживаются во всех пулах пакетной службы, созданных после 5 июля 2017 г. Они поддерживаются в пулах пакета, созданные между 10 марта 2016 г. и 5 июля 2017 г., только в том случае, если пул hello был создан с помощью конфигурации облачной службы. Пакеты приложений не поддерживают пулы пакета, созданные предыдущей too10 марта 2016 г.
>
> Hello API-интерфейсы для создания и управления пакетами приложения являются частью hello [пакет управления .NET] [[api_net_mgmt]] библиотеки. Hello API-интерфейсы для установки пакетов приложений в вычислительном узле являются частью hello [пакета .NET] [ api_net] библиотеки.  
>
> функция пакеты приложения Hello, описанные здесь заменяет функции hello пакет приложений, доступны в предыдущих версиях службы hello.
> 
> 

## <a name="application-package-requirements"></a>Требования к пакетам приложений
пакеты приложений toouse, требуется слишком[связать учетную запись хранилища Azure](#link-a-storage-account) tooyour пакетной учетной записи.

Эта функция появилась в [API REST пакета] [ api_rest] версии 2015-12-01.2.2 и соответствующий hello [пакета .NET] [ api_net] версия библиотеки 3.1.0. Рекомендуется всегда использовать последнюю версию API hello при работе с использованием пакета.

> [!NOTE]
> Пакеты приложений поддерживаются во всех пулах пакетной службы, созданных после 5 июля 2017 г. Они поддерживаются в пулах пакета, созданные между 10 марта 2016 г. и 5 июля 2017 г., только в том случае, если пул hello был создан с помощью конфигурации облачной службы. Пакеты приложений не поддерживают пулы пакета, созданные предыдущей too10 марта 2016 г.
>
>

## <a name="about-applications-and-application-packages"></a>О приложениях и пакетах приложений
В пакете Azure *приложения* ссылается набор tooa версии двоичных файлов, которые могут быть автоматически загружаемые toohello вычислительных узлов в пуле. *Пакета приложения* ссылается tooa *определенный набор* этих двоичных файлов и представляет данного *версии* приложения hello.

![Обзорная схема: приложения и пакеты приложений][1]

### <a name="applications"></a>Приложения
Приложения в пакете содержит один или несколько приложений, пакеты и задает параметры конфигурации для приложения hello. Например приложение может указать tooinstall к версии пакета приложения hello по умолчанию на вычислительные узлы и ли его пакетов могут быть обновлены или удалены.

### <a name="application-packages"></a>Пакеты приложений
Пакет приложения является ZIP-файл, содержащий двоичные файлы приложения hello и вспомогательные файлы, которые требуются для приложения hello toorun задачи. Каждый пакет приложения представляет конкретную версию приложения hello.

Можно указать пакетов приложений на уровнях hello пула и задач. При создании пула или задачи можно указать один или несколько таких пакетов и (при необходимости) версию.

* **Пул пакетов приложений** развертываются слишком*каждого* узла в пуле hello. Развертывание приложений осуществляется во время присоединения узла к пулу, а также когда узел перезагружается или для него пересоздается образ.
  
    Если все узлы в пуле выполняют задачи задания, пакеты приложения уровня пула считаются пригодными. При создании пула можно указать один или несколько пакетов приложений, а также добавить или обновить имеющиеся в пуле пакеты. При обновлении пакетов существующий пул приложений, необходимо перезапустить его tooinstall узлы hello новый пакет.
* **Задача пакетов приложений** развертываются только tooa вычислительном узле запланированные задачи, toorun непосредственно перед запуском задачу hello командной строки. Если указан hello пакета приложения и версии уже находится на узле hello, не развертывается и используется hello существующий пакет.
  
    Пакеты приложений задачи полезны в общий пул средах, где различные задания выполняются на один пул и пул hello не удаляется при завершении задания. Если в задании содержится меньшее количество задач, чем узлы в пуле hello, пакеты приложения задач можно свести к минимуму передачи данных так, как приложение будет развернутой toohello только узлы, выполнять задачи.
  
    Мы также рекомендуем использовать пакеты приложений уровня задач для выполнения небольшого количества задач в сценариях с большими приложениями. Например стадии предварительной обработки или задача слияния, где приложение hello предварительной обработки или слияния является высокой плотности, могут использовать преимущества пакеты задач приложения.

> [!IMPORTANT]
> Существуют ограничения на количество hello приложений и пакетов приложений внутри пакета учетной записи и на размер пакета максимальное приложения hello. В разделе [квоты и лимиты для пакетной службы Azure hello](batch-quota-limit.md) подробные сведения об этих ограничениях.
> 
> 

### <a name="benefits-of-application-packages"></a>Преимущества пакетов приложений
Пакеты приложений можно упростить код hello в пакет решения и нижней hello служебных данных требуется toomanage hello работающих приложений ваших задач.

С пакетами приложения задачи запуска в пуле нет toospecify длинный список отдельных ресурсов tooinstall файлы на узлах hello. У вас нет toomanually управления несколькими версиями файлов приложения в службе хранилища Azure или на узлах. И нет необходимости tooworry о создании [URL-адреса SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide доступ к файлам toohello вашей учетной записи хранилища. Пакетный работает в фоновом режиме hello пакетов приложений toostore хранилища Azure и развертывать их toocompute узлов.

> [!NOTE] 
> Hello общий размер задачи запуска должен быть меньше или равно too32768 символов, включая файлы ресурсов и переменные среды. Если задача запуска превышает это ограничение, то можно воспользоваться пакетами приложений. Можно также создать ZIP-архив, содержащий файлы ресурсов, передать его как tooAzure BLOB-объекта хранилища и затем распакуйте его из командной строки hello вашей задачи запуска. 
>
>

## <a name="upload-and-manage-applications"></a>Передача приложений и управление ими
Можно использовать hello [портал Azure] [ portal] или hello [пакета управления .NET](batch-management-dotnet.md) пакетов приложений библиотеки toomanage hello в вашей учетной записи пакета. Здравствуйте рядом в нескольких разделах, сначала отобразить как toolink учетную запись хранилища, затем приводятся добавления приложений и пакетов и управления ими с помощью hello портала.

### <a name="link-a-storage-account"></a>Связывание учетной записи хранения
toouse пакетов приложений, необходимо сначала связать tooyour учетной записи хранилища Azure пакетной учетной записи. Если учетная запись хранения еще не настроен, hello Azure портал отображает hello предупреждение первом нажатии hello **приложений** плитки в hello **учетная запись пакетной службы** колонку.

> [!IMPORTANT]
> В настоящее время пакета поддерживает *только* hello **общего назначения** тип учетной записи хранения, как описано в шаге 5, [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account)в [о Azure учетные записи хранения](../storage/common/storage-create-storage-account.md). При связывании tooyour учетной записи хранилища Azure пакетной учетной записи, связать *только* **общего назначения** учетной записи хранилища.
> 
> 

![Предупреждение "Нет настроенной учетной записи хранения" на портале Azure][9]

Hello пакетной службы использует hello связанные toostore учетной записи хранилища пакетов приложений. После привязки hello две учетные записи, пакет можно автоматически развертывать hello пакеты, хранимые в связанной hello хранилища учетной записи tooyour вычислительных узлов. toolink tooyour учетной записи хранилища пакетной учетной записи, нажмите кнопку **параметры учетной записи хранилища** на hello **предупреждение** и, при необходимости нажмите кнопку **учетной записи хранилища** на hello **Учетной записи хранилища** колонку.

![Выбор колонки учетной записи хранения на портале Azure][10]

Мы рекомендуем создать учетную запись хранения *специально* для учетной записи пакетной службы и выбрать ее здесь. Дополнительные сведения о том, как toocreate учетную запись хранилища, в разделе «Создание учетной записи хранения» в [учетные записи о хранилище Azure](../storage/common/storage-create-storage-account.md). После создания учетной записи хранилища, можно затем связать его tooyour пакетной учетной записи с помощью hello **учетной записи хранилища** колонку.

> [!WARNING]
> Hello пакетная служба использует toostore хранилища Azure пакеты приложения в качестве блочных больших двоичных объектов. Вы являетесь [взимается плата в обычном режиме] [ storage_pricing] для данных большого двоичного объекта блока hello. Убедиться, что размер tooconsider hello и количество пакетов приложения и периодически удалять устаревшие пакеты toominimize затраты.
> 
> 

### <a name="view-current-applications"></a>Просмотр текущих приложений
tooview приложения hello в учетной записи пакета щелкните hello **приложений** пункта меню в левом меню hello во время просмотра hello **учетная запись пакетной службы** колонку.

![Элемент "Приложения"][2]

При выборе этого параметра меню открывается hello **приложений** колонки:

![Список приложений][3]

Hello **приложений** колонке отображает hello идентификатор каждого приложения в вашей учетной записи и hello следующие свойства:

* **Пакеты**: hello номер версии, связанные с этим приложением.
* **Версия по умолчанию**: версия приложения hello установлены, если версия не указана при указании приложения hello в пуле. Это необязательный параметр.
* **Разрешить обновления**: hello значение, указывающее, является ли пакет обновления, удаления и дополнения разрешены. Если это значение задано слишком**нет**, пакет обновления и удаления для приложения hello отключены. Вы сможете только добавлять новые версии пакета приложения. по умолчанию Hello — **Да**.

### <a name="view-application-details"></a>Просмотр сведений о приложении
tooopen hello колонки, включая данные о hello для приложения hello приложения, выберите в hello **приложений** колонку.

![Сведения о приложении][4]

В колонке сведений приложения hello можно настроить следующие параметры для приложения hello.

* **Разрешить обновления**: возможность обновления и удаления пакетов приложений. См. раздел "Обновление или удаление пакета приложения" ниже.
* **Версия по умолчанию**: укажите toocompute узлы toodeploy пакета по умолчанию приложения.
* **Отображаемое имя**: укажите понятное имя, которое пакет решения можно использовать при отображении сведений о приложении hello, например, в hello пользовательского интерфейса, которые предоставляют tooyour клиентов с помощью пакетной службы.

### <a name="add-a-new-application"></a>Добавление нового приложения
toocreate нового приложения, добавьте пакет приложения и укажите приложения новый, уникальный идентификатор. Hello первого приложения пакета, добавлении с новым Идентификатором приложения hello также создает новое приложение hello.

Нажмите кнопку **добавить** на hello **приложений** hello колонке tooopen **новое приложение** колонку.

![Колонка "Новое приложение" на портале Azure][5]

Hello **новое приложение** колонке предоставляет следующие hello полей параметры hello toospecify новое приложение и пакет приложения.

**Идентификатор приложения**

Это поле указывает идентификатор hello нового приложения, являющегося правила проверки стандартный идентификатор пакета Azure toohello субъекта. Ниже приведены правила Hello для предоставления идентификатора приложения:

* На узлах Windows hello идентификатор может содержать любое сочетание буквенно-цифровые символы, дефисы и знаки подчеркивания. На узлах Linux допускаются только буквенно-цифровые знаки и символы подчеркивания.
* Не может содержать более 64 символов.
* Должно быть уникальным в пределах hello пакетной учетной записи.
* Не меняет и не учитывает регистр.

**Версия**

Это поле указывает hello версии пакета приложения hello, которые вы отправляете. Строки версии приведены toohello субъекта правилам проверки.

* На узлах Windows hello версии строка может содержать любое сочетание буквенно-цифровые символы, дефисы, подчеркивания и точки. На узлах Linux hello версии строка может содержать только буквы, цифры и знаки подчеркивания.
* Не может содержать более 64 символов.
* Должно быть уникальным в пределах приложения hello.
* Не меняет и не учитывает регистр.

**Пакет приложения**

Это поле указывает hello ZIP-файл, содержащий двоичные файлы приложения hello и вспомогательные файлы, необходимые tooexecute приложения hello. Нажмите кнопку hello **выберите файл** поле или hello tooand toobrowse значок папки выберите ZIP-файл, содержащий файлы приложения.

После выбора файла, нажмите кнопку **ОК** toobegin hello передачи tooAzure хранилища. После завершения операции отправки hello hello портал отображает уведомление и закрывает hello колонку. В зависимости от размера hello файла hello, отправка и hello скорость сетевого подключения эта операция может занять некоторое время.

> [!WARNING]
> Не закрывайте hello **новое приложение** колонке до завершения операции отправки hello. Это останавливает процесс передачи hello.
> 
> 

### <a name="add-a-new-application-package"></a>Добавление нового пакета приложения
tooadd новой версии пакета приложения для существующего приложения, откройте приложение в hello **приложений** колонка, щелкните **пакетов**, нажмите кнопку **добавить** tooopen Hello **добавить пакет** колонку.

![Колонка "Добавление пакета приложения" на портале Azure][8]

Как видите, hello полей совпадают с hello **новое приложение** колонки, но hello **идентификатор приложения** поле отключено. Как и для нового приложения hello, укажите hello **версии** для нового пакета, Обзор tooyour **пакета приложения** .zip файла, после чего нажмите кнопку **ОК** tooupload hello пакет.

### <a name="update-or-delete-an-application-package"></a>Обновление или удаление пакета приложения
tooupdate или удалить существующий пакет приложения, откройте hello колонке сведения для приложения hello, нажмите кнопку **пакетов** tooopen hello **пакетов** колонке щелкните hello **многоточие**в строке приветствия пакета приложения hello, toomodify и выберите требуемый tooperform действие hello.

![Обновление или удаление пакета на портале Azure][7]

**Блокировка изменений**

При нажатии кнопки **обновление**, hello *обновление* колонке отображается. Эта колонка находится аналогичные toohello *новый пакет приложения* колонки, однако только поле выбора пакета hello включен, позволяя toospecify новый tooupload файла ZIP.

![Колонка "Обновление пакета" на портале Azure][11]

**Удалить**

При нажатии кнопки **удалить**, будет предложено удаление hello tooconfirm версия пакета hello и пакетные удаления hello пакет из хранилища Azure. При удалении версии по умолчанию hello приложения hello **версия по умолчанию** удалить параметр для приложения hello.

![Удаление приложения][12]

## <a name="install-applications-on-compute-nodes"></a>Установка приложений на вычислительных узлах
Теперь, когда вы узнали, как приложение toomanage пакетов с hello портал Azure, рассмотрим, как toodeploy их toocompute узлов и запускать их с пакетные задачи.

### <a name="install-pool-application-packages"></a>Установка пакетов приложений уровня пула
tooinstall пакета приложения на всех вычислительных узлов в пуле, укажите один или несколько пакетов приложений *ссылки* hello в пуле. пакеты приложения Hello, указываемые в пуле устанавливаются на каждом вычислительном узле, когда этот узел будет присоединен пула hello и при узел hello перезагрузки или повторного создания образа.

В .NET пакетной службы укажите одно или несколько свойств [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] для нового пула во время создания или для имеющегося пула. Hello [ApplicationPackageReference] [ net_pkgref] класс указывает идентификатор приложения и версии tooinstall в пуле вычислительных узлов.

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> Если какой-либо причине произошел сбой развертывания пакета приложения, знаков обслуживания пакетного hello hello узел [непригодным для использования][net_nodestate], и никакие задачи, планируются на выполнение на этом узле. В этом случае следует **перезапустите** hello узел tooreinitiate hello пакета развертывания. Перезапускать hello узла также позволяет повторно планированием задач на узле hello.
> 
> 

### <a name="install-task-application-packages"></a>Установка пакетов приложений уровня задач
Аналогичные tooa пула, укажите пакет приложения *ссылки* для задачи. Если задача становится запланированных toorun на узле, пакет hello загрузку и извлечение непосредственно перед выполнением задачи hello командной строки. Если указанный пакет и версию уже установлен на узле hello, hello пакет не загружается и используется существующий пакет hello.

tooinstall задач пакета приложения, настроить задачу hello [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] свойства:

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-hello-installed-applications"></a>Выполнение приложений установлены hello
Hello пакеты, которые вы указали для пула или задачи загрузили и извлекли tooa с именем каталога в hello `AZ_BATCH_ROOT_DIR` hello узла. Пакет также создается переменная среды, которая содержит каталог с именем toohello путь hello. Командные строки вашей задачи использовать эту переменную среды, при ссылке на приложение hello на узле hello. 

На узлах Windows hello переменная будет попадать в hello следующий формат:

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

На узлах Linux формат hello немного отличается. Точки (.), дефисы (-) и символом решетки (#) — это плоский toounderscores в переменной среды hello. Например:

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

`APPLICATIONID`и `version` — это значения, которые соответствуют toohello приложения и версия пакета, указанного для развертывания. Например, если указано, версии 2.7 приложения *blender* должен быть установлен на узлах Windows вашей задачи командные строки использовать этот tooaccess переменной среды ее файлы:

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

На узлах Linux Укажите переменную среды hello в следующем формате:

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

При передаче пакета приложения, можно указать, по умолчанию версии toodeploy tooyour вычислительных узлов. Если указана версия по умолчанию для приложения, можно опустить суффикса версии hello при ссылке на приложение hello. Можно указать версию приложения по умолчанию hello в hello портал Azure, в колонке приложения hello, как показано в [отправка и управление приложениями](#upload-and-manage-applications).

Например, если указать «2.7» hello версия по умолчанию для приложения *blender*, задачам ссылаться hello следующая переменная среды, затем узлы Windows будет выполняться версии 2.7:

`AZ_BATCH_APP_PACKAGE_BLENDER`

Hello следующий фрагмент кода показывает пример задачи командной строки, запускающей версия по умолчанию hello hello *blender* приложения:

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> В разделе [параметры среды для задачи](batch-api-basics.md#environment-settings-for-tasks) в hello [Обзор возможностей пакетной](batch-api-basics.md) Дополнительные сведения о параметрах среды вычислительного узла.
> 
> 

## <a name="update-a-pools-application-packages"></a>Обновление пакетов приложений пула
Если существующий пул уже был настроен с помощью пакета приложения, можно указать новый пакет для пула hello. При указании новую ссылку пакета для пула применяются следующие hello.

* Hello пакетная служба устанавливает hello вновь указанного пакета на всех новых узлов, которые присоединиться к пулу hello и на любой существующий узел, перезагрузки или повторного создания образа.
* Вычислительные узлы, которые уже находятся в пуле hello при обновлении ссылки на пакет hello не устанавливают новый пакет приложения hello автоматически. Эти вычисляемые узлов должны быть перезагружены или Модернизированные tooreceive hello новый пакет.
* При развертывании нового пакета hello создать переменные среды отражают hello новые ссылки пакета приложения.

В этом примере hello существующий пул имеет версию 2.7 hello *blender* приложения, настроенного как один из его [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref]. узлы tooupdate hello пул с версией 2.76b, укажите новое [ApplicationPackageReference] [ net_pkgref] с новой версией hello и фиксации изменений hello.

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

Теперь, когда hello новой версии будет настроена, hello пакетная служба устанавливает версию 2.76b tooany *новый* узел присоединяется hello пула. tooinstall 2.76b на узлах hello, *уже* в пуле hello перезагрузки или повторного создания образа их. Обратите внимание, что перезагруженный узлы сохраняют hello файлы из предыдущего пакета развертывания.

## <a name="list-hello-applications-in-a-batch-account"></a>Список приложений hello в пакетную учетную запись
Список приложений hello и их пакетов в пакетную учетную запись можно с помощью hello [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] метод.

```csharp
// List hello applications and their application packages in hello Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a>Заключение
Пакеты приложений, которые могут пригодиться клиентов выберите приложения hello для своей работы и указать точную версию toouse hello при обработке задания с активированным пакетным режимом службы. Может также предоставляют возможность hello для вашего tooupload клиентов и отслеживать своих приложений в службе.

## <a name="next-steps"></a>Дальнейшие действия
* Hello [API REST пакета] [ api_rest] также обеспечивает поддержку toowork пакетов приложений. Пример в статье hello [applicationPackageReferences] [ rest_add_pool_with_packages] элемент в [добавить учетную запись пула tooan] [ rest_add_pool] сведения о том, как toospecify tooinstall пакетов с помощью API-интерфейса REST hello. В разделе [приложений] [ rest_applications] для получения сведений об как tooobtain сведений о приложении с помощью hello API REST пакета.
* Узнайте, как tooprogrammatically [управление учетными записями пакетной службы Azure и квоты, с помощью пакета управления .NET](batch-management-dotnet.md). Hello [пакета управления .NET][api_net_mgmt] библиотеки можно включить функции создания и удаления учетной записи для пакета приложения или службы.

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "Общая схема: пакеты приложений"
[2]: ./media/batch-application-packages/app_pkg_02.png "Элемент "Приложения" на портале Azure"
[3]: ./media/batch-application-packages/app_pkg_03.png "Колонка "Приложения" на портале Azure"
[4]: ./media/batch-application-packages/app_pkg_04.png "Параметры в колонке "Сведения о приложении" на портале Azure"
[5]: ./media/batch-application-packages/app_pkg_05.png "Колонка "Новое приложение" на портале Azure"
[7]: ./media/batch-application-packages/app_pkg_07.png "Пункты "Обновить" и "Удалить" для пакетов на портале Azure"
[8]: ./media/batch-application-packages/app_pkg_08.png "Колонка "Новый пакет приложения" на портале Azure"
[9]: ./media/batch-application-packages/app_pkg_09.png "Предупреждение об отсутствии связанной учетной записи хранения"
[10]: ./media/batch-application-packages/app_pkg_10.png "Выбор колонки учетной записи хранения на портале Azure"
[11]: ./media/batch-application-packages/app_pkg_11.png "Колонка "Обновление пакета" на портале Azure"
[12]: ./media/batch-application-packages/app_pkg_12.png "Диалоговое окно для подтверждения удаления пакета на портале Azure"
