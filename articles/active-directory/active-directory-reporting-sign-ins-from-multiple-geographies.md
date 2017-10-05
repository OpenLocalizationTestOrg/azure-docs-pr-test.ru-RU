---
title: "Операции входа из нескольких географических регионов"
description: "В этом отчете содержится информация о пользователях, от имени которых были совершены две попытки входа из разных регионов, причем времени между этими попытками было недостаточно, чтобы пользователь мог добраться из одного региона в другой."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: 79259c8a-2388-4747-b41e-c07434ea9a02
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 1de57f64692ade442f9ef8d1e3b587ffee35d7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-multiple-geographies"></a><span data-ttu-id="00588-103">"Операции входа из нескольких географических регионов".</span><span class="sxs-lookup"><span data-stu-id="00588-103">Sign-ins from multiple geographies</span></span>
<span data-ttu-id="00588-104">В этом отчете содержится информация об успешных попытках входа пользователя, от имени которого были совершены две попытки входа из разных регионов, причем времени между этими попытками было недостаточно, чтобы пользователь мог добраться из одного региона в другой.</span><span class="sxs-lookup"><span data-stu-id="00588-104">This report includes successful sign-ins from a user where two sign-ins appeared to originate from different regions and the time between the sign-ins makes it impossible for the user to have traveled between those regions.</span></span> <span data-ttu-id="00588-105">Возможные причины:</span><span class="sxs-lookup"><span data-stu-id="00588-105">Possible causes include:</span></span>

* <span data-ttu-id="00588-106">пользователь использует пароль совместно с другими пользователями;</span><span class="sxs-lookup"><span data-stu-id="00588-106">User is sharing their password with other users</span></span>
* <span data-ttu-id="00588-107">для входа пользователь запускает браузер с помощью удаленного рабочего стола;</span><span class="sxs-lookup"><span data-stu-id="00588-107">User is using a remote desktop to launch a web browser for sign-in</span></span>
* <span data-ttu-id="00588-108">злоумышленник вошел в учетную запись пользователя из другой страны;</span><span class="sxs-lookup"><span data-stu-id="00588-108">A hacker has signed in to the account of a user from a different country</span></span>
* <span data-ttu-id="00588-109">пользователь использует VPN или прокси-сервер;</span><span class="sxs-lookup"><span data-stu-id="00588-109">User is using a VPN or proxy</span></span>
* <span data-ttu-id="00588-110">пользователь выполнил вход сразу с нескольких устройств, например настольного ПК и мобильного телефона, и IP-адрес мобильного телефона необычен.</span><span class="sxs-lookup"><span data-stu-id="00588-110">User is signed in from multiple devices at the same time, such as a desktop and a mobile phone, and the IP address of the mobile phone is unusual.</span></span>

<span data-ttu-id="00588-111">В результатах этого отчета отображаются события успешного входа, время между входами, регионы, из которых предположительно они были выполнены, и примерное время перемещения между этими регионами.</span><span class="sxs-lookup"><span data-stu-id="00588-111">Results from this report will show you the successful sign-in events, together with the time between the sign-ins, the regions where the sign-ins appeared to originate from, and the estimated travel time between those regions.</span></span> <span data-ttu-id="00588-112">Показанное время представляет собой только оценочное значение и может отличаться от фактического времени перемещения между расположениями.</span><span class="sxs-lookup"><span data-stu-id="00588-112">The travel time shown is only an estimate and may be different from the actual travel time between the locations.</span></span>

![Операции входа из нескольких географических регионов](./media/active-directory-reporting-sign-ins-from-multiple-geographies/signInsFromMultipleGeographies.PNG)

