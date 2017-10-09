---
title: "aaaCreate табличной модели с помощью конструктора веб-Azure Analysis Services hello | Документы Microsoft"
description: "Узнайте, как toocreate табличной модели служб Azure Analysis Services с помощью hello Web designer на портале Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: a37b326b76c84fc3a4300827bc1c8706b0584701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-model-in-azure-portal"></a>Создание модели на портале Azure

Hello Azure Analysis Services web designer (Предварительная версия) на портале Azure дает toocreate легко и быстро и редактирование табличных моделей и запрос модели данных прямо в браузере. 

Помните, является веб-дизайнера hello **предварительной версии**. Во время добавления новых функций все время hello, во время предварительного просмотра ограничена функциональные возможности. Для более сложных модель разработки и тестирования это лучший toouse Visual Studio (SSDT) и SQL Server Management Studio (SSMS).

## <a name="prerequisites"></a>Предварительные требования

- Сервер служб Analysis Services Azure на уровне Standard или разработчика hello. Новые модели, созданные с помощью веб-дизайнера hello, DirectQuery, поддерживаемое только эти уровни.
- База данных SQL Azure, хранилище данных SQL Azure или PBIX-файл Power BI Desktop в качестве источника данных. Новые модели, созданные из файлов Power BI Desktop, поддерживают в качестве источников данных Базу данных SQL Azure, хранилище данных SQL Azure, Oracle и Teradata.
- Учетная запись SQL Server и пароль для подключения tooAzure источники данных базы данных SQL или хранилище данных SQL Azure.

## <a name="toocreate-a-new-tabular-model"></a>toocreate новой табличной модели

1. В колонке сервера **Обзор** выберите **Web designer** (Конструктор веб-приложений) и нажмите кнопку **Открыть**.

    ![Создание модели на портале Azure](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. Выбрав **Web designer** (Конструктор веб-приложений)  >  **Модели**, нажмите кнопку **+ Добавить**.

    ![Создание модели на портале Azure](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. В диалоговом окне **Новая модель** введите имя модели и выберите источник данных.

    ![Диалоговое окно "Новая модель" на портале Azure](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. В **Connect**, введите hello свойства соединения. Необходимо указать имя пользователя и пароль учетной записи SQL Server.

     ![Диалоговое окно "Подключение" на портале Azure](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. В **таблиц и представлений**, выберите tooinclude hello таблиц в модели и нажмите кнопку **создать**. Связи между таблицами создаются автоматически с помощью пары ключей.

     ![Выбор таблиц и представлений](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

Новая модель отобразится в браузере. На данном этапе можно сделать следующее:   

- Запрос данных модели, перетаскивая поля конструктор запросов toohello и добавления фильтров.
- Создавать новые меры в таблицах.
- Изменение метаданных модели с помощью редактора json hello.
- Откройте модель hello в Visual Studio (SSDT), Power BI Desktop или Excel.

![Выбор таблиц и представлений](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> При попытке создать новые меры в браузере или изменить метаданные модели, модели tooyour эти изменения сохраняются в Azure. Если вы также работаете с моделью в SSDT, Power BI Desktop или Excel, то она может оказаться несинхронизированной.


## <a name="next-steps"></a>Дальнейшие действия 
[Управление ролями и пользователями базы данных](analysis-services-database-users.md)  
[Подключение с помощью Excel](analysis-services-connect-excel.md)  


