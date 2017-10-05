---
title: "Синхронизация содержимого из папки в облаке со службами приложений Azure"
description: "Узнайте, как развертывать приложение в службе приложений Azure с помощью синхронизации содержимого из папки в облаке."
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
ms.openlocfilehash: 010e7dc492abefaa3afe814c0322af9f6fe5acd2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="sync-content-from-a-cloud-folder-to-azure-app-service"></a><span data-ttu-id="76092-103">Синхронизация содержимого из папки в облаке со службами приложений Azure</span><span class="sxs-lookup"><span data-stu-id="76092-103">Sync content from a cloud folder to Azure App Service</span></span>
<span data-ttu-id="76092-104">В этом учебнике показано, как выполнить развертывание в [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) , синхронизируя содержимое из популярных облачных служб хранилища, например Dropbox и OneDrive.</span><span class="sxs-lookup"><span data-stu-id="76092-104">This tutorial shows you how to deploy to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="76092-105"><a name="overview"></a>Обзор развертывания синхронизации содержимого</span><span class="sxs-lookup"><span data-stu-id="76092-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="76092-106">Развертывание синхронизации содержимого по запросу основано на [механизме развертывания Kudu](https://github.com/projectkudu/kudu/wiki), который интегрирован в службу приложений.</span><span class="sxs-lookup"><span data-stu-id="76092-106">The on-demand content sync deployment is powered by the [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="76092-107">На [портале Azure](https://portal.azure.com) в облачном хранилище можно указать специальную папку, в которой вы будете работать с кодом приложения и содержимым. Затем эту папку можно синхронизировать со службой приложений нажатием всего лишь одной кнопки.</span><span class="sxs-lookup"><span data-stu-id="76092-107">In the [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync to App Service with the click of a button.</span></span> <span data-ttu-id="76092-108">При синхронизации содержимого для выполнения сборки и развертывания используется процесс Kudu.</span><span class="sxs-lookup"><span data-stu-id="76092-108">Content sync utilizes the Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="76092-109"><a name="contentsync"></a>Как включить развертывание синхронизации содержимого</span><span class="sxs-lookup"><span data-stu-id="76092-109"><a name="contentsync"></a>How to enable content sync deployment</span></span>
<span data-ttu-id="76092-110">Чтобы включить синхронизацию содержимого на [портале Azure](https://portal.azure.com), выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="76092-110">To enable content sync from the [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="76092-111">На портале Azure в колонке приложения щелкните **Параметры** > **Источник развертывания**.</span><span class="sxs-lookup"><span data-stu-id="76092-111">In your app's blade in the Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="76092-112">Щелкните **Выбор источника** и в качестве источника развертывания выберите **OneDrive** или **Dropbox**.</span><span class="sxs-lookup"><span data-stu-id="76092-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as the source for deployment.</span></span> 
   
    ![Синхронизация содержимого](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="76092-114">Из-за основных различий в интерфейсах API **OneDrive для бизнеса** пока не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="76092-114">Because of underlying differences in the APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="76092-115">Завершите процесс авторизации, чтобы разрешить службе приложений доступ к конкретному предварительно определенному пути OneDrive или Dropbox, где будет храниться все ваше содержимое службы приложений.</span><span class="sxs-lookup"><span data-stu-id="76092-115">Complete the authorization workflow to enable App Service to access a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="76092-116">После авторизации платформа службы приложений предоставит возможность создать папку содержимого по указанному пути либо выбрать существующую папку содержимого по этому пути.</span><span class="sxs-lookup"><span data-stu-id="76092-116">After authorization the App Service platform will give you the option to create a content folder under the designated content path, or to choose an existing content folder under this designated content path.</span></span> <span data-ttu-id="76092-117">Ниже перечислены назначенные пути к содержимому учетных записей хранения в облаке, используемые для синхронизации службы приложений.</span><span class="sxs-lookup"><span data-stu-id="76092-117">The designated content paths under your cloud storage accounts used for App Service sync are the following:</span></span>  
   
   * <span data-ttu-id="76092-118">**OneDrive**: `Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="76092-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="76092-119">**Dropbox**: `Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="76092-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="76092-120">После первоначальной синхронизации содержимого ее можно будет запускать по требованию с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="76092-120">After the initial content sync the content sync can be initiated on demand from the Azure portal.</span></span> <span data-ttu-id="76092-121">Журнал развертываний доступен в колонке **Развертывания** .</span><span class="sxs-lookup"><span data-stu-id="76092-121">Deployment history is available with the **Deployments** blade.</span></span>
   
    ![Журнал развертываний](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="76092-123">Дополнительные сведения о развертывании Dropbox можно найти в разделе [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span><span class="sxs-lookup"><span data-stu-id="76092-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

