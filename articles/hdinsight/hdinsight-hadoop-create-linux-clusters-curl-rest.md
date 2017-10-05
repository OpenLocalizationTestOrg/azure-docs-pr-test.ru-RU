---
title: "Создание кластеров Hadoop с помощью REST API Azure | Документы Майкрософт"
description: "Узнайте, как создавать кластеры HDInsight, отправив шаблоны Azure Resource Manager в Azure REST API."
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
ms.openlocfilehash: a36a41c231472ceeeb46d02ddb65549b1c79728a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-hadoop-clusters-using-the-azure-rest-api"></a><span data-ttu-id="271cc-103">Создание кластеров Hadoop с помощью Azure REST API</span><span class="sxs-lookup"><span data-stu-id="271cc-103">Create Hadoop clusters using the Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="271cc-104">Узнайте, как создавать кластеры HDInsight с помощью шаблонов Azure Resource Manager и Azure REST API.</span><span class="sxs-lookup"><span data-stu-id="271cc-104">Learn how to create an HDInsight cluster using an Azure Resource Manager template and the Azure REST API.</span></span>

<span data-ttu-id="271cc-105">Azure REST API позволяет управлять службами, размещенными на платформе Azure, в том числе создавать ресурсы, например кластеры HDInsight.</span><span class="sxs-lookup"><span data-stu-id="271cc-105">The Azure REST API allows you to perform management operations on services hosted in the Azure platform, including the creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="271cc-106">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="271cc-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="271cc-107">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="271cc-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="271cc-108">В описанных в этом документе инструкциях для связи с Azure REST API используется служебная программа [curl (https://curl.haxx.se/)](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="271cc-108">The steps in this document use the [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility to communicate with the Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="271cc-109">Создание шаблона</span><span class="sxs-lookup"><span data-stu-id="271cc-109">Create a template</span></span>

<span data-ttu-id="271cc-110">Шаблоны Azure Resource Manager — это документы JSON, описывающие **группу ресурсов** и все входящие в нее ресурсы (например, HDInsight). Такой подход позволяет определять ресурсы, требуемые для работы с HDInsight, в один шаблон.</span><span class="sxs-lookup"><span data-stu-id="271cc-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you to define the resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="271cc-111">Ниже приведен документ JSON, представляющий собой результат слияния файлов параметров и шаблона, доступного по адресу [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password). Будет создан кластер под управлением Linux с паролем для защиты учетной записи пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="271cc-111">The following JSON document is a merger of the template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password to secure the SSH user account.</span></span>

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
                           "description": "The type of the HDInsight cluster to create."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "The name of the HDInsight cluster to create."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
                       }
                   },
                   "clusterLoginPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "sshUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used to remotely access the cluster."
                       }
                   },
                   "sshPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "The name of the storage account to be created and be used as the cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "The number of nodes in the HDInsight cluster."
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

<span data-ttu-id="271cc-112">Этот пример используется при выполнении действий в этом документе.</span><span class="sxs-lookup"><span data-stu-id="271cc-112">This example is used in the steps in this document.</span></span> <span data-ttu-id="271cc-113">Замените пример *значений* в разделе **Параметры** значениями для своего кластера.</span><span class="sxs-lookup"><span data-stu-id="271cc-113">Replace the example *values* in the **Parameters** section with the values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="271cc-114">Шаблон использует стандартное количество рабочих узлов (4) для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="271cc-114">The template uses the default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="271cc-115">Если вы планируете использовать более 32 рабочих узлов, для головного узла потребуется минимум 8-ядерный процессор и 14 ГБ ОЗУ.</span><span class="sxs-lookup"><span data-stu-id="271cc-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="271cc-116">Дополнительные сведения о размерах узлов и их стоимости см. на странице с [ценами на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="271cc-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="271cc-117">Вход в подписку Azure</span><span class="sxs-lookup"><span data-stu-id="271cc-117">Log in to your Azure subscription</span></span>

