---
title: "aaaService карты интеграции с System Center Operations Manager | Документы Microsoft"
description: "Схемы услуг — это решение Operations Management Suite, который автоматически обнаруживает компонентов приложений в Windows и системами Linux и карты hello обмен данными между службами. В этой статье описывается с помощью схемы услуг tooautomatically Создание диаграмм распределенных приложений в Operations Manager."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: cff9cce2559448ec3a5fd14087b867f314716560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a>Интеграция схемы услуги с System Center Operations Manager
  > [!NOTE]
  > Эта функция предоставляется в общедоступной предварительной версии.
  > 
  
Схемы услуг Operations Management Suite автоматическое обнаружение компонентов приложения в системах Windows и Linux и сопоставляет hello обмен данными между службами. Схемы услуг можно tooview образом hello серверов можно считать из них, соединенных друг с другом систем, доставляющих критически важных служб. Схемы услуг показаны соединения между серверами, процессы и порты через любой архитектуры TCP-подключения без настройки помимо hello установки агента. Дополнительные сведения см. в разделе hello [документации схемы услуг](operations-management-suite-service-map.md).

С этой интеграции между схемы услуг и System Center Operations Manager можно автоматически создать диаграммах распределенных приложений в Operations Manager, которые основаны на картах hello динамических зависимостей на карте службы.

