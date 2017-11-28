---
title: "Что произошло с моим проектом облачных служб? | Документация Майкрософт"
description: "Сведения о том, что происходит в проекте облачных служб после подключения к учетной записи хранения Azure с помощью подключенных служб Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: ca0ea68d-f417-4ce8-9413-40d76f69cdea
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 4e0d4864c2fad624fbde39080146dc62ebebff09
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="what-happened-to-my-cloud-services-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="19f76-104">Что произошло с моим проектом облачных служб (подключенными к службе хранилища Azure службами Visual Studio)?</span><span class="sxs-lookup"><span data-stu-id="19f76-104">What happened to my cloud services project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="19f76-105">Добавлены ссылки</span><span class="sxs-lookup"><span data-stu-id="19f76-105">References added</span></span>
<span data-ttu-id="19f76-106">Пакет NuGet хранилища Azure был добавлен в проект Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19f76-106">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="19f76-107">Этот пакет добавляет следующие ссылки .NET:</span><span class="sxs-lookup"><span data-stu-id="19f76-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="19f76-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="19f76-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="19f76-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="19f76-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="19f76-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="19f76-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="19f76-111">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="19f76-111">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="19f76-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="19f76-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="19f76-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="19f76-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="19f76-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="19f76-114">**System.Data**</span></span>
* <span data-ttu-id="19f76-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="19f76-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="19f76-116">Добавлена строка подключения к хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="19f76-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="19f76-117">Созданы элементы с ключом и строкой подключения выбранной учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="19f76-117">Elements were created with the selected storage account's connection string and key.</span></span> <span data-ttu-id="19f76-118">Внесены изменения в следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="19f76-118">Modifications were made to the following files:</span></span>

* <span data-ttu-id="19f76-119">**ServiceDefinition.csdef**</span><span class="sxs-lookup"><span data-stu-id="19f76-119">**ServiceDefinition.csdef**</span></span>
* <span data-ttu-id="19f76-120">**ServiceConfiguration.Cloud.cscfg**</span><span class="sxs-lookup"><span data-stu-id="19f76-120">**ServiceConfiguration.Cloud.cscfg**</span></span>
* <span data-ttu-id="19f76-121">**ServiceConfiguration.Local.cscfg**</span><span class="sxs-lookup"><span data-stu-id="19f76-121">**ServiceConfiguration.Local.cscfg**</span></span>

