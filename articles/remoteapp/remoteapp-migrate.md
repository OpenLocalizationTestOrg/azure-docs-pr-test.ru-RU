---
title: "Перенос данных пользователя из Azure RemoteApp | Документация Майкрософт"
description: "Узнайте, как переносить данные пользователя в службу Azure RemoteApp и из нее."
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
ms.openlocfilehash: ba3cf4c6834279bbd7f94d666fd8abbb7ac05bf0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-migrate-data-into-and-out-of-azure-remoteapp"></a><span data-ttu-id="73ad8-103">Как перенести данные в службу Azure RemoteApp и из нее</span><span class="sxs-lookup"><span data-stu-id="73ad8-103">How to migrate data into and out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="73ad8-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="73ad8-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="73ad8-105">Дополнительные сведения см. в [объявлении](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="73ad8-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="73ad8-106">Для передачи [данных пользователя](remoteapp-upd.md) в удаленное приложение Azure RemoteApp и из него можно использовать множество различных инструментов и способов.</span><span class="sxs-lookup"><span data-stu-id="73ad8-106">You can use many different tools and methods to transfer [user data](remoteapp-upd.md) into and out of Azure RemoteApp.</span></span> <span data-ttu-id="73ad8-107">Ниже приведено несколько таких способов.</span><span class="sxs-lookup"><span data-stu-id="73ad8-107">Here are a few methods:</span></span>

* <span data-ttu-id="73ad8-108">Копирование и вставка с помощью совместно используемого буфера обмена.</span><span class="sxs-lookup"><span data-stu-id="73ad8-108">Copy and paste using clipboard sharing</span></span>
* <span data-ttu-id="73ad8-109">Копирование файлов и данных на файловый сервер.</span><span class="sxs-lookup"><span data-stu-id="73ad8-109">Copy files and data to a file server</span></span>
* <span data-ttu-id="73ad8-110">Копирование файлов на OneDrive для бизнеса через браузер.</span><span class="sxs-lookup"><span data-stu-id="73ad8-110">Copy files to OneDrive for Business through a browser</span></span>
* <span data-ttu-id="73ad8-111">Копирование файлов с помощью перенаправления.</span><span class="sxs-lookup"><span data-stu-id="73ad8-111">Copy files using redirection</span></span>

> [!NOTE]
> <span data-ttu-id="73ad8-112">Вы не сможете включить агенты синхронизации OneDrive для бизнеса или OneDrive for Consumer — они [не поддерживаются](remoteapp-onedrive.md) в удаленном приложении Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="73ad8-112">You cannot enable the OneDrive for Business or Consumer sync agents - they [are not supported](remoteapp-onedrive.md) in Azure RemoteApp.</span></span>
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a><span data-ttu-id="73ad8-113">Копирование и вставка в проводнике</span><span class="sxs-lookup"><span data-stu-id="73ad8-113">Use copy and paste in File Explorer</span></span>
<span data-ttu-id="73ad8-114">Функция копирования и вставки через буфер обмена включена в развертываниях RemoteApp [по умолчанию](remoteapp-redirection.md).</span><span class="sxs-lookup"><span data-stu-id="73ad8-114">Copy and paste using the clipboard is enabled in RemoteApp deployments [by default](remoteapp-redirection.md).</span></span> <span data-ttu-id="73ad8-115">Это позволяет пользователям копировать файлы между локальным компьютером и приложениями RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="73ad8-115">This lets users copy files between their local PC and RemoteApp apps.</span></span> <span data-ttu-id="73ad8-116">Часто при использовании приложений в RemoteApp в обычном режиме пользователи сохраняют файлы на диски UPD. Эти данные легко переместить из RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="73ad8-116">Often, through the normal course of using apps in RemoteApp, users have saved files to their UPDs - moving that data out of RemoteApp is easy:</span></span>

