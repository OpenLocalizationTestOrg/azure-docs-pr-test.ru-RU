---
title: "aaaHow toocreate обращение в службу поддержки для хранилища данных SQL | Документы Microsoft"
description: "Как toocreate поддержка билета в хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: a91d1f53-03cb-464b-9d5b-4a9c1a194ed3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 72f7eac82112fb7f1bfb05abca4ce40aeb3c828c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-support-ticket-for-sql-data-warehouse"></a>Как билета toocreate технической поддержки для хранилища данных SQL
Если у вас возникли проблемы с хранилищем данных SQL, создайте запрос в службу поддержки, чтобы получить помощь от нашей команды разработчиков.

> [!NOTE] 
> Начиная с 12/20/2016 hello проверки работоспособности ресурса в hello портал Azure не является точным. Мы активно работаем toofix эту проблему. 


## <a name="create-a-support-ticket"></a>Создание запроса в службу поддержки
1. Откройте hello [портал Azure][Azure portal].
2. На экране приветствия домашней щелкните hello **Справка и поддержка** плитки.
   
    ![Справка + поддержка](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. Hello Справка + поддержка колонка, щелкните **запрос поддержки создания**.
   
    ![Новый запрос на техническую поддержку](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. Выберите hello **запрос типа**.
   
    ![Тип запроса](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > По умолчанию для каждого экземпляра SQL Server (например, myserver.database.windows.net) предусмотрена следующая **квота на DTU**: 45 000. Эта квота является просто ограничением для безопасности. Можно увеличить квоту, создав запрос в службу поддержки и выбрав *квоты* как тип запроса hello. toocalculate вашей DTU умножьте hello 7.5 с hello общее [DWU] [ DWU] необходимости. Например, вы хотите toohost двух DW6000s на один сервер SQL server, то следует запросить квоту DTU 90,000.  Можно просмотреть вашего текущего потребления DTU в колонке сервера SQL hello hello портала. Приостановлен, Отмена приостановленных баз данных учитываются hello Квота DTU. 
   > 
   > 
5. Выберите hello **подписки** Здравствуйте, узлы, базы данных с ошибкой hello, вы сообщаете.
   
    ![Подписки](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. Выберите **хранилище данных SQL** как hello ресурсов.
   
    ![Ресурс](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. Выберите свой [план поддержки Azure][Azure support plan].
   
   * **вопросам, связанным с выставлением счетов, квотами и управлением подпиской** , доступна на всех уровнях.
   * Поддержка по **замене или ремонту** обеспечивается на уровнях [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] и [Premier][Premier]. Устранения неполадок возникли неполадки, из-за клиентов при использовании Azure там, где имеется проблема оправданное предположение, вызвавшего Microsoft hello.
   * **Разработчик обучения** и **советы по службами** можно найти по адресу hello [Professional Direct] [ Professional Direct] и [Premier] [ Premier] уровней поддержки. 
     
     Если у вас есть Premier support плана, отчет можно также хранилище данных SQL проблем на hello [портал Microsoft Premier online][Microsoft Premier online portal].  В разделе [планами поддержки Azure] [ Azure support plan] toolearn Дополнительные сведения о различных поддержки схем, включая области, время цен, ответа hello и т. д.  Часто задаваемые вопросы о поддержке Azure см. на [этой странице][Azure support FAQs].  
     
     ![План поддержки](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. Выберите hello **тип проблемы** и **категории**. В этом примере мы выбрали hello тип проблемы «средства» и «Клиентские средства» как категория hello. 
   
    ![Категория типов проблем](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. Опишите проблему hello и выбрать уровень hello влияние на бизнес.
   
    ![Описание проблемы](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. Ваши **контактные данные** для этого запроса в службу поддержки будут заполнены предварительно. При необходимости обновите их.
    
    ![Контактные данные](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. Нажмите кнопку **создать** запроса на поддержку toosubmit hello.

## <a name="monitor-a-support-ticket"></a>Мониторинг запроса в службу поддержки
После отправки запроса на поддержку hello hello Azure поддержки свяжется с вами. toocheck состояние запроса и сведения, нажмите кнопку **запросов поддержки управление** на панели мониторинга hello.

![Проверка состояния](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a>Другие ресурсы
Кроме того, можно подключиться, используя hello сообщества хранилище данных SQL на [переполнения стека] [ Stack Overflow] или на hello [форум MSDN хранилища данных SQL Azure] [ Azure SQL Data Warehouse MSDN forum].

<!--Image references--> 

<!--Article references--> 
[DWU]: ./sql-data-warehouse-overview-what-is.md

<!--MSDN references--> 

<!--Other web references--> 
[Azure portal]: https://portal.azure.com/
[Azure support plan]: https://azure.microsoft.com/support/plans/?WT.mc_id=Support_Plan_510979/  
[Developer]: https://azure.microsoft.com/support/plans/developer/  
[Standard]: https://azure.microsoft.com/support/plans/standard/  
[Professional Direct]: https://azure.microsoft.com/support/plans/prodirect/  
[Premier]: https://azure.microsoft.com/support/plans/premier/  
[Azure support FAQs]: https://azure.microsoft.com/support/faq/
[Microsoft Premier online portal]: https://premier.microsoft.com/
[Stack Overflow]: https://stackoverflow.com/questions/tagged/azure-sqldw/
[Azure SQL Data Warehouse MSDN forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse/

