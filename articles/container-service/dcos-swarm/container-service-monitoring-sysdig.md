---
title: "кластер aaaMonitor контейнера службы Azure с Sysdig | Документы Microsoft"
description: "Мониторинг кластера службы контейнеров Azure с помощью Sysdig."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Контейнеры, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a>Мониторинг кластера службы контейнеров Azure с помощью Sysdig
В этой статье описывается развертывание узлов Sysdig агенты tooall hello агента в кластере службы контейнера Azure. Для работы с этой конфигурацией вам понадобится учетная запись с Sysdig. 

## <a name="prerequisites"></a>Предварительные требования
[Разверните](container-service-deployment.md) и [подключите](../container-service-connect.md) кластер, настроенный службой контейнеров Azure. Просмотр hello [Marathon пользовательского интерфейса](container-service-mesos-marathon-ui.md). Go слишком[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset Sysdig облачной учетной записи. 

## <a name="sysdig"></a>Sysdig
Sysdig является службой мониторинга, которая позволяет вам toomonitor к контейнерам внутри кластера. Sysdig известен toohelp способы устранения неполадок, но также имеет базовые показатели мониторинга для ЦП, сети, памяти и ввода-вывода. Sysdig позволяет легко toosee работе какие контейнеры hello hardest или по существу, используя hello большинство памяти и ЦП. Это представление расположено hello раздела «Обзор», в котором в настоящее время находится в бета-версии. 

![Sysdig: пользовательский интерфейс](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a>Настройка развертывания Sysdig с помощью Marathon
Эти действия демонстрируют, как tooconfigure и развернуть кластер tooyour Sysdig приложений с Marathon. 

Доступ к Интерфейсу DC/OS через [http://localhost: 80 /](http://localhost:80/) один раз в hello DC/OS пользовательского интерфейса выберите toohello «Среда», на hello вниз, влево и выполните поиск «Sysdig».

![Sysdig: раздел "Universe" (Вселенная) DC/OS](./media/container-service-monitoring-sysdig/sysdig1.png)

Теперь конфигурация hello toocomplete необходимо Sysdig облачной учетной записи или бесплатную пробную учетную запись. После входа в toohello Sysdig облачные и веб-сайт, щелкните имя пользователя, и на странице приветствия вы увидите «Ключа доступа.» 

![Sysdig: ключ API](./media/container-service-monitoring-sysdig/sysdig2.png) 

Далее введите ключ доступа в конфигурации Sysdig hello в hello вселенной DC/OS. 

![Конфигурация Sysdig в hello вселенной DC/OS](./media/container-service-monitoring-sysdig/sysdig3.png)

Теперь установите too10000000 экземпляров hello так, чтобы каждый раз при добавлении нового узла кластера toohello Sysdig будет автоматически развернуть агент toothat нового узла. Это промежуточное решение toomake том, что Sysdig развернет tooall новых агентов в пределах кластера hello. 

![Конфигурация Sysdig в hello контроллера домена, среда операционной системы-экземпляров](./media/container-service-monitoring-sysdig/sysdig4.png)

После установки пакета hello Перейдите назад toohello Sysdig пользовательского интерфейса, и вы будете может tooexplore hello различных показателями для контейнеров hello в пределах кластера. 

Вы также можете установить панели мониторинга Mesos и Marathon с помощью [мастера создания панелей мониторинга](https://app.sysdigcloud.com/#/dashboards/new).
