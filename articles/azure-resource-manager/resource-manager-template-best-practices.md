---
title: "Рекомендации по созданию шаблонов Resource Manager | Документация Майкрософт"
description: "Рекомендации по упрощению шаблонов Azure Resource Manager."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: a23301ba88279af3f7bf4d353ae808e9eeb0900d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a><span data-ttu-id="01da7-103">Рекомендации по созданию шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="01da7-103">Best practices for creating Azure Resource Manager templates</span></span>
<span data-ttu-id="01da7-104">Эти рекомендации помогут создавать надежные и удобные в использовании шаблоны Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="01da7-104">These guidelines can help you create Azure Resource Manager templates that are reliable and easy to use.</span></span> <span data-ttu-id="01da7-105">Приведенные здесь указания носят рекомендательный характер и</span><span class="sxs-lookup"><span data-stu-id="01da7-105">The guidelines are only suggestions.</span></span> <span data-ttu-id="01da7-106">не являются обязательными (если это явно не обозначено).</span><span class="sxs-lookup"><span data-stu-id="01da7-106">They are not requirements, except where noted.</span></span> <span data-ttu-id="01da7-107">Для вашего сценария может потребоваться использовать один из описанных ниже подходов или примеров.</span><span class="sxs-lookup"><span data-stu-id="01da7-107">Your scenario might require a variation of one of the following approaches or examples.</span></span>

## <a name="resource-names"></a><span data-ttu-id="01da7-108">Имена ресурсов</span><span class="sxs-lookup"><span data-stu-id="01da7-108">Resource names</span></span>
<span data-ttu-id="01da7-109">Обычно в Resource Manager вы работаете с именами ресурсов трех типов:</span><span class="sxs-lookup"><span data-stu-id="01da7-109">Generally, you work with three types of resource names in Resource Manager:</span></span>

* <span data-ttu-id="01da7-110">имена ресурсов, которые должны быть уникальными;</span><span class="sxs-lookup"><span data-stu-id="01da7-110">Resource names that must be unique.</span></span>
* <span data-ttu-id="01da7-111">имена ресурсов, которые могут не быть уникальными, но должны помогать в определении ресурса на основе контекста;</span><span class="sxs-lookup"><span data-stu-id="01da7-111">Resource names that are not required to be unique, but you choose to provide a name that can help you identify a resource based on context.</span></span>
* <span data-ttu-id="01da7-112">имена ресурсов, которые могут быть универсальными.</span><span class="sxs-lookup"><span data-stu-id="01da7-112">Resource names that can be generic.</span></span>

 <span data-ttu-id="01da7-113">Сведения об ограничениях имен ресурсов см. в статье [Рекомендуемые соглашения об именовании для ресурсов Azure](../guidance/guidance-naming-conventions.md).</span><span class="sxs-lookup"><span data-stu-id="01da7-113">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span></span>

### <a name="unique-resource-names"></a><span data-ttu-id="01da7-114">Уникальные имена ресурсов</span><span class="sxs-lookup"><span data-stu-id="01da7-114">Unique resource names</span></span>
<span data-ttu-id="01da7-115">Необходимо указать уникальное имя для любого типа ресурса, который имеет конечную точку доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="01da7-115">You must provide a unique resource name for any resource type that has a data access endpoint.</span></span> <span data-ttu-id="01da7-116">Ниже приведено несколько распространенных типов ресурсов, для которых требуются уникальные имена:</span><span class="sxs-lookup"><span data-stu-id="01da7-116">Some common resource types that require a unique name include:</span></span>

* <span data-ttu-id="01da7-117">служба хранилища Azure<sup>1</sup>;</span><span class="sxs-lookup"><span data-stu-id="01da7-117">Azure Storage<sup>1</sup></span></span> 
* <span data-ttu-id="01da7-118">веб-приложения службы приложений Azure;</span><span class="sxs-lookup"><span data-stu-id="01da7-118">Web Apps feature of Azure App Service</span></span>
* <span data-ttu-id="01da7-119">SQL Server</span><span class="sxs-lookup"><span data-stu-id="01da7-119">SQL Server</span></span>
* <span data-ttu-id="01da7-120">Хранилище ключей Azure</span><span class="sxs-lookup"><span data-stu-id="01da7-120">Azure Key Vault</span></span>
* <span data-ttu-id="01da7-121">кэш Azure Redis</span><span class="sxs-lookup"><span data-stu-id="01da7-121">Azure Redis Cache</span></span>
* <span data-ttu-id="01da7-122">Пакетная служба Azure</span><span class="sxs-lookup"><span data-stu-id="01da7-122">Azure Batch</span></span>
* <span data-ttu-id="01da7-123">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="01da7-123">Azure Traffic Manager</span></span>
* <span data-ttu-id="01da7-124">поиск Azure;</span><span class="sxs-lookup"><span data-stu-id="01da7-124">Azure Search</span></span>
* <span data-ttu-id="01da7-125">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="01da7-125">Azure HDInsight</span></span>

