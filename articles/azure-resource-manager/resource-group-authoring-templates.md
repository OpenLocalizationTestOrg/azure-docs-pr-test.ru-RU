---
title: "Диспетчер ресурсов aaaAzure шаблона структуре и синтаксисе | Документы Microsoft"
description: "Описывает структуру hello и свойства с помощью декларативного синтаксиса JSON шаблонов диспетчера ресурсов Azure."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="b64eb-103">Описание структуры hello и синтаксис шаблонов диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="b64eb-103">Understand hello structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="b64eb-104">В этом разделе описывается структура hello шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="b64eb-104">This topic describes hello structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="b64eb-105">Представляет различные разделы шаблона и hello свойства, которые доступны в этих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-105">It presents hello different sections of a template and hello properties that are available in those sections.</span></span> <span data-ttu-id="b64eb-106">шаблон Hello состоит из выражения, что tooconstruct значения можно использовать для развертывания и JSON.</span><span class="sxs-lookup"><span data-stu-id="b64eb-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="b64eb-107">Пошаговое руководство по созданию шаблона приведено в разделе [Создание первого шаблона Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="b64eb-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="b64eb-108">Формат шаблона</span><span class="sxs-lookup"><span data-stu-id="b64eb-108">Template format</span></span>
<span data-ttu-id="b64eb-109">В его Простейшая структура шаблона содержит hello следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="b64eb-109">In its simplest structure, a template contains hello following elements:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| <span data-ttu-id="b64eb-110">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="b64eb-110">Element name</span></span> | <span data-ttu-id="b64eb-111">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b64eb-111">Required</span></span> | <span data-ttu-id="b64eb-112">Описание</span><span class="sxs-lookup"><span data-stu-id="b64eb-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b64eb-113">$schema</span><span class="sxs-lookup"><span data-stu-id="b64eb-113">$schema</span></span> |<span data-ttu-id="b64eb-114">Да</span><span class="sxs-lookup"><span data-stu-id="b64eb-114">Yes</span></span> |<span data-ttu-id="b64eb-115">Расположение файла схемы JSON hello, описывающего версию hello hello шаблона языка.</span><span class="sxs-lookup"><span data-stu-id="b64eb-115">Location of hello JSON schema file that describes hello version of hello template language.</span></span> <span data-ttu-id="b64eb-116">Используйте hello URL-адрес, показанный на предшествующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-116">Use hello URL shown in hello preceding example.</span></span> |
| <span data-ttu-id="b64eb-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="b64eb-117">contentVersion</span></span> |<span data-ttu-id="b64eb-118">Да</span><span class="sxs-lookup"><span data-stu-id="b64eb-118">Yes</span></span> |<span data-ttu-id="b64eb-119">Версия шаблона hello (например, 1.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="b64eb-119">Version of hello template (such as 1.0.0.0).</span></span> <span data-ttu-id="b64eb-120">Для этого элемента можно предоставить любое значение.</span><span class="sxs-lookup"><span data-stu-id="b64eb-120">You can provide any value for this element.</span></span> <span data-ttu-id="b64eb-121">При развертывании ресурсов с помощью шаблона hello, это значение может быть используется toomake в том, что используется правильный шаблон, hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-121">When deploying resources using hello template, this value can be used toomake sure that hello right template is being used.</span></span> |
| <span data-ttu-id="b64eb-122">parameters</span><span class="sxs-lookup"><span data-stu-id="b64eb-122">parameters</span></span> |<span data-ttu-id="b64eb-123">Нет</span><span class="sxs-lookup"><span data-stu-id="b64eb-123">No</span></span> |<span data-ttu-id="b64eb-124">Значения, которые предоставляются при развертывании выполняются toocustomize развертывания ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b64eb-124">Values that are provided when deployment is executed toocustomize resource deployment.</span></span> |
| <span data-ttu-id="b64eb-125">variables</span><span class="sxs-lookup"><span data-stu-id="b64eb-125">variables</span></span> |<span data-ttu-id="b64eb-126">Нет</span><span class="sxs-lookup"><span data-stu-id="b64eb-126">No</span></span> |<span data-ttu-id="b64eb-127">Значения, которые используются в качестве фрагментов JSON в выражениях языка шаблона toosimplify шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-127">Values that are used as JSON fragments in hello template toosimplify template language expressions.</span></span> |
| <span data-ttu-id="b64eb-128">ресурсов</span><span class="sxs-lookup"><span data-stu-id="b64eb-128">resources</span></span> |<span data-ttu-id="b64eb-129">Да</span><span class="sxs-lookup"><span data-stu-id="b64eb-129">Yes</span></span> |<span data-ttu-id="b64eb-130">Типы ресурсов, которые развертываются или обновляются в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b64eb-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="b64eb-131">outputs</span><span class="sxs-lookup"><span data-stu-id="b64eb-131">outputs</span></span> |<span data-ttu-id="b64eb-132">Нет</span><span class="sxs-lookup"><span data-stu-id="b64eb-132">No</span></span> |<span data-ttu-id="b64eb-133">Значения, возвращаемые после развертывания.</span><span class="sxs-lookup"><span data-stu-id="b64eb-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="b64eb-134">Каждый элемент содержит свойства, которые можно задать.</span><span class="sxs-lookup"><span data-stu-id="b64eb-134">Each element contains properties you can set.</span></span> <span data-ttu-id="b64eb-135">Следующий пример Hello содержит hello полный синтаксис для шаблона:</span><span class="sxs-lookup"><span data-stu-id="b64eb-135">hello following example contains hello full syntax for a template:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-hello parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

<span data-ttu-id="b64eb-136">Мы изучаем hello разделах шаблона hello более подробно далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="b64eb-136">We examine hello sections of hello template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="b64eb-137">Выражения и функции</span><span class="sxs-lookup"><span data-stu-id="b64eb-137">Expressions and functions</span></span>
<span data-ttu-id="b64eb-138">Базовый синтаксис Hello hello шаблона является JSON.</span><span class="sxs-lookup"><span data-stu-id="b64eb-138">hello basic syntax of hello template is JSON.</span></span> <span data-ttu-id="b64eb-139">Однако выражения и функции расширить значений JSON hello, доступных в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-139">However, expressions and functions extend hello JSON values available within hello template.</span></span>  <span data-ttu-id="b64eb-140">Выражения записываются с помощью JSON строковые литералы, первого и последние символы являются скобкой hello: `[` и `]`соответственно.</span><span class="sxs-lookup"><span data-stu-id="b64eb-140">Expressions are written within JSON string literals whose first and last characters are hello brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="b64eb-141">значение Hello hello выражения вычисляется при развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-141">hello value of hello expression is evaluated when hello template is deployed.</span></span> <span data-ttu-id="b64eb-142">Во время записи как строковый литерал hello результат вычисления выражения hello может быть другого типа JSON, например массиву или целое число, в зависимости от фактического выражение hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-142">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array or integer, depending on hello actual expression.</span></span>  <span data-ttu-id="b64eb-143">строковый литерал запустить скобкой toohave `[`, без его интерпретируются как выражения, добавляется строка hello toostart дополнительную квадратную скобку с `[[`.</span><span class="sxs-lookup"><span data-stu-id="b64eb-143">toohave a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket toostart hello string with `[[`.</span></span>

<span data-ttu-id="b64eb-144">Как правило используются выражения с помощью функции tooperform операций для настройки развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-144">Typically, you use expressions with functions tooperform operations for configuring hello deployment.</span></span> <span data-ttu-id="b64eb-145">Как и в языке JavaScript, вызовы функций форматируются так: `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="b64eb-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="b64eb-146">Ссылки на свойства с помощью операторов [index] и точками hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-146">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="b64eb-147">Hello в следующем примере показано, как toouse, некоторые функции при создании значения:</span><span class="sxs-lookup"><span data-stu-id="b64eb-147">hello following example shows how toouse several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="b64eb-148">Hello полный список функций шаблонов см. в разделе [функции шаблона Azure Resource Manager](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="b64eb-148">For hello full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="b64eb-149">Параметры</span><span class="sxs-lookup"><span data-stu-id="b64eb-149">Parameters</span></span>
<span data-ttu-id="b64eb-150">В разделе параметров hello шаблона hello укажите значения, которые можно ввести при развертывании hello ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b64eb-150">In hello parameters section of hello template, you specify which values you can input when deploying hello resources.</span></span> <span data-ttu-id="b64eb-151">Значения этих параметров включить toocustomize hello развертывания, предоставляя значения, которые предназначены для определенной среде (например, разработки, тестирования и эксплуатации).</span><span class="sxs-lookup"><span data-stu-id="b64eb-151">These parameter values enable you toocustomize hello deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="b64eb-152">У вас tooprovide параметры в шаблоне, но без параметров ваш шаблон будет всегда следует развертывать hello и те же ресурсы с hello одинаковые имена, расположения и свойства.</span><span class="sxs-lookup"><span data-stu-id="b64eb-152">You do not have tooprovide parameters in your template, but without parameters your template would always deploy hello same resources with hello same names, locations, and properties.</span></span>

<span data-ttu-id="b64eb-153">Определить параметры с hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="b64eb-153">You define parameters with hello following structure:</span></span>

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| <span data-ttu-id="b64eb-154">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="b64eb-154">Element name</span></span> | <span data-ttu-id="b64eb-155">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b64eb-155">Required</span></span> | <span data-ttu-id="b64eb-156">Описание</span><span class="sxs-lookup"><span data-stu-id="b64eb-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b64eb-157">имя_параметра</span><span class="sxs-lookup"><span data-stu-id="b64eb-157">parameterName</span></span> |<span data-ttu-id="b64eb-158">Да</span><span class="sxs-lookup"><span data-stu-id="b64eb-158">Yes</span></span> |<span data-ttu-id="b64eb-159">Имя параметра hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-159">Name of hello parameter.</span></span> <span data-ttu-id="b64eb-160">Должно быть допустимым идентификатором JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b64eb-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="b64eb-161">type</span><span class="sxs-lookup"><span data-stu-id="b64eb-161">type</span></span> |<span data-ttu-id="b64eb-162">Да</span><span class="sxs-lookup"><span data-stu-id="b64eb-162">Yes</span></span> |<span data-ttu-id="b64eb-163">Тип значения параметра hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-163">Type of hello parameter value.</span></span> <span data-ttu-id="b64eb-164">После этой таблицы. в разделе hello списка разрешенных типов.</span><span class="sxs-lookup"><span data-stu-id="b64eb-164">See hello list of allowed types after this table.</span></span> |
| <span data-ttu-id="b64eb-165">defaultValue</span><span class="sxs-lookup"><span data-stu-id="b64eb-165">defaultValue</span></span> |<span data-ttu-id="b64eb-166">Нет</span><span class="sxs-lookup"><span data-stu-id="b64eb-166">No</span></span> |<span data-ttu-id="b64eb-167">Значение по умолчанию для параметра hello, если значение не указано для параметра hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-167">Default value for hello parameter, if no value is provided for hello parameter.</span></span> |
| <span data-ttu-id="b64eb-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="b64eb-168">allowedValues</span></span> |<span data-ttu-id="b64eb-169">Нет</span><span class="sxs-lookup"><span data-stu-id="b64eb-169">No</span></span> |<span data-ttu-id="b64eb-170">Массив допустимых значений для hello параметр toomake материалы hello правильного значения.</span><span class="sxs-lookup"><span data-stu-id="b64eb-170">Array of allowed values for hello parameter toomake sure that hello right value is provided.</span></span> |
| <span data-ttu-id="b64eb-171">minValue</span><span class="sxs-lookup"><span data-stu-id="b64eb-171">minValue</span></span> |<span data-ttu-id="b64eb-172">Нет</span><span class="sxs-lookup"><span data-stu-id="b64eb-172">No</span></span> |<span data-ttu-id="b64eb-173">Hello минимальное значение для параметров типа int, это значение является включительно.</span><span class="sxs-lookup"><span data-stu-id="b64eb-173">hello minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="b64eb-174">maxValue</span><span class="sxs-lookup"><span data-stu-id="b64eb-174">maxValue</span></span> |<span data-ttu-id="b64eb-175">Нет</span><span class="sxs-lookup"><span data-stu-id="b64eb-175">No</span></span> |<span data-ttu-id="b64eb-176">Hello максимальное значение для параметров типа int, это значение равно включительно.</span><span class="sxs-lookup"><span data-stu-id="b64eb-176">hello maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="b64eb-177">minLength</span><span class="sxs-lookup"><span data-stu-id="b64eb-177">minLength</span></span> |<span data-ttu-id="b64eb-178">Нет</span><span class="sxs-lookup"><span data-stu-id="b64eb-178">No</span></span> |<span data-ttu-id="b64eb-179">Hello минимальную длину строки, secureString и параметры типа массива, это значение является включительно.</span><span class="sxs-lookup"><span data-stu-id="b64eb-179">hello minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="b64eb-180">maxLength</span><span class="sxs-lookup"><span data-stu-id="b64eb-180">maxLength</span></span> |<span data-ttu-id="b64eb-181">Нет</span><span class="sxs-lookup"><span data-stu-id="b64eb-181">No</span></span> |<span data-ttu-id="b64eb-182">Hello Максимальная длина строки secureString и параметры типа массива, это значение является включительно.</span><span class="sxs-lookup"><span data-stu-id="b64eb-182">hello maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="b64eb-183">Описание</span><span class="sxs-lookup"><span data-stu-id="b64eb-183">description</span></span> |<span data-ttu-id="b64eb-184">Нет</span><span class="sxs-lookup"><span data-stu-id="b64eb-184">No</span></span> |<span data-ttu-id="b64eb-185">Описание параметра hello, отображаться toousers через портал hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-185">Description of hello parameter that is displayed toousers through hello portal.</span></span> |

<span data-ttu-id="b64eb-186">Hello допустимые типы и значения являются:</span><span class="sxs-lookup"><span data-stu-id="b64eb-186">hello allowed types and values are:</span></span>

* <span data-ttu-id="b64eb-187">**string**</span><span class="sxs-lookup"><span data-stu-id="b64eb-187">**string**</span></span>
* <span data-ttu-id="b64eb-188">**secureString**;</span><span class="sxs-lookup"><span data-stu-id="b64eb-188">**secureString**</span></span>
* <span data-ttu-id="b64eb-189">**int**</span><span class="sxs-lookup"><span data-stu-id="b64eb-189">**int**</span></span>
* <span data-ttu-id="b64eb-190">**bool**;</span><span class="sxs-lookup"><span data-stu-id="b64eb-190">**bool**</span></span>
* <span data-ttu-id="b64eb-191">**object**;</span><span class="sxs-lookup"><span data-stu-id="b64eb-191">**object**</span></span> 
* <span data-ttu-id="b64eb-192">**secureObject**;</span><span class="sxs-lookup"><span data-stu-id="b64eb-192">**secureObject**</span></span>
* <span data-ttu-id="b64eb-193">**array**.</span><span class="sxs-lookup"><span data-stu-id="b64eb-193">**array**</span></span>

<span data-ttu-id="b64eb-194">toospecify параметр как необязательный, укажите значение по умолчанию (может быть пустой строкой).</span><span class="sxs-lookup"><span data-stu-id="b64eb-194">toospecify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="b64eb-195">При указании имени параметра в шаблон, соответствующий параметр в шаблон hello toodeploy hello команды нет возможной неоднозначности о заданные значения hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-195">If you specify a parameter name in your template that matches a parameter in hello command toodeploy hello template, there is potential ambiguity about hello values you provide.</span></span> <span data-ttu-id="b64eb-196">Диспетчер ресурсов устраняет этой путаницы, добавив постфиксная hello **FromTemplate** toohello параметр шаблона.</span><span class="sxs-lookup"><span data-stu-id="b64eb-196">Resource Manager resolves this confusion by adding hello postfix **FromTemplate** toohello template parameter.</span></span> <span data-ttu-id="b64eb-197">Например, если включить параметр с именем **ResourceGroupName** в шаблоне, это противоречит hello **ResourceGroupName** параметр в hello [ Новый AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) командлета.</span><span class="sxs-lookup"><span data-stu-id="b64eb-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="b64eb-198">Во время развертывания, вы являетесь запрашиваемые tooprovide значение **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="b64eb-198">During deployment, you are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="b64eb-199">В общем случае следует избегать этой путаницы, не присвоив имена параметров с hello точно такое же имя в качестве параметров, используемых для операций развертывания.</span><span class="sxs-lookup"><span data-stu-id="b64eb-199">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="b64eb-200">Все пароли, ключи и другие секретные данные следует использовать hello **secureString** типа.</span><span class="sxs-lookup"><span data-stu-id="b64eb-200">All passwords, keys, and other secrets should use hello **secureString** type.</span></span> <span data-ttu-id="b64eb-201">При передаче конфиденциальных данных в объект JSON, следует использовать hello **secureObject** типа.</span><span class="sxs-lookup"><span data-stu-id="b64eb-201">If you pass sensitive data in a JSON object, use hello **secureObject** type.</span></span> <span data-ttu-id="b64eb-202">Параметры шаблона с типами secureString и secureObject невозможно прочитать после развертывания ресурса.</span><span class="sxs-lookup"><span data-stu-id="b64eb-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="b64eb-203">Например hello следующую запись в журнале развертывания hello показывает значение hello для string и object, но не для secureString и secureObject.</span><span class="sxs-lookup"><span data-stu-id="b64eb-203">For example, hello following entry in hello deployment history shows hello value for a string and object but not for secureString and secureObject.</span></span>
>
> ![показать значения развертывания](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="b64eb-205">Следующий пример показывает как Hello toodefine параметры:</span><span class="sxs-lookup"><span data-stu-id="b64eb-205">hello following example shows how toodefine parameters:</span></span>

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

<span data-ttu-id="b64eb-206">Как значения параметров tooinput hello, во время развертывания, в разделе [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b64eb-206">For how tooinput hello parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="b64eb-207">Переменные</span><span class="sxs-lookup"><span data-stu-id="b64eb-207">Variables</span></span>
<span data-ttu-id="b64eb-208">В разделе "переменные" hello создания значений, которые могут использоваться в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="b64eb-208">In hello variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="b64eb-209">Переменные toodefine не обязательно, но они часто упростить шаблон за счет уменьшения сложных выражений.</span><span class="sxs-lookup"><span data-stu-id="b64eb-209">You do not need toodefine variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="b64eb-210">Определите переменные с hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="b64eb-210">You define variables with hello following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="b64eb-211">Следующий пример показывает как Hello toodefine переменную, которая создается из значений двух параметров:</span><span class="sxs-lookup"><span data-stu-id="b64eb-211">hello following example shows how toodefine a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="b64eb-212">Hello далее пример переменной, которая является сложным типом, JSON и переменные, которые созданы из других переменных.</span><span class="sxs-lookup"><span data-stu-id="b64eb-212">hello next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a><span data-ttu-id="b64eb-213">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="b64eb-213">Resources</span></span>
<span data-ttu-id="b64eb-214">В разделе "ресурсы" hello необходимо указать hello ресурсы, которые будут развертываться или обновляться.</span><span class="sxs-lookup"><span data-stu-id="b64eb-214">In hello resources section, you define hello resources that are deployed or updated.</span></span> <span data-ttu-id="b64eb-215">В этом разделе может усложняться так, как необходимо понимать типы hello вы развертываете tooprovide hello правильные значения.</span><span class="sxs-lookup"><span data-stu-id="b64eb-215">This section can get complicated because you must understand hello types you are deploying tooprovide hello right values.</span></span> <span data-ttu-id="b64eb-216">Hello ресурсом значения (apiVersion, тип и свойства), необходимо tooset см [определения ресурсов в шаблоны Azure Resource Manager](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="b64eb-216">For hello resource-specific values (apiVersion, type, and properties) that you need tooset, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="b64eb-217">Определить ресурсы с hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="b64eb-217">You define resources with hello following structure:</span></span>

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| <span data-ttu-id="b64eb-218">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="b64eb-218">Element name</span></span> | <span data-ttu-id="b64eb-219">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b64eb-219">Required</span></span> | <span data-ttu-id="b64eb-220">Описание</span><span class="sxs-lookup"><span data-stu-id="b64eb-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b64eb-221">condition</span><span class="sxs-lookup"><span data-stu-id="b64eb-221">condition</span></span> | <span data-ttu-id="b64eb-222">Нет</span><span class="sxs-lookup"><span data-stu-id="b64eb-222">No</span></span> | <span data-ttu-id="b64eb-223">Логическое значение, указывающее, развернуто ли ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-223">Boolean value that indicates whether hello resource is deployed.</span></span> |
| <span data-ttu-id="b64eb-224">версия_API</span><span class="sxs-lookup"><span data-stu-id="b64eb-224">apiVersion</span></span> |<span data-ttu-id="b64eb-225">Да</span><span class="sxs-lookup"><span data-stu-id="b64eb-225">Yes</span></span> |<span data-ttu-id="b64eb-226">Версия toouse hello API-интерфейса REST для создания ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-226">Version of hello REST API toouse for creating hello resource.</span></span> |
| <span data-ttu-id="b64eb-227">type</span><span class="sxs-lookup"><span data-stu-id="b64eb-227">type</span></span> |<span data-ttu-id="b64eb-228">Да</span><span class="sxs-lookup"><span data-stu-id="b64eb-228">Yes</span></span> |<span data-ttu-id="b64eb-229">Тип ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-229">Type of hello resource.</span></span> <span data-ttu-id="b64eb-230">Это значение представляет собой сочетание hello пространство имен поставщика ресурсов hello и тип ресурса hello (такие как **Microsoft.Storage/storageAccounts**).</span><span class="sxs-lookup"><span data-stu-id="b64eb-230">This value is a combination of hello namespace of hello resource provider and hello resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="b64eb-231">name</span><span class="sxs-lookup"><span data-stu-id="b64eb-231">name</span></span> |<span data-ttu-id="b64eb-232">Да</span><span class="sxs-lookup"><span data-stu-id="b64eb-232">Yes</span></span> |<span data-ttu-id="b64eb-233">Имя ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-233">Name of hello resource.</span></span> <span data-ttu-id="b64eb-234">Hello имя должно соответствовать ограничениям для компонента URI определен в RFC3986.</span><span class="sxs-lookup"><span data-stu-id="b64eb-234">hello name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="b64eb-235">Кроме того, Azure службы, предоставляющие имя toooutside hello ресурсов сторон проверки убедитесь, что не toospoof попытка toomake имя hello другим удостоверением.</span><span class="sxs-lookup"><span data-stu-id="b64eb-235">In addition, Azure services that expose hello resource name toooutside parties validate hello name toomake sure it is not an attempt toospoof another identity.</span></span> |
| <span data-ttu-id="b64eb-236">location</span><span class="sxs-lookup"><span data-stu-id="b64eb-236">location</span></span> |<span data-ttu-id="b64eb-237">Varies</span><span class="sxs-lookup"><span data-stu-id="b64eb-237">Varies</span></span> |<span data-ttu-id="b64eb-238">Поддерживаемые географические расположения hello существовало ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b64eb-238">Supported geo-locations of hello provided resource.</span></span> <span data-ttu-id="b64eb-239">Можно выбрать любой из доступных расположений hello, но обычно он выполняет toopick смысле это закрыть tooyour пользователей.</span><span class="sxs-lookup"><span data-stu-id="b64eb-239">You can select any of hello available locations, but typically it makes sense toopick one that is close tooyour users.</span></span> <span data-ttu-id="b64eb-240">Как правило, также имеет смысл tooplace ресурсы, которые взаимодействуют друг с другом в hello же области.</span><span class="sxs-lookup"><span data-stu-id="b64eb-240">Usually, it also makes sense tooplace resources that interact with each other in hello same region.</span></span> <span data-ttu-id="b64eb-241">Большинству типов ресурсов нужно расположение, но некоторым типам (например, назначению роли) оно не требуется.</span><span class="sxs-lookup"><span data-stu-id="b64eb-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="b64eb-242">Ознакомьтесь с разделом [Определение расположения ресурса в шаблонах Azure Resource Manager](resource-manager-template-location.md).</span><span class="sxs-lookup"><span data-stu-id="b64eb-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="b64eb-243">tags</span><span class="sxs-lookup"><span data-stu-id="b64eb-243">tags</span></span> |<span data-ttu-id="b64eb-244">Нет</span><span class="sxs-lookup"><span data-stu-id="b64eb-244">No</span></span> |<span data-ttu-id="b64eb-245">Теги, связанные с ресурсом hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-245">Tags that are associated with hello resource.</span></span> <span data-ttu-id="b64eb-246">Ознакомьтесь с разделом [Присвоение тегов ресурсам в шаблоне Azure Resource Manager](resource-manager-template-tags.md).</span><span class="sxs-lookup"><span data-stu-id="b64eb-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="b64eb-247">комментарии</span><span class="sxs-lookup"><span data-stu-id="b64eb-247">comments</span></span> |<span data-ttu-id="b64eb-248">Нет</span><span class="sxs-lookup"><span data-stu-id="b64eb-248">No</span></span> |<span data-ttu-id="b64eb-249">Заметки для документирования hello ресурсы в шаблон</span><span class="sxs-lookup"><span data-stu-id="b64eb-249">Your notes for documenting hello resources in your template</span></span> |
| <span data-ttu-id="b64eb-250">копирование</span><span class="sxs-lookup"><span data-stu-id="b64eb-250">copy</span></span> |<span data-ttu-id="b64eb-251">Нет</span><span class="sxs-lookup"><span data-stu-id="b64eb-251">No</span></span> |<span data-ttu-id="b64eb-252">Если требуется более одного экземпляра hello число toocreate ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b64eb-252">If more than one instance is needed, hello number of resources toocreate.</span></span> <span data-ttu-id="b64eb-253">режим по умолчанию Hello работает параллельно.</span><span class="sxs-lookup"><span data-stu-id="b64eb-253">hello default mode is parallel.</span></span> <span data-ttu-id="b64eb-254">Укажите режим последовательного hello toodeploy ресурсы в hello или не все одновременно.</span><span class="sxs-lookup"><span data-stu-id="b64eb-254">Specify serial mode when you do not want all or hello resources toodeploy at hello same time.</span></span> <span data-ttu-id="b64eb-255">Дополнительные сведения см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="b64eb-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="b64eb-256">Свойство dependsOn</span><span class="sxs-lookup"><span data-stu-id="b64eb-256">dependsOn</span></span> |<span data-ttu-id="b64eb-257">Нет</span><span class="sxs-lookup"><span data-stu-id="b64eb-257">No</span></span> |<span data-ttu-id="b64eb-258">Ресурсы, которые должны быть развернуты перед развертыванием этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="b64eb-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="b64eb-259">Диспетчер ресурсов оценивает hello зависимости между ресурсами и развертывает их в правильном порядке hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-259">Resource Manager evaluates hello dependencies between resources and deploys them in hello correct order.</span></span> <span data-ttu-id="b64eb-260">Если ресурсы не зависят друг от друга, они развертываются параллельно.</span><span class="sxs-lookup"><span data-stu-id="b64eb-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="b64eb-261">Hello значение может быть ресурса список разделенных запятыми имен или уникальные идентификаторы ресурса.</span><span class="sxs-lookup"><span data-stu-id="b64eb-261">hello value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="b64eb-262">Выводится только список ресурсов, развертываемых в этом шаблоне.</span><span class="sxs-lookup"><span data-stu-id="b64eb-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="b64eb-263">Ресурсы, которые не определены в этом шаблоне, уже должны существовать.</span><span class="sxs-lookup"><span data-stu-id="b64eb-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="b64eb-264">Избегайте добавления ненужных зависимостей, так как это может замедлить развертывание и привести к созданию циклических зависимостей.</span><span class="sxs-lookup"><span data-stu-id="b64eb-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="b64eb-265">Рекомендации по настройке зависимостей см. в статье [Определение зависимостей в шаблонах диспетчера ресурсов Azure](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="b64eb-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="b64eb-266">properties</span><span class="sxs-lookup"><span data-stu-id="b64eb-266">properties</span></span> |<span data-ttu-id="b64eb-267">Нет</span><span class="sxs-lookup"><span data-stu-id="b64eb-267">No</span></span> |<span data-ttu-id="b64eb-268">Параметры конфигурации ресурса.</span><span class="sxs-lookup"><span data-stu-id="b64eb-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="b64eb-269">Hello значения для свойств hello hello таким же, как hello значения, которые можно указать в тексте запроса hello hello API-интерфейса REST операции (метод PUT) toocreate hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b64eb-269">hello values for hello properties are hello same as hello values you provide in hello request body for hello REST API operation (PUT method) toocreate hello resource.</span></span> <span data-ttu-id="b64eb-270">Кроме того, можно указать toocreate копии массива несколько экземпляров свойства.</span><span class="sxs-lookup"><span data-stu-id="b64eb-270">You can also specify a copy array toocreate multiple instances of a property.</span></span> <span data-ttu-id="b64eb-271">Дополнительные сведения см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="b64eb-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="b64eb-272">ресурсов</span><span class="sxs-lookup"><span data-stu-id="b64eb-272">resources</span></span> |<span data-ttu-id="b64eb-273">Нет</span><span class="sxs-lookup"><span data-stu-id="b64eb-273">No</span></span> |<span data-ttu-id="b64eb-274">Дочерние ресурсы, зависящие от определяемого ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-274">Child resources that depend on hello resource being defined.</span></span> <span data-ttu-id="b64eb-275">Предоставлять только типы ресурсов, разрешенные схемой "hello" hello родительский ресурс.</span><span class="sxs-lookup"><span data-stu-id="b64eb-275">Only provide resource types that are permitted by hello schema of hello parent resource.</span></span> <span data-ttu-id="b64eb-276">Hello полное имя типа hello дочерний ресурс включает hello родительским типом ресурса, например **Microsoft.Web/sites/extensions**.</span><span class="sxs-lookup"><span data-stu-id="b64eb-276">hello fully qualified type of hello child resource includes hello parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="b64eb-277">Зависимость от родительского ресурса hello не предусмотрено.</span><span class="sxs-lookup"><span data-stu-id="b64eb-277">Dependency on hello parent resource is not implied.</span></span> <span data-ttu-id="b64eb-278">Ее необходимо определить явным образом.</span><span class="sxs-lookup"><span data-stu-id="b64eb-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="b64eb-279">раздел ресурсов Hello содержит массив toodeploy ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-279">hello resources section contains an array of hello resources toodeploy.</span></span> <span data-ttu-id="b64eb-280">Внутри каждого ресурса можно также определить набор дочерних ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b64eb-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="b64eb-281">Таким образом раздел ресурсов может иметь примерно следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="b64eb-281">Therefore, your resources section could have a structure like:</span></span>

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

<span data-ttu-id="b64eb-282">Дополнительные сведения об определении дочерних ресурсов см. в разделе [Указание имени и типа дочернего ресурса в шаблоне Resource Manager](resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="b64eb-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="b64eb-283">Hello **условие** элемент определяет, развертывается ли ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-283">hello **condition** element specifies whether hello resource is deployed.</span></span> <span data-ttu-id="b64eb-284">Hello значение для этого элемента разрешает tootrue или false.</span><span class="sxs-lookup"><span data-stu-id="b64eb-284">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="b64eb-285">Например toospecify ли развернуть новую учетную запись хранения, используйте:</span><span class="sxs-lookup"><span data-stu-id="b64eb-285">For example, toospecify whether a new storage account is deployed, use:</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="b64eb-286">Пример использования нового или имеющегося шаблона условий см. [здесь](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="b64eb-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="b64eb-287">toospecify ли развертывание виртуальных машин с помощью пароля или ключа SSH определения двух версий hello виртуальной машины в шаблон и использовать **условие** toodifferentiate использования.</span><span class="sxs-lookup"><span data-stu-id="b64eb-287">toospecify whether a virtual machine is deployed with a password or SSH key, define two versions of hello virtual machine in your template and use **condition** toodifferentiate usage.</span></span> <span data-ttu-id="b64eb-288">Передайте параметр, указывающий, какие сценарии toodeploy.</span><span class="sxs-lookup"><span data-stu-id="b64eb-288">Pass a parameter that specifies which scenario toodeploy.</span></span>

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

<span data-ttu-id="b64eb-289">Пример использования пароля или SSH ключа toodeploy виртуальной машины, в разделе [имя пользователя или SSH условие шаблона](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="b64eb-289">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="b64eb-290">outputs</span><span class="sxs-lookup"><span data-stu-id="b64eb-290">Outputs</span></span>
<span data-ttu-id="b64eb-291">В разделе hello выходные данные укажите значения, возвращаемые из развертывания.</span><span class="sxs-lookup"><span data-stu-id="b64eb-291">In hello Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="b64eb-292">Например может вернуть hello URI tooaccess развернутых ресурсах.</span><span class="sxs-lookup"><span data-stu-id="b64eb-292">For example, you could return hello URI tooaccess a deployed resource.</span></span>

<span data-ttu-id="b64eb-293">Hello ниже приведен пример структуры hello определения выходных данных.</span><span class="sxs-lookup"><span data-stu-id="b64eb-293">hello following example shows hello structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="b64eb-294">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="b64eb-294">Element name</span></span> | <span data-ttu-id="b64eb-295">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b64eb-295">Required</span></span> | <span data-ttu-id="b64eb-296">Описание</span><span class="sxs-lookup"><span data-stu-id="b64eb-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b64eb-297">outputName</span><span class="sxs-lookup"><span data-stu-id="b64eb-297">outputName</span></span> |<span data-ttu-id="b64eb-298">Да</span><span class="sxs-lookup"><span data-stu-id="b64eb-298">Yes</span></span> |<span data-ttu-id="b64eb-299">Имя hello выходное значение.</span><span class="sxs-lookup"><span data-stu-id="b64eb-299">Name of hello output value.</span></span> <span data-ttu-id="b64eb-300">Должно быть допустимым идентификатором JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b64eb-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="b64eb-301">type</span><span class="sxs-lookup"><span data-stu-id="b64eb-301">type</span></span> |<span data-ttu-id="b64eb-302">Да</span><span class="sxs-lookup"><span data-stu-id="b64eb-302">Yes</span></span> |<span data-ttu-id="b64eb-303">Тип выходного значения hello.</span><span class="sxs-lookup"><span data-stu-id="b64eb-303">Type of hello output value.</span></span> <span data-ttu-id="b64eb-304">Выходные значения поддерживает hello же типы в качестве входных параметров шаблона.</span><span class="sxs-lookup"><span data-stu-id="b64eb-304">Output values support hello same types as template input parameters.</span></span> |
| <span data-ttu-id="b64eb-305">value</span><span class="sxs-lookup"><span data-stu-id="b64eb-305">value</span></span> |<span data-ttu-id="b64eb-306">Да</span><span class="sxs-lookup"><span data-stu-id="b64eb-306">Yes</span></span> |<span data-ttu-id="b64eb-307">Выражение на языке шаблона, которое вычисляется и возвращается в качестве выходного значения.</span><span class="sxs-lookup"><span data-stu-id="b64eb-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="b64eb-308">Hello пример значение, которое возвращается в разделе hello выходные данные.</span><span class="sxs-lookup"><span data-stu-id="b64eb-308">hello following example shows a value that is returned in hello Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="b64eb-309">Дополнительные сведения о работе с выходными данными см. в статье [Совместное использование состояния в шаблонах Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="b64eb-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="b64eb-310">Ограничения шаблонов</span><span class="sxs-lookup"><span data-stu-id="b64eb-310">Template limits</span></span>

<span data-ttu-id="b64eb-311">Ограничить размер hello ваш шаблон too1 МБ, а также каждый параметр файловой too64 КБ.</span><span class="sxs-lookup"><span data-stu-id="b64eb-311">Limit hello size of your template too1 MB, and each parameter file too64 KB.</span></span> <span data-ttu-id="b64eb-312">ограничение 1 МБ Hello применяется toohello конечное состояние шаблона hello после была расширена с помощью определения итеративный ресурсов и значения для переменных и параметров.</span><span class="sxs-lookup"><span data-stu-id="b64eb-312">hello 1-MB limit applies toohello final state of hello template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="b64eb-313">Кроме того, ограничение распространяется на:</span><span class="sxs-lookup"><span data-stu-id="b64eb-313">You are also limited to:</span></span>

* <span data-ttu-id="b64eb-314">256 параметров;</span><span class="sxs-lookup"><span data-stu-id="b64eb-314">256 parameters</span></span>
* <span data-ttu-id="b64eb-315">256 переменных;</span><span class="sxs-lookup"><span data-stu-id="b64eb-315">256 variables</span></span>
* <span data-ttu-id="b64eb-316">800 ресурсов (включая число копий);</span><span class="sxs-lookup"><span data-stu-id="b64eb-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="b64eb-317">64 выходных значения;</span><span class="sxs-lookup"><span data-stu-id="b64eb-317">64 output values</span></span>
* <span data-ttu-id="b64eb-318">24 576 знаков в выражении шаблона.</span><span class="sxs-lookup"><span data-stu-id="b64eb-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="b64eb-319">Некоторые ограничения можно превысить, используя вложенные шаблоны.</span><span class="sxs-lookup"><span data-stu-id="b64eb-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="b64eb-320">Дополнительные сведения см. разделе [Использование связанных шаблонов в при развертывании ресурсов Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b64eb-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="b64eb-321">tooreduce hello число параметров, переменных или выходных данных, можно объединить несколько значений в объект.</span><span class="sxs-lookup"><span data-stu-id="b64eb-321">tooreduce hello number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="b64eb-322">См. дополнительные сведения об [использовании объектов как параметров](resource-manager-objects-as-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="b64eb-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b64eb-323">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b64eb-323">Next steps</span></span>
* <span data-ttu-id="b64eb-324">tooview завершения шаблоны для различных типов решений, см. hello [шаблоны быстрый запуск Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="b64eb-324">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="b64eb-325">Дополнительные сведения о функциях hello, можно использовать из шаблона, в разделе [функции шаблона диспетчера ресурсов Azure](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="b64eb-325">For details about hello functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="b64eb-326">toocombine несколько шаблонов во время развертывания, см. раздел [с помощью шаблонов, связанных с диспетчером ресурсов Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b64eb-326">toocombine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="b64eb-327">Может потребоваться toouse ресурсов, которые существуют в другой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b64eb-327">You may need toouse resources that exist within a different resource group.</span></span> <span data-ttu-id="b64eb-328">Это распространенная ситуация при работе с учетными записями хранения или виртуальными сетями, которые совместно используются в нескольких группах ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b64eb-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="b64eb-329">Дополнительные сведения см. в разделе hello [функции resourceId](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="b64eb-329">For more information, see hello [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
