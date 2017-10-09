---
title: "aaaDevelop приложений для Azure стек | Документы Microsoft"
description: "Дополнительные сведения, рекомендации по разработке в приложениях создания прототипов стек Azure"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d3ebc6b1-0ffe-4d3e-ba4a-388239d6cdc3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 9bea75d0f0ecf19c05ff55ac3ef4e778d53a1912
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-stack"></a><span data-ttu-id="035b9-103">Разработка для Azure Stack</span><span class="sxs-lookup"><span data-stu-id="035b9-103">Develop for Azure Stack</span></span>
<span data-ttu-id="035b9-104">Вы можете приступить к разработке приложений в настоящее время даже при отсутствии доступа tooan Azure стека среды.</span><span class="sxs-lookup"><span data-stu-id="035b9-104">You can get started developing applications today, even if you don't have access tooan Azure Stack environment.</span></span> <span data-ttu-id="035b9-105">Поскольку стек Azure обеспечивает службы Microsoft Azure, выполняемых в вашем центре обработки данных, можно использовать аналогичные средства и процессы toodevelop к стеку Azure, как и с Azure.</span><span class="sxs-lookup"><span data-stu-id="035b9-105">Because Azure Stack delivers Microsoft Azure services that run in your datacenter, you can use similar tools and processes toodevelop against Azure Stack as you would with Azure.</span></span>  <span data-ttu-id="035b9-106">Битом подготовки и руководств по hello следующие вопросы можно использовать Azure tooemulate среду стека Azure:</span><span class="sxs-lookup"><span data-stu-id="035b9-106">With a bit of preparation and guidance from hello following topics, you can use Azure tooemulate an Azure Stack environment:</span></span>

* <span data-ttu-id="035b9-107">В Azure можно создавать шаблоны Azure Resource Manager, которые также развертываемых tooAzure стека.</span><span class="sxs-lookup"><span data-stu-id="035b9-107">In Azure, you can create Azure Resource Manager templates that are also deployable tooAzure Stack.</span></span>  <span data-ttu-id="035b9-108">В разделе [рекомендации по шаблонам](azure-stack-develop-templates.md) рекомендации по разработке вашей переносимость tooensure шаблонов.</span><span class="sxs-lookup"><span data-stu-id="035b9-108">See [template considerations](azure-stack-develop-templates.md) for guidance on developing your templates tooensure portability.</span></span>
* <span data-ttu-id="035b9-109">Нет изменений в службы доступности и управление версиями службы между Azure и Azure стека.</span><span class="sxs-lookup"><span data-stu-id="035b9-109">There is a delta in service availability and service versioning between Azure and Azure Stack.</span></span> <span data-ttu-id="035b9-110">Можно использовать hello [модуля политики Azure стека](azure-stack-policy-module.md) toorestrict службы Azure доступности и ресурсов типы toowhat в стек Azure.</span><span class="sxs-lookup"><span data-stu-id="035b9-110">You can use hello [Azure Stack policy module](azure-stack-policy-module.md) toorestrict Azure service availability and resource types toowhat's available in Azure Stack.</span></span> <span data-ttu-id="035b9-111">Ограничить доступные службы поможет приложения используют службы доступны tooAzure стека.</span><span class="sxs-lookup"><span data-stu-id="035b9-111">Constraining available services will help your application rely on services available tooAzure Stack.</span></span>
* <span data-ttu-id="035b9-112">Hello [шаблоны быстрый запуск Azure стека](https://github.com/Azure/AzureStack-QuickStart-Templates) приведены распространенные примеры сценарий toodevelop шаблонами, поэтому они могут быть развернуты tooboth Azure и Azure стека.</span><span class="sxs-lookup"><span data-stu-id="035b9-112">hello [Azure Stack Quickstart Templates](https://github.com/Azure/AzureStack-QuickStart-Templates) are common scenario examples of how toodevelop your templates so they can be deployed tooboth Azure and Azure Stack.</span></span>


