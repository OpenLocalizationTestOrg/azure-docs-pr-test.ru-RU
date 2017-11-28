---
title: "Общие сведения о службах мультимедиа aaaAzure | Документы Microsoft"
description: "В этом разделе приводится краткий обзор служб мультимедиа Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/04/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 81f9f4d9ff75effea30c10fd09449e9d2025f377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-overview"></a><span data-ttu-id="5bba1-103">Общие сведения о службах мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="5bba1-103">Azure Media Services overview</span></span> 

<span data-ttu-id="5bba1-104">Службы мультимедиа Microsoft Azure — это расширяемая платформа облачных, который позволяет разработчикам toobuild масштабируемая мультимедийная управления и доставки приложения.</span><span class="sxs-lookup"><span data-stu-id="5bba1-104">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers toobuild scalable media management and delivery applications.</span></span> <span data-ttu-id="5bba1-105">Media Services основана на API REST, которые позволяют toosecurely передачи, хранения, кодирования и упаковки аудио-и по запросу и динамической потоковой передачи доставки toovarious клиентов (например, ТВ, ПК и мобильных устройств).</span><span class="sxs-lookup"><span data-stu-id="5bba1-105">Media Services is based on REST APIs that enable you toosecurely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery toovarious clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="5bba1-106">Можно создавать сквозные рабочие процессы, полностью использующие службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5bba1-106">You can build end-to-end workflows using entirely Media Services.</span></span> <span data-ttu-id="5bba1-107">Можно также toouse компоненты сторонних разработчиков для некоторых частей рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="5bba1-107">You can also choose toouse third-party components for some parts of your workflow.</span></span> <span data-ttu-id="5bba1-108">Например, можно выполнять кодирование с помощью стороннего кодировщика.</span><span class="sxs-lookup"><span data-stu-id="5bba1-108">For example, encode using a third-party encoder.</span></span> <span data-ttu-id="5bba1-109">А затем отправить, защитить, упаковать и доставить содержимое с использованием служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5bba1-109">Then, upload, protect, package, deliver using Media Services.</span></span>

<span data-ttu-id="5bba1-110">Можно выбрать toostream динамического содержимого или доставки содержимого по запросу.</span><span class="sxs-lookup"><span data-stu-id="5bba1-110">You can choose toostream your content live or deliver content on-demand.</span></span> <span data-ttu-id="5bba1-111">Hello разделе также приведены ссылки tooother соответствующие разделы.</span><span class="sxs-lookup"><span data-stu-id="5bba1-111">hello topic also links tooother relevant topics.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="5bba1-112">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="5bba1-112">Media Services learning paths</span></span>
<span data-ttu-id="5bba1-113">Схемы обучения AMS можно просмотреть здесь:</span><span class="sxs-lookup"><span data-stu-id="5bba1-113">You can view AMS learning paths here:</span></span>

