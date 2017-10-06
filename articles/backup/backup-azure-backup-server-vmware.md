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
# <a name="back-up-a-vmware-server-tooazure"></a>Резервное копирование сервера VMware tooAzure

В этой статье объясняется, как резервное копирование Azure toohelp tooconfigure защитить рабочие нагрузки сервера VMware. Чтобы приступить к работе с этим руководством, вам необходимо установить сервер резервного копирования Azure. Если у вас нет Azure Backup Server установлены, см. раздел [Подготовка tooback копирование рабочих нагрузок, использующих Azure Backup Server](backup-azure-microsoft-azure-backup.md).

Azure Backup Server обеспечивает резервное копирование (или защиту) серверов VMware vCenter версий 6.5, 6.0 и 5.5.


## <a name="create-a-secure-connection-toohello-vcenter-server"></a>Создать безопасное подключение toohello vCenter Server

По умолчанию Azure Backup Server взаимодействует с каждым сервером vCenter через канал HTTPS. tooturn на hello безопасного взаимодействия рекомендуется устанавливать hello VMware центра сертификации (ЦС) сертификата на сервер резервного копирования Azure. Если не требуется безопасное соединение и предпочитаете toodisable hello обязательное использование протокола HTTPS, см. раздел [отключение безопасного взаимодействия протокола](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol). toocreate безопасное подключение между сервером резервного копирования Azure и hello vCenter Server, импортируйте hello доверенных сертификатов на сервере резервного копирования Azure.

Как правило используется браузер на vCenter toohello tooconnect Azure Backup Server машины hello Server через vSphere hello веб-клиента. Hello при первом обращении hello Azure Backup Server браузера tooconnect toohello vCenter Server, подключение hello не защищены. Следующие изображения Hello демонстрирует подключение hello незащищенным.

![Пример сервера tooVMware небезопасное подключение](./media/backup-azure-backup-server-vmware/unsecure-url.png)

toofix эту проблему и создать безопасное соединение, загрузка hello доверенных корневых сертификатов.

