---
title: "aaaTutorial - использование hello Azure пакета SDK для Python | Документы Microsoft"
description: "Изучите основные понятия hello пакетной службы Azure и создайте простое решение, с помощью Python."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: 42cae157-d43d-47f8-88f5-486ccfd334f4
ms.service: batch
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c4d5152aeef31848c50a7f2aae5e7a7e0e1e9535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-sdk-for-python"></a>Начало работы с hello пакета SDK для Python

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Основы hello объекта [пакетной службы Azure] [ azure_batch] и hello [пакета Python] [ py_azure_sdk] клиента в обсуждении небольшой пакет приложения, написанного на Python. Рассматривается, как эти два примера скриптов используйте hello пакетной службы tooprocess параллельной рабочей нагрузки на виртуальных машинах Linux в облаке hello и их взаимодействие с [хранилища Azure](../storage/common/storage-introduction.md) для файла промежуточного хранения и извлечения. Будет узнать общий рабочий процесс приложения пакета и получить представление о базовых hello основных компонентов пакета, например заданий, задач, пулы и вычислительных узлов.

![Рабочий процесс решения пакетной службы (основной)][11]<br/>

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы уже работали с Python и знаете, как работать в Linux. Также предполагается, что вы будете требования к создания может toosatisfy hello учетной записи, указанные ниже для Azure и пакета hello и служб хранилища.

### <a name="accounts"></a>Учетные записи
* **Учетная запись Azure.** Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure][azure_free_account].
* **Учетная запись пакетной службы**. Если у вас есть подписка Azure, [создайте учетную запись пакетной службы Azure](batch-account-create-portal.md).
* **Учетная запись хранения**. См. раздел [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account) в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).

### <a name="code-sample"></a>Пример кода
Учебник Python Hello [образец кода] [ github_article_samples] является одним из hello найти множество образцов кода пакета в hello [образцы azure пакета] [ github_samples] репозитория на GitHub. Можно загрузить все образцы hello, щелкнув **клон или загрузки > загрузить ZIP** на домашней странице hello репозитория или щелкнув hello [azure пакета образцы master.zip] [ github_samples_zip]прямой ссылкой скачивания. Как только вы извлекли содержимое hello hello ZIP-файл, hello двух сценариев в этом учебнике можно найти на hello `article_samples` каталога:

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a>Среда Python
toorun hello *python_tutorial_client.py* образец скрипта на локальной рабочей станции, необходимо **интерпретатор Python** совместим с версией **2.7** или **3.3 +**. Hello сценарий протестирован на Windows и Linux.

### <a name="cryptography-dependencies"></a>Зависимости шифрования
Необходимо установить зависимости hello для hello [криптографии] [ crypto] библиотеки, необходимые для hello `azure-batch` и `azure-storage` пакеты Python. Выполните одно из следующих операций, подходящих для вашей платформы hello, или ссылается toohello [установки криптографии] [ crypto_install] Дополнительные сведения:

* Ubuntu

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* CentOS

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* SLES/OpenSUSE

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* Windows

    `pip install cryptography`

