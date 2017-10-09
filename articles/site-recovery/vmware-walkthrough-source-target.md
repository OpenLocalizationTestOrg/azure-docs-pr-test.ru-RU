---
title: "aaaSet hello исходного и целевого объекта для VMware tooAzure репликации с помощью Azure Site Recovery | Документы Microsoft"
description: "Перечислены tooset действия hello исходных и целевых параметров репликации виртуальных машин VMware tooAzure хранилища с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a>Шаг 8: Настройка hello исходной и целевой для VMware tooAzure репликации

В этой статье описывается, как tooconfigure источника и целевых параметров при репликации локально tooAzure виртуальные машины VMware, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.

Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Настройка среды источника hello

Настройка сервера конфигурации hello, зарегистрируйте его в хранилище hello и обнаружение виртуальных машин.

1. Щелкните **Site Recovery** > **Шаг 1. Подготовка инфраструктуры** > **Источник**.
2. Если у вас нет сервера конфигурации, щелкните **+Configuration server** (+ Сервер конфигурации).
3. В колонке **Добавление сервера** в поле **Тип сервера** должно быть указано **Сервер конфигурации**.
4. Загрузите файл установки hello установка единой Site Recovery.
5. Загрузите ключ регистрации в хранилище hello. Он потребуется при запуске единой установки. Hello ключ действителен в течение пяти дней после его создания.

   ![Настройка источника](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Зарегистрируйте сервер конфигурации hello в хранилище hello

Следующие hello, прежде чем начать, а затем выполните tooinstall hello конфигурации сервера, сервера обработки hello и главный целевой сервер hello единой программы установки.
    - Посмотрите краткий видеообзор:

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - На сервере конфигурации hello виртуальной Машины, убедитесь, что системные часы, hello синхронизируется с [сервер времени](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Значения времени должны совпадать. Если системные часы отстают или спешат в пределах 15 минут, установка может завершиться ошибкой.
    - Запустите программу установки с учетной записью локального администратора на сервере hello конфигурации виртуальной Машины.
    - Убедитесь в том, что протоколы TLS 1.0 включен в hello виртуальной Машины.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> также можно установить сервер конфигурации Hello [из командной строки hello](http://aka.ms/installconfigsrv).



## <a name="connect-toovmware-servers"></a>Подключение серверов tooVMware

tooallow Azure Site Recovery toodiscover виртуальных машин, работающих в локальной среде, необходимо tooconnect VMware vCenter Server или узлы vSphere ESXi с Site Recovery. Прежде чем начать, обратите внимание hello следующие:

- При добавлении сервера vCenter hello или узлы vSphere tooSite восстановления с помощью учетной записи без прав администратора на сервере hello, учетная запись hello должна включены следующие права доступа:
    - привилегии центра обработки данных, хранилища данных, папки, узла, сети, ресурса, виртуальной машины и распределенного коммутатора vSphere;
    - сервер vCenter Hello необходимы разрешения представления хранилища.
- При добавлении серверов VMware tooSite восстановления может потребоваться 15 минут или больше времени для них tooappear hello портала.

### <a name="add-hello-account-for-automatic-discovery"></a>Добавьте учетную запись hello автоматического обнаружения

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a>Настройка подключения

Подключение tooservers следующим образом:

1. Выберите **+ vCenter** toostart подключение сервера VMware vCenter server или узла ESXi VMware vSphere.
2. В **добавьте vCenter**, укажите понятное имя для сервера узла или vCenter vSphere hello, а затем укажите hello IP-адрес или полное доменное имя сервера hello.
3. Если серверы VMware, настроенных toolisten для запросов на другой порт оставьте hello порт 443. Выберите учетную запись hello tooconnect toohello VMware vCenter или vSphere ESXi сервера. Нажмите кнопку **ОК**.
4. Site Recovery подключает tooVMware серверы с помощью hello указаны параметры и выполняет обнаружение виртуальных машин.

> [!NOTE]
> При добавлении сервера или узел с учетной записью, не имеет прав администратора на сервере vCenter или узла hello, убедитесь, что учетная запись hello имеет включены следующие права доступа: центра обработки данных, хранилище данных, папки, узла, сети, ресурс виртуальной машины и vSphere распределенных коммутатора. Кроме того hello VMware vCenter server должен включены привилегий представления хранилища hello.


## <a name="set-up-hello-target-environment"></a>Настройка целевой среды hello

Перед настройкой hello целевой среде, убедитесь, что у вас есть учетная запись хранения Azure и настройка виртуальной сети.

1. Нажмите кнопку **подготовки инфраструктуры** > **целевой**, и выберите hello требуется toouse подписки Azure.
2. Укажите, какая целевая модель развертывания используется: классическая или Resource Manager.
3. Site Recovery проверяет наличие одной или нескольких совместимых учетных записей хранения и сетей Azure.

   ![Цель](./media/vmware-walkthrough-source-target/gs-target.png)
4. Если вы еще не создали учетную запись хранения или сети, нажмите кнопку **+ учетная запись хранения** или **+ сети**, toocreate диспетчера ресурсов учетной записи или сети встроенной.

## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 9: настроить политику репликации](vmware-walkthrough-replication.md)
