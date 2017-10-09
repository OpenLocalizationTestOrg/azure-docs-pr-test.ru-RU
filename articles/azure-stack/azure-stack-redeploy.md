---
title: "aaaRedeploy стек Azure | Документы Microsoft"
description: "Повторное развертывание стек Azure."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 795af5ea-892d-40b1-a080-42e4472e4bba
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: erikje
ms.openlocfilehash: ec26745bcb54edd7c26960eec55d41504aff1911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-azure-stack"></a><span data-ttu-id="31720-103">Повторное развертывание стек Azure</span><span class="sxs-lookup"><span data-stu-id="31720-103">Redeploy Azure Stack</span></span>
<span data-ttu-id="31720-104">tooredeploy стек Azure вы должны начать с нуля как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="31720-104">tooredeploy Azure Stack, you must start over from scratch as described below.</span></span>

## <a name="steps-tooredeploy-azure-stack"></a><span data-ttu-id="31720-105">Действия tooredeploy стек Azure</span><span class="sxs-lookup"><span data-stu-id="31720-105">Steps tooredeploy Azure Stack</span></span>
1. <span data-ttu-id="31720-106">На узел комплект средств для разработки hello, откройте консоль PowerShell с повышенными привилегиями > перейдите сценарий asdk installer.ps1 toohello > запустите его > щелкните **перезагрузки**.</span><span class="sxs-lookup"><span data-stu-id="31720-106">On hello development kit host, open an elevated PowerShell console > navigate toohello asdk-installer.ps1 script > run it > click **Reboot**.</span></span>
2. <span data-ttu-id="31720-107">Здравствуйте, выберите базовую операционную систему (не **стека Azure**) и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31720-107">Select hello base operating system (not **Azure Stack**) and click **Next**.</span></span>
3. <span data-ttu-id="31720-108">После перезагрузки узла комплект средств для разработки hello, удалите файл CloudBuilder.vhdx hello, который использовался в рамках предыдущего развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="31720-108">After hello development kit host reboots, delete hello CloudBuilder.vhdx file that was used as part of hello previous deployment.</span></span>
4. <span data-ttu-id="31720-109">[Развертывание пакета средств разработки hello](azure-stack-run-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="31720-109">[Deploy hello development kit](azure-stack-run-powershell-script.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31720-110">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="31720-110">Next steps</span></span>
[<span data-ttu-id="31720-111">Подключение tooAzure стека</span><span class="sxs-lookup"><span data-stu-id="31720-111">Connect tooAzure Stack</span></span>](azure-stack-connect-azure-stack.md)

