---
title: "Как использовать io.js с веб-приложениями службы приложений Azure"
description: "Узнайте, как использовать веб-приложения службы приложений Azure с io.js."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 4800504e1939a46842d15e8c9d4279a4b9cae787
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="50592-103">Как использовать io.js с веб-приложениями службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="50592-103">How to use io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="50592-104">Популярный узел ветвления [io.js] предлагает различные возможности для проекта Node.js компании Joyent, в том числе более открытую модель управления, сокращение цикла выпуска, а также ускорение принятия новых и экспериментальных функций JavaScript.</span><span class="sxs-lookup"><span data-stu-id="50592-104">The popular Node fork [io.js] features various differences to Joyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="50592-105">Несмотря на то, что для веб-приложений [службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) имеется достаточно много предустановленных версий Node.js, существует возможность использовать двоичный файл Node.js, предоставляемый пользователями.</span><span class="sxs-lookup"><span data-stu-id="50592-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="50592-106">В этой статье рассматриваются два метода, позволяющие использовать платформу io.js в веб-приложениях службы приложений: применение сценария расширенного развертывания, при реализации которого происходит автоматическая настройка Azure для использования новейшей доступной версии платформы io.js, а также отправка двоичного файла io.js в ручном режиме.</span><span class="sxs-lookup"><span data-stu-id="50592-106">This article discusses two methods enabling the use of io.js on App Service Web Apps: The use of an extended deployment script, which automatically configures Azure to use the latest available io.js version, as well as the manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="50592-107">Использование скрипта развертывания.</span><span class="sxs-lookup"><span data-stu-id="50592-107">Using a Deployment Script</span></span>
<span data-ttu-id="50592-108">При развертывании приложения Node.js веб-приложения службы приложений выполняют ряд небольших команд, гарантирующих правильную настройку среды.</span><span class="sxs-lookup"><span data-stu-id="50592-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands to ensure that the environment is configured properly.</span></span> <span data-ttu-id="50592-109">Скрипт развертывания дает возможность настроить этот процесс таким образом, чтобы включить в него загрузку и конфигурацию платформы io.js.</span><span class="sxs-lookup"><span data-stu-id="50592-109">Using a deployment script, this process can be customized to include the download and configuration of io.js.</span></span>

<span data-ttu-id="50592-110">[Сценарий развертывания платформы io.js](https://github.com/felixrieseberg/iojs-azure) доступен в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="50592-110">The [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="50592-111">Чтобы обеспечить поддержку io.js на веб-сайте, достаточно просто скопировать файлы **.deployment**, **deploy.cmd** и **IISNode.yml** в корневую папку приложения и развернуть их в веб-приложениях.</span><span class="sxs-lookup"><span data-stu-id="50592-111">To enable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** to the root of your application folder and deploy to Web Apps.</span></span>  

<span data-ttu-id="50592-112">Первый файл, **.deployment**, указывает веб-приложениям на необходимость выполнить **deploy.cmd** при развертывании.</span><span class="sxs-lookup"><span data-stu-id="50592-112">The first file, **.deployment**, instructs Web Apps to run **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="50592-113">Этот скрипт выполняет все обычные операции для приложения Node.js, но также загружает последнюю версию платформы io.js.</span><span class="sxs-lookup"><span data-stu-id="50592-113">This script runs all the usual steps for a Node.js application, but also downloads the latest version of io.js.</span></span> <span data-ttu-id="50592-114">И наконец, **IISNode.yml** обеспечивает настройку веб-приложений для использования только что скачанного двоичного файла io.js вместо предустановленного двоичного файла Node.js.</span><span class="sxs-lookup"><span data-stu-id="50592-114">Finally, **IISNode.yml** configures Web Apps to use just the downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="50592-115">Чтобы обновить используемый двоичный файл io.js, необходимо просто выполнять повторное развертывание приложения. Скрипт будет загружать новую версию платформы io.js при каждом развертывании приложения.</span><span class="sxs-lookup"><span data-stu-id="50592-115">To update the used io.js binary, just redeploy your application - the script will download a new version of io.js every single time the application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="50592-116">Использование ручной установки</span><span class="sxs-lookup"><span data-stu-id="50592-116">Using Manual Installation</span></span>
<span data-ttu-id="50592-117">Установка настраиваемой версии платформы io.js в ручном режиме состоит всего их двух шагов.</span><span class="sxs-lookup"><span data-stu-id="50592-117">The manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="50592-118">Сначала необходимо скачать двоичный файл **win-x64** непосредственно из [дистрибутива io.js].</span><span class="sxs-lookup"><span data-stu-id="50592-118">First, download the **win-x64** binary directly from the [io.js distribution].</span></span> <span data-ttu-id="50592-119">Требуются два файла, **iojs.exe** и **iojs.lib**.</span><span class="sxs-lookup"><span data-stu-id="50592-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="50592-120">Сохраните оба файла в папке в своем веб-приложении, например, в папке **bin/iojs**.</span><span class="sxs-lookup"><span data-stu-id="50592-120">Save both files to a folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="50592-121">Для настройки веб-приложений таким образом, чтобы они использовали **iojs.exe** вместо предварительно установленной версии Node, создайте файл **IISNode.yml** в корневом каталоге приложения и добавьте следующую строку.</span><span class="sxs-lookup"><span data-stu-id="50592-121">To configure Web Apps to use **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at the root of your application and add the following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="50592-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="50592-122">Next Steps</span></span>
<span data-ttu-id="50592-123">В этой статье вы узнали, как использовать платформу io.js с веб-приложениями службы приложений с помощью как предоставленных сценариев развертывания, так и установки в ручном режиме.</span><span class="sxs-lookup"><span data-stu-id="50592-123">In this article you learned how to use io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="50592-124">Платформа io.js продолжает усиленно разрабатываться и обновляется чаще чем Node.js.</span><span class="sxs-lookup"><span data-stu-id="50592-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="50592-125">Ряд модулей Node.js может не работать с платформой io.js. Для устранения неполадок обратитесь к материалам по платформе [io.js на сайте GitHub].</span><span class="sxs-lookup"><span data-stu-id="50592-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="50592-126">Изменения</span><span class="sxs-lookup"><span data-stu-id="50592-126">What's changed</span></span>
* <span data-ttu-id="50592-127">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="50592-127">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="50592-128">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="50592-128">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="50592-129">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="50592-129">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="50592-130">[io.js]: https://iojs.org</span><span class="sxs-lookup"><span data-stu-id="50592-130">[io.js]: https://iojs.org</span></span>
<span data-ttu-id="50592-131">[дистрибутива io.js]: https://iojs.org/dist/</span><span class="sxs-lookup"><span data-stu-id="50592-131">[io.js distribution]: https://iojs.org/dist/</span></span>
<span data-ttu-id="50592-132">[io.js на сайте GitHub]: https://github.com/iojs/io.js</span><span class="sxs-lookup"><span data-stu-id="50592-132">[io.js on GitHub]: https://github.com/iojs/io.js</span></span>
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
