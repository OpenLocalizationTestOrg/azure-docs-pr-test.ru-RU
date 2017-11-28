---
title: "aaaSet копирование приложений MPI toorun кластера Linux RDMA | Документы Microsoft"
description: "Создать кластер размер toouse H16r, H16mr, A8 или A9 виртуальных машин Linux hello Azure RDMA сетевых toorun MPI приложениях"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a><span data-ttu-id="4c3c5-103">Настройка приложений MPI Linux RDMA toorun кластера</span><span class="sxs-lookup"><span data-stu-id="4c3c5-103">Set up a Linux RDMA cluster toorun MPI applications</span></span>
<span data-ttu-id="4c3c5-104">Узнайте, как кластер tooset копирование Linux RDMA в Azure с помощью [высокопроизводительных вычислений размеры виртуальных Машин](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun параллельных приложений интерфейса передачи сообщений (MPI).</span><span class="sxs-lookup"><span data-stu-id="4c3c5-104">Learn how tooset up a Linux RDMA cluster in Azure with [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun parallel Message Passing Interface (MPI) applications.</span></span> <span data-ttu-id="4c3c5-105">Эта статья содержит действия tooprepare toorun образа Linux HPC Intel MPI в кластере.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-105">This article provides steps tooprepare a Linux HPC image toorun Intel MPI on a cluster.</span></span> <span data-ttu-id="4c3c5-106">После подготовки развернуть кластер виртуальных машин с помощью этого образа и одну hello размеров ВМ с поддержкой RDMA Azure (в настоящее время H16r, H16mr, A8 или A9).</span><span class="sxs-lookup"><span data-stu-id="4c3c5-106">After preparation, you deploy a cluster of VMs using this image and one of hello RDMA-capable Azure VM sizes (currently H16r, H16mr, A8, or A9).</span></span> <span data-ttu-id="4c3c5-107">Используйте hello кластера toorun приложений MPI, эффективно взаимодействуют через низкой задержкой, высокой пропускной способностью сети на основе удаленного прямого доступа к памяти (RDMA) технологии.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-107">Use hello cluster toorun MPI applications that communicate efficiently over a low-latency, high-throughput network based on remote direct memory access (RDMA) technology.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4c3c5-108">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager](../../../resource-manager-deployment-model.md) и классическая модель.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-108">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="4c3c5-109">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="4c3c5-110">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

## <a name="cluster-deployment-options"></a><span data-ttu-id="4c3c5-111">Варианты развертывания кластера</span><span class="sxs-lookup"><span data-stu-id="4c3c5-111">Cluster deployment options</span></span>
<span data-ttu-id="4c3c5-112">Ниже перечислены методы, независимо от планировщика заданий можно использовать toocreate кластеров Linux RDMA.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-112">Following are methods you can use toocreate a Linux RDMA cluster with or without a job scheduler.</span></span>

* <span data-ttu-id="4c3c5-113">**Скрипты Azure CLI**: как показано далее в этой статье, использовать hello [интерфейс командной строки Azure](../../../cli-install-nodejs.md) (CLI) tooscript hello развертывания кластера виртуальных машин, имеющих функцию RDMA.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-113">**Azure CLI scripts**: As shown later in this article, use hello [Azure command-line interface](../../../cli-install-nodejs.md) (CLI) tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span> <span data-ttu-id="4c3c5-114">Hello CLI в режиме управления службой создает hello узлов кластера последовательно в hello классической модели развертывания, поэтому развертывание много вычислительных узлов может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-114">hello CLI in Service Management mode creates hello cluster nodes serially in hello classic deployment model, so deploying many compute nodes might take several minutes.</span></span> <span data-ttu-id="4c3c5-115">hello tooenable сетевое соединение RDMA при использовании hello классической модели развертывания, развертывания виртуальных машин hello в hello же облачной службе.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-115">tooenable hello RDMA network connection when you use hello classic deployment model, deploy hello VMs in hello same cloud service.</span></span>
* <span data-ttu-id="4c3c5-116">**Шаблоны Azure Resource Manager**: также можно использовать модель развертывания toodeploy кластер виртуальных машин, имеющих функцию RDMA, который подключается toohello сети RDMA для hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-116">**Azure Resource Manager templates**: You can also use hello Resource Manager deployment model toodeploy a cluster of RDMA-capable VMs that connects toohello RDMA network.</span></span> <span data-ttu-id="4c3c5-117">Вы можете [создать собственный шаблон](../../../resource-group-authoring-templates.md), или проверьте hello [шаблоны Azure краткое руководство](https://azure.microsoft.com/documentation/templates/) для шаблонов, представленные Microsoft или hello сообщества toodeploy hello решения, нужно.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-117">You can [create your own template](../../../resource-group-authoring-templates.md), or check hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/) for templates contributed by Microsoft or hello community toodeploy hello solution you want.</span></span> <span data-ttu-id="4c3c5-118">Шаблоны диспетчера ресурсов можно предоставить toodeploy быстрый и надежный способ кластеров Linux.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-118">Resource Manager templates can provide a fast and reliable way toodeploy a Linux cluster.</span></span> <span data-ttu-id="4c3c5-119">hello tooenable сетевое соединение RDMA при использовании модели развертывания диспетчера ресурсов hello, развертывание виртуальных машин hello в hello одной группе доступности.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-119">tooenable hello RDMA network connection when you use hello Resource Manager deployment model, deploy hello VMs in hello same availability set.</span></span>
* <span data-ttu-id="4c3c5-120">**Пакет HPC**: создайте кластер из пакета Microsoft HPC в Azure и добавить поддержку функции RDMA вычислительных узлов под управлением поддерживаемых к сети RDMA tooaccess распространения Linux hello.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-120">**HPC Pack**: Create a Microsoft HPC Pack cluster in Azure and add RDMA-capable compute nodes that run a supported Linux distribution tooaccess hello RDMA network.</span></span> <span data-ttu-id="4c3c5-121">Дополнительную информацию см. в статье [Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="4c3c5-121">For more information, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="sample-deployment-steps-in-hello-classic-model"></a><span data-ttu-id="4c3c5-122">Пример развертывания шагов в классической модели hello</span><span class="sxs-lookup"><span data-stu-id="4c3c5-122">Sample deployment steps in hello classic model</span></span>
<span data-ttu-id="4c3c5-123">Hello следующие шаги показывают, как настроить toouse hello Azure CLI toodeploy виртуальную Машину HPC SP1 SUSE Linux Enterprise Server (SLES) 12 hello Azure Marketplace и создать образ виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-123">hello following steps show how toouse hello Azure CLI toodeploy a SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM from hello Azure Marketplace, customize it, and create a custom VM image.</span></span> <span data-ttu-id="4c3c5-124">Затем можно использовать hello tooscript изображения hello развертывания кластера виртуальных машин, имеющих функцию RDMA.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-124">Then you can use hello image tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span>

> [!TIP]
> <span data-ttu-id="4c3c5-125">Используйте аналогичные действия toodeploy кластера функцией RDMA виртуальных машин на основании изображений на основе CentOS HPC в hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-125">Use similar steps toodeploy a cluster of RDMA-capable VMs based on CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="4c3c5-126">Некоторые шаги незначительно отличаются (мы указываем на это).</span><span class="sxs-lookup"><span data-stu-id="4c3c5-126">Some steps differ slightly, as noted.</span></span> 
>
>

### <a name="prerequisites"></a><span data-ttu-id="4c3c5-127">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4c3c5-127">Prerequisites</span></span>
* <span data-ttu-id="4c3c5-128">**Клиентский компьютер**: требуется toocommunicate компьютера Mac, Linux или Windows клиента с помощью Azure.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-128">**Client computer**: You need a Mac, Linux, or Windows client computer toocommunicate with Azure.</span></span> <span data-ttu-id="4c3c5-129">Далее предполагается, что вы используете клиент Linux.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-129">These steps assume you are using a Linux client.</span></span>
* <span data-ttu-id="4c3c5-130">**Подписка Azure**. Если у вас ее нет, можно за пару минут создать [бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="4c3c5-130">**Azure subscription**: If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span> <span data-ttu-id="4c3c5-131">Для больших кластеров можно использовать подписку с оплатой по мере использования или другие варианты приобретения.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-131">For larger clusters, consider a pay-as-you-go subscription or other purchase options.</span></span>
* <span data-ttu-id="4c3c5-132">**Доступность размер виртуальной Машины**: hello следующие размеры экземпляра являются поддержкой RDMA: H16r, H16mr, A8 и A9.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-132">**VM size availability**: hello following instance sizes are RDMA capable: H16r, H16mr, A8, and A9.</span></span> <span data-ttu-id="4c3c5-133">Проверьте [доступность продуктов по регионам](https://azure.microsoft.com/regions/services/) , чтобы узнать, в каких регионах Azure их можно использовать.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-133">Check [Products available by region](https://azure.microsoft.com/regions/services/) for availability in Azure regions.</span></span>
* <span data-ttu-id="4c3c5-134">**Квота ядер**: может потребоваться Квота hello tooincrease toodeploy ядра кластера виртуальных машин с большим объемом вычислений.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-134">**Cores quota**: You might need tooincrease hello quota of cores toodeploy a cluster of compute-intensive VMs.</span></span> <span data-ttu-id="4c3c5-135">Например менее 128 ядрами требуется, если требуется, чтобы ВМ A9 toodeploy 8, как показано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-135">For example, you need at least 128 cores if you want toodeploy 8 A9 VMs as shown in this article.</span></span> <span data-ttu-id="4c3c5-136">Подписки также может ограничить hello количество ядер, развертываемого в определенных семейств размер виртуальной Машины, включая hello H-series.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-136">Your subscription might also limit hello number of cores you can deploy in certain VM size families, including hello H-series.</span></span> <span data-ttu-id="4c3c5-137">toorequest увеличить квоту, [откройте запрос поддержки сети клиента](../../../azure-supportability/how-to-create-azure-support-request.md) бесплатно.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-137">toorequest a quota increase, [open an online customer support request](../../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
* <span data-ttu-id="4c3c5-138">**Azure CLI**: [установить](../../../cli-install-nodejs.md) hello Azure CLI и [подключения tooyour подписки Azure](../../../xplat-cli-connect.md) hello клиентского компьютера.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-138">**Azure CLI**: [Install](../../../cli-install-nodejs.md) hello Azure CLI and [connect tooyour Azure subscription](../../../xplat-cli-connect.md) from hello client computer.</span></span>

### <a name="provision-an-sles-12-sp1-hpc-vm"></a><span data-ttu-id="4c3c5-139">Подготовка виртуальной машины SLES 12 SP1 HPC</span><span class="sxs-lookup"><span data-stu-id="4c3c5-139">Provision an SLES 12 SP1 HPC VM</span></span>
<span data-ttu-id="4c3c5-140">После входа в tooAzure с hello Azure CLI, запустите `azure config list` tooconfirm, hello выходных данных показан режим службы управления.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-140">After signing in tooAzure with hello Azure CLI, run `azure config list` tooconfirm that hello output shows Service Management mode.</span></span> <span data-ttu-id="4c3c5-141">Если нет, установите режим hello, запустив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4c3c5-141">If it does not, set hello mode by running this command:</span></span>

    azure config mode asm


<span data-ttu-id="4c3c5-142">Введите следующие toolist hello все подписки hello вы являетесь авторизованным toouse:</span><span class="sxs-lookup"><span data-stu-id="4c3c5-142">Type hello following toolist all hello subscriptions you are authorized toouse:</span></span>

    azure account list

<span data-ttu-id="4c3c5-143">Hello текущей активной подписки обозначена `Current` значение слишком`true`.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-143">hello current active subscription is identified with `Current` set too`true`.</span></span> <span data-ttu-id="4c3c5-144">Если эта подписка не hello тот, который toouse toocreate hello кластера, назначить идентификатор hello соответствующие подписки hello активной подписки:</span><span class="sxs-lookup"><span data-stu-id="4c3c5-144">If this subscription isn't hello one you want toouse toocreate hello cluster, set hello appropriate subscription ID as hello active subscription:</span></span>

    azure account set <subscription-Id>

<span data-ttu-id="4c3c5-145">общедоступные образы SLES 12 SP1 HPC в Azure, выполните такую команду hello следующие, при условии, что среда поддерживает ваш оболочки hello toosee **grep**:</span><span class="sxs-lookup"><span data-stu-id="4c3c5-145">toosee hello publicly available SLES 12 SP1 HPC images in Azure, run a command like hello following, assuming your shell environment supports **grep**:</span></span>

    azure vm image list | grep "suse.*hpc"

<span data-ttu-id="4c3c5-146">Подготовить функцией RDMA ВМ с помощью образа SLES 12 SP1 HPC, выполнив команду hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4c3c5-146">Provision an RDMA-capable VM with a SLES 12 SP1 HPC image by running a command like hello following:</span></span>

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

<span data-ttu-id="4c3c5-147">Описание</span><span class="sxs-lookup"><span data-stu-id="4c3c5-147">Where:</span></span>

* <span data-ttu-id="4c3c5-148">Здравствуйте, размер (в данном примере — A9) является одним из размеров виртуальных Машин hello функцией RDMA.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-148">hello size (A9 in this example) is one of hello RDMA-capable VM sizes.</span></span>
* <span data-ttu-id="4c3c5-149">номер порта внешних SSH для Hello (22 в этом примере — hello SSH по умолчанию) — любой допустимый номер порта.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-149">hello external SSH port number (22 in this example, which is hello SSH default) is any valid port number.</span></span> <span data-ttu-id="4c3c5-150">Hello внутренний номер порта SSH устанавливается too22.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-150">hello internal SSH port number is set too22.</span></span>
* <span data-ttu-id="4c3c5-151">Новой облачной службы создается в hello Azure область, задаваемую расположение hello.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-151">A new cloud service is created in hello Azure region specified by hello location.</span></span> <span data-ttu-id="4c3c5-152">Укажите расположение, в какие hello виртуальной Машины доступен выбранного размера.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-152">Specify a location in which hello VM size you choose is available.</span></span>
* <span data-ttu-id="4c3c5-153">Для поддержки назначения приоритета SUSE (что влечет за собой дополнительной оплаты) имя образа hello SLES 12 SP1 в настоящее время может принимать одно из этих двух вариантов:</span><span class="sxs-lookup"><span data-stu-id="4c3c5-153">For SUSE priority support (which incurs additional charges), hello SLES 12 SP1 image name currently can be one of these two options:</span></span> 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a><span data-ttu-id="4c3c5-154">Настройка hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="4c3c5-154">Customize hello VM</span></span>
<span data-ttu-id="4c3c5-155">По завершении подготовки виртуальной Машины hello toohello SSH виртуальной Машины с помощью hello внешний IP-адрес Виртуальной машины (или DNS-имя) и hello внешний порт настроен и настроить его.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-155">After hello VM finishes provisioning, SSH toohello VM by using hello VM's external IP address (or DNS name) and hello external port number you configured, and then customize it.</span></span> <span data-ttu-id="4c3c5-156">Дополнительные сведения о подключении, в разделе [как toolog на tooa виртуальной машине под управлением Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4c3c5-156">For connection details, see [How toolog on tooa virtual machine running Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4c3c5-157">Выполните команды имени пользователя hello, настроенные на hello виртуальной Машины, если доступ к корню не требуется toocomplete шаг.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-157">Perform commands as hello user you configured on hello VM, unless root access is required toocomplete a step.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4c3c5-158">Microsoft Azure не предоставляет доступ к корню tooLinux виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-158">Microsoft Azure does not provide root access tooLinux VMs.</span></span> <span data-ttu-id="4c3c5-159">toogain административный доступ при подключении в качестве пользователя toohello виртуальной Машины, выполните команды с помощью `sudo`.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-159">toogain administrative access when connected as a user toohello VM, run commands by using `sudo`.</span></span>
>
>

* <span data-ttu-id="4c3c5-160">**Обновления**. Установите обновления с помощью zypper.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-160">**Updates**: Install updates by using zypper.</span></span> <span data-ttu-id="4c3c5-161">Можно использовать программы tooinstall NFS.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-161">You might also want tooinstall NFS utilities.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="4c3c5-162">В SP1 HPC SLES 12 ВМ рекомендуется не применять обновления ядра, которые могут вызвать проблемы с hello Linux RDMA драйверы.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-162">In a SLES 12 SP1 HPC VM, we recommend that you don't apply kernel updates, which can cause issues with hello Linux RDMA drivers.</span></span>
  >
  >
* <span data-ttu-id="4c3c5-163">**Intel MPI**: завершить установку hello Intel MPI на hello SLES 12 SP1 HPC ВМ, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="4c3c5-163">**Intel MPI**: Complete hello installation of Intel MPI on hello SLES 12 SP1 HPC VM by running hello following command:</span></span>

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* <span data-ttu-id="4c3c5-164">**Блокировать память**: для MPI коды toolock hello доступной памяти для RDMA, добавить или изменить следующие параметры в файле /etc/security/limits.conf hello hello.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-164">**Lock memory**: For MPI codes toolock hello memory available for RDMA, add or change hello following settings in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="4c3c5-165">Требуется корневой доступ tooedit этот файл.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-165">You need root access tooedit this file.</span></span>

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > <span data-ttu-id="4c3c5-166">В целях тестирования можно также задать memlock toounlimited.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-166">For testing purposes, you can also set memlock toounlimited.</span></span> <span data-ttu-id="4c3c5-167">Например, `<User or group name>    hard    memlock unlimited`.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-167">For example: `<User or group name>    hard    memlock unlimited`.</span></span> <span data-ttu-id="4c3c5-168">Дополнительные сведения см. в статье [Best Known Methods for Setting Locked Memory Size](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size) (Рекомендуемые методы определения размера заблокированной памяти).</span><span class="sxs-lookup"><span data-stu-id="4c3c5-168">For more information, see [Best known methods for setting locked memory size](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span></span>
  >
  >
* <span data-ttu-id="4c3c5-169">**Ключи SSH для виртуальных машин SLES**: создание SSH ключи tooestablish доверия для вашей учетной записи пользователя между hello вычислительных узлов в кластере SLES hello, при выполнении заданий MPI.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-169">**SSH keys for SLES VMs**: Generate SSH keys tooestablish trust for your user account among hello compute nodes in hello SLES cluster when running MPI jobs.</span></span> <span data-ttu-id="4c3c5-170">Если развернута виртуальная машина HPC на основе CentOS, не выполняйте этот шаг.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-170">If you deployed a CentOS-based HPC VM, don't follow this step.</span></span> <span data-ttu-id="4c3c5-171">См. инструкции далее в этой статье tooset passwordless доверительные SSH узлам кластера hello после записи образа hello и развертывания кластера hello.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-171">See instructions later in this article tooset up passwordless SSH trust among hello cluster nodes after you capture hello image and deploy hello cluster.</span></span>

    <span data-ttu-id="4c3c5-172">toocreate ключи SSH, запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-172">toocreate SSH keys, run hello following command.</span></span> <span data-ttu-id="4c3c5-173">При появлении запроса для ввода выберите **ввод** ключей toogenerate hello в расположение по умолчанию hello без указания пароля.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-173">When you are prompted for input, select **Enter** toogenerate hello keys in hello default location without setting a password.</span></span>

        ssh-keygen

    <span data-ttu-id="4c3c5-174">Добавьте файл authorized_keys hello toohello открытого ключа для известных открытых ключей.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-174">Append hello public key toohello authorized_keys file for known public keys.</span></span>

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    <span data-ttu-id="4c3c5-175">В каталоге ~/.ssh hello изменить или создать файл конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-175">In hello ~/.ssh directory, edit or create hello config file.</span></span> <span data-ttu-id="4c3c5-176">Укажите диапазон IP-адресов hello hello частной сети планировать toouse в Azure (10.32.0.0/16 в этом примере):</span><span class="sxs-lookup"><span data-stu-id="4c3c5-176">Provide hello IP address range of hello private network that you plan toouse in Azure (10.32.0.0/16 in this example):</span></span>

        host 10.32.0.*
        StrictHostKeyChecking no

    <span data-ttu-id="4c3c5-177">Кроме того список hello частной сети IP-адрес каждой виртуальной Машины в кластере следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4c3c5-177">Alternatively, list hello private network IP address of each VM in your cluster as follows:</span></span>

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > <span data-ttu-id="4c3c5-178">Настройка `StrictHostKeyChecking no` может создать потенциальную угрозу безопасности, если определенный IP-адрес или диапазон не задан.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-178">Configuring `StrictHostKeyChecking no` can create a potential security risk when a specific IP address or range is not specified.</span></span>
  >
  >
* <span data-ttu-id="4c3c5-179">**Приложения**: установки приложений необходимо или выполнить другие пользовательские настройки до того как образ hello.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-179">**Applications**: Install any applications you need or perform other customizations before you capture hello image.</span></span>

### <a name="capture-hello-image"></a><span data-ttu-id="4c3c5-180">Записать образ hello</span><span class="sxs-lookup"><span data-stu-id="4c3c5-180">Capture hello image</span></span>
<span data-ttu-id="4c3c5-181">hello изображение toocapture, сначала необходимо запустить следующую команду на виртуальной Машине Linux hello hello.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-181">toocapture hello image, first run hello following command on hello Linux VM.</span></span> <span data-ttu-id="4c3c5-182">Эта команда deprovisions hello виртуальной Машины, но поддерживает учетные записи пользователей и ключи SSH, которые можно настроить.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-182">This command deprovisions hello VM but maintains user accounts and SSH keys that you set up.</span></span>

```
sudo waagent -deprovision
```

<span data-ttu-id="4c3c5-183">С клиентского компьютера выполните следующие toocapture hello Azure CLI команды изображения hello.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-183">From your client computer, run hello following Azure CLI commands toocapture hello image.</span></span> <span data-ttu-id="4c3c5-184">Дополнительные сведения см. в разделе [как toocapture классической виртуальной машины Linux как изображение](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="4c3c5-184">For more information, see [How toocapture a classic Linux virtual machine as an image](capture-image.md).</span></span>  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

<span data-ttu-id="4c3c5-185">После выполнения этих команд образа виртуальной Машины hello для использования, а удаляется hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-185">After you run these commands, hello VM image is captured for your use and hello VM is deleted.</span></span> <span data-ttu-id="4c3c5-186">Теперь у вас ваш пользовательский образ готов toodeploy кластера.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-186">Now you have your custom image ready toodeploy a cluster.</span></span>

### <a name="deploy-a-cluster-with-hello-image"></a><span data-ttu-id="4c3c5-187">Развертывание кластера с изображением hello</span><span class="sxs-lookup"><span data-stu-id="4c3c5-187">Deploy a cluster with hello image</span></span>
<span data-ttu-id="4c3c5-188">Измените следующий сценарий Bash с соответствующими значениями для вашей среды hello и запустите его с клиентского компьютера.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-188">Modify hello following Bash script with appropriate values for your environment and run it from your client computer.</span></span> <span data-ttu-id="4c3c5-189">Поскольку Azure развертывает ВМ hello последовательно в hello классической модели развертывания, он занимает несколько минут, toodeploy hello восемь ВМ A9, предлагаемые в этот сценарий.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-189">Because Azure deploys hello VMs serially in hello classic deployment model, it takes a few minutes toodeploy hello eight A9 VMs suggested in this script.</span></span>

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a><span data-ttu-id="4c3c5-190">Рекомендации для кластера CentOS HPC</span><span class="sxs-lookup"><span data-stu-id="4c3c5-190">Considerations for a CentOS HPC cluster</span></span>
<span data-ttu-id="4c3c5-191">Tooset кластера на основе одного из изображений на основе CentOS HPC hello в hello Azure Marketplace вместо SLES 12 для HPC, выполните общие шаги hello в предшествующих раздел hello.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-191">If you want tooset up a cluster based on one of hello CentOS-based HPC images in hello Azure Marketplace instead of SLES 12 for HPC, follow hello general steps in hello preceding section.</span></span> <span data-ttu-id="4c3c5-192">Обратите внимание, hello при инициализации и настройки виртуальной Машины hello следующие различия:</span><span class="sxs-lookup"><span data-stu-id="4c3c5-192">Note hello following differences when you provision and configure hello VM:</span></span>

- <span data-ttu-id="4c3c5-193">На виртуальной машине, подготовленной из образа на основе CentOS HPC, уже установлен интерфейс Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-193">Intel MPI is already installed on a VM provisioned from a CentOS-based HPC image.</span></span>
- <span data-ttu-id="4c3c5-194">Параметры памяти блокировки уже добавлены в файл /etc/security/limits.conf hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-194">Lock memory settings are already added in hello VM's /etc/security/limits.conf file.</span></span>
- <span data-ttu-id="4c3c5-195">Не создавайте ключи SSH на hello Подготовка виртуальной Машины для отслеживания.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-195">Do not generate SSH keys on hello VM you provision for capture.</span></span> <span data-ttu-id="4c3c5-196">Вместо этого рекомендуется настроить проверку подлинности на основе пользователя после развертывания кластера hello.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-196">Instead, we recommend setting up user-based authentication after you deploy hello cluster.</span></span> <span data-ttu-id="4c3c5-197">Дополнительные сведения см. в разделе hello в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-197">For more information, see hello following section.</span></span>  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a><span data-ttu-id="4c3c5-198">Настройка passwordless доверия SSH в кластере hello</span><span class="sxs-lookup"><span data-stu-id="4c3c5-198">Set up passwordless SSH trust on hello cluster</span></span>
<span data-ttu-id="4c3c5-199">В кластере HPC на основе CentOS существует два метода для установления отношений доверия между вычислительными узлами hello: проверка подлинности на основе узла и проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-199">On a CentOS-based HPC cluster, there are two methods for establishing trust between hello compute nodes: host-based authentication and user-based authentication.</span></span> <span data-ttu-id="4c3c5-200">Проверка подлинности на основе узла находится вне области hello данной статьи и обычно должны осуществляться через сценарий расширения во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-200">Host-based authentication is outside of hello scope of this article and generally must be done through an extension script during deployment.</span></span> <span data-ttu-id="4c3c5-201">Проверку подлинности удобен для установления отношений доверия после развертывания и требует создания hello и совместное использование ключей SSH среди hello вычислительных узлов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-201">User-based authentication is convenient for establishing trust after deployment and requires hello generation and sharing of SSH keys among hello compute nodes in hello cluster.</span></span> <span data-ttu-id="4c3c5-202">Такой метод, называемый входом через SSH без пароля, необходим для выполнения заданий MPI.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-202">This method is commonly known as passwordless SSH login and is required when running MPI jobs.</span></span>

<span data-ttu-id="4c3c5-203">Пример сценария, были получены из hello сообщества можно найти в [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) проверки подлинности пользователя легко tooenable в кластере HPC на основе CentOS.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-203">A sample script contributed from hello community is available on [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable easy user authentication on a CentOS-based HPC cluster.</span></span> <span data-ttu-id="4c3c5-204">Загрузите и используйте этот скрипт с помощью hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-204">Download and use this script by using hello following steps.</span></span> <span data-ttu-id="4c3c5-205">Кроме того, можно изменить этот скрипт или использовать любой другой метод tooestablish passwordless SSH проверки подлинности между hello кластерных вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-205">You can also modify this script or use any other method tooestablish passwordless SSH authentication between hello cluster compute nodes.</span></span>

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

<span data-ttu-id="4c3c5-206">сценарий toorun hello, необходима tooknow hello префикс подсети IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-206">toorun hello script, you need tooknow hello prefix for your subnet IP addresses.</span></span> <span data-ttu-id="4c3c5-207">Получите префикс hello, выполнив следующую команду на одном из узлов кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-207">Get hello prefix by running hello following command on one of hello cluster nodes.</span></span> <span data-ttu-id="4c3c5-208">Ваш результат должен выглядеть примерно так 10.1.3.5 и часть hello 10.1.3 используется префикс hello.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-208">Your output should look something like 10.1.3.5, and hello prefix is hello 10.1.3 portion.</span></span>

    ifconfig eth0 | grep -w inet | awk '{print $2}'

<span data-ttu-id="4c3c5-209">Теперь запустите скрипт hello, используя три параметра: hello общее имя пользователя на hello вычислительных узлов, hello общий пароль для этого пользователя на hello вычислительных узлов и префикса подсети hello, который был возвращен из предыдущей команды hello.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-209">Now run hello script using three parameters: hello common user name on hello compute nodes, hello common password for that user on hello compute nodes, and hello subnet prefix that was returned from hello previous command.</span></span>

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

<span data-ttu-id="4c3c5-210">Этот сценарий hello следующие:</span><span class="sxs-lookup"><span data-stu-id="4c3c5-210">This script does hello following:</span></span>

* <span data-ttu-id="4c3c5-211">Создает каталог на hello узла с именем .ssh, который необходим для passwordless входа.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-211">Creates a directory on hello host node named .ssh, which is required for passwordless login.</span></span>
* <span data-ttu-id="4c3c5-212">Создает файл конфигурации в каталоге .ssh hello, который указывает, что имя входа tooallow passwordless входа из любого узла в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-212">Creates a configuration file in hello .ssh directory that instructs passwordless login tooallow login from any node in hello cluster.</span></span>
* <span data-ttu-id="4c3c5-213">Создает файлы, содержащие имена узлов hello и узла IP-адреса для всех узлов кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-213">Creates files containing hello node names and node IP addresses for all hello nodes in hello cluster.</span></span> <span data-ttu-id="4c3c5-214">Эти файлы остаются после выполнения скрипта hello для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-214">These files are left after hello script is run for later reference.</span></span>
* <span data-ttu-id="4c3c5-215">Создает пару закрытого и открытого ключа для каждого узла кластера (включая hello главного узла) и записи в файл authorized_keys hello.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-215">Creates a private and public key pair for each cluster node (including hello host node) and creates entries in hello authorized_keys file.</span></span>

> [!WARNING]
> <span data-ttu-id="4c3c5-216">Выполнение этого сценария может создать угрозу безопасности.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-216">Running this script can create a potential security risk.</span></span> <span data-ttu-id="4c3c5-217">Убедитесь, что hello сведения об открытом ключе в ~/.ssh не распространяется.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-217">Ensure that hello public key information in ~/.ssh is not distributed.</span></span>
>
>

## <a name="configure-intel-mpi"></a><span data-ttu-id="4c3c5-218">Настройка Intel MPI</span><span class="sxs-lookup"><span data-stu-id="4c3c5-218">Configure Intel MPI</span></span>
<span data-ttu-id="4c3c5-219">toorun приложений MPI в Azure Linux RDMA, требуется tooconfigure конкретных tooIntel каталога переменные определенные среды MPI.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-219">toorun MPI applications on Azure Linux RDMA, you need tooconfigure certain environment variables specific tooIntel MPI.</span></span> <span data-ttu-id="4c3c5-220">Ниже приведен пример Bash сценария tooconfigure hello переменные, необходимые toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-220">Here is a sample Bash script tooconfigure hello variables needed toorun an application.</span></span> <span data-ttu-id="4c3c5-221">Измените путь toompivars.sh hello для установки Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-221">Change hello path toompivars.sh as needed for your installation of Intel MPI.</span></span>

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

<span data-ttu-id="4c3c5-222">Hello hello узла файла имеет следующий формат.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-222">hello format of hello host file is as follows.</span></span> <span data-ttu-id="4c3c5-223">Добавьте одну строку для каждого узла в кластере.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-223">Add one line for each node in your cluster.</span></span> <span data-ttu-id="4c3c5-224">Укажите частные IP-адреса из виртуальной сети hello определенные ранее, не DNS-имена.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-224">Specify private IP addresses from hello virtual network defined earlier, not DNS names.</span></span> <span data-ttu-id="4c3c5-225">Например для двух узлов с IP-адресами 10.32.0.1 и 10.32.0.2 hello файл содержит hello следующее:</span><span class="sxs-lookup"><span data-stu-id="4c3c5-225">For example, for two hosts with IP addresses 10.32.0.1 and 10.32.0.2, hello file contains hello following:</span></span>

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a><span data-ttu-id="4c3c5-226">Запуск интерфейса MPI на базовом кластере с двумя узлами</span><span class="sxs-lookup"><span data-stu-id="4c3c5-226">Run MPI on a basic two-node cluster</span></span>
<span data-ttu-id="4c3c5-227">Если это еще не сделано, настройте hello среды для Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-227">If you haven't already done so, first set up hello environment for Intel MPI.</span></span>

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a><span data-ttu-id="4c3c5-228">Выполнение команды MPI</span><span class="sxs-lookup"><span data-stu-id="4c3c5-228">Run an MPI command</span></span>
<span data-ttu-id="4c3c5-229">Выполните команду MPI на одном из hello вычислительных узлов tooshow, MPI правильно установлен и может обмениваться данными между по крайней мере два вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-229">Run an MPI command on one of hello compute nodes tooshow that MPI is installed properly and can communicate between at least two compute nodes.</span></span> <span data-ttu-id="4c3c5-230">следующие Hello **mpirun** команда выполняет hello **hostname** команду на двух узлах.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-230">hello following **mpirun** command runs hello **hostname** command on two nodes.</span></span>

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
<span data-ttu-id="4c3c5-231">Выходные данные должны быть перечислены hello имена всех узлов hello, переданные как входные данные для `-hosts`.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-231">Your output should list hello names of all hello nodes that you passed as input for `-hosts`.</span></span> <span data-ttu-id="4c3c5-232">Например **mpirun** команды с двумя узлами возвращает выходные данные hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4c3c5-232">For example, an **mpirun** command with two nodes returns output like hello following:</span></span>

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a><span data-ttu-id="4c3c5-233">Запуск теста производительности MPI</span><span class="sxs-lookup"><span data-stu-id="4c3c5-233">Run an MPI benchmark</span></span>
<span data-ttu-id="4c3c5-234">Следующая команда Intel MPI Hello выполняется pingpong тест tooverify hello конфигурации и подключения toohello RDMA сети кластера.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-234">hello following Intel MPI command runs a pingpong benchmark tooverify hello cluster configuration and connection toohello RDMA network.</span></span>

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

<span data-ttu-id="4c3c5-235">В работе кластера с двумя узлами вы увидите выходные данные hello следующим образом.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-235">On a working cluster with two nodes, you should see output like hello following.</span></span> <span data-ttu-id="4c3c5-236">В сети Azure RDMA hello ожидать задержки на уровне или ниже 3 микросекундах размеры сообщений вверх too512 байт.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-236">On hello Azure RDMA network, expect latency at or below 3 microseconds for message sizes up too512 bytes.</span></span>

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks toorun:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a><span data-ttu-id="4c3c5-237">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4c3c5-237">Next steps</span></span>
* <span data-ttu-id="4c3c5-238">Разверните и запустите приложения MPI в кластере Linux.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-238">Deploy and run your Linux MPI applications on your Linux cluster.</span></span>
* <span data-ttu-id="4c3c5-239">В разделе hello [документация по библиотеке MPI Intel](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) рекомендации по Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-239">See hello [Intel MPI Library documentation](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) for guidance on Intel MPI.</span></span>
* <span data-ttu-id="4c3c5-240">Повторите [шаблоном краткого руководства](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate Lustre Intel кластера с помощью образа на основе CentOS HPC.</span><span class="sxs-lookup"><span data-stu-id="4c3c5-240">Try a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate an Intel Lustre cluster by using a CentOS-based HPC image.</span></span> <span data-ttu-id="4c3c5-241">Дополнительные сведения см. в статье [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/) (Развертывание Intel Cloud Edition для Lustre в Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="4c3c5-241">For details, see [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span></span>
