---
title: "Что произошло с моим проектом ASP.NET 5 (подключенные службы Visual Studio) | Документация Майкрософт"
description: "Сведения о том, что происходит после подключения к учетной записи хранения Azure в проекте Visual Studio ASP.NET 5 с помощью подключенных служб Visual Studio"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: e7caa9fa-c780-45eb-a546-299fc1c68455
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 2a25c24fd7625374d269622a805f386fcd52bb5f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-aspnet-5-project-visual-studio-azure-storage-connected-services"></a><span data-ttu-id="acd25-103">Что произошло с моим проектом ASP.NET 5 (подключенными к службе хранилища Azure службами Visual Studio)?</span><span class="sxs-lookup"><span data-stu-id="acd25-103">What happened to my ASP.NET 5 project (Visual Studio Azure Storage connected services)?</span></span>
## <a name="references-added"></a><span data-ttu-id="acd25-104">Добавлены ссылки</span><span class="sxs-lookup"><span data-stu-id="acd25-104">References added</span></span>
<span data-ttu-id="acd25-105">Пакет NuGet хранилища Azure был добавлен в проект Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="acd25-105">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="acd25-106">Этот пакет добавляет следующие ссылки .NET:</span><span class="sxs-lookup"><span data-stu-id="acd25-106">This package adds the following .NET references:</span></span>

* <span data-ttu-id="acd25-107">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="acd25-107">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="acd25-108">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="acd25-108">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="acd25-109">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="acd25-109">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="acd25-110">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="acd25-110">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="acd25-111">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="acd25-111">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="acd25-112">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="acd25-112">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="acd25-113">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="acd25-113">**System.Data**</span></span>
* <span data-ttu-id="acd25-114">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="acd25-114">**System.Spatial**</span></span>

<span data-ttu-id="acd25-115">Кроме того, добавлен пакет NuGet **Microsoft.Framework.Configuration.Json** .</span><span class="sxs-lookup"><span data-stu-id="acd25-115">Also, the NuGet package **Microsoft.Framework.Configuration.Json** was added.</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="acd25-116">Добавлена строка подключения к хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="acd25-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="acd25-117">В файле config.json проекта был создан элемент с ключом и строкой подключения выбранной учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="acd25-117">In the config.json file of your project, an element was created with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="acd25-118">Дополнительные сведения см. на сайте [ASP.NET 5](http://www.asp.net/vnext).</span><span class="sxs-lookup"><span data-stu-id="acd25-118">For more information, see [ASP.NET 5](http://www.asp.net/vnext).</span></span>

