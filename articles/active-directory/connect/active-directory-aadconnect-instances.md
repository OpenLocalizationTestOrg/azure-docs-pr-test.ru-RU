---
title: "Azure AD Connect: экземпляры службы синхронизации | Документация Майкрософт"
description: "На этой странице приводятся специальные рекомендации для экземпляров Azure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e8321c3d16253226a5931cacbce6fa5d50b697bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="b6db0-103">Azure AD Connect: специальные рекомендации для экземпляров</span><span class="sxs-lookup"><span data-stu-id="b6db0-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="b6db0-104">Azure AD Connect чаще всего используется с доступным во всем мире экземпляром Azure AD и Office 365.</span><span class="sxs-lookup"><span data-stu-id="b6db0-104">Azure AD Connect is most commonly used with the world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="b6db0-105">Но существуют и другие экземпляры, и они имеют другие требования к URL-адресам и прочие особенности.</span><span class="sxs-lookup"><span data-stu-id="b6db0-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="b6db0-106">Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="b6db0-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="b6db0-107">[Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) — это независимое облако, обслуживаемое управителем данными из Германии.</span><span class="sxs-lookup"><span data-stu-id="b6db0-107">The [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="b6db0-108">URL-адреса для открытия на прокси-сервере</span><span class="sxs-lookup"><span data-stu-id="b6db0-108">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="b6db0-109">\*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="b6db0-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="b6db0-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="b6db0-110">\*.windows.net</span></span> |
| <span data-ttu-id="b6db0-111">+Списки отзыва сертификатов</span><span class="sxs-lookup"><span data-stu-id="b6db0-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="b6db0-112">При входе в клиент Azure AD необходимо использовать учетную запись в домене onmicrosoft.de.</span><span class="sxs-lookup"><span data-stu-id="b6db0-112">When you sign in to your Azure AD tenant, you must use an account in the onmicrosoft.de domain.</span></span>

<span data-ttu-id="b6db0-113">Функции, которые пока отсутствуют в Microsoft Cloud Germany:</span><span class="sxs-lookup"><span data-stu-id="b6db0-113">Features currently not present in the Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="b6db0-114">Служба **Azure AD Connect Health** недоступна.</span><span class="sxs-lookup"><span data-stu-id="b6db0-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="b6db0-115">**Автоматические обновления** недоступны.</span><span class="sxs-lookup"><span data-stu-id="b6db0-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="b6db0-116">**Компонент обратной записи паролей** доступен в предварительной версии в Azure AD Connect версии 1.1.570.0 и более поздних.</span><span class="sxs-lookup"><span data-stu-id="b6db0-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="b6db0-117">Другие службы Azure AD Premium недоступны.</span><span class="sxs-lookup"><span data-stu-id="b6db0-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="b6db0-118">Облако Microsoft Azure для государственных организаций</span><span class="sxs-lookup"><span data-stu-id="b6db0-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="b6db0-119">[Облако Microsoft Azure для государственных организаций](https://azure.microsoft.com/features/gov/) — это облако для правительства США.</span><span class="sxs-lookup"><span data-stu-id="b6db0-119">The [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="b6db0-120">Это облако поддерживается в более ранних выпусках DirSync.</span><span class="sxs-lookup"><span data-stu-id="b6db0-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="b6db0-121">Начиная со сборки 1.1.180 Azure AD Connect поддерживается следующее поколение облака.</span><span class="sxs-lookup"><span data-stu-id="b6db0-121">From build 1.1.180 of Azure AD Connect, the next generation of the cloud is supported.</span></span> <span data-ttu-id="b6db0-122">Это поколение использует базирующиеся только в США конечные точки и имеет другой список URL-адресов для открытия на прокси-сервере.</span><span class="sxs-lookup"><span data-stu-id="b6db0-122">This generation is using US-only based endpoints and have a different list of URLs to open in your proxy server.</span></span>

| <span data-ttu-id="b6db0-123">URL-адреса для открытия на прокси-сервере</span><span class="sxs-lookup"><span data-stu-id="b6db0-123">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="b6db0-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="b6db0-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="b6db0-125">\*.microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="b6db0-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="b6db0-126">\*.gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="b6db0-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="b6db0-127">+Списки отзыва сертификатов</span><span class="sxs-lookup"><span data-stu-id="b6db0-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="b6db0-128">Azure AD Connect не может автоматически определять, что клиент Azure AD находится в облаке правительства США.</span><span class="sxs-lookup"><span data-stu-id="b6db0-128">Azure AD Connect is not able to automatically detect that your Azure AD tenant is located in the Government cloud.</span></span> <span data-ttu-id="b6db0-129">Вместо этого при установке Azure AD Connect необходимо выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b6db0-129">Instead you need to take the following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="b6db0-130">Начните установку Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="b6db0-130">Start the Azure AD Connect installation.</span></span>
2. <span data-ttu-id="b6db0-131">Когда отобразится первая страница, на которой предлагается принять условия лицензионного соглашения, не продолжайте, но и не прерывайте работу мастера установки.</span><span class="sxs-lookup"><span data-stu-id="b6db0-131">When you see the first page where you are supposed to accept the EULA, do not continue but leave the installation wizard running.</span></span>
3. <span data-ttu-id="b6db0-132">Запустите редактор реестра (regedit) и измените раздел реестра `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance`, присвоив ему значение `2`.</span><span class="sxs-lookup"><span data-stu-id="b6db0-132">Start regedit and change the registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` to the value `2`.</span></span>
4. <span data-ttu-id="b6db0-133">Вернитесь в мастер установки Azure AD Connect, примите условия лицензионного соглашения и перейдите к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="b6db0-133">Go back to the Azure AD Connect installation wizard, accept the EULA, and continue.</span></span> <span data-ttu-id="b6db0-134">Во время установки убедитесь, что используется путь установки из **пользовательской конфигурации** (а не экспресс-установка).</span><span class="sxs-lookup"><span data-stu-id="b6db0-134">During installation, make sure to use the **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="b6db0-135">Затем продолжите обычную последовательность установки.</span><span class="sxs-lookup"><span data-stu-id="b6db0-135">Then continue the installation as usual.</span></span>

<span data-ttu-id="b6db0-136">Функции, которые пока отсутствуют в облаке Microsoft Azure для государственных организаций:</span><span class="sxs-lookup"><span data-stu-id="b6db0-136">Features currently not present in the Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="b6db0-137">Служба **Azure AD Connect Health** недоступна.</span><span class="sxs-lookup"><span data-stu-id="b6db0-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="b6db0-138">**Автоматические обновления** недоступны.</span><span class="sxs-lookup"><span data-stu-id="b6db0-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="b6db0-139">**Компонент обратной записи паролей** доступен в предварительной версии в Azure AD Connect версии 1.1.570.0 и более поздних.</span><span class="sxs-lookup"><span data-stu-id="b6db0-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="b6db0-140">Другие службы Azure AD Premium недоступны.</span><span class="sxs-lookup"><span data-stu-id="b6db0-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6db0-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b6db0-141">Next steps</span></span>
<span data-ttu-id="b6db0-142">Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="b6db0-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
