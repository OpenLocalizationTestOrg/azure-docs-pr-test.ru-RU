---
title: "aaaMigrate данные пользователя из Azure RemoteApp | Документы Microsoft"
description: "Узнайте, как toomigrate данные пользователей и из него Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a><span data-ttu-id="9484e-103">Как toomigrate данных в действие и из Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="9484e-103">How toomigrate data into and out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9484e-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="9484e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="9484e-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="9484e-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="9484e-106">Можно использовать множество различных средств и методов tootransfer [данные пользователя](remoteapp-upd.md) в действие и из Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="9484e-106">You can use many different tools and methods tootransfer [user data](remoteapp-upd.md) into and out of Azure RemoteApp.</span></span> <span data-ttu-id="9484e-107">Ниже приведено несколько таких способов.</span><span class="sxs-lookup"><span data-stu-id="9484e-107">Here are a few methods:</span></span>

* <span data-ttu-id="9484e-108">Копирование и вставка с помощью совместно используемого буфера обмена.</span><span class="sxs-lookup"><span data-stu-id="9484e-108">Copy and paste using clipboard sharing</span></span>
* <span data-ttu-id="9484e-109">Скопируйте файлы и данные tooa файлового сервера</span><span class="sxs-lookup"><span data-stu-id="9484e-109">Copy files and data tooa file server</span></span>
* <span data-ttu-id="9484e-110">Скопируйте файлы tooOneDrive для бизнеса с помощью браузера</span><span class="sxs-lookup"><span data-stu-id="9484e-110">Copy files tooOneDrive for Business through a browser</span></span>
* <span data-ttu-id="9484e-111">Копирование файлов с помощью перенаправления.</span><span class="sxs-lookup"><span data-stu-id="9484e-111">Copy files using redirection</span></span>

> [!NOTE]
> <span data-ttu-id="9484e-112">Не удается включить hello OneDrive для бизнеса или потребителя агенты синхронизации — они [не поддерживаются](remoteapp-onedrive.md) в Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="9484e-112">You cannot enable hello OneDrive for Business or Consumer sync agents - they [are not supported](remoteapp-onedrive.md) in Azure RemoteApp.</span></span>
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a><span data-ttu-id="9484e-113">Копирование и вставка в проводнике</span><span class="sxs-lookup"><span data-stu-id="9484e-113">Use copy and paste in File Explorer</span></span>
<span data-ttu-id="9484e-114">Копирование и вставка с помощью буфера обмена hello включен в развертываниях RemoteApp [по умолчанию](remoteapp-redirection.md).</span><span class="sxs-lookup"><span data-stu-id="9484e-114">Copy and paste using hello clipboard is enabled in RemoteApp deployments [by default](remoteapp-redirection.md).</span></span> <span data-ttu-id="9484e-115">Это позволяет пользователям копировать файлы между локальным компьютером и приложениями RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="9484e-115">This lets users copy files between their local PC and RemoteApp apps.</span></span> <span data-ttu-id="9484e-116">Часто через hello обычной использования приложений в удаленных приложений RemoteApp, пользователи сохранили файлы UPDs tootheir - перемещения удобно, данные из удаленных приложений RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="9484e-116">Often, through hello normal course of using apps in RemoteApp, users have saved files tootheir UPDs - moving that data out of RemoteApp is easy:</span></span>

1. <span data-ttu-id="9484e-117">[Опубликуйте проводник как приложение](remoteapp-publish.md) в коллекции RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="9484e-117">[Publish File Explorer as an app](remoteapp-publish.md) in a RemoteApp collection.</span></span> <span data-ttu-id="9484e-118">(Обратите внимание, что это задача администрирования.)</span><span class="sxs-lookup"><span data-stu-id="9484e-118">(Note that this is an administrative task.)</span></span>
2. <span data-ttu-id="9484e-119">Прямой ваши пользователи toolaunch hello проводнике опубликованному вами приложению и toouse, toocopy и вставить файлы как в их UPD, так и вне его.</span><span class="sxs-lookup"><span data-stu-id="9484e-119">Direct your users toolaunch hello File Explorer app you published and toouse that toocopy and paste files both into their UPD and out of it.</span></span>

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a><span data-ttu-id="9484e-120">Отправка файлов и данных tooa файлового сервера с помощью стандартного сетевого копирования файлов</span><span class="sxs-lookup"><span data-stu-id="9484e-120">Upload files and data tooa file server by using standard network file copy</span></span>
<span data-ttu-id="9484e-121">Часто организации использовать файловые серверы toostore общие данные.</span><span class="sxs-lookup"><span data-stu-id="9484e-121">Often organizations use file servers toostore general data.</span></span> <span data-ttu-id="9484e-122">Если известно имя сервера hello или расположение, пользователям можно просмотреть hello локальной сети для сервера hello и скопировать их файлы, подобно выполняются гораздо выше.</span><span class="sxs-lookup"><span data-stu-id="9484e-122">If you know hello server name or location, your users can browse hello local network for hello server and then copy their files there, much like they did above.</span></span> <span data-ttu-id="9484e-123">Снова вы хотите tooRemoteApp toopublish проводника и затем использовать его совместно с пользователями.</span><span class="sxs-lookup"><span data-stu-id="9484e-123">Again you'll want toopublish File Explorer tooRemoteApp and then share it with your users.</span></span>

