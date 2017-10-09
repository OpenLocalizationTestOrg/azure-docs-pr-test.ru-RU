---
title: "Сохраните данные и параметры пользователя, aaaHow ли Azure RemoteApp? | Документация Майкрософт"
description: "Узнайте, как Azure RemoteApp сохраняет данные пользователя, с помощью hello диск профиля пользователя."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: e125af62-5c1a-4186-a238-52f537f7bb34
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dccebc7861e8a0d87cb3ee174f399a2df7fe023c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-remoteapp-save-user-data-and-settings"></a>Как Azure RemoteApp сохраняет данные и параметры пользователя?
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Azure RemoteApp сохраняет удостоверения и настройки пользователя для различных устройств и сеансов. Такие данные пользователей хранятся на диске для каждой коллекции и для каждого пользователя, который называется диском профиля пользователя (UPD). диск Hello следует пользователя hello и гарантирует, что согласованной работы, независимо от того, где они вход пользователя hello.

Диски профилей пользователей являются полностью прозрачна toohello пользователя — пользователей сохранить документы папке "документы" tootheir (на то, что отображается toobe локального диска) и изменять параметры приложения как обычно. AT hello же времени, все личные параметры сохраняются при подключении tooAzure RemoteApp с любого устройства. Все hello пользователь видит на свои данные в hello одинаково.

Каждый UPD имеет 50 ГБ памяти для постоянного хранения и содержит как данные пользователя, так и параметры приложения. 

Чтение конкретных сведений в данных профиля пользователя.

> [!NOTE]
> Необходимость toodisable hello UPD? Сведения о том, как это сделать, см. в записи блога Pavithra [Disable User Profile Disks (UPDs) in Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) (Отключение дисков профилей пользователей в Azure RemoteApp).
> 
> 

## <a name="how-can-an-admin-get-toohello-data"></a>Как администратор может получить toohello данных
Если вам требуется tooaccess hello данных у пользователей (для аварийного восстановления или если hello пользователь покидает компанию hello), обратитесь в службу поддержки Azure и предоставить сведения о подписке hello для коллекции hello и удостоверение пользователя hello. Команда Hello Azure RemoteApp предоставляют toohello URL-адрес виртуального жесткого диска. Загрузите VHD по ссылке и извлеките документы и файлы, которые вам потребуются. Обратите внимание, что hello виртуального жесткого диска составляет 50 ГБ, и она займет toodownload бит его.

## <a name="is-hello-data-backed-up"></a>Hello резервное копирование данных?
Да, мы сохранить резервную копию данных пользователя hello в каждом географическом расположении. Hello данные только для чтения и может быть открыто из hello таким же, как бы обычных данных hello (обратитесь к Azure RemoteApp tooget его), если hello основного центра обработки данных не работает. Hello данные копируются в режиме реального времени toohello расположение резервной копии и не могут поддерживать копий различных версий. Таким образом, о повреждении данных, мы не будет возможности toorestore его tooa ранее правильную версию, но если hello основного центра обработки данных не работает, можно будет tooget данные пользователя из hello другое местоположение.

## <a name="how-do-users-see-hello-upd-on-hello-server-side"></a>Как пользователи увидят hello UPD на стороне сервера hello?
Каждый пользователь будет иметь свои собственные каталог на сервере hello, сопоставленное tootheir UPD: c:\Users\username.

## <a name="whats-hello-best-way-toouse-outlook-and-upd"></a>Что такое hello лучшим способом toouse Outlook и UPD?
Azure RemoteApp сохраняет состояние Outlook hello (почтовых ящиков, PST-файлы) между сеансами. tooenable это, мы должны hello toobe по тихоокеанскому времени, хранящихся в данные профиля пользователя hello (c:\users\<имя пользователя >). Это расположение по умолчанию hello hello данных, поэтому при условии, что не следует изменять расположение hello, hello данных будет сохраняться между сеансами.

Также рекомендуем использовать «кэшированный» режим в Outlook, а также режим server/online для поиска.

Дополнительные сведения об использовании Outlook и Azure RemoteApp см. в [этой статье](remoteapp-outlook.md).

## <a name="what-about-redirection"></a>Поддерживается ли перенаправление?
Можно настроить Azure RemoteApp toolet пользователям доступ к локальным устройствам, настроив [перенаправления](remoteapp-redirection.md). Локальные устройства должен быть данных hello может tooaccess на hello UPD.

