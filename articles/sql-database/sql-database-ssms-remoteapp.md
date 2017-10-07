---
title: "aaaConnect tooSQL базы данных с помощью SQL Server Management Studio в Azure RemoteApp | Документы Microsoft"
description: "Как использовать этот учебник toolearn toouse SQL Server Management Studio в Azure RemoteApp для обеспечения безопасности и производительности при подключении tooSQL базы данных"
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a><span data-ttu-id="fcc42-103">Используйте SQL Server Management Studio в Azure RemoteApp tooconnect tooSQL базы данных</span><span class="sxs-lookup"><span data-stu-id="fcc42-103">Use SQL Server Management Studio in Azure RemoteApp tooconnect tooSQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fcc42-104">Мы выводим удаленное приложение Azure RemoteApp из эксплуатации.</span><span class="sxs-lookup"><span data-stu-id="fcc42-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="fcc42-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="fcc42-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="fcc42-106">Введение</span><span class="sxs-lookup"><span data-stu-id="fcc42-106">Introduction</span></span>
<span data-ttu-id="fcc42-107">В этом учебнике показано как toouse SQL Server Management Studio (SSMS) в Azure RemoteApp tooconnect tooSQL базы данных.</span><span class="sxs-lookup"><span data-stu-id="fcc42-107">This tutorial shows you how toouse SQL Server Management Studio (SSMS) in Azure RemoteApp tooconnect tooSQL Database.</span></span> <span data-ttu-id="fcc42-108">Пошаговое описание процесса настройки SQL Server Management Studio в Azure RemoteApp hello, объясняет преимущества hello и показывает средства безопасности, которые можно использовать в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fcc42-108">It walks you through hello process of setting up SQL Server Management Studio in Azure RemoteApp, explains hello benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="fcc42-109">**Предполагаемое время toocomplete:** 45 минут</span><span class="sxs-lookup"><span data-stu-id="fcc42-109">**Estimated time toocomplete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="fcc42-110">SSMS в Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="fcc42-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="fcc42-111">Azure RemoteApp — это служба удаленных рабочих столов в Azure, предоставляющая приложения.</span><span class="sxs-lookup"><span data-stu-id="fcc42-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="fcc42-112">Узнать о ней больше можно здесь: [Что такое Azure RemoteApp?](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="fcc42-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="fcc42-113">Среда SSMS, работающих в Azure RemoteApp позволяет hello такие же возможности, как при запуске среда SSMS локально.</span><span class="sxs-lookup"><span data-stu-id="fcc42-113">SSMS running in Azure RemoteApp gives you hello same experience as running SSMS locally.</span></span>

![Снимок экрана: выполнение SSMS в Azure RemoteApp][1]

