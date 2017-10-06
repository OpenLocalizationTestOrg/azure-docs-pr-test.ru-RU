---
title: "уровень совместимости модели aaaData в Azure Analysis Services | Документы Microsoft"
description: "Основные сведения об уровне совместимости табличной модели данных."
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
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Уровень совместимости табличных моделей Analysis Services

*Уровень совместимости* ссылается toorelease поведения в hello ядро служб Analysis Services. Уровень совместимости toohello изменения обычно совпадают с основные выпуски SQL Server. Эти изменения также реализованы в Azure Analysis Services toomaintain четность между обеих платформах. Изменения уровня совместимости также влияют на функции, доступные в табличных моделях. Например DirectQuery и метаданные табличных объектов имеют разные реализации в зависимости от уровня совместимости hello. 

Azure службы Analysis Services поддерживают табличные модели с уровнем совместимости hello 1200 и 1400.

Последний уровень совместимости Hello — 1400. Этот уровень совпадает с уровнем SQL Server 2017 Analysis Services. Основные функции на уровне совместимости 1400 hello:

*  Новая инфраструктура подключения к данным и импорта в табличные модели с поддержкой интерфейсов API TOM и сценариев TMSL. Эта новая функция обеспечивает поддержку дополнительных источников данных, таких как хранилище BLOB-объектов Azure.
*  Возможности преобразования и комбинирования данных с помощью выражений Get Data и M.
*  Меры поддерживают свойство "Строки детализации" с использованием выражения DAX. Это свойство включает клиентские средства, как Microsoft Excel toodrill вниз toodetailed данные из объединенного отчета. Например при просмотре общий объем продаж по региону и месяц, они могут просматривать связанные hello подробности заказа. 
*  Безопасность на уровне объекта для таблицы и столбца имен, кроме toohello содержащихся в них данных.
*  Расширенная поддержка несбалансированных иерархий.
*  Усовершенствованный мониторинг и повышение производительности.
  
## <a name="set-compatibility-level"></a>Установка уровня совместимости 
 При создании нового проекта табличной модели в SSDT, вы можете указать уровень совместимости hello на hello **конструктор табличных моделей** диалогового окна. 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 При выборе hello **больше не показывать это сообщение** , во всех последующих проектах использовать указанное по умолчанию hello уровень совместимости hello. Можно изменить уровень совместимости по умолчанию hello в SSDT в **средства** > **параметры**.  
  
 tooupgrade существующего проекта табличной модели в SSDT, набор hello **уровень совместимости** свойства в модели hello **свойства** окна. Имейте в виду, обновление уровня совместимости hello является необратимым.
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a>Проверка уровня совместимости базы данных табличной модели в SQL Server Management Studio 
 В среде SSMS щелкните правой кнопкой мыши имя базы данных hello > **свойства** > **уровень совместимости**.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>Проверка поддерживаемого уровня совместимости сервера в SSMS  
 В среде SSMS щелкните правой кнопкой мыши имя сервера hello > **свойства** > **поддерживаемый уровень совместимости**.  
  
 Это свойство указывает hello наивысший уровень совместимости базы данных, которая будет выполняться на сервере hello (без предварительной версии). Невозможно изменить уровень совместимости Hello поддерживается.  

## <a name="next-steps"></a>Дальнейшие действия
  [Создание модели на портале Azure](analysis-services-create-model-portal.md)   
  [Управление службами Analysis Services](analysis-services-manage.md)  
