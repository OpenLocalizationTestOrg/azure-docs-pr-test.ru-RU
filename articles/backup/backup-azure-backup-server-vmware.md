---
title: "Резервное копирование серверов VMware с помощью Azure Backup Server | Документация Майкрософт"
description: "Для резервного копирования серверов VMware vCenter и ESXi в облако Azure или на диск можно использовать Azure Backup Server. В этой статье приведены пошаговые инструкции для резервного копирования (или защиты) рабочих нагрузок VMware."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
ms.assetid: 6b131caf-de85-4eba-b8e6-d8a04545cd9d
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: markgal;
ms.openlocfilehash: ad331dffb7c31d12290f4223967c568e4535fe3c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-a-vmware-server-to-azure"></a><span data-ttu-id="a4b87-104">Резервное копирование сервера VMware в Azure</span><span class="sxs-lookup"><span data-stu-id="a4b87-104">Back up a VMware server to Azure</span></span>

<span data-ttu-id="a4b87-105">В этой статье описывается, как настроить Azure Backup Server для защиты рабочих нагрузок сервера VMware.</span><span class="sxs-lookup"><span data-stu-id="a4b87-105">This article explains how to configure Azure Backup Server to help protect VMware server workloads.</span></span> <span data-ttu-id="a4b87-106">Чтобы приступить к работе с этим руководством, вам необходимо установить сервер резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b87-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="a4b87-107">Если у вас не установлен Azure Backup Server, ознакомьтесь со статьей [Подготовка к резервному копированию рабочих нагрузок с использованием сервера службы архивации Azure](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="a4b87-107">If you don't have Azure Backup Server installed, see [Prepare to back up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="a4b87-108">Azure Backup Server обеспечивает резервное копирование (или защиту) серверов VMware vCenter версий 6.5, 6.0 и 5.5.</span><span class="sxs-lookup"><span data-stu-id="a4b87-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-to-the-vcenter-server"></a><span data-ttu-id="a4b87-109">Создание безопасного подключения к серверу vCenter</span><span class="sxs-lookup"><span data-stu-id="a4b87-109">Create a secure connection to the vCenter Server</span></span>

<span data-ttu-id="a4b87-110">По умолчанию Azure Backup Server взаимодействует с каждым сервером vCenter через канал HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a4b87-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="a4b87-111">Чтобы включить безопасное взаимодействие, мы рекомендуем установить сертификат центра сертификации (ЦС) VMware на сервере Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="a4b87-111">To turn on the secure communication, we recommend that you install the VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="a4b87-112">Если безопасный обмен данными не требуется и вы хотите отключить требование HTTPS, ознакомьтесь с разделом [Отключение протокола безопасной связи](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span><span class="sxs-lookup"><span data-stu-id="a4b87-112">If you don't require secure communication, and would prefer to disable the HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="a4b87-113">Чтобы создать безопасное подключение между сервером Azure Backup Server и сервером vCenter, импортируйте доверенный сертификат на сервер Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="a4b87-113">To create a secure connection between Azure Backup Server and the vCenter Server, import the trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="a4b87-114">Обычно для подключения к серверу vCenter через веб-клиент vSphere используется браузер на компьютере сервера Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="a4b87-114">Typically, you use a browser on the Azure Backup Server machine to connect to the vCenter Server via the vSphere Web Client.</span></span> <span data-ttu-id="a4b87-115">При первом использовании браузера на сервере Azure Backup Server для подключения к серверу vCenter устанавливается небезопасное подключение.</span><span class="sxs-lookup"><span data-stu-id="a4b87-115">The first time you use the Azure Backup Server browser to connect to the vCenter Server, the connection isn't secure.</span></span> <span data-ttu-id="a4b87-116">На следующем рисунке показано незащищенное подключение.</span><span class="sxs-lookup"><span data-stu-id="a4b87-116">The following image shows the unsecured connection.</span></span>

![Пример незащищенного подключения к серверу VMware](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="a4b87-118">Чтобы устранить эту проблему и создать безопасное подключение, скачайте сертификаты доверенного корневого ЦС.</span><span class="sxs-lookup"><span data-stu-id="a4b87-118">To fix this issue, and create a secure connection, download the trusted root CA certificates.</span></span>

1. <span data-ttu-id="a4b87-119">В браузере на сервере Azure Backup Server введите URL-адрес веб-клиента vSphere.</span><span class="sxs-lookup"><span data-stu-id="a4b87-119">In the browser on Azure Backup Server, enter the URL to the vSphere Web Client.</span></span> <span data-ttu-id="a4b87-120">Откроется страница входа веб-клиента vSphere.</span><span class="sxs-lookup"><span data-stu-id="a4b87-120">The vSphere Web Client login page appears.</span></span>

    ![Веб-клиент vSphere](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="a4b87-122">В нижней части сведений для администраторов и разработчиков найдите ссылку для **скачивания сертификатов доверенного корневого ЦС**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-122">At the bottom of the information for administrators and developers, locate the **Download trusted root CA certificates** link.</span></span>

    ![Ссылка для скачивания доверенных корневых сертификатов ЦС](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="a4b87-124">Если страница входа веб-клиента vSphere не отображается, проверьте параметры прокси-сервера в браузере.</span><span class="sxs-lookup"><span data-stu-id="a4b87-124">If you don't see the vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="a4b87-125">Щелкните **Download trusted root CA certificates** (Скачать сертификаты доверенного корневого ЦС).</span><span class="sxs-lookup"><span data-stu-id="a4b87-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="a4b87-126">Сервер vCenter скачает файл на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="a4b87-126">The vCenter Server downloads a file to your local computer.</span></span> <span data-ttu-id="a4b87-127">Имя этого файла — **download**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-127">The file's name is named **download**.</span></span> <span data-ttu-id="a4b87-128">В зависимости от браузера появится сообщение с предложением открыть или сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="a4b87-128">Depending on your browser, you receive a message that asks whether to open or save the file.</span></span>

    ![Сообщение после скачивания сертификатов](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="a4b87-130">Сохраните файл в расположение на сервере Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="a4b87-130">Save the file to a location on Azure Backup Server.</span></span> <span data-ttu-id="a4b87-131">При сохранении файла добавьте к его имени расширение ZIP.</span><span class="sxs-lookup"><span data-stu-id="a4b87-131">When you save the file, add the .zip file name extension.</span></span>

    <span data-ttu-id="a4b87-132">Это ZIP-файл, содержащий сведения о сертификатах.</span><span class="sxs-lookup"><span data-stu-id="a4b87-132">The file is a .zip file that contains the information about the certificates.</span></span> <span data-ttu-id="a4b87-133">С расширением .zip можно использовать средства извлечения.</span><span class="sxs-lookup"><span data-stu-id="a4b87-133">With the .zip extension, you can use the extraction tools.</span></span>

4. <span data-ttu-id="a4b87-134">Щелкните правой кнопкой мыши файл **download.zip**, а затем выберите **Извлечь все**, чтобы извлечь его содержимое.</span><span class="sxs-lookup"><span data-stu-id="a4b87-134">Right-click **download.zip**, and then select **Extract All** to extract the contents.</span></span>

    <span data-ttu-id="a4b87-135">Содержимое сжатого ZIP-файла будет извлечено в папку **certs**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-135">The .zip file extracts its contents to a folder named **certs**.</span></span> <span data-ttu-id="a4b87-136">В этой папке содержатся файлы двух типов.</span><span class="sxs-lookup"><span data-stu-id="a4b87-136">Two types of files appear in the certs folder.</span></span> <span data-ttu-id="a4b87-137">Файл корневого сертификата имеет расширение, которое начинается с нумерованной последовательности, например .0 и .1.</span><span class="sxs-lookup"><span data-stu-id="a4b87-137">The root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="a4b87-138">Файл списка отзыва сертификатов имеет расширение, которое начинается с такой последовательности, как .r0 или .r1.</span><span class="sxs-lookup"><span data-stu-id="a4b87-138">The CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="a4b87-139">Файл списка отзыва сертификатов связан с сертификатом.</span><span class="sxs-lookup"><span data-stu-id="a4b87-139">The CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="a4b87-140">Извлечение скачанного файла на локальный компьютер</span><span class="sxs-lookup"><span data-stu-id="a4b87-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="a4b87-141">В папке **certs** щелкните правой кнопкой мыши файл корневого сертификата, а затем щелкните **Переименовать**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-141">In the **certs** folder, right-click the root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="a4b87-142">Переименование корневого сертификата</span><span class="sxs-lookup"><span data-stu-id="a4b87-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="a4b87-143">Измените расширение файла корневого сертификата на CRT.</span><span class="sxs-lookup"><span data-stu-id="a4b87-143">Change the root certificate's extension to .crt.</span></span> <span data-ttu-id="a4b87-144">При появлении запроса на изменение расширения нажмите кнопку **ОК** или **Да**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-144">When you're asked if you're sure you want to change the extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="a4b87-145">В противном случае изменится соответствующая функция файла.</span><span class="sxs-lookup"><span data-stu-id="a4b87-145">Otherwise, you change the file's intended function.</span></span> <span data-ttu-id="a4b87-146">Значок файла изменится на значок корневого сертификата.</span><span class="sxs-lookup"><span data-stu-id="a4b87-146">The icon for the file changes to an icon that represents a root certificate.</span></span>

6. <span data-ttu-id="a4b87-147">Щелкните правой кнопкой мыши этот корневой сертификат и во всплывающем меню выберите **Установить сертификат**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-147">Right-click the root certificate and from the pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="a4b87-148">Появится диалоговое окно **Мастер импорта сертификатов**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-148">The **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="a4b87-149">В диалоговом окне **Мастер импорта сертификатов** выберите **Локальный компьютер** в качестве места назначения для сертификата, а затем щелкните **Далее**, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="a4b87-149">In the **Certificate Import Wizard** dialog box, select **Local Machine** as the destination for the certificate, and then click **Next** to continue.</span></span>

    ![<span data-ttu-id="a4b87-150">Параметры назначения хранилища сертификатов</span><span class="sxs-lookup"><span data-stu-id="a4b87-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="a4b87-151">Если отобразится запрос разрешения на внесение изменений на компьютер, нажмите кнопку **Да** или **ОК** для всех изменений.</span><span class="sxs-lookup"><span data-stu-id="a4b87-151">If you're asked if you want to allow changes to the computer, click **Yes** or **OK**, to all the changes.</span></span>

8. <span data-ttu-id="a4b87-152">На странице **Хранилище сертификатов** выберите **Поместить все сертификаты в следующее хранилище**, а затем щелкните **Обзор**, чтобы выбрать хранилище сертификатов.</span><span class="sxs-lookup"><span data-stu-id="a4b87-152">On the **Certificate Store** page, select **Place all certificates in the following store**, and then click **Browse** to choose the certificate store.</span></span>

    ![Размещение сертификатов в определенном месте в хранилище](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="a4b87-154">Появится диалоговое окно **Выбор хранилища сертификата**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-154">The **Select Certificate Store** dialog box appears.</span></span>

    ![Иерархия папки хранилища сертификатов](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="a4b87-156">В качестве папки назначения для сертификатов выберите **Доверенные корневые центры сертификации** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-156">Select **Trusted Root Certification Authorities** as the destination folder for the certificates, and then click **OK**.</span></span>

    ![Папка назначения для сертификата](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="a4b87-158">Папка **Доверенные корневые центры сертификации** утверждается как хранилище сертификатов.</span><span class="sxs-lookup"><span data-stu-id="a4b87-158">The **Trusted Root Certification Authorities** folder is confirmed as the certificate store.</span></span> <span data-ttu-id="a4b87-159">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-159">Click **Next**.</span></span>

    ![Папка хранилища сертификатов](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="a4b87-161">На странице **Завершение мастера импорта сертификатов** проверьте, находится ли сертификат в нужной папке, а затем щелкните **Готово**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-161">On the **Completing the Certificate Import Wizard** page, verify that the certificate is in the desired folder, and then click **Finish**.</span></span>

    ![Проверка наличия сертификата в нужной папке](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="a4b87-163">Появится диалоговое окно, что подтверждает успешный импорт сертификата.</span><span class="sxs-lookup"><span data-stu-id="a4b87-163">A dialog box appears, the successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="a4b87-164">Войдите на сервер vCenter, чтобы подтвердить, что подключение защищено.</span><span class="sxs-lookup"><span data-stu-id="a4b87-164">Sign in to the vCenter Server to confirm that your connection is secure.</span></span>

  <span data-ttu-id="a4b87-165">Если при импорте сертификата возникли проблемы и вам не удается установить безопасное подключение, обратитесь к документации по VMware vSphere на странице [VMware vSphere](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span><span class="sxs-lookup"><span data-stu-id="a4b87-165">If the certificate import is not successful, and you cannot establish a secure connection, consult the VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="a4b87-166">Вы можете отключить безопасное подключение, следуя приведенным ниже инструкциям, если в организации защищены границы или вы не хотите включать протокол HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a4b87-166">If you have secure boundaries within your organization, and don't want to turn on the HTTPS protocol, use the following procedure to disable the secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="a4b87-167">Отключение протокола безопасной связи</span><span class="sxs-lookup"><span data-stu-id="a4b87-167">Disable secure communication protocol</span></span>

<span data-ttu-id="a4b87-168">Если вашей организации не требуется протокол HTTPS, отключите его, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="a4b87-168">If your organization doesn't require the HTTPS protocol, use the following steps to disable HTTPS.</span></span> <span data-ttu-id="a4b87-169">Чтобы отключить поведение по умолчанию, создайте раздел реестра, который игнорирует поведение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a4b87-169">To disable the default behavior, create a registry key that ignores the default behavior.</span></span>

1. <span data-ttu-id="a4b87-170">Скопируйте приведенный ниже текст и вставьте его в TXT-файл.</span><span class="sxs-lookup"><span data-stu-id="a4b87-170">Copy and paste the following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="a4b87-171">Сохраните файл на компьютере Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="a4b87-171">Save the file to your Azure Backup Server computer.</span></span> <span data-ttu-id="a4b87-172">Используйте DisableSecureAuthentication.reg как имя файла.</span><span class="sxs-lookup"><span data-stu-id="a4b87-172">For the file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="a4b87-173">Дважды щелкните этот файл, чтобы активировать запись реестра.</span><span class="sxs-lookup"><span data-stu-id="a4b87-173">Double-click the file to activate the registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-the-vcenter-server"></a><span data-ttu-id="a4b87-174">Создание роли и учетной записи пользователя на сервере vCenter</span><span class="sxs-lookup"><span data-stu-id="a4b87-174">Create a role and user account on the vCenter Server</span></span>

<span data-ttu-id="a4b87-175">На сервере vCenter роль — это предварительно определенный набор привилегий.</span><span class="sxs-lookup"><span data-stu-id="a4b87-175">On the vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="a4b87-176">Администратор сервера vCenter создает роли.</span><span class="sxs-lookup"><span data-stu-id="a4b87-176">A vCenter Server administrator creates the roles.</span></span> <span data-ttu-id="a4b87-177">Чтобы назначить разрешения,администратор связывает учетные записи пользователей с ролями.</span><span class="sxs-lookup"><span data-stu-id="a4b87-177">To assign permissions, the administrator pairs user accounts with a role.</span></span> <span data-ttu-id="a4b87-178">Чтобы настроить необходимые учетные данные пользователя для архивации компьютера сервера vCenter, создайте роль с определенными привилегиями и свяжите с ней учетную запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="a4b87-178">To establish the necessary user credentials to back up the vCenter Server computer, create a role with specific privileges, and then associate the user account with the role.</span></span>

<span data-ttu-id="a4b87-179">Сервер Azure Backup Server использует имя пользователя и пароль для аутентификации на сервере vCenter.</span><span class="sxs-lookup"><span data-stu-id="a4b87-179">Azure Backup Server uses a username and password to authenticate with the vCenter Server.</span></span> <span data-ttu-id="a4b87-180">Сервер резервного копирования Azure использует эти учетные данные пользователя для аутентификации всех операций архивации.</span><span class="sxs-lookup"><span data-stu-id="a4b87-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="a4b87-181">Вот как можно добавить роль сервера vCenter и привилегии для администратора архивации.</span><span class="sxs-lookup"><span data-stu-id="a4b87-181">To add a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="a4b87-182">Войдите на сервер vCenter, а затем в области **Navigator** (Навигатор) щелкните **Administration** (Администрирование).</span><span class="sxs-lookup"><span data-stu-id="a4b87-182">Sign in to the vCenter Server, and then in the vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![Параметр администрирования в области Navigator (Навигатор) на сервере vCenter](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="a4b87-184">В разделе **Administration** (Администрирование) выберите **Roles** (Роли), а затем в области **ролей** щелкните значок добавления роли (знак "+").</span><span class="sxs-lookup"><span data-stu-id="a4b87-184">In **Administration** select **Roles**, and then in the **Roles** panel click the add role icon (the + symbol).</span></span>

    ![Добавление роли](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="a4b87-186">Появится диалоговое окно **Create Role** (Создание роли).</span><span class="sxs-lookup"><span data-stu-id="a4b87-186">The **Create Role** dialog box appears.</span></span>

    ![Создание роли](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="a4b87-188">В диалоговом окне **Create Role** (Создание роли) в поле **Role name** (Имя роли) введите *BackupAdminRole*.</span><span class="sxs-lookup"><span data-stu-id="a4b87-188">In the **Create Role** dialog box, in the **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="a4b87-189">Это может быть любое имя, описывающее назначение этой роли.</span><span class="sxs-lookup"><span data-stu-id="a4b87-189">The role name can be whatever you like, but it should be recognizable for the role's purpose.</span></span>

4. <span data-ttu-id="a4b87-190">Выберите привилегии для соответствующей версии vCenter и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-190">Select the privileges for the appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="a4b87-191">В следующей таблице перечислены привилегии, необходимые для vCenter 6.0 и vCenter 5.5.</span><span class="sxs-lookup"><span data-stu-id="a4b87-191">The following table identifies the required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="a4b87-192">При выборе привилегий щелкните значок рядом с родительской меткой, чтобы раскрыть родительскую иерархию и просмотреть дочерние привилегии.</span><span class="sxs-lookup"><span data-stu-id="a4b87-192">When you select the privileges, click the icon next to the parent label to expand the parent and view the child privileges.</span></span> <span data-ttu-id="a4b87-193">Чтобы выбрать привилегии виртуальной машины, необходимо использовать несколько уровней иерархии родителей-потомков.</span><span class="sxs-lookup"><span data-stu-id="a4b87-193">To select the VirtualMachine privileges, you need to go several levels into the parent child hierarchy.</span></span> <span data-ttu-id="a4b87-194">Вам не нужно выбирать все дочерние привилегии, входящие в родительскую.</span><span class="sxs-lookup"><span data-stu-id="a4b87-194">You don't need to select all child privileges within a parent privilege.</span></span>

  ![Иерархия привилегий родителей-потомков](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="a4b87-196">После нажатия кнопки **OК** новая роль появится в списке в области ролей.</span><span class="sxs-lookup"><span data-stu-id="a4b87-196">After you click **OK**, the new role appears in the list on the Roles panel.</span></span>

|<span data-ttu-id="a4b87-197">Привилегии для vCenter 6.0</span><span class="sxs-lookup"><span data-stu-id="a4b87-197">Privileges for vCenter 6.0</span></span>| <span data-ttu-id="a4b87-198">Привилегии для vCenter 5.5</span><span class="sxs-lookup"><span data-stu-id="a4b87-198">Privileges for vCenter 5.5</span></span>|
|--------------------------|---------------------------|
|<span data-ttu-id="a4b87-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="a4b87-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="a4b87-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="a4b87-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="a4b87-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="a4b87-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="a4b87-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="a4b87-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="a4b87-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="a4b87-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="a4b87-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="a4b87-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="a4b87-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="a4b87-205">Network.Assign</span></span> |
|<span data-ttu-id="a4b87-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="a4b87-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="a4b87-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="a4b87-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="a4b87-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="a4b87-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="a4b87-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="a4b87-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="a4b87-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="a4b87-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="a4b87-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="a4b87-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="a4b87-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="a4b87-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="a4b87-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="a4b87-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="a4b87-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="a4b87-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="a4b87-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="a4b87-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="a4b87-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="a4b87-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="a4b87-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="a4b87-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="a4b87-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="a4b87-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="a4b87-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="a4b87-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="a4b87-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="a4b87-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="a4b87-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="a4b87-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="a4b87-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="a4b87-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="a4b87-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="a4b87-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="a4b87-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="a4b87-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="a4b87-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="a4b87-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="a4b87-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="a4b87-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="a4b87-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="a4b87-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="a4b87-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="a4b87-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="a4b87-229">Создание учетной записи пользователя сервера vCenter и разрешений</span><span class="sxs-lookup"><span data-stu-id="a4b87-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="a4b87-230">После настройки роли с привилегиями вы можете создать учетную запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="a4b87-230">After the role with privileges is set up, create a user account.</span></span> <span data-ttu-id="a4b87-231">Имя и пароль учетной записи пользователя являются учетными данными, используемыми для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="a4b87-231">The user account has a name and password, which provides the credentials that are used for authentication.</span></span>

1. <span data-ttu-id="a4b87-232">Чтобы создать учетную запись пользователя, на панели **Navigator** (Навигатор) на сервере vCenter щелкните **Users and Groups** (Пользователи и группы).</span><span class="sxs-lookup"><span data-stu-id="a4b87-232">To create a user account, in the vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![Пользователи и группы](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="a4b87-234">Появится панель **vCenter Users and Groups** (Пользователи и группы vCenter).</span><span class="sxs-lookup"><span data-stu-id="a4b87-234">The **vCenter Users and Groups** panel appears.</span></span>

    ![Панель vCenter Users and Groups (Пользователи и группы vCenter)](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="a4b87-236">На панели **vCenter Users and Groups** (Пользователи и группы vCenter) выберите вкладку **Users** (Пользователи), а затем щелкните значок добавления пользователей (знак "+").</span><span class="sxs-lookup"><span data-stu-id="a4b87-236">In the **vCenter Users and Groups** panel, select the **Users** tab, and then click the add users icon (the + symbol).</span></span>

    <span data-ttu-id="a4b87-237">Появится диалоговое окно **New User** (Новый пользователь).</span><span class="sxs-lookup"><span data-stu-id="a4b87-237">The **New User** dialog box appears.</span></span>

3. <span data-ttu-id="a4b87-238">В диалоговом окне **New User** (Новый пользователь) добавьте сведения о пользователе и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-238">In the **New User** dialog box, add the user's information and then click **OK**.</span></span> <span data-ttu-id="a4b87-239">В этой процедуре имя пользователя — BackupAdmin.</span><span class="sxs-lookup"><span data-stu-id="a4b87-239">In this procedure, the username is BackupAdmin.</span></span>

    ![Диалоговое окно New User (Новый пользователь)](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="a4b87-241">Новая учетная запись пользователя появится в списке.</span><span class="sxs-lookup"><span data-stu-id="a4b87-241">The new user account appears in the list.</span></span>

4. <span data-ttu-id="a4b87-242">Чтобы связать учетную запись пользователя с ролью, на панели **Navigator** (Навигатор) щелкните **Global Permissions** (Глобальные разрешения).</span><span class="sxs-lookup"><span data-stu-id="a4b87-242">To associate the user account with the role, in the **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="a4b87-243">На панели **Global Permissions** (Глобальные разрешения) выберите вкладку **Manage** (Управление), а затем щелкните значок добавления (знак "+").</span><span class="sxs-lookup"><span data-stu-id="a4b87-243">In the **Global Permissions** panel, select the **Manage** tab, and then click the add icon (the + symbol).</span></span>

    ![Панель Global Permissions (Глобальные разрешения)](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="a4b87-245">Появится диалоговое окно **корневой папки глобальных разрешений для добавления разрешения**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-245">The **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="a4b87-246">В диалоговом окне **корневой папки глобальных разрешений для добавления разрешения** щелкните **Add** (Добавить), чтобы выбрать пользователя или группу.</span><span class="sxs-lookup"><span data-stu-id="a4b87-246">In the **Global Permission Root - Add Permission** dialog box, click **Add** to choose the user or group.</span></span>

    ![Выбор пользователя или группы](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="a4b87-248">Появится диалоговое окно для **выбора пользователей или групп**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-248">The **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="a4b87-249">В диалоговом окне **выбора пользователей или групп** выберите **BackupAdmin**, а затем щелкните **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="a4b87-249">In the **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="a4b87-250">В разделе **Users** (Пользователи) для учетной записи пользователя используется формат *домен\имя пользователя*.</span><span class="sxs-lookup"><span data-stu-id="a4b87-250">In **Users**, the *domain\username* format is used for the user account.</span></span> <span data-ttu-id="a4b87-251">Если вы хотите использовать другой домен, выберите его из списка **доменов**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-251">If you want to use a different domain, choose it from the **Domain** list.</span></span>

    ![Добавление пользователя BackupAdmin](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="a4b87-253">Нажмите кнопку **ОК**, чтобы добавить выбранных пользователей в диалоговое окно **Add Permission** (Добавление разрешения).</span><span class="sxs-lookup"><span data-stu-id="a4b87-253">Click **OK** to add the selected users to the **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="a4b87-254">Теперь, когда вы определили пользователя, вы можете назначить его роли.</span><span class="sxs-lookup"><span data-stu-id="a4b87-254">Now that you've identified the user, assign the user to the role.</span></span> <span data-ttu-id="a4b87-255">В области **назначенной роли** в раскрывающемся меню выберите **BackupAdminRole** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-255">In **Assigned Role**, from the drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![Назначение пользователя роли](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="a4b87-257">На вкладке **Manage** (Управление) на панели **Global Permissions** (Глобальные разрешения) в списке появятся новая учетная запись пользователя и связанная роль.</span><span class="sxs-lookup"><span data-stu-id="a4b87-257">On the **Manage** tab in the **Global Permissions** panel, the new user account and the associated role appear in the list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="a4b87-258">Настройка учетных данных сервера vCenter на Сервере резервного копирования Azure</span><span class="sxs-lookup"><span data-stu-id="a4b87-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="a4b87-259">Прежде чем добавить сервер VMware на сервер Azure Backup Server, установите [обновление 1 для Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span><span class="sxs-lookup"><span data-stu-id="a4b87-259">Before you add the VMware server to Azure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="a4b87-260">Чтобы открыть Сервер резервного копирования Azure, дважды щелкните соответствующий значок на рабочем столе Сервера резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b87-260">To open Azure Backup Server, double-click the icon on the Azure Backup Server desktop.</span></span>

    ![Значок сервера резервного копирования Azure](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="a4b87-262">Если не удается найти значок на рабочем столе, откройте Сервер резервного копирования Azure из списка установленных приложений.</span><span class="sxs-lookup"><span data-stu-id="a4b87-262">If you can't find the icon on the desktop, open Azure Backup Server from the list of installed apps.</span></span> <span data-ttu-id="a4b87-263">Имя приложения сервера Azure Backup Server — Microsoft Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="a4b87-263">The Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="a4b87-264">На консоли сервера Azure Backup Server щелкните раздел **Управление**, затем выберите **Рабочие серверы** и на ленте инструментов щелкните **Управление VMware**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-264">In the Azure Backup Server console, click **Management**, click **Production Servers**, and then on the tool ribbon, click **Manage VMware**.</span></span>

    ![Консоль сервера Azure Backup Server](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="a4b87-266">Появится диалоговое окно **Управление учетными данными**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-266">The **Manage Credentials** dialog box appears.</span></span>

    ![Диалоговое окно управления учетными данными на сервере Azure Backup Server](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="a4b87-268">В диалоговом окне **управления учетными данными** нажмите кнопку **Добавить**, чтобы открыть диалоговое окно **добавления учетных данных**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-268">In the **Manage Credentials** dialog box, click **Add** to open the **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="a4b87-269">В диалоговом окне **добавления учетных данных** введите имя и описание для новых учетных данных.</span><span class="sxs-lookup"><span data-stu-id="a4b87-269">In the **Add Credential** dialog box, enter a name and a description for the new credential.</span></span> <span data-ttu-id="a4b87-270">Затем укажите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="a4b87-270">Then specify the username and password.</span></span> <span data-ttu-id="a4b87-271">Имя *Contoso Vcenter credential* используется для идентификации учетных данных в следующей процедуре.</span><span class="sxs-lookup"><span data-stu-id="a4b87-271">The name, *Contoso Vcenter credential* is used to identify the credential in the next procedure.</span></span> <span data-ttu-id="a4b87-272">Используйте те же имя пользователя и пароль, которые использовались для сервера vCenter.</span><span class="sxs-lookup"><span data-stu-id="a4b87-272">Use the same username and password that is used for the vCenter Server.</span></span> <span data-ttu-id="a4b87-273">Если сервер vCenter и сервер Azure Backup Server размещены в разных доменах, укажите домен в **имени пользователя**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-273">If the vCenter Server and Azure Backup Server are not in the same domain, in **User name**, specify the domain.</span></span>

    ![Диалоговое окно добавления учетных данных на сервере Azure Backup Server](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="a4b87-275">Нажмите кнопку **Добавить**, чтобы добавить новые учетные данные на сервер резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b87-275">Click **Add** to add the new credential to Azure Backup Server.</span></span> <span data-ttu-id="a4b87-276">Новые учетные данные появятся в списке диалогового окна **управления учетными данными**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-276">The new credential appears in the list in the **Manage Credentials** dialog box.</span></span>
    
    ![Диалоговое окно управления учетными данными на сервере Azure Backup Server](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="a4b87-278">Чтобы закрыть диалоговое окно **Управление учетными данными**, нажмите кнопку **X** в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="a4b87-278">To close the **Manage Credentials** dialog box, click the **X** in the upper-right corner.</span></span>


## <a name="add-the-vcenter-server-to-azure-backup-server"></a><span data-ttu-id="a4b87-279">Добавление сервера vCenter на Сервер резервного копирования Azure</span><span class="sxs-lookup"><span data-stu-id="a4b87-279">Add the vCenter Server to Azure Backup Server</span></span>

<span data-ttu-id="a4b87-280">Мастер добавления рабочего сервера используется для добавления сервера vCenter на сервер Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="a4b87-280">Production Server Addition Wizard is used to add the vCenter Server to Azure Backup Server.</span></span>

<span data-ttu-id="a4b87-281">Чтобы открыть мастер добавления рабочего сервера, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a4b87-281">To open Production Server Addition Wizard, complete the following procedure:</span></span>

1. <span data-ttu-id="a4b87-282">На консоли сервера Azure Backup Server щелкните раздел **Управление**, затем выберите **Рабочие серверы** и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-282">In the Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![Открытие мастера добавления рабочего сервера](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="a4b87-284">Появится диалоговое окно **мастера добавления рабочего сервера**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-284">The **Production Server Addition Wizard** dialog box appears.</span></span>

    ![Мастер добавления рабочего сервера](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="a4b87-286">На странице **выбора типа рабочего сервера** выберите **серверы VMware** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-286">On the **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="a4b87-287">В поле **имени или IP-адреса сервера** укажите полное доменное имя сервера VMware или его IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a4b87-287">In **Server Name/IP Address**, specify the fully qualified domain name (FQDN) or IP address of the VMware server.</span></span> <span data-ttu-id="a4b87-288">Если всеми серверами ESXi управляет один сервер vCenter, то вы можете ввести имя сервера vCenter.</span><span class="sxs-lookup"><span data-stu-id="a4b87-288">If all the ESXi servers are managed by the same vCenter, you can use the vCenter name.</span></span>

    ![Указание полного доменного имени или IP-адреса сервера VMware](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="a4b87-290">В поле **SSL-порт** введите порт, используемый для взаимодействия с сервером VMware.</span><span class="sxs-lookup"><span data-stu-id="a4b87-290">In **SSL Port**, enter the port that is used to communicate with the VMware server.</span></span> <span data-ttu-id="a4b87-291">Если вам не нужно вводить какой-то определенный порт, используйте порт 443, который является портом по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a4b87-291">Use port 443, which is the default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="a4b87-292">В поле **указания учетных данных** выберите созданные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="a4b87-292">In **Specify Credential**, select the credential that you created earlier.</span></span>

    ![Указание учетных данных](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="a4b87-294">Нажмите кнопку **Добавить**, чтобы добавить сервер VMware в список **добавленных серверов VMware**, а затем нажмите кнопку **Далее**, чтобы перейти к следующей странице мастера.</span><span class="sxs-lookup"><span data-stu-id="a4b87-294">Click **Add** to add the VMware server to the list of **Added VMware Servers**, and then click **Next** to move to the next page in the wizard.</span></span>

    ![Добавление сервера VMware и учетных данных](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="a4b87-296">На странице **сводки** нажмите кнопку **Добавить**, чтобы добавить указанный сервер VMware на сервер Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="a4b87-296">In the **Summary** page, click **Add** to add the specified VMware server to Azure Backup Server.</span></span>

    ![Добавление сервера VMware на сервер резервного копирования Azure](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="a4b87-298">Так как резервное копирование сервера VMware происходит без агента, новый сервер можно добавить за несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="a4b87-298">The VMware server backup is an agentless backup, and the new server is added immediately.</span></span> <span data-ttu-id="a4b87-299">На странице **окончания** будут показаны результаты.</span><span class="sxs-lookup"><span data-stu-id="a4b87-299">The **Finish** page shows you the results.</span></span>

  ![Страница "Готово"](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="a4b87-301">Чтобы добавить несколько экземпляров сервера vCenter на сервер Azure Backup Server, повторите предыдущие шаги в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="a4b87-301">To add multiple instances of vCenter Server to Azure Backup Server, repeat the previous steps in this section.</span></span>

<span data-ttu-id="a4b87-302">После добавления сервера vCenter на сервер Azure Backup Server следует создать группу защиты.</span><span class="sxs-lookup"><span data-stu-id="a4b87-302">After you add the vCenter Server to Azure Backup Server, the next step is to create a protection group.</span></span> <span data-ttu-id="a4b87-303">Группа защиты указывает различные детали для краткосрочного или долгосрочного хранения. В этой группе вы определяете и применяете политику архивации.</span><span class="sxs-lookup"><span data-stu-id="a4b87-303">The protection group specifies the various details for short or long-term retention, and it is where you define and apply the backup policy.</span></span> <span data-ttu-id="a4b87-304">С помощью политики архивации вы определяете, какие данные подлежат резервному копированию, а также когда оно будет происходить.</span><span class="sxs-lookup"><span data-stu-id="a4b87-304">The backup policy is the schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="a4b87-305">Настройка группы защиты</span><span class="sxs-lookup"><span data-stu-id="a4b87-305">Configure a protection group</span></span>

<span data-ttu-id="a4b87-306">Если вы прежде не использовали сервер Azure Backup Server или System Center Data Protection Manager, ознакомьтесь со статьей [Планирование резервного копирования на диски](https://technet.microsoft.com/library/hh758026.aspx), чтобы подготовить аппаратную среду.</span><span class="sxs-lookup"><span data-stu-id="a4b87-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) to prepare your hardware environment.</span></span> <span data-ttu-id="a4b87-307">Если у вас есть подходящее хранилище, используйте мастер создания групп защиты, чтобы добавить виртуальные машины VMware.</span><span class="sxs-lookup"><span data-stu-id="a4b87-307">After you check that you have proper storage, use the Create New Protection Group wizard to add VMware virtual machines.</span></span>

1. <span data-ttu-id="a4b87-308">На консоли сервера резервного копирования Azure щелкните раздел **Защита**, затем выберите на ленте инструментов **Создать**, чтобы открыть мастер создания групп защиты.</span><span class="sxs-lookup"><span data-stu-id="a4b87-308">In the Azure Backup Server console, click **Protection**, and in the tool ribbon, click **New** to open the Create New Protection Group wizard.</span></span>

    ![Открытие мастера создания групп защиты](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="a4b87-310">Появится диалоговое окно **мастера создания групп защиты**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-310">The **Create New Protection Group** wizard dialog box appears.</span></span>

    ![Диалоговое окно мастера создания групп защиты](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="a4b87-312">Нажмите кнопку **Далее**, чтобы перейти на страницу **Выбор типа группы защиты**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-312">Click **Next** to advance to the **Select protection group type** page.</span></span>

2. <span data-ttu-id="a4b87-313">На странице **Выбор типа группы защиты** выберите **Серверы** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-313">On the **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="a4b87-314">Появится страница **Выбор элементов группы**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-314">The **Select group members** page appears.</span></span>

3. <span data-ttu-id="a4b87-315">На странице **Выбор элементов группы** появятся доступные элементы и выбранные.</span><span class="sxs-lookup"><span data-stu-id="a4b87-315">On the **Select group members** page, the available members and the selected members appear.</span></span> <span data-ttu-id="a4b87-316">Выберите элементы, которые вы хотите защитить, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-316">Select the members that you want to protect, and then click **Next**.</span></span>

    ![Выберите членов группы](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="a4b87-318">Если при выборе элемента вы выберете папку, содержащую другие папки или виртуальные машины, эти элементы также будут выбраны.</span><span class="sxs-lookup"><span data-stu-id="a4b87-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="a4b87-319">Включение папок и виртуальных машин в родительскую папку называется защитой на уровне папки.</span><span class="sxs-lookup"><span data-stu-id="a4b87-319">The inclusion of the folders and VMs in the parent folder is called folder-level protection.</span></span> <span data-ttu-id="a4b87-320">Чтобы удалить папку или виртуальную машину, снимите флажок.</span><span class="sxs-lookup"><span data-stu-id="a4b87-320">To remove a folder or VM, clear the check box.</span></span>

    <span data-ttu-id="a4b87-321">Если виртуальная машина или папка, содержащая виртуальную машину, уже защищена в Azure, вы не сможете выбрать эту виртуальную машину снова.</span><span class="sxs-lookup"><span data-stu-id="a4b87-321">If a VM, or a folder containing a VM, is already protected to Azure, you cannot select that VM again.</span></span> <span data-ttu-id="a4b87-322">Таким образом, если виртуальная машина защищена в Azure, для нее нельзя включить повторную защиту, что предотвращает создание повторяющихся точек восстановления для одной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a4b87-322">That is, after a VM is protected to Azure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="a4b87-323">Если вы хотите увидеть, какой экземпляр Azure Backup Server уже защищает элемент, наведите указатель мыши на нужный элемент.</span><span class="sxs-lookup"><span data-stu-id="a4b87-323">If you want to see which Azure Backup Server instance already protects a member, point to the member to see the name of the protecting server.</span></span>

4. <span data-ttu-id="a4b87-324">На странице **Выбор метода защиты данных** введите имя для группы защиты.</span><span class="sxs-lookup"><span data-stu-id="a4b87-324">On the **Select Data Protection Method** page, enter a name for the protection group.</span></span> <span data-ttu-id="a4b87-325">Выбраны краткосрочная защита (на диск) и оперативная защита.</span><span class="sxs-lookup"><span data-stu-id="a4b87-325">Short-term protection (to disk) and online protection are selected.</span></span> <span data-ttu-id="a4b87-326">Если вы хотите использовать оперативную защиту (в Azure), необходимо использовать краткосрочную защиту на диск.</span><span class="sxs-lookup"><span data-stu-id="a4b87-326">If you want to use online protection (to Azure), you must use short-term protection to disk.</span></span> <span data-ttu-id="a4b87-327">Нажмите кнопку **Далее**, чтобы перейти к диапазону краткосрочной защиты.</span><span class="sxs-lookup"><span data-stu-id="a4b87-327">Click **Next** to proceed to the short-term protection range.</span></span>

    ![Выберите метод защиты данных](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="a4b87-329">На странице **указания краткосрочных целей** в **диапазоне хранения** укажите число дней, в течение которых необходимо хранить точки восстановления *на диске*.</span><span class="sxs-lookup"><span data-stu-id="a4b87-329">On the **Specify Short-Term Goals** page, for **Retention Range**, specify the number of days that you want to retain recovery points that are *stored to disk*.</span></span> <span data-ttu-id="a4b87-330">Чтобы изменить время и дни создания точек восстановления, нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-330">If you want to change the time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="a4b87-331">Точки восстановления краткосрочного хранения представляют собой полные резервные копии.</span><span class="sxs-lookup"><span data-stu-id="a4b87-331">The short-term recovery points are full backups.</span></span> <span data-ttu-id="a4b87-332">Для них не выполняется добавочное резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="a4b87-332">They are not incremental backups.</span></span> <span data-ttu-id="a4b87-333">Если вы задали необходимые параметры для краткосрочных целей, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-333">When you are satisfied with the short-term goals, click **Next**.</span></span>

    ![Выберите краткосрочные цели](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="a4b87-335">На странице **проверки выделения места на диске** просмотрите объем места на диске для виртуальных машин и при необходимости измените его.</span><span class="sxs-lookup"><span data-stu-id="a4b87-335">On the **Review Disk Allocation** page, review and if necessary, modify the disk space for the VMs.</span></span> <span data-ttu-id="a4b87-336">Рекомендуемые выделения дискового пространства основаны на диапазоне хранения, указанном на **предыдущей** странице, типе рабочей нагрузки и размере защищенных данных (определенных на шаге 3).</span><span class="sxs-lookup"><span data-stu-id="a4b87-336">The recommended disk allocations are based on the retention range that is specified in the **Specify Short-Term Goals** page, the type of workload, and the size of the protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="a4b87-337">**Размер данных** — размер данных в группе защиты.</span><span class="sxs-lookup"><span data-stu-id="a4b87-337">**Data size:** Size of the data in the protection group.</span></span>
  - <span data-ttu-id="a4b87-338">**Место на диске** — рекомендуемый объем дискового пространства для группы защиты.</span><span class="sxs-lookup"><span data-stu-id="a4b87-338">**Disk space:** The recommended amount of disk space for the protection group.</span></span> <span data-ttu-id="a4b87-339">Если вы хотите изменить этот параметр, вы должны выделить общее место, объем которого будет немного превышать рассчитанный вами объем для каждого источника данных.</span><span class="sxs-lookup"><span data-stu-id="a4b87-339">If you want to modify this setting, you should allocate total space that is slightly larger than the amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="a4b87-340">**Совместное размещение данных** — если вы включите совместное размещение, несколько источников данных в защите могут сопоставиться с отдельной репликой и томом точек восстановления.</span><span class="sxs-lookup"><span data-stu-id="a4b87-340">**Colocate data:** If you turn on colocation, multiple data sources in the protection can map to a single replica and recovery point volume.</span></span> <span data-ttu-id="a4b87-341">Совместное размещение поддерживается не для всех рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="a4b87-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="a4b87-342">**Автоматическое увеличение** — если вы включите этот параметр, то в случае, когда объем данных в защищенной группе превысит первоначальный выделенный объем, System Center Data Protection Manager попытается увеличить размер диска на 25 %.</span><span class="sxs-lookup"><span data-stu-id="a4b87-342">**Automatically grow:** If you turn on this setting, if data in the protected group outgrows the initial allocation, System Center Data Protection Manager tries to increase the disk size by 25 percent.</span></span>
  - <span data-ttu-id="a4b87-343">**Дополнительные сведения о пуле носителей** — этот параметр отображает состояние пула носителей, включая общий размер диска и оставшийся.</span><span class="sxs-lookup"><span data-stu-id="a4b87-343">**Storage pool details:** Shows the status of the storage pool, including total and remaining disk size.</span></span>

    ![Просмотр выделения дискового пространства](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="a4b87-345">Если вас устраивает выделенное пространство, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-345">When you are satisfied with the space allocation, click **Next**.</span></span>

7. <span data-ttu-id="a4b87-346">На странице **Выбор метода создания реплики** укажите, каким образом нужно создавать начальную копию или реплику защищенных данных на сервере Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="a4b87-346">On the **Choose Replica Creation Method** page, specify how you want to generate the initial copy, or replica, of the protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="a4b87-347">Значения по умолчанию — **Автоматически по сети** и **Сейчас**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-347">The default is **Automatically over the network** and **Now**.</span></span> <span data-ttu-id="a4b87-348">Если вы используете значения по умолчанию, укажите время низкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="a4b87-348">If you use the default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="a4b87-349">Выберите параметр **Позже** и укажите день и время.</span><span class="sxs-lookup"><span data-stu-id="a4b87-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="a4b87-350">Для больших объемов данных или неоптимальных условий сети лучше выбрать автономную репликацию данных с использованием съемных носителей.</span><span class="sxs-lookup"><span data-stu-id="a4b87-350">For large amounts of data or less-than-optimal network conditions, consider replicating the data offline by using removable media.</span></span>

    <span data-ttu-id="a4b87-351">Задав параметры по своему усмотрению, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-351">After you have made your choices, click **Next**.</span></span>

    ![Выберите метод создания реплики](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="a4b87-353">На странице **Параметры проверки согласованности** выберите способ проверок на согласованность и время их автоматизации.</span><span class="sxs-lookup"><span data-stu-id="a4b87-353">On the **Consistency Check Options** page, select how and when to automate the consistency checks.</span></span> <span data-ttu-id="a4b87-354">В случае несогласованности данных реплики вы можете запустить проверку на согласованность, либо эта проверка может выполняться по расписанию.</span><span class="sxs-lookup"><span data-stu-id="a4b87-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="a4b87-355">Если настраивать автоматическую проверку согласованности не требуется, можно выполнить проверку вручную.</span><span class="sxs-lookup"><span data-stu-id="a4b87-355">If you don't want to configure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="a4b87-356">В области защиты консоли сервера Azure Backup Server щелкните правой кнопкой мыши группу защиты и выберите **Выполнить проверку согласованности**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-356">In the protection area of the Azure Backup Server console, right-click the protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="a4b87-357">Чтобы перейти к следующей странице, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-357">Click **Next** to move to the next page.</span></span>

9. <span data-ttu-id="a4b87-358">На странице **Указание данных для оперативной защиты** выберите один или несколько источников данных, которые необходимо защитить.</span><span class="sxs-lookup"><span data-stu-id="a4b87-358">On the **Specify Online Protection Data** page, select one or more data sources that you want to protect.</span></span> <span data-ttu-id="a4b87-359">Вы можете выбрать элементы по отдельности или же щелкнуть **Выделить все**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-359">You can select the members individually, or click **Select All** to choose all members.</span></span> <span data-ttu-id="a4b87-360">Выбрав необходимые элементы, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-360">After you choose the members, click **Next**.</span></span>

    ![Выбор оперативной защиты данных](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="a4b87-362">На странице **Укажите расписание архивации в сети** укажите расписание для создания точек восстановления из резервной копии диска.</span><span class="sxs-lookup"><span data-stu-id="a4b87-362">On the **Specify Online Backup Schedule** page, specify the schedule to generate recovery points from the disk backup.</span></span> <span data-ttu-id="a4b87-363">Созданная точка восстановления передается в хранилище служб восстановления в Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b87-363">After the recovery point is generated, it is transferred to the Recovery Services vault in Azure.</span></span> <span data-ttu-id="a4b87-364">Когда вы зададите параметры расписания оперативного резервного копирования, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-364">When you are satisfied with the online backup schedule, click **Next**.</span></span>

    ![Выбор расписания оперативного резервного копирования](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="a4b87-366">На странице **Укажите политику хранения в сети** укажите необходимое время хранения резервных копий данных в Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b87-366">On the **Specify Online Retention Policy** page, indicate how long you want to retain the backup data in Azure.</span></span> <span data-ttu-id="a4b87-367">После определения политики нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-367">After the policy is defined, click **Next**.</span></span>

    ![Выбор политики оперативного хранения](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="a4b87-369">Временных ограничений для хранения данных в Azure нет.</span><span class="sxs-lookup"><span data-stu-id="a4b87-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="a4b87-370">Если вы храните данные точек восстановления в Azure, единственным ограничением является количество точек восстановления — не более 9999 на защищенный экземпляр.</span><span class="sxs-lookup"><span data-stu-id="a4b87-370">When you store recovery point data in Azure, the only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="a4b87-371">В этом примере защищенным экземпляром является сервер VMware.</span><span class="sxs-lookup"><span data-stu-id="a4b87-371">In this example, the protected instance is the VMware server.</span></span>

12. <span data-ttu-id="a4b87-372">На странице **сводки** просмотрите подробные сведения для элементов группы защиты и параметры, а затем нажмите кнопку **Создать группу**.</span><span class="sxs-lookup"><span data-stu-id="a4b87-372">On the **Summary** page, review the details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![Сводка параметров и элементов группы защиты](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="a4b87-374">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a4b87-374">Next steps</span></span>
<span data-ttu-id="a4b87-375">Если вы используете сервер Azure Backup Server для защиты рабочих нагрузок VMware, попробуйте использовать этот сервер для защиты [Microsoft Exchange Server](./backup-azure-exchange-mabs.md), [фермы Microsoft SharePoint](./backup-azure-backup-sharepoint-mabs.md) или [базы данных SQL Server](./backup-azure-sql-mabs.md).</span><span class="sxs-lookup"><span data-stu-id="a4b87-375">If you use Azure Backup Server to protect VMware workloads, you may be interested in using Azure Backup Server to help protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="a4b87-376">Дополнительные сведения о проблемах с регистрацией агента, настройкой группы защиты и заданиями резервного копирования см. в статье [Устранение неполадок на сервере резервного копирования Azure](./backup-azure-mabs-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="a4b87-376">For information on problems with registering the agent, configuring the protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>
