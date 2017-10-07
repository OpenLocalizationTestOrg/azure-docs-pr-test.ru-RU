---
title: "aaaService участника для кластера Azure Kubernetes | Документы Microsoft"
description: "Сведения о настройке субъекта-службы Azure Active Directory для кластера Kubernetes и управлении им в Службе контейнеров Azure."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 7a01624c5ac3fa717dbcbd570e05ceb4d917c53a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a>Настройка субъекта-службы Azure AD для кластера Kubernetes в Службе контейнеров


В контейнере службы Azure, требуется кластер Kubernetes [участника-службы Azure Active Directory](../../active-directory/develop/active-directory-application-objects.md) toointeract с API-интерфейсов Azure. Hello участника-службы требуется toodynamically управления ресурсами, такими как [определяемых пользователем маршрутов](../../virtual-network/virtual-networks-udr-overview.md) и hello [подсистемы балансировки нагрузки уровня 4 Azure](../../load-balancer/load-balancer-overview.md). 


В этой статье показано tooset различные параметры службы для кластера Kubernetes участника. Например, если необходимо установить и настроить hello [Azure CLI 2.0](/cli/azure/install-az-cli2), можно запустить hello [ `az acs create` ](/cli/azure/acs#create) toocreate команда hello в hello субъектом-службой кластера и hello Kubernetes то же время.


## <a name="requirements-for-hello-service-principal"></a>Требования к субъекту-службе hello

Можно использовать существующий субъект службы Azure AD, соответствует hello следующие требования, или создать новый.

* **Область**: hello группы ресурсов в подписке hello используемого кластера Kubernetes toodeploy hello, или (менее restrictively) hello подписки toodeploy hello кластера.

* **Роль** — **Участник**.

* **Секрет клиента** — должен быть паролем. Сейчас субъект-службу нельзя использовать для проверки подлинности сертификата.

> [!IMPORTANT] 
> toocreate участника-службы, необходимо иметь разрешения tooregister приложение с клиентом Azure AD и роль tooa приложения hello tooassign в вашей подписке. toosee при наличии разрешений требуется hello [возврата hello портала](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions). 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a>Вариант 1. Создание субъекта-службы в Azure AD

Если перед развертыванием кластера Kubernetes toocreate участника-службы Azure AD, Azure предоставляет несколько методов. 

Следующие примеры команд Hello показывается, как toodo с hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md). Кроме того, можно создать участника службы с помощью [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [портала](../../azure-resource-manager/resource-group-create-service-principal-portal.md), или других методов.

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

Выходные данные выглядят примерно следующее toohello (показанных здесь исправленную):

![Создание субъекта-службы](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

Выделены hello **идентификатор клиента** (`appId`) и hello **секрет клиента** (`password`), используемый в качестве основного параметры службы для развертывания кластера.


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a>Укажите участника-службы, при создании кластера Kubernetes hello

Укажите hello **идентификатор клиента** (также называется hello `appId`, для идентификатора приложения) и **секрет клиента** (`password`) существующей службы субъекта в качестве параметров при создании hello Kubernetes кластера. Убедитесь, что субъект-служба hello требованиям hello в hello, начинающиеся в этой статье.

Можно указать эти параметры при развертывании кластера Kubernetes hello, с помощью hello [Azure интерфейс командной строки (CLI) 2.0](container-service-kubernetes-walkthrough.md), [портал Azure](../dcos-swarm/container-service-deployment.md), или других методов.

>[!TIP] 
>При указании hello **идентификатор клиента**, быть убедиться, что hello toouse `appId`, не hello `ObjectId`, hello субъекта-службы.
>

Hello примере показан один из способов toopass параметров hello hello Azure CLI 2.0. В этом примере используется hello [Kubernetes шаблоном краткого руководства](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).

1. [Загрузить](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) файл параметров шаблона hello `azuredeploy.parameters.json` из GitHub.

2. Участник, службы hello toospecify введите значения для `servicePrincipalClientId` и `servicePrincipalClientSecret` в файле hello. (Необходимо также tooprovide собственные значения для `dnsNamePrefix` и `sshRSAPublicKey`. последний Hello — кластер hello tooaccess открытого ключа SSH, hello.) Сохраните файл hello.

    ![Передача параметров субъекта-службы](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. Выполнения hello следующую команду, с помощью `--parameters` tooset hello путь toohello azuredeploy.parameters.json файл. Эта команда выполняет развертывание кластера hello в группе ресурсов, вы создаете вызываемой `myResourceGroup` в hello Запад США.

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a>Вариант 2: Создание субъекта-службы при создании кластера hello с`az acs create`

При запуске hello [ `az acs create` ](/cli/azure/acs#create) toocreate команда Здравствуйте Kubernetes кластера, у вас есть параметр toogenerate hello участника службы автоматически.

Как и в случае с другими вариантами создания кластера Kubernetes, выполняя команду `az acs create`, вы можете указать параметры для существующего субъекта-службы. Однако при пропуске этих параметров hello Azure CLI создает одно автоматически для использования со службой контейнера. Это происходит прозрачно во время развертывания hello. 

Hello следующая команда создает кластер Kubernetes и создает ключи SSH и учетных данных участника службы:

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> Если ваша учетная запись не имеет hello Azure AD и toocreate подписки разрешения участника службы, команда hello также создает сообщение об ошибке`Insufficient privileges toocomplete hello operation.`
> 

## <a name="additional-considerations"></a>Дополнительные замечания

* Если у вас нет разрешения toocreate участника службы в подписке, то может потребоваться tooask в Azure AD или tooassign администратора подписки hello необходимые разрешения или запрашивать toouse участника службы с помощью контейнера службы Azure. 

* Hello субъекта-службы для Kubernetes является частью конфигурации кластера hello. Тем не менее не следует использовать toodeploy hello hello удостоверение кластера.

* Все субъекты-службы связаны с определенными приложениями Azure AD. Hello участника-службы для кластера Kubernetes могут быть связаны с любой допустимый Azure AD имя приложения (например: `https://www.contoso.org/example`). Hello URL-адрес приложения hello не toobe реальных конечной точки.

* При указании участника-службы hello **идентификатор клиента**, можно использовать значение hello hello `appId` (как показано в этой статье) или hello соответствующего участника службы `name` (например,`https://www.contoso.org/example`).

* Образец hello, и агент виртуальных машин в кластере Kubernetes hello учетных данных участника службы hello хранятся в /etc/kubernetes/azure.json файл hello.

* При использовании hello `az acs create` участника-службы hello toogenerate автоматически см. в записи учетных данных участника службы hello toohello ~/.azure/acsServicePrincipal.json файл на компьютере hello используется команда toorun hello. 

* При использовании hello `az acs create` автоматически команды участника-службы toogenerate hello, hello субъект-служба также позволяет проверять подлинность с [контейнер Azure реестра](../../container-registry/container-registry-intro.md) созданные hello же подписки.




## <a name="next-steps"></a>Дальнейшие действия

* Узнайте, как [начать работу с Kubernetes](container-service-kubernetes-walkthrough.md) в кластере службы контейнеров.

* tootroubleshoot hello субъекта-службы для Kubernetes, в разделе hello [документация по ядру СУБД ACS](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).


