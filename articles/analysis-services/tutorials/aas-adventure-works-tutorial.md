---
title: "Учебник по Adventure Works для служб Azure Analysis Services | Документы Майкрософт"
description: "Здесь представлен учебник по Adventure Works для служб Analysis Services Azure"
services: analysis-services
documentationcenter: 
author: Minewiskan
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
ms.openlocfilehash: 81a378c6b1a15cc240ca30fa19b557312ca54922
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a>Azure Analysis Services — учебник по Adventure Works

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Этот учебник состоит из занятий по созданию и развертыванию табличной модели на уровне совместимости 1400 с помощью [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  

Если ранее вы не работали со службами Analysis Services и табличным моделированием, с помощью этого руководства вы быстро научитесь создавать и развертывать простые табличные модели. После установки всех необходимых компонентов прохождение руководства займет около 2–3 часов.  
  
## <a name="what-you-learn"></a>Что вы узнаете   
  
-   Создание проекта табличной модели на **уровне совместимости 1400** в SSDT.
  
-   Импорт данных из реляционной базы данных в проекте табличной модели.  
  
-   Способы создания связей между таблицами в модели и управления ими.  
  
-   Создание вычисляемых столбцов, мер и ключевых показателей эффективности, помогающих пользователям анализировать критические бизнес-метрики.  
  
-   Создание перспектив и иерархий, которые помогают пользователям просматривать данные в модели, предоставляя точки наблюдения для конкретного бизнеса и приложения, а также управление ими.  
  
-   Создание секций, разбивающих данные таблицы на более мелкие логические части, которые можно обрабатывать независимо от других секций.  
  
-   Защита объектов и данных посредством создания ролей с членами в виде пользователей.  
  
-   Развертывание табличной модели на сервере **служб Azure Analysis Services** или на локальном сервере SQL Server 2017 Analysis Services.  
  
## <a name="prerequisites"></a>Предварительные требования  
Для работы с этим руководством необходимы указанные ниже компоненты.  
  
-   Экземпляр служб Azure Analysis Services или SQL Server 2017 Analysis Services для развертывания модели. Подпишитесь для получения бесплатной [пробной версии служб Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) и [создайте сервер](../analysis-services-create-server.md). Либо зарегистрируйтесь и скачайте [ознакомительную версию для сообщества SQL Server 2017](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp). 

-   Хранилище данных SQL Server или хранилище данных SQL Azure с [примером базы данных AdventureWorksDW2014](http://go.microsoft.com/fwlink/?LinkID=335807). Этот пример базы данных содержит данные, необходимые для работы с настоящим учебником. Скачайте [бесплатные выпуски SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads). Либо зарегистрируйтесь для получения бесплатной [пробной версии базы данных SQL Azure](https://azure.microsoft.com/services/sql-database/). 

    **Важно!** При установке примера базы данных на SQL Server и развертывании модели на сервере служб Azure Analysis Services [локальный шлюз данных](../analysis-services-gateway.md) является обязательным.

-   Последняя версия [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

-   Последняя версия [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).    

-   Клиентское приложение, например [Power BI Desktop](https://powerbi.microsoft.com/desktop/) или Excel. 

## <a name="scenario"></a>Сценарий  
В этом учебнике используется вымышленная компания Adventure Works Cycles. Adventure Works — это большая международная производственная компания, выпускающая и реализующая велосипеды, запчасти и аксессуары для рынков Северной Америки, Европы и Азии. Штат компании насчитывает 500 сотрудников. Кроме того, на Adventure Works работает несколько региональных групп, относящихся к разным ее рынкам сбыта. В рамках проекта вы создадите табличную модель для пользователей, специализирующихся на продажах и маркетинге, чтобы проанализировать в базе данных AdventureWorksDW данные об интернет-продажах.  
  
Это руководство содержит несколько занятий, каждое из которых содержит определенную задачу. Чтобы завершить занятие, вам нужно решить соответствующую задачу. Хотя в определенном занятии может присутствовать несколько задач, дающих схожий результат, решаться они будут несколько разными способами. Такой подход не только помогает понять, что в большинстве случаев есть несколько способов решения определенной задачи, но и стимулирует вас применять полученные ранее знания.  
  
Эти занятия помогут вам создать простую табличную модель с использованием разных функций, доступных в SSDT. Поскольку каждое из занятий основывается на предыдущем, их следует выполнять по порядку.
  
Это руководство не обучает управлению сервером на портале Azure, а также управлению сервером или базой данных с помощью SSMS или клиентского приложения для просмотра данных модели. 


## <a name="lessons"></a>Занятия  
Учебник включает в себя следующие занятия:  
  
|Занятие|Предполагаемое время выполнения|  
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
Эти занятия не требуются для работы с учебником, но могут оказаться полезными при получении более общих сведений о функциях расширенной табличной модели.  
  
|Занятие|Предполагаемое время выполнения|  
|----------|------------------------------|  
|[Строки детализации](../tutorials/aas-supplemental-lesson-detail-rows.md)|10 минут|
|[Динамическая безопасность](../tutorials/aas-supplemental-lesson-dynamic-security.md)|30 минут|
|[Неоднородные иерархии](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|20 минут| 

  
## <a name="next-steps"></a>Дальнейшие действия  
Для начала работы см. [Занятие 1. Создание нового проекта табличной модели](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

