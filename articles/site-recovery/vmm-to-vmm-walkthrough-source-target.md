---
title: "aaaSet hello исходного и целевого объекта для Hyper-V репликации tooa вторичного сайта с помощью Azure Site Recovery | Документы Microsoft"
description: "Описывает, как tooset вверх hello исходный и целевой при репликации виртуальных машин Hyper-V сайта toosecondary VMM с помощью Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a>Шаг 6: Настройка hello репликации исходной и целевой


После создания службы восстановления хранилище для Hyper-V репликации tooa вторичный сайт VMM с [Azure Site Recovery](site-recovery-overview.md), использование этой статьи tooset источник hello и целевые расположения для репликации. 

После считывания в этой статье, отправлять любые комментарии, внизу hello, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="set-up-hello-source-environment"></a>Настройка среды источника hello

Установите hello поставщика Azure Site Recovery на серверах VMM и обнаружение и регистрации серверов в хранилище hello.

1. Щелкните **Шаг 1. Подготовка инфраструктуры** > **Источник**.

    ![Настройка источника](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. В **Подготовка источника**, нажмите кнопку **+ VMM** tooadd сервера VMM.

    ![Настройка источника](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. В **добавить сервер**, убедитесь, что **System Center VMM server** отображается в **тип сервера** , и этот сервер VMM hello соответствует hello [необходимые компоненты](#prerequisites).
4. Загрузите файл установки поставщика Azure Site Recovery hello.
5. Скачайте ключ регистрации hello. Он потребуется при запуске программы установки. Hello ключ действителен в течение пяти дней после его создания.

    ![Настройка источника](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. Установите hello поставщика Azure Site Recovery на сервере VMM hello. Не нужно ничего устанавливать tooexplicitly на серверах узлов Hyper-V.


## <a name="install-hello-azure-site-recovery-provider"></a>Установка поставщика Azure Site Recovery hello

1. Запустите файл установки поставщика hello на каждом сервере VMM. Если VMM развертывается в кластере, следующие hello hello при первом запуске установки:
    -  Установите hello поставщик на активном узле и окончания сервера hello установки tooregister hello VMM в хранилище hello.
    - Затем установите hello поставщика на hello другие узлы. Узлы кластера следует запускать hello ту же версию hello поставщика.
2. Программа установки выполняет ряд проверок необходимых компонентов и запрашивает разрешение toostop hello VMM службы. Hello службы VMM будет автоматически перезапущена после завершения программы установки. При установке на кластере VMM вы запрашиваемые toostop hello кластерной роли.
3. В **центра обновления Майкрософт**, вы можете выбрать в toospecify, что поставщик обновления устанавливаются в соответствии с политикой центра обновления Майкрософт.
4. В **установки**, примите или измените расположение установки по умолчанию hello и нажмите кнопку **установить**.

    ![Расположение установки](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. После завершения установки нажмите кнопку **зарегистрировать** tooregister hello сервера в хранилище hello.

    ![Расположение установки](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. В **имя хранилища**, проверьте имя hello hello хранилища, в которых hello будет зарегистрирован сервер. Щелкните *Далее*.

    ![Регистрация сервера](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. В **подключение к Интернету**, укажите способ подключения hello поставщик, запущенный на сервере VMM hello tooAzure.

    ![Параметры Интернета](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - Можно указать, поставщик hello следует подключаться напрямую toohello Интернет, или с помощью учетной записи-посредника.
   - При необходимости задайте параметры прокси-сервера.
   - При использовании прокси-сервер, учетная запись VMM RunAs (DRAProxyAccount) создается автоматически с использованием указанного hello учетные данные прокси-сервера. Настройте hello прокси-сервера таким образом, чтобы эта учетная запись успешно проходят проверку подлинности. Hello параметры учетной записи запуска от имени можно изменить в консоли VMM hello > **параметры** > **безопасности** > **учетные записи запуска от**. Перезапустите службы tooupdate hello VMM изменения.
8. В **регистрационный ключ**выберите ключ hello, загружаются из Azure Site Recovery и копируются toohello сервера VMM.
9. параметр шифрования Hello используется только при репликации виртуальных машин Hyper-V в облаках tooAzure VMM. Если выполняется репликация tooa вторичного сайта она не используется.
10. В **имя сервера**, укажите сервер VMM hello tooidentify понятное имя в хранилище hello. В конфигурации кластера укажите имя роли кластера VMM hello.
11. В **синхронизация метаданных облака**выберите, следует ли использовать toosynchronize метаданные для всех облаков на сервере VMM hello hello хранилище. Это действие нужно только toohappen один раз на каждом сервере. Если вы не хотите toosynchronize все облака, можно не устанавливать флажок и синхронизировать каждое облако отдельно в свойствах облака hello в консоли VMM hello.
12. Нажмите кнопку **Далее** toocomplete hello процесса. После регистрации службой Azure Site Recovery извлекает метаданные с сервера VMM hello. сервер Hello отображается на hello **серверов VMM** вкладку на hello **серверы** страницы в хранилище hello.

    ![сервер;](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. После hello сервер доступен в консоли восстановления сайта hello в **источника** > **Подготовка источника** выберите сервер VMM hello и выберите hello облака, в какие hello Hyper-V находится узел. Нажмите кнопку **ОК**.

Также можно установить поставщик hello hello командной строке:

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Настройка целевой среды hello

Выберите целевой сервер VMM hello и облака.

1. Нажмите кнопку **подготовки инфраструктуры** > **целевой**и выберите hello целевой сервер VMM требуется toouse.
2. Будут отображены облаков на сервере hello, которые синхронизируются с Site Recovery. Выберите целевое облако hello.

   ![Цель](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 7: Настройка сетевого сопоставления](vmm-to-vmm-walkthrough-network-mapping.md).
