---
title: "aaaRun OpenFOAM с пакетом HPC на виртуальных машинах Linux | Документы Microsoft"
description: "Развертывание кластера Microsoft HPC в Azure и запуск заданий OpenFOAM на нескольких вычислительных узлах Linux в сети RDMA."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="cea24-103">Выполнение заданий OpenFoam в кластере Linux RDMA в Azure с помощью пакета Microsoft HPC</span><span class="sxs-lookup"><span data-stu-id="cea24-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="cea24-104">В этой статье показывает один из способов toorun OpenFoam в виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="cea24-104">This article shows you one way toorun OpenFoam in Azure virtual machines.</span></span> <span data-ttu-id="cea24-105">Здесь мы развернем кластер пакета Microsoft HPC в Azure с использованием вычислительных узлов Linux и запустим задание [OpenFoam](http://openfoam.com/), используя библиотеку Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="cea24-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span></span> <span data-ttu-id="cea24-106">Функцией RDMA виртуальных машинах Azure для hello вычислительных узлов, можно использовать, чтобы hello вычислительных узлов обмениваться данными по сети Azure RDMA hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-106">You can use RDMA-capable Azure VMs for hello compute nodes, so that hello compute nodes communicate over hello Azure RDMA network.</span></span> <span data-ttu-id="cea24-107">Другие параметры toorun, полностью включить OpenFoam в Azure настроен коммерческих образов, доступных в hello Marketplace, например UberCloud [OpenFoam 2.3 в CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/)и запустив на [пакетной службы Azure](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span><span class="sxs-lookup"><span data-stu-id="cea24-107">Other options toorun OpenFoam in Azure include fully configured commercial images available in hello Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="cea24-108">OpenFOAM (англ. Open Field Operation and Manipulation) — это пакет программного обеспечения с открытым исходным кодом для вычислительной гидродинамики (CFD). Он широко используется в технической и научной областях, а также в коммерческих и научных организациях.</span><span class="sxs-lookup"><span data-stu-id="cea24-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span></span> <span data-ttu-id="cea24-109">Пакет содержит средства для сеточного разбиения (например, snappyHexMesh), включает средство распараллеливания расчетов для сложных геометрических объектов, а также функции предварительной и последующей обработки.</span><span class="sxs-lookup"><span data-stu-id="cea24-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span></span> <span data-ttu-id="cea24-110">Почти все процессы выполняются параллельно, включение tootake потенциала пользователей оборудования компьютера в их распоряжении.</span><span class="sxs-lookup"><span data-stu-id="cea24-110">Almost all processes run in parallel, enabling users tootake full advantage of computer hardware at their disposal.</span></span>  

<span data-ttu-id="cea24-111">Пакет Microsoft HPC предоставляет возможности toorun крупномасштабных HPC и параллельных приложений, включая приложения MPI, в кластерах из виртуальных машин Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cea24-111">Microsoft HPC Pack provides features toorun large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="cea24-112">Пакет HPC также поддерживает приложения высокопроизводительных вычислений для Linux на виртуальных вычислительных узлах Linux, развернутых в кластере HPC.</span><span class="sxs-lookup"><span data-stu-id="cea24-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="cea24-113">В разделе [Приступая к работе с Linux вычислительных узлов в кластере HPC Pack в Azure](hpcpack-cluster.md) для toousing введение Linux вычислительных узлов с помощью пакета HPC.</span><span class="sxs-lookup"><span data-stu-id="cea24-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction toousing Linux compute nodes with HPC Pack.</span></span>

