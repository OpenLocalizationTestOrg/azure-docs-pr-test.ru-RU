---
title: "Параметры изображения aaaConfigure Azure Marketplace в Azure DevTest Labs | Документы Microsoft"
description: "Настройка образов Azure Marketplace, которые можно использовать при создании виртуальной машины в Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a>Настройка параметров образов Azure Marketplace в Azure DevTest Labs
DevTest Labs поддерживает создание виртуальных машин на основе образов Azure Marketplace в зависимости от того, как вы настроили Azure Marketplace toobe изображений, используемых в лаборатории. В этой статье показано, как toospecify, который, если таковые имеются, образы Azure Marketplace можно использовать при создании виртуальных машин в лаборатории. Это гарантирует, что у команды есть только доступ toohello Marketplace образов, которые они должны. 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a>Выбор разрешенных образов Azure Marketplace при создании виртуальной машины
1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.
3. Выберите из списка hello лабораториям hello требуемой лаборатории. 
4. В колонке hello лаборатории выберите **конфигурации и политиках**.
5. В колонке **Конфигурация и политики** лаборатории в разделе **Базы виртуальных машин** выберите **Образы Marketplace**.
6. Укажите, следует ли все hello полное toobe образы Azure Marketplace, доступных для использования в качестве основы новой виртуальной Машины. При выборе **Да**, затем все образы Azure Marketplace hello в лаборатории hello допускается, удовлетворяющих hello все следующие условия:
   
   * изображение Hello создает одной виртуальной Машины **и**
   * образ Hello использует ВМ tooprovision диспетчера ресурсов Azure, **и**
   * изображение Hello не требует приобретения дополнительного лицензирования план
     
    Если нужно, toobe изображений не допускается, или вы хотите toospecify изображения, можно использовать, выберите **нет**.
     
     ![Параметр tooallow все toobe Marketplace образов используется в качестве базовые образы для виртуальных машин](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. При выборе **нет** toohello предыдущего шага hello **разрешено изображения или выбирать все** установлен флажок. 
   Можно использовать этот параметр вместе с tooquickly hello поиска выберите или отмените выбор всех hello элементов, отображаемых в списке hello.
   * Выберите образы Azure Marketplace hello требуется tooallow для создания виртуальной Машины по отдельности, установив соответствующий флажок для каждого изображения.
   * Если вы не хотите tooallow любой toobe образы Azure Marketplace, используемых в лаборатории hello, выбор пуст из списка hello.
   
    ![Можно указать, какие образы Azure Marketplace будут использоваться в качестве базовых образов для виртуальных машин.](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Дальнейшие действия
После настройки как образы Azure Marketplace могут при создании виртуальной Машины hello следующим шагом является слишком[добавления виртуальных Машин лаборатории tooyour](devtest-lab-add-vm-with-artifacts.md).

