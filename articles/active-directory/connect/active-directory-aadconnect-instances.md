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
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="49f48-103">Azure AD Connect: специальные рекомендации для экземпляров</span><span class="sxs-lookup"><span data-stu-id="49f48-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="49f48-104">Чаще всего используется Azure AD Connect с hello world wide экземпляром Azure AD и Office 365.</span><span class="sxs-lookup"><span data-stu-id="49f48-104">Azure AD Connect is most commonly used with hello world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="49f48-105">Но существуют и другие экземпляры, и они имеют другие требования к URL-адресам и прочие особенности.</span><span class="sxs-lookup"><span data-stu-id="49f48-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="49f48-106">Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="49f48-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="49f48-107">Hello [Германия Microsoft Cloud](http://www.microsoft.de/cloud-deutschland) sovereign облако, обслуживаемой немецком данных доверенного лица.</span><span class="sxs-lookup"><span data-stu-id="49f48-107">hello [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="49f48-108">Tooopen URL-адреса в прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="49f48-108">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="49f48-109">\*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="49f48-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="49f48-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="49f48-110">\*.windows.net</span></span> |
| <span data-ttu-id="49f48-111">+Списки отзыва сертификатов</span><span class="sxs-lookup"><span data-stu-id="49f48-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="49f48-112">Когда вы войдете в клиенте Azure AD tooyour, необходимо использовать учетную запись в домене onmicrosoft.de hello.</span><span class="sxs-lookup"><span data-stu-id="49f48-112">When you sign in tooyour Azure AD tenant, you must use an account in hello onmicrosoft.de domain.</span></span>

<span data-ttu-id="49f48-113">В настоящее время не присутствует в Германии Microsoft Cloud hello функции:</span><span class="sxs-lookup"><span data-stu-id="49f48-113">Features currently not present in hello Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="49f48-114">Служба **Azure AD Connect Health** недоступна.</span><span class="sxs-lookup"><span data-stu-id="49f48-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="49f48-115">**Автоматические обновления** недоступны.</span><span class="sxs-lookup"><span data-stu-id="49f48-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="49f48-116">**Компонент обратной записи паролей** доступен в предварительной версии в Azure AD Connect версии 1.1.570.0 и более поздних.</span><span class="sxs-lookup"><span data-stu-id="49f48-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="49f48-117">Другие службы Azure AD Premium недоступны.</span><span class="sxs-lookup"><span data-stu-id="49f48-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="49f48-118">Облако Microsoft Azure для государственных организаций</span><span class="sxs-lookup"><span data-stu-id="49f48-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="49f48-119">Hello [облако Microsoft Azure для государственных](https://azure.microsoft.com/features/gov/) облако для государственных организаций США.</span><span class="sxs-lookup"><span data-stu-id="49f48-119">hello [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="49f48-120">Это облако поддерживается в более ранних выпусках DirSync.</span><span class="sxs-lookup"><span data-stu-id="49f48-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="49f48-121">Сборки 1.1.180 Azure AD Connect hello следующего поколения облака hello поддерживается.</span><span class="sxs-lookup"><span data-stu-id="49f48-121">From build 1.1.180 of Azure AD Connect, hello next generation of hello cloud is supported.</span></span> <span data-ttu-id="49f48-122">Это поколение используется только для США на основе конечных точек и имеют разные списки tooopen URL-адреса в прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="49f48-122">This generation is using US-only based endpoints and have a different list of URLs tooopen in your proxy server.</span></span>

| <span data-ttu-id="49f48-123">Tooopen URL-адреса в прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="49f48-123">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="49f48-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="49f48-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="49f48-125">\*.microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="49f48-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="49f48-126">\*.gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="49f48-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="49f48-127">+Списки отзыва сертификатов</span><span class="sxs-lookup"><span data-stu-id="49f48-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="49f48-128">Azure AD Connect не может обнаружить tooautomatically, клиент Azure AD находится в облаке государственных hello.</span><span class="sxs-lookup"><span data-stu-id="49f48-128">Azure AD Connect is not able tooautomatically detect that your Azure AD tenant is located in hello Government cloud.</span></span> <span data-ttu-id="49f48-129">Вместо этого необходимо hello tootake при установке Azure AD Connect следующие действия.</span><span class="sxs-lookup"><span data-stu-id="49f48-129">Instead you need tootake hello following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="49f48-130">Запустите установку hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="49f48-130">Start hello Azure AD Connect installation.</span></span>
2. <span data-ttu-id="49f48-131">При появлении hello первую страницу, где должны tooaccept hello лицензионного соглашения, не продолжайте, но оставьте работы мастера установки hello.</span><span class="sxs-lookup"><span data-stu-id="49f48-131">When you see hello first page where you are supposed tooaccept hello EULA, do not continue but leave hello installation wizard running.</span></span>
3. <span data-ttu-id="49f48-132">Запустите редактор реестра и изменить раздел реестра hello `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello значение `2`.</span><span class="sxs-lookup"><span data-stu-id="49f48-132">Start regedit and change hello registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello value `2`.</span></span>
4. <span data-ttu-id="49f48-133">Вернитесь в мастер установки toohello Azure AD Connect, принять лицензионное соглашение hello и продолжить.</span><span class="sxs-lookup"><span data-stu-id="49f48-133">Go back toohello Azure AD Connect installation wizard, accept hello EULA, and continue.</span></span> <span data-ttu-id="49f48-134">Во время установки, убедитесь, что hello toouse **пользовательской конфигурации** путь установки (и не экспресс-установки).</span><span class="sxs-lookup"><span data-stu-id="49f48-134">During installation, make sure toouse hello **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="49f48-135">Затем продолжите установку hello обычным образом.</span><span class="sxs-lookup"><span data-stu-id="49f48-135">Then continue hello installation as usual.</span></span>

<span data-ttu-id="49f48-136">В настоящее время не присутствует в облако Microsoft Azure для государственных hello функции:</span><span class="sxs-lookup"><span data-stu-id="49f48-136">Features currently not present in hello Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="49f48-137">Служба **Azure AD Connect Health** недоступна.</span><span class="sxs-lookup"><span data-stu-id="49f48-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="49f48-138">**Автоматические обновления** недоступны.</span><span class="sxs-lookup"><span data-stu-id="49f48-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="49f48-139">**Компонент обратной записи паролей** доступен в предварительной версии в Azure AD Connect версии 1.1.570.0 и более поздних.</span><span class="sxs-lookup"><span data-stu-id="49f48-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="49f48-140">Другие службы Azure AD Premium недоступны.</span><span class="sxs-lookup"><span data-stu-id="49f48-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49f48-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="49f48-141">Next steps</span></span>
<span data-ttu-id="49f48-142">Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="49f48-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
