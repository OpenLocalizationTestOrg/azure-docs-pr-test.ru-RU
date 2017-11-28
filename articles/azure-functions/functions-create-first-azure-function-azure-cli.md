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
# <a name="create-your-first-function-using-hello-azure-cli"></a><span data-ttu-id="66113-103">Создание первой функции с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="66113-103">Create your first function using hello Azure CLI</span></span>

<span data-ttu-id="66113-104">Этот учебник рассматривается toocreate функции Azure toouse первой функции.</span><span class="sxs-lookup"><span data-stu-id="66113-104">This quickstart tutorial walks through how toouse Azure Functions toocreate your first function.</span></span> <span data-ttu-id="66113-105">Hello Azure CLI toocreate приложения функции, являющийся hello без сервера инфраструктуры, на котором размещена ваша функция используется.</span><span class="sxs-lookup"><span data-stu-id="66113-105">You use hello Azure CLI toocreate a function app, which is hello serverless infrastructure that hosts your function.</span></span> <span data-ttu-id="66113-106">Код самой функции Hello развертывается из репозитория GitHub образца.</span><span class="sxs-lookup"><span data-stu-id="66113-106">hello function code itself is deployed from a GitHub sample repository.</span></span>    

<span data-ttu-id="66113-107">Выполните действия hello ниже на компьютере Mac, Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="66113-107">You can follow hello steps below using a Mac, Windows, or Linux computer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="66113-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="66113-108">Prerequisites</span></span> 

<span data-ttu-id="66113-109">Перед запуском этого образца, необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="66113-109">Before running this sample, you must have hello following:</span></span>

