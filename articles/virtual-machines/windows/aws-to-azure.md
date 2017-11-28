---
title: "Перемещение виртуальных машин Windows из AWS в Azure | Документация Майкрософт"
description: "В этой статье описывается перемещение экземпляра виртуальной машины Windows EC2 из Amazon Web Services (AWS) в службу виртуальных машин Azure с помощью Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: cynthn
ms.openlocfilehash: 7d2b498d3f84c4fd6cccf97c6d7781f293f5b395
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-to-azure-using-powershell"></a><span data-ttu-id="048ab-103">Перемещение виртуальной машины Windows из Amazon Web Services (AWS) в Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="048ab-103">Move a Windows VM from Amazon Web Services (AWS) to Azure using PowerShell</span></span>

<span data-ttu-id="048ab-104">При оценке виртуальных машин Azure для размещения рабочих нагрузок можно экспортировать существующий экземпляр виртуальной машины Windows EC2 из Amazon Web Services (AWS) и передать виртуальный жесткий диск (VHD) в Azure.</span><span class="sxs-lookup"><span data-stu-id="048ab-104">If you are evaluating Azure virtual machines for hosting your workloads, you can export an existing Amazon Web Services (AWS) EC2 Windows VM instance then upload the virtual hard disk (VHD) to Azure.</span></span> <span data-ttu-id="048ab-105">После передачи VHD вы можете создать на его основе виртуальную машину в Azure.</span><span class="sxs-lookup"><span data-stu-id="048ab-105">Once the VHD is uploaded, you can create a new VM in Azure from the VHD.</span></span> 

