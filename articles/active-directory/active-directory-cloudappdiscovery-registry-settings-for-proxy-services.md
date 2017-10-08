---
title: "Параметры реестра обнаружения приложения для службы прокси-сервера aaaCloud | Документы Microsoft"
description: "Hello цель этой статьи — tooprovide вам hello действия требуется порт hello необходимые tooset tooperform на компьютерах hello агентом hello Cloud App Discovery."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="ca946-103">Параметры реестра Cloud App Discovery для прокси-служб</span><span class="sxs-lookup"><span data-stu-id="ca946-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="ca946-104">По умолчанию агент hello Cloud App Discovery — настроенное toouse только hello порты 80 и 443.</span><span class="sxs-lookup"><span data-stu-id="ca946-104">By default, hello Cloud App Discovery agent is configured toouse only hello ports 80 or 443.</span></span> <span data-ttu-id="ca946-105">Если вы планируете установить Cloud App Discovery в среде с прокси-сервер, который использует другой номер порта (не 80 или 443), необходимо tooconfigure вашей toouse агентов этот порт.</span><span class="sxs-lookup"><span data-stu-id="ca946-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need tooconfigure your agents toouse this port.</span></span> <span data-ttu-id="ca946-106">Настройка Hello основана на раздел реестра.</span><span class="sxs-lookup"><span data-stu-id="ca946-106">hello configuration is based on a registry key.</span></span>

<span data-ttu-id="ca946-107">Hello цель этой статьи — tooprovide вам hello действия требуется порт hello необходимые tooset tooperform на компьютерах hello агентом hello Cloud App Discovery.</span><span class="sxs-lookup"><span data-stu-id="ca946-107">hello objective of this topic is tooprovide you with hello steps you need tooperform tooset hello required port on hello computers running hello Cloud App Discovery agent.</span></span>

<span data-ttu-id="ca946-108">**toomodify hello порт, используемый hello компьютера под управлением агента Cloud App Discovery hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ca946-108">**toomodify hello port used by hello computer running hello Cloud App Discovery agent, perform hello following steps:**</span></span>

1. <span data-ttu-id="ca946-109">Откройте редактор реестра hello.</span><span class="sxs-lookup"><span data-stu-id="ca946-109">Start hello registry editor.</span></span> <br> ![Выполнить](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="ca946-111">Перейдите tooor создать hello следующий раздел реестра:</span><span class="sxs-lookup"><span data-stu-id="ca946-111">Navigate tooor create hello following registry key:</span></span> <br> <span data-ttu-id="ca946-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span><span class="sxs-lookup"><span data-stu-id="ca946-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="ca946-113">Создайте новый **мультистроковый** параметр **Ports**.</span><span class="sxs-lookup"><span data-stu-id="ca946-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="ca946-114">![Создать](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="ca946-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="ca946-115">tooopen hello **Редактирование мультистроки** диалоговое окно, дважды щелкните значение Ports hello.</span><span class="sxs-lookup"><span data-stu-id="ca946-115">tooopen hello **Edit Multi-String** dialog, double-click hello Ports value.</span></span>
5. <span data-ttu-id="ca946-116">Hello значение данных в текстовое поле введите следующие значения hello и добавьте все настраиваемые порты, которые используются в вашей организации:</span><span class="sxs-lookup"><span data-stu-id="ca946-116">In hello Value data textbox, type hello following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="ca946-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="ca946-117">
   **80**</span></span> <br><span data-ttu-id="ca946-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="ca946-118">
   **8080**</span></span> <br><span data-ttu-id="ca946-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="ca946-119">
   **8118**</span></span> <br><span data-ttu-id="ca946-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="ca946-120">
   **8888**</span></span> <br><span data-ttu-id="ca946-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="ca946-121">
   **81**</span></span> <br><span data-ttu-id="ca946-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="ca946-122">
   **12080**</span></span> <br><span data-ttu-id="ca946-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="ca946-123">
**6999**</span></span> <br><span data-ttu-id="ca946-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="ca946-124">
**30606**</span></span> <br><span data-ttu-id="ca946-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="ca946-125">
**31595**</span></span> <br><span data-ttu-id="ca946-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="ca946-126">
**4080**</span></span> <br><span data-ttu-id="ca946-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="ca946-127">
**443**</span></span> <br><span data-ttu-id="ca946-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="ca946-128">
**1110**</span></span> <br><br><span data-ttu-id="ca946-129">
![Редактирование мультистроки](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="ca946-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="ca946-130">Нажмите кнопку **ОК** tooclose hello **Редактирование мультистроки** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ca946-130">Click **OK** tooclose hello **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="ca946-131">**Дополнительные ресурсы**</span><span class="sxs-lookup"><span data-stu-id="ca946-131">**Additional Resources**</span></span>

* [<span data-ttu-id="ca946-132">Как обнаруживать несанкционированные облачные приложения, которые используются в моей организации</span><span class="sxs-lookup"><span data-stu-id="ca946-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

