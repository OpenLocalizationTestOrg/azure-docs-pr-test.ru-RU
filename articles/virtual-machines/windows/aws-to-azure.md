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
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a>Перемещение виртуальной Машины Windows с tooAzure Amazon Web Services (AWS), с помощью PowerShell

При оценке виртуальных машин Azure для размещения рабочих нагрузок, можно экспортировать существующий экземпляр виртуальной Машины Windows EC2 Amazon Web Services (AWS) и отправка виртуального жесткого диска (VHD) tooAzure hello. Один раз hello, переданный виртуальный жесткий ДИСК, можно создать новую виртуальную Машину в Azure из hello виртуального жесткого диска. 

В этом разделе описывается перемещение одной виртуальной Машины из AWS tooAzure. Виртуальные машины toomove из tooAzure AWS в масштабе см [перенос виртуальных машин в tooAzure Amazon Web Services (AWS) с Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).

## <a name="prepare-hello-vm"></a>Подготовка виртуальной Машины hello 
 
Можно передать обобщенной и специализированные tooAzure виртуальных жестких дисков. Для каждого типа требуется подготовить hello виртуальной Машины, прежде чем экспортировать из AWS. 

- **Универсальный виртуальный жесткий диск**. С универсального VHD с помощью Sysprep удалены все сведения вашей личной учетной записи. Если предполагается toouse hello VHD как toocreate изображения следует новые виртуальные машины из: 
 
    * [Подготовьте виртуальную машину Windows](prepare-for-upload-vhd-image.md).  
    * Обобщить hello виртуальной машины с помощью программы Sysprep.  

 
- **Специализированные VHD** -специализированные виртуальный жесткий ДИСК поддерживает учетные записи пользователей hello, приложений и других данных о состоянии из исходной виртуальной Машины. Если предполагается toouse hello VHD как-является toocreate новой виртуальной Машины, убедитесь, выполняются следующие шаги hello.  
    * [Подготовка виртуального жесткого диска Windows tooupload tooAzure](prepare-for-upload-vhd-image.md). **Нет** generalize hello виртуальную Машину с помощью Sysprep. 
    * Удалите все гостевой средств виртуализации и агентов, установленных на hello виртуальной Машины (т. е. средства VMware). 
    * Обеспечить hello виртуальной Машины является настроенным toopull его IP-адрес и параметры DNS через DHCP. Это гарантирует, что этот сервер hello получает IP-адрес в пределах hello виртуальной сети при запуске.  


## <a name="export-and-download-hello-vhd"></a>Экспорт и загрузка виртуального жесткого диска hello 

Экспорт hello EC2 экземпляр tooa виртуального жесткого диска в сегмент Amazon S3. Выполните hello действия, описанные в разделе документации Amazon hello [Экспорт экземпляр как виртуальной Машины с помощью виртуальной Машины импорта и экспорта](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) и выполнения hello [создания экземпляра export задач](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) команда tooexport hello EC2 экземпляр tooa VHD-файл. 

Hello экспортированный файл виртуального жесткого диска сохраняется в контейнере hello Amazon S3, указываемые. Hello базовый синтаксис для экспорта hello виртуального жесткого диска является ниже, просто замените замещающий текст hello в <brackets> с собственными данными.

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

После экспорта hello виртуального жесткого диска, следуйте инструкциям hello [как загрузить объект с сегмент S3?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload hello VHD файлов из контейнеров hello S3. 

> [!IMPORTANT]
> AWS оплата сборов передачи данных по загрузке hello виртуального жесткого диска. Дополнительные сведения см. на странице [Цены на Amazon S3](https://aws.amazon.com/s3/pricing/).


## <a name="next-steps"></a>Дальнейшие действия

Теперь можно загрузить hello VHD tooAzure и создания новой виртуальной Машины. 

- При запуске средства Sysprep в источнике слишком**generalize** его перед экспортом. в разделе [Отправка обобщенный виртуальный жесткий ДИСК и использовать toocreate новые виртуальные машины в Azure](upload-generalized-managed.md)
- Если вы не запускали Sysprep перед экспортом, hello VHD считается **специализированные**, в разделе [передача специализированные tooAzure виртуального жесткого диска и создание новой виртуальной Машины](create-vm-specialized.md)

 
