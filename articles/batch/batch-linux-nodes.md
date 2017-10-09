---
title: "aaaRun Linux на виртуальной машине вычислительных узлов - пакетной службы Azure | Документы Microsoft"
description: "Узнайте, как tooprocess параллельных вычислений рабочих нагрузок на пулы виртуальных машин Linux в пакете Azure."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3daabd5c577baaafd0544f9f7913cb7b116d74d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="provision-linux-compute-nodes-in-batch-pools"></a>Подготовка вычислительных узлов Linux в пулах пакетной службы

Можно использовать пакетной службы Azure toorun параллельных вычислительных рабочих нагрузок на виртуальных машинах Linux и Windows. В этой статье описаны как пулы toocreate Linux узлы вычисления в hello пакетной службы с помощью обоих hello [пакета Python] [ py_batch_package] и [пакета .NET] [ api_net] клиентских библиотек.

> [!NOTE]
> Пакеты приложений поддерживаются во всех пулах пакетной службы, созданных после 5 июля 2017 г. Они поддерживаются в пулах пакета, созданные между 10 марта 2016 г. и 5 июля 2017 г., только в том случае, если пул hello был создан с помощью конфигурации облачной службы. Пакеты приложений не поддерживают пулы пакета, созданные предыдущей too10 марта 2016 г. Дополнительные сведения об использовании приложения пакетах toodeploy узлы tooyour пакета приложений, в разделе [развертывания приложений toocompute узлов с пакетами приложения пакета](batch-application-packages.md).
>
>

## <a name="virtual-machine-configuration"></a>Конфигурация виртуальной машины
При создании пула вычислительных узлов в пакете есть два способа из какой размер узла tooselect hello и операционной системы: Конфигурация облачных служб и конфигурации виртуальной машины.

**Cloud Services Configuration** (Конфигурация облачных служб) предоставляет *только*вычислительные узлы Windows. Размеры доступных вычислительных узлов, перечислены в [размеров для облачных служб](../cloud-services/cloud-services-sizes-specs.md), и доступных операционных систем перечисленных в hello [выпуски гостевой ОС Azure и Матрица совместимости пакетов SDK](../cloud-services/cloud-services-guestos-update-matrix.md). При создании пула, который содержит узлы для облачных служб Azure, необходимо указать размер узла hello и hello семейства ОС, которые описаны в hello упомянутых выше статьи. Для пулов вычислительных узлов Windows чаще всего используются облачные службы.

**Virtual Machine Configuration** предоставляет образы Windows и Linux для вычислительных узлов. Доступные размеры вычислительных узлов перечислены в статьях [Размеры виртуальных машин в Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) и [Размеры виртуальных машин в Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows). При создании пула, содержащего узлы конфигурации виртуальной машины, необходимо указать размер hello узлы hello, ссылка на изображение виртуальной машины hello и hello пакета узел агента SKU toobe на узлах, hello.

