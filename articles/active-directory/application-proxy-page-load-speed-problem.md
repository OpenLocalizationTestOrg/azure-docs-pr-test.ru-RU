---
title: "Загрузка приложения прокси приложения занимает слишком много времени | Документы Майкрософт"
description: "Устранение проблем с производительностью загрузки страницы в прокси приложения Azure AD."
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
ms.openlocfilehash: ce462c90746e6af0dc201686557121665b82b93d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="an-application-proxy-application-takes-too-long-to-load"></a><span data-ttu-id="d6085-103">Загрузка приложения прокси приложения занимает слишком много времени</span><span class="sxs-lookup"><span data-stu-id="d6085-103">An Application Proxy application takes too long to load</span></span>

<span data-ttu-id="d6085-104">Эта статья описывает, почему приложение прокси приложения Azure AD может загружаться слишком долго и как устранить эту проблему.</span><span class="sxs-lookup"><span data-stu-id="d6085-104">This article help you to understand why an Azure AD Application Proxy application may take a long time to load, and what you can do to resolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="d6085-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="d6085-105">Overview</span></span>
<span data-ttu-id="d6085-106">Если приложение работает, но наблюдается большая задержка, можно использовать некоторые аспекты топологии сети для повышения скорости.</span><span class="sxs-lookup"><span data-stu-id="d6085-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider to improve the speed.</span></span> <span data-ttu-id="d6085-107">Оценку различных топологий см. в [документе с рекомендациями по сети](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span><span class="sxs-lookup"><span data-stu-id="d6085-107">For an evaluation of different topologies, see the [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="d6085-108">Если эти рекомендации не помогают, других советов по настройке производительности у нас, к сожалению, пока нет.</span><span class="sxs-lookup"><span data-stu-id="d6085-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="d6085-109">По мере того, как прокси-служба приложения охватывает все больше центров обработки данных, которые могут находиться ближе к вам, вы можете заметить сокращение задержки.</span><span class="sxs-lookup"><span data-stu-id="d6085-109">As the Application Proxy service expands to more data centers that may be closer to you, you may start to see improved latency directly.</span></span> <span data-ttu-id="d6085-110">Чтобы просмотреть полный список центров обработки данных Azure, см. [страницу проверки задержки](http://www.azurespeed.com/Azure/Latency).</span><span class="sxs-lookup"><span data-stu-id="d6085-110">To see the full list of Azure data centers, you can see the [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="d6085-111">Центры обработки данных с прокси-службой приложения можно найти с помощью [средства проверки портов соединителя](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span><span class="sxs-lookup"><span data-stu-id="d6085-111">The data centers with the Application Proxy service can be found with the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="d6085-112">Отзывы о расположениях центров обработки данных для прокси приложения</span><span class="sxs-lookup"><span data-stu-id="d6085-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="d6085-113">Могут существовать центры обработки данных Azure, которые пока не используют прокси приложения, но способны значительно сократить вашу задержку.</span><span class="sxs-lookup"><span data-stu-id="d6085-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead to a great latency improvement for you.</span></span> <span data-ttu-id="d6085-114">Сообщения о расположении центров обработки данных направляйте на адрес <aadapfeedback@microsoft.com>, чтобы мы могли учитывать ваши отзывы при планировании расширения.</span><span class="sxs-lookup"><span data-stu-id="d6085-114">The data center location at <aadapfeedback@microsoft.com> so we can use your feedback to plan as we expand.</span></span>

<span data-ttu-id="d6085-115">Мы работаем над некоторыми дополнительными возможностями, помогающими сократить задержку для клиентов, которые сталкиваются со слишком большими ее значениями, и обязательно поделимся с вами документацией, когда она станет доступна.</span><span class="sxs-lookup"><span data-stu-id="d6085-115">We are working on some additional capabilities that help improve the latency for tenants that currently see long latencies, and be sure to share documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6085-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d6085-116">Next steps</span></span>
[<span data-ttu-id="d6085-117">Работа с имеющимися локальными прокси-серверами</span><span class="sxs-lookup"><span data-stu-id="d6085-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
