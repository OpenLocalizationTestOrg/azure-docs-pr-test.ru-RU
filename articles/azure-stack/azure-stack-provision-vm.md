---
title: "aaaCreate теста виртуальной Машины в Azure стек | Документы Microsoft"
description: "Узнайте, как tooprovision теста виртуальной Машины в стеке Azure как оператор облака."
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
ms.date: 7/21/2017
ms.author: erikje
ms.openlocfilehash: 9633cc20852e16283ad4522da78971133028efdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-test-virtual-machine-in-azure-stack"></a>Создать тестовую виртуальную машину в стек Azure
Как оператор облака toovalidate теста виртуальной машины можно создать развертывание стека Azure.

> [!NOTE]
> Прежде чем можно подготовить виртуальные машины, необходимо [добавьте hello ознакомительную версию Windows Server 2016 изображения toohello стека Azure marketplace](azure-stack-add-default-image.md).
> 
> 

## <a name="create-a-virtual-machine"></a>Создание виртуальной машины
1. На узле пакет средств разработки Azure стека hello [входа в](azure-stack-connect-azure-stack.md) toohello Администратор портала (`https://adminportal.local.azurestack.external`) и нажмите кнопку **New** > **вычислений**  >  **Windows Server 2016 Datacenter Eval** > **создания**.  
2. В hello **основы** колонке введите **имя**, **имя пользователя**, и **пароль**. Выберите **подписку**. Создание **группы ресурсов**, или выберите существующий и нажмите кнопку **ОК**.  
3. В hello **выберите размер** колонке нажмите кнопку **A1 Standard**, а затем нажмите кнопку **выберите**.  
4. В hello **параметры** колонке примите значения по умолчанию hello и нажмите кнопку **ОК**
5. В hello **Сводка** колонка, щелкните **ОК** toocreate hello виртуальной машины.  
6. toosee новой виртуальной машины, нажмите кнопку **все ресурсы**, а затем найдите hello виртуальную машину и щелкните ее имя.
    ![](media/azure-stack-provision-vm/image06.png)


## <a name="next-steps"></a>Дальнейшие действия
[С помощью hello порталы администратора и пользователя в стек Azure](azure-stack-manage-portals.md)
