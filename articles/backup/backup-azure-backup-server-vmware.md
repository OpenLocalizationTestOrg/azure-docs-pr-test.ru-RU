---
title: "aaaBack серверов VMware с Azure Backup Server | Документы Microsoft"
description: "Используйте резервное копирование Azure tooback tooAzure VMware vCenter/ESXi серверов или диска. В этой статье приведены пошаговые инструкции для резервного копирования (или защиты) рабочих нагрузок VMware."
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
ms.openlocfilehash: 3edb6880a526ed0b18605fee0fac27196a608e7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-vmware-server-tooazure"></a><span data-ttu-id="e59f1-104">Резервное копирование сервера VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="e59f1-104">Back up a VMware server tooAzure</span></span>

<span data-ttu-id="e59f1-105">В этой статье объясняется, как резервное копирование Azure toohelp tooconfigure защитить рабочие нагрузки сервера VMware.</span><span class="sxs-lookup"><span data-stu-id="e59f1-105">This article explains how tooconfigure Azure Backup Server toohelp protect VMware server workloads.</span></span> <span data-ttu-id="e59f1-106">Чтобы приступить к работе с этим руководством, вам необходимо установить сервер резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="e59f1-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="e59f1-107">Если у вас нет Azure Backup Server установлены, см. раздел [Подготовка tooback копирование рабочих нагрузок, использующих Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="e59f1-107">If you don't have Azure Backup Server installed, see [Prepare tooback up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="e59f1-108">Azure Backup Server обеспечивает резервное копирование (или защиту) серверов VMware vCenter версий 6.5, 6.0 и 5.5.</span><span class="sxs-lookup"><span data-stu-id="e59f1-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-toohello-vcenter-server"></a><span data-ttu-id="e59f1-109">Создать безопасное подключение toohello vCenter Server</span><span class="sxs-lookup"><span data-stu-id="e59f1-109">Create a secure connection toohello vCenter Server</span></span>

