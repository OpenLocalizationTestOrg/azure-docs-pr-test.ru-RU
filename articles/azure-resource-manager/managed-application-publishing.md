---
title: "aaaCreate и публикации каталога управляемого приложения службы Azure | Документы Microsoft"
description: "Показывает, как toocreate Azure управляемые приложения, предназначенные для членов вашей организации."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 31f2f9e3b50f57dae7f4dcf2edefa7366bfff25c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a><span data-ttu-id="d8435-103">Публикация управляемого приложения для внутреннего использования</span><span class="sxs-lookup"><span data-stu-id="d8435-103">Publish a managed application for internal consumption</span></span>

<span data-ttu-id="d8435-104">Вы можете создавать и публиковать [управляемые приложения Azure](managed-application-overview.md), предназначенные для членов вашей организации.</span><span class="sxs-lookup"><span data-stu-id="d8435-104">You can create and publish Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="d8435-105">Например, отдел ИТ может публиковать управляемые приложения, которые обеспечивают соответствие стандартам организации.</span><span class="sxs-lookup"><span data-stu-id="d8435-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span></span> <span data-ttu-id="d8435-106">Эти управляемые приложения доступны через каталог услуг hello, hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d8435-106">These managed applications are available through hello service catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="d8435-107">toopublish для каталога услуг hello управляемого приложения, необходимо выполнить следующее:</span><span class="sxs-lookup"><span data-stu-id="d8435-107">toopublish a managed application for hello service catalog, you must:</span></span>

* <span data-ttu-id="d8435-108">Создайте ZIP-пакете, содержащий три файла требуемый шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="d8435-108">Create a .zip package that contains hello three required template files.</span></span>
* <span data-ttu-id="d8435-109">Определите, какой пользователь, группа или приложения должен получить доступ к toohello группы ресурсов в подписке hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="d8435-109">Decide which user, group, or application needs access toohello resource group in hello user's subscription.</span></span>
* <span data-ttu-id="d8435-110">Создание определения hello управляемого приложения, которое указывает toohello ZIP-архив и запрашивает доступ к идентификатору hello.</span><span class="sxs-lookup"><span data-stu-id="d8435-110">Create hello managed application definition that points toohello .zip package and requests access for hello identity.</span></span>

## <a name="create-a-managed-application-package"></a><span data-ttu-id="d8435-111">Создание пакета управляемого приложения</span><span class="sxs-lookup"><span data-stu-id="d8435-111">Create a managed application package</span></span>

<span data-ttu-id="d8435-112">Hello прежде всего три файла требуемый шаблон toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="d8435-112">hello first step is toocreate hello three required template files.</span></span> <span data-ttu-id="d8435-113">Упаковать все три файла в ZIP-файл и отправьте его tooan доступном месте, например в учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="d8435-113">Package all three files into a .zip file, and upload it tooan accessible location, such as a storage account.</span></span> <span data-ttu-id="d8435-114">При создании hello управляемое определение приложения передать ссылку toothis ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="d8435-114">You pass a link toothis .zip file when creating hello managed application definition.</span></span>

