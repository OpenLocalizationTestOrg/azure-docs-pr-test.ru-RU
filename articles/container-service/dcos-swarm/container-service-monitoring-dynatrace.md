---
title: "кластер Azure DC/OS aaaMonitor - Dynatrace | Документы Microsoft"
description: "Мониторинг кластера DC/OS Службы контейнеров Azure с помощью Dynatrace. Развертывание hello Dynatrace OneAgent с помощью панели мониторинга DC/OS hello."
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: "Контейнеры, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 9e2e2d1c8b454422d1db30dac7c385d31d336853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a>Мониторинг кластера DC/OS в Службе контейнеров Azure с помощью Dynatrace SaaS/Managed
В этой статье мы покажем, как toodeploy hello [Dynatrace](https://www.dynatrace.com/) OneAgent toomonitor все hello агента узлов в кластере служба контейнера Azure. Для работы с этой конфигурацией вам понадобится учетная запись с Dynatrace SaaS/Managed. 

## <a name="dynatrace-saasmanaged"></a>Dynatrace SaaS/Managed
DynaTrace — облачное решение для мониторинга, предназначенное для высокодинамичных сред контейнеров и кластеров. Оно позволяет оптимизировать toobetter развертывания контейнера и выделения памяти с помощью данных об использовании в режиме реального времени. Это решение способно автоматически выявлять проблемы приложений и инфраструктуры, обеспечивая автоматизированное задание базовых показателей, обобщение проблем и определение первопричин.

Hello следующем рисунке показано hello Dynatrace пользовательского интерфейса:

![Пользовательский интерфейс Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a>Предварительные требования 
[Развертывание](container-service-deployment.md) и [подключения](./../container-service-connect.md) tooa кластер настроен службой контейнера Azure. Просмотр hello [Marathon пользовательского интерфейса](container-service-mesos-marathon-ui.md). Go слишком[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset Dynatrace SaaS учетной записи.  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a>Настройка развертывания Dynatrace с использованием Marathon
Следующие шаги показывают, как tooconfigure и развернуть кластер tooyour Dynatrace приложений с Marathon.

1. Откройте пользовательский интерфейс DC/OS по адресу [http://localhost:80/](http://localhost:80/). Один раз в hello DC/OS пользовательского интерфейса, перехода toohello **Universe** и затем найдите **Dynatrace**.

    ![Dynatrace на вкладке "Universe" (Вселенная) DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. Конфигурация toocomplete hello, необходим учетной записи Dynatrace SaaS бесплатную пробную учетную запись. После входа в панель мониторинга Dynatrace hello выберите **развертывание Dynatrace**.

    ![Настройка интеграции PaaS для Dynatrace](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. На странице приветствия выберите **Настройте интеграцию PaaS**. 

    ![Маркер API Dynatrace](./media/container-service-monitoring-dynatrace/api-token.png) 

4. Введите токен API в конфигурацию Dynatrace OneAgent внутри hello вселенной DC/OS hello. 

    ![Конфигурация dynaTrace OneAgent в hello вселенной DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. Номер toohello набора экземпляров hello узлов предполагается toorun. Установка более высокий номер также работает, но DC/OS попытки будут продолжаться новые экземпляры toofind до достижения этого числа фактически. При желании можно также задать это значение tooa как 1000000. В этом случае каждый раз, когда toohello кластер добавляется новый узел, Dynatrace автоматически развертывает агент toothat новый узел, по цене hello постоянно работаем дополнительные экземпляры toodeploy контроллера домена или ОС.

    ![Конфигурация dynaTrace в hello контроллера домена, среда операционной системы-экземпляров](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a>Дальнейшие действия

После установки пакета hello, перейдите назад toohello Dynatrace мониторинга. Вы можете просмотреть hello метрики использования разных контейнеров hello в пределах кластера. 
