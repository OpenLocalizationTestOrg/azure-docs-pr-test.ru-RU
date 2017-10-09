---
title: "aaaMonitor Azure Cosmos DB запросов и хранения | Документы Microsoft"
description: "Узнайте, как toomonitor базы данных Azure Cosmos учетной записи для метрики производительности, такие как запросы и ошибки сервера и использования метрик, таких как использование хранилища."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 4c6a2e6f-6e78-48e3-8dc6-f4498b235a9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: mimig
ms.openlocfilehash: aea029d10717236a573a080dab9d06d87f97f318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-cosmos-db-requests-usage-and-storage"></a>Мониторинг запросов, использования и хранилища Azure Cosmos DB
Можно наблюдать за своими учетными записями Azure Cosmos DB hello [портал Azure](https://portal.azure.com/). Для каждой учетной записи Azure Cosmos DB доступны метрики производительности, такие как запросы и ошибки сервера, и использования, например потребление памяти.

Метрики можно просмотреть в колонке hello учетной записи, Новая колонка метрики hello, или в мониторе Azure.

## <a name="view-performance-metrics-on-hello-metrics-blade"></a>Просмотр метрик производительности в колонке метрики hello
1. В hello [портал Azure](https://portal.azure.com/), нажмите кнопку **более служб**, прокрутите слишком**баз данных**, нажмите кнопку **Azure Cosmos DB**и щелкните имя hello hello Cosmos DB учетная запись Azure для которого вы хотите tooview метрики производительности.
2. В меню hello ресурсов в разделе **мониторинг**, нажмите кнопку **метрики**.

открывается колонка метрики Hello и выборе tooreview коллекции hello. Можно просмотреть метрики доступности, запросы, пропускной способности и хранения и сравнить их Cosmos DB toohello Azure соглашений об уровне обслуживания.

## <a name="view-performance-metrics-by-using-azure-monitoring"></a>Просмотр метрик производительности с помощью Azure Monitor
1. В hello [портал Azure](https://portal.azure.com/), нажмите кнопку **монитор** на hello Jumpbar.
2. В меню ресурса hello, щелкните **метрики**.
3. В hello **монитор — метрики** окна в hello **группы ресурсов** раскрывающееся меню, выберите hello группы ресурсов, связанных с учетной записью Azure Cosmos DB hello, что хотелось бы toomonitor. 
4. В hello **ресурсов** раскрывающееся меню, toomonitor учетной записи базы данных выберите hello.
5. В списке hello **доступные метрики**, выберите toodisplay метрики hello. Используйте кнопку CTRL hello, toomulti выбор. 

    Показатели отображаются на в hello **построения** окна. 

## <a name="view-performance-metrics-on-hello-account-blade"></a>Просмотр метрик производительности в колонке hello учетной записи
1. В hello [портал Azure](https://portal.azure.com/), нажмите кнопку **более служб**, прокрутите слишком**баз данных**, нажмите кнопку **Azure Cosmos DB**и щелкните имя hello hello Cosmos DB учетная запись Azure для которого вы хотите tooview метрики производительности.
2. Hello **мониторинг** следить за состоянием отображаются следующие плитки, по умолчанию hello:
   
   * Общее количество запросов для hello текущего дня.
   * Используемое хранилище.
   
   Если таблица отображает **нет доступных данных** и вы уверены, есть данные в базе данных см. в разделе hello [Устранение неполадок](#troubleshooting) раздела.
   
   ![Снимок экрана: hello мониторинг следить за состоянием hello запросов и использования хранилища hello](./media/monitor-accounts/documentdb-total-requests-and-usage.png)
3. Щелкнув hello **запросов** или **квоты на использование** плитки открывает подробные **метрика** колонку.
4. Hello **метрика** колонке показывает сведения о выбранных метрики hello.  Hello верхней части колонки hello является запросов на диаграмме каждый час, диаграммы и ниже, является таблица, показывающая статистической обработки значений для регулируемой, общее число запросов.  Hello колонка метрики также показывает список предупреждений, которым были определено, отфильтрованный toohello метрики, которые отображаются на текущей колонка метрики hello hello (таким образом, если у вас есть ряд предупреждений, остаются только те hello соответствующие из них, представленные здесь).   
   
   ![Снимок экрана: колонка метрики hello, включая регулирование запросов](./media/monitor-accounts/documentdb-metric-blade.png)

## <a name="customize-performance-metric-views-in-hello-portal"></a>Настройка представлений метрики производительности в портал hello
1. toocustomize hello метрик, отображаемых в конкретной диаграммы, щелкните диаграмму tooopen hello в hello **метрика** и, при необходимости нажмите кнопку **изменение диаграммы**.  
   ![Снимок экрана: колонка метрики hello элементов управления, с выделенной изменение диаграммы](./media/monitor-accounts/madocdb3.png)
2. На hello **изменить диаграмму** колонке предусмотрены параметры toomodify hello метрики, которые отображаются в диаграмме hello, а также их диапазон времени.  
   ![Снимок экрана: колонка изменить диаграмму hello](./media/monitor-accounts/madocdb4.png)
3. toochange метрик hello, отображаемых в части «hello», просто выберите или очистите hello доступные метрики производительности и нажмите кнопку **ОК** hello нижней части колонки hello.  
4. toochange hello временной диапазон, выберите другой диапазон (например, **настраиваемый**) и нажмите кнопку **ОК** hello нижней части колонки hello.  
   
   ![Снимок hello диапазон времени части колонки отображение hello изменить диаграмму как tooenter заданного интервала времени](./media/monitor-accounts/madocdb5.png)

## <a name="create-side-by-side-charts-in-hello-portal"></a>Создание диаграмм side-by-side hello портала
Hello Azure портал позволяет toocreate side-by-side метрики диаграммы.  

1. Во-первых, щелкните правой кнопкой мыши на диаграмме hello toocopy и выберите **Настройка**.
   
   ![Снимок экрана: hello диаграммы общее количество запросов с параметром Настройка hello выделен](./media/monitor-accounts/madocdb6.png)
2. Нажмите кнопку **клон** hello часть hello toocopy меню и нажмите кнопку **выполняется настройка**.
   
   ![Экран снимок диаграммы hello общее количество запросов с hello клонирования и выполняется настройка параметров выделен](./media/monitor-accounts/madocdb7.png)  

Теперь может обрабатывать эту часть как других метрик частей, Настройка hello метрик и временной диапазон, в части hello.  Таким образом, можно увидеть два различных показателей диаграммы side-by-side на hello то же время.  
    ![Общее количество запросов диаграммы hello снимок экрана и hello новое общее количество запросов за час диаграммы](./media/monitor-accounts/madocdb8.png)  

## <a name="set-up-alerts-in-hello-portal"></a>Настройка оповещений в портале hello
1. В hello [портал Azure](https://portal.azure.com/), нажмите кнопку **более служб**, нажмите кнопку **Azure Cosmos DB**и щелкните имя учетной записи Azure Cosmos DB hello, для которого вы хотите toosetup hello предупреждения для метрики производительности.
2. В hello ресурсов меню выберите **правила оповещения** tooopen hello правила оповещения колонку.  
   ![Снимок экрана: hello предупреждение правила выделенный фрагмент](./media/monitor-accounts/madocdb10.5.png)
3. В hello **предупреждения правила** колонка, щелкните **добавить оповещение**.  
   ![Снимок экрана: колонка hello правила оповещений, с выделенной кнопкой на Добавление оповещения hello](./media/monitor-accounts/madocdb11.png)
4. В hello **Добавление правила оповещения** колонки, укажите:
   
   * Имя Hello hello правило оповещения, которые вы настраиваете.
   * Описание hello новое правило оповещения.
   * Hello метрики для правила оповещения hello.
   * Hello условие, пороговое значение и период, определяющие при активации оповещения hello. Например ошибка сервера счетчика больше 5 через hello последние 15 минут.
   * Является ли Здравствуйте, администратор службы и coadministrators являются уведомления по электронной почте при выводе предупреждения hello.
   * дополнительные адреса для оповещений электронной почты.  
     ![Снимок экрана: hello добавить колонку правило генерации оповещений](./media/monitor-accounts/madocdb12.png)

## <a name="monitor-azure-cosmos-db-programatically"></a>Программный мониторинг Azure Cosmos DB
Здравствуйте метрик уровня учетная запись доступна на портале hello, например учетной записи хранилища использования и общее количество запросов, не доступны через интерфейсы API DocumentDB hello. Тем не менее можно получить данные об использовании на уровне коллекции hello с помощью hello интерфейсы API DocumentDB. tooretrieve коллекции данных на уровне, hello следующие:

* hello toouse REST API [выполнение метода GET на коллекцию hello](https://msdn.microsoft.com/library/mt489073.aspx). Hello квоты и сведения об использовании коллекции hello возвращается в заголовки x-ms-resource-quota и x-ms-resource-usage hello в ответ hello.
* hello toouse .NET SDK, используйте hello [DocumentClient.ReadDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.readdocumentcollectionasync.aspx) метод, возвращающий [ResourceResponse](https://msdn.microsoft.com/library/dn799209.aspx) , такие как содержит ряд свойств использования  **CollectionSizeUsage**, **DatabaseUsage**, **DocumentUsage**и многое другое.

tooaccess дополнительные метрики, использовать hello [Azure SDK монитор](https://www.nuget.org/packages/Microsoft.Azure.Insights). Доступные определения метрик можно получить с помощью следующего вызова.

    https://management.azure.com/subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metricDefinitions?api-version=2015-04-08

Запросы tooretrieve отдельных показателей использования hello следующий формат:

    https://management.azure.com/subscriptions/{SubecriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metrics?api-version=2015-04-08&$filter=%28name.value%20eq%20%27Total%20Requests%27%29%20and%20timeGrain%20eq%20duration%27PT5M%27%20and%20startTime%20eq%202016-06-03T03%3A26%3A00.0000000Z%20and%20endTime%20eq%202016-06-10T03%3A26%3A00.0000000Z

Дополнительные сведения см. в разделе [Получение метрик ресурсов через API REST Azure монитор hello](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/02/23/retrieving-resource-metrics-via-the-azure-insights-api/). Обратите внимание, что служба Azure Inights была переименована в Azure Monitor.  Запись в блоге относится имя старой toohello.

## <a name="troubleshooting"></a>Устранение неполадок
Если наблюдение плитки приветствия отображения **нет доступных данных** сообщение и недавно внесенные запросы или добавлены toohello базу данных, можно изменить последних использования tooreflect плитки приветствия hello.

### <a name="edit-a-tile-toorefresh-current-data"></a>Изменить текущие данные с toorefresh плитки
1. toocustomize hello метрик, отображаемых в определенной области, щелкните hello диаграммы tooopen hello **метрика** и, при необходимости нажмите кнопку **изменить диаграмму**.  
   ![Снимок экрана: колонка метрики hello элементов управления, с выделенной изменение диаграммы](./media/monitor-accounts/madocdb3.png)
2. На hello **изменить диаграмму** колонки в hello **диапазон времени** щелкните **за последний час**, а затем нажмите кнопку **ОК**.  
   ![Снимок экрана: колонка hello изменить диаграмму с выбран последний час](./media/monitor-accounts/documentdb-no-available-data-past-hour.png)
3. Элемент должен обновиться: теперь в нем должны отображаться текущие данные и сведения об использовании.  
   ![Hello обновить снимок экрана общее число запросов за час плитки](./media/monitor-accounts/documentdb-no-available-data-fixed.png)

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о базе данных Azure Cosmos планирования емкости, в разделе hello [калькулятора планировщик Azure Cosmos DB емкость](https://www.documentdb.com/capacityplanner).

