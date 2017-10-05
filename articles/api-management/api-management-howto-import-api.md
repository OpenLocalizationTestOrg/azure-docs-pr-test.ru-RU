---
title: "Импорт API в службу управления API Azure | Документация Майкрософт"
description: "Узнайте, как импортировать API и его операции в службу управления API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c851b88fc1067e65044266d07775717c028e75d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-the-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="125ca-103">Как импортировать определение API с операциями в Azure API Management</span><span class="sxs-lookup"><span data-stu-id="125ca-103">How to import the definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="125ca-104">В управлении API можно создавать новые интерфейсы API и добавлять операции вручную, либо API можно импортировать вместе с операциями за один шаг.</span><span class="sxs-lookup"><span data-stu-id="125ca-104">In API Management, new APIs can be created and the operations added manually, or the API can be imported along with the operations in one step.</span></span>

<span data-ttu-id="125ca-105">Интерфейсы API и их операции можно импортировать с помощью следующих форматов.</span><span class="sxs-lookup"><span data-stu-id="125ca-105">APIs and their operations can be imported using the following formats.</span></span>

* <span data-ttu-id="125ca-106">WADL</span><span class="sxs-lookup"><span data-stu-id="125ca-106">WADL</span></span>
* <span data-ttu-id="125ca-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="125ca-107">Swagger</span></span>

<span data-ttu-id="125ca-108">В этом руководстве показано, как создать новый API и импортировать его операции за один шаг.</span><span class="sxs-lookup"><span data-stu-id="125ca-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="125ca-109">Дополнительные сведения о создании API и добавлении операций вручную см. в статьях [Как создавать интерфейсы API в Azure API Management][How to create APIs] и [Добавление операций в API в Azure API Management][How to add operations to an API].</span><span class="sxs-lookup"><span data-stu-id="125ca-109">For information on manually creating an API and adding operations, see [How to create APIs][How to create APIs] and [How to add operations to an API][How to add operations to an API].</span></span>

## <span data-ttu-id="125ca-110"><a name="import-api"> </a>Импорт API</span><span class="sxs-lookup"><span data-stu-id="125ca-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="125ca-111">API создаются и настраиваются на портале издателя.</span><span class="sxs-lookup"><span data-stu-id="125ca-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="125ca-112">Чтобы перейти на портал издателя, на портале Azure щелкните **Publisher portal** (Портал издателя) для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="125ca-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="125ca-113">Если экземпляр службы управления API еще не создан, см. раздел [Создание экземпляра управления API][Create an API Management service instance] в руководстве [Начало работы со службой управления Azure API][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="125ca-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Портал издателя][api-management-management-console]

<span data-ttu-id="125ca-115">Щелкните **APIs** в расположенном слева меню **Управление API**, а затем — **Импортировать API**.</span><span class="sxs-lookup"><span data-stu-id="125ca-115">Click **APIs** from the **API Management** menu on the left, and then click **import API**.</span></span>

![Импортировать API][api-management-import-apis]

<span data-ttu-id="125ca-117">Окно **Импорт API** содержит три вкладки, которые соответствуют трем способам ввода спецификации API.</span><span class="sxs-lookup"><span data-stu-id="125ca-117">The **Import API** window has three tabs that correspond to the three ways to provide the API specification.</span></span>

* <span data-ttu-id="125ca-118">**Из буфера обмена** позволяет вставлять спецификацию API в указанное текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="125ca-118">**From clipboard** allows you to paste the API specification into the designated text box.</span></span>
* <span data-ttu-id="125ca-119">**Из файла** позволяет искать и выбирать файл, который содержит спецификацию API.</span><span class="sxs-lookup"><span data-stu-id="125ca-119">**From file** allows you to browse to and select the file that contains the API specification.</span></span>
* <span data-ttu-id="125ca-120">**Из URL-адреса** позволяет ввести URL-адрес спецификации для API.</span><span class="sxs-lookup"><span data-stu-id="125ca-120">**From URL** allows you to supply the URL to the specification for the API.</span></span>

![Формат импорта API][api-management-import-api-clipboard]

