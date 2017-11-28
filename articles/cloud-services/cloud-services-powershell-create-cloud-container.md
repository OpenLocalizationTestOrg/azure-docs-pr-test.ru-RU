---
title: "aaaCreate контейнер облачной службы с помощью PowerShell | Документы Microsoft"
description: "В этой статье объясняется, как toocreate облачной службы контейнера с помощью PowerShell. контейнер Hello находится рабочих и веб-ролей."
services: cloud-services
documentationcenter: .net
author: cawaMS
manager: timlt
editor: 
ms.assetid: c8f32469-610e-4f37-a3aa-4fac5c714e13
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 4c47b10b5ba1f9cc39594a45cd869bf04fcaadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a><span data-ttu-id="8bb86-104">Использование Azure PowerShell команды toocreate контейнер пустой облачной службы</span><span class="sxs-lookup"><span data-stu-id="8bb86-104">Use an Azure PowerShell command toocreate an empty cloud service container</span></span>
<span data-ttu-id="8bb86-105">В этой статье объясняется, как tooquickly создать контейнер облачные службы с помощью командлетов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8bb86-105">This article explains how tooquickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="8bb86-106">Выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="8bb86-106">Please follow hello steps below:</span></span>

1. <span data-ttu-id="8bb86-107">Установка командлетов Microsoft Azure PowerShell hello из hello [Azure PowerShell загружает](http://aka.ms/webpi-azps) страницы.</span><span class="sxs-lookup"><span data-stu-id="8bb86-107">Install hello Microsoft Azure PowerShell cmdlet from hello [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="8bb86-108">Откройте командную строку PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="8bb86-108">Open hello PowerShell command prompt.</span></span>
3. <span data-ttu-id="8bb86-109">Используйте hello [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign в.</span><span class="sxs-lookup"><span data-stu-id="8bb86-109">Use hello [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8bb86-110">Дополнительные инструкции по установке командлет Azure PowerShell hello и подключении tooyour подписки Azure см. в разделе слишком[как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8bb86-110">For further instruction on installing hello Azure PowerShell cmdlet and connecting tooyour Azure subscription, refer too[How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
   >
   >
4. <span data-ttu-id="8bb86-111">Используйте hello **New-AzureService** toocreate командлет контейнер пустой Azure облачной службы.</span><span class="sxs-lookup"><span data-stu-id="8bb86-111">Use hello **New-AzureService** cmdlet toocreate an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="8bb86-112">Выполните этот командлет пример tooinvoke hello.</span><span class="sxs-lookup"><span data-stu-id="8bb86-112">Follow this example tooinvoke hello cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="8bb86-113">Дополнительные сведения о создании hello облачной службы Azure выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8bb86-113">For more information about creating hello Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="8bb86-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8bb86-114">Next steps</span></span>
* <span data-ttu-id="8bb86-115">toomanage hello развертывание облачной службы см. в toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), и [AzureService набора](https://msdn.microsoft.com/library/azure/dn495242.aspx) команды.</span><span class="sxs-lookup"><span data-stu-id="8bb86-115">toomanage hello cloud service deployment, refer toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="8bb86-116">Можно также указать слишком[как tooconfigure облачные службы](cloud-services-how-to-configure.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="8bb86-116">You may also refer too[How tooconfigure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="8bb86-117">toopublish облачной службы проекта tooAzure см. в toohello **PublishCloudService.ps1** образец кода из [непрерывная доставка для облачной службы в Azure](cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="8bb86-117">toopublish your cloud service project tooAzure, refer toohello  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
