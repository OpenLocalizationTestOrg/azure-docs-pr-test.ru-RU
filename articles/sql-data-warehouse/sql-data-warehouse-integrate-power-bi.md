---
title: "aaaUse Power BI с хранилищем данных SQL | Документы Microsoft"
description: "Советы по использованию Power BI с хранилищем данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a>Использование Power BI с хранилищем данных SQL
Как и в базе данных SQL Azure SQL хранилища прямого подключения к данным позволяет пользователя tooleverage мощные логических Включение наряду с hello аналитических возможностей Power BI.  При использовании Direct Connect запросы отправляются назад tooyour хранилище данных SQL Azure в реальном времени при просмотре данных hello.  Это, в сочетании с hello масштабирования хранилища данных SQL, позволяет пользователям toocreate динамических отчетов в минутах терабайтов данных.  Кроме того, пользователи hello появлением Привет открыть в Power BI кнопку toodirectly подключения Power BI tootheir хранилище данных SQL не собирая сведения из других частей Azure.

При использовании прямого соединения следует обратить внимание на следующее.

* Укажите hello полное имя сервера, при подключении (см. ниже дополнительные сведения)
* Убедитесь, правила брандмауэра для базы данных hello настроены слишком «разрешать доступ tooAzure служб».
* Каждое действие, например Выбор столбца или Добавление фильтра, отправляет запрос непосредственно hello хранилища данных
* Плитки обновляются примерно каждые 15 минут, (обновления не требуются toobe запланировано)
* Раздел вопросов и ответов недоступен для наборов данных прямого соединения.
* Изменения схемы не выбираются автоматически.
* Время ожидания любых запросов на прямое соединение истекает через две минуты.

Эти ограничения и примечания может измениться по мере возможности tooimprove hello. Ниже описаны шаги tooconnect Hello.  

## <a name="using-hello-open-in-power-bi-button"></a>С помощью кнопки «Открыть в Power BI» hello
toomove простым способом Hello между хранилищем данных SQL и Power BI — с Привет открыть в Power BI кнопку. Эта кнопка позволяет tooseamlessly начать создание новых панелей мониторинга в Power BI.  

1. tooget работы перейдите tooyour экземпляр хранилища данных SQL в hello классический портал Azure.
2. Нажмите кнопку «Открыть в Power BI» hello.
3. Если мы не может toosign в напрямую, или если у вас учетная запись Power BI, вам потребуется в toosign.  
4. Вы будете направлены подставлен toohello страницы подключения хранилища данных SQL, hello данными с хранилищем данных SQL.
5. После ввода учетных данных будет полностью соединенными tooyour хранилище данных SQL.

## <a name="connecting-through-hello-power-bi-portal"></a>Подключение через портал hello Power BI
В добавление toousing Привет открыть кнопку Power BI пользователи также могут подключаться tootheir хранилище данных SQL через hello портале Power BI.

1. Нажмите кнопку «Получить данные» hello нижней части панели навигации hello.
2. Выберите «Базы данных».
3. Один раз на странице приветствия базами данных, выберите «Хранилище данных SQL Azure» и нажмите кнопку «Подключиться».
4. Введите hello необходимые сведения о подключении.  Имя сервера и имя базы данных можно найти в hello портала Azure.
5. Вы будете перенаправлены обратно с именем hello экземпляра появится toohello главной странице Power BI, а после подключения к новой записи в разделе «Наборы данных».  
6. Можно щелкнуть на новый набор данных tooexplore hello все hello таблиц и представлений в базе данных. При выборе столбца будет отправлено назад toohello источника запроса, динамически создается визуальный. Эти визуальные элементы можно сохранить в новом отчете и закрепить tooyour панели мониторинга.

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
