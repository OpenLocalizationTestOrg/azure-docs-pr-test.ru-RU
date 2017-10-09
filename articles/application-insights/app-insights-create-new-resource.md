---
title: "aaaCreate новый ресурс Azure Application Insights | Документы Microsoft"
description: "Вручную настройте мониторинг Application Insights для нового работающего приложения."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a>Создание ресурса Application Insights
В Azure Application Insights данные о приложении отображаются в *ресурсе* Microsoft Azure. Создание нового ресурса таким образом является частью [Настройка нового приложения Application Insights toomonitor][start]. Во многих случаях Создание ресурса может выполняться автоматически hello интегрированной среды разработки. Но в некоторых случаях вы вручную создайте ресурс — например, toohave отдельные ресурсы для разработки и эксплуатации построений приложения.

После создания ресурса hello получить свой ключ инструментирования, а затем использовать этот tooconfigure hello SDK, в приложение hello. ссылки на ресурсы Hello ключа hello телеметрии toohello ресурсов.

## <a name="sign-up-toomicrosoft-azure"></a>Регистрация tooMicrosoft Azure
Если у вас еще нет [учетной записи Майкрософт, получите ее сейчас](http://live.com). (Если вы используете такие службы, как Outlook.com, OneDrive, Windows Phone или XBox Live, значит, у вас уже есть учетная запись Майкрософт.)

Вам также потребуется подписка слишком[Microsoft Azure](http://azure.com). Если команде или организации имеет подписку Azure, владелец hello можно добавить вас tooit, с помощью идентификатора Windows Live ID. Плата взимается только за используемый объем, Базовый план по умолчанию Hello позволяет определенное количество экспериментальных целей бесплатно.

Если у вас есть подписка tooa доступ, войдите в tooApplication аналитики в [http://portal.azure.com](https://portal.azure.com)и использовать ваш идентификатор Live ID toologin.

## <a name="create-an-application-insights-resource"></a>Создание ресурса Application Insights
В hello [portal.azure.com](https://portal.azure.com), добавьте ресурс Application Insights:

![Нажмите "Создать" и "Application Insights"](./media/app-insights-create-new-resource/01-new.png)

* **Тип приложения** влияет на содержимое, отображаемое на колонки Обзор hello и hello свойств, доступных в [метрики обозреватель][metrics]. Если тип приложения не отображается, выберите пункт "Общие".
* **Подписка** представляет собой учетную запись для оплаты в Azure.
* **Группа ресурсов** – удобный способ для управления свойствами наподобие контроля доступа. Если вы уже создали другим ресурсам Azure, вы можете tooput этот новый ресурс в hello одной группе.
* **Расположение** – это место, в котором мы храним ваши данные.
* **ПИН-код toodashboard** помещает плитки быстрого доступа для ресурса на Azure домашней страницы. (рекомендуется).

После создания приложения откроется новая колонка. В этой колонке будут представлены данные о производительности и использовании приложения. 

Назад tooit tooget при очередном входе в tooAzure, найдите плитку: быстрый запуск приложения на hello запустите доски (начальный экран). Или нажмите кнопку обзора toofind его.

## <a name="copy-hello-instrumentation-key"></a>Скопируйте ключ инструментирования hello
ключ инструментирования Hello идентифицирует созданный ресурс hello. Вы должны toogive toohello SDK.

![Установите Essentials, щелкните hello ключ инструментирования, CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a>Установка пакета SDK для hello в приложении
Установите пакет SDK Application Insights hello в вашем приложении. Этот шаг сильно зависит от типа приложения hello. 

Использовать tooconfigure ключа инструментирования hello [пакета SDK, которую можно установить в приложение hello][start].

Hello SDK включает стандартные модули, отправка данных телеметрии без необходимости toowrite любого кода. действия пользователя tootrack или Диагностика проблем более подробно [использовать hello API] [ api] toosend собственные телеметрии.

## <a name="monitor"></a>Просмотр данных телеметрии
Закрыть hello быстрый запуск колонки tooreturn tooyour приложения колонки в hello портал Azure.

Щелкните плитку toosee hello поиска [диагностики поиска][diagnostic], где отображаются первые события hello. 

Нажмите кнопку **Обновить** через несколько секунд, если ожидаете дополнительные данные.

## <a name="creating-a-resource-automatically"></a>Автоматическое создание ресурса
Можно написать [сценарий PowerShell](app-insights-powershell.md) toocreate ресурс автоматически.

## <a name="next-steps"></a>Дальнейшие действия
* [Создание панели мониторинга](app-insights-dashboards.md)
* [Поиск по журналу диагностики](app-insights-diagnostic-search.md)
* [Изучение метрик](app-insights-metrics-explorer.md)
* [Написание запросов аналитики](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

