---
title: "Общие сведения о создании определения пользовательского интерфейса для управляемых приложений Azure | Документация Майкрософт"
description: "Сведения о создании определений пользовательского интерфейса для управляемых приложений Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 176b891538f85c5638a2321561c3d8bd377d245b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="2b4db-103">Начало работы с CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="2b4db-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="2b4db-104">В этом документе приводится обзор ключевых понятий определения CreateUiDefinition, которое используется на портале Azure, чтобы сгенерировать пользовательский интерфейс для создания управляемого приложения.</span><span class="sxs-lookup"><span data-stu-id="2b4db-104">This document introduces the core concepts of a CreateUiDefinition, which is used by the Azure portal to generate the user interface for creating a managed application.</span></span>

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

<span data-ttu-id="2b4db-105">CreateUiDefinition всегда содержит три свойства:</span><span class="sxs-lookup"><span data-stu-id="2b4db-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="2b4db-106">handler;</span><span class="sxs-lookup"><span data-stu-id="2b4db-106">handler</span></span>
* <span data-ttu-id="2b4db-107">версия</span><span class="sxs-lookup"><span data-stu-id="2b4db-107">version</span></span>
* <span data-ttu-id="2b4db-108">parameters</span><span class="sxs-lookup"><span data-stu-id="2b4db-108">parameters</span></span>

