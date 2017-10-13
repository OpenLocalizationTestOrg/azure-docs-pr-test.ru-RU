---
title: "Создание тестовой виртуальной Машине в Azure стек | Документы Microsoft"
description: "Узнайте, как подготовка тестовой виртуальной Машине в стеке Azure как оператор облака."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: c86646e1-a12e-493f-b396-f17bfacd60c2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: erikje
ms.openlocfilehash: 233cf4df53af6a49e5fe4c5d51e112d8196a7530
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-test-virtual-machine-in-azure-stack"></a>Создать тестовую виртуальную машину в стек Azure

*Применяется к: Azure стека пакет средств разработки*

Как оператор стек Azure можно создать тестовую виртуальную машину для проверки вашей [стека Azure](azure-stack-poc.md) развертывания пакет средств разработки.

> [!NOTE]
> Прежде чем можно подготовить виртуальные машины, необходимо [добавить образ Windows Server 2016 Evaluation в стек Azure Marketplace](azure-stack-add-default-image.md).
> 
> 

## <a name="create-a-virtual-machine"></a>Создание виртуальной машины
1. На узле пакет средств разработки Azure стека [входа](azure-stack-connect-azure-stack.md) портал администратора (`https://adminportal.local.azurestack.external`) и нажмите кнопку **New** > **вычислений**  >  **Windows Server 2016 Datacenter Eval** > **создания**.  
2. В **основы** колонке введите **имя**, **имя пользователя**, и **пароль**. Выберите **подписку**. Создание **группы ресурсов**, или выберите существующий и нажмите кнопку **ОК**.  
3. В **выберите размер** колонке нажмите кнопку **A1 Standard**, а затем нажмите кнопку **выберите**.  
4. В **параметры** колонке примите значения по умолчанию и нажмите кнопку **ОК**
5. В **Сводка** колонка, щелкните **ОК** для создания виртуальной машины.  
6. Для просмотра на новую виртуальную машину, щелкните **все ресурсы**, а затем найдите виртуальную машину и щелкните ее имя.
    ![](media/azure-stack-provision-vm/image06.png)


## <a name="next-steps"></a>Дальнейшие действия
[С помощью порталы администратора и пользователя в стек Azure](azure-stack-manage-portals.md)
