---
title: "Как открыть порты брандмауэра, необходимые для приложения прокси приложения | Документы Майкрософт"
description: "Узнайте, какие порты необходимо открыть для правильной работы прокси приложения Azure AD."
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
ms.openlocfilehash: 8ecd6d7e666d362194126a4abba7a65f2c7b8b6b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-open-the-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="8bad8-103">Как открыть порты брандмауэра, необходимые для приложения прокси приложения</span><span class="sxs-lookup"><span data-stu-id="8bad8-103">How to open the firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="8bad8-104">Чтобы просмотреть полный список необходимых портов и функции каждого порта, обратитесь к разделу "Необходимые компоненты" в [документации по прокси приложения](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span><span class="sxs-lookup"><span data-stu-id="8bad8-104">To see a full list of the required ports and the function of each port, see the prerequisites section of the [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="8bad8-105">Обратите внимание, что прокси приложения использует только исходящие порты.</span><span class="sxs-lookup"><span data-stu-id="8bad8-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="8bad8-106">Проверить, что все необходимые порты открыты, также можно с помощью [Средства тестирования портов соединителя](https://aadap-portcheck.connectorporttest.msappproxy.net/) из локальной сети.</span><span class="sxs-lookup"><span data-stu-id="8bad8-106">You can also check whether you have all the required ports open by opening the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="8bad8-107">Большее число зеленых флажков означает большую устойчивость.</span><span class="sxs-lookup"><span data-stu-id="8bad8-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="8bad8-108">Регионы прокси приложения</span><span class="sxs-lookup"><span data-stu-id="8bad8-108">App Proxy regions</span></span>

<span data-ttu-id="8bad8-109">Мы работаем над тем, чтобы зеленым цветом выделялись только необходимые для вас регионы.</span><span class="sxs-lookup"><span data-stu-id="8bad8-109">We are working on a way to let you know which of these regions needs to be green for you.</span></span> <span data-ttu-id="8bad8-110">Пока убедитесь, что все регионы выделены зеленым цветом.</span><span class="sxs-lookup"><span data-stu-id="8bad8-110">For now, make sure they all are.</span></span> <span data-ttu-id="8bad8-111">Регион "Центральная часть США" должен быть выделен зеленым цветом независимо от того, в каком регионе вы находитесь.</span><span class="sxs-lookup"><span data-stu-id="8bad8-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="8bad8-112">Чтобы получить правильные результаты, необходимо:</span><span class="sxs-lookup"><span data-stu-id="8bad8-112">To make sure the tool gives you the right results, be sure to:</span></span>

-   <span data-ttu-id="8bad8-113">Откройте средство в браузере на сервере, на котором установлен соединитель.</span><span class="sxs-lookup"><span data-stu-id="8bad8-113">Open the tool on a browser from the server where you have installed the Connector.</span></span>

-   <span data-ttu-id="8bad8-114">Убедитесь, что все прокси-серверы или брандмауэры, которые применяются к соединителю, также применяются к этой странице.</span><span class="sxs-lookup"><span data-stu-id="8bad8-114">Ensure that any proxies or firewalls applicable to your Connector are also applied to this page.</span></span> <span data-ttu-id="8bad8-115">Для этого в Internet Explorer выберите **Параметры** -&gt; **Свойства обозревателя** -&gt; **Подключения** -&gt; **Настройка сети**.</span><span class="sxs-lookup"><span data-stu-id="8bad8-115">This can be done in Internet Explorer by going to **Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="8bad8-116">На этой странице появится флажок "Использовать прокси-сервер для локальной сети".</span><span class="sxs-lookup"><span data-stu-id="8bad8-116">On this page, you see the field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="8bad8-117">Установите этот флажок и укажите адрес прокси-сервера в поле "Адрес".</span><span class="sxs-lookup"><span data-stu-id="8bad8-117">Select this box, and put the proxy address into the “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bad8-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8bad8-118">Next steps</span></span>
[<span data-ttu-id="8bad8-119">Сведения о соединителях прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bad8-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