> [!NOTE]
> <span data-ttu-id="cea24-114">В этой статье показано, как toorun рабочей нагрузки Linux MPI с пакетом HPC.</span><span class="sxs-lookup"><span data-stu-id="cea24-114">This article illustrates how toorun a Linux MPI workload with HPC Pack.</span></span> <span data-ttu-id="cea24-115">Здесь предполагается, что у вас есть опыт в администрировании Linux и выполнении рабочих нагрузок MPI на кластерах Linux.</span><span class="sxs-lookup"><span data-stu-id="cea24-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span></span> <span data-ttu-id="cea24-116">При использовании версии MPI и отличаются от тех, которые показаны в этой статье hello OpenFOAM возможно toomodify некоторые шаги установки и настройки.</span><span class="sxs-lookup"><span data-stu-id="cea24-116">If you use versions of MPI and OpenFOAM different from hello ones shown in this article, you might have toomodify some installation and configuration steps.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="cea24-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cea24-117">Prerequisites</span></span>
* <span data-ttu-id="cea24-118">**Кластер пакета HPC с вычислительными узлами Linux с поддержкой RDMA**. Разверните кластер пакета HPC с вычислительными узлами размером A8, A9, H16r или H16rm под управлением Linux, используя [шаблон Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) или [сценарий Azure PowerShell](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="cea24-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="cea24-119">В разделе [Приступая к работе с Linux вычислительных узлов в кластере HPC Pack в Azure](hpcpack-cluster.md) hello предварительные условия и действия в любом случае.</span><span class="sxs-lookup"><span data-stu-id="cea24-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="cea24-120">При выборе hello вариант развертывания сценария PowerShell см. Образец hello файла конфигурации в файлах образца hello в конце hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="cea24-120">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="cea24-121">Используйте этот кластер HPC Pack toodeploy основе Azure конфигурации, состоящий из головного узла размера A8 Windows Server 2012 R2 и 2 размер A8 SUSE Linux Enterprise Server 12 вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="cea24-121">Use this configuration toodeploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span></span> <span data-ttu-id="cea24-122">Вместо используемых в файле имен подписки и службы подставьте свои значения.</span><span class="sxs-lookup"><span data-stu-id="cea24-122">Substitute appropriate values for your subscription and service names.</span></span> 
  
  <span data-ttu-id="cea24-123">**Дополнительные важные tooknow**</span><span class="sxs-lookup"><span data-stu-id="cea24-123">**Additional things tooknow**</span></span>
  
  * <span data-ttu-id="cea24-124">Предварительные требования к использованию вычислительных узлов Linux RDMA в Azure см. в статье [Размеры виртуальных машин, оптимизированных для высокопроизводительных вычислений](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cea24-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  * <span data-ttu-id="cea24-125">При использовании варианта развертывания сценария Powershell hello развертывания все hello Linux вычислительных узлов в рамках одной облачной службы toouse hello RDMA сетевое подключение.</span><span class="sxs-lookup"><span data-stu-id="cea24-125">If you use hello Powershell script deployment option, deploy all hello Linux compute nodes within one cloud service toouse hello RDMA network connection.</span></span>
  * <span data-ttu-id="cea24-126">После развертывания узлов hello Linux, подключаться с SSH tooperform любые дополнительные задачи администрирования.</span><span class="sxs-lookup"><span data-stu-id="cea24-126">After deploying hello Linux nodes, connect by SSH tooperform any additional administrative tasks.</span></span> <span data-ttu-id="cea24-127">Сведения о подключении hello SSH для каждой виртуальной Машины Linux можно найти в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cea24-127">Find hello SSH connection details for each Linux VM in hello Azure portal.</span></span>  
* <span data-ttu-id="cea24-128">**Intel MPI** -toorun OpenFOAM на SLES 12 HPC вычислительные узлы в Azure, необходимо, чтобы среда выполнения hello 5 библиотеки Intel MPI tooinstall из hello [сайта Intel.com](https://software.intel.com/en-us/intel-mpi-library/).</span><span class="sxs-lookup"><span data-stu-id="cea24-128">**Intel MPI** - toorun OpenFOAM on SLES 12 HPC compute nodes in Azure, you need tooinstall hello Intel MPI Library 5 runtime from hello [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span></span> <span data-ttu-id="cea24-129">(Среда выполнения Intel MPI 5 предустановлена в образах на основе CentOS для HPC.)  Позже установите Intel MPI на вычислительные узлы Linux, если это будет необходимо.</span><span class="sxs-lookup"><span data-stu-id="cea24-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span></span> <span data-ttu-id="cea24-130">tooprepare для выполнения этого шага после регистрации с Intel, по ссылке hello hello подтверждение по электронной почте toohello связанных веб-странице.</span><span class="sxs-lookup"><span data-stu-id="cea24-130">tooprepare for this step, after you register with Intel, follow hello link in hello confirmation email toohello related web page.</span></span> <span data-ttu-id="cea24-131">Затем копия hello Загрузите ссылку для файла .tgz hello для hello соответствующую версию Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="cea24-131">Then, copy hello download link for hello .tgz file for hello appropriate version of Intel MPI.</span></span> <span data-ttu-id="cea24-132">В этой статье используется Intel MPI версии 5.0.3.048.</span><span class="sxs-lookup"><span data-stu-id="cea24-132">This article is based on Intel MPI version 5.0.3.048.</span></span>
* <span data-ttu-id="cea24-133">**Источник пакета OpenFOAM** -загрузки программного обеспечения hello OpenFOAM источника пакета для Linux с hello [OpenFOAM Foundation сайта](http://openfoam.org/download/2-3-1-source/).</span><span class="sxs-lookup"><span data-stu-id="cea24-133">**OpenFOAM Source Pack** - Download hello OpenFOAM Source Pack software for Linux from hello [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span></span> <span data-ttu-id="cea24-134">В этой статье используется пакет версии 2.3.1, доступный для загрузки в виде файла OpenFOAM-2.3.1.tgz.</span><span class="sxs-lookup"><span data-stu-id="cea24-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span></span> <span data-ttu-id="cea24-135">Следуйте инструкциям hello далее в этой статье toounpack и скомпилируйте OpenFOAM на вычислительных узлах hello Linux.</span><span class="sxs-lookup"><span data-stu-id="cea24-135">Follow hello instructions later in this article toounpack and compile OpenFOAM on hello Linux compute nodes.</span></span>
* <span data-ttu-id="cea24-136">**EnSight** (необязательно) — результаты hello toosee вашей модели OpenFOAM, загрузите и установите hello [EnSight](https://www.ceisoftware.com/download/) визуализации и анализа программы.</span><span class="sxs-lookup"><span data-stu-id="cea24-136">**EnSight** (optional) - toosee hello results of your OpenFOAM simulation, download and install hello [EnSight](https://www.ceisoftware.com/download/) visualization and analysis program.</span></span> <span data-ttu-id="cea24-137">Сведения о лицензировании и загрузки, на сайте EnSight hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-137">Licensing and download information are at hello EnSight site.</span></span>

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="cea24-138">Настройка взаимного доверия между вычислительными узлами</span><span class="sxs-lookup"><span data-stu-id="cea24-138">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="cea24-139">Запуск задания межузловых на нескольких узлах Linux требует hello узлы tootrust друг с другом (с **rsh** или **ssh**).</span><span class="sxs-lookup"><span data-stu-id="cea24-139">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="cea24-140">При создании кластера HPC Pack hello с hello скрипт развертывания IaaS пакета HPC Microsoft hello сценарий автоматически настраивает постоянное взаимного доверия для учетной записи администратора hello, указываемые.</span><span class="sxs-lookup"><span data-stu-id="cea24-140">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="cea24-141">Для пользователей без прав администратора, созданные в домене hello кластера имеют tooset копирование временной взаимного доверия между узлами hello выделяется toothem, и задания уничтожить hello связь после завершения задания hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-141">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem, and destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="cea24-142">tooestablish доверия для каждого пользователя предоставляют кластер toohello пару ключей RSA, пакет HPC для отношения доверия hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-142">tooestablish trust for each user, provide an RSA key pair toohello cluster that HPC Pack uses for hello trust relationship.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="cea24-143">Создание пары ключей RSA</span><span class="sxs-lookup"><span data-stu-id="cea24-143">Generate an RSA key pair</span></span>
<span data-ttu-id="cea24-144">Легко toogenerate пару ключей RSA, который содержит открытый ключ и закрытый ключ, выполнив hello Linux **ssh-keygen** команды.</span><span class="sxs-lookup"><span data-stu-id="cea24-144">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="cea24-145">Войдите в систему tooa компьютера Linux.</span><span class="sxs-lookup"><span data-stu-id="cea24-145">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="cea24-146">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-146">Run hello following command:</span></span>
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="cea24-147">Нажмите клавишу **ввод** toouse параметры по умолчанию hello до завершения команды hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-147">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="cea24-148">Не вводите парольную фразу. При запросе пароля просто нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="cea24-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Создание пары ключей RSA][keygen]
3. <span data-ttu-id="cea24-150">Изменить каталог toohello ~/.ssh каталог.</span><span class="sxs-lookup"><span data-stu-id="cea24-150">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="cea24-151">Hello закрытый ключ хранится в id_rsa и hello открытый ключ в id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="cea24-151">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![Открытые и закрытые ключи][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="cea24-153">Добавление кластера HPC Pack toohello пары ключей hello</span><span class="sxs-lookup"><span data-stu-id="cea24-153">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="cea24-154">Сделать удаленного рабочего стола подключения tooyour головной узел с вашей учетной записью администратора HPC Pack (hello администратора учетной записи, настроенной при запуске скрипта развертывания hello).</span><span class="sxs-lookup"><span data-stu-id="cea24-154">Make a Remote Desktop connection tooyour head node with your HPC Pack administrator account (hello administrator account you set up when you ran hello deployment script).</span></span>
2. <span data-ttu-id="cea24-155">Используйте стандартные toocreate процедуры Windows Server, учетную запись пользователя домена в домене Active Directory кластера hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-155">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="cea24-156">Например с помощью средства компьютеров и hello пользователя Active Directory на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-156">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="cea24-157">Hello примеры в этой статье предполагается, что пользователь домена с именем hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="cea24-157">hello examples in this article assume you create a domain user named hpclab\hpcuser.</span></span>
3. <span data-ttu-id="cea24-158">Создайте файл с именем C:\cred.xml и скопируйте данные ключа hello RSA в него.</span><span class="sxs-lookup"><span data-stu-id="cea24-158">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="cea24-159">Образец файла cred.xml-конец hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="cea24-159">A sample cred.xml file is at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. <span data-ttu-id="cea24-160">Откройте командную строку и введите следующую команду, tooset hello учетных данных данные для учетной записи hpclab\hpcuser hello hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-160">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="cea24-161">Использовать hello **extendeddata** toopass параметр hello имя C:\cred.xml файл, созданный для hello данных ключа.</span><span class="sxs-lookup"><span data-stu-id="cea24-161">You use hello **extendeddata** parameter toopass hello name of C:\cred.xml file you created for hello key data.</span></span>
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="cea24-162">Эта команда успешно завершается без выходных данных.</span><span class="sxs-lookup"><span data-stu-id="cea24-162">This command completes successfully without output.</span></span> <span data-ttu-id="cea24-163">После установки hello учетные данные для учетных записей пользователей hello, необходимые toorun заданий, hello cred.xml файл хранится в безопасном месте или удалите его.</span><span class="sxs-lookup"><span data-stu-id="cea24-163">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
5. <span data-ttu-id="cea24-164">Если на одном из узлов Linux создан hello пару ключей RSA, помните ключи hello toodelete после завершения работы с ними.</span><span class="sxs-lookup"><span data-stu-id="cea24-164">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="cea24-165">Пакет HPC не устанавливает взаимное доверие, если обнаруживает файл id_rsa или id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="cea24-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cea24-166">Не рекомендуется запускать задания Linux как администратор кластера на общего кластера, поскольку задания, отправлен администратором выполняется под учетной записью root hello на узлах Linux hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="cea24-167">Тем не менее задания, отправленный пользователем без прав администратора выполняется под локальной учетной записью пользователя Linux с точно такое же имя, как пользователь задания hello hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-167">However, a job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="cea24-168">В этом случае пакет HPC устанавливает взаимного доверия для этого пользователя Linux по узлам hello выделенной toohello задания.</span><span class="sxs-lookup"><span data-stu-id="cea24-168">In this case, HPC Pack sets up mutual trust for this Linux user across hello nodes allocated toohello job.</span></span> <span data-ttu-id="cea24-169">Можно настроить пользователя Linux hello вручную на узлах Linux hello перед выполнением задания hello или автоматически создает hello пользователя при отправке задания hello пакета HPC.</span><span class="sxs-lookup"><span data-stu-id="cea24-169">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="cea24-170">Если пакет HPC создает пользователя hello, HPC Pack удаляет его после завершения задания hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-170">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="cea24-171">угрозы безопасности tooreduce, пакет HPC удаляет ключи hello после завершения задания.</span><span class="sxs-lookup"><span data-stu-id="cea24-171">tooreduce security threats, HPC Pack removes hello keys after job completion.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="cea24-172">Настройка файлового ресурса для узлов Linux</span><span class="sxs-lookup"><span data-stu-id="cea24-172">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="cea24-173">Теперь Настройка стандартных ресурсу SMB на папку на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-173">Now set up a standard SMB share on a folder on hello head node.</span></span> <span data-ttu-id="cea24-174">tooallow hello Linux узлы tooaccess файлы приложения с общий путь подключения hello общей папки на узлах Linux hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-174">tooallow hello Linux nodes tooaccess application files with a common path, mount hello shared folder on hello Linux nodes.</span></span> <span data-ttu-id="cea24-175">Вы можете также использовать другие параметры общего доступа, например общие файлы Azure (рекомендуется для большинства сценариев) или общие папки NFS.</span><span class="sxs-lookup"><span data-stu-id="cea24-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span></span> <span data-ttu-id="cea24-176">Совместное использование информации и подробное описание действий в файле hello [Приступая к работе с Linux вычислительных узлов в кластере HPC Pack в Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="cea24-176">See hello file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="cea24-177">Создайте папку на головном узле hello и предоставить к нему tooEveryone, задав права чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="cea24-177">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="cea24-178">Например, общий ресурс C:\OpenFOAM на hello головного узла в качестве \\ \\SUSE12RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="cea24-178">For example, share C:\OpenFOAM on hello head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="cea24-179">Здесь *SUSE12RDMA HN* — имя узла hello hello головного узла.</span><span class="sxs-lookup"><span data-stu-id="cea24-179">Here, *SUSE12RDMA-HN* is hello host name of hello head node.</span></span>
2. <span data-ttu-id="cea24-180">Откройте окно Windows PowerShell и выполните следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="cea24-180">Open a Windows PowerShell window and run hello following commands:</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

<span data-ttu-id="cea24-181">Hello первая команда создает папку с именем /openfoam на всех узлах в группе LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-181">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="cea24-182">Вторая команда Hello подключает //SUSE12RDMA-HN/OpenFOAM hello общие папки на узлах Linux hello с dir_mode и file_mode too777 набор битов.</span><span class="sxs-lookup"><span data-stu-id="cea24-182">hello second command mounts hello shared folder //SUSE12RDMA-HN/OpenFOAM on hello Linux nodes with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="cea24-183">Hello *username* и *пароль* в hello команды должны быть учетные данные пользователя на головном узле hello hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-183">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="cea24-184">Hello "\\`" символа в hello вторая команда является escape-символа для PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cea24-184">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="cea24-185">«\\`, «hello», означает» (запятая) является частью команды hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-185">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="install-mpi-and-openfoam"></a><span data-ttu-id="cea24-186">Установка пакетов MPI и OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="cea24-186">Install MPI and OpenFOAM</span></span>
<span data-ttu-id="cea24-187">toorun OpenFOAM как задание MPI hello сети RDMA требуется toocompile OpenFOAM с библиотеками Intel MPI hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-187">toorun OpenFOAM as an MPI job on hello RDMA network, you need toocompile OpenFOAM with hello Intel MPI libraries.</span></span> 

<span data-ttu-id="cea24-188">Во-первых, выполнения нескольких **clusrun** команды tooinstall библиотеки Intel MPI (если она еще не установлена), а также OpenFOAM на узлах Linux.</span><span class="sxs-lookup"><span data-stu-id="cea24-188">First, run several **clusrun** commands tooinstall Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span></span> <span data-ttu-id="cea24-189">Используйте hello головной узел папка ранее настраивается tooshare hello установочные файлы по узлам Linux hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-189">Use hello head node share configured previously tooshare hello installation files among hello Linux nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cea24-190">Приведенные действия по установке и компиляции являются примерами.</span><span class="sxs-lookup"><span data-stu-id="cea24-190">These installation and compiling steps are examples.</span></span> <span data-ttu-id="cea24-191">Требуется знание tooensure администрирования системы Linux, правильность установки зависимых компиляторы и библиотеки.</span><span class="sxs-lookup"><span data-stu-id="cea24-191">You need some knowledge of Linux system administration tooensure that dependent compilers and libraries are installed correctly.</span></span> <span data-ttu-id="cea24-192">Может потребоваться toomodify определенные переменные среды или другие параметры для версий Intel MPI и OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="cea24-192">You might need toomodify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="cea24-193">Дополнительные сведения см. в разделах [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) (Руководство по установке библиотеки Intel MPI для Linux) и [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) (Установка исходного пакета OpenFOAM) для своей среды.</span><span class="sxs-lookup"><span data-stu-id="cea24-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span></span>
> 
> 

### <a name="install-intel-mpi"></a><span data-ttu-id="cea24-194">Установка пакета Intel MPI</span><span class="sxs-lookup"><span data-stu-id="cea24-194">Install Intel MPI</span></span>
<span data-ttu-id="cea24-195">Сохраните hello загруженного пакета установки для Intel MPI (l_mpi_p_5.0.3.048.tgz в этом примере) в C:\OpenFoam на головной узел hello и узлы Linux hello доступен этот файл с /openfoam.</span><span class="sxs-lookup"><span data-stu-id="cea24-195">Save hello downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on hello head node so that hello Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="cea24-196">Затем запустите **clusrun** tooinstall библиотеки Intel MPI на всех узлах Linux hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-196">Then run **clusrun** tooinstall Intel MPI library on all hello Linux nodes.</span></span>

1. <span data-ttu-id="cea24-197">Hello ниже команды копирования hello установочный пакет и извлеките его слишком/opt/intel на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="cea24-197">hello following commands copy hello installation package and extract it too/opt/intel on each node.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. <span data-ttu-id="cea24-198">Библиотека MPI Intel tooinstall без вмешательства пользователя, используйте файл silent.cfg.</span><span class="sxs-lookup"><span data-stu-id="cea24-198">tooinstall Intel MPI Library silently, use a silent.cfg file.</span></span> <span data-ttu-id="cea24-199">Пример можно найти в hello файлы образцов в конце hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="cea24-199">You can find an example in hello sample files at hello end of this article.</span></span> <span data-ttu-id="cea24-200">Поместить этот файл в hello общей папки /openfoam.</span><span class="sxs-lookup"><span data-stu-id="cea24-200">Place this file in hello shared folder /openfoam.</span></span> <span data-ttu-id="cea24-201">Дополнительные сведения о файле silent.cfg hello см. в разделе [библиотека MPI Intel для Linux руководство по установке - автоматической установки](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span><span class="sxs-lookup"><span data-stu-id="cea24-201">For details about hello silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="cea24-202">Сохраните файл silent.cfg как текстовый файл, в котором для завершения строк используется нотация Linux (только LF, а не CR LF).</span><span class="sxs-lookup"><span data-stu-id="cea24-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="cea24-203">Это действие гарантирует, что он работает правильно на узлах Linux hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-203">This step ensures that it runs properly on hello Linux nodes.</span></span>
   > 
   > 
3. <span data-ttu-id="cea24-204">Установка библиотеки Intel MPI в автоматическом режиме.</span><span class="sxs-lookup"><span data-stu-id="cea24-204">Install Intel MPI Library in silent mode.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a><span data-ttu-id="cea24-205">Настройка MPI</span><span class="sxs-lookup"><span data-stu-id="cea24-205">Configure MPI</span></span>
<span data-ttu-id="cea24-206">Для тестирования, следует добавить следующие строки toohello /etc/security/limits.conf на каждом узле Linux hello hello:</span><span class="sxs-lookup"><span data-stu-id="cea24-206">For testing, you should add hello following lines toohello /etc/security/limits.conf on each of hello Linux nodes:</span></span>

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


<span data-ttu-id="cea24-207">После обновления файла limits.conf hello, перезапустите hello узлах Linux.</span><span class="sxs-lookup"><span data-stu-id="cea24-207">Restart hello Linux nodes after you update hello limits.conf file.</span></span> <span data-ttu-id="cea24-208">Например, используйте следующие hello **clusrun** команды:</span><span class="sxs-lookup"><span data-stu-id="cea24-208">For example, use hello following **clusrun** command:</span></span>

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

<span data-ttu-id="cea24-209">После перезагрузки компьютера убедитесь, что в этой общей папке hello подключается как /openfoam.</span><span class="sxs-lookup"><span data-stu-id="cea24-209">After restarting, ensure that hello shared folder is mounted as /openfoam.</span></span>

### <a name="compile-and-install-openfoam"></a><span data-ttu-id="cea24-210">Компиляция и установка OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="cea24-210">Compile and install OpenFOAM</span></span>
<span data-ttu-id="cea24-211">Сохраните hello загруженного пакета установки для hello tooC:\OpenFoam OpenFOAM источника пакета (в этом примере OpenFOAM 2.3.1.tgz) на головной узел hello и узлы Linux hello доступен этот файл с /openfoam.</span><span class="sxs-lookup"><span data-stu-id="cea24-211">Save hello downloaded installation package for hello OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) tooC:\OpenFoam on hello head node so that hello Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="cea24-212">Затем запустите **clusrun** команды Здравствуйте, toocompile OpenFOAM на всех узлах Linux.</span><span class="sxs-lookup"><span data-stu-id="cea24-212">Then run **clusrun** commands toocompile OpenFOAM on all hello Linux nodes.</span></span>

1. <span data-ttu-id="cea24-213">Создайте /opt/OpenFOAM папки на каждом узле Linux, копирование hello источника пакета toothis папки и его извлечения.</span><span class="sxs-lookup"><span data-stu-id="cea24-213">Create a folder /opt/OpenFOAM on each Linux node, copy hello source package toothis folder, and extract it there.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. <span data-ttu-id="cea24-214">toocompile OpenFOAM с hello Intel MPI библиотеки, сначала настроить несколько переменных среды для Intel MPI и OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="cea24-214">toocompile OpenFOAM with hello Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="cea24-215">Используйте сценарий bash, называются переменными hello tooset settings.sh.</span><span class="sxs-lookup"><span data-stu-id="cea24-215">Use a bash script called settings.sh tooset hello variables.</span></span> <span data-ttu-id="cea24-216">Пример можно найти в hello файлы образцов в конце hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="cea24-216">You can find an example in hello sample files at hello end of this article.</span></span> <span data-ttu-id="cea24-217">Поместить этот файл (с окончаниях Linux) в hello общей папки /openfoam.</span><span class="sxs-lookup"><span data-stu-id="cea24-217">Place this file (saved with Linux line endings) in hello shared folder /openfoam.</span></span> <span data-ttu-id="cea24-218">Этот файл также содержит параметры для сред MPI и OpenFOAM выполнения hello, используется более поздней версии toorun OpenFOAM задания.</span><span class="sxs-lookup"><span data-stu-id="cea24-218">This file also contains settings for hello MPI and OpenFOAM runtimes that you use later toorun an OpenFOAM job.</span></span>
3. <span data-ttu-id="cea24-219">Установите необходимые зависимые пакеты toocompile OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="cea24-219">Install dependent packages needed toocompile OpenFOAM.</span></span> <span data-ttu-id="cea24-220">В зависимости от вашей дистрибутив Linux сначала необходимо tooadd репозитория.</span><span class="sxs-lookup"><span data-stu-id="cea24-220">Depending on your Linux distribution, you might first need tooadd a repository.</span></span> <span data-ttu-id="cea24-221">Запустите **clusrun** аналогичные toohello следующие команды:</span><span class="sxs-lookup"><span data-stu-id="cea24-221">Run **clusrun** commands similar toohello following:</span></span>
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    <span data-ttu-id="cea24-222">При необходимости SSH tooeach Linux узел toorun hello команды tooconfirm правильного запуска.</span><span class="sxs-lookup"><span data-stu-id="cea24-222">If necessary, SSH tooeach Linux node toorun hello commands tooconfirm that they run properly.</span></span>
4. <span data-ttu-id="cea24-223">Выполните следующие команды toocompile OpenFOAM hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-223">Run hello following command toocompile OpenFOAM.</span></span> <span data-ttu-id="cea24-224">процесс компиляции Hello принимает toocomplete некоторое время и создает большой объем выходных данных toostandard сведения журнала, поэтому следует использовать hello **/ чередуются** параметр вывода hello toodisplay с чередованием.</span><span class="sxs-lookup"><span data-stu-id="cea24-224">hello compilation process takes some time toocomplete and generates a large amount of log information toostandard output, so use hello **/interleaved** option toodisplay hello output interleaved.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > <span data-ttu-id="cea24-225">Hello "\\`" символ в команде hello является escape-символа для PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cea24-225">hello “\\`” symbol in hello command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="cea24-226">«\\`&» является частью команды hello hello означает «&».</span><span class="sxs-lookup"><span data-stu-id="cea24-226">“\\`&” means hello “&” is a part of hello command.</span></span>
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a><span data-ttu-id="cea24-227">Подготовка задания OpenFOAM toorun</span><span class="sxs-lookup"><span data-stu-id="cea24-227">Prepare toorun an OpenFOAM job</span></span>
<span data-ttu-id="cea24-228">Теперь get готов toorun задания MPI вызывается sloshingTank3D, которое является одним из примеров OpenFoam hello, на двух узлах Linux.</span><span class="sxs-lookup"><span data-stu-id="cea24-228">Now get ready toorun an MPI job called sloshingTank3D, which is one of hello OpenFoam samples, on two Linux nodes.</span></span> 

### <a name="set-up-hello-runtime-environment"></a><span data-ttu-id="cea24-229">Настройка среды выполнения hello</span><span class="sxs-lookup"><span data-stu-id="cea24-229">Set up hello runtime environment</span></span>
<span data-ttu-id="cea24-230">tooset hello среды выполнения для MPI и OpenFOAM на узлах Linux hello, запустите следующую команду в окне Windows PowerShell на головном узле hello hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-230">tooset up hello runtime environments for MPI and OpenFOAM on hello Linux nodes, run hello following command in a Windows PowerShell window on hello head node.</span></span> <span data-ttu-id="cea24-231">(Эта команда допустима только для SUSE Linux.)</span><span class="sxs-lookup"><span data-stu-id="cea24-231">(This command is valid for SUSE Linux only.)</span></span>

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a><span data-ttu-id="cea24-232">Подготовка примера данных</span><span class="sxs-lookup"><span data-stu-id="cea24-232">Prepare sample data</span></span>
<span data-ttu-id="cea24-233">Используйте hello головном узле настроена общая папка вы ранее tooshare файлов между узлами Linux hello (Подключить как /openfoam).</span><span class="sxs-lookup"><span data-stu-id="cea24-233">Use hello head node share you configured previously tooshare files among hello Linux nodes (mounted as /openfoam).</span></span>

1. <span data-ttu-id="cea24-234">Tooone SSH в ОС Linux вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="cea24-234">SSH tooone of your Linux compute nodes.</span></span>
2. <span data-ttu-id="cea24-235">Запустите hello, следующая команда tooset среды выполнения OpenFOAM hello, если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="cea24-235">Run hello following command tooset up hello OpenFOAM runtime environment, if you haven’t already done this.</span></span>
   
   ```
   $ source /openfoam/settings.sh
   ```
3. <span data-ttu-id="cea24-236">Скопируйте hello sloshingTank3D пример toohello общей папки и перейдите tooit.</span><span class="sxs-lookup"><span data-stu-id="cea24-236">Copy hello sloshingTank3D sample toohello shared folder and navigate tooit.</span></span>
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. <span data-ttu-id="cea24-237">При использовании параметров по умолчанию hello в этом примере может занять десятки toorun минут, поэтому вы можете toomodify toomake некоторых параметров, ее выполняться быстрее.</span><span class="sxs-lookup"><span data-stu-id="cea24-237">When you use hello default parameters of this sample, it can take tens of minutes toorun, so you might want toomodify some parameters toomake it run faster.</span></span> <span data-ttu-id="cea24-238">Один простой вариант — toomodify hello время шаг переменные deltaT и writeInterval в файле system/controlDict hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-238">One simple choice is toomodify hello time step variables deltaT and writeInterval in hello system/controlDict file.</span></span> <span data-ttu-id="cea24-239">Этот файл хранит все входные данные, относящиеся управления toohello времени и чтения и записи данных в решении.</span><span class="sxs-lookup"><span data-stu-id="cea24-239">This file stores all input data relating toohello control of time and reading and writing solution data.</span></span> <span data-ttu-id="cea24-240">Например можно изменить значение hello deltaT из 0,05 too0.5 и writeInterval из 0,05 too0.5 значение hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-240">For example, you could change hello value of deltaT from 0.05 too0.5 and hello value of writeInterval from 0.05 too0.5.</span></span>
   
   ![Изменение переменных шага][step_variables]
5. <span data-ttu-id="cea24-242">Укажите нужные значения для переменных hello в файле system/decomposeParDict hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-242">Specify desired values for hello variables in hello system/decomposeParDict file.</span></span> <span data-ttu-id="cea24-243">В этом примере используются две Linux узлы каждого с 8 ядер, поэтому набора numberOfSubdomains too16 и n hierarchicalCoeffs too(1 1 16), означающее, что выполняется OpenFOAM параллельно с 16 процессов.</span><span class="sxs-lookup"><span data-stu-id="cea24-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains too16 and n of hierarchicalCoeffs too(1 1 16), which means run OpenFOAM in parallel with 16 processes.</span></span> <span data-ttu-id="cea24-244">Дополнительные сведения см. в статье [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4) (Руководство пользователя OpenFOAM. 3.4. Запуск приложений в параллельном режиме).</span><span class="sxs-lookup"><span data-stu-id="cea24-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span></span>
   
   ![Разделение процессов][decompose]
6. <span data-ttu-id="cea24-246">Выполните следующие команды из данных образца hello tooprepare каталога hello sloshingTank3D hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-246">Run hello following commands from hello sloshingTank3D directory tooprepare hello sample data.</span></span>
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. <span data-ttu-id="cea24-247">На головном узле hello вы увидите, что C:\OpenFoam\sloshingTank3D копируются файлы образцов данных hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-247">On hello head node, you should see hello sample data files are copied into C:\OpenFoam\sloshingTank3D.</span></span> <span data-ttu-id="cea24-248">(C:\OpenFoam — hello общая папка на головном узле hello).</span><span class="sxs-lookup"><span data-stu-id="cea24-248">(C:\OpenFoam is hello shared folder on hello head node.)</span></span>
   
   ![Файлы данных на головном узле hello][data_files]

### <a name="host-file-for-mpirun"></a><span data-ttu-id="cea24-250">Файл узлов для mpirun</span><span class="sxs-lookup"><span data-stu-id="cea24-250">Host file for mpirun</span></span>
<span data-ttu-id="cea24-251">На этом шаге создается узел файл (список вычислительных узлов) какие hello **mpirun** команда использует.</span><span class="sxs-lookup"><span data-stu-id="cea24-251">In this step, you create a host file (a list of compute nodes) which hello **mpirun** command uses.</span></span>

1. <span data-ttu-id="cea24-252">На одном из узлов Linux hello создайте файл с именем hostfile под /openfoam, поэтому этот файл может быть достигнута по /openfoam/hostfile на всех узлах Linux.</span><span class="sxs-lookup"><span data-stu-id="cea24-252">On one of hello Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span></span>
2. <span data-ttu-id="cea24-253">В этом файле укажите имена ваших узлов Linux.</span><span class="sxs-lookup"><span data-stu-id="cea24-253">Write your Linux node names into this file.</span></span> <span data-ttu-id="cea24-254">В этом примере файл hello содержит hello следующие имена:</span><span class="sxs-lookup"><span data-stu-id="cea24-254">In this example, hello file contains hello following names:</span></span>
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > <span data-ttu-id="cea24-255">Можно также создать этот файл в C:\OpenFoam\hostfile на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-255">You can also create this file at C:\OpenFoam\hostfile on hello head node.</span></span> <span data-ttu-id="cea24-256">В таком случае сохраните его в виде текстового файла с нотацией Linux для завершения строк (только LF, а не CR LF).</span><span class="sxs-lookup"><span data-stu-id="cea24-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="cea24-257">Это гарантирует, что он работает правильно на узлах Linux hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-257">This ensures that it runs properly on hello Linux nodes.</span></span>
   > 
   > 
   
   <span data-ttu-id="cea24-258">**Оболочка сценария bash**</span><span class="sxs-lookup"><span data-stu-id="cea24-258">**Bash script wrapper**</span></span>
   
   <span data-ttu-id="cea24-259">При наличии большого числа узлов Linux и требуется, чтобы ваш toorun задания на лишь некоторые из них, это не рекомендуется toouse, файл основного узла, так как вы не знаете, какие узлы будут выделяться tooyour задания.</span><span class="sxs-lookup"><span data-stu-id="cea24-259">If you have many Linux nodes and you want your job toorun on only some of them, it’s not a good idea toouse a fixed host file, because you don’t know which nodes will be allocated tooyour job.</span></span> <span data-ttu-id="cea24-260">В этом случае написать скрипт оболочку bash для **mpirun** toocreate hello файл узлов автоматически.</span><span class="sxs-lookup"><span data-stu-id="cea24-260">In this case, write a bash script wrapper for **mpirun** toocreate hello host file automatically.</span></span> <span data-ttu-id="cea24-261">Можно найти оболочку скрипт bash примере вызывается hpcimpirun.sh конце hello в этой статье и сохраните его как /openfoam/hpcimpirun.sh. В этом примере скрипта hello следующие:</span><span class="sxs-lookup"><span data-stu-id="cea24-261">You can find an example bash script wrapper called hpcimpirun.sh at hello end of this article, and save it as /openfoam/hpcimpirun.sh. This example script does hello following:</span></span>
   
   1. <span data-ttu-id="cea24-262">Настраивает hello переменные среды для **mpirun**и некоторые Добавление команды Параметры toorun hello задания MPI через сеть RDMA hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-262">Sets up hello environment variables for **mpirun**, and some addition command parameters toorun hello MPI job through hello RDMA network.</span></span> <span data-ttu-id="cea24-263">В этом случае он устанавливает hello следующие переменные:</span><span class="sxs-lookup"><span data-stu-id="cea24-263">In this case, it sets hello following variables:</span></span>
      
      * <span data-ttu-id="cea24-264">I_MPI_FABRICS=shm:dapl</span><span class="sxs-lookup"><span data-stu-id="cea24-264">I_MPI_FABRICS=shm:dapl</span></span>
      * <span data-ttu-id="cea24-265">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span><span class="sxs-lookup"><span data-stu-id="cea24-265">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span></span>
      * <span data-ttu-id="cea24-266">I_MPI_DYNAMIC_CONNECTION=0</span><span class="sxs-lookup"><span data-stu-id="cea24-266">I_MPI_DYNAMIC_CONNECTION=0</span></span>
   2. <span data-ttu-id="cea24-267">Создает файл узлов, в соответствии с toohello $ переменной среды CCP_NODES_CORES, задаваемый свойством головного узла HPC hello при активации задания hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-267">Creates a host file according toohello environment variable $CCP_NODES_CORES, which is set by hello HPC head node when hello job is activated.</span></span>
      
      <span data-ttu-id="cea24-268">Формат Hello $CCP_NODES_CORES имеет следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="cea24-268">hello format of $CCP_NODES_CORES follows this pattern:</span></span>
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      <span data-ttu-id="cea24-269">где:</span><span class="sxs-lookup"><span data-stu-id="cea24-269">where</span></span>
      
      * <span data-ttu-id="cea24-270">`<Number of nodes>`-hello количество узлов, выделенных toothis задания.</span><span class="sxs-lookup"><span data-stu-id="cea24-270">`<Number of nodes>` - hello number of nodes allocated toothis job.</span></span>  
      * <span data-ttu-id="cea24-271">`<Name of node_n_...>`— Задание toothis выделенной hello имя каждого узла.</span><span class="sxs-lookup"><span data-stu-id="cea24-271">`<Name of node_n_...>` - hello name of each node allocated toothis job.</span></span>
      * <span data-ttu-id="cea24-272">`<Cores of node_n_...>`-hello количество ядер на задание toothis выделенный узел hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-272">`<Cores of node_n_...>` - hello number of cores on hello node allocated toothis job.</span></span>
      
      <span data-ttu-id="cea24-273">Например если задание hello должен toorun двух узлов, $CCP_NODES_CORES аналогична</span><span class="sxs-lookup"><span data-stu-id="cea24-273">For example, if hello job needs two nodes toorun, $CCP_NODES_CORES is similar to</span></span>
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. <span data-ttu-id="cea24-274">Hello вызовов **mpirun** команды и добавляет два параметры toohello командную строку.</span><span class="sxs-lookup"><span data-stu-id="cea24-274">Calls hello **mpirun** command and appends two parameters toohello command line.</span></span>
      
      * <span data-ttu-id="cea24-275">`--hostfile <hostfilepath>: <hostfilepath>`-Создает hello путь файла hello hello узел сценария</span><span class="sxs-lookup"><span data-stu-id="cea24-275">`--hostfile <hostfilepath>: <hostfilepath>` - hello path of hello host file hello script creates</span></span>
      * <span data-ttu-id="cea24-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`— Задание toothis выделенной переменной среды, заданные hello головной узел пакета HPC, где хранятся номера hello общего количества ядер.</span><span class="sxs-lookup"><span data-stu-id="cea24-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by hello HPC Pack head node, which stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="cea24-277">В этом случае он указывает hello число процессов для **mpirun**.</span><span class="sxs-lookup"><span data-stu-id="cea24-277">In this case, it specifies hello number of processes for **mpirun**.</span></span>

## <a name="submit-an-openfoam-job"></a><span data-ttu-id="cea24-278">Отправка задания OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="cea24-278">Submit an OpenFOAM job</span></span>
<span data-ttu-id="cea24-279">Теперь вы можете отправить задание из диспетчера кластера HPC.</span><span class="sxs-lookup"><span data-stu-id="cea24-279">Now you can submit a job in HPC Cluster Manager.</span></span> <span data-ttu-id="cea24-280">Для некоторых задач задания hello должны hpcimpirun.sh сценария toopass hello в hello команд из командной строки.</span><span class="sxs-lookup"><span data-stu-id="cea24-280">You need toopass hello script hpcimpirun.sh in hello command lines for some of hello job tasks.</span></span>

1. <span data-ttu-id="cea24-281">Подключение tooyour головного узла кластера и запуск диспетчера кластеров HPC.</span><span class="sxs-lookup"><span data-stu-id="cea24-281">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="cea24-282">**В управлении ресурсами**, убедитесь, что hello Linux вычислительных узлов в hello **Online** состояния.</span><span class="sxs-lookup"><span data-stu-id="cea24-282">**In Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="cea24-283">Если это не так, выберите их и щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="cea24-283">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="cea24-284">В разделе **Управление заданиями** щелкните **Новое задание**.</span><span class="sxs-lookup"><span data-stu-id="cea24-284">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="cea24-285">Введите имя задания, например *sloshingTank3D*.</span><span class="sxs-lookup"><span data-stu-id="cea24-285">Enter a name for job such as *sloshingTank3D*.</span></span>
   
   ![Сведения о задании][job_details]
5. <span data-ttu-id="cea24-287">В **задания ресурсы**выберите тип ресурса в виде «Узла» hello и установите too2 минимум hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-287">In **Job resources**, choose hello type of resource as “Node” and set hello Minimum too2.</span></span> <span data-ttu-id="cea24-288">Эта конфигурация запускает задание hello на двух узлах Linux, каждый из которых имеет восемь ядер в этом примере.</span><span class="sxs-lookup"><span data-stu-id="cea24-288">This configuration runs hello job on two Linux nodes, each of which has eight cores in this example.</span></span>
   
   ![Ресурсы задания][job_resources]
6. <span data-ttu-id="cea24-290">Нажмите кнопку **изменение задач** в левой области навигации hello и нажмите кнопку **добавить** tooadd задание toohello задачи.</span><span class="sxs-lookup"><span data-stu-id="cea24-290">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span> <span data-ttu-id="cea24-291">Добавьте четыре задание toohello задачи с hello следующие команды и параметры.</span><span class="sxs-lookup"><span data-stu-id="cea24-291">Add four tasks toohello job with hello following command lines and settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cea24-292">Под управлением `source /openfoam/settings.sh` настраивает среды выполнения по hello OpenFOAM и MPI, поэтому каждый из следующих задач hello вызывает перед hello OpenFOAM команды.</span><span class="sxs-lookup"><span data-stu-id="cea24-292">Running `source /openfoam/settings.sh` sets up hello OpenFOAM and MPI runtime environments, so each of hello following tasks calls it before hello OpenFOAM command.</span></span>
   > 
   > 
   
   * <span data-ttu-id="cea24-293">**Задача 1**.</span><span class="sxs-lookup"><span data-stu-id="cea24-293">**Task 1**.</span></span> <span data-ttu-id="cea24-294">Запустите **decomposePar** toogenerate файлы данных для выполнения **interDyMFoam** в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="cea24-294">Run **decomposePar** toogenerate data files for running **interDyMFoam** in parallel.</span></span>
     
     * <span data-ttu-id="cea24-295">Назначить задачу toohello один узел</span><span class="sxs-lookup"><span data-stu-id="cea24-295">Assign one node toohello task</span></span>
     * <span data-ttu-id="cea24-296">**Командная строка** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="cea24-296">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="cea24-297">**Рабочий каталог** — /openfoam/sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="cea24-297">**Working directory** - /openfoam/sloshingTank3D</span></span>
     
     <span data-ttu-id="cea24-298">См. следующий рисунок hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-298">See hello following figure.</span></span> <span data-ttu-id="cea24-299">Аналогичным образом настроить hello оставшихся задач.</span><span class="sxs-lookup"><span data-stu-id="cea24-299">You configure hello remaining tasks similarly.</span></span>
     
     ![Сведения о задаче 1][task_details1]
   * <span data-ttu-id="cea24-301">**Задача 2**.</span><span class="sxs-lookup"><span data-stu-id="cea24-301">**Task 2**.</span></span> <span data-ttu-id="cea24-302">Запустите **interDyMFoam** в образце hello параллельных toocompute.</span><span class="sxs-lookup"><span data-stu-id="cea24-302">Run **interDyMFoam** in parallel toocompute hello sample.</span></span>
     
     * <span data-ttu-id="cea24-303">Назначить задачу toohello двух узлов</span><span class="sxs-lookup"><span data-stu-id="cea24-303">Assign two nodes toohello task</span></span>
     * <span data-ttu-id="cea24-304">**Командная строка** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="cea24-304">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="cea24-305">**Рабочий каталог** — /openfoam/sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="cea24-305">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="cea24-306">**Задача 3**.</span><span class="sxs-lookup"><span data-stu-id="cea24-306">**Task 3**.</span></span> <span data-ttu-id="cea24-307">Запустите **reconstructPar** toomerge hello задает время каталогов из каждого каталога processor_N_ в один набор.</span><span class="sxs-lookup"><span data-stu-id="cea24-307">Run **reconstructPar** toomerge hello sets of time directories from each processor_N_ directory into a single set.</span></span>
     
     * <span data-ttu-id="cea24-308">Назначить задачу toohello один узел</span><span class="sxs-lookup"><span data-stu-id="cea24-308">Assign one node toohello task</span></span>
     * <span data-ttu-id="cea24-309">**Командная строка** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="cea24-309">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="cea24-310">**Рабочий каталог** — /openfoam/sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="cea24-310">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="cea24-311">**Задача 4**.</span><span class="sxs-lookup"><span data-stu-id="cea24-311">**Task 4**.</span></span> <span data-ttu-id="cea24-312">Запустите **foamToEnsight** в параллельных tooconvert hello OpenFOAM результирующие файлы в EnSight форматирования и поместить hello EnSight файлы в каталоге с именем Ensight в каталоге вариантов hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-312">Run **foamToEnsight** in parallel tooconvert hello OpenFOAM result files into EnSight format and place hello EnSight files in a directory named Ensight in hello case directory.</span></span>
     
     * <span data-ttu-id="cea24-313">Назначить задачу toohello двух узлов</span><span class="sxs-lookup"><span data-stu-id="cea24-313">Assign two nodes toohello task</span></span>
     * <span data-ttu-id="cea24-314">**Командная строка** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="cea24-314">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="cea24-315">**Рабочий каталог** — /openfoam/sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="cea24-315">**Working directory** - /openfoam/sloshingTank3D</span></span>
7. <span data-ttu-id="cea24-316">Добавьте зависимости toothese задачи по возрастанию задачи.</span><span class="sxs-lookup"><span data-stu-id="cea24-316">Add dependencies toothese tasks in ascending task order.</span></span>
   
   ![Зависимости задачи][task_dependencies]
8. <span data-ttu-id="cea24-318">Нажмите кнопку **отправить** toorun этого задания.</span><span class="sxs-lookup"><span data-stu-id="cea24-318">Click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="cea24-319">По умолчанию пакет HPC отправляет задание hello в качестве учетной записи текущего вошедшего в систему пользователя.</span><span class="sxs-lookup"><span data-stu-id="cea24-319">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="cea24-320">После нажатия кнопки **отправить**, может появиться диалоговое окно с приглашением tooenter hello имя и пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="cea24-320">After you click **Submit**, you might see a dialog box prompting you tooenter hello user name and password.</span></span>
   
   ![Учетные данные для задания][creds]
   
   <span data-ttu-id="cea24-322">При некоторых условиях HPC Pack запоминает сведения о пользователе hello входных данных до и не показывать это окно.</span><span class="sxs-lookup"><span data-stu-id="cea24-322">Under some conditions, HPC Pack remembers hello user information you input before and doesn’t show this dialog box.</span></span> <span data-ttu-id="cea24-323">toomake HPC Pack снова отобразить его, введите следующую команду в командной строке hello и затем отправить задание hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-323">toomake HPC Pack show it again, enter hello following command at a Command prompt and then submit hello job.</span></span>
   
   ```
   hpccred delcreds
   ```
9. <span data-ttu-id="cea24-324">Задание Hello принимает от десятки минут tooseveral часов в соответствии с toohello параметров, заданных для образца hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-324">hello job takes from tens of minutes tooseveral hours according toohello parameters you have set for hello sample.</span></span> <span data-ttu-id="cea24-325">В карте температур hello вы видите hello задание, выполняющееся на узлах Linux hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-325">In hello heat map, you see hello job running on hello Linux nodes.</span></span> 
   
   ![Тепловая карта][heat_map]
   
   <span data-ttu-id="cea24-327">На каждом узле запускается 8 процессов.</span><span class="sxs-lookup"><span data-stu-id="cea24-327">On each node, eight processes are started.</span></span>
   
   ![Процессы Linux][linux_processes]
10. <span data-ttu-id="cea24-329">По завершении задания hello найти результаты задания hello в папках C:\OpenFoam\sloshingTank3D и файлы журнала hello в C:\OpenFoam.</span><span class="sxs-lookup"><span data-stu-id="cea24-329">When hello job finishes, find hello job results in folders under C:\OpenFoam\sloshingTank3D, and hello log files at C:\OpenFoam.</span></span>

## <a name="view-results-in-ensight"></a><span data-ttu-id="cea24-330">Просмотр результатов в EnSight</span><span class="sxs-lookup"><span data-stu-id="cea24-330">View results in EnSight</span></span>
<span data-ttu-id="cea24-331">При необходимости использовать [EnSight](https://www.ceisoftware.com/) toovisualize и анализ результатов hello hello OpenFOAM задания.</span><span class="sxs-lookup"><span data-stu-id="cea24-331">Optionally use [EnSight](https://www.ceisoftware.com/) toovisualize and analyze hello results of hello OpenFOAM job.</span></span> <span data-ttu-id="cea24-332">Дополнительные сведения о визуализации и анимации в EnSight см. в этом [видеоролике](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span><span class="sxs-lookup"><span data-stu-id="cea24-332">For more about visualization and animation in EnSight, see this [video guide](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span></span>

1. <span data-ttu-id="cea24-333">После установки EnSight на головном узле hello, запустите ее.</span><span class="sxs-lookup"><span data-stu-id="cea24-333">After you install EnSight on hello head node, start it.</span></span>
2. <span data-ttu-id="cea24-334">Откройте файл C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span><span class="sxs-lookup"><span data-stu-id="cea24-334">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span></span>
   
   <span data-ttu-id="cea24-335">Вы увидите бак в средстве просмотра hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-335">You see a tank in hello viewer.</span></span>
   
   ![Резервуар в EnSight][tank]
3. <span data-ttu-id="cea24-337">Создание **Isosurface** из **internalMesh**, а затем выберите переменную hello **alpha_water**.</span><span class="sxs-lookup"><span data-stu-id="cea24-337">Create an **Isosurface** from **internalMesh**, and then choose hello variable **alpha_water**.</span></span>
   
   ![Создание isosurface][isosurface]
4. <span data-ttu-id="cea24-339">Задайте цвет hello в **Isosurface_part** на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-339">Set hello color for **Isosurface_part** created in hello previous step.</span></span> <span data-ttu-id="cea24-340">Например задайте его toowater синим.</span><span class="sxs-lookup"><span data-stu-id="cea24-340">For example, set it toowater blue.</span></span>
   
   ![Изменение цвета isosurface][isosurface_color]
5. <span data-ttu-id="cea24-342">Создание **тома Iso** из **стен** , выбрав **стен** в hello **частей** панели и нажмите кнопку hello **Isosurfaces**  на инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-342">Create an **Iso-volume** from **walls** by selecting **walls** in hello **Parts** panel and click hello **Isosurfaces** button in hello toolbar.</span></span>
6. <span data-ttu-id="cea24-343">В диалоговом окне приветствия выберите **тип** как **Isovolume** и задайте hello минимум **Isovolume диапазон** too0.5.</span><span class="sxs-lookup"><span data-stu-id="cea24-343">In hello dialog box, select **Type** as **Isovolume** and set hello Min of **Isovolume range** too0.5.</span></span> <span data-ttu-id="cea24-344">toocreate Здравствуйте isovolume, нажмите кнопку **создать с помощью выделенных частей**.</span><span class="sxs-lookup"><span data-stu-id="cea24-344">toocreate hello isovolume, click **Create with selected parts**.</span></span>
7. <span data-ttu-id="cea24-345">Задайте цвет hello в **Iso_volume_part** на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-345">Set hello color for **Iso_volume_part** created in hello previous step.</span></span> <span data-ttu-id="cea24-346">Например задайте его toodeep воды синим.</span><span class="sxs-lookup"><span data-stu-id="cea24-346">For example, set it toodeep water blue.</span></span>
8. <span data-ttu-id="cea24-347">Задайте цвет hello в **стен**.</span><span class="sxs-lookup"><span data-stu-id="cea24-347">Set hello color for **walls**.</span></span> <span data-ttu-id="cea24-348">Например задайте его tootransparent белый.</span><span class="sxs-lookup"><span data-stu-id="cea24-348">For example, set it tootransparent white.</span></span>
9. <span data-ttu-id="cea24-349">Теперь щелкните **воспроизведение** toosee hello результаты моделирования hello.</span><span class="sxs-lookup"><span data-stu-id="cea24-349">Now click **Play** toosee hello results of hello simulation.</span></span>
   
    ![Результат для резервуара][tank_result]

## <a name="sample-files"></a><span data-ttu-id="cea24-351">Файлы с примерами</span><span class="sxs-lookup"><span data-stu-id="cea24-351">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="cea24-352">Пример XML-файла конфигурации для развертывания кластера с помощью скрипта PowerShell</span><span class="sxs-lookup"><span data-stu-id="cea24-352">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

### <a name="sample-credxml-file"></a><span data-ttu-id="cea24-353">Пример файла cred.xml</span><span class="sxs-lookup"><span data-stu-id="cea24-353">Sample cred.xml file</span></span>
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```
### <a name="sample-silentcfg-file-tooinstall-mpi"></a><span data-ttu-id="cea24-354">Образец silent.cfg файл tooinstall MPI</span><span class="sxs-lookup"><span data-stu-id="cea24-354">Sample silent.cfg file tooinstall MPI</span></span>
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a><span data-ttu-id="cea24-355">Пример сценария settings.sh</span><span class="sxs-lookup"><span data-stu-id="cea24-355">Sample settings.sh script</span></span>
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a><span data-ttu-id="cea24-356">Пример сценария hpcimpirun.sh</span><span class="sxs-lookup"><span data-stu-id="cea24-356">Sample hpcimpirun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
