---
title: "aaaRun задачи, связанные с учетными записями пользователей в пакете Azure | Документы Microsoft"
description: "Настройка учетных записей пользователей для выполнения задач в пакетной службе Azure."
services: batch
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.openlocfilehash: 13d7d76451d89a3cca090c4ef24ed0ed781bbf09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a>Выполнение задач с учетными записями пользователей в пакетной службе

Задача в пакетной службе Azure всегда выполняется с учетной записью пользователя. По умолчанию задачи выполняются со стандартными учетными записями пользователей без разрешений администратора. Как правило, параметров этих учетных записей пользователей по умолчанию достаточно. Для определенных сценариев Однако это полезно toobe учетной записи для пользователя может tooconfigure hello в которой вы хотите toorun задачи. В этой статье рассматриваются типы hello учетных записей пользователей и настройке их для вашего сценария.

## <a name="types-of-user-accounts"></a>Типы учетных записей пользователей

В пакетной службе Azure доступны два типа учетных записей пользователей:

- **Автоматические учетные записи пользователей.** Учетные записи пользователей автоматически являются встроенные учетные записи пользователей, создаваемых автоматически hello пакетной службы. По умолчанию задачи выполняются с автоматической учетной записью пользователя. Вы можете настроить hello спецификации tooindicate задачи, с какой пользователь автоматически должна выполняться задача учетной записи пользователя автоматически. Спецификация автоматического пользователя Hello позволяет toospecify уровня прав hello и область действия учетной записи пользователя автоматически hello, который будет выполняться задача hello. 

- **Именованная учетная запись пользователя.** При создании пула hello, можно указать один или несколько учетных записей пользователей с именем для пула. Каждая учетная запись создается на каждом узле hello пула. В дополнение к этому toohello имя учетной записи, укажите пароль учетной записи пользователя hello, повышение уровня, а также для Linux пулах, hello закрытый ключ SSH. При добавлении задачи, можно указать с именем учетной записи пользователя, с которым должна выполняться эта задача hello.

