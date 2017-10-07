---
title: "aaaLoad сбалансировать Kubernetes контейнеры в Azure | Документы Microsoft"
description: "Подключайтесь извне и выполняйте балансировку нагрузки нескольких контейнеров в кластере Kubernetes в Службе контейнеров Azure."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Контейнеры, микрослужбы, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 8073c8d3a015a53a532c326749571cb2582e1bac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a>Балансировка нагрузки контейнеров в кластере Kubernetes в Службе контейнеров Azure 
В этой статье рассматривается балансировка нагрузки в кластере Kubernetes в Службе контейнеров Azure. Балансировка нагрузки предоставляет доступном IP-адрес для службы hello и распределяет сетевой трафик между стойками hello выполнение в агенте ВМ.

Можно настроить службы Kubernetes toouse [подсистемы балансировки нагрузки Azure](../../load-balancer/load-balancer-overview.md) toomanage внешний трафик сети (TCP). Благодаря дополнительной настройке возможна балансировка нагрузки и маршрутизация трафика HTTP или HTTPS или более сложные сценарии.

## <a name="prerequisites"></a>Предварительные требования
* [Развертывание кластера Kubernetes](container-service-kubernetes-walkthrough.md) в Службе контейнеров Azure
* [Подключите клиента](../container-service-connect.md) tooyour кластера

## <a name="azure-load-balancer"></a>Azure Load Balancer

По умолчанию Kubernetes кластер, развернутых в службе контейнера Azure включает в себя балансировки нагрузки Azure с выходом в Интернет для hello агента ВМ. (Ресурс балансировки нагрузки на отдельные настроен для образца hello виртуальные машины). Azure Load Balancer является подсистемой балансировки нагрузки 4-го уровня. В настоящее время hello балансировки нагрузки поддерживает только TCP-трафика в Kubernetes.

При создании службы Kubernetes toohello hello нагрузки Azure балансировки tooallow доступ службы можно настроить автоматически. подсистемы балансировки нагрузки hello tooconfigure, набор hello службы `type` слишком`LoadBalancer`. Hello балансировки нагрузки создает toomap правило общедоступный IP-адрес и номер порта входящего трафика toohello частных IP-адресов службы и номера портов hello модулей в агенте виртуальных машин (и, наоборот, для ответного трафика). 

 Ниже приведены два примера, показывающий, как tooset hello Kubernetes службы `type` слишком`LoadBalancer`. (После идет примеры hello, удалите hello развертывания, если они больше не нужны.)

### <a name="example-use-hello-kubectl-expose-command"></a>Пример: Используйте hello `kubectl expose` команды 
Hello [Kubernetes Пошаговое руководство](container-service-kubernetes-walkthrough.md) включает пример tooexpose службы с hello `kubectl expose` команды и ее `--type=LoadBalancer` флаг. Ниже приведены шаги hello.

