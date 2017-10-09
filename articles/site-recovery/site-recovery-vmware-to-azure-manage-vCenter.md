---
title: " Управление сервером VMware vCenter Server в Azure Site Recovery | Документация Майкрософт"
description: "В этой статье описывается добавление и администрирование сервера VMware vCenter Server в Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 5be995f137d0c0efaf3050b5366a107098cae15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-vmware-vcenter-server-in-azure-site-recovery"></a>Управление сервером VMware vCenter Server в Azure Site Recovery
В этой статье описывается hello различные операции восстановления сайта, которые могут быть выполнены на VMware vCenter.

## <a name="prerequisites"></a>Предварительные требования

**Поддержка сервера VMware vCenter Server и узла VMware vSphere ESX** | **Дополнительные сведения** |
|--- | --- |
|**Локальные серверы VMware** | Один или несколько серверов VMware vSphere (версии 6.0, 5.5 или 5.1 с последними обновлениями). Серверы должны находиться в hello сетевых как hello конфигурации сервера (или отдельный сервер обработки).<br/><br/> Корпорация Майкрософт рекомендует vCenter server toomanage узлов под управлением версии 6.0 или 5.5 с последними обновлениями hello. При развертывании версии 6.0 поддерживаются только функции, доступные в версии 5.5.|

## <a name="prepare-an-account-for-automatic-discovery"></a>Подготовка учетной записи для автоматического обнаружения
Site Recovery должен tooVMware доступ для hello процесса сервера tooautomatically обнаружение виртуальных машин, а также для отработки отказа и восстановления размещения виртуальных машин.

* **Перенос**: Если требуется только tooAzure виртуальных машин VMware toomigrate, без когда-либо ошибок их обратно, можно использовать учетную запись VMware с ролью только для чтения. Такая роль позволяет выполнять отработку отказа только без выключения исходных защищенных компьютеров. Это не является обязательным для переноса.
* **Реплицировать или восстановить**: Если вы хотите toodeploy полной репликации (репликация, отработки отказа, восстановление после сбоя) hello, учетная запись должна быть может toorun операций, таких как создание и удаление дисков, при включении виртуальной машины.
* **Автоматическое обнаружение** — требуется по крайней мере учетная запись только для чтения.


|**Задачи** | **Требуемая учетная запись или роль** | **Разрешения** | **Дополнительные сведения**|
|--- | --- | --- | ---|
|**Сервер обработки автоматически обнаруживает виртуальные машины VMware** | Потребуется по крайней мере пользователь только для чтения | Центр обработки данных объекта –> Propagate tooChild объекта, роль = только для чтения | Пользователь назначаются на уровне центра обработки данных и не имеет доступа tooall hello объектов в центре обработки данных hello.<br/><br/> toorestrict доступ, назначьте hello **нет доступа** роль с hello **распространение toochild** объекта toohello дочерние объекты (узлы vSphere, хранилища данных, виртуальные машины и сети).|
|**Тип отработки отказа** | Потребуется по крайней мере пользователь только для чтения | Центр обработки данных объекта –> Propagate tooChild объекта, роль = только для чтения | Пользователь назначаются на уровне центра обработки данных и не имеет доступа tooall hello объектов в центре обработки данных hello.<br/><br/> toorestrict доступ, назначьте hello **нет доступа** роль с hello **распространение toochild** объекта toohello дочерние объекты (узлы vSphere, хранилища данных, виртуальные машины и сети).<br/><br/> Это полезно для сценария переноса, но не подходит для полной репликации, отработки отказа и восстановления размещения.|
|**Отработка отказа и восстановление размещения** | Мы рекомендуем вам создать роль (AzureSiteRecoveryRole) с hello необходимые разрешения, а затем назначьте tooa VMware hello роли пользователя или группы | Центр обработки данных объекта –> Propagate tooChild объекта, роль = AzureSiteRecoveryRole<br/><br/> Хранилище данных -> выделение места, обзор хранилища данных, низкоуровневые операции с файлами, удаление файлов, обновление файлов виртуальной машины<br/><br/> Сеть -> Назначение сети<br/><br/> Ресурс "->" пул tooresource назначить виртуальной Машине, перенести отключенные на виртуальной Машине, перенести питание на виртуальной Машине<br/><br/> Задачи -> Создание задач, Обновление задач<br/><br/> Виртуальная машина -> конфигурация<br/><br/> Виртуальная машина -> взаимодействие -> ответ на вопрос, подключение устройства, настройка компакт-диска носителя, настройка дискеты носителя, отключение, включение, установка средств VMware<br/><br/> Виртуальная машина -> инвентаризация -> создание, регистрация, отмена регистрации<br/><br/> Виртуальная машина -> подготовка -> разрешение загрузки виртуальной машины, разрешение отправки файлов виртуальной машины<br/><br/> виртуальная машина -> моментальные снимки -> удаление моментальных снимков. | Пользователь назначаются на уровне центра обработки данных и не имеет доступа tooall hello объектов в центре обработки данных hello.<br/><br/> toorestrict доступ, назначьте hello **нет доступа** роль с hello **распространение toochild** объекта toohello дочерние объекты (узлы vSphere, хранилища данных, виртуальные машины и сети).|

