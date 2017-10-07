---
title: "aaaCreate Hadoop кластеры, использующие Azure REST API - Azure | Документы Microsoft"
description: "Узнайте, как кластеры toocreate HDInsight, отправляя toohello шаблонов диспетчера ресурсов Azure Azure REST API."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 98be5893-2c6f-4dfa-95ec-d4d8b5b7dcb5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/10/2017
ms.author: larryfr
ms.openlocfilehash: 87b585e5084eccdc3d7c57483deabb4ad6e32597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-using-hello-azure-rest-api"></a><span data-ttu-id="fed39-103">Создавать кластеры Hadoop, с помощью Azure REST API hello</span><span class="sxs-lookup"><span data-stu-id="fed39-103">Create Hadoop clusters using hello Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="fed39-104">Узнайте, как toocreate HDInsight кластера с помощью шаблона диспетчера ресурсов Azure и hello Azure REST API.</span><span class="sxs-lookup"><span data-stu-id="fed39-104">Learn how toocreate an HDInsight cluster using an Azure Resource Manager template and hello Azure REST API.</span></span>

<span data-ttu-id="fed39-105">Hello Azure REST API позволяет выполнять операции управления tooperform служб, размещенных в hello платформы Azure, включая создание новых ресурсов, таких как кластеры HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="fed39-105">hello Azure REST API allows you tooperform management operations on services hosted in hello Azure platform, including hello creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fed39-106">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="fed39-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="fed39-107">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="fed39-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="fed39-108">Hello шагов в этот документ используйте hello [curl (https://curl.haxx.se/)](https://curl.haxx.se/) toocommunicate программы с hello Azure REST API.</span><span class="sxs-lookup"><span data-stu-id="fed39-108">hello steps in this document use hello [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility toocommunicate with hello Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="fed39-109">Создание шаблона</span><span class="sxs-lookup"><span data-stu-id="fed39-109">Create a template</span></span>

<span data-ttu-id="fed39-110">Шаблоны Azure Resource Manager — это документы JSON, описывающие **группу ресурсов** и все входящие в нее ресурсы (например, HDInsight). Такой подход на основе шаблона позволяет toodefine hello ресурсы, которые необходимы для HDInsight в один шаблон.</span><span class="sxs-lookup"><span data-stu-id="fed39-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you toodefine hello resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="fed39-111">Hello следующий документ JSON является слияния hello файлы шаблонов и параметров из [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), который создает на основе Linux кластер с помощью типа hello toosecure пароль учетной записи пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="fed39-111">hello following JSON document is a merger of hello template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password toosecure hello SSH user account.</span></span>

   ```json
   {
       "properties": {
           "template": {
               "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
               "contentVersion": "1.0.0.0",
               "parameters": {
                   "clusterType": {
                       "type": "string",
                       "allowedValues": ["hadoop",
                       "hbase",
                       "storm",
                       "spark"],
                       "metadata": {
                           "description": "hello type of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
                       }
                   },
                   "clusterLoginPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "sshUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used tooremotely access hello cluster."
                       }
                   },
                   "sshPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello storage account toobe created and be used as hello cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "hello number of nodes in hello HDInsight cluster."
                       }
                   }
               },
               "variables": {
                   "defaultApiVersion": "2015-05-01-preview",
                   "clusterApiVersion": "2015-03-01-preview"
               },
               "resources": [{
                   "name": "[parameters('clusterStorageAccountName')]",
                   "type": "Microsoft.Storage/storageAccounts",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('defaultApiVersion')]",
                   "dependsOn": [],
                   "tags": {

                   },
                   "properties": {
                       "accountType": "Standard_LRS"
                   }
               },
               {
                   "name": "[parameters('clusterName')]",
                   "type": "Microsoft.HDInsight/clusters",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('clusterApiVersion')]",
                   "dependsOn": ["[concat('Microsoft.Storage/storageAccounts/',parameters('clusterStorageAccountName'))]"],
                   "tags": {

                   },
                   "properties": {
                       "clusterVersion": "3.5",
                       "osType": "Linux",
                       "clusterDefinition": {
                           "kind": "[parameters('clusterType')]",
                           "configurations": {
                               "gateway": {
                                   "restAuthCredential.isEnabled": true,
                                   "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                                   "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                               }
                           }
                       },
                       "storageProfile": {
                           "storageaccounts": [{
                               "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                               "isDefault": true,
                               "container": "[parameters('clusterName')]",
                               "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), variables('defaultApiVersion')).key1]"
                           }]
                       },
                       "computeProfile": {
                           "roles": [{
                               "name": "headnode",
                               "targetInstanceCount": "2",
                               "hardwareProfile": {
                                   "vmSize": "Standard_D3"
                               },
                               "osProfile": {
                                   "linuxOperatingSystemProfile": {
                                       "username": "[parameters('sshUserName')]",
                                       "password": "[parameters('sshPassword')]"
                                   }
                               }
                           },
                           {
                               "name": "workernode",
                               "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                               "hardwareProfile": {
                                   "vmSize": "Standard_D3"
                               },
                               "osProfile": {
                                   "linuxOperatingSystemProfile": {
                                       "username": "[parameters('sshUserName')]",
                                       "password": "[parameters('sshPassword')]"
                                   }
                               }
                           }]
                       }
                   }
               }],
               "outputs": {
                   "cluster": {
                       "type": "object",
                       "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                   }
               }
           },
           "mode": "incremental",
           "Parameters": {
               "clusterName": {
                   "value": "newclustername"
               },
               "clusterType": {
                   "value": "hadoop"
               },
               "clusterStorageAccountName": {
                   "value": "newstoragename"
               },
               "clusterLoginUserName": {
                   "value": "admin"
               },
               "clusterLoginPassword": {
                   "value": "changeme"
               },
               "sshUserName": {
                   "value": "sshuser"
               },
               "sshPassword": {
                   "value": "changeme"
               }
           }
       }
   }
   ```