<span data-ttu-id="2b4db-109">Для управляемых приложений handler должен всегда иметь значение `Microsoft.Compute.MultiVm`, а последняя поддерживаемая версия — `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="2b4db-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and the latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="2b4db-110">Схема свойства parameters зависит от сочетания определенных значений handler и version.</span><span class="sxs-lookup"><span data-stu-id="2b4db-110">The schema of the parameters property depends on the combination of the specified handler and version.</span></span> <span data-ttu-id="2b4db-111">Для управляемых приложений поддерживаются свойства `basics`, `steps` и `outputs`.</span><span class="sxs-lookup"><span data-stu-id="2b4db-111">For managed applications, the supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="2b4db-112">Свойства basics и steps содержат _элементы_, например текстовые поля и раскрывающиеся списки, которые отображаются на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2b4db-112">The basics and steps properties contain the _elements_ - like textboxes and dropdowns - to be displayed in the Azure portal.</span></span> <span data-ttu-id="2b4db-113">Свойство output используется для сопоставления значений определенных элементов с параметрами шаблона развертывания Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2b4db-113">The outputs property is used to map the output values of the specified elements to the parameters of the Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="2b4db-114">Советуем также использовать параметр `$schema`, но это необязательно.</span><span class="sxs-lookup"><span data-stu-id="2b4db-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="2b4db-115">При его использовании значение параметра `version` должно совпадать с версией в URI `$schema`.</span><span class="sxs-lookup"><span data-stu-id="2b4db-115">If specified, the value for `version` must match the version within the `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="2b4db-116">Основы</span><span class="sxs-lookup"><span data-stu-id="2b4db-116">Basics</span></span>
<span data-ttu-id="2b4db-117">Шаг basics всегда является первым шагом мастера, который создается, когда портал Azure анализирует CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="2b4db-117">The Basics step is always the first step of the wizard generated when the Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="2b4db-118">Помимо отображения элементов, указанных в `basics`, портал вводит элементы, чтобы пользователи выбрали подписку, группу ресурсов и местоположение для развертывания.</span><span class="sxs-lookup"><span data-stu-id="2b4db-118">In addition to displaying the elements specified in `basics`, the portal injects elements for users to choose the subscription, resource group, and location for the deployment.</span></span> <span data-ttu-id="2b4db-119">Как правило, на этом шаге должны выполняться элементы, запрашивающие параметры для всего развертывания, такие как имя кластера или учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="2b4db-119">Generally, elements that query for deployment-wide parameters, like the name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="2b4db-120">Если поведение элемента зависит от подписки пользователя, группы ресурсов или местоположения, тогда он не может использоваться на шаге basics.</span><span class="sxs-lookup"><span data-stu-id="2b4db-120">If an element's behavior depends on the user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="2b4db-121">Например, **Microsoft.Compute.SizeSelector** определяет список доступных размеров в зависимости от подписки пользователя и местоположения.</span><span class="sxs-lookup"><span data-stu-id="2b4db-121">For example, **Microsoft.Compute.SizeSelector** depends on the user's subscription and location to determine the list of available sizes.</span></span> <span data-ttu-id="2b4db-122">Таким образом, **Microsoft.Compute.SizeSelector** может использоваться только в steps.</span><span class="sxs-lookup"><span data-stu-id="2b4db-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="2b4db-123">Как правило, только элементы в пространстве имен **Microsoft.Common** могут использоваться в basics.</span><span class="sxs-lookup"><span data-stu-id="2b4db-123">Generally, only elements in the **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="2b4db-124">Хотя некоторые элементы в других пространствах имен (например, **Microsoft.Compute.Credentials**), которые не зависят от контекста пользователя, по-прежнему разрешены.</span><span class="sxs-lookup"><span data-stu-id="2b4db-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on the user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="2b4db-125">Действия</span><span class="sxs-lookup"><span data-stu-id="2b4db-125">Steps</span></span>
<span data-ttu-id="2b4db-126">Свойство steps может содержать как ноль, так и несколько дополнительных шагов для отображения после basics, каждый из которых содержит один или несколько элементов.</span><span class="sxs-lookup"><span data-stu-id="2b4db-126">The steps property can contain zero or more additional steps to display after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="2b4db-127">Вы можете добавить действия для каждой роли или уровня развертываемого приложения.</span><span class="sxs-lookup"><span data-stu-id="2b4db-127">Consider adding steps per role or tier of the application being deployed.</span></span> <span data-ttu-id="2b4db-128">Например, действие для входных данных главных узлов и действие для рабочих узлов в кластере.</span><span class="sxs-lookup"><span data-stu-id="2b4db-128">For example, add a step for inputs for the master nodes, and a step for the worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="2b4db-129">outputs</span><span class="sxs-lookup"><span data-stu-id="2b4db-129">Outputs</span></span>
<span data-ttu-id="2b4db-130">Портал Azure использует свойство `outputs` для сопоставления элементов `basics` и `steps` с параметрами шаблона развертывания Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2b4db-130">The Azure portal uses the `outputs` property to map elements from `basics` and `steps` to the parameters of the Azure Resource Manager deployment template.</span></span> <span data-ttu-id="2b4db-131">Ключами являются имена параметров шаблона, а значениями — свойства выходных объектов из элементов, на которые даются ссылки.</span><span class="sxs-lookup"><span data-stu-id="2b4db-131">The keys of this dictionary are the names of the template parameters, and the values are properties of the output objects from the referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="2b4db-132">Функции</span><span class="sxs-lookup"><span data-stu-id="2b4db-132">Functions</span></span>
<span data-ttu-id="2b4db-133">Аналогично [функциям шаблонов](resource-group-template-functions.md) в Azure Resource Manager (и синтаксис, и функции) CreateUiDefinition предоставляет функции для работы с входными и выходными данными элементов, а также условные выражения.</span><span class="sxs-lookup"><span data-stu-id="2b4db-133">Similar to [template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b4db-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2b4db-134">Next steps</span></span>
<span data-ttu-id="2b4db-135">CreateUiDefinition имеет простую схему.</span><span class="sxs-lookup"><span data-stu-id="2b4db-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="2b4db-136">Заложенные в нем возможности раскрываются с помощью всех поддерживаемых элементов и функций, которые подробно описаны в следующих документах:</span><span class="sxs-lookup"><span data-stu-id="2b4db-136">The real depth of it comes from all the supported elements and functions, which the following documents describe in wondrous detail:</span></span>

- <span data-ttu-id="2b4db-137">[CreateUiDefinition elements](managed-application-createuidefinition-elements.md) (Элементы CreateUiDefinition)</span><span class="sxs-lookup"><span data-stu-id="2b4db-137">[Elements](managed-application-createuidefinition-elements.md)</span></span>
- [<span data-ttu-id="2b4db-138">Функции</span><span class="sxs-lookup"><span data-stu-id="2b4db-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="2b4db-139">Текущая схема JSON для CreateUiDefinition доступна здесь: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span><span class="sxs-lookup"><span data-stu-id="2b4db-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="2b4db-140">Более поздние версии будут доступны там же.</span><span class="sxs-lookup"><span data-stu-id="2b4db-140">Later versions will be available at the same location.</span></span> <span data-ttu-id="2b4db-141">Замените часть `0.1.2-preview` URL-адреса и значение `version` идентификатором версии, которую вы собираетесь использовать.</span><span class="sxs-lookup"><span data-stu-id="2b4db-141">Replace the `0.1.2-preview` portion of the URL and the `version` value with the version identifier you intend to use.</span></span> <span data-ttu-id="2b4db-142">Сейчас поддерживаются идентификаторы версий `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview` и `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="2b4db-142">The currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>