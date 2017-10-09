---
title: "aaaAzure экземпляры контейнером - группы нескольких контейнеров | Azure документы"
description: "Служба \"Экземпляры контейнеров Azure\". Многоконтейнерная группа"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 976f578cd2a9bf7f05ab97f24662139bb72062ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-group"></a>Развертывание группы контейнеров

Экземпляры контейнером Azure поддерживает развертывание hello несколько контейнеров на одном узле с помощью *группы контейнеров*. Это полезно при создании сопроводительного приложения для ведения журнала, мониторинга или любой другой конфигурации, когда службе требуется еще один прикрепленный процесс. 

В этом документе рассматривается запуск простой конфигурации многоконтейнерного сопроводительного приложения с использованием шаблона Azure Resource Manager.

## <a name="configure-hello-template"></a>Настройка шаблона hello

Создайте файл с именем `azuredeploy.json` и копирования hello json в него. 

В этом примере определяется группа контейнеров с двумя контейнерами и общедоступным IP-адресом. первый контейнер Hello hello группы выполняется с выходом Интернет-приложения. второй контейнер Hello, сопроводительные hello делает HTTP запроса toohello основной веб-приложение через локальную сеть hello группы. 

В этом примере сопроводительные может быть развернутой tootrigger оповещение, если получен код ответа HTTP, отличным от 200 OK. 

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
  },
  "variables": {
    "container1name": "aci-tutorial-app",
    "container1image": "microsoft/aci-helloworld:latest",
    "container2name": "aci-tutorial-sidecar",    
    "container2image": "microsoft/aci-tutorial-sidecar"
  },
    "resources": [
      {
        "name": "myContainerGroup",
        "type": "Microsoft.ContainerInstance/containerGroups",
        "apiVersion": "2017-08-01-preview",
        "location": "[resourceGroup().location]",
        "properties": {
          "containers": [
            {
              "name": "[variables('container1name')]",
              "properties": {
                "image": "[variables('container1image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                },
                "ports": [
                  {
                    "port": 80
                  }
                ]
              }
            },
            {
              "name": "[variables('container2name')]",
              "properties": {
                "image": "[variables('container2image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                }
              }
            }
          ],
          "osType": "Linux",
          "ipAddress": {
            "type": "Public",
            "ports": [
              {
                "protocol": "tcp",
                "port": "80"
              }
            ]
          }
        }
      }
    ],
    "outputs": {
      "containerIPv4Address": {
        "type": "string",
        "value": "[reference(resourceId('Microsoft.ContainerInstance/containerGroups/', 'myContainerGroup')).ipAddress.ip]"
      }
    }
  }
```

toouse закрытый контейнер реестра образа, добавления документа json объект toohello с hello следующая формата.

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a>Развертывание шаблона hello

Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

Развертывание шаблона hello с hello [создания развертывания группы az](/cli/azure/group/deployment#create) команды.

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

В течение нескольких секунд вы получите исходный ответ Azure. 

## <a name="view-deployment-state"></a>Просмотр состояния развертывания

состояние hello tooview hello развертывания, используйте hello `az container show` команды. Возвращает hello подготовить общедоступный IP-адрес через какие hello доступных приложений.

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

Выходные данные:

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a>Просмотр журналов   

Просмотр выходных данных журнала hello контейнера при помощи hello `az container logs` команды. Hello `--container-name` аргумент указывает контейнер hello из журналов, для которых toopull. В этом примере задается hello первый контейнер. 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

Выходные данные:

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

toosee hello в журналах hello car стороны контейнера, запустите hello же команда Указание имени контейнера второй hello.

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

Выходные данные:

```bash
Every 3.0s: curl -I http://localhost                                                                                                                       Mon Jul 17 11:27:36 2017

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0  0  1663    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
HTTP/1.1 200 OK
Accept-Ranges: bytes
Content-Length: 1663
Content-Type: text/html; charset=utf-8
Last-Modified: Sun, 16 Jul 2017 02:08:22 GMT
Date: Mon, 17 Jul 2017 18:27:36 GMT
```

Как видите, сопроводительные hello периодически выполняет HTTP запроса toohello основной веб-приложения через tooensure hello группы локальной сети, на котором он выполняется.

## <a name="next-steps"></a>Дальнейшие действия

В этом документе рассматривается hello шаги, необходимые для развертывания нескольких контейнер экземпляра контейнер Azure. Tooend окончания работы экземпляров контейнеров Azure см. в учебнике экземпляры контейнером Azure hello.

> [!div class="nextstepaction"]
> [Руководство по службе "Экземпляры контейнеров Azure"]: ./container-instances-tutorial-prepare-app.md
