---
title: "aaaRules для именования сущностей фабрики данных Azure | Документы Microsoft"
description: "Описывает правила именования для сущностей фабрик данных."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 98c5fc5fc932b72b65894afad438b4dc321c8aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---naming-rules"></a><span data-ttu-id="6331d-103">Фабрика данных Azure — правила именования</span><span class="sxs-lookup"><span data-stu-id="6331d-103">Azure Data Factory - naming rules</span></span>
<span data-ttu-id="6331d-104">Привет, в следующей таблице приведены правила именования для артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="6331d-104">hello following table provides naming rules for Data Factory artifacts.</span></span>

| <span data-ttu-id="6331d-105">Имя</span><span class="sxs-lookup"><span data-stu-id="6331d-105">Name</span></span> | <span data-ttu-id="6331d-106">Уникальность имени</span><span class="sxs-lookup"><span data-stu-id="6331d-106">Name Uniqueness</span></span> | <span data-ttu-id="6331d-107">Проверки</span><span class="sxs-lookup"><span data-stu-id="6331d-107">Validation Checks</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6331d-108">Фабрика данных</span><span class="sxs-lookup"><span data-stu-id="6331d-108">Data Factory</span></span> |<span data-ttu-id="6331d-109">Уникально в рамках Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6331d-109">Unique across Microsoft Azure.</span></span> <span data-ttu-id="6331d-110">Именах не учитывается регистр, то есть `MyDF` и `mydf` ссылаться toohello же фабрику данных.</span><span class="sxs-lookup"><span data-stu-id="6331d-110">Names are case-insensitive, that is, `MyDF` and `mydf` refer toohello same data factory.</span></span> |<ul><li><span data-ttu-id="6331d-111">Каждая фабрика данных — связанные tooexactly одной подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="6331d-111">Each data factory is tied tooexactly one Azure subscription.</span></span></li><li><span data-ttu-id="6331d-112">Имена объектов должно начинаться с буквы или цифры и может содержать только буквы, цифры и знак дефиса (-) hello.</span><span class="sxs-lookup"><span data-stu-id="6331d-112">Object names must start with a letter or a number, and can contain only letters, numbers, and hello dash (-) character.</span></span></li><li><span data-ttu-id="6331d-113">Перед каждым знаком тире (-) и после него должна стоять буква или цифра.</span><span class="sxs-lookup"><span data-stu-id="6331d-113">Every dash (-) character must be immediately preceded and followed by a letter or a number.</span></span> <span data-ttu-id="6331d-114">Последовательные тире в именах контейнеров использовать нельзя.</span><span class="sxs-lookup"><span data-stu-id="6331d-114">Consecutive dashes are not permitted in container names.</span></span></li><li><span data-ttu-id="6331d-115">Имя может содержать от 3 до 63 символов.</span><span class="sxs-lookup"><span data-stu-id="6331d-115">Name can be 3-63 characters long.</span></span></li></ul> |
| <span data-ttu-id="6331d-116">Связанные службы/таблицы/конвейеры</span><span class="sxs-lookup"><span data-stu-id="6331d-116">Linked Services/Tables/Pipelines</span></span> |<span data-ttu-id="6331d-117">Уникально в рамках фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="6331d-117">Unique with in a data factory.</span></span> <span data-ttu-id="6331d-118">Регистр в именах не учитывается.</span><span class="sxs-lookup"><span data-stu-id="6331d-118">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="6331d-119">Максимальное количество символов в имени таблицы: 260.</span><span class="sxs-lookup"><span data-stu-id="6331d-119">Maximum number of characters in a table name: 260.</span></span></li><li><span data-ttu-id="6331d-120">Имена объектов должны начинаться с буквы, цифры или символа подчеркивания (_).</span><span class="sxs-lookup"><span data-stu-id="6331d-120">Object names must start with a letter, number, or an underscore (_).</span></span></li><li><span data-ttu-id="6331d-121">Следующие символы не допускаются: ".", "+", "?", "/", "<", ">", "*", "%", "&", ":", "\\".</span><span class="sxs-lookup"><span data-stu-id="6331d-121">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |
| <span data-ttu-id="6331d-122">Группа ресурсов</span><span class="sxs-lookup"><span data-stu-id="6331d-122">Resource Group</span></span> |<span data-ttu-id="6331d-123">Уникально в рамках Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6331d-123">Unique across Microsoft Azure.</span></span> <span data-ttu-id="6331d-124">Регистр в именах не учитывается.</span><span class="sxs-lookup"><span data-stu-id="6331d-124">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="6331d-125">Максимальное количество символов: 1000.</span><span class="sxs-lookup"><span data-stu-id="6331d-125">Maximum number of characters: 1000.</span></span></li><li><span data-ttu-id="6331d-126">Имя может содержать буквы, цифры и следующие символы hello: «-», «_ «,», «и».»</span><span class="sxs-lookup"><span data-stu-id="6331d-126">Name can contain letters, digits, and hello following characters: “-”, “_”, “,” and “.”</span></span></li></ul> |

