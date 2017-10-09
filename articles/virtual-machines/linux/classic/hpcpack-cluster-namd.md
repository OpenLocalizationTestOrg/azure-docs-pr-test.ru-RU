---
title: "aaaNAMD с пакетом Microsoft HPC на виртуальных машинах Linux | Документы Microsoft"
description: "Развертывание кластера пакета Microsoft HPC в Azure и запуск моделирования NAMD с использованием charmrun на нескольких вычислительных узлах Linux."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a><span data-ttu-id="b078c-103">Запуск NAMD с пакетом Microsoft HPC на вычислительных узлах Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="b078c-103">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>
<span data-ttu-id="b078c-104">В этой статье показано одним из способов toorun Linux высокопроизводительных вычислительных систем (HPC) рабочей нагрузки на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="b078c-104">This article shows you one way toorun a Linux high-performance computing (HPC) workload on Azure virtual machines.</span></span> <span data-ttu-id="b078c-105">Здесь, настроить [пакета Microsoft HPC](https://technet.microsoft.com/library/cc514029) кластер в Azure с Linux вычислительных узлов и запустите [NAMD](http://www.ks.uiuc.edu/Research/namd/) toocalculate моделирование и визуализировать структуру hello больших biomolecular системы.</span><span class="sxs-lookup"><span data-stu-id="b078c-105">Here, you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster on Azure with Linux compute nodes and run a [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulation toocalculate and visualize hello structure of a large biomolecular system.</span></span>  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* <span data-ttu-id="b078c-106">**NAMD** (для программы Nanoscale молекулярные Dynamics) — параллельных молекулярные dynamics пакет, предназначенный для высокопроизводительных моделирования больших biomolecular систем, содержащий копии toomillions из атомами.</span><span class="sxs-lookup"><span data-stu-id="b078c-106">**NAMD** (for Nanoscale Molecular Dynamics program) is a parallel molecular dynamics package designed for high-performance simulation of large biomolecular systems containing up toomillions of atoms.</span></span> <span data-ttu-id="b078c-107">К этим системам относятся вирусы, клеточные структуры и большие белки.</span><span class="sxs-lookup"><span data-stu-id="b078c-107">Examples of these systems include viruses, cell structures, and large proteins.</span></span> <span data-ttu-id="b078c-108">NAMD масштабирует toohundreds ядер для типичных моделирования и toomore более 500 000 ядер для имитации наибольшее hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-108">NAMD scales toohundreds of cores for typical simulations and toomore than 500,000 cores for hello largest simulations.</span></span>
* <span data-ttu-id="b078c-109">**Пакет Microsoft HPC** предоставляет возможности toorun крупномасштабных HPC и параллельных приложений в кластерах с локальных компьютеров или виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="b078c-109">**Microsoft HPC Pack** provides features toorun large-scale HPC and parallel applications in clusters of on-premises computers or Azure virtual machines.</span></span> <span data-ttu-id="b078c-110">Изначально предназначенный для рабочих нагрузок HPC, пакет HPC теперь поддерживает приложения HPC для Linux на виртуальных машинах вычислительного узла Linux, развернутых в кластере пакета HPC.</span><span class="sxs-lookup"><span data-stu-id="b078c-110">Originally developed as a solution for Windows HPC workloads, HPC Pack now supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="b078c-111">Общие сведения см. в статье [Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="b078c-111">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction.</span></span>

<span data-ttu-id="b078c-112">Для других параметров toorun Linux HPC рабочих нагрузок в Azure, в разделе [технические ресурсы для пакета и высокопроизводительных вычислительных систем](../../../batch/batch-hpc-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="b078c-112">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/batch-hpc-solutions.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b078c-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b078c-113">Prerequisites</span></span>
* <span data-ttu-id="b078c-114">**Кластер пакета HPC с вычислительными узлами Linux.** Разверните кластер пакета HPC с вычислительными узлами Linux в Azure, используя [шаблон Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) или [скрипт Azure PowerShell](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="b078c-114">**HPC Pack cluster with Linux compute nodes** - Deploy an HPC Pack cluster with Linux compute nodes on Azure using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="b078c-115">В разделе [Приступая к работе с Linux вычислительных узлов в кластере HPC Pack в Azure](hpcpack-cluster.md) hello предварительные условия и действия в любом случае.</span><span class="sxs-lookup"><span data-stu-id="b078c-115">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="b078c-116">При выборе hello вариант развертывания сценария PowerShell см. Образец hello файла конфигурации в файлах образца hello в конце hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="b078c-116">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="b078c-117">Этот файл позволяет настроить кластер пакета HPC на основе Azure, который состоит из головного узла Windows Server 2012 R2 и четырех вычислительных узлов большого размера под управлением CentOS 6.6.</span><span class="sxs-lookup"><span data-stu-id="b078c-117">This file configures an Azure-based HPC Pack cluster consisting of a Windows Server 2012 R2 head node and four size Large CentOS 6.6 compute nodes.</span></span> <span data-ttu-id="b078c-118">Измените этот файл в соответствии со своей средой.</span><span class="sxs-lookup"><span data-stu-id="b078c-118">Customize this file as needed for your environment.</span></span>
* <span data-ttu-id="b078c-119">**Файлы программного обеспечения и учебник NAMD** -NAMD загрузить программное обеспечение для Linux из hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) сайта (требуется регистрация).</span><span class="sxs-lookup"><span data-stu-id="b078c-119">**NAMD software and tutorial files** - Download NAMD software for Linux from hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registration required).</span></span> <span data-ttu-id="b078c-120">В этой статье на основании NAMD версии 2.10 и использует hello [Linux-x86_64 (64-разрядных Intel и AMD с Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) архива.</span><span class="sxs-lookup"><span data-stu-id="b078c-120">This article is based on NAMD version 2.10, and uses hello [Linux-x86_64 (64-bit Intel/AMD with Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span></span> <span data-ttu-id="b078c-121">Кроме того, загрузить hello [файлы учебника NAMD](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span><span class="sxs-lookup"><span data-stu-id="b078c-121">Also download hello [NAMD tutorial files](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span></span> <span data-ttu-id="b078c-122">Hello загружаемые файлы — это файлы в формате TAR, и требуется tooextract средство Windows hello файлов на головном узле кластера hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-122">hello downloads are .tar files, and you need a Windows tool tooextract hello files on hello cluster head node.</span></span> <span data-ttu-id="b078c-123">файлы tooextract hello, следуйте инструкциям hello далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="b078c-123">tooextract hello files, follow hello instructions later in this article.</span></span> 
* <span data-ttu-id="b078c-124">**VMD** (необязательно) — toosee hello результаты задания NAMD, загрузите и установите программу молекулярные визуализации hello [VMD](http://www.ks.uiuc.edu/Research/vmd/) на компьютере по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="b078c-124">**VMD** (optional) - toosee hello results of your NAMD job, download and install hello molecular visualization program [VMD](http://www.ks.uiuc.edu/Research/vmd/) on a computer of your choice.</span></span> <span data-ttu-id="b078c-125">Текущая версия Hello — 1.9.2.</span><span class="sxs-lookup"><span data-stu-id="b078c-125">hello current version is 1.9.2.</span></span> <span data-ttu-id="b078c-126">В разделе hello VMD загрузки tooget сайт к работе.</span><span class="sxs-lookup"><span data-stu-id="b078c-126">See hello VMD download site tooget started.</span></span>  

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="b078c-127">Настройка взаимного доверия между вычислительными узлами</span><span class="sxs-lookup"><span data-stu-id="b078c-127">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="b078c-128">Запуск задания межузловых на нескольких узлах Linux требует hello узлы tootrust друг с другом (с **rsh** или **ssh**).</span><span class="sxs-lookup"><span data-stu-id="b078c-128">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="b078c-129">При создании кластера HPC Pack hello с hello скрипт развертывания IaaS пакета HPC Microsoft hello сценарий автоматически настраивает постоянное взаимного доверия для учетной записи администратора hello, указываемые.</span><span class="sxs-lookup"><span data-stu-id="b078c-129">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="b078c-130">Для пользователей без прав администратора, созданные в домене hello кластера имеют tooset копирование временной взаимного доверия между узлами hello при выделении toothem задания.</span><span class="sxs-lookup"><span data-stu-id="b078c-130">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem.</span></span> <span data-ttu-id="b078c-131">Затем удалите связь hello после завершения задания hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-131">Then, destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="b078c-132">toodo это действие для каждого пользователя, укажите кластер toohello пару ключей RSA какие HPC пакет использует tooestablish hello доверительные отношения.</span><span class="sxs-lookup"><span data-stu-id="b078c-132">toodo this for each user, provide an RSA key pair toohello cluster which HPC Pack uses tooestablish hello trust relationship.</span></span> <span data-ttu-id="b078c-133">Следуйте инструкциям ниже.</span><span class="sxs-lookup"><span data-stu-id="b078c-133">Instructions follow.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="b078c-134">Создание пары ключей RSA</span><span class="sxs-lookup"><span data-stu-id="b078c-134">Generate an RSA key pair</span></span>
<span data-ttu-id="b078c-135">Легко toogenerate пару ключей RSA, который содержит открытый ключ и закрытый ключ, выполнив hello Linux **ssh-keygen** команды.</span><span class="sxs-lookup"><span data-stu-id="b078c-135">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="b078c-136">Войдите в систему tooa компьютера Linux.</span><span class="sxs-lookup"><span data-stu-id="b078c-136">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="b078c-137">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-137">Run hello following command:</span></span>
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="b078c-138">Нажмите клавишу **ввод** toouse параметры по умолчанию hello до завершения команды hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-138">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="b078c-139">Не вводите парольную фразу. При запросе пароля просто нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="b078c-139">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Создание пары ключей RSA][keygen]
3. <span data-ttu-id="b078c-141">Изменить каталог toohello ~/.ssh каталог.</span><span class="sxs-lookup"><span data-stu-id="b078c-141">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="b078c-142">Hello закрытый ключ хранится в id_rsa и hello открытый ключ в id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="b078c-142">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![Открытые и закрытые ключи][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="b078c-144">Добавление кластера HPC Pack toohello пары ключей hello</span><span class="sxs-lookup"><span data-stu-id="b078c-144">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="b078c-145">[Подключитесь с удаленного рабочего стола](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello головного узла виртуальной Машины с помощью учетных данных домена, указанный при развертывании кластера hello (например, hpc\clusteradmin) "hello".</span><span class="sxs-lookup"><span data-stu-id="b078c-145">[Connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, hpc\clusteradmin).</span></span> <span data-ttu-id="b078c-146">Управление hello кластера из головного узла hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-146">You manage hello cluster from hello head node.</span></span>
2. <span data-ttu-id="b078c-147">Используйте стандартные toocreate процедуры Windows Server, учетную запись пользователя домена в домене Active Directory кластера hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-147">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="b078c-148">Например с помощью средства компьютеров и hello пользователя Active Directory на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-148">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="b078c-149">Hello примеры в этой статье предполагается, что пользователь домена с именем hpcuser в домене hpclab hello (hpclab\hpcuser).</span><span class="sxs-lookup"><span data-stu-id="b078c-149">hello examples in this article assume you create a domain user named hpcuser in hello hpclab domain (hpclab\hpcuser).</span></span>
3. <span data-ttu-id="b078c-150">Добавление домена пользователя hello toohello-кластера HPC Pack в качестве пользователя кластера.</span><span class="sxs-lookup"><span data-stu-id="b078c-150">Add hello domain user toohello HPC Pack cluster as a cluster user.</span></span> <span data-ttu-id="b078c-151">Инструкции см. в статье [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx) (Добавление и удаление пользователей кластера).</span><span class="sxs-lookup"><span data-stu-id="b078c-151">For instructions, see [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).</span></span>
4. <span data-ttu-id="b078c-152">Создайте файл с именем C:\cred.xml и скопируйте данные ключа hello RSA в него.</span><span class="sxs-lookup"><span data-stu-id="b078c-152">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="b078c-153">Пример можно найти в hello файлы образцов в конце hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="b078c-153">You can find an example in hello sample files at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. <span data-ttu-id="b078c-154">Откройте командную строку и введите следующую команду, tooset hello учетных данных данные для учетной записи hpclab\hpcuser hello hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-154">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="b078c-155">Использовать hello **extendeddata** toopass параметр hello имя hello C:\cred.xml файл, созданный для hello данных ключа.</span><span class="sxs-lookup"><span data-stu-id="b078c-155">You use hello **extendeddata** parameter toopass hello name of hello C:\cred.xml file you created for hello key data.</span></span>
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="b078c-156">Эта команда успешно завершается без выходных данных.</span><span class="sxs-lookup"><span data-stu-id="b078c-156">This command completes successfully without output.</span></span> <span data-ttu-id="b078c-157">После установки hello учетные данные для учетных записей пользователей hello, необходимые toorun заданий, hello cred.xml файл хранится в безопасном месте или удалите его.</span><span class="sxs-lookup"><span data-stu-id="b078c-157">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
6. <span data-ttu-id="b078c-158">Если на одном из узлов Linux создан hello пару ключей RSA, помните ключи hello toodelete после завершения работы с ними.</span><span class="sxs-lookup"><span data-stu-id="b078c-158">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="b078c-159">Пакет HPC не устанавливает взаимное доверие, если обнаруживает существующий файл id_rsa или id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="b078c-159">HPC Pack does not set up mutual trust if it finds an existing id_rsa file or id_rsa.pub file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b078c-160">Не рекомендуется запускать задания Linux как администратор кластера на общего кластера, поскольку задания, отправлен администратором выполняется под учетной записью root hello на узлах Linux hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-160">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="b078c-161">Задания, отправленный пользователем без прав администратора выполняется под локальной учетной записью пользователя Linux с точно такое же имя, как пользователь задания hello hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-161">A job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="b078c-162">В этом случае пакет HPC устанавливает взаимного доверия для этого пользователя Linux на всех узлах hello выделенной toohello задания.</span><span class="sxs-lookup"><span data-stu-id="b078c-162">In this case, HPC Pack sets up mutual trust for this Linux user across all hello nodes allocated toohello job.</span></span> <span data-ttu-id="b078c-163">Можно настроить пользователя Linux hello вручную на узлах Linux hello перед выполнением задания hello или автоматически создает hello пользователя при отправке задания hello пакета HPC.</span><span class="sxs-lookup"><span data-stu-id="b078c-163">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="b078c-164">Если пакет HPC создает пользователя hello, HPC Pack удаляет его после завершения задания hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-164">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="b078c-165">tooreduce угрозу безопасности, ключи, удаляются после завершения задания hello на узлах hello hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-165">tooreduce security threat, hello keys are removed after hello job completes on hello nodes.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="b078c-166">Настройка файлового ресурса для узлов Linux</span><span class="sxs-lookup"><span data-stu-id="b078c-166">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="b078c-167">Теперь настроить файловый ресурс SMB и подключить hello общей папки на все Linux узлы tooallow hello Linux узлы tooaccess NAMD файлы с общий путь.</span><span class="sxs-lookup"><span data-stu-id="b078c-167">Now set up an SMB file share, and mount hello shared folder on all Linux nodes tooallow hello Linux nodes tooaccess NAMD files with a common path.</span></span> <span data-ttu-id="b078c-168">Ниже приведены шаги toomount общей папки на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-168">Following are steps toomount a shared folder on hello head node.</span></span> <span data-ttu-id="b078c-169">Например CentOS 6.6 распределения, которые в настоящее время не поддерживают hello файловая служба Azure рекомендуется общую папку.</span><span class="sxs-lookup"><span data-stu-id="b078c-169">A share is recommended for distributions such as CentOS 6.6 that currently don’t support hello Azure File service.</span></span> <span data-ttu-id="b078c-170">Если на узлах Linux поддерживает Azure файловый ресурс, в разделе [как toouse хранилища Azure File с Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b078c-170">If your Linux nodes support an Azure File share, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="b078c-171">Дополнительные параметры использования файловых ресурсов с помощью пакета HPC описаны в статье [Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="b078c-171">For additional file sharing options with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="b078c-172">Создайте папку на головном узле hello и предоставить к нему tooEveryone, задав права чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="b078c-172">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="b078c-173">В этом примере \\ \\CentOS66HN\Namd — имя hello hello папки, где CentOS66HN — имя узла hello hello головного узла.</span><span class="sxs-lookup"><span data-stu-id="b078c-173">In this example, \\\\CentOS66HN\Namd is hello name of hello folder, where CentOS66HN is hello host name of hello head node.</span></span>
2. <span data-ttu-id="b078c-174">Создайте вложенную папку с именем namd2 в общей папке hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-174">Create a subfolder named namd2 in hello shared folder.</span></span> <span data-ttu-id="b078c-175">В namd2 создайте вложенную папку namdsample.</span><span class="sxs-lookup"><span data-stu-id="b078c-175">In namd2, create another subfolder named namdsample.</span></span>
3. <span data-ttu-id="b078c-176">Для извлечения файлов NAMD hello в папке hello используется версия Windows **tar** или другой программы Windows, работающая в формате TAR архивы.</span><span class="sxs-lookup"><span data-stu-id="b078c-176">Extract hello NAMD files in hello folder by using a Windows version of **tar** or another Windows utility that operates on .tar archives.</span></span> 
   
   * <span data-ttu-id="b078c-177">Извлеките архив tar NAMD hello слишком\\\\CentOS66HN\Namd\namd2.</span><span class="sxs-lookup"><span data-stu-id="b078c-177">Extract hello NAMD tar archive too\\\\CentOS66HN\Namd\namd2.</span></span>
   * <span data-ttu-id="b078c-178">Извлеките файлы учебника hello под \\ \\CentOS66HN\Namd\namd2\namdsample.</span><span class="sxs-lookup"><span data-stu-id="b078c-178">Extract hello tutorial files under \\\\CentOS66HN\Namd\namd2\namdsample.</span></span>
4. <span data-ttu-id="b078c-179">Откройте окно Windows PowerShell и выполните следующие команды toomount hello общую папку на узлах Linux hello hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-179">Open a Windows PowerShell window and run hello following commands toomount hello shared folder on hello Linux nodes.</span></span>
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="b078c-180">Hello первая команда создает папку с именем /namd2 на всех узлах в группе LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-180">hello first command creates a folder named /namd2 on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="b078c-181">Вторая команда Hello подключает //CentOS66HN/Namd/namd2 hello общие папки на папку hello с dir_mode и file_mode too777 набор битов.</span><span class="sxs-lookup"><span data-stu-id="b078c-181">hello second command mounts hello shared folder //CentOS66HN/Namd/namd2 onto hello folder with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="b078c-182">Hello *username* и *пароль* в hello команды должны быть учетные данные пользователя на головном узле hello hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-182">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="b078c-183">Hello "\\`" символа в hello вторая команда является escape-символа для PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b078c-183">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="b078c-184">«\\`, «hello», означает» (запятая) является частью команды hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-184">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a><span data-ttu-id="b078c-185">Создание скрипта Bash toorun NAMD задания</span><span class="sxs-lookup"><span data-stu-id="b078c-185">Create a Bash script toorun a NAMD job</span></span>
<span data-ttu-id="b078c-186">Задание NAMD должен *nodelist* в файле **charmrun** toodetermine hello количество узлов toouse при запуске NAMD процессов.</span><span class="sxs-lookup"><span data-stu-id="b078c-186">Your NAMD job needs a *nodelist* file for **charmrun** toodetermine hello number of nodes toouse when starting NAMD processes.</span></span> <span data-ttu-id="b078c-187">С помощью Bash скрипта, создающий файл nodelist hello и запускает **charmrun** с этим файлом набору узлов.</span><span class="sxs-lookup"><span data-stu-id="b078c-187">You use a Bash script that generates hello nodelist file and runs **charmrun** with this nodelist file.</span></span> <span data-ttu-id="b078c-188">Затем отправьте задание NAMD в диспетчер кластера HPC, вызывающий этот сценарий.</span><span class="sxs-lookup"><span data-stu-id="b078c-188">You can then submit a NAMD job in HPC Cluster Manager that calls this script.</span></span>

<span data-ttu-id="b078c-189">В текстовом редакторе, по своему усмотрению, создайте сценарий Bash папки /namd2 hello hello NAMD программные файлы и назовите его hpccharmrun.sh. Для быстрого пробной версии, скопируйте сценарий hpccharmrun.sh пример hello, приведенный в конце hello в этой статье и перейти слишком[отправить задание NAMD](#submit-a-namd-job).</span><span class="sxs-lookup"><span data-stu-id="b078c-189">Using a text editor of your choice, create a Bash script in hello /namd2 folder containing hello NAMD program files and name it hpccharmrun.sh. For a quick proof of concept, copy hello example hpccharmrun.sh script provided at hello end of this article and go too[Submit a NAMD job](#submit-a-namd-job).</span></span>

> [!TIP]
> <span data-ttu-id="b078c-190">Сохраните сценарий как текстовый файл, в котором для завершения строк используется нотация Linux (только LF, а не CR LF).</span><span class="sxs-lookup"><span data-stu-id="b078c-190">Save your script as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="b078c-191">Это гарантирует, что он работает правильно на узлах Linux hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-191">This ensures that it runs properly on hello Linux nodes.</span></span>
> 
> 

<span data-ttu-id="b078c-192">Ниже приведены сведения о том, что делает этот сценарий Bash.</span><span class="sxs-lookup"><span data-stu-id="b078c-192">Following are details about what this bash script does.</span></span> 

1. <span data-ttu-id="b078c-193">Определите несколько переменных.</span><span class="sxs-lookup"><span data-stu-id="b078c-193">Define some variables.</span></span>
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. <span data-ttu-id="b078c-194">Получите сведения об узле из переменных среды hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-194">Get node information from hello environment variables.</span></span> <span data-ttu-id="b078c-195">В переменной $NODESCORES хранится список разбиения слов из $CCP_NODES_CORES.</span><span class="sxs-lookup"><span data-stu-id="b078c-195">$NODESCORES stores a list of split words from $CCP_NODES_CORES.</span></span> <span data-ttu-id="b078c-196">$COUNT — размер hello $NODESCORES.</span><span class="sxs-lookup"><span data-stu-id="b078c-196">$COUNT is hello size of $NODESCORES.</span></span>
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   <span data-ttu-id="b078c-197">Hello для переменной CCP_NODES_CORES hello $ имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="b078c-197">hello format for hello $CCP_NODES_CORES variable is as follows:</span></span>
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   <span data-ttu-id="b078c-198">Эта переменная перечисляет hello общее число узлов, имена узлов и количество ядер на каждом узле, выделенных toohello задания.</span><span class="sxs-lookup"><span data-stu-id="b078c-198">This variable lists hello total number of nodes, node names, and number of cores on each node that are allocated toohello job.</span></span> <span data-ttu-id="b078c-199">Например если задание hello должен 10 toorun ядер, значение hello $CCP_NODES_CORES похожа на:</span><span class="sxs-lookup"><span data-stu-id="b078c-199">For example, if hello job needs 10 cores toorun, hello value of $CCP_NODES_CORES is similar to:</span></span>
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. <span data-ttu-id="b078c-200">Если переменная CCP_NODES_CORES $ hello не задано, запустите **charmrun** напрямую.</span><span class="sxs-lookup"><span data-stu-id="b078c-200">If hello $CCP_NODES_CORES variable is not set, start **charmrun** directly.</span></span> <span data-ttu-id="b078c-201">(это должно происходить, только если сценарий запускается непосредственно на узлах Linux).</span><span class="sxs-lookup"><span data-stu-id="b078c-201">(This should only occur when you run this script directly on your Linux nodes.)</span></span>
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. <span data-ttu-id="b078c-202">Или создайте файл nodelist для **charmrun**.</span><span class="sxs-lookup"><span data-stu-id="b078c-202">Or create a nodelist file for **charmrun**.</span></span>
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. <span data-ttu-id="b078c-203">Запустите **charmrun** файлом nodelist hello, получить его состояние возврата и удалите файл nodelist hello в конце hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-203">Run **charmrun** with hello nodelist file, get its return status, and remove hello nodelist file at hello end.</span></span>
   
   <span data-ttu-id="b078c-204">${CCP_NUMCPUS} является другой переменной среды, заданные головной узел пакета HPC hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-204">${CCP_NUMCPUS} is another environment variable set by hello HPC Pack head node.</span></span> <span data-ttu-id="b078c-205">Он хранит номер hello общего количества ядер, выделенных toothis задания.</span><span class="sxs-lookup"><span data-stu-id="b078c-205">It stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="b078c-206">Мы используем его toospecify hello число процессов для charmrun.</span><span class="sxs-lookup"><span data-stu-id="b078c-206">We use it toospecify hello number of processes for charmrun.</span></span>
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. <span data-ttu-id="b078c-207">Выход с hello **charmrun** код возврата.</span><span class="sxs-lookup"><span data-stu-id="b078c-207">Exit with hello **charmrun** return status.</span></span>
   
   ```
   exit ${RTNSTS}
   ```

<span data-ttu-id="b078c-208">Ниже приведен hello данные в файле nodelist hello, какой сценарий hello приводит к возникновению ошибки.</span><span class="sxs-lookup"><span data-stu-id="b078c-208">Following is hello information in hello nodelist file, which hello script generates:</span></span>

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

<span data-ttu-id="b078c-209">Например:</span><span class="sxs-lookup"><span data-stu-id="b078c-209">For example:</span></span>

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a><span data-ttu-id="b078c-210">Отправка задания NAMD</span><span class="sxs-lookup"><span data-stu-id="b078c-210">Submit a NAMD job</span></span>
<span data-ttu-id="b078c-211">Теперь все готово toosubmit NAMD задания в диспетчере кластера HPC.</span><span class="sxs-lookup"><span data-stu-id="b078c-211">Now you are ready toosubmit a NAMD job in HPC Cluster Manager.</span></span>

1. <span data-ttu-id="b078c-212">Подключение tooyour головного узла кластера и запуск диспетчера кластеров HPC.</span><span class="sxs-lookup"><span data-stu-id="b078c-212">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="b078c-213">В **управление ресурсами**, убедитесь, что hello Linux вычислительных узлов в hello **Online** состояния.</span><span class="sxs-lookup"><span data-stu-id="b078c-213">In **Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="b078c-214">Если это не так, выберите их и щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="b078c-214">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="b078c-215">В разделе **Управление заданиями** щелкните **Новое задание**.</span><span class="sxs-lookup"><span data-stu-id="b078c-215">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="b078c-216">Введите для задания имя, например *hpccharmrun*.</span><span class="sxs-lookup"><span data-stu-id="b078c-216">Enter a name for job such as *hpccharmrun*.</span></span>
   
   ![Новое задание HPC][namd_job]
5. <span data-ttu-id="b078c-218">На hello **сведений о задании** в разделе **ресурсы задания**, выберите тип ресурса в качестве hello **узел** и набор hello **минимум** too3.</span><span class="sxs-lookup"><span data-stu-id="b078c-218">On hello **Job Details** page, under **Job Resources**, select hello type of resource as **Node** and set hello **Minimum** too3.</span></span> <span data-ttu-id="b078c-219">, запустим hello задания на трех узлах Linux, и каждый узел имеет четыре ядра.</span><span class="sxs-lookup"><span data-stu-id="b078c-219">, we run hello job on three Linux nodes and each node has four cores.</span></span>
   
   ![Ресурсы задания][job_resources]
6. <span data-ttu-id="b078c-221">Нажмите кнопку **изменение задач** в левой области навигации hello и нажмите кнопку **добавить** tooadd задание toohello задачи.</span><span class="sxs-lookup"><span data-stu-id="b078c-221">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span>    
7. <span data-ttu-id="b078c-222">На hello **сведения о задаче и перенаправление ввода-вывода** страница hello набор следующие значения:</span><span class="sxs-lookup"><span data-stu-id="b078c-222">On hello **Task Details and I/O Redirection** page, set hello following values:</span></span>
   
   * <span data-ttu-id="b078c-223">**Командная строка** -
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span><span class="sxs-lookup"><span data-stu-id="b078c-223">**Command line** -
`/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span></span>
     
     > [!TIP]
     > <span data-ttu-id="b078c-224">Hello предыдущей командной строке является единственной командой, без разрывов.</span><span class="sxs-lookup"><span data-stu-id="b078c-224">hello preceding command line is a single command without line breaks.</span></span> <span data-ttu-id="b078c-225">Создает оболочку tooappear на несколько строк в группе **командной строки**.</span><span class="sxs-lookup"><span data-stu-id="b078c-225">It wraps tooappear on several lines under **Command line**.</span></span>
     > 
     > 
   * <span data-ttu-id="b078c-226">**Рабочий каталог** — /namd2.</span><span class="sxs-lookup"><span data-stu-id="b078c-226">**Working directory** - /namd2</span></span>
   * <span data-ttu-id="b078c-227">**Минимум** — 3.</span><span class="sxs-lookup"><span data-stu-id="b078c-227">**Minimum** - 3</span></span>
     
     ![Сведения о задаче][task_details]
     
     > [!NOTE]
     > <span data-ttu-id="b078c-229">Заданные hello рабочий каталог из-за **charmrun** пытается toonavigate toohello же рабочий каталог на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="b078c-229">You set hello working directory here because **charmrun** tries toonavigate toohello same working directory on each node.</span></span> <span data-ttu-id="b078c-230">Если hello рабочий каталог не настроен, пакет HPC запускается команда hello в произвольным именем папки, созданной на одном из узлов Linux hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-230">If hello working directory isn't set, HPC Pack starts hello command in a randomly named folder created on one of hello Linux nodes.</span></span> <span data-ttu-id="b078c-231">В результате следующая ошибка на hello hello других узлов: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid эту проблему, укажите путь к папке, доступный на всех узлах как hello рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="b078c-231">This causes hello following error on hello other nodes: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid this problem, specify a folder path that can be accessed by all nodes as hello working directory.</span></span>
     > 
     > 
8. <span data-ttu-id="b078c-232">Нажмите кнопку **ОК** и нажмите кнопку **отправить** toorun этого задания.</span><span class="sxs-lookup"><span data-stu-id="b078c-232">Click **OK** and then click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="b078c-233">По умолчанию пакет HPC отправляет задание hello в качестве учетной записи текущего вошедшего в систему пользователя.</span><span class="sxs-lookup"><span data-stu-id="b078c-233">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="b078c-234">Диалоговое окно может попросить tooenter hello имя и пароль пользователя после нажатия кнопки **отправить**.</span><span class="sxs-lookup"><span data-stu-id="b078c-234">A dialog box might prompt you tooenter hello user name and password after you click **Submit**.</span></span>
   
   ![Учетные данные для задания][creds]
   
   <span data-ttu-id="b078c-236">При некоторых условиях HPC Pack запоминает сведения о пользователе hello входных данных до и не показывать это окно.</span><span class="sxs-lookup"><span data-stu-id="b078c-236">Under some conditions, HPC Pack remembers hello user information you input before and doesn't show this dialog box.</span></span> <span data-ttu-id="b078c-237">toomake HPC Pack снова отобразить его, введите следующую команду в командной строке hello и затем отправить задание hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-237">toomake HPC Pack show it again, enter hello following command at a Command Prompt and then submit hello job.</span></span>
   
   ```command
   hpccred delcreds
   ```
9. <span data-ttu-id="b078c-238">Задание Hello занимает несколько минут toofinish.</span><span class="sxs-lookup"><span data-stu-id="b078c-238">hello job takes several minutes toofinish.</span></span>
10. <span data-ttu-id="b078c-239">Поиск журнала задания hello в \\ <headnodeName>\Namd\namd2\namd2_hpccharmrun.log и hello выходные файлы в \\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span><span class="sxs-lookup"><span data-stu-id="b078c-239">Find hello job log at \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log and hello output files in \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span></span>
11. <span data-ttu-id="b078c-240">При необходимости запустите VMD tooview результаты задания.</span><span class="sxs-lookup"><span data-stu-id="b078c-240">Optionally, start VMD tooview your job results.</span></span> <span data-ttu-id="b078c-241">Hello действия для визуализации hello NAMD выходных файлов (в данном случае молекула белок ubiquitin в сфере воды) выходят за рамки данной статьи hello.</span><span class="sxs-lookup"><span data-stu-id="b078c-241">hello steps for visualizing hello NAMD output files (in this case, a ubiquitin protein molecule in a water sphere) are beyond hello scope of this article.</span></span> <span data-ttu-id="b078c-242">Дополнительные сведения см. в [руководстве по NAMD](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf).</span><span class="sxs-lookup"><span data-stu-id="b078c-242">See [NAMD Tutorial](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) for details.</span></span>
    
    ![Результаты задания][vmd_view]

## <a name="sample-files"></a><span data-ttu-id="b078c-244">Файлы с примерами</span><span class="sxs-lookup"><span data-stu-id="b078c-244">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="b078c-245">Пример XML-файла конфигурации для развертывания кластера с помощью скрипта PowerShell</span><span class="sxs-lookup"><span data-stu-id="b078c-245">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>    
```

### <a name="sample-credxml-file"></a><span data-ttu-id="b078c-246">Пример файла cred.xml</span><span class="sxs-lookup"><span data-stu-id="b078c-246">Sample cred.xml file</span></span>
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

### <a name="sample-hpccharmrunsh-script"></a><span data-ttu-id="b078c-247">Пример сценария hpccharmrun.sh</span><span class="sxs-lookup"><span data-stu-id="b078c-247">Sample hpccharmrun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png
