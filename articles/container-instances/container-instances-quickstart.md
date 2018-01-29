---
title: "Краткое руководство. Создание первого контейнера в службе \"Экземпляры контейнеров Azure\""
description: "Начало работы со службой \"Экземпляры контейнеров Azure\" и развертывание в ней"
services: container-instances
author: seanmck
manager: timlt
ms.service: container-instances
ms.topic: quickstart
ms.date: 01/02/2018
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 4c7f48c993d66dd79538fd73ccaed1355c2e8cdd
ms.sourcegitcommit: 9890483687a2b28860ec179f5fd0a292cdf11d22
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/24/2018
---
# <a name="create-your-first-container-in-azure-container-instances"></a>Создание первого контейнера в службе "Экземпляры контейнеров Azure"
Служба "Экземпляры контейнеров Azure" упрощает создание контейнеров Docker и управление ими в Azure, избавляя от необходимости подготавливать виртуальные машины или применять службу более высокого уровня. В этом кратком руководстве вы создадите контейнер в Azure и предоставите к нему доступ в Интернете по общедоступному IP-адресу. Эта операция выполняется при помощи одной команды. Через несколько секунд в браузере отобразится следующее.

![Приложение, развернутое с помощью службы "Экземпляры контейнеров Azure" (просмотр в браузере)][aci-app-browser]

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись][azure-account], прежде чем начинать работу.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Для выполнения инструкций этого краткого руководства можно использовать Azure Cloud Shell или локальный экземпляр Azure CLI. Если вы решили установить и использовать CLI локально, для выполнения инструкций из этого руководства вам потребуется Azure CLI 2.0.21 или более поздней версии. Чтобы узнать версию, выполните команду `az --version`. Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0][azure-cli-install].

## <a name="create-a-resource-group"></a>Создание группы ресурсов

Служба "Экземпляры контейнеров Azure" является ресурсом Azure и должна быть помещена в группу ресурсов Azure — логическую коллекцию, в которой выполняется развертывание ресурсов Azure и управление ими.

Создайте группу ресурсов с помощью команды [az group create][az-group-create].

В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *eastus*.

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a>Создание контейнера

Чтобы создать контейнер, нужно указать его имя, образ Docker и группу ресурсов Azure в команде [az container create][az-container-create]. Либо же можно предоставить контейнер в Интернете по общедоступному IP-адресу. В ходе работы с этим руководством вы развернете контейнер, содержащий небольшое веб-приложение, написанное на языке [Node.js][node-js].

```azurecli-interactive
az container create --resource-group myResourceGroup --name mycontainer --image microsoft/aci-helloworld --ip-address public --ports 80
```

Через несколько секунд вы должны получить ответ на запрос. Изначально контейнер находится в состоянии **Создание**, но через несколько секунд он запустится. Вы можете проверить состояние, выполнив команду [az container show][az-container-show]:

```azurecli-interactive
az container show --resource-group myResourceGroup --name mycontainer
```

В нижней части окна выходных данных отобразятся сведения о состоянии подготовки контейнера и его IP-адрес:

```json
...
"ipAddress": {
      "ip": "13.88.176.27",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "location:": "eastus",
    "name": "mycontainer",
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

Когда контейнер перейдет в состояние **успешного выполнения**, к нему можно будет получить доступ в браузере по указанному IP-адресу.

![Приложение, развернутое с помощью службы "Экземпляры контейнеров Azure" (просмотр в браузере)][aci-app-browser]

## <a name="pull-the-container-logs"></a>Извлечение журналов контейнера

Вы можете извлечь журналы для созданного контейнера с помощью команды [az container logs][az-container-logs]:

```azurecli-interactive
az container logs --resource-group myResourceGroup --name mycontainer
```

Выходные данные:

```bash
listening on port 80
::ffff:10.240.255.107 - - [29/Nov/2017:20:48:50 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.3202.94 Safari/537.36"
::ffff:10.240.255.107 - - [29/Nov/2017:20:48:50 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://52.224.178.107/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.3202.94 Safari/537.36"
```

## <a name="delete-the-container"></a>Удаление контейнера

По завершении работы с контейнером его можно удалить с помощью команды [az container delete][az-container-delete]:

```azurecli-interactive
az container delete --resource-group myResourceGroup --name mycontainer
```

Чтобы проверить, удален ли контейнер, выполните команду [az container list](/cli/azure/container#az_container_list).

```azurecli-interactive
az container list --resource-group myResourceGroup --output table
```

Контейнер **mycontainer** не должен отображаться в выходных данных этой команды. Если у вас нет других контейнеров в группе ресурсов, выходные данные будут отсутствовать.

## <a name="next-steps"></a>Дополнительная информация

Полный код для контейнера, используемого в этом кратком руководстве, и файл Dockerfile доступны [на сайте GitHub][app-github-repo]. Если вы хотите выполнить сборку самостоятельно и развернуть контейнер в службе "Экземпляры контейнеров Azure" с помощью реестра контейнеров Azure, продолжайте изучение руководств по этой службе.

> [!div class="nextstepaction"]
> [Руководства по использованию службы "Экземпляры контейнеров Azure"](./container-instances-tutorial-prepare-app.md)

Чтобы проверить параметры запуска контейнеров в системе оркестрации Azure, см. краткие руководства по [Service Fabric][service-fabric] или [ службе контейнеров Azure (AKS)][container-service].

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png

<!-- LINKS - External -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git
[azure-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F
[node-js]: http://nodejs.org

<!-- LINKS - Internal -->
[az-group-create]: /cli/azure/group?view=azure-cli-latest#az_group_create
[az-container-create]: /cli/azure/container?view=azure-cli-latest#az_container_create
[az-container-delete]: /cli/azure/container?view=azure-cli-latest#az_container_delete
[az-container-list]: /cli/azure/container?view=azure-cli-latest#az_container_list
[az-container-logs]: /cli/azure/container?view=azure-cli-latest#az_container_logs
[az-container-show]: /cli/azure/container?view=azure-cli-latest#az_container_show
[azure-cli-install]: /cli/azure/install-azure-cli
[container-service]: ../aks/kubernetes-walkthrough.md
[service-fabric]: ../service-fabric/service-fabric-quickstart-containers.md
