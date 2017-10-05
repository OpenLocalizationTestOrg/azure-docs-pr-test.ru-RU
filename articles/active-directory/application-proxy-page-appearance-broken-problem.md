---
title: "Неправильное отображение страницы приложения для приложения прокси приложения | Документы Майкрософт"
description: "Указания на случай, когда страница отображается неправильно в приложении прокси приложения, интегрированном с Azure AD."
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
ms.openlocfilehash: cac4c333e59ef9a0f28a2f93a7afee22eeafd54e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="cce86-103">Неправильное отображение страницы приложения для приложения прокси приложения</span><span class="sxs-lookup"><span data-stu-id="cce86-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="cce86-104">Эта статья помогает устранить проблемы с приложениями прокси приложения Azure Active Directory, когда вы переходите на страницу и на ней что-то работает неправильно.</span><span class="sxs-lookup"><span data-stu-id="cce86-104">This article help you to troubleshoot issues with Azure Active Directory Application Proxy applications when you navigate to the page, but something on the page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="cce86-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="cce86-105">Overview</span></span>
<span data-ttu-id="cce86-106">При публикации приложения прокси приложения доступны только страницы из корневого каталога.</span><span class="sxs-lookup"><span data-stu-id="cce86-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing the application.</span></span> <span data-ttu-id="cce86-107">Если страница отображается неправильно, возможно, в корневом внутреннем URL-адресе для этого приложения отсутствуют некоторые ресурсы страницы.</span><span class="sxs-lookup"><span data-stu-id="cce86-107">If the page isn’t displaying correctly, the root internal URL used for the application may be missing some page resources.</span></span> <span data-ttu-id="cce86-108">Чтобы решить проблему, убедитесь, что вы опубликовали *все* ресурсы для страницы в составе своего приложения.</span><span class="sxs-lookup"><span data-stu-id="cce86-108">To resolve, make sure you have published *all* the resources for the page as part of your application.</span></span>

<span data-ttu-id="cce86-109">Убедиться в наличии проблемы можно, открыв средство отслеживания сети (например, Fiddler либо инструменты F12 в Internet Explorer или Edge), загрузив страницу и выполнив поиск ошибок 404.</span><span class="sxs-lookup"><span data-stu-id="cce86-109">You can verify this is the issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading the page, and looking for 404 errors.</span></span> <span data-ttu-id="cce86-110">Это позволяет выявить страницы, которые сейчас не удается найти и, возможно, все еще требуется опубликовать.</span><span class="sxs-lookup"><span data-stu-id="cce86-110">That indicates the pages that currently cannot be found and may still need to be published.</span></span>

<span data-ttu-id="cce86-111">В качестве примера этой ситуации предположим, что вы опубликовали приложение учета расходов с помощью внутреннего URL-адреса <http://myapps/expenses>, но приложение использует таблицу стилей <http://myapps/style.css>.</span><span class="sxs-lookup"><span data-stu-id="cce86-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but the app uses the stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="cce86-112">В этом случае таблица стилей не публикуется в вашем приложении, поэтому при запуске приложения выдается ошибка 404 из-за попытки загрузить style.css.</span><span class="sxs-lookup"><span data-stu-id="cce86-112">In this case, the stylesheet is not published in your application, so loading the expenses app throw a 404 error while trying to load style.css.</span></span> <span data-ttu-id="cce86-113">В этом примере проблему можно было бы решить, опубликовав приложение с помощью внутреннего URL-адреса <http://myapp/>.</span><span class="sxs-lookup"><span data-stu-id="cce86-113">In this example, the problem would be resolved by publishing the application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="cce86-114">Проблемы при публикации в качестве одного приложения</span><span class="sxs-lookup"><span data-stu-id="cce86-114">Problems with publishing as one application</span></span>

<span data-ttu-id="cce86-115">Если невозможно опубликовать все ресурсы в одном приложении, нужно опубликовать несколько приложений и включить ссылки между ними.</span><span class="sxs-lookup"><span data-stu-id="cce86-115">If it is not possible to publish all resources within the same application, you need to publish multiple applications and enable links between them.</span></span>

<span data-ttu-id="cce86-116">Для этого рекомендуется использовать решение на базе [личных доменов](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="cce86-116">To do so, we recommend using the [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="cce86-117">Однако это решение требует, чтобы вы владели сертификатом для своего домена, а ваши приложения использовали полные доменные имена (FQDN).</span><span class="sxs-lookup"><span data-stu-id="cce86-117">However, this solution requires that you own the certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="cce86-118">Другие варианты описаны в [документации по устранению неполадок с неработающими ссылками](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span><span class="sxs-lookup"><span data-stu-id="cce86-118">For other options, see the [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cce86-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cce86-119">Next steps</span></span>
[<span data-ttu-id="cce86-120">Публикация приложений с помощью прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="cce86-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
