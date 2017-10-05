---
title: "Отправка сертификата API управления в Azure | Документация Майкрософт"
description: "Узнайте, как отправить сертификат API управления в Microsoft Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 9dc438e927acd9aef38f06807fabf3dda9b021c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a><span data-ttu-id="48428-103">Отправка сертификата управления Azure для API управления</span><span class="sxs-lookup"><span data-stu-id="48428-103">Upload an Azure Management API Management Certificate</span></span>
<span data-ttu-id="48428-104">Сертификаты управления позволяют выполнять аутентификацию с помощью классической модели развертывания Azure.</span><span class="sxs-lookup"><span data-stu-id="48428-104">Management certificates allow you to authenticate with the classic deployment model provided by Azure.</span></span> <span data-ttu-id="48428-105">Многие программы и инструменты (например, Visual Studio или пакет SDK Azure) будут использовать эти сертификаты для автоматизации настройки и развертывания разных служб Azure.</span><span class="sxs-lookup"><span data-stu-id="48428-105">Many programs and tools (such as Visual Studio or the Azure SDK) use these certificates to automate configuration and deployment of various Azure services.</span></span> 

> [!WARNING]
> <span data-ttu-id="48428-106">Будьте осторожны!</span><span class="sxs-lookup"><span data-stu-id="48428-106">Be careful!</span></span> <span data-ttu-id="48428-107">Эти типы сертификатов позволяют каждому, кто прошел проверку подлинности, управлять подпиской, с которой они связаны.</span><span class="sxs-lookup"><span data-stu-id="48428-107">These types of certificates allow anyone who authenticates with them to manage the subscription they are associated with.</span></span>
>
>

<span data-ttu-id="48428-108">Дополнительные сведения о сертификатах Azure (включая сведения о создании самозаверяющего сертификата) см. в разделе [Что такое сертификаты управления](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span><span class="sxs-lookup"><span data-stu-id="48428-108">If you'd like more information about Azure certificates (including creating a self-signed certificate), see [Certificates overview for Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="48428-109">Для автоматизации проверки подлинности клиентского кода можно также использовать службу [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="48428-109">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) to authenticate client-code for automation purposes.</span></span>

## <a name="upload-a-management-certificate"></a><span data-ttu-id="48428-110">Отправка сертификата управления</span><span class="sxs-lookup"><span data-stu-id="48428-110">Upload a management certificate</span></span>
<span data-ttu-id="48428-111">Создав сертификат управления (CER-файл только с открытым ключом), передайте его на портал.</span><span class="sxs-lookup"><span data-stu-id="48428-111">Once you have a management certificate created, (.cer file with only the public key) you can upload it into the portal.</span></span> <span data-ttu-id="48428-112">Когда сертификат доступен на портале, любой пользователь с соответствующим сертификатом (закрытым ключом) сможет подключаться через API управления и работать с ресурсами связанной подписки.</span><span class="sxs-lookup"><span data-stu-id="48428-112">When the certificate is available in the portal, anyone with a matching certificate (private key) can connect through the Management API and access the resources for the associated subscription.</span></span>

1. <span data-ttu-id="48428-113">Войдите на [портал Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="48428-113">Log in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="48428-114">Щелкните **Больше служб** внизу списка служб Azure и выберите **Подписки** в группе служб _Общие_.</span><span class="sxs-lookup"><span data-stu-id="48428-114">Click **More services** at the bottom Azure service list, then select **Subscriptions** in the _General_ service group.</span></span>

    ![Меню "Подписка"](./media/azure-api-management-certs/subscriptions_menu.png)

3. <span data-ttu-id="48428-116">Обязательно выберите именно ту подписку, с которой необходимо связать сертификат.</span><span class="sxs-lookup"><span data-stu-id="48428-116">Make sure to select the correct subscription that you want to associate with the certificate.</span></span>     
4. <span data-ttu-id="48428-117">Выбрав правильную подписку, щелкните **Сертификаты управления** в группе _Параметры_.</span><span class="sxs-lookup"><span data-stu-id="48428-117">After you have selected the correct subscription, press **Management certificates** in the _Settings_ group.</span></span>

    ![данных](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. <span data-ttu-id="48428-119">Нажмите кнопку **Отправить** .</span><span class="sxs-lookup"><span data-stu-id="48428-119">Press the **Upload** button.</span></span>

    ![Кнопка "Отправить" на странице сертификатов](./media/azure-api-management-certs/certificates_page.png)
6. <span data-ttu-id="48428-121">Укажите сведения в диалоговом окне и нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="48428-121">Fill out the dialog information and press **Upload**.</span></span>

    ![данных](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a><span data-ttu-id="48428-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="48428-123">Next steps</span></span>
<span data-ttu-id="48428-124">Связав сертификат управления с подпиской и установив соответствующий сертификат локально, вы можете программно подключаться к [REST API классической модели управления](https://msdn.microsoft.com/library/azure/mt420159.aspx) и автоматизировать различные ресурсы Azure, связанные с этой же подпиской.</span><span class="sxs-lookup"><span data-stu-id="48428-124">Now that you have a management certificate associated with a subscription, you can (after you have installed the matching certificate locally) programmatically connect to the [classic deployment model REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate the various Azure resources that are also associated with that subscription.</span></span>