* <span data-ttu-id="d8435-115">**applianceMainTemplate.json**: этот файл определяет hello Azure ресурсов, предоставляемых в составе приветствия управляемого приложения.</span><span class="sxs-lookup"><span data-stu-id="d8435-115">**applianceMainTemplate.json**: This file defines hello Azure resources that are provisioned as part of hello managed application.</span></span> <span data-ttu-id="d8435-116">шаблон Hello ничем не отличается от обычных шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d8435-116">hello template is no different than a regular Resource Manager template.</span></span> <span data-ttu-id="d8435-117">Например toocreate учетной записи хранилища через управляемого приложения applianceMainTemplate.json содержит:</span><span class="sxs-lookup"><span data-stu-id="d8435-117">For example, toocreate a storage account through a managed application, applianceMainTemplate.json contains:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(parameters('storageAccountNamePrefix'), uniqueString(resourceGroup().id))]",
            "apiVersion": "2016-01-01",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {}
        }
    ],
    "outputs": {}
  }
  ```

* <span data-ttu-id="d8435-118">**mainTemplate.json**: пользователи развертывают этот шаблон при создании hello управляемых приложений.</span><span class="sxs-lookup"><span data-stu-id="d8435-118">**mainTemplate.json**: Users deploy this template when creating hello managed application.</span></span> <span data-ttu-id="d8435-119">Он определяет ресурса hello управляемого приложения, который является Microsoft.Solutions/appliances типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="d8435-119">It defines hello managed application resource, which is a Microsoft.Solutions/appliances resource type.</span></span> <span data-ttu-id="d8435-120">Этот файл содержит все параметры hello, необходимое для ресурсов hello в applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="d8435-120">This file contains all hello parameters you need for hello resources in applianceMainTemplate.json.</span></span>

  <span data-ttu-id="d8435-121">В этом шаблоне задаются два важных свойства.</span><span class="sxs-lookup"><span data-stu-id="d8435-121">You set two important properties in this template.</span></span> <span data-ttu-id="d8435-122">Во-первых, hello **applianceDefinitionId** свойство — идентификатор hello определение hello управляемого приложения.</span><span class="sxs-lookup"><span data-stu-id="d8435-122">First, hello **applianceDefinitionId** property is hello ID of hello managed application definition.</span></span> <span data-ttu-id="d8435-123">Создайте определение hello далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="d8435-123">You create hello definition later in this topic.</span></span> <span data-ttu-id="d8435-124">При установке этого параметра, необходимо решить, какие подписки и toouse группы ресурсов для хранения hello определения управляемого приложения.</span><span class="sxs-lookup"><span data-stu-id="d8435-124">When setting this value, you must decide which subscription and resource group toouse for storing hello managed application definitions.</span></span> <span data-ttu-id="d8435-125">И необходимо решить, имя определения hello.</span><span class="sxs-lookup"><span data-stu-id="d8435-125">And, you must decide on a name for hello definition.</span></span> <span data-ttu-id="d8435-126">Идентификатор Hello имеет формат hello:</span><span class="sxs-lookup"><span data-stu-id="d8435-126">hello ID is in hello format:</span></span>

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  <span data-ttu-id="d8435-127">Во-вторых, hello **managedResourceGroupId** свойство — идентификатор hello hello группы ресурсов, где hello Azure ресурсы создаются.</span><span class="sxs-lookup"><span data-stu-id="d8435-127">Second, hello **managedResourceGroupId** property is hello ID of hello resource group where hello Azure resources are created.</span></span> <span data-ttu-id="d8435-128">Можно назначить значение для этого имени группы ресурсов или позволить hello пользователя введите имя.</span><span class="sxs-lookup"><span data-stu-id="d8435-128">You can assign a value for this resource group name or let hello user provide a name.</span></span> <span data-ttu-id="d8435-129">Hello с идентификатором hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d8435-129">hello format of hello ID is:</span></span>

  <span data-ttu-id="d8435-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span><span class="sxs-lookup"><span data-stu-id="d8435-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span></span>

  <span data-ttu-id="d8435-131">Привет, в следующем примере показан файл mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="d8435-131">hello following example shows a mainTemplate.json file.</span></span> <span data-ttu-id="d8435-132">Он указывает группу ресурсов для hello развертывания ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d8435-132">It specifies a resource group for hello deployed resources.</span></span> <span data-ttu-id="d8435-133">Hello идентификатор определения — toouse набор с именем определения **storageApp** в группу ресурсов с именем **managedApplicationGroup**.</span><span class="sxs-lookup"><span data-stu-id="d8435-133">hello definition ID is set toouse a definition named **storageApp** in a resource group named **managedApplicationGroup**.</span></span> <span data-ttu-id="d8435-134">Можно изменить эти значения toouse разные имена.</span><span class="sxs-lookup"><span data-stu-id="d8435-134">You can change these values toouse different names.</span></span> <span data-ttu-id="d8435-135">Укажите идентификатор подписки в идентификатор определения hello.</span><span class="sxs-lookup"><span data-stu-id="d8435-135">Provide your own subscription ID in hello definition ID.</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "variables": {
        "managedRGId": "[concat(resourceGroup().id,'-application-resources')]",
        "managedAppName": "[concat('managedStorage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Solutions/appliances",
            "name": "[variables('managedAppName')]",
            "apiVersion": "2016-09-01-preview",
            "location": "[resourceGroup().location]",
            "kind": "ServiceCatalog",
            "properties": {
                "managedResourceGroupId": "[variables('managedRGId')]",
                "applianceDefinitionId": "/subscriptions/<subscription-id>/resourceGroups/managedApplicationGroup/providers/Microsoft.Solutions/applianceDefinitions/storageApp",
                "parameters": {
                    "storageAccountNamePrefix": {
                        "value": "[parameters('storageAccountNamePrefix')]"
                    }
                }
            }
        }
    ]
  }
  ```

