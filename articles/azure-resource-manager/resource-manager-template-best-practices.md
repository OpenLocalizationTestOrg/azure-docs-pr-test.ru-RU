---
title: "aaaBest и рекомендации по созданию шаблонов диспетчера ресурсов | Документы Microsoft"
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
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a><span data-ttu-id="63ae1-103">Рекомендации по созданию шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="63ae1-103">Best practices for creating Azure Resource Manager templates</span></span>
<span data-ttu-id="63ae1-104">Эти рекомендации помогут создать шаблоны Azure Resource Manager, надежное и легко toouse.</span><span class="sxs-lookup"><span data-stu-id="63ae1-104">These guidelines can help you create Azure Resource Manager templates that are reliable and easy toouse.</span></span> <span data-ttu-id="63ae1-105">Hello рекомендации предназначены только для примера.</span><span class="sxs-lookup"><span data-stu-id="63ae1-105">hello guidelines are only suggestions.</span></span> <span data-ttu-id="63ae1-106">не являются обязательными (если это явно не обозначено).</span><span class="sxs-lookup"><span data-stu-id="63ae1-106">They are not requirements, except where noted.</span></span> <span data-ttu-id="63ae1-107">Сценарий может потребоваться вариантом hello следующие подходы и примеры.</span><span class="sxs-lookup"><span data-stu-id="63ae1-107">Your scenario might require a variation of one of hello following approaches or examples.</span></span>

## <a name="resource-names"></a><span data-ttu-id="63ae1-108">Имена ресурсов</span><span class="sxs-lookup"><span data-stu-id="63ae1-108">Resource names</span></span>
<span data-ttu-id="63ae1-109">Обычно в Resource Manager вы работаете с именами ресурсов трех типов:</span><span class="sxs-lookup"><span data-stu-id="63ae1-109">Generally, you work with three types of resource names in Resource Manager:</span></span>

* <span data-ttu-id="63ae1-110">имена ресурсов, которые должны быть уникальными;</span><span class="sxs-lookup"><span data-stu-id="63ae1-110">Resource names that must be unique.</span></span>
* <span data-ttu-id="63ae1-111">Имена ресурсов, которые не требуется уникальный toobe, но выберите tooprovide имя, которое может помочь определить ресурс на основе контекста.</span><span class="sxs-lookup"><span data-stu-id="63ae1-111">Resource names that are not required toobe unique, but you choose tooprovide a name that can help you identify a resource based on context.</span></span>
* <span data-ttu-id="63ae1-112">имена ресурсов, которые могут быть универсальными.</span><span class="sxs-lookup"><span data-stu-id="63ae1-112">Resource names that can be generic.</span></span>

 <span data-ttu-id="63ae1-113">Сведения об ограничениях имен ресурсов см. в статье [Рекомендуемые соглашения об именовании для ресурсов Azure](../guidance/guidance-naming-conventions.md).</span><span class="sxs-lookup"><span data-stu-id="63ae1-113">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span></span>

### <a name="unique-resource-names"></a><span data-ttu-id="63ae1-114">Уникальные имена ресурсов</span><span class="sxs-lookup"><span data-stu-id="63ae1-114">Unique resource names</span></span>
<span data-ttu-id="63ae1-115">Необходимо указать уникальное имя для любого типа ресурса, который имеет конечную точку доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="63ae1-115">You must provide a unique resource name for any resource type that has a data access endpoint.</span></span> <span data-ttu-id="63ae1-116">Ниже приведено несколько распространенных типов ресурсов, для которых требуются уникальные имена:</span><span class="sxs-lookup"><span data-stu-id="63ae1-116">Some common resource types that require a unique name include:</span></span>

* <span data-ttu-id="63ae1-117">служба хранилища Azure<sup>1</sup>;</span><span class="sxs-lookup"><span data-stu-id="63ae1-117">Azure Storage<sup>1</sup></span></span> 
* <span data-ttu-id="63ae1-118">веб-приложения службы приложений Azure;</span><span class="sxs-lookup"><span data-stu-id="63ae1-118">Web Apps feature of Azure App Service</span></span>
* <span data-ttu-id="63ae1-119">SQL Server</span><span class="sxs-lookup"><span data-stu-id="63ae1-119">SQL Server</span></span>
* <span data-ttu-id="63ae1-120">Хранилище ключей Azure</span><span class="sxs-lookup"><span data-stu-id="63ae1-120">Azure Key Vault</span></span>
* <span data-ttu-id="63ae1-121">кэш Azure Redis</span><span class="sxs-lookup"><span data-stu-id="63ae1-121">Azure Redis Cache</span></span>
* <span data-ttu-id="63ae1-122">Пакетная служба Azure</span><span class="sxs-lookup"><span data-stu-id="63ae1-122">Azure Batch</span></span>
* <span data-ttu-id="63ae1-123">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="63ae1-123">Azure Traffic Manager</span></span>
* <span data-ttu-id="63ae1-124">поиск Azure;</span><span class="sxs-lookup"><span data-stu-id="63ae1-124">Azure Search</span></span>
* <span data-ttu-id="63ae1-125">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="63ae1-125">Azure HDInsight</span></span>

