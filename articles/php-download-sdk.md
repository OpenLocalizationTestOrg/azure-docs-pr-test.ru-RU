---
title: "aaaDownload hello Azure SDK для PHP"
description: "Узнайте, как toodownload и установите hello Azure SDK для PHP."
documentationcenter: php
services: app-service\web
author: allclark
manager: douge
editor: 
ms.assetid: bac355ac-4c25-42f4-8273-c5112eafa8d4
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 06/01/2016
ms.author: allclark;yaqiyang
ms.openlocfilehash: 94f56fc4f91bb175c08b9f7a43cb221c827694a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="9bafa-103">Скачать hello Azure SDK для PHP</span><span class="sxs-lookup"><span data-stu-id="9bafa-103">Download hello Azure SDK for PHP</span></span>
## <a name="overview"></a><span data-ttu-id="9bafa-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="9bafa-104">Overview</span></span>
<span data-ttu-id="9bafa-105">компоненты, позволяющие toodevelop включает Hello Azure SDK для PHP, развертывания и управления приложений PHP для Azure.</span><span class="sxs-lookup"><span data-stu-id="9bafa-105">hello Azure SDK for PHP includes components that allow you toodevelop, deploy, and manage PHP applications for Azure.</span></span> <span data-ttu-id="9bafa-106">В частности hello Azure SDK для PHP содержит hello следующее:</span><span class="sxs-lookup"><span data-stu-id="9bafa-106">Specifically, hello Azure SDK for PHP includes hello following:</span></span>

* <span data-ttu-id="9bafa-107">**Здравствуйте, клиентские библиотеки PHP для Azure**.</span><span class="sxs-lookup"><span data-stu-id="9bafa-107">**hello PHP client libraries for Azure**.</span></span> <span data-ttu-id="9bafa-108">Эти библиотеки классов предоставляют интерфейс для доступа к функциям Azure, таким как службы управления данными и облачные службы.</span><span class="sxs-lookup"><span data-stu-id="9bafa-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span></span>  
* <span data-ttu-id="9bafa-109">**Интерфейс командной строки Azure для Mac, Linux и Windows (Azure CLI) Hello**.</span><span class="sxs-lookup"><span data-stu-id="9bafa-109">**hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span></span> <span data-ttu-id="9bafa-110">Это набор команд для развертывания и управления службами Azure, например веб-сайтами Azure и виртуальными машинами Azure.</span><span class="sxs-lookup"><span data-stu-id="9bafa-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="9bafa-111">Hello Azure CLI работы на любой платформе, включая Mac, Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="9bafa-111">hello Azure CLI work on any platform, including Mac, Linux, and Windows.</span></span>
* <span data-ttu-id="9bafa-112">**Azure PowerShell (только для Windows)**.</span><span class="sxs-lookup"><span data-stu-id="9bafa-112">**Azure PowerShell (Windows Only)**.</span></span> <span data-ttu-id="9bafa-113">Это набор командлетов PowerShell для развертывания служб Azure, таких как облачные службы и виртуальные машины, и управления ими.</span><span class="sxs-lookup"><span data-stu-id="9bafa-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span></span>
* <span data-ttu-id="9bafa-114">**Привет эмуляторы Azure (только Windows)**.</span><span class="sxs-lookup"><span data-stu-id="9bafa-114">**hello Azure Emulators (Windows Only)**.</span></span> <span data-ttu-id="9bafa-115">Привет эмуляторы вычислений и хранения являются локальными эмуляторами облачных служб и служб управления данными, позволяющие tootest приложения локально.</span><span class="sxs-lookup"><span data-stu-id="9bafa-115">hello compute and storage emulators are local emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="9bafa-116">Привет эмуляторы Azure работают только в Windows.</span><span class="sxs-lookup"><span data-stu-id="9bafa-116">hello Azure Emulators run on Windows only.</span></span>

<span data-ttu-id="9bafa-117">Hello разделах описываются hello как toodownload и установите компоненты, описанные выше.</span><span class="sxs-lookup"><span data-stu-id="9bafa-117">hello sections below describe how toodownload and install hello components described above.</span></span>

<span data-ttu-id="9bafa-118">Hello инструкции в этом разделе предполагается, что вы [PHP] [ install-php] установлен.</span><span class="sxs-lookup"><span data-stu-id="9bafa-118">hello instructions in this topic assume that you have [PHP][install-php] installed.</span></span>

> [!NOTE]
> <span data-ttu-id="9bafa-119">Необходимо иметь PHP 5.5 или более поздней версии клиентских библиотек toouse hello PHP для Azure.</span><span class="sxs-lookup"><span data-stu-id="9bafa-119">You must have PHP 5.5 or higher toouse hello PHP client libraries for Azure.</span></span>
> 
> 

## <a name="php-client-libraries-for-azure"></a><span data-ttu-id="9bafa-120">Клиентские библиотеки PHP для Azure</span><span class="sxs-lookup"><span data-stu-id="9bafa-120">PHP client libraries for Azure</span></span>
<span data-ttu-id="9bafa-121">Hello PHP клиентские библиотеки для Azure предоставляют интерфейс для доступа к Azure возможностей, таких как службы управления данными и облачным службам из любой операционной системы.</span><span class="sxs-lookup"><span data-stu-id="9bafa-121">hello PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span></span> <span data-ttu-id="9bafa-122">Эти библиотеки могут устанавливаться через hello редактор.</span><span class="sxs-lookup"><span data-stu-id="9bafa-122">These libraries can be installed via hello Composer.</span></span>