<span data-ttu-id="fed39-112">В этом примере используется в hello в данном пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="fed39-112">This example is used in hello steps in this document.</span></span> <span data-ttu-id="fed39-113">Замените пример hello *значения* в hello **параметры** раздел со значениями hello для кластера.</span><span class="sxs-lookup"><span data-stu-id="fed39-113">Replace hello example *values* in hello **Parameters** section with hello values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fed39-114">шаблон Hello использует по умолчанию hello, число рабочих узлов (4) для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fed39-114">hello template uses hello default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="fed39-115">Если вы планируете использовать более 32 рабочих узлов, для головного узла потребуется минимум 8-ядерный процессор и 14 ГБ ОЗУ.</span><span class="sxs-lookup"><span data-stu-id="fed39-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="fed39-116">Дополнительные сведения о размерах узлов и их стоимости см. на странице с [ценами на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="fed39-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="fed39-117">Войдите в tooyour подписки Azure</span><span class="sxs-lookup"><span data-stu-id="fed39-117">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="fed39-118">Выполните hello шагов, описанных в [Приступая к работе с Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) и подключите tooyour подписку, используя hello `az login` команды.</span><span class="sxs-lookup"><span data-stu-id="fed39-118">Follow hello steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect tooyour subscription using hello `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="fed39-119">Создание субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="fed39-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="fed39-120">Эти действия не сокращенную версию hello *создания участника службы с паролем* раздел hello [toocreate использование Azure CLI участника службы ресурсов tooaccess](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) документа.</span><span class="sxs-lookup"><span data-stu-id="fed39-120">These steps are an abridged version of hello *Create service principal with password* section of hello [Use Azure CLI toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="fed39-121">Эти шаги создают участника службы, используемые tooauthenticate toohello Azure REST API.</span><span class="sxs-lookup"><span data-stu-id="fed39-121">These steps create a service principal that is used tooauthenticate toohello Azure REST API.</span></span>

1. <span data-ttu-id="fed39-122">Из командной строки используйте следующие команды toolist hello подписками Azure.</span><span class="sxs-lookup"><span data-stu-id="fed39-122">From a command line, use hello following command toolist your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="fed39-123">В списке hello выберите hello подписки требуется toouse и обратите внимание, hello **ИД_ПОДПИСКИ** и __Tenant_ID__ столбцы.</span><span class="sxs-lookup"><span data-stu-id="fed39-123">In hello list, select hello subscription that you want toouse and note hello **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="fed39-124">Сохраните эти значения.</span><span class="sxs-lookup"><span data-stu-id="fed39-124">Save these values.</span></span>

2. <span data-ttu-id="fed39-125">Используйте следующие команды toocreate приложения в Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="fed39-125">Use hello following command toocreate an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="fed39-126">Замените значения hello hello `--display-name`, `--homepage`, и `--identifier-uris` собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="fed39-126">Replace hello values for hello `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="fed39-127">Введите пароль для новой записи Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="fed39-127">Provide a password for hello new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fed39-128">Hello `--home-page` и `--identifier-uris` значения не должны tooreference фактической веб-страницы, размещенной на hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="fed39-128">hello `--home-page` and `--identifier-uris` values don't need tooreference an actual web page hosted on hello internet.</span></span> <span data-ttu-id="fed39-129">Это должны быть уникальные универсальные коды ресурса.</span><span class="sxs-lookup"><span data-stu-id="fed39-129">They must be unique URIs.</span></span>

   <span data-ttu-id="fed39-130">Hello значение, возвращаемое из этой команды — hello __идентификатор приложения__ для нового приложения hello.</span><span class="sxs-lookup"><span data-stu-id="fed39-130">hello value returned from this command is hello __App ID__ for hello new application.</span></span> <span data-ttu-id="fed39-131">Сохраните его.</span><span class="sxs-lookup"><span data-stu-id="fed39-131">Save this value.</span></span>

