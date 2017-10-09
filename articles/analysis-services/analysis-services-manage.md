---
title: "aaaManage Azure Analysis Services | Документы Microsoft"
description: "Узнайте, как toomanage служб Analysis Services server в Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a><span data-ttu-id="9cc08-103">Управление службами Analysis Services</span><span class="sxs-lookup"><span data-stu-id="9cc08-103">Manage Analysis Services</span></span>
<span data-ttu-id="9cc08-104">После создания сервера служб Analysis Services в Azure, могут иметься некоторые задачи администрирования и управления tooperform необходимо немедленно или некоторое время вниз road hello.</span><span class="sxs-lookup"><span data-stu-id="9cc08-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need tooperform right away or sometime down hello road.</span></span> <span data-ttu-id="9cc08-105">Например запустите обработку toohello обновления данных, управление правами на доступ к моделям hello на сервере, или наблюдать за исправностью сервера.</span><span class="sxs-lookup"><span data-stu-id="9cc08-105">For example, run processing toohello refresh data, control who can access hello models on your server, or monitor your server's health.</span></span> <span data-ttu-id="9cc08-106">Некоторые задачи управления можно выполнять только на портале Azure, другие — только в SQL Server Management Studio (SSMS), а некоторые — и там, и там.</span><span class="sxs-lookup"><span data-stu-id="9cc08-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="9cc08-107">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="9cc08-107">Azure portal</span></span>
<span data-ttu-id="9cc08-108">[Портал Azure](http://portal.azure.com/) можно создать и удалить серверы, отслеживать ресурсы сервера, изменить размер, и управления, у кого есть доступ tooyour серверов.</span><span class="sxs-lookup"><span data-stu-id="9cc08-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access tooyour servers.</span></span>  <span data-ttu-id="9cc08-109">При возникновении проблем вы также можете отправить запрос на техническую поддержку.</span><span class="sxs-lookup"><span data-stu-id="9cc08-109">If you're having some problems, you can also submit a support request.</span></span>

![Получение имени сервера в Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="9cc08-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="9cc08-111">SQL Server Management Studio</span></span>
<span data-ttu-id="9cc08-112">Подключение сервера tooyour в Azure выполняется так же, как соединение tooa экземпляра сервера в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="9cc08-112">Connecting tooyour server in Azure is just like connecting tooa server instance in your own organization.</span></span> <span data-ttu-id="9cc08-113">В SSMS можно выполнять многие hello же задачи, такие как обработки данных или создайте сценарий обработки, управление ролями и с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9cc08-113">From SSMS, you can perform many of hello same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="9cc08-115">Скачивание и установка SSMS</span><span class="sxs-lookup"><span data-stu-id="9cc08-115">Download and install SSMS</span></span>
<span data-ttu-id="9cc08-116">tooget все Здравствуйте новейшие функции и возможности наиболее hello, при подключении сервера tooyour Azure Analysis Services, убедитесь, что вы используете последнюю версию SSMS hello.</span><span class="sxs-lookup"><span data-stu-id="9cc08-116">tooget all hello latest features, and hello smoothest experience when connecting tooyour Azure Analysis Services server, be sure you're using hello latest version of SSMS.</span></span> 

<span data-ttu-id="9cc08-117">[Скачайте SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="9cc08-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="tooconnect-with-ssms"></a><span data-ttu-id="9cc08-118">tooconnect со средой SSMS</span><span class="sxs-lookup"><span data-stu-id="9cc08-118">tooconnect with SSMS</span></span>
 <span data-ttu-id="9cc08-119">При использовании SSMS до подключения приветствие сервера tooyour первый раз, убедитесь, что ваше имя пользователя входит в группу "Администраторы" Analysis Services hello.</span><span class="sxs-lookup"><span data-stu-id="9cc08-119">When using SSMS, before connecting tooyour server hello first time, make sure your username is included in hello Analysis Services Admins group.</span></span> <span data-ttu-id="9cc08-120">toolearn более, в разделе [администраторам](#server-administrators) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="9cc08-120">toolearn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="9cc08-121">Перед подключением, необходимо имя сервера tooget hello.</span><span class="sxs-lookup"><span data-stu-id="9cc08-121">Before you connect, you need tooget hello server name.</span></span> <span data-ttu-id="9cc08-122">В **портал Azure** > сервера > **Обзор** > **имя сервера**, имя сервера hello копирования.</span><span class="sxs-lookup"><span data-stu-id="9cc08-122">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Получение имени сервера в Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="9cc08-124">В среде SSMS выберите **Обозреватель объектов** и щелкните **Подключиться** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="9cc08-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="9cc08-125">В hello **подключения tooServer** диалоговое окно «», вставьте в поле имя сервера hello, а затем в **проверки подлинности**, выберите один из следующих типов проверки подлинности hello:</span><span class="sxs-lookup"><span data-stu-id="9cc08-125">In hello **Connect tooServer** dialog box, paste in hello server name, then in **Authentication**, choose one of hello following authentication types:</span></span>
   
    <span data-ttu-id="9cc08-126">**Проверка подлинности Windows** toouse учетные данные Windows домен\имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="9cc08-126">**Windows Authentication** toouse your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="9cc08-127">**Пароль проверки подлинности Active Directory** toouse учетной записи организации.</span><span class="sxs-lookup"><span data-stu-id="9cc08-127">**Active Directory Password Authentication** toouse an organizational account.</span></span> <span data-ttu-id="9cc08-128">Например, при подключении с компьютера, не присоединенного к домену.</span><span class="sxs-lookup"><span data-stu-id="9cc08-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="9cc08-129">**Универсальной проверки подлинности Active Directory** toouse [неинтерактивной или многофакторной проверки подлинности](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9cc08-129">**Active Directory Universal Authentication** toouse [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![Подключение в среде SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="9cc08-131">Администраторы сервера и пользователи базы данных</span><span class="sxs-lookup"><span data-stu-id="9cc08-131">Server administrators and database users</span></span>
<span data-ttu-id="9cc08-132">В службах Azure Analysis Services существует два типа пользователей, администраторы сервера и пользователи базы данных.</span><span class="sxs-lookup"><span data-stu-id="9cc08-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="9cc08-133">Оба типа пользователей должны находиться в Azure Active Directory и иметь настроенный адрес электронной почты организации или имя участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="9cc08-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="9cc08-134">toolearn более, в разделе [проверки подлинности и пользовательские разрешения](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="9cc08-134">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="9cc08-135">Устранение неполадок с подключением</span><span class="sxs-lookup"><span data-stu-id="9cc08-135">Troubleshooting connection problems</span></span>
<span data-ttu-id="9cc08-136">При подключении с помощью SSMS, если возникли проблемы, может потребоваться tooclear hello входа кэша.</span><span class="sxs-lookup"><span data-stu-id="9cc08-136">When connecting using SSMS, if you run into problems, you may need tooclear hello login cache.</span></span> <span data-ttu-id="9cc08-137">Ничего не кэшированных toodisc.</span><span class="sxs-lookup"><span data-stu-id="9cc08-137">Nothing is cached toodisc.</span></span> <span data-ttu-id="9cc08-138">tooclear hello кэш-памяти, закройте и перезапустите hello подключения процесса.</span><span class="sxs-lookup"><span data-stu-id="9cc08-138">tooclear hello cache, close and restart hello connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9cc08-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9cc08-139">Next steps</span></span>
<span data-ttu-id="9cc08-140">Если уже еще не развернут новый сервер tooyour табличной модели, сейчас самое подходящее время.</span><span class="sxs-lookup"><span data-stu-id="9cc08-140">If you haven't already deployed a tabular model tooyour new server, now is a good time.</span></span> <span data-ttu-id="9cc08-141">toolearn более, в разделе [развертывания служб Analysis Services tooAzure](analysis-services-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="9cc08-141">toolearn more, see [Deploy tooAzure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="9cc08-142">При развертывании сервера tooyour модели вы готовы tooconnect tooit с помощью клиента или браузера.</span><span class="sxs-lookup"><span data-stu-id="9cc08-142">If you've deployed a model tooyour server, you're ready tooconnect tooit using a client or browser.</span></span> <span data-ttu-id="9cc08-143">toolearn более, в разделе [получение данных из служб Azure Analysis server](analysis-services-connect.md).</span><span class="sxs-lookup"><span data-stu-id="9cc08-143">toolearn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

