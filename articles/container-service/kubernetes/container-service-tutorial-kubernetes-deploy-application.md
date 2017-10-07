---
title: "Учебник контейнера службы aaaAzure - развертывание приложений | Документы Microsoft"
description: "Руководство по Службе контейнеров Azure: развертывание приложения"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7e2fa06d359caf83e684df3966624a6e9a8e7efa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-applications-in-kubernetes"></a>Запуск приложений в Kubernetes

В этом руководстве (часть 4 из 7) выполняется развертывание примера приложения в кластер Kubernetes. В частности, рассматриваются такие шаги:

> [!div class="checklist"]
> * скачивание файлов манифестов Kubernetes;
> * выполнение приложения в Kubernetes;
> * Тестирование приложения hello

В последующих учебники это приложение является горизонтального масштабирования, обновления и Operations Management Suite настраивается toomonitor hello Kubernetes кластера.

В этом учебнике предполагается основные понятия Kubernetes см. подробные сведения о Kubernetes hello [Kubernetes документации](https://kubernetes.io/docs/home/).

## <a name="before-you-begin"></a>Перед началом работы

В предыдущих учебниках приложение было упаковано в образ контейнера, этот образ был отправленного tooAzure реестре контейнеров и Kubernetes кластера был создан. Если вы не были выполнены следующие действия и хотите toofollow вдоль, возвращают слишком[учебник 1 – Создание образов контейнеров](./container-service-tutorial-kubernetes-prepare-app.md). 

Для изучения данного руководства как минимум необходим кластер Kubernetes.

## <a name="get-manifest-file"></a>Получение файла манифеста

В этом руководстве [объекты Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) развертываются с помощью манифеста Kubernetes. Манифест Kubernetes — это файл формата YAML или JSON, содержащий инструкции по развертыванию и настройке объектов Kubernetes.

файл манифеста приложения Hello для этого учебника доступен в репозитории приложения hello голос Azure, которая была клонирована в предыдущем учебнике. Если вы еще не сделали клонируйте репозиторий hello с hello следующую команду: 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

файл манифеста Hello находится в следующий каталог hello клонирования репозитория hello.

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a>Обновление файла манифеста

При использовании образов контейнеров hello toostore реестра контейнера Azure, toobe манифеста потребностей hello дополнен hello loginServer имя записи контроля доступа.

Получить имя входа сервера hello контроля доступа с hello [списка контроля доступа az](/cli/azure/acr#list) команды.

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Hello манифест образец был предварительно созданную с именем репозитория *microsoft*. Откройте файл hello в любом текстовом редакторе и замените hello *microsoft* значение с именем входа сервера hello, контроля доступа экземпляра.

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a>Развертывание приложения

Используйте hello [kubectl создания](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) команды toorun приложения hello. Это команда hello производит синтаксический анализ файла манифеста и создания объектов Kubernetes определенные hello.

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

Выходные данные:

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a>Тестирование приложения

Объект [Kubernetes службы](https://kubernetes.io/docs/concepts/services-networking/service/) создается в результате чего предоставляется toohello приложения hello Интернета. Это может занять несколько минут. 

toomonitor о ходе выполнения, используйте hello [kubectl получить службу](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) с hello `--watch` аргумент.

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

Здравствуйте, изначально **внешний IP-** для hello *azure голос передней панели* службы отображается как *ожидающие*. После hello внешний IP-адрес отличается от *ожидающие* tooan *IP-адрес*, используйте `CTRL-C` toostop hello kubectl Контрольные значения процесса.

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

приложение hello toosee, обзора toohello внешний IP-адрес.

![Схема кластера Kubernetes в Аzure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике hello приложения Azure голос был кластера развернутой tooan Kubernetes службы контейнера Azure. Вам предстоят следующие задачи:  

> [!div class="checklist"]
> * скачивание файлов манифестов Kubernetes;
> * Запустите приложение hello в Kubernetes
> * Протестированные hello приложения

Переместить Далее учебника toolearn toohello о масштабировании hello базовой инфраструктуры Kubernetes и Kubernetes приложения. 

> [!div class="nextstepaction"]
> [Масштабирование pod и инфраструктуры Kubernetes](./container-service-tutorial-kubernetes-scale.md)