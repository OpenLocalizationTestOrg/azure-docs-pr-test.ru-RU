---
title: "содержимое aaaSync из tooAzure папку облачной службы приложений"
description: "Узнайте, как toodeploy tooAzure вашего приложения службы приложений, через содержимое синхронизации из папки облака."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 88d3a670-303a-4fa2-9de9-715cc904acec
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: e1c6d53a427c36126d9cdb33cc21b4126b9d9c2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a><span data-ttu-id="6307e-103">Синхронизация содержимого из tooAzure папку облачной службы приложений</span><span class="sxs-lookup"><span data-stu-id="6307e-103">Sync content from a cloud folder tooAzure App Service</span></span>
<span data-ttu-id="6307e-104">В этом учебнике показано как toodeploy слишком[службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) по синхронизации содержимого из популярных облачные службы хранения, такие как общий банк данных и OneDrive.</span><span class="sxs-lookup"><span data-stu-id="6307e-104">This tutorial shows you how toodeploy too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="6307e-105"><a name="overview"></a>Обзор развертывания синхронизации содержимого</span><span class="sxs-lookup"><span data-stu-id="6307e-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="6307e-106">на платформе развертывания содержимого синхронизации по требованию Hello hello [подсистема развертывания Kudu](https://github.com/projectkudu/kudu/wiki) интегрировать службы приложений.</span><span class="sxs-lookup"><span data-stu-id="6307e-106">hello on-demand content sync deployment is powered by hello [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="6307e-107">В hello [портала Azure](https://portal.azure.com), можно указать папку в облачного хранилища, работают с кодом приложения и содержимого в этой папке и tooApp синхронизация службы с hello нажатием кнопки.</span><span class="sxs-lookup"><span data-stu-id="6307e-107">In hello [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync tooApp Service with hello click of a button.</span></span> <span data-ttu-id="6307e-108">Синхронизация содержимого использует процесс Kudu hello для построения и развертывания.</span><span class="sxs-lookup"><span data-stu-id="6307e-108">Content sync utilizes hello Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="6307e-109"><a name="contentsync"></a>Каким образом содержимое tooenable синхронизации развертывания</span><span class="sxs-lookup"><span data-stu-id="6307e-109"><a name="contentsync"></a>How tooenable content sync deployment</span></span>
<span data-ttu-id="6307e-110">Синхронизация содержимого tooenable из hello [портала Azure](https://portal.azure.com), выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="6307e-110">tooenable content sync from hello [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="6307e-111">В колонке приложения в hello портала Azure щелкните **параметры** > **источник развертывания**.</span><span class="sxs-lookup"><span data-stu-id="6307e-111">In your app's blade in hello Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="6307e-112">Нажмите кнопку **Выбор источника**, а затем выберите **OneDrive** или **Dropbox** как источник hello для развертывания.</span><span class="sxs-lookup"><span data-stu-id="6307e-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as hello source for deployment.</span></span> 
   
    ![Синхронизация содержимого](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="6307e-114">Из-за базовых различий в API-интерфейсы, hello **OneDrive для бизнеса** в настоящее время не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="6307e-114">Because of underlying differences in hello APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="6307e-115">Полный hello авторизации рабочего процесса tooenable tooaccess службы приложений определенный заранее определенные назначенного пути для OneDrive или Dropbox, все содержимое приложения службы будет храниться.</span><span class="sxs-lookup"><span data-stu-id="6307e-115">Complete hello authorization workflow tooenable App Service tooaccess a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="6307e-116">После авторизации hello, который предоставит службы приложений платформы toocreate параметр hello папки содержимого в hello назначить путь к содержимому или toochoose содержимого папок по этому пути, указанного содержимого.</span><span class="sxs-lookup"><span data-stu-id="6307e-116">After authorization hello App Service platform will give you hello option toocreate a content folder under hello designated content path, or toochoose an existing content folder under this designated content path.</span></span> <span data-ttu-id="6307e-117">Hello указанных путей к содержимому в вашей учетных записей облачного хранилища используется для синхронизации службы приложений являются hello следующее:</span><span class="sxs-lookup"><span data-stu-id="6307e-117">hello designated content paths under your cloud storage accounts used for App Service sync are hello following:</span></span>  
   
   * <span data-ttu-id="6307e-118">**OneDrive**: `Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="6307e-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="6307e-119">**Dropbox**: `Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="6307e-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="6307e-120">После hello синхронизации содержимого hello начальной синхронизации содержимого может запускаться по требованию из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6307e-120">After hello initial content sync hello content sync can be initiated on demand from hello Azure portal.</span></span> <span data-ttu-id="6307e-121">Журнал развертывания недоступен с hello **развертываний** колонку.</span><span class="sxs-lookup"><span data-stu-id="6307e-121">Deployment history is available with hello **Deployments** blade.</span></span>
   
    ![Журнал развертываний](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="6307e-123">Дополнительные сведения о развертывании Dropbox можно найти в разделе [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span><span class="sxs-lookup"><span data-stu-id="6307e-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

