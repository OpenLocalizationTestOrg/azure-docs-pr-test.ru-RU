---
title: "aaaMove tooAzure виртуальных машин Windows AWS | Документы Microsoft"
description: "Переместите tooAzure экземпляр Windows EC2 Amazon Web Services (AWS) виртуальных машин с помощью Azure PowerShell."
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
ms.openlocfilehash: f912c28d3ffe585162c3add715a1318ac3cd4643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a><span data-ttu-id="b6d54-103">Перемещение виртуальной Машины Windows с tooAzure Amazon Web Services (AWS), с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6d54-103">Move a Windows VM from Amazon Web Services (AWS) tooAzure using PowerShell</span></span>

<span data-ttu-id="b6d54-104">При оценке виртуальных машин Azure для размещения рабочих нагрузок, можно экспортировать существующий экземпляр виртуальной Машины Windows EC2 Amazon Web Services (AWS) и отправка виртуального жесткого диска (VHD) tooAzure hello.</span><span class="sxs-lookup"><span data-stu-id="b6d54-104">If you are evaluating Azure virtual machines for hosting your workloads, you can export an existing Amazon Web Services (AWS) EC2 Windows VM instance then upload hello virtual hard disk (VHD) tooAzure.</span></span> <span data-ttu-id="b6d54-105">Один раз hello, переданный виртуальный жесткий ДИСК, можно создать новую виртуальную Машину в Azure из hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="b6d54-105">Once hello VHD is uploaded, you can create a new VM in Azure from hello VHD.</span></span> 

<span data-ttu-id="b6d54-106">В этом разделе описывается перемещение одной виртуальной Машины из AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b6d54-106">This topic covers moving a single VM from AWS tooAzure.</span></span> <span data-ttu-id="b6d54-107">Виртуальные машины toomove из tooAzure AWS в масштабе см [перенос виртуальных машин в tooAzure Amazon Web Services (AWS) с Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="b6d54-107">If you want toomove VMs from AWS tooAzure at scale, see [Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="b6d54-108">Подготовка виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="b6d54-108">Prepare hello VM</span></span> 
 
<span data-ttu-id="b6d54-109">Можно передать обобщенной и специализированные tooAzure виртуальных жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="b6d54-109">You can upload both generalized and specialized VHDs tooAzure.</span></span> <span data-ttu-id="b6d54-110">Для каждого типа требуется подготовить hello виртуальной Машины, прежде чем экспортировать из AWS.</span><span class="sxs-lookup"><span data-stu-id="b6d54-110">Each type requires that you prepare hello VM before exporting from AWS.</span></span> 

