---
title: "NAMD с пакетом Microsoft HPC на виртуальных машинах Linux | Документация Майкрософт"
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
ms.openlocfilehash: e31845f3d7aa08357b0e8a1b3b77d97302442ac3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a><span data-ttu-id="48e7f-103">Запуск NAMD с пакетом Microsoft HPC на вычислительных узлах Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="48e7f-103">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>
<span data-ttu-id="48e7f-104">В этой статье показан один из способов выполнения рабочих нагрузок высокопроизводительных вычислительных систем Linux на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="48e7f-104">This article shows you one way to run a Linux high-performance computing (HPC) workload on Azure virtual machines.</span></span> <span data-ttu-id="48e7f-105">Кроме того, здесь показано, как настроить кластер [пакета Microsoft HPC](https://technet.microsoft.com/library/cc514029) в Azure, используя вычислительные узлы Linux, и выполнить моделирование [NAMD](http://www.ks.uiuc.edu/Research/namd/), чтобы вычислить и визуализировать структуру большой биомолекулярной системы.</span><span class="sxs-lookup"><span data-stu-id="48e7f-105">Here, you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster on Azure with Linux compute nodes and run a [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulation to calculate and visualize the structure of a large biomolecular system.</span></span>  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* <span data-ttu-id="48e7f-106">**NAMD** (программа Nanoscale Molecular Dynamics) — это пакет для параллельных вычислений молекулярной динамики, разработанный для высокопроизводительного моделирования больших биомолекулярных систем с миллионами атомов.</span><span class="sxs-lookup"><span data-stu-id="48e7f-106">**NAMD** (for Nanoscale Molecular Dynamics program) is a parallel molecular dynamics package designed for high-performance simulation of large biomolecular systems containing up to millions of atoms.</span></span> <span data-ttu-id="48e7f-107">К этим системам относятся вирусы, клеточные структуры и большие белки.</span><span class="sxs-lookup"><span data-stu-id="48e7f-107">Examples of these systems include viruses, cell structures, and large proteins.</span></span> <span data-ttu-id="48e7f-108">NAMD масштабируется до сотен ядер для стандартного моделирования и более чем 500 000 ядер для моделирования самых крупных систем.</span><span class="sxs-lookup"><span data-stu-id="48e7f-108">NAMD scales to hundreds of cores for typical simulations and to more than 500,000 cores for the largest simulations.</span></span>
* <span data-ttu-id="48e7f-109">**Пакет Microsoft HPC** предоставляет функции, необходимые для запуска приложений высокопроизводительных и параллельных вычислений в кластерах локальных компьютеров или виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="48e7f-109">**Microsoft HPC Pack** provides features to run large-scale HPC and parallel applications in clusters of on-premises computers or Azure virtual machines.</span></span> <span data-ttu-id="48e7f-110">Изначально предназначенный для рабочих нагрузок HPC, пакет HPC теперь поддерживает приложения HPC для Linux на виртуальных машинах вычислительного узла Linux, развернутых в кластере пакета HPC.</span><span class="sxs-lookup"><span data-stu-id="48e7f-110">Originally developed as a solution for Windows HPC workloads, HPC Pack now supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="48e7f-111">Общие сведения см. в статье [Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="48e7f-111">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction.</span></span>

<span data-ttu-id="48e7f-112">Чтобы изучить другие варианты выполнения высокопроизводительных рабочих нагрузок HPC для Linux в Azure, ознакомьтесь с [техническими материалами по пакетным и высокопроизводительным вычислениям](../../../batch/batch-hpc-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="48e7f-112">For other options to run Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/batch-hpc-solutions.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48e7f-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="48e7f-113">Prerequisites</span></span>
* <span data-ttu-id="48e7f-114">**Кластер пакета HPC с вычислительными узлами Linux.** Разверните кластер пакета HPC с вычислительными узлами Linux в Azure, используя [шаблон Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) или [скрипт Azure PowerShell](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="48e7f-114">**HPC Pack cluster with Linux compute nodes** - Deploy an HPC Pack cluster with Linux compute nodes on Azure using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="48e7f-115">Предварительные требования и необходимые действия для обоих вариантов см. в статье [Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="48e7f-115">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for the prerequisites and steps for either option.</span></span> <span data-ttu-id="48e7f-116">Если вы выбрали вариант со сценарием PowerShell, просмотрите один из примеров файлов конфигурации в конце этой статьи.</span><span class="sxs-lookup"><span data-stu-id="48e7f-116">If you choose the PowerShell script deployment option, see the sample configuration file in the sample files at the end of this article.</span></span> <span data-ttu-id="48e7f-117">Этот файл позволяет настроить кластер пакета HPC на основе Azure, который состоит из головного узла Windows Server 2012 R2 и четырех вычислительных узлов большого размера под управлением CentOS 6.6.</span><span class="sxs-lookup"><span data-stu-id="48e7f-117">This file configures an Azure-based HPC Pack cluster consisting of a Windows Server 2012 R2 head node and four size Large CentOS 6.6 compute nodes.</span></span> <span data-ttu-id="48e7f-118">Измените этот файл в соответствии со своей средой.</span><span class="sxs-lookup"><span data-stu-id="48e7f-118">Customize this file as needed for your environment.</span></span>
* <span data-ttu-id="48e7f-119">**Программное обеспечение NAMD и руководства.** Скачайте программное обеспечение NAMD для Linux с веб-сайта [NAMD](http://www.ks.uiuc.edu/Research/namd/) (требуется регистрация).</span><span class="sxs-lookup"><span data-stu-id="48e7f-119">**NAMD software and tutorial files** - Download NAMD software for Linux from the [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registration required).</span></span> <span data-ttu-id="48e7f-120">Для выполнения действий, описанных в этой статье, используется NAMD версии 2.10 и архив [Linux-x86_64 (64-разрядный процессор Intel или AMD с поддержкой Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310).</span><span class="sxs-lookup"><span data-stu-id="48e7f-120">This article is based on NAMD version 2.10, and uses the [Linux-x86_64 (64-bit Intel/AMD with Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span></span> <span data-ttu-id="48e7f-121">Кроме того, скачайте [файлы руководства по NAMD](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span><span class="sxs-lookup"><span data-stu-id="48e7f-121">Also download the [NAMD tutorial files](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span></span> <span data-ttu-id="48e7f-122">Эти файлы имеют формат TAR, поэтому вам понадобится средство Windows для извлечения этих файлов на головной узел кластера.</span><span class="sxs-lookup"><span data-stu-id="48e7f-122">The downloads are .tar files, and you need a Windows tool to extract the files on the cluster head node.</span></span> <span data-ttu-id="48e7f-123">Чтобы извлечь эти файлы, следуйте инструкциям, приведенным далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="48e7f-123">To extract the files, follow the instructions later in this article.</span></span> 
* <span data-ttu-id="48e7f-124">**VMD** (необязательно). Чтобы просмотреть результаты задания NAMD, скачайте и установите на любом компьютере программу [VMD](http://www.ks.uiuc.edu/Research/vmd/), позволяющую визуализировать молекулярные системы.</span><span class="sxs-lookup"><span data-stu-id="48e7f-124">**VMD** (optional) - To see the results of your NAMD job, download and install the molecular visualization program [VMD](http://www.ks.uiuc.edu/Research/vmd/) on a computer of your choice.</span></span> <span data-ttu-id="48e7f-125">Текущая версия — 1.9.2.</span><span class="sxs-lookup"><span data-stu-id="48e7f-125">The current version is 1.9.2.</span></span> <span data-ttu-id="48e7f-126">Чтобы скачать программу, перейдите на сайт загрузки VMD.</span><span class="sxs-lookup"><span data-stu-id="48e7f-126">See the VMD download site to get started.</span></span>  

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="48e7f-127">Настройка взаимного доверия между вычислительными узлами</span><span class="sxs-lookup"><span data-stu-id="48e7f-127">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="48e7f-128">Чтобы задание выполнялось на нескольких узлах Linux одновременно, сначала необходимо настроить взаимное доверие узлов (через протокол **rsh** или **ssh**).</span><span class="sxs-lookup"><span data-stu-id="48e7f-128">Running a cross-node job on multiple Linux nodes requires the nodes to trust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="48e7f-129">При создании кластера HPC с помощью сценария развертывания Microsoft HPC IaaS сценарий автоматически настраивает постоянное взаимное доверие для указанной учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="48e7f-129">When you create the HPC Pack cluster with the Microsoft HPC Pack IaaS deployment script, the script automatically sets up permanent mutual trust for the administrator account you specify.</span></span> <span data-ttu-id="48e7f-130">Для учетных записей пользователей без прав администратора, создаваемых в домене кластера, взаимное доверие между узлами должно создаваться в момент назначения им задания</span><span class="sxs-lookup"><span data-stu-id="48e7f-130">For non-administrator users you create in the cluster's domain, you have to set up temporary mutual trust among the nodes when a job is allocated to them.</span></span> <span data-ttu-id="48e7f-131">и уничтожаться после завершения задания.</span><span class="sxs-lookup"><span data-stu-id="48e7f-131">Then, destroy the relationship after the job is complete.</span></span> <span data-ttu-id="48e7f-132">Чтобы реализовать это для всех пользователей, укажите пару ключей RSA в кластере, который пакет HPC использует для установления отношения доверия.</span><span class="sxs-lookup"><span data-stu-id="48e7f-132">To do this for each user, provide an RSA key pair to the cluster which HPC Pack uses to establish the trust relationship.</span></span> <span data-ttu-id="48e7f-133">Следуйте инструкциям ниже.</span><span class="sxs-lookup"><span data-stu-id="48e7f-133">Instructions follow.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="48e7f-134">Создание пары ключей RSA</span><span class="sxs-lookup"><span data-stu-id="48e7f-134">Generate an RSA key pair</span></span>
<span data-ttu-id="48e7f-135">Чтобы создать пару ключей RSA, состоящую из открытого и закрытого ключей, достаточно выполнить команду Linux **ssh-keygen** .</span><span class="sxs-lookup"><span data-stu-id="48e7f-135">It's easy to generate an RSA key pair, which contains a public key and a private key, by running the Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="48e7f-136">Войдите на компьютер под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="48e7f-136">Log on to a Linux computer.</span></span>
2. <span data-ttu-id="48e7f-137">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="48e7f-137">Run the following command:</span></span>
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="48e7f-138">В ходе выполнения команды используйте параметры по умолчанию (нажимайте клавишу **ВВОД**).</span><span class="sxs-lookup"><span data-stu-id="48e7f-138">Press **Enter** to use the default settings until the command is completed.</span></span> <span data-ttu-id="48e7f-139">Не вводите парольную фразу. При запросе пароля просто нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="48e7f-139">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Создание пары ключей RSA][keygen]
3. <span data-ttu-id="48e7f-141">Измените каталог на ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="48e7f-141">Change directory to the ~/.ssh directory.</span></span> <span data-ttu-id="48e7f-142">Закрытый ключ хранится в файле id_rsa, а открытый — в файле id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="48e7f-142">The private key is stored in id_rsa and the public key in id_rsa.pub.</span></span>
   
   ![Открытые и закрытые ключи][keys]

### <a name="add-the-key-pair-to-the-hpc-pack-cluster"></a><span data-ttu-id="48e7f-144">Добавление пары ключей в кластер HPC</span><span class="sxs-lookup"><span data-stu-id="48e7f-144">Add the key pair to the HPC Pack cluster</span></span>
1. <span data-ttu-id="48e7f-145">[Подключитесь к головному узлу виртуальной машины с помощью удаленного рабочего стола](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), используя учетные данные домена, указанные при развертывании кластера (например, hpc\clusteradmin).</span><span class="sxs-lookup"><span data-stu-id="48e7f-145">[Connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to the head node VM using the domain credentials you provided when you deployed the cluster (for example, hpc\clusteradmin).</span></span> <span data-ttu-id="48e7f-146">Управление кластером осуществляется из головного узла.</span><span class="sxs-lookup"><span data-stu-id="48e7f-146">You manage the cluster from the head node.</span></span>
2. <span data-ttu-id="48e7f-147">С помощью стандартных процедур Windows Server создайте учетную запись пользователя домена в домене Active Directory кластера.</span><span class="sxs-lookup"><span data-stu-id="48e7f-147">Use standard Windows Server procedures to create a domain user account in the cluster's Active Directory domain.</span></span> <span data-ttu-id="48e7f-148">Например, на головном узле можно использовать инструмент Active Directory «Пользователи и компьютеры».</span><span class="sxs-lookup"><span data-stu-id="48e7f-148">For example, use the Active Directory User and Computers tool on the head node.</span></span> <span data-ttu-id="48e7f-149">В приведенных в этой статье примерах предполагается, что вы создаете пользователя hpcuser в домене hpclab (hpclab\hpcuser).</span><span class="sxs-lookup"><span data-stu-id="48e7f-149">The examples in this article assume you create a domain user named hpcuser in the hpclab domain (hpclab\hpcuser).</span></span>
3. <span data-ttu-id="48e7f-150">Добавьте пользователя домена в кластер пакета HPC в качестве пользователя кластера.</span><span class="sxs-lookup"><span data-stu-id="48e7f-150">Add the domain user to the HPC Pack cluster as a cluster user.</span></span> <span data-ttu-id="48e7f-151">Инструкции см. в статье [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx) (Добавление и удаление пользователей кластера).</span><span class="sxs-lookup"><span data-stu-id="48e7f-151">For instructions, see [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).</span></span>
4. <span data-ttu-id="48e7f-152">Создайте файл с именем C:\cred.xml и скопируйте в него данные ключей RSA.</span><span class="sxs-lookup"><span data-stu-id="48e7f-152">Create a file named C:\cred.xml and copy the RSA key data into it.</span></span> <span data-ttu-id="48e7f-153">Пример можно найти в файлах примеров в конце этой статьи.</span><span class="sxs-lookup"><span data-stu-id="48e7f-153">You can find an example in the sample files at the end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy the contents of private key here</PrivateKey>
     <PublicKey>Copy the contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. <span data-ttu-id="48e7f-154">Откройте командную строку и введите следующую команду, чтобы задать учетные данные для учетной записи hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="48e7f-154">Open a Command Prompt and enter the following command to set the credentials data for the hpclab\hpcuser account.</span></span> <span data-ttu-id="48e7f-155">Используйте параметр **extendeddata**, чтобы передать имя файла C:\cred.xml, созданного для данных ключей.</span><span class="sxs-lookup"><span data-stu-id="48e7f-155">You use the **extendeddata** parameter to pass the name of the C:\cred.xml file you created for the key data.</span></span>
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="48e7f-156">Эта команда успешно завершается без выходных данных.</span><span class="sxs-lookup"><span data-stu-id="48e7f-156">This command completes successfully without output.</span></span> <span data-ttu-id="48e7f-157">Задав учетные данные для учетных записей пользователей, необходимых для выполнения заданий, сохраните файл cred.xml в безопасном месте или удалите его.</span><span class="sxs-lookup"><span data-stu-id="48e7f-157">After setting the credentials for the user accounts you need to run jobs, store the cred.xml file in a secure location, or delete it.</span></span>
6. <span data-ttu-id="48e7f-158">Если вы создали пару ключей RSA на одном из узлов Linux, не забудьте удалить ключи после завершения работы с ними.</span><span class="sxs-lookup"><span data-stu-id="48e7f-158">If you generated the RSA key pair on one of your Linux nodes, remember to delete the keys after you finish using them.</span></span> <span data-ttu-id="48e7f-159">Пакет HPC не устанавливает взаимное доверие, если обнаруживает существующий файл id_rsa или id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="48e7f-159">HPC Pack does not set up mutual trust if it finds an existing id_rsa file or id_rsa.pub file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48e7f-160">Мы не рекомендуем выполнять задания Linux от имени администратора кластера в общем кластере, так как задания, отправленные администратором, выполняются на узлах Linux под учетной записью root.</span><span class="sxs-lookup"><span data-stu-id="48e7f-160">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under the root account on the Linux nodes.</span></span> <span data-ttu-id="48e7f-161">Задание, отправленное пользователем без прав администратора, выполняется под локальной учетной записью пользователя Linux с тем же именем, что и у пользователя задания.</span><span class="sxs-lookup"><span data-stu-id="48e7f-161">A job submitted by a non-administrator user runs under a local Linux user account with the same name as the job user.</span></span> <span data-ttu-id="48e7f-162">В таком случае пакет HPC устанавливает взаимное доверие для этого пользователя Linux на всех узлах, выделенных для выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="48e7f-162">In this case, HPC Pack sets up mutual trust for this Linux user across all the nodes allocated to the job.</span></span> <span data-ttu-id="48e7f-163">Учетную запись пользователя Linux можно настроить вручную на узлах Linux перед выполнением задания, или пакет HPC автоматически создаст ее при отправке задания.</span><span class="sxs-lookup"><span data-stu-id="48e7f-163">You can set up the Linux user manually on the Linux nodes before running the job, or HPC Pack creates the user automatically when the job is submitted.</span></span> <span data-ttu-id="48e7f-164">Если учетную запись пользователя создает пакет HPC, она удаляется после завершения задания.</span><span class="sxs-lookup"><span data-stu-id="48e7f-164">If HPC Pack creates the user, HPC Pack deletes it after the job completes.</span></span> <span data-ttu-id="48e7f-165">Из соображений безопасности после завершения задания ключи на узлах удаляются.</span><span class="sxs-lookup"><span data-stu-id="48e7f-165">To reduce security threat, the keys are removed after the job completes on the nodes.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="48e7f-166">Настройка файлового ресурса для узлов Linux</span><span class="sxs-lookup"><span data-stu-id="48e7f-166">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="48e7f-167">Теперь настройте стандартный общий ресурс SMB и смонтируйте общую папку на всех узлах Linux, чтобы узлы Linux могли обращаться к файлам NAMD по общему пути.</span><span class="sxs-lookup"><span data-stu-id="48e7f-167">Now set up an SMB file share, and mount the shared folder on all Linux nodes to allow the Linux nodes to access NAMD files with a common path.</span></span> <span data-ttu-id="48e7f-168">Ниже приведены действия для подключения общей папки на головном узле.</span><span class="sxs-lookup"><span data-stu-id="48e7f-168">Following are steps to mount a shared folder on the head node.</span></span> <span data-ttu-id="48e7f-169">Мы советуем выполнять эти действия для таких дистрибутивов, как CentOS 6.6, которые в настоящее время не поддерживают службу файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="48e7f-169">A share is recommended for distributions such as CentOS 6.6 that currently don’t support the Azure File service.</span></span> <span data-ttu-id="48e7f-170">Если ваши узлы Linux поддерживают файловый ресурс Azure, см. статью [Использование хранилища файлов Azure в Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="48e7f-170">If your Linux nodes support an Azure File share, see [How to use Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="48e7f-171">Дополнительные параметры использования файловых ресурсов с помощью пакета HPC описаны в статье [Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="48e7f-171">For additional file sharing options with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="48e7f-172">Создайте папку на головном узле и сделайте ее общедоступной для чтения и записи для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="48e7f-172">Create a folder on the head node, and share it to Everyone by setting Read/Write privileges.</span></span> <span data-ttu-id="48e7f-173">В этом примере \\\\CentOS66HN\Namd — это имя папки, где CentOS66HN — имя головного узла.</span><span class="sxs-lookup"><span data-stu-id="48e7f-173">In this example, \\\\CentOS66HN\Namd is the name of the folder, where CentOS66HN is the host name of the head node.</span></span>
2. <span data-ttu-id="48e7f-174">Создайте в общей папке вложенную папку namd2.</span><span class="sxs-lookup"><span data-stu-id="48e7f-174">Create a subfolder named namd2 in the shared folder.</span></span> <span data-ttu-id="48e7f-175">В namd2 создайте вложенную папку namdsample.</span><span class="sxs-lookup"><span data-stu-id="48e7f-175">In namd2, create another subfolder named namdsample.</span></span>
3. <span data-ttu-id="48e7f-176">Извлеките файлы NAMD в папку с помощью служебной программы **tar** (версия для Windows) или другой служебной программы Windows, которая работает с TAR-архивами.</span><span class="sxs-lookup"><span data-stu-id="48e7f-176">Extract the NAMD files in the folder by using a Windows version of **tar** or another Windows utility that operates on .tar archives.</span></span> 
   
   * <span data-ttu-id="48e7f-177">Извлеките содержимое TAR-архива NAMD в папку \\\\CentOS66HN\Namd\namd2.</span><span class="sxs-lookup"><span data-stu-id="48e7f-177">Extract the NAMD tar archive to \\\\CentOS66HN\Namd\namd2.</span></span>
   * <span data-ttu-id="48e7f-178">Извлеките файлы руководства в папку \\\\CentOS66HN\Namd\namd2\namdsample.</span><span class="sxs-lookup"><span data-stu-id="48e7f-178">Extract the tutorial files under \\\\CentOS66HN\Namd\namd2\namdsample.</span></span>
4. <span data-ttu-id="48e7f-179">Откройте окно Windows PowerShell и выполните следующие команды для подключения общей папки к узлам Linux.</span><span class="sxs-lookup"><span data-stu-id="48e7f-179">Open a Windows PowerShell window and run the following commands to mount the shared folder on the Linux nodes.</span></span>
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="48e7f-180">Первая команда создает папку с именем /namd2 на всех узлах в группе LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="48e7f-180">The first command creates a folder named /namd2 on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="48e7f-181">Вторая команда подключает общую папку //CentOS66HN/Namd/namd2 к папке и задает для параметров dir_mode и file_mode значение 777.</span><span class="sxs-lookup"><span data-stu-id="48e7f-181">The second command mounts the shared folder //CentOS66HN/Namd/namd2 onto the folder with dir_mode and file_mode bits set to 777.</span></span> <span data-ttu-id="48e7f-182">Значения *username* и *password* должны соответствовать учетным данным пользователя на головном узле.</span><span class="sxs-lookup"><span data-stu-id="48e7f-182">The *username* and *password* in the command should be the credentials of a user on the head node.</span></span>

> [!NOTE]
> <span data-ttu-id="48e7f-183">Символ "\\`" во второй команде — это escape-символ для PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48e7f-183">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="48e7f-184">"\\`," означает, что "," (запятая) является частью команды.</span><span class="sxs-lookup"><span data-stu-id="48e7f-184">“\\`,” means the “,” (comma character) is a part of the command.</span></span>
> 
> 

## <a name="create-a-bash-script-to-run-a-namd-job"></a><span data-ttu-id="48e7f-185">Создание сценария Bash для выполнения задания NAMD</span><span class="sxs-lookup"><span data-stu-id="48e7f-185">Create a Bash script to run a NAMD job</span></span>
<span data-ttu-id="48e7f-186">Заданию NAMD требуется файл *nodelist* , с помощью которого **charmrun** определяет количество узлов, которые следует использовать при запуске процессов NAMD.</span><span class="sxs-lookup"><span data-stu-id="48e7f-186">Your NAMD job needs a *nodelist* file for **charmrun** to determine the number of nodes to use when starting NAMD processes.</span></span> <span data-ttu-id="48e7f-187">Используется скрипт Bash, который создает файл nodelist и запускает **charmrun** с этим файлом.</span><span class="sxs-lookup"><span data-stu-id="48e7f-187">You use a Bash script that generates the nodelist file and runs **charmrun** with this nodelist file.</span></span> <span data-ttu-id="48e7f-188">Затем отправьте задание NAMD в диспетчер кластера HPC, вызывающий этот сценарий.</span><span class="sxs-lookup"><span data-stu-id="48e7f-188">You can then submit a NAMD job in HPC Cluster Manager that calls this script.</span></span>

<span data-ttu-id="48e7f-189">Используя любой текстовый редактор, создайте сценарий Bash в папке /namd2 с файлами программы NAMD и назовите его hpccharmrun.sh. Для быстрого подтверждения концепции скопируйте пример скрипта hpccharmrun.sh, приведенный в конце этой статьи, и перейдите к разделу [Отправка задания NAMD](#submit-a-namd-job).</span><span class="sxs-lookup"><span data-stu-id="48e7f-189">Using a text editor of your choice, create a Bash script in the /namd2 folder containing the NAMD program files and name it hpccharmrun.sh. For a quick proof of concept, copy the example hpccharmrun.sh script provided at the end of this article and go to [Submit a NAMD job](#submit-a-namd-job).</span></span>

> [!TIP]
> <span data-ttu-id="48e7f-190">Сохраните сценарий как текстовый файл, в котором для завершения строк используется нотация Linux (только LF, а не CR LF).</span><span class="sxs-lookup"><span data-stu-id="48e7f-190">Save your script as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="48e7f-191">Это гарантирует, что файл будет правильно работать на узлах Linux.</span><span class="sxs-lookup"><span data-stu-id="48e7f-191">This ensures that it runs properly on the Linux nodes.</span></span>
> 
> 

<span data-ttu-id="48e7f-192">Ниже приведены сведения о том, что делает этот сценарий Bash.</span><span class="sxs-lookup"><span data-stu-id="48e7f-192">Following are details about what this bash script does.</span></span> 

1. <span data-ttu-id="48e7f-193">Определите несколько переменных.</span><span class="sxs-lookup"><span data-stu-id="48e7f-193">Define some variables.</span></span>
   
   ```bash
   #!/bin/bash
   
   # The path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. <span data-ttu-id="48e7f-194">Получите сведения об узле из переменных среды.</span><span class="sxs-lookup"><span data-stu-id="48e7f-194">Get node information from the environment variables.</span></span> <span data-ttu-id="48e7f-195">В переменной $NODESCORES хранится список разбиения слов из $CCP_NODES_CORES.</span><span class="sxs-lookup"><span data-stu-id="48e7f-195">$NODESCORES stores a list of split words from $CCP_NODES_CORES.</span></span> <span data-ttu-id="48e7f-196">$COUNT — это размер $NODESCORES.</span><span class="sxs-lookup"><span data-stu-id="48e7f-196">$COUNT is the size of $NODESCORES.</span></span>
   
   ```
   # Get node information from the environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   <span data-ttu-id="48e7f-197">В переменной $CCP_NODES_CORES используется такой формат:</span><span class="sxs-lookup"><span data-stu-id="48e7f-197">The format for the $CCP_NODES_CORES variable is as follows:</span></span>
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   <span data-ttu-id="48e7f-198">Здесь перечисляется общее число узлов, имена узлов и количество ядер на каждом узле, выделенных для выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="48e7f-198">This variable lists the total number of nodes, node names, and number of cores on each node that are allocated to the job.</span></span> <span data-ttu-id="48e7f-199">Например, если для выполнения задания требуется 10 ядер, значение $CCP_NODES_CORES будет выглядеть примерно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="48e7f-199">For example, if the job needs 10 cores to run, the value of $CCP_NODES_CORES is similar to:</span></span>
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. <span data-ttu-id="48e7f-200">Если значение переменной $CCP_NODES_CORES не задано, запустите **charmrun** напрямую.</span><span class="sxs-lookup"><span data-stu-id="48e7f-200">If the $CCP_NODES_CORES variable is not set, start **charmrun** directly.</span></span> <span data-ttu-id="48e7f-201">(это должно происходить, только если сценарий запускается непосредственно на узлах Linux).</span><span class="sxs-lookup"><span data-stu-id="48e7f-201">(This should only occur when you run this script directly on your Linux nodes.)</span></span>
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. <span data-ttu-id="48e7f-202">Или создайте файл nodelist для **charmrun**.</span><span class="sxs-lookup"><span data-stu-id="48e7f-202">Or create a nodelist file for **charmrun**.</span></span>
   
   ```
   else
     # Create the nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write the head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into the nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. <span data-ttu-id="48e7f-203">Запустите **charmrun** с файлом nodelist, получите для него состояние возврата и в конце удалите файл nodelist.</span><span class="sxs-lookup"><span data-stu-id="48e7f-203">Run **charmrun** with the nodelist file, get its return status, and remove the nodelist file at the end.</span></span>
   
   <span data-ttu-id="48e7f-204">${CCP_NUMCPUS} — еще одна переменная среды, которую задает головной узел HPC.</span><span class="sxs-lookup"><span data-stu-id="48e7f-204">${CCP_NUMCPUS} is another environment variable set by the HPC Pack head node.</span></span> <span data-ttu-id="48e7f-205">В ней хранится общее число ядер, выделенных для этого задания.</span><span class="sxs-lookup"><span data-stu-id="48e7f-205">It stores the number of total cores allocated to this job.</span></span> <span data-ttu-id="48e7f-206">Мы используем ее, чтобы указать число процессов для charmrun.</span><span class="sxs-lookup"><span data-stu-id="48e7f-206">We use it to specify the number of processes for charmrun.</span></span>
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. <span data-ttu-id="48e7f-207">Завершите работу, выдав состояние возврата **charmrun** .</span><span class="sxs-lookup"><span data-stu-id="48e7f-207">Exit with the **charmrun** return status.</span></span>
   
   ```
   exit ${RTNSTS}
   ```

<span data-ttu-id="48e7f-208">Ниже приведены сведения в файле nodelist, который создается скриптом.</span><span class="sxs-lookup"><span data-stu-id="48e7f-208">Following is the information in the nodelist file, which the script generates:</span></span>

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

<span data-ttu-id="48e7f-209">Например:</span><span class="sxs-lookup"><span data-stu-id="48e7f-209">For example:</span></span>

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a><span data-ttu-id="48e7f-210">Отправка задания NAMD</span><span class="sxs-lookup"><span data-stu-id="48e7f-210">Submit a NAMD job</span></span>
<span data-ttu-id="48e7f-211">Теперь вы можете отправить задание NAMD в диспетчер кластера HPC.</span><span class="sxs-lookup"><span data-stu-id="48e7f-211">Now you are ready to submit a NAMD job in HPC Cluster Manager.</span></span>

1. <span data-ttu-id="48e7f-212">Подключитесь к головному узлу кластера и запустите диспетчер кластера HPC.</span><span class="sxs-lookup"><span data-stu-id="48e7f-212">Connect to your cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="48e7f-213">В разделе **Управление ресурсами** убедитесь, что для вычислительных узлов Linux отображается состояние **В сети**.</span><span class="sxs-lookup"><span data-stu-id="48e7f-213">In **Resource Management**, ensure that the Linux compute nodes are in the **Online** state.</span></span> <span data-ttu-id="48e7f-214">Если это не так, выберите их и щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="48e7f-214">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="48e7f-215">В разделе **Управление заданиями** щелкните **Новое задание**.</span><span class="sxs-lookup"><span data-stu-id="48e7f-215">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="48e7f-216">Введите для задания имя, например *hpccharmrun*.</span><span class="sxs-lookup"><span data-stu-id="48e7f-216">Enter a name for job such as *hpccharmrun*.</span></span>
   
   ![Новое задание HPC][namd_job]
5. <span data-ttu-id="48e7f-218">На странице **Сведения о задании** в разделе **Ресурсы задания**, выберите тип ресурса **Узел** и задайте для параметра **Минимум** значение 3.</span><span class="sxs-lookup"><span data-stu-id="48e7f-218">On the **Job Details** page, under **Job Resources**, select the type of resource as **Node** and set the **Minimum** to 3.</span></span> <span data-ttu-id="48e7f-219">В этом примере мы выполним задание на трех узлах Linux, каждый из которых имеет по четыре ядра.</span><span class="sxs-lookup"><span data-stu-id="48e7f-219">, we run the job on three Linux nodes and each node has four cores.</span></span>
   
   ![Ресурсы задания][job_resources]
6. <span data-ttu-id="48e7f-221">Щелкните **Изменение задач** в левой области навигации, а затем — **Добавить**, чтобы добавить задачу в задание.</span><span class="sxs-lookup"><span data-stu-id="48e7f-221">Click **Edit Tasks** in the left navigation, and then click **Add** to add a task to the job.</span></span>    
7. <span data-ttu-id="48e7f-222">На странице **Task Details and I/O Redirection** (Сведения о задаче и перенаправление операций ввода-вывода) задайте следующие значения.</span><span class="sxs-lookup"><span data-stu-id="48e7f-222">On the **Task Details and I/O Redirection** page, set the following values:</span></span>
   
   * <span data-ttu-id="48e7f-223">**Командная строка** -
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span><span class="sxs-lookup"><span data-stu-id="48e7f-223">**Command line** -
`/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span></span>
     
     > [!TIP]
     > <span data-ttu-id="48e7f-224">Предыдущая командная строка содержит одну команду без разрывов.</span><span class="sxs-lookup"><span data-stu-id="48e7f-224">The preceding command line is a single command without line breaks.</span></span> <span data-ttu-id="48e7f-225">В области **Командная строка** она будет разбита на несколько строк.</span><span class="sxs-lookup"><span data-stu-id="48e7f-225">It wraps to appear on several lines under **Command line**.</span></span>
     > 
     > 
   * <span data-ttu-id="48e7f-226">**Рабочий каталог** — /namd2.</span><span class="sxs-lookup"><span data-stu-id="48e7f-226">**Working directory** - /namd2</span></span>
   * <span data-ttu-id="48e7f-227">**Минимум** — 3.</span><span class="sxs-lookup"><span data-stu-id="48e7f-227">**Minimum** - 3</span></span>
     
     ![Сведения о задаче][task_details]
     
     > [!NOTE]
     > <span data-ttu-id="48e7f-229">Так как **charmrun** пытается переходить в один и тот же рабочий каталог на каждом узле, рабочий каталог задается на этой странице.</span><span class="sxs-lookup"><span data-stu-id="48e7f-229">You set the working directory here because **charmrun** tries to navigate to the same working directory on each node.</span></span> <span data-ttu-id="48e7f-230">Если рабочий каталог не задан, пакет HPC запускает команду в папке со случайным именем, созданной на одном из узлов Linux.</span><span class="sxs-lookup"><span data-stu-id="48e7f-230">If the working directory isn't set, HPC Pack starts the command in a randomly named folder created on one of the Linux nodes.</span></span> <span data-ttu-id="48e7f-231">Это приведет к возникновению на других узлах следующей ошибки: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.`. Чтобы избежать этой проблемы, укажите путь к папке, к которой все узлы смогут обращаться как к рабочему каталогу.</span><span class="sxs-lookup"><span data-stu-id="48e7f-231">This causes the following error on the other nodes: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` To avoid this problem, specify a folder path that can be accessed by all nodes as the working directory.</span></span>
     > 
     > 
8. <span data-ttu-id="48e7f-232">Нажмите кнопку **ОК**, а затем щелкните **Отправить**, чтобы выполнить это задание.</span><span class="sxs-lookup"><span data-stu-id="48e7f-232">Click **OK** and then click **Submit** to run this job.</span></span>
   
   <span data-ttu-id="48e7f-233">По умолчанию пакет HPC отправляет задание от имени текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="48e7f-233">By default, HPC Pack submits the job as your current logged-on user account.</span></span> <span data-ttu-id="48e7f-234">После нажатия кнопки **Отправить**может появиться диалоговое окно с запросом на ввод имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="48e7f-234">A dialog box might prompt you to enter the user name and password after you click **Submit**.</span></span>
   
   ![Учетные данные для задания][creds]
   
   <span data-ttu-id="48e7f-236">При некоторых обстоятельствах пакет HPC запоминает введенные ранее сведения о пользователе, и это диалоговое окно не появляется.</span><span class="sxs-lookup"><span data-stu-id="48e7f-236">Under some conditions, HPC Pack remembers the user information you input before and doesn't show this dialog box.</span></span> <span data-ttu-id="48e7f-237">Чтобы пакет HPC отобразил его снова, введите в командной строке указанную ниже команду, а затем отправьте задание.</span><span class="sxs-lookup"><span data-stu-id="48e7f-237">To make HPC Pack show it again, enter the following command at a Command Prompt and then submit the job.</span></span>
   
   ```command
   hpccred delcreds
   ```
9. <span data-ttu-id="48e7f-238">Выполнение задания занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="48e7f-238">The job takes several minutes to finish.</span></span>
10. <span data-ttu-id="48e7f-239">Журнал задания будет помещен в папку \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log, а выходные файлы — в папку \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\..</span><span class="sxs-lookup"><span data-stu-id="48e7f-239">Find the job log at \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log and the output files in \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span></span>
11. <span data-ttu-id="48e7f-240">При необходимости запустите VMD, чтобы просмотреть результаты задания.</span><span class="sxs-lookup"><span data-stu-id="48e7f-240">Optionally, start VMD to view your job results.</span></span> <span data-ttu-id="48e7f-241">Шаги по визуализации выходных файлов NAMD (в данном случае — молекулы белка убиквитина в водяном шаре) не входят в эту статью.</span><span class="sxs-lookup"><span data-stu-id="48e7f-241">The steps for visualizing the NAMD output files (in this case, a ubiquitin protein molecule in a water sphere) are beyond the scope of this article.</span></span> <span data-ttu-id="48e7f-242">Дополнительные сведения см. в [руководстве по NAMD](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf).</span><span class="sxs-lookup"><span data-stu-id="48e7f-242">See [NAMD Tutorial](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) for details.</span></span>
    
    ![Результаты задания][vmd_view]

## <a name="sample-files"></a><span data-ttu-id="48e7f-244">Файлы с примерами</span><span class="sxs-lookup"><span data-stu-id="48e7f-244">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="48e7f-245">Пример XML-файла конфигурации для развертывания кластера с помощью скрипта PowerShell</span><span class="sxs-lookup"><span data-stu-id="48e7f-245">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
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

### <a name="sample-credxml-file"></a><span data-ttu-id="48e7f-246">Пример файла cred.xml</span><span class="sxs-lookup"><span data-stu-id="48e7f-246">Sample cred.xml file</span></span>
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

### <a name="sample-hpccharmrunsh-script"></a><span data-ttu-id="48e7f-247">Пример сценария hpccharmrun.sh</span><span class="sxs-lookup"><span data-stu-id="48e7f-247">Sample hpccharmrun.sh script</span></span>
```
#!/bin/bash

# The path of this script
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
    # If CCP_NODES_CORES is not found or is empty, just run the charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create the nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write the head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into the nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run the charmrun with nodelist arg
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
