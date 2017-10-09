---
title: "брандмауэр aaaHow tooopen hello порты, необходимые для приложения прокси приложения | Документы Microsoft"
description: "Правильно определить какие порты tooopen для toowork прокси приложения hello Azure AD"
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
ms.openlocfilehash: cdc7badb7c15591689a3bfd6bb26da182b00fb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-hello-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="28186-103">Как tooopen hello порты брандмауэра, необходимые для приложения прокси приложения</span><span class="sxs-lookup"><span data-stu-id="28186-103">How tooopen hello firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="28186-104">Полный список hello необходимые порты и функции hello каждого порта toosee разделе hello необходимые компоненты hello [документации прокси-сервера приложения](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span><span class="sxs-lookup"><span data-stu-id="28186-104">toosee a full list of hello required ports and hello function of each port, see hello prerequisites section of hello [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="28186-105">Обратите внимание, что прокси приложения использует только исходящие порты.</span><span class="sxs-lookup"><span data-stu-id="28186-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="28186-106">Можно также проверить, имеют ли все открытые порты hello необходимые путем открытия hello [средство тестирования порты соединитель](https://aadap-portcheck.connectorporttest.msappproxy.net/) из локальной сети.</span><span class="sxs-lookup"><span data-stu-id="28186-106">You can also check whether you have all hello required ports open by opening hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="28186-107">Большее число зеленых флажков означает большую устойчивость.</span><span class="sxs-lookup"><span data-stu-id="28186-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="28186-108">Регионы прокси приложения</span><span class="sxs-lookup"><span data-stu-id="28186-108">App Proxy regions</span></span>

<span data-ttu-id="28186-109">Мы работаем над toolet можно узнать, какие из этих областей требуется toobe зеленый для вас образом.</span><span class="sxs-lookup"><span data-stu-id="28186-109">We are working on a way toolet you know which of these regions needs toobe green for you.</span></span> <span data-ttu-id="28186-110">Пока убедитесь, что все регионы выделены зеленым цветом.</span><span class="sxs-lookup"><span data-stu-id="28186-110">For now, make sure they all are.</span></span> <span data-ttu-id="28186-111">Регион "Центральная часть США" должен быть выделен зеленым цветом независимо от того, в каком регионе вы находитесь.</span><span class="sxs-lookup"><span data-stu-id="28186-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="28186-112">предоставляет hello средство toomake для убедиться, что hello правильные результаты быть убедитесь, что:</span><span class="sxs-lookup"><span data-stu-id="28186-112">toomake sure hello tool gives you hello right results, be sure to:</span></span>

-   <span data-ttu-id="28186-113">Откройте средство hello в браузере с сервера hello, где установлен соединитель hello.</span><span class="sxs-lookup"><span data-stu-id="28186-113">Open hello tool on a browser from hello server where you have installed hello Connector.</span></span>

-   <span data-ttu-id="28186-114">Убедитесь, что все прокси-серверы или брандмауэры tooyour применимо, соединитель, также применены toothis страницы.</span><span class="sxs-lookup"><span data-stu-id="28186-114">Ensure that any proxies or firewalls applicable tooyour Connector are also applied toothis page.</span></span> <span data-ttu-id="28186-115">Это можно сделать в Internet Explorer, перейдя слишком**параметры**  - &gt; **обозревателя**  - &gt; **подключений**  - &gt; **Параметры локальной сети**.</span><span class="sxs-lookup"><span data-stu-id="28186-115">This can be done in Internet Explorer by going too**Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="28186-116">На этой странице вы видите hello поле «Использовать прокси-сервера сервера для ЛС».</span><span class="sxs-lookup"><span data-stu-id="28186-116">On this page, you see hello field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="28186-117">Установите этот флажок и поместите hello адрес прокси-сервера в поле «Адрес» hello.</span><span class="sxs-lookup"><span data-stu-id="28186-117">Select this box, and put hello proxy address into hello “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28186-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="28186-118">Next steps</span></span>
[<span data-ttu-id="28186-119">Сведения о соединителях прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="28186-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