<span data-ttu-id="63ae1-126"><sup>1</sup> Имена учетных записей хранения также должны содержать до 24 знаков в нижнем регистре без дефисов.</span><span class="sxs-lookup"><span data-stu-id="63ae1-126"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span></span>

<span data-ttu-id="63ae1-127">При указании параметра имени ресурса, необходимо указать уникальное имя, при развертывании ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="63ae1-127">If you provide a parameter for a resource name, you must provide a unique name when you deploy hello resource.</span></span> <span data-ttu-id="63ae1-128">При необходимости можно создать переменную, которая использует hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) toogenerate имя функции.</span><span class="sxs-lookup"><span data-stu-id="63ae1-128">Optionally, you can create a variable that uses hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) function toogenerate a name.</span></span> 

<span data-ttu-id="63ae1-129">Необходимо также может собирать tooadd префикс или суффикс toohello **uniqueString** результат.</span><span class="sxs-lookup"><span data-stu-id="63ae1-129">You also might want tooadd a prefix or suffix toohello **uniqueString** result.</span></span> <span data-ttu-id="63ae1-130">Изменение hello уникальное имя может помочь более легко определить тип ресурса hello из имени hello.</span><span class="sxs-lookup"><span data-stu-id="63ae1-130">Modifying hello unique name can help you more easily identify hello resource type from hello name.</span></span> <span data-ttu-id="63ae1-131">Например можно создать уникальное имя для учетной записи хранилища с помощью следующих переменной hello:</span><span class="sxs-lookup"><span data-stu-id="63ae1-131">For example, you can generate a unique name for a storage account by using hello following variable:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a><span data-ttu-id="63ae1-132">Имена ресурсов для идентификации</span><span class="sxs-lookup"><span data-stu-id="63ae1-132">Resource names for identification</span></span>
<span data-ttu-id="63ae1-133">Некоторые типы ресурсов может потребоваться tooname, но их имена могут не toobe уникальным.</span><span class="sxs-lookup"><span data-stu-id="63ae1-133">Some resource types you might want tooname, but their names do not have toobe unique.</span></span> <span data-ttu-id="63ae1-134">Для этих типов ресурсов можно предоставить имя, которое определяет контекст ресурса hello и тип ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="63ae1-134">For these resource types, you can provide a name that identifies both hello resource context and hello resource type.</span></span> <span data-ttu-id="63ae1-135">Укажите описательное имя, которое помогает определить hello ресурс в список ресурсов.</span><span class="sxs-lookup"><span data-stu-id="63ae1-135">Provide a descriptive name that helps you identify hello resource in a list of resources.</span></span> <span data-ttu-id="63ae1-136">При необходимости toouse имя другого ресурса для различных развертываний можно использовать параметр для имени hello:</span><span class="sxs-lookup"><span data-stu-id="63ae1-136">If you need toouse a different resource name for different deployments, you can use a parameter for hello name:</span></span>

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

<span data-ttu-id="63ae1-137">Если во время развертывания toopass в имени не требуется, можно использовать переменную:</span><span class="sxs-lookup"><span data-stu-id="63ae1-137">If you do not need toopass in a name during deployment, you can use a variable:</span></span> 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

<span data-ttu-id="63ae1-138">Вы также можете использовать жестко заданное значение:</span><span class="sxs-lookup"><span data-stu-id="63ae1-138">You also can use a hard-coded value:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a><span data-ttu-id="63ae1-139">Универсальные имена ресурсов</span><span class="sxs-lookup"><span data-stu-id="63ae1-139">Generic resource names</span></span>
<span data-ttu-id="63ae1-140">Для типов ресурсов, которые обычно открываются другого ресурса можно использовать универсального имени, которое жестко запрограммированы в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="63ae1-140">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in hello template.</span></span> <span data-ttu-id="63ae1-141">Например, можно задать стандартное универсальное имя для правил брандмауэра на SQL Server:</span><span class="sxs-lookup"><span data-stu-id="63ae1-141">For example, you can set a standard, generic name for firewall rules on a SQL server:</span></span>

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a><span data-ttu-id="63ae1-142">Параметры</span><span class="sxs-lookup"><span data-stu-id="63ae1-142">Parameters</span></span>
<span data-ttu-id="63ae1-143">Hello следующие сведения могут оказаться полезными при работе с параметрами:</span><span class="sxs-lookup"><span data-stu-id="63ae1-143">hello following information can be helpful when you work with parameters:</span></span>