<span data-ttu-id="271cc-118">Выполните действия, описанные в статье [Get started with Azure CLI 2.0 (Preview)](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) (Приступая к работе с Azure CLI 2.0 (предварительная версия)) и подключитесь к подписке, используя команду `az login`.</span><span class="sxs-lookup"><span data-stu-id="271cc-118">Follow the steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect to your subscription using the `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="271cc-119">Создание субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="271cc-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="271cc-120">Приведенные действия представляют собой сокращенную версию раздела *Создание субъекта-службы с использованием пароля* статьи [Использование интерфейса командной строки Azure для создания субъекта-службы и доступа к ресурсам](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password).</span><span class="sxs-lookup"><span data-stu-id="271cc-120">These steps are an abridged version of the *Create service principal with password* section of the [Use Azure CLI to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="271cc-121">Выполнив эти действия, вы создадите субъект-службу, используемый для аутентификации в Azure REST API.</span><span class="sxs-lookup"><span data-stu-id="271cc-121">These steps create a service principal that is used to authenticate to the Azure REST API.</span></span>

1. <span data-ttu-id="271cc-122">Используйте следующую команду в командной строке, чтобы вывести список подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="271cc-122">From a command line, use the following command to list your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="271cc-123">Из списка выберите подписку, которую нужно использовать, и обратите внимание на столбцы **Subscription_ID** и __Tenant_ID__.</span><span class="sxs-lookup"><span data-stu-id="271cc-123">In the list, select the subscription that you want to use and note the **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="271cc-124">Сохраните эти значения.</span><span class="sxs-lookup"><span data-stu-id="271cc-124">Save these values.</span></span>

2. <span data-ttu-id="271cc-125">Используйте следующую команду, чтобы создать приложение в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="271cc-125">Use the following command to create an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="271cc-126">Замените значения `--display-name`, `--homepage` и `--identifier-uris` собственными.</span><span class="sxs-lookup"><span data-stu-id="271cc-126">Replace the values for the `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="271cc-127">Введите пароль для новой записи Active Directory.</span><span class="sxs-lookup"><span data-stu-id="271cc-127">Provide a password for the new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="271cc-128">Значения `--home-page` и `--identifier-uris` не обязательно должны ссылаться на фактическую веб-страницу, размещенную в Интернете.</span><span class="sxs-lookup"><span data-stu-id="271cc-128">The `--home-page` and `--identifier-uris` values don't need to reference an actual web page hosted on the internet.</span></span> <span data-ttu-id="271cc-129">Это должны быть уникальные универсальные коды ресурса.</span><span class="sxs-lookup"><span data-stu-id="271cc-129">They must be unique URIs.</span></span>

   <span data-ttu-id="271cc-130">Эта команда возвращает значение __App ID__ для нового приложения.</span><span class="sxs-lookup"><span data-stu-id="271cc-130">The value returned from this command is the __App ID__ for the new application.</span></span> <span data-ttu-id="271cc-131">Сохраните его.</span><span class="sxs-lookup"><span data-stu-id="271cc-131">Save this value.</span></span>

3. <span data-ttu-id="271cc-132">Используйте следующую команду, чтобы создать субъект-службу с помощью **App ID**:</span><span class="sxs-lookup"><span data-stu-id="271cc-132">Use the following command to create a service principal using the **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="271cc-133">Эта команда возвращает значение __Object ID__.</span><span class="sxs-lookup"><span data-stu-id="271cc-133">The value returned from this command is the __Object ID__.</span></span> <span data-ttu-id="271cc-134">Сохраните его.</span><span class="sxs-lookup"><span data-stu-id="271cc-134">Save this value.</span></span>