- <span data-ttu-id="b6d54-111">**Универсальный виртуальный жесткий диск**. С универсального VHD с помощью Sysprep удалены все сведения вашей личной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b6d54-111">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="b6d54-112">Если предполагается toouse hello VHD как toocreate изображения следует новые виртуальные машины из:</span><span class="sxs-lookup"><span data-stu-id="b6d54-112">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span> 
 
    * <span data-ttu-id="b6d54-113">[Подготовьте виртуальную машину Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="b6d54-113">[Prepare a Windows VM](prepare-for-upload-vhd-image.md).</span></span>  
    * <span data-ttu-id="b6d54-114">Обобщить hello виртуальной машины с помощью программы Sysprep.</span><span class="sxs-lookup"><span data-stu-id="b6d54-114">Generalize hello virtual machine using Sysprep.</span></span>  

 
- <span data-ttu-id="b6d54-115">**Специализированные VHD** -специализированные виртуальный жесткий ДИСК поддерживает учетные записи пользователей hello, приложений и других данных о состоянии из исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b6d54-115">**Specialized VHD** - a specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="b6d54-116">Если предполагается toouse hello VHD как-является toocreate новой виртуальной Машины, убедитесь, выполняются следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="b6d54-116">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span>  
    * <span data-ttu-id="b6d54-117">[Подготовка виртуального жесткого диска Windows tooupload tooAzure](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="b6d54-117">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> <span data-ttu-id="b6d54-118">**Нет** generalize hello виртуальную Машину с помощью Sysprep.</span><span class="sxs-lookup"><span data-stu-id="b6d54-118">**Do not** generalize hello VM using Sysprep.</span></span> 
    * <span data-ttu-id="b6d54-119">Удалите все гостевой средств виртуализации и агентов, установленных на hello виртуальной Машины (т. е. средства VMware).</span><span class="sxs-lookup"><span data-stu-id="b6d54-119">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span> 
    * <span data-ttu-id="b6d54-120">Обеспечить hello виртуальной Машины является настроенным toopull его IP-адрес и параметры DNS через DHCP.</span><span class="sxs-lookup"><span data-stu-id="b6d54-120">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="b6d54-121">Это гарантирует, что этот сервер hello получает IP-адрес в пределах hello виртуальной сети при запуске.</span><span class="sxs-lookup"><span data-stu-id="b6d54-121">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span>  


## <a name="export-and-download-hello-vhd"></a><span data-ttu-id="b6d54-122">Экспорт и загрузка виртуального жесткого диска hello</span><span class="sxs-lookup"><span data-stu-id="b6d54-122">Export and download hello VHD</span></span> 

<span data-ttu-id="b6d54-123">Экспорт hello EC2 экземпляр tooa виртуального жесткого диска в сегмент Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="b6d54-123">Export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="b6d54-124">Выполните hello действия, описанные в разделе документации Amazon hello [Экспорт экземпляр как виртуальной Машины с помощью виртуальной Машины импорта и экспорта](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) и выполнения hello [создания экземпляра export задач](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) команда tooexport hello EC2 экземпляр tooa VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="b6d54-124">Follow hello steps described in hello Amazon documentation topic [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) and run hello [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) command tooexport hello EC2 instance tooa VHD file.</span></span> 

<span data-ttu-id="b6d54-125">Hello экспортированный файл виртуального жесткого диска сохраняется в контейнере hello Amazon S3, указываемые.</span><span class="sxs-lookup"><span data-stu-id="b6d54-125">hello exported VHD file is saved in hello Amazon S3 bucket you specify.</span></span> <span data-ttu-id="b6d54-126">Hello базовый синтаксис для экспорта hello виртуального жесткого диска является ниже, просто замените замещающий текст hello в <brackets> с собственными данными.</span><span class="sxs-lookup"><span data-stu-id="b6d54-126">hello basic syntax for exporting hello VHD is below, just replace hello placeholder text in <brackets> with your information.</span></span>

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

<span data-ttu-id="b6d54-127">После экспорта hello виртуального жесткого диска, следуйте инструкциям hello [как загрузить объект с сегмент S3?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload hello VHD файлов из контейнеров hello S3.</span><span class="sxs-lookup"><span data-stu-id="b6d54-127">Once hello VHD has been exported, follow hello instructions in [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload hello VHD file from hello S3 bucket.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b6d54-128">AWS оплата сборов передачи данных по загрузке hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="b6d54-128">AWS charges data transfer fees for downloading hello VHD.</span></span> <span data-ttu-id="b6d54-129">Дополнительные сведения см. на странице [Цены на Amazon S3](https://aws.amazon.com/s3/pricing/).</span><span class="sxs-lookup"><span data-stu-id="b6d54-129">See [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) for more information.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b6d54-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b6d54-130">Next steps</span></span>

<span data-ttu-id="b6d54-131">Теперь можно загрузить hello VHD tooAzure и создания новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b6d54-131">Now you can upload hello VHD tooAzure and create a new VM.</span></span> 

- <span data-ttu-id="b6d54-132">При запуске средства Sysprep в источнике слишком**generalize** его перед экспортом. в разделе [Отправка обобщенный виртуальный жесткий ДИСК и использовать toocreate новые виртуальные машины в Azure](upload-generalized-managed.md)</span><span class="sxs-lookup"><span data-stu-id="b6d54-132">If you ran Sysprep on your source too**generalize** it before exporting, see [Upload a generalized VHD and use it toocreate a new VMs in Azure](upload-generalized-managed.md)</span></span>
- <span data-ttu-id="b6d54-133">Если вы не запускали Sysprep перед экспортом, hello VHD считается **специализированные**, в разделе [передача специализированные tooAzure виртуального жесткого диска и создание новой виртуальной Машины](create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="b6d54-133">If you did not run Sysprep before exporting, hello VHD is considered **specialized**, see [Upload a specialized VHD tooAzure and create a new VM](create-vm-specialized.md)</span></span>

 
