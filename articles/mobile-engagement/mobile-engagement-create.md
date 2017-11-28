---
title: "Создание приложения Служб мобильного взаимодействия Azure | Документация Майкрософт"
description: "В этой статье описано, как создать новую коллекцию приложений Служб мобильного взаимодействия в Azure и приступить к управлению приложениями с помощью портала Служб мобильного взаимодействия."
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: b8aa1798-28c6-424c-a5b5-8a264d5a0ff0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/10/2016
ms.author: piyushjo
ms.openlocfilehash: 47c1e122f6f38654cd63bb59e50e68803f76c83d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-mobile-engagement-app"></a><span data-ttu-id="aeb0e-103">Создание приложения Служб мобильного взаимодействия Azure</span><span class="sxs-lookup"><span data-stu-id="aeb0e-103">Create an Azure Mobile Engagement App</span></span>
<span data-ttu-id="aeb0e-104">В этой статье показано, как с помощью метода **Быстрое создание** создать новое приложение **Служб мобильного взаимодействия Azure**.</span><span class="sxs-lookup"><span data-stu-id="aeb0e-104">This article shows how to use the **Quick Create** method to create a new **Azure Mobile Engagement** App.</span></span> <span data-ttu-id="aeb0e-105">В статье также показано, как перейти на портал **Служб мобильного взаимодействия**, чтобы начать мониторинг приложений и управление ими.</span><span class="sxs-lookup"><span data-stu-id="aeb0e-105">The article also shows how to navigate to your **Mobile Engagement** portal in order to start monitoring and managing your apps.</span></span> 

<span data-ttu-id="aeb0e-106">Обратите внимание, что вам потребуется добавить минимальный набор базовой интеграции, чтобы иметь возможность собирать данные для приложения и отправлять push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="aeb0e-106">Note that you must add a minimum set of "basic integration" in order to be able to collect data for your app and send push notifications.</span></span> <span data-ttu-id="aeb0e-107">Полную документацию по интеграции можно найти в разделе [Интеграция Служб мобильного взаимодействия](mobile-engagement-windows-store-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="aeb0e-107">The complete integration documentation can be found in the [Mobile Engagement integration](mobile-engagement-windows-store-integrate-engagement.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aeb0e-108">Для работы с любым руководством по Службам мобильного взаимодействия Azure необходима активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="aeb0e-108">To complete any Azure Mobile Engagement tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="aeb0e-109">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="aeb0e-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="aeb0e-110">Дополнительные сведения см. в разделе <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fwww.windowsazure.com%2Fen-us%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Бесплатная пробная версия Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="aeb0e-110">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fwww.windowsazure.com%2Fen-us%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-mobile-app-in-azure"></a><span data-ttu-id="aeb0e-111">Настройка Служб мобильного взаимодействия для мобильного приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="aeb0e-111">Setup Mobile Engagement for your mobile app in Azure</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="navigate-to-your-mobile-engagement-portal"></a><span data-ttu-id="aeb0e-112">Перейдите на портал Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="aeb0e-112">Navigate to your Mobile Engagement portal</span></span>
<span data-ttu-id="aeb0e-113">Чтобы начать мониторинг приложения и управление им, перейдите на портал Служб мобильного взаимодействия. Для этого нажмите кнопку **Engagement portal** (Портал взаимодействия) на верхней панели.</span><span class="sxs-lookup"><span data-stu-id="aeb0e-113">To start monitoring and managing your application, navigate to your Mobile Engagement portal by clicking the **Engagement portal** button in the top bar.</span></span>

<span data-ttu-id="aeb0e-114">После входа на портал Служб мобильного взаимодействия вы можете анализировать и создавать сегменты, управлять ими, привлекать пользователей и выполнять другие действия.</span><span class="sxs-lookup"><span data-stu-id="aeb0e-114">Once you are in the  Mobile Engagement portal, you can analyze, create and manage segments, reach out to the users, etc.:</span></span>    

* [<span data-ttu-id="aeb0e-115">Наблюдение за работой приложения в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="aeb0e-115">Monitor real time data about your application</span></span>](mobile-engagement-user-interface-monitor.md)
* [<span data-ttu-id="aeb0e-116">Анализ журналов данных о приложении</span><span class="sxs-lookup"><span data-stu-id="aeb0e-116">Analyze historical data about your application</span></span>](mobile-engagement-user-interface-analytics.md)
* [<span data-ttu-id="aeb0e-117">Создание сегментов пользователей и управление ими для выявления закономерностей</span><span class="sxs-lookup"><span data-stu-id="aeb0e-117">Create and manage segments of users to identify usage patterns</span></span>](mobile-engagement-user-interface-segments.md)
* [<span data-ttu-id="aeb0e-118">Охват пользователей приложения с помощью push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="aeb0e-118">Reach out to the users of your application with push notifications</span></span>](mobile-engagement-user-interface-reach.md)

## <a name="see-also"></a><span data-ttu-id="aeb0e-119">См. также</span><span class="sxs-lookup"><span data-stu-id="aeb0e-119">See Also</span></span>
[<span data-ttu-id="aeb0e-120">Определение стратегии Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="aeb0e-120">Define your Mobile Engagement strategy</span></span>](mobile-engagement-define-your-mobile-engagement-strategy.md)

<span data-ttu-id="aeb0e-121">[Приступая к работе со Службами мобильного взаимодействия Azure](mobile-engagement-windows-store-dotnet-get-started.md) (в верхней части страницы можно выбрать другие мобильные платформы).</span><span class="sxs-lookup"><span data-stu-id="aeb0e-121">[Get started with Azure Mobile Engagement](mobile-engagement-windows-store-dotnet-get-started.md) (you can select other mobile platforms at the top of the page).</span></span>