<span data-ttu-id="01da7-126"><sup>1</sup> Имена учетных записей хранения также должны содержать до 24 знаков в нижнем регистре без дефисов.</span><span class="sxs-lookup"><span data-stu-id="01da7-126"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span></span>

<span data-ttu-id="01da7-127">Если указать параметр для имени ресурса, при развертывании необходимо указать уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="01da7-127">If you provide a parameter for a resource name, you must provide a unique name when you deploy the resource.</span></span> <span data-ttu-id="01da7-128">При необходимости вы можете создать переменную, которая использует функцию [uniqueString()](resource-group-template-functions-string.md#uniquestring) для создания имени.</span><span class="sxs-lookup"><span data-stu-id="01da7-128">Optionally, you can create a variable that uses the [uniqueString()](resource-group-template-functions-string.md#uniquestring) function to generate a name.</span></span> 

<span data-ttu-id="01da7-129">Вам также может потребоваться добавить префикс или суффикс к результату **uniqueString**.</span><span class="sxs-lookup"><span data-stu-id="01da7-129">You also might want to add a prefix or suffix to the **uniqueString** result.</span></span> <span data-ttu-id="01da7-130">Измените уникальное имя, чтобы было проще определить тип ресурса по его имени.</span><span class="sxs-lookup"><span data-stu-id="01da7-130">Modifying the unique name can help you more easily identify the resource type from the name.</span></span> <span data-ttu-id="01da7-131">Например, можно создать уникальное имя учетной записи хранения с помощью следующей переменной:</span><span class="sxs-lookup"><span data-stu-id="01da7-131">For example, you can generate a unique name for a storage account by using the following variable:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a><span data-ttu-id="01da7-132">Имена ресурсов для идентификации</span><span class="sxs-lookup"><span data-stu-id="01da7-132">Resource names for identification</span></span>
<span data-ttu-id="01da7-133">Для некоторых типов ресурсов необязательно указывать уникальные имена.</span><span class="sxs-lookup"><span data-stu-id="01da7-133">Some resource types you might want to name, but their names do not have to be unique.</span></span> <span data-ttu-id="01da7-134">Вы можете просто указать имя, которое определяет контекст и тип ресурса.</span><span class="sxs-lookup"><span data-stu-id="01da7-134">For these resource types, you can provide a name that identifies both the resource context and the resource type.</span></span> <span data-ttu-id="01da7-135">Укажите описательное имя, которое поможет определить ресурс в списке ресурсов.</span><span class="sxs-lookup"><span data-stu-id="01da7-135">Provide a descriptive name that helps you identify the resource in a list of resources.</span></span> <span data-ttu-id="01da7-136">Если для различных развертываний требуется использовать разные имена ресурсов, то используйте для имени следующий параметр:</span><span class="sxs-lookup"><span data-stu-id="01da7-136">If you need to use a different resource name for different deployments, you can use a parameter for the name:</span></span>

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "The name of the VM to create."
        }
    }
}
```

<span data-ttu-id="01da7-137">Если необходимо передать имя во время развертывания, используйте следующую переменную:</span><span class="sxs-lookup"><span data-stu-id="01da7-137">If you do not need to pass in a name during deployment, you can use a variable:</span></span> 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

<span data-ttu-id="01da7-138">Вы также можете использовать жестко заданное значение:</span><span class="sxs-lookup"><span data-stu-id="01da7-138">You also can use a hard-coded value:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a><span data-ttu-id="01da7-139">Универсальные имена ресурсов</span><span class="sxs-lookup"><span data-stu-id="01da7-139">Generic resource names</span></span>
<span data-ttu-id="01da7-140">Для типов ресурсов, к которым часто обращаются через другой ресурс, можно использовать универсальное имя, жестко заданное в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="01da7-140">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in the template.</span></span> <span data-ttu-id="01da7-141">Например, можно задать стандартное универсальное имя для правил брандмауэра на SQL Server:</span><span class="sxs-lookup"><span data-stu-id="01da7-141">For example, you can set a standard, generic name for firewall rules on a SQL server:</span></span>

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a><span data-ttu-id="01da7-142">Параметры</span><span class="sxs-lookup"><span data-stu-id="01da7-142">Parameters</span></span>
<span data-ttu-id="01da7-143">Ниже приведены некоторые рекомендации по работе с параметрами.</span><span class="sxs-lookup"><span data-stu-id="01da7-143">The following information can be helpful when you work with parameters:</span></span>

* <span data-ttu-id="01da7-144">Используйте как можно меньше параметров.</span><span class="sxs-lookup"><span data-stu-id="01da7-144">Minimize your use of parameters.</span></span> <span data-ttu-id="01da7-145">По возможности используйте переменную или литеральное значение.</span><span class="sxs-lookup"><span data-stu-id="01da7-145">Whenever possible, use a variable or a literal value.</span></span> <span data-ttu-id="01da7-146">Используйте параметры только для следующих сценариев:</span><span class="sxs-lookup"><span data-stu-id="01da7-146">Use parameters only for these scenarios:</span></span>
   
   * <span data-ttu-id="01da7-147">параметры, значения которых должны отличаться в зависимости от среды (SKU, размер или емкость);</span><span class="sxs-lookup"><span data-stu-id="01da7-147">Settings that you want to use variations of according to environment (SKU, size, capacity).</span></span>
   * <span data-ttu-id="01da7-148">имена ресурсов, которые вы хотите задать, чтобы упростить идентификацию;</span><span class="sxs-lookup"><span data-stu-id="01da7-148">Resource names that you want to specify for easy identification.</span></span>
   * <span data-ttu-id="01da7-149">значения, которые часто используются для выполнения других задач (например, имя пользователя администратора);</span><span class="sxs-lookup"><span data-stu-id="01da7-149">Values that you use frequently to complete other tasks (such as an admin user name).</span></span>
   * <span data-ttu-id="01da7-150">секреты (например, пароли);</span><span class="sxs-lookup"><span data-stu-id="01da7-150">Secrets (such as passwords).</span></span>
   * <span data-ttu-id="01da7-151">числа или массивы значений, используемые при создании нескольких экземпляров типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="01da7-151">The number or array of values to use when you create multiple instances of a resource type.</span></span>
* <span data-ttu-id="01da7-152">Имена для параметров необходимо указывать в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="01da7-152">Use camel case for parameter names.</span></span>
* <span data-ttu-id="01da7-153">Укажите описание для каждого параметра в метаданных.</span><span class="sxs-lookup"><span data-stu-id="01da7-153">Provide a description of every parameter in the metadata:</span></span>

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "The type of the new storage account created to store the VM disks."
           }
       }
   }
   ```

