---
title: "кластер Azure DC/OS - стек ELK aaaMonitor | Документы Microsoft"
description: "Мониторинг кластера DC/OS в кластере службы контейнеров Azure с помощью ELK (Elasticsearch, Logstash и Kibana)."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Контейнеры, DC/OS, Azure, мониторинг, elk"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 8d81c5342616ec14880d38803cdf95f5845a669b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a>Мониторинг кластера службы контейнеров Azure с помощью ELK
В этой статье показано, как стека toodeploy hello ELK (Elasticsearch Logstash, Kibana) в кластере DC/OS в контейнере службы Azure. 

## <a name="prerequisites"></a>Предварительные требования
[Развертывание](container-service-deployment.md) и [подключение](../container-service-connect.md) кластера DC/OS, настроенного службой контейнеров Azure. Просматривать панели мониторинга hello DC/OS и службы Marathon [здесь](container-service-mesos-marathon-ui.md). Также установить hello [балансировки нагрузки Marathon](container-service-load-balancing.md).


## <a name="elk-elasticsearch-logstash-kibana"></a>ELK (Elasticsearch, Logstash, Kibana)
Стек ELK представляет собой сочетание Elasticsearch Logstash, и Kibana, предоставляющий tooend конец стека, который можно использовать toomonitor и анализировать журналы в кластере.

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a>Настройка hello ELK стека в кластере DC/OS
Доступ к Интерфейсу DC/OS через [http://localhost: 80 /](http://localhost:80/) один раз в hello пользовательского интерфейса DC/OS перейдите слишком**вселенной**. Поиск и установка Elasticsearch, Logstash и Kibana из hello вселенной DC/OS и что-либо порядка перечисления. Дополнительные сведения о конфигурации в случае перехода toohello **расширенный установки** ссылку.

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

Один раз Здравствуйте ELK контейнеры и являются запуска, необходимо получить с помощью балансировки Нагрузки Marathon toobe Kibana tooenable. Перейдите в слишком **службы** > **kibana**и нажмите кнопку **изменить** как показано ниже.

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


Переключение слишком**режим JSON** и найдите раздел toohello метки.
Требуется tooadd `"HAPROXY_GROUP": "external"` здесь запись как показано ниже.
После нажатия кнопки **Deploy changes** (Развернуть изменения) контейнер будет перезагружен.

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


Если вы хотите tooverify, Kibana зарегистрирован в качестве службы на панели мониторинга HAPROXY hello, требуется порт tooopen 9090 в кластере агент hello как HAPROXY использует порт 9090.
По умолчанию мы открывать порты 80, 8080 и 443 в hello DC/OS агента кластера.
Инструкции tooopen порт и предоставить открытый оценки предоставляются [здесь](container-service-enable-public-access.md).

Здравствуйте, tooaccess HAPROXY панели мониторинга, откройте hello балансировки Нагрузки Marathon интерфейса администратора на: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.
После перейти toohello URL-адрес, вы увидите панель мониторинга HAPROXY hello, как показано ниже, и вы увидите записи службы для Kibana.

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


панель Kibana hello tooaccess, в которой развертывается на порт 5601, требуется порт tooopen 5601. Инструкции см. [здесь](container-service-enable-public-access.md). Откройте панель мониторинга Kibana hello в: `http://localhost:5601`.

## <a name="next-steps"></a>Дальнейшие действия

* Чтобы узнать о пересылке и настройке системного журнала и журнала приложений, изучите раздел [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/) (Управление журналами в DC/OS с помощью ELK).

* см. журналы toofilter [фильтрации журналов с помощью ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/). 

 