> [!NOTE]
> <span data-ttu-id="9484e-124">Hello файловый сервер должен находиться в сети маршрутизируемый hello, развернутого в RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="9484e-124">hello file server must be on hello routable network that RemoteApp was deployed into.</span></span>
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a><span data-ttu-id="9484e-125">Скопируйте файлы tooOneDrive для бизнеса</span><span class="sxs-lookup"><span data-stu-id="9484e-125">Copy files tooOneDrive for Business</span></span>
<span data-ttu-id="9484e-126">Несмотря на то, что не удается включить hello OneDrive для бизнеса агент синхронизации в удаленных приложений RemoteApp, то можно скопировать файлы из вашей tooOneDrive UPD для бизнеса через браузер.</span><span class="sxs-lookup"><span data-stu-id="9484e-126">Although you cannot enable hello OneDrive for Business sync agent in RemoteApp, you can still copy files from your UPD tooOneDrive for Business through a browser.</span></span> 

1. <span data-ttu-id="9484e-127">Опубликовать файл в проводнике tooRemoteApp и послать tooaccess пользователей hello файлов с помощью этого приложения.</span><span class="sxs-lookup"><span data-stu-id="9484e-127">Publish File Explorer tooRemoteApp and then tell users tooaccess hello files through that app.</span></span> 
2. <span data-ttu-id="9484e-128">Является простым tootransfer файлы сжимаются, поэтому пользователи должны создавать ZIP-файл, содержащий все tooOneDrive toomove файлы hello для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="9484e-128">It's easiest tootransfer files if they are compressed, so users should create a .zip file that contains all of hello files toomove tooOneDrive for Business.</span></span>
3. <span data-ttu-id="9484e-129">Попросите пользователей toogo toohello Office 365 portal и затем перейдите tooOneDrive и отправить hello ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="9484e-129">Ask users toogo toohello Office 365 portal, and then go tooOneDrive and upload hello .zip file.</span></span>

## <a name="copy-files-by-using-drive-redirection"></a><span data-ttu-id="9484e-130">Копирование файлов с помощью перенаправления дисков</span><span class="sxs-lookup"><span data-stu-id="9484e-130">Copy files by using drive redirection</span></span>
<span data-ttu-id="9484e-131">Если вы включили [перенаправление дисков](remoteapp-redirection.md), то вы уже создали подключенный диск для пользователей.</span><span class="sxs-lookup"><span data-stu-id="9484e-131">If you have enabled [drive redirection](remoteapp-redirection.md), you have already created a mapped drive for your users.</span></span> <span data-ttu-id="9484e-132">В этом случае ZIP-файлы на диск перенаправлено hello и сохранить их tootheir локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="9484e-132">In this case, they can zip their files on hello redirected drive and then save them tootheir local PC.</span></span>

## <a name="how-administrators-can-export-data"></a><span data-ttu-id="9484e-133">Экспорт данных администраторами</span><span class="sxs-lookup"><span data-stu-id="9484e-133">How administrators can export data</span></span>

<span data-ttu-id="9484e-134">Администрирование для Azure RemoteApp можно экспортировать все диски профилей пользователей (UPD) для всех коллекций в рамках подписки tooAzure хранилища с помощью Azure PowerShell командлет Export-AzureRemoteAppUserDisk.</span><span class="sxs-lookup"><span data-stu-id="9484e-134">Administers for Azure RemoteApp can export all user profile disks (UPD) for all collections within a subscription tooAzure Storage using Azure PowerShell cmdlet, Export-AzureRemoteAppUserDisk.</span></span>  <span data-ttu-id="9484e-135">Нет возможности tooselect отдельных UPD элемента не существует.</span><span class="sxs-lookup"><span data-stu-id="9484e-135">There is no ability tooselect individual UPD's.</span></span>  <span data-ttu-id="9484e-136">При выполнении команды PowerShell hello каждого диска пользователя будет фиксированный диск размером 50 ГБ и быть экспортированного tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="9484e-136">When hello PowerShell command is executed, each user disk will be a 50gb in fixed disk size and be exported tooAzure storage.</span></span>  <span data-ttu-id="9484e-137">Оплата использования хранилища Azure будет выполнена немедленно для этого хранилища.</span><span class="sxs-lookup"><span data-stu-id="9484e-137">Costs of Azure storage will incur immediately for this storage.</span></span>  <span data-ttu-id="9484e-138">При выполнении этой команды убедитесь отсутствуют сеансы, в противном случае экспорта hello, будут завершаться сбоем.</span><span class="sxs-lookup"><span data-stu-id="9484e-138">When running this command ensure there are no sessions otherwise hello export will fail.</span></span>

<span data-ttu-id="9484e-139">UPD для развертываний удаленного приложения Azure RemoteApp, присоединенных к домену, можно использовать повторно только в развертывании служб удаленных рабочих столов, тогда как для развертываний, не присоединенных к домену, такая возможность отсутствует.</span><span class="sxs-lookup"><span data-stu-id="9484e-139">UPD's for domain joined Azure RemoteApp deployments can only be used again in an RDS deployment, non-domain joined deployments cannot be used.</span></span>  <span data-ttu-id="9484e-140">Если эти диски, которые будут использоваться в развертывании служб удаленных рабочих СТОЛОВ рекомендуется toouse наших [автоматических скриптов](https://github.com/arcadiahlyy/aramigration) , будет экспортировать, преобразование и импорт hello UPD элемента в развертывании служб удаленных рабочих СТОЛОВ.</span><span class="sxs-lookup"><span data-stu-id="9484e-140">If these disks will be used in an RDS deployment we recommend toouse our [automated scripts](https://github.com/arcadiahlyy/aramigration) that will export, convert, and import hello UPD's into an RDS deployment.</span></span>

