---
title: "io.js toouse aaaHow с веб-приложениях службы приложений Azure"
description: "Узнайте, как веб-приложения в службе приложений Azure с io.js toouse."
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
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="6446a-103">Как io.js toouse с веб-приложениях службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="6446a-103">How toouse io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="6446a-104">Популярные узел ветвления Hello [io.js] функции проекта Node.js различные tooJoyent различия, включая более откройте модель управления, быстрее цикл выпуска и быстрее внедрения новых и экспериментальный функций JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6446a-104">hello popular Node fork [io.js] features various differences tooJoyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="6446a-105">Несмотря на то, что для веб-приложений [службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) имеется достаточно много предустановленных версий Node.js, существует возможность использовать двоичный файл Node.js, предоставляемый пользователями.</span><span class="sxs-lookup"><span data-stu-id="6446a-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="6446a-106">В этой статье описываются два способа, применение hello io.js в веб-приложениях службы приложений: hello использования расширенного развертывания сценария, который автоматически настраивает последнюю версию доступных io.js Azure toouse hello, а также отправки вручную hello io.js двоичного файла.</span><span class="sxs-lookup"><span data-stu-id="6446a-106">This article discusses two methods enabling hello use of io.js on App Service Web Apps: hello use of an extended deployment script, which automatically configures Azure toouse hello latest available io.js version, as well as hello manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="6446a-107">Использование скрипта развертывания.</span><span class="sxs-lookup"><span data-stu-id="6446a-107">Using a Deployment Script</span></span>
<span data-ttu-id="6446a-108">При развертывании приложения Node.js приложение службы веб-приложения выполняется ряд небольших команды tooensure, hello среде правильно настроена.</span><span class="sxs-lookup"><span data-stu-id="6446a-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands tooensure that hello environment is configured properly.</span></span> <span data-ttu-id="6446a-109">С помощью скрипта развертывания, этот процесс может быть настроенный tooinclude hello загрузки и конфигурации io.js.</span><span class="sxs-lookup"><span data-stu-id="6446a-109">Using a deployment script, this process can be customized tooinclude hello download and configuration of io.js.</span></span>

<span data-ttu-id="6446a-110">Hello [io.js скрипт развертывания](https://github.com/felixrieseberg/iojs-azure) можно найти в GitHub.</span><span class="sxs-lookup"><span data-stu-id="6446a-110">hello [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="6446a-111">io.js tooenable на веб-приложения, просто скопируйте **.deployment**, **deploy.cmd** и **IISNode.yml** toohello корневой папке приложения и развертывать приложения tooWeb.</span><span class="sxs-lookup"><span data-stu-id="6446a-111">tooenable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** toohello root of your application folder and deploy tooWeb Apps.</span></span>  

<span data-ttu-id="6446a-112">Первый файл Hello, **.deployment**, указывает, что веб-приложений toorun **deploy.cmd** после развертывания.</span><span class="sxs-lookup"><span data-stu-id="6446a-112">hello first file, **.deployment**, instructs Web Apps toorun **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="6446a-113">Этот скрипт выполняется все обычные действия приветствия для Node.js приложения, но также загружает последнюю версию io.js hello.</span><span class="sxs-lookup"><span data-stu-id="6446a-113">This script runs all hello usual steps for a Node.js application, but also downloads hello latest version of io.js.</span></span> <span data-ttu-id="6446a-114">Наконец **IISNode.yml** настраивает веб-приложений toouse просто hello загружены io.js двоичных вместо предустановленных двоичный файл Node.js.</span><span class="sxs-lookup"><span data-stu-id="6446a-114">Finally, **IISNode.yml** configures Web Apps toouse just hello downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="6446a-115">tooupdate hello используется двоичный файл io.js, просто повторите развертывание приложения — hello скрипт загрузит новую версию io.js развертывания каждое приложение hello один раз.</span><span class="sxs-lookup"><span data-stu-id="6446a-115">tooupdate hello used io.js binary, just redeploy your application - hello script will download a new version of io.js every single time hello application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="6446a-116">Использование ручной установки</span><span class="sxs-lookup"><span data-stu-id="6446a-116">Using Manual Installation</span></span>
<span data-ttu-id="6446a-117">Ручная установка версии пользовательских io.js Hello включает только два этапа.</span><span class="sxs-lookup"><span data-stu-id="6446a-117">hello manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="6446a-118">Сначала загрузите hello **win x64** двоичных непосредственно из hello [io.js распространения].</span><span class="sxs-lookup"><span data-stu-id="6446a-118">First, download hello **win-x64** binary directly from hello [io.js distribution].</span></span> <span data-ttu-id="6446a-119">Требуются два файла, **iojs.exe** и **iojs.lib**.</span><span class="sxs-lookup"><span data-stu-id="6446a-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="6446a-120">Сохранить обе папки с файлами tooa внутри веб-приложения, например в **bin/iojs**.</span><span class="sxs-lookup"><span data-stu-id="6446a-120">Save both files tooa folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="6446a-121">toouse веб-приложений tooconfigure **iojs.exe** вместо предварительно установленную версию узла, создайте **IISNode.yml** в корневом каталоге приложения hello и добавьте следующей строкой hello.</span><span class="sxs-lookup"><span data-stu-id="6446a-121">tooconfigure Web Apps toouse **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at hello root of your application and add hello following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="6446a-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6446a-122">Next Steps</span></span>
<span data-ttu-id="6446a-123">В этой статье вы узнали, как указано io.js toouse для приложения службы веб-приложений, с помощью скриптов развертывания, а также установка вручную.</span><span class="sxs-lookup"><span data-stu-id="6446a-123">In this article you learned how toouse io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="6446a-124">Платформа io.js продолжает усиленно разрабатываться и обновляется чаще чем Node.js.</span><span class="sxs-lookup"><span data-stu-id="6446a-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="6446a-125">Ряд модулей Node.js может не работать с платформой io.js. Для устранения неполадок обратитесь к материалам по платформе [io.js на сайте GitHub].</span><span class="sxs-lookup"><span data-stu-id="6446a-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="6446a-126">Изменения</span><span class="sxs-lookup"><span data-stu-id="6446a-126">What's changed</span></span>
* <span data-ttu-id="6446a-127">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="6446a-127">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="6446a-128">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="6446a-128">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="6446a-129">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="6446a-129">No credit cards required; no commitments.</span></span>
> 
> 

[io.js]: https://iojs.org
[io.js распространения]: https://iojs.org/dist/
[io.js на сайте GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