4. <span data-ttu-id="271cc-135">Назначьте роль **Владелец** субъекту-службе, используя значение **Object ID**.</span><span class="sxs-lookup"><span data-stu-id="271cc-135">Assign the **Owner** role to the service principal using the **Object ID** value.</span></span> <span data-ttu-id="271cc-136">Используйте **идентификатор подписки**, полученный ранее.</span><span class="sxs-lookup"><span data-stu-id="271cc-136">Use the **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="271cc-137">Получение маркера проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="271cc-137">Get an authentication token</span></span>

<span data-ttu-id="271cc-138">Используйте следующую команду, чтобы получить маркер аутентификации:</span><span class="sxs-lookup"><span data-stu-id="271cc-138">Use the following command to retrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="271cc-139">Задайте для `$TENANTID`, `$APPID` и `$PASSWORD` полученные или указанные ранее значения.</span><span class="sxs-lookup"><span data-stu-id="271cc-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` to the values obtained or used previously.</span></span>

<span data-ttu-id="271cc-140">Если этот запрос завершится успешно, будет получен ответ серии 200, и тело ответа будет содержать документ JSON.</span><span class="sxs-lookup"><span data-stu-id="271cc-140">If this request is successful, you receive a 200 series response and the response body contains a JSON document.</span></span>

<span data-ttu-id="271cc-141">Документ JSON, возвращаемый этим запросом, содержит элемент **access_token**.</span><span class="sxs-lookup"><span data-stu-id="271cc-141">The JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="271cc-142">Значение **access_token** используется для проверки подлинности запросов API REST.</span><span class="sxs-lookup"><span data-stu-id="271cc-142">The value of **access_token** is used to authentication requests to the REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="271cc-143">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="271cc-143">Create a resource group</span></span>

<span data-ttu-id="271cc-144">Чтобы создать группу ресурсов, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="271cc-144">Use the following to create a resource group.</span></span>

* <span data-ttu-id="271cc-145">Задайте `$SUBSCRIPTIONID` для идентификатора подписки, полученного при создании субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="271cc-145">Set `$SUBSCRIPTIONID` to the subscription ID received while creating the service principal.</span></span>
* <span data-ttu-id="271cc-146">Для маркера доступа, полученного на предыдущем этапе, задайте `$ACCESSTOKEN`.</span><span class="sxs-lookup"><span data-stu-id="271cc-146">Set `$ACCESSTOKEN` to the access token received in the previous step.</span></span>
* <span data-ttu-id="271cc-147">Замените `DATACENTERLOCATION` центром обработки данных, в котором вы хотите создать группу ресурсов и ресурсы.</span><span class="sxs-lookup"><span data-stu-id="271cc-147">Replace `DATACENTERLOCATION` with the data center you wish to create the resource group, and resources, in.</span></span> <span data-ttu-id="271cc-148">Например, "Южно-центральный регион США".</span><span class="sxs-lookup"><span data-stu-id="271cc-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="271cc-149">Задайте для `$RESOURCEGROUPNAME` имя, которое хотите использовать для этой группы:</span><span class="sxs-lookup"><span data-stu-id="271cc-149">Set `$RESOURCEGROUPNAME` to the name you wish to use for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="271cc-150">Если этот запрос завершится успешно, будет получен ответ серии 200, и тело ответа будет включать в себя документ JSON, содержащий информацию о группе.</span><span class="sxs-lookup"><span data-stu-id="271cc-150">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the group.</span></span> <span data-ttu-id="271cc-151">Элемент `"provisioningState"` будет содержать значение `"Succeeded"`.</span><span class="sxs-lookup"><span data-stu-id="271cc-151">The `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="271cc-152">Создание развертывания</span><span class="sxs-lookup"><span data-stu-id="271cc-152">Create a deployment</span></span>

<span data-ttu-id="271cc-153">Используйте следующую команду, чтобы развернуть шаблон в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="271cc-153">Use the following command to deploy the template to the resource group.</span></span>