> [!NOTE]
> При установке для Python 3.3 + в Linux, используйте hello python3 эквиваленты для hello Python зависимостей. Например, в Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`
>
>

### <a name="azure-packages"></a>Пакеты Azure
После этого установите hello **пакетной службы Azure** и **хранилища Azure** пакеты Python. Можно установить оба пакета с помощью **pip** и hello *requirements.txt* по следующему адресу:

`/azure-batch-samples/Python/Batch/requirements.txt`

Следующие проблемы **pip** команды tooinstall hello пакета и хранения пакетов:

`pip install -r requirements.txt`

Кроме того, можно установить hello [пакета azure] [ pypi_batch] и [хранилища azure] [ pypi_storage] Python пакетов вручную:

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> Если вы используете непривилегированной учетной записи, может потребоваться tooprefix команды с `sudo`. Например, `sudo pip install -r requirements.txt`. Дополнительные сведения об установке пакетов Python см. в статье [Installing Packages][pypi_install] (Установка пакетов) на сайте python.org.
>
>

## <a name="batch-python-tutorial-code-sample"></a>Пример кода Python для руководства по пакетной службе
Образец учебника код пакета Python Hello состоит из двух сценариев Python и несколько файлов данных.

* **python_tutorial_client.py**: взаимодействует с tooexecute hello пакета и хранилище служб параллельной рабочей нагрузки на вычислительных узлов (виртуальных машин). Hello *python_tutorial_client.py* сценарий выполняется на локальной рабочей станции.
* **python_tutorial_task.py**: hello сценарий, запускаемый на вычислительных узлов в Azure tooperform hello фактическую работу. В образце hello *python_tutorial_task.py* анализирует hello текст в файл, загруженный из хранилища Azure (hello входного файла). Затем он создает текстовый файл (hello выходной файл), содержащий список hello первых трех слов, которые содержатся во входном файле hello. После создания выходного файла hello, *python_tutorial_task.py* передач hello tooAzure файла хранилища. Это делает доступными для загрузки toohello клиента скрипт, выполняемый на рабочей станции. Hello *python_tutorial_task.py* сценарий выполняется параллельно на нескольких вычислительных узлов в hello пакетной службы.
* **./Data/taskdata\*.txt**: эти три текстовых файлов ввода hello для hello задач, выполняемых на hello вычислительных узлов.

Привет, следующая схема иллюстрирует hello основных операций, выполняемых скриптов клиента "и" задача hello. Этот основной рабочий процесс является типичным для многих вычислительных решений, созданных с помощью пакетной службы. Хотя здесь не показаны каждый компонент, доступный в hello пакетная служба, практически все пакета сценарий включает некоторые части этого рабочего процесса.

![Пример рабочего процесса пакетной службы][8]<br/>

[**Шаг 1.**](#step-1-create-storage-containers) Создайте **контейнеры** в хранилище BLOB-объектов Azure.<br/>
[**Шаг 2.**](#step-2-upload-task-script-and-data-files) Отправьте toocontainers задачи скрипта и входные файлы.<br/>
[**Шаг 3.**](#step-3-create-batch-pool) Создайте **пул** пакетной службы.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** Здравствуйте, пул **StartTask** загрузки hello toonodes Задача сценария (python_tutorial_task.py), которые они присоединиться к пулу hello.<br/>
[**Шаг 4.**](#step-4-create-batch-job) Создайте **задание** пакетной службы.<br/>
[**Шаг 5.**](#step-5-add-tasks-to-job) Добавить **задачи** toohello задания.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** Hello задачи, запланированные tooexecute на узлах.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** Каждая задача скачивает свои входные данные из службы хранилища Azure, а затем начинает выполнение.<br/>
[**Шаг 6.**](#step-6-monitor-tasks) Мониторинг задач.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** Как выполнить действия, они отправляют их вывода данных tooAzure хранилища.<br/>
[**Шаг 7.**](#step-7-download-task-output) Скачайте выходные данные задачи из службы хранилища.

Как уже упоминалось, не каждое решение пакетной службы будет выполнять именно эти шаги. Некоторые решения могут выполнять больше действий, но этот пример демонстрирует общие процессы в решении пакетной службы.

## <a name="prepare-client-script"></a>Подготовка сценария клиента
Перед запуском образца hello, необходимо добавить учетные данные учетной записи пакета и хранилища слишком*python_tutorial_client.py*. Если вы еще не сделали этого, откройте файл hello в вашей избранные редактор и обновление hello следующие строки с учетными данными.

```python
# Update hello Batch and Storage account credential strings below with hello values
# unique tooyour accounts. These are used when constructing connection strings
# for hello Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

Пакет и хранения учетные данные учетной записи в колонке hello учетной записи каждой службы можно найти в hello [портал Azure][azure_portal]:

![Пакетное учетные данные на портале hello][9]
![учетные данные хранилища на портале hello][10]<br/>

В следующих разделах hello, анализируются hello шагов, используемых hello скрипты tooprocess рабочую нагрузку в hello пакетной службы. Мы рекомендуем вам регулярно toorefer toohello сценариев в редакторе, используемом во время продвигайтесь hello оставшейся части статьи hello.

Перейдите следующей строкой в toohello **python_tutorial_client.py** toostart с шага 1:

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a>Шаг 1. Создание контейнеров службы хранилища
![Создание контейнеров в службе хранилища Azure][1]
<br/>