* <span data-ttu-id="d8435-136">**applianceCreateUiDefinition.json**: hello портал Azure использует этот файл toogenerate hello пользовательский интерфейс для пользователей, создающих hello управляемого приложения.</span><span class="sxs-lookup"><span data-stu-id="d8435-136">**applianceCreateUiDefinition.json**: hello Azure portal uses this file toogenerate hello user interface for users who create hello managed application.</span></span> <span data-ttu-id="d8435-137">Можно определить способ ввода каждого параметра пользователями.</span><span class="sxs-lookup"><span data-stu-id="d8435-137">You define how users provide input for each parameter.</span></span> <span data-ttu-id="d8435-138">например раскрывающийся список, текстовое поле, поле ввода пароля или другие средства ввода.</span><span class="sxs-lookup"><span data-stu-id="d8435-138">You can use options like a drop-down list, text box, password box, and other input tools.</span></span> <span data-ttu-id="d8435-139">toocreate файл определения пользовательского интерфейса для управляемого приложения. в статье toolearn [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8435-139">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>

  <span data-ttu-id="d8435-140">Hello следующем примере показан файл applianceCreateUiDefinition.json, позволяющий пользователям toospecify hello хранилища учетной записи префикс имени через текстового поля.</span><span class="sxs-lookup"><span data-stu-id="d8435-140">hello following example shows an applianceCreateUiDefinition.json file that enables users toospecify hello storage account name prefix through a textbox.</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
    "handler": "Microsoft.Compute.MultiVm",
    "version": "0.1.2-preview",
    "parameters": {
        "basics": [
            {
                "name": "storageAccounts",
                "type": "Microsoft.Common.TextBox",
                "label": "Storage account name prefix",
                "defaultValue": "storage",
                "toolTip": "Provide a value that is used for hello prefix of your storage account. Limit too11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-11 characters long."
                },
                "visible": true
            }
        ],
        "steps": [],
        "outputs": {
            "storageAccountNamePrefix": "[basics('storageAccounts')]"
        }
    }
  }
  ```

<span data-ttu-id="d8435-141">При готовности все файлы hello требуется упаковать их как ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="d8435-141">After all hello needed files are ready, package them as a .zip file.</span></span> <span data-ttu-id="d8435-142">Hello три файлы должны находиться на корневом уровне hello hello ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="d8435-142">hello three files must be at hello root level of hello .zip file.</span></span> <span data-ttu-id="d8435-143">Если поместить их в папке при создании hello управляемых определение приложения о том, что файлы отсутствуют требуемые hello сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="d8435-143">If you put them in a folder, you receive an error when creating hello managed application definition that states hello required files are not present.</span></span> <span data-ttu-id="d8435-144">Отправьте hello пакета tooan доступное расположение, из которых могут быть использованы.</span><span class="sxs-lookup"><span data-stu-id="d8435-144">Upload hello package tooan accessible location from where it can be consumed.</span></span> <span data-ttu-id="d8435-145">Hello оставшейся части этой статьи предполагается, что существует hello ZIP-файла в контейнер больших двоичных объектов хранилища общего доступа.</span><span class="sxs-lookup"><span data-stu-id="d8435-145">hello remainder of this article assumes hello .zip file exists in a publicly accessible storage blob container.</span></span>

## <a name="create-an-azure-active-directory-user-group-or-application"></a><span data-ttu-id="d8435-146">Создание группы пользователей или приложения Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8435-146">Create an Azure Active Directory user group or application</span></span>

<span data-ttu-id="d8435-147">второй шаг Hello — tooselect группы пользователей или приложения для управления ресурсами hello от имени клиента hello.</span><span class="sxs-lookup"><span data-stu-id="d8435-147">hello second step is tooselect a user group or application for managing hello resources on behalf of hello customer.</span></span> <span data-ttu-id="d8435-148">Данной группы пользователей или приложения имеет разрешения на hello управляемого ресурса группы соответствующим toohello роль, назначенная.</span><span class="sxs-lookup"><span data-stu-id="d8435-148">This user group or application has permissions on hello managed resource group according toohello role that is assigned.</span></span> <span data-ttu-id="d8435-149">Hello роль может быть любой встроенной роли управления доступом на основе ролей (RBAC), например владельца или участника.</span><span class="sxs-lookup"><span data-stu-id="d8435-149">hello role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span></span> <span data-ttu-id="d8435-150">Также можно предоставить отдельному пользователю разрешение toomanage hello ресурсов, но обычно назначается разрешение tooa пользователя группы.</span><span class="sxs-lookup"><span data-stu-id="d8435-150">You also can give an individual user permission toomanage hello resources, but typically you assign this permission tooa user group.</span></span> <span data-ttu-id="d8435-151">toocreate группу пользователей Active Directory в разделе [Создание группы и добавление членов в Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d8435-151">toocreate a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span></span>

<span data-ttu-id="d8435-152">Требуется идентификатор hello объекта группы toouse hello пользователя для управления ресурсами hello.</span><span class="sxs-lookup"><span data-stu-id="d8435-152">You need hello object ID of hello user group toouse for managing hello resources.</span></span> <span data-ttu-id="d8435-153">Hello в следующем примере показано, как tooget hello идентификатор объекта из группы hello отображаемого имени:</span><span class="sxs-lookup"><span data-stu-id="d8435-153">hello following example shows how tooget hello object ID from hello group's display name:</span></span>

```azurecli-interactive
az ad group show --group exampleGroupName
```

<span data-ttu-id="d8435-154">Hello примере команда возвращает hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="d8435-154">hello example command returns hello following output:</span></span>

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

<span data-ttu-id="d8435-155">Идентификатор объекта просто hello tooretrieve, использование</span><span class="sxs-lookup"><span data-stu-id="d8435-155">tooretrieve just hello object ID, use:</span></span>

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a><span data-ttu-id="d8435-156">Получить идентификатор определения роли hello</span><span class="sxs-lookup"><span data-stu-id="d8435-156">Get hello role definition ID</span></span>

<span data-ttu-id="d8435-157">Далее необходимо идентификатор определения роли hello hello RBAC встроенная роль, нужно toogrant доступа toohello пользователей, группы пользователей или приложение.</span><span class="sxs-lookup"><span data-stu-id="d8435-157">Next, you need hello role definition ID of hello RBAC built-in role you want toogrant access toohello user, user group, or application.</span></span> <span data-ttu-id="d8435-158">Как правило используется hello владельца или роль участника или чтения.</span><span class="sxs-lookup"><span data-stu-id="d8435-158">Typically, you use hello Owner or Contributor or Reader role.</span></span> <span data-ttu-id="d8435-159">Hello, следующая команда показывает, как tooget hello идентификатор определения роли для роли владельца hello:</span><span class="sxs-lookup"><span data-stu-id="d8435-159">hello following command shows how tooget hello role definition ID for hello Owner role:</span></span>


```azurecli-interactive
az role definition list --name owner
```

<span data-ttu-id="d8435-160">Эта команда возвращает hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="d8435-160">That command returns hello following output:</span></span>

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access tooresources.",
      "permissions": [
        {
          "actions": [
            "*"
         ],
         "notActions": []
        }
      ],
      "roleName": "Owner",
      "type": "BuiltInRole"
    },
    "type": "Microsoft.Authorization/roleDefinitions"
}
```