<span data-ttu-id="125ca-122">После предоставления спецификации API используйте переключатели, расположенные справа, для выбора формата спецификации.</span><span class="sxs-lookup"><span data-stu-id="125ca-122">After providing the API specification, use the radio buttons on the right to indicate the specification format.</span></span> <span data-ttu-id="125ca-123">Поддерживаются следующие форматы.</span><span class="sxs-lookup"><span data-stu-id="125ca-123">The following formats are supported.</span></span>

* <span data-ttu-id="125ca-124">WADL</span><span class="sxs-lookup"><span data-stu-id="125ca-124">WADL</span></span>
* <span data-ttu-id="125ca-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="125ca-125">Swagger</span></span>

<span data-ttu-id="125ca-126">Затем, введите **Суффикс URL-адреса веб-API**.</span><span class="sxs-lookup"><span data-stu-id="125ca-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="125ca-127">Он добавляется к основному URL-адресу для вашей службы API Management.</span><span class="sxs-lookup"><span data-stu-id="125ca-127">This is appended to the base URL for your API management service.</span></span> <span data-ttu-id="125ca-128">Основной URL-адрес является общим для всех интерфейсов API, размещенных в каждом экземпляре службы API Management.</span><span class="sxs-lookup"><span data-stu-id="125ca-128">The base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="125ca-129">API Management различает интерфейсы API по их суффиксу. Следовательно, суффикс должен быть уникальным для каждого API в конкретном экземпляре службы API Management.</span><span class="sxs-lookup"><span data-stu-id="125ca-129">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="125ca-130">После ввода всех значений щелкните **Сохранить** для создания API и связанных операций.</span><span class="sxs-lookup"><span data-stu-id="125ca-130">Once all values are entered, click **Save** to create the API and the associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="125ca-131">Инструкции по импорту API базового калькулятора в формате Swagger см. в статье [Начало работы со службой управления Azure API](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="125ca-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="125ca-132"><a name="export-api"> </a> Экспорт API</span><span class="sxs-lookup"><span data-stu-id="125ca-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="125ca-133">Помимо импорта новых API можно экспортировать определения своих API с портала издателя.</span><span class="sxs-lookup"><span data-stu-id="125ca-133">In addition to importing new APIs, you can export the definitions of your APIs from the publisher portal.</span></span> <span data-ttu-id="125ca-134">Для этого щелкните **Экспорт API** на вкладке **Сводка** своего интерфейса **API**.</span><span class="sxs-lookup"><span data-stu-id="125ca-134">To do so, click **Export API** from the **Summary tab** of your **API**.</span></span>

![Экспорт API][api-management-export-api]

<span data-ttu-id="125ca-136">Интерфейсы API можно экспортировать в формате WADL или Swagger.</span><span class="sxs-lookup"><span data-stu-id="125ca-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="125ca-137">Выберите требуемый формат, щелкните **Сохранить**и выберите папку, в которую следует сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="125ca-137">Select the desired format, click **Save**, and choose the location in which to save the file.</span></span>

![Формат экспорта API][api-management-export-api-format]

## <span data-ttu-id="125ca-139"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="125ca-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="125ca-140">Как только API создан, и операции импортированы, можно просмотреть и настроить все дополнительные параметры, добавить API к продукту, и опубликовать его, чтобы он стал доступен для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="125ca-140">Once an API is created and the operations imported, you can review and configure any additional settings, add the API to a Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="125ca-141">Дополнительные сведения см. в следующих руководствах.</span><span class="sxs-lookup"><span data-stu-id="125ca-141">For more information, see the following guides.</span></span>

* <span data-ttu-id="125ca-142">[Настройка параметров API][How to configure API settings]</span><span class="sxs-lookup"><span data-stu-id="125ca-142">[How to configure API settings][How to configure API settings]</span></span>
* <span data-ttu-id="125ca-143">[Создание и публикация продукта в службе управления API Azure][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="125ca-143">[How to create and publish a product][How to create and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to create APIs]: api-management-howto-create-apis.md
[How to configure API settings]: api-management-howto-create-apis.md#configure-api-settings
