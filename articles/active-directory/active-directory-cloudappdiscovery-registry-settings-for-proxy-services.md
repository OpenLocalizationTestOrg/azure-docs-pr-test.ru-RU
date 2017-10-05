---
title: "Параметры реестра Cloud App Discovery для прокси-служб | Документация Майкрософт"
description: "В этой статье приведены шаги, которые необходимо выполнить, чтобы задать требуемый порт на компьютере с запущенным агентом Cloud App Discovery."
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
ms.openlocfilehash: ea15dc9a9f20a296e622c8fb1011f7ee99de3e99
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="bdb76-103">Параметры реестра Cloud App Discovery для прокси-служб</span><span class="sxs-lookup"><span data-stu-id="bdb76-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="bdb76-104">По умолчанию агент Cloud App Discovery настроен на использование только портов 80 и 443.</span><span class="sxs-lookup"><span data-stu-id="bdb76-104">By default, the Cloud App Discovery agent is configured to use only the ports 80 or 443.</span></span> <span data-ttu-id="bdb76-105">Если вы планируете установить Cloud App Discovery в среде с прокси-сервером, который использует другой порт (не 80 или 443), необходимо настроить агенты на использование этого порта.</span><span class="sxs-lookup"><span data-stu-id="bdb76-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need to configure your agents to use this port.</span></span> <span data-ttu-id="bdb76-106">Конфигурация основана на разделе реестра.</span><span class="sxs-lookup"><span data-stu-id="bdb76-106">The configuration is based on a registry key.</span></span>

<span data-ttu-id="bdb76-107">В этой статье приведены шаги, которые необходимо выполнить, чтобы задать требуемый порт на компьютере с запущенным агентом Cloud App Discovery.</span><span class="sxs-lookup"><span data-stu-id="bdb76-107">The objective of this topic is to provide you with the steps you need to perform to set the required port on the computers running the Cloud App Discovery agent.</span></span>

<span data-ttu-id="bdb76-108">**Чтобы изменить порт, используемый на компьютере с запущенным агентом Cloud App Discovery, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="bdb76-108">**To modify the port used by the computer running the Cloud App Discovery agent, perform the following steps:**</span></span>

1. <span data-ttu-id="bdb76-109">Откройте редактор реестра.</span><span class="sxs-lookup"><span data-stu-id="bdb76-109">Start the registry editor.</span></span> <br> ![Выполнить](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="bdb76-111">Перейдите в следующий раздел реестра или создайте его: </span><span class="sxs-lookup"><span data-stu-id="bdb76-111">Navigate to or create the following registry key:</span></span> <br> <span data-ttu-id="bdb76-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span><span class="sxs-lookup"><span data-stu-id="bdb76-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="bdb76-113">Создайте новый **мультистроковый** параметр **Ports**.</span><span class="sxs-lookup"><span data-stu-id="bdb76-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="bdb76-114">![Создать](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="bdb76-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="bdb76-115">Откройте диалоговое окно **Редактирование мультистроки** , дважды щелкнув значение Ports.</span><span class="sxs-lookup"><span data-stu-id="bdb76-115">To open the **Edit Multi-String** dialog, double-click the Ports value.</span></span>
5. <span data-ttu-id="bdb76-116">В текстовом поле «Данные параметра» введите следующие значения и добавьте все настраиваемые порты, которые используются в вашей организации: </span><span class="sxs-lookup"><span data-stu-id="bdb76-116">In the Value data textbox, type the following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="bdb76-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="bdb76-117">
   **80**</span></span> <br><span data-ttu-id="bdb76-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="bdb76-118">
   **8080**</span></span> <br><span data-ttu-id="bdb76-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="bdb76-119">
   **8118**</span></span> <br><span data-ttu-id="bdb76-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="bdb76-120">
   **8888**</span></span> <br><span data-ttu-id="bdb76-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="bdb76-121">
   **81**</span></span> <br><span data-ttu-id="bdb76-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="bdb76-122">
   **12080**</span></span> <br><span data-ttu-id="bdb76-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="bdb76-123">
**6999**</span></span> <br><span data-ttu-id="bdb76-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="bdb76-124">
**30606**</span></span> <br><span data-ttu-id="bdb76-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="bdb76-125">
**31595**</span></span> <br><span data-ttu-id="bdb76-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="bdb76-126">
**4080**</span></span> <br><span data-ttu-id="bdb76-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="bdb76-127">
**443**</span></span> <br><span data-ttu-id="bdb76-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="bdb76-128">
**1110**</span></span> <br><br><span data-ttu-id="bdb76-129">
![Редактирование мультистроки](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="bdb76-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="bdb76-130">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Редактирование мультистроки**.</span><span class="sxs-lookup"><span data-stu-id="bdb76-130">Click **OK** to close the **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="bdb76-131">**Дополнительные ресурсы**</span><span class="sxs-lookup"><span data-stu-id="bdb76-131">**Additional Resources**</span></span>

* [<span data-ttu-id="bdb76-132">Как обнаруживать несанкционированные облачные приложения, которые используются в моей организации</span><span class="sxs-lookup"><span data-stu-id="bdb76-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

