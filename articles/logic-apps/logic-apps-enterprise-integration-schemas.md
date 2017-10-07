---
title: "aaaSchemas для проверки XML - приложения логики Azure | Документы Microsoft"
description: "Проверка XML-документов с помощью схем для Azure Logic Apps и пакета интеграции Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 87cf92741e10ff7cccd260f27442909e34928903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a>Проверка XML с помощью схем для приложения логики Azure и hello пакет интеграции Enterprise

Схемы убедитесь, что hello XML-документов, полученный являются допустимыми и hello ожиданиям данных в стандартных форматов. С помощью схем также можно проверить сообщения, которыми стороны обмениваются в сценарии B2B.

## <a name="add-a-schema"></a>Добавление схемы

1. В hello портал Azure, выберите **дополнительные службы**.

    ![Портал Azure, "Другие службы"](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. Введите в поле поиска фильтра hello, **интеграции**и выберите **учетные записи службы интеграции** из списка результатов hello.

    ![Поле фильтра поиска](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. Выберите hello **учетной записи интеграции** место tooadd hello схемы.

    ![Список учетных записей интеграции](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. Выберите hello **схемы** плитки.

    ![Пример учетной записи интеграции, "Схемы"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a>Добавление файла схемы, размер которого меньше 2 МБ

1. В hello **схемы** колонку, которая открывает (из hello предыдущих шагах), выберите **добавить**.

    ![Колонка "Схемы", "Добавить"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. Введите имя для схемы. Загрузить файл схемы hello, выбрав toohello Далее значок папки hello **схемы** поле. После завершения процесса отправки hello **ОК**.

    ![Снимок экрана: колонка "Добавление схемы" с выделенным элементом "Мелкий файл"](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a>Добавьте файл схемы, размер которых превышает 2 МБ (вверх максимум too8 МБ)

Эти действия различаются в зависимости от уровня доступа для контейнера большого двоичного объекта hello: **открытый** или **отсутствие анонимного доступа**.

**toodetermine этот уровень доступа**

1.  Откройте **обозреватель хранилищ Azure**. 

2.  В разделе **контейнеров больших двоичных объектов**, выберите контейнер больших двоичных объектов hello требуется. 

3.  Выберите последовательно **Безопасность**, **Уровень доступа**.

Если уровень доступа hello большого двоичного объекта безопасности **открытый**, выполните следующие действия.

![Обозреватель хранилищ Azure с выделенными элементами "Контейнеры больших двоичных объектов", "Безопасность" и "Общедоступный"](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. Передайте учетной записи хранилища tooyour схемы hello и скопируйте hello URI.

    ![Учетная запись хранения с выделенным URI](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. В **добавить схему**выберите **большого файла**и укажите hello URI в hello **URI содержимого** текстовое поле.

    ![Страница "Схемы", на которой выделены кнопка "Добавить" и параметр "Большой файл"](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

Если уровень доступа hello большого двоичного объекта безопасности **отсутствие анонимного доступа**, выполните следующие действия.

![Обозреватель хранилищ Azure с выделенными элементами "Контейнеры больших двоичных объектов", "Безопасность" и "Без анонимного доступа"](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. Передача схемы для hello tooyour учетной записи хранилища.

    ![Учетная запись хранения](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. Создать подпись общего доступа для схемы hello.

    ![Учетная запись хранения с выделенной вкладкой подписанных URL-адресов](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. В **добавить схему**выберите **большого файла**и укажите URI подписи коллективного доступа hello в hello **URI содержимого** текстовое поле.

    ![Страница "Схемы", на которой выделены кнопка "Добавить" и параметр "Большой файл"](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. В hello **схемы** колонке учетной записи интеграции должны появиться добавленный схему.

    ![Вашей учетной записи интеграции с «Схемы» и новой схемы hello выделен](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a>Изменение схем

1. Выберите hello **схемы** плитки.

2. После hello **схемы** открывает колонку hello выберите схемы, которые должны tooedit.

3. На hello **схемы** колонке выберите **изменить**.

    ![Колонка "Схемы"](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. Файл схемы выберите hello требуется tooedit, затем выберите **откройте**.

    ![Открытие схемы файла tooedit](media/logic-apps-enterprise-integration-schemas/edit-31.png)

Azure отображает сообщение, hello схемы успешно отправлены.

## <a name="delete-schemas"></a>Удаление схем

1. Выберите hello **схемы** плитки.

2. После hello **схемы** открывает колонку, требуется toodelete схемы выберите hello.

3. На hello **схемы** колонке выберите **удалить**.

    ![Колонка "Схемы"](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. tooconfirm, что требуется toodelete hello выбора схемы, выберите **Да**.

    ![Сообщение с подтверждением "Удаление схемы"](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    В hello **схемы** колонке hello схемы список обновляется и больше не включает схему hello удаленного.

    ![Учетная запись интеграции с выделенной плиткой "Схемы"](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a>Дальнейшие действия
* [Дополнительные сведения о hello пакет интеграции Enterprise](logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции enterprise hello").  

