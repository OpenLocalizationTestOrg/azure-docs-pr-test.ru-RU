---
title: "aaaCreate лаборатории в Azure DevTest Labs | Документы Microsoft"
description: "Создание лаборатории в Azure DevTest Labs для виртуальных машин"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a>Создание лаборатории в лаборатории для разработки и тестирования Azure
Лаборатории в Azure DevTest Labs — hello инфраструктурой, которая содержит группы ресурсов, например виртуальных машин (ВМ), которые позволяют лучше управлять этими ресурсами, указывая, ограничения и квоты. В этой статье рассматриваются hello процесс создания лаборатории, используя hello портал Azure.

## <a name="prerequisites"></a>Предварительные требования
toocreate лабораторной среде, необходимо:

* Подписка Azure. toolearn о варианты приобретения Azure, в разделе [как toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) или [бесплатной пробной версии один месяц](https://azure.microsoft.com/pricing/free-trial/). Необходимо быть владельцем hello hello подписки toocreate hello лаборатории.

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a>Действия toocreate лаборатории в Azure DevTest Labs
Привет, следующие шаги показывают, как toouse hello Azure портала toocreate лаборатории в Azure DevTest Labs. 

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Hello в главном меню в левой части hello, выберите **более служб** (внизу hello hello список).

    ![Пункт меню "Больше служб"](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. Из списка доступных служб hello **DevTest Labs**.
1. На hello **DevTest Labs** колонке выберите **добавить**.
   
    ![Добавление лаборатории](./media/devtest-lab-create-lab/add-lab-button.png)

1. На hello **создание лаборатории, DevTest** колонки:
   
    1. Введите **имени лаборатории** для новой лабораторной hello.
    2. Выберите hello **подписки** tooassociate hello лаборатории.
    3. Выберите **расположение** в какой лаборатории toostore hello.
    4. Выберите **автоматическое завершение работы** toospecify tooenable - и определения параметров hello - hello автоматическое завершение работы всех лаборатории hello виртуальных машин. Hello автоматического завершения работы компонент является главным образом снизить издержки при котором можно указать, когда требуется hello ВМ tooautomatically завершить работу. Параметры автоматического завершения работы можно изменить после создания лаборатории hello hello выполните действия, описанные в статье hello [управления всеми политиками для лаборатории в Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).
    5. Выберите **tooDashboard ПИН-код** Если нужно упростить hello tooappear лаборатории на панели мониторинга портала hello.
    6. Выберите **возможности автоматизации** tooget шаблонов диспетчера ресурсов Azure для автоматизации настройки. 
    7. Нажмите кнопку **Создать**. После выбора **создать**, hello **DevTest Labs** отображает колонку. Можно отслеживать состояние hello процесса создания лаборатории hello посмотрите hello **уведомления** области. После завершения обновления hello страницы toosee hello новые лаборатории в списке hello лабораторий.  
    
    ![Колонка создания лаборатории](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Дальнейшие действия
После создания лаборатории, ниже приведены некоторые Далее tooconsider действия.

* [Безопасный доступ tooa лаборатории](devtest-lab-add-devtest-user.md).
* [Определение политик лаборатории](devtest-lab-set-lab-policy.md).
* [Создание шаблона лаборатории](devtest-lab-create-template.md).
* [Создание пользовательских артефактов для виртуальных машин](devtest-lab-artifact-author.md).
* [Добавить виртуальную Машину с артефакты лаборатории tooa](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).

