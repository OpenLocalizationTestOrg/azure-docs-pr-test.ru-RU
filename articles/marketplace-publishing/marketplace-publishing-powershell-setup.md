---
title: "aaaSet копирование toocreate PowerShell виртуальной Машины для hello Marketplace | Документы Microsoft"
description: "Инструкции по установке Azure PowerShell и использовать ее в качестве необязательный процесс потока toocreate toodeploy образы виртуальных Машин и продавать, hello Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: cd2ebad7472248b8f921706e1a8c82d41f33b9cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a><span data-ttu-id="36aad-103">Настройка Azure PowerShell toocreate предложение hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="36aad-103">Set up Azure PowerShell toocreate an offer for hello Azure Marketplace</span></span>
<span data-ttu-id="36aad-104">Подробные сведения о том, как tooset копирование PowerShell в Azure, в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="36aad-104">For detailed information on how tooset up PowerShell in Azure, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="36aad-105">Простой подход — toouse hello сертификат метод, который загружает и импортирует сертификат, необходимый для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="36aad-105">A simple approach is toouse hello certificate method, which downloads and imports a certificate needed for authentication.</span></span> <span data-ttu-id="36aad-106">требуется сертификат, используйте hello tooobtain hello **Get-AzurePublishSettingsFile** командлета.</span><span class="sxs-lookup"><span data-stu-id="36aad-106">tooobtain hello needed certificate, use hello **Get-AzurePublishSettingsFile** cmdlet.</span></span> <span data-ttu-id="36aad-107">Сохраните файл hello, когда появится запрос.</span><span class="sxs-lookup"><span data-stu-id="36aad-107">Save hello file when you're prompted.</span></span> <span data-ttu-id="36aad-108">сертификат tooimport hello в сеанс PowerShell, используйте hello **команду Import-AzurePublishSettingsFile** командлета.</span><span class="sxs-lookup"><span data-stu-id="36aad-108">tooimport hello certificate into a PowerShell session, use hello **Import-AzurePublishSettingsFile** cmdlet.</span></span>

<span data-ttu-id="36aad-109">tooconfigure и хранилище hello общих Microsoft Azure подписки для параметров сеанса PowerShell hello, используется hello **Set-AzureSubscription** и **Select-AzureSubscription** командлетов:</span><span class="sxs-lookup"><span data-stu-id="36aad-109">tooconfigure and store hello common Microsoft Azure subscription settings for hello PowerShell session, use hello **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span></span>

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

<span data-ttu-id="36aad-110">Первая команда Hello связывает учетную запись хранения по умолчанию с hello подписки (требуется для некоторых операций подготовки виртуальной Машины).</span><span class="sxs-lookup"><span data-stu-id="36aad-110">hello first command associates a default storage account with hello subscription (needed for some VM provisioning operations).</span></span>  <span data-ttu-id="36aad-111">Во-вторых Hello делает подписки hello hello текущим (распознать другими командлетами).</span><span class="sxs-lookup"><span data-stu-id="36aad-111">hello second makes hello subscription hello current one (recognized by other cmdlets).</span></span>

## <a name="see-also"></a><span data-ttu-id="36aad-112">См. также</span><span class="sxs-lookup"><span data-stu-id="36aad-112">See also</span></span>
* [<span data-ttu-id="36aad-113">Приступая к работе: как toopublish toohello предложение Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="36aad-113">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="36aad-114">Создание образа виртуальной машины для hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="36aad-114">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)

