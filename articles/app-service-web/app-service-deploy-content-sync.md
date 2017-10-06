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
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a>Синхронизация содержимого из tooAzure папку облачной службы приложений
В этом учебнике показано как toodeploy слишком[службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) по синхронизации содержимого из популярных облачные службы хранения, такие как общий банк данных и OneDrive. 

## <a name="overview"></a>Обзор развертывания синхронизации содержимого
на платформе развертывания содержимого синхронизации по требованию Hello hello [подсистема развертывания Kudu](https://github.com/projectkudu/kudu/wiki) интегрировать службы приложений. В hello [портала Azure](https://portal.azure.com), можно указать папку в облачного хранилища, работают с кодом приложения и содержимого в этой папке и tooApp синхронизация службы с hello нажатием кнопки. Синхронизация содержимого использует процесс Kudu hello для построения и развертывания. 

## <a name="contentsync"></a>Каким образом содержимое tooenable синхронизации развертывания
Синхронизация содержимого tooenable из hello [портала Azure](https://portal.azure.com), выполните следующие действия:

1. В колонке приложения в hello портала Azure щелкните **параметры** > **источник развертывания**. Нажмите кнопку **Выбор источника**, а затем выберите **OneDrive** или **Dropbox** как источник hello для развертывания. 
   
    ![Синхронизация содержимого](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > Из-за базовых различий в API-интерфейсы, hello **OneDrive для бизнеса** в настоящее время не поддерживается. 
   > 
   > 
2. Полный hello авторизации рабочего процесса tooenable tooaccess службы приложений определенный заранее определенные назначенного пути для OneDrive или Dropbox, все содержимое приложения службы будет храниться.  
    После авторизации hello, который предоставит службы приложений платформы toocreate параметр hello папки содержимого в hello назначить путь к содержимому или toochoose содержимого папок по этому пути, указанного содержимого. Hello указанных путей к содержимому в вашей учетных записей облачного хранилища используется для синхронизации службы приложений являются hello следующее:  
   
   * **OneDrive**: `Apps\Azure Web Apps` 
   * **Dropbox**: `Dropbox\Apps\Azure`
3. После hello синхронизации содержимого hello начальной синхронизации содержимого может запускаться по требованию из hello портал Azure. Журнал развертывания недоступен с hello **развертываний** колонку.
   
    ![Журнал развертываний](./media/app-service-deploy-content-sync/onedrive_sync.png)

Дополнительные сведения о развертывании Dropbox можно найти в разделе [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx). 

