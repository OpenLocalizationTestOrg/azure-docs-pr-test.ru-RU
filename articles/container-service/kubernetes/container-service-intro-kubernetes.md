---
title: "aaaIntroduction tooAzure контейнер службы для Kubernetes | Документы Microsoft"
description: "Служба Azure контейнер для Kubernetes делает простой toodeploy и управлять приложениями на основе контейнера в Azure."
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kubernetes, Docker, контейнеры, микрослужбы, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a>Введение tooAzure контейнер службы для Kubernetes
Служба Azure контейнер для Kubernetes делает простой toocreate, настройки и управления кластера виртуальных машин, которые являются предварительно настроенных toorun контейнерных приложений. Это позволяет вам toouse существующие навыки работы или рисования при растущих части опытом сообщества, toodeploy и управлять приложениями на основе контейнера на Microsoft Azure.

С помощью контейнера службы Azure, можно воспользоваться преимуществами hello функций корпоративного уровня, Azure, одновременно сохраняя переносимость приложения через Kubernetes и hello Docker формат изображения.

## <a name="using-azure-container-service-for-kubernetes"></a>Использование службы контейнеров Azure для Kubernetes
Наша цель, с помощью контейнера службы Azure — tooprovide среды размещения контейнера с помощью средств с открытым исходным кодом и технологии, которые часто используются для наших заказчиков сегодня. конец toothis мы предоставляем hello стандартные конечные точки Kubernetes API. Используя эти стандартные конечные точки, может использовать программное обеспечение, которое поддерживает обмен данными tooa Kubernetes кластера. Например, можно выбрать [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [Helm](https://helm.sh/) или [Draft](https://github.com/Azure/draft).

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a>Создание кластера Kubernetes с помощью службы контейнеров Azure
toobegin с помощью контейнера службы Azure, развернуть кластер контейнера службы Azure с hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) или через портал hello (hello поиска Marketplace для **контейнера службы Azure**). Опытных пользователей, которым необходим больший контроль над hello шаблоны диспетчера ресурсов Azure можно использовать Привет открыть источник [acs ядра](https://github.com/Azure/acs-engine) toobuild проект собственных пользовательских Kubernetes кластера и его развертывания через hello `az` CLI.

### <a name="using-kubernetes"></a>Использование Kubernetes
Kubernetes автоматизирует развертывание, масштабирование приложений-контейнеров и управление ими. Это решение предоставляет обширный набор возможностей, в том числе:
* автоматическая упаковка в контейнеры;
* самовосстановление;
* горизонтальное масштабирование;
* обнаружение служб и балансировка нагрузки;
* автоматические обновления и откаты;
* управление секретами и конфигурациями;
* оркестрация хранилища;
* пакетное выполнение.

Архитектура службы Kubernetes, развернутой с помощью службы контейнеров Azure:

![Служба Azure контейнера настроен toouse Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a>Видеоролики

Поддержка Kubernetes в службе контейнеров ("Пятница с Azure", январь 2017 г.):

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

Средства разработки и развертывания приложений в Kubernetes (Azure OpenDev, июнь 2017 г.):

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a>Дальнейшие действия

Просмотр hello [краткое руководство Kubernetes](container-service-kubernetes-walkthrough.md) toobegin сегодня изучение контейнера службы Azure.
