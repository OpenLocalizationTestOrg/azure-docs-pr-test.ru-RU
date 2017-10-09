---
title: "событие aaaReal во время обработки с обработкой событий Stream Analytics | Документы Microsoft"
description: "Узнайте о том, как обрабатывать и анализировать события в режиме реального времени с помощью различных служб Azure."
keywords: "обработка в режиме реального времени, обработка событий, эталонная архитектура"
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: a43c503d709609ba61e9932822d30bc2208906ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a>Эталонная архитектура: обработка событий в режиме реального времени средствами Microsoft Azure Stream Analytics
Эталонная архитектура Hello для событий в реальном времени обработки при помощи Azure Stream Analytics — предполагаемого tooprovide универсальный проект для развертывания в режиме реального времени платформы как услуги (PaaS) решение обработки потока с помощью Microsoft Azure.

## <a name="summary"></a>Сводка
В большинстве случаев аналитические решения основанными на возможности, такие как ETL (extract, transform, нагрузки) и хранения данных, где tooanalysis хранимых предыдущих данных. Изменяющимся требованиям, включая дополнительные быстро поступающие данные, уже не хватает предела toohello существующей модели. данные tooanalyze возможность Hello внутри скользящего предыдущих toostorage потоки одного решения и пока не является новой возможностью, подход hello не было широко приняла через все отраслевых вертикалях. 

Платформа Microsoft Azure предлагает богатый ассортимент аналитических технологий, позволяющих реализовать самые разные сценарии и решения с различными требованиями. Выбор, какой toodeploy служб Azure для решения конца в конец может оказаться сложной задачей, учитывая hello спектр предложений. Этот документ предназначен возможности спроектированный toodescribe hello и взаимодействие hello различных служб Azure, которые поддерживают решение для потоковой передачи событий. Здесь также описываются некоторые сценарии hello, в которых клиенты могут использовать преимущества такой подход.

## <a name="contents"></a>Оглавление
* Аннотация
* Аналитика времени tooReal введение
* Ценность средств Azure для работы с данными в режиме реального времени
* Распространенные сценарии применения средств аналитики в режиме реального времени
* Архитектура и компоненты
  * Источники данных
  * Уровень интеграции данных
  * Уровень аналитики в режиме реального времени
  * Уровень хранения данных
  * Уровень представления или потребления
* Заключение

**Автор:** Чарльз Феддерсен (Charles Feddersen), архитектор решений, Научно-инновационный центр анализа данных (Data Insights Center of Excellence), корпорация Майкрософт

**Опубликовано:** январь 2015 г.

**Версия:** 1.0

**Ссылка для загрузки:** [Обработка событий в режиме реального времени средствами Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)

## <a name="get-help"></a>Справка
Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

