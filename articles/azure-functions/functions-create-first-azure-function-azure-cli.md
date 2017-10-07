---
title: "функции первого из hello Azure CLI aaaCreate | Документы Microsoft"
description: "Узнайте, как первый Azure функции для выполнения без сервера с помощью toocreate hello Azure CLI."
services: functions
keywords: 
author: ggailey777
ms.author: glenga
ms.assetid: 674a01a7-fd34-4775-8b69-893182742ae0
ms.date: 08/22/2017
ms.topic: hero-article
ms.service: functions
ms.custom: mvc
ms.devlang: azure-cli
manager: erikre
ms.openlocfilehash: 5feed0045d4998b88b0e1bb50996cb7bb42b0822
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-hello-azure-cli"></a>Создание первой функции с помощью hello Azure CLI

Этот учебник рассматривается toocreate функции Azure toouse первой функции. Hello Azure CLI toocreate приложения функции, являющийся hello без сервера инфраструктуры, на котором размещена ваша функция используется. Код самой функции Hello развертывается из репозитория GitHub образца.    

Выполните действия hello ниже на компьютере Mac, Windows или Linux. 

## <a name="prerequisites"></a>Предварительные требования 

Перед запуском этого образца, необходимо иметь следующие hello.

+ Активная учетная запись [GitHub](https://github.com). 
+ Активная подписка Azure.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 


## <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create). Группа ресурсов Azure — это логический контейнер, в котором происходит развертывание ресурсов Azure (приложений-функций, баз данных и учетных записей хранения) и управление ими.

Hello следующий пример создает группу ресурсов с именем `myResourceGroup`.  
Если вы не используете Cloud Shell, сначала выполните вход с помощью `az login`.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a>Создание учетной записи хранения Azure

Функции использует состояние toomaintain учетной записи хранилища Azure и другие сведения о функции. Создать учетную запись хранилища в группе ресурсов hello, созданного с помощью hello [создания учетной записи хранилища az](/cli/azure/storage/account#create) команды.

Hello следующую команду, подставьте собственные глобальный уникальный имя учетной записи хранения когда вы видите hello `<storage_name>` заполнителя. Имя учетной записи хранения должно содержать от 3 до 24 символов и состоять только из цифр и строчных букв.

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

После создания учетной записи хранилища hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:

```json
{
  "creationTime": "2017-04-15T17:14:39.320307+00:00",
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myresourcegroup/...",
  "kind": "Storage",
  "location": "westeurope",
  "name": "myfunctionappstorage",
  "primaryEndpoints": {
    "blob": "https://myfunctionappstorage.blob.core.windows.net/",
    "file": "https://myfunctionappstorage.file.core.windows.net/",
    "queue": "https://myfunctionappstorage.queue.core.windows.net/",
    "table": "https://myfunctionappstorage.table.core.windows.net/"
  },
     ....
    // Remaining output has been truncated for readability.
}
```

## <a name="create-a-function-app"></a>Создание приложения-функции

Требуется выполнение функции приложения toohost hello функций. функция приложение Hello предоставляет среду для выполнения кода функции без сервера. Это позволяет группировать функции в логические единицы и упростить развертывание и совместное использование ресурсов, а также управление ими. Создание приложения функции с помощью hello [az functionapp создать](/cli/azure/functionapp#create) команды. 

Hello следующую команду, подставьте собственные уникальные функции имя приложения, где вы видите hello `<app_name>` заполнитель и hello имя учетной записи хранения для `<storage_name>`. Hello `<app_name>` используется как домен DNS по умолчанию hello приложение функции hello и поэтому имя hello должен toobe уникальным для всех приложений в Azure. 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
По умолчанию приложение функция создается с hello потребления плана размещения, это означает, что ресурсы добавляются динамически, как того требует функций и оплата производится только во время выполнения функции. Дополнительные сведения см. в разделе [плана правильного размещения hello выберите](functions-scale.md). 

После создания приложения hello функции hello Azure CLI показано toohello аналогичные сведения, следующий пример:

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "containerSize": 1536,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "quickstart.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "quickstart.azurewebsites.net",
    "quickstart.scm.azurewebsites.net"
  ],
   ....
    // Remaining output has been truncated for readability.
}
```

Теперь, когда имеется функция приложение, вы можете развернуть кода функции hello из репозитория образец hello GitHub.

## <a name="deploy-your-function-code"></a>Развертывание кода функции  

Существует несколько способов toocreate код функции в приложении новые функции. В этом разделе подключается tooa образец репозитория в GitHub. Как и раньше, в hello после кода замените hello `<app_name>` заполнитель с именем hello вы создали приложение функции hello. 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
После развертывания hello источник был установлен, hello Azure CLI показывает toohello аналогичные сведения, следующий пример (значения null, удалены для удобства чтения):

```json
{
  "branch": "master",
  "deploymentRollbackEnabled": false,
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myResourceGroup/...",
  "isManualIntegration": true,
  "isMercurial": false,
  "location": "West Europe",
  "name": "quickstart",
  "repoUrl": "https://github.com/Azure-Samples/functions-quickstart",
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.Web/sites/sourcecontrols"
}
```

## <a name="test-hello-function"></a>Проверка функции hello

Функция перелистывания tootest hello развернуты на компьютере Mac или Linux, с помощью Bash в Windows. Выполните следующую перелистывание команду, заменив hello hello `<app_name>` заполнитель с именем hello функции приложения. Добавить строку hello запроса `&name=<yourname>` toohello URL-адрес.

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Ответ функции в браузере](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

Если у вас нет перелистывание в командную строку, введите hello же URL-адрес в веб-браузере адрес hello. Опять же, замените hello `<app_name>` заполнитель с именем hello функции приложения и добавляет строку запроса hello `&name=<yourname>` toohello URL-адрес и выполнения запроса hello. 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Ответ функции в браузере](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a>Очистка ресурсов

Другие краткие руководства в этой коллекции созданы на основе этого документа. Если планируется toocontinue toowork последующие примеры использования или с hello учебники, выполните не очистить ресурсы hello, созданные в этом кратком руководстве. Если вы не планируете toocontinue, используйте следующие команды toodelete hello все ресурсы, созданные краткого руководства:

```azurecli-interactive
az group delete --name myResourceGroup
```
При появлении запроса введите `y`.

## <a name="next-steps"></a>Дальнейшие действия

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