1. Запустите новое развертывание контейнера. Здравствуйте, например, следующая команда запускает вызывается новое развертывание `mynginx`. Развертывание Hello состоит из трех контейнеров на основе образа Docker hello для веб-сервер Nginx hello.

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. Убедитесь, что запущена hello контейнеров. Например, если вы запрашиваете hello контейнерами с помощью `kubectl get pods`, появится примерно toohello следующие выходные данные:

    ![Получение контейнеров Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. tooconfigure hello нагрузки балансировки tooaccept внешнего трафика toohello развертывания, запустите `kubectl expose` с `--type=LoadBalancer`. Hello следующая команда предоставляет сервер Nginx hello на порт 80.

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. Тип `kubectl get svc` toosee hello состояния служб hello в кластере hello. Здравствуйте, пока балансировки нагрузки hello настраивает правила hello, `EXTERNAL-IP` из hello службы отображается как `<pending>`. Через несколько минут hello внешнего IP-адреса: 

    ![Настройка Azure Load Balancer](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. Убедитесь, что доступ к службе hello hello внешний IP-адрес. Например откройте веб-браузер toohello IP адрес показано. Hello браузер отображает веб-сервер Nginx hello, работающих в одном из контейнеров hello. Или выполнения hello `curl` или `wget` команды. Например:

    ```
    curl 13.82.93.130
    ```

    Должен отобразиться примерно такой результат:

    ![Доступ к Nginx с использованием curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. toosee hello конфигурации подсистемы балансировки нагрузки Azure hello, последовательно выберите toohello [портал Azure](https://portal.azure.com).

7. Поиск hello группы ресурсов для службы кластера контейнер и выберите hello балансировки нагрузки для hello агент ВМ. То же, что контейнер службы hello следует hello его имя. (Не выбора hello подсистемы балансировки нагрузки для hello главных узлов, один, имя которого содержит hello **балансировки нагрузки master**.) 

    ![Балансировщик нагрузки в группе ресурсов](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. Щелкните toosee hello сведения о конфигурации подсистемы балансировки нагрузки hello, **правила подсистемы балансировки нагрузки** и hello имя правила hello, который был настроен.

    ![Правила балансировщика нагрузки](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a>Пример: Задание `type: LoadBalancer` в файле конфигурации службы hello

При развертывании приложения контейнера Kubernetes из YAML или JSON [файла конфигурации службы](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), укажите внешней подсистемы балансировки нагрузки, добавив hello спецификации службы toohello строки:

```YAML
 "type": "LoadBalancer"
``` 



Hello Далее используется hello Kubernetes [примере гостевую](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook). Этот пример является многоуровневым веб-приложением на основе образов Redis и PHP Docker. Можно указать в файле конфигурации службы hello hello балансировки нагрузки Azure использует этот сервер PHP hello переднего плана.

1. Загрузите файл hello `guestbook-all-in-one.yaml` из [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one). 
2. Поиск hello `spec` для hello `frontend` службы.
3. Раскомментируйте строку hello `type: LoadBalancer`.

    ![Балансировщик нагрузки в конфигурации службы](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. Сохраните файл hello и разверните приложение hello, выполнив следующую команду hello:

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. Тип `kubectl get svc` toosee hello состояния служб hello в кластере hello. Здравствуйте, пока балансировки нагрузки hello настраивает правила hello, `EXTERNAL-IP` из hello `frontend` службы отображается как `<pending>`. Через несколько минут hello внешнего IP-адреса: 

    ![Настройка Azure Load Balancer](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. Убедитесь, что доступ к службе hello hello внешний IP-адрес. Например можно открыть веб браузера toohello внешний IP-адрес службы hello.

    ![Внешний доступ к гостевой книге](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    Вы можете добавить записи гостевой книги.

7. toosee hello конфигурации подсистемы балансировки нагрузки Azure hello, поиск ресурсов подсистемы балансировки нагрузки hello для кластера hello в hello [портал Azure](https://portal.azure.com). См. шаги hello в предыдущем примере hello.

### <a name="considerations"></a>Рекомендации

* Создание правила подсистемы балансировки нагрузки hello происходит асинхронно, и данные балансировки hello подготовить публикуются в службе hello `status.loadBalancer` поля.
* Каждая служба автоматически назначается свой собственный виртуальный IP-адрес в hello балансировки нагрузки.
* Если требуется балансировки нагрузки hello tooreach DNS-именем, работаете с вашей toocreate поставщика службы доменных DNS-имя для правила hello IP-адреса.

## <a name="http-or-https-traffic"></a>Трафик HTTP или HTTPS

Баланс tooload HTTP или HTTPS toocontainer трафик веб-приложений и управление сертификатами для безопасности транспортного уровня (TLS), можно использовать hello Kubernetes [входящих](https://kubernetes.io/docs/user-guide/ingress/) ресурсов. Входящие — это совокупность правила, разрешающие входящие подключения службы кластеров tooreach hello. Для входящих сообщений toowork ресурсов, hello Kubernetes кластер должен иметь [входящих контроллера](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) под управлением.

Служба контейнеров Azure не реализует контроллер Ingress Kubernetes автоматически. Доступны несколько реализаций контроллера. В настоящее время hello [Nginx входящих контроллера](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) рекомендуется tooconfigure входящих правил и балансировки нагрузки трафика HTTP и HTTPS. 

Дополнительные сведения см. в разделе hello [Nginx входящих контроллер документация](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).

> [!IMPORTANT]
> При использовании hello контроллера Nginx входящих сообщений в службе контейнера Azure, должен предоставлять развертывания контроллера hello как служба с `type: LoadBalancer`. Это настраивает toohello hello нагрузки Azure балансировки tooroute трафика контроллера. Дополнительные сведения см. в разделе hello предыдущего раздела.


## <a name="next-steps"></a>Дальнейшие действия

* В разделе hello [документации Kubernetes Подсистема балансировки нагрузки](https://kubernetes.io/docs/user-guide/load-balancer/)
* Узнайте больше о [контроллерах Ingress Kubernetes](https://kubernetes.io/docs/user-guide/ingress/)
* Ознакомьтесь с [примерами Kubernetes](https://github.com/kubernetes/kubernetes/tree/master/examples)