* <span data-ttu-id="01da7-154">Определите значения по умолчанию для параметров (за исключением паролей и ключей SSH).</span><span class="sxs-lookup"><span data-stu-id="01da7-154">Define default values for parameters (except for passwords and SSH keys):</span></span>
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "The type of the new storage account created to store the VM disks."
            }
        }
   }
   ```

* <span data-ttu-id="01da7-155">Используйте **securestring** для всех паролей и секретов.</span><span class="sxs-lookup"><span data-stu-id="01da7-155">Use **SecureString** for all passwords and secrets:</span></span> 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "The value of the secret to store in the vault."
           }
       }
   }
   ```

* <span data-ttu-id="01da7-156">По возможности не используйте параметр, чтобы указать расположение.</span><span class="sxs-lookup"><span data-stu-id="01da7-156">Whenever possible, don't use a parameter to specify location.</span></span> <span data-ttu-id="01da7-157">Вместо этого используйте свойство **location** группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="01da7-157">Instead, use the **location** property of the resource group.</span></span> <span data-ttu-id="01da7-158">Чтобы развернуть ресурсы в шаблоне в том же расположении, что и группа ресурсов, используйте выражение **resourceGroup().location** для всех ресурсов.</span><span class="sxs-lookup"><span data-stu-id="01da7-158">By using the **resourceGroup().location** expression for all your resources, resources in the template are deployed in the same location as the resource group:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   <span data-ttu-id="01da7-159">Если тип ресурса поддерживается в ограниченном наборе расположений, то допустимое расположение необходимо указать непосредственно в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="01da7-159">If a resource type is supported in only a limited number of locations, you might want to specify a valid location directly in the template.</span></span> <span data-ttu-id="01da7-160">Когда вам необходимо использовать параметр **location**, то указывайте его значение для ресурсов, которые могут находиться в одном расположении, насколько это возможно.</span><span class="sxs-lookup"><span data-stu-id="01da7-160">If you must use a **location** parameter, share that parameter value as much as possible with resources that are likely to be in the same location.</span></span> <span data-ttu-id="01da7-161">Так пользователям придется реже указывать информацию о расположении.</span><span class="sxs-lookup"><span data-stu-id="01da7-161">This minimizes the number of times users are asked to provide location information.</span></span>
* <span data-ttu-id="01da7-162">Избегайте использовать параметр или переменную для версии API для типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="01da7-162">Avoid using a parameter or variable for the API version for a resource type.</span></span> <span data-ttu-id="01da7-163">Свойства и значения ресурса могут отличаться для разных версий.</span><span class="sxs-lookup"><span data-stu-id="01da7-163">Resource properties and values can vary by version number.</span></span> <span data-ttu-id="01da7-164">Функции IntelliSense в редакторах кода не могут определить правильную схему, если версия API указана в качестве значения параметра или переменной.</span><span class="sxs-lookup"><span data-stu-id="01da7-164">IntelliSense in a code editor cannot determine the correct schema when the API version is set to a parameter or variable.</span></span> <span data-ttu-id="01da7-165">Вместо этого жестко задайте версию API в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="01da7-165">Instead, hard-code the API version in the template.</span></span>

