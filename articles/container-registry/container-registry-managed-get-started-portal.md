---
title: "aaaCreate частного реестра Docker - портал Azure | Документы Microsoft"
description: "Начать создание и управление ими частных реестрах контейнера Docker с hello портал Azure"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a>Создание управляемого контейнера реестра, с помощью портала Azure hello

Реестр контейнеров Azure — это управляемая служба реестра контейнеров Docker, используемая для хранения частных образов контейнеров Docker. В этом руководстве рассматривается создание экземпляра управляемого реестра контейнера Azure с помощью портала Azure hello.

Управляемые реестры контейнеров Azure находятся на стадии предварительной версии и не доступны во всех регионах.

## <a name="log-in-tooazure"></a>Войдите в tooAzure

Войдите в систему toohello портал Azure по адресу http://portal.azure.com.

## <a name="create-a-container-registry"></a>Создание реестра контейнеров

1. Нажмите кнопку hello **New** кнопка найдена в верхнем левом углу hello hello портал Azure.

2. Поиск hello marketplace для **контейнер Azure реестра** и выберите его.

3. Нажмите кнопку **создать** которого открывается колонка создания ACR hello.

    ![Параметры реестра контейнеров](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. В hello **реестра контейнера Azure** колонки, введите следующую информацию hello. Закончив, нажмите кнопку **Создать**.

    а. **Имя реестра** — глобальное уникальное доменное имя верхнего уровня для определенного реестра. В этом примере — имя реестра hello *myAzureContainerRegistry1*, но заменить собственным уникальное имя. Hello имя может содержать только буквы и цифры.

    b. **Группа ресурсов**: выберите существующую [группы ресурсов](../azure-resource-manager/resource-group-overview.md#resource-groups) или имя типа hello новую.

    c. **Расположение**: Выбор расположения центра обработки данных Azure, где hello службы [доступных](https://azure.microsoft.com/regions/services/), такие как **центральных штатах юга США**.

    d. **Пользователю с правами администратора**: следует включить в реестре hello tooaccess пользователя администратора. Можно изменить этот параметр после создания hello реестра.

    д. **Использование управляемых реестра**: выберите «Да» toohave ACR автоматически Управление хранилищем реестра hello, использование веб-перехватчиков и использование проверки подлинности AAD.

    f. **Ценовая категория.** Выберите ценовую категорию. См. дополнительные сведения о ценах на ACR.

## <a name="log-in-tooacr-instance"></a>Войдите в экземпляр tooACR

Перед принудительной отправки и извлекать образы контейнеров, необходимо войти в экземпляр toohello контроля доступа. 

Таким образом, toodo используйте hello Azure CLI 2.0. Во-первых, при необходимости войдите в Azure, с помощью hello [входа az](/cli/azure/#login) команды. 

```azurecli
az login
```

Затем используйте hello [входа acr az](/cli/azure/acr#login) toolog команды в toohello реестра контейнера Azure.

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a>Использование реестра контейнеров Azure

### <a name="list-container-images"></a>Список образов контейнеров

Используйте hello `az acr` CLI команды tooquery hello изображения и теги в репозитории.

> [!NOTE]
> В настоящее время реестре контейнеров не поддерживает hello `docker search` tooquery команды для изображений и теги.

### <a name="list-repositories"></a>Вывод списка репозиториев

Hello следующий пример формирует список репозиториев hello в реестре, в формате JSON (JavaScript Object Notation).

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a>Вывод списка тегов

Hello следующий пример отображает список тегов hello на hello **образцы/nginx** репозитория, в формате JSON:

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Дальнейшие действия

В этом кратком руководстве вы создали экземпляр управляемого реестра контейнера Azure, используя hello портал Azure.

> [!div class="nextstepaction"]
> [Принудительная первый образ с помощью hello Docker CLI](container-registry-get-started-docker-cli.md)
