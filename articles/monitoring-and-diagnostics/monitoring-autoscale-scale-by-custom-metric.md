---
title: "aaaGet работы с автоматическое масштабирование по метрике пользовательских в Azure | Документы Microsoft"
description: "Узнайте, как tooscale ресурс пользовательские метрики в Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a>Начало работы с автомасштабированием на основе пользовательской метрики в Azure
В этой статье описывается как tooscale ресурс пользовательские метрики на портале Azure.

Автоматическое масштабирование Azure монитор применяется только tooVirtual задает масштаб компьютера (VMSS), облачные службы, планах службы приложений и среды службы приложений. 

# <a name="lets-get-started"></a>Начало работы
В данной статье предполагается, что у вас есть веб-приложение, для которого настроена среда Application Insights. Если у вас его нет, вы можете [установить Application Insights для веб-сайта ASP.NET][1].

- Откройте [портал Azure][2].
- Щелкните значок Azure монитора hello левой панели навигации.
  ![Запуск Azure Monitor][3]
- Щелкните параметр tooview все ресурсы hello, для которого автоматически масштаб не применимо, а также ее текущее состояние автомасштабирования автомасштабирования ![обнаружение автоматическое масштабирование в Azure монитора][4]
- Откройте колонку «Автомасштабирования» в мониторе Azure и выберите ресурс, нужно tooscale
> Примечание: hello шаги использовать план обслуживания приложений, связанных с веб-приложения с настроить подробные сведения о приложении.
- В колонке параметр hello масштабирования для ресурса hello Обратите внимание, что текущее количество экземпляров hello 1. Щелкните Enable autoscale (Включить автомасштабирование).
  ![Параметр масштабирования для нового веб-приложения][5]
- Введите имя для параметра масштабирования hello и hello щелкните «Добавить правило». Обратите внимание, параметров правил масштабирования hello, открывается в виде контекстной области в правую часть hello. По умолчанию он устанавливает экземпляр счетчика на 1, если percetage ЦП hello hello ресурса превышает 70% tooscale параметр hello. Источник метрики hello изменение вверху hello слишком выберите «Application Insights» hello ресурсов аналитики приложений в раскрывающийся список «Resource» hello "и" hello, а затем выберите пользовательские метрики на основе tooscale для которых нужно получить.
  ![Масштабирование на основе пользовательской метрики][6]
- Аналогичные toohello шаг выше, добавьте правила масштабирования, которая будет масштабировать и уменьшить число hello масштабирования на 1, если пользовательская метрика hello ниже порогового значения.
  ![Масштабирование на основе использования ЦП][7]
- Установите экземпляр ограничения hello. Например, если требуется tooscale между экземплярами 2 – 5 в зависимости от пользовательские метрики колебания hello задать «Минимальная» слишком "2", «максимум» слишком "5" и «default» слишком "2"
> Примечание: Если имеется проблема при чтении метрики ресурсов hello и hello текущая емкость меньше емкости по умолчанию hello, затем tooensure hello доступности ресурса hello автомасштабирования будет масштабировать toohello значение по умолчанию. Если текущая емкость hello уже превышает емкость по умолчанию, в не масштабируется автоматического масштабирования.
- Щелкните "Сохранить".

Поздравляем! Теперь ваш tooauto параметр масштабирования успешно созданы масштабировать веб-приложения, в зависимости от пользовательской метрики.

> Примечание: hello же действия, применимые tooget работы с ролью VMSS или облачной службы.

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
