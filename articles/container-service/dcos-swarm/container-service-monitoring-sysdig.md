---
title: "Мониторинг кластера службы контейнеров Azure с помощью Sysdig | Документация Майкрософт"
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
ms.openlocfilehash: e61001161e632a5d2e513107e30f1eaf06103989
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a>Мониторинг кластера службы контейнеров Azure с помощью Sysdig
В этой статье описывается развертывание агентов Sysdig на все узлы агента в кластере службы контейнеров Azure. Для работы с этой конфигурацией вам понадобится учетная запись с Sysdig. 

## <a name="prerequisites"></a>Предварительные требования
[Разверните](container-service-deployment.md) и [подключите](../container-service-connect.md) кластер, настроенный службой контейнеров Azure. Изучите [пользовательский интерфейс Marathon](container-service-mesos-marathon-ui.md). Настройте учетную запись Sysdig на странице [http://app.sysdigcloud.com](http://app.sysdigcloud.com) . 

## <a name="sysdig"></a>Sysdig
Sysdig — это служба мониторинга, которая позволяет отслеживать контейнеры в пределах кластера. Sysdig используется для устранения неполадок, а также для отслеживания базовых метрик ЦП, сети, памяти и ввода-вывода. Sysdig позволяет легко определить, какие контейнеры потребляют больше всего ресурсов, включая память и ЦП. Это представление сейчас доступно в разделе "Обзор" в режиме бета-версии. 

![Sysdig: пользовательский интерфейс](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a>Настройка развертывания Sysdig с помощью Marathon
Ниже описано, как настраивать и развертывать в кластере приложения Sysdig с помощью Marathon. 

Откройте пользовательский интерфейс DC/OS по адресу [http://localhost:80/](http://localhost:80/). Затем щелкните "Universe" (Вселенная) в левом нижнем углу и выполните поиск по запросу "Sysdig".

![Sysdig: раздел "Universe" (Вселенная) DC/OS](./media/container-service-monitoring-sysdig/sysdig1.png)

Чтобы завершить настройку, вам понадобится облачная учетная запись Sysdig или бесплатная пробная учетная запись. Войдите на облачный сайт Sysdig, щелкните свое имя пользователя. На странице отобразится ваш ключ доступа. 

![Sysdig: ключ API](./media/container-service-monitoring-sysdig/sysdig2.png) 

Затем введите ключ доступа в конфигурации Sysdig в разделе "Universe" (Вселенная) DC/OS. 

![Sysdig: конфигурация в разделе "Universe" (Вселенная) DC/OS](./media/container-service-monitoring-sysdig/sysdig3.png)

Теперь укажите для экземпляров значение 10 000 000, чтобы при каждом добавлении узла в кластер в Sysdig автоматически выполнялось развертывание агента на этот новый узел. Это промежуточное решение помогает проверить, выполнит ли Sysdig развертывание на всех новых агентах в рамках кластера. 

![Sysdig: конфигурация в разделе "Universe" (Вселенная) DC/OS; экземпляры](./media/container-service-monitoring-sysdig/sysdig4.png)

Установите пакет, затем вернитесь в пользовательский интерфейс Sysdig. Там вы сможете просмотреть разные метрики использования ресурсов контейнерами в рамках кластера. 

Вы также можете установить панели мониторинга Mesos и Marathon с помощью [мастера создания панелей мониторинга](https://app.sysdigcloud.com/#/dashboards/new).