+ <span data-ttu-id="66113-110">Активная учетная запись [GitHub](https://github.com).</span><span class="sxs-lookup"><span data-stu-id="66113-110">An active [GitHub](https://github.com) account.</span></span> 
+ <span data-ttu-id="66113-111">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="66113-111">An active Azure subscription.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="66113-112">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="66113-112">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="66113-113">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="66113-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="66113-114">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="66113-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="66113-115">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="66113-115">Create a resource group</span></span>

<span data-ttu-id="66113-116">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="66113-116">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="66113-117">Группа ресурсов Azure — это логический контейнер, в котором происходит развертывание ресурсов Azure (приложений-функций, баз данных и учетных записей хранения) и управление ими.</span><span class="sxs-lookup"><span data-stu-id="66113-117">An Azure resource group is a logical container into which Azure resources like function apps, databases, and storage accounts are deployed and managed.</span></span>

<span data-ttu-id="66113-118">Hello следующий пример создает группу ресурсов с именем `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="66113-118">hello following example creates a resource group named `myResourceGroup`.</span></span>  
<span data-ttu-id="66113-119">Если вы не используете Cloud Shell, сначала выполните вход с помощью `az login`.</span><span class="sxs-lookup"><span data-stu-id="66113-119">If you are not using Cloud Shell, you must first sign in using `az login`.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a><span data-ttu-id="66113-120">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="66113-120">Create an Azure Storage account</span></span>

<span data-ttu-id="66113-121">Функции использует состояние toomaintain учетной записи хранилища Azure и другие сведения о функции.</span><span class="sxs-lookup"><span data-stu-id="66113-121">Functions uses an Azure Storage account toomaintain state and other information about your functions.</span></span> <span data-ttu-id="66113-122">Создать учетную запись хранилища в группе ресурсов hello, созданного с помощью hello [создания учетной записи хранилища az](/cli/azure/storage/account#create) команды.</span><span class="sxs-lookup"><span data-stu-id="66113-122">Create a storage account in hello resource group you created by using hello [az storage account create](/cli/azure/storage/account#create) command.</span></span>

<span data-ttu-id="66113-123">Hello следующую команду, подставьте собственные глобальный уникальный имя учетной записи хранения когда вы видите hello `<storage_name>` заполнителя.</span><span class="sxs-lookup"><span data-stu-id="66113-123">In hello following command, substitute your own globally unique storage account name where you see hello `<storage_name>` placeholder.</span></span> <span data-ttu-id="66113-124">Имя учетной записи хранения должно содержать от 3 до 24 символов и состоять только из цифр и строчных букв.</span><span class="sxs-lookup"><span data-stu-id="66113-124">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

<span data-ttu-id="66113-125">После создания учетной записи хранилища hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="66113-125">After hello storage account has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

## <a name="create-a-function-app"></a><span data-ttu-id="66113-126">Создание приложения-функции</span><span class="sxs-lookup"><span data-stu-id="66113-126">Create a function app</span></span>

<span data-ttu-id="66113-127">Требуется выполнение функции приложения toohost hello функций.</span><span class="sxs-lookup"><span data-stu-id="66113-127">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="66113-128">функция приложение Hello предоставляет среду для выполнения кода функции без сервера.</span><span class="sxs-lookup"><span data-stu-id="66113-128">hello function app provides an environment for serverless execution of your function code.</span></span> <span data-ttu-id="66113-129">Это позволяет группировать функции в логические единицы и упростить развертывание и совместное использование ресурсов, а также управление ими.</span><span class="sxs-lookup"><span data-stu-id="66113-129">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> <span data-ttu-id="66113-130">Создание приложения функции с помощью hello [az functionapp создать](/cli/azure/functionapp#create) команды.</span><span class="sxs-lookup"><span data-stu-id="66113-130">Create a function app by using hello [az functionapp create](/cli/azure/functionapp#create) command.</span></span> 

<span data-ttu-id="66113-131">Hello следующую команду, подставьте собственные уникальные функции имя приложения, где вы видите hello `<app_name>` заполнитель и hello имя учетной записи хранения для `<storage_name>`.</span><span class="sxs-lookup"><span data-stu-id="66113-131">In hello following command, substitute your own unique function app name where you see hello `<app_name>` placeholder and hello storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="66113-132">Hello `<app_name>` используется как домен DNS по умолчанию hello приложение функции hello и поэтому имя hello должен toobe уникальным для всех приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="66113-132">hello `<app_name>` is used as hello default DNS domain for hello function app, and so hello name needs toobe unique across all apps in Azure.</span></span> 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
<span data-ttu-id="66113-133">По умолчанию приложение функция создается с hello потребления плана размещения, это означает, что ресурсы добавляются динамически, как того требует функций и оплата производится только во время выполнения функции.</span><span class="sxs-lookup"><span data-stu-id="66113-133">By default, a function app is created with hello Consumption hosting plan, which means that resources are added dynamically as required by your functions and you only pay when functions are running.</span></span> <span data-ttu-id="66113-134">Дополнительные сведения см. в разделе [плана правильного размещения hello выберите](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="66113-134">For more information, see [Choose hello correct hosting plan](functions-scale.md).</span></span> 

<span data-ttu-id="66113-135">После создания приложения hello функции hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="66113-135">After hello function app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="66113-136">Теперь, когда имеется функция приложение, вы можете развернуть кода функции hello из репозитория образец hello GitHub.</span><span class="sxs-lookup"><span data-stu-id="66113-136">Now that you have a function app, you can deploy hello actual function code from hello GitHub sample repository.</span></span>

## <a name="deploy-your-function-code"></a><span data-ttu-id="66113-137">Развертывание кода функции</span><span class="sxs-lookup"><span data-stu-id="66113-137">Deploy your function code</span></span>  

<span data-ttu-id="66113-138">Существует несколько способов toocreate код функции в приложении новые функции.</span><span class="sxs-lookup"><span data-stu-id="66113-138">There are several ways toocreate your function code in your new function app.</span></span> <span data-ttu-id="66113-139">В этом разделе подключается tooa образец репозитория в GitHub.</span><span class="sxs-lookup"><span data-stu-id="66113-139">This topic connects tooa sample repository in GitHub.</span></span> <span data-ttu-id="66113-140">Как и раньше, в hello после кода замените hello `<app_name>` заполнитель с именем hello вы создали приложение функции hello.</span><span class="sxs-lookup"><span data-stu-id="66113-140">As before, in hello following code replace hello `<app_name>` placeholder with hello name of hello function app you created.</span></span> 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
<span data-ttu-id="66113-141">После развертывания hello источник был установлен, hello Azure CLI показывает toohello аналогичные сведения, следующий пример (значения null, удалены для удобства чтения):</span><span class="sxs-lookup"><span data-stu-id="66113-141">After hello deployment source been set, hello Azure CLI shows information similar toohello following example (null values removed for readability):</span></span>

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

## <a name="test-hello-function"></a><span data-ttu-id="66113-142">Проверка функции hello</span><span class="sxs-lookup"><span data-stu-id="66113-142">Test hello function</span></span>

<span data-ttu-id="66113-143">Функция перелистывания tootest hello развернуты на компьютере Mac или Linux, с помощью Bash в Windows.</span><span class="sxs-lookup"><span data-stu-id="66113-143">Use cURL tootest hello deployed function on a Mac or Linux computer or using Bash on Windows.</span></span> <span data-ttu-id="66113-144">Выполните следующую перелистывание команду, заменив hello hello `<app_name>` заполнитель с именем hello функции приложения.</span><span class="sxs-lookup"><span data-stu-id="66113-144">Execute hello following cURL command, replacing hello `<app_name>` placeholder with hello name of your function app.</span></span> <span data-ttu-id="66113-145">Добавить строку hello запроса `&name=<yourname>` toohello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="66113-145">Append hello query string `&name=<yourname>` toohello URL.</span></span>

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Ответ функции в браузере](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

<span data-ttu-id="66113-147">Если у вас нет перелистывание в командную строку, введите hello же URL-адрес в веб-браузере адрес hello.</span><span class="sxs-lookup"><span data-stu-id="66113-147">If you don't have cURL available in your command line, enter hello same URL in hello address of your web browser.</span></span> <span data-ttu-id="66113-148">Опять же, замените hello `<app_name>` заполнитель с именем hello функции приложения и добавляет строку запроса hello `&name=<yourname>` toohello URL-адрес и выполнения запроса hello.</span><span class="sxs-lookup"><span data-stu-id="66113-148">Again, replace hello `<app_name>` placeholder with hello name of your function app, and append hello query string `&name=<yourname>` toohello URL and execute hello request.</span></span> 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Ответ функции в браузере](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a><span data-ttu-id="66113-150">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="66113-150">Clean up resources</span></span>

<span data-ttu-id="66113-151">Другие краткие руководства в этой коллекции созданы на основе этого документа.</span><span class="sxs-lookup"><span data-stu-id="66113-151">Other quickstarts in this collection build upon this quickstart.</span></span> <span data-ttu-id="66113-152">Если планируется toocontinue toowork последующие примеры использования или с hello учебники, выполните не очистить ресурсы hello, созданные в этом кратком руководстве.</span><span class="sxs-lookup"><span data-stu-id="66113-152">If you plan toocontinue on toowork with subsequent quickstarts or with hello tutorials, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="66113-153">Если вы не планируете toocontinue, используйте следующие команды toodelete hello все ресурсы, созданные краткого руководства:</span><span class="sxs-lookup"><span data-stu-id="66113-153">If you do not plan toocontinue, use hello following command toodelete all resources created by this quickstart:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```
<span data-ttu-id="66113-154">При появлении запроса введите `y`.</span><span class="sxs-lookup"><span data-stu-id="66113-154">Type `y` when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66113-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="66113-155">Next steps</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
