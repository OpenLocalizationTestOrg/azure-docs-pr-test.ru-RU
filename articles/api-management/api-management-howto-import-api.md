---
title: "aaaImport API в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как tooimport API и операций в API управления Azure."
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
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="ac053-103">Как tooimport hello определение API и операций в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="ac053-103">How tooimport hello definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="ac053-104">В службе управления API можно создать новые интерфейсы API и операции hello добавлять вручную или hello API могут быть импортированы вместе с операциями hello за один шаг.</span><span class="sxs-lookup"><span data-stu-id="ac053-104">In API Management, new APIs can be created and hello operations added manually, or hello API can be imported along with hello operations in one step.</span></span>

<span data-ttu-id="ac053-105">API-интерфейсы и связанных с ними операций можно импортировать с помощью hello следующие форматы.</span><span class="sxs-lookup"><span data-stu-id="ac053-105">APIs and their operations can be imported using hello following formats.</span></span>

* <span data-ttu-id="ac053-106">WADL</span><span class="sxs-lookup"><span data-stu-id="ac053-106">WADL</span></span>
* <span data-ttu-id="ac053-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="ac053-107">Swagger</span></span>

<span data-ttu-id="ac053-108">В этом руководстве показано, как создать новый API и импортировать его операции за один шаг.</span><span class="sxs-lookup"><span data-stu-id="ac053-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="ac053-109">Сведения для создания вручную API и добавление операций в разделе [как toocreate API-интерфейсы] [ How toocreate APIs] и [как tooan tooadd операций API] [ How tooadd operations tooan API].</span><span class="sxs-lookup"><span data-stu-id="ac053-109">For information on manually creating an API and adding operations, see [How toocreate APIs][How toocreate APIs] and [How tooadd operations tooan API][How tooadd operations tooan API].</span></span>

## <span data-ttu-id="ac053-110"><a name="import-api"> </a>Импорт API</span><span class="sxs-lookup"><span data-stu-id="ac053-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="ac053-111">API-интерфейсы создаются и настраиваются на портале hello издателя.</span><span class="sxs-lookup"><span data-stu-id="ac053-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="ac053-112">tooaccess hello издателя, щелкните **портал издателя** в hello портала Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="ac053-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="ac053-113">Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.</span><span class="sxs-lookup"><span data-stu-id="ac053-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Портал издателя][api-management-management-console]

<span data-ttu-id="ac053-115">Нажмите кнопку **API-интерфейсы** из hello **API управления** меню hello слева, а затем нажмите **импорта API**.</span><span class="sxs-lookup"><span data-stu-id="ac053-115">Click **APIs** from hello **API Management** menu on hello left, and then click **import API**.</span></span>

![Импортировать API][api-management-import-apis]

<span data-ttu-id="ac053-117">Hello **импорта API** окно имеет три вкладки, которые соответствуют toohello тремя способами tooprovide hello API спецификации.</span><span class="sxs-lookup"><span data-stu-id="ac053-117">hello **Import API** window has three tabs that correspond toohello three ways tooprovide hello API specification.</span></span>

* <span data-ttu-id="ac053-118">**Из буфера обмена** позволяет toopaste hello API спецификации в hello указанного текстового поля.</span><span class="sxs-lookup"><span data-stu-id="ac053-118">**From clipboard** allows you toopaste hello API specification into hello designated text box.</span></span>
* <span data-ttu-id="ac053-119">**Из файла** позволяет toobrowse tooand hello, выберите файл, содержащий спецификацию hello API.</span><span class="sxs-lookup"><span data-stu-id="ac053-119">**From file** allows you toobrowse tooand select hello file that contains hello API specification.</span></span>
* <span data-ttu-id="ac053-120">**С URL-адреса** позволяет спецификации toohello toosupply hello URL-адрес для hello API.</span><span class="sxs-lookup"><span data-stu-id="ac053-120">**From URL** allows you toosupply hello URL toohello specification for hello API.</span></span>

![Формат импорта API][api-management-import-api-clipboard]

