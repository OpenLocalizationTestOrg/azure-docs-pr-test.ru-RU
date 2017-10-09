---
title: "aaaWhat — стек Azure? | Документация Майкрософт"
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
ms.openlocfilehash: 3f7c84f2302a6411f49a07de171501fbd72812e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-stack"></a><span data-ttu-id="64521-104">Что такое Azure Stack?</span><span class="sxs-lookup"><span data-stu-id="64521-104">What is Azure Stack?</span></span>

<span data-ttu-id="64521-105">Стека Microsoft Azure — это платформа гибридного облака, которая позволяет получать служб Azure из центра обработки данных вашей организации.</span><span class="sxs-lookup"><span data-stu-id="64521-105">Microsoft Azure Stack is a hybrid cloud platform that lets you deliver Azure services from your organization’s datacenter.</span></span>  <span data-ttu-id="64521-106">Стек Azure — спроектированный toohelp в основные сценарии, например соблюдения требований безопасности и соответствия требованиям, или когда нужен tooaccess ресурсы Azure без подключения к Интернету.</span><span class="sxs-lookup"><span data-stu-id="64521-106">Azure Stack is designed toohelp you in key scenarios, like meeting security and compliance requirements, or where you need tooaccess Azure resources without internet connectivity.</span></span>  

## <a name="azure-stack-development-kit"></a><span data-ttu-id="64521-107">Набор разработки Azure Stack</span><span class="sxs-lookup"><span data-stu-id="64521-107">Azure Stack Development Kit</span></span>
<span data-ttu-id="64521-108">Пакет средств разработки Microsoft Azure стек — это версия одного узла Azure стека, который затем можно использовать tooevaluate и получить дополнительные сведения о стеке Azure.</span><span class="sxs-lookup"><span data-stu-id="64521-108">Microsoft Azure Stack Development Kit is a single-node version of Azure Stack, which you can use tooevaluate and learn about Azure Stack.</span></span>  <span data-ttu-id="64521-109">Также можно использовать пакет средств разработки стек Azure как среды разработки, можно было разрабатывать с помощью согласованные API-интерфейсы и средства.</span><span class="sxs-lookup"><span data-stu-id="64521-109">You can also use Azure Stack Development Kit as a developer environment, where you can develop using consistent APIs and tooling.</span></span>  

<span data-ttu-id="64521-110">Следует учитывать эти точки с Azure стека Development Kit.</span><span class="sxs-lookup"><span data-stu-id="64521-110">You should be aware of these points with Azure Stack Development Kit:</span></span>

* <span data-ttu-id="64521-111">Пакет разработчика Azure стека не должны использоваться в производственной среде и должен использоваться только для оценки, тестирования и демонстрации.</span><span class="sxs-lookup"><span data-stu-id="64521-111">Azure Stack Development Kit must not be used as a production environment and should only be used for testing, evaluation, and demonstration.</span></span>  
* <span data-ttu-id="64521-112">Развертывание стека Azure связана с одного поставщика удостоверений Azure Active Directory или служб федерации Active Directory.</span><span class="sxs-lookup"><span data-stu-id="64521-112">Your deployment of Azure Stack is associated with a single Azure Active Directory or Active Directory Federation Services identity provider.</span></span> <span data-ttu-id="64521-113">Можно создать несколько пользователей в этом каталоге и назначить пользователя tooeach подписки.</span><span class="sxs-lookup"><span data-stu-id="64521-113">You can create multiple users in this directory and assign subscriptions tooeach user.</span></span>
* <span data-ttu-id="64521-114">Со всеми компонентами, развернуты на одном компьютере hello доступны только физические ресурсы для ресурсов клиента.</span><span class="sxs-lookup"><span data-stu-id="64521-114">With all components deployed on hello single machine, there are limited physical resources available for tenant resources.</span></span> <span data-ttu-id="64521-115">Эта конфигурация не предназначен для оценки масштабирования и производительности.</span><span class="sxs-lookup"><span data-stu-id="64521-115">This configuration is not intended for scale or performance evaluation.</span></span>
* <span data-ttu-id="64521-116">Сценарии сети ограничены из-за требований toohello одного узла или сетевого Адаптера.</span><span class="sxs-lookup"><span data-stu-id="64521-116">Networking scenarios are limited due toohello single host/NIC requirement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64521-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="64521-117">Next steps</span></span>
[<span data-ttu-id="64521-118">Основные возможности и концепции</span><span class="sxs-lookup"><span data-stu-id="64521-118">Key features and concepts</span></span>](azure-stack-key-features.md)

[<span data-ttu-id="64521-119">Инновации гибридных приложений с Azure и Azure стека (pdf)</span><span class="sxs-lookup"><span data-stu-id="64521-119">Hybrid Application innovation with Azure and Azure Stack (pdf)</span></span>](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409)