## <a name="can-i-use-my-upd-as-a-network-share"></a>Можно ли использовать мой диск UPD в качестве общей сетевой папки?
Нет. Диски UPD не могут использоваться в качестве общей сетевой папки. UPD — только доступные toohello пользователь при активно hello пользователь подключен tooAzure RemoteApp.

## <a name="if-i-delete-a-user-from-a-collection-is-their-upd-deleted"></a>Если удалить пользователя из коллекции, удаляется ли также и его диск UPD?
Нет, при удалении пользователя, мы автоматически не удаляет hello UPD - вместо этого мы хранения данных hello, пока не будет удалена коллекция hello. через 90 дней после удаления коллекции hello мы удалить все UPDs. 

Если вам требуется toodelete UPD из коллекции, обратитесь в службу Azure RemoteApp - UPD можно удалить с нашей стороны.

## <a name="can-i-access-my-users-upds-either-current-or-deleted-users"></a>Можно ли получить доступ к дискам UPD моих пользователей (текущих или удаленных пользователей)?
Да, при обращении в службу [Azure RemoteApp](mailto:remoteappforum@microsoft.com), мы можем настроить вы с tooaccess URL-адрес данных hello. У вас будет о toodownload 10 часов данные или файлы из hello UPD до истечения срока действия доступа hello.

## <a name="are-upds-available-offline"></a>Доступны ли диски UPD в автономном режиме (вне сети)?
В данный момент мы не предоставляем tooUPDs автономный доступ, помимо доступа окна hello 10 часов, описанных выше. Это означает, что мы не можем сейчас tooprovide способом, с при к настолько долго, toocomplete более сложных задач, таких как на hello UPDs запущена антивирусная программа или доступа к данным для аудита.

## <a name="do-registry-key-settings-persist"></a>Сохраняются ли параметры раздела реестра?
Да, все записи tooHKEY_Current_User является частью hello UPD.

## <a name="can-i-disable-upds-for-a-collection"></a>Можно ли отключить диски UPD для коллекции?
Да, вы можете запросить Azure RemoteApp toodisable UPDs подписки, но не может выполнить самостоятельно. Это означает, что UPDs будет отключена для всех коллекций в подписке hello.

Может потребоваться UPDs toodisable в любом hello в следующих ситуациях: 

* Вам необходим полный доступ и контроль пользовательских данных (для целей аудита и проверки, например, для финансовых учреждений).
* У вас есть сторонних поставщиков пользователем профиля управления решения в локальной и хотите toocontinue их использования в развертывании Azure RemoteApp, присоединенных к домену. Это потребует hello профиль агента toobe загружается hello золотой образ. 
* Не требуется локального хранилища данных или все данные находятся в облаке или в общей папке hello и хотите toocontrol сохранения данных локально с помощью Azure RemoteApp.

Дополнительные сведения см. в записи блога [Disable User Profile Disks (UPDs) in Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) (Отключение дисков профилей пользователей в Azure RemoteApp).

## <a name="can-i-restrict-users-from-saving-data-toohello-system-drive"></a>Можно запретить пользователям сохранение данных toohello системного диска?
Да, но вам потребуется tooset, копирование в шаблоне hello изображения, прежде чем создавать коллекции hello. Используйте следующие шаги tooblock доступа toohello системный диск hello.

1. Запустите **gpedit.msc** на образ шаблона hello.
2. Перейдите в слишком**Конфигурация пользователя > Административные шаблоны > компоненты Windows > обозреватель**.
3. Выберите hello следующие параметры:
   * **Скрыть выбранные диски на моем компьютере**
   * **Запретить доступ toodrives с моего компьютера**

## <a name="can-i-seed-upds-i-want-tooput-some-data-in-hello-upd-thats-available-hello-first-time-hello-user-signs-in"></a>Могу ли я загружать данные на диски UPD? Я хочу tooput, некоторые данные в hello UPD, доступных hello первый время hello пользователь выполняет вход.
Да, при создании образа шаблона hello, можно добавить профиль по умолчанию toohello сведения. Эти сведения затем добавляется toohello UPD.

