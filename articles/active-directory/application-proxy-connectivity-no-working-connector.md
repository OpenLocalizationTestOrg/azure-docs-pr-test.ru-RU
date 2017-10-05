---
title: "Не удается найти рабочую группу соединителей для приложения прокси приложения | Документы Майкрософт"
description: "В этой статье описаны проблемы, которые могут возникнуть при отсутствии рабочего соединителя или группы соединителей для приложения прокси приложения."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4945958deedc8a1d9989ff901192c03a5363b4dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="a67a3-103">Не удается найти рабочую группу соединителей для приложения прокси приложения</span><span class="sxs-lookup"><span data-stu-id="a67a3-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="a67a3-104">Эта статья поможет решить распространенные проблемы при отсутствии соединителя для приложения прокси приложения, интегрированного с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a67a3-104">This article help you to resolve the common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="a67a3-105">Обзор действий</span><span class="sxs-lookup"><span data-stu-id="a67a3-105">Overview of steps</span></span>
<span data-ttu-id="a67a3-106">Если для вашего приложения отсутствуют рабочий соединитель или группа соединителей, решить эту проблему можно несколькими способами:</span><span class="sxs-lookup"><span data-stu-id="a67a3-106">If there is no working Connector in a Connector Group for your application, there are a few ways to resolve the problem:</span></span>

-   <span data-ttu-id="a67a3-107">При отсутствии соединителей в группе можно выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a67a3-107">If you have no connectors in the group, you can:</span></span>

    -   <span data-ttu-id="a67a3-108">Скачайте новый соединитель на соответствующий локальный сервер и назначьте его этой группе</span><span class="sxs-lookup"><span data-stu-id="a67a3-108">Download a new Connector on the right on-prem server, and assign it to this group</span></span>

    -   <span data-ttu-id="a67a3-109">Переместите активный соединитель в группу</span><span class="sxs-lookup"><span data-stu-id="a67a3-109">Move an active Connector into the group</span></span>

-   <span data-ttu-id="a67a3-110">При отсутствии активных соединителей в группе можно выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a67a3-110">If you have no active connectors in the group, you can:</span></span>

    -   <span data-ttu-id="a67a3-111">Определите причину, по которой соединитель не активен, и устраните ее</span><span class="sxs-lookup"><span data-stu-id="a67a3-111">Identify the reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="a67a3-112">Переместите активный соединитель в группу</span><span class="sxs-lookup"><span data-stu-id="a67a3-112">Move an active Connector into the group</span></span>

<span data-ttu-id="a67a3-113">Чтобы узнать, какая из приведенных проблем возникла в вашем случае, откройте меню "Прокси приложения" в приложении и просмотрите предупреждение, связанное с группой соединителей.</span><span class="sxs-lookup"><span data-stu-id="a67a3-113">To know which of these is the issue, open the “Application Proxy” menu in your Application, and look at the Connector Group warning message.</span></span> <span data-ttu-id="a67a3-114">В нем указано, что в группе должен быть по крайней мере один соединитель (это означает, что в группе нет ни одного соединителя) или что активные соединители отсутствуют (это означает, что скорее всего у вас есть неактивные соединители).</span><span class="sxs-lookup"><span data-stu-id="a67a3-114">It specify either that the group needs at least one Connector (you have none in the group) or that it has no active Connectors (though you likely have inactive Connectors).</span></span>

   ![Выбор группы соединителей на портале Azure](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="a67a3-116">Сведения о каждом из этих вариантов см. в соответствующем разделе ниже.</span><span class="sxs-lookup"><span data-stu-id="a67a3-116">For details on each of these options, see the corresponding section below.</span></span> <span data-ttu-id="a67a3-117">В каждом из них нужно начать со страницы управления соединителями.</span><span class="sxs-lookup"><span data-stu-id="a67a3-117">Each of these assumes that you are starting from the Connector management page.</span></span> <span data-ttu-id="a67a3-118">Если у вас есть сообщение об ошибке, то можно щелкнуть по нему, чтобы перейти на эту страницу.</span><span class="sxs-lookup"><span data-stu-id="a67a3-118">If you are looking at the error message above, you can go to this page by clicking on the warning message.</span></span> <span data-ttu-id="a67a3-119">В противном случае перейдите в **Azure Active Directory**, щелкните **Корпоративные приложения** и затем **Прокси приложения**.</span><span class="sxs-lookup"><span data-stu-id="a67a3-119">Otherwise this can be found by going to **Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Управление группой соединителей на портале Azure](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="a67a3-121">Скачайте новый соединитель</span><span class="sxs-lookup"><span data-stu-id="a67a3-121">Download a new Connector</span></span>

<span data-ttu-id="a67a3-122">Чтобы скачать новый соединитель, нажмите кнопку "Скачать соединитель" в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="a67a3-122">To download a new Connector, use the “Download Connector” button at the top of the page.</span></span>

<span data-ttu-id="a67a3-123">Обратите внимание, что соединитель нужно установить на компьютере, находящемся в прямой видимости для серверного приложения, и обычно соединитель размещается на том же сервере, что и приложение.</span><span class="sxs-lookup"><span data-stu-id="a67a3-123">note the Connector needs to be installed on a machine with direct line of sight to the backend application, and is typically placed on the same server as the application.</span></span> <span data-ttu-id="a67a3-124">После загрузки соединитель должен появиться в этом меню.</span><span class="sxs-lookup"><span data-stu-id="a67a3-124">After downloading, the Connector should appear in this menu.</span></span> <span data-ttu-id="a67a3-125">Щелкните соединитель и укажите соответствующую группу соединителя в раскрывающемся списке "Группа соединителя".</span><span class="sxs-lookup"><span data-stu-id="a67a3-125">click the Connector, and use the “Connector Group” drop-down to make sure it belongs to the right group.</span></span> <span data-ttu-id="a67a3-126">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="a67a3-126">Save the change.</span></span>

   ![Скачайте соединитель на портале Azure](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="a67a3-128">Переместите активный соединитель</span><span class="sxs-lookup"><span data-stu-id="a67a3-128">Move an Active Connector</span></span>

<span data-ttu-id="a67a3-129">Если у вас есть активный соединитель, который должен принадлежать к группе и находится в прямой видимости для серверного приложения, можно перенести соединитель в назначенную группу.</span><span class="sxs-lookup"><span data-stu-id="a67a3-129">If you have an active Connector that should belong to the group and has line of sight to the target backend application, you can move the Connector into the assigned group.</span></span> <span data-ttu-id="a67a3-130">Для этого щелкните соединитель.</span><span class="sxs-lookup"><span data-stu-id="a67a3-130">To do so, click the Connector.</span></span> <span data-ttu-id="a67a3-131">В раскрывающемся списке "Группа соединителя" выберите соответствующую группу и нажмите кнопку "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="a67a3-131">In the “Connector Group” field, use the drop-down to select the correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="a67a3-132">Решите проблему с неактивным соединителем</span><span class="sxs-lookup"><span data-stu-id="a67a3-132">Resolve an inactive Connector</span></span>

<span data-ttu-id="a67a3-133">Если только соединители группы неактивны, скорее всего на компьютере, на котором они находятся, открыты не все необходимые порты.</span><span class="sxs-lookup"><span data-stu-id="a67a3-133">If the only Connectors in the group are inactive, they are likely on a machine that does not have all the necessary ports unblocked.</span></span>

<span data-ttu-id="a67a3-134">Дополнительные сведения о решении этой проблемы см. в документе "Решение проблем с портами".</span><span class="sxs-lookup"><span data-stu-id="a67a3-134">see the ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a67a3-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a67a3-135">Next steps</span></span>
[<span data-ttu-id="a67a3-136">Сведения о соединителях прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="a67a3-136">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)