<span data-ttu-id="d8435-161">Вы должны hello значение свойства «имя» hello из предшествующих пример hello.</span><span class="sxs-lookup"><span data-stu-id="d8435-161">You need hello value of hello "name" property from hello preceding example.</span></span> <span data-ttu-id="d8435-162">Вы можете получить только это свойство, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d8435-162">You can retrieve just that property with:</span></span>

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a><span data-ttu-id="d8435-163">Создайте определение приложения hello управляемых</span><span class="sxs-lookup"><span data-stu-id="d8435-163">Create hello managed application definition</span></span>

<span data-ttu-id="d8435-164">Если у вас еще нет группы ресурсов для хранения определения управляемого приложения, создайте ее.</span><span class="sxs-lookup"><span data-stu-id="d8435-164">If you do not already have a resource group for storing your managed application definition, create one now:</span></span>

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

<span data-ttu-id="d8435-165">Теперь можно Создайте определение ресурса hello управляемого приложения.</span><span class="sxs-lookup"><span data-stu-id="d8435-165">Now, create hello managed application definition resource.</span></span>

```azurecli-interactive
az managedapp definition create \
  --name storageApp \
  --location "westcentralus" \
  --resource-group managedApplicationGroup \
  --lock-level ReadOnly \
  --display-name myteststorageapp \
  --description storageapp \
  --authorizations "$groupid:$roleid" \
  --package-file-uri <uri-path-to-zip-file>
```