<span data-ttu-id="048ab-106">В этой статье описывается перемещение одной виртуальной машины из AWS в Azure.</span><span class="sxs-lookup"><span data-stu-id="048ab-106">This topic covers moving a single VM from AWS to Azure.</span></span> <span data-ttu-id="048ab-107">Сведения о том, как переместить масштабируемые виртуальные машины из AWS в Azure, см. в статье [Перенос виртуальных машин из Amazon Web Services (AWS) в Azure с помощью Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="048ab-107">If you want to move VMs from AWS to Azure at scale, see [Migrate virtual machines in Amazon Web Services (AWS) to Azure with Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span></span>

## <a name="prepare-the-vm"></a><span data-ttu-id="048ab-108">Подготовка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="048ab-108">Prepare the VM</span></span> 
 
<span data-ttu-id="048ab-109">В Azure можно передавать как универсальные, так и специализированные виртуальные жесткие диски.</span><span class="sxs-lookup"><span data-stu-id="048ab-109">You can upload both generalized and specialized VHDs to Azure.</span></span> <span data-ttu-id="048ab-110">Для обоих типов требуется предварительная подготовка виртуальной машины к экспорту из AWS.</span><span class="sxs-lookup"><span data-stu-id="048ab-110">Each type requires that you prepare the VM before exporting from AWS.</span></span> 

- <span data-ttu-id="048ab-111">**Универсальный виртуальный жесткий диск**. С универсального VHD с помощью Sysprep удалены все сведения вашей личной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="048ab-111">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="048ab-112">Если вы планируете использовать виртуальный жесткий диск в качестве образа для создания виртуальных машин, то выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="048ab-112">If you intend to use the VHD as an image to create new VMs from, you should:</span></span> 
 
    * <span data-ttu-id="048ab-113">[Подготовьте виртуальную машину Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="048ab-113">[Prepare a Windows VM](prepare-for-upload-vhd-image.md).</span></span>  
    * <span data-ttu-id="048ab-114">Сделайте виртуальную машину универсальной с помощью Sysprep.</span><span class="sxs-lookup"><span data-stu-id="048ab-114">Generalize the virtual machine using Sysprep.</span></span>  

 
- <span data-ttu-id="048ab-115">**Специализированный виртуальный жесткий диск**. На специализированном VHD сохраняются учетные записи пользователей, приложения и другие данные о состоянии исходной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="048ab-115">**Specialized VHD** - a specialized VHD maintains the user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="048ab-116">Если вы планируете использовать виртуальный жесткий диск "как есть" для создания виртуальной машины, то необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="048ab-116">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span>  
    * <span data-ttu-id="048ab-117">[Подготовьте виртуальный жесткий диск Windows к передаче в Azure](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="048ab-117">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md).</span></span> <span data-ttu-id="048ab-118">**Не выполняйте** подготовку виртуальной машины к использованию с помощью Sysprep.</span><span class="sxs-lookup"><span data-stu-id="048ab-118">**Do not** generalize the VM using Sysprep.</span></span> 
    * <span data-ttu-id="048ab-119">Удалите все гостевые инструменты и агенты виртуализации, которые установлены на виртуальной машине (т. е. инструменты VMware).</span><span class="sxs-lookup"><span data-stu-id="048ab-119">Remove any guest virtualization tools and agents that are installed on the VM (i.e. VMware tools).</span></span> 
    * <span data-ttu-id="048ab-120">Убедитесь, что виртуальная машина настроена на получение IP-адреса и параметров DNS через DHCP.</span><span class="sxs-lookup"><span data-stu-id="048ab-120">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="048ab-121">Таким образом, сервер будет получать IP-адрес в виртуальной сети при запуске.</span><span class="sxs-lookup"><span data-stu-id="048ab-121">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span>  


## <a name="export-and-download-the-vhd"></a><span data-ttu-id="048ab-122">Экспорт и скачивание VHD-файла</span><span class="sxs-lookup"><span data-stu-id="048ab-122">Export and download the VHD</span></span> 

<span data-ttu-id="048ab-123">Экспортируйте экземпляр EC2 на VHD в контейнере Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="048ab-123">Export the EC2 instance to a VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="048ab-124">Выполните действия, описанные в документации по Amazon в разделе об [экспорте экземпляра виртуальной машины с помощью импорта и экспорта](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html), и выполните команду [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html), чтобы экспортировать экземпляр EC2 в VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="048ab-124">Follow the steps described in the Amazon documentation topic [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) and run the [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) command to export the EC2 instance to a VHD file.</span></span> 

<span data-ttu-id="048ab-125">Экспортированный VHD-файл сохраняется в указанном контейнере Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="048ab-125">The exported VHD file is saved in the Amazon S3 bucket you specify.</span></span> <span data-ttu-id="048ab-126">Базовый синтаксис для экспорта VHD приведен ниже. Просто замените замещающий текст в <brackets> собственными данными.</span><span class="sxs-lookup"><span data-stu-id="048ab-126">The basic syntax for exporting the VHD is below, just replace the placeholder text in <brackets> with your information.</span></span>

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

<span data-ttu-id="048ab-127">По завершении экспорта VHD следуйте инструкциям в разделе о [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) (Как скачать объект из контейнера S3?), чтобы скачать VHD-файл из контейнера S3.</span><span class="sxs-lookup"><span data-stu-id="048ab-127">Once the VHD has been exported, follow the instructions in [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) to download the VHD file from the S3 bucket.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="048ab-128">В AWS взимается плата за передачу данных при скачивании VHD-файла.</span><span class="sxs-lookup"><span data-stu-id="048ab-128">AWS charges data transfer fees for downloading the VHD.</span></span> <span data-ttu-id="048ab-129">Дополнительные сведения см. на странице [Цены на Amazon S3](https://aws.amazon.com/s3/pricing/).</span><span class="sxs-lookup"><span data-stu-id="048ab-129">See [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) for more information.</span></span>


## <a name="next-steps"></a><span data-ttu-id="048ab-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="048ab-130">Next steps</span></span>

<span data-ttu-id="048ab-131">Теперь можно передать VHD в Azure и создать виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="048ab-131">Now you can upload the VHD to Azure and create a new VM.</span></span> 

- <span data-ttu-id="048ab-132">Если вы запустили Sysprep на исходной виртуальной машине, чтобы **сделать ее универсальной** перед экспортом, см. статью о [передаче универсального виртуального жесткого диска и его использовании для создания виртуальных машин в Azure](upload-generalized-managed.md)</span><span class="sxs-lookup"><span data-stu-id="048ab-132">If you ran Sysprep on your source to **generalize** it before exporting, see [Upload a generalized VHD and use it to create a new VMs in Azure](upload-generalized-managed.md)</span></span>
- <span data-ttu-id="048ab-133">Если вы не запускали Sysprep перед экспортом, VHD считается **специализированным**. См. статью [Создание виртуальной машины из специализированного диска](create-vm-specialized.md).</span><span class="sxs-lookup"><span data-stu-id="048ab-133">If you did not run Sysprep before exporting, the VHD is considered **specialized**, see [Upload a specialized VHD to Azure and create a new VM](create-vm-specialized.md)</span></span>

 