Пакетная служба включает встроенную поддержку для взаимодействия со службой хранилища Azure. Контейнеры в учетной записи хранилища обеспечивают hello файлов, необходимых hello задач, которые выполняются в вашей учетной записи пакета. контейнеры Hello также обеспечивают месте toostore hello выходные данные задачи hello выдавать. Здравствуйте, первое, что hello *python_tutorial_client.py* сценарий выполняет создают три контейнера в [хранилища больших двоичных объектов](../storage/common/storage-introduction.md#blob-storage):

* **приложение**: этот контейнер будет хранить hello Python сценариев, запускаемых задач hello *python_tutorial_task.py*.
* **входной**: задачи будут загружены файлы tooprocess hello данных с hello *ввода* контейнера.
* **выходные данные**: после завершения выполнения задач обработки входных файлов они загрузит hello результаты toohello *вывода* контейнера.

В порядке toointeract с хранилищем учетной записи и создавать контейнеры, мы используем hello [хранилища azure] [ pypi_storage] пакета toocreate [BlockBlobService] [ py_blockblobservice] объект — hello «большой двоичный объект клиент». Затем создадим три контейнера в учетной записи хранения hello, с помощью клиента hello BLOB-объектов.

```python
import azure.storage.blob as azureblob

# Create hello blob client, for use in obtaining references to
# blob storage containers and uploading files toocontainers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use hello blob client toocreate hello containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

После создания контейнеров hello приложения hello, теперь можно отправить hello файлы, которые будут использоваться задачами hello.

> [!TIP]
> [Как toouse хранилища больших двоичных объектов Azure в Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) хороший Обзор работы с контейнеров хранилища Azure и больших двоичных объектов. В начале работы с использованием пакета должно быть hello верхней части списка для чтения.
>
>

## <a name="step-2-upload-task-script-and-data-files"></a>Шаг 2. Отправка сценария задач и файлов данных
![Задача передачи приложения и ввода (данных) файлы toocontainers][2]
<br/>

В файле hello операции, передачи *python_tutorial_client.py* сначала определяет коллекции **приложения** и **ввода** пути к файлам, в котором они хранятся на локальном компьютере hello. Затем он передает эти контейнеры toohello файлы, созданные на предыдущем шаге hello.

```python
# Paths toohello task script. This script will be executed by hello tasks that
# run on hello compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# hello collection of data files that are toobe processed by hello tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload hello application script tooAzure Storage. This is hello script that
# will process hello data files, and is executed by each of hello tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload hello data files. This is hello data that will be processed by each of
# hello tasks executed on hello compute nodes in hello pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

Здравствуйте, используя охватом списка, `upload_file_to_container` функция вызывается для каждого файла в hello коллекций и двух [ResourceFile] [ py_resource_file] заполняются коллекций. Hello `upload_file_to_container` функция появляется ниже:

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file tooan Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: hello name of hello Azure Blob storage container.
    :param str file_path: hello local path toohello file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} toocontainer [{}]...'.format(path,
                                                          container_name))

    block_blob_client.create_blob_from_path(container_name,
                                            blob_name,
                                            file_path)

    sas_token = block_blob_client.generate_blob_shared_access_signature(
        container_name,
        blob_name,
        permission=azureblob.BlobPermissions.READ,
        expiry=datetime.datetime.utcnow() + datetime.timedelta(hours=2))

    sas_url = block_blob_client.make_blob_url(container_name,
                                              blob_name,
                                              sas_token=sas_token)

    return batchmodels.ResourceFile(file_path=blob_name,
                                    blob_source=sas_url)