### <a name="virtual-machine-image-reference"></a>Ссылка на образ виртуальной машины
Здравствуйте, пакетная служба использует [наборы масштабирования виртуальных машин](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux вычислительных узлов. Можно задать изображение из hello [Azure Marketplace][vm_marketplace], или укажите пользовательского образа, который был подготовлен. Дополнительные сведения о пользовательских образах см. в руководстве по [разработке решений для крупномасштабных параллельных вычислений с помощью пакетной службы](batch-api-basics.md#pool).

При настройке ссылку образ виртуальной машины, необходимо указать hello свойств hello образ виртуальной машины. следующие свойства Hello необходимы при создании ссылки образ виртуальной машины:

| **Свойства ссылки на образ** | **Пример** |
| --- | --- |
| Издатель |Canonical |
| ПРЕДЛОЖЕНИЕ |UbuntuServer |
| SKU |14.04.4-LTS |
| Версия |последних |

> [!TIP]
> Дополнительные сведения об этих свойствах и как образы toolist Marketplace в [перейдите и выберите образы виртуальных машин Linux в Azure с помощью интерфейса командной строки или PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Обратите внимание, что не все образы из Marketplace в настоящее время совместимы с пакетной службой. Дополнительные сведения см. в разделе [Номер SKU агента узла](#node-agent-sku).
>
>

### <a name="node-agent-sku"></a>Номер SKU агента узла
агент узла Hello пакета — программа, которая запускается на каждом узле в пуле hello и предоставляет интерфейс команды управления hello между узлом hello и hello пакетной службы. Существуют различные реализации агента узла hello, известный как SKU для разных операционных систем. По сути при создании конфигурации виртуальной машины, сначала указывается ссылка на изображение hello виртуальной машины и укажите hello узел агента tooinstall на изображении hello. Как правило, каждый номер SKU агента узла совместим с несколькими образами виртуальных машин. Вот несколько примеров номеров SKU агентов узлов:

* batch.node.ubuntu 14.04;
* batch.node.centos 7;
* batch.node.windows amd64

> [!IMPORTANT]
> Не все образы виртуальных машин, доступных в hello Marketplace, несовместимы с hello в настоящее время доступных пакета узел агентов. Пакет SDK toolist hello hello доступный узел, агент SKU и hello образы виртуальных машин, с которыми они совместимы. В разделе hello [образы список виртуальных машин](#list-of-virtual-machine-images) далее в этой статье, Дополнительные сведения и примеры использования tooretrieve список допустимых изображений во время выполнения.
>
>

## <a name="create-a-linux-pool-batch-python"></a>Создание пула Linux: библиотека Python для пакетной службы
Hello следующем фрагменте кода показан пример того, как toouse hello [клиентская библиотека пакета Microsoft Azure для Python] [ py_batch_package] toocreate пул Ubuntu Server вычислительных узлов. Справочная документация для hello модуля Python пакета можно найти в [пакета azure.batch] [ py_batch_docs] на чтения hello документы.

В этом фрагменте кода явно создается объект [ImageReference][py_imagereference] и указывается каждое из его свойств (publisher, offer, SKU, version). В рабочем коде, однако мы рекомендуем использовать hello [list_node_agent_skus] [ py_list_skus] toodetermine метод и выберите из hello доступные изображения и узел агента SKU комбинаций во время выполнения.

```python
# Import hello required modules from the
# Azure Batch Client Library for Python
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify Batch account credentials
account = "<batch-account-name>"
key = "<batch-account-key>"
batch_url = "<batch-account-url>"

# Pool settings
pool_id = "LinuxNodesSamplePoolPython"
vm_size = "STANDARD_A1"
node_count = 1

# Initialize hello Batch client
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create hello unbound pool
new_pool = batchmodels.PoolAddParameter(id = pool_id, vm_size = vm_size)
new_pool.target_dedicated = node_count

# Configure hello start task for hello pool
start_task = batchmodels.StartTask()
start_task.run_elevated = True
start_task.command_line = "printenv AZ_BATCH_NODE_STARTUP_DIR"
new_pool.start_task = start_task

# Create an ImageReference which specifies hello Marketplace
# virtual machine image tooinstall on hello nodes.
ir = batchmodels.ImageReference(
    publisher = "Canonical",
    offer = "UbuntuServer",
    sku = "14.04.2-LTS",
    version = "latest")

# Create hello VirtualMachineConfiguration, specifying
# hello VM image reference and hello Batch node agent to
# be installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign hello virtual machine configuration toohello pool
new_pool.virtual_machine_configuration = vmc

# Create pool in hello Batch service
client.pool.add(new_pool)
```

Как упоминалось ранее, рекомендуется вместо создания hello [ImageReference] [ py_imagereference] явно, используйте hello [list_node_agent_skus] [ py_list_skus] toodynamically выберите метод hello в настоящее время поддерживаемые сочетания изображения агент/Marketplace узла. Здравствуйте, в следующем фрагменте кода показан Python как toouse этот метод.

```python
# Get hello list of node agents from hello Batch service
nodeagents = client.account.list_node_agent_skus()

# Obtain hello desired node agent
ubuntu1404agent = next(agent for agent in nodeagents if "ubuntu 14.04" in agent.id)

# Pick hello first image reference from hello list of verified references
ir = ubuntu1404agent.verified_image_references[0]

# Create hello VirtualMachineConfiguration, specifying hello VM image
# reference and hello Batch node agent toobe installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = ubuntu1404agent.id)
```

## <a name="create-a-linux-pool-batch-net"></a>Создание пула Linux: библиотека .NET для пакетной службы
Hello следующем фрагменте кода показан пример того, как toouse hello [пакета .NET] [ nuget_batch_net] toocreate библиотеки клиента пул Ubuntu Server вычислительных узлов. Можно найти hello [справочной документации пакета .NET] [ api_net] в библиотеке MSDN.

Hello следующий фрагмент кода использует hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] tooselect метод из списка hello комбинаций в настоящее время поддерживаются Marketplace изображения и узел агента SKU. Этот метод является предпочтительным, так как список поддерживаемых сочетаний hello может измениться из tootime времени. Чаще всего добавляются поддерживаемые сочетания.

```csharp
// Pool settings
const string poolId = "LinuxNodesSamplePoolDotNet";
const string vmSize = "STANDARD_A1";
const int nodeCount = 1;

// Obtain a collection of all available node agent SKUs.
// This allows us tooselect from a list of supported
// VM image/node agent combinations.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image
// that we wish toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. Note that there are one or more image
// references associated with this node agent SKU.
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello VirtualMachineConfiguration for use when actually
// creating hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

// Create hello unbound pool object using hello VirtualMachineConfiguration
// created above
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    virtualMachineSize: vmSize,
    virtualMachineConfiguration: virtualMachineConfiguration,
    targetDedicatedComputeNodes: nodeCount);

// Commit hello pool toohello Batch service
await pool.CommitAsync();
```

Хотя в предыдущем фрагменте hello используется hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] метод toodynamically список и выберите из поддерживается изображения и узел агента SKU сочетания (рекомендуется), можно также настроить [ImageReference] [ net_imagereference] явным образом:

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a>Список образов виртуальных машин
Hello следующей таблице перечислены образы виртуальных машин Marketplace hello, совместимых с hello доступных агентов узел пакета на момент последнего обновления в этой статье. Это важные toonote, что этот список не является предписывающим, так как изображения и агенты узел может добавлять или удалять в любое время. Мы рекомендуем пакета приложения и службы всегда использовать [list_node_agent_skus] [ py_list_skus] (Python) и [ListNodeAgentSkus] [ net_list_skus] Toodetermine (пакет .NET) и выберите из hello в настоящее время доступные номера SKU.

> [!WARNING]
> После списка Hello может измениться в любое время. Всегда используйте hello **агент узла списка SKU** методов, доступных в API-интерфейсы пакета toolist hello hello совместимую виртуальную машину и узел агента SKU, при выполнении пакетных заданий.
>
>

| **Издатель** | **ПРЕДЛОЖЕНИЕ** | **Номер SKU образа** | **Версия** | **Идентификатор SKU агента узла** |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| Canonical | UbuntuServer | 14.04.5-LTS | последних | batch.node.ubuntu 14.04 |
| Canonical | UbuntuServer | 16.04.0-LTS | последних | batch.node.ubuntu 16.04 |
| Credativ | Debian | 8 | последних | batch.node.debian 8 |
| OpenLogic | CentOS | 7.0 | последних | batch.node.centos 7 |
| OpenLogic | CentOS | 7.1. | последних | batch.node.centos 7 |
| OpenLogic | CentOS-HPC | 7.1. | последних | batch.node.centos 7 |
| OpenLogic | CentOS | 7,2 | последних | batch.node.centos 7 |
| Oracle | Oracle-Linux | 7.0 | последних | batch.node.centos 7 |
| Oracle | Oracle-Linux | 7,2 | последних | batch.node.centos 7 |
| SUSE | openSUSE | 13.2 | последних | batch.node.opensuse 13.2 |
| SUSE | openSUSE-Leap | 42.1 | последних | batch.node.opensuse 42.1 |
| SUSE | SLES | 12-SP1 | последних | batch.node.opensuse 42.1 |
| SUSE | SLES-HPC | 12-SP1 | последних | batch.node.opensuse 42.1 |
| microsoft-ads | linux-data-science-vm | linuxdsvm | последних | batch.node.centos 7; |
| microsoft-ads | standard-data-science-vm | standard-data-science-vm | последних | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2008-R2-SP1 | последних | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2012-Datacenter | последних | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2012-R2-Datacenter | последних | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2016-Datacenter | последних | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2016-Datacenter-with-Containers | последних | batch.node.windows amd64 |

## <a name="connect-toolinux-nodes-using-ssh"></a>Соединяют узлы tooLinux с помощью SSH
Во время разработки или во время устранения неполадок может оказаться необходимые toosign toohello узлов в пуле. В отличие от вычислительных узлов Windows нельзя использовать узлы tooLinux tooconnect удаленного рабочего стола (RDP). Вместо этого hello пакетная служба предоставляет доступ для SSH на каждом узле для удаленного подключения.

Hello следующий фрагмент кода Python создает пользователя на каждом узле в пуле, который необходим для удаленного подключения. Затем выводятся на печать сведения о соединении hello безопасного shell (SSH) для каждого узла.

```python
import datetime
import getpass
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify your own account credentials
batch_account_name = ''
batch_account_key = ''
batch_account_url = ''

# Specify hello ID of an existing pool containing Linux nodes
# currently in hello 'idle' state
pool_id = ''

# Specify hello username and prompt for a password
username = 'linuxuser'
password = getpass.getpass()

# Create a BatchClient
credentials = batchauth.SharedKeyCredentials(
    batch_account_name,
    batch_account_key
)
batch_client = batch.BatchServiceClient(
        credentials,
        base_url=batch_account_url
)

# Create hello user that will be added tooeach node in hello pool
user = batchmodels.ComputeNodeUser(username)
user.password = password
user.is_admin = True
user.expiry_time = \
    (datetime.datetime.today() + datetime.timedelta(days=30)).isoformat()

# Get hello list of nodes in hello pool
nodes = batch_client.compute_node.list(pool_id)

# Add hello user tooeach node in hello pool and print
# hello connection information for hello node
for node in nodes:
    # Add hello user toohello node
    batch_client.compute_node.add_user(pool_id, node.id, user)

    # Obtain SSH login information for hello node
    login = batch_client.compute_node.get_remote_login_settings(pool_id,
                                                                node.id)

    # Print hello connection info for hello node
    print("{0} | {1} | {2} | {3}".format(node.id,
                                         node.state,
                                         login.remote_login_ip_address,
                                         login.remote_login_port))
```

Ниже приведен пример выходных данных для предыдущего кода hello для пула, который содержит четыре узла Linux:

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

При создании пользователя на узле вместо пароля можно указать открытый ключ SSH. В hello Python SDK, используйте hello **ssh_public_key** параметр на [ComputeNodeUser][py_computenodeuser]. В .NET, используйте hello [ComputeNodeUser][net_computenodeuser].[ Параметры SshPublicKey] [ net_ssh_key] свойство.

## <a name="pricing"></a>Цены
Пакетная служба Azure основана на технологии виртуальных машин Azure и облачных служб Azure. Hello пакетная служба сама предлагается бесплатно, что означает, что плата взимается только для hello вычислений ресурсы, которые потребляют пакета решения. При выборе **конфигурация облачных служб**, взимается плата, в зависимости от hello [облачные службы цены] [ cloud_services_pricing] структуры. При выборе **конфигурации виртуальной машины**, взимается плата, в зависимости от hello [ценах — виртуальные машины] [ vm_pricing] структуры. 

При развертывании приложения tooyour пакета узлов с помощью [пакетов приложений](batch-application-packages.md), также взимается плата за ресурсы хранилища Azure hello, использовать пакеты приложения. Как правило затраты на хранилище Azure hello минимальны. 

## <a name="next-steps"></a>Дальнейшие действия
### <a name="batch-python-tutorial"></a>Учебник по пакетной службе (Python)
Более подробное руководство о том, как toowork с использованием пакета с помощью Python, извлечение [приступить к работе с клиентом Azure пакета Python hello](batch-python-tutorial.md). Его дополнительное [образец кода] [ github_samples_pyclient] включает вспомогательная функция `get_vm_config_for_distro`, tooobtain другой метод, отображающий конфигурации виртуальной машины.

### <a name="batch-python-code-samples"></a>Примеры кода Python для пакетной службы
Hello [примеры кода Python] [ github_samples_py] в hello [образцы azure пакета] [ github_samples] репозитория в GitHub содержит скрипты, которые показывают, как tooperform Общие пакетных операций, таких как пул, задания и создания задачи. Hello [README] [ github_py_readme] , сопровождающее образцы Python hello подробно описываются как tooinstall hello необходимые пакеты.

### <a name="batch-forum"></a>Форум по Пакетной службе
Hello [форум по пакетной Azure] [ forum] на сайте MSDN — лучшие поместите toodiscuss пакета и ответы на вопросы о службе hello. Изучайте полезные "закрепленные" публикации и задавайте вопросы, возникающие во время сборки решений пакетной службы.

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[cloud_services_pricing]: https://azure.microsoft.com/pricing/details/cloud-services/
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_py_readme]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/README.md
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_py]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[github_samples_pyclient]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/python_tutorial_client.py
[portal]: https://portal.azure.com
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_computenodeuser]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.aspx
[net_imagereference]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.imagereference.aspx
[net_list_skus]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listnodeagentskus.aspx
[net_pool_ops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.aspx
[net_ssh_key]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.sshpublickey.aspx
[nuget_batch_net]: https://www.nuget.org/packages/Azure.Batch/
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_list_skus]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
[vm_pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/