<span data-ttu-id="e59f1-110">По умолчанию Azure Backup Server взаимодействует с каждым сервером vCenter через канал HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e59f1-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="e59f1-111">tooturn на hello безопасного взаимодействия рекомендуется устанавливать hello VMware центра сертификации (ЦС) сертификата на сервер резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="e59f1-111">tooturn on hello secure communication, we recommend that you install hello VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="e59f1-112">Если не требуется безопасное соединение и предпочитаете toodisable hello обязательное использование протокола HTTPS, см. раздел [отключение безопасного взаимодействия протокола](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span><span class="sxs-lookup"><span data-stu-id="e59f1-112">If you don't require secure communication, and would prefer toodisable hello HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="e59f1-113">toocreate безопасное подключение между сервером резервного копирования Azure и hello vCenter Server, импортируйте hello доверенных сертификатов на сервере резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="e59f1-113">toocreate a secure connection between Azure Backup Server and hello vCenter Server, import hello trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="e59f1-114">Как правило используется браузер на vCenter toohello tooconnect Azure Backup Server машины hello Server через vSphere hello веб-клиента.</span><span class="sxs-lookup"><span data-stu-id="e59f1-114">Typically, you use a browser on hello Azure Backup Server machine tooconnect toohello vCenter Server via hello vSphere Web Client.</span></span> <span data-ttu-id="e59f1-115">Hello при первом обращении hello Azure Backup Server браузера tooconnect toohello vCenter Server, подключение hello не защищены.</span><span class="sxs-lookup"><span data-stu-id="e59f1-115">hello first time you use hello Azure Backup Server browser tooconnect toohello vCenter Server, hello connection isn't secure.</span></span> <span data-ttu-id="e59f1-116">Следующие изображения Hello демонстрирует подключение hello незащищенным.</span><span class="sxs-lookup"><span data-stu-id="e59f1-116">hello following image shows hello unsecured connection.</span></span>

![Пример сервера tooVMware небезопасное подключение](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="e59f1-118">toofix эту проблему и создать безопасное соединение, загрузка hello доверенных корневых сертификатов.</span><span class="sxs-lookup"><span data-stu-id="e59f1-118">toofix this issue, and create a secure connection, download hello trusted root CA certificates.</span></span>

1. <span data-ttu-id="e59f1-119">В браузере hello на сервер резервного копирования Azure введите vSphere toohello hello URL-адрес веб-клиента.</span><span class="sxs-lookup"><span data-stu-id="e59f1-119">In hello browser on Azure Backup Server, enter hello URL toohello vSphere Web Client.</span></span> <span data-ttu-id="e59f1-120">отображается страница входа веб-клиент vSphere Hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-120">hello vSphere Web Client login page appears.</span></span>

    ![Веб-клиент vSphere](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="e59f1-122">Внизу hello hello сведения для администраторов и разработчиков, найдите hello **загрузки корневые сертификаты доверенного ЦС** ссылку.</span><span class="sxs-lookup"><span data-stu-id="e59f1-122">At hello bottom of hello information for administrators and developers, locate hello **Download trusted root CA certificates** link.</span></span>

    ![Ссылка toodownload hello доверенных корневых сертификатов](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="e59f1-124">Если вы не видите страницу входа веб-клиент vSphere hello, проверьте параметры прокси-сервера в браузере.</span><span class="sxs-lookup"><span data-stu-id="e59f1-124">If you don't see hello vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="e59f1-125">Щелкните **Download trusted root CA certificates** (Скачать сертификаты доверенного корневого ЦС).</span><span class="sxs-lookup"><span data-stu-id="e59f1-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="e59f1-126">Hello vCenter Server загружает файл tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="e59f1-126">hello vCenter Server downloads a file tooyour local computer.</span></span> <span data-ttu-id="e59f1-127">Hello имя файла называется **загрузить**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-127">hello file's name is named **download**.</span></span> <span data-ttu-id="e59f1-128">В зависимости от браузера, появится сообщение с запросом, является ли tooopen или сохранение файла hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-128">Depending on your browser, you receive a message that asks whether tooopen or save hello file.</span></span>

    ![Сообщение после скачивания сертификатов](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="e59f1-130">Hello файл tooa расположение для сохранения на сервере резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="e59f1-130">Save hello file tooa location on Azure Backup Server.</span></span> <span data-ttu-id="e59f1-131">При сохранении файла hello добавьте расширение имени файла .zip hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-131">When you save hello file, add hello .zip file name extension.</span></span>

    <span data-ttu-id="e59f1-132">Hello файл является ZIP-файл, содержащий hello сведения о сертификатах hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-132">hello file is a .zip file that contains hello information about hello certificates.</span></span> <span data-ttu-id="e59f1-133">С расширением .zip hello можно использовать средства извлечения hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-133">With hello .zip extension, you can use hello extraction tools.</span></span>

4. <span data-ttu-id="e59f1-134">Щелкните правой кнопкой мыши **download.zip**, а затем выберите **извлечь все** tooextract hello содержимое.</span><span class="sxs-lookup"><span data-stu-id="e59f1-134">Right-click **download.zip**, and then select **Extract All** tooextract hello contents.</span></span>

    <span data-ttu-id="e59f1-135">ZIP-файл Hello извлекает его содержимое tooa папка **сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-135">hello .zip file extracts its contents tooa folder named **certs**.</span></span> <span data-ttu-id="e59f1-136">Два типа файлов отображаются в папке сертификатов hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-136">Two types of files appear in hello certs folder.</span></span> <span data-ttu-id="e59f1-137">файл корневого сертификата Hello имеет расширение, которое начинается с номером последовательности как.0 и.1.</span><span class="sxs-lookup"><span data-stu-id="e59f1-137">hello root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="e59f1-138">файл списка отзыва Сертификатов Hello имеет расширение, которое начинается с последовательности как .r0 или .r1.</span><span class="sxs-lookup"><span data-stu-id="e59f1-138">hello CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="e59f1-139">файл списка отзыва Сертификатов Hello связан с сертификатом.</span><span class="sxs-lookup"><span data-stu-id="e59f1-139">hello CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="e59f1-140">Извлечение скачанного файла на локальный компьютер</span><span class="sxs-lookup"><span data-stu-id="e59f1-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="e59f1-141">В hello **сертификатов** папку, щелкните правой кнопкой мыши файл hello корневого сертификата и нажмите кнопку **переименование**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-141">In hello **certs** folder, right-click hello root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="e59f1-142">Переименование корневого сертификата</span><span class="sxs-lookup"><span data-stu-id="e59f1-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="e59f1-143">Измените расширение too.crt hello корневой сертификат.</span><span class="sxs-lookup"><span data-stu-id="e59f1-143">Change hello root certificate's extension too.crt.</span></span> <span data-ttu-id="e59f1-144">В ответ на запрос, если Вы действительно хотите toochange hello расширение, нажмите кнопку **Да** или **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-144">When you're asked if you're sure you want toochange hello extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="e59f1-145">В противном случае изменении функции hello файла.</span><span class="sxs-lookup"><span data-stu-id="e59f1-145">Otherwise, you change hello file's intended function.</span></span> <span data-ttu-id="e59f1-146">значок Hello hello изменения файла tooan значок, представляющий корневой сертификат.</span><span class="sxs-lookup"><span data-stu-id="e59f1-146">hello icon for hello file changes tooan icon that represents a root certificate.</span></span>

6. <span data-ttu-id="e59f1-147">Щелкните правой кнопкой мыши корневой сертификат hello и hello во всплывающем меню, выберите **установить сертификат**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-147">Right-click hello root certificate and from hello pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="e59f1-148">Hello **мастер импорта сертификатов** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="e59f1-148">hello **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="e59f1-149">В hello **мастер импорта сертификатов** выберите **локального компьютера** назначения hello hello сертификат, а затем нажмите кнопку **Далее** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="e59f1-149">In hello **Certificate Import Wizard** dialog box, select **Local Machine** as hello destination for hello certificate, and then click **Next** toocontinue.</span></span>

    ![<span data-ttu-id="e59f1-150">Параметры назначения хранилища сертификатов</span><span class="sxs-lookup"><span data-stu-id="e59f1-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="e59f1-151">В ответ на вопрос, следует ли компьютер toohello tooallow изменения, нажмите кнопку **Да** или **ОК**, tooall hello изменения.</span><span class="sxs-lookup"><span data-stu-id="e59f1-151">If you're asked if you want tooallow changes toohello computer, click **Yes** or **OK**, tooall hello changes.</span></span>

8. <span data-ttu-id="e59f1-152">На hello **хранилище сертификатов** выберите **поместить все сертификаты в следующие хранилища hello**, а затем нажмите кнопку **Обзор** хранилище сертификатов toochoose hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-152">On hello **Certificate Store** page, select **Place all certificates in hello following store**, and then click **Browse** toochoose hello certificate store.</span></span>

    ![Размещение сертификатов в определенном месте в хранилище](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="e59f1-154">Hello **Выбор хранилища сертификата** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="e59f1-154">hello **Select Certificate Store** dialog box appears.</span></span>

    ![Иерархия папки хранилища сертификатов](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="e59f1-156">Выберите **доверенные корневые центры сертификации** как hello конечную папку для hello сертификатов, а затем щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-156">Select **Trusted Root Certification Authorities** as hello destination folder for hello certificates, and then click **OK**.</span></span>

    ![Папка назначения для сертификата](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="e59f1-158">Hello **доверенные корневые центры сертификации** папку подтверждено как хранилище сертификатов hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-158">hello **Trusted Root Certification Authorities** folder is confirmed as hello certificate store.</span></span> <span data-ttu-id="e59f1-159">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-159">Click **Next**.</span></span>

    ![Папка хранилища сертификатов](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="e59f1-161">На hello **hello завершение работы мастера импорта сертификатов** , убедитесь, что hello сертификат находится в нужной папке hello и выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-161">On hello **Completing hello Certificate Import Wizard** page, verify that hello certificate is in hello desired folder, and then click **Finish**.</span></span>

    ![Убедитесь, что сертификат находится в соответствующей папке hello](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="e59f1-163">Появится диалоговое окно, hello импорта сертификатов успешно подтверждена.</span><span class="sxs-lookup"><span data-stu-id="e59f1-163">A dialog box appears, hello successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="e59f1-164">Войдите в систему toohello vCenter Server tooconfirm, что соединение является безопасным.</span><span class="sxs-lookup"><span data-stu-id="e59f1-164">Sign in toohello vCenter Server tooconfirm that your connection is secure.</span></span>

  <span data-ttu-id="e59f1-165">Если не удается установить безопасное соединение hello Импорт сертификата не выполнена успешно, в документации hello VMware vSphere на [получение сертификатов сервера](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span><span class="sxs-lookup"><span data-stu-id="e59f1-165">If hello certificate import is not successful, and you cannot establish a secure connection, consult hello VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="e59f1-166">Если имеется области безопасности вашей организации и не требуется tooturn на hello протокола HTTPS, используйте hello, выполнив процедуру toodisable hello безопасных соединений.</span><span class="sxs-lookup"><span data-stu-id="e59f1-166">If you have secure boundaries within your organization, and don't want tooturn on hello HTTPS protocol, use hello following procedure toodisable hello secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="e59f1-167">Отключение протокола безопасной связи</span><span class="sxs-lookup"><span data-stu-id="e59f1-167">Disable secure communication protocol</span></span>

<span data-ttu-id="e59f1-168">Если ваша организация не требует протокол HTTPS hello, используйте следующие шаги toodisable HTTPS hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-168">If your organization doesn't require hello HTTPS protocol, use hello following steps toodisable HTTPS.</span></span> <span data-ttu-id="e59f1-169">toodisable hello поведение по умолчанию, создайте раздел реестра, который пропускает поведение по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-169">toodisable hello default behavior, create a registry key that ignores hello default behavior.</span></span>

1. <span data-ttu-id="e59f1-170">Скопируйте и вставьте следующий текст в файл hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-170">Copy and paste hello following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="e59f1-171">Сохраните hello файл tooyour Azure Backup Server компьютера.</span><span class="sxs-lookup"><span data-stu-id="e59f1-171">Save hello file tooyour Azure Backup Server computer.</span></span> <span data-ttu-id="e59f1-172">Для имени файла hello используйте DisableSecureAuthentication.reg.</span><span class="sxs-lookup"><span data-stu-id="e59f1-172">For hello file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="e59f1-173">Дважды щелкните запись реестра hello tooactivate файла hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-173">Double-click hello file tooactivate hello registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a><span data-ttu-id="e59f1-174">Создать роли и учетной записи для hello vCenter Server</span><span class="sxs-lookup"><span data-stu-id="e59f1-174">Create a role and user account on hello vCenter Server</span></span>

<span data-ttu-id="e59f1-175">На сервере vCenter hello роль — это стандартный набор привилегий.</span><span class="sxs-lookup"><span data-stu-id="e59f1-175">On hello vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="e59f1-176">Администратор сервера vCenter создаются роли hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-176">A vCenter Server administrator creates hello roles.</span></span> <span data-ttu-id="e59f1-177">разрешения tooassign Здравствуйте, администратор пар учетных записей пользователей с ролью.</span><span class="sxs-lookup"><span data-stu-id="e59f1-177">tooassign permissions, hello administrator pairs user accounts with a role.</span></span> <span data-ttu-id="e59f1-178">tooback tooestablish hello пользователя необходимые учетные данные компьютера сервера vCenter hello, создать роль с определенными правами доступа и затем связать hello учетная запись пользователя с ролью hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-178">tooestablish hello necessary user credentials tooback up hello vCenter Server computer, create a role with specific privileges, and then associate hello user account with hello role.</span></span>

<span data-ttu-id="e59f1-179">Сервер резервного копирования Azure использует имя пользователя и пароль tooauthenticate с hello vCenter Server.</span><span class="sxs-lookup"><span data-stu-id="e59f1-179">Azure Backup Server uses a username and password tooauthenticate with hello vCenter Server.</span></span> <span data-ttu-id="e59f1-180">Сервер резервного копирования Azure использует эти учетные данные пользователя для аутентификации всех операций архивации.</span><span class="sxs-lookup"><span data-stu-id="e59f1-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="e59f1-181">tooadd vCenter роли сервера и соответствующие права для администратора резервного копирования:</span><span class="sxs-lookup"><span data-stu-id="e59f1-181">tooadd a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="e59f1-182">Войдите в toohello vCenter Server, а затем в hello vCenter Server **Навигатор** нажмите кнопку **администрирования**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-182">Sign in toohello vCenter Server, and then in hello vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![Параметр администрирования в области Navigator (Навигатор) на сервере vCenter](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="e59f1-184">В **администрирования** выберите **ролей**, а затем в hello **ролей** щелкните панель hello добавить значок роли ("Здравствуйте," + "символ").</span><span class="sxs-lookup"><span data-stu-id="e59f1-184">In **Administration** select **Roles**, and then in hello **Roles** panel click hello add role icon (hello + symbol).</span></span>

    ![Добавление роли](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="e59f1-186">Hello **Create Role** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="e59f1-186">hello **Create Role** dialog box appears.</span></span>

    ![Создание роли](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="e59f1-188">В hello **Create Role** диалогового окна hello **имя роли** введите *BackupAdminRole*.</span><span class="sxs-lookup"><span data-stu-id="e59f1-188">In hello **Create Role** dialog box, in hello **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="e59f1-189">Имя роли Hello может быть любым, но должны распознаваться для цели hello роли.</span><span class="sxs-lookup"><span data-stu-id="e59f1-189">hello role name can be whatever you like, but it should be recognizable for hello role's purpose.</span></span>

4. <span data-ttu-id="e59f1-190">Выберите hello права доступа для соответствующей версии vCenter hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-190">Select hello privileges for hello appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="e59f1-191">Привет, в следующей таблице идентифицирует hello необходимые привилегии для vCenter 6.0 и vCenter 5.5.</span><span class="sxs-lookup"><span data-stu-id="e59f1-191">hello following table identifies hello required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="e59f1-192">При выборе привилегии hello щелкните hello значок Далее toohello родительской метки tooexpand hello родительского представления hello дочерних правами доступа и.</span><span class="sxs-lookup"><span data-stu-id="e59f1-192">When you select hello privileges, click hello icon next toohello parent label tooexpand hello parent and view hello child privileges.</span></span> <span data-ttu-id="e59f1-193">tooselect hello VirtualMachine права доступа, необходимые toogo несколько уровней в hello родительская иерархия дочерних.</span><span class="sxs-lookup"><span data-stu-id="e59f1-193">tooselect hello VirtualMachine privileges, you need toogo several levels into hello parent child hierarchy.</span></span> <span data-ttu-id="e59f1-194">Не нужно tooselect все дочерние привилегий в пределах родительского права доступа.</span><span class="sxs-lookup"><span data-stu-id="e59f1-194">You don't need tooselect all child privileges within a parent privilege.</span></span>

  ![Иерархия привилегий родителей-потомков](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="e59f1-196">После нажатия кнопки **ОК**, появится новая роль hello в списке hello на панели ролей hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-196">After you click **OK**, hello new role appears in hello list on hello Roles panel.</span></span>

|<span data-ttu-id="e59f1-197">Привилегии для vCenter 6.0</span><span class="sxs-lookup"><span data-stu-id="e59f1-197">Privileges for vCenter 6.0</span></span>| <span data-ttu-id="e59f1-198">Привилегии для vCenter 5.5</span><span class="sxs-lookup"><span data-stu-id="e59f1-198">Privileges for vCenter 5.5</span></span>|
|--------------------------|---------------------------|
|<span data-ttu-id="e59f1-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="e59f1-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="e59f1-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="e59f1-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="e59f1-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="e59f1-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="e59f1-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="e59f1-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="e59f1-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="e59f1-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="e59f1-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="e59f1-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="e59f1-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="e59f1-205">Network.Assign</span></span> |
|<span data-ttu-id="e59f1-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="e59f1-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="e59f1-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="e59f1-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="e59f1-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="e59f1-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="e59f1-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="e59f1-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="e59f1-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="e59f1-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="e59f1-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="e59f1-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="e59f1-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="e59f1-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="e59f1-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="e59f1-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="e59f1-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="e59f1-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="e59f1-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="e59f1-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="e59f1-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="e59f1-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="e59f1-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="e59f1-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="e59f1-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="e59f1-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="e59f1-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="e59f1-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="e59f1-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="e59f1-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="e59f1-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="e59f1-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="e59f1-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="e59f1-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="e59f1-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="e59f1-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="e59f1-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="e59f1-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="e59f1-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="e59f1-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="e59f1-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="e59f1-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="e59f1-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="e59f1-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="e59f1-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="e59f1-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="e59f1-229">Создание учетной записи пользователя сервера vCenter и разрешений</span><span class="sxs-lookup"><span data-stu-id="e59f1-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="e59f1-230">После настройки hello роли с правами, создайте учетную запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="e59f1-230">After hello role with privileges is set up, create a user account.</span></span> <span data-ttu-id="e59f1-231">Hello учетная запись имеет имя и пароль, который предоставляет hello учетные данные, используемые для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e59f1-231">hello user account has a name and password, which provides hello credentials that are used for authentication.</span></span>

1. <span data-ttu-id="e59f1-232">учетной записи пользователя в hello vCenter Server toocreate **Навигатор** нажмите кнопку **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-232">toocreate a user account, in hello vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![Пользователи и группы](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="e59f1-234">Hello **vCenter пользователей и групп** появится панель.</span><span class="sxs-lookup"><span data-stu-id="e59f1-234">hello **vCenter Users and Groups** panel appears.</span></span>

    ![Панель vCenter Users and Groups (Пользователи и группы vCenter)](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="e59f1-236">В hello **vCenter пользователей и групп** панель, выберите hello **пользователей** , а затем щелкните hello добавить значок пользователей ("Здравствуйте," + "символ").</span><span class="sxs-lookup"><span data-stu-id="e59f1-236">In hello **vCenter Users and Groups** panel, select hello **Users** tab, and then click hello add users icon (hello + symbol).</span></span>

    <span data-ttu-id="e59f1-237">Hello **нового пользователя** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="e59f1-237">hello **New User** dialog box appears.</span></span>

3. <span data-ttu-id="e59f1-238">В hello **нового пользователя** диалоговое окно добавления сведений о пользователе hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-238">In hello **New User** dialog box, add hello user's information and then click **OK**.</span></span> <span data-ttu-id="e59f1-239">В этой процедуре hello пользователя является BackupAdmin.</span><span class="sxs-lookup"><span data-stu-id="e59f1-239">In this procedure, hello username is BackupAdmin.</span></span>

    ![Диалоговое окно New User (Новый пользователь)](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="e59f1-241">Hello новой учетной записи пользователя отображается в списке hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-241">hello new user account appears in hello list.</span></span>

4. <span data-ttu-id="e59f1-242">Учетная запись пользователя hello tooassociate с роли hello в hello **Навигатор** нажмите кнопку **глобальные разрешения**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-242">tooassociate hello user account with hello role, in hello **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="e59f1-243">В hello **глобальные разрешения** панель, выберите hello **управление** , а затем щелкните hello добавить значок ("Здравствуйте," + "символ").</span><span class="sxs-lookup"><span data-stu-id="e59f1-243">In hello **Global Permissions** panel, select hello **Manage** tab, and then click hello add icon (hello + symbol).</span></span>

    ![Панель Global Permissions (Глобальные разрешения)](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="e59f1-245">Hello **глобальные разрешения Root - добавить разрешение** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="e59f1-245">hello **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="e59f1-246">В hello **глобальных разрешений Root - добавить разрешение** диалоговое окно, нажмите кнопку **добавить** toochoose hello пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="e59f1-246">In hello **Global Permission Root - Add Permission** dialog box, click **Add** toochoose hello user or group.</span></span>

    ![Выбор пользователя или группы](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="e59f1-248">Hello **выберите пользователей или группы** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="e59f1-248">hello **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="e59f1-249">В hello **выберите пользователей или группы** диалогового окна выберите **BackupAdmin** и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-249">In hello **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="e59f1-250">В **пользователей**, hello *домен\имя_пользователя* формат используется для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-250">In **Users**, hello *domain\username* format is used for hello user account.</span></span> <span data-ttu-id="e59f1-251">Если вы хотите toouse другого домена, выберите его из hello **домена** списка.</span><span class="sxs-lookup"><span data-stu-id="e59f1-251">If you want toouse a different domain, choose it from hello **Domain** list.</span></span>

    ![Добавление пользователя BackupAdmin](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="e59f1-253">Нажмите кнопку **ОК** tooadd hello выбранные пользователи toohello **добавить разрешение** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="e59f1-253">Click **OK** tooadd hello selected users toohello **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="e59f1-254">Теперь, когда вы определили hello пользователей, назначьте роль toohello hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="e59f1-254">Now that you've identified hello user, assign hello user toohello role.</span></span> <span data-ttu-id="e59f1-255">В **назначены роли**, hello раскрывающемся списке выберите **BackupAdminRole**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-255">In **Assigned Role**, from hello drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![Назначить пользователя toorole](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="e59f1-257">На hello **управление** на вкладке hello **глобальные разрешения** панель, hello новой учетной записи пользователя и роли hello связанные отображается в списке hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-257">On hello **Manage** tab in hello **Global Permissions** panel, hello new user account and hello associated role appear in hello list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="e59f1-258">Настройка учетных данных сервера vCenter на Сервере резервного копирования Azure</span><span class="sxs-lookup"><span data-stu-id="e59f1-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="e59f1-259">Перед добавлением hello VMware server tooAzure резервное копирование, установите [обновления 1 для Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span><span class="sxs-lookup"><span data-stu-id="e59f1-259">Before you add hello VMware server tooAzure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="e59f1-260">tooopen Azure Backup Server дважды щелкните значок hello на рабочем столе hello Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="e59f1-260">tooopen Azure Backup Server, double-click hello icon on hello Azure Backup Server desktop.</span></span>

    ![Значок сервера резервного копирования Azure](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="e59f1-262">Если не удается найти hello значка на рабочем столе hello, откройте Azure Backup Server из hello список установленных приложений.</span><span class="sxs-lookup"><span data-stu-id="e59f1-262">If you can't find hello icon on hello desktop, open Azure Backup Server from hello list of installed apps.</span></span> <span data-ttu-id="e59f1-263">Имя приложения Hello Azure Backup Server называется архивации Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e59f1-263">hello Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="e59f1-264">В консоли Azure Backup Server приветствия щелкните **управления**, нажмите кнопку **рабочих серверов**и на ленте инструментов hello, щелкните **управление VMware**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-264">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then on hello tool ribbon, click **Manage VMware**.</span></span>

    ![Консоль сервера Azure Backup Server](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="e59f1-266">Hello **управление учетными данными** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="e59f1-266">hello **Manage Credentials** dialog box appears.</span></span>

    ![Диалоговое окно управления учетными данными на сервере Azure Backup Server](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="e59f1-268">В hello **управление учетными данными** диалоговое окно, нажмите кнопку **добавить** tooopen hello **Add Credential** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="e59f1-268">In hello **Manage Credentials** dialog box, click **Add** tooopen hello **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="e59f1-269">В hello **Add Credential** диалоговом окне введите имя и описание для hello новые учетные данные.</span><span class="sxs-lookup"><span data-stu-id="e59f1-269">In hello **Add Credential** dialog box, enter a name and a description for hello new credential.</span></span> <span data-ttu-id="e59f1-270">Затем укажите hello имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="e59f1-270">Then specify hello username and password.</span></span> <span data-ttu-id="e59f1-271">Имя Hello *credential Contoso Vcenter* используется учетных данных hello tooidentify в следующей процедуре hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-271">hello name, *Contoso Vcenter credential* is used tooidentify hello credential in hello next procedure.</span></span> <span data-ttu-id="e59f1-272">Используйте hello же имя пользователя и пароль, используемый для hello vCenter Server.</span><span class="sxs-lookup"><span data-stu-id="e59f1-272">Use hello same username and password that is used for hello vCenter Server.</span></span> <span data-ttu-id="e59f1-273">Если hello vCenter Server и сервера Azure Backup не находятся в hello в одном домене **имя пользователя**, укажите домен hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-273">If hello vCenter Server and Azure Backup Server are not in hello same domain, in **User name**, specify hello domain.</span></span>

    ![Диалоговое окно добавления учетных данных на сервере Azure Backup Server](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="e59f1-275">Нажмите кнопку **добавить** tooadd hello tooAzure новых учетных данных сервер резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="e59f1-275">Click **Add** tooadd hello new credential tooAzure Backup Server.</span></span> <span data-ttu-id="e59f1-276">Hello новых учетных данных появляется в списке hello в hello **управление учетными данными** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="e59f1-276">hello new credential appears in hello list in hello **Manage Credentials** dialog box.</span></span>
    
    ![Диалоговое окно управления учетными данными на сервере Azure Backup Server](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="e59f1-278">tooclose hello **управление учетными данными** диалоговое окно, нажмите кнопку hello **X** в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-278">tooclose hello **Manage Credentials** dialog box, click hello **X** in hello upper-right corner.</span></span>


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a><span data-ttu-id="e59f1-279">Добавить hello vCenter Server tooAzure резервное копирование сервера</span><span class="sxs-lookup"><span data-stu-id="e59f1-279">Add hello vCenter Server tooAzure Backup Server</span></span>

<span data-ttu-id="e59f1-280">Мастер добавления производственного сервера — используется tooadd hello vCenter Server tooAzure резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="e59f1-280">Production Server Addition Wizard is used tooadd hello vCenter Server tooAzure Backup Server.</span></span>

<span data-ttu-id="e59f1-281">tooopen мастер Добавление Server производства, полный hello после процедуры:</span><span class="sxs-lookup"><span data-stu-id="e59f1-281">tooopen Production Server Addition Wizard, complete hello following procedure:</span></span>

1. <span data-ttu-id="e59f1-282">В консоли Azure Backup Server hello щелкните **управления**, нажмите кнопку **рабочих серверов**и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-282">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![Открытие мастера добавления рабочего сервера](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="e59f1-284">Hello **мастер добавления производственного сервера** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="e59f1-284">hello **Production Server Addition Wizard** dialog box appears.</span></span>

    ![Мастер добавления рабочего сервера](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="e59f1-286">На hello **рабочего сервера, выберите тип** выберите **серверов VMware**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-286">On hello **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="e59f1-287">В **имя или IP-адрес сервера**, hello полное доменное имя (FQDN) или IP-адрес сервера VMware hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-287">In **Server Name/IP Address**, specify hello fully qualified domain name (FQDN) or IP address of hello VMware server.</span></span> <span data-ttu-id="e59f1-288">Если все серверы ESXi hello управляются hello же vCenter, можно использовать имя vCenter hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-288">If all hello ESXi servers are managed by hello same vCenter, you can use hello vCenter name.</span></span>

    ![Указание полного доменного имени или IP-адреса сервера VMware](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="e59f1-290">В **порт SSL**, введите порт, используемый toocommunicate с сервером VMware hello на hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-290">In **SSL Port**, enter hello port that is used toocommunicate with hello VMware server.</span></span> <span data-ttu-id="e59f1-291">Используйте порт 443, который является порт по умолчанию hello, если нет уверенности, что требуется другой порт.</span><span class="sxs-lookup"><span data-stu-id="e59f1-291">Use port 443, which is hello default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="e59f1-292">В **задание учетных данных**, выберите hello учетных данных, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="e59f1-292">In **Specify Credential**, select hello credential that you created earlier.</span></span>

    ![Указание учетных данных](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="e59f1-294">Нажмите кнопку **добавить** tooadd hello VMware toohello список серверов **добавленные серверы VMware**, а затем нажмите кнопку **Далее** toomove toohello следующей странице приветствия мастера создания.</span><span class="sxs-lookup"><span data-stu-id="e59f1-294">Click **Add** tooadd hello VMware server toohello list of **Added VMware Servers**, and then click **Next** toomove toohello next page in hello wizard.</span></span>

    ![Добавление сервера VMware и учетных данных](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="e59f1-296">В hello **Сводка** щелкните **добавить** tooadd hello указан сервер VMware tooAzure резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="e59f1-296">In hello **Summary** page, click **Add** tooadd hello specified VMware server tooAzure Backup Server.</span></span>

    ![Добавление сервера VMware tooAzure резервное копирование сервера](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="e59f1-298">резервная копия сервера VMware Hello является без агента и немедленно добавляется новый сервер hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-298">hello VMware server backup is an agentless backup, and hello new server is added immediately.</span></span> <span data-ttu-id="e59f1-299">Hello **Готово** страниц отображает hello результаты.</span><span class="sxs-lookup"><span data-stu-id="e59f1-299">hello **Finish** page shows you hello results.</span></span>

  ![Страница "Готово"](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="e59f1-301">tooadd несколько экземпляров tooAzure vCenter Server резервное копирование сервера, повторите hello предыдущих шагов в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="e59f1-301">tooadd multiple instances of vCenter Server tooAzure Backup Server, repeat hello previous steps in this section.</span></span>

<span data-ttu-id="e59f1-302">После добавления hello vCenter Server tooAzure резервное копирование сервера hello следующим шагом является toocreate группы защиты.</span><span class="sxs-lookup"><span data-stu-id="e59f1-302">After you add hello vCenter Server tooAzure Backup Server, hello next step is toocreate a protection group.</span></span> <span data-ttu-id="e59f1-303">Группа защиты Hello указывает hello различные сведения для коротких и долгосрочному хранению, а где определить и применить политику резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-303">hello protection group specifies hello various details for short or long-term retention, and it is where you define and apply hello backup policy.</span></span> <span data-ttu-id="e59f1-304">Hello политику резервного копирования — расписание hello, когда выполняется резервное копирование и объекты для резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="e59f1-304">hello backup policy is hello schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="e59f1-305">Настройка группы защиты</span><span class="sxs-lookup"><span data-stu-id="e59f1-305">Configure a protection group</span></span>

<span data-ttu-id="e59f1-306">Если вы не работали System Center Data Protection Manager или сервер резервного копирования Azure перед, см. раздел [Планирование резервного копирования на диск](https://technet.microsoft.com/library/hh758026.aspx) tooprepare аппаратную среду.</span><span class="sxs-lookup"><span data-stu-id="e59f1-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) tooprepare your hardware environment.</span></span> <span data-ttu-id="e59f1-307">После проверки наличия необходимый объем ресурсов хранения, используйте hello мастера создания новой группы защиты tooadd VMware виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e59f1-307">After you check that you have proper storage, use hello Create New Protection Group wizard tooadd VMware virtual machines.</span></span>

1. <span data-ttu-id="e59f1-308">В консоли Azure Backup Server hello щелкните **защиты**и на ленте инструментов hello, щелкните **New** мастера создания новой группы защиты tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-308">In hello Azure Backup Server console, click **Protection**, and in hello tool ribbon, click **New** tooopen hello Create New Protection Group wizard.</span></span>

    ![Привет открыть мастер создания новой группы защиты](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="e59f1-310">Hello **создания новой группы защиты** откроется диалоговое окно мастера.</span><span class="sxs-lookup"><span data-stu-id="e59f1-310">hello **Create New Protection Group** wizard dialog box appears.</span></span>

    ![Диалоговое окно мастера создания групп защиты](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="e59f1-312">Нажмите кнопку **Далее** tooadvance toohello **Выбор типа группы защиты** страницы.</span><span class="sxs-lookup"><span data-stu-id="e59f1-312">Click **Next** tooadvance toohello **Select protection group type** page.</span></span>

2. <span data-ttu-id="e59f1-313">На hello **типа группы защиты выберите** выберите **серверы** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-313">On hello **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="e59f1-314">Hello **Выбор членов группы** появится страница.</span><span class="sxs-lookup"><span data-stu-id="e59f1-314">hello **Select group members** page appears.</span></span>

3. <span data-ttu-id="e59f1-315">На hello **Выбор членов группы** страницы, доступные элементы hello и hello выбранные элементы отображаются.</span><span class="sxs-lookup"><span data-stu-id="e59f1-315">On hello **Select group members** page, hello available members and hello selected members appear.</span></span> <span data-ttu-id="e59f1-316">Выбор членов hello требуется tooprotect и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-316">Select hello members that you want tooprotect, and then click **Next**.</span></span>

    ![Выберите членов группы](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="e59f1-318">Если при выборе элемента вы выберете папку, содержащую другие папки или виртуальные машины, эти элементы также будут выбраны.</span><span class="sxs-lookup"><span data-stu-id="e59f1-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="e59f1-319">Включение Hello hello папки и виртуальные машины в родительской папке hello называется защиту на уровне папки.</span><span class="sxs-lookup"><span data-stu-id="e59f1-319">hello inclusion of hello folders and VMs in hello parent folder is called folder-level protection.</span></span> <span data-ttu-id="e59f1-320">tooremove папки или виртуальной Машины, hello, снимите флажок.</span><span class="sxs-lookup"><span data-stu-id="e59f1-320">tooremove a folder or VM, clear hello check box.</span></span>

    <span data-ttu-id="e59f1-321">Если виртуальная машина или папке, содержащей виртуальную Машину, уже защищенные tooAzure, нельзя выбрать эту виртуальную Машину еще раз.</span><span class="sxs-lookup"><span data-stu-id="e59f1-321">If a VM, or a folder containing a VM, is already protected tooAzure, you cannot select that VM again.</span></span> <span data-ttu-id="e59f1-322">Т. е после tooAzure защищенных ВМ него невозможно включить защиту еще раз, который предотвращает создание для одной виртуальной Машиной точек восстановления повторяющиеся.</span><span class="sxs-lookup"><span data-stu-id="e59f1-322">That is, after a VM is protected tooAzure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="e59f1-323">Если вы хотите toosee, какому экземпляру сервера резервного копирования Azure уже защищает элемент, toohello точки toosee hello имени члена hello защищает сервер.</span><span class="sxs-lookup"><span data-stu-id="e59f1-323">If you want toosee which Azure Backup Server instance already protects a member, point toohello member toosee hello name of hello protecting server.</span></span>

4. <span data-ttu-id="e59f1-324">На hello **Выбор метода защиты данных** введите имя для группы защиты hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-324">On hello **Select Data Protection Method** page, enter a name for hello protection group.</span></span> <span data-ttu-id="e59f1-325">Выбраны краткосрочной защиты (toodisk) и оперативной защиты.</span><span class="sxs-lookup"><span data-stu-id="e59f1-325">Short-term protection (toodisk) and online protection are selected.</span></span> <span data-ttu-id="e59f1-326">Если требуется оперативная защита toouse (tooAzure), необходимо использовать toodisk краткосрочной защиты.</span><span class="sxs-lookup"><span data-stu-id="e59f1-326">If you want toouse online protection (tooAzure), you must use short-term protection toodisk.</span></span> <span data-ttu-id="e59f1-327">Нажмите кнопку **Далее** диапазон tooproceed toohello краткосрочной защиты.</span><span class="sxs-lookup"><span data-stu-id="e59f1-327">Click **Next** tooproceed toohello short-term protection range.</span></span>

    ![Выберите метод защиты данных](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="e59f1-329">На hello **Выбор краткосрочных целей** страницы, для **диапазон хранения**, укажите количество hello в днях точек восстановления tooretain *хранимых toodisk*.</span><span class="sxs-lookup"><span data-stu-id="e59f1-329">On hello **Specify Short-Term Goals** page, for **Retention Range**, specify hello number of days that you want tooretain recovery points that are *stored toodisk*.</span></span> <span data-ttu-id="e59f1-330">Toochange hello время и дни, когда создаются точки восстановления, нажмите кнопку **изменить**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-330">If you want toochange hello time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="e59f1-331">Hello точек краткосрочного восстановления выполняется полная архивация.</span><span class="sxs-lookup"><span data-stu-id="e59f1-331">hello short-term recovery points are full backups.</span></span> <span data-ttu-id="e59f1-332">Для них не выполняется добавочное резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="e59f1-332">They are not incremental backups.</span></span> <span data-ttu-id="e59f1-333">Когда краткосрочных целей hello вас устраивают, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-333">When you are satisfied with hello short-term goals, click **Next**.</span></span>

    ![Выберите краткосрочные цели](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="e59f1-335">На hello **Просмотр распределения места на** просмотрите и при необходимости измените hello места на диске для виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-335">On hello **Review Disk Allocation** page, review and if necessary, modify hello disk space for hello VMs.</span></span> <span data-ttu-id="e59f1-336">Рекомендуется Hello выделения места на диске основаны на диапазон хранения hello, которая указана в hello **Выбор краткосрочных целей** странице hello тип рабочей нагрузки и размер hello hello защищенных данных, (определенный на шаге 3).</span><span class="sxs-lookup"><span data-stu-id="e59f1-336">hello recommended disk allocations are based on hello retention range that is specified in hello **Specify Short-Term Goals** page, hello type of workload, and hello size of hello protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="e59f1-337">**Размер данных:** размер данных hello в группе защиты hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-337">**Data size:** Size of hello data in hello protection group.</span></span>
  - <span data-ttu-id="e59f1-338">**Место на диске:** hello, рекомендуемый объем дискового пространства для группы защиты hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-338">**Disk space:** hello recommended amount of disk space for hello protection group.</span></span> <span data-ttu-id="e59f1-339">Если требуется toomodify этот параметр, необходимо выделить пространство, немного превышающее сумму hello, которое увеличивается для каждого источника данных.</span><span class="sxs-lookup"><span data-stu-id="e59f1-339">If you want toomodify this setting, you should allocate total space that is slightly larger than hello amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="e59f1-340">**Совместное размещение данных:** при включении совместного размещения несколько источников данных в hello защиты можно сопоставить tooa одной репликой и томом точек восстановления.</span><span class="sxs-lookup"><span data-stu-id="e59f1-340">**Colocate data:** If you turn on colocation, multiple data sources in hello protection can map tooa single replica and recovery point volume.</span></span> <span data-ttu-id="e59f1-341">Совместное размещение поддерживается не для всех рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="e59f1-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="e59f1-342">**Автоматически увеличивать размер:** Если включить этот параметр, то при превышении в группе защищенных hello начального выделения hello, System Center Data Protection Manager предпринимает tooincrease hello места на диске на 25 процентов.</span><span class="sxs-lookup"><span data-stu-id="e59f1-342">**Automatically grow:** If you turn on this setting, if data in hello protected group outgrows hello initial allocation, System Center Data Protection Manager tries tooincrease hello disk size by 25 percent.</span></span>
  - <span data-ttu-id="e59f1-343">**Сведения о пуле носителей:** hello состояние пула носителей hello, включая общий и оставшийся размер диска.</span><span class="sxs-lookup"><span data-stu-id="e59f1-343">**Storage pool details:** Shows hello status of hello storage pool, including total and remaining disk size.</span></span>

    ![Просмотр выделения дискового пространства](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="e59f1-345">После выделения пространства hello вас устраивают, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-345">When you are satisfied with hello space allocation, click **Next**.</span></span>

7. <span data-ttu-id="e59f1-346">На hello **Выбор метода создания реплики** укажите способ начальной копии toogenerate hello или реплики hello защищенных данных на сервере резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="e59f1-346">On hello **Choose Replica Creation Method** page, specify how you want toogenerate hello initial copy, or replica, of hello protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="e59f1-347">по умолчанию Hello — **автоматически по сети hello** и **теперь**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-347">hello default is **Automatically over hello network** and **Now**.</span></span> <span data-ttu-id="e59f1-348">Если используется по умолчанию hello, рекомендуется указывать время низкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e59f1-348">If you use hello default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="e59f1-349">Выберите параметр **Позже** и укажите день и время.</span><span class="sxs-lookup"><span data-stu-id="e59f1-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="e59f1-350">Для больших объемов данных или менее чем оптимального состояния сети рассмотрите возможность репликации данных hello в автономном режиме с помощью съемного носителя.</span><span class="sxs-lookup"><span data-stu-id="e59f1-350">For large amounts of data or less-than-optimal network conditions, consider replicating hello data offline by using removable media.</span></span>

    <span data-ttu-id="e59f1-351">Задав параметры по своему усмотрению, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-351">After you have made your choices, click **Next**.</span></span>

    ![Выберите метод создания реплики](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="e59f1-353">На hello **параметры проверки согласованности** выберите, как и когда проверяет согласованность tooautomate hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-353">On hello **Consistency Check Options** page, select how and when tooautomate hello consistency checks.</span></span> <span data-ttu-id="e59f1-354">В случае несогласованности данных реплики вы можете запустить проверку на согласованность, либо эта проверка может выполняться по расписанию.</span><span class="sxs-lookup"><span data-stu-id="e59f1-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="e59f1-355">Если вы не хотите tooconfigure автоматической проверки согласованности, можно выполнить проверку вручную.</span><span class="sxs-lookup"><span data-stu-id="e59f1-355">If you don't want tooconfigure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="e59f1-356">В области защиты hello hello Azure Backup Server консоли, щелкните правой кнопкой мыши группу защиты hello, а затем выберите **выполнить проверку согласованности**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-356">In hello protection area of hello Azure Backup Server console, right-click hello protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="e59f1-357">Нажмите кнопку **Далее** toomove toohello следующую страницу.</span><span class="sxs-lookup"><span data-stu-id="e59f1-357">Click **Next** toomove toohello next page.</span></span>

9. <span data-ttu-id="e59f1-358">На hello **укажите оперативной защиты данных** выберите одного или нескольких источников данных, которые должны tooprotect.</span><span class="sxs-lookup"><span data-stu-id="e59f1-358">On hello **Specify Online Protection Data** page, select one or more data sources that you want tooprotect.</span></span> <span data-ttu-id="e59f1-359">Можно выбрать элементы hello по отдельности или нажать кнопку **выделить все** toochoose все элементы.</span><span class="sxs-lookup"><span data-stu-id="e59f1-359">You can select hello members individually, or click **Select All** toochoose all members.</span></span> <span data-ttu-id="e59f1-360">Hello членов, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-360">After you choose hello members, click **Next**.</span></span>

    ![Выбор оперативной защиты данных](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="e59f1-362">На hello **указание расписания оперативной архивации** укажите hello расписание точек восстановления toogenerate из резервной копии диска hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-362">On hello **Specify Online Backup Schedule** page, specify hello schedule toogenerate recovery points from hello disk backup.</span></span> <span data-ttu-id="e59f1-363">После создания точки восстановления hello это хранилище служб восстановления toohello переносятся в Azure.</span><span class="sxs-lookup"><span data-stu-id="e59f1-363">After hello recovery point is generated, it is transferred toohello Recovery Services vault in Azure.</span></span> <span data-ttu-id="e59f1-364">Если вас устраивают hello расписания оперативного резервного копирования, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-364">When you are satisfied with hello online backup schedule, click **Next**.</span></span>

    ![Выбор расписания оперативного резервного копирования](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="e59f1-366">На hello **указание политики оперативного хранения** укажите, как долго tooretain hello резервного копирования данных в Azure.</span><span class="sxs-lookup"><span data-stu-id="e59f1-366">On hello **Specify Online Retention Policy** page, indicate how long you want tooretain hello backup data in Azure.</span></span> <span data-ttu-id="e59f1-367">После определения политики hello щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-367">After hello policy is defined, click **Next**.</span></span>

    ![Выбор политики оперативного хранения](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="e59f1-369">Временных ограничений для хранения данных в Azure нет.</span><span class="sxs-lookup"><span data-stu-id="e59f1-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="e59f1-370">При сохранении данных точки восстановления в Azure hello только ограничен, не может иметь больше 9999 точек восстановления для каждого защищенного экземпляра.</span><span class="sxs-lookup"><span data-stu-id="e59f1-370">When you store recovery point data in Azure, hello only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="e59f1-371">В этом примере hello защищенного экземпляра — сервер VMware hello.</span><span class="sxs-lookup"><span data-stu-id="e59f1-371">In this example, hello protected instance is hello VMware server.</span></span>

12. <span data-ttu-id="e59f1-372">На hello **Сводка** страницы, просмотрите сведения об hello для членов группы защиты и параметры и нажмите кнопку **создать группу**.</span><span class="sxs-lookup"><span data-stu-id="e59f1-372">On hello **Summary** page, review hello details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![Сводка параметров и элементов группы защиты](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="e59f1-374">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e59f1-374">Next steps</span></span>
<span data-ttu-id="e59f1-375">При использовании рабочих нагрузок VMware tooprotect резервное копирование Azure, может быть хотят использовать Azure Backup Server защиты toohelp [Microsoft Exchange server](./backup-azure-exchange-mabs.md), [фермы Microsoft SharePoint](./backup-azure-backup-sharepoint-mabs.md), или [Базы данных SQL Server](./backup-azure-sql-mabs.md).</span><span class="sxs-lookup"><span data-stu-id="e59f1-375">If you use Azure Backup Server tooprotect VMware workloads, you may be interested in using Azure Backup Server toohelp protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="e59f1-376">Сведения о проблемах с регистрация агента hello настройку группы защиты hello или резервное копирование заданий, в разделе [Устранение неполадок Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="e59f1-376">For information on problems with registering hello agent, configuring hello protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>
