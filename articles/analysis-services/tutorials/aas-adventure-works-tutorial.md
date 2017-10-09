---
title: "AAA» служб Azure Analysis Services Adventure Works учебника | Документы Microsoft»"
description: "Предоставляет учебник hello Adventure Works для Azure Analysis Services"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 2df8b3ab4e8c4ffbe0086418d60fd2e2abd35e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a>Azure Analysis Services — учебник по Adventure Works

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

О том, как в этом учебнике содержатся занятия toocreate и развертывание с помощью табличной модели на уровне совместимости hello 1400 [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  

Если вы новые службы tooAnalysis и табличного моделирования, изучения этого учебника является быстрым способом toolearn hello как toocreate и развертывание табличной модели. При наличии необходимых компонентов hello в месте, он должен принимать между двумя toocomplete toothree часов.  
  
## <a name="what-you-learn"></a>Что вы узнаете   
  
-   Как toocreate новой табличной модели проекта в hello **уровень совместимости 1400** в SSDT.
  
-   Как tooimport данных из реляционной базы данных в проект табличной модели.  
  
-   Как toocreate связей между таблицами в модели hello и управление ими.  
  
-   Как toocreate вычисляемые столбцы, меры и ключевые индикаторы производительности, которые помогут пользователям анализировать показатели критически важные для бизнеса.  
  
-   Как toocreate и управление перспективами и иерархиями, которые помогут пользователям более легко просматривать данные модели, предоставляя бизнеса и точки зрения конкретного приложения.  
  
-   Как toocreate секций, разделяющих табличные данные на более мелкие логические части, которые могут быть обработаны независимо от других секций.  
  
-   Как toosecure модели объектов и данных путем создания ролей с членами пользователя.  
  
-   Как toodeploy tooan табличной модели **Azure Analysis Services** сервера или локального сервера служб Analysis Services SQL Server 2017 г.  
  
## <a name="prerequisites"></a>Предварительные требования  
toocomplete этого учебника, необходимо:  
  
-   Azure Analysis Services или служб аналитики SQL Server 2017 г экземпляра toodeploy для модели. Подпишитесь для получения бесплатной [пробной версии служб Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) и [создайте сервер](../analysis-services-create-server.md). Либо зарегистрируйтесь и скачайте [ознакомительную версию для сообщества SQL Server 2017](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp). 

-   Хранилище данных SQL Server или хранилище данных SQL Azure с hello [AdventureWorksDW2014 образца базы данных](http://go.microsoft.com/fwlink/?LinkID=335807). Этот образец базы данных включает в себя необходимые toocomplete hello данных этого учебника. Скачайте [бесплатные выпуски SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads). Либо зарегистрируйтесь для получения бесплатной [пробной версии базы данных SQL Azure](https://azure.microsoft.com/services/sql-database/). 

    **Важно:** при установке образца hello базы данных на локальном сервере SQL, и развертывание сервера служб Analysis Services Azure tooan модели, [локального шлюза данных](../analysis-services-gateway.md) является обязательным.

-   Hello последнюю версию [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

-   Hello последнюю версию [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).    

-   Клиентское приложение, например [Power BI Desktop](https://powerbi.microsoft.com/desktop/) или Excel. 

## <a name="scenario"></a>Сценарий  
В этом учебнике используется вымышленная компания Adventure Works Cycles. Adventure Works — это большой, многонациональная производственная компания, производящая и реализующая велосипедов, элементы и стандартные toocommercial рынках Северной Америки, Европы и Азии. ней работают 500 сотрудников компании Hello. Кроме того, на Adventure Works работает несколько региональных групп, относящихся к разным ее рынкам сбыта. Проект является toocreate табличную модель для пользователей, отделов продаж и маркетинга tooanalyze данных Интернет-продаж в базы данных AdventureWorksDW hello.  
  
toocomplete hello учебника, необходимо выполнить различные занятий. каждое из которых содержит определенную задачу. Выполнение каждой задачи в порядке является обязательным для завершения занятия hello. Хотя в определенном занятии может присутствовать несколько задач, дающих схожий результат, решаться они будут несколько разными способами. В этом показан метод часто больше, чем один из способов toocomplete задачи и toochallenge, можно использовать навыки вы узнали в предыдущих уроках и задачах.  
  
Hello занятий hello предназначен tooguide через создание простой табличной модели с использованием разных функций hello включены в SSDT. Поскольку каждое занятие строится на предыдущем занятии hello, следует выполнить hello по порядку.
  
Этот учебник не предоставляет уроки по управлению сервером на портале Azure, управление сервера или базы данных с помощью SSMS или с помощью клиента приложения toobrowse модели данных. 


## <a name="lessons"></a>Занятия  
Этот учебник содержит следующие занятия hello:  
  
|Занятие|Предполагаемое время toocomplete|  
|----------|------------------------------|  
|[1. Создание проекта табличной модели](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|10 минут|  
|[2. Получение данных](../tutorials/aas-lesson-2-get-data.md)|10 минут|  
|[3. Обозначение таблицы дат](../tutorials/aas-lesson-3-mark-as-date-table.md)|3 минуты|  
|[4. Создание связей](../tutorials/aas-lesson-4-create-relationships.md)|10 минут|  
|[5. Создание вычисляемых столбцов](../tutorials/aas-lesson-5-create-calculated-columns.md)|15 минут|
|[6. Создание мер](../tutorials/aas-lesson-6-create-measures.md)|30 минут|  
|[7. Создание ключевых показателей эффективности (KPI)](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|15 минут|  
|[8. Создание перспектив](../tutorials/aas-lesson-8-create-perspectives.md)|5 мин|  
|[9. Создание иерархий](../tutorials/aas-lesson-9-create-hierarchies.md)|20 минут|  
|[10. Создание секций](../tutorials/aas-lesson-10-create-partitions.md)|15 минут|  
|[11. Создание ролей](../tutorials/aas-lesson-11-create-roles.md)|15 минут|  
|[12. Анализ в Excel](../tutorials/aas-lesson-12-analyze-in-excel.md)|5 мин| 
|[13. Развертывание](../tutorials/aas-lesson-13-deploy.md)|5 мин|  
  
## <a name="supplemental-lessons"></a>Дополнительные занятия  
Эти занятия не требуется toocomplete hello учебника, но могут быть полезны для улучшения понимания расширенной табличной моделью функции.  
  
|Занятие|Предполагаемое время toocomplete|  
|----------|------------------------------|  
|[Строки детализации](../tutorials/aas-supplemental-lesson-detail-rows.md)|10 минут|
|[Динамическая безопасность](../tutorials/aas-supplemental-lesson-dynamic-security.md)|30 минут|
|[Неоднородные иерархии](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|20 минут| 

  
## <a name="next-steps"></a>Дальнейшие действия  
tooget работы см. в разделе [занятия 1: Создание нового проекта табличной модели](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

