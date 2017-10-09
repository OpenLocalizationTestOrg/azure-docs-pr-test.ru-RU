---
title: "aaaApplication страницы отображается неправильно, для приложения прокси приложения | Документы Microsoft"
description: "Рекомендации, когда страница hello не правильно отображаться в приложении прокси приложения, интегрированные с Azure AD"
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
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="bd95c-103">Неправильное отображение страницы приложения для приложения прокси приложения</span><span class="sxs-lookup"><span data-stu-id="bd95c-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="bd95c-104">В этой статье помогут tootroubleshoot проблем с приложениями прокси приложения Azure Active Directory перейдите toohello страницы, когда что-нибудь на странице приветствия выглядит правильно.</span><span class="sxs-lookup"><span data-stu-id="bd95c-104">This article help you tootroubleshoot issues with Azure Active Directory Application Proxy applications when you navigate toohello page, but something on hello page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="bd95c-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="bd95c-105">Overview</span></span>
<span data-ttu-id="bd95c-106">При публикации приложения прокси приложения только страницы в корневом каталоге, доступны при доступе к приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bd95c-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing hello application.</span></span> <span data-ttu-id="bd95c-107">Если страница hello не отображаются правильно, hello корневой внутреннего URL-адреса для приложения hello могут отсутствовать некоторые ресурсы страницы.</span><span class="sxs-lookup"><span data-stu-id="bd95c-107">If hello page isn’t displaying correctly, hello root internal URL used for hello application may be missing some page resources.</span></span> <span data-ttu-id="bd95c-108">tooresolve, убедитесь, что вы опубликовали *все* hello ресурсы для hello страницы как части приложения.</span><span class="sxs-lookup"><span data-stu-id="bd95c-108">tooresolve, make sure you have published *all* hello resources for hello page as part of your application.</span></span>

<span data-ttu-id="bd95c-109">Можно проверить это проблема hello, открыв tracker вашей сети (такие как Fiddler или F12 средства в Internet Explorer или Edge), загрузка страницы hello и поиск ошибки 404.</span><span class="sxs-lookup"><span data-stu-id="bd95c-109">You can verify this is hello issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading hello page, and looking for 404 errors.</span></span> <span data-ttu-id="bd95c-110">Указывает, hello страниц, которые в настоящее время не удается найти, а также по-прежнему может потребоваться toobe публикации.</span><span class="sxs-lookup"><span data-stu-id="bd95c-110">That indicates hello pages that currently cannot be found and may still need toobe published.</span></span>

<span data-ttu-id="bd95c-111">Например связи данного варианта, предположим, вы опубликовали приложения расходы с помощью внутреннего URL-адреса из <http://myapps/expenses>, но приложение hello использует таблицу стилей hello <http://myapps/style.css>.</span><span class="sxs-lookup"><span data-stu-id="bd95c-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but hello app uses hello stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="bd95c-112">В этом случае hello таблицы стилей не публикуется в приложении, поэтому загрузка прибыли приложение hello выдавать ошибку 404, при попытке tooload style.css.</span><span class="sxs-lookup"><span data-stu-id="bd95c-112">In this case, hello stylesheet is not published in your application, so loading hello expenses app throw a 404 error while trying tooload style.css.</span></span> <span data-ttu-id="bd95c-113">В этом примере hello проблема может быть решена публикации приложения hello внутренний URL-адрес <http://myapp/> вместо него.</span><span class="sxs-lookup"><span data-stu-id="bd95c-113">In this example, hello problem would be resolved by publishing hello application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="bd95c-114">Проблемы при публикации в качестве одного приложения</span><span class="sxs-lookup"><span data-stu-id="bd95c-114">Problems with publishing as one application</span></span>

<span data-ttu-id="bd95c-115">Если это не возможно toopublish всех ресурсов в Здравствуйте того же приложения, нужно toopublish несколько приложений и включить ссылки между ними.</span><span class="sxs-lookup"><span data-stu-id="bd95c-115">If it is not possible toopublish all resources within hello same application, you need toopublish multiple applications and enable links between them.</span></span>

<span data-ttu-id="bd95c-116">toodo таким образом, мы рекомендуем использовать hello [пользовательских доменов](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) решения.</span><span class="sxs-lookup"><span data-stu-id="bd95c-116">toodo so, we recommend using hello [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="bd95c-117">Тем не менее это решение требует владения hello сертификат для домена и приложениях используются полные доменные имена (FQDN).</span><span class="sxs-lookup"><span data-stu-id="bd95c-117">However, this solution requires that you own hello certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="bd95c-118">Другие варианты см. в разделе hello [Устранение неполадок неработающих ссылок документации](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span><span class="sxs-lookup"><span data-stu-id="bd95c-118">For other options, see hello [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd95c-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bd95c-119">Next steps</span></span>
[<span data-ttu-id="bd95c-120">Публикация приложений с помощью прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd95c-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