> [!IMPORTANT] 
> версия обновления пакета Hello 2017 г-01-01.4.0 содержит критические изменения, необходимо обновить ваш код toocall этой версии. Если перенос кода из более старой версии пакета, обратите внимание, что hello **runElevated** свойство больше не поддерживается в клиентских библиотек hello API-интерфейса REST или пакета. Используйте hello новый **Удостоверение_пользователя** свойства задачи toospecify повышение уровня. См. раздел hello [обновление библиотеки клиента последней пакета кода toohello](#update-your-code-to-the-latest-batch-client-library) быстрого инструкции для обновления кода пакета, если вы используете одну из библиотек клиентских hello.
>
>

> [!NOTE] 
> учетные записи пользователей Hello, рассматриваемые в данной статье не поддерживают протокол удаленного рабочего стола (RDP) или Secure Shell (SSH), по соображениям безопасности. 
>
> . в разделе tooconnect tooa узел выполняющегося hello Linux конфигурации виртуальной машины через SSH, [tooa использование удаленного рабочего стола виртуальной Машины Linux в Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md). см. под управлением Windows с помощью протокола RDP, toonodes tooconnect [подключения tooa виртуальной Машины Windows Server](../virtual-machines/windows/connect-logon.md).<br /><br />
> в разделе tooconnect tooa узел выполняющегося hello конфигурацию облачной службы по этому Протоколу, [включить удаленный рабочий стол для роли в облачных службах Azure](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).
>
>

## <a name="user-account-access-toofiles-and-directories"></a>Toofiles доступа учетной записи пользователя и каталогов

Учетная запись пользователя автоматически и учетной записи пользователя с именем имеют задаче для чтения и записи доступа toohello рабочий каталог, общий каталог и каталог задачи нескольких экземпляров. Обоих типов учетных записей имеют доступ на чтение toohello запуска задания подготовки каталоги и.

Если задача запускается с hello же учетная запись, которая использовалась для запуска задачи запуска, задачу hello имеет доступ на чтение запись toohello начала задачи каталог. Аналогично, если задача запускается с hello же учетная запись, использованная для выполнения задачи подготовки задания, задачу hello имеет каталог задач подготовки задания toohello доступ для чтения и записи. Если задача выполняется с другой учетной записью, чем hello запуска задачи или задачи подготовки задания, задачу hello имеет только доступ на чтение toohello соответствующий каталог.

Дополнительные сведения о доступе к файлам и каталогам из задачи см. в разделе [Разработка решений для крупномасштабных параллельных вычислений с использованием пакетной службы](batch-api-basics.md#files-and-directories).

## <a name="elevated-access-for-tasks"></a>Повышенные права доступа для задач 

Повышение уровня учетной записи пользователя Hello указывает, выполняется ли задача с повышенными правами доступа. Автоматическая и именованная учетная запись пользователя могут выполнять задачи с повышенными правами доступа. Ниже приведены два варианта Hello для повышения уровня:

- **NonAdmin:** задачу hello выполняется как обычный пользователь без повышенных прав привилегированного доступа. всегда является Hello уровня прав по умолчанию для учетной записи пользователя пакета **NonAdmin**.
- **Администрирование:** задачу hello запускается от имени пользователя с повышенными правами доступа и работает с полными правами администратора. 

## <a name="auto-user-accounts"></a>Автоматические учетные записи пользователей

По умолчанию задачи выполняются в пакетной службе с автоматической учетной записью пользователя от имени стандартного пользователя без повышенных прав доступа и в области задачи. При настройке hello пользователя автоматически спецификации для области задач hello пакетная служба создает для этой задачи только учетную запись пользователя автоматически.

Hello альтернативных tootask область — область пула. При настройке hello пользователя автоматически спецификации задачи для области пула задачу hello выполняется под учетной записью пользователя автоматически, доступных tooany задач в пуле hello. Дополнительные сведения об области пула разделе hello [выполнение задачи, как hello auto пользователя с областью видимости пула](#run-a-task-as-the-autouser-with-pool-scope).   

область по умолчанию Hello отличается на узлах Windows и Linux.

- На узлах Windows задачи выполняются в области задачи по умолчанию.
- Узлы Linux всегда выполняют задачи в области пула.

Существует четыре возможных конфигурации для спецификации пользователя автоматически hello, каждое из которых соответствует tooa уникальную auto-учетную запись пользователя.

- Доступ без прав администратора с областью задач (определение пользователя автоматически hello по умолчанию)
- Доступ от имени администратора (с повышенными правами) с областью задачи.
- Доступ от имени стандартного пользователя с областью пула.
- Доступ от имени администратора с областью пула.

> [!IMPORTANT] 
> Задачи, выполняемые в области задач нет фактически доступ tooother задачи на узле. Тем не менее злонамеренный пользователь с учетной записью доступа toohello удалось обойти это ограничение, отправляя задачу, которая выполняется с правами администратора и получает доступ к другим каталогам задачи. Пользователь-злоумышленник также можно использовать узел tooa tooconnect RDP или SSH. Это важные tooprotect доступа tooyour пакета ключей учетной записи tooprevent такой сценарий. Если есть подозрение, что ваша учетная запись была скомпрометирована, быть tooregenerate убедиться, что ваши ключи.
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a>Выполнение задачи от имени автоматического пользователя с повышенными правами доступа

При необходимости toorun задачи с помощью повышенные права доступа, можно настроить hello спецификации автоматически пользователя права администратора. Например задача запуска может понадобиться программного обеспечения tooinstall повышенные права доступа на узле hello.

> [!NOTE] 
> Как правило, лучше всего подходит toouse расширенные права доступа только при необходимости. Рекомендуется предоставление hello минимальными правами доступа необходимые tooachieve hello желаемого результата. Например если начальная задача устанавливает программное обеспечение для текущего пользователя hello, вместо того, для всех пользователей может быть доступ tooavoid предоставление tootasks повышенные права доступа. Вы можете настроить hello спецификации автоматически пользователя для доступа к области и не являющихся администраторами пула для всех задач, требующих toorun в учетную запись, включая задачи запуска hello hello. 
>
>

Hello следующие фрагменты кода показывают, как tooconfigure hello спецификации пользователя автоматически. Примеры Hello уровень hello повышение слишком`Admin` и hello области слишком`Task`. Область задач установлен по умолчанию hello, но включается в список ради hello примера.

#### <a name="batch-net"></a>.NET для пакетной службы

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a>Java для пакетной службы

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a>Python для пакетной службы

```python
user = batchmodels.UserIdentity(
    auto_user=batchmodels.AutoUserSpecification(
        elevation_level=batchmodels.ElevationLevel.admin,
        scope=batchmodels.AutoUserScope.task))
task = batchmodels.TaskAddParameter(
    id='task_1',
    command_line='cmd /c "echo hello world"',
    user_identity=user)
batch_client.task.add(job_id=jobid, task=task)
```

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a>Выполнение задачи от имени автоматического пользователя с областью пула

При подготовке узла две всему пулу auto-учетные записи пользователей создаются на каждом узле в пуле hello, с повышенные права доступа и без повышенных прав привилегированного доступа. Настройка области toopool области hello auto пользователя для данной задачи запускает задачу hello в одном из этих учетных записей два пользователя автоматически всему пулу. 

При указании области пула для hello auto пользователя всех задач, которые выполняются с правами администратора запускаться hello одной учетной записи пользователя автоматически всему пулу. Аналогичным образом задачи, которые выполняются без разрешений администратора, также выполняются с одной автоматической учетной записью пользователя пула. 

> [!NOTE] 
> два пользователя автоматически всему пулу Hello представляют отдельные учетные записи. Задачи, выполняемые в группе hello пула административных учетных записей не может обмениваться данными задачи, выполняемые hello стандартной учетной записью и наоборот. 
>
>

Здравствуйте, преимущество toorunning под одной учетной записи пользователя автоматически является задачи могли tooshare данных с помощью других задач, выполняющихся на hello hello того же узла.

Общий доступ к секретной информации между задачами-один сценарий, когда выполнение задачи, связанные с одной из учетных записей пользователей автоматически всему пулу hello двух полезно. Например предположим, что задача запуска должен tooprovision секрет на узле hello, можно использовать другие задачи. Можно использовать hello API защиты данных Windows (DPAPI), но он требует наличия прав администратора. Вместо этого можно защитить секрет hello на уровне пользователя hello. Секрет без повышенных прав привилегированного доступа hello задач, выполняемых в рамках hello, можно получить доступ к одной учетной записи пользователя.

Совместное использование другой сценарий, где вы можете toorun задачи, связанные с учетной записи пользователя автоматически с областью видимости пул — это файл интерфейса передачи сообщений (MPI). Общий файловый ресурс MPI полезно в том случае, если узлы hello в toowork необходимость задача hello MPI на hello и те же данные файла. Hello головного узла создает общую папку, hello дочерние узлы можно получить доступ, если они выполняются в рамках hello же учетной записи пользователя автоматически. 

Следующий фрагмент кода Hello устанавливается область toopool область hello auto пользователя для задачи в пакете .NET. Повышение уровня Hello опущен, поэтому задачу hello запускается под учетной записью обычного пользователя автоматически всему пулу hello.

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a>Именованные учетные записи пользователей

При создании пула можно определить именованные учетные записи пользователей. Для именованной учетной записи пользователя указываются имя и пароль. Можно указать hello уровня прав для учетной записи пользователя с именем. Для узлов Linux можно также предоставить закрытый ключ SSH.

Учетную запись пользователя с именем существует на всех узлах в кластере hello и задачи доступны tooall работает на этих узлах. Для пула можно определить любое число именованных пользователей. При добавлении задачи или коллекцию задач, можно указать, что задача hello будет запускаться под одной из учетных записей пользователей, определенных для пула hello с именем hello.

Учетную запись пользователя с именем полезен при необходимости toorun всех задач в задании в разделе hello же учетной записью пользователя, но изолировать их друг от задачи, выполняемые в других заданиях на hello то же время. Например, можно создать именованного пользователя для каждого задания и выполнять задачи каждого задания с этой именованной учетной записью пользователя. В этом случае каждое задание сможет передать секрет своим задачам, но не задачам, выполняемым в других заданиях.

Можно также использовать toorun учетной записи пользователя с именем задачу, которая задает разрешения на внешние ресурсы, такие как общие файловые ресурсы. С учетной записью пользователя с именем контролировать удостоверение пользователя hello и можно использовать разрешения tooset удостоверение этого пользователя.  

Применяя именованные учетные записи пользователей, можно обеспечить SSH-подключение без пароля между узлами Linux. Можно использовать учетную запись пользователя с именем с узлами Linux, требующие toorun многоэкземплярные задачи. Каждый узел в пул hello можно выполнять задачи с учетной записью пользователя, определенные для всего пула hello. Дополнительные сведения о задачах нескольких экземпляров см. в разделе [используется несколькими\-экземпляр задачи приложений MPI toorun](batch-mpi.md).

### <a name="create-named-user-accounts"></a>Создание именованных учетных записей пользователей

toocreate с именем учетные записи пользователей в пакете, добавить коллекцию пула toohello учетных записей пользователей. Hello следующих фрагментах кода показано, как учетные записи пользователей в .NET, Java и Python с именем toocreate. Эти Показать фрагменты кода как toocreate администратора и учетные записи в пуле с именем без прав администратора. Примеры Hello создавать пулы с использованием hello конфигурацию облачной службы, но использовать же подход при создании пула Windows или Linux с помощью конфигурации виртуальной машины hello hello.

#### <a name="batch-net-example-windows"></a>Пример использования .NET в пакетной службе (Windows)

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using hello cloud service configuration.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                                         
    virtualMachineSize: "small",                                                
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));   

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount("adminUser", "xyz123", ElevationLevel.Admin),
    new UserAccount("nonAdminUser", "123xyz", ElevationLevel.NonAdmin),
};