3. <span data-ttu-id="fed39-132">Используйте hello следующая команда toocreate участника службы с помощью hello **идентификатор приложения**.</span><span class="sxs-lookup"><span data-stu-id="fed39-132">Use hello following command toocreate a service principal using hello **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="fed39-133">Hello значение, возвращаемое из этой команды — hello __идентификатор объекта__.</span><span class="sxs-lookup"><span data-stu-id="fed39-133">hello value returned from this command is hello __Object ID__.</span></span> <span data-ttu-id="fed39-134">Сохраните его.</span><span class="sxs-lookup"><span data-stu-id="fed39-134">Save this value.</span></span>

4. <span data-ttu-id="fed39-135">Назначить hello **владельца** с помощью hello участника-службы роли toohello **идентификатор объекта** значение.</span><span class="sxs-lookup"><span data-stu-id="fed39-135">Assign hello **Owner** role toohello service principal using hello **Object ID** value.</span></span> <span data-ttu-id="fed39-136">Используйте hello **идентификатор подписки** полученного ранее.</span><span class="sxs-lookup"><span data-stu-id="fed39-136">Use hello **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="fed39-137">Получение маркера проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="fed39-137">Get an authentication token</span></span>

<span data-ttu-id="fed39-138">Используйте hello, следующая команда tooretrieve маркер проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="fed39-138">Use hello following command tooretrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="fed39-139">Задать `$TENANTID`, `$APPID`, и `$PASSWORD` toohello значений, полученных или ранее.</span><span class="sxs-lookup"><span data-stu-id="fed39-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` toohello values obtained or used previously.</span></span>

<span data-ttu-id="fed39-140">При успешном выполнении этот запрос был получен ответ 200 рядов и hello текст ответа содержит документ JSON.</span><span class="sxs-lookup"><span data-stu-id="fed39-140">If this request is successful, you receive a 200 series response and hello response body contains a JSON document.</span></span>

<span data-ttu-id="fed39-141">Hello JSON-документа, возвращаемого этим запросом содержит элемент с именем **access_token**.</span><span class="sxs-lookup"><span data-stu-id="fed39-141">hello JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="fed39-142">Здравствуйте, значение **access_token** — toohello запросов используется tooauthentication API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="fed39-142">hello value of **access_token** is used tooauthentication requests toohello REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="fed39-143">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="fed39-143">Create a resource group</span></span>

<span data-ttu-id="fed39-144">Используйте hello, следуя toocreate группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fed39-144">Use hello following toocreate a resource group.</span></span>

* <span data-ttu-id="fed39-145">Задать `$SUBSCRIPTIONID` toohello идентификатор подписки, полученных при создании hello участника-службы.</span><span class="sxs-lookup"><span data-stu-id="fed39-145">Set `$SUBSCRIPTIONID` toohello subscription ID received while creating hello service principal.</span></span>
* <span data-ttu-id="fed39-146">Задать `$ACCESSTOKEN` toohello маркер доступа, полученный в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="fed39-146">Set `$ACCESSTOKEN` toohello access token received in hello previous step.</span></span>
* <span data-ttu-id="fed39-147">Замените `DATACENTERLOCATION` hello центра данных нужно toocreate hello ресурсов группы, а ресурсы, в.</span><span class="sxs-lookup"><span data-stu-id="fed39-147">Replace `DATACENTERLOCATION` with hello data center you wish toocreate hello resource group, and resources, in.</span></span> <span data-ttu-id="fed39-148">Например, "Южно-центральный регион США".</span><span class="sxs-lookup"><span data-stu-id="fed39-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="fed39-149">Задать `$RESOURCEGROUPNAME` toohello имени toouse для этой группы:</span><span class="sxs-lookup"><span data-stu-id="fed39-149">Set `$RESOURCEGROUPNAME` toohello name you wish toouse for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="fed39-150">При успешном выполнении этот запрос был получен ответ 200 рядов и hello текст ответа содержит документ JSON, содержащий сведения о группе hello.</span><span class="sxs-lookup"><span data-stu-id="fed39-150">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello group.</span></span> <span data-ttu-id="fed39-151">Hello `"provisioningState"` элемент содержит значение `"Succeeded"`.</span><span class="sxs-lookup"><span data-stu-id="fed39-151">hello `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="fed39-152">Создание развертывания</span><span class="sxs-lookup"><span data-stu-id="fed39-152">Create a deployment</span></span>

