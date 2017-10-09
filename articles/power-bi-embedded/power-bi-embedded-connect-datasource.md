---
title: "Power BI Embedded - подключения источника данных tooa aaaMicrosoft"
description: "Power BI Embedded, подключить источники toodata"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a>Соединение с источником данных tooa
С **Power BI Embedded**вы сможете вставлять отчеты в свои приложения. Если внедрение отчета Power BI в приложение, hello отчет подключается toohello исходные данные, **Импорт** копии данных hello или с помощью **непосредственное подключение** toohello источнику данных с помощью  **DirectQuery**.

Ниже приведены hello различия между использованием **импорта** и **DirectQuery**.

| Импорт | DirectQuery |
| --- | --- |
| Таблицы, столбцы, *и данные* импортируются или копируются в наборе данных отчета hello. toosee изменения базовых данных, произошедших toohello, необходимо обновить или импортировать завершения, текущее набора данных еще раз. |Только *таблицы и столбцы* импортируются или копируются в наборе данных отчета hello. Всегда можно просмотреть hello самых последних данных. |

Благодаря Power BI Embedded в настоящее время можно использовать DirectQuery с облачными источниками данных, но не с локальными источниками данных.

> [!NOTE]
> Hello локальный шлюз данных не поддерживается с Power BI Embedded в данный момент. Это означает, что нельзя использовать DirectQuery для локальных источников данных.

## <a name="supported-data-sources"></a>Поддерживаемые источники данных

**DirectQuery**
* База данных SQL Azure
* Хранилище данных SQL Azure

**Импорт**

Можно импортировать с помощью любых hello доступных источников данных в Power BI Desktop. Вы будете **не** быть может toorefresh этих данных в Power BI Embedded. Будет иметь изменения tooupload tooyour PBIX файл tooPower BI Embedded. Это происходит из-за toono доступного шлюза. 

## <a name="benefits-of-using-directquery"></a>Преимущества использования DirectQuery
Использование **DirectQuery**связано с такими преимуществами:

* **DirectQuery** Здравствуйте, позволяет создавать визуализации на очень больших наборов данных, где в противном случае было бы нецелесообразной toofirst импорта всех данных.
* Изменения в базовых данных могут потребовать обновления данных, а для некоторых отчетов hello требуется toodisplay текущего данных может потребоваться большой объем данных, делая повторный импорт данных нецелесообразным. В отчетах **DirectQuery** , напротив, всегда используются текущие данные.

## <a name="limitations-of-directquery"></a>Ограничения DirectQuery
   Существует несколько ограничений toousing **DirectQuery**:

* Все таблицы должны находиться в одной базе данных.
* Если hello является слишком сложным, произойдет ошибка. Ошибка hello tooremedy необходимо внести изменения в запрос hello, менее сложна. Если запрос hello должны быть сложными, вам потребуется tooimport hello данные вместо использования **DirectQuery**.
* Фильтрация связей — ограниченный tooa одно направление, а не в обоих направлениях.
* Невозможно изменить тип данных столбца hello.
* По умолчанию ограничения помещаются в выражения DAX, разрешенные в мерах. Дополнительные сведения см. в разделе [DirectQuery и меры](#measures).

<a name="measures"/>

## <a name="directquery-and-measures"></a>DirectQuery и меры
tooensure запросов, отправляемых toohello базового источника данных имеют приемлемую производительность, ограничения накладываются на меры. При использовании **Power BI Desktop**расширенные пользователи могут выбирать toobypass это ограничение, выбрав **файл > Параметры и настройки > Параметры**. В hello **параметры** диалоговое окно, выберите **DirectQuery**и выберите параметр hello **разрешить неограниченные меры в режиме DirectQuery**. При выборе этого параметра может использоваться любое выражение DAX, которое является допустимым для меры. Пользователям необходимо иметь в виду; Тем не менее, некоторые выражения, которые выполняют очень хорошо при импорте данных hello может привести к очень медленного выполнения запросов toohello внутреннего источника, когда оно **DirectQuery** режим. 

## <a name="see-also"></a>См. также
* [Начало работы с Microsoft Power BI Embedded (предварительная версия)](power-bi-embedded-get-started.md)
* [Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

У вас имеются и другие вопросы? [Повторите hello сообщества Power BI](http://community.powerbi.com/)