## <a name="benefits"></a><span data-ttu-id="fcc42-115">Преимущества</span><span class="sxs-lookup"><span data-stu-id="fcc42-115">Benefits</span></span>
<span data-ttu-id="fcc42-116">Существует много преимуществ toousing SSMS в Azure RemoteApp, включая:</span><span class="sxs-lookup"><span data-stu-id="fcc42-116">There are many benefits toousing SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="fcc42-117">Порт 1433 для Azure SQL server не поддерживает toobe предоставляется извне (за пределами Azure).</span><span class="sxs-lookup"><span data-stu-id="fcc42-117">Port 1433 on Azure SQL server does not have toobe exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="fcc42-118">Нет необходимости tookeep, добавлять и удалять IP-адреса в брандмауэр сервера Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="fcc42-118">No need tookeep adding and removing IP addresses in hello Azure SQL server firewall.</span></span>
* <span data-ttu-id="fcc42-119">Все подключения к Azure RemoteApp выполняются по протоколу HTTPS к порту 443 с помощью зашифрованного протокола удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="fcc42-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="fcc42-120">Предусмотрена возможность масштабирования и поддержка многопользовательского режима.</span><span class="sxs-lookup"><span data-stu-id="fcc42-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="fcc42-121">Нет выигрыш от необходимости SSMS в hello в одном регионе hello базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="fcc42-121">There is a performance gain from having SSMS in hello same region as hello SQL Database.</span></span>
* <span data-ttu-id="fcc42-122">Можно проводить аудит использования Azure RemoteApp на выпуск Premium hello Azure Active Directory, которая содержит отчеты о действиях пользователя.</span><span class="sxs-lookup"><span data-stu-id="fcc42-122">You can audit use of Azure RemoteApp with hello Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="fcc42-123">Можно включить многофакторную проверку подлинности (MFA).</span><span class="sxs-lookup"><span data-stu-id="fcc42-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="fcc42-124">Доступ SSMS в любом месте в любом из hello поддерживается Azure RemoteApp клиентов, включая Android, Mac, Windows Phone, iOS и ПК Windows.</span><span class="sxs-lookup"><span data-stu-id="fcc42-124">Access SSMS anywhere when using any of hello supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-hello-azure-remoteapp-collection"></a><span data-ttu-id="fcc42-125">Создайте коллекцию Azure RemoteApp hello</span><span class="sxs-lookup"><span data-stu-id="fcc42-125">Create hello Azure RemoteApp collection</span></span>
<span data-ttu-id="fcc42-126">Ниже приведены шаги toocreate hello вашей коллекции Azure RemoteApp с помощью SSMS.</span><span class="sxs-lookup"><span data-stu-id="fcc42-126">Here are hello steps toocreate your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="fcc42-127">1. Создание новой виртуальной машины Windows из образа</span><span class="sxs-lookup"><span data-stu-id="fcc42-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="fcc42-128">Используйте hello «Windows Server удаленного рабочего стола сеанса узла Windows Server 2012 R2» образ из коллекции toomake hello вашей новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="fcc42-128">Use hello "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from hello Gallery toomake your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="fcc42-129">2. Установка SSMS из SQL Express</span><span class="sxs-lookup"><span data-stu-id="fcc42-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="fcc42-130">Перейдите на hello новой виртуальной Машины и перейдите на страницу загрузки toothis: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="fcc42-130">Go onto hello new VM and navigate toothis download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="fcc42-131">Отсутствует параметр tooonly загрузки SSMS.</span><span class="sxs-lookup"><span data-stu-id="fcc42-131">There is an option tooonly download SSMS.</span></span> <span data-ttu-id="fcc42-132">После загрузки перейдите в каталог установки hello и запустите программу установки tooinstall SSMS.</span><span class="sxs-lookup"><span data-stu-id="fcc42-132">After download, go into hello install directory and run Setup tooinstall SSMS.</span></span>

<span data-ttu-id="fcc42-133">Необходимо также tooinstall SQL Server 2014 с пакетом обновления 1.</span><span class="sxs-lookup"><span data-stu-id="fcc42-133">You also need tooinstall SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="fcc42-134">Файл для скачивания доступен здесь: [Microsoft SQL Server 2014 с пакетом обновления 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694).</span><span class="sxs-lookup"><span data-stu-id="fcc42-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="fcc42-135">SQL Server 2014 с пакетом обновления 1 включает основные функциональные возможности для работы с базой данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc42-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="fcc42-136">3. Запуск сценария проверки и средства SysPrep</span><span class="sxs-lookup"><span data-stu-id="fcc42-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="fcc42-137">Сценарий PowerShell с именем Validate hello является рабочий стол hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="fcc42-137">On hello desktop of hello VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="fcc42-138">Запустите его двойным щелчком мыши.</span><span class="sxs-lookup"><span data-stu-id="fcc42-138">Run this by double-clicking.</span></span> <span data-ttu-id="fcc42-139">Он будет проверить, hello виртуальной Машины готовы toobe, используемое для размещения удаленных приложений.</span><span class="sxs-lookup"><span data-stu-id="fcc42-139">It will verify that hello VM is ready toobe used for remote hosting of applications.</span></span> <span data-ttu-id="fcc42-140">После завершения проверки он запросит toorun sysprep - toorun выберите его.</span><span class="sxs-lookup"><span data-stu-id="fcc42-140">When verification is complete, it will ask toorun sysprep - choose toorun it.</span></span>

