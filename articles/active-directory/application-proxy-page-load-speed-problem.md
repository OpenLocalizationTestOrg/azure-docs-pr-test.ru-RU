---
title: "aaaAn приложения прокси приложения занимает слишком длинный tooload | Документы Microsoft"
description: "Устранение неполадок производительности загрузки страницы с помощью hello прокси приложения Azure AD"
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
ms.openlocfilehash: 4c7a51f96840966a1d88933fa4e30f39479d8a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="an-application-proxy-application-takes-too-long-tooload"></a><span data-ttu-id="97564-103">Слишком длинный tooload принимает приложения прокси приложения</span><span class="sxs-lookup"><span data-stu-id="97564-103">An Application Proxy application takes too long tooload</span></span>

<span data-ttu-id="97564-104">В этой статье помогут toounderstand, почему приложение прокси приложения Azure AD может потребоваться tooload много времени и что можно сделать tooresolve эту проблему.</span><span class="sxs-lookup"><span data-stu-id="97564-104">This article help you toounderstand why an Azure AD Application Proxy application may take a long time tooload, and what you can do tooresolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="97564-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="97564-105">Overview</span></span>
<span data-ttu-id="97564-106">При работе приложения, но вы видите большие задержки, может возникнуть некоторые небольшие настройки топологии сети, можно учитывать скорость tooimprove hello.</span><span class="sxs-lookup"><span data-stu-id="97564-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider tooimprove hello speed.</span></span> <span data-ttu-id="97564-107">Для оценки различных топологий, в разделе hello [сети вопросы документа](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span><span class="sxs-lookup"><span data-stu-id="97564-107">For an evaluation of different topologies, see hello [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="97564-108">Если эти рекомендации не помогают, других советов по настройке производительности у нас, к сожалению, пока нет.</span><span class="sxs-lookup"><span data-stu-id="97564-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="97564-109">Как службы прокси приложения hello разворачивается toomore центрах обработки данных, которые могут быть более подробно tooyou, можно запустить toosee улучшена задержки напрямую.</span><span class="sxs-lookup"><span data-stu-id="97564-109">As hello Application Proxy service expands toomore data centers that may be closer tooyou, you may start toosee improved latency directly.</span></span> <span data-ttu-id="97564-110">Центрирует toosee hello полный список данных Azure, вы увидите hello [задержки тестовой страницы](http://www.azurespeed.com/Azure/Latency).</span><span class="sxs-lookup"><span data-stu-id="97564-110">toosee hello full list of Azure data centers, you can see hello [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="97564-111">Hello центрах обработки данных с помощью службы прокси приложения hello можно найти с помощью hello [средство тестирования порты соединитель](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span><span class="sxs-lookup"><span data-stu-id="97564-111">hello data centers with hello Application Proxy service can be found with hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="97564-112">Отзывы о расположениях центров обработки данных для прокси приложения</span><span class="sxs-lookup"><span data-stu-id="97564-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="97564-113">Может быть центрах обработки данных Azure, которые еще не включайте прокси приложения, но улучшение значительные задержки tooa привели бы.</span><span class="sxs-lookup"><span data-stu-id="97564-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead tooa great latency improvement for you.</span></span> <span data-ttu-id="97564-114">расположение центра обработки данных Hello < aadapfeedback@microsoft.com > , мы планируем можно использовать tooplan ваш отзыв.</span><span class="sxs-lookup"><span data-stu-id="97564-114">hello data center location at <aadapfeedback@microsoft.com> so we can use your feedback tooplan as we expand.</span></span>

<span data-ttu-id="97564-115">Мы работаем над некоторые дополнительные возможности, повышающие hello задержку для клиентов, которые в настоящее время доступны long задержки и быть убедиться, что документация tooshare после доступных.</span><span class="sxs-lookup"><span data-stu-id="97564-115">We are working on some additional capabilities that help improve hello latency for tenants that currently see long latencies, and be sure tooshare documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97564-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="97564-116">Next steps</span></span>
[<span data-ttu-id="97564-117">Работа с имеющимися локальными прокси-серверами</span><span class="sxs-lookup"><span data-stu-id="97564-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
