---
title: "aaaDeploy QuickBooks в Azure RemoteApp | Документы Microsoft"
description: "Узнайте, как tooshare QuickBooks с Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a><span data-ttu-id="cc083-103">Развертывание QuickBooks в Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="cc083-103">How do you deploy QuickBooks in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cc083-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="cc083-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="cc083-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="cc083-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="cc083-106">Используйте следующие сведения tooshare QuickBooks как приложение в Azure RemoteApp hello.</span><span class="sxs-lookup"><span data-stu-id="cc083-106">Use hello following information tooshare QuickBooks as an app in Azure RemoteApp.</span></span>

<span data-ttu-id="cc083-107">Предоставить совместный доступ к QuickBooks 2015 Enterprise в Azure RemoteApp можно либо в гибридной, либо в облачной коллекции.</span><span class="sxs-lookup"><span data-stu-id="cc083-107">You can share QuickBooks 2015 Enterprise with Azure RemoteApp in either a hybrid or cloud collection.</span></span> <span data-ttu-id="cc083-108">Hello компании файл должен находиться на виртуальной Машине, на котором работает сервер базы данных QuickBooks отдельно от серверов hello Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cc083-108">hello company file must reside on a VM that is running QuickBooks database server that is separate from hello Azure RemoteApp servers.</span></span> <span data-ttu-id="cc083-109">Никогда не храните файл hello компании на образ Azure RemoteApp - потери данных происходит в том случае, если это сделать.</span><span class="sxs-lookup"><span data-stu-id="cc083-109">Never store hello company file on your Azure RemoteApp image - data loss is expected if you do this.</span></span> <span data-ttu-id="cc083-110">Только QuickBooks Enterprise поддерживает размещения файла QuickBooks hello на внешнего общего ресурса с сервером базы данных QuickBooks через стандартные сети Windows.</span><span class="sxs-lookup"><span data-stu-id="cc083-110">Only QuickBooks Enterprise supports hosting hello QuickBooks file on an external share with QuickBooks database server accessible via standard Windows networking.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="cc083-111">Hello QuickBooks сервера базы данных, на котором размещается файл hello компании должны размещаться на отдельных виртуальных Машин в пределах hello же виртуальной сети как hello коллекции Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cc083-111">hello QuickBooks database server that is hosting hello company file must reside on a separate VM within hello same VNET as hello Azure RemoteApp collection.</span></span>  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a><span data-ttu-id="cc083-112">Действия toodeploy QuickBooks</span><span class="sxs-lookup"><span data-stu-id="cc083-112">Steps toodeploy QuickBooks</span></span>
1. <span data-ttu-id="cc083-113">Создание виртуальной Машины Azure и установите QuickBooks QuickBooks сервера базы данных и поместите файл hello компании на виртуальной Машине Azure.</span><span class="sxs-lookup"><span data-stu-id="cc083-113">Create an Azure VM and install QuickBooks, QuickBooks database server, and place hello company file on a Azure VM.</span></span>  <span data-ttu-id="cc083-114">Убедитесь, что tooproperly Настройка правил брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="cc083-114">Make sure tooproperly configure firewall rules.</span></span>
2. <span data-ttu-id="cc083-115">Установите на QuickBooks [пользовательского образа](remoteapp-imageoptions.md) и создать [коллекции Azure RemoteApp](remoteapp-collections.md), облачной или гибридной, в пределах hello точного одной виртуальной сети, где размещение виртуальной Машины hello hello QuickBooks сервер базы данных с находится корпоративных файлов.</span><span class="sxs-lookup"><span data-stu-id="cc083-115">Install QuickBooks on a [custom image](remoteapp-imageoptions.md) and create an [Azure RemoteApp collection](remoteapp-collections.md), either cloud or hybrid, within hello exact same VNET where hello VM hosting hello QuickBooks database server with company files resides.</span></span> 
3. <span data-ttu-id="cc083-116">[Публикация](remoteapp-publish.md) toousers QuickBooks приложения</span><span class="sxs-lookup"><span data-stu-id="cc083-116">[Publish](remoteapp-publish.md) QuickBooks app toousers</span></span>
4. <span data-ttu-id="cc083-117">Запустить клиент hello QuickBooks, размещенных в Azure RemoteApp, перейдите с помощью стандартных сетевых toohello ВМ размещения hello QuickBooks сервера базы данных Windows и откройте файл компании hello.</span><span class="sxs-lookup"><span data-stu-id="cc083-117">Launch hello Azure RemoteApp-hosted QuickBooks client, navigate using standard Windows networking toohello VM hosting hello QuickBooks database server and open hello company file.</span></span> 

## <a name="documentation-references"></a><span data-ttu-id="cc083-118">Ссылки на документацию</span><span class="sxs-lookup"><span data-stu-id="cc083-118">Documentation references</span></span>
* <span data-ttu-id="cc083-119">[Поддерживаемые конфигурации](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span><span class="sxs-lookup"><span data-stu-id="cc083-119">QuickBooks [supported configurations](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span></span>
* <span data-ttu-id="cc083-120">[Варианты развертывания](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span><span class="sxs-lookup"><span data-stu-id="cc083-120">QuickBooks [deployment options](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span></span>

<span data-ttu-id="cc083-121">Также можно проверить презентации Ignite [основы из Microsoft Azure RemoteApp управления и администрирования](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -too1:02:45 tooget toohello QuickBooks часть Перемотка вперед.</span><span class="sxs-lookup"><span data-stu-id="cc083-121">You can also check out my Ignite presentation, [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - fast-forward too1:02:45 tooget toohello QuickBooks part.</span></span>

## <a name="deployment-architecture"></a><span data-ttu-id="cc083-122">Архитектура развертывания</span><span class="sxs-lookup"><span data-stu-id="cc083-122">Deployment architecture</span></span>
![Развертывание QuickBooks + Azure RemoteApp](./media/remoteapp-quickbooks/ra-quickbooks.png)

