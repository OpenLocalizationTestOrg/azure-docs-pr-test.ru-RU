---
title: "кластер Azure DC/OS aaaMonitor - Datadog | Документы Microsoft"
description: "Мониторинг кластера службы контейнеров Azure с помощью Datadog. Использование hello DC/OS web пользовательского интерфейса toodeploy hello Datadog агенты tooyour кластера."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Контейнеры, DC/OS, Docker Swarm, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a>Мониторинг кластера DC/OS в Службе контейнеров Azure с помощью Datadog
В этой статье описывается развертывание узлов Datadog агенты tooall hello агента в кластере службы контейнера Azure. Для работы с этой конфигурацией вам понадобится учетная запись с Datadog. 

## <a name="prerequisites"></a>Предварительные требования
[Разверните](container-service-deployment.md) и [подключите](../container-service-connect.md) кластер, настроенный службой контейнеров Azure. Просмотр hello [Marathon пользовательского интерфейса](container-service-mesos-marathon-ui.md). Go слишком[http://datadoghq.com](http://datadoghq.com) tooset Datadog учетной записи. 

## <a name="datadog"></a>Datadog
Datadog представляет собой службу мониторинга, которая собирает данные мониторинга из контейнеров в кластере службы контейнеров Azure. Datadog имеет панель мониторинга интеграции с Docker, в которой вы можете увидеть некоторые метрики своих контейнеров. Метрики контейнеров собраны в несколько групп: ЦП, память, сеть и ввод-вывод. Datadog разделяет метрики по контейнерам и образам. Примером какие hello пользовательского интерфейса похоже для ЦП использования ниже.

![Пользовательский интерфейс Datadog](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a>Настройка развертывания Datadog с помощью Marathon
Эти действия демонстрируют, как tooconfigure и развернуть кластер tooyour Datadog приложений с Marathon. 

Откройте пользовательский интерфейс DC/OS по адресу [http://localhost:80/](http://localhost:80/). Один раз в hello перейдите пользовательского интерфейса DC/OS toohello «Среда», находящийся на hello вниз, влево и выполните поиск «Datadog» и нажмите кнопку «Установить».

![Пакет Datadog в hello вселенной DC/OS](./media/container-service-monitoring/datadog1.png)

Теперь конфигурация hello toocomplete, вам потребуется учетной записи Datadog или бесплатную пробную учетную запись. После входа в веб-сайт Datadog toohello найдите toohello влево и перейти tooIntegrations ->, затем [API-интерфейсы](https://app.datadoghq.com/account/settings#api). 

![Ключ API Datadog](./media/container-service-monitoring/datadog2.png)

Затем введите ваш ключ API в конфигурацию Datadog hello внутри hello вселенной DC/OS. 

![Конфигурация Datadog в hello вселенной DC/OS](./media/container-service-monitoring/datadog3.png) 

В hello выше конфигурации экземпляров устанавливаются too10000000, поэтому каждый раз при добавлении нового узла кластера toohello Datadog автоматически развертывать узел toothat агента. Это промежуточное решение. После установки пакета hello следует перейти назад toohello Datadog веб-сайта и найти «[панелей мониторинга](https://app.datadoghq.com/dash/list).» Здесь вы увидите пользовательские панели мониторинга и панели интеграции. Hello [Docker мониторинга](https://app.datadoghq.com/screen/integration/docker) будет иметь все метрики контейнера hello, необходимые для мониторинга кластера. 

