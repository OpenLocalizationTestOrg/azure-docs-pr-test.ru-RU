---
title: "aaaUse Azure Stream Analytics с хранилищем данных SQL | Документы Microsoft"
description: "Советы по использованию службы Azure Stream Analytics и хранилища данных SQL для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a>Работа со службой Azure Stream Analytics и хранилищем данных SQL
Azure Stream Analytics является полностью управляемой службы, предоставляя обработки сложных событий низкой задержкой, высокодоступные и масштабируемые потоковой передаче данных в облаке hello. Вы можете изучить основы hello, чтении [tooAzure введение Stream Analytics][Introduction tooAzure Stream Analytics]. Затем можно узнать, как hello toocreate решения конца в конец с Stream Analytics, следуя [приступить к использованию Azure Stream Analytics] [ Get started using Azure Stream Analytics] учебника.

В этой статье вы узнаете, как toouse хранилище данных SQL Azure базы данных в качестве приемника выходных данных для заданий Analytics поток данных.

## <a name="prerequisites"></a>Предварительные требования
Во-первых, выполните следующие шаги в hello hello [приступить к использованию Azure Stream Analytics] [ Get started using Azure Stream Analytics] учебника.  

1. Создание ввода концентратора событий
2. Настройка и запуск приложения генератора событий
3. Подготовка задания Stream Analytics
4. Указание входных данных задания и запроса

Затем создание базы данных хранилища данных SQL Azure

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a>Указание выходных данных задания: база данных хранилища данных SQL Azure
### <a name="step-1"></a>Шаг 1
В задание Stream Analytics щелкните **ВЫВОДА** сверху hello страницу приветствия и нажмите кнопку **Добавление выходных данных**.

### <a name="step-2"></a>Шаг 2
Выберите базу данных SQL и нажмите кнопку «Далее».

![][add-output]

### <a name="step-3"></a>Шаг 3.
Введите следующие значения на следующую страницу приветствия hello:

* *Псевдоним выходных данных*: введите понятное имя для выходных данных этого задания.
* *Подписка*:
  * Если база данных хранилища данных SQL в hello той же подписке, задание Stream Analytics hello, выберите использовать базу данных SQL из текущей подписки.
  * Если ваша база данных находится в другой подписке, выберите параметр "Использовать базу данных SQL из другой подписки".
* *База данных*: укажите имя hello в целевую базу данных.
* *Имя сервера*: укажите имя сервера hello для указанной базы данных hello. Toofind hello классический портал Azure можно использовать это.

![][server-name]

* *Имя пользователя*: укажите hello имя пользователя учетной записи, которая имеет разрешения на запись для базы данных hello.
* *Пароль*: укажите пароль hello для hello указанную учетную запись пользователя.
* *Таблица*: укажите имя hello hello целевой таблицы в базе данных hello.

![][add-database]

### <a name="step-4"></a>Шаг 4.
Щелкните tooadd кнопку флажок hello этот результат выполнения задания и tooverify успешного подключения базы данных toohello Stream Analytics.

![][test-connection]

После успешного завершения hello подключение к базе данных toohello, вы увидите уведомление hello нижней части портала hello. Hello нижней tootest hello подключения toohello базы данных нажмите кнопку Проверить подключение.

## <a name="next-steps"></a>Дальнейшие действия
Общие сведения об интеграции см. в статье [Интеграция других служб с хранилищем данных SQL][SQL Data Warehouse integration overview].

Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][SQL Data Warehouse development overview].

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
