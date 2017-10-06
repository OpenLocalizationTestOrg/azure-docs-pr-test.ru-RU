---
title: "aaaConvert XML-данных с преобразованиями - приложения логики Azure | Документы Microsoft"
description: "Создание преобразования или mapps tooconvert XML-данные между форматами в приложениях для логики с помощью hello SDK интеграции Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: b56ec1072c5058d3aefc7f88ac9b2748ebe56456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a>Интеграция Enterprise с преобразованием данных XML
## <a name="overview"></a>Обзор
Соединитель преобразования интеграции Enterprise Hello преобразует данные из одного формата tooanother формат. Например имеется входящее сообщение, которое содержит текущую дату в формате YearMonthDay hello hello. Можно использовать преобразование tooreformat hello даты toobe в формате MonthDayYear hello.

## <a name="what-does-a-transform-do"></a>Что делает преобразование?
Преобразования, который также называется карты, состоит из источника XML-схемы (hello входных данных) и целевой XML-схемы (hello выходных данных). Можно использовать различные встроенные функции toohelp управления или управления hello данных, включая обработку строк, условного назначения, арифметические выражения, модули форматирования даты времени и даже циклические конструкции.

## <a name="how-toocreate-a-transform"></a>Как toocreate преобразование?
Преобразование или карты можно создать с помощью Visual Studio hello [SDK интеграции Enterprise](https://aka.ms/vsmapsandschemas). После завершения создания и тестирования hello преобразования, преобразования hello загрузки в вашей учетной записи интеграции. 

## <a name="how-toouse-a-transform"></a>Как toouse преобразования
После преобразования hello/map передать в учетную запись интеграции, его можно использовать toocreate приложения логики. приложение Hello логика выполняет преобразования всякий раз, когда запускается приложение hello логики (существует входного содержимого, которое требуется преобразовать toobe).

**Ниже приведены шаги toouse hello преобразования**:

### <a name="prerequisites"></a>Предварительные требования

* Создайте учетную запись интеграции и добавьте tooit карты  

Теперь, когда вы занимается hello предварительные требования, это время toocreate логику приложения:  

1. Создание приложения логики и [связать его учетной записи интеграции tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md "узнать toolink tooa логики интеграции учетной записи приложения") , содержащий hello карты.
2. Добавить **запроса** приложения логики триггера tooyour  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. Добавить hello **преобразование XML** действия путем выбора **добавить действие**   
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. Введите слово hello *преобразование* в toofilter поле поиска hello все hello один toohello действия, которые должны toouse  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. Выберите hello **преобразование XML** действие   
6. Добавить hello XML **СОДЕРЖИМОГО** , необходимо преобразование. Можно использовать любой XML-данных, появляется в запросе hello HTTP как hello **СОДЕРЖИМОГО**. В этом примере выберите текст hello hello HTTP-запроса, запустившего приложение hello логику.
7. Выберите hello имя hello **КАРТЫ** нужных toouse tooperform hello преобразования. карта Hello должен быть в вашей учетной записи интеграции. На предыдущем шаге вы дали уже учетной интеграции tooyour доступа логики приложения, содержащий схему.      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. Сохраните результаты своих действий.  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

На этом настройка карты завершена. В реальных приложениях вы можете toostore hello преобразования данных в бизнес-приложения, таких как SalesForce. Можно легко, как выходные данные hello toosend действие hello преобразовывать tooSalesforce. 

Теперь можно проверить преобразование, делая конечную точку HTTP toohello запроса.  

## <a name="features-and-use-cases"></a>Функции и варианты использования
* Преобразование Hello, созданные на карте могут быть простыми, например для копирования из одного документа tooanother имя и адрес. Также можно создавать более сложные преобразования, использование операций сопоставления out of box hello.  
* Многие операции или функции сопоставления легко доступны, включая строки, функции даты-времени и пр.  
* Это можно сделать копию прямой данных между схемами hello. В hello сопоставления, включенный в пакет SDK для hello это просто рисования линии, соединяющей hello элементов в исходной схеме hello их аналогами в целевой схеме hello.  
* При создании карты, можно просмотреть графическое представление hello карты, которая показывает все отношения hello и ссылки, создаваемые вами.
* Используйте tooadd функции hello тестового сопоставления пример XML-сообщения. С одним щелчком мыши можно проверить hello карты вы создали и увидеть результаты созданных hello.  
* Передача существующих карт  
* Включает поддержку hello XML-формате.

## <a name="learn-more"></a>Подробнее
* [Дополнительные сведения о hello пакет интеграции Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции Enterprise")  
* [Узнайте больше о картах](../logic-apps/logic-apps-enterprise-integration-maps.md "Узнайте о картах интеграции Enterprise")  

