---
title: "сбои aaaDiagnose артефакта в виртуальной Машине Azure DevTest Labs | Документы Microsoft"
description: "Узнайте, как tootroubleshoot сбоев артефакта в DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 115e0086-3293-4adf-8738-9f639f31f918
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: tarcher
ms.openlocfilehash: 40b3cea72cf071cc5d9a6d002d309d923c3d3084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-artifact-failures-in-hello-lab"></a>Диагностику сбоев артефакта в лаборатории hello 
После создания артефакта toosee можно проверить, если он успешно или неудачно. Журналы артефакта в DevTest Labs предоставляют сведения, которые можно использовать toodiagnose сбоя артефакта. Существует несколько способов, можно просмотреть сведения о журнале hello артефакта для виртуальной Машины Windows.

> [!NOTE]
> tooensure, сбои идентифицируются и описано, очень важно, этим артефактом hello неправильно структурированы правильно. Сведения о как toocorrectly построить артефакта содержатся [создать пользовательские артефакты](devtest-lab-artifact-author.md). И toosee пример правильно структурированного артефакта, ознакомьтесь с этой [типы параметров тестирования](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) артефакта.

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a>Устранение неполадок при неудачном артефакта, с помощью портала Azure hello
toouse hello Azure портала toodiagnose сбоев во время создания артефакта, выполните следующие действия.

1. Выберите из списка hello ресурсов лаборатории.

2. Выберите hello виртуальной Машине Windows, включающий требуется tooinvestigate артефакта hello.

3. Hello левой панели в разделе **Общие**, выберите **артефакты**. Отображается список артефакты, связанные с этой виртуальной Машины, является признаком того, имя hello hello артефактов и их состояния.

   ![Пример репозитория артефактов Git](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. Выберите артефакт, для которого отображается состояние **Сбой**. артефакт Hello открывается и отображается сообщение расширения, включающий сведения о сбое hello hello артефакта.

   ![Пример репозитория артефактов Git](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a>Устранение неполадок при неудачном артефакта из внутри hello виртуальной Машины
tooview hello артефакта журналы hello виртуальной машине, выполните следующие действия.

1. Войдите в виртуальной Машине, которая содержит артефакт hello требуется toodiagnose toohello.

2. Перейдите tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status где «1.9 — номер версии CSE hello.

   ![Пример репозитория артефактов Git](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. Откройте hello **состояние** файл tooview данные, что помогает диагностировать артефакта для этой виртуальной Машины.




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Связанные записи в блогах
* [Присоединение виртуальной Машины tooexisting домена AD, с помощью шаблона диспетчера ресурсов в Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте, каким образом слишком[добавьте лаборатории tooa репозитория Git](devtest-lab-add-artifact-repo.md).