<span data-ttu-id="fed39-153">Используйте hello, следующая команда toodeploy hello шаблона toohello группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fed39-153">Use hello following command toodeploy hello template toohello resource group.</span></span>

* <span data-ttu-id="fed39-154">Задать `$DEPLOYMENTNAME` toohello имени toouse для этого развертывания.</span><span class="sxs-lookup"><span data-stu-id="fed39-154">Set `$DEPLOYMENTNAME` toohello name you wish toouse for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string toohello template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="fed39-155">Если вы сохранили файл tooa шаблона hello, можно использовать следующую команду, а не hello `-d "{ template and parameters}"`:</span><span class="sxs-lookup"><span data-stu-id="fed39-155">If you saved hello template tooa file, you can use hello following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="fed39-156">При успешном выполнении этот запрос был получен ответ 200 рядов и hello текст ответа содержит документ JSON, содержащий сведения об операции развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="fed39-156">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fed39-157">Hello развертывания был отправлен, но не завершена.</span><span class="sxs-lookup"><span data-stu-id="fed39-157">hello deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="fed39-158">Он может занять несколько минут, обычно около 15 для развертывания toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="fed39-158">It can take several minutes, usually around 15, for hello deployment toocomplete.</span></span>

## <a name="check-hello-status-of-a-deployment"></a><span data-ttu-id="fed39-159">Проверьте состояние развертывания hello</span><span class="sxs-lookup"><span data-stu-id="fed39-159">Check hello status of a deployment</span></span>

<span data-ttu-id="fed39-160">состояние hello toocheck развертывания hello, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fed39-160">toocheck hello status of hello deployment, use hello following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="fed39-161">Эта команда возвращает документ JSON, содержащий сведения об операции развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="fed39-161">This command returns a JSON document containing information about hello deployment operation.</span></span> <span data-ttu-id="fed39-162">Hello `"provisioningState"` элемент содержит состояние hello hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="fed39-162">hello `"provisioningState"` element contains hello status of hello deployment.</span></span> <span data-ttu-id="fed39-163">Если этот элемент содержит значение `"Succeeded"`, а затем hello развертывания успешно завершена.</span><span class="sxs-lookup"><span data-stu-id="fed39-163">If this element contains a value of `"Succeeded"`, then hello deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="fed39-164">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="fed39-164">Troubleshoot</span></span>

<span data-ttu-id="fed39-165">Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="fed39-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fed39-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fed39-166">Next steps</span></span>

<span data-ttu-id="fed39-167">Теперь, когда вы успешно создали кластер HDInsight, используйте следующие toolearn как hello toowork с кластером.</span><span class="sxs-lookup"><span data-stu-id="fed39-167">Now that you have successfully created an HDInsight cluster, use hello following toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="fed39-168">Кластеры Hadoop</span><span class="sxs-lookup"><span data-stu-id="fed39-168">Hadoop clusters</span></span>

* [<span data-ttu-id="fed39-169">Использование Hive с HDInsight</span><span class="sxs-lookup"><span data-stu-id="fed39-169">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="fed39-170">Использование Pig с HDInsight</span><span class="sxs-lookup"><span data-stu-id="fed39-170">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="fed39-171">Использование MapReduce с HDInsight</span><span class="sxs-lookup"><span data-stu-id="fed39-171">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="fed39-172">Кластеры HBase</span><span class="sxs-lookup"><span data-stu-id="fed39-172">HBase clusters</span></span>

* [<span data-ttu-id="fed39-173">Начало работы с HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="fed39-173">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="fed39-174">Разработка приложений Java для HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="fed39-174">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="fed39-175">Кластеры Storm</span><span class="sxs-lookup"><span data-stu-id="fed39-175">Storm clusters</span></span>

* [<span data-ttu-id="fed39-176">Разработка приложений Java для Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="fed39-176">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="fed39-177">Использование компонентов Python в Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="fed39-177">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="fed39-178">Развертывание и мониторинг топологий с помощью Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="fed39-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
