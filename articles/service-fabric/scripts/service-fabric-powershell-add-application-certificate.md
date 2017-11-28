---
title: "Пример сценария PowerShell - aaaAzure добавить кластер tooa cert приложения | Документы Microsoft"
description: "Сценарий Azure PowerShell пример — Добавление кластера Service Fabric tooa сертификатов приложений."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a><span data-ttu-id="33a43-103">Добавить к кластеру Service Fabric tooa сертификата приложения</span><span class="sxs-lookup"><span data-stu-id="33a43-103">Add an application certificate tooa Service Fabric cluster</span></span>

<span data-ttu-id="33a43-104">Этот сценарий создает самозаверяющий сертификат в хранилище ключей заданного Azure hello и устанавливает его tooall узлы кластера Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="33a43-104">This sample script creates a self-signed certificate in hello specified Azure key vault and installs it tooall nodes of hello Service Fabric cluster.</span></span> <span data-ttu-id="33a43-105">также сертификат Hello загружает tooa локальную папку.</span><span class="sxs-lookup"><span data-stu-id="33a43-105">hello certificate also downloads tooa local folder.</span></span> <span data-ttu-id="33a43-106">Имя сертификата, загружаются hello Hello hello совпадает с именем hello hello сертификата в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="33a43-106">hello name of hello downloaded certificate is hello same as hello name of hello certificate in hello key vault.</span></span> <span data-ttu-id="33a43-107">При необходимости настройте параметры hello.</span><span class="sxs-lookup"><span data-stu-id="33a43-107">Customize hello parameters as needed.</span></span>

<span data-ttu-id="33a43-108">При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](/powershell/azure/overview) , а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure.</span><span class="sxs-lookup"><span data-stu-id="33a43-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="33a43-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="33a43-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a><span data-ttu-id="33a43-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="33a43-110">Script explanation</span></span>

<span data-ttu-id="33a43-111">Этот скрипт использует hello, следующие команды: Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="33a43-111">This script uses hello following commands: Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="33a43-112">Команда</span><span class="sxs-lookup"><span data-stu-id="33a43-112">Command</span></span> | <span data-ttu-id="33a43-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="33a43-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="33a43-114">Add-AzureRmServiceFabricApplicationCertificate</span><span class="sxs-lookup"><span data-stu-id="33a43-114">Add-AzureRmServiceFabricApplicationCertificate</span></span>](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | <span data-ttu-id="33a43-115">Добавьте новое приложение сертификат toohello набора масштабирования виртуальных машин, составляющих кластер hello.</span><span class="sxs-lookup"><span data-stu-id="33a43-115">Add a new application certificate toohello virtual machine scale set that make up hello cluster.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="33a43-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="33a43-116">Next steps</span></span>

<span data-ttu-id="33a43-117">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="33a43-117">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="33a43-118">Дополнительные примеры Azure Service Fabric Azure Powershell можно найти в hello [примеры Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="33a43-118">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
