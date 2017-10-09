---
title: "aaaTransform XML с картами XSLT - приложения логики Azure | Документы Microsoft"
description: "Добавление XSLT карты tootransform XML-данных с помощью приложения логики Azure и hello пакет интеграции Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 720e6f988b8542136dfcc402c3c463fcfb2f23cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-maps-for-xml-data-transform"></a>Добавление карт для преобразования данных XML

Enterprise интеграции использует сопоставляет XML-данные tootransform между форматами. Карта представляет XML-документ, который определяет hello данные в документе, который необходимо преобразовать в другой формат. 

## <a name="why-use-maps"></a>Для чего используются карты?

Предположим, что регулярно появление B2B заказов или счетов из клиента, который использует формат YYYMMDD hello для дат. Однако в вашей организации хранить даты в формате MMDDYYY hello. Также можно использовать карту*преобразования* формат даты YYYMMDD hello в hello MMDDYYY перед сохранением в базе данных активности клиентов hello подробности заказа или счета.

## <a name="how-do-i-create-a-map"></a>Как создать карту?

Вы можете создавать проекты интеграции BizTalk с hello [пакет интеграции Enterprise](logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции enterprise hello") для Visual Studio 2015. Затем создайте файл карты интеграции, чтобы визуально сопоставить элементы между двумя XML-файлами схем. После создания этого проекта вы получите документ XSLT.

## <a name="how-do-i-add-a-map"></a>Добавление карты

1. В hello портал Azure, выберите **Обзор**.

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. Введите в поле поиска фильтра hello, **интеграции**, а затем выберите **учетные записи службы интеграции** из списка результатов hello.

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. Выберите счет интеграции hello место tooadd hello карты.

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Выберите hello **Maps** плитки.

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. После открытия колонке hello карты, выберите **добавить**.

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. Введите **имя** карты. карта hello tooupload файла, выберите значок папки hello hello правой части hello **карты** текстовое поле. После завершения процесса передачи hello выберите **ОК**.

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. После Azure добавляет учетной записи интеграции tooyour карты hello, выдается сообщение на экране, показывающий, добавлен ли файл карты. После получения этого сообщения, выберите hello **Maps** плитку, чтобы можно было просматривать hello вновь добавить карты.

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a>Изменение карты

Новый файл карты с hello изменений, которые необходимо передать. Можно сначала загрузить hello карты для редактирования.

tooupload новую карту, которая заменяет существующую карту hello, выполните следующие действия.

1. Выберите hello **Maps** плитки.

2. После открытия колонке hello карты, выберите hello карты, которые должны tooedit.

3. На hello **Maps** колонке выберите **обновление**.

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. В средства выбора файлов hello, выберите файл карты hello требуется tooupload, затем выберите **откройте**.

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a>Как toodelete карты?

1. Выберите hello **Maps** плитки.

2. После открытия колонке hello карты, выберите требуется toodelete карты hello.

3. Щелкните **Удалить**.

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. Подтвердите toodelete hello карты.

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a>Дальнейшие действия
* [Дополнительные сведения о hello пакет интеграции Enterprise](logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции Enterprise")  
* [Узнайте о соглашениях и Пакете интеграции Enterprise](../logic-apps/logic-apps-enterprise-integration-agreements.md "Узнайте о соглашениях и Пакете интеграции Enterprise")  
* [Интеграция Enterprise с преобразованием данных XML](logic-apps-enterprise-integration-transform.md "Интеграция Enterprise с преобразованием данных XML")  

