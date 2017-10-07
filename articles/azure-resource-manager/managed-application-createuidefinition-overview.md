---
title: "Создание определения пользовательского интерфейса для управляемого приложения Azure aaaUnderstand | Документы Microsoft"
description: "Описывает способ определения toocreate пользовательского интерфейса для управляемого приложения Azure"
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
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="bf8be-103">Начало работы с CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="bf8be-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="bf8be-104">В этом документе понятия hello core CreateUiDefinition, который используется для создания управляемого приложения hello Azure портала toogenerate hello пользовательским интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="bf8be-104">This document introduces hello core concepts of a CreateUiDefinition, which is used by hello Azure portal toogenerate hello user interface for creating a managed application.</span></span>

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

<span data-ttu-id="bf8be-105">CreateUiDefinition всегда содержит три свойства:</span><span class="sxs-lookup"><span data-stu-id="bf8be-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="bf8be-106">handler;</span><span class="sxs-lookup"><span data-stu-id="bf8be-106">handler</span></span>
* <span data-ttu-id="bf8be-107">версия</span><span class="sxs-lookup"><span data-stu-id="bf8be-107">version</span></span>
* <span data-ttu-id="bf8be-108">parameters</span><span class="sxs-lookup"><span data-stu-id="bf8be-108">parameters</span></span>