* <span data-ttu-id="63ae1-144">Используйте как можно меньше параметров.</span><span class="sxs-lookup"><span data-stu-id="63ae1-144">Minimize your use of parameters.</span></span> <span data-ttu-id="63ae1-145">По возможности используйте переменную или литеральное значение.</span><span class="sxs-lookup"><span data-stu-id="63ae1-145">Whenever possible, use a variable or a literal value.</span></span> <span data-ttu-id="63ae1-146">Используйте параметры только для следующих сценариев:</span><span class="sxs-lookup"><span data-stu-id="63ae1-146">Use parameters only for these scenarios:</span></span>
   
   * <span data-ttu-id="63ae1-147">Параметры, которые должны toouse различные виды tooenvironment (SKU, размер, емкость) в соответствии с.</span><span class="sxs-lookup"><span data-stu-id="63ae1-147">Settings that you want toouse variations of according tooenvironment (SKU, size, capacity).</span></span>
   * <span data-ttu-id="63ae1-148">Имена ресурсов, что требуется toospecify для упрощения идентификации.</span><span class="sxs-lookup"><span data-stu-id="63ae1-148">Resource names that you want toospecify for easy identification.</span></span>
   * <span data-ttu-id="63ae1-149">Значения, которые часто используются toocomplete других задач (например, имя пользователя администратора).</span><span class="sxs-lookup"><span data-stu-id="63ae1-149">Values that you use frequently toocomplete other tasks (such as an admin user name).</span></span>
   * <span data-ttu-id="63ae1-150">секреты (например, пароли);</span><span class="sxs-lookup"><span data-stu-id="63ae1-150">Secrets (such as passwords).</span></span>
   * <span data-ttu-id="63ae1-151">Номер Hello или массив значений toouse при создании нескольких экземпляров типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="63ae1-151">hello number or array of values toouse when you create multiple instances of a resource type.</span></span>
* <span data-ttu-id="63ae1-152">Имена для параметров необходимо указывать в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="63ae1-152">Use camel case for parameter names.</span></span>
* <span data-ttu-id="63ae1-153">Описание каждого параметра в hello метаданных:</span><span class="sxs-lookup"><span data-stu-id="63ae1-153">Provide a description of every parameter in hello metadata:</span></span>

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* <span data-ttu-id="63ae1-154">Определите значения по умолчанию для параметров (за исключением паролей и ключей SSH).</span><span class="sxs-lookup"><span data-stu-id="63ae1-154">Define default values for parameters (except for passwords and SSH keys):</span></span>
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* <span data-ttu-id="63ae1-155">Используйте **securestring** для всех паролей и секретов.</span><span class="sxs-lookup"><span data-stu-id="63ae1-155">Use **SecureString** for all passwords and secrets:</span></span> 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* <span data-ttu-id="63ae1-156">Когда это возможно, не используйте параметр toospecify расположение.</span><span class="sxs-lookup"><span data-stu-id="63ae1-156">Whenever possible, don't use a parameter toospecify location.</span></span> <span data-ttu-id="63ae1-157">Вместо этого используйте hello **расположение** свойства группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="63ae1-157">Instead, use hello **location** property of hello resource group.</span></span> <span data-ttu-id="63ae1-158">С помощью hello **.location () в группе ресурсов** выражение для всех ресурсов, ресурсы в шаблоне hello развертываются в hello местоположения hello группа ресурсов:</span><span class="sxs-lookup"><span data-stu-id="63ae1-158">By using hello **resourceGroup().location** expression for all your resources, resources in hello template are deployed in hello same location as hello resource group:</span></span>
   
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
   
   <span data-ttu-id="63ae1-159">Если тип ресурса поддерживается только ограниченное число расположений, может потребоваться toospecify допустимое расположение непосредственно в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="63ae1-159">If a resource type is supported in only a limited number of locations, you might want toospecify a valid location directly in hello template.</span></span> <span data-ttu-id="63ae1-160">Если необходимо использовать **расположение** параметра, совместно используют значение этого параметра максимальной с ресурсами, скорее всего, toobe в hello местоположения.</span><span class="sxs-lookup"><span data-stu-id="63ae1-160">If you must use a **location** parameter, share that parameter value as much as possible with resources that are likely toobe in hello same location.</span></span> <span data-ttu-id="63ae1-161">Это сводит к минимуму hello количество раз, когда пользователям предлагается tooprovide сведения о расположении.</span><span class="sxs-lookup"><span data-stu-id="63ae1-161">This minimizes hello number of times users are asked tooprovide location information.</span></span>
