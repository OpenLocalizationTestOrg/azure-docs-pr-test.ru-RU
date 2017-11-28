---
title: "Что такое Azure Stack? | Документация Майкрософт"
description: "Пакет разработчика Azure стек — это среда для оценки Azure стека функции и сценарии."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d9e6aee1-4cba-4df5-b5a3-6f38da9627a3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: helaw
ms.custom: mvc
ms.openlocfilehash: 65278e7b352df5651f04151210ccc34a58dd321a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-azure-stack"></a><span data-ttu-id="7ff58-104">Что такое Azure Stack?</span><span class="sxs-lookup"><span data-stu-id="7ff58-104">What is Azure Stack?</span></span>

<span data-ttu-id="7ff58-105">Стека Microsoft Azure — это платформа гибридного облака, которая позволяет получать служб Azure из центра обработки данных вашей организации.</span><span class="sxs-lookup"><span data-stu-id="7ff58-105">Microsoft Azure Stack is a hybrid cloud platform that lets you deliver Azure services from your organization’s datacenter.</span></span>  <span data-ttu-id="7ff58-106">Стек Azure призвана помочь вам в основные сценарии, например соблюдения требований безопасности и соответствия требованиям, или когда необходимо получить доступ к ресурсам Azure без подключения к Интернету.</span><span class="sxs-lookup"><span data-stu-id="7ff58-106">Azure Stack is designed to help you in key scenarios, like meeting security and compliance requirements, or where you need to access Azure resources without internet connectivity.</span></span>  

## <a name="azure-stack-development-kit"></a><span data-ttu-id="7ff58-107">Набор разработки Azure Stack</span><span class="sxs-lookup"><span data-stu-id="7ff58-107">Azure Stack Development Kit</span></span>
<span data-ttu-id="7ff58-108">Пакет средств разработки Microsoft Azure стек — это версия одного узла Azure стек, который можно использовать для оценки и Дополнительные сведения о стеке Azure.</span><span class="sxs-lookup"><span data-stu-id="7ff58-108">Microsoft Azure Stack Development Kit is a single-node version of Azure Stack, which you can use to evaluate and learn about Azure Stack.</span></span>  <span data-ttu-id="7ff58-109">Также можно использовать пакет средств разработки стек Azure как среды разработки, можно было разрабатывать с помощью согласованные API-интерфейсы и средства.</span><span class="sxs-lookup"><span data-stu-id="7ff58-109">You can also use Azure Stack Development Kit as a developer environment, where you can develop using consistent APIs and tooling.</span></span>  

<span data-ttu-id="7ff58-110">Следует учитывать эти точки с Azure стека Development Kit.</span><span class="sxs-lookup"><span data-stu-id="7ff58-110">You should be aware of these points with Azure Stack Development Kit:</span></span>

* <span data-ttu-id="7ff58-111">Пакет разработчика Azure стека не должны использоваться в производственной среде и должен использоваться только для оценки, тестирования и демонстрации.</span><span class="sxs-lookup"><span data-stu-id="7ff58-111">Azure Stack Development Kit must not be used as a production environment and should only be used for testing, evaluation, and demonstration.</span></span>  
* <span data-ttu-id="7ff58-112">Развертывание стека Azure связана с одного поставщика удостоверений Azure Active Directory или служб федерации Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7ff58-112">Your deployment of Azure Stack is associated with a single Azure Active Directory or Active Directory Federation Services identity provider.</span></span> <span data-ttu-id="7ff58-113">В этом каталоге можно создать несколько пользователей и назначить им подписки.</span><span class="sxs-lookup"><span data-stu-id="7ff58-113">You can create multiple users in this directory and assign subscriptions to each user.</span></span>
* <span data-ttu-id="7ff58-114">Так как все компоненты развернуты на одном компьютере, для ресурсов клиента доступны ограниченные физические ресурсы.</span><span class="sxs-lookup"><span data-stu-id="7ff58-114">With all components deployed on the single machine, there are limited physical resources available for tenant resources.</span></span> <span data-ttu-id="7ff58-115">Эта конфигурация не предназначен для оценки масштабирования и производительности.</span><span class="sxs-lookup"><span data-stu-id="7ff58-115">This configuration is not intended for scale or performance evaluation.</span></span>
* <span data-ttu-id="7ff58-116">Также ограничено применение в сетевых сценариях, что обусловлено обязательным одним излом или сетевой картой.</span><span class="sxs-lookup"><span data-stu-id="7ff58-116">Networking scenarios are limited due to the single host/NIC requirement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ff58-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7ff58-117">Next steps</span></span>
[<span data-ttu-id="7ff58-118">Основные возможности и концепции</span><span class="sxs-lookup"><span data-stu-id="7ff58-118">Key features and concepts</span></span>](azure-stack-key-features.md)

[<span data-ttu-id="7ff58-119">Инновации гибридных приложений с Azure и Azure стека (pdf)</span><span class="sxs-lookup"><span data-stu-id="7ff58-119">Hybrid Application innovation with Azure and Azure Stack (pdf)</span></span>](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409)