// Commit hello pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a>Пример использования .NET в пакетной службе (Linux)

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello virtual machine configuration toouse toocreate hello pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create hello unbound pool.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                             
    virtualMachineSize: "Standard_A1",                                      
    virtualMachineConfiguration: virtualMachineConfiguration);                  

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount(
        name: "adminUser",
        password: "xyz123",
        elevationLevel: ElevationLevel.Admin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 12345,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
    new UserAccount(
        name: "nonAdminUser",
        password: "123xyz",
        elevationLevel: ElevationLevel.NonAdmin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 45678,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
};

// Commit hello pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a>Пример на Java для пакетной службы

```java
List<UserAccount> userList = new ArrayList<>();
userList.add(new UserAccount().withName(adminUserAccountName).withPassword(adminPassword).withElevationLevel(ElevationLevel.ADMIN));
userList.add(new UserAccount().withName(nonAdminUserAccountName).withPassword(nonAdminPassword).withElevationLevel(ElevationLevel.NONADMIN));
PoolAddParameter addParameter = new PoolAddParameter()
        .withId(poolId)
        .withTargetDedicatedNodes(POOL_VM_COUNT)
        .withVmSize(POOL_VM_SIZE)
        .withCloudServiceConfiguration(configuration)
        .withUserAccounts(userList);
batchClient.poolOperations().createPool(addParameter);
```

#### <a name="batch-python-example"></a>Пример на Python для пакетной службы

```python
users = [
    batchmodels.UserAccount(
        name='pool-admin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.admin)
    batchmodels.UserAccount(
        name='pool-nonadmin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.nonadmin)
]
pool = batchmodels.PoolAddParameter(
    id=pool_id,
    user_accounts=users,
    virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
        image_reference=image_ref_to_use,
        node_agent_sku_id=sku_to_use),
    vm_size=vm_size,
    target_dedicated=vm_count)
batch_client.pool.add(pool)
```

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a>Выполнение задачи с именованной учетной записью пользователя с повышенными правами доступа

toorun задачи как с повышенными правами пользователя, задачу hello набор **Удостоверение_пользователя** tooa свойство с именем учетной записи пользователя, который был создан с его **ElevationLevel** значение свойства слишком`Admin`.

Этот фрагмент кода указывает, что задача hello должны выполняться под учетной записью пользователя с именем. Эта учетная запись пользователя с именем был определен в пуле hello при создании пула hello. В этом случае hello с именем учетной записи пользователя была создана с правами администратора:

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a>Обновление библиотеки клиента последней пакета кода toohello

2017 г-01-01.4.0 содержит критические изменения, заменив hello версия обновления пакета Hello **runElevated** свойства доступны в предыдущих версиях с hello **Удостоверение_пользователя** свойство. следующие таблицы Hello предоставляют простой сопоставления, которые можно использовать tooupdate кода из более ранних версий клиентских библиотек hello.

### <a name="batch-net"></a>.NET для пакетной службы

| Если в коде используется…                  | Замените его на…                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| Свойство `CloudTask.RunElevated` не указано | Обновление не требуется.                                                                                               |

### <a name="batch-java"></a>Java для пакетной службы

| Если в коде используется…                      | Замените его на…                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| Свойство `CloudTask.withRunElevated` не указано | Обновление не требуется.                                                                                                                     |

### <a name="batch-python"></a>Python для пакетной службы

| Если в коде используется…                      | Замените его на…                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | `user_identity=user`, where <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | `user_identity=user`, where <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| Свойство `run_elevated` не указано | Обновление не требуется.                                                                                                                                  |


## <a name="next-steps"></a>Дальнейшие действия

### <a name="batch-forum"></a>Форум по Пакетной службе

Hello [форум по пакетной Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) на сайте MSDN — лучшие поместите toodiscuss пакета и ответы на вопросы о службе hello. Изучайте полезные закрепленные сообщения и задавайте вопросы, возникающие во время сборки пакетных решений.
