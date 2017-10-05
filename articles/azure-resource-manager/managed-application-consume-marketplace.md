---
title: "Использование управляемого приложения Azure в Marketplace | Документация Майкрософт"
description: "В этой статье объясняется, как создать управляемое приложение Azure, которое будет доступно в Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: baf456740bddd562391ed64d707f990c8921d710
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="consume-azure-managed-applications-in-the-marketplace"></a><span data-ttu-id="ce1d8-103">Использование управляемых приложений Azure в Marketplace</span><span class="sxs-lookup"><span data-stu-id="ce1d8-103">Consume Azure managed applications in the Marketplace</span></span>

<span data-ttu-id="ce1d8-104">Как обсуждалось в статье [Обзор управляемых приложений Azure](managed-application-overview.md), существует два сценария работы с управляемыми приложениями:</span><span class="sxs-lookup"><span data-stu-id="ce1d8-104">As discussed in the [Managed Application overview](managed-application-overview.md) article, there are two scenarios in the end to end experience.</span></span> <span data-ttu-id="ce1d8-105">первый — для издателя или поставщика, желающего создать управляемое приложение и предоставить его пользователям,</span><span class="sxs-lookup"><span data-stu-id="ce1d8-105">One is the publisher or vendor who wants to create a managed application for use by customers.</span></span> <span data-ttu-id="ce1d8-106">и второй — для пользователя, использующего управляемое приложение.</span><span class="sxs-lookup"><span data-stu-id="ce1d8-106">The second is the end customer or the consumer of the managed application.</span></span> <span data-ttu-id="ce1d8-107">Эта статья посвящена второму сценарию.</span><span class="sxs-lookup"><span data-stu-id="ce1d8-107">This article covers the second scenario.</span></span> <span data-ttu-id="ce1d8-108">В ней описывается, как можно развернуть управляемое приложение из Microsoft Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ce1d8-108">It describes how you can deploy a managed application from the Microsoft Azure Marketplace.</span></span>

## <a name="create-from-the-marketplace"></a><span data-ttu-id="ce1d8-109">Создание из Marketplace</span><span class="sxs-lookup"><span data-stu-id="ce1d8-109">Create from the Marketplace</span></span>

<span data-ttu-id="ce1d8-110">Управляемое приложение развертывается из Marketplace аналогично развертыванию любого типа ресурсов из Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ce1d8-110">Deploying a managed application from the Marketplace is similar to deploying any type of resources from the Marketplace.</span></span> 

<span data-ttu-id="ce1d8-111">На портале выберите **+ Создать** и найдите тип решения, которое следует развернуть.</span><span class="sxs-lookup"><span data-stu-id="ce1d8-111">In the portal, select **+ New** and search for the type of solution to deploy.</span></span> <span data-ttu-id="ce1d8-112">Из доступных вариантов выберите тот, который вам нужен.</span><span class="sxs-lookup"><span data-stu-id="ce1d8-112">From the available options, select the one you need.</span></span>

![Поиск решений](./media/managed-application-consume-marketplace/search-apps.png)

<span data-ttu-id="ce1d8-114">Просмотрите сводку приложения и выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ce1d8-114">Review the summary of the application, and select **Create**.</span></span>

![Создание управляемого приложения](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

<span data-ttu-id="ce1d8-116">Как и в любом другом решении, отобразятся поля, в которых следует указать значения.</span><span class="sxs-lookup"><span data-stu-id="ce1d8-116">Like any other solution, you are presented with fields to provide values for.</span></span> <span data-ttu-id="ce1d8-117">Эти поля различаются в зависимости от типа управляемого приложения, которое создается.</span><span class="sxs-lookup"><span data-stu-id="ce1d8-117">These fields vary by the type of managed application you create.</span></span> 

## <a name="view-support-information"></a><span data-ttu-id="ce1d8-118">Просмотр сведений о поддержке</span><span class="sxs-lookup"><span data-stu-id="ce1d8-118">View support information</span></span>

<span data-ttu-id="ce1d8-119">После того как управляемое приложение будет развернуто, просмотрите сведения о его поддержке.</span><span class="sxs-lookup"><span data-stu-id="ce1d8-119">After your managed application has deployed, view the support information for the application.</span></span> <span data-ttu-id="ce1d8-120">Сведения о поддержке перечисляются в колонке управляемого приложения.</span><span class="sxs-lookup"><span data-stu-id="ce1d8-120">In the managed application blade, the support information is listed.</span></span>

![support](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a><span data-ttu-id="ce1d8-122">Просмотр разрешений издателя</span><span class="sxs-lookup"><span data-stu-id="ce1d8-122">View publisher permissions</span></span>

<span data-ttu-id="ce1d8-123">Поставщику, который управляет вашим приложением, предоставляется доступ к вашим ресурсам.</span><span class="sxs-lookup"><span data-stu-id="ce1d8-123">The vendor that manages your application is granted access to your resources.</span></span> <span data-ttu-id="ce1d8-124">Чтобы просмотреть эти разрешения, выберите **Авторизации**.</span><span class="sxs-lookup"><span data-stu-id="ce1d8-124">To see those permissions, select **Authorizations**.</span></span>

![Авторизации](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a><span data-ttu-id="ce1d8-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ce1d8-126">Next steps</span></span>

* <span data-ttu-id="ce1d8-127">Сведения о публикации управляемого приложения в Marketplace см. в статье [Azure managed applications in the Marketplace](managed-application-author-marketplace.md) (Управляемые приложения Azure в Marketplace).</span><span class="sxs-lookup"><span data-stu-id="ce1d8-127">For information about publishing a managed application in the Marketplace, see [Azure Managed Applications in Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="ce1d8-128">Сведения о публикации управляемых приложений, которые доступны только пользователям вашей организации, см. в статье [Создание и публикация управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="ce1d8-128">To publish managed applications that are only available to users in your organization, see [Create and publish Service Catalog Managed Application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="ce1d8-129">Сведения об использовании управляемых приложений, которые доступны только пользователям вашей организации, см. в статье [Использование управляемого приложения Azure](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="ce1d8-129">To consume managed applications that are only available to users in your organization, see [Consume a Service Catalog Managed Application](managed-application-consumption.md).</span></span>