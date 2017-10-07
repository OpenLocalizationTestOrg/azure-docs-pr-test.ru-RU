---
title: "Источник OpenShift tooAzure aaaDeploy | Документы Microsoft"
description: "Узнайте toodeploy OpenShift источника tooAzure виртуальных машин."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a>Развертывание источника OpenShift tooAzure виртуальные машины 

[OpenShift Origin](https://www.openshift.org/) — это платформа контейнера с открытым исходным кодом, созданная на основе [Kubernetes](https://kubernetes.io/). Он упрощает процесс hello развертывания, масштабирование и эксплуатации приложения с несколькими клиентами. 

В этом руководстве описывается, как hello toodeploy OpenShift источника на виртуальных машинах Azure с помощью Azure CLI и шаблоны Azure Resource Manager. Из этого руководства вы узнаете, как выполнить следующие задачи:

> [!div class="checklist"]
> * Создание ключей SSH для кластера hello OpenShift KeyVault toomanage.
> * развернуть кластер OpenShift на виртуальных машинах Azure; 
> * Установка и настройка hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello кластера.
> * Настройка развертывания OpenShift hello.

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.

В этом кратком руководстве требует hello Azure CLI версии 2.0.8 или более поздней версии. версия toofind hello, запустите `az --version`. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a>Войдите в tooAzure 
Войдите в подписку Azure совместно с hello tooyour [входа az](/cli/azure/#login) команды и выполните hello на экране инструкции или нажмите кнопку **опробовать** toouse оболочки облака.

```azurecli 
az login
```
## <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды. Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими. 

Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение.

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a>создать хранилище ключей;
Создать ключи SSH для кластера hello hello toostore KeyVault hello [az keyvault создать](/cli/azure/keyvault#create) команды.  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a>Создание ключа SSH 
SSH-ключ является toohello доступа необходимые toosecure источника OpenShift кластера. Создать пару ключей SSH с помощью hello `ssh-keygen` команды. 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> Hello пару ключей SSH, создаваемые вами, не должны иметь парольную фразу.

Дополнительные сведения о ключах SSH в Windows [как ключи toocreate SSH в Windows](/azure/virtual-machines/linux/ssh-from-windows).

## <a name="store-ssh-private-key-in-key-vault"></a>Сохранение закрытого ключа SSH в Key Vault
Hello OpenShift развертывания использует hello SSH-ключ создан доступа toosecure toohello OpenShift master. Развертывание toosecurely tooenable hello извлечь ключ SSH hello, hello ключ хранится в хранилище ключей с помощью hello следующую команду.

# <a name="enabled-for-template-deployment"></a>Включение для развертывания шаблона
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a>Создание субъекта-службы 
OpenShift взаимодействует с Azure, используя имя пользователя и пароль или субъект-службу. Субъект-служба Azure является удостоверением безопасности, которое можно использовать с приложениями, службами и инструментами автоматизации, такими как OpenShift. Управление и определить hello разрешения участника службы hello toowhat операции можно выполнять в Azure. безопасность tooimprove просто задать имя пользователя и пароль, этот пример создает базовую службу участника.

Создание службы с основной [az ad sp создать для rbac](/cli/azure/ad/sp#create-for-rbac) и hello учетные данные, которые требуется OpenShift выходные данные:

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
Запишите команда hello возвращать свойство appId hello.
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > Не используйте ненадежный пароль.  Следуйте руководству по [правилам и ограничениям для паролей Azure AD](/azure/active-directory/active-directory-passwords-policy).

Дополнительные сведения о субъект-службе см. в статье [Создание субъекта-службы Azure с помощью Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="deploy-hello-openshift-origin-template"></a>Развертывание hello OpenShift источника шаблона
Далее развернем OpenShift Origin с помощью шаблона Azure Resource Manager. 

> [!NOTE] 
> Hello следующая команда требует az CLI 2.0.8 или более поздней версии. Вы можете проверить hello az CLI версии с hello `az --version` команды. hello tooupdate версии CLI. в разделе [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).

Используйте hello `appId` значение из hello участника службы, созданные ранее для hello `aadClientId` параметра.

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
Hello развертывания может занять до минуты toocomplete too20. Hello URL-адрес консоли OpenShift hello и DNS-имя hello OpenShift мастер находится на печать toohello терминалов после завершения развертывания hello.

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a>Подключите кластер OpenShift toohello
После завершения развертывания hello подключения консоли OpenShift toohello, с помощью браузера hello, с помощью hello `OpenShift Console Uri`. Кроме того можно подключаться toohello OpenShift master с помощью hello следующую команду.

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a>Очистка ресурсов
Если больше не нужны, можно использовать hello [удаление группы az](/cli/azure/group#delete) команд группы ресурсов tooremove hello, OpenShift кластера и все связанные ресурсы.

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

В рамках этого руководства вы узнали, как выполнять следующие задачи:
> [!div class="checklist"]
> * Создание ключей SSH для кластера hello OpenShift KeyVault toomanage.
> * развернуть кластер OpenShift на виртуальных машинах Azure; 
> * Установка и настройка hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello кластера.

Теперь, когда вы развернули кластер OpenShift Origin, Можно выполнить как toolearn OpenShift учебники toodeploy первого приложения и используйте hello OpenShift средства. В разделе [Приступая к работе с источником OpenShift](https://docs.openshift.org/latest/getting_started/index.html) tooget работы. 