## <a name="create-an-account-tooconnect-toovmware-vcenter-server-vmware-vsphere-exsi-host"></a>Создание учетной записи tooconnect tooVMware vCenter Server или VMware vSphere EXSi узла
1. Имя входа в hello конфигурации сервера и запустите hello cspsconfigtool.exe с помощью ярлыка hello обмена hello рабочего стола.
2. Нажмите кнопку **Добавление учетной записи** на hello **Управление учетной записью** вкладки.

  ![add-account](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Укажите сведения учетной записи hello и нажмите кнопку ОК tooadd hello счета. Hello учетная запись должна иметь привилегии hello, перечисленные в hello [подготовить учетную запись для автоматического обнаружения](#prepare-an-account-for-automatic-discovery) раздела.

  >[!NOTE]
  Он занимает около 15 минут для hello учетной записи сведения toobe синхронизации со службой восстановления сайтов hello.


## <a name="associate-a-vmware-vcenter-vmware-vsphere-esx-host-add-vcenter"></a>Связывание сервера VMware vCenter Server или узла VMware vSphere ESX (в разделе "Добавить vCenter Server")
* В случае hello портал Azure — Обзор слишком*YourRecoveryServicesVault* > **инфраструктура Site Recovery** > **серверов конфигураций**  >  *ConfigurationServer*
* Страница сведений о конфигурации сервера hello щелкните hello + vCenter кнопки.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

## <a name="modify-credentials-used-tooconnect-toohello-vcenter-server-vsphere-esxi-host"></a>Изменить учетные данные, используемые tooconnect toohello vCenter server или узла ESXi vSphere

1. Имя входа в hello конфигурации сервера и запустите hello cspsconfigtool.exe
2. Нажмите кнопку **Добавление учетной записи** на hello **Управление учетной записью** вкладки.

  ![add-account](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Укажите hello новые данные учетных записей и нажмите кнопку ОК tooadd hello счета. Hello учетная запись должна иметь привилегии hello, перечисленные в hello [подготовить учетную запись для автоматического обнаружения](#prepare-an-account-for-automatic-discovery) раздела.
4. В случае hello портал Azure — Обзор слишком*YourRecoveryServicesVault* > **инфраструктура Site Recovery** > **серверов конфигураций**  >  *ConfigurationServer*
5. На странице сведений о конфигурации сервера hello щелкните hello **обновление сервера** кнопки.
6. После завершения задания сервера hello обновления выберите hello vCenter Server tooopen hello vCenter страница «Сводка».
7. Выберите hello добавления учетной записи в hello **учетной записи узла vCenter server/vSphere** поле и нажмите кнопку hello **Сохранить** кнопки.

  ![modify-account](./media/site-recovery-vmware-to-azure-manage-vcenter/modify-vcente-creds.png)

## <a name="delete-a-vcenter-in-azure-site-recovery"></a>Удаление сервера vCenter Server в Azure Site Recovery
1. В случае hello портал Azure — Обзор слишком*YourRecoveryServicesVault* > **инфраструктура Site Recovery** > **серверов конфигураций**  >  *ConfigurationServer*
2. Сервер конфигурации hello сведения о странице выберите hello vCenter Server tooopen hello vCenter страница «Сводка».
3. Щелкните hello **удалить** кнопку toodelete hello vCenter

  ![delete-account](./media/site-recovery-vmware-to-azure-manage-vcenter/delete-vcenter.png)

> [!NOTE]
Если необходимо toomodify hello v-Center IP адрес или полное доменное имя, сведения о портах, то требуется toodelete hello vCenter Server и снова добавьте его снова.
