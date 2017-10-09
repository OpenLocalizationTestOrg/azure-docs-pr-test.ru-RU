---
title: "aaaManage Azure Kubernetes кластер с веб-Интерфейсе | Документы Microsoft"
description: "С помощью hello Kubernetes веб-интерфейсом пользователя в службе контейнера Azure"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a>С помощью hello Kubernetes веб-интерфейсом пользователя с помощью контейнера службы Azure

## <a name="prerequisites"></a>Предварительные требования
В этом пошаговом руководстве предполагается, что вы [создали кластер Kubernetes с помощью службы контейнеров Azure](container-service-kubernetes-walkthrough.md).


Также предполагается, что имеется hello Azure CLI 2.0 и `kubectl` установлены инструменты.

Можно проверить при наличии hello `az` установить, запустив средство:

```console
$ az --version
```

Если у вас нет hello `az` средство установки приведены инструкции по [здесь](https://github.com/azure/azure-cli#installation).

Можно проверить при наличии hello `kubectl` установить, запустив средство:

```console
$ kubectl version
```

Если средство `kubectl` не установлено, выполните команду:

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a>Обзор

### <a name="connect-toohello-web-ui"></a>Подключиться к Интернету toohello пользовательского интерфейса
Hello Kubernetes пользовательского веб-интерфейса можно запустить с помощью команды:

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

Откроется веб-браузер настроен tootalk tooa безопасного прокси подключения на локальном компьютере toohello Kubernetes веб-интерфейса.

### <a name="create-and-expose-a-service"></a>Создание и предоставление службы
1. В веб-Kubernetes hello пользовательского интерфейса, нажмите кнопку **создать** кнопка в верхнем правом окне приветствия.

    ![Кнопка Create (Создать) в веб-интерфейсе Kubernetes](./media/container-service-kubernetes-ui/create.png)

    При этом откроется диалоговое окно, в котором можно приступить к созданию приложения.

2. Присвойте ему имя hello `hello-nginx`. Используйте hello [ `nginx` контейнера Docker](https://hub.docker.com/_/nginx/) и развернуть три реплики этой веб-службы.

    ![Диалоговое окно создания модуля Kubernetes](./media/container-service-kubernetes-ui/nginx.png)

3. В разделе **Service** (Служба) выберите вариант **External** (Внешняя) и укажите порт 80.

    Этот параметр балансировку нагрузки трафика toohello три реплики.

    ![Диалоговое окно создания службы Kubernetes](./media/container-service-kubernetes-ui/service.png)

4. Нажмите кнопку **развернуть** toodeploy эти контейнеры и службы.

    ![Развертывание Kubernetes](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a>Просмотр контейнеров
После нажатия кнопки **развернуть**, hello пользовательского интерфейса показано представление в виде службы, как развертывания:

![Состояние Kubernetes](./media/container-service-kubernetes-ui/status.png)

Состояние каждого объекта Kubernetes в кружке hello hello hello левой части пользовательского интерфейса, можно отслеживать в разделе **модулей**. Если это частично полный круг hello объекта по-прежнему развертывание. Когда объект будет полностью развернут, отобразится зеленая галочка:

![Объект Kubernetes развернут](./media/container-service-kubernetes-ui/deployed.png)

Как только все работает, выберите один из модулей toosee подробные сведения о hello выполнение веб-службы.

![Модули Kubernetes](./media/container-service-kubernetes-ui/pods.png)

В hello **модулей** представления, можно просмотреть информацию о контейнерах hello в hello pod, а также hello ЦП и памяти ресурсы, используемые в этих контейнерах:

![Ресурсы Kubernetes](./media/container-service-kubernetes-ui/resources.png)

Если вы не видите hello ресурсы, может потребоваться toowait через несколько минут для мониторинга данных toopropagate hello.

toosee hello журналы для контейнера, нажмите кнопку **Просмотр журналов**.

![Журналы Kubernetes](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a>Просмотр службы
В дополнение toorunning вашей контейнеры hello Kubernetes пользовательского интерфейса создал внешней `Service` которого подготавливает контейнерам нагрузки балансировки toobring трафика toohello в кластере.

Hello панели навигации слева щелкните **службы** tooview все службы (должна быть только одна).

![Службы Kubernetes](./media/container-service-kubernetes-ui/service-deployed.png)

В этом представлении вы увидите внешнюю конечную точку (IP-адрес), занятый tooyour службы.
Если щелкнуть этот IP-адрес, то отобразится контейнер Nginx, выполняющийся за подсистемой балансировки нагрузки.

![Представление nginx](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a>Изменение размеров службы
В дополнение tooviewing объектов в Здравствуйте пользовательского интерфейса, можно изменить и обновить объекты Kubernetes API hello.

Во-первых, нажмите кнопку **развертываний** в hello слева развертывания hello toosee панель навигации для службы.

После входа в это представление, щелкните на наборе реплик hello и нажмите кнопку **изменить** hello верхней навигационной панели:

![Окно изменения в Kubernetes](./media/container-service-kubernetes-ui/edit.png)

Изменить hello `spec.replicas` toobe поле `2`и нажмите кнопку **обновление**.

В этом случае hello число tootwo toodrop реплик, удалив один из вашего модулей.

 

