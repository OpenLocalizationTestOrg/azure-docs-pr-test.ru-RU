---
title: "Операции входа из неизвестных источников"
description: "Отчет, в котором указываются пользователи, успешно выполнившие вход в каталог, используя анонимный IP-адрес прокси-сервера."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: 2f045543-1578-4972-bf70-b35310f23110
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 90006121e4b3392f6e3ecffb4a56aca330feb02f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-unknown-sources"></a><span data-ttu-id="0eafe-103">Операции входа из неизвестных источников</span><span class="sxs-lookup"><span data-stu-id="0eafe-103">Sign ins from unknown sources</span></span>
<span data-ttu-id="0eafe-104">В этом отчете указываются пользователи, которые успешно выполнили вход в ваш каталог, при этом им назначен IP-адрес клиента, который распознается корпорацией Майкрософт как IP-адрес анонимного прокси-сервера (например, IP-адрес Tor).</span><span class="sxs-lookup"><span data-stu-id="0eafe-104">This report indicates users who have successfully signed in to your directory while assigned a client IP address that has been recognized by Microsoft as an anonymous proxy IP address (for example, a Tor IP address).</span></span> <span data-ttu-id="0eafe-105">Пользователи часто используют эти прокси-серверы, чтобы скрыть IP-адреса своих компьютеров. Иногда их используют злоумышленники.</span><span class="sxs-lookup"><span data-stu-id="0eafe-105">These proxies are often used by users that want to hide their computer’s IP address, and may be used for malicious intent.</span></span>

<span data-ttu-id="0eafe-106">В результатах этого отчета отображается количество успешных операций входа пользователя в ваш каталог со своего адреса и с IP-адреса прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="0eafe-106">Results from this report will show the number of times a user successfully signed in to your directory from that address and the proxy’s IP address.</span></span>

![Операции входа из неизвестных источников](./media/active-directory-reporting-sign-ins-from-unknown-sources/signInsFromUnknownSources.PNG)

