---
title: "кластер Azure DC/OS aaaMonitor - операций управления | Документы Microsoft"
description: "Мониторинг кластера DC/OS в Службе контейнеров Azure с помощью Microsoft Operations Management Suite."
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a>Мониторинг кластера DC/OS в Службе контейнеров Azure с помощью Operations Management Suite

Microsoft Operations Management Suite (OMS) — это облачное решение Майкрософт для управления ИТ-средой, которое помогает управлять локальной и облачной инфраструктурой и защищать ее. Решение контейнер — это решение в аналитику журнала OMS, служащей для просмотра данных инвентаризации контейнера hello, производительности и журналов в одном месте. Аудит, устранение неполадок контейнеры путем просмотра журналов hello в центральном расположении и найти шумный использование лишние контейнер на узле.

![](media/container-service-monitoring-oms/image1.png)

Дополнительные сведения о решении контейнера можно найти toothe [анализа журналов контейнера решение](../../log-analytics/log-analytics-containers.md).

## <a name="setting-up-oms-from-hello-dcos-universe"></a>Установка OMS с контроллера домена/OS вселенной hello


В этой статье предполагается, что настройки контроллера домена/OS и развертывания простого веб-приложения контейнера в кластере hello.

### <a name="pre-requisite"></a>Предварительные требования
- [Подписка Microsoft Azure](https://azure.microsoft.com/free/) — ее можно получить бесплатно.  
- Настройка рабочей области Microsoft OMS — см. раздел "Шаг 3" ниже.
- Установленный [интерфейс командной строки DC/OS](https://dcos.io/docs/1.8/usage/cli/install/).

1. В панели мониторинга hello DC/OS щелкните вселенной и выполните поиск «OMS», как показано ниже.

![](media/container-service-monitoring-oms/image2.png)

2. Щелкните **Install**(Установить). Вы увидите pop вверх на сведения о версии OMS hello и **установить пакет** или **расширенный установки** кнопки. При нажатии кнопки **расширенный установки**, который проводит toohello **OMS конкретной конфигурации свойства** страницы.

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. Здесь, будет выведено tooenter hello `wsid` (hello идентификатор рабочей области OMS) и `wskey` (hello OMS первичный ключ для hello идентификатор рабочей области). Оба tooget `wsid` и `wskey` требуется учетная запись OMS в toocreate <https://mms.microsoft.com>. Выполните шаги hello toocreate учетную запись. После завершения создания учетной записи hello, вам потребуется tooobtain вашей `wsid` и `wskey` , щелкнув **параметры**, затем **подключенные источники**, а затем **серверы Linux** , как показано ниже.

 ![](media/container-service-monitoring-oms/image5.png)

4. Выберите hello числа вы OMS экземпляров, необходимо и нажмите кнопку «Просмотреть и установить» hello. Как правило следует toohave hello число OMS экземпляры равны toohello количество Виртуальных машин в кластере агент. Агент OMS для Linux — устанавливает как отдельные контейнеры на каждой виртуальной Машине, что ему toocollect сведения для мониторинга и ведения журнала.

## <a name="setting-up-a-simple-oms-dashboard"></a>Настройка простой панели мониторинга OMS

После установки hello агента OMS для Linux на виртуальных машинах hello, следующим шагом является tooset копирование hello мониторинга OMS. Существует два способа toodo это: портала OMS или портала Azure.

### <a name="oms-portal"></a>Портал OMS 

Войдите в портал OMS toohello (<https://mms.microsoft.com>), а toohello **коллекции решений**.

![](media/container-service-monitoring-oms/image6.png)

После входа в hello **коллекции решений**выберите **контейнеры**.

![](media/container-service-monitoring-oms/image7.png)

После выбора hello контейнера решений, вы увидите плитку на странице панели мониторинга OMS Обзор hello hello. После индексируется hello полученный контейнер данных, вы увидите плитку hello, заполненный данными на плитках решений представление.

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a>Портал Azure 

Портал tooAzure входа на <https://portal.microsoft.com/>. Выберите **Marketplace**, **Мониторинг и управление** и **Показать все**. Затем в поле поиска введите `containers`. Вы увидите «контейнеры» в результатах поиска hello. Выберите **Контейнеры** и нажмите кнопку **Создать**.

![](media/container-service-monitoring-oms/image9.png)

После нажатия кнопки **Создать** вам будет предложено выбрать рабочую область. Выберите свою рабочую область, а если у вас ее нет, создайте ее.

![](media/container-service-monitoring-oms/image10.PNG)

Выбрав рабочую область, щелкните **Создать**.

![](media/container-service-monitoring-oms/image11.png)

Дополнительные сведения о hello контейнера решение OMS, можно найти toothe [анализа журналов контейнера решение](../../log-analytics/log-analytics-containers.md).

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a>Как tooscale агента OMS с ACS DC/OS 

В случае необходимости toohave установлен агент OMS во всех остальных случаях hello фактического числа или масштабирование VMSS путем добавления дополнительных виртуальных Машин, это можно сделать путем масштабирования hello `msoms` службы.

Можно перейти tooMarathon или hello вкладку пользовательского интерфейса службы контроллера домена/OS и вертикальное масштабирование на число узлов.

![](media/container-service-monitoring-oms/image12.PNG)

Будет выполнено развертывание tooother узлов, которые еще не установлен агент OMS hello.

## <a name="uninstall-ms-oms"></a>Удаление MS OMS

toouninstall MS OMS введите hello следующую команду:

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a>Сообщите нам!
Что работает? Чего не хватает? Что еще необходимо для этого toobe полезным для вас? Сообщите нам по адресу <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.

## <a name="next-steps"></a>Дальнейшие действия

 Теперь, когда настройки OMS toomonitor вашей контейнеры[просмотра вашей информационной панели контейнера](../../log-analytics/log-analytics-containers.md).
