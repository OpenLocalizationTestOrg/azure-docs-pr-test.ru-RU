---
title: "пулы агентов aaaDC/OS для контейнера службы Azure | Документы Microsoft"
description: "Как работают пулы агентов открытых и закрытых hello с кластер контейнера службы Azure DC/OS"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a>Пулы агентов DC/OS для службы контейнеров Azure
Кластеры DC/OS службы контейнеров Azure содержат узлы агентов в двух пулах —общедоступном и частном. Приложения могут развертываться tooeither пула, влияя на доступность между машинами в контейнере службы. Hello машины могут быть предоставляется toohello Интернета (public) или внутренний (частный) сохраняются. В этой статье приводятся общие сведения о причинах использования общедоступных и частных пулов.


* **Частные агенты**: частные узлы агентов работают в сети без глобальной маршрутизации. Эта сеть доступна только из зоны hello администрирования или с помощью hello открытый зоны пограничный маршрутизатор. По умолчанию DC/OS запускает приложения на частных узлах агента. 

* **Общедоступные агенты**: общедоступные узлы агентов выполняют приложения и службы DC/OS в общедоступной сети. 

Дополнительные сведения о сетевой безопасности контроллера домена/OS см. в разделе hello [документации DC/OS](https://dcos.io/docs/1.7/administration/securing-your-cluster/).

## <a name="deploy-agent-pools"></a>Развертывание пулов агента

пулы агентов DC/OS Hello в контейнере службы Azure создаются следующим образом:

* Hello **закрытый пула** содержит hello число узлов агента, укажите время вы [развертывание кластера DC/OS hello](container-service-deployment.md). 

* Hello **открытый пул** изначально содержит заранее заданное количество узлов агента. Этот пул добавляется автоматически при подготовке кластера DC/OS hello.

закрытый пула Hello и открытые пула hello являются наборы масштабирования виртуальной машины Azure. Размер этих пулов можно изменить после развертывания.

## <a name="use-agent-pools"></a>Использование пулов агента
По умолчанию **Marathon** развертывает все новые приложения toohello *закрытый* узлы агентов. У вас есть tooexplicitly развертывание toohello приложения hello *открытый* узлов во время создания приложения hello hello. Выберите hello **необязательно** вкладку и введите **slave_public** для hello **принят ролей ресурса** значение. Этот процесс описан в [здесь](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) и в hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) документации.

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте больше об [управлении контейнерами DC/OS](container-service-mesos-marathon-ui.md).

* Узнайте, каким образом слишком[открыть брандмауэр hello](container-service-enable-public-access.md) , предоставляемые Azure tooallow общего доступа tooyour DC/OS контейнеров.

