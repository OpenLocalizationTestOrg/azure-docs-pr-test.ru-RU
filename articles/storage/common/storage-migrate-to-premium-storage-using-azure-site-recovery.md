---
title: "aaaMigrating tooAzure хранилища Premium, с помощью Azure Site Recovery (неуправляемой диски) | Документы Microsoft"
description: "Перенос вашей существующие виртуальные машины tooAzure хранилище Premium с помощью Site Recovery (неуправляемой диски)."
services: storage
documentationcenter: 
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: luywang
ms.openlocfilehash: 2c82fffaa38baeeb4a676748125bd85d6e0500f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-toopremium-storage-using-azure-site-recovery-unmanaged-disks"></a>Миграция tooPremium хранилища с помощью Azure Site Recovery (неуправляемой диски)

[Хранилище Azure класса Premium](storage-premium-storage.md) обеспечивает поддержку дисков с высокой производительностью и малой задержкой для виртуальных машин с интенсивной рабочей нагрузкой ввода-вывода. Hello данное руководство служит пользователям toohelp перенос их дисков виртуальной Машины в tooa учетных записей стандартного хранилища учетной записи хранения Premium с помощью [Azure Site Recovery](../../site-recovery/site-recovery-overview.md).

Site Recovery — это служба Azure, вклада tooyour непрерывность бизнеса и стратегии аварийного восстановления, управляя операциями hello репликации локальных физических серверов и облако виртуальных машин toohello (Azure) или tooa дополнительный центр обработки данных. При возникновении сбоев в расположении первичной, переключением toohello вторичное расположение tookeep приложений и рабочих нагрузок доступны. При toonormal операция возвращает сбой задней tooyour первичного расположения. Site Recovery предоставляет отработки отказа toosupport аварийного восстановления без влияния на рабочих средах. Вы можете выполнять отработки отказа с минимальной потерей данных (в зависимости от частоты репликации) в случае непредвиденных аварий. В сценарии hello миграция tooPremium хранилища, можно использовать hello [перехода на другой ресурс в Site Recovery](../../site-recovery/site-recovery-failover.md) в Azure Site Recovery toomigrate целевой дисков tooa учетной записи хранения Premium.

Мы рекомендуем перейти tooPremium хранилища с помощью Site Recovery, так как этот параметр обеспечивает минимальное время простоя и позволяет избежать ручного выполнения копирования дисков и создание новых виртуальных машин hello. В ходе отработки отказа Site Recovery будет систематически копировать диски и создавать новые виртуальные машины. Site Recovery поддерживает несколько типов отработки отказа — без простоя или с минимальным простоем. tooplan вашей время простоя и оценка потери данных. в разделе hello [типы отработки отказа](../../site-recovery/site-recovery-failover.md) таблицы в Site Recovery. Если вы [Подготовка tooconnect tooAzure виртуальных машин после отработки отказа](../../site-recovery/vmware-walkthrough-overview.md), должно быть возможности tooconnect toohello ВМ Azure с помощью протокола удаленного рабочего СТОЛА, после отработки отказа.

![][1]

## <a name="azure-site-recovery-components"></a>Компоненты Azure Site Recovery

Это компоненты hello Site Recovery, соответствующие toothis сценария миграции.

* **Сервер конфигурации** — виртуальная машина Azure, которая координирует обмен данными и управляет процессами репликации и восстановления данных. На этой виртуальной Машины будет выполняться сервере одиночной установки hello tooinstall файлов конфигурации и дополнительный компонент, называется сервером процессу, как шлюз репликации. См. дополнительные сведения о [требованиях к серверу конфигурации](../../site-recovery/vmware-walkthrough-overview.md). Сервер конфигурации необходимо настроить один раз toobe и может использоваться для всех toohello миграций одного региона.