* [<span data-ttu-id="5bba1-114">Рабочий процесс для потоковой передачи в реальном времени в службах AMS</span><span class="sxs-lookup"><span data-stu-id="5bba1-114">AMS Live Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [<span data-ttu-id="5bba1-115">Рабочий процесс для потоковой передачи по запросу в службах AMS</span><span class="sxs-lookup"><span data-stu-id="5bba1-115">AMS on-Demand Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a><span data-ttu-id="5bba1-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5bba1-116">Prerequisites</span></span>

<span data-ttu-id="5bba1-117">toostart с помощью служб мультимедиа Azure, должен иметь hello ниже:</span><span class="sxs-lookup"><span data-stu-id="5bba1-117">toostart using Azure Media Services, you should have hello following:</span></span>

* <span data-ttu-id="5bba1-118">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="5bba1-118">An Azure account.</span></span> <span data-ttu-id="5bba1-119">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="5bba1-119">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5bba1-120">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="5bba1-120">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="5bba1-121">Учетная запись служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="5bba1-121">An Azure Media Services account.</span></span> <span data-ttu-id="5bba1-122">Дополнительные сведения см. в статье [Создание учетной записи служб мультимедиа Azure с помощью портала Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="5bba1-122">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="5bba1-123">Настройка среды разработки (необязательно) Выберите .NET или REST API для среды разработки.</span><span class="sxs-lookup"><span data-stu-id="5bba1-123">(Optional) Set up development environment.</span></span> <span data-ttu-id="5bba1-124">Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="5bba1-124">Choose .NET or REST API for your development environment.</span></span> <span data-ttu-id="5bba1-125">в [разделе о настройке среды](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="5bba1-125">For more information, see [Set up environment](media-services-dotnet-how-to-use.md).</span></span>

    <span data-ttu-id="5bba1-126">Кроме того, узнайте, каким образом слишком[программно подключаться tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="5bba1-126">Also, learn how too[connect  programmatically tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
* <span data-ttu-id="5bba1-127">Конечная точка потоковой передачи уровня "Стандартный" или "Премиум" в состоянии "Запущено".</span><span class="sxs-lookup"><span data-stu-id="5bba1-127">A standard or premium streaming endpoint in started state.</span></span>  <span data-ttu-id="5bba1-128">Дополнительные сведения см. в статье [Управление конечными точками потоковой передачи](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="5bba1-128">For more information, see [Managing streaming endpoints](media-services-portal-manage-streaming-endpoints.md)</span></span>

## <a name="sdks-and-tools"></a><span data-ttu-id="5bba1-129">Пакеты SDK и средства</span><span class="sxs-lookup"><span data-stu-id="5bba1-129">SDKs and tools</span></span>

<span data-ttu-id="5bba1-130">toobuild решений служб мультимедиа, можно использовать:</span><span class="sxs-lookup"><span data-stu-id="5bba1-130">toobuild Media Services solutions, you can use:</span></span>

* [<span data-ttu-id="5bba1-131">REST API для службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5bba1-131">Media Services REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* <span data-ttu-id="5bba1-132">Одно из доступных клиентских hello SDK:</span><span class="sxs-lookup"><span data-stu-id="5bba1-132">One of hello available client SDKs:</span></span>
    * <span data-ttu-id="5bba1-133">[Пакет SDK служб мультимедиа Azure для .NET](https://github.com/Azure/azure-sdk-for-media-services).</span><span class="sxs-lookup"><span data-stu-id="5bba1-133">[Azure Media Services SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services),</span></span>
    * <span data-ttu-id="5bba1-134">[Пакет Azure SDK для Java](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="5bba1-134">[Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java),</span></span>
    * <span data-ttu-id="5bba1-135">[Пакет Azure SDK для PHP](https://github.com/Azure/azure-sdk-for-php).</span><span class="sxs-lookup"><span data-stu-id="5bba1-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span></span>
    * <span data-ttu-id="5bba1-136">[Службы мультимедиа Azure для Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (это версия пакета SDK для Node.js сторонних производителей.</span><span class="sxs-lookup"><span data-stu-id="5bba1-136">[Azure Media Services for Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (This is a non-Microsoft version of a Node.js SDK.</span></span> <span data-ttu-id="5bba1-137">Он поддерживается сообществом и в настоящее время не поддерживает полностью защитить hello API-интерфейсы AMS).</span><span class="sxs-lookup"><span data-stu-id="5bba1-137">It is maintained by a community and currently does not have a 100% coverage of hello AMS APIs).</span></span>
* <span data-ttu-id="5bba1-138">Существующие средства:</span><span class="sxs-lookup"><span data-stu-id="5bba1-138">Existing tools:</span></span>
    * [<span data-ttu-id="5bba1-139">портал Azure</span><span class="sxs-lookup"><span data-stu-id="5bba1-139">Azure portal</span></span>](https://portal.azure.com/)
    * <span data-ttu-id="5bba1-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (обозреватель служб мультимедиа Azure (AMSE) является приложением Winforms/С# для Windows)</span><span class="sxs-lookup"><span data-stu-id="5bba1-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) is a Winforms/C# application for Windows)</span></span>

## <a name="concepts-and-overview"></a><span data-ttu-id="5bba1-141">Основные сведения и понятия</span><span class="sxs-lookup"><span data-stu-id="5bba1-141">Concepts and overview</span></span>
<span data-ttu-id="5bba1-142">Основные понятия служб мультимедиа Azure см. в статье [Основные понятия служб мультимедиа Azure](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="5bba1-142">For Azure Media Services concepts, see [Concepts](media-services-concepts.md).</span></span>

<span data-ttu-id="5bba1-143">Как tooseries, демонстрирующих tooall hello основные компоненты служб мультимедиа Azure, в разделе [учебники Azure Media Services пошаговое](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span><span class="sxs-lookup"><span data-stu-id="5bba1-143">For a how-tooseries that introduces you tooall hello main components of Azure Media Services, see [Azure Media Services Step-by-Step tutorials](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span></span> <span data-ttu-id="5bba1-144">Эта серия имеет отличный обзор понятий и использует средство toodemonstrate AMS hello AMSE задачи.</span><span class="sxs-lookup"><span data-stu-id="5bba1-144">This series has a great overview of concepts and it uses hello AMSE tool toodemonstrate AMS tasks.</span></span> <span data-ttu-id="5bba1-145">Средство AMSE разработано для Windows.</span><span class="sxs-lookup"><span data-stu-id="5bba1-145">AMSE tool is a Windows tool.</span></span> <span data-ttu-id="5bba1-146">Это средство поддерживает большинство задач hello, можно получить программным образом с [AMS пакет SDK для .NET](https://github.com/Azure/azure-sdk-for-media-services), [пакет Azure SDK для Java](https://github.com/Azure/azure-sdk-for-java), или [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span><span class="sxs-lookup"><span data-stu-id="5bba1-146">This tool supports most of hello tasks you can achieve programmatically with [AMS SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java), or  [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span></span>

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a><span data-ttu-id="5bba1-147">Поддерживаемые сценарии и доступность служб мультимедиа в центрах обработки данных</span><span class="sxs-lookup"><span data-stu-id="5bba1-147">Supported scenarios and availability of Media Services across data centers</span></span>

<span data-ttu-id="5bba1-148">Дополнительные сведения см. в статье [Scenarios and availability of features and services across data centers](scenarios-and-availability.md) (Сценарии и доступность функций служб мультимедиа в центрах обработки данных).</span><span class="sxs-lookup"><span data-stu-id="5bba1-148">For detailed information, see [AMS scenarios and availability of features and services across data centers](scenarios-and-availability.md).</span></span>

## <a name="service-level-agreement-sla"></a><span data-ttu-id="5bba1-149">Соглашение об уровне обслуживания (SLA):</span><span class="sxs-lookup"><span data-stu-id="5bba1-149">Service Level Agreement (SLA)</span></span>

* <span data-ttu-id="5bba1-150">для кодирования с помощью служб мультимедиа мы гарантируем доступность транзакций через интерфейс REST API на уровне 99,9 %;</span><span class="sxs-lookup"><span data-stu-id="5bba1-150">For Media Services Encoding, we guarantee 99.9% availability of REST API transactions.</span></span>
* <span data-ttu-id="5bba1-151">Для потоковой передачи мы будем успешно обслуживать запросы с гарантией доступности на уровне 99,9 % для существующего мультимедийного содержимого, если приобретена одна конечная точка потоковой передачи уровня "Стандартный" или "Премиум".</span><span class="sxs-lookup"><span data-stu-id="5bba1-151">For Streaming, we will successfully service requests with a 99.9% availability guarantee for existing media content when a standard or premium streaming endpoint is purchased.</span></span>
* <span data-ttu-id="5bba1-152">Для каналов Live мы гарантирует выполнение каналы внешнего подключения менее 99,9% времени hello.</span><span class="sxs-lookup"><span data-stu-id="5bba1-152">For Live Channels, we guarantee that running Channels will have external connectivity at least 99.9% of hello time.</span></span>
* <span data-ttu-id="5bba1-153">При защите содержимого мы гарантируем, что мы будет успешно выполнения ключа запросов менее 99,9% времени hello.</span><span class="sxs-lookup"><span data-stu-id="5bba1-153">For Content Protection, we guarantee that we will successfully fulfill key requests at least 99.9% of hello time.</span></span>
* <span data-ttu-id="5bba1-154">Для индексатора, мы будет успешно обслуживать запросы индексатора задач, обрабатываться с кодировкой зарезервированный устройство 99,9% времени hello.</span><span class="sxs-lookup"><span data-stu-id="5bba1-154">For Indexer, we will successfully service Indexer Task requests processed with an Encoding Reserved Unit 99.9% of hello time.</span></span>

<span data-ttu-id="5bba1-155">Дополнительные сведения можно найти в разделе [Соглашение об уровне обслуживания Microsoft Azure](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="5bba1-155">For more information, see [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="5bba1-156">Сведения о доступности в центрах обработки данных см. в разделе hello [Avaiability](scenarios-and-availability.md#availability) раздела.</span><span class="sxs-lookup"><span data-stu-id="5bba1-156">For information about availability in datacenters, see hello [Avaiability](scenarios-and-availability.md#availability) section.</span></span>

## <a name="support"></a><span data-ttu-id="5bba1-157">Поддержка</span><span class="sxs-lookup"><span data-stu-id="5bba1-157">Support</span></span>

<span data-ttu-id="5bba1-158">[Служба поддержки Azure](https://azure.microsoft.com/support/options/) обеспечивает различные варианты поддержки для Azure, включая службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5bba1-158">[Azure Support](https://azure.microsoft.com/support/options/) provides support options for Azure, including Media Services.</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="5bba1-159">Отзывы</span><span class="sxs-lookup"><span data-stu-id="5bba1-159">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