<span data-ttu-id="9bafa-123">Сведения о как toouse hello клиентские библиотеки PHP для Azure см. в разделе [как tooUse hello службы BLOB-объектов][blob-service], [как tooUse hello службы таблиц] [ table-service] и [как tooUse hello службы очередей][queue-service].</span><span class="sxs-lookup"><span data-stu-id="9bafa-123">For information about how toouse hello PHP Client Libraries for Azure, see [How tooUse hello Blob Service][blob-service], [How tooUse hello Table Service][table-service] and [How tooUse hello Queue Service][queue-service].</span></span>

### <a name="install-via-composer"></a><span data-ttu-id="9bafa-124">Установка через компоновщик</span><span class="sxs-lookup"><span data-stu-id="9bafa-124">Install via Composer</span></span>
1. <span data-ttu-id="9bafa-125">[Установите Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="9bafa-125">[Install Git][install-git].</span></span>

    > [AZURE.NOTE] <span data-ttu-id="9bafa-126">В Windows необходимо также tooadd hello Git исполняемый tooyour в переменную среды PATH.</span><span class="sxs-lookup"><span data-stu-id="9bafa-126">On Windows, you will also need tooadd hello Git executable tooyour PATH environment variable.</span></span>

1. <span data-ttu-id="9bafa-127">Создайте файл с именем **composer.json** в hello корень проекта и добавьте следующий код tooit hello:</span><span class="sxs-lookup"><span data-stu-id="9bafa-127">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. <span data-ttu-id="9bafa-128">Скачайте **[composer.phar][composer-phar]** в корневой каталог проекта.</span><span class="sxs-lookup"><span data-stu-id="9bafa-128">Download **[composer.phar][composer-phar]** in your project root.</span></span>
3. <span data-ttu-id="9bafa-129">Откройте командную строку и выполните эту команду в корневом каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="9bafa-129">Open a command prompt and execute this in your project root</span></span>
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a><span data-ttu-id="9bafa-130">Azure PowerShell и эмуляторы Azure</span><span class="sxs-lookup"><span data-stu-id="9bafa-130">Azure PowerShell and Azure Emulators</span></span>
<span data-ttu-id="9bafa-131">Azure PowerShell — это набор командлетов PowerShell для развертывания служб Azure и управления ими, например облачных служб и виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="9bafa-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span></span> <span data-ttu-id="9bafa-132">Привет эмуляторы Azure — это эмуляторы облачных служб и служб управления данными, позволяющие tootest приложения локально.</span><span class="sxs-lookup"><span data-stu-id="9bafa-132">hello Azure Emulators are emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="9bafa-133">Эти компоненты поддерживаются только в Windows.</span><span class="sxs-lookup"><span data-stu-id="9bafa-133">These components are supported Windows only.</span></span>

<span data-ttu-id="9bafa-134">Здравствуйте, рекомендуемым способом tooinstall Azure PowerShell и Привет эмуляторы Azure — toouse hello [Microsoft Web Platform Installer][download-wpi].</span><span class="sxs-lookup"><span data-stu-id="9bafa-134">hello recommended way tooinstall Azure PowerShell and hello Azure Emulators is toouse hello [Microsoft Web Platform Installer][download-wpi].</span></span> <span data-ttu-id="9bafa-135">Обратите внимание, что можно также выбрать tooinstall другими компонентами разработки, такие как PHP, SQL Server, hello драйверы Майкрософт для SQL Server для PHP и WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="9bafa-135">Note that you can also choose tooinstall other development components, such as PHP, SQL Server, hello Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span></span>

<span data-ttu-id="9bafa-136">Сведения о разделе toouse Azure PowerShell, [как tooUse Azure PowerShell][powershell-tools].</span><span class="sxs-lookup"><span data-stu-id="9bafa-136">For information about how toouse Azure PowerShell, see [How tooUse Azure PowerShell][powershell-tools].</span></span>

## <a name="azure-cli"></a><span data-ttu-id="9bafa-137">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="9bafa-137">Azure CLI</span></span>
<span data-ttu-id="9bafa-138">Hello Azure CLI — это набор команд для развертывания и управления службами Azure, такие как веб-сайтов Azure и виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="9bafa-138">hello Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="9bafa-139">Сведения об установке Azure CLI см. в разделе [Install hello Azure CLI](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9bafa-139">For information about installing Azure CLI, see [Install hello Azure CLI](cli-install-nodejs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9bafa-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9bafa-140">Next steps</span></span>
<span data-ttu-id="9bafa-141">Дополнительные сведения см. в разделе hello [Центр разработчика PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="9bafa-141">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[composer-github]: https://github.com/composer/composer
[composer-phar]: http://getcomposer.org/composer.phar
[nodejs-org]: http://nodejs.org/
[install-node-linux]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[download-wpi]: http://go.microsoft.com/fwlink/?LinkId=253447
[mac-installer]: http://go.microsoft.com/fwlink/?LinkId=252249
[blob-service]: http://go.microsoft.com/fwlink/?LinkId=252714
[table-service]: http://go.microsoft.com/fwlink/?LinkId=252715
[queue-service]: http://go.microsoft.com/fwlink/?LinkId=252716
[azure cli]: http://go.microsoft.com/fwlink/?LinkId=252717
[powershell-tools]: http://go.microsoft.com/fwlink/?LinkId=252718
[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
