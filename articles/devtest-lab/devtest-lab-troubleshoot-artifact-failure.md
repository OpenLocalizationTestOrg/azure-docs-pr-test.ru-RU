---
title: "Диагностика сбоев артефактов на виртуальной машине Azure DevTest Labs | Документация Майкрософт"
description: "Узнайте, как устранять неполадки при сбоях артефактов в DevTest Labs."
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
ms.openlocfilehash: e4f2946d0ba0756f36622aded0e8594acabb9527
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="diagnose-artifact-failures-in-the-lab"></a>Диагностика сбоев артефактов в лаборатории 
После создания артефакта можно проверить, успешно ли он работает. Журналы артефактов в DevTest Labs предоставляют сведения, которые можно использовать для диагностики сбоя артефакта. Существует несколько способов просмотреть сведения журнала артефактов для виртуальной машины Windows.

> [!NOTE]
> Чтобы можно было правильно идентифицировать и объяснить сбой, важно правильно структурировать артефакт. Сведения о том, как правильно создать артефакт, см. в статье [Создание пользовательских артефактов для виртуальной машины DevTest Labs](devtest-lab-artifact-author.md). Правильно структурированный артефакт можно изучить на примере этого артефакта [тестовых типов параметров](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes).

## <a name="troubleshoot-artifact-failures-using-the-azure-portal"></a>Устранение неполадок при сбоях артефактов с помощью портала Azure
Чтобы использовать портал Azure для диагностики неполадок при создании артефактов, выполните следующие действия:

1. В списке ресурсов выберите свою лабораторию.

2. Выберите виртуальную машину Windows, которая содержит анализируемый артефакт.

3. На левой панели в разделе **ОБЩИЕ** выберите **Артефакты**. Отобразится список артефактов, связанных с этой виртуальной машиной, в котором указывается имя артефакта и его состояние.

   ![Пример репозитория артефактов Git](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. Выберите артефакт, для которого отображается состояние **Сбой**. Артефакт откроется и отобразится сообщение расширения, содержащее сведения о сбое артефакта.

   ![Пример репозитория артефактов Git](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-the-vm"></a>Устранение неполадок при сбоях артефактов из виртуальной машины
Чтобы просмотреть журналы артефактов из виртуальной машины, выполните следующие действия:

1. Войдите в виртуальную машину, содержащую артефакт, для которого требуется выполнить диагностику.

2. Перейдите к расположению C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status, где 1.9 — это номер версии CSE.

   ![Пример репозитория артефактов Git](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. Откройте файл **status**, чтобы просмотреть сведения, которые помогут диагностировать сбои артефактов для данной виртуальной машины.




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Связанные записи в блогах
* [Join a VM to existing AD Domain using ARM template in Azure Dev Test Lab](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs) (Присоединение виртуальной машины к существующему домену AD с помощью шаблона ARM в Azure DevTest Labs)

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте, как [добавить в лабораторию репозиторий Git](devtest-lab-add-artifact-repo.md).

