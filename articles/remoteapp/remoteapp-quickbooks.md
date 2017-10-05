---
title: "Развертывание QuickBooks в Azure RemoteApp | Документация Майкрософт"
description: "Узнайте, как предоставить совместный доступ к QuickBooks с помощью Azure RemoteApp."
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
ms.openlocfilehash: bbfac45220f6ef36c9951daae0ced1974e8ddabb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a><span data-ttu-id="d7f47-103">Развертывание QuickBooks в Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="d7f47-103">How do you deploy QuickBooks in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d7f47-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="d7f47-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d7f47-105">Дополнительные сведения см. в [объявлении](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="d7f47-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="d7f47-106">В этой статье рассказывается, как предоставить совместный доступ к QuickBooks как к приложению в Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d7f47-106">Use the following information to share QuickBooks as an app in Azure RemoteApp.</span></span>

<span data-ttu-id="d7f47-107">Предоставить совместный доступ к QuickBooks 2015 Enterprise в Azure RemoteApp можно либо в гибридной, либо в облачной коллекции.</span><span class="sxs-lookup"><span data-stu-id="d7f47-107">You can share QuickBooks 2015 Enterprise with Azure RemoteApp in either a hybrid or cloud collection.</span></span> <span data-ttu-id="d7f47-108">Файл компании должен находиться на виртуальной машине, где располагается сервер базы данных QuickBooks, отдельный от серверов Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d7f47-108">The company file must reside on a VM that is running QuickBooks database server that is separate from the Azure RemoteApp servers.</span></span> <span data-ttu-id="d7f47-109">Нельзя хранить файл компании в образе Azure RemoteApp, иначе данные могут быть утеряны.</span><span class="sxs-lookup"><span data-stu-id="d7f47-109">Never store the company file on your Azure RemoteApp image - data loss is expected if you do this.</span></span> <span data-ttu-id="d7f47-110">Размещать файл QuickBooks на внешнем сервере базы данных QuickBooks, доступ к которому осуществляется через стандартную сеть Windows, позволяет только QuickBooks Enterprise.</span><span class="sxs-lookup"><span data-stu-id="d7f47-110">Only QuickBooks Enterprise supports hosting the QuickBooks file on an external share with QuickBooks database server accessible via standard Windows networking.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="d7f47-111">Сервер базы данных QuickBooks, на котором хранится файл компании, должен находиться на отдельной виртуальной машине в той же виртуальной сети, что и коллекция Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d7f47-111">The QuickBooks database server that is hosting the company file must reside on a separate VM within the same VNET as the Azure RemoteApp collection.</span></span>  
> 
> 

## <a name="steps-to-deploy-quickbooks"></a><span data-ttu-id="d7f47-112">Процедура развертывания QuickBooks</span><span class="sxs-lookup"><span data-stu-id="d7f47-112">Steps to deploy QuickBooks</span></span>
1. <span data-ttu-id="d7f47-113">Создайте виртуальную машину Azure, установите на нее QuickBooks и сервер базы данных QuickBooks и перенесите на эту виртуальную машину файл компании.</span><span class="sxs-lookup"><span data-stu-id="d7f47-113">Create an Azure VM and install QuickBooks, QuickBooks database server, and place the company file on a Azure VM.</span></span>  <span data-ttu-id="d7f47-114">Проверьте настройки правил брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="d7f47-114">Make sure to properly configure firewall rules.</span></span>
2. <span data-ttu-id="d7f47-115">Установите QuickBooks на [пользовательский образ](remoteapp-imageoptions.md) и создайте облачную или гибридную [коллекцию Azure RemoteApp](remoteapp-collections.md) в одной виртуальной сети с сервером базы данных QuickBooks, на котором находится файл компании.</span><span class="sxs-lookup"><span data-stu-id="d7f47-115">Install QuickBooks on a [custom image](remoteapp-imageoptions.md) and create an [Azure RemoteApp collection](remoteapp-collections.md), either cloud or hybrid, within the exact same VNET where the VM hosting the QuickBooks database server with company files resides.</span></span> 
3. <span data-ttu-id="d7f47-116">[Опубликуйте](remoteapp-publish.md) приложение QuickBooks для пользователей.</span><span class="sxs-lookup"><span data-stu-id="d7f47-116">[Publish](remoteapp-publish.md) QuickBooks app to users</span></span>
4. <span data-ttu-id="d7f47-117">Запустите клиент QuickBooks из коллекции Azure RemoteApp, через стандартную сеть Windows перейдите к виртуальной машине с сервером базы данных QuickBooks и откройте файл компании.</span><span class="sxs-lookup"><span data-stu-id="d7f47-117">Launch the Azure RemoteApp-hosted QuickBooks client, navigate using standard Windows networking to the VM hosting the QuickBooks database server and open the company file.</span></span> 

## <a name="documentation-references"></a><span data-ttu-id="d7f47-118">Ссылки на документацию</span><span class="sxs-lookup"><span data-stu-id="d7f47-118">Documentation references</span></span>
* <span data-ttu-id="d7f47-119">[Поддерживаемые конфигурации](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span><span class="sxs-lookup"><span data-stu-id="d7f47-119">QuickBooks [supported configurations](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span></span>
* <span data-ttu-id="d7f47-120">[Варианты развертывания](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span><span class="sxs-lookup"><span data-stu-id="d7f47-120">QuickBooks [deployment options](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span></span>

<span data-ttu-id="d7f47-121">Ознакомьтесь также с моей презентацией по Ignite, [Основы управления и администрирования Microsoft Azure RemoteApp](https://channel9.msdn.com/Events/Ignite/2015/BRK3868). Перемотайте на 1:02:45, чтобы перейти сразу к той части, где говорится о QuickBooks.</span><span class="sxs-lookup"><span data-stu-id="d7f47-121">You can also check out my Ignite presentation, [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - fast-forward to 1:02:45 to get to the QuickBooks part.</span></span>

## <a name="deployment-architecture"></a><span data-ttu-id="d7f47-122">Архитектура развертывания</span><span class="sxs-lookup"><span data-stu-id="d7f47-122">Deployment architecture</span></span>
![Развертывание QuickBooks + Azure RemoteApp](./media/remoteapp-quickbooks/ra-quickbooks.png)