1. В браузере hello на сервер резервного копирования Azure введите vSphere toohello hello URL-адрес веб-клиента. отображается страница входа веб-клиент vSphere Hello.

    ![Веб-клиент vSphere](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    Внизу hello hello сведения для администраторов и разработчиков, найдите hello **загрузки корневые сертификаты доверенного ЦС** ссылку.

    ![Ссылка toodownload hello доверенных корневых сертификатов](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  Если вы не видите страницу входа веб-клиент vSphere hello, проверьте параметры прокси-сервера в браузере.

2. Щелкните **Download trusted root CA certificates** (Скачать сертификаты доверенного корневого ЦС).

    Hello vCenter Server загружает файл tooyour локального компьютера. Hello имя файла называется **загрузить**. В зависимости от браузера, появится сообщение с запросом, является ли tooopen или сохранение файла hello.

    ![Сообщение после скачивания сертификатов](./media/backup-azure-backup-server-vmware/download-certs.png)

3. Hello файл tooa расположение для сохранения на сервере резервного копирования Azure. При сохранении файла hello добавьте расширение имени файла .zip hello.

    Hello файл является ZIP-файл, содержащий hello сведения о сертификатах hello. С расширением .zip hello можно использовать средства извлечения hello.

4. Щелкните правой кнопкой мыши **download.zip**, а затем выберите **извлечь все** tooextract hello содержимое.

    ZIP-файл Hello извлекает его содержимое tooa папка **сертификаты**. Два типа файлов отображаются в папке сертификатов hello. файл корневого сертификата Hello имеет расширение, которое начинается с номером последовательности как.0 и.1.
    
    файл списка отзыва Сертификатов Hello имеет расширение, которое начинается с последовательности как .r0 или .r1. файл списка отзыва Сертификатов Hello связан с сертификатом.

    ![Извлечение скачанного файла на локальный компьютер ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. В hello **сертификатов** папку, щелкните правой кнопкой мыши файл hello корневого сертификата и нажмите кнопку **переименование**.

    ![Переименование корневого сертификата ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    Измените расширение too.crt hello корневой сертификат. В ответ на запрос, если Вы действительно хотите toochange hello расширение, нажмите кнопку **Да** или **ОК**. В противном случае изменении функции hello файла. значок Hello hello изменения файла tooan значок, представляющий корневой сертификат.

6. Щелкните правой кнопкой мыши корневой сертификат hello и hello во всплывающем меню, выберите **установить сертификат**.

    Hello **мастер импорта сертификатов** откроется диалоговое окно.

7. В hello **мастер импорта сертификатов** выберите **локального компьютера** назначения hello hello сертификат, а затем нажмите кнопку **Далее** toocontinue.

    ![Параметры назначения хранилища сертификатов ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    В ответ на вопрос, следует ли компьютер toohello tooallow изменения, нажмите кнопку **Да** или **ОК**, tooall hello изменения.

8. На hello **хранилище сертификатов** выберите **поместить все сертификаты в следующие хранилища hello**, а затем нажмите кнопку **Обзор** хранилище сертификатов toochoose hello.

    ![Размещение сертификатов в определенном месте в хранилище](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    Hello **Выбор хранилища сертификата** откроется диалоговое окно.

    ![Иерархия папки хранилища сертификатов](./media/backup-azure-backup-server-vmware/cert-store.png)

9. Выберите **доверенные корневые центры сертификации** как hello конечную папку для hello сертификатов, а затем щелкните **ОК**.

    ![Папка назначения для сертификата](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    Hello **доверенные корневые центры сертификации** папку подтверждено как хранилище сертификатов hello. Щелкните **Далее**.

    ![Папка хранилища сертификатов](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. На hello **hello завершение работы мастера импорта сертификатов** , убедитесь, что hello сертификат находится в нужной папке hello и выберите **Готово**.

    ![Убедитесь, что сертификат находится в соответствующей папке hello](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    Появится диалоговое окно, hello импорта сертификатов успешно подтверждена.

11. Войдите в систему toohello vCenter Server tooconfirm, что соединение является безопасным.

  Если не удается установить безопасное соединение hello Импорт сертификата не выполнена успешно, в документации hello VMware vSphere на [получение сертификатов сервера](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).

  Если имеется области безопасности вашей организации и не требуется tooturn на hello протокола HTTPS, используйте hello, выполнив процедуру toodisable hello безопасных соединений.

### <a name="disable-secure-communication-protocol"></a>Отключение протокола безопасной связи

Если ваша организация не требует протокол HTTPS hello, используйте следующие шаги toodisable HTTPS hello. toodisable hello поведение по умолчанию, создайте раздел реестра, который пропускает поведение по умолчанию hello.

1. Скопируйте и вставьте следующий текст в файл hello.

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. Сохраните hello файл tooyour Azure Backup Server компьютера. Для имени файла hello используйте DisableSecureAuthentication.reg.

3. Дважды щелкните запись реестра hello tooactivate файла hello.


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a>Создать роли и учетной записи для hello vCenter Server

На сервере vCenter hello роль — это стандартный набор привилегий. Администратор сервера vCenter создаются роли hello. разрешения tooassign Здравствуйте, администратор пар учетных записей пользователей с ролью. tooback tooestablish hello пользователя необходимые учетные данные компьютера сервера vCenter hello, создать роль с определенными правами доступа и затем связать hello учетная запись пользователя с ролью hello.

Сервер резервного копирования Azure использует имя пользователя и пароль tooauthenticate с hello vCenter Server. Сервер резервного копирования Azure использует эти учетные данные пользователя для аутентификации всех операций архивации.

tooadd vCenter роли сервера и соответствующие права для администратора резервного копирования:

1. Войдите в toohello vCenter Server, а затем в hello vCenter Server **Навигатор** нажмите кнопку **администрирования**.

    ![Параметр администрирования в области Navigator (Навигатор) на сервере vCenter](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. В **администрирования** выберите **ролей**, а затем в hello **ролей** щелкните панель hello добавить значок роли ("Здравствуйте," + "символ").

    ![Добавление роли](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    Hello **Create Role** откроется диалоговое окно.

    ![Создание роли](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. В hello **Create Role** диалогового окна hello **имя роли** введите *BackupAdminRole*. Имя роли Hello может быть любым, но должны распознаваться для цели hello роли.

4. Выберите hello права доступа для соответствующей версии vCenter hello и нажмите кнопку **ОК**. Привет, в следующей таблице идентифицирует hello необходимые привилегии для vCenter 6.0 и vCenter 5.5.

  При выборе привилегии hello щелкните hello значок Далее toohello родительской метки tooexpand hello родительского представления hello дочерних правами доступа и. tooselect hello VirtualMachine права доступа, необходимые toogo несколько уровней в hello родительская иерархия дочерних. Не нужно tooselect все дочерние привилегий в пределах родительского права доступа.

  ![Иерархия привилегий родителей-потомков](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  После нажатия кнопки **ОК**, появится новая роль hello в списке hello на панели ролей hello.

|Привилегии для vCenter 6.0| Привилегии для vCenter 5.5|
|--------------------------|---------------------------|
|Datastore.AllocateSpace   | Datastore.AllocateSpace|
|Global.ManageCustomFields | Global.ManageCustomerFields|
|Global.SetCustomFields    |   |
|Host.Local.CreateVM       | Network.Assign |
|Network.Assign            |  |
|Resource.AssignVMToPool   |  |
|VirtualMachine.Config.AddNewDisk  | VirtualMachine.Config.AddNewDisk   |
|VirtualMachine.Config.AdvanceConfig| VirtualMachine.Config.AdvancedConfig|
|VirtualMachine.Config.ChangeTracking| VirtualMachine.Config.ChangeTracking |
|VirtualMachine.Config.HostUSBDevice||
|VirtualMachine.Config.QueryUnownedFiles|    |
|VirtualMachine.Config.SwapPlacement| VirtualMachine.Config.SwapPlacement |
|VirtualMachine.Interact.PowerOff| VirtualMachine.Interact.PowerOff |
|VirtualMachine.Inventory.Create| VirtualMachine.Inventory.Create |
|VirtualMachine.Provisioning.DiskRandomAccess| |
|VirtualMachine.Provisioning.DiskRandomRead|VirtualMachine.Provisioning.DiskRandomRead |
|VirtualMachine.State.CreateSnapshot| VirtualMachine.State.CreateSnapshot|
|VirtualMachine.State.RemoveSnapshot|VirtualMachine.State.RemoveSnapshot |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a>Создание учетной записи пользователя сервера vCenter и разрешений

После настройки hello роли с правами, создайте учетную запись пользователя. Hello учетная запись имеет имя и пароль, который предоставляет hello учетные данные, используемые для проверки подлинности.

1. учетной записи пользователя в hello vCenter Server toocreate **Навигатор** нажмите кнопку **пользователей и групп**.

    ![Пользователи и группы](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    Hello **vCenter пользователей и групп** появится панель.

    ![Панель vCenter Users and Groups (Пользователи и группы vCenter)](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. В hello **vCenter пользователей и групп** панель, выберите hello **пользователей** , а затем щелкните hello добавить значок пользователей ("Здравствуйте," + "символ").

    Hello **нового пользователя** откроется диалоговое окно.

3. В hello **нового пользователя** диалоговое окно добавления сведений о пользователе hello и нажмите кнопку **ОК**. В этой процедуре hello пользователя является BackupAdmin.

    ![Диалоговое окно New User (Новый пользователь)](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    Hello новой учетной записи пользователя отображается в списке hello.

4. Учетная запись пользователя hello tooassociate с роли hello в hello **Навигатор** нажмите кнопку **глобальные разрешения**. В hello **глобальные разрешения** панель, выберите hello **управление** , а затем щелкните hello добавить значок ("Здравствуйте," + "символ").

    ![Панель Global Permissions (Глобальные разрешения)](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    Hello **глобальные разрешения Root - добавить разрешение** откроется диалоговое окно.

5. В hello **глобальных разрешений Root - добавить разрешение** диалоговое окно, нажмите кнопку **добавить** toochoose hello пользователя или группы.

    ![Выбор пользователя или группы](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    Hello **выберите пользователей или группы** откроется диалоговое окно.

6. В hello **выберите пользователей или группы** диалогового окна выберите **BackupAdmin** и нажмите кнопку **добавить**.

    В **пользователей**, hello *домен\имя_пользователя* формат используется для учетной записи пользователя hello. Если вы хотите toouse другого домена, выберите его из hello **домена** списка.

    ![Добавление пользователя BackupAdmin](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    Нажмите кнопку **ОК** tooadd hello выбранные пользователи toohello **добавить разрешение** диалоговое окно.

7. Теперь, когда вы определили hello пользователей, назначьте роль toohello hello пользователя. В **назначены роли**, hello раскрывающемся списке выберите **BackupAdminRole**, а затем нажмите кнопку **ОК**.

    ![Назначить пользователя toorole](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  На hello **управление** на вкладке hello **глобальные разрешения** панель, hello новой учетной записи пользователя и роли hello связанные отображается в списке hello.


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a>Настройка учетных данных сервера vCenter на Сервере резервного копирования Azure

Перед добавлением hello VMware server tooAzure резервное копирование, установите [обновления 1 для Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).

1. tooopen Azure Backup Server дважды щелкните значок hello на рабочем столе hello Azure Backup Server.

    ![Значок сервера резервного копирования Azure](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    Если не удается найти hello значка на рабочем столе hello, откройте Azure Backup Server из hello список установленных приложений. Имя приложения Hello Azure Backup Server называется архивации Microsoft Azure.

2. В консоли Azure Backup Server приветствия щелкните **управления**, нажмите кнопку **рабочих серверов**и на ленте инструментов hello, щелкните **управление VMware**.

    ![Консоль сервера Azure Backup Server](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    Hello **управление учетными данными** откроется диалоговое окно.

    ![Диалоговое окно управления учетными данными на сервере Azure Backup Server](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. В hello **управление учетными данными** диалоговое окно, нажмите кнопку **добавить** tooopen hello **Add Credential** диалоговое окно.

4. В hello **Add Credential** диалоговом окне введите имя и описание для hello новые учетные данные. Затем укажите hello имя пользователя и пароль. Имя Hello *credential Contoso Vcenter* используется учетных данных hello tooidentify в следующей процедуре hello. Используйте hello же имя пользователя и пароль, используемый для hello vCenter Server. Если hello vCenter Server и сервера Azure Backup не находятся в hello в одном домене **имя пользователя**, укажите домен hello.

    ![Диалоговое окно добавления учетных данных на сервере Azure Backup Server](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    Нажмите кнопку **добавить** tooadd hello tooAzure новых учетных данных сервер резервного копирования. Hello новых учетных данных появляется в списке hello в hello **управление учетными данными** диалоговое окно.
    
    ![Диалоговое окно управления учетными данными на сервере Azure Backup Server](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. tooclose hello **управление учетными данными** диалоговое окно, нажмите кнопку hello **X** в правом верхнем углу hello.


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a>Добавить hello vCenter Server tooAzure резервное копирование сервера

Мастер добавления производственного сервера — используется tooadd hello vCenter Server tooAzure резервное копирование.

tooopen мастер Добавление Server производства, полный hello после процедуры:

1. В консоли Azure Backup Server hello щелкните **управления**, нажмите кнопку **рабочих серверов**и нажмите кнопку **добавить**.

    ![Открытие мастера добавления рабочего сервера](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    Hello **мастер добавления производственного сервера** откроется диалоговое окно.

    ![Мастер добавления рабочего сервера](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. На hello **рабочего сервера, выберите тип** выберите **серверов VMware**, а затем нажмите кнопку **Далее**.

3. В **имя или IP-адрес сервера**, hello полное доменное имя (FQDN) или IP-адрес сервера VMware hello. Если все серверы ESXi hello управляются hello же vCenter, можно использовать имя vCenter hello.

    ![Указание полного доменного имени или IP-адреса сервера VMware](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. В **порт SSL**, введите порт, используемый toocommunicate с сервером VMware hello на hello. Используйте порт 443, который является порт по умолчанию hello, если нет уверенности, что требуется другой порт.

5. В **задание учетных данных**, выберите hello учетных данных, которое было создано ранее.

    ![Указание учетных данных](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. Нажмите кнопку **добавить** tooadd hello VMware toohello список серверов **добавленные серверы VMware**, а затем нажмите кнопку **Далее** toomove toohello следующей странице приветствия мастера создания.

    ![Добавление сервера VMware и учетных данных](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. В hello **Сводка** щелкните **добавить** tooadd hello указан сервер VMware tooAzure резервное копирование.

    ![Добавление сервера VMware tooAzure резервное копирование сервера](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  резервная копия сервера VMware Hello является без агента и немедленно добавляется новый сервер hello. Hello **Готово** страниц отображает hello результаты.

  ![Страница "Готово"](./media/backup-azure-backup-server-vmware/summary-screen.png)

  tooadd несколько экземпляров tooAzure vCenter Server резервное копирование сервера, повторите hello предыдущих шагов в этом разделе.

После добавления hello vCenter Server tooAzure резервное копирование сервера hello следующим шагом является toocreate группы защиты. Группа защиты Hello указывает hello различные сведения для коротких и долгосрочному хранению, а где определить и применить политику резервного копирования hello. Hello политику резервного копирования — расписание hello, когда выполняется резервное копирование и объекты для резервного копирования.


## <a name="configure-a-protection-group"></a>Настройка группы защиты

Если вы не работали System Center Data Protection Manager или сервер резервного копирования Azure перед, см. раздел [Планирование резервного копирования на диск](https://technet.microsoft.com/library/hh758026.aspx) tooprepare аппаратную среду. После проверки наличия необходимый объем ресурсов хранения, используйте hello мастера создания новой группы защиты tooadd VMware виртуальных машин.

1. В консоли Azure Backup Server hello щелкните **защиты**и на ленте инструментов hello, щелкните **New** мастера создания новой группы защиты tooopen hello.

    ![Привет открыть мастер создания новой группы защиты](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    Hello **создания новой группы защиты** откроется диалоговое окно мастера.

    ![Диалоговое окно мастера создания групп защиты](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    Нажмите кнопку **Далее** tooadvance toohello **Выбор типа группы защиты** страницы.

2. На hello **типа группы защиты выберите** выберите **серверы** и нажмите кнопку **Далее**. Hello **Выбор членов группы** появится страница.

3. На hello **Выбор членов группы** страницы, доступные элементы hello и hello выбранные элементы отображаются. Выбор членов hello требуется tooprotect и нажмите кнопку **Далее**.

    ![Выберите членов группы](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    Если при выборе элемента вы выберете папку, содержащую другие папки или виртуальные машины, эти элементы также будут выбраны. Включение Hello hello папки и виртуальные машины в родительской папке hello называется защиту на уровне папки. tooremove папки или виртуальной Машины, hello, снимите флажок.

    Если виртуальная машина или папке, содержащей виртуальную Машину, уже защищенные tooAzure, нельзя выбрать эту виртуальную Машину еще раз. Т. е после tooAzure защищенных ВМ него невозможно включить защиту еще раз, который предотвращает создание для одной виртуальной Машиной точек восстановления повторяющиеся. Если вы хотите toosee, какому экземпляру сервера резервного копирования Azure уже защищает элемент, toohello точки toosee hello имени члена hello защищает сервер.

4. На hello **Выбор метода защиты данных** введите имя для группы защиты hello. Выбраны краткосрочной защиты (toodisk) и оперативной защиты. Если требуется оперативная защита toouse (tooAzure), необходимо использовать toodisk краткосрочной защиты. Нажмите кнопку **Далее** диапазон tooproceed toohello краткосрочной защиты.

    ![Выберите метод защиты данных](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. На hello **Выбор краткосрочных целей** страницы, для **диапазон хранения**, укажите количество hello в днях точек восстановления tooretain *хранимых toodisk*. Toochange hello время и дни, когда создаются точки восстановления, нажмите кнопку **изменить**. Hello точек краткосрочного восстановления выполняется полная архивация. Для них не выполняется добавочное резервное копирование. Когда краткосрочных целей hello вас устраивают, нажмите кнопку **Далее**.

    ![Выберите краткосрочные цели](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. На hello **Просмотр распределения места на** просмотрите и при необходимости измените hello места на диске для виртуальных машин hello. Рекомендуется Hello выделения места на диске основаны на диапазон хранения hello, которая указана в hello **Выбор краткосрочных целей** странице hello тип рабочей нагрузки и размер hello hello защищенных данных, (определенный на шаге 3).  

  - **Размер данных:** размер данных hello в группе защиты hello.
  - **Место на диске:** hello, рекомендуемый объем дискового пространства для группы защиты hello. Если требуется toomodify этот параметр, необходимо выделить пространство, немного превышающее сумму hello, которое увеличивается для каждого источника данных.
  - **Совместное размещение данных:** при включении совместного размещения несколько источников данных в hello защиты можно сопоставить tooa одной репликой и томом точек восстановления. Совместное размещение поддерживается не для всех рабочих нагрузок.
  - **Автоматически увеличивать размер:** Если включить этот параметр, то при превышении в группе защищенных hello начального выделения hello, System Center Data Protection Manager предпринимает tooincrease hello места на диске на 25 процентов.
  - **Сведения о пуле носителей:** hello состояние пула носителей hello, включая общий и оставшийся размер диска.

    ![Просмотр выделения дискового пространства](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    После выделения пространства hello вас устраивают, нажмите кнопку **Далее**.

7. На hello **Выбор метода создания реплики** укажите способ начальной копии toogenerate hello или реплики hello защищенных данных на сервере резервного копирования Azure.

    по умолчанию Hello — **автоматически по сети hello** и **теперь**. Если используется по умолчанию hello, рекомендуется указывать время низкой нагрузки. Выберите параметр **Позже** и укажите день и время.

    Для больших объемов данных или менее чем оптимального состояния сети рассмотрите возможность репликации данных hello в автономном режиме с помощью съемного носителя.

    Задав параметры по своему усмотрению, нажмите кнопку **Далее**.

    ![Выберите метод создания реплики](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. На hello **параметры проверки согласованности** выберите, как и когда проверяет согласованность tooautomate hello. В случае несогласованности данных реплики вы можете запустить проверку на согласованность, либо эта проверка может выполняться по расписанию.

    Если вы не хотите tooconfigure автоматической проверки согласованности, можно выполнить проверку вручную. В области защиты hello hello Azure Backup Server консоли, щелкните правой кнопкой мыши группу защиты hello, а затем выберите **выполнить проверку согласованности**.

    Нажмите кнопку **Далее** toomove toohello следующую страницу.

9. На hello **укажите оперативной защиты данных** выберите одного или нескольких источников данных, которые должны tooprotect. Можно выбрать элементы hello по отдельности или нажать кнопку **выделить все** toochoose все элементы. Hello членов, нажмите кнопку **Далее**.

    ![Выбор оперативной защиты данных](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. На hello **указание расписания оперативной архивации** укажите hello расписание точек восстановления toogenerate из резервной копии диска hello. После создания точки восстановления hello это хранилище служб восстановления toohello переносятся в Azure. Если вас устраивают hello расписания оперативного резервного копирования, нажмите кнопку **Далее**.

    ![Выбор расписания оперативного резервного копирования](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. На hello **указание политики оперативного хранения** укажите, как долго tooretain hello резервного копирования данных в Azure. После определения политики hello щелкните **Далее**.

    ![Выбор политики оперативного хранения](./media/backup-azure-backup-server-vmware/retention-policy.png)

    Временных ограничений для хранения данных в Azure нет. При сохранении данных точки восстановления в Azure hello только ограничен, не может иметь больше 9999 точек восстановления для каждого защищенного экземпляра. В этом примере hello защищенного экземпляра — сервер VMware hello.

12. На hello **Сводка** страницы, просмотрите сведения об hello для членов группы защиты и параметры и нажмите кнопку **создать группу**.

    ![Сводка параметров и элементов группы защиты](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a>Дальнейшие действия
При использовании рабочих нагрузок VMware tooprotect резервное копирование Azure, может быть хотят использовать Azure Backup Server защиты toohelp [Microsoft Exchange server](./backup-azure-exchange-mabs.md), [фермы Microsoft SharePoint](./backup-azure-backup-sharepoint-mabs.md), или [Базы данных SQL Server](./backup-azure-sql-mabs.md).

Сведения о проблемах с регистрация агента hello настройку группы защиты hello или резервное копирование заданий, в разделе [Устранение неполадок Azure Backup Server](./backup-azure-mabs-troubleshoot.md).