```

### <a name="resourcefiles"></a>ResourceFiles
Объект [ResourceFile] [ py_resource_file] предоставляет задачи в пакете с файлом tooa hello URL-адрес в службе хранилища Azure, загруженные tooa вычислительный узел перед запуском этой задачи. Hello [ResourceFile][py_resource_file]. **blob_source** свойство указывает hello полный URL-адрес файла hello, которое существовало в хранилище Azure. Hello URL-адрес может также включать подписанного URL-адреса (SAS), предоставляющий безопасный доступ toohello файла. Большинство типов задач в пакетной службе, в том числе перечисленные ниже, содержат свойство *ResourceFiles* .

* [CloudTask][py_task]
* [StartTask][py_starttask]
* [JobPreparationTask][py_jobpreptask]
* [JobReleaseTask][py_jobreltask]

Этот образец не использует hello JobPreparationTask или JobReleaseTask типы задач, но вы можете прочитать больше о них в [выполнения задания Подготовка и выполнение задач в пакете Azure вычислительные узлы](batch-job-prep-release.md).

### <a name="shared-access-signature-sas"></a>Подписанный URL-адрес (SAS)
Подписи общего доступа являются строки, которые обеспечивают безопасный доступ toocontainers и больших двоичных объектов в хранилище Azure. Hello *python_tutorial_client.py* скрипт использует оба большого двоичного объекта и контейнера подписи коллективного доступа, а также показано, как эти общие tooobtain доступ к строки подписи из hello службы хранилища.

* **BLOB-объектов подписи коллективного доступа**: hello пула StartTask использует BLOB-объектов подписи коллективного доступа при загрузке hello задачи скрипта и входные файлы данных из хранилища (в разделе [шаг 3](#step-3-create-batch-pool) ниже). Hello `upload_file_to_container` функционировать в *python_tutorial_client.py* содержит hello код, который получает подпись общего доступа для каждого большого двоичного объекта. Это достигается путем вызова [BlockBlobService.make_blob_url] [ py_make_blob_url] в модуле хранения hello.
* **Подписанный URL-адрес контейнера**: как каждая задача завершит свою работу на вычислительном узле hello, передает его выходной файл toohello *вывода* контейнера в хранилище Azure. toodo таким образом, *python_tutorial_task.py* используется подпись общего доступа контейнера, которая предоставляет доступ на запись toohello контейнера. Hello `get_container_sas_token` функционировать в *python_tutorial_client.py* получает hello контейнер подписанный URL-адрес, который затем передается как аргумент командной строки toohello задачи. Шаг #5 [добавить задачи tooa задания](#step-5-add-tasks-to-job), рассматривается использование hello hello SAS контейнера.

> [!TIP]
> Извлечение серии из двух частей hello подписей общего доступа [часть 1: Общие сведения о модели SAS hello](../storage/common/storage-dotnet-shared-access-signature-part-1.md) и [часть 2: создать и использовать SAS с hello службы BLOB-объектов](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn Дополнительные сведения о предоставления безопасного доступа toodata вашей учетной записи хранилища.
>
>

## <a name="step-3-create-batch-pool"></a>Шаг 3. Создание пула пакетной службы
![Создание пула пакетной службы][3]
<br/>

**Пул** пакетной службы — это коллекция вычислительных узлов (виртуальных машин), на которых пакетная служба выполняет задачи задания.

После передает hello задач сценариев и данных файлов toohello учетной записи хранилища, *python_tutorial_client.py* запускает его взаимодействия с hello пакетной службы с помощью модуля hello пакета Python. toodo таким образом, [BatchServiceClient] [ py_batchserviceclient] создается:

```python
# Create a Batch service client. We'll now be interacting with hello Batch
# service in addition tooStorage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