<span data-ttu-id="d8435-166">используются следующие параметры Hello, используемый в предыдущих пример hello.</span><span class="sxs-lookup"><span data-stu-id="d8435-166">hello parameters used in hello preceding example are:</span></span>

* <span data-ttu-id="d8435-167">**Группа ресурсов**: hello имя группы ресурсов hello, где hello управляемое определение приложения создается.</span><span class="sxs-lookup"><span data-stu-id="d8435-167">**resource-group**: hello name of hello resource group where hello managed application definition is created.</span></span>
* <span data-ttu-id="d8435-168">**уровень блокировки**: hello тип блокировки включен в группу hello управляемых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d8435-168">**lock-level**: hello type of lock placed on hello managed resource group.</span></span> <span data-ttu-id="d8435-169">Они препятствуют клиента hello нежелательных операций в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d8435-169">It prevents hello customer from performing undesirable operations on this resource group.</span></span> <span data-ttu-id="d8435-170">В настоящее время только для чтения — hello поддерживается только уровень блокировки.</span><span class="sxs-lookup"><span data-stu-id="d8435-170">Currently, ReadOnly is hello only supported lock level.</span></span> <span data-ttu-id="d8435-171">Если указан только для чтения, hello клиентов можно только для чтения hello ресурсы в группе hello управляемых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d8435-171">When ReadOnly is specified, hello customer can only read hello resources present in hello managed resource group.</span></span>
* <span data-ttu-id="d8435-172">**параметры авторизации**: описывает идентификатор участника hello и hello идентификатор определения роли, которые toohello управляемого ресурса используется toogrant разрешений группы.</span><span class="sxs-lookup"><span data-stu-id="d8435-172">**authorizations**: Describes hello principal ID and hello role definition ID that are used toogrant permission toohello managed resource group.</span></span> <span data-ttu-id="d8435-173">Он указан в формате hello `<principalId>:<roleDefinitionId>`.</span><span class="sxs-lookup"><span data-stu-id="d8435-173">It's specified in hello format of `<principalId>:<roleDefinitionId>`.</span></span> <span data-ttu-id="d8435-174">Для него можно указать несколько значений.</span><span class="sxs-lookup"><span data-stu-id="d8435-174">Multiple values also can be specified for this property.</span></span> <span data-ttu-id="d8435-175">Если требуются несколько значений, их следует указывать в форме hello `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span><span class="sxs-lookup"><span data-stu-id="d8435-175">If multiple values are needed, they should be specified in hello form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span></span> <span data-ttu-id="d8435-176">Разные значения разделяются пробелами.</span><span class="sxs-lookup"><span data-stu-id="d8435-176">Multiple values are separated by a space.</span></span>
* <span data-ttu-id="d8435-177">**uri для файла пакета**: hello расположение пакета управляемого приложения hello, содержащего файлы шаблона hello, которые могут быть BLOB-объект хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="d8435-177">**package-file-uri**: hello location of hello managed application package that contains hello template files, which can be an Azure Storage blob.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8435-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d8435-178">Next steps</span></span>

* <span data-ttu-id="d8435-179">Введение toomanaged приложений, в разделе [Обзор управляемого приложения](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8435-179">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="d8435-180">Примеры файлов hello в разделе [управляемых образцы приложений](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="d8435-180">For examples of hello files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span></span>
* <span data-ttu-id="d8435-181">Дополнительные сведения об использовании управляемых приложений из каталога услуг см. в разделе [Использование управляемого приложения Azure](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="d8435-181">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
* <span data-ttu-id="d8435-182">Сведения о публикации toohello управляемые приложения Azure Marketplace см. в разделе [Azure управляемого приложения в hello Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="d8435-182">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="d8435-183">Сведения о использование управляемого приложения из hello Marketplace в разделе [использовать Azure управляемого приложения в hello Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="d8435-183">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="d8435-184">toocreate файл определения пользовательского интерфейса для управляемого приложения. в статье toolearn [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8435-184">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
