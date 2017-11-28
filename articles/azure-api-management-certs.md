---
title: "aaaUpload сертификат API управления Azure | Документы Microsoft"
description: "Узнайте, как сертификат tooupload athe API-Интерфейс управления для hello классический портал Azure."
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
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a><span data-ttu-id="7bdc1-103">Отправка сертификата управления Azure для API управления</span><span class="sxs-lookup"><span data-stu-id="7bdc1-103">Upload an Azure Management API Management Certificate</span></span>
<span data-ttu-id="7bdc1-104">Сертификаты управления позволяют tooauthenticate с hello классической модели развертывания, предоставляемых Azure.</span><span class="sxs-lookup"><span data-stu-id="7bdc1-104">Management certificates allow you tooauthenticate with hello classic deployment model provided by Azure.</span></span> <span data-ttu-id="7bdc1-105">Многие программы и средства (например, Visual Studio или hello Azure SDK) использовать эти сертификаты tooautomate конфигурации и развертывания различных служб Azure.</span><span class="sxs-lookup"><span data-stu-id="7bdc1-105">Many programs and tools (such as Visual Studio or hello Azure SDK) use these certificates tooautomate configuration and deployment of various Azure services.</span></span> 

> [!WARNING]
> <span data-ttu-id="7bdc1-106">Будьте осторожны!</span><span class="sxs-lookup"><span data-stu-id="7bdc1-106">Be careful!</span></span> <span data-ttu-id="7bdc1-107">Разрешить эти типы сертификатов всех, кто выполняет проверку подлинности с ними toomanage hello подписки, связанные с ними.</span><span class="sxs-lookup"><span data-stu-id="7bdc1-107">These types of certificates allow anyone who authenticates with them toomanage hello subscription they are associated with.</span></span>
>
>

<span data-ttu-id="7bdc1-108">Дополнительные сведения о сертификатах Azure (включая сведения о создании самозаверяющего сертификата) см. в разделе [Что такое сертификаты управления](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span><span class="sxs-lookup"><span data-stu-id="7bdc1-108">If you'd like more information about Azure certificates (including creating a self-signed certificate), see [Certificates overview for Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="7bdc1-109">Можно также использовать [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate-код клиента в целях автоматизации.</span><span class="sxs-lookup"><span data-stu-id="7bdc1-109">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate client-code for automation purposes.</span></span>

## <a name="upload-a-management-certificate"></a><span data-ttu-id="7bdc1-110">Отправка сертификата управления</span><span class="sxs-lookup"><span data-stu-id="7bdc1-110">Upload a management certificate</span></span>
<span data-ttu-id="7bdc1-111">После создания сертификата управления, (CER-файл только hello открытым ключом) можно загрузить его в портал hello.</span><span class="sxs-lookup"><span data-stu-id="7bdc1-111">Once you have a management certificate created, (.cer file with only hello public key) you can upload it into hello portal.</span></span> <span data-ttu-id="7bdc1-112">При наличии hello сертификатов на портале hello, имеющий соответствующий сертификат (закрытый ключ) могут подключаться через hello API управления и получения ресурсов hello для hello связанные подписки.</span><span class="sxs-lookup"><span data-stu-id="7bdc1-112">When hello certificate is available in hello portal, anyone with a matching certificate (private key) can connect through hello Management API and access hello resources for hello associated subscription.</span></span>

1. <span data-ttu-id="7bdc1-113">Войдите в toohello [портал Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7bdc1-113">Log in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="7bdc1-114">Нажмите кнопку **дополнительные службы** в hello нижнем списке службы Azure, затем выберите **подписки** в hello _Общие_ группы служб.</span><span class="sxs-lookup"><span data-stu-id="7bdc1-114">Click **More services** at hello bottom Azure service list, then select **Subscriptions** in hello _General_ service group.</span></span>

    ![Меню "Подписка"](./media/azure-api-management-certs/subscriptions_menu.png)

3. <span data-ttu-id="7bdc1-116">Убедитесь, что tooselect hello нужной подписки, которые должны tooassociate сертификатом hello.</span><span class="sxs-lookup"><span data-stu-id="7bdc1-116">Make sure tooselect hello correct subscription that you want tooassociate with hello certificate.</span></span>     
4. <span data-ttu-id="7bdc1-117">После того как выбрана правильная подписка hello, нажмите клавишу **сертификаты управления** в hello _параметры_ группы.</span><span class="sxs-lookup"><span data-stu-id="7bdc1-117">After you have selected hello correct subscription, press **Management certificates** in hello _Settings_ group.</span></span>

    ![данных](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. <span data-ttu-id="7bdc1-119">Нажмите клавишу hello **отправить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="7bdc1-119">Press hello **Upload** button.</span></span>

    ![Кнопка "Отправить" на странице сертификатов](./media/azure-api-management-certs/certificates_page.png)
6. <span data-ttu-id="7bdc1-121">Заполните данные в диалоговом окне приветствия и нажмите клавишу **отправить**.</span><span class="sxs-lookup"><span data-stu-id="7bdc1-121">Fill out hello dialog information and press **Upload**.</span></span>

    ![данных](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a><span data-ttu-id="7bdc1-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7bdc1-123">Next steps</span></span>
<span data-ttu-id="7bdc1-124">Теперь, когда сертификат управления, связанных с подпиской (после установки сопоставления локальный сертификат hello) программно подключением toohello [классической модели развертывания API-интерфейса REST](https://msdn.microsoft.com/library/azure/mt420159.aspx) и автоматизации Здравствуйте, различные ресурсы Azure, связанных с этой подпиской.</span><span class="sxs-lookup"><span data-stu-id="7bdc1-124">Now that you have a management certificate associated with a subscription, you can (after you have installed hello matching certificate locally) programmatically connect toohello [classic deployment model REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate hello various Azure resources that are also associated with that subscription.</span></span>