Далее пул вычислительных узлов создается в hello пакетной учетной записи с помощью вызова слишком`create_pool`.

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with hello specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for hello new pool.
    :param list resource_files: A collection of resource files for hello pool's
    start task.
    :param str publisher: Marketplace image publisher
    :param str offer: Marketplace image offer
    :param str sku: Marketplace image sku
    """
    print('Creating pool [{}]...'.format(pool_id))

    # Create a new pool of Linux compute nodes using an Azure Virtual Machines
    # Marketplace image. For more information about creating pools of Linux
    # nodes, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/

    # Specify hello commands for hello pool's start task. hello start task is run
    # on each node as it joins hello pool, and when it's rebooted or re-imaged.
    # We use hello start task tooprep hello node for running our task script.
    task_commands = [
        # Copy hello python_tutorial_task.py script toohello "shared" directory
        # that all tasks that run on hello node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and hello dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install hello azure-storage module so that hello task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get hello node agent SKU and image reference for hello virtual machine
    # configuration.
    # For more information about hello virtual machine configuration, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/
    sku_to_use, image_ref_to_use = \
        common.helpers.select_latest_verified_vm_image_with_node_agent_sku(
            batch_service_client, publisher, offer, sku)

    new_pool = batch.models.PoolAddParameter(
        id=pool_id,
        virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
            image_reference=image_ref_to_use,
            node_agent_sku_id=sku_to_use),
        vm_size=_POOL_VM_SIZE,
        target_dedicated=_POOL_NODE_COUNT,
        start_task=batch.models.StartTask(
            command_line=
            common.helpers.wrap_commands_in_shell('linux', task_commands),
            run_elevated=True,
            wait_for_success=True,
            resource_files=resource_files),
        )

    try:
        batch_service_client.pool.add(new_pool)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

При создании пула определяется [PoolAddParameter] [ py_pooladdparam] , указывающий несколько свойств пула hello:

* **Идентификатор** hello пула (*идентификатор* — требуется)<p/>Как и у большинства сущностей в пакетной службе, у нового пула должен быть идентификатор, уникальный в учетной записи этой службы. Ваш код ссылается с помощью его идентификатора пула toothis, и именно вы идентифицируете пула hello в hello Azure [портала][azure_portal].
* **Количество вычислительных узлов** (*target_dedicated*, обязательное).<p/>Это свойство определяет, сколько виртуальных машин должны развертываться в пуле hello. Является важным toonote, что все учетные записи пакетного имеют значение по умолчанию **квоты** hello, ограничения числа **ядер** (и, таким образом, вычислительных узлов) в учетной записи пакета. Можно найти квот по умолчанию hello и инструкции о том, как слишком[увеличить квоту](batch-quota-limit.md#increase-a-quota) (таких как максимальное количество ядер в вашей учетной записи пакетного hello) в [квоты и лимиты для пакетной службы Azure hello](batch-quota-limit.md). Если возник вопрос о том, почему пул не использует больше определенного количества узлов, Эта квота ядра может быть причиной hello.
* **Операционная система** для узлов (*virtual_machine_configuration* **или** *cloud_service_configuration*, обязательное).<p/>В *python_tutorial_client.py* мы создаем пул узлов Linux с использованием [VirtualMachineConfiguration][py_vm_config]. Hello `select_latest_verified_vm_image_with_node_agent_sku` функционировать в `common.helpers` упрощает работу с [виртуальных машин Azure Marketplace] [ vm_marketplace] изображения. Дополнительные сведения об использовании образов из магазина см. в статье [Подготовка вычислительных узлов Linux в пулах пакетной службы Azure](batch-linux-nodes.md).
* **Размер вычислительных узлов** (*vm_size*, обязательное).<p/>Так как мы указываем узлы Linux для [VirtualMachineConfiguration][py_vm_config], необходимо указать их размер (в этом примере — `STANDARD_A1`), как описано в статье [Размеры виртуальных машин в Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Дополнительные сведения см. в статье [Подготовка вычислительных узлов Linux в пулах пакетной службы Azure](batch-linux-nodes.md).
* **Задача запуска** (*start_task*, не обязательное).<p/>Вместе с hello выше свойства физического узла, можно также указать [StartTask] [ py_starttask] для пула hello (не требуется). Hello StartTask выполняет на каждом узле, как этот узел соединяет hello пул, и каждый раз при перезапуске узла. Hello StartTask особенно полезна для подготовки вычислительных узлов для выполнения задач, таких как установка приложения hello, выполняющиеся задачи hello.<p/>В этом образце приложения hello StartTask копирует hello файлы, загружаемые из хранилища (которые указываются с помощью hello StartTask **resource_files** свойство) из hello StartTask *рабочий каталог* toohello *общего* каталог, в котором доступны все задачи, выполняемые на узле hello. По сути, это копирует `python_tutorial_task.py` toohello каталог общих на каждый узел при присоединении узла hello пула hello доступа к ней все задачи, выполняемых в узле hello.

Вы можете заметить hello вызовов toohello `wrap_commands_in_shell` вспомогательную функцию. Она использует коллекцию отдельных команд и создает одну соответствующую командную строку для свойства командной строки задачи.

Также значительным в приведенном выше фрагменте кода hello используется hello двух переменных среды в hello **командная_строка** свойство hello StartTask: `AZ_BATCH_TASK_WORKING_DIR` и `AZ_BATCH_NODE_SHARED_DIR`. Несколько переменных среды, которые являются определенной tooBatch автоматически настраивается каждом вычислительном узле в пуле пакета. Любой процесс, выполняемый задачей имеет доступ к переменным среды toothese.

> [!TIP]
> toofind Дополнительные сведения о переменных среды hello, доступные на вычислительных узлах пула, а также сведения о задаче рабочие каталоги, в разделе **параметры среды для задачи** и **файлов и каталогов**  в hello [Обзор возможностей пакетной службы Azure](batch-api-basics.md).
>
>

## <a name="step-4-create-batch-job"></a>Шаг 4. Создание задания пакетной службы
![Создание задания пакетной службы][4]<br/>

**Задание** пакетной службы — это коллекция задач, связанных с пулом вычислительных узлов. Hello задачи в задании, выполняются в hello связанный пул вычислительных узлов.

Задания можно использовать не только для упорядочивания и отслеживания задач в связанных рабочих нагрузок, но также и для налагающий определенные ограничения, например hello максимального времени для задания hello (и по расширению, его задачи) и приоритет задания в заданиях tooother отношения в hello пакетной учетной записи. В этом примере задание hello связаны только с пулом hello, который был создан на шаге #3. Дополнительные свойства не настроены.

Все задания пакетной службы связаны с конкретным пулом. Эта связь указывает, какие задачи hello задания выполняются в узлы. Укажите hello пула с помощью hello [PoolInformation] [ py_poolinfo] свойства, как показано в приведенном ниже фрагменте кода hello.

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with hello specified ID, associated with hello specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID for hello job.
    :param str pool_id: hello ID for hello pool.
    """
    print('Creating job [{}]...'.format(job_id))

    job = batch.models.JobAddParameter(
        job_id,
        batch.models.PoolInformation(pool_id=pool_id))

    try:
        batch_service_client.job.add(job)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