* **Сервер обработки** репликации шлюза, который получает данные репликации из источника виртуальных машин оптимизирует hello данных с помощью кэширования, сжатия и шифрования, и отправляет его tooa учетной записи хранилища. Также обрабатывает принудительной установки toosource службы hello мобильность виртуальных машин и выполняет автоматическое обнаружение источника виртуальных машин. сервер обработки по умолчанию Hello устанавливается на сервере конфигурации hello. Вы можете развернуть серверы tooscale дополнительных автономный процесс развертывания. Ознакомьтесь с [рекомендациями по развертыванию сервера обработки](https://azure.microsoft.com/blog/best-practices-for-process-server-deployment-when-protecting-vmware-and-physical-workloads-with-azure-site-recovery/) и [дополнительных серверов обработки](../../site-recovery/site-recovery-plan-capacity-vmware.md#deploy-additional-process-servers). Сервер обработки требуется toobe настроить один раз и может использоваться для всех toohello миграции одного региона.

* **Служба мобильности** — это компонент, который развертывается на каждом Стандартная виртуальная машина будет tooreplicate. Он получает запись данных на hello Стандартная виртуальная машина и пересылает их toohello сервер обработки. Ознакомьтесь с [предварительными требованиями для реплицируемых компьютеров](../../site-recovery/vmware-walkthrough-overview.md).

На этом рисунке показано, как взаимодействуют эти компоненты.

![][15]

> [!NOTE]
> Site Recovery не поддерживает миграцию hello дисков дисковых пространств.

Дополнительные компоненты для других сценариев, можно найти слишком[архитектура сценария](../../site-recovery/vmware-walkthrough-overview.md).

## <a name="azure-essentials"></a>Основные компоненты Azure

Они являются hello Azure требования для данного сценария миграции.

* Подписка Azure
* Данные, реплицированные toostore учетной записи хранилища Azure Premium
* Toowhich виртуальной сети (VNet) Azure виртуальные машины будут подключаться, когда они создаются на переход на другой ресурс. Hello виртуальной сети Azure должны находиться в hello же регионе, как один в какой hello Site Recovery работает hello
* Azure Стандартная учетная запись хранения в какие журналы toostore репликации. Это может быть hello учетную запись хранения, как диски виртуальной Машины hello переносимым

## <a name="prerequisites"></a>Предварительные требования

* Понимать, какие hello миграции соответствующие сценарии компонентов в предшествующих раздел hello
* Планировать время отключения путем изучения о hello [отработки отказа в службе восстановления сайтов](../../site-recovery/site-recovery-failover.md)

## <a name="setup-and-migration-steps"></a>Этапы настройки и переноса данных

Site Recovery toomigrate ВМ IaaS Azure можно использовать между регионами или в одном регионе. Hello следующие инструкции были специально созданных этот сценарий миграции из статьи hello [репликацию виртуальных машин VMware или физическими серверами tooAzure](../../site-recovery/vmware-walkthrough-overview.md). Следуйте hello содержатся ссылки на подробные действия в инструкциях дополнительных toohello в этой статье.

1. **Создание хранилища служб восстановления**. Создание и управление хранилищем восстановления сайта hello через hello [портал Azure](https://portal.azure.com). Щелкните **Создать** > **Управление** > **Архивация** и **Site Recovery (OMS)**. Также можно щелкнуть **Обзор** > **Хранилище служб восстановления** > **Добавить**. Виртуальные машины будут реплицированных toohello область, указанная в этом шаге. В целях миграции в hello hello же регионе, выберите hello области источника виртуальных машин и хранилища исходных учетных записей. 

2. Hello следующие действия помогут **выберите ваши цели защиты**.

    2.1. На hello место tooinstall hello конфигурации сервера виртуальной Машины, откройте hello [портал Azure](https://portal.azure.com). Go слишком**хранилищ служб восстановления** > **параметры**. В разделе **Параметры** выберите **Site Recovery**. В разделе **Site Recovery** выберите **Шаг 1. Подготовка инфраструктуры**. В разделе **Подготовка инфраструктуры** выберите **Цель защиты**.

    ![][2]

    2.2. В разделе **цель защиты**в первом раскрывающемся списке hello, выберите **tooAzure**. Выберите в раскрывающемся списке второй hello **не виртуализированных, другие**, а затем нажмите кнопку **ОК**.

    ![][3]

3. Hello следующие действия помогут **Настройка среды hello источник (сервер конфигурации)**.

    3.1. Загрузите hello **Установка Azure Site Recovery единой** и hello **ключ регистрации в хранилище** с переходом toohello **подготовки инфраструктуры**  >  **Подготовка источника** > **добавить сервер** колонку. Вам потребуется hello настройкой hello единой toorun ключа регистрации хранилища. Hello ключ действителен в течение 5 дней после его создания.

    ![][4]

    3.2. Добавление конфигурации сервера в hello **добавить сервер** колонку.

    ![][5]

    3.3. Запустите на hello виртуальной Машины используется в качестве сервера конфигурации hello единой установки tooinstall hello конфигурации сервера и сервера обработки hello. Вы можете выполнить снимки экрана приветствия [здесь](../../site-recovery/vmware-walkthrough-overview.md) toocomplete hello установки. Можно ссылаться toohello следующие снимки экрана для действия, описанные в этом сценарии миграции.

    В **перед началом**выберите **установить hello конфигурации сервера и сервера обработки**.

    ![][6]

    3.4. В **регистрации**перейдите и выберите ключ регистрации hello, загруженный из хранилища hello.

    ![][7]

    3.5. В **подробные сведения о среде**укажите, требуется ли ты tooreplicate виртуальных машин VMware. В данном случае выберите **Нет**.

    ![][8]

    3.6. После завершения установки hello, вы увидите hello **сервера к конфигурации восстановления сайта Microsoft Azure** окна. Использовать hello **управление учетными записями** вкладке hello toocreate учетную запись, которая Site Recovery можно использовать для автоматического обнаружения. (В случае hello о защите физические компьютеры, Настройка учетной записи hello не имеет значения, но требуется по крайней мере один учетной записи tooenable один из шагов hello. В этом случае можно назвать hello учетной записи и пароля любым.) Используйте hello **регистрации хранилища** файл вкладку tooupload hello хранилища учетных данных.

    ![][9]

4. **Настройка целевой среды hello**. Нажмите кнопку **подготовки инфраструктуры** > **целевой**и укажите hello развертывания модель будет toouse для виртуальных машин после отработки отказа. В зависимости от конкретного сценария можно выбрать **классическую модель** или **модель развертывания Resource Manager**.

    ![][10]

    Site Recovery проверяет наличие одной или нескольких совместимых учетных записей хранения и сетей Azure. Обратите внимание, что если вы используете учетную запись хранения Premium для реплицируемых данных, tooset репликацию учетной записи toostore дополнительных стандартное хранилище журналов.

5. **Настройте параметры репликации**. Следуйте инструкциям в [настроить параметры репликации](../../site-recovery/vmware-walkthrough-overview.md) tooverify, сервер конфигурации успешно связан с политикой репликации hello, вы создаете.

6. **Планирование ресурсов**. Используйте hello [планировщик ресурсов](../../site-recovery/site-recovery-capacity-planner.md) должен tooaccurately оценки пропускной способности сети, хранилища и toomeet другие требования к репликации. После этого в поле **Вы выполнили планирование ресурсов?** выберите **Да**.

    ![][11]

7. Hello следующие действия помогут **установки службы mobility service и включить репликацию**.

    7.1. Вы можете слишком[Принудительная установка](../../site-recovery/vmware-walkthrough-overview.md) tooyour источника виртуальных машин или слишком[вручную установить службу mobility](../../site-recovery/site-recovery-vmware-to-azure-install-mob-svc.md) на источнике виртуальных машин. Требование hello проталкивания установки и пути hello hello вручную установщика можно найти в ссылке hello. Если вы выполняете установку вручную, может потребоваться toouse внутренний IP-адрес toofind hello конфигурации сервера.

    ![][12]

    Hello отработка отказа виртуальной Машины будет иметь два временных диска: один из hello основной виртуальной Машины и hello других создан во время подготовки виртуальной Машины в регионе восстановления hello hello. временный диск tooexclude hello до репликации, установите hello mobility service, прежде чем включать репликации. toolearn Дополнительные сведения о как tooexclude hello временный диск ссылаться слишком[исключить из репликации дисков](../../site-recovery/vmware-walkthrough-overview.md).

    7.2. Включите репликацию следующим образом:
      * Выберите **Репликация приложения** > **Источник**. После включения репликации hello первый раз, нажмите кнопку + репликации в репликации tooenable hello хранилище для дополнительных компьютеров.
      * На шаге 1 выберите в качестве источника сервер обработки.
      * На шаге 2 укажите модель развертывания после отработки отказа hello, toomigrate учетной записи хранения Premium, чтобы, журналы toosave стандартное хранилище учетной записи и toofail виртуальной сети для.
      * На шаге 3, добавьте защищенных виртуальных машин, IP-адрес (Внутренняя toofind IP-адрес может потребоваться их).
      * На шаге 4 настройте свойства hello, выбрав hello учетные записи, установленные ранее на сервере обработки hello.
      * На шаге 5 выберите политику репликации hello, созданный ранее, Настройка параметров репликации.
      Нажмите кнопку **ОК** и включите репликацию.

    > [!NOTE]
    > Когда ВМ Azure освобождается и снова запустить, нет гарантии, он получит hello же IP-адрес. Если hello IP-адрес сервера server или процесс конфигурации hello или hello защищенных виртуальных машинах Azure изменений, репликации hello в этом случае могут работать неправильно.

    ![][13]

    При разработке среды службы хранилища Azure для каждой виртуальной машины в группе доступности рекомендуется использовать отдельные учетные записи хранения. Мы рекомендуем слишком следуйте рекомендациям по hello на уровне хранилища hello[использование нескольких учетных записей хранения для каждого набора доступности](../../virtual-machines/windows/manage-availability.md). Распространение учетных записей хранения toomultiple дисков виртуальной Машины помогает tooimprove доступности хранилища и распределяет инфраструктуры хранилища Azure hello hello ввода-вывода. Если виртуальные машины находятся в наборе доступности, вместо репликации дисков всех виртуальных машин в одну учетную запись хранения, корпорация Майкрософт рекомендует миграцию нескольких виртуальных машин несколько раз, чтобы виртуальные машины hello в hello же группы доступности не имеют одной учетной записи хранения. Используйте hello **включить репликацию** tooset колонке назначения учетной записи хранилища для каждой виртуальной Машины, по одному. Можно выбрать модель развертывания после отработки отказа, в соответствии с tooyour необходимость. При выборе диспетчера ресурсов (RM) в качестве используемой модели развертывания после отработки отказа можно выполнить переход виртуальной Машины RM tooan RM виртуальной Машины или можно выполнить переход классический tooan ВМ RM виртуальной Машины.

8. **Выполнение тестовой отработки отказа**. toocheck ли ваш репликация не завершится, нажмите кнопку восстановления сайта и нажмите кнопку **параметры** > **реплицируются элементы**. Вы увидите состояние hello и процент процесс репликации. После начальной репликации не завершено, запустите тестовую отработку отказа toovalidate стратегии репликации. Подробное описание шагов теста отработки отказа см. слишком[выполнить тестовую отработку отказа в Site Recovery](../../site-recovery/vmware-walkthrough-overview.md). Вы можете просматривать состояние hello теста отработки отказа в **параметры** > **заданий** > **YOUR_FAILOVER_PLAN_NAME**. В колонке hello вы увидите декомпозиция hello шаги и результаты успешных завершений и сбоев. В случае hello тестовой отработки отказа на любом этапе щелкните сообщение hello шаг toocheck hello. Убедитесь, что виртуальные машины и стратегии репликации требованиям hello перед запуском отработки отказа. Чтение [tooAzure тестовой отработки отказа в Site Recovery](../../site-recovery/site-recovery-test-failover-to-azure.md) Дополнительные сведения и инструкции теста отработки отказа.

9. **Запустите отработку отказа**. По завершении тестовой отработки отказа hello запустите toomigrate отработки отказа вашей tooPremium дисков хранилища и реплицировать hello экземпляров виртуальных Машин. Следуйте инструкциям hello подробные инструкции в [запуск отработки отказа](../../site-recovery/site-recovery-failover.md#run-a-failover). Необходимо выбрать **выключить виртуальные машины и синхронизировать последние данные hello** toospecify что Site Recovery следует повторите tooshut вниз hello защищенных виртуальных машин и синхронизацию данных hello hello последнюю версию данных hello отработка отказа будет выполняться. Если этот параметр не выбран или не удалась попытка hello hello отработки отказа будет hello последней доступной точки восстановления для виртуальной Машины hello. Site Recovery создаст экземпляр виртуальной Машины, тип которого — hello, совпадает или аналогичные tooa Premium функцией хранилища виртуальной Машины. Можно проверить производительность hello и цены различных экземпляров виртуальных Машин, перейдя слишком[расценки на виртуальные машины Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) или [расценки на виртуальные машины Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/).

## <a name="post-migration-steps"></a>Действия после переноса данных

1. **Настройка реплицированные виртуальные машины toohello доступности, если применимо**. Site Recovery не поддерживает перенос виртуальных машин вместе с hello группы доступности. В зависимости от развертывания hello реплицированной виртуальной Машины выполните одно из следующих hello.
  * Для виртуальной Машины, созданные с помощью hello классической модели развертывания: Добавление доступности toohello hello виртуальной Машины в hello портал Azure. Подробные инструкции см. слишком[добавить существующую группу доступности виртуальной машины tooan](../../virtual-machines/windows/classic/configure-availability.md#addmachine).
  * Для модели развертывания диспетчера ресурсов hello: сохранить конфигурацию hello виртуальной Машины и затем удалите и повторно создать виртуальные машины hello в наборе доступности hello. toodo таким образом, используйте сценарий hello в [набор ресурсов диспетчера виртуальных Машин группе доступности Azure](https://gallery.technet.microsoft.com/Set-Azure-Resource-Manager-f7509ec4). Проверьте ограничение hello этого сценария и планировать время простоя перед выполнением сценария hello.

2. **Удаление старых виртуальных машин и дисков**. Прежде чем удалять их, убедитесь, что диски Premium hello являются соответствующим исходных дисков и hello новые виртуальные машины выполнения hello же выступать в роли источника hello виртуальных машин. В модели развертывания диспетчера ресурсов (RM) hello удаление hello виртуальной Машины и удаление hello дисков из учетных записей хранилища источника в hello портал Azure. Hello классической модели развертывания можно удалить hello ВМ и дисков в классическом портале hello или портал Azure. Если имеется проблема в какой hello диск не удален, несмотря на то, что вы удалили hello виртуальной Машины, см. в разделе [Устранение ошибок при удалении VHD](storage-resource-manager-cannot-delete-storage-account-container-vhd.md).

3. **Очистить hello инфраструктуры Azure Site Recovery**. Если восстановление сайта больше не требуется, можно удалить свою инфраструктуру, удаление реплицированные элементы, сервер конфигурации hello и hello политика восстановления, а затем удаляет хранилище Azure Site Recovery hello.

## <a name="troubleshooting"></a>Устранение неполадок

* [Мониторинг и устранение неполадок защиты виртуальных машин и физических серверов](../../site-recovery/site-recovery-monitoring-and-troubleshooting.md)
* [Форум Microsoft Azure Site Recovery](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)

## <a name="next-steps"></a>Дальнейшие действия

См. следующие ресурсы для конкретных сценариев для автоматической миграции виртуальных машин hello.

* [Перенос виртуальных машин Azure между учетными записями хранения.](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [Создание и отправка tooAzure виртуального жесткого диска Windows Server.](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Создание и загрузка виртуального жесткого диска, который содержит hello операционной системы Linux](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Перенос виртуальных машин из Amazon AWS tooMicrosoft Azure](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

Кроме того см. следующие ресурсы toolearn Дополнительные сведения о хранилище Azure и виртуальных машин Azure hello:

* [Хранилище Azure](https://azure.microsoft.com/documentation/services/storage/)
* [Виртуальные машины Azure](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Хранилище Premium: высокопроизводительное хранилище для рабочих нагрузок виртуальной машины Azure](storage-premium-storage.md)

[1]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-1.png
[2]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-2.png
[3]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-3.png
[4]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-4.png
[5]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-5.png
[6]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-6.PNG
[7]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-7.PNG
[8]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-8.PNG
[9]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-9.PNG
[10]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-10.png
[11]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-11.PNG
[12]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-12.PNG
[13]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-13.png
[14]:../site-recovery/media/site-recovery-vmware-to-azure/v2a-architecture-henry.png
[15]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-14.png
