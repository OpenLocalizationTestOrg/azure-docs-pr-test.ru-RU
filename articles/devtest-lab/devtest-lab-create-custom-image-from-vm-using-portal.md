---
title: "aaaCreate Azure DevTest Labs пользовательского образа из виртуальной Машины | Документы Microsoft"
description: "Узнайте, как toocreate из подготовленных виртуальной Машины с помощью настраиваемого изображения в Azure DevTest Labs hello портал Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a>Создание пользовательского образа из виртуальной машины

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a>Пошаговые инструкции

Создать образ из подготовленных виртуальной Машины и впоследствии использовать toocreate этого пользовательского образа идентичные виртуальные машины. Привет, следующие шаги показывают, как toocreate пользовательского образа из виртуальной Машины:

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Выберите **дополнительные службы**, а затем выберите **DevTest Labs** из списка hello.

1. Выберите из списка hello лабораториям hello требуемой лаборатории.  

1. В колонке hello лаборатории выберите **моих виртуальных машин**.
 
1. На hello **моих виртуальных машин** колонки, из которого нужно toocreate hello пользовательского образа виртуальной Машины выберите hello.

1. В колонке hello виртуальной Машины выберите **создать пользовательский образ (VHD)**.

    ![Пункт меню "Создание пользовательского образа"](./media/devtest-lab-create-template/create-custom-image.png)

1. На hello **создать изображение** колонки, введите имя и описание для настраиваемого образа. Эта информация отображается в списке базовых классов hello при создании виртуальной Машины.

    ![Колонка "Создание пользовательского образа"](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. Выберите, будут ли на hello виртуальной Машины было запущено средство sysprep. Если hello sysprep не была запущена на hello виртуальной Машины, укажите, следует ли запускать, когда виртуальная машина создается из этого пользовательского образа sysprep.

1. Выберите **ОК** при завершении toocreate hello пользовательского образа.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Связанные записи в блогах

- [Custom images or formulas? (Пользовательские изображения или формулы?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Copying Custom Images between Azure DevTest Labs (Копирование пользовательских образов между лабораториями для разработки и тестирования Azure)](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Дальнейшие действия

- [Добавление виртуальных Машин лаборатории tooyour](./devtest-lab-add-vm-with-artifacts.md)