После создания задания задачи добавляются рабочие tooperform hello.

## <a name="step-5-add-tasks-toojob"></a>Шаг 5: Добавление toojob задачи
![Добавление задачи toojob][5]<br/>
*(1) задачи добавляются toohello задания, (2) hello задачи, запланированные toorun на узлах и (3) hello задачи загрузки tooprocess файлы данных hello*

Пакет **задачи** являются hello отдельных рабочих элементов, выполните на hello вычислительных узлов. Задача имеет командную строку и выполняется hello сценарии или исполняемые файлы, укажите в этой командной строке.

tooactually выполнения работы, задачи должны быть добавлены tooa задания. Каждый [CloudTask] [ py_task] настраивается с помощью свойства командной строки и [ResourceFiles] [ py_resource_file] (как в случае с StartTask hello пула), hello Задача загружает toohello узла перед его командной строки выполняется автоматически. В образце hello каждая задача обрабатывает только один файл. Поэтому его коллекция ResourceFiles содержит один элемент.

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in hello collection toohello specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID of hello job toowhich tooadd hello tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: hello ID of an Azure Blob storage container to
    which hello tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    hello specified Azure Blob storage container.
    """

    print('Adding {} tasks toojob [{}]...'.format(len(input_files), job_id))

    tasks = list()

    for input_file in input_files:

        command = ['python $AZ_BATCH_NODE_SHARED_DIR/python_tutorial_task.py '
                   '--filepath {} --numwords {} --storageaccount {} '
                   '--storagecontainer {} --sastoken "{}"'.format(
                    input_file.file_path,
                    '3',
                    _STORAGE_ACCOUNT_NAME,
                    output_container_name,
                    output_container_sas_token)]

        tasks.append(batch.models.TaskAddParameter(
                'topNtask{}'.format(input_files.index(input_file)),
                wrap_commands_in_shell('linux', command),
                resource_files=[input_file]
                )
        )

    batch_service_client.task.add_collection(job_id, tasks)
```

> [!IMPORTANT]
> При доступе переменные среды, такие как `$AZ_BATCH_NODE_SHARED_DIR` или выполнить приложение не найдено в узле hello `PATH`, задача командные строки необходимо вызвать hello оболочки явно, такие как с `/bin/sh -c MyTaskApplication $MY_ENV_VAR`. Это требование не требуется, если задачи Выполнение приложения в узле hello `PATH` и не ссылаться на переменные среды.
>
>

В рамках hello `for` цикла в приведенном выше фрагменте кода hello, можно увидеть, что hello командной строки для задачи «hello» создается пять аргументов командной строки, которые передаются слишком*python_tutorial_task.py*:

1. **FILEPATH**: это файл toohello hello локальный путь, поскольку она существует на узле hello. Когда hello объекта ResourceFile в `upload_file_to_container` был создан на шаге 2 выше, имя файла hello был использован для этого свойства (hello `file_path` параметра в конструктор ResourceFile hello). Это означает, что этот файл hello можно найти в hello же каталог на узле hello в виде *python_tutorial_task.py*.
2. **NUMWORDS**: hello верхней *N* слова должны быть написаны toohello выходного файла.
3. **storageaccount**: hello имя учетной записи хранилища, которому принадлежит выходные данные задачи hello контейнера toowhich hello hello должна быть загружена.
4. **storagecontainer**: hello имя контейнера toowhich hello хранилища hello вывода файлов должна быть загружена.
5. **sastoken**: hello подписанного URL-адреса (SAS), предоставляющий доступ на запись toohello **вывода** контейнера в хранилище Azure. Hello *python_tutorial_task.py* скрипт использует подписанный URL-адрес при создает его BlockBlobService ссылку. Это обеспечивает доступ для записи toohello контейнера без использования клавиши доступа для учетной записи хранения hello.

```python
# NOTE: Taken from python_tutorial_task.py

# Create hello blob client using hello container's SAS token.
# This allows us toocreate a client that provides write
# access only toohello container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a>Шаг 6. Мониторинг задач
![Мониторинг задач][6]<br/>
*Здравствуйте, (1) мониторы hello задачи состояние завершения, а задачи hello (2) добавьте tooAzure результат данных хранилища*

При добавлении задачи задания tooa они автоматически в очередь и запланировать выполнение на вычислительных узлах пула hello, связанный с заданием hello. В зависимости от настройки hello пакета обрабатывает все очереди задач, планирования, повтор и другие задачи администрирования обязанностей.

Существует множество подходов toomonitoring выполнения задачи. Hello `wait_for_tasks_to_complete` функционировать в *python_tutorial_client.py* предоставляет простой пример задач наблюдения для определенного состояния, в данном случае hello [завершения] [ py_taskstate] состояние.

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in hello specified job reach hello Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello id of hello job whose tasks should be toomonitored.
    :param timedelta timeout: hello duration toowait for task completion. If all
    tasks in hello specified job do not reach Completed state within this time
    period, an exception will be raised.
    """
    timeout_expiration = datetime.datetime.now() + timeout

    print("Monitoring all tasks for 'Completed' state, timeout in {}..."
          .format(timeout), end='')

    while datetime.datetime.now() < timeout_expiration:
        print('.', end='')
        sys.stdout.flush()
        tasks = batch_service_client.task.list(job_id)

        incomplete_tasks = [task for task in tasks if
                            task.state != batchmodels.TaskState.completed]
        if not incomplete_tasks:
            print()
            return True
        else:
            time.sleep(1)

    print()
    raise RuntimeError("ERROR: Tasks did not reach 'Completed' state within "
                       "timeout period of " + str(timeout))