## <a name="prerequisites"></a>Предварительные требования
* Группа управления Operations Manager, управляющая набором серверов.
* Рабочая область Operations Management Suite с hello включено решение схемы услуг.
* Набор серверов (по крайней мере, один), которые находятся под управлением Operations Manager и отправки данных tooService карты. Поддерживаются серверы Windows и Linux.
* Участника службы с toohello доступа к подписке Azure, связанный с рабочей области Operations Management Suite hello. Дополнительные сведения см. слишком[Создание субъекта-службы](#creating-a-service-principal).

## <a name="install-hello-service-map-management-pack"></a>Установите пакет управления hello схемы услуг
Включить hello интеграцию между Operations Manager и схемы услуг, импортировав набор пакетов управления hello Microsoft.SystemCenter.ServiceMap (Microsoft.SystemCenter.ServiceMap.mpb). Hello пакет содержит следующие пакеты управления hello:
* Microsoft.ServiceMap.Application.Views;
* Microsoft.System.Center.ServiceMap.Internal;
* Microsoft.System.Center.ServiceMap.Overrides;
* Microsoft.System.Center.ServiceMap.

## <a name="configure-hello-service-map-integration"></a>Настройка интеграции службы карты hello
После установки пакета управления схемы услуг hello, новый узел **схемы услуг**, отображается в столбце **Operations Management Suite** в hello **администрирования** области. 

tooconfigure интеграции схемы услуг hello следующие:

1. Мастер настройки hello tooopen в hello **Общие сведения о службе карты** области, нажмите кнопку **добавить рабочую область**.  

    ![Область "Service Map Overview" (Обзор схемы услуги)](media/oms-service-map/scom-configuration.png)

2. В hello **конфигурация подключения** окно, введите имя клиента hello или идентификатор, идентификатор приложения (также известный как имя пользователя hello или clientID) и пароль субъекта-службы hello и нажмите кнопку **Далее**. Дополнительные сведения см. слишком[Создание субъекта-службы](#creating-a-service-principal).

    ![окно конфигурации соединения Hello](media/oms-service-map/scom-config-spn.png)

3. В hello **выбора подписки** окно, выберите hello подписки Azure, группы ресурсов Azure (hello, содержащей рабочей области Operations Management Suite hello) и рабочей области Operations Management Suite и нажмите кнопку **Далее**.

    ![Hello рабочей конфигурации Operations Manager](media/oms-service-map/scom-config-workspace.png)

4. В hello **Выбор группы машины** окно, выберите группы компьютеров карты какие службы требуется toosync tooOperations диспетчера. Нажмите кнопку **Добавление или удаление группы компьютеров**, выбрать группы из списка hello **доступных групп машины**и нажмите кнопку **добавить**.  После завершения выбора групп нажмите кнопку **ОК** toofinish.
    
    ![Hello групп Operations Manager конфигурации компьютера](media/oms-service-map/scom-config-machine-groups.png)
    
5. В hello **Выбор сервера** окна, настройке hello группы серверов служб карты с серверами hello, что требуется toosync между Operations Manager и схемы услуг. Нажмите кнопку **Добавление и удаление серверов**.   
    
    Для toobuild интеграции hello схеме распределенного приложения на сервере должны быть hello server:

    * находиться под управлением Operations Manager;
    * находиться под управлением решения "Сопоставление служб";
    * Перечисленные в hello группы серверов служб карты

    ![Hello конфигурации группы Operations Manager](media/oms-service-map/scom-config-group.png)

6. Необязательно: Установите toocommunicate пула ресурсов hello сервера управления с помощью Operations Management Suite и нажмите кнопку **Добавление рабочей области**.

    ![Пул ресурсов Operations Manager конфигурации Hello](media/oms-service-map/scom-config-pool.png)

    Может потребовать минуты tooconfigure и зарегистрировать рабочей области Operations Management Suite hello. После настройки, Operations Manager инициирует hello первой синхронизации схемы услуг от Operations Management Suite.

    ![Пул ресурсов Operations Manager конфигурации Hello](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a>Мониторинг схемы услуги
После подключения рабочей области Operations Management Suite hello новую папку схемы услуг отображается в hello **мониторинг** hello консоли Operations Manager.

![панели мониторинга Operations Manager Hello](media/oms-service-map/scom-monitoring.png)

Папка схемы услуг Hello имеет четыре узла:
* **Активные предупреждения**: список всех активных предупреждений hello hello соединения между Operations Manager и схемы услуг.  Обратите внимание, что эти оповещения не оповещения Operations Management Suite, синхронизированных tooOperations диспетчера. 

* **Серверы**: списки hello отслеживаемых серверов, которые являются настроен toosync из схемы услуг.

    ![панель мониторинга серверов Operations Manager Hello](media/oms-service-map/scom-monitoring-servers.png)

* **Machine Group Dependency Views** (Представления зависимостей групп компьютеров): здесь указаны группы компьютеров, синхронизируемых с решением "Сопоставление служб". Можно щелкнуть любой группы tooview его схема распределенного приложения.

    ![Схема распределенного приложения Hello Operations Manager](media/oms-service-map/scom-group-dad.png)

* **Server Dependency Views** (Представления зависимости серверов): список всех серверов, синхронизируемых из схемы услуги. Можно щелкнуть любой сервер tooview его схема распределенного приложения.

    ![Схема распределенного приложения Hello Operations Manager](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-hello-workspace"></a>Изменить или удалить рабочую область hello
Можно изменить или удалить рабочую область hello настроен через hello **Общие сведения о службе карты** области (**администрирования** области > **Operations Management Suite**  >  **Службы карты**). Пока можно настроить только одну рабочую область Operations Management Suite.

![Hello Operations Manager изменение рабочей области](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a>Настройка правил и переопределений
Правило, _Microsoft.SystemCenter.ServiceMapImport.Rule_, создается tooperiodically информация выборки из схемы услуг. toochange синхронизации времени можно настроить переопределения правила hello (**Authoring** области > **правила** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).

![окно свойств переопределения Operations Manager Hello](media/oms-service-map/scom-overrides.png)

* **Enabled**: позволяет включить или отключить автоматическое обновление. 
* **IntervalMinutes**: сброс времени hello между обновлениями. Интервал по умолчанию Hello составляет один час. Если требуется maps сервер toosync чаще, можно изменить значение hello.
* **Время тайм-аута**: сброс hello отрезок времени до времени ожидания запроса hello. 
* **TimeWindowMinutes**: сброс hello временное окно для запроса данных. Значение по умолчанию — 60 минут. Hello допустимому значению схемы услуг — 60 минут.

## <a name="known-issues-and-limitations"></a>Известные проблемы и ограничения

Hello текущего конструктора представляет hello следующие проблемы и ограничения:
* Можно подключиться только tooa одной рабочей области Operations Management Suite.
* Несмотря на то, что можно добавить серверы toohello группы серверов служб карты вручную с помощью hello **Authoring** немедленно синхронизируются области карты hello для этих серверов.  Они будут синхронизированы из службы сопоставления во время следующего цикла синхронизации hello.
* Если вы внесли изменения схемы распределенного приложения toohello, созданные пакетом управления hello, эти изменения будут перезаписаны скорее всего на hello следующей синхронизации с помощью схемы услуг.

## <a name="create-a-service-principal"></a>Создание субъекта-службы
Официальная документация Azure по созданию субъекта-службы представлена в следующих статьях:
* [Использование Azure PowerShell для создания субъекта-службы и доступа к ресурсам](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Использование интерфейса командной строки Azure для создания субъекта-службы и доступа к ресурсам](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [Создание участника службы с помощью hello портал Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a>Отзыв
У вас есть комментарии относительно схемы услуги или этой документации? Посетите [страницу пользовательских мнений](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), где можно предложить функции или проголосовать за существующие предложения.
