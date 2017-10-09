---
title: "aaaSet hello исходного и целевого объекта для tooAzure репликации Hyper-V (с помощью System Center VMM) с Azure Site Recovery | Документы Microsoft"
description: "Перечислены tooset действия hello исходных и целевых параметров репликации виртуальных машин Hyper-V в хранилище tooAzure облака VMM с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5edb6d87-25a5-40fe-b6f1-ddf7b55a6b31
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: 3f8c5386cb64527c775aef636980bac098ee9905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-with-vmm-replication-tooazure"></a>Шаг 8: Настройка hello исходной и целевой для tooAzure репликации Hyper-V (с помощью VMM)

После [Создание хранилища](vmm-to-azure-walkthrough-create-vault.md) и указания теми, которые хотите tooreplicate, использующие этот источник tooconfigure статьи и целевой настройки при репликации виртуальных машин Hyper-V локально в диспетчере виртуальных машин System Center (VMM) tooAzure облаков, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.

Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Настройка среды источника hello

S1. Выберите **Подготовка инфраструктуры** > **Источник**.

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. В **Подготовка источника**, нажмите кнопку **+ VMM** tooadd сервера VMM.

    ![Настройка источника](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. В **добавить сервер**, убедитесь, что **System Center VMM server** отображается в **тип сервера** , и этот сервер VMM hello соответствует hello [предварительные условия и URL-адрес требования к](#prerequisites).
4. Загрузите файл установки поставщика Azure Site Recovery hello.
5. Скачайте ключ регистрации hello. Он потребуется при запуске программы установки. Hello ключ действителен в течение пяти дней после его создания.

    ![Настройка источника](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-hello-provider-on-hello-vmm-server"></a>Установка hello поставщика на сервере VMM hello

1. Запустите файл установки поставщика hello на сервере VMM hello.
2. Обновления можно включить на странице **Центр обновления Майкрософт**. Это позволит устанавливать обновления поставщика в соответствии с политикой Центра обновления Майкрософт.
3. В **установки**примите или измените расположение установки поставщика по умолчанию hello и нажмите кнопку **установить**.

    ![Расположение установки](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. По завершении установки нажмите кнопку **зарегистрировать** tooregister hello VMM-сервера в хранилище hello.
5. В hello **параметры хранилища** щелкните **Обзор** файл ключа хранилища hello tooselect. Укажите подписку Azure Site Recovery hello и имя хранилища hello.

    ![Регистрация сервера](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. В **подключение к Интернету**, укажите, каким образом поставщик, запущенный на сервере VMM hello связь tooSite восстановления через hello hello internet.

   * Поставщик tooconnect hello напрямую, установите **подключаться напрямую tooAzure Site Recovery без учетной записи-посредника**.
   * Если существующий прокси-сервер требует проверки подлинности, либо требуется toouse настраиваемого прокси-сервера, выберите **подключения tooAzure Site Recovery с использованием прокси-сервер**.
   * При использовании настраиваемого прокси-сервера, укажите адрес hello, порт и учетные данные.
   * Если вы используете учетную запись-посредник, должны уже разрешены hello URL-адреса, описанной в [необходимых компонентов](#on-premises-prerequisites).
   * При использовании настраиваемого прокси-сервера, учетная запись VMM RunAs (DRAProxyAccount) будет создана автоматически с помощью указанного hello учетные данные прокси-сервера. Настройте hello прокси-сервера таким образом, чтобы эта учетная запись успешно проходят проверку подлинности. можно изменить параметры учетной записи запуска от имени VMM Hello в консоли VMM hello. В **параметры**, разверните **безопасности** > **учетные записи запуска от**, а затем измените hello пароль для DRAProxyAccount. Служба VMM hello toorestart потребуется, чтобы этот параметр вступает в силу.

     ![Интернет](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. Примите или измените расположение hello SSL-сертификат, который создается автоматически для шифрования данных. Этот сертификат используется в том случае, если включить шифрование данных для облака, защищаемого платформой Azure на портале Azure Site Recovery hello. Сертификат следует хранить в безопасном месте. При запуске tooAzure отработки отказа необходимо его toodecrypt, если включено шифрование данных.
8. В **имя сервера**, укажите сервер VMM hello tooidentify понятное имя в хранилище hello. В конфигурации кластера укажите имя роли кластера VMM hello.
9. Включить **синхронизация метаданных облака**, если вы хотите toosynchronize метаданные для всех облаков на сервере VMM hello hello хранилище. Это действие нужно только toohappen один раз на каждом сервере. Если вы не хотите toosynchronize все облака, можно не устанавливать флажок и синхронизировать каждое облако отдельно в свойствах облака hello в консоли VMM hello. Нажмите кнопку **зарегистрировать** toocomplete hello процесса.

    ![Регистрация сервера](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. Начнется процедура регистрации. После завершения регистрации сервера hello отображается в **инфраструктура Site Recovery** > **серверов VMM**.


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a>Установка агента служб восстановления Azure hello на узлах Hyper-V

1. После настройки hello поставщика требуется файл установки hello toodownload для агента служб восстановления Azure hello. Запустите программу установки на каждом сервере Hyper-V в облаке VMM hello.

    ![Сайты Hyper-V](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. В разделе **Проверка предварительных требований** нажмите кнопку **Далее**. Все отсутствующие предварительные требования будут установлены автоматически.

    ![Предварительные требования для агента служб восстановления](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. В **параметры установки**примите или измените расположение установки hello и расположение кэша hello. Можно настроить hello кэша на диске, не менее 5 ГБ объема хранилища, но мы рекомендуем дискового кэша более 600 ГБ свободного места. Нажмите **Install**(Установить).
4. После завершения установки нажмите кнопку **закрыть** toofinish.

    ![Регистрация агента служб восстановления Microsoft Azure](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a>Установка из командной строки
Hello агента служб восстановления Microsoft Azure можно установить из командной строки с помощью hello следующую команду:

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a>Настройка tooSite доступа к прокси-сервера Интернета восстановления из узлов Hyper-V

агент служб восстановления Hello, работающих на узлах Hyper-V должен tooAzure доступ в Интернет для репликации виртуальной Машины. Если вы обращаетесь hello Интернет через прокси, настроить его следующим образом:

1. Откройте hello Microsoft Azure Backup MMC оснастку на узле Hyper-V hello. По умолчанию для быстрого архивации Microsoft Azure доступен с рабочего стола hello или C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. В оснастке hello, нажмите кнопку **изменить свойства**.
3. На hello **конфигурация прокси-сервера** укажите сведения о сервере прокси-сервера.

    ![Регистрация агента служб восстановления Microsoft Azure](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. Проверьте, что hello агент может достигать hello URL-адреса, описанные в hello [необходимых компонентов](#on-premises-prerequisites).

## <a name="set-up-hello-target-environment"></a>Настройка целевой среды hello
Укажите toobe учетной записи хранилища Azure hello, используемым для репликации и hello toowhich сети Azure виртуальные машины Azure будут подключаться после отработки отказа.

1. Нажмите кнопку **подготовки инфраструктуры** > **целевой**, выберите подписку hello и hello группы ресурсов, место toocreate hello отработку отказа виртуальных машин. Выберите модель развертывания hello, toouse в Azure (классического или ресурса управления), необходимый для hello отработку отказа виртуальных машин.

    ![Хранилище](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. Site Recovery проверяет наличие одной или нескольких совместимых учетных записей хранения и сетей Azure.

    ![Хранилище](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. Если вы еще не создали учетную запись хранилища, и требуется toocreate один с помощью диспетчера ресурсов, щелкните **+ учетная запись хранения** toodo этой встроенной.  На hello **создать учетную запись хранения** колонке укажите имя учетной записи, тип, подписки и расположения. Учетная запись Hello должна находиться в hello местоположения hello в хранилище служб восстановления.

   ![Хранилище](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * Если вы хотите toocreate учетной записи хранилища с помощью классической модели hello, сделать это в hello портал Azure. [Дополнительные сведения](../storage/common/storage-create-storage-account.md)
   * Если вы используете учетную запись хранения premium для реплицируемых данных, настройте дополнительная Стандартная учетная запись хранения, toostore журналов репликации, захватывающих данные локальной tooon текущие изменения.
5. Если вы еще не создали сети Azure, и требуется toocreate один с помощью диспетчера ресурсов, щелкните **+ сети** toodo этой встроенной. На hello **Создание виртуальной сети** колонке укажите сетевое имя, диапазон адресов, сведения о подсети, подписки и расположения. сеть Hello должны находиться в hello местоположения hello в хранилище служб восстановления.

   ![Сеть](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   Если вы хотите toocreate сети с помощью классической модели hello, сделать это в hello портал Azure. [Подробнее](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).





## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 9: настройте сетевое сопоставление](vmm-to-azure-walkthrough-network-mapping.md)