* <span data-ttu-id="63ae1-162">Избегайте использования параметра или переменной для hello версии API-интерфейса для типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="63ae1-162">Avoid using a parameter or variable for hello API version for a resource type.</span></span> <span data-ttu-id="63ae1-163">Свойства и значения ресурса могут отличаться для разных версий.</span><span class="sxs-lookup"><span data-stu-id="63ae1-163">Resource properties and values can vary by version number.</span></span> <span data-ttu-id="63ae1-164">IntelliSense в редакторе кода не может определить правильную схему hello при tooa параметра или переменной, задана версия API hello.</span><span class="sxs-lookup"><span data-stu-id="63ae1-164">IntelliSense in a code editor cannot determine hello correct schema when hello API version is set tooa parameter or variable.</span></span> <span data-ttu-id="63ae1-165">Вместо этого следует жестко кодировать hello версии API-интерфейса в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="63ae1-165">Instead, hard-code hello API version in hello template.</span></span>

## <a name="variables"></a><span data-ttu-id="63ae1-166">Переменные</span><span class="sxs-lookup"><span data-stu-id="63ae1-166">Variables</span></span>
<span data-ttu-id="63ae1-167">Hello следующие сведения могут оказаться полезными при работе с переменными:</span><span class="sxs-lookup"><span data-stu-id="63ae1-167">hello following information can be helpful when you work with variables:</span></span>