1. <span data-ttu-id="73ad8-117">[Опубликуйте проводник как приложение](remoteapp-publish.md) в коллекции RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="73ad8-117">[Publish File Explorer as an app](remoteapp-publish.md) in a RemoteApp collection.</span></span> <span data-ttu-id="73ad8-118">(Обратите внимание, что это задача администрирования.)</span><span class="sxs-lookup"><span data-stu-id="73ad8-118">(Note that this is an administrative task.)</span></span>
2. <span data-ttu-id="73ad8-119">Укажите, чтобы ваши пользователи запускали опубликованное приложение проводника и использовали его для копирования и вставки файлов как на свои диски UPD, так и с них.</span><span class="sxs-lookup"><span data-stu-id="73ad8-119">Direct your users to launch the File Explorer app you published and to use that to copy and paste files both into their UPD and out of it.</span></span>

## <a name="upload-files-and-data-to-a-file-server-by-using-standard-network-file-copy"></a><span data-ttu-id="73ad8-120">Передача файлов и данных на файловый сервер с помощью стандартного сетевого копирования файлов</span><span class="sxs-lookup"><span data-stu-id="73ad8-120">Upload files and data to a file server by using standard network file copy</span></span>
<span data-ttu-id="73ad8-121">Часто организации используют файловые серверы для хранения общих данных.</span><span class="sxs-lookup"><span data-stu-id="73ad8-121">Often organizations use file servers to store general data.</span></span> <span data-ttu-id="73ad8-122">Если известно имя или расположение сервера, пользователи могут просмотреть локальную сеть, чтобы найти этот сервер, и скопировать свои файлы на него практически так же, как было описано выше.</span><span class="sxs-lookup"><span data-stu-id="73ad8-122">If you know the server name or location, your users can browse the local network for the server and then copy their files there, much like they did above.</span></span> <span data-ttu-id="73ad8-123">Снова потребуется опубликовать проводник в RemoteApp и настроить его совместное использование для пользователей.</span><span class="sxs-lookup"><span data-stu-id="73ad8-123">Again you'll want to publish File Explorer to RemoteApp and then share it with your users.</span></span>

> [!NOTE]
> <span data-ttu-id="73ad8-124">Файловый сервер должен находиться в маршрутизируемой сети, в которой развернута служба RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="73ad8-124">The file server must be on the routable network that RemoteApp was deployed into.</span></span>
> 
> 

## <a name="copy-files-to-onedrive-for-business"></a><span data-ttu-id="73ad8-125">Копирование файлов в OneDrive для бизнеса</span><span class="sxs-lookup"><span data-stu-id="73ad8-125">Copy files to OneDrive for Business</span></span>
<span data-ttu-id="73ad8-126">Несмотря на то, что в RemoteApp невозможно включить агент синхронизации OneDrive для бизнеса, по-прежнему можно скопировать файлы с диска UPD в OneDrive для бизнеса через браузер.</span><span class="sxs-lookup"><span data-stu-id="73ad8-126">Although you cannot enable the OneDrive for Business sync agent in RemoteApp, you can still copy files from your UPD to OneDrive for Business through a browser.</span></span> 

1. <span data-ttu-id="73ad8-127">Опубликуйте проводник в RemoteApp и укажите пользователям использовать его для доступа к файлам.</span><span class="sxs-lookup"><span data-stu-id="73ad8-127">Publish File Explorer to RemoteApp and then tell users to access the files through that app.</span></span> 
2. <span data-ttu-id="73ad8-128">Проще передавать сжатые файлы, поэтому пользователям следует создать ZIP-файл, который содержит все файлы для перемещения в OneDrive для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="73ad8-128">It's easiest to transfer files if they are compressed, so users should create a .zip file that contains all of the files to move to OneDrive for Business.</span></span>
3. <span data-ttu-id="73ad8-129">Попросите пользователей перейти на портал Office 365, затем перейти к OneDrive и передать ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="73ad8-129">Ask users to go to the Office 365 portal, and then go to OneDrive and upload the .zip file.</span></span>

