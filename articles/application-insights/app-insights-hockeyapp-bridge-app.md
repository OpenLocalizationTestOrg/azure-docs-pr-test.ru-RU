---
title: "aaaExploring HockeyApp данные в Azure Application Insights | Документы Microsoft"
description: "Анализ использования и производительности приложения Azure с помощью Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 97783cc6-67d6-465f-9926-cb9821f4176e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: bwren
ms.openlocfilehash: ed7cf99b48f5ec78d6b401bb954cfcd014b9d1f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a>Просмотр данных HockeyApp в Application Insights
[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) hello рекомендуется использовать платформу для отслеживания динамической приложений для настольных компьютеров и мобильных устройств. От HockeyApp можно отправлять пользовательские и трассировки телеметрии toomonitor использования и упростить диагностику (в данных аварийного toogetting сложения). Этот поток телеметрии можно запросить, используя hello мощные [Analytics](app-insights-analytics.md) функция [Azure Application Insights](app-insights-overview.md). Кроме того, вы можете [экспорт пользовательских hello и телеметрии трассировки](app-insights-export-telemetry.md). tooenable их с функциями, можно настроить мост, который ретранслирует tooApplication HockeyApp пользовательские данные аналитики.

## <a name="hello-hockeyapp-bridge-app"></a>приложение Hello моста HockeyApp
HockeyApp моста приложения Hello является основной функцией hello, благодаря которой вы tooaccess ваши пользовательские HockeyApp и трассировки телеметрии в Application Insights через hello аналитика и непрерывный Экспорт функций. Пользовательские и трассировки событий, собранных HockeyApp после создания hello hello HockeyApp мост приложения будут доступны из этих функций. Давайте посмотрим, как tooset один из этих приложений моста.

В HockeyApp откройте параметры учетной записи и щелкните [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens)(Маркеры API). Создайте новый маркер или воспользуйтесь существующим. минимальные права Hello требуется являются «только для чтения». Сделайте копию hello API маркеров.

![Получение маркера API HockeyApp](./media/app-insights-hockeyapp-bridge-app/01.png)

Привет открыть портал Microsoft Azure и [создать ресурс Application Insights](app-insights-create-new-resource.md). Задайте тип приложения слишком «Приложение моста HockeyApp»:

![Новый ресурс Application Insights](./media/app-insights-hockeyapp-bridge-app/02.png)

Не нужно tooset имя — это будет автоматически на основе имени HockeyApp hello.

отображаются поля моста HockeyApp Hello. 

![Мост: заполнение полей](./media/app-insights-hockeyapp-bridge-app/03.png)

Введите токен HockeyApp hello записанные ранее. Это действие вносит hello «HockeyApp приложение» раскрывающееся меню в приложениях HockeyApp. Выберите hello один toouse и завершения hello оставшуюся часть поля hello. 

Откройте новый ресурс hello. 

Обратите внимание, что hello данных занимает некоторое время toostart потока.

![Ресурс Application Insights: ожидание данных](./media/app-insights-hockeyapp-bridge-app/04.png)

Это все! Пользовательские и трассировки данных, собранных в HockeyApp инструментированного приложения с этого момента теперь также является доступной tooyou в hello аналитика и непрерывный Экспорт функций Application Insights.

Кратко рассмотрим каждый из эти компоненты теперь доступно tooyou.

## <a name="analytics"></a>Аналитика
Аналитика является мощным средством для нерегламентированных запросов данных, позволяя toodiagnose анализа телеметрии и быстро Осваивайте шаблоны и основных причин.

![Аналитика](./media/app-insights-hockeyapp-bridge-app/05.png)

* [Знакомство с аналитикой в Application Insights](app-insights-analytics-tour.md)

## <a name="continuous-export"></a>непрерывный экспорт.
Непрерывный Экспорт позволяет tooexport данных в контейнер хранилища больших двоичных объектов. Это очень полезно, если необходимо tookeep данных дольше, чем срок хранения hello в настоящее время предлагаемых Application Insights. Можно хранить данные hello в хранилище больших двоичных объектов, его обработки в базе данных SQL или предпочтительный решения хранилищ данных.

[Экспорт данных телеметрии из Application Insights](app-insights-export-telemetry.md)

## <a name="next-steps"></a>Дальнейшие действия
* [Применить данные tooyour аналитика](app-insights-analytics-tour.md)

