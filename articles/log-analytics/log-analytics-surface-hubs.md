---
title: "aaaMonitor устройства Surface Hub с Azure Log Analytics | Документы Microsoft"
description: "Используйте hello Surface Hub решения tootrack hello работоспособность вашего устройства Surface Hub и понять, как они используются."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 623d30e749cafdd4a34ba0c5b3408164f1b4a95b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-tootrack-their-health"></a>Отслеживать их работоспособность устройства Surface Hub с tootrack анализа журналов

![Символ решения Surface Hub](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

В этой статье описывается, как можно использовать hello Surface Hub решения в службе анализа журналов устройства Microsoft Surface Hub toomonitor с hello Microsoft Operations Management Suite (OMS). Аналитика журналов позволяет отслеживать работоспособность вашего устройства Surface Hub hello также понять, как они используются.

Каждый Surface Hub имеет hello установки Microsoft Monitoring Agent. Его следует отправить данные из вашей tooOMS Surface Hub агенту hello. Файлы журналов считываются из вашего устройства Surface Hub и затем отправляются в службу OMS toohello. Проблемы как календарь не синхронизирует hello серверы находятся в автономном режиме, или если учетная запись устройств hello не удается toolog в Скайп в OMS hello Surface Hub панели отображаются. С помощью данных hello в панель мониторинга hello, можно определить устройства, которые не работают, или возникли другие проблемы и потенциально применить исправления hello обнаружены проблемы.

## <a name="installing-and-configuring-hello-solution"></a>Установка и настройка решения hello
Используйте следующие сведения tooinstall hello и настроить решение hello. Порядок toomanage концентраторов поверхность из hello Microsoft Operations Management Suite (OMS), вам потребуется hello следующие:

* Действующая подписка слишком[OMS](http://www.microsoft.com/oms).
* [Подписки OMS](https://azure.microsoft.com/pricing/details/log-analytics/) уровень, который будет поддерживать hello номера устройств требуется toomonitor. Цены на OMS зависят от количества зарегистрированных устройств и объема обрабатываемых данных. Будет необходимо tootake это во внимание при планировании развертывания Surface Hub.

Далее будет добавить существующую подписку Microsoft Azure OMS подписки tooyour или создать новую рабочую область непосредственно через портал OMS hello. Подробные инструкции по использованию любого из этих методов содержатся в статье [Начало работы с Log Analytics](log-analytics-get-started.md). После настройки подписки OMS hello существует два способа tooenroll устройства Surface Hub.

* автоматически с помощью InTune;
* вручную в приложении **Settings** на устройстве Surface Hub.

## <a name="set-up-monitoring"></a>Настройка мониторинга
Можно отслеживать hello работоспособности и активности вашей Surface Hub, с помощью аналитики журналов в OMS. Вы можете зарегистрировать hello Surface Hub в OMS с помощью Intune или локально с помощью **параметры** на hello Surface Hub.

## <a name="connect-surface-hubs-toooms-through-intune"></a>Подключение устройства Surface Hub tooOMS через Intune
Идентификатор рабочей области и ключ рабочей области для рабочей области OMS hello, который будет управлять концентраторов поверхности будет требуется hello. Можно получить из портала OMS hello.

Intune — продукт Майкрософт, которая позволяет вам toocentrally Управление параметрами конфигурации OMS hello, примененные tooone или несколько устройств. Выполните эти шаги tooconfigure устройствами с помощью Intune.

1. Войдите в tooIntune.
2. Перейдите в слишком**параметры** > **подключенные источники**.
3. Создание или изменение политики на основе шаблона hello Surface Hub.
4. Перейдите в раздел OMS (оперативной аналитики Azure) toohello политики hello и добавить hello *идентификатор рабочей области* и *ключ рабочей области* toohello политики.
5. Сохраните политику hello.
6. Свяжите политику hello с hello соответствующую группу устройств.

   ![Политика Intune](./media/log-analytics-surface-hubs/intune.png)

Затем Intune синхронизируется hello OMS параметры с устройствами hello в целевую группу hello, регистрировать их в рабочую область OMS.

## <a name="connect-surface-hubs-toooms-using-hello-settings-app"></a>Подключиться с помощью параметров приложения hello tooOMS устройства Surface Hub
Идентификатор рабочей области и ключ рабочей области для рабочей области OMS hello, который будет управлять концентраторов поверхности будет требуется hello. Можно получить из портала OMS hello.

Если вы не используете Intune toomanage среды, можно регистрировать устройства вручную до **параметры** на каждом Surface Hub:

1. На устройстве Surface Hub откройте приложение **Settings**.
2. Введите учетные данные hello устройства администратора при появлении запроса.
3. Нажмите кнопку **это устройство**и hello под **мониторинг**, нажмите кнопку **Настройка параметров OMS**.
4. Выберите **Enable monitoring** (Включить мониторинг).
5. В диалоговом окне Параметры OMS hello, введите hello **идентификатор рабочей области** и типа hello **ключ рабочей области**.  
   ![параметры](./media/log-analytics-surface-hubs/settings.png)
6. Нажмите кнопку **ОК** toocomplete hello конфигурации.

Подтверждающее сообщение, информирующее о ли приветствия OMS конфигурации были успешно применены toohello устройства. Если он был, появляется сообщение о том, что этот агент hello успешного подключения toohello службой OMS. устройство Hello начинает отправку данных tooOMS, где можно просматривать и работать с ней.

## <a name="monitor-surface-hubs"></a>Мониторинг устройств Surface Hub
Мониторинг устройств Surface Hub с помощью OMS во многом напоминает мониторинг любых других зарегистрированных устройств.

1. Войдите в систему toohello портал OMS.
2. Перейдите в панель мониторинга пакета решения Surface Hub toohello.
3. Отобразится состояние работоспособности устройства.

   ![Панель мониторинга Surface Hub](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

Можно создавать [оповещения](log-analytics-alerts.md) на основе существующих или настраиваемых поисковых запросов к журналу. С помощью OMS собирает данные из концентраторов область данных приветствия hello, можно искать проблемы и оповещения об hello условия, определенные для устройств.

## <a name="next-steps"></a>Дальнейшие действия
* Используйте [входа поиска аналитики журналов](log-analytics-log-searches.md) tooview подробных данных Surface Hub.
* Создание [оповещения](log-analytics-alerts.md) toonotify вы при возникновении проблем с вашего устройства Surface Hub.
