---
title: "aaaCreate плана в стек Azure | Документы Microsoft"
description: "Как администратор облака создайте план, который позволяет подписчикам подготовки виртуальных машин."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 3dc92e5c-c004-49db-9a94-783f1f798b98
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: erikje
ms.openlocfilehash: 3665bae5d212002da43316e62ce73686b4c66eea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-plan-in-azure-stack"></a>Создание плана в Azure Stack
[Планы](azure-stack-key-features.md) — это группы, содержащие одну или несколько служб. В качестве поставщика можно создавать планы toooffer tooyour клиентов. В свою очередь клиентам подписываться tooyour предложения toouse hello планы и службы, которые они включают. В этом примере показано, как toocreate план, который включает в себя hello поставщики ресурсов вычисления, сети и хранилища. Этот план дает подписчиков hello возможность tooprovision виртуальных машин.

1. Войдите в систему toohello портала администратора Azure стека (https://adminportal.local.azurestack.external). Введите учетные данные hello hello учетной записи, созданной на шаге 5 hello [скрипт PowerShell hello](azure-stack-run-powershell-script.md) раздела.

2. Щелкните toocreate плана и предложения, который клиенты могут подписываться на, **New** > **клиента предлагает + планы** > **плана**.

   ![](media/azure-stack-create-plan/image01.png)
3. В hello **создать план** колонки, заполните **отображаемое имя** и **имя ресурса**. Hello отображаемое имя — hello плана понятное имя, которое будет отображаться для клиентов. Только администратор hello можно увидеть hello имя ресурса. Он является hello имя, "Администраторы" использовать toowork с планом hello в качестве ресурса диспетчера ресурсов Azure.

   ![](media/azure-stack-create-plan/image02.png)
4. Создайте новый **группы ресурсов**, или выберите существующий как контейнер для плана hello.

   ![](media/azure-stack-create-plan/image02a.png)
5. Нажмите кнопку **службы**выберите **Microsoft.Compute**, **Microsoft.Network**, и **хранилища Майкрософт**, а затем нажмите кнопку **Выберите**.

   ![](media/azure-stack-create-plan/image03.png)
6. Нажмите кнопку **квоты**, нажмите кнопку **хранилища Майкрософт (local)**и затем либо выберите hello Квота по умолчанию или нажмите кнопку **Создание новой квоте** toocustomize hello квоты.

   ![](media/azure-stack-create-plan/image04.png)
7. При создании новой квоте, введите имя для квоты hello > задать значения квоты hello > щелкните **ОК** > щелкните имя новой квоте hello hello.

   ![](media/azure-stack-create-plan/image06.png)
8. Нажмите кнопку **Microsoft.Network (local)**и затем либо выберите hello Квота по умолчанию или нажмите кнопку **Создание новой квоте** toocustomize hello квоты.

    ![](media/azure-stack-create-plan/image07.png)
9. При создании новой квоте, введите имя для квоты hello > задать значения квоты hello > щелкните **ОК** > щелкните имя новой квоте hello hello.

    ![](media/azure-stack-create-plan/image08.png)
10. Нажмите кнопку **Microsoft.Compute (local)**и затем либо выберите hello Квота по умолчанию или нажмите кнопку **Создание новой квоте** toocustomize hello квоты.

    ![](media/azure-stack-create-plan/image09.png)
11. При создании новой квоте, введите имя для квоты hello > задать значения квоты hello > щелкните **ОК** > щелкните имя новой квоте hello hello.

    ![](media/azure-stack-create-plan/image10.png)
12. В hello **квоты** колонке нажмите кнопку **ОК**и затем в hello **новый план** колонке нажмите кнопку **создать** toocreate hello плана.

    ![](media/azure-stack-create-plan/image11.png)
13. toosee новый план, нажмите кнопку **все ресурсы**, а затем найдите hello план и щелкните ее имя.

    ![](media/azure-stack-create-plan/image12.png)

### <a name="next-steps"></a>Дальнейшие действия
[Создание предложения](azure-stack-create-offer.md)
