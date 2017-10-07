---
title: "веб-перехватчиков реестра контейнера aaaAzure | Документы Microsoft"
description: "Веб-перехватчики реестра контейнеров Azure."
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: "Docker, контейнеры, ACR"
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a>Использование веб-перехватчиков реестра контейнеров Azure с помощью портала Azure

В реестре контейнер Azure хранит данные и управляет частных образов контейнеров Docker, так же как toohello Docker Hub содержит общедоступные образы Docker. Веб-перехватчиков tootrigger события, когда выполнение определенных действий в одном репозитории вашей реестра использовать. Веб-перехватчиков учитывали tooevents на уровне реестра hello или они могут задаваться на работу tooa определенный репозиторий тег. 

Дополнительные сведения и основные понятия в разделе hello [Обзор](./container-registry-intro.md).

## <a name="prerequisites"></a>Предварительные требования 

- Управляемый реестр контейнеров Azure. Создайте управляемый реестр контейнеров в своей подписке Azure. Например использовать портал Azure hello или hello Azure CLI 2.0. 
- Docker CLI - tooset ваш локальный компьютер как узла и доступа к hello Docker CLI команды Docker, установите подсистему Docker. 

## <a name="create-webhook-azure-portal"></a>Создание веб-перехватчика на портале Azure

1. Войдите в портал Azure toohello и перейдите реестра toohello, которой требуется toocreate веб-привязок. 

2. В колонке контейнера hello перейдите на вкладку «Веб-перехватчиков» hello. 

3. Нажмите «Добавить» в колонке веб-перехватчика hello. 

4. Полный hello *создать веб-перехватчика* формы с hello следующую информацию:

| Значение | Описание |
|---|---|
| Имя | Hello имя, которое будет toogive toohello веб-перехватчика. Оно может содержать только 5–50 строчных букв и цифр. |
| URI службы | Здравствуйте, где веб-перехватчика hello следует отправлять уведомления POST URI. |
| Настраиваемые заголовки | Заголовки, которые требуется toopass вместе с запросом POST hello. Они должны быть в формате "ключ: значение". |
| "Trigger actions" (Активирующие действия) | Действия, которые вызывают веб-перехватчика hello. В настоящее время веб-привязок может быть вызвано push и/или удалить изображение tooan действия. |
| Состояние | состояние Hello веб-перехватчика hello после его создания. По умолчанию он включен. |
| Область | область Hello, на котором работает веб-перехватчика hello. По умолчанию hello область — для всех событий в реестре hello. Указанный для репозитория или из тега, используя формат hello» репозитория: тег». |

Пример формы для веб-перехватчика приведен ниже.

![Пользовательский интерфейс DCOS](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a>Создание веб-перехватчика с помощью Azure CLI

Здравствуйте, toocreate веб-перехватчик с помощью Azure CLI, используйте hello [создать веб-перехватчика acr az](/cli/azure/acr/webhook#create) команды.

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a>Проверка веб-перехватчика

### <a name="azure-portal"></a>Портал Azure

Веб-перехватчика hello предыдущих toousing контейнере образ push и удалить действия, его можно проверить при помощи hello **Ping** кнопки. При использовании hello Ping отправляет запрос post в универсальный toohello указало конечной точки и журналы hello ответа. Это может оказаться полезным, hello веб-перехватчика tooverify настроен правильно.

1. Выберите веб-перехватчика hello требуется tootest. 
2. В верхней части панели инструментов hello выберите действие «Проверить связь с» hello. 
3. Проверьте hello запроса и ответа.

### <a name="azure-cli"></a>Инфраструктура CLI Azure

tootest перехватчик контроля доступа с hello Azure CLI, используйте hello [ping веб-перехватчика acr az](/cli/azure/acr/webhook#ping) команды.

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

toosee hello результаты, использование hello [события az acr веб-перехватчика списка](/cli/azure/acr/webhook#list-events) команды. 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a>Удаление веб-перехватчика

### <a name="azure-portal"></a>Портал Azure

Каждый веб-перехватчика могут быть удалены с веб-перехватчика hello, а затем кнопку удаления hello на hello портал Azure.

### <a name="azure-cli"></a>Инфраструктура CLI Azure

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```