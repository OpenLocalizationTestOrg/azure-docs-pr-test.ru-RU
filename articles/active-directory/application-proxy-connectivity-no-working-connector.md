---
title: "найти aaaNo рабочая группа соединителя для приложения прокси приложения | Документы Microsoft"
description: "Решать проблемы, которые могут возникнуть при наличии не работе соединителя в группе соединитель для вашего приложения с hello прокси приложения Azure AD"
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
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="92b37-103">Не удается найти рабочую группу соединителей для приложения прокси приложения</span><span class="sxs-lookup"><span data-stu-id="92b37-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="92b37-104">Статьи справки вы tooresolve hello распространенных проблем не обнаружено приложение прокси приложения соединителя интегрированы с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92b37-104">This article help you tooresolve hello common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="92b37-105">Обзор действий</span><span class="sxs-lookup"><span data-stu-id="92b37-105">Overview of steps</span></span>
<span data-ttu-id="92b37-106">Если нет работы соединителя в группе соединитель для вашего приложения, существует несколько способов tooresolve hello проблемы:</span><span class="sxs-lookup"><span data-stu-id="92b37-106">If there is no working Connector in a Connector Group for your application, there are a few ways tooresolve hello problem:</span></span>

-   <span data-ttu-id="92b37-107">Если соединители не в группе hello, вы можете:</span><span class="sxs-lookup"><span data-stu-id="92b37-107">If you have no connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="92b37-108">Загрузить новый соединитель hello правом локального сервера и назначьте его группе toothis</span><span class="sxs-lookup"><span data-stu-id="92b37-108">Download a new Connector on hello right on-prem server, and assign it toothis group</span></span>

    -   <span data-ttu-id="92b37-109">Переместите соединитель active в группу hello</span><span class="sxs-lookup"><span data-stu-id="92b37-109">Move an active Connector into hello group</span></span>

-   <span data-ttu-id="92b37-110">Если нет активных соединителей в группе hello, вы можете:</span><span class="sxs-lookup"><span data-stu-id="92b37-110">If you have no active connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="92b37-111">Определите hello причина, по которой соединителя неактивна и устраните</span><span class="sxs-lookup"><span data-stu-id="92b37-111">Identify hello reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="92b37-112">Переместите соединитель active в группу hello</span><span class="sxs-lookup"><span data-stu-id="92b37-112">Move an active Connector into hello group</span></span>

<span data-ttu-id="92b37-113">tooknow, какой из этих hello проблема, откройте меню «Прокси-сервер приложения» hello в приложении и просмотрите предупреждающее сообщение hello группы соединителей.</span><span class="sxs-lookup"><span data-stu-id="92b37-113">tooknow which of these is hello issue, open hello “Application Proxy” menu in your Application, and look at hello Connector Group warning message.</span></span> <span data-ttu-id="92b37-114">Она указывать нее hello требуется по крайней мере один соединитель (у вас нет в группе hello) или что он не имеет active соединителей (при наличии скорее всего неактивных соединители).</span><span class="sxs-lookup"><span data-stu-id="92b37-114">It specify either that hello group needs at least one Connector (you have none in hello group) or that it has no active Connectors (though you likely have inactive Connectors).</span></span>

   ![Выбор группы соединителей на портале Azure](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="92b37-116">Дополнительные сведения о каждом из этих параметров в разделе hello соответствующего ниже.</span><span class="sxs-lookup"><span data-stu-id="92b37-116">For details on each of these options, see hello corresponding section below.</span></span> <span data-ttu-id="92b37-117">Каждый из них предполагается запускается со страницы управления соединителя hello.</span><span class="sxs-lookup"><span data-stu-id="92b37-117">Each of these assumes that you are starting from hello Connector management page.</span></span> <span data-ttu-id="92b37-118">Если вы видите сообщение hello выше, можно перейти toothis страницу, щелкнув предупреждающее сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="92b37-118">If you are looking at hello error message above, you can go toothis page by clicking on hello warning message.</span></span> <span data-ttu-id="92b37-119">В противном случае ее можно найти, перейдя слишком**Azure Active Directory**, чтобы выбрать **корпоративных приложений**, затем **прокси-сервера приложения.**</span><span class="sxs-lookup"><span data-stu-id="92b37-119">Otherwise this can be found by going too**Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Управление группой соединителей на портале Azure](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="92b37-121">Скачайте новый соединитель</span><span class="sxs-lookup"><span data-stu-id="92b37-121">Download a new Connector</span></span>

<span data-ttu-id="92b37-122">toodownload новый соединитель, используйте кнопку «Загрузить соединитель» hello вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="92b37-122">toodownload a new Connector, use hello “Download Connector” button at hello top of hello page.</span></span>

<span data-ttu-id="92b37-123">Примечание hello соединителя потребностей toobe установлены на компьютере с прямая линия видимости toohello внутреннее приложение и обычно помещается в hello же сервере, что приложение hello.</span><span class="sxs-lookup"><span data-stu-id="92b37-123">note hello Connector needs toobe installed on a machine with direct line of sight toohello backend application, and is typically placed on hello same server as hello application.</span></span> <span data-ttu-id="92b37-124">После загрузки hello соединителя должны появиться в этом меню.</span><span class="sxs-lookup"><span data-stu-id="92b37-124">After downloading, hello Connector should appear in this menu.</span></span> <span data-ttu-id="92b37-125">Щелкните соединитель hello и используйте убедиться, что он принадлежит подходящей группой toohello toomake раскрывающийся список «Группы соединителей» hello.</span><span class="sxs-lookup"><span data-stu-id="92b37-125">click hello Connector, and use hello “Connector Group” drop-down toomake sure it belongs toohello right group.</span></span> <span data-ttu-id="92b37-126">Сохраните изменение hello.</span><span class="sxs-lookup"><span data-stu-id="92b37-126">Save hello change.</span></span>

   ![Загрузить соединитель hello hello портала Azure](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="92b37-128">Переместите активный соединитель</span><span class="sxs-lookup"><span data-stu-id="92b37-128">Move an Active Connector</span></span>

<span data-ttu-id="92b37-129">При наличии активных соединитель, должны принадлежать к группе toohello с прямой видимости toohello целевой серверной части приложения hello соединителя можно переместить в назначенный hello группы.</span><span class="sxs-lookup"><span data-stu-id="92b37-129">If you have an active Connector that should belong toohello group and has line of sight toohello target backend application, you can move hello Connector into hello assigned group.</span></span> <span data-ttu-id="92b37-130">Таким образом, toodo щелкните hello соединителя.</span><span class="sxs-lookup"><span data-stu-id="92b37-130">toodo so, click hello Connector.</span></span> <span data-ttu-id="92b37-131">В поле «Группы соединителей» hello hello раскрывающемся tooselect hello нужной группе и нажмите кнопку Сохранить.</span><span class="sxs-lookup"><span data-stu-id="92b37-131">In hello “Connector Group” field, use hello drop-down tooselect hello correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="92b37-132">Решите проблему с неактивным соединителем</span><span class="sxs-lookup"><span data-stu-id="92b37-132">Resolve an inactive Connector</span></span>

<span data-ttu-id="92b37-133">Если hello только соединителей в hello группы находятся в неактивном состоянии, они, скорее всего на компьютере, который не содержит все необходимые порты hello разблокированы.</span><span class="sxs-lookup"><span data-stu-id="92b37-133">If hello only Connectors in hello group are inactive, they are likely on a machine that does not have all hello necessary ports unblocked.</span></span>

<span data-ttu-id="92b37-134">порты hello в разделе Устранение неполадок документа сведения о изучает эту проблему.</span><span class="sxs-lookup"><span data-stu-id="92b37-134">see hello ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92b37-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="92b37-135">Next steps</span></span>
[<span data-ttu-id="92b37-136">Сведения о соединителях прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="92b37-136">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)


