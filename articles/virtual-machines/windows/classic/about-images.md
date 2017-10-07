---
title: "aaaAbout образов для виртуальных машин Windows | Документы Microsoft"
description: "Узнайте о том, как использовать образы с виртуальными машинами Windows в Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: c7cfa1d018a5e99d5b68f559ec9ae1f14e4dec8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-windows-virtual-machines"></a>Образы виртуальных машин
> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Сведения о поиске и использование изображений в модели hello диспетчера ресурсов. в разделе [здесь](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a>Работа с образами

Можно использовать модуль Azure PowerShell hello и hello Azure портала toomanage hello изображения доступен tooyour подписки Azure. Hello модуля Azure PowerShell предоставляет дополнительные параметры команды, чтобы точно определить, что можно проследить toosee или выполните. Hello портал Azure предоставляет графический пользовательский Интерфейс для многих hello повседневных административных задач.

Вот несколько примеров использования модуля Azure PowerShell hello.

* **Получить все образы**:`Get-AzureVMImage`возвращает список всех образов hello, доступных в текущей подписке: образов и предоставленных Azure или партнерами. полученный список Hello может быть большим. Здравствуйте далее примерах показано, как tooget более короткому списку.
* **Получить семейства образов.** `Get-AzureVMImage | select ImageFamily` возвращает список семейств образов, отображая свойство строк **ImageFamily**.
* **Получить все образы из указанного семейства.** `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`
* **Поиск образов виртуальных Машин**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` этот командлет работает путем фильтрации свойство DataDiskConfiguration hello, которое применяется только tooVM изображения. В этом примере также фильтры hello вывода tooonly hello метки и имени образ.
* **Сохранить обобщенный образ.** `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`
* **Сохранить специализированный образ.** `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`

  > [!TIP]
  > параметр OSState Hello является обязательным toocreate образ виртуальной Машины, который включает hello диска операционной системы и присоединенных дисков с данными. Если вы не используете параметр hello, hello командлет создает образ ОС. Hello значение параметра hello указывает ли hello образа, обобщенный или специальный, на основании hello диск операционной системы был подготовлен для повторного использования.

* **Удалить образ.** `Remove-AzureVMImage –ImageName "MyOldVmImage"`

## <a name="next-steps"></a>Дальнейшие действия
Вы также можете [Создание машины Windows с помощью портала Azure hello](tutorial.md).
