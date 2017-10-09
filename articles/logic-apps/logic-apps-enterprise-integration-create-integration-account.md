---
title: "aaaCreate, ссылку, удалить или переместить учетную запись интеграции приложения логики Azure | Документы Microsoft"
description: "Как toocreate интеграцию учетной записи и связать его tooyour логику приложения"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a>Что такое учетная запись интеграции?

Учетная запись интеграции позволяет интеграции корпоративных приложений toomanage артефакты, включая схемы, карты, сертификаты, партнеров и соглашения. Любое приложение интеграции, создаваемые вами использует tooaccess учетной записи интеграции эти схемы, карты, сертификаты и т. д.

## <a name="create-an-integration-account"></a>Создание учетной записи интеграции

1.  Войдите в toohello [портал Azure](http://portal.azure.com "портал Azure"). Hello в левом меню, выберите **дополнительные службы**.

    ![Выбор "Больше служб"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. В поле поиска hello введите «интеграция» для фильтра. В списке результатов hello выберите **учетные записи службы интеграции**.

    ![Фильтрация по интеграции, выбор "Учетные записи интеграции"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. В начале hello страницы приветствия, выберите **добавить**.

    ![Кнопка "Добавить"](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. Имя вашей учетной записи интеграции и выберите hello подписки Azure, которые должны toouse. Вы можете создать **группу ресурсов** или выбрать имеющуюся. Выберите **Расположение** для размещения учетной записи интеграции и **ценовую категорию**. 

    Когда вы будете готовы, нажмите кнопку **Создать**.

    ![Ввод сведений для учетной записи интеграции](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    Azure подготавливает учетную запись интеграции в hello выбрать расположение, которое следует выполнить в пределах 1 минуты.

5. Обновите страницу приветствия. Вы увидите новую учетную запись интеграции в списке.

    ![Отображение новой учетной записи интеграции](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

Затем подключитесь учетной записи интеграции hello, то созданный tooyour приложения логики. 

## <a name="link-an-integration-account-tooa-logic-app"></a>Связать приложение логики интеграции tooa учетной записи

toogive свои приложения логики доступа к toomaps, схемы, соглашения и другие артефакты в учетной записи интеграции tooyour ссылку hello интеграции учетной записи приложения логики.

### <a name="prerequisites"></a>Предварительные требования

* Учетная запись интеграции.
* Приложение логики

> [!NOTE] 
> Убедитесь, что приложения учетной записи и логики интеграции в hello *же расположению Azure* перед началом.


1. В hello портал Azure выберите логику приложения и проверить расположение приложения логики.

    ![Выбор приложения логики, проверка расположения](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. В разделе **Параметры** выберите **Учетная запись интеграции**.

    ![Выбор "Учетная запись интеграции"](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. Из hello **выберите учетную запись интеграции** список, выберите hello интеграции счета, toolink tooyour логику приложения. Выберите toofinish связывания, **Сохранить**.

    ![Выбор учетной записи интеграции](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    Вы получаете уведомление, которое показывает интеграцию учетной записи связанного tooyour логику приложения, и все артефакты в вашей учетной записи интеграции, теперь доступны tooyour логику приложения.

    ![Логика приложения связана учетная запись tooyour интеграции](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

Теперь, когда ваша учетная запись интеграции связанного tooyour логику приложения, можно использовать в приложениях для логики соединители hello B2B. Некоторые распространенные соединители B2B включают в себя проверку XML, кодирование и декодирование неструктурированных файлов.  

## <a name="delete-your-integration-account"></a>Удаление учетной записи интеграции

1. Выберите **Больше служб**.

    ![Выбор "Больше служб"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. В поле поиска hello введите «интеграция» для фильтра. В списке результатов hello выберите **учетные записи службы интеграции**.

    ![Фильтрация по интеграции, выбор "Учетные записи интеграции"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. Выберите hello интеграции учетной записью, которую toodelete.

    ![Выбор учетной записи toodelete интеграции](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. Выберите пункт меню hello **удалить**.

    ![Выбор команды "Удалить"](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. Подтверждение учетной записи интеграции choice toodelete hello.

## <a name="move-your-integration-account"></a>Перемещение учетной записи интеграции

toomove tooanother учетной записи интеграции Azure подписка или группа ресурсов, выполните следующие действия.

> [!IMPORTANT]
> После перемещения интеграции учетную запись, необходимо обновить все сценарии toouse hello новые идентификаторы ресурсов.

1. Выберите **Больше служб**.

    ![Выбор "Больше служб"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. В поле поиска hello введите «интеграция» для фильтра. В списке результатов hello выберите **учетные записи службы интеграции**.

    ![Фильтрация по интеграции, выбор "Учетные записи интеграции"](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. Выберите hello интеграции учетной записью, которую toomove. В разделе **Параметры** выберите **Свойства**.

    ![Выберите toomove учетной записи интеграции. Раздел "Параметры", выбор "Свойства"](./media/logic-apps-enterprise-integration-accounts/move.png)

5. Изменение hello группы ресурсов или подписку Azure, связанной с вашей учетной записи интеграции.

    ![Выбор "Изменить группу ресурсов" или "Изменить подписку"](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a>Дальнейшие действия
* [Узнайте о соглашениях и Пакете интеграции Enterprise](../logic-apps/logic-apps-enterprise-integration-agreements.md "Узнайте о соглашениях и Пакете интеграции Enterprise")  

