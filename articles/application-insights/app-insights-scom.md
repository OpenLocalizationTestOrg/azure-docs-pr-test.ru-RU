---
title: "aaaSCOM интеграция с Application Insights | Документы Microsoft"
description: "Если вы используете SCOM, примените Application Insights для мониторинга производительности и диагностики. Подробные панели мониторинга, смарт-оповещения, мощные средства диагностики и аналитические запросы."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a>Мониторинг производительности приложений с помощью Application Insights для SCOM
При использовании серверов toomanage System Center Operations Manager (SCOM) можно отслеживать производительности и диагностики проблем с производительностью с помощью hello [Azure Application Insights](app-insights-asp-net.md). Application Insights отслеживает входящие запросы вашего веб-приложения, исходящие вызовы REST и SQL, а также исключения и трассировку журналов. Вы можете использовать панели мониторинга с диаграммами метрик и смарт-оповещениями, а также мощные средства диагностического поиска и аналитических запросов для работы с данными телеметрии. 

Мониторинг Application Insights можно включить с помощью пакета управления SCOM.

## <a name="before-you-start"></a>Перед началом работы
Предполагается следующий сценарий:

* Веб-серверы, вы уже знакомы с SCOM и использовать SCOM 2012 R2 или 2016 toomanage служб IIS.
* Уже установки на серверах веб-приложения, которые должны toomonitor с помощью Application Insights.
* Используется платформа .NET версии 4.5 и выше.
* У вас есть подписка tooa доступ [Microsoft Azure](https://azure.com) и может подписывать в toohello [портал Azure](https://portal.azure.com). Организации могут иметь подписку, а также добавлять вашей tooit учетной записи Майкрософт.

(команда разработчиков hello может построить hello [пакет SDK Application Insights](app-insights-asp-net.md) в веб-приложения hello. Этот инструментарий, подключаемый во время сборки, делает процесс написания пользовательской телеметрии более гибким. Тем не менее, не имеет значения: можно использовать hello действия, описанные здесь, с указанием или без hello встроенные SDK.)

## <a name="one-time-install-application-insights-management-pack"></a>(Однократно) Установка пакета управления Application Insights
На компьютере, где запускается Operations Manager для hello:

1. Удалите все старые версии пакета управления hello:
   1. В Operations Manager откройте меню "Администрирование", щелкните "Пакеты управления". 
   2. Удалите старую версию hello.
2. Загрузите и установите пакет управления hello из каталога hello.
3. Перезапустите Operations Manager.

## <a name="create-a-management-pack"></a>Создание пакета управления
1. В Operations Manager откройте **Разработка**, **.NET...with Application Insights** (.NET... с Application Insights), **Мастер добавления объекта мониторинга**, а затем снова выберите **.NET...with Application Insights** (.NET... с Application Insights).
   
    ![](./media/app-insights-scom/020.png)
2. Имя конфигурации hello после приложения. (Имеется tooinstrument одно приложение за раз.)
   
    ![](./media/app-insights-scom/030.png)
3. Hello же на странице мастера, либо создать новый управления пакет, или выберите пакет, созданный для Application Insights, более ранних версий.
   
     (hello Application Insights [пакет управления](https://technet.microsoft.com/library/cc974491.aspx) — это шаблон, из которого можно создать экземпляр. Можно повторно использовать hello же экземпляр более поздней версии.)

    ![В hello вкладка «Общие свойства» введите имя hello приложение hello. Нажмите кнопку "Создать" и введите имя пакета управления. Нажмите кнопку "ОК", а затем — "Далее".](./media/app-insights-scom/040.png)

1. Выберите одно приложение, которые должны toomonitor. Функция поиска Hello поиск среди приложений, установленных на серверах.
   
    ![Какие вкладки tooMonitor нажмите кнопку Добавить, введите часть имени приложения hello, нажмите кнопку поиска, выберите OK приложение hello, а затем добавить.](./media/app-insights-scom/050.png)
   
    Hello необязательный мониторинг поле «область» может быть используется toospecify подмножество серверов, если не нужно, чтобы приложение hello toomonitor на всех серверах.
2. На следующей странице мастера hello прежде всего необходимо указать вашей toosign учетные данные в tooMicrosoft Azure.
   
    На этой странице выберите ресурс Application Insights hello место hello toobe данных телеметрии анализируются и отображаются. 
   
   * Hello приложение настроено для Application Insights во время разработки, выберите его в существующий ресурс.
   * В противном случае создайте новый ресурс с именем для приложения hello. Если имеются другие приложения, которые являются компонентами для hello одной системе, поместите их в hello одну группу ресурсов, проще toomanage телеметрии toohello toomake доступа.
     
     Эти параметры можно изменить позже.
     
     ![На вкладке параметров Application Insights нажмите кнопку "Войти" и укажите учетные данные учетной записи Майкрософт для Azure. Затем выберите подписку, группу ресурсов и ресурс.](./media/app-insights-scom/060.png)
3. Мастер завершения hello.
   
    ![Нажмите кнопку "Создать"](./media/app-insights-scom/070.png)

Повторите эту процедуру для каждого приложения, которое следует toomonitor.

Если требуется toochange параметры позже, снова откройте hello свойства монитора hello из окна "Создание и настройка hello".

![В разделе "Создание" выберите ".NET Application Performance Monitoring with Application Insights" (Мониторинг производительности приложений .NET с помощью Application Insights), укажите монитор и щелкните "Свойства".](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a>Проверка мониторинга
монитор Hello, что вы установили ищет приложения на каждом сервере. Где находит приложение hello, настраивает приложение hello toomonitor монитор состояния Application Insights. При необходимости сначала устанавливает монитор состояния на сервере hello.

Можно проверить, какие экземпляры приложение hello нахождения.

![В разделе "Мониторинг" откройте Application Insights.](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a>Просмотр данных телеметрии в Application Insights
В hello [портал Azure](https://portal.azure.com), Обзор ресурсов toohello для вашего приложения. Вы увидите [диаграммы телеметрии](app-insights-dashboards.md) для этого приложения. (Если он еще не отображаются на главной странице hello еще, щелкните обновляющегося потока метрики).

## <a name="next-steps"></a>Дальнейшие действия
* [Настройка панели мониторинга](app-insights-dashboards.md) toobring вместе hello наиболее важных диаграмм мониторинг это и другие приложения.
* [Дополнительная информация о метриках](app-insights-metrics-explorer.md)
* [Настройка оповещений](app-insights-alerts.md)
* [Диагностика проблем с производительностью](app-insights-detect-triage-diagnose.md)
* [Мощные аналитические запросы](app-insights-analytics.md)
* [Доступность веб-тестов](app-insights-monitor-web-app-availability.md)