<span data-ttu-id="bf8be-109">Для управляемых приложений обработчик должен всегда быть `Microsoft.Compute.MultiVm`, hello последние поддерживаемые версии и `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="bf8be-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and hello latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="bf8be-110">Схема Hello hello свойства параметров зависит от сочетание hello указанного обработчика hello и версии.</span><span class="sxs-lookup"><span data-stu-id="bf8be-110">hello schema of hello parameters property depends on hello combination of hello specified handler and version.</span></span> <span data-ttu-id="bf8be-111">Для управляемых приложений hello поддерживается свойства являются `basics`, `steps`, и `outputs`.</span><span class="sxs-lookup"><span data-stu-id="bf8be-111">For managed applications, hello supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="bf8be-112">Hello основы и действия свойства содержат hello _элементы_ - например, текстовые поля и раскрывающиеся меню - toobe отображаются в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bf8be-112">hello basics and steps properties contain hello _elements_ - like textboxes and dropdowns - toobe displayed in hello Azure portal.</span></span> <span data-ttu-id="bf8be-113">Hello результатов, которые оно используется toomap hello выходные значения hello указанные элементы toohello параметров шаблона развертывания диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bf8be-113">hello outputs property is used toomap hello output values of hello specified elements toohello parameters of hello Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="bf8be-114">Советуем также использовать параметр `$schema`, но это необязательно.</span><span class="sxs-lookup"><span data-stu-id="bf8be-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="bf8be-115">Если указано, hello значение `version` должна совпадать с версией hello в hello `$schema` URI.</span><span class="sxs-lookup"><span data-stu-id="bf8be-115">If specified, hello value for `version` must match hello version within hello `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="bf8be-116">Основы</span><span class="sxs-lookup"><span data-stu-id="bf8be-116">Basics</span></span>
<span data-ttu-id="bf8be-117">Основы шаг Hello всегда является этапом hello приветствия мастера создается при CreateUiDefinition анализирует hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bf8be-117">hello Basics step is always hello first step of hello wizard generated when hello Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="bf8be-118">В дополнение к этому toodisplaying hello указываются в `basics`, портал hello вставляет элементы для подписки hello toochoose пользователи, группы ресурсов и расположение для развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="bf8be-118">In addition toodisplaying hello elements specified in `basics`, hello portal injects elements for users toochoose hello subscription, resource group, and location for hello deployment.</span></span> <span data-ttu-id="bf8be-119">Как правило элементы, которые запрос для всего развертывания параметров, как hello имя кластера или администратор учетных данных, следует перейти на этом шаге.</span><span class="sxs-lookup"><span data-stu-id="bf8be-119">Generally, elements that query for deployment-wide parameters, like hello name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="bf8be-120">Если поведение элемента зависит от подписки, группы ресурсов или расположения hello пользователя, этот элемент не может использоваться в основы.</span><span class="sxs-lookup"><span data-stu-id="bf8be-120">If an element's behavior depends on hello user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="bf8be-121">Например **Microsoft.Compute.SizeSelector** зависит от пользователя hello подписке и расположении toodetermine hello список доступных размеров.</span><span class="sxs-lookup"><span data-stu-id="bf8be-121">For example, **Microsoft.Compute.SizeSelector** depends on hello user's subscription and location toodetermine hello list of available sizes.</span></span> <span data-ttu-id="bf8be-122">Таким образом, **Microsoft.Compute.SizeSelector** может использоваться только в steps.</span><span class="sxs-lookup"><span data-stu-id="bf8be-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="bf8be-123">Как правило, только элементы hello **Microsoft.Common** пространства имен можно использовать в основы.</span><span class="sxs-lookup"><span data-stu-id="bf8be-123">Generally, only elements in hello **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="bf8be-124">Несмотря на то что некоторые элементы в других пространствах имен (таких как **Microsoft.Compute.Credentials**), которые не зависят от контекста пользователя hello, по-прежнему разрешены.</span><span class="sxs-lookup"><span data-stu-id="bf8be-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on hello user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="bf8be-125">Действия</span><span class="sxs-lookup"><span data-stu-id="bf8be-125">Steps</span></span>
<span data-ttu-id="bf8be-126">Свойство действия Hello может содержать ноль или более toodisplay дополнительные действия после основные, каждый из которых содержит один или несколько элементов.</span><span class="sxs-lookup"><span data-stu-id="bf8be-126">hello steps property can contain zero or more additional steps toodisplay after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="bf8be-127">Рассмотрите возможность добавления действия в каждой роли или уровня развертываемое приложение hello.</span><span class="sxs-lookup"><span data-stu-id="bf8be-127">Consider adding steps per role or tier of hello application being deployed.</span></span> <span data-ttu-id="bf8be-128">Например добавьте шаг для входных данных для главных узлов hello и шаг для hello рабочих узлов в кластере.</span><span class="sxs-lookup"><span data-stu-id="bf8be-128">For example, add a step for inputs for hello master nodes, and a step for hello worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="bf8be-129">outputs</span><span class="sxs-lookup"><span data-stu-id="bf8be-129">Outputs</span></span>
<span data-ttu-id="bf8be-130">Hello портал Azure использует hello `outputs` toomap элементы свойств из `basics` и `steps` toohello параметров шаблона развертывания диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bf8be-130">hello Azure portal uses hello `outputs` property toomap elements from `basics` and `steps` toohello parameters of hello Azure Resource Manager deployment template.</span></span> <span data-ttu-id="bf8be-131">Hello ключи данного словаря — hello имена параметров шаблона hello и hello значения являются свойствами объектов hello выходные данные из hello ссылки на элементы.</span><span class="sxs-lookup"><span data-stu-id="bf8be-131">hello keys of this dictionary are hello names of hello template parameters, and hello values are properties of hello output objects from hello referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="bf8be-132">Функции</span><span class="sxs-lookup"><span data-stu-id="bf8be-132">Functions</span></span>
<span data-ttu-id="bf8be-133">Аналогичные слишком[функции шаблона](resource-group-template-functions.md) в диспетчере ресурсов Azure (как в синтаксис и функции), CreateUiDefinition предоставляет функции для работы с входными и выходными данными элементов, а также функции, например, условные выражения.</span><span class="sxs-lookup"><span data-stu-id="bf8be-133">Similar too[template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf8be-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bf8be-134">Next steps</span></span>
<span data-ttu-id="bf8be-135">CreateUiDefinition имеет простую схему.</span><span class="sxs-lookup"><span data-stu-id="bf8be-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="bf8be-136">Hello реальные глубину он поступает из все элементы hello поддерживается и функции, удивительное подробного описания какие hello следующие документы:</span><span class="sxs-lookup"><span data-stu-id="bf8be-136">hello real depth of it comes from all hello supported elements and functions, which hello following documents describe in wondrous detail:</span></span>

- <span data-ttu-id="bf8be-137">[CreateUiDefinition elements](managed-application-createuidefinition-elements.md) (Элементы CreateUiDefinition)</span><span class="sxs-lookup"><span data-stu-id="bf8be-137">[Elements](managed-application-createuidefinition-elements.md)</span></span>
- [<span data-ttu-id="bf8be-138">Функции</span><span class="sxs-lookup"><span data-stu-id="bf8be-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="bf8be-139">Текущая схема JSON для CreateUiDefinition доступна здесь: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span><span class="sxs-lookup"><span data-stu-id="bf8be-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="bf8be-140">Более поздние версии можно найти по адресу hello местоположения.</span><span class="sxs-lookup"><span data-stu-id="bf8be-140">Later versions will be available at hello same location.</span></span> <span data-ttu-id="bf8be-141">Замените hello `0.1.2-preview` часть URL-адрес hello и hello `version` значение с идентификатором hello версии планируется toouse.</span><span class="sxs-lookup"><span data-stu-id="bf8be-141">Replace hello `0.1.2-preview` portion of hello URL and hello `version` value with hello version identifier you intend toouse.</span></span> <span data-ttu-id="bf8be-142">идентификаторы Hello в настоящее время поддерживается версия `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, и `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="bf8be-142">hello currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>
