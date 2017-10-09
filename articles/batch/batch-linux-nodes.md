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
# <a name="provision-linux-compute-nodes-in-batch-pools"></a><span data-ttu-id="4a36c-103">Подготовка вычислительных узлов Linux в пулах пакетной службы</span><span class="sxs-lookup"><span data-stu-id="4a36c-103">Provision Linux compute nodes in Batch pools</span></span>

<span data-ttu-id="4a36c-104">Можно использовать пакетной службы Azure toorun параллельных вычислительных рабочих нагрузок на виртуальных машинах Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="4a36c-104">You can use Azure Batch toorun parallel compute workloads on both Linux and Windows virtual machines.</span></span> <span data-ttu-id="4a36c-105">В этой статье описаны как пулы toocreate Linux узлы вычисления в hello пакетной службы с помощью обоих hello [пакета Python] [ py_batch_package] и [пакета .NET] [ api_net] клиентских библиотек.</span><span class="sxs-lookup"><span data-stu-id="4a36c-105">This article details how toocreate pools of Linux compute nodes in hello Batch service by using both hello [Batch Python][py_batch_package] and [Batch .NET][api_net] client libraries.</span></span>

> [!NOTE]
> <span data-ttu-id="4a36c-106">Пакеты приложений поддерживаются во всех пулах пакетной службы, созданных после 5 июля 2017 г.</span><span class="sxs-lookup"><span data-stu-id="4a36c-106">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="4a36c-107">Они поддерживаются в пулах пакета, созданные между 10 марта 2016 г. и 5 июля 2017 г., только в том случае, если пул hello был создан с помощью конфигурации облачной службы.</span><span class="sxs-lookup"><span data-stu-id="4a36c-107">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="4a36c-108">Пакеты приложений не поддерживают пулы пакета, созданные предыдущей too10 марта 2016 г.</span><span class="sxs-lookup"><span data-stu-id="4a36c-108">Batch pools created prior too10 March 2016 do not support application packages.</span></span> <span data-ttu-id="4a36c-109">Дополнительные сведения об использовании приложения пакетах toodeploy узлы tooyour пакета приложений, в разделе [развертывания приложений toocompute узлов с пакетами приложения пакета](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="4a36c-109">For more information about using application packages toodeploy your applications tooyour Batch nodes, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>
>
>

## <a name="virtual-machine-configuration"></a><span data-ttu-id="4a36c-110">Конфигурация виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="4a36c-110">Virtual machine configuration</span></span>
<span data-ttu-id="4a36c-111">При создании пула вычислительных узлов в пакете есть два способа из какой размер узла tooselect hello и операционной системы: Конфигурация облачных служб и конфигурации виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4a36c-111">When you create a pool of compute nodes in Batch, you have two options from which tooselect hello node size and operating system: Cloud Services Configuration and Virtual Machine Configuration.</span></span>

<span data-ttu-id="4a36c-112">**Cloud Services Configuration** (Конфигурация облачных служб) предоставляет *только*вычислительные узлы Windows.</span><span class="sxs-lookup"><span data-stu-id="4a36c-112">**Cloud Services Configuration** provides Windows compute nodes *only*.</span></span> <span data-ttu-id="4a36c-113">Размеры доступных вычислительных узлов, перечислены в [размеров для облачных служб](../cloud-services/cloud-services-sizes-specs.md), и доступных операционных систем перечисленных в hello [выпуски гостевой ОС Azure и Матрица совместимости пакетов SDK](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="4a36c-113">Available compute node sizes are listed in [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md), and available operating systems are listed in hello [Azure Guest OS releases and SDK compatibility matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> <span data-ttu-id="4a36c-114">При создании пула, который содержит узлы для облачных служб Azure, необходимо указать размер узла hello и hello семейства ОС, которые описаны в hello упомянутых выше статьи.</span><span class="sxs-lookup"><span data-stu-id="4a36c-114">When you create a pool that contains Azure Cloud Services nodes, you specify hello node size and hello OS family, which are described in hello previously mentioned articles.</span></span> <span data-ttu-id="4a36c-115">Для пулов вычислительных узлов Windows чаще всего используются облачные службы.</span><span class="sxs-lookup"><span data-stu-id="4a36c-115">For pools of Windows compute nodes, Cloud Services is most commonly used.</span></span>

<span data-ttu-id="4a36c-116">**Virtual Machine Configuration** предоставляет образы Windows и Linux для вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="4a36c-116">**Virtual Machine Configuration** provides both Linux and Windows images for compute nodes.</span></span> <span data-ttu-id="4a36c-117">Доступные размеры вычислительных узлов перечислены в статьях [Размеры виртуальных машин в Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) и [Размеры виртуальных машин в Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span><span class="sxs-lookup"><span data-stu-id="4a36c-117">Available compute node sizes are listed in [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span></span> <span data-ttu-id="4a36c-118">При создании пула, содержащего узлы конфигурации виртуальной машины, необходимо указать размер hello узлы hello, ссылка на изображение виртуальной машины hello и hello пакета узел агента SKU toobe на узлах, hello.</span><span class="sxs-lookup"><span data-stu-id="4a36c-118">When you create a pool that contains Virtual Machine Configuration nodes, you must specify hello size of hello nodes, hello virtual machine image reference, and hello Batch node agent SKU toobe installed on hello nodes.</span></span>

### <a name="virtual-machine-image-reference"></a><span data-ttu-id="4a36c-119">Ссылка на образ виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="4a36c-119">Virtual machine image reference</span></span>
<span data-ttu-id="4a36c-120">Здравствуйте, пакетная служба использует [наборы масштабирования виртуальных машин](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="4a36c-120">hello Batch service uses [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux compute nodes.</span></span> <span data-ttu-id="4a36c-121">Можно задать изображение из hello [Azure Marketplace][vm_marketplace], или укажите пользовательского образа, который был подготовлен.</span><span class="sxs-lookup"><span data-stu-id="4a36c-121">You can specify an image from hello [Azure Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span> <span data-ttu-id="4a36c-122">Дополнительные сведения о пользовательских образах см. в руководстве по [разработке решений для крупномасштабных параллельных вычислений с помощью пакетной службы](batch-api-basics.md#pool).</span><span class="sxs-lookup"><span data-stu-id="4a36c-122">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

<span data-ttu-id="4a36c-123">При настройке ссылку образ виртуальной машины, необходимо указать hello свойств hello образ виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4a36c-123">When you configure a virtual machine image reference, you specify hello properties of hello virtual machine image.</span></span> <span data-ttu-id="4a36c-124">следующие свойства Hello необходимы при создании ссылки образ виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="4a36c-124">hello following properties are required when you create a virtual machine image reference:</span></span>

| <span data-ttu-id="4a36c-125">**Свойства ссылки на образ**</span><span class="sxs-lookup"><span data-stu-id="4a36c-125">**Image reference properties**</span></span> | <span data-ttu-id="4a36c-126">**Пример**</span><span class="sxs-lookup"><span data-stu-id="4a36c-126">**Example**</span></span> |
| --- | --- |
| <span data-ttu-id="4a36c-127">Издатель</span><span class="sxs-lookup"><span data-stu-id="4a36c-127">Publisher</span></span> |<span data-ttu-id="4a36c-128">Canonical</span><span class="sxs-lookup"><span data-stu-id="4a36c-128">Canonical</span></span> |
| <span data-ttu-id="4a36c-129">ПРЕДЛОЖЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="4a36c-129">Offer</span></span> |<span data-ttu-id="4a36c-130">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="4a36c-130">UbuntuServer</span></span> |
| <span data-ttu-id="4a36c-131">SKU</span><span class="sxs-lookup"><span data-stu-id="4a36c-131">SKU</span></span> |<span data-ttu-id="4a36c-132">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="4a36c-132">14.04.4-LTS</span></span> |
| <span data-ttu-id="4a36c-133">Версия</span><span class="sxs-lookup"><span data-stu-id="4a36c-133">Version</span></span> |<span data-ttu-id="4a36c-134">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-134">latest</span></span> |

> [!TIP]
> <span data-ttu-id="4a36c-135">Дополнительные сведения об этих свойствах и как образы toolist Marketplace в [перейдите и выберите образы виртуальных машин Linux в Azure с помощью интерфейса командной строки или PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4a36c-135">You can learn more about these properties and how toolist Marketplace images in [Navigate and select Linux virtual machine images in Azure with CLI or PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4a36c-136">Обратите внимание, что не все образы из Marketplace в настоящее время совместимы с пакетной службой.</span><span class="sxs-lookup"><span data-stu-id="4a36c-136">Note that not all Marketplace images are currently compatible with Batch.</span></span> <span data-ttu-id="4a36c-137">Дополнительные сведения см. в разделе [Номер SKU агента узла](#node-agent-sku).</span><span class="sxs-lookup"><span data-stu-id="4a36c-137">For more information, see [Node agent SKU](#node-agent-sku).</span></span>
>
>

### <a name="node-agent-sku"></a><span data-ttu-id="4a36c-138">Номер SKU агента узла</span><span class="sxs-lookup"><span data-stu-id="4a36c-138">Node agent SKU</span></span>
<span data-ttu-id="4a36c-139">агент узла Hello пакета — программа, которая запускается на каждом узле в пуле hello и предоставляет интерфейс команды управления hello между узлом hello и hello пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="4a36c-139">hello Batch node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="4a36c-140">Существуют различные реализации агента узла hello, известный как SKU для разных операционных систем.</span><span class="sxs-lookup"><span data-stu-id="4a36c-140">There are different implementations of hello node agent, known as SKUs, for different operating systems.</span></span> <span data-ttu-id="4a36c-141">По сути при создании конфигурации виртуальной машины, сначала указывается ссылка на изображение hello виртуальной машины и укажите hello узел агента tooinstall на изображении hello.</span><span class="sxs-lookup"><span data-stu-id="4a36c-141">Essentially, when you create a Virtual Machine Configuration, you first specify hello virtual machine image reference, and then you specify hello node agent tooinstall on hello image.</span></span> <span data-ttu-id="4a36c-142">Как правило, каждый номер SKU агента узла совместим с несколькими образами виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="4a36c-142">Typically, each node agent SKU is compatible with multiple virtual machine images.</span></span> <span data-ttu-id="4a36c-143">Вот несколько примеров номеров SKU агентов узлов:</span><span class="sxs-lookup"><span data-stu-id="4a36c-143">Here are a few examples of node agent SKUs:</span></span>

* <span data-ttu-id="4a36c-144">batch.node.ubuntu 14.04;</span><span class="sxs-lookup"><span data-stu-id="4a36c-144">batch.node.ubuntu 14.04</span></span>
* <span data-ttu-id="4a36c-145">batch.node.centos 7;</span><span class="sxs-lookup"><span data-stu-id="4a36c-145">batch.node.centos 7</span></span>
* <span data-ttu-id="4a36c-146">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="4a36c-146">batch.node.windows amd64</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a36c-147">Не все образы виртуальных машин, доступных в hello Marketplace, несовместимы с hello в настоящее время доступных пакета узел агентов.</span><span class="sxs-lookup"><span data-stu-id="4a36c-147">Not all virtual machine images that are available in hello Marketplace are compatible with hello currently available Batch node agents.</span></span> <span data-ttu-id="4a36c-148">Пакет SDK toolist hello hello доступный узел, агент SKU и hello образы виртуальных машин, с которыми они совместимы.</span><span class="sxs-lookup"><span data-stu-id="4a36c-148">Use hello Batch SDKs toolist hello available node agent SKUs and hello virtual machine images with which they are compatible.</span></span> <span data-ttu-id="4a36c-149">В разделе hello [образы список виртуальных машин](#list-of-virtual-machine-images) далее в этой статье, Дополнительные сведения и примеры использования tooretrieve список допустимых изображений во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="4a36c-149">See hello [List of Virtual Machine images](#list-of-virtual-machine-images) later in this article for more information and examples of how tooretrieve a list of valid images at runtime.</span></span>
>
>

## <a name="create-a-linux-pool-batch-python"></a><span data-ttu-id="4a36c-150">Создание пула Linux: библиотека Python для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="4a36c-150">Create a Linux pool: Batch Python</span></span>
<span data-ttu-id="4a36c-151">Hello следующем фрагменте кода показан пример того, как toouse hello [клиентская библиотека пакета Microsoft Azure для Python] [ py_batch_package] toocreate пул Ubuntu Server вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="4a36c-151">hello following code snippet shows an example of how toouse hello [Microsoft Azure Batch Client Library for Python][py_batch_package] toocreate a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="4a36c-152">Справочная документация для hello модуля Python пакета можно найти в [пакета azure.batch] [ py_batch_docs] на чтения hello документы.</span><span class="sxs-lookup"><span data-stu-id="4a36c-152">Reference documentation for hello Batch Python module can be found at [azure.batch package][py_batch_docs] on Read hello Docs.</span></span>

<span data-ttu-id="4a36c-153">В этом фрагменте кода явно создается объект [ImageReference][py_imagereference] и указывается каждое из его свойств (publisher, offer, SKU, version).</span><span class="sxs-lookup"><span data-stu-id="4a36c-153">This snippet creates an [ImageReference][py_imagereference] explicitly and specifies each of its properties (publisher, offer, SKU, version).</span></span> <span data-ttu-id="4a36c-154">В рабочем коде, однако мы рекомендуем использовать hello [list_node_agent_skus] [ py_list_skus] toodetermine метод и выберите из hello доступные изображения и узел агента SKU комбинаций во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="4a36c-154">In production code, however, we recommend that you use hello [list_node_agent_skus][py_list_skus] method toodetermine and select from hello available image and node agent SKU combinations at runtime.</span></span>

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

<span data-ttu-id="4a36c-155">Как упоминалось ранее, рекомендуется вместо создания hello [ImageReference] [ py_imagereference] явно, используйте hello [list_node_agent_skus] [ py_list_skus] toodynamically выберите метод hello в настоящее время поддерживаемые сочетания изображения агент/Marketplace узла.</span><span class="sxs-lookup"><span data-stu-id="4a36c-155">As mentioned previously, we recommend that instead of creating hello [ImageReference][py_imagereference] explicitly, you use hello [list_node_agent_skus][py_list_skus] method toodynamically select from hello currently supported node agent/Marketplace image combinations.</span></span> <span data-ttu-id="4a36c-156">Здравствуйте, в следующем фрагменте кода показан Python как toouse этот метод.</span><span class="sxs-lookup"><span data-stu-id="4a36c-156">hello following Python snippet shows how toouse this method.</span></span>

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

## <a name="create-a-linux-pool-batch-net"></a><span data-ttu-id="4a36c-157">Создание пула Linux: библиотека .NET для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="4a36c-157">Create a Linux pool: Batch .NET</span></span>
<span data-ttu-id="4a36c-158">Hello следующем фрагменте кода показан пример того, как toouse hello [пакета .NET] [ nuget_batch_net] toocreate библиотеки клиента пул Ubuntu Server вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="4a36c-158">hello following code snippet shows an example of how toouse hello [Batch .NET][nuget_batch_net] client library toocreate a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="4a36c-159">Можно найти hello [справочной документации пакета .NET] [ api_net] в библиотеке MSDN.</span><span class="sxs-lookup"><span data-stu-id="4a36c-159">You can find hello [Batch .NET reference documentation][api_net] on MSDN.</span></span>

<span data-ttu-id="4a36c-160">Hello следующий фрагмент кода использует hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] tooselect метод из списка hello комбинаций в настоящее время поддерживаются Marketplace изображения и узел агента SKU.</span><span class="sxs-lookup"><span data-stu-id="4a36c-160">hello following code snippet uses hello [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method tooselect from hello list of currently supported Marketplace image and node agent SKU combinations.</span></span> <span data-ttu-id="4a36c-161">Этот метод является предпочтительным, так как список поддерживаемых сочетаний hello может измениться из tootime времени.</span><span class="sxs-lookup"><span data-stu-id="4a36c-161">This technique is desirable because hello list of supported combinations may change from time tootime.</span></span> <span data-ttu-id="4a36c-162">Чаще всего добавляются поддерживаемые сочетания.</span><span class="sxs-lookup"><span data-stu-id="4a36c-162">Most commonly, supported combinations are added.</span></span>

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

<span data-ttu-id="4a36c-163">Хотя в предыдущем фрагменте hello используется hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] метод toodynamically список и выберите из поддерживается изображения и узел агента SKU сочетания (рекомендуется), можно также настроить [ImageReference] [ net_imagereference] явным образом:</span><span class="sxs-lookup"><span data-stu-id="4a36c-163">Although hello previous snippet uses hello [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method toodynamically list and select from supported image and node agent SKU combinations (recommended), you can also configure an [ImageReference][net_imagereference] explicitly:</span></span>

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a><span data-ttu-id="4a36c-164">Список образов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="4a36c-164">List of virtual machine images</span></span>
<span data-ttu-id="4a36c-165">Hello следующей таблице перечислены образы виртуальных машин Marketplace hello, совместимых с hello доступных агентов узел пакета на момент последнего обновления в этой статье.</span><span class="sxs-lookup"><span data-stu-id="4a36c-165">hello following table lists hello Marketplace virtual machine images that are compatible with hello available Batch node agents when this article was last updated.</span></span> <span data-ttu-id="4a36c-166">Это важные toonote, что этот список не является предписывающим, так как изображения и агенты узел может добавлять или удалять в любое время.</span><span class="sxs-lookup"><span data-stu-id="4a36c-166">It is important toonote that this list is not definitive because images and node agents may be added or removed at any time.</span></span> <span data-ttu-id="4a36c-167">Мы рекомендуем пакета приложения и службы всегда использовать [list_node_agent_skus] [ py_list_skus] (Python) и [ListNodeAgentSkus] [ net_list_skus] Toodetermine (пакет .NET) и выберите из hello в настоящее время доступные номера SKU.</span><span class="sxs-lookup"><span data-stu-id="4a36c-167">We recommend that your Batch applications and services always use [list_node_agent_skus][py_list_skus] (Python) and [ListNodeAgentSkus][net_list_skus] (Batch .NET) toodetermine and select from hello currently available SKUs.</span></span>

> [!WARNING]
> <span data-ttu-id="4a36c-168">После списка Hello может измениться в любое время.</span><span class="sxs-lookup"><span data-stu-id="4a36c-168">hello following list may change at any time.</span></span> <span data-ttu-id="4a36c-169">Всегда используйте hello **агент узла списка SKU** методов, доступных в API-интерфейсы пакета toolist hello hello совместимую виртуальную машину и узел агента SKU, при выполнении пакетных заданий.</span><span class="sxs-lookup"><span data-stu-id="4a36c-169">Always use hello **list node agent SKU** methods available in hello Batch APIs toolist hello compatible virtual machine and node agent SKUs when you run your Batch jobs.</span></span>
>
>

| <span data-ttu-id="4a36c-170">**Издатель**</span><span class="sxs-lookup"><span data-stu-id="4a36c-170">**Publisher**</span></span> | <span data-ttu-id="4a36c-171">**ПРЕДЛОЖЕНИЕ**</span><span class="sxs-lookup"><span data-stu-id="4a36c-171">**Offer**</span></span> | <span data-ttu-id="4a36c-172">**Номер SKU образа**</span><span class="sxs-lookup"><span data-stu-id="4a36c-172">**Image SKU**</span></span> | <span data-ttu-id="4a36c-173">**Версия**</span><span class="sxs-lookup"><span data-stu-id="4a36c-173">**Version**</span></span> | <span data-ttu-id="4a36c-174">**Идентификатор SKU агента узла**</span><span class="sxs-lookup"><span data-stu-id="4a36c-174">**Node agent SKU ID**</span></span> |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| <span data-ttu-id="4a36c-175">Canonical</span><span class="sxs-lookup"><span data-stu-id="4a36c-175">Canonical</span></span> | <span data-ttu-id="4a36c-176">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="4a36c-176">UbuntuServer</span></span> | <span data-ttu-id="4a36c-177">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="4a36c-177">14.04.5-LTS</span></span> | <span data-ttu-id="4a36c-178">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-178">latest</span></span> | <span data-ttu-id="4a36c-179">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="4a36c-179">batch.node.ubuntu 14.04</span></span> |
| <span data-ttu-id="4a36c-180">Canonical</span><span class="sxs-lookup"><span data-stu-id="4a36c-180">Canonical</span></span> | <span data-ttu-id="4a36c-181">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="4a36c-181">UbuntuServer</span></span> | <span data-ttu-id="4a36c-182">16.04.0-LTS</span><span class="sxs-lookup"><span data-stu-id="4a36c-182">16.04.0-LTS</span></span> | <span data-ttu-id="4a36c-183">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-183">latest</span></span> | <span data-ttu-id="4a36c-184">batch.node.ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="4a36c-184">batch.node.ubuntu 16.04</span></span> |
| <span data-ttu-id="4a36c-185">Credativ</span><span class="sxs-lookup"><span data-stu-id="4a36c-185">Credativ</span></span> | <span data-ttu-id="4a36c-186">Debian</span><span class="sxs-lookup"><span data-stu-id="4a36c-186">Debian</span></span> | <span data-ttu-id="4a36c-187">8</span><span class="sxs-lookup"><span data-stu-id="4a36c-187">8</span></span> | <span data-ttu-id="4a36c-188">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-188">latest</span></span> | <span data-ttu-id="4a36c-189">batch.node.debian 8</span><span class="sxs-lookup"><span data-stu-id="4a36c-189">batch.node.debian 8</span></span> |
| <span data-ttu-id="4a36c-190">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="4a36c-190">OpenLogic</span></span> | <span data-ttu-id="4a36c-191">CentOS</span><span class="sxs-lookup"><span data-stu-id="4a36c-191">CentOS</span></span> | <span data-ttu-id="4a36c-192">7.0</span><span class="sxs-lookup"><span data-stu-id="4a36c-192">7.0</span></span> | <span data-ttu-id="4a36c-193">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-193">latest</span></span> | <span data-ttu-id="4a36c-194">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="4a36c-194">batch.node.centos 7</span></span> |
| <span data-ttu-id="4a36c-195">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="4a36c-195">OpenLogic</span></span> | <span data-ttu-id="4a36c-196">CentOS</span><span class="sxs-lookup"><span data-stu-id="4a36c-196">CentOS</span></span> | <span data-ttu-id="4a36c-197">7.1.</span><span class="sxs-lookup"><span data-stu-id="4a36c-197">7.1</span></span> | <span data-ttu-id="4a36c-198">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-198">latest</span></span> | <span data-ttu-id="4a36c-199">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="4a36c-199">batch.node.centos 7</span></span> |
| <span data-ttu-id="4a36c-200">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="4a36c-200">OpenLogic</span></span> | <span data-ttu-id="4a36c-201">CentOS-HPC</span><span class="sxs-lookup"><span data-stu-id="4a36c-201">CentOS-HPC</span></span> | <span data-ttu-id="4a36c-202">7.1.</span><span class="sxs-lookup"><span data-stu-id="4a36c-202">7.1</span></span> | <span data-ttu-id="4a36c-203">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-203">latest</span></span> | <span data-ttu-id="4a36c-204">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="4a36c-204">batch.node.centos 7</span></span> |
| <span data-ttu-id="4a36c-205">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="4a36c-205">OpenLogic</span></span> | <span data-ttu-id="4a36c-206">CentOS</span><span class="sxs-lookup"><span data-stu-id="4a36c-206">CentOS</span></span> | <span data-ttu-id="4a36c-207">7,2</span><span class="sxs-lookup"><span data-stu-id="4a36c-207">7.2</span></span> | <span data-ttu-id="4a36c-208">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-208">latest</span></span> | <span data-ttu-id="4a36c-209">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="4a36c-209">batch.node.centos 7</span></span> |
| <span data-ttu-id="4a36c-210">Oracle</span><span class="sxs-lookup"><span data-stu-id="4a36c-210">Oracle</span></span> | <span data-ttu-id="4a36c-211">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="4a36c-211">Oracle-Linux</span></span> | <span data-ttu-id="4a36c-212">7.0</span><span class="sxs-lookup"><span data-stu-id="4a36c-212">7.0</span></span> | <span data-ttu-id="4a36c-213">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-213">latest</span></span> | <span data-ttu-id="4a36c-214">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="4a36c-214">batch.node.centos 7</span></span> |
| <span data-ttu-id="4a36c-215">Oracle</span><span class="sxs-lookup"><span data-stu-id="4a36c-215">Oracle</span></span> | <span data-ttu-id="4a36c-216">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="4a36c-216">Oracle-Linux</span></span> | <span data-ttu-id="4a36c-217">7,2</span><span class="sxs-lookup"><span data-stu-id="4a36c-217">7.2</span></span> | <span data-ttu-id="4a36c-218">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-218">latest</span></span> | <span data-ttu-id="4a36c-219">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="4a36c-219">batch.node.centos 7</span></span> |
| <span data-ttu-id="4a36c-220">SUSE</span><span class="sxs-lookup"><span data-stu-id="4a36c-220">SUSE</span></span> | <span data-ttu-id="4a36c-221">openSUSE</span><span class="sxs-lookup"><span data-stu-id="4a36c-221">openSUSE</span></span> | <span data-ttu-id="4a36c-222">13.2</span><span class="sxs-lookup"><span data-stu-id="4a36c-222">13.2</span></span> | <span data-ttu-id="4a36c-223">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-223">latest</span></span> | <span data-ttu-id="4a36c-224">batch.node.opensuse 13.2</span><span class="sxs-lookup"><span data-stu-id="4a36c-224">batch.node.opensuse 13.2</span></span> |
| <span data-ttu-id="4a36c-225">SUSE</span><span class="sxs-lookup"><span data-stu-id="4a36c-225">SUSE</span></span> | <span data-ttu-id="4a36c-226">openSUSE-Leap</span><span class="sxs-lookup"><span data-stu-id="4a36c-226">openSUSE-Leap</span></span> | <span data-ttu-id="4a36c-227">42.1</span><span class="sxs-lookup"><span data-stu-id="4a36c-227">42.1</span></span> | <span data-ttu-id="4a36c-228">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-228">latest</span></span> | <span data-ttu-id="4a36c-229">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="4a36c-229">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="4a36c-230">SUSE</span><span class="sxs-lookup"><span data-stu-id="4a36c-230">SUSE</span></span> | <span data-ttu-id="4a36c-231">SLES</span><span class="sxs-lookup"><span data-stu-id="4a36c-231">SLES</span></span> | <span data-ttu-id="4a36c-232">12-SP1</span><span class="sxs-lookup"><span data-stu-id="4a36c-232">12-SP1</span></span> | <span data-ttu-id="4a36c-233">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-233">latest</span></span> | <span data-ttu-id="4a36c-234">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="4a36c-234">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="4a36c-235">SUSE</span><span class="sxs-lookup"><span data-stu-id="4a36c-235">SUSE</span></span> | <span data-ttu-id="4a36c-236">SLES-HPC</span><span class="sxs-lookup"><span data-stu-id="4a36c-236">SLES-HPC</span></span> | <span data-ttu-id="4a36c-237">12-SP1</span><span class="sxs-lookup"><span data-stu-id="4a36c-237">12-SP1</span></span> | <span data-ttu-id="4a36c-238">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-238">latest</span></span> | <span data-ttu-id="4a36c-239">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="4a36c-239">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="4a36c-240">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="4a36c-240">microsoft-ads</span></span> | <span data-ttu-id="4a36c-241">linux-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="4a36c-241">linux-data-science-vm</span></span> | <span data-ttu-id="4a36c-242">linuxdsvm</span><span class="sxs-lookup"><span data-stu-id="4a36c-242">linuxdsvm</span></span> | <span data-ttu-id="4a36c-243">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-243">latest</span></span> | <span data-ttu-id="4a36c-244">batch.node.centos 7;</span><span class="sxs-lookup"><span data-stu-id="4a36c-244">batch.node.centos 7</span></span> |
| <span data-ttu-id="4a36c-245">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="4a36c-245">microsoft-ads</span></span> | <span data-ttu-id="4a36c-246">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="4a36c-246">standard-data-science-vm</span></span> | <span data-ttu-id="4a36c-247">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="4a36c-247">standard-data-science-vm</span></span> | <span data-ttu-id="4a36c-248">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-248">latest</span></span> | <span data-ttu-id="4a36c-249">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="4a36c-249">batch.node.windows amd64</span></span> |
| <span data-ttu-id="4a36c-250">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="4a36c-250">MicrosoftWindowsServer</span></span> | <span data-ttu-id="4a36c-251">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="4a36c-251">WindowsServer</span></span> | <span data-ttu-id="4a36c-252">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="4a36c-252">2008-R2-SP1</span></span> | <span data-ttu-id="4a36c-253">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-253">latest</span></span> | <span data-ttu-id="4a36c-254">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="4a36c-254">batch.node.windows amd64</span></span> |
| <span data-ttu-id="4a36c-255">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="4a36c-255">MicrosoftWindowsServer</span></span> | <span data-ttu-id="4a36c-256">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="4a36c-256">WindowsServer</span></span> | <span data-ttu-id="4a36c-257">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="4a36c-257">2012-Datacenter</span></span> | <span data-ttu-id="4a36c-258">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-258">latest</span></span> | <span data-ttu-id="4a36c-259">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="4a36c-259">batch.node.windows amd64</span></span> |
| <span data-ttu-id="4a36c-260">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="4a36c-260">MicrosoftWindowsServer</span></span> | <span data-ttu-id="4a36c-261">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="4a36c-261">WindowsServer</span></span> | <span data-ttu-id="4a36c-262">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="4a36c-262">2012-R2-Datacenter</span></span> | <span data-ttu-id="4a36c-263">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-263">latest</span></span> | <span data-ttu-id="4a36c-264">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="4a36c-264">batch.node.windows amd64</span></span> |
| <span data-ttu-id="4a36c-265">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="4a36c-265">MicrosoftWindowsServer</span></span> | <span data-ttu-id="4a36c-266">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="4a36c-266">WindowsServer</span></span> | <span data-ttu-id="4a36c-267">2016-Datacenter</span><span class="sxs-lookup"><span data-stu-id="4a36c-267">2016-Datacenter</span></span> | <span data-ttu-id="4a36c-268">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-268">latest</span></span> | <span data-ttu-id="4a36c-269">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="4a36c-269">batch.node.windows amd64</span></span> |
| <span data-ttu-id="4a36c-270">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="4a36c-270">MicrosoftWindowsServer</span></span> | <span data-ttu-id="4a36c-271">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="4a36c-271">WindowsServer</span></span> | <span data-ttu-id="4a36c-272">2016-Datacenter-with-Containers</span><span class="sxs-lookup"><span data-stu-id="4a36c-272">2016-Datacenter-with-Containers</span></span> | <span data-ttu-id="4a36c-273">последних</span><span class="sxs-lookup"><span data-stu-id="4a36c-273">latest</span></span> | <span data-ttu-id="4a36c-274">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="4a36c-274">batch.node.windows amd64</span></span> |

## <a name="connect-toolinux-nodes-using-ssh"></a><span data-ttu-id="4a36c-275">Соединяют узлы tooLinux с помощью SSH</span><span class="sxs-lookup"><span data-stu-id="4a36c-275">Connect tooLinux nodes using SSH</span></span>
<span data-ttu-id="4a36c-276">Во время разработки или во время устранения неполадок может оказаться необходимые toosign toohello узлов в пуле.</span><span class="sxs-lookup"><span data-stu-id="4a36c-276">During development or while troubleshooting, you may find it necessary toosign in toohello nodes in your pool.</span></span> <span data-ttu-id="4a36c-277">В отличие от вычислительных узлов Windows нельзя использовать узлы tooLinux tooconnect удаленного рабочего стола (RDP).</span><span class="sxs-lookup"><span data-stu-id="4a36c-277">Unlike Windows compute nodes, you cannot use Remote Desktop Protocol (RDP) tooconnect tooLinux nodes.</span></span> <span data-ttu-id="4a36c-278">Вместо этого hello пакетная служба предоставляет доступ для SSH на каждом узле для удаленного подключения.</span><span class="sxs-lookup"><span data-stu-id="4a36c-278">Instead, hello Batch service enables SSH access on each node for remote connection.</span></span>

<span data-ttu-id="4a36c-279">Hello следующий фрагмент кода Python создает пользователя на каждом узле в пуле, который необходим для удаленного подключения.</span><span class="sxs-lookup"><span data-stu-id="4a36c-279">hello following Python code snippet creates a user on each node in a pool, which is required for remote connection.</span></span> <span data-ttu-id="4a36c-280">Затем выводятся на печать сведения о соединении hello безопасного shell (SSH) для каждого узла.</span><span class="sxs-lookup"><span data-stu-id="4a36c-280">It then prints hello secure shell (SSH) connection information for each node.</span></span>

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

<span data-ttu-id="4a36c-281">Ниже приведен пример выходных данных для предыдущего кода hello для пула, который содержит четыре узла Linux:</span><span class="sxs-lookup"><span data-stu-id="4a36c-281">Here is sample output for hello previous code for a pool that contains four Linux nodes:</span></span>

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

<span data-ttu-id="4a36c-282">При создании пользователя на узле вместо пароля можно указать открытый ключ SSH.</span><span class="sxs-lookup"><span data-stu-id="4a36c-282">Instead of a password, you can specify an SSH public key when you create a user on a node.</span></span> <span data-ttu-id="4a36c-283">В hello Python SDK, используйте hello **ssh_public_key** параметр на [ComputeNodeUser][py_computenodeuser].</span><span class="sxs-lookup"><span data-stu-id="4a36c-283">In hello Python SDK, use hello **ssh_public_key** parameter on [ComputeNodeUser][py_computenodeuser].</span></span> <span data-ttu-id="4a36c-284">В .NET, используйте hello [ComputeNodeUser][net_computenodeuser].[ Параметры SshPublicKey] [ net_ssh_key] свойство.</span><span class="sxs-lookup"><span data-stu-id="4a36c-284">In .NET, use hello [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] property.</span></span>

## <a name="pricing"></a><span data-ttu-id="4a36c-285">Цены</span><span class="sxs-lookup"><span data-stu-id="4a36c-285">Pricing</span></span>
<span data-ttu-id="4a36c-286">Пакетная служба Azure основана на технологии виртуальных машин Azure и облачных служб Azure.</span><span class="sxs-lookup"><span data-stu-id="4a36c-286">Azure Batch is built on Azure Cloud Services and Azure Virtual Machines technology.</span></span> <span data-ttu-id="4a36c-287">Hello пакетная служба сама предлагается бесплатно, что означает, что плата взимается только для hello вычислений ресурсы, которые потребляют пакета решения.</span><span class="sxs-lookup"><span data-stu-id="4a36c-287">hello Batch service itself is offered at no cost, which means you are charged only for hello compute resources that your Batch solutions consume.</span></span> <span data-ttu-id="4a36c-288">При выборе **конфигурация облачных служб**, взимается плата, в зависимости от hello [облачные службы цены] [ cloud_services_pricing] структуры.</span><span class="sxs-lookup"><span data-stu-id="4a36c-288">When you choose **Cloud Services Configuration**, you are charged based on hello [Cloud Services pricing][cloud_services_pricing] structure.</span></span> <span data-ttu-id="4a36c-289">При выборе **конфигурации виртуальной машины**, взимается плата, в зависимости от hello [ценах — виртуальные машины] [ vm_pricing] структуры.</span><span class="sxs-lookup"><span data-stu-id="4a36c-289">When you choose **Virtual Machine Configuration**, you are charged based on hello [Virtual Machines pricing][vm_pricing] structure.</span></span> 

<span data-ttu-id="4a36c-290">При развертывании приложения tooyour пакета узлов с помощью [пакетов приложений](batch-application-packages.md), также взимается плата за ресурсы хранилища Azure hello, использовать пакеты приложения.</span><span class="sxs-lookup"><span data-stu-id="4a36c-290">If you deploy applications tooyour Batch nodes using [application packages](batch-application-packages.md), you are also charged for hello Azure Storage resources that your application packages consume.</span></span> <span data-ttu-id="4a36c-291">Как правило затраты на хранилище Azure hello минимальны.</span><span class="sxs-lookup"><span data-stu-id="4a36c-291">In general, hello Azure Storage costs are minimal.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4a36c-292">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4a36c-292">Next steps</span></span>
### <a name="batch-python-tutorial"></a><span data-ttu-id="4a36c-293">Учебник по пакетной службе (Python)</span><span class="sxs-lookup"><span data-stu-id="4a36c-293">Batch Python tutorial</span></span>
<span data-ttu-id="4a36c-294">Более подробное руководство о том, как toowork с использованием пакета с помощью Python, извлечение [приступить к работе с клиентом Azure пакета Python hello](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="4a36c-294">For a more in-depth tutorial about how toowork with Batch by using Python, check out [Get started with hello Azure Batch Python client](batch-python-tutorial.md).</span></span> <span data-ttu-id="4a36c-295">Его дополнительное [образец кода] [ github_samples_pyclient] включает вспомогательная функция `get_vm_config_for_distro`, tooobtain другой метод, отображающий конфигурации виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4a36c-295">Its companion [code sample][github_samples_pyclient] includes a helper function, `get_vm_config_for_distro`, that shows another technique tooobtain a virtual machine configuration.</span></span>

### <a name="batch-python-code-samples"></a><span data-ttu-id="4a36c-296">Примеры кода Python для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="4a36c-296">Batch Python code samples</span></span>
<span data-ttu-id="4a36c-297">Hello [примеры кода Python] [ github_samples_py] в hello [образцы azure пакета] [ github_samples] репозитория в GitHub содержит скрипты, которые показывают, как tooperform Общие пакетных операций, таких как пул, задания и создания задачи.</span><span class="sxs-lookup"><span data-stu-id="4a36c-297">hello [Python code samples][github_samples_py] in hello [azure-batch-samples][github_samples] repository on GitHub contain scripts that show you how tooperform common Batch operations, such as pool, job, and task creation.</span></span> <span data-ttu-id="4a36c-298">Hello [README] [ github_py_readme] , сопровождающее образцы Python hello подробно описываются как tooinstall hello необходимые пакеты.</span><span class="sxs-lookup"><span data-stu-id="4a36c-298">hello [README][github_py_readme] that accompanies hello Python samples has details about how tooinstall hello required packages.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="4a36c-299">Форум по Пакетной службе</span><span class="sxs-lookup"><span data-stu-id="4a36c-299">Batch forum</span></span>
<span data-ttu-id="4a36c-300">Hello [форум по пакетной Azure] [ forum] на сайте MSDN — лучшие поместите toodiscuss пакета и ответы на вопросы о службе hello.</span><span class="sxs-lookup"><span data-stu-id="4a36c-300">hello [Azure Batch Forum][forum] on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="4a36c-301">Изучайте полезные "закрепленные" публикации и задавайте вопросы, возникающие во время сборки решений пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="4a36c-301">Read helpful "pinned" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

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
