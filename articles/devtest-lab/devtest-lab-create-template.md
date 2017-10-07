---
title: "aaaCreate Azure DevTest Labs образ из VHD-файл | Документы Microsoft"
description: "Узнайте, как toocreate из файла виртуального жесткого диска с помощью настраиваемого изображения в Azure DevTest Labs hello портал Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a>Создание пользовательского образа из VHD-файла

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a>Пошаговые инструкции

Hello следующие шаги содержат пошаговые инструкции по созданию настраиваемого образа из VHD-файла с помощью портала Azure hello:

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Выберите **дополнительные службы**, а затем выберите **DevTest Labs** из списка hello.

1. Выберите из списка hello лабораториям hello требуемой лаборатории.  

1. В колонке hello лаборатории выберите **конфигурации**. 

1. В лаборатории hello **конфигурации** колонке выберите **пользовательских изображений (VHD)**.

1. На hello **пользовательских образов** колонке выберите **+ добавить**.

    ![Добавить пользовательский образ](./media/devtest-lab-create-template/add-custom-image.png)

1. Введите имя пользовательского образа hello hello. Это имя отображается в списке hello базовые образы, при создании виртуальной Машины.

1. Введите описание hello hello пользовательского образа. Это описание отображается в списке hello базовые образы, при создании виртуальной Машины.

1. Выберите **VHD**.

1. Из hello **VHD** колонки, выберите hello требуемого файла виртуального жесткого диска.

1. Выберите **ОК** tooclose hello **VHD** колонку.

1. Щелкните **Конфигурация ОС**.

1. На hello **конфигурация ОС** выберите либо **Windows** или **Linux**.

1. Если **Windows** — флажок установлен, укажите через флажок hello ли *Sysprep* была запущена на компьютере hello. 

1. Выберите **ОК** tooclose hello **конфигурация ОС** колонку.

1. Выберите **ОК** toocreate hello пользовательского образа.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Связанные записи в блогах

- [Custom images or formulas? (Пользовательские изображения или формулы?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Copying Custom Images between Azure DevTest Labs (Копирование пользовательских образов между лабораториями для разработки и тестирования Azure)](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Дальнейшие действия

- [Добавление виртуальных Машин лаборатории tooyour](./devtest-lab-add-vm-with-artifacts.md)
