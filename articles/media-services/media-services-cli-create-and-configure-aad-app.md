---
title: "Создание приложения Azure AD и его настройка для доступа к API служб мультимедиа Azure с помощью Azure CLI 2.0 | Документация Майкрософт"
description: "В этом разделе описывается, как создать и настроить приложение Azure AD для доступа к API служб мультимедиа Azure с помощью Azure CLI 2.0."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 01a2bb6d99776feec936315bc882c3097ce832d4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-cli-20-to-create-an-aad-app-and-configure-it-to-access-azure-media-services-api"></a><span data-ttu-id="1ed6d-103">Создание и настройка приложения Azure AD для доступа к API служб мультимедиа Azure с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1ed6d-103">Use CLI 2.0 to create an AAD app and configure it to access Azure Media Services API</span></span>

<span data-ttu-id="1ed6d-104">В этом разделе показано, как с помощью Azure CLI 2.0 создать приложение Azure Active Directory (Azure AD) и участник-службу для доступа к ресурсам служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="1ed6d-104">This topic shows you how to use CLI 2.0 to create an Azure Active Directory (Azure AD) application and service principal to access Azure Media Services resources.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1ed6d-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1ed6d-105">Prerequisites</span></span>

- <span data-ttu-id="1ed6d-106">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="1ed6d-106">An Azure account.</span></span> <span data-ttu-id="1ed6d-107">Дополнительные сведения см. на странице с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1ed6d-107">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="1ed6d-108">Учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="1ed6d-108">A Media Services account.</span></span> <span data-ttu-id="1ed6d-109">Дополнительные сведения см. в статье [Создание учетной записи служб мультимедиа Azure с помощью портала Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="1ed6d-109">For more information, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>

## <a name="use-the-azure-cloud-shell"></a><span data-ttu-id="1ed6d-110">Использование Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="1ed6d-110">Use the Azure Cloud Shell</span></span>

1. <span data-ttu-id="1ed6d-111">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1ed6d-111">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1ed6d-112">Запустите Cloud Shell с помощью верхней области навигации портала.</span><span class="sxs-lookup"><span data-stu-id="1ed6d-112">Launch the Cloud Shell from the upper navigation pane of the portal.</span></span>

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

<span data-ttu-id="1ed6d-114">Дополнительные сведения см. в [обзоре Azure Cloud Shell](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="1ed6d-114">For more information, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md).</span></span>

## <a name="create-an-azure-ad-app-and-configure-access-to-the-media-account-with-cli-20"></a><span data-ttu-id="1ed6d-115">Создание приложения Azure AD и настройка доступа к учетной записи служб мультимедиа с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1ed6d-115">Create an Azure AD app and configure access to the media account with CLI 2.0</span></span>
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

<span data-ttu-id="1ed6d-116">Например:</span><span class="sxs-lookup"><span data-stu-id="1ed6d-116">For example:</span></span>

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

<span data-ttu-id="1ed6d-117">В этом примере **область** — полный путь к ресурсу учетной записи служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="1ed6d-117">In this example, the **scope** is the full resource path for the media services account.</span></span> <span data-ttu-id="1ed6d-118">Однако **область** может быть задана на любом уровне.</span><span class="sxs-lookup"><span data-stu-id="1ed6d-118">However, the **scope** can be at any level.</span></span>

<span data-ttu-id="1ed6d-119">Например, ее можно задать на одном из следующих уровней:</span><span class="sxs-lookup"><span data-stu-id="1ed6d-119">For example, it could be one of the following levels:</span></span>
 
* <span data-ttu-id="1ed6d-120">**подписка**;</span><span class="sxs-lookup"><span data-stu-id="1ed6d-120">The **subscription** level.</span></span>
* <span data-ttu-id="1ed6d-121">**группа ресурсов**;</span><span class="sxs-lookup"><span data-stu-id="1ed6d-121">The **resource group** level.</span></span>
* <span data-ttu-id="1ed6d-122">**ресурс** (например, учетная запись служб мультимедиа).</span><span class="sxs-lookup"><span data-stu-id="1ed6d-122">The **resource** level (for example, a Media account).</span></span>

<span data-ttu-id="1ed6d-123">Дополнительные сведения см. в статье [Создание субъекта-службы Azure с помощью Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1ed6d-123">For more information, see [Create an Azure service principal with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

<span data-ttu-id="1ed6d-124">Ознакомьтесь также с разделом [Управление доступом на основе ролей с помощью интерфейса командной строки Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="1ed6d-124">Also see [Manage Role-Based Access Control with the Azure command-line interface](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1ed6d-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1ed6d-125">Next steps</span></span>

<span data-ttu-id="1ed6d-126">Приступите к [передаче файлов в учетную запись](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="1ed6d-126">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span></span>
