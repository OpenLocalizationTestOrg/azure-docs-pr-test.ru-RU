---
title: "Создание контейнера облачной службы с помощью PowerShell | Документация Майкрософт"
description: "В этой статье объясняется, как создать контейнер облачной службы с помощью PowerShell. В контейнере размещаются веб- и рабочие роли."
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
ms.openlocfilehash: 2023fa7b318f9f76ce1e1ea0a46110297be9a001
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-an-azure-powershell-command-to-create-an-empty-cloud-service-container"></a><span data-ttu-id="7f64e-104">Использование команды Azure PowerShell для создания пустого контейнера облачной службы</span><span class="sxs-lookup"><span data-stu-id="7f64e-104">Use an Azure PowerShell command to create an empty cloud service container</span></span>
<span data-ttu-id="7f64e-105">В этой статье объясняется, как быстро создать контейнер облачных служб с помощью командлетов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f64e-105">This article explains how to quickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="7f64e-106">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7f64e-106">Please follow the steps below:</span></span>

1. <span data-ttu-id="7f64e-107">Установите командлет Microsoft Azure PowerShell со страницы [Загрузки Azure PowerShell](http://aka.ms/webpi-azps) .</span><span class="sxs-lookup"><span data-stu-id="7f64e-107">Install the Microsoft Azure PowerShell cmdlet from the [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="7f64e-108">Запустите командную строку PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f64e-108">Open the PowerShell command prompt.</span></span>
3. <span data-ttu-id="7f64e-109">Войдите, используя [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) .</span><span class="sxs-lookup"><span data-stu-id="7f64e-109">Use the [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) to sign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7f64e-110">Инструкции по установке командлета Azure PowerShell и подключению к подписке Azure см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7f64e-110">For further instruction on installing the Azure PowerShell cmdlet and connecting to your Azure subscription, refer to [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
   >
   >
4. <span data-ttu-id="7f64e-111">Используйте командлет **New-AzureService** , чтобы создать пустой контейнер облачной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="7f64e-111">Use the **New-AzureService** cmdlet to create an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="7f64e-112">Ниже приводится пример вызова командлета:</span><span class="sxs-lookup"><span data-stu-id="7f64e-112">Follow this example to invoke the cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="7f64e-113">Чтобы получить дополнительные сведения о создании облачной службы Azure, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7f64e-113">For more information about creating the Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="7f64e-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7f64e-114">Next steps</span></span>
* <span data-ttu-id="7f64e-115">Чтобы управлять развертыванием облачной службы, используйте команды [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx) и [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f64e-115">To manage the cloud service deployment, refer to the [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="7f64e-116">Кроме того, дополнительные сведения можно получить в статье [Настройка облачных служб](cloud-services-how-to-configure.md) .</span><span class="sxs-lookup"><span data-stu-id="7f64e-116">You may also refer to [How to configure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="7f64e-117">Чтобы опубликовать проект облачной службы в Azure, используйте образец кода **PublishCloudService.ps1** из статьи [Непрерывная доставка для облачных служб в Azure](cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="7f64e-117">To publish your cloud service project to Azure, refer to the  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
