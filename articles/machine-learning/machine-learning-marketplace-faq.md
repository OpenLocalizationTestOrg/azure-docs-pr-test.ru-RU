---
title: "Вопросы и ответы о публикации и использовании приложений машинного обучения в Azure Marketplace (устаревшая версия) | Документация Майкрософт"
description: "Вопросы и ответы о публикации приложений машинного обучения в Azure Marketplace (устаревшая версия)."
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: a4631dfeb2f817b3a3c612a8f6af48398e4f2ab9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-the-azure-marketplace-faq"></a><span data-ttu-id="100a5-103">Вопросы и ответы о публикации и использовании приложений машинного обучения в Azure Marketplace (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="100a5-103">(deprecated) Publishing and using Machine Learning apps in the Azure Marketplace: FAQ</span></span>

> [!NOTE]
> <span data-ttu-id="100a5-104">Работа DataMarket и служб данных прекращается. Начиная с 31 марта 2017 г. имеющиеся подписки выводятся из эксплуатации и будут отменены.</span><span class="sxs-lookup"><span data-stu-id="100a5-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="100a5-105">Поэтому мы не рекомендуем использовать эту статью.</span><span class="sxs-lookup"><span data-stu-id="100a5-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="100a5-106">В качестве альтернативы вы можете публиковать свои эксперименты машинного обучения в [коллекции Cortana Intelligence](https://gallery.cortanaintelligence.com/) и поделиться ими с сообществом, занимающимся анализом данных.</span><span class="sxs-lookup"><span data-stu-id="100a5-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span></span> <span data-ttu-id="100a5-107">Дополнительные сведения см. в статье [Поиск ресурсов в коллекции Cortana Intelligence и обмен ими](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="100a5-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>


## <a name="questions-about-consuming-from-marketplace"></a><span data-ttu-id="100a5-108">Вопросы об использовании приложений из Marketplace</span><span class="sxs-lookup"><span data-stu-id="100a5-108">Questions about consuming from Marketplace</span></span>
<span data-ttu-id="100a5-109">**1. Почему, когда я ввожу данные для веб-службы, отображается такое сообщение об ошибке:**</span><span class="sxs-lookup"><span data-stu-id="100a5-109">**1. Why do I get the following error message after I enter input for the web service:**</span></span>

<span data-ttu-id="100a5-110">**При выполнении запроса возникла внутренняя ошибка или истекло время ожидания. Наша команда изучает эту проблему. Приносим извинения за причиненные неудобства. (500)**</span><span class="sxs-lookup"><span data-stu-id="100a5-110">**The request resulted in a back-end time out or back-end error. The team is investigating the issue. We are sorry for the inconvenience. (500)**</span></span>

<span data-ttu-id="100a5-111">Возможно, формат указанных вами входных параметров не соответствует требованиям для этой веб-службы.</span><span class="sxs-lookup"><span data-stu-id="100a5-111">Your input parameter(s) may not conform to the required format for the specific web service.</span></span> <span data-ttu-id="100a5-112">Правильный формат входных параметров и ограничения для данной веб-службы см. по ссылке на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="100a5-112">Please refer to the corresponding documentation link to find the correct format for input parameters and the limitations of this web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="100a5-113">**2. Если скопировать ссылку на API для веб-службы из страницы «Просмотр набора данных» и вставить ее в другом окне браузера, какие учетные данные нужно использовать для просмотра результатов и в каком виде они отображаются?**</span><span class="sxs-lookup"><span data-stu-id="100a5-113">**2. If I copy the API link for the web service that I see on the "Explore this dataset" page and paste it into another browser window, what credentials should I use to access the results, and how do I see them?**</span></span>

<span data-ttu-id="100a5-114">Укажите имя пользователя своей учетной записи Marketplace, а в качестве пароля — основной ключ к ней.</span><span class="sxs-lookup"><span data-stu-id="100a5-114">You should use your Marketplace account as the username and the primary account key as the password.</span></span> <span data-ttu-id="100a5-115">Ключ основной учетной записи можно найти на странице **Explore this dataset** (Просмотр набора данных) под описанием веб-службы (нажмите кнопку **Показать**).</span><span class="sxs-lookup"><span data-stu-id="100a5-115">The primary account key can be found on the **Explore this dataset** page under the description of the web service (click the **show** button).</span></span> <span data-ttu-id="100a5-116">Результат может отображаться в браузере или будет доступен для скачивания (в зависимости от вашего браузера).</span><span class="sxs-lookup"><span data-stu-id="100a5-116">The result may display in the browser or it may be available to  download, depending on which browser you are using.</span></span>

<span data-ttu-id="100a5-117">**3. Почему, когда я ввожу данные для веб-службы на странице «Просмотр набора данных», отображается такое сообщение об ошибке:**</span><span class="sxs-lookup"><span data-stu-id="100a5-117">**3. Why do I get the following error message after I enter the input for the web service on the "Explore this dataset" page:**</span></span> 

<span data-ttu-id="100a5-118">**При обработке запроса произошла непредвиденная ошибка. Повторите попытку позже.**</span><span class="sxs-lookup"><span data-stu-id="100a5-118">**An unexpected error occurred while processing your request. Please try again.**</span></span>

<span data-ttu-id="100a5-119">Когда вы использовали веб-службу на странице магазина **Explore this dataset** (Просмотр набора данных), длина некоторых входных параметров вашей веб-службы превысила максимальное значение.</span><span class="sxs-lookup"><span data-stu-id="100a5-119">One or more input parameters of your web service may have exceeded the length limit when consuming the web service on the marketplace **Explore this dataset** page.</span></span> <span data-ttu-id="100a5-120">С помощью методов HTTP POST можно вызывать службы с большей длиной входных данных.</span><span class="sxs-lookup"><span data-stu-id="100a5-120">The services can be called with a longer input length by using HTTP POST methods.</span></span> <span data-ttu-id="100a5-121">Примеры см. в статье [Примеры веб-служб, построенных с помощью языка R в Azure ML и опубликованных в Marketplace](machine-learning-r-csharp-web-service-examples.md).</span><span class="sxs-lookup"><span data-stu-id="100a5-121">For examples, see [Sample solutions using R on Machine Learning and published to Marketplace](machine-learning-r-csharp-web-service-examples.md).</span></span>

<span data-ttu-id="100a5-122">**4. Почему ничего не отображается на вкладке "ОБОЗРЕВАТЕЛЬ API" в магазине на классическом портале Azure?**</span><span class="sxs-lookup"><span data-stu-id="100a5-122">**4. Why do I not see anything in the "API EXPLORER" tab int the Store in the Azure Classic Portal?**</span></span> 

<span data-ttu-id="100a5-123">Это известная проблема с магазином Marketplace классического портала Azure.</span><span class="sxs-lookup"><span data-stu-id="100a5-123">This is a known issue with the Azure Classic Portal Marketplace.</span></span> <span data-ttu-id="100a5-124">Наша команда работает над ее устранением.</span><span class="sxs-lookup"><span data-stu-id="100a5-124">The team is working to resolve this issue.</span></span> 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a><span data-ttu-id="100a5-125">Вопросы о публикации с помощью веб-служб машинного обучения Azure в магазине Marketplace</span><span class="sxs-lookup"><span data-stu-id="100a5-125">Questions about publishing from Azure Machine Learning on Marketplace</span></span>
<span data-ttu-id="100a5-126">**1. Почему в моей веб-службе не отражаются транзакции логотипов или изображений?**</span><span class="sxs-lookup"><span data-stu-id="100a5-126">**1. Why are my transactions of logos or images not refreshing for my web service?**</span></span> 

<span data-ttu-id="100a5-127">Логотипы и изображения кэшируются на портале публикации, и их обновление на портале может занять до 10 дней.</span><span class="sxs-lookup"><span data-stu-id="100a5-127">Logos and images are cached in the publishing portal, and it may take up to 10 days for the new logo or image to update on the portal.</span></span>

<span data-ttu-id="100a5-128">**2. Почему на вкладке «Подробности» моей веб-службы в магазине Marketplace отображается сообщение об ошибке?**</span><span class="sxs-lookup"><span data-stu-id="100a5-128">**2. Why is the “Detail" tab of my web service on Marketplace showing an error message?**</span></span>

<span data-ttu-id="100a5-129">Это известная проблема Marketplace, возникающая при попытке подключиться к платформе Azure ML и запросить сведения о службе.</span><span class="sxs-lookup"><span data-stu-id="100a5-129">There is a known Marketplace issue when connecting to Azure Machine Learning for service details.</span></span> <span data-ttu-id="100a5-130">Наша команда работает над ее устранением.</span><span class="sxs-lookup"><span data-stu-id="100a5-130">The team is working to resolve this issue.</span></span>

<span data-ttu-id="100a5-131">**3. Почему с помощью образца кода R веб-служб Azure ML не удается использовать веб-службы Marketplace?**</span><span class="sxs-lookup"><span data-stu-id="100a5-131">**3. Why does the R sample code in the Azure Machine Learning web services not work for consuming the web services in Marketplace?**</span></span>

<span data-ttu-id="100a5-132">При подключении к веб-службам Azure ML напрямую и при подключении через Marketplace применяются разные системы аутентификации.</span><span class="sxs-lookup"><span data-stu-id="100a5-132">The authentication systems are different when connecting to Azure Machine Learning web services directly compared to connecting to these web services through the Marketplace.</span></span> <span data-ttu-id="100a5-133">Службы Marketplace являются службами OData, и для их вызова можно использовать методы GET и POST.</span><span class="sxs-lookup"><span data-stu-id="100a5-133">The services in Marketplace are OData services, and they can be called with GET or POST methods.</span></span> 

<span data-ttu-id="100a5-134">**4. Почему для некоторых из предлагаемых мною веб-служб неправильно обновляются ссылки для получения поддержки?**</span><span class="sxs-lookup"><span data-stu-id="100a5-134">**4. Why are the support links of my web service offers not updating correctly for some of my offers?**</span></span>

<span data-ttu-id="100a5-135">Ссылки для получения поддержки задаются глобально для издателя, а не для каждого из его предложений.</span><span class="sxs-lookup"><span data-stu-id="100a5-135">The support links are global per publisher, not per offer.</span></span> 

<span data-ttu-id="100a5-136">**5. Как опубликовать в Marketplace веб-службу с пакетным режимом ввода?**</span><span class="sxs-lookup"><span data-stu-id="100a5-136">**5. How do I publish a web service with batch input mode in Marketplace?**</span></span>

<span data-ttu-id="100a5-137">В настоящее время веб-службы Marketplace не поддерживают пакетный режим ввода.</span><span class="sxs-lookup"><span data-stu-id="100a5-137">The batch input mode is currently not supported in Marketplace web services.</span></span>

<span data-ttu-id="100a5-138">**6. К кому можно обратиться с вопросом о том, как стать издателем данных, или при возникновении проблем во время публикации?**</span><span class="sxs-lookup"><span data-stu-id="100a5-138">**6. Who should I contact to get help if I have questions about becoming a data publisher, or if I have issues during publishing?**</span></span>

<span data-ttu-id="100a5-139">Чтобы получить дополнительные сведения, напишите команде Azure Marketplace по адресу <mailto:datamarketbd@microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="100a5-139">Please contact the Azure Marketplace team at <mailto:datamarketbd@microsoft.com> for more information.</span></span>

