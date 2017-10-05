---
title: "Развертывание шаблонов с помощью командной строки в стеке Azure | Документы Microsoft"
description: "Сведения об использовании интерфейса кросс платформенных командной строки (CLI) для развертывания шаблонов Azure стека."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 9584177f-4af3-4834-864d-930b09ae0995
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: cd1b61899ead7b4e86a81125841c1b37d019280b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-templates-in-azure-stack-using-the-command-line"></a><span data-ttu-id="1a266-103">Развертывание шаблонов в Azure Stack с помощью командной строки</span><span class="sxs-lookup"><span data-stu-id="1a266-103">Deploy templates in Azure Stack using the command line</span></span>
<span data-ttu-id="1a266-104">Использование командной строки для развертывания пакета средств разработки Azure стека шаблонов диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="1a266-104">Use the command line to deploy Azure Resource Manager templates to the Azure Stack Development Kit.</span></span> <span data-ttu-id="1a266-105">Шаблоны диспетчера ресурсов Azure, развертывание и предоставление все ресурсы для приложения в один, согласованной операции.</span><span class="sxs-lookup"><span data-stu-id="1a266-105">Azure Resource Manager templates deploy and provision all the resources for your application in a single, coordinated operation.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1a266-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="1a266-106">Before you begin</span></span>
 - <span data-ttu-id="1a266-107">[Установка и подключение](azure-stack-connect-cli.md) стек Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1a266-107">[Install and connect](azure-stack-connect-cli.md) to Azure Stack with Azure CLI</span></span>
 - <span data-ttu-id="1a266-108">Загрузите файлы *azuredeploy.json* и *azuredeploy.parameters.json* из [Создание шаблона пример учетной записи хранилища](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="1a266-108">Download the files *azuredeploy.json* and *azuredeploy.parameters.json* from the [create storage account example template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account).</span></span>
 
## <a name="deploy-template"></a><span data-ttu-id="1a266-109">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="1a266-109">Deploy template</span></span>
<span data-ttu-id="1a266-110">Перейдите к папке, где эти файлы были загружены и выполните следующую команду для развертывания шаблона:</span><span class="sxs-lookup"><span data-stu-id="1a266-110">Navigate to the folder where these files were downloaded and run the following command to deploy the template:</span></span>

    azure group create "cliRG" "local" –f azuredeploy.json –d "testDeploy" –e azuredeploy.parameters.json

<span data-ttu-id="1a266-111">Эта команда выполняет развертывание шаблона в группу ресурсов **cliRG** в расположение по умолчанию для проверки Концепции стек Azure.</span><span class="sxs-lookup"><span data-stu-id="1a266-111">This command deploys the template to the resource group **cliRG** in the Azure Stack POC’s default location.</span></span>

## <a name="validate-template-deployment"></a><span data-ttu-id="1a266-112">Проверка шаблона-развертывания</span><span class="sxs-lookup"><span data-stu-id="1a266-112">Validate template deployment</span></span>
<span data-ttu-id="1a266-113">Чтобы просмотреть эту группу ресурсов и учетную запись хранения, используйте следующие команды.</span><span class="sxs-lookup"><span data-stu-id="1a266-113">To see this resource group and storage account, use the following commands:</span></span>

    azure group list

    azure storage account list

## <a name="next-steps"></a><span data-ttu-id="1a266-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1a266-114">Next steps</span></span>
[<span data-ttu-id="1a266-115">Управление разрешениями пользователей</span><span class="sxs-lookup"><span data-stu-id="1a266-115">Manage user permissions</span></span>](azure-stack-manage-permissions.md)

