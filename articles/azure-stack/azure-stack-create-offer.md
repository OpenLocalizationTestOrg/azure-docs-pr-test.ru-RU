---
title: "предложение Azure стека aaaCreate | Документы Microsoft"
description: "Как администратор облака, узнайте, как toocreate предложение для клиентов в Azure стека."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 96b080a4-a9a5-407c-ba54-111de2413d59
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: erikje
ms.openlocfilehash: 924526a0ff1c634b7c127c03a4572057c35b497b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-offer-in-azure-stack"></a>Создание предложения в Azure Stack
[Предлагает](azure-stack-key-features.md) — это группы один или несколько планов, поставщики присутствует tootenants toopurchase или подписаться на него. В этом документе показано, как предложение, включающее hello toocreate [план, созданный](azure-stack-create-plan.md) на последнем шаге hello. Это предложение обеспечивает подписчиков hello возможность tooprovision виртуальных машин.

1. Войдите в портал администратора Azure стека toohello (https://adminportal.local.azurestack.external) > щелкните **New** > **клиента предлагает + планы**  >   **Предложить**.

   ![](media/azure-stack-create-offer/image01.png)
2. В hello **новое предложение** колонки, заполните **отображаемое имя** и **имя ресурса**и затем выберите новую или существующую **группы ресурсов**. Hello отображаемое имя является hello предложение понятное имя и hello только сведения о предложение hello, hello пользователи будут видеть при подписке. Таким образом будет убедиться, что toouse интуитивно имя, которое помогает понять, что следует предложение hello пользователя hello. Только администратор hello можно увидеть hello имя ресурса. Он является hello имя, "Администраторы" использовать toowork с hello предложения в качестве ресурса диспетчера ресурсов Azure.

   ![](media/azure-stack-create-offer/image01a.png)
3. Нажмите кнопку **базовые планы** и в hello **планирование** колонки, выберите hello планы tooinclude в предложение hello и нажмите кнопку **выберите**. Нажмите кнопку **создать** toocreate hello предложения.

   ![](media/azure-stack-create-offer/image02.png)
4. Нажмите кнопку **все ресурсы**, поиск новое предложение, щелкните на новое предложение hello, **изменению состояния**и нажмите кнопку **открытый**.

   ![](media/azure-stack-create-offer/image03.png)

Предложения должны выполняться открытым и позволить клиентам tooget hello полное представление при подписке. Предложения можно:

* **Открытый**: tootenants видимым.
* **Закрытый**: только администраторы видимым toohello облака. Полезно при набора hello план или предложение, или если администратор облака hello хочет tooapprove каждую подписку.
* **Списать**: закрыто toonew подписчиков. Здравствуйте, администратор облака можно использовать списанные tooprevent будущие подписки, но оставьте текущие подписчики без изменений.

Предложение toohello изменения не являются видимыми toohello клиента. изменения toosee hello, может потребоваться toologout/входа toosee hello новую подписку в hello «Средством выбора подписки» при создании групп ресурсов и ресурсов.

> [!NOTE]
>Предложения по умолчанию, планы и квоты также можно создать с помощью PowerShell, как описано в hello [файл сведений для администратора службы Azure стека](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).
>


## <a name="next-steps"></a>Дальнейшие действия
[Подписаться на предложение tooan и затем подготовьте виртуальную Машину](azure-stack-subscribe-plan-provision-vm.md)
