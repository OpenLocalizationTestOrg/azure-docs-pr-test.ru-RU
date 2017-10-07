---
title: "hello aaaUse представление выполнения вершин в средствах Озера данных для Visual Studio | Документы Microsoft"
description: "Узнайте, как toouse hello представление выполнения вершин tooexam аналитики Озера данных задания."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a>Используйте представление выполнения вершин hello в средствах Озера данных для Visual Studio
Узнайте, как toouse hello представление выполнения вершин tooexam аналитики Озера данных задания.

## <a name="prerequisites"></a>Предварительные требования

Необходимо, чтобы базовые сведения об использовании средства Озера данных для скрипта toodevelop U-SQL в Visual Studio.  См. [Учебник. Разработка скриптов U-SQL с помощью средств Data Lake для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).

## <a name="open-hello-vertex-execution-view"></a>Откройте представление выполнения вершин hello
Откройте задание U-SQL в Средствах Data Lake для Visual Studio. Нажмите кнопку **представление выполнения вершин** в левом нижнем углу hello. Может быть запрос tooload профилей сначала, и она может занять некоторое время в зависимости от сетевого подключения.

![Представление выполнения вершин средств Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a>Сведения о представлении выполнения вершин
Hello вершин представление выполнения состоит из трех частей:

![Представление выполнения вершин средств Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

Hello **вершин селектор** на левой позволяет hello выберите вершин, компоненты (такие как top 10 данных чтения, или выберите по этапам). Одно из наиболее часто используемые фильтры hello — toosee hello **вершин на критический путь**. Hello **критический путь** hello самая длинная цепочка вершин задания U-SQL. Основные сведения о hello критический путь можно использовать для оптимизации заданиям, проверьте, какие вершин занимает большое время hello.
  
![Представление выполнения вершин средств Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

Hello вверху по центру области отображаются hello **текущий статус всех вершин hello**.
  
![Представление выполнения вершин средств Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

Hello нижней центральной области отображаются сведения о каждой вершины:
* Имя процесса: hello имя экземпляра вершин hello. Оно состоит из различных частей в StageName|VertexName|VertexRunInstance. Например, [62] .v1 вершин hello SV7_Split означает hello второй работающего экземпляра (.v1, индекс, начиная с 0) числом вершин 62 в SV7_Split рабочей области.
* Общее чтение данных и создано: hello данных было прочитать или записать с этого вершин.
* Состояние и выхода, состояние: hello конечного состояния завершения hello вершин.
* Тип кода и сбоев выхода: hello ошибка при сбое вершин hello.
* Причина создания: Почему вершин hello был создан.
* Задержка очереди задержка/PN задержки или процесс ресурсов: hello время, необходимое для hello toowait вершин для ресурсов, данные tooprocess и toostay в очереди hello.
* Создатель процесса и идентификатор GUID: Идентификатор GUID для текущего выполнения вершин hello или его создатель.
* Версия: hello N-й экземпляр запущен вершин hello (hello системы может запланировать новые экземпляры вершин для вычислений многим причинам, например переход на другой ресурс, избыточность и т. д.)
* Время создания версии.
* Создать начала время или процесс в очереди время или процесс начала время или процесс завершения обработки времени: при запуске процесса вершин hello создания; Когда процесс вершин hello начинается tooqueue; Когда hello начинается процесс определенных вершин; hello определенных вершин завершении.

## <a name="next-steps"></a>Дальнейшие действия
* сведения диагностики toolog см. в разделе [доступ к журналов диагностики для аналитики Озера данных Azure](data-lake-analytics-diagnostic-logs.md)
* в разделе toosee более сложный запрос, [веб-сайта анализ журналов с помощью аналитики Озера данных Azure](data-lake-analytics-analyze-weblogs.md).
* см. сведения о задании tooview, [используйте браузер задания и представление заданий для задания аналитики Озера данных Azure](data-lake-analytics-data-lake-tools-view-jobs.md)