* <span data-ttu-id="63ae1-168">Используйте переменные для значений, необходимость toouse более одного раза в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="63ae1-168">Use variables for values that you need toouse more than once in a template.</span></span> <span data-ttu-id="63ae1-169">Если значение используется только один раз, жестко запрограммированных значений делает проще tooread ваш шаблон.</span><span class="sxs-lookup"><span data-stu-id="63ae1-169">If a value is used only once, a hard-coded value makes your template easier tooread.</span></span>
* <span data-ttu-id="63ae1-170">Нельзя использовать hello [ссылки](resource-group-template-functions-resource.md#reference) функции hello **переменных** раздел hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="63ae1-170">You cannot use hello [reference](resource-group-template-functions-resource.md#reference) function in hello **variables** section of hello template.</span></span> <span data-ttu-id="63ae1-171">Hello **ссылки** функции является производным свое значение из состояния среды выполнения hello ресурса.</span><span class="sxs-lookup"><span data-stu-id="63ae1-171">hello **reference** function derives its value from hello resource's runtime state.</span></span> <span data-ttu-id="63ae1-172">Однако переменные разрешаются во время начальной синтаксический анализ шаблона hello hello.</span><span class="sxs-lookup"><span data-stu-id="63ae1-172">However, variables are resolved during hello initial parsing of hello template.</span></span> <span data-ttu-id="63ae1-173">Создать значения, которые необходимо hello **ссылки** функции непосредственно в hello **ресурсов** или **выводит** раздел hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="63ae1-173">Construct values that need hello **reference** function directly in hello **resources** or **outputs** section of hello template.</span></span>
* <span data-ttu-id="63ae1-174">Добавьте переменные для имен ресурсов, которые должны быть уникальными, как описано в разделе [Имена ресурсов](#resource-names).</span><span class="sxs-lookup"><span data-stu-id="63ae1-174">Include variables for resource names that must be unique, as described in [Resource names](#resource-names).</span></span>
* <span data-ttu-id="63ae1-175">Переменные можно группировать в составные объекты.</span><span class="sxs-lookup"><span data-stu-id="63ae1-175">You can group variables into complex objects.</span></span> <span data-ttu-id="63ae1-176">Используйте hello **variable.subentry** формата tooreference значение из сложного объекта.</span><span class="sxs-lookup"><span data-stu-id="63ae1-176">Use hello **variable.subentry** format tooreference a value from a complex object.</span></span> <span data-ttu-id="63ae1-177">Группирование переменных помогает следить за связанными переменными</span><span class="sxs-lookup"><span data-stu-id="63ae1-177">Grouping variables can help you track related variables.</span></span> <span data-ttu-id="63ae1-178">Она также повышает удобочитаемость hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="63ae1-178">It also improves readability of hello template.</span></span> <span data-ttu-id="63ae1-179">Ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="63ae1-179">Here's an example:</span></span>
   
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
   > <span data-ttu-id="63ae1-180">Составной объект не может содержать выражение, которое ссылается на значение из составного объекта.</span><span class="sxs-lookup"><span data-stu-id="63ae1-180">A complex object cannot contain an expression that references a value from a complex object.</span></span> <span data-ttu-id="63ae1-181">Для этого определите отдельную переменную.</span><span class="sxs-lookup"><span data-stu-id="63ae1-181">Define a separate variable for this purpose.</span></span>
   > 
   > 
   
     <span data-ttu-id="63ae1-182">Расширенные примеры использования составных объектов в качестве переменных доступны в статье [Передача состояния в шаблоны Azure Resource Manager и из них](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="63ae1-182">For advanced examples of using complex objects as variables, see [Share state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="resources"></a><span data-ttu-id="63ae1-183">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="63ae1-183">Resources</span></span>
<span data-ttu-id="63ae1-184">Hello следующие сведения могут оказаться полезными при работе с ресурсами:</span><span class="sxs-lookup"><span data-stu-id="63ae1-184">hello following information can be helpful when you work with resources:</span></span>

* <span data-ttu-id="63ae1-185">toohelp других участников понимать назначение hello hello ресурса, укажите **комментарии** для каждого ресурса в шаблоне hello:</span><span class="sxs-lookup"><span data-stu-id="63ae1-185">toohelp other contributors understand hello purpose of hello resource, specify **comments** for each resource in hello template:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* <span data-ttu-id="63ae1-186">Можно использовать теги tooadd метаданные tooresources.</span><span class="sxs-lookup"><span data-stu-id="63ae1-186">You can use tags tooadd metadata tooresources.</span></span> <span data-ttu-id="63ae1-187">Используйте метаданные tooadd сведения о ресурсах.</span><span class="sxs-lookup"><span data-stu-id="63ae1-187">Use metadata tooadd information about your resources.</span></span> <span data-ttu-id="63ae1-188">Например можно добавить toorecord тарификация метаданные для ресурса.</span><span class="sxs-lookup"><span data-stu-id="63ae1-188">For example, you can add metadata toorecord billing details for a resource.</span></span> <span data-ttu-id="63ae1-189">Дополнительные сведения см. в разделе [использование теги tooorganize ресурсам Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="63ae1-189">For more information, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>
* <span data-ttu-id="63ae1-190">При использовании *общедоступную конечную точку* в шаблоне (например, больших двоичных объектов Azure хранилища общей конечной точки), *не следует жестко кодировать* hello пространства имен.</span><span class="sxs-lookup"><span data-stu-id="63ae1-190">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* hello namespace.</span></span> <span data-ttu-id="63ae1-191">Используйте hello **ссылки** функция toodynamically Получение имен hello.</span><span class="sxs-lookup"><span data-stu-id="63ae1-191">Use hello **reference** function toodynamically retrieve hello namespace.</span></span> <span data-ttu-id="63ae1-192">Можно использовать этот подход toodeploy hello шаблона toodifferent открытых пространствах имен без изменения конечной точки hello в шаблоне hello вручную.</span><span class="sxs-lookup"><span data-stu-id="63ae1-192">You can use this approach toodeploy hello template toodifferent public namespace environments without manually changing hello endpoint in hello template.</span></span> <span data-ttu-id="63ae1-193">Задать hello API версии toohello же версии, которая используется для учетной записи хранения hello в шаблоне:</span><span class="sxs-lookup"><span data-stu-id="63ae1-193">Set hello API version toohello same version that you are using for hello storage account in your template:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="63ae1-194">Если учетная запись хранения hello развернут в hello того же шаблона, который вы создаете, не требуется пространство имен поставщика hello toospecify при ссылке на ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="63ae1-194">If hello storage account is deployed in hello same template that you are creating, you do not need toospecify hello provider namespace when you reference hello resource.</span></span> <span data-ttu-id="63ae1-195">Это hello упрощенный синтаксис:</span><span class="sxs-lookup"><span data-stu-id="63ae1-195">This is hello simplified syntax:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="63ae1-196">Если у вас есть другие значения в шаблон, настроенный toouse имен public, измените значения этих tooreflect hello же **ссылки** функции.</span><span class="sxs-lookup"><span data-stu-id="63ae1-196">If you have other values in your template that are configured toouse a public namespace, change these values tooreflect hello same **reference** function.</span></span> <span data-ttu-id="63ae1-197">Например, можно задать hello **storageUri** свойство профиля диагностики hello виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="63ae1-197">For example, you can set hello **storageUri** property of hello virtual machine diagnostics profile:</span></span>
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   <span data-ttu-id="63ae1-198">Вы также можете использовать функцию reference для ссылки на учетную запись хранения в другой группе ресурсов:</span><span class="sxs-lookup"><span data-stu-id="63ae1-198">You also can reference an existing storage account that is in a different resource group:</span></span>

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* <span data-ttu-id="63ae1-199">Назначьте открытый IP адресов tooa виртуальную машину, только в том случае, если она требуется приложению.</span><span class="sxs-lookup"><span data-stu-id="63ae1-199">Assign public IP addresses tooa virtual machine only when an application requires it.</span></span> <span data-ttu-id="63ae1-200">tooconnect tooa виртуальной машины (VM) для отладки, или для управления или административных задач, используйте правила для входящих подключений NAT, шлюз виртуальной сети или jumpbox.</span><span class="sxs-lookup"><span data-stu-id="63ae1-200">tooconnect tooa virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span></span>
   
     <span data-ttu-id="63ae1-201">Дополнительные сведения о подключении toovirtual машин см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="63ae1-201">For more information about connecting toovirtual machines, see:</span></span>
   
   * <span data-ttu-id="63ae1-202">[Run Windows VMs for an N-tier application](../guidance/guidance-compute-n-tier-vm.md) (Запуск виртуальных машин Windows в n-уровневом приложении)</span><span class="sxs-lookup"><span data-stu-id="63ae1-202">[Run VMs for an N-tier architecture in Azure](../guidance/guidance-compute-n-tier-vm.md)</span></span>
   * [<span data-ttu-id="63ae1-203">Настройка доступа WinRM для виртуальных машин в Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="63ae1-203">Set up WinRM access for VMs in Azure Resource Manager</span></span>](../virtual-machines/windows/winrm.md)
   * [<span data-ttu-id="63ae1-204">Разрешить внешний доступ tooyour виртуальной Машины с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="63ae1-204">Allow external access tooyour VM by using hello Azure portal</span></span>](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [<span data-ttu-id="63ae1-205">Разрешить внешний доступ tooyour виртуальной Машины с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="63ae1-205">Allow external access tooyour VM by using PowerShell</span></span>](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [<span data-ttu-id="63ae1-206">Разрешить внешний доступ tooyour виртуальных Машин Linux с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="63ae1-206">Allow external access tooyour Linux VM by using Azure CLI</span></span>](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* <span data-ttu-id="63ae1-207">Hello **domainNameLabel** свойства для общих IP-адресов должны быть уникальными.</span><span class="sxs-lookup"><span data-stu-id="63ae1-207">hello **domainNameLabel** property for public IP addresses must be unique.</span></span> <span data-ttu-id="63ae1-208">Hello **domainNameLabel** значение должно находиться в диапазоне от 3 до 63 символов и выполните hello правил, заданных это регулярное выражение: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span><span class="sxs-lookup"><span data-stu-id="63ae1-208">hello **domainNameLabel** value must be between 3 and 63 characters long, and follow hello rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span></span> <span data-ttu-id="63ae1-209">Поскольку hello **uniqueString** функция создает строку, которая является 13 символов hello **dnsPrefixString** параметр является ограниченной too50 символов:</span><span class="sxs-lookup"><span data-stu-id="63ae1-209">Because hello **uniqueString** function generates a string that is 13 characters long, hello **dnsPrefixString** parameter is limited too50 characters:</span></span>

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* <span data-ttu-id="63ae1-210">При добавлении расширение пользовательского скрипта tooa пароля используйте hello **commandToExecute** свойство в hello **protectedSettings** свойства:</span><span class="sxs-lookup"><span data-stu-id="63ae1-210">When you add a password tooa custom script extension, use hello **commandToExecute** property in hello **protectedSettings** property:</span></span>
   
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
   > <span data-ttu-id="63ae1-211">tooensure, секреты представляют шифруется при передаче в качестве параметров tooVMs и расширения, используйте hello **protectedSettings** свойство применимо расширений hello.</span><span class="sxs-lookup"><span data-stu-id="63ae1-211">tooensure that secrets are encrypted when they are passed as parameters tooVMs and extensions, use hello **protectedSettings** property of hello relevant extensions.</span></span>
   > 
   > 

## <a name="outputs"></a><span data-ttu-id="63ae1-212">outputs</span><span class="sxs-lookup"><span data-stu-id="63ae1-212">Outputs</span></span>
<span data-ttu-id="63ae1-213">При использовании шаблона toocreate общих IP-адресов, включите **выводит** раздел, в котором для извлечения сведений о hello IP-адрес и hello полное доменное имя (FQDN).</span><span class="sxs-lookup"><span data-stu-id="63ae1-213">If you use a template toocreate public IP addresses, include an **outputs** section that returns details of hello IP address and hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="63ae1-214">После развертывания можно использовать выходные данные значения tooeasily извлечь подробности открытый IP-адреса и полные доменные имена.</span><span class="sxs-lookup"><span data-stu-id="63ae1-214">You can use output values tooeasily retrieve details about public IP addresses and FQDNs after deployment.</span></span> <span data-ttu-id="63ae1-215">При ссылке на ресурс hello, использовать версию hello API, которое вы использовали toocreate его:</span><span class="sxs-lookup"><span data-stu-id="63ae1-215">When you reference hello resource, use hello API version that you used toocreate it:</span></span> 

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

## <a name="single-template-vs-nested-templates"></a><span data-ttu-id="63ae1-216">Отдельный шаблон и вложенные шаблоны</span><span class="sxs-lookup"><span data-stu-id="63ae1-216">Single template vs. nested templates</span></span>
<span data-ttu-id="63ae1-217">toodeploy решение, можно использовать один шаблон или основного шаблона с несколькими шаблонами вложенных.</span><span class="sxs-lookup"><span data-stu-id="63ae1-217">toodeploy your solution, you can use either a single template or a main template with multiple nested templates.</span></span> <span data-ttu-id="63ae1-218">Вложенные шаблоны обычно используются для более сложных сценариев.</span><span class="sxs-lookup"><span data-stu-id="63ae1-218">Nested templates are common for more advanced scenarios.</span></span> <span data-ttu-id="63ae1-219">С помощью вложенных шаблонов дает, hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="63ae1-219">Using a nested template gives you hello following advantages:</span></span>

* <span data-ttu-id="63ae1-220">вы можете разбить решение на целевые компоненты;</span><span class="sxs-lookup"><span data-stu-id="63ae1-220">You can break down a solution into targeted components.</span></span>
* <span data-ttu-id="63ae1-221">вложенные шаблоны можно повторно использовать в разных основных шаблонах.</span><span class="sxs-lookup"><span data-stu-id="63ae1-221">You can reuse nested templates with different main templates.</span></span>

<span data-ttu-id="63ae1-222">При выборе toouse вложенные шаблоны hello, следование правилам может помочь стандартизировать макет шаблона.</span><span class="sxs-lookup"><span data-stu-id="63ae1-222">If you choose toouse nested templates, hello following guidelines can help you standardize your template design.</span></span> <span data-ttu-id="63ae1-223">Эти рекомендации основаны на статье [Приемы разработки шаблонов Azure Resource Manager при развертывании сложных решений](best-practices-resource-manager-design-templates.md).</span><span class="sxs-lookup"><span data-stu-id="63ae1-223">These guidelines are based on [patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="63ae1-224">Рекомендуется разработать проект, который имеет hello следующие шаблоны:</span><span class="sxs-lookup"><span data-stu-id="63ae1-224">We recommend a design that has hello following templates:</span></span>

* <span data-ttu-id="63ae1-225">**Основной шаблон** (azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="63ae1-225">**Main template** (azuredeploy.json).</span></span> <span data-ttu-id="63ae1-226">Используйте для hello входных параметров.</span><span class="sxs-lookup"><span data-stu-id="63ae1-226">Use for hello input parameters.</span></span>
* <span data-ttu-id="63ae1-227">**Шаблон общих ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="63ae1-227">**Shared resources template**.</span></span> <span data-ttu-id="63ae1-228">Используйте toodeploy общих ресурсов, использующих другие ресурсы (например, виртуальной сети и доступность наборов).</span><span class="sxs-lookup"><span data-stu-id="63ae1-228">Use toodeploy shared resources that all other resources use (for example, virtual network and availability sets).</span></span> <span data-ttu-id="63ae1-229">Используйте hello **dependsOn** tooensure выражения, что шаблон будет развернут перед другими шаблонами.</span><span class="sxs-lookup"><span data-stu-id="63ae1-229">Use hello **dependsOn** expression tooensure that this template is deployed before other templates.</span></span>
* <span data-ttu-id="63ae1-230">**Шаблон дополнительных ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="63ae1-230">**Optional resources template**.</span></span> <span data-ttu-id="63ae1-231">Используйте tooconditionally развертывания ресурсов на основе параметра (например, jumpbox).</span><span class="sxs-lookup"><span data-stu-id="63ae1-231">Use tooconditionally deploy resources based on a parameter (for example, a jumpbox).</span></span>
* <span data-ttu-id="63ae1-232">**Шаблон элемента ресурсов.**</span><span class="sxs-lookup"><span data-stu-id="63ae1-232">**Member resources template**.</span></span> <span data-ttu-id="63ae1-233">У каждого типа экземпляра в пределах уровня приложения есть собственная конфигурация.</span><span class="sxs-lookup"><span data-stu-id="63ae1-233">Each instance type within an application tier has its own configuration.</span></span> <span data-ttu-id="63ae1-234">В пределах уровня можно определить разные типы экземпляров.</span><span class="sxs-lookup"><span data-stu-id="63ae1-234">Within a tier, you can define different instance types.</span></span> <span data-ttu-id="63ae1-235">(Например, hello первый экземпляр создает кластер, а дополнительные экземпляры будут добавлены toohello существующего кластера.) У каждого типа экземпляра есть собственный шаблон развертывания.</span><span class="sxs-lookup"><span data-stu-id="63ae1-235">(For example, hello first instance creates a cluster, and additional instances are added toohello existing cluster.) Each instance type has its own deployment template.</span></span>
* <span data-ttu-id="63ae1-236">**Сценарии**.</span><span class="sxs-lookup"><span data-stu-id="63ae1-236">**Scripts**.</span></span> <span data-ttu-id="63ae1-237">Повторно используемые сценарии, которые можно применить к каждому типу экземпляра (например, для инициализации и форматирования дополнительных дисков).</span><span class="sxs-lookup"><span data-stu-id="63ae1-237">Widely reusable scripts are applicable for each instance type (for example, initialize and format additional disks).</span></span> <span data-ttu-id="63ae1-238">Пользовательские сценарии, создаваемые в целях, определенные настройки отличаются, на основе типа экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="63ae1-238">Custom scripts that you create for a specific customization purpose are different, based on hello instance type.</span></span>

![Вложенный шаблон](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

<span data-ttu-id="63ae1-240">Дополнительные сведения см. в статье [Использование связанных шаблонов при развертывании ресурсов Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="63ae1-240">For more information, see [Use linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="conditionally-link-toonested-templates"></a><span data-ttu-id="63ae1-241">Условно связать toonested шаблонов</span><span class="sxs-lookup"><span data-stu-id="63ae1-241">Conditionally link toonested templates</span></span>
<span data-ttu-id="63ae1-242">Можно использовать параметр tooconditionally ссылку toonested шаблонов.</span><span class="sxs-lookup"><span data-stu-id="63ae1-242">You can use a parameter tooconditionally link toonested templates.</span></span> <span data-ttu-id="63ae1-243">параметр Hello становится частью hello URI для hello шаблона:</span><span class="sxs-lookup"><span data-stu-id="63ae1-243">hello parameter becomes part of hello URI for hello template:</span></span>

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

## <a name="template-format"></a><span data-ttu-id="63ae1-244">Формат шаблона</span><span class="sxs-lookup"><span data-stu-id="63ae1-244">Template format</span></span>
<span data-ttu-id="63ae1-245">Это toopass хорошей практикой шаблон через проверяющем элементе управления JSON.</span><span class="sxs-lookup"><span data-stu-id="63ae1-245">It's a good practice toopass your template through a JSON validator.</span></span> <span data-ttu-id="63ae1-246">чтобы удалить лишние запятые, скобки и квадратные скобки, которые могут привести к ошибке во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="63ae1-246">A validator can help you remove extraneous commas, parentheses, and brackets that might cause an error during deployment.</span></span> <span data-ttu-id="63ae1-247">Попробуйте [JSONlint](http://jsonlint.com/) или пакет linter для предпочитаемой среды редактирования (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="63ae1-247">Try [JSONLint](http://jsonlint.com/) or a linter package for your favorite editing environment (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span></span>

<span data-ttu-id="63ae1-248">Это также tooformat хорошее представление JSON для повышения удобочитаемости.</span><span class="sxs-lookup"><span data-stu-id="63ae1-248">It's also a good idea tooformat your JSON for better readability.</span></span> <span data-ttu-id="63ae1-249">Вы можете использовать пакет модуля форматирования данных JSON для своего локального редактора.</span><span class="sxs-lookup"><span data-stu-id="63ae1-249">You can use a JSON formatter package for your local editor.</span></span> <span data-ttu-id="63ae1-250">В Visual Studio, tooformat hello документа, нажмите клавишу **Ctrl + K, Ctrl + D**.</span><span class="sxs-lookup"><span data-stu-id="63ae1-250">In Visual Studio, tooformat hello document, press **Ctrl+K, Ctrl+D**.</span></span> <span data-ttu-id="63ae1-251">В Visual Studio Code нажмите клавиши **ALT+SHIFT+F**.</span><span class="sxs-lookup"><span data-stu-id="63ae1-251">In Visual Studio Code, press **Alt+Shift+F**.</span></span> <span data-ttu-id="63ae1-252">Если ваш локальный редактор не форматировать документ hello, можно использовать [online форматирования](https://www.bing.com/search?q=json+formatter).</span><span class="sxs-lookup"><span data-stu-id="63ae1-252">If your local editor doesn't format hello document, you can use an [online formatter](https://www.bing.com/search?q=json+formatter).</span></span>

## <a name="next-steps"></a><span data-ttu-id="63ae1-253">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="63ae1-253">Next steps</span></span>
* <span data-ttu-id="63ae1-254">Рекомендации по разработке архитектуры решения для виртуальных машин см. в статьях [Run a Windows VM on Azure](../guidance/guidance-compute-single-vm.md) (Запуск виртуальной машины Windows в Azure) и [Run a Linux VM on Azure](../guidance/guidance-compute-single-vm-linux.md) (Запуск виртуальной машины Linux в Azure).</span><span class="sxs-lookup"><span data-stu-id="63ae1-254">For guidance on architecting your solution for virtual machines, see [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) and [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md).</span></span>
* <span data-ttu-id="63ae1-255">Рекомендации по настройке учетной записи хранения см. в статье [Производительность хранилища Microsoft Azure и контрольный список масштабируемости](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="63ae1-255">For guidance on setting up a storage account, see [Azure Storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>
* <span data-ttu-id="63ae1-256">toolearn об использовании диспетчера ресурсов tooeffectively предприятия управление подписками см. в разделе [формирования шаблонов Azure enterprise: управление конкретные подписки](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="63ae1-256">toolearn about how an enterprise can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold: Prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