## <a name="can-i-change-hello-size-of-hello-upd-depending-on-how-much-data-i-want-toostore"></a>Можно ли изменить размер hello hello UPD в зависимости от того, сколько данных требуется toostore?
Нет, все диски UPD имеют емкость 50 ГБ. Toostore различных объемов данных, попробуйте hello следующее:

1. Отключите UPDs для hello коллекции.
2. Настройка совместного использования файла tooaccess пользователей.
3. Hello нагрузки общей папки с помощью сценария запуска. Дополнительные сведения о сценариях запуска в Azure RemoteApp см. ниже.
4. Направьте пользователей toosave все данные toohello общей папки.

## <a name="how-do-i-run-a-startup-script-in-azure-remoteapp"></a>Как выполнить сценарий запуска в Azure RemoteApp?
Toorun сценарий запуска необходимо начать путем создания запланированной задачи в образе шаблона hello ты toouse для hello коллекции. (Сделайте это *до* запуска sysprep.) 

![Создание системной задачи](./media/remoteapp-upd/upd1.png)

![Создайте системную задачу, которая запускается при входе пользователя в систему](./media/remoteapp-upd/upd2.png)

На hello **Общие** мыши будет убедиться, что hello toochange **учетной записи пользователя** в режиме безопасности слишком ««BUILTIN\Пользователи».»

![Изменить группу tooa учетной записи пользователя hello](./media/remoteapp-upd/upd4.png)

Запланированная задача Hello приведет к запуску скрипта запуска, используя учетные данные пользователя hello. Планирование задач toorun hello каждый раз, когда пользователь входит.

![Задать триггер hello для задачи hello «В журнале на»](./media/remoteapp-upd/upd3.png)

Можно также использовать [Сценарии запуска на основе групповой политики](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx). 

## <a name="what-about-placing-a-startup-script-in-hello-start-menu-would-that-work"></a>Меню «Пуск» как обстоят дела помещение скрипта запуска в hello? Это будет работать?
Другими словами можно создавать BAT-файла, которое запускает сценарий конфигурации окна и сохраните его в папку меню\Программы\Автозагрузка c:\ProgramData\Microsoft\Windows\Start toohello и иметь этот сценарий, выполняющийся при каждом запуске сеанса RemoteApp?

Нет, который не поддерживается в Azure RemoteApp, которая использует RDSH, которая также не поддерживает сценарии запуска в меню "Пуск" hello.

## <a name="can-i-use-mstscexe-hello-remote-desktop-program-tooconfigure-logon-scripts"></a>Можно использовать сценарии входа в систему tooconfigure mstsc.exe (программа hello удаленного рабочего стола)
Нет, это не поддерживается в Azure RemoteApp.

## <a name="can-i-store-data-on-hello-vm-locally"></a>Можно хранить данные на локально hello виртуальной Машины
Нет, данные, хранящиеся в любом месте на hello виртуальной Машины, отличных от в hello UPD будут потеряны. Имеется большая вероятность hello пользователь не получит hello же ВМ hello очередном входе в Azure RemoteApp. Мы не поддерживают Сохранение виртуальной Машины пользователя, поэтому hello пользователя не будут входить в одной виртуальной Машины hello и hello данные будут потеряны. Кроме того Если мы обновить коллекцию hello, существующих виртуальных машин заменяются на новый набор виртуальных машин — то есть данные, хранящиеся на самой ВМ hello приветствия будут утеряны. Hello рекомендуется toostore данные в hello UPD, общее хранилище, например файлов Azure, файловый сервер внутри виртуальной сети или в облаке hello, с помощью системы облачного хранилища, например DropBox.

## <a name="how-do-i-mount-an-azure-file-share-on-a-vm-using-powershell"></a>Как подключить общую папку Azure на виртуальной машине с помощью PowerShell?
Hello Net-PSDrive командлет toomount hello диска, можно использовать следующим образом:

    New-PSDrive -Name <drive-name> -PSProvider FileSystem -Root \\<storage-account-name>.file.core.windows.net\<share-name> -Credential :<storage-account-name>


Также можно сохранить учетные данные, выполнив следующие hello:

    cmdkey /add:<storage-account-name>.file.core.windows.net /user:<storage-account-name> /pass:<storage-account-key>


Позволяет пропустить hello - параметр учетных данных в командлет New-PSDrive hello.

