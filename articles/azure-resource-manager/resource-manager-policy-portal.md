---
title: "портал aaaAzure для политики ресурсов | Документы Microsoft"
description: "Описывает способ toouse Azure портала toocreate политик диспетчера ресурсов и управление ими. Политики могут применяться для групп hello подписка или ресурс."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a>Использование Azure портала tooassign политики и управлять ими ресурсов
Hello портал Azure позволяет вам tooassign политики tooresource групп ресурсов и подписки. Hello пользовательский интерфейс позволяет легко tooselect hello политики требуется tooassign и укажите значения параметров для этого toocustomize hello политика. 

tooassign политики через портал hello определения политики hello должна существовать в вашей подписке. Ваша подписка имеет несколько определений встроенных политик, готовых для вас tooassign tooresource группы или подписки. Вы увидите этих встроенных политик и пользовательских политик, определенных при использовании портала tooassign политики hello. Toopolicies введение и как toodefine настроить политики см. в разделе [Общие сведения о политике ресурсов](resource-manager-policy.md).

Политики наследуются всеми дочерними ресурсами. Таким образом Если политика не применяется tooa группы ресурсов, это применимо tooall hello ресурсов в этой группе ресурсов. В этой статье термин hello **область** ссылается toohello группы ресурсов или подписку, которая будет назначена политика hello. 

Политики оцениваются при создании и обновлении ресурсов (операции PUT и PATCH).

## <a name="assign-a-policy"></a>Назначение политики

1. tooassign tooeither политики группу ресурсов или подписку, выберите этой группы ресурсов или подписки. В параметрах hello выберите **политики**.

   ![выбор политик](./media/resource-manager-policy-portal/select-policies.png)

2. Выберите назначение политики для этой области toocreate **добавить назначение**.

   ![добавление назначения](./media/resource-manager-policy-portal/add-assignment.png)

3. Выберите политику hello требуется tooassign. Даже если вы не добавили любую подписку tooyour определения политики, может появиться hello встроенных политик, доступных для назначения. Эти встроенные политики охватывают множество распространенных сценариев.

   ![выбор определения](./media/resource-manager-policy-portal/select-definition.png)

4. После выбора политики, то см. описание политики hello и все параметры этой политики. Hello следующем рисунке показано, hello **допускается расположения** параметр, который требуется для hello политику, которая ограничивает hello доступных расположений.

   ![отображение параметров](./media/resource-manager-policy-portal/show-parameters.png)

5. Пользовательским интерфейсом приложения hello выберите hello toospecify значения для параметров политики hello (например, размещение hello, которые могут использоваться для развертывания).

   ![выбор значений параметров](./media/resource-manager-policy-portal/select-parameters.png)

6. Укажите значения для hello другие параметры. область Hello задается автоматически в колонке hello, выбранным при запуске назначения политики hello. По окончании нажмите кнопку **ОК** .

   ![определение параметров](./media/resource-manager-policy-portal/define-parameters.png)

  Назначена политика hello toohello указан области.

## <a name="view-policy-assignments"></a>Просмотр назначенных политик

После назначения политики, найдите его в списке hello политик для данной области. Hello **сведения** вкладка со сводкой назначения политики hello.

![отображение сведений](./media/resource-manager-policy-portal/show-details.png)

Hello **правила назначения** вкладке отображается hello JSON для определения политики hello.

![отображение правила назначения](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a>Изменение существующего назначения политики

Выберите политику, toochange **изменить назначение** или **удалить**

![изменение или удаление назначения](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a>Назначение пользовательских политик

Если в вашей подписке определены настраиваемые политики, эти политики доступны для назначения через портал hello. Эти политики содержат в своем названии приставку **[Custom]**.

![пользовательские политики](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a>Дальнейшие действия
* toolearn о синтаксисе hello JSON для определения политик, в разделе [Общие сведения о политике ресурсов](resource-manager-policy.md).
* Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).
* Схема политики Hello опубликованы по адресу [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json). 