```

## <a name="step-7-download-task-output"></a>Шаг 7. Загрузка выходных данных задачи
![Загрузка выходных данных задачи из службы хранилища][7]<br/>

Теперь, когда hello работа завершена, hello выходные данные задач hello можно загрузить из хранилища Azure. Это делается с помощью вызова слишком`download_blobs_from_container` в *python_tutorial_client.py*:

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from hello specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: hello Azure Blob storage container from which to
     download files.
    :param directory_path: hello local directory toowhich toodownload hello files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] too{}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> Здравствуйте вызов слишком`download_blobs_from_container` в *python_tutorial_client.py* указывает, hello файлы должны быть загруженного tooyour домашнего каталога. Свободное toomodify считаете это расположение выходных данных.
>
>

## <a name="step-8-delete-containers"></a>Шаг 8. Удаление контейнеров
Поскольку плата взимается для данных, которые хранятся в хранилище Azure, это всегда tooremove рекомендуется, когда все большие двоичные объекты, которые больше не нужен для пакетных заданий. В *python_tutorial_client.py*, это делается с помощью трех вызовов слишком[BlockBlobService.delete_container][py_delete_container]:

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a>Шаг 9: Удалить задание hello и hello пула
В последнем шаге hello, запрашиваемые toodelete hello задания и hello пула, созданных по hello *python_tutorial_client.py* сценария. Хотя вы и не платите за задания и задачи, *взимается* плата за используемые вычислительные узлы. Поэтому рекомендуется выделять узлы только при необходимости. Удаление неиспользуемых пулов может быть частью процесса обслуживания.

Hello BatchServiceClient [JobOperations] [ py_job] и [PoolOperations] [ py_pool] имеют соответствующих методов удаления, которые являются вызывается, если подтверждение удаления:

```python
# Clean up Batch resources (if hello user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> Помните, что вы платите за использование вычислительных ресурсов, поэтому удаление неиспользуемых пулов позволит сократить затраты. Кроме того помните, что при удалении пула удаляются все вычислительные узлы этого пула, и все данные на узлах hello будет неустранимой после удаления пула hello.
>
>

