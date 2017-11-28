---
title: "Настройка PowerShell для создания виртуальной машины для Marketplace | Документация Майкрософт"
description: "Указания по настройке Azure PowerShell и, в качестве дополнения, описание процесса создания образов виртуальных машин для развертывания и продажи в Azure Marketplace"
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
ms.openlocfilehash: bbcce5093d2bbd5326523063db7d0e565fe4de6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-azure-powershell-to-create-an-offer-for-the-azure-marketplace"></a><span data-ttu-id="984df-103">Настройка Azure PowerShell для создания предложения для Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="984df-103">Set up Azure PowerShell to create an offer for the Azure Marketplace</span></span>
<span data-ttu-id="984df-104">Подробные сведения о том, как настроить PowerShell в Azure, см. в статье [Приступая к работе с командлетами Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="984df-104">For detailed information on how to set up PowerShell in Azure, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="984df-105">Простой подход заключается в использовании сертификата. Для этого скачивается и импортируется сертификат, необходимый для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="984df-105">A simple approach is to use the certificate method, which downloads and imports a certificate needed for authentication.</span></span> <span data-ttu-id="984df-106">Чтобы получить необходимый сертификат, используйте командлет **Get-AzurePublishSettingsFile**.</span><span class="sxs-lookup"><span data-stu-id="984df-106">To obtain the needed certificate, use the **Get-AzurePublishSettingsFile** cmdlet.</span></span> <span data-ttu-id="984df-107">Когда появится запрос, сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="984df-107">Save the file when you're prompted.</span></span> <span data-ttu-id="984df-108">Чтобы импортировать сертификат в сеанс PowerShell, используйте командлет **Import-AzurePublishSettingsFile**.</span><span class="sxs-lookup"><span data-stu-id="984df-108">To import the certificate into a PowerShell session, use the **Import-AzurePublishSettingsFile** cmdlet.</span></span>

<span data-ttu-id="984df-109">Чтобы настроить и сохранить общие параметры подписки Microsoft Azure для сеанса PowerShell, используйте командлеты **Set-AzureSubscription** и **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="984df-109">To configure and store the common Microsoft Azure subscription settings for the PowerShell session, use the **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span></span>

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

<span data-ttu-id="984df-110">Первая команда связывает учетную запись хранения по умолчанию с подпиской (требуется для некоторых операций подготовки виртуальной машины).</span><span class="sxs-lookup"><span data-stu-id="984df-110">The first command associates a default storage account with the subscription (needed for some VM provisioning operations).</span></span>  <span data-ttu-id="984df-111">Вторая делает подписку текущей (для других командлетов).</span><span class="sxs-lookup"><span data-stu-id="984df-111">The second makes the subscription the current one (recognized by other cmdlets).</span></span>

## <a name="see-also"></a><span data-ttu-id="984df-112">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="984df-112">See also</span></span>
* [<span data-ttu-id="984df-113">Приступая к работе: как опубликовать предложение в Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="984df-113">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="984df-114">Создание образа виртуальной машины для Marketplace</span><span class="sxs-lookup"><span data-stu-id="984df-114">Creating a virtual machine image for the Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)