## <a name="copy-files-by-using-drive-redirection"></a><span data-ttu-id="73ad8-130">Копирование файлов с помощью перенаправления дисков</span><span class="sxs-lookup"><span data-stu-id="73ad8-130">Copy files by using drive redirection</span></span>
<span data-ttu-id="73ad8-131">Если вы включили [перенаправление дисков](remoteapp-redirection.md), то вы уже создали подключенный диск для пользователей.</span><span class="sxs-lookup"><span data-stu-id="73ad8-131">If you have enabled [drive redirection](remoteapp-redirection.md), you have already created a mapped drive for your users.</span></span> <span data-ttu-id="73ad8-132">В этом случае они могут сжать файлы в ZIP-файл на подключенном диске, а затем сохранить его на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="73ad8-132">In this case, they can zip their files on the redirected drive and then save them to their local PC.</span></span>

## <a name="how-administrators-can-export-data"></a><span data-ttu-id="73ad8-133">Экспорт данных администраторами</span><span class="sxs-lookup"><span data-stu-id="73ad8-133">How administrators can export data</span></span>

<span data-ttu-id="73ad8-134">Администраторы удаленного приложения Azure RemoteApp могут экспортировать все диски профилей пользователей (UPD) для всех коллекций в рамках подписки на службу хранилища Azure Storage с помощью командлета Azure PowerShell "Export-AzureRemoteAppUserDisk".</span><span class="sxs-lookup"><span data-stu-id="73ad8-134">Administers for Azure RemoteApp can export all user profile disks (UPD) for all collections within a subscription to Azure Storage using Azure PowerShell cmdlet, Export-AzureRemoteAppUserDisk.</span></span>  <span data-ttu-id="73ad8-135">Выбрать отдельные UPD невозможно.</span><span class="sxs-lookup"><span data-stu-id="73ad8-135">There is no ability to select individual UPD's.</span></span>  <span data-ttu-id="73ad8-136">При выполнении команды PowerShell размер каждого диска пользователя будет составлять фиксированные 50 ГБ, а сам диск будет экспортирован в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="73ad8-136">When the PowerShell command is executed, each user disk will be a 50gb in fixed disk size and be exported to Azure storage.</span></span>  <span data-ttu-id="73ad8-137">Оплата использования хранилища Azure будет выполнена немедленно для этого хранилища.</span><span class="sxs-lookup"><span data-stu-id="73ad8-137">Costs of Azure storage will incur immediately for this storage.</span></span>  <span data-ttu-id="73ad8-138">При выполнении этой команды убедитесь в том, что отсутствуют другие сеансы, в противном случае операция экспорта завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="73ad8-138">When running this command ensure there are no sessions otherwise the export will fail.</span></span>

<span data-ttu-id="73ad8-139">UPD для развертываний удаленного приложения Azure RemoteApp, присоединенных к домену, можно использовать повторно только в развертывании служб удаленных рабочих столов, тогда как для развертываний, не присоединенных к домену, такая возможность отсутствует.</span><span class="sxs-lookup"><span data-stu-id="73ad8-139">UPD's for domain joined Azure RemoteApp deployments can only be used again in an RDS deployment, non-domain joined deployments cannot be used.</span></span>  <span data-ttu-id="73ad8-140">Если эти диски будут использоваться в развертывании служб удаленных рабочих столов, рекомендуется использовать наши [сценарии автоматизации](https://github.com/arcadiahlyy/aramigration) для экспорта, преобразования и импорта UPD в развертывание служб удаленных рабочих столов.</span><span class="sxs-lookup"><span data-stu-id="73ad8-140">If these disks will be used in an RDS deployment we recommend to use our [automated scripts](https://github.com/arcadiahlyy/aramigration) that will export, convert, and import the UPD's into an RDS deployment.</span></span>