## <a name="variables"></a><span data-ttu-id="01da7-166">Переменные</span><span class="sxs-lookup"><span data-stu-id="01da7-166">Variables</span></span>
<span data-ttu-id="01da7-167">Ниже приведены некоторые рекомендации по работе с переменными.</span><span class="sxs-lookup"><span data-stu-id="01da7-167">The following information can be helpful when you work with variables:</span></span>

* <span data-ttu-id="01da7-168">Применяйте переменные для значений, которые необходимо использовать в шаблоне более одного раза.</span><span class="sxs-lookup"><span data-stu-id="01da7-168">Use variables for values that you need to use more than once in a template.</span></span> <span data-ttu-id="01da7-169">Если значение используется только один раз, жестко задайте его. Это облегчит чтение шаблона.</span><span class="sxs-lookup"><span data-stu-id="01da7-169">If a value is used only once, a hard-coded value makes your template easier to read.</span></span>
* <span data-ttu-id="01da7-170">Нельзя использовать функцию [reference](resource-group-template-functions-resource.md#reference) в разделе **переменных** шаблона.</span><span class="sxs-lookup"><span data-stu-id="01da7-170">You cannot use the [reference](resource-group-template-functions-resource.md#reference) function in the **variables** section of the template.</span></span> <span data-ttu-id="01da7-171">Функция **reference** получает свое значение из состояния среды выполнения ресурса,</span><span class="sxs-lookup"><span data-stu-id="01da7-171">The **reference** function derives its value from the resource's runtime state.</span></span> <span data-ttu-id="01da7-172">а переменные разрешаются при начальной обработке шаблона.</span><span class="sxs-lookup"><span data-stu-id="01da7-172">However, variables are resolved during the initial parsing of the template.</span></span> <span data-ttu-id="01da7-173">Сформируйте значения, которым требуется функция **reference**, непосредственно в разделе **resources** или **outputs** шаблона.</span><span class="sxs-lookup"><span data-stu-id="01da7-173">Construct values that need the **reference** function directly in the **resources** or **outputs** section of the template.</span></span>
* <span data-ttu-id="01da7-174">Добавьте переменные для имен ресурсов, которые должны быть уникальными, как описано в разделе [Имена ресурсов](#resource-names).</span><span class="sxs-lookup"><span data-stu-id="01da7-174">Include variables for resource names that must be unique, as described in [Resource names](#resource-names).</span></span>
* <span data-ttu-id="01da7-175">Переменные можно группировать в составные объекты.</span><span class="sxs-lookup"><span data-stu-id="01da7-175">You can group variables into complex objects.</span></span> <span data-ttu-id="01da7-176">Используйте формат **переменная.дополнительный_элемент** для ссылки на значение из составного объекта.</span><span class="sxs-lookup"><span data-stu-id="01da7-176">Use the **variable.subentry** format to reference a value from a complex object.</span></span> <span data-ttu-id="01da7-177">Группирование переменных помогает следить за связанными переменными</span><span class="sxs-lookup"><span data-stu-id="01da7-177">Grouping variables can help you track related variables.</span></span> <span data-ttu-id="01da7-178">и улучшает читаемость шаблона.</span><span class="sxs-lookup"><span data-stu-id="01da7-178">It also improves readability of the template.</span></span> <span data-ttu-id="01da7-179">Ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="01da7-179">Here's an example:</span></span>
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > <span data-ttu-id="01da7-180">Составной объект не может содержать выражение, которое ссылается на значение из составного объекта.</span><span class="sxs-lookup"><span data-stu-id="01da7-180">A complex object cannot contain an expression that references a value from a complex object.</span></span> <span data-ttu-id="01da7-181">Для этого определите отдельную переменную.</span><span class="sxs-lookup"><span data-stu-id="01da7-181">Define a separate variable for this purpose.</span></span>
   > 
   > 
   
     <span data-ttu-id="01da7-182">Расширенные примеры использования составных объектов в качестве переменных доступны в статье [Передача состояния в шаблоны Azure Resource Manager и из них](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="01da7-182">For advanced examples of using complex objects as variables, see [Share state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="resources"></a><span data-ttu-id="01da7-183">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="01da7-183">Resources</span></span>
<span data-ttu-id="01da7-184">Ниже приведены некоторые рекомендации по работе с ресурсами.</span><span class="sxs-lookup"><span data-stu-id="01da7-184">The following information can be helpful when you work with resources:</span></span>

* <span data-ttu-id="01da7-185">Чтобы другим участникам было проще понять назначение этого ресурса, укажите **комментарии** для каждого ресурса в шаблоне:</span><span class="sxs-lookup"><span data-stu-id="01da7-185">To help other contributors understand the purpose of the resource, specify **comments** for each resource in the template:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used to store the VM disks.",
         ...
     }
   ]
   ```

* <span data-ttu-id="01da7-186">Используйте теги для добавления метаданных в ресурсы.</span><span class="sxs-lookup"><span data-stu-id="01da7-186">You can use tags to add metadata to resources.</span></span> <span data-ttu-id="01da7-187">С помощью метаданных можно указать дополнительную информацию о ресурсах.</span><span class="sxs-lookup"><span data-stu-id="01da7-187">Use metadata to add information about your resources.</span></span> <span data-ttu-id="01da7-188">Например, можно добавить метаданные для записи сведений о выставлении счетов ресурса.</span><span class="sxs-lookup"><span data-stu-id="01da7-188">For example, you can add metadata to record billing details for a resource.</span></span> <span data-ttu-id="01da7-189">Дополнительные сведения см. в статье [Использование тегов для организации ресурсов в Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="01da7-189">For more information, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span></span>
* <span data-ttu-id="01da7-190">Если вы используете в шаблоне *общедоступную конечную точку* (например, общедоступную конечную точку хранилища BLOB-объектов Azure), то *не следует жестко задавать* пространство имен.</span><span class="sxs-lookup"><span data-stu-id="01da7-190">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* the namespace.</span></span> <span data-ttu-id="01da7-191">Используйте функцию **reference** для динамического извлечения пространства имен.</span><span class="sxs-lookup"><span data-stu-id="01da7-191">Use the **reference** function to dynamically retrieve the namespace.</span></span> <span data-ttu-id="01da7-192">Вы можете использовать этот подход, чтобы развернуть шаблон в другом общедоступном пространстве имен, не изменяя конечную точку в шаблоне вручную.</span><span class="sxs-lookup"><span data-stu-id="01da7-192">You can use this approach to deploy the template to different public namespace environments without manually changing the endpoint in the template.</span></span> <span data-ttu-id="01da7-193">Задайте для версии API ту же версию, которая указана в учетной записи хранения в вашем шаблоне.</span><span class="sxs-lookup"><span data-stu-id="01da7-193">Set the API version to the same version that you are using for the storage account in your template:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="01da7-194">Если учетная запись хранения развертывается в том же создаваемом шаблоне, то при указании ссылки на ресурс нет необходимости указывать пространство имен поставщика.</span><span class="sxs-lookup"><span data-stu-id="01da7-194">If the storage account is deployed in the same template that you are creating, you do not need to specify the provider namespace when you reference the resource.</span></span> <span data-ttu-id="01da7-195">Вот как выглядит упрощенный синтаксис:</span><span class="sxs-lookup"><span data-stu-id="01da7-195">This is the simplified syntax:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="01da7-196">Если в шаблоне имеются другие значения, настроенные для использования общедоступного пространства имен, измените их, указав одну и ту же функцию **reference**.</span><span class="sxs-lookup"><span data-stu-id="01da7-196">If you have other values in your template that are configured to use a public namespace, change these values to reflect the same **reference** function.</span></span> <span data-ttu-id="01da7-197">Например, можно задать свойство **storageUri** диагностического профиля виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="01da7-197">For example, you can set the **storageUri** property of the virtual machine diagnostics profile:</span></span>
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   <span data-ttu-id="01da7-198">Вы также можете использовать функцию reference для ссылки на учетную запись хранения в другой группе ресурсов:</span><span class="sxs-lookup"><span data-stu-id="01da7-198">You also can reference an existing storage account that is in a different resource group:</span></span>

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* <span data-ttu-id="01da7-199">Назначайте общедоступные IP-адреса виртуальной машине только в том случае, если это требуется для работы приложения.</span><span class="sxs-lookup"><span data-stu-id="01da7-199">Assign public IP addresses to a virtual machine only when an application requires it.</span></span> <span data-ttu-id="01da7-200">Чтобы подключиться к виртуальной машине с целью отладки, управления или администрирования, используйте правила преобразования сетевых адресов для входящих подключений, шлюз виртуальной машины или jumpbox.</span><span class="sxs-lookup"><span data-stu-id="01da7-200">To connect to a virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span></span>
   
     <span data-ttu-id="01da7-201">Дополнительные сведения о подключении к виртуальным машинам можно получить в приведенных ниже статьях.</span><span class="sxs-lookup"><span data-stu-id="01da7-201">For more information about connecting to virtual machines, see:</span></span>
   
   * <span data-ttu-id="01da7-202">[Run Windows VMs for an N-tier application](../guidance/guidance-compute-n-tier-vm.md) (Запуск виртуальных машин Windows в n-уровневом приложении)</span><span class="sxs-lookup"><span data-stu-id="01da7-202">[Run VMs for an N-tier architecture in Azure](../guidance/guidance-compute-n-tier-vm.md)</span></span>
   * [<span data-ttu-id="01da7-203">Настройка доступа WinRM для виртуальных машин в Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="01da7-203">Set up WinRM access for VMs in Azure Resource Manager</span></span>](../virtual-machines/windows/winrm.md)
   * [<span data-ttu-id="01da7-204">Открытие портов для виртуальной машины в Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="01da7-204">Allow external access to your VM by using the Azure portal</span></span>](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [<span data-ttu-id="01da7-205">Открытие портов и конечных точек для виртуальной машины в Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="01da7-205">Allow external access to your VM by using PowerShell</span></span>](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [<span data-ttu-id="01da7-206">Открытие портов и конечных точек для виртуальной машины Linux с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="01da7-206">Allow external access to your Linux VM by using Azure CLI</span></span>](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* <span data-ttu-id="01da7-207">Свойство **DomainNameLabel** для общедоступных IP-адресов должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="01da7-207">The **domainNameLabel** property for public IP addresses must be unique.</span></span> <span data-ttu-id="01da7-208">Свойство **domainNameLabel** должно содержать то 3 до 63 знаков и соответствовать правилам, определенным этим регулярным выражением: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span><span class="sxs-lookup"><span data-stu-id="01da7-208">The **domainNameLabel** value must be between 3 and 63 characters long, and follow the rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span></span> <span data-ttu-id="01da7-209">Так как функция **uniqueString** создает строку длиной 13 знаков, в параметре **dnsPrefixString** можно использовать не более 50 знаков:</span><span class="sxs-lookup"><span data-stu-id="01da7-209">Because the **uniqueString** function generates a string that is 13 characters long, the **dnsPrefixString** parameter is limited to 50 characters:</span></span>

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "The DNS label for the public IP address. It must be lowercase. It should match the following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* <span data-ttu-id="01da7-210">При добавлении пароля в расширение пользовательских скриптов используйте свойство **commandToExecute** в **protectedSettings**:</span><span class="sxs-lookup"><span data-stu-id="01da7-210">When you add a password to a custom script extension, use the **commandToExecute** property in the **protectedSettings** property:</span></span>
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > <span data-ttu-id="01da7-211">Чтобы обеспечить шифрование секретов, которые передаются как параметры в виртуальные машины и расширения, необходимо использовать свойство **protectedSettings** соответствующих расширений.</span><span class="sxs-lookup"><span data-stu-id="01da7-211">To ensure that secrets are encrypted when they are passed as parameters to VMs and extensions, use the **protectedSettings** property of the relevant extensions.</span></span>
   > 
   > 

## <a name="outputs"></a><span data-ttu-id="01da7-212">outputs</span><span class="sxs-lookup"><span data-stu-id="01da7-212">Outputs</span></span>
<span data-ttu-id="01da7-213">Если вы используете шаблон, чтобы создать общедоступные IP-адреса, включая раздел **outputs**, который возвращает сведения об IP-адресах и полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="01da7-213">If you use a template to create public IP addresses, include an **outputs** section that returns details of the IP address and the fully qualified domain name (FQDN).</span></span> <span data-ttu-id="01da7-214">С помощью этих выходных данных можно легко получить сведения об общедоступных IP-адресах и полных доменных именах после развертывания.</span><span class="sxs-lookup"><span data-stu-id="01da7-214">You can use output values to easily retrieve details about public IP addresses and FQDNs after deployment.</span></span> <span data-ttu-id="01da7-215">При указании ссылки на ресурс используйте версию API, которая была использована для его создания:</span><span class="sxs-lookup"><span data-stu-id="01da7-215">When you reference the resource, use the API version that you used to create it:</span></span> 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a><span data-ttu-id="01da7-216">Отдельный шаблон и вложенные шаблоны</span><span class="sxs-lookup"><span data-stu-id="01da7-216">Single template vs. nested templates</span></span>
<span data-ttu-id="01da7-217">Для развертывания решения можно использовать отдельный шаблон или основной шаблон с несколькими вложенными шаблонами.</span><span class="sxs-lookup"><span data-stu-id="01da7-217">To deploy your solution, you can use either a single template or a main template with multiple nested templates.</span></span> <span data-ttu-id="01da7-218">Вложенные шаблоны обычно используются для более сложных сценариев.</span><span class="sxs-lookup"><span data-stu-id="01da7-218">Nested templates are common for more advanced scenarios.</span></span> <span data-ttu-id="01da7-219">Использование вложенных шаблонов обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="01da7-219">Using a nested template gives you the following advantages:</span></span>

* <span data-ttu-id="01da7-220">вы можете разбить решение на целевые компоненты;</span><span class="sxs-lookup"><span data-stu-id="01da7-220">You can break down a solution into targeted components.</span></span>
* <span data-ttu-id="01da7-221">вложенные шаблоны можно повторно использовать в разных основных шаблонах.</span><span class="sxs-lookup"><span data-stu-id="01da7-221">You can reuse nested templates with different main templates.</span></span>

<span data-ttu-id="01da7-222">Если вы решили использовать вложенные шаблоны, воспользуйтесь приведенными ниже рекомендациями, чтобы стандартизировать структуру шаблона.</span><span class="sxs-lookup"><span data-stu-id="01da7-222">If you choose to use nested templates, the following guidelines can help you standardize your template design.</span></span> <span data-ttu-id="01da7-223">Эти рекомендации основаны на статье [Приемы разработки шаблонов Azure Resource Manager при развертывании сложных решений](best-practices-resource-manager-design-templates.md).</span><span class="sxs-lookup"><span data-stu-id="01da7-223">These guidelines are based on [patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="01da7-224">Мы советуем структуру, которая состоит из следующих шаблонов:</span><span class="sxs-lookup"><span data-stu-id="01da7-224">We recommend a design that has the following templates:</span></span>

* <span data-ttu-id="01da7-225">**Основной шаблон** (azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="01da7-225">**Main template** (azuredeploy.json).</span></span> <span data-ttu-id="01da7-226">Используется для входных параметров.</span><span class="sxs-lookup"><span data-stu-id="01da7-226">Use for the input parameters.</span></span>
* <span data-ttu-id="01da7-227">**Шаблон общих ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="01da7-227">**Shared resources template**.</span></span> <span data-ttu-id="01da7-228">Используется для развертывания общих ресурсов, используемых всеми прочими ресурсами (например, виртуальная сеть и группы доступности).</span><span class="sxs-lookup"><span data-stu-id="01da7-228">Use to deploy shared resources that all other resources use (for example, virtual network and availability sets).</span></span> <span data-ttu-id="01da7-229">Используйте выражение **dependsOn**, чтобы обеспечить развертывание этого шаблона раньше остальных шаблонов.</span><span class="sxs-lookup"><span data-stu-id="01da7-229">Use the **dependsOn** expression to ensure that this template is deployed before other templates.</span></span>
* <span data-ttu-id="01da7-230">**Шаблон дополнительных ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="01da7-230">**Optional resources template**.</span></span> <span data-ttu-id="01da7-231">Используется для условного развертывания ресурсов на основе параметра (например, jumpbox).</span><span class="sxs-lookup"><span data-stu-id="01da7-231">Use to conditionally deploy resources based on a parameter (for example, a jumpbox).</span></span>
* <span data-ttu-id="01da7-232">**Шаблон элемента ресурсов.**</span><span class="sxs-lookup"><span data-stu-id="01da7-232">**Member resources template**.</span></span> <span data-ttu-id="01da7-233">У каждого типа экземпляра в пределах уровня приложения есть собственная конфигурация.</span><span class="sxs-lookup"><span data-stu-id="01da7-233">Each instance type within an application tier has its own configuration.</span></span> <span data-ttu-id="01da7-234">В пределах уровня можно определить разные типы экземпляров.</span><span class="sxs-lookup"><span data-stu-id="01da7-234">Within a tier, you can define different instance types.</span></span> <span data-ttu-id="01da7-235">(Например, первый экземпляр создает кластер, а дополнительные экземпляры добавляются в существующий кластер.) У каждого типа экземпляра есть собственный шаблон развертывания.</span><span class="sxs-lookup"><span data-stu-id="01da7-235">(For example, the first instance creates a cluster, and additional instances are added to the existing cluster.) Each instance type has its own deployment template.</span></span>
* <span data-ttu-id="01da7-236">**Сценарии**.</span><span class="sxs-lookup"><span data-stu-id="01da7-236">**Scripts**.</span></span> <span data-ttu-id="01da7-237">Повторно используемые сценарии, которые можно применить к каждому типу экземпляра (например, для инициализации и форматирования дополнительных дисков).</span><span class="sxs-lookup"><span data-stu-id="01da7-237">Widely reusable scripts are applicable for each instance type (for example, initialize and format additional disks).</span></span> <span data-ttu-id="01da7-238">Пользовательские скрипты, которые создаются для специальной настройки, отличаются для каждого типа экземпляра.</span><span class="sxs-lookup"><span data-stu-id="01da7-238">Custom scripts that you create for a specific customization purpose are different, based on the instance type.</span></span>

![Вложенный шаблон](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

<span data-ttu-id="01da7-240">Дополнительные сведения см. в статье [Использование связанных шаблонов при развертывании ресурсов Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="01da7-240">For more information, see [Use linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="conditionally-link-to-nested-templates"></a><span data-ttu-id="01da7-241">Условная связь с вложенным шаблоном</span><span class="sxs-lookup"><span data-stu-id="01da7-241">Conditionally link to nested templates</span></span>
<span data-ttu-id="01da7-242">Вы можете использовать параметр, чтобы установить условную связь с вложенными шаблонами.</span><span class="sxs-lookup"><span data-stu-id="01da7-242">You can use a parameter to conditionally link to nested templates.</span></span> <span data-ttu-id="01da7-243">Параметр становится частью универсального кода ресурса (URI) для шаблона:</span><span class="sxs-lookup"><span data-stu-id="01da7-243">The parameter becomes part of the URI for the template:</span></span>

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a><span data-ttu-id="01da7-244">Формат шаблона</span><span class="sxs-lookup"><span data-stu-id="01da7-244">Template format</span></span>
<span data-ttu-id="01da7-245">Рекомендуется обработать шаблон проверяющим элементом управления JSON,</span><span class="sxs-lookup"><span data-stu-id="01da7-245">It's a good practice to pass your template through a JSON validator.</span></span> <span data-ttu-id="01da7-246">чтобы удалить лишние запятые, скобки и квадратные скобки, которые могут привести к ошибке во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="01da7-246">A validator can help you remove extraneous commas, parentheses, and brackets that might cause an error during deployment.</span></span> <span data-ttu-id="01da7-247">Попробуйте [JSONlint](http://jsonlint.com/) или пакет linter для предпочитаемой среды редактирования (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="01da7-247">Try [JSONLint](http://jsonlint.com/) or a linter package for your favorite editing environment (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span></span>

<span data-ttu-id="01da7-248">Кроме того, рекомендуется отформатировать код JSON для повышения удобочитаемости.</span><span class="sxs-lookup"><span data-stu-id="01da7-248">It's also a good idea to format your JSON for better readability.</span></span> <span data-ttu-id="01da7-249">Вы можете использовать пакет модуля форматирования данных JSON для своего локального редактора.</span><span class="sxs-lookup"><span data-stu-id="01da7-249">You can use a JSON formatter package for your local editor.</span></span> <span data-ttu-id="01da7-250">В Visual Studio документ можно отформатировать, нажав клавиши **CTRL+K и CTRL+D**.</span><span class="sxs-lookup"><span data-stu-id="01da7-250">In Visual Studio, to format the document, press **Ctrl+K, Ctrl+D**.</span></span> <span data-ttu-id="01da7-251">В Visual Studio Code нажмите клавиши **ALT+SHIFT+F**.</span><span class="sxs-lookup"><span data-stu-id="01da7-251">In Visual Studio Code, press **Alt+Shift+F**.</span></span> <span data-ttu-id="01da7-252">Если ваш локальный редактор не может отформатировать документ, то можно использовать [модуль форматирования данных в Интернете](https://www.bing.com/search?q=json+formatter).</span><span class="sxs-lookup"><span data-stu-id="01da7-252">If your local editor doesn't format the document, you can use an [online formatter](https://www.bing.com/search?q=json+formatter).</span></span>

## <a name="next-steps"></a><span data-ttu-id="01da7-253">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="01da7-253">Next steps</span></span>
* <span data-ttu-id="01da7-254">Рекомендации по разработке архитектуры решения для виртуальных машин см. в статьях [Run a Windows VM on Azure](../guidance/guidance-compute-single-vm.md) (Запуск виртуальной машины Windows в Azure) и [Run a Linux VM on Azure](../guidance/guidance-compute-single-vm-linux.md) (Запуск виртуальной машины Linux в Azure).</span><span class="sxs-lookup"><span data-stu-id="01da7-254">For guidance on architecting your solution for virtual machines, see [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) and [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md).</span></span>
* <span data-ttu-id="01da7-255">Рекомендации по настройке учетной записи хранения см. в статье [Производительность хранилища Microsoft Azure и контрольный список масштабируемости](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="01da7-255">For guidance on setting up a storage account, see [Azure Storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>
* <span data-ttu-id="01da7-256">Сведения об использовании Resource Manager для эффективного управления подписками в организациях см. в статье [Корпоративный каркас Azure: рекомендуемая система управления подписками](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="01da7-256">To learn about how an enterprise can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold: Prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