* <span data-ttu-id="271cc-154">Задайте для `$DEPLOYMENTNAME` имя, которое хотите использовать для этого развертывания.</span><span class="sxs-lookup"><span data-stu-id="271cc-154">Set `$DEPLOYMENTNAME` to the name you wish to use for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string to the template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="271cc-155">При сохранении шаблона в файл вместо `-d "{ template and parameters}"` можно использовать следующую команду:</span><span class="sxs-lookup"><span data-stu-id="271cc-155">If you saved the template to a file, you can use the following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="271cc-156">Если этот запрос завершится успешно, будет получен ответ серии 200, и тело ответа будет включать в себя документ JSON, содержащий информацию об операции развертывания.</span><span class="sxs-lookup"><span data-stu-id="271cc-156">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="271cc-157">Развертывание было отправлено, но не завершено.</span><span class="sxs-lookup"><span data-stu-id="271cc-157">The deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="271cc-158">Для завершения развертывания может потребоваться несколько минут, обычно около 15.</span><span class="sxs-lookup"><span data-stu-id="271cc-158">It can take several minutes, usually around 15, for the deployment to complete.</span></span>

## <a name="check-the-status-of-a-deployment"></a><span data-ttu-id="271cc-159">Проверка состояния развертывания</span><span class="sxs-lookup"><span data-stu-id="271cc-159">Check the status of a deployment</span></span>

<span data-ttu-id="271cc-160">Чтобы проверить состояние развертывания, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="271cc-160">To check the status of the deployment, use the following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="271cc-161">Эта команда возвращает документ JSON, содержащий сведения об операции развертывания.</span><span class="sxs-lookup"><span data-stu-id="271cc-161">This command returns a JSON document containing information about the deployment operation.</span></span> <span data-ttu-id="271cc-162">Элемент `"provisioningState"` содержит сведения о состоянии развертывания.</span><span class="sxs-lookup"><span data-stu-id="271cc-162">The `"provisioningState"` element contains the status of the deployment.</span></span> <span data-ttu-id="271cc-163">Если элемент содержит значение `"Succeeded"`, развертывание завершилось успешно.</span><span class="sxs-lookup"><span data-stu-id="271cc-163">If this element contains a value of `"Succeeded"`, then the deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="271cc-164">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="271cc-164">Troubleshoot</span></span>

<span data-ttu-id="271cc-165">Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="271cc-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="271cc-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="271cc-166">Next steps</span></span>

<span data-ttu-id="271cc-167">Теперь, когда вы успешно создали кластер HDInsight, обратитесь к следующим статьям, чтобы научиться работать с кластером.</span><span class="sxs-lookup"><span data-stu-id="271cc-167">Now that you have successfully created an HDInsight cluster, use the following to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="271cc-168">Кластеры Hadoop</span><span class="sxs-lookup"><span data-stu-id="271cc-168">Hadoop clusters</span></span>

* [<span data-ttu-id="271cc-169">Использование Hive с HDInsight</span><span class="sxs-lookup"><span data-stu-id="271cc-169">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="271cc-170">Использование Pig с HDInsight</span><span class="sxs-lookup"><span data-stu-id="271cc-170">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="271cc-171">Использование MapReduce с HDInsight</span><span class="sxs-lookup"><span data-stu-id="271cc-171">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="271cc-172">Кластеры HBase</span><span class="sxs-lookup"><span data-stu-id="271cc-172">HBase clusters</span></span>

* [<span data-ttu-id="271cc-173">Начало работы с HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="271cc-173">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="271cc-174">Разработка приложений Java для HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="271cc-174">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="271cc-175">Кластеры Storm</span><span class="sxs-lookup"><span data-stu-id="271cc-175">Storm clusters</span></span>

* [<span data-ttu-id="271cc-176">Разработка приложений Java для Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="271cc-176">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="271cc-177">Использование компонентов Python в Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="271cc-177">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="271cc-178">Развертывание и мониторинг топологий с помощью Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="271cc-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