<span data-ttu-id="fcc42-141">По завершении работы программы sysprep завершается hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="fcc42-141">When sysprep completes, it will shut down hello VM.</span></span>

<span data-ttu-id="fcc42-142">. в разделе toolearn Дополнительные сведения о создании образа Azure RemoteApp: [как toocreate шаблона RemoteApp образа в Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="fcc42-142">toolearn more about creating a Azure RemoteApp image, see: [How toocreate a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="fcc42-143">4. Запись образа</span><span class="sxs-lookup"><span data-stu-id="fcc42-143">4. Capture image</span></span>
<span data-ttu-id="fcc42-144">Когда hello, виртуальная машина остановлена, найдите ее в текущем портале hello и записать ее.</span><span class="sxs-lookup"><span data-stu-id="fcc42-144">When hello VM has stopped running, find it in hello current portal and capture it.</span></span>

<span data-ttu-id="fcc42-145">toolearn Дополнительные сведения о записи образа, в разделе [запись образа виртуальной машины Microsoft Azure, созданных с помощью hello классической модели развертывания](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="fcc42-145">toolearn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with hello classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-tooazure-remoteapp-template-images"></a><span data-ttu-id="fcc42-146">5. Добавление изображений tooAzure шаблона RemoteApp</span><span class="sxs-lookup"><span data-stu-id="fcc42-146">5. Add tooAzure RemoteApp Template images</span></span>
<span data-ttu-id="fcc42-147">В hello раздел hello текущей версией портала Azure RemoteApp перейдите на вкладку toohello образы шаблона и нажмите кнопку Добавить.</span><span class="sxs-lookup"><span data-stu-id="fcc42-147">In hello Azure RemoteApp section of hello current portal, go toohello Template Images tab and click Add.</span></span> <span data-ttu-id="fcc42-148">Во всплывающем окне приветствия выберите «Импортировать образ из библиотеки виртуальных машин» и выберите hello образ, который вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="fcc42-148">In hello pop-up box, select "Import an image from your Virtual Machines library" and then choose hello Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="fcc42-149">6. Создание облачной коллекции</span><span class="sxs-lookup"><span data-stu-id="fcc42-149">6. Create cloud collection</span></span>
<span data-ttu-id="fcc42-150">В текущем портале hello создайте новую коллекцию облако Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fcc42-150">In hello current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="fcc42-151">Выберите образ шаблона только что импортированный вами с помощью SSMS, установленными на нем hello.</span><span class="sxs-lookup"><span data-stu-id="fcc42-151">Choose hello Template Image that you just imported with SSMS installed on it.</span></span>

![Создание облачной коллекции][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="fcc42-153">7. Публикация SSMS</span><span class="sxs-lookup"><span data-stu-id="fcc42-153">7. Publish SSMS</span></span>
<span data-ttu-id="fcc42-154">На hello публикации вкладка облачной коллекции, выберите опубликовать приложение из меню "Пуск" Здравствуйте и выберите из списка hello SSMS.</span><span class="sxs-lookup"><span data-stu-id="fcc42-154">On hello Publishing tab of your new cloud collection, select Publish an application from hello Start Menu and then choose SSMS from hello list.</span></span>

![Публикация приложения][5]

### <a name="8-add-users"></a><span data-ttu-id="fcc42-156">8. Добавление пользователей</span><span class="sxs-lookup"><span data-stu-id="fcc42-156">8. Add users</span></span>
<span data-ttu-id="fcc42-157">На вкладке hello доступ пользователя можно выбрать hello пользователей, которые будут иметь коллекции Azure RemoteApp toothis доступа, которая включает только SSMS.</span><span class="sxs-lookup"><span data-stu-id="fcc42-157">On hello User Access tab you can select hello users that will have access toothis Azure RemoteApp collection which only includes SSMS.</span></span>

![Добавить пользователя][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a><span data-ttu-id="fcc42-159">9. Установить клиентское приложение hello Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="fcc42-159">9. Install hello Azure RemoteApp client application</span></span>
<span data-ttu-id="fcc42-160">Клиент Azure RemoteApp можно скачать и установить отсюда: [Скачивание | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="fcc42-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="fcc42-161">Настройка Azure SQL Server</span><span class="sxs-lookup"><span data-stu-id="fcc42-161">Configure Azure SQL server</span></span>
<span data-ttu-id="fcc42-162">Hello только tooensure, которая обслуживает Azure — требуется настройка включено для hello брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="fcc42-162">hello only configuration needed is tooensure that Azure Services is enabled for hello firewall.</span></span> <span data-ttu-id="fcc42-163">При использовании этого решения, то вам не требуется tooadd любом брандмауэре hello tooopen адресов IP.</span><span class="sxs-lookup"><span data-stu-id="fcc42-163">If you use this solution, then you do not need tooadd any IP addresses tooopen hello firewall.</span></span> <span data-ttu-id="fcc42-164">Hello сетевой трафик, который может быть toohello SQL Server — от других служб Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc42-164">hello network traffic that is allowed toohello SQL Server is from other Azure services.</span></span>

![Разрешение Azure][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="fcc42-166">Многофакторная проверка подлинности (MFA)</span><span class="sxs-lookup"><span data-stu-id="fcc42-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="fcc42-167">Многофакторную проверку подлинности можно включить специально для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="fcc42-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="fcc42-168">Go toohello вкладке приложений в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fcc42-168">Go toohello Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="fcc42-169">Здесь вы найдете запись для Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fcc42-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="fcc42-170">Если щелкнуть это приложение и затем настройте, вы увидите hello страницу под которой вы можете включить многофакторную проверку Подлинности для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="fcc42-170">If you click that application and then configure, you will see hello page below where you can enable MFA for this application.</span></span>

![Включение MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="fcc42-172">Аудит действий пользователей с помощью Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="fcc42-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="fcc42-173">Если у вас Azure AD Premium, то у вас есть tooturn его на в hello лицензий раздела каталога.</span><span class="sxs-lookup"><span data-stu-id="fcc42-173">If you do not have Azure AD Premium, then you have tooturn it on in hello Licenses section of your directory.</span></span> <span data-ttu-id="fcc42-174">С помощью Premium включена можно назначать пользователей toohello уровня Premium.</span><span class="sxs-lookup"><span data-stu-id="fcc42-174">With Premium enabled, you can assign users toohello Premium level.</span></span>

<span data-ttu-id="fcc42-175">При переходе пользователя tooa в Azure Active Directory можно переходить tooAzure входа сведения для действия вкладку toohello toosee RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fcc42-175">When you go tooa user in your Azure Active Directory, you can then go toohello Activity tab toosee login information tooAzure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcc42-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fcc42-176">Next steps</span></span>
<span data-ttu-id="fcc42-177">После выполнения всех hello выше действия, необходимо будет toorun hello Azure RemoteApp клиента и в журнал с назначенный пользователь.</span><span class="sxs-lookup"><span data-stu-id="fcc42-177">After completing all hello above steps, you will be able toorun hello Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="fcc42-178">Откроется с помощью SSMS как одно из приложений и запустить его как если бы она была установлена на компьютере с SQL server tooAzure доступа.</span><span class="sxs-lookup"><span data-stu-id="fcc42-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access tooAzure SQL server.</span></span>

<span data-ttu-id="fcc42-179">Дополнительные сведения о как toomake hello tooSQL подключения базы данных см. в разделе [подключать tooSQL базы данных SQL Server Management Studio и выполнить пробный запрос T-SQL](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="fcc42-179">For more information on how toomake hello connection tooSQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="fcc42-180">Пока что у нас всё.</span><span class="sxs-lookup"><span data-stu-id="fcc42-180">That's everything for now.</span></span> <span data-ttu-id="fcc42-181">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="fcc42-181">Enjoy!</span></span>

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png