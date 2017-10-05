---
title: "Запуск заданий OpenFOAM с помощью пакета HPC на виртуальных машинах Linux | Документация Майкрософт"
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
ms.openlocfilehash: ef124a8983fa112d499252460bff9ed2fcccc02b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="c66fc-103">Выполнение заданий OpenFoam в кластере Linux RDMA в Azure с помощью пакета Microsoft HPC</span><span class="sxs-lookup"><span data-stu-id="c66fc-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="c66fc-104">В этой статье показан один из способов запуска OpenFoam на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="c66fc-104">This article shows you one way to run OpenFoam in Azure virtual machines.</span></span> <span data-ttu-id="c66fc-105">Здесь мы развернем кластер пакета Microsoft HPC в Azure с использованием вычислительных узлов Linux и запустим задание [OpenFoam](http://openfoam.com/), используя библиотеку Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="c66fc-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span></span> <span data-ttu-id="c66fc-106">Для вычислительных узлов можно использовать виртуальные машины Azure с поддержкой RDMA. Так они смогут взаимодействовать по сети Azure RDMA.</span><span class="sxs-lookup"><span data-stu-id="c66fc-106">You can use RDMA-capable Azure VMs for the compute nodes, so that the compute nodes communicate over the Azure RDMA network.</span></span> <span data-ttu-id="c66fc-107">Другие варианты запуска OpenFoam в Azure включают в себя полностью настроенные коммерческие образы, доступные на сайте Marketplace, например образ [OpenFoam 2.3 на основе CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/) от UberCloud, и запуск посредством [пакетной службы Azure](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span><span class="sxs-lookup"><span data-stu-id="c66fc-107">Other options to run OpenFoam in Azure include fully configured commercial images available in the Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="c66fc-108">OpenFOAM (англ. Open Field Operation and Manipulation) — это пакет программного обеспечения с открытым исходным кодом для вычислительной гидродинамики (CFD). Он широко используется в технической и научной областях, а также в коммерческих и научных организациях.</span><span class="sxs-lookup"><span data-stu-id="c66fc-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span></span> <span data-ttu-id="c66fc-109">Пакет содержит средства для сеточного разбиения (например, snappyHexMesh), включает средство распараллеливания расчетов для сложных геометрических объектов, а также функции предварительной и последующей обработки.</span><span class="sxs-lookup"><span data-stu-id="c66fc-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span></span> <span data-ttu-id="c66fc-110">Почти все процессы выполняются параллельно, что позволяет пользователям максимально задействовать ресурсы компьютера.</span><span class="sxs-lookup"><span data-stu-id="c66fc-110">Almost all processes run in parallel, enabling users to take full advantage of computer hardware at their disposal.</span></span>  

<span data-ttu-id="c66fc-111">Пакет Microsoft HPC предоставляет функции, необходимые для работы приложений высокопроизводительных и параллельных вычислений, включая приложения MPI, в кластерах виртуальных машин Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c66fc-111">Microsoft HPC Pack provides features to run large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="c66fc-112">Пакет HPC также поддерживает приложения высокопроизводительных вычислений для Linux на виртуальных вычислительных узлах Linux, развернутых в кластере HPC.</span><span class="sxs-lookup"><span data-stu-id="c66fc-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="c66fc-113">Общие сведения об использовании вычислительных узлов Linux и пакета HPC см. в статье [Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="c66fc-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction to using Linux compute nodes with HPC Pack.</span></span>

> [!NOTE]
> <span data-ttu-id="c66fc-114">В этой статье демонстрируется выполнение рабочей нагрузки MPI в Linux с помощью пакета HPC.</span><span class="sxs-lookup"><span data-stu-id="c66fc-114">This article illustrates how to run a Linux MPI workload with HPC Pack.</span></span> <span data-ttu-id="c66fc-115">Здесь предполагается, что у вас есть опыт в администрировании Linux и выполнении рабочих нагрузок MPI на кластерах Linux.</span><span class="sxs-lookup"><span data-stu-id="c66fc-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span></span> <span data-ttu-id="c66fc-116">При использовании версий MPI и OpenFOAM, отличных от тех, которые показаны в этой статье, может потребоваться изменить некоторые действия по установке и настройке.</span><span class="sxs-lookup"><span data-stu-id="c66fc-116">If you use versions of MPI and OpenFOAM different from the ones shown in this article, you might have to modify some installation and configuration steps.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c66fc-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c66fc-117">Prerequisites</span></span>
* <span data-ttu-id="c66fc-118">**Кластер пакета HPC с вычислительными узлами Linux с поддержкой RDMA**. Разверните кластер пакета HPC с вычислительными узлами размером A8, A9, H16r или H16rm под управлением Linux, используя [шаблон Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) или [сценарий Azure PowerShell](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="c66fc-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="c66fc-119">Предварительные требования и необходимые действия для обоих вариантов см. в статье [Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="c66fc-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for the prerequisites and steps for either option.</span></span> <span data-ttu-id="c66fc-120">Если вы выбрали вариант со сценарием PowerShell, просмотрите один из примеров файлов конфигурации в конце этой статьи.</span><span class="sxs-lookup"><span data-stu-id="c66fc-120">If you choose the PowerShell script deployment option, see the sample configuration file in the sample files at the end of this article.</span></span> <span data-ttu-id="c66fc-121">Используйте его, чтобы развернуть кластер пакета HPC Azure, состоящий из головного узла Windows Server 2012 R2 размера А8 и двух вычислительных узлов размера А8 под управлением SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="c66fc-121">Use this configuration to deploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span></span> <span data-ttu-id="c66fc-122">Вместо используемых в файле имен подписки и службы подставьте свои значения.</span><span class="sxs-lookup"><span data-stu-id="c66fc-122">Substitute appropriate values for your subscription and service names.</span></span> 
  
  <span data-ttu-id="c66fc-123">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="c66fc-123">**Additional things to know**</span></span>
  
  * <span data-ttu-id="c66fc-124">Предварительные требования к использованию вычислительных узлов Linux RDMA в Azure см. в статье [Размеры виртуальных машин, оптимизированных для высокопроизводительных вычислений](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c66fc-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  * <span data-ttu-id="c66fc-125">Если вы выбрали вариант развертывания скрипта Powershell, развертывайте все вычислительные узлы Linux в пределах одной облачной службы, чтобы использовать сетевое подключение RDMA.</span><span class="sxs-lookup"><span data-stu-id="c66fc-125">If you use the Powershell script deployment option, deploy all the Linux compute nodes within one cloud service to use the RDMA network connection.</span></span>
  * <span data-ttu-id="c66fc-126">После развертывания узлов Linux установите SSH-подключение для выполнения дополнительных задач администрирования.</span><span class="sxs-lookup"><span data-stu-id="c66fc-126">After deploying the Linux nodes, connect by SSH to perform any additional administrative tasks.</span></span> <span data-ttu-id="c66fc-127">Сведения о SSH-подключении для каждой виртуальной машины Linux можно найти на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c66fc-127">Find the SSH connection details for each Linux VM in the Azure portal.</span></span>  
* <span data-ttu-id="c66fc-128">**Intel MPI**. Для запуска OpenFOAM на вычислительных узлах SLES 12 HPC в Azure вам потребуется установить библиотеку среды выполнения Intel MPI Library 5, которую можно скачать с сайта [Intel.com](https://software.intel.com/en-us/intel-mpi-library/).</span><span class="sxs-lookup"><span data-stu-id="c66fc-128">**Intel MPI** - To run OpenFOAM on SLES 12 HPC compute nodes in Azure, you need to install the Intel MPI Library 5 runtime from the [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span></span> <span data-ttu-id="c66fc-129">(Среда выполнения Intel MPI 5 предустановлена в образах на основе CentOS для HPC.)  Позже установите Intel MPI на вычислительные узлы Linux, если это будет необходимо.</span><span class="sxs-lookup"><span data-stu-id="c66fc-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span></span> <span data-ttu-id="c66fc-130">Для этого после регистрации на сайте Intel перейдите по ссылке в письме с подтверждением на соответствующую веб-страницу.</span><span class="sxs-lookup"><span data-stu-id="c66fc-130">To prepare for this step, after you register with Intel, follow the link in the confirmation email to the related web page.</span></span> <span data-ttu-id="c66fc-131">Затем скопируйте ссылку для скачивания TGZ-файла для соответствующей версии Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="c66fc-131">Then, copy the download link for the .tgz file for the appropriate version of Intel MPI.</span></span> <span data-ttu-id="c66fc-132">В этой статье используется Intel MPI версии 5.0.3.048.</span><span class="sxs-lookup"><span data-stu-id="c66fc-132">This article is based on Intel MPI version 5.0.3.048.</span></span>
* <span data-ttu-id="c66fc-133">**Исходный пакет OpenFOAM.** Загрузите исходный пакет OpenFOAM для Linux на сайте [OpenFOAM Foundation](http://openfoam.org/download/2-3-1-source/).</span><span class="sxs-lookup"><span data-stu-id="c66fc-133">**OpenFOAM Source Pack** - Download the OpenFOAM Source Pack software for Linux from the [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span></span> <span data-ttu-id="c66fc-134">В этой статье используется пакет версии 2.3.1, доступный для загрузки в виде файла OpenFOAM-2.3.1.tgz.</span><span class="sxs-lookup"><span data-stu-id="c66fc-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span></span> <span data-ttu-id="c66fc-135">Инструкции по распаковке и компиляции OpenFOAM на вычислительных узлах Linux приведены далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="c66fc-135">Follow the instructions later in this article to unpack and compile OpenFOAM on the Linux compute nodes.</span></span>
* <span data-ttu-id="c66fc-136">**EnSight** (необязательно). Для просмотра результатов моделирования OpenFOAM скачайте и установите программу [EnSight](https://www.ceisoftware.com/download/), предназначенную для визуализации и анализа данных.</span><span class="sxs-lookup"><span data-stu-id="c66fc-136">**EnSight** (optional) - To see the results of your OpenFOAM simulation, download and install the [EnSight](https://www.ceisoftware.com/download/) visualization and analysis program.</span></span> <span data-ttu-id="c66fc-137">Сведения о лицензировании и загрузке приведены на сайте EnSight.</span><span class="sxs-lookup"><span data-stu-id="c66fc-137">Licensing and download information are at the EnSight site.</span></span>

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="c66fc-138">Настройка взаимного доверия между вычислительными узлами</span><span class="sxs-lookup"><span data-stu-id="c66fc-138">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="c66fc-139">Чтобы задание выполнялось на нескольких узлах Linux одновременно, сначала необходимо настроить взаимное доверие узлов (через протокол **rsh** или **ssh**).</span><span class="sxs-lookup"><span data-stu-id="c66fc-139">Running a cross-node job on multiple Linux nodes requires the nodes to trust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="c66fc-140">При создании кластера HPC с помощью сценария развертывания Microsoft HPC IaaS сценарий автоматически настраивает постоянное взаимное доверие для указанной учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="c66fc-140">When you create the HPC Pack cluster with the Microsoft HPC Pack IaaS deployment script, the script automatically sets up permanent mutual trust for the administrator account you specify.</span></span> <span data-ttu-id="c66fc-141">Для учетных записей пользователей без прав администратора, создаваемых в домене кластера, взаимное доверие между узлами должно создаваться в момент назначения им задания и уничтожаться после завершения задания.</span><span class="sxs-lookup"><span data-stu-id="c66fc-141">For non-administrator users you create in the cluster's domain, you have to set up temporary mutual trust among the nodes when a job is allocated to them, and destroy the relationship after the job is complete.</span></span> <span data-ttu-id="c66fc-142">Чтобы реализовать это для всех пользователей, укажите пару ключей RSA в кластере, который пакет HPC использует для установления отношения доверия.</span><span class="sxs-lookup"><span data-stu-id="c66fc-142">To establish trust for each user, provide an RSA key pair to the cluster that HPC Pack uses for the trust relationship.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="c66fc-143">Создание пары ключей RSA</span><span class="sxs-lookup"><span data-stu-id="c66fc-143">Generate an RSA key pair</span></span>
<span data-ttu-id="c66fc-144">Чтобы создать пару ключей RSA, состоящую из открытого и закрытого ключей, достаточно выполнить команду Linux **ssh-keygen** .</span><span class="sxs-lookup"><span data-stu-id="c66fc-144">It's easy to generate an RSA key pair, which contains a public key and a private key, by running the Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="c66fc-145">Войдите на компьютер под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="c66fc-145">Log on to a Linux computer.</span></span>
2. <span data-ttu-id="c66fc-146">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c66fc-146">Run the following command:</span></span>
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="c66fc-147">В ходе выполнения команды используйте параметры по умолчанию (нажимайте клавишу **ВВОД**).</span><span class="sxs-lookup"><span data-stu-id="c66fc-147">Press **Enter** to use the default settings until the command is completed.</span></span> <span data-ttu-id="c66fc-148">Не вводите парольную фразу. При запросе пароля просто нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="c66fc-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Создание пары ключей RSA][keygen]
3. <span data-ttu-id="c66fc-150">Измените каталог на ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="c66fc-150">Change directory to the ~/.ssh directory.</span></span> <span data-ttu-id="c66fc-151">Закрытый ключ хранится в файле id_rsa, а открытый — в файле id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="c66fc-151">The private key is stored in id_rsa and the public key in id_rsa.pub.</span></span>
   
   ![Открытые и закрытые ключи][keys]

### <a name="add-the-key-pair-to-the-hpc-pack-cluster"></a><span data-ttu-id="c66fc-153">Добавление пары ключей в кластер HPC</span><span class="sxs-lookup"><span data-stu-id="c66fc-153">Add the key pair to the HPC Pack cluster</span></span>
1. <span data-ttu-id="c66fc-154">Подключитесь к головному узлу через протокол удаленного рабочего стола, используя учетную запись администратора пакета HPC (учетная запись администратора, настроенная при запуске сценария развертывания).</span><span class="sxs-lookup"><span data-stu-id="c66fc-154">Make a Remote Desktop connection to your head node with your HPC Pack administrator account (the administrator account you set up when you ran the deployment script).</span></span>
2. <span data-ttu-id="c66fc-155">С помощью стандартных процедур Windows Server создайте учетную запись пользователя домена в домене Active Directory кластера.</span><span class="sxs-lookup"><span data-stu-id="c66fc-155">Use standard Windows Server procedures to create a domain user account in the cluster's Active Directory domain.</span></span> <span data-ttu-id="c66fc-156">Например, на головном узле можно использовать инструмент Active Directory «Пользователи и компьютеры».</span><span class="sxs-lookup"><span data-stu-id="c66fc-156">For example, use the Active Directory User and Computers tool on the head node.</span></span> <span data-ttu-id="c66fc-157">В приведенных здесь примерах предполагается, что вы создали пользователя домена с именем hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="c66fc-157">The examples in this article assume you create a domain user named hpclab\hpcuser.</span></span>
3. <span data-ttu-id="c66fc-158">Создайте файл с именем C:\cred.xml и скопируйте в него данные ключей RSA.</span><span class="sxs-lookup"><span data-stu-id="c66fc-158">Create a file named C:\cred.xml and copy the RSA key data into it.</span></span> <span data-ttu-id="c66fc-159">Пример файла cred.xml можно найти в конце этой статьи.</span><span class="sxs-lookup"><span data-stu-id="c66fc-159">A sample cred.xml file is at the end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy the contents of private key here</PrivateKey>
     <PublicKey>Copy the contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. <span data-ttu-id="c66fc-160">Откройте командную строку и введите следующую команду, чтобы задать учетные данные для учетной записи hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="c66fc-160">Open a Command Prompt and enter the following command to set the credentials data for the hpclab\hpcuser account.</span></span> <span data-ttu-id="c66fc-161">Используйте параметр **extendeddata**, чтобы передать имя файла C:\cred.xml, созданного для данных ключей.</span><span class="sxs-lookup"><span data-stu-id="c66fc-161">You use the **extendeddata** parameter to pass the name of C:\cred.xml file you created for the key data.</span></span>
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="c66fc-162">Эта команда успешно завершается без выходных данных.</span><span class="sxs-lookup"><span data-stu-id="c66fc-162">This command completes successfully without output.</span></span> <span data-ttu-id="c66fc-163">Задав учетные данные для учетных записей пользователей, необходимых для выполнения заданий, сохраните файл cred.xml в безопасном месте или удалите его.</span><span class="sxs-lookup"><span data-stu-id="c66fc-163">After setting the credentials for the user accounts you need to run jobs, store the cred.xml file in a secure location, or delete it.</span></span>
5. <span data-ttu-id="c66fc-164">Если вы создали пару ключей RSA на одном из узлов Linux, не забудьте удалить ключи после завершения работы с ними.</span><span class="sxs-lookup"><span data-stu-id="c66fc-164">If you generated the RSA key pair on one of your Linux nodes, remember to delete the keys after you finish using them.</span></span> <span data-ttu-id="c66fc-165">Пакет HPC не устанавливает взаимное доверие, если обнаруживает файл id_rsa или id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="c66fc-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c66fc-166">Мы не рекомендуем выполнять задания Linux от имени администратора кластера в общем кластере, так как задания, отправленные администратором, выполняются на узлах Linux под учетной записью root.</span><span class="sxs-lookup"><span data-stu-id="c66fc-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under the root account on the Linux nodes.</span></span> <span data-ttu-id="c66fc-167">Но задание, отправленное пользователем без прав администратора, выполняется под локальной учетной записью пользователя Linux с тем же именем, что и у пользователя задания.</span><span class="sxs-lookup"><span data-stu-id="c66fc-167">However, a job submitted by a non-administrator user runs under a local Linux user account with the same name as the job user.</span></span> <span data-ttu-id="c66fc-168">В таком случае пакет HPC устанавливает взаимное доверие для этого пользователя Linux на всех узлах, выделенных для выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="c66fc-168">In this case, HPC Pack sets up mutual trust for this Linux user across the nodes allocated to the job.</span></span> <span data-ttu-id="c66fc-169">Учетную запись пользователя Linux можно настроить вручную на узлах Linux перед выполнением задания, или пакет HPC автоматически создаст ее при отправке задания.</span><span class="sxs-lookup"><span data-stu-id="c66fc-169">You can set up the Linux user manually on the Linux nodes before running the job, or HPC Pack creates the user automatically when the job is submitted.</span></span> <span data-ttu-id="c66fc-170">Если учетную запись пользователя создает пакет HPC, она удаляется после завершения задания.</span><span class="sxs-lookup"><span data-stu-id="c66fc-170">If HPC Pack creates the user, HPC Pack deletes it after the job completes.</span></span> <span data-ttu-id="c66fc-171">Из соображений безопасности после завершения задания пакет HPC удаляет ключи.</span><span class="sxs-lookup"><span data-stu-id="c66fc-171">To reduce security threats, HPC Pack removes the keys after job completion.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="c66fc-172">Настройка файлового ресурса для узлов Linux</span><span class="sxs-lookup"><span data-stu-id="c66fc-172">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="c66fc-173">В папке на головном узле настройте стандартный общий ресурс SMB.</span><span class="sxs-lookup"><span data-stu-id="c66fc-173">Now set up a standard SMB share on a folder on the head node.</span></span> <span data-ttu-id="c66fc-174">Затем подключите его на узлах Linux, чтобы предоставить им доступ к файлам приложения по общему пути.</span><span class="sxs-lookup"><span data-stu-id="c66fc-174">To allow the Linux nodes to access application files with a common path, mount the shared folder on the Linux nodes.</span></span> <span data-ttu-id="c66fc-175">Вы можете также использовать другие параметры общего доступа, например общие файлы Azure (рекомендуется для большинства сценариев) или общие папки NFS.</span><span class="sxs-lookup"><span data-stu-id="c66fc-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span></span> <span data-ttu-id="c66fc-176">Подробные сведения о параметрах и этапах настройки общего доступа к файлам см. в статье [Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="c66fc-176">See the file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="c66fc-177">Создайте папку на головном узле и сделайте ее общедоступной для чтения и записи для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="c66fc-177">Create a folder on the head node, and share it to Everyone by setting Read/Write privileges.</span></span> <span data-ttu-id="c66fc-178">Например, откройте доступ к папке C:\OpenFOAM на головном узле как \\\\SUSE12RDMA-HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="c66fc-178">For example, share C:\OpenFOAM on the head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="c66fc-179">Здесь *SUSE12RDMA-HN* является именем головного узла.</span><span class="sxs-lookup"><span data-stu-id="c66fc-179">Here, *SUSE12RDMA-HN* is the host name of the head node.</span></span>
2. <span data-ttu-id="c66fc-180">Откройте окно Windows PowerShell и выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="c66fc-180">Open a Windows PowerShell window and run the following commands:</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

<span data-ttu-id="c66fc-181">Первая команда создает папку /openfoam на всех узлах в группе LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="c66fc-181">The first command creates a folder named /openfoam on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="c66fc-182">Вторая команда подключает общую папку //SUSE12RDMA-HN/OpenFOAM и задает для битов режимов dir_mode и file_mode на узлах Linux значение 777.</span><span class="sxs-lookup"><span data-stu-id="c66fc-182">The second command mounts the shared folder //SUSE12RDMA-HN/OpenFOAM on the Linux nodes with dir_mode and file_mode bits set to 777.</span></span> <span data-ttu-id="c66fc-183">Значения *username* и *password* должны соответствовать учетным данным пользователя на головном узле.</span><span class="sxs-lookup"><span data-stu-id="c66fc-183">The *username* and *password* in the command should be the credentials of a user on the head node.</span></span>

> [!NOTE]
> <span data-ttu-id="c66fc-184">Символ "\\`" во второй команде — это escape-символ для PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c66fc-184">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="c66fc-185">"\\`," означает, что "," (запятая) является частью команды.</span><span class="sxs-lookup"><span data-stu-id="c66fc-185">“\\`,” means the “,” (comma character) is a part of the command.</span></span>
> 
> 

## <a name="install-mpi-and-openfoam"></a><span data-ttu-id="c66fc-186">Установка пакетов MPI и OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="c66fc-186">Install MPI and OpenFOAM</span></span>
<span data-ttu-id="c66fc-187">Чтобы запустить OpenFOAM в виде задания MPI в сети RDMA, нужно скомпилировать пакет OpenFOAM с помощью библиотеки Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="c66fc-187">To run OpenFOAM as an MPI job on the RDMA network, you need to compile OpenFOAM with the Intel MPI libraries.</span></span> 

<span data-ttu-id="c66fc-188">Сначала следует выполнить несколько команд **clusrun** , чтобы установить библиотеки Intel MPI (если они не установлены) и OpenFOAM на узлы Linux.</span><span class="sxs-lookup"><span data-stu-id="c66fc-188">First, run several **clusrun** commands to install Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span></span> <span data-ttu-id="c66fc-189">Для доступа к файлам установки на разных узлах Linux используйте общий доступ к папке на головном узле.</span><span class="sxs-lookup"><span data-stu-id="c66fc-189">Use the head node share configured previously to share the installation files among the Linux nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c66fc-190">Приведенные действия по установке и компиляции являются примерами.</span><span class="sxs-lookup"><span data-stu-id="c66fc-190">These installation and compiling steps are examples.</span></span> <span data-ttu-id="c66fc-191">Для правильной установки зависимых компиляторов и библиотек требуются некоторые знания в сфере администрирования Linux.</span><span class="sxs-lookup"><span data-stu-id="c66fc-191">You need some knowledge of Linux system administration to ensure that dependent compilers and libraries are installed correctly.</span></span> <span data-ttu-id="c66fc-192">Возможно, в зависимости от версии Intel MPI и OpenFOAM вам потребуется изменить некоторые переменные среды или другие параметры.</span><span class="sxs-lookup"><span data-stu-id="c66fc-192">You might need to modify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="c66fc-193">Дополнительные сведения см. в разделах [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) (Руководство по установке библиотеки Intel MPI для Linux) и [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) (Установка исходного пакета OpenFOAM) для своей среды.</span><span class="sxs-lookup"><span data-stu-id="c66fc-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span></span>
> 
> 

### <a name="install-intel-mpi"></a><span data-ttu-id="c66fc-194">Установка пакета Intel MPI</span><span class="sxs-lookup"><span data-stu-id="c66fc-194">Install Intel MPI</span></span>
<span data-ttu-id="c66fc-195">Сохраните загруженный пакет установки библиотеки Intel MPI (в этом примере это файл l_mpi_p_5.0.3.048.tgz) в папку C:\OpenFoam на головном узле. Таким образом, другие узлы Linux получат доступ к этому файлу через /openfoam.</span><span class="sxs-lookup"><span data-stu-id="c66fc-195">Save the downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="c66fc-196">Затем запустите **clusrun**, чтобы установить библиотеку Intel MPI на всех узлах Linux.</span><span class="sxs-lookup"><span data-stu-id="c66fc-196">Then run **clusrun** to install Intel MPI library on all the Linux nodes.</span></span>

1. <span data-ttu-id="c66fc-197">Следующие команды копируют установочный пакет и извлекают его в расположение /opt/intel на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="c66fc-197">The following commands copy the installation package and extract it to /opt/intel on each node.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. <span data-ttu-id="c66fc-198">Для автоматической установки библиотеки Intel MPI используйте файл silent.cfg.</span><span class="sxs-lookup"><span data-stu-id="c66fc-198">To install Intel MPI Library silently, use a silent.cfg file.</span></span> <span data-ttu-id="c66fc-199">Пример можно найти в файлах примеров в конце этой статьи.</span><span class="sxs-lookup"><span data-stu-id="c66fc-199">You can find an example in the sample files at the end of this article.</span></span> <span data-ttu-id="c66fc-200">Поместите этот файл в общую папку /openfoam.</span><span class="sxs-lookup"><span data-stu-id="c66fc-200">Place this file in the shared folder /openfoam.</span></span> <span data-ttu-id="c66fc-201">Дополнительные сведения о файле silent.cfg см. в статье [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall) (Руководство по установке библиотеки Intel MPI для Linux. Автоматическая установка).</span><span class="sxs-lookup"><span data-stu-id="c66fc-201">For details about the silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="c66fc-202">Сохраните файл silent.cfg как текстовый файл, в котором для завершения строк используется нотация Linux (только LF, а не CR LF).</span><span class="sxs-lookup"><span data-stu-id="c66fc-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="c66fc-203">Это гарантирует, что файл будет правильно работать на узлах Linux.</span><span class="sxs-lookup"><span data-stu-id="c66fc-203">This step ensures that it runs properly on the Linux nodes.</span></span>
   > 
   > 
3. <span data-ttu-id="c66fc-204">Установка библиотеки Intel MPI в автоматическом режиме.</span><span class="sxs-lookup"><span data-stu-id="c66fc-204">Install Intel MPI Library in silent mode.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a><span data-ttu-id="c66fc-205">Настройка MPI</span><span class="sxs-lookup"><span data-stu-id="c66fc-205">Configure MPI</span></span>
<span data-ttu-id="c66fc-206">Для тестирования вам следует добавить следующие строки в файл /etc/security/limits.conf на каждом из узлов Linux:</span><span class="sxs-lookup"><span data-stu-id="c66fc-206">For testing, you should add the following lines to the /etc/security/limits.conf on each of the Linux nodes:</span></span>

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


<span data-ttu-id="c66fc-207">После обновления файла limits.conf перезапустите узлы Linux.</span><span class="sxs-lookup"><span data-stu-id="c66fc-207">Restart the Linux nodes after you update the limits.conf file.</span></span> <span data-ttu-id="c66fc-208">Например, используйте следующую команду **clusrun** :</span><span class="sxs-lookup"><span data-stu-id="c66fc-208">For example, use the following **clusrun** command:</span></span>

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

<span data-ttu-id="c66fc-209">После перезапуска убедитесь, что общая папка доступна по адресу /openfoam.</span><span class="sxs-lookup"><span data-stu-id="c66fc-209">After restarting, ensure that the shared folder is mounted as /openfoam.</span></span>

### <a name="compile-and-install-openfoam"></a><span data-ttu-id="c66fc-210">Компиляция и установка OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="c66fc-210">Compile and install OpenFOAM</span></span>
<span data-ttu-id="c66fc-211">Сохраните загруженный исходный пакет OpenFOAM (в этом примере это файл OpenFOAM-2.3.1.tgz) в папку C:\OpenFoam на головном узле. Таким образом другие узлы Linux получат доступ к этому файлу через /openfoam.</span><span class="sxs-lookup"><span data-stu-id="c66fc-211">Save the downloaded installation package for the OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) to C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="c66fc-212">Затем выполните команды **clusrun**, чтобы скомпилировать OpenFOAM на всех узлах Linux.</span><span class="sxs-lookup"><span data-stu-id="c66fc-212">Then run **clusrun** commands to compile OpenFOAM on all the Linux nodes.</span></span>

1. <span data-ttu-id="c66fc-213">Создайте папку /opt/OpenFOAM на каждом узле Linux. Затем скопируйте в эту папку исходный пакет и распакуйте его.</span><span class="sxs-lookup"><span data-stu-id="c66fc-213">Create a folder /opt/OpenFOAM on each Linux node, copy the source package to this folder, and extract it there.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. <span data-ttu-id="c66fc-214">Чтобы скомпилировать OpenFOAM с помощью библиотеки Intel MPI, сначала потребуется настроить некоторые переменные среды для Intel MPI и OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="c66fc-214">To compile OpenFOAM with the Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="c66fc-215">Для этого используйте скрипт bash с именем settings.sh.</span><span class="sxs-lookup"><span data-stu-id="c66fc-215">Use a bash script called settings.sh to set the variables.</span></span> <span data-ttu-id="c66fc-216">Пример можно найти в файлах примеров в конце этой статьи.</span><span class="sxs-lookup"><span data-stu-id="c66fc-216">You can find an example in the sample files at the end of this article.</span></span> <span data-ttu-id="c66fc-217">Поместите этот файл (сохраненный с нотацией Linux для завершения строк) в общую папку /openfoam.</span><span class="sxs-lookup"><span data-stu-id="c66fc-217">Place this file (saved with Linux line endings) in the shared folder /openfoam.</span></span> <span data-ttu-id="c66fc-218">Этот файл также содержит параметры для сред выполнения MPI и OpenFOAM, которые впоследствии будут использованы для выполнения задания OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="c66fc-218">This file also contains settings for the MPI and OpenFOAM runtimes that you use later to run an OpenFOAM job.</span></span>
3. <span data-ttu-id="c66fc-219">Установите зависимые пакеты, необходимые для компиляции OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="c66fc-219">Install dependent packages needed to compile OpenFOAM.</span></span> <span data-ttu-id="c66fc-220">В зависимости от дистрибутива Linux вам может потребоваться сначала добавить репозиторий.</span><span class="sxs-lookup"><span data-stu-id="c66fc-220">Depending on your Linux distribution, you might first need to add a repository.</span></span> <span data-ttu-id="c66fc-221">Выполните команду **clusrun** , аналогичную следующей:</span><span class="sxs-lookup"><span data-stu-id="c66fc-221">Run **clusrun** commands similar to the following:</span></span>
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    <span data-ttu-id="c66fc-222">Для надлежащего выполнения команд подключайтесь к каждому узлу Linux по SSH, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="c66fc-222">If necessary, SSH to each Linux node to run the commands to confirm that they run properly.</span></span>
4. <span data-ttu-id="c66fc-223">Чтобы скомпилировать OpenFOAM, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c66fc-223">Run the following command to compile OpenFOAM.</span></span> <span data-ttu-id="c66fc-224">Процесс компиляции займет некоторое время. Выходных данных достаточно много, поэтому используйте ключ **/interleaved**, чтобы отображать их с чередованием.</span><span class="sxs-lookup"><span data-stu-id="c66fc-224">The compilation process takes some time to complete and generates a large amount of log information to standard output, so use the **/interleaved** option to display the output interleaved.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > <span data-ttu-id="c66fc-225">Символ "\\`" в команде — это escape-символ для PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c66fc-225">The “\\`” symbol in the command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="c66fc-226">"\\`&" означает, что "&" является частью команды.</span><span class="sxs-lookup"><span data-stu-id="c66fc-226">“\\`&” means the “&” is a part of the command.</span></span>
   > 
   > 

## <a name="prepare-to-run-an-openfoam-job"></a><span data-ttu-id="c66fc-227">Подготовка к запуску задания OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="c66fc-227">Prepare to run an OpenFOAM job</span></span>
<span data-ttu-id="c66fc-228">Теперь попробуем запустить задание MPI с названием sloshingTank3D (пример из пакета OpenFoam) на двух узлах Linux.</span><span class="sxs-lookup"><span data-stu-id="c66fc-228">Now get ready to run an MPI job called sloshingTank3D, which is one of the OpenFoam samples, on two Linux nodes.</span></span> 

### <a name="set-up-the-runtime-environment"></a><span data-ttu-id="c66fc-229">Настройка среды выполнения</span><span class="sxs-lookup"><span data-stu-id="c66fc-229">Set up the runtime environment</span></span>
<span data-ttu-id="c66fc-230">На головном узле откройте Windows PowerShell и запустите следующую команду, чтобы настроить среду выполнения MPI и OpenFOAM на узлах Linux.</span><span class="sxs-lookup"><span data-stu-id="c66fc-230">To set up the runtime environments for MPI and OpenFOAM on the Linux nodes, run the following command in a Windows PowerShell window on the head node.</span></span> <span data-ttu-id="c66fc-231">(Эта команда допустима только для SUSE Linux.)</span><span class="sxs-lookup"><span data-stu-id="c66fc-231">(This command is valid for SUSE Linux only.)</span></span>

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a><span data-ttu-id="c66fc-232">Подготовка примера данных</span><span class="sxs-lookup"><span data-stu-id="c66fc-232">Prepare sample data</span></span>
<span data-ttu-id="c66fc-233">Чтобы открыть доступ к файлам с других узлов Linux, используйте ранее настроенную папку общего доступа (подключается как /openfoam).</span><span class="sxs-lookup"><span data-stu-id="c66fc-233">Use the head node share you configured previously to share files among the Linux nodes (mounted as /openfoam).</span></span>

1. <span data-ttu-id="c66fc-234">Выполните подключение к одному из вычислительных узлов Linux по SSH.</span><span class="sxs-lookup"><span data-stu-id="c66fc-234">SSH to one of your Linux compute nodes.</span></span>
2. <span data-ttu-id="c66fc-235">Если это еще не сделано, запустите следующую команду, чтобы настроить среду выполнения OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="c66fc-235">Run the following command to set up the OpenFOAM runtime environment, if you haven’t already done this.</span></span>
   
   ```
   $ source /openfoam/settings.sh
   ```
3. <span data-ttu-id="c66fc-236">Скопируйте пример sloshingTank3D в общую папку и перейдите к нему.</span><span class="sxs-lookup"><span data-stu-id="c66fc-236">Copy the sloshingTank3D sample to the shared folder and navigate to it.</span></span>
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. <span data-ttu-id="c66fc-237">Если вы используете стандартные параметры, представленные в этом примере, выполнение может занять несколько десятков минут. Поэтому для ускорения выполнения можно изменить некоторые параметры.</span><span class="sxs-lookup"><span data-stu-id="c66fc-237">When you use the default parameters of this sample, it can take tens of minutes to run, so you might want to modify some parameters to make it run faster.</span></span> <span data-ttu-id="c66fc-238">Простым решением является изменение переменных интервала времени deltaT и writeInterval в файле system/controlDict.</span><span class="sxs-lookup"><span data-stu-id="c66fc-238">One simple choice is to modify the time step variables deltaT and writeInterval in the system/controlDict file.</span></span> <span data-ttu-id="c66fc-239">Этот файл хранит все входные данные, связанные с управлением временем, чтением и записью данных в решении.</span><span class="sxs-lookup"><span data-stu-id="c66fc-239">This file stores all input data relating to the control of time and reading and writing solution data.</span></span> <span data-ttu-id="c66fc-240">Например, значение deltaT можно изменить с 0,05 на 0,5, а значение writeInterval — с 0,05 на 0,5.</span><span class="sxs-lookup"><span data-stu-id="c66fc-240">For example, you could change the value of deltaT from 0.05 to 0.5 and the value of writeInterval from 0.05 to 0.5.</span></span>
   
   ![Изменение переменных шага][step_variables]
5. <span data-ttu-id="c66fc-242">Укажите нужные значения переменных в файле system/decomposeParDict.</span><span class="sxs-lookup"><span data-stu-id="c66fc-242">Specify desired values for the variables in the system/decomposeParDict file.</span></span> <span data-ttu-id="c66fc-243">В этом примере используется 2 узла Linux с 8 ядрами, поэтому присвойте параметру numberOfSubdomains значение 16, а параметру n hierarchicalCoeffs — (1 1 16), что означает выполнение задания OpenFOAM с созданием 16 параллельных процессов.</span><span class="sxs-lookup"><span data-stu-id="c66fc-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains to 16 and n of hierarchicalCoeffs to (1 1 16), which means run OpenFOAM in parallel with 16 processes.</span></span> <span data-ttu-id="c66fc-244">Дополнительные сведения см. в статье [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4) (Руководство пользователя OpenFOAM. 3.4. Запуск приложений в параллельном режиме).</span><span class="sxs-lookup"><span data-stu-id="c66fc-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span></span>
   
   ![Разделение процессов][decompose]
6. <span data-ttu-id="c66fc-246">Выполните следующие команды из каталога sloshingTank3D, чтобы подготовить пример данных.</span><span class="sxs-lookup"><span data-stu-id="c66fc-246">Run the following commands from the sloshingTank3D directory to prepare the sample data.</span></span>
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. <span data-ttu-id="c66fc-247">На головном узле вы увидите, что файлы с примерами данных копируются в папку C:\OpenFoam\sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="c66fc-247">On the head node, you should see the sample data files are copied into C:\OpenFoam\sloshingTank3D.</span></span> <span data-ttu-id="c66fc-248">(C:\OpenFoam — это общая папка на головном узле).</span><span class="sxs-lookup"><span data-stu-id="c66fc-248">(C:\OpenFoam is the shared folder on the head node.)</span></span>
   
   ![Файлы данных на головном узле][data_files]

### <a name="host-file-for-mpirun"></a><span data-ttu-id="c66fc-250">Файл узлов для mpirun</span><span class="sxs-lookup"><span data-stu-id="c66fc-250">Host file for mpirun</span></span>
<span data-ttu-id="c66fc-251">На этом шаге вы создадите файл узлов (список вычислительных узлов), который будет использовать команда **mpirun** .</span><span class="sxs-lookup"><span data-stu-id="c66fc-251">In this step, you create a host file (a list of compute nodes) which the **mpirun** command uses.</span></span>

1. <span data-ttu-id="c66fc-252">На одном из узлов Linux создайте файл с именем hostfile и поместите его в папку /openfoam. В результате к нему будет открыт доступ с каждого узла Linux (в расположении /openfoam/hostfile).</span><span class="sxs-lookup"><span data-stu-id="c66fc-252">On one of the Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span></span>
2. <span data-ttu-id="c66fc-253">В этом файле укажите имена ваших узлов Linux.</span><span class="sxs-lookup"><span data-stu-id="c66fc-253">Write your Linux node names into this file.</span></span> <span data-ttu-id="c66fc-254">В этом примере файл содержит следующие имена:</span><span class="sxs-lookup"><span data-stu-id="c66fc-254">In this example, the file contains the following names:</span></span>
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > <span data-ttu-id="c66fc-255">Также вы можете создать этот файл в каталоге C:\OpenFoam\hostfile на головном узле.</span><span class="sxs-lookup"><span data-stu-id="c66fc-255">You can also create this file at C:\OpenFoam\hostfile on the head node.</span></span> <span data-ttu-id="c66fc-256">В таком случае сохраните его в виде текстового файла с нотацией Linux для завершения строк (только LF, а не CR LF).</span><span class="sxs-lookup"><span data-stu-id="c66fc-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="c66fc-257">Это гарантирует, что файл будет правильно работать на узлах Linux.</span><span class="sxs-lookup"><span data-stu-id="c66fc-257">This ensures that it runs properly on the Linux nodes.</span></span>
   > 
   > 
   
   <span data-ttu-id="c66fc-258">**Оболочка сценария bash**</span><span class="sxs-lookup"><span data-stu-id="c66fc-258">**Bash script wrapper**</span></span>
   
   <span data-ttu-id="c66fc-259">Если у вас есть несколько узлов Linux, а задания нужно выполнять только на некоторых из них, использовать фиксированный файл узлов не рекомендуется, так как вы не будете знать, какие узлы будут выделены для выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="c66fc-259">If you have many Linux nodes and you want your job to run on only some of them, it’s not a good idea to use a fixed host file, because you don’t know which nodes will be allocated to your job.</span></span> <span data-ttu-id="c66fc-260">В этом случае можно создать оболочку для сценария bash, которая будет использоваться командой **mpirun** для автоматического создания файла узлов.</span><span class="sxs-lookup"><span data-stu-id="c66fc-260">In this case, write a bash script wrapper for **mpirun** to create the host file automatically.</span></span> <span data-ttu-id="c66fc-261">Пример оболочки для скрипта bash можно найти в файле hpcimpirun.sh, приведенном в конце этой статьи. Сохраните этот файл в расположении /openfoam/hpcimpirun.sh.</span><span class="sxs-lookup"><span data-stu-id="c66fc-261">You can find an example bash script wrapper called hpcimpirun.sh at the end of this article, and save it as /openfoam/hpcimpirun.sh.</span></span> <span data-ttu-id="c66fc-262">Этот пример сценария выполняет следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c66fc-262">This example script does the following:</span></span>
   
   1. <span data-ttu-id="c66fc-263">Используя сеть RDMA, устанавливает переменные среды для команды **mpirun**и некоторые дополнительные параметры для выполнения заданий MPI.</span><span class="sxs-lookup"><span data-stu-id="c66fc-263">Sets up the environment variables for **mpirun**, and some addition command parameters to run the MPI job through the RDMA network.</span></span> <span data-ttu-id="c66fc-264">В данном примере устанавливаются следующие переменные:</span><span class="sxs-lookup"><span data-stu-id="c66fc-264">In this case, it sets the following variables:</span></span>
      
      * <span data-ttu-id="c66fc-265">I_MPI_FABRICS=shm:dapl</span><span class="sxs-lookup"><span data-stu-id="c66fc-265">I_MPI_FABRICS=shm:dapl</span></span>
      * <span data-ttu-id="c66fc-266">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span><span class="sxs-lookup"><span data-stu-id="c66fc-266">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span></span>
      * <span data-ttu-id="c66fc-267">I_MPI_DYNAMIC_CONNECTION=0</span><span class="sxs-lookup"><span data-stu-id="c66fc-267">I_MPI_DYNAMIC_CONNECTION=0</span></span>
   2. <span data-ttu-id="c66fc-268">Создает файл узлов в соответствии с переменной среды $CCP_NODES_CORES. Значение этой переменной устанавливается головным узлом HPC при активации задания.</span><span class="sxs-lookup"><span data-stu-id="c66fc-268">Creates a host file according to the environment variable $CCP_NODES_CORES, which is set by the HPC head node when the job is activated.</span></span>
      
      <span data-ttu-id="c66fc-269">Формат $CCP_NODES_CORES соответствует следующему шаблону:</span><span class="sxs-lookup"><span data-stu-id="c66fc-269">The format of $CCP_NODES_CORES follows this pattern:</span></span>
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      <span data-ttu-id="c66fc-270">где:</span><span class="sxs-lookup"><span data-stu-id="c66fc-270">where</span></span>
      
      * <span data-ttu-id="c66fc-271">`<Number of nodes>` : количество узлов, выделенных для этого задания.</span><span class="sxs-lookup"><span data-stu-id="c66fc-271">`<Number of nodes>` - the number of nodes allocated to this job.</span></span>  
      * <span data-ttu-id="c66fc-272">`<Name of node_n_...>` : имя каждого узла, выделенного для этого задания.</span><span class="sxs-lookup"><span data-stu-id="c66fc-272">`<Name of node_n_...>` - the name of each node allocated to this job.</span></span>
      * <span data-ttu-id="c66fc-273">`<Cores of node_n_...>`: количество ядер каждого узла, выделенного для этого задания.</span><span class="sxs-lookup"><span data-stu-id="c66fc-273">`<Cores of node_n_...>` - the number of cores on the node allocated to this job.</span></span>
      
      <span data-ttu-id="c66fc-274">Например, если для выполнения задания требуется 2 узла, значение $CCP_NODES_CORES будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c66fc-274">For example, if the job needs two nodes to run, $CCP_NODES_CORES is similar to</span></span>
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. <span data-ttu-id="c66fc-275">Вызывает команду **mpirun** и добавляет 2 параметра командной строки.</span><span class="sxs-lookup"><span data-stu-id="c66fc-275">Calls the **mpirun** command and appends two parameters to the command line.</span></span>
      
      * <span data-ttu-id="c66fc-276">`--hostfile <hostfilepath>: <hostfilepath>` : путь к файлу узлов, который будет создан сценарием</span><span class="sxs-lookup"><span data-stu-id="c66fc-276">`--hostfile <hostfilepath>: <hostfilepath>` - the path of the host file the script creates</span></span>
      * <span data-ttu-id="c66fc-277">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`: переменная среды, задаваемая головным узлом пакета HPC. Хранит общее количество ядер, выделенных для этого задания.</span><span class="sxs-lookup"><span data-stu-id="c66fc-277">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by the HPC Pack head node, which stores the number of total cores allocated to this job.</span></span> <span data-ttu-id="c66fc-278">В этом случае указывается количество процессов для команды **mpirun**.</span><span class="sxs-lookup"><span data-stu-id="c66fc-278">In this case, it specifies the number of processes for **mpirun**.</span></span>

## <a name="submit-an-openfoam-job"></a><span data-ttu-id="c66fc-279">Отправка задания OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="c66fc-279">Submit an OpenFOAM job</span></span>
<span data-ttu-id="c66fc-280">Теперь вы можете отправить задание из диспетчера кластера HPC.</span><span class="sxs-lookup"><span data-stu-id="c66fc-280">Now you can submit a job in HPC Cluster Manager.</span></span> <span data-ttu-id="c66fc-281">Для некоторых задач вам потребуется указать в командной строке скрипт hpcimpirun.sh.</span><span class="sxs-lookup"><span data-stu-id="c66fc-281">You need to pass the script hpcimpirun.sh in the command lines for some of the job tasks.</span></span>

1. <span data-ttu-id="c66fc-282">Подключитесь к головному узлу кластера и запустите диспетчер кластера HPC.</span><span class="sxs-lookup"><span data-stu-id="c66fc-282">Connect to your cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="c66fc-283">Убедитесь, что в разделе **Управление ресурсами** для вычислительных узлов Linux отображается состояние **В сети**.</span><span class="sxs-lookup"><span data-stu-id="c66fc-283">**In Resource Management**, ensure that the Linux compute nodes are in the **Online** state.</span></span> <span data-ttu-id="c66fc-284">Если это не так, выберите их и щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="c66fc-284">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="c66fc-285">В разделе **Управление заданиями** щелкните **Новое задание**.</span><span class="sxs-lookup"><span data-stu-id="c66fc-285">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="c66fc-286">Введите имя задания, например *sloshingTank3D*.</span><span class="sxs-lookup"><span data-stu-id="c66fc-286">Enter a name for job such as *sloshingTank3D*.</span></span>
   
   ![Сведения о задании][job_details]
5. <span data-ttu-id="c66fc-288">На странице **Ресурсы задания**выберите тип ресурса "Узел" и задайте для параметра "Минимум" значение 2.</span><span class="sxs-lookup"><span data-stu-id="c66fc-288">In **Job resources**, choose the type of resource as “Node” and set the Minimum to 2.</span></span> <span data-ttu-id="c66fc-289">При такой конфигурации задания будут выполняться на двух узлах Linux, каждый из которых имеет по восемь ядер.</span><span class="sxs-lookup"><span data-stu-id="c66fc-289">This configuration runs the job on two Linux nodes, each of which has eight cores in this example.</span></span>
   
   ![Ресурсы задания][job_resources]
6. <span data-ttu-id="c66fc-291">Щелкните **Изменение задач** в левой области навигации, а затем — **Добавить**, чтобы добавить задачу в задание.</span><span class="sxs-lookup"><span data-stu-id="c66fc-291">Click **Edit Tasks** in the left navigation, and then click **Add** to add a task to the job.</span></span> <span data-ttu-id="c66fc-292">Добавьте 4 задачи к заданию, используя следующие команды и параметры.</span><span class="sxs-lookup"><span data-stu-id="c66fc-292">Add four tasks to the job with the following command lines and settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c66fc-293">Выполнение команды `source /openfoam/settings.sh` настраивает среды выполнения OpenFOAM и MPI, поэтому каждая из задач вызывает ее перед командой OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="c66fc-293">Running `source /openfoam/settings.sh` sets up the OpenFOAM and MPI runtime environments, so each of the following tasks calls it before the OpenFOAM command.</span></span>
   > 
   > 
   
   * <span data-ttu-id="c66fc-294">**Задача 1**.</span><span class="sxs-lookup"><span data-stu-id="c66fc-294">**Task 1**.</span></span> <span data-ttu-id="c66fc-295">Запуск **decomposePar** для создания файла данных для параллельного запуска **interDyMFoam**.</span><span class="sxs-lookup"><span data-stu-id="c66fc-295">Run **decomposePar** to generate data files for running **interDyMFoam** in parallel.</span></span>
     
     * <span data-ttu-id="c66fc-296">Назначьте этой задаче 1 узел.</span><span class="sxs-lookup"><span data-stu-id="c66fc-296">Assign one node to the task</span></span>
     * <span data-ttu-id="c66fc-297">**Командная строка** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="c66fc-297">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="c66fc-298">**Рабочий каталог** — /openfoam/sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="c66fc-298">**Working directory** - /openfoam/sloshingTank3D</span></span>
     
     <span data-ttu-id="c66fc-299">См. следующий рисунок.</span><span class="sxs-lookup"><span data-stu-id="c66fc-299">See the following figure.</span></span> <span data-ttu-id="c66fc-300">Остальные задачи настраиваются аналогичным образом.</span><span class="sxs-lookup"><span data-stu-id="c66fc-300">You configure the remaining tasks similarly.</span></span>
     
     ![Сведения о задаче 1][task_details1]
   * <span data-ttu-id="c66fc-302">**Задача 2**.</span><span class="sxs-lookup"><span data-stu-id="c66fc-302">**Task 2**.</span></span> <span data-ttu-id="c66fc-303">Запуск **interDyMFoam** в параллельном режиме для выполнения расчета на основании примера данных.</span><span class="sxs-lookup"><span data-stu-id="c66fc-303">Run **interDyMFoam** in parallel to compute the sample.</span></span>
     
     * <span data-ttu-id="c66fc-304">Назначьте этой задаче 2 узла.</span><span class="sxs-lookup"><span data-stu-id="c66fc-304">Assign two nodes to the task</span></span>
     * <span data-ttu-id="c66fc-305">**Командная строка** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="c66fc-305">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="c66fc-306">**Рабочий каталог** — /openfoam/sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="c66fc-306">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="c66fc-307">**Задача 3**.</span><span class="sxs-lookup"><span data-stu-id="c66fc-307">**Task 3**.</span></span> <span data-ttu-id="c66fc-308">Запуск **reconstructPar** для слияния наборов каталогов времени из каждого каталога processor_N_ в общий набор.</span><span class="sxs-lookup"><span data-stu-id="c66fc-308">Run **reconstructPar** to merge the sets of time directories from each processor_N_ directory into a single set.</span></span>
     
     * <span data-ttu-id="c66fc-309">Назначьте этой задаче 1 узел.</span><span class="sxs-lookup"><span data-stu-id="c66fc-309">Assign one node to the task</span></span>
     * <span data-ttu-id="c66fc-310">**Командная строка** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="c66fc-310">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="c66fc-311">**Рабочий каталог** — /openfoam/sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="c66fc-311">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="c66fc-312">**Задача 4**.</span><span class="sxs-lookup"><span data-stu-id="c66fc-312">**Task 4**.</span></span> <span data-ttu-id="c66fc-313">Запуск **foamToEnsight** в параллельном режиме для преобразования выходных файлов OpenFOAM в формат EnSight. Преобразованные файлы помещаются в папку Ensight учебного каталога.</span><span class="sxs-lookup"><span data-stu-id="c66fc-313">Run **foamToEnsight** in parallel to convert the OpenFOAM result files into EnSight format and place the EnSight files in a directory named Ensight in the case directory.</span></span>
     
     * <span data-ttu-id="c66fc-314">Назначьте этой задаче 2 узла.</span><span class="sxs-lookup"><span data-stu-id="c66fc-314">Assign two nodes to the task</span></span>
     * <span data-ttu-id="c66fc-315">**Командная строка** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="c66fc-315">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="c66fc-316">**Рабочий каталог** — /openfoam/sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="c66fc-316">**Working directory** - /openfoam/sloshingTank3D</span></span>
7. <span data-ttu-id="c66fc-317">Добавьте зависимости этих задач в возрастающем порядке.</span><span class="sxs-lookup"><span data-stu-id="c66fc-317">Add dependencies to these tasks in ascending task order.</span></span>
   
   ![Зависимости задачи][task_dependencies]
8. <span data-ttu-id="c66fc-319">Щелкните **Отправить** , чтобы выполнить это задание.</span><span class="sxs-lookup"><span data-stu-id="c66fc-319">Click **Submit** to run this job.</span></span>
   
   <span data-ttu-id="c66fc-320">По умолчанию пакет HPC отправляет задание от имени текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="c66fc-320">By default, HPC Pack submits the job as your current logged-on user account.</span></span> <span data-ttu-id="c66fc-321">После нажатия кнопки **Отправить**может появиться диалоговое окно с запросом на ввод имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="c66fc-321">After you click **Submit**, you might see a dialog box prompting you to enter the user name and password.</span></span>
   
   ![Учетные данные для задания][creds]
   
   <span data-ttu-id="c66fc-323">При некоторых обстоятельствах пакет HPC запоминает введенные ранее сведения о пользователе, и это диалоговое окно не появляется.</span><span class="sxs-lookup"><span data-stu-id="c66fc-323">Under some conditions, HPC Pack remembers the user information you input before and doesn’t show this dialog box.</span></span> <span data-ttu-id="c66fc-324">Чтобы пакет HPC отобразил его снова, введите в командной строке указанную ниже команду, а затем отправьте задание.</span><span class="sxs-lookup"><span data-stu-id="c66fc-324">To make HPC Pack show it again, enter the following command at a Command prompt and then submit the job.</span></span>
   
   ```
   hpccred delcreds
   ```
9. <span data-ttu-id="c66fc-325">Выполнение задания занимает от нескольких десятков минут до нескольких часов в зависимости от заданных параметров.</span><span class="sxs-lookup"><span data-stu-id="c66fc-325">The job takes from tens of minutes to several hours according to the parameters you have set for the sample.</span></span> <span data-ttu-id="c66fc-326">На тепловой карте вы увидите, что задание выполняется на узлах Linux.</span><span class="sxs-lookup"><span data-stu-id="c66fc-326">In the heat map, you see the job running on the Linux nodes.</span></span> 
   
   ![Тепловая карта][heat_map]
   
   <span data-ttu-id="c66fc-328">На каждом узле запускается 8 процессов.</span><span class="sxs-lookup"><span data-stu-id="c66fc-328">On each node, eight processes are started.</span></span>
   
   ![Процессы Linux][linux_processes]
10. <span data-ttu-id="c66fc-330">После завершения задания результаты можно будет найти в папке C:\OpenFoam\sloshingTank3D, а файлы журнала — в папке C:\OpenFoam.</span><span class="sxs-lookup"><span data-stu-id="c66fc-330">When the job finishes, find the job results in folders under C:\OpenFoam\sloshingTank3D, and the log files at C:\OpenFoam.</span></span>

## <a name="view-results-in-ensight"></a><span data-ttu-id="c66fc-331">Просмотр результатов в EnSight</span><span class="sxs-lookup"><span data-stu-id="c66fc-331">View results in EnSight</span></span>
<span data-ttu-id="c66fc-332">Для отображения и анализа результатов заданий OpenFOAM можно использовать [EnSight](https://www.ceisoftware.com/).</span><span class="sxs-lookup"><span data-stu-id="c66fc-332">Optionally use [EnSight](https://www.ceisoftware.com/) to visualize and analyze the results of the OpenFOAM job.</span></span> <span data-ttu-id="c66fc-333">Дополнительные сведения о визуализации и анимации в EnSight см. в этом [видеоролике](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span><span class="sxs-lookup"><span data-stu-id="c66fc-333">For more about visualization and animation in EnSight, see this [video guide](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span></span>

1. <span data-ttu-id="c66fc-334">Установив программное обеспечение EnSight на головном узле, запустите его.</span><span class="sxs-lookup"><span data-stu-id="c66fc-334">After you install EnSight on the head node, start it.</span></span>
2. <span data-ttu-id="c66fc-335">Откройте файл C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span><span class="sxs-lookup"><span data-stu-id="c66fc-335">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span></span>
   
   <span data-ttu-id="c66fc-336">В окне просмотра вы увидите резервуар.</span><span class="sxs-lookup"><span data-stu-id="c66fc-336">You see a tank in the viewer.</span></span>
   
   ![Резервуар в EnSight][tank]
3. <span data-ttu-id="c66fc-338">Создайте объект **Isosurface** из **internalMesh** и выберите переменную **alpha_water**.</span><span class="sxs-lookup"><span data-stu-id="c66fc-338">Create an **Isosurface** from **internalMesh**, and then choose the variable **alpha_water**.</span></span>
   
   ![Создание isosurface][isosurface]
4. <span data-ttu-id="c66fc-340">Задайте цвет для части **Isosurface_part**, созданной на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="c66fc-340">Set the color for **Isosurface_part** created in the previous step.</span></span> <span data-ttu-id="c66fc-341">Например, выберите голубой цвет.</span><span class="sxs-lookup"><span data-stu-id="c66fc-341">For example, set it to water blue.</span></span>
   
   ![Изменение цвета isosurface][isosurface_color]
5. <span data-ttu-id="c66fc-343">Создайте объект **Iso-volume** из коллекции **стен**. Для этого на панели **Parts** (Части) выберите **Walls** (Стены) и нажмите кнопку **Isosurfaces** (Изоповерхности).</span><span class="sxs-lookup"><span data-stu-id="c66fc-343">Create an **Iso-volume** from **walls** by selecting **walls** in the **Parts** panel and click the **Isosurfaces** button in the toolbar.</span></span>
6. <span data-ttu-id="c66fc-344">В диалоговом окне в поле **Type** (Тип) выберите **Isovolume** (Изообъем) и для диапазона **Isovolume range** (Диапазон изообъема) задайте минимальное значение 0,5.</span><span class="sxs-lookup"><span data-stu-id="c66fc-344">In the dialog box, select **Type** as **Isovolume** and set the Min of **Isovolume range** to 0.5.</span></span> <span data-ttu-id="c66fc-345">Щелкните **Create with selected parts**(Создать с помощью выделенных частей), чтобы создать объект Isovolume.</span><span class="sxs-lookup"><span data-stu-id="c66fc-345">To create the isovolume, click **Create with selected parts**.</span></span>
7. <span data-ttu-id="c66fc-346">Задайте цвет для части **Iso_volume_part**, созданной на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="c66fc-346">Set the color for **Iso_volume_part** created in the previous step.</span></span> <span data-ttu-id="c66fc-347">Например, выберите темно-синий цвет.</span><span class="sxs-lookup"><span data-stu-id="c66fc-347">For example, set it to deep water blue.</span></span>
8. <span data-ttu-id="c66fc-348">Выберите цвет для **стен**.</span><span class="sxs-lookup"><span data-stu-id="c66fc-348">Set the color for **walls**.</span></span> <span data-ttu-id="c66fc-349">Например, выберите прозрачный белый.</span><span class="sxs-lookup"><span data-stu-id="c66fc-349">For example, set it to transparent white.</span></span>
9. <span data-ttu-id="c66fc-350">Теперь щелкните **Play** (Воспроизведение), чтобы увидеть результаты моделирования.</span><span class="sxs-lookup"><span data-stu-id="c66fc-350">Now click **Play** to see the results of the simulation.</span></span>
   
    ![Результат для резервуара][tank_result]

## <a name="sample-files"></a><span data-ttu-id="c66fc-352">Файлы с примерами</span><span class="sxs-lookup"><span data-stu-id="c66fc-352">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="c66fc-353">Пример XML-файла конфигурации для развертывания кластера с помощью скрипта PowerShell</span><span class="sxs-lookup"><span data-stu-id="c66fc-353">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
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

### <a name="sample-credxml-file"></a><span data-ttu-id="c66fc-354">Пример файла cred.xml</span><span class="sxs-lookup"><span data-stu-id="c66fc-354">Sample cred.xml file</span></span>
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
### <a name="sample-silentcfg-file-to-install-mpi"></a><span data-ttu-id="c66fc-355">Пример файла silent.cfg для установки MPI</span><span class="sxs-lookup"><span data-stu-id="c66fc-355">Sample silent.cfg file to install MPI</span></span>
```
# Patterns used to check silent configuration file
#
# anythingpat - any string
# filepat     - the file location pattern (/file/location/to/license.lic)
# lspat       - the license server address pattern (0123@hostname)
# snpat       - the serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components to install, valid values are: {ALL, DEFAULTS, anythingpat}
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

# Path to the cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes to enable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes to update ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a><span data-ttu-id="c66fc-356">Пример сценария settings.sh</span><span class="sxs-lookup"><span data-stu-id="c66fc-356">Sample settings.sh script</span></span>
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


### <a name="sample-hpcimpirunsh-script"></a><span data-ttu-id="c66fc-357">Пример сценария hpcimpirun.sh</span><span class="sxs-lookup"><span data-stu-id="c66fc-357">Sample hpcimpirun.sh script</span></span>
```
#!/bin/bash

# The path of this script
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
    # CCP_NODES_CORES is not found or is empty, just run the mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create the hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into the hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run the mpirun with hostfile arg
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