## <a name="run-hello-sample-script"></a>Запустите сценарий образец hello
При запуске hello *python_tutorial_client.py* сценарий из учебника hello [образец кода][github_article_samples], вывод на консоль hello — примерно следующие toohello. Нет приостановит `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` пока hello пула вычислительные узлы создаются, запущена, и выполняются команды hello в задачу запуска пула hello. Используйте hello [портал Azure] [ azure_portal] toomonitor пула, вычислительные узлы, заданий и задач во время и после выполнения. Используйте hello [портал Azure] [ azure_portal] или hello [Microsoft Azure Storage Explorer] [ storage_explorer] tooview ресурсов хранилища hello (контейнеров и больших двоичных объектов) созданные приложения hello.

> [!TIP]
> Запустите hello *python_tutorial_client.py* сценарий из внутри hello `azure-batch-samples/Python/Batch/article_samples` каталога. Он использует относительный путь для hello `common.helpers` импорт модуля, чтобы можно было увидеть `ImportError: No module named 'common'` Если не выполнить скрипт hello из этого каталога.
>
>

Обычно время выполнения равно **приблизительно 5 – 7 минут** при запуске образца hello в конфигурации по умолчанию.

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py toocontainer [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt toocontainer [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks toojob [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached hello 'Completed' state within hello specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] too/home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] too/home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] too/home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER tooexit...
```

## <a name="next-steps"></a>Дальнейшие действия
Чувствовать себя свободного toomake изменения слишком*python_tutorial_client.py* и *python_tutorial_task.py* tooexperiment с различными вычислений сценариев. Например, попробуйте добавить задержки выполнения слишком*python_tutorial_task.py* toosimulate длительные задачи, а также отслеживать их на портале hello. Попробуйте установить дополнительные задачи или изменить hello количество вычислительных узлов. Добавьте toocheck логику для и разрешить использование hello существующих времени выполнения toospeed пула.

Теперь, когда вы знакомы с hello базовый рабочий процесс пакета решения, это время toodig в дополнительные возможности toohello hello пакетной службы.

* Просмотрите hello [возможности пакетной обработки Обзор Azure](batch-api-basics.md) статьи, которая рекомендуется, если вы новую службу toohello.
* Здравствуйте, запуска на другие статьи по разработке пакета в списке **разработки подробные** в hello [план обучения пакета][batch_learning_path].
* Извлечение другой реализации обработки hello «N основных слова» рабочей нагрузки с использованием пакета в hello [TopNWords] [ github_topnwords] образца.

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[blog_linux]: http://blogs.technet.com/b/windowshpc/archive/2016/03/30/introducing-linux-support-on-azure-batch.aspx
[crypto]: https://cryptography.io/en/latest/
[crypto_install]: https://cryptography.io/en/latest/installation/
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[github_article_samples]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/article_samples

[nuget_packagemgr]: https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build

[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_batchserviceclient]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html#azure.batch.BatchServiceClient
[py_blockblobservice]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.blockblobservice.html#azure.storage.blob.blockblobservice.BlockBlobService
[py_cloudtask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_cs_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudServiceConfiguration
[py_delete_container]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.delete_container
[py_gen_blob_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_blob_shared_access_signature
[py_gen_container_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_container_shared_access_signature
[py_image_ref]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_job]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.JobOperations
[py_jobpreptask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobPreparationTask
[py_jobreltask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobReleaseTask
[py_list_skus]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[py_make_blob_url]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.make_blob_url
[py_pool]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.PoolOperations
[py_pooladdparam]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolAddParameter
[py_poolinfo]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolInformation
[py_resource_file]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ResourceFile
[py_samples_github]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_task]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_taskstate]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.TaskState
[py_vm_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.VirtualMachineConfiguration
[pypi_batch]: https://pypi.python.org/pypi/azure-batch
[pypi_storage]: https://pypi.python.org/pypi/azure-storage
[pypi_install]: https://packaging.python.org/installing/
[storage_explorer]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/products/vs-2015-product-editions
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-python-tutorial/batch_workflow_01_sm.png "Создание контейнеров в службе хранилища Azure"
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "Задача передачи приложения и ввода (данных) файлы toocontainers"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "Создание пула пакетной службы"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "Создание задания пакетной службы"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "Добавление задачи toojob"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "Мониторинг задач"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "Скачивание выходных данных задачи из службы хранилища"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Рабочий процесс решения пакетной службы (полная схема)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "Учетные данные пакетной службы на портале"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "Учетные данные службы хранилища на портале"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Рабочий процесс решения пакетной службы (сокращенная схема)"
