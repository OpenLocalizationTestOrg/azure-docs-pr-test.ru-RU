---
title: "шаблоны aaaDeploy с hello командной строки в стеке Azure | Документы Microsoft"
description: "Узнайте, как toouse hello tooAzure шаблоны toodeploy кросс платформенных командной строки (CLI) стека."
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
ms.openlocfilehash: 6fa6b19ac94d3f020008d04ff07f1ce489aa3418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-hello-command-line"></a><span data-ttu-id="a8bd2-103">Развертывание шаблонов в стек Azure, с помощью командной строки hello</span><span class="sxs-lookup"><span data-stu-id="a8bd2-103">Deploy templates in Azure Stack using hello command line</span></span>
<span data-ttu-id="a8bd2-104">Используйте шаблоны Azure Resource Manager toohello пакет средств разработки Azure стека hello командной строки toodeploy.</span><span class="sxs-lookup"><span data-stu-id="a8bd2-104">Use hello command line toodeploy Azure Resource Manager templates toohello Azure Stack Development Kit.</span></span> <span data-ttu-id="a8bd2-105">Шаблоны диспетчера ресурсов Azure, развертывание и предоставление всех hello ресурсы для приложения в один, согласованной операции.</span><span class="sxs-lookup"><span data-stu-id="a8bd2-105">Azure Resource Manager templates deploy and provision all hello resources for your application in a single, coordinated operation.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a8bd2-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a8bd2-106">Before you begin</span></span>
 - <span data-ttu-id="a8bd2-107">[Установка и подключение](azure-stack-connect-cli.md) tooAzure стека с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a8bd2-107">[Install and connect](azure-stack-connect-cli.md) tooAzure Stack with Azure CLI</span></span>
 - <span data-ttu-id="a8bd2-108">Загрузка файлов hello *azuredeploy.json* и *azuredeploy.parameters.json* из hello [Создание шаблона пример учетной записи хранилища](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="a8bd2-108">Download hello files *azuredeploy.json* and *azuredeploy.parameters.json* from hello [create storage account example template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account).</span></span>
 
## <a name="deploy-template"></a><span data-ttu-id="a8bd2-109">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="a8bd2-109">Deploy template</span></span>
<span data-ttu-id="a8bd2-110">Перейдите в папку toohello, где эти файлы были загружены и запустите следующий шаблон hello toodeploy команды hello:</span><span class="sxs-lookup"><span data-stu-id="a8bd2-110">Navigate toohello folder where these files were downloaded and run hello following command toodeploy hello template:</span></span>

    azure group create "cliRG" "local" –f azuredeploy.json –d "testDeploy" –e azuredeploy.parameters.json

<span data-ttu-id="a8bd2-111">Эта команда выполняет развертывание группы ресурсов hello шаблона toohello **cliRG** в расположении по умолчанию эта для hello Azure стека.</span><span class="sxs-lookup"><span data-stu-id="a8bd2-111">This command deploys hello template toohello resource group **cliRG** in hello Azure Stack POC’s default location.</span></span>

## <a name="validate-template-deployment"></a><span data-ttu-id="a8bd2-112">Проверка шаблона-развертывания</span><span class="sxs-lookup"><span data-stu-id="a8bd2-112">Validate template deployment</span></span>
<span data-ttu-id="a8bd2-113">toosee этот ресурс группы и учетную запись хранилища, hello используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="a8bd2-113">toosee this resource group and storage account, use hello following commands:</span></span>

    azure group list

    azure storage account list

## <a name="next-steps"></a><span data-ttu-id="a8bd2-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8bd2-114">Next steps</span></span>
[<span data-ttu-id="a8bd2-115">Управление разрешениями пользователей</span><span class="sxs-lookup"><span data-stu-id="a8bd2-115">Manage user permissions</span></span>](azure-stack-manage-permissions.md)

