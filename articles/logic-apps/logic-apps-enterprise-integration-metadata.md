---
title: "Интеграция aaaManage учетной записи метаданных артефакта - приложения логики Azure | Документы Microsoft"
description: "Узнайте, как добавлять и извлекать метаданные артефактов учетных записей интеграции для Azure Logic Apps."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8de71bffa9f9975d5409716b2208fa6c3a9545d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a>Управление метаданными артефактов в учетных записях интеграции для приложений логики

Вы можете определять пользовательские метаданные для артефактов в учетных записях интеграции и извлекать эти метаданные в среде выполнения приложений логики. Например, можно указать метаданные для артефактов (партнеры, соглашения, схемы, сопоставления и др.) и сохранить все метаданные с помощью пар "ключ — значение". В настоящее время артефактов не может создать метаданные через пользовательский Интерфейс, но можно использовать API-интерфейс REST toocreate метаданных. Выберите tooadd метаданных при создании или выберите в hello Azure портал партнера, соглашения или схемы **изменить как JSON**. tooretrieve артефактов метаданных в логику приложения, можно использовать средство просмотра артефакта учетной записи интеграции hello.

## <a name="add-metadata-tooartifacts-in-integration-accounts"></a>Добавить метаданные tooartifacts в учетные записи службы интеграции

1. Создайте [учетную запись интеграции](logic-apps-enterprise-integration-create-integration-account.md).

2. Добавьте учетную запись интеграции tooyour артефакта, например, [партнера](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [соглашение](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), или [схемы](logic-apps-enterprise-integration-schemas.md).

3.  Выберите артефакт hello, выберите **изменить как JSON**и введите сведения о метаданных.

    ![Ввод метаданных](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a>Извлечение метаданных из артефактов для приложений логики

1. Создайте [приложение логики](logic-apps-create-a-logic-app.md).

2. Создание [ссылку из вашей учетной записи интеграции логики приложения tooyour](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app). 

3. В конструкторе логики приложения, добавить триггер как *запроса* или *HTTP* tooyour логику приложения.

4.  Выберите **Следующий шаг** > **Добавить действие**. Выполните поиск по слову *интеграции*, чтобы найти и выбрать **Учетная запись интеграции > Поиск артефакта учетной записи интеграции**.

    ![Выбор функции "Поиск артефакта учетной записи интеграции"](media/logic-apps-enterprise-integration-metadata/image2.png)

5. Выберите hello **тип артефакта**и укажите hello **имя артефакта**.

    ![Выбор типа артефакта и указание имени артефакта](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a>Пример: извлечение метаданных партнера

Метаданные партнера содержат такие сведения о `routingUrl`:

![Поиск в метаданных партнера сведений о routingURL](media/logic-apps-enterprise-integration-metadata/image6.png)

1. В приложении логики добавьте триггер, действие **Учетная запись интеграции > Поиск артефакта учетной записи интеграции** для партнера, а затем — **HTTP**.

    ![Добавление триггера, артефакта подстановки и приложения логики tooyour «HTTP»](media/logic-apps-enterprise-integration-metadata/image4.png)

2. hello tooretrieve URI, последовательно tooCode представление логики приложения. Определение приложения логики должно выглядеть примерно как в этом примере:

    ![Поиск](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a>Дальнейшие действия
* [Узнайте о соглашениях и Пакете интеграции Enterprise](logic-apps-enterprise-integration-agreements.md "Узнайте о соглашениях и Пакете интеграции Enterprise")  