<span data-ttu-id="ac053-122">После предоставления hello API спецификации, используйте переключатели hello hello правой tooindicate hello спецификации формата.</span><span class="sxs-lookup"><span data-stu-id="ac053-122">After providing hello API specification, use hello radio buttons on hello right tooindicate hello specification format.</span></span> <span data-ttu-id="ac053-123">поддерживаются следующие форматы Hello.</span><span class="sxs-lookup"><span data-stu-id="ac053-123">hello following formats are supported.</span></span>

* <span data-ttu-id="ac053-124">WADL</span><span class="sxs-lookup"><span data-stu-id="ac053-124">WADL</span></span>
* <span data-ttu-id="ac053-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="ac053-125">Swagger</span></span>

<span data-ttu-id="ac053-126">Затем, введите **Суффикс URL-адреса веб-API**.</span><span class="sxs-lookup"><span data-stu-id="ac053-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="ac053-127">Это присоединенных toohello базовый URL-адрес для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="ac053-127">This is appended toohello base URL for your API management service.</span></span> <span data-ttu-id="ac053-128">Hello базовый URL-адрес является общим для всех интерфейсов API, размещенных на каждом экземпляре служб управления API.</span><span class="sxs-lookup"><span data-stu-id="ac053-128">hello base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="ac053-129">API управления API-интерфейсы отличает их суффикс и поэтому должно быть уникальным для каждый API в конкретном экземпляре служб управления API суффикс hello.</span><span class="sxs-lookup"><span data-stu-id="ac053-129">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="ac053-130">После ввода всех значений нажмите кнопку **Сохранить** toocreate hello API и hello связанные операции.</span><span class="sxs-lookup"><span data-stu-id="ac053-130">Once all values are entered, click **Save** toocreate hello API and hello associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="ac053-131">Инструкции по импорту API базового калькулятора в формате Swagger см. в статье [Начало работы со службой управления Azure API](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ac053-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="ac053-132"><a name="export-api"> </a> Экспорт API</span><span class="sxs-lookup"><span data-stu-id="ac053-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="ac053-133">В дополнение tooimporting новые интерфейсы API, можно экспортировать определения hello собственные интерфейсы API из портала издателя hello.</span><span class="sxs-lookup"><span data-stu-id="ac053-133">In addition tooimporting new APIs, you can export hello definitions of your APIs from hello publisher portal.</span></span> <span data-ttu-id="ac053-134">toodo таким образом, нажмите кнопку **экспорта API** из hello **вкладка со сводкой** из вашего **API**.</span><span class="sxs-lookup"><span data-stu-id="ac053-134">toodo so, click **Export API** from hello **Summary tab** of your **API**.</span></span>

![Экспорт API][api-management-export-api]

<span data-ttu-id="ac053-136">Интерфейсы API можно экспортировать в формате WADL или Swagger.</span><span class="sxs-lookup"><span data-stu-id="ac053-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="ac053-137">Выберите нужный формат hello, щелкните **Сохранить**и выберите местоположение hello в какой файл toosave hello.</span><span class="sxs-lookup"><span data-stu-id="ac053-137">Select hello desired format, click **Save**, and choose hello location in which toosave hello file.</span></span>

![Формат экспорта API][api-management-export-api-format]

## <span data-ttu-id="ac053-139"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ac053-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="ac053-140">После создания API и hello операции импорта, можно просмотреть и настроить дополнительные параметры, добавьте tooa hello API продукта и опубликовать его, чтобы он был доступен для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="ac053-140">Once an API is created and hello operations imported, you can review and configure any additional settings, add hello API tooa Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="ac053-141">Дополнительные сведения см. в разделе hello следующие руководства.</span><span class="sxs-lookup"><span data-stu-id="ac053-141">For more information, see hello following guides.</span></span>

* <span data-ttu-id="ac053-142">[Как параметры tooconfigure API][How tooconfigure API settings]</span><span class="sxs-lookup"><span data-stu-id="ac053-142">[How tooconfigure API settings][How tooconfigure API settings]</span></span>
* <span data-ttu-id="ac053-143">[Как toocreate и публикация продукта][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="ac053-143">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings
