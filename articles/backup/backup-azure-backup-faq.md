---
title: "aaaAzure часто задаваемые вопросы резервного копирования | Документы Microsoft"
description: "Содержит ответы на вопросы toocommon об: функций резервного копирования Azure, включая службы восстановления хранилищ, его выполнять резервное копирование, как это работает, шифрования и ограничения. "
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "резервное копирование и аварийное восстановление; служба архивации"
ms.assetid: 1011bdd6-7a64-434f-abd7-2783436668d7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/21/2017
ms.author: markgal;arunak;trinadhk;
ms.openlocfilehash: 3338f7620bcc6ebf53c9c161191f2d8bca1a29da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-service"></a>Вопросы о hello службы архивации Azure
Данная статья содержит ответы toocommon вопросы toohelp быстро понять компонент резервного копирования Azure hello. В некоторые ответы hello существуют ссылки toohello статей, имеющих исчерпывающую информацию. Можно задать вопросы о службе архивации Azure, щелкнув **комментарии** (toohello справа). Комментарии отображаются внизу hello в этой статье. Учетная запись Livefyre — необходимые toocomment. Вы также можете публиковать вопросы о hello службы архивации Azure в hello [дискуссионный форум](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

tooquickly сканирование hello содержание этой статьи используется параметр right toohello hello ссылки, в разделе **в этой статье**.


## <a name="recovery-services-vault"></a>Хранилище служб восстановления

### <a name="is-there-any-limit-on-hello-number-of-vaults-that-can-be-created-in-each-azure-subscription-br"></a>Существует какого-либо ограничения на количество hello хранилищ, которые могут быть созданы в каждой подписке Azure? <br/>
Да. Начиная с сентября 2016 года можно создать 25 хранилищ служб восстановления или службы архивации на подписку. Можно создать too25 восстановления служб хранилища в поддерживаемом регионе Azure Backup для каждой подписки. Если вам нужно больше хранилищ, создайте дополнительную подписку.

### <a name="are-there-limits-on-hello-number-of-serversmachines-that-can-be-registered-against-each-vault-br"></a>Существуют ограничения на число hello серверов и компьютеров, которые могут быть зарегистрированы для каждого хранилища? <br/>
Да, можно зарегистрировать too50 машин в каждом хранилище. Для виртуальных машин Azure IaaS hello ограничение составляет 200 виртуальных машин на хранилище. При необходимости tooregister нескольких компьютеров, создайте другое хранилище.

### <a name="if-my-organization-has-one-vault-how-can-i-isolate-one-servers-data-from-another-server-when-restoring-databr"></a>Если у моей организации есть одно хранилище, как изолировать восстановление данных определенного сервера от других серверов?<br/>
Все серверы, являющиеся зарегистрированными toohello же хранилище, можно восстановить hello данных резервная копия другими серверами *, использующих hello парольная фраза*. При наличии серверов резервного копирования, данные которого вы хотите tooisolate с других серверов в вашей организации, используйте указанный парольную фразу для этих серверов. Например, серверы отдела по работе с персоналом могут использовать одну зашифрованную парольную фразу, серверы бухгалтерии — другую, а серверы-хранилища — третью.

### <a name="can-i-migrate-my-backup-data-or-vault-between-subscriptions-br"></a>Можно ли перенести резервные копии данных или хранилище резервных копий из одной подписки в другую? <br/>
Нет. Hello хранилище создается на уровне подписки и не может быть повторно назначенного tooanother подписки после ее создания.

### <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Хранилища служб восстановления развернуты с помощью Resource Manager. Поддерживаются ли еще хранилища службы архивации, развернутые с помощью классической модели? <br/>
Все существующие хранилища резервной копии в hello [классический портал](https://manage.windowsazure.com) продолжить toobe поддерживается. Однако невозможно использовать hello классического портала toodeploy новые хранилища резервной копии. Майкрософт рекомендует использовать хранилищами служб восстановления для всех развертываний, поскольку хранилищами служб tooRecovery, только применяются в будущем. При попытке toocreate резервное хранилище в классическом портале hello будет перенаправленный toohello [портал Azure](https://portal.azure.com).

### <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>Можно перенести хранилище служб восстановления хранилище tooa резервной копии <br/>
К сожалению нет, нельзя перенести содержимое hello tooa хранилища резервной копии, в хранилище служб восстановления. Мы работаем над добавлением этих функциональных возможностей, но пока они недоступны.

### <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>Резервные копии классических виртуальных машин находятся в хранилище службы архивации. Можно ли выполнить миграцию виртуальных машин из классического режима tooResource Manager режима и защитить их в хранилище служб восстановления?
Классический точек восстановления виртуальной Машины в резервном хранилище не автоматически перенести tooa хранилище служб восстановления, при перемещении hello виртуальной Машины из tooResource классический режим Manager. Выполните эти шаги tootransfer резервных копий виртуальной Машины.

1. В резервное хранилище hello, перейдите toohello **защищенные элементы** и выберите hello виртуальной Машины. Щелкните [Остановить защиту](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). *Снимите* флажок **Удаление связанных архивируемых данных**.
2. Удалите расширение резервного копирования или создания моментального снимка hello hello виртуальной Машины.
3. Миграция виртуальной машины hello из диспетчера tooResource классический режим. Убедитесь, что hello хранилища и сети миграцию информации о соответствующая виртуальная машина toohello также является режим tooResource Manager.
4. Создайте хранилище служб восстановления и настройка виртуальной машины с помощью резервной копии на hello перенести **резервного копирования** действия на основе мониторинга хранилища. Подробные сведения о резервном копировании виртуальной Машины tooa восстановления службы хранилища, см. в статье hello [защиты виртуальных машин Azure в хранилище служб восстановления](backup-azure-vms-first-look-arm.md).

## <a name="azure-backup-agent"></a>Агент службы архивации Azure
Подробный список вопросов см. на странице [часто задаваемых вопросов о резервном копировании файлов и папок в Azure](backup-azure-file-folder-backup-faq.md).

## <a name="azure-vm-backup"></a>Резервное копирование виртуальных машин Azure
Подробный список вопросов см. на странице [часто задаваемых вопросов о резервном копировании виртуальных машин Azure](backup-azure-vm-backup-faq.md).

## <a name="back-up-vmware-servers"></a>Резервное копирование серверов VMware

### <a name="can-i-back-up-vmware-vcenter-servers-tooazure"></a>Можно архивировать tooAzure серверов VMware vCenter?

Да. Можно использовать резервное копирование Azure tooback VMware vCenter и ESXi tooAzure. Сведения о версии hello поддерживается VMware см. в статье hello, [матрицы защиты резервное копирование Azure](backup-mabs-protection-matrix.md). Пошаговые инструкции см. в разделе [tooback использования Azure Backup Server сервер VMware](backup-azure-backup-server-vmware.md).


## <a name="azure-backup-server-and-system-center-data-protection-manager"></a>Azure Backup Server и System Center Data Protection Manager
### <a name="can-i-use-azure-backup-server-toocreate-a-bare-metal-recovery-bmr-backup-for-a-physical-server-br"></a>Можно использовать сервер службы архивации Azure toocreate резервной копии состояния системы восстановления исходного состояния системы (BMR) для физического сервера? <br/>
Да.

### <a name="can-i-register-my-dpm-server-toomultiple-vaults-br"></a>Можно зарегистрировать хранилищ toomultiple Мой сервер DPM <br/>
Нет. Сервер DPM или MABS может быть tooonly зарегистрированного одно хранилище.

### <a name="which-version-of-system-center-data-protection-manager-is-supported-br"></a>Какая версия System Center Data Protection Manager поддерживается? <br/>
Рекомендуется устанавливать hello [последние](http://aka.ms/azurebackup_agent) Azure Backup agent на hello последний накопительный пакет обновления (UR) для System Center Data Protection Manager (DPM). Начиная с августа 2016 г. 11 накопительного пакета обновления — hello последнее обновление.

### <a name="i-have-installed-azure-backup-agent-tooprotect-my-files-and-folders-can-i-now-install-system-center-dpm-toowork-with-azure-backup-agent-tooprotect-on-premises-applicationvm-workloads-tooazure-br"></a>Файлы и папки установлен tooprotect агента Azure Backup. System Center DPM toowork теперь установить с помощью службы архивации Azure агента tooprotect локальных рабочих нагрузок приложений или виртуальных Машин tooAzure? <br/>
toouse резервного копирования Azure с помощью System Center Data Protection Manager (DPM), сначала установите DPM, а затем установите агент Azure Backup. Установка компонентов Azure Backup hello в указанном порядке гарантирует, что hello агента Azure Backup работает с DPM. Установка агента Azure Backup hello перед установкой DPM не рекомендуется и не поддерживается.


## <a name="how-azure-backup-works"></a>Принцип работы службы архивации Azure
### <a name="if-i-cancel-a-backup-job-once-it-has-started-is-hello-transferred-backup-data-deleted-br"></a>Если отменить задание резервного копирования после ее запуска, hello передаваемых данных резервного копирования удаляется? <br/>
Нет. Все данные передаются в хранилище hello перед hello задание резервного копирования была отменена, остается в хранилище hello. Azure использует резервного копирования, toooccasionally механизм checkpoint добавить контрольные точки toohello резервных копий данных во время hello резервного копирования. Так как имеются контрольные точки в резервной копии данных hello, hello следующий процесс резервного копирования можно проверить целостность hello hello файлов. следующее задание архивации Hello будет данных toohello добавочного резервного копирования. Добавочное резервное копирование переносятся только новых или измененных данных, который соответствует toobetter использование пропускной способности.

Если вы отмените задание резервного копирования для виртуальной машины Azure, все переданные данные игнорируются. следующее задание архивации Hello передает добавочное данные из задания резервного копирования последнего успешного hello.

### <a name="are-there-limits-on-when-or-how-many-times-a-backup-job-can-be-scheduledbr"></a>Существует ли ограничение на время выполнения и количество запланированных заданий резервного копирования?<br/>
Да. Задания резервного копирования можно запустить на сервере Windows или рабочих станциях Windows вверх toothree раз / день. Можно запускать задания резервного копирования на System Center DPM вверх tootwice в день. Для виртуальных машин IaaS резервное копирование можно выполнять один раз в день. Можно использовать планирование политики для Windows Server или toospecify рабочей станции Windows hello ежедневного или еженедельного расписания. При использовании System Center DPM можно настроить ежедневное, еженедельное, ежемесячное и ежегодное расписание.

### <a name="why-is-hello-size-of-hello-data-transferred-toohello-recovery-services-vault-smaller-than-hello-data-i-backed-upbr"></a>Почему необходимо hello объем данных, передаваемых toohello hello, меньше, чем hello архивируемых данных в хранилище служб восстановления?<br/>
 Все данные hello, резервного копирования Azure Backup Agent или SCDPM или резервное копирование Azure, сжимаются и шифруются перед передачей. После применения hello сжатия и шифрования данных hello в резервном хранилище hello — меньше 30-40%.

## <a name="what-can-i-back-up"></a>Ограничения, связанные с резервным копированием
### <a name="which-operating-systems-do-azure-backup-support-br"></a>Какие операционные системы поддерживает служба архивации Azure? <br/>
Служба архивации Azure поддерживает hello следующий список операционных систем для резервного копирования: файлы и папки и рабочей нагрузки приложений, защищенных с помощью Azure Backup Server и System Center Data Protection Manager (DPM).

| Операционная система | платформа | SKU |
|:--- | --- |:--- |
| Windows 8 и последние пакеты обновления |64-разрядная |Корпоративная, Профессиональная |
| Windows 7 и последние пакеты обновления |64-разрядная |Максимальная, Корпоративная, Профессиональная, Домашняя расширенная, Домашняя базовая, Начальная |
| Windows 8.1 и последние пакеты обновления |64-разрядная |Корпоративная, Профессиональная |
| Windows 10 |64-разрядная |Корпоративная, Профессиональная, Домашняя |
| Windows Server 2016 |64-разрядная |Standard, Datacenter, Essentials |
| Windows Server 2012 R2 и последние пакеты обновления |64-разрядная |Standard, Datacenter, Foundation |
| Windows Server 2012 и последние пакеты обновления |64-разрядная |Datacenter, Foundation, Standard |
| Windows Storage Server 2016 и последние пакеты обновления |64-разрядная |Standard, Workgroup | 
| Windows Storage Server 2012 R2 и последние пакеты обновления |64-разрядная |Standard, Workgroup |
| Windows Storage Server 2012 и последние пакеты обновления |64-разрядная |Standard, Workgroup |
| Windows Server 2012 R2 и последние пакеты обновления |64-разрядная |Essential |
| Windows Server 2008 R2 с пакетом обновления 1 |64-разрядная |Standard, Enterprise, Datacenter, Foundation |
| Windows Server 2008 с пакетом обновления 2 (SP2) |64-разрядная |Standard, Enterprise, Datacenter, Foundation |

**Резервное копирование виртуальных машин Azure:**

* **Linux**: служба архивации Azure поддерживает весь [список дистрибутивов, рекомендуемых для использования в Azure](../virtual-machines/linux/endorsed-distros.md) , за исключением CoreOS Linux.  Также другие перевести-Your-владельцем-дистрибутивы Linux могут работать, пока агент ВМ hello доступен на виртуальной машине hello и поддержку существует Python.
* **Windows Server**: версии до Windows Server 2008 R2 не поддерживаются.


### <a name="is-there-a-limit-on-hello-size-of-each-data-source-being-backed-up-br"></a>Существует ли ограничение на размер каждого источника данных, резервная копия hello? <br/>
Нет ограничений на hello объем данных, которые можно выполнять резервное копирование tooa хранилища. Резервное копирование Azure ограничивает максимальный размер источника данных hello hello, тем не менее, эти ограничения имеют большой размер. Начиная с августа 2015 г. является hello максимальный размер для источника данных для hello поддерживаемых операционных систем:

| Серийный номер | Операционная система | Максимальный размер источника данных |
|:---:|:--- |:--- |
| 1 |Windows Server 2012 или более поздней версии; |54 400 ГБ |
| 2 |Windows 8 или более поздняя версия |54 400 ГБ |
| 3 |Windows Server 2008, Windows Server 2008 R2 |1700 ГБ |
| 4. |Windows 7 |1700 ГБ |

Hello в следующей таблице объясняется, как определяется каждый размер источника данных.

| Источник данных | Сведения |
|:---:|:--- |
| Том |Hello объем данных, резервная копия из одного тома на машине сервера или клиента |
| Виртуальные машины Hyper-V |Сумма данных всех VHD hello hello виртуальной машины, резервная копия |
| База данных Microsoft SQL Server |Размер одной базы данных SQL, для которой выполняется резервное копирование |
| Microsoft SharePoint |Сумма базы данных содержимого и конфигурации hello в пределах фермы SharePoint, резервная копия |
| Microsoft Exchange |Общее количество баз данных Exchange на сервере Exchange, для которого выполняется резервное копирование |
| Восстановление исходного состояния системы и состояние системы |Каждая отдельная копия BMR или состояния системы машины hello, резервная копия |

Для резервного копирования виртуальной Машины Azure Каждая виртуальная машина может иметь too16 диски данных с каждого данных диска, размером 1023 ГБ или меньше. 

## <a name="retention-policy-and-recovery-points"></a>Политика хранения и точки восстановления
### <a name="is-there-a-difference-between-hello-retention-policy-for-dpm-and-windows-serverclient-that-is-on-windows-server-without-dpmbr"></a>Есть ли разница между hello политику хранения для DPM и Windows Server или клиентской (то есть, в Windows Server без DPM)?<br/>
Нет, с помощью DPM, Windows Server и клиента Windows можно настроить ежедневную, еженедельную, ежемесячную и ежегодную политику хранения.

### <a name="can-i-configure-my-retention-policies-selectively--ie-configure-weekly-and-daily-but-not-yearly-and-monthlybr"></a>Можно ли настроить политики хранения выборочно, т. е. настроить еженедельную и ежедневную политики, но не ежегодную или ежемесячную?<br/>
Да, hello структуры хранения Azure Backup позволяет toohave полную гибкость при определении политики хранения hello согласно вашим требованиям.

### <a name="can-i-schedule-a-backup-at-6pm-and-specify-retention-policies-at-a-different-timebr"></a>Можно ли запланировать резервное копирование на 18:00, а политики хранения настроить на другое время?<br/>
Нет. Политики хранения можно применять только в точках резервного копирования. В следующие изображения hello политика хранения hello задано резервные копии, созданные в 12: 00 и 18: 00. <br/>

![Планирование резервного копирования и хранения](./media/backup-azure-backup-faq/Schedule.png)
<br/>

### <a name="if-a-backup-is-retained-for-a-long-duration-does-it-take-more-time-toorecover-an-older-data-point-br"></a>Если резервная копия сохраняется в течение длительного времени, занимает больше времени toorecover старых точек данных? <br/>
Нет — время hello toorecover hello старые или hello последней точки hello же. Каждая точка восстановления ведет себя как полная точка.

### <a name="if-each-recovery-point-is-like-a-full-point-does-it-impact-hello-total-billable-backup-storagebr"></a>Если каждая точка восстановления, как полный точки его влияет общее hello оплачиваемых резервного хранилища?<br/>
Обычно продукты с точками длительного срока хранения хранят резервные данные как полные точки. Hello полный моментов хранилища *неэффективным* , но проще и быстрее toorestore. Добавочные копии являются хранилища *эффективный* , но требуют toorestore цепочки данных, который влияет на время восстановления. Azure Backup хранилища архитектура дает hello преимущества обоих миров оптимально хранения данных для быстрого восстановления и расходов на низкий хранилища. Этот подход обеспечивает эффективное использование пропускной способности (как для входящих, так и для исходящих данных). Оба hello объем данных хранилища и hello время необходимых данных toorecover hello, сохраняется tooa минимальное. Дополнительные сведения об эффективности [добавочных резервных копий](https://azure.microsoft.com/blog/microsoft-azure-backup-save-on-long-term-storage/).

### <a name="is-there-a-limit-on-hello-number-of-recovery-points-that-can-be-createdbr"></a>Существует ограничение на количество точек восстановления, которые могут быть созданы в hello?<br/>
Можно создать копии too9999 точек восстановления для защищенного экземпляра. Защищенного экземпляра — это компьютер, сервера (физических или виртуальных) или tooback рабочей нагрузки настройки копирования tooAzure данных. Дополнительные сведения см. в разделе объяснения hello [резервного копирования и хранения](./backup-introduction-to-azure-backup.md#backup-and-retention), и [возможности защищенных экземпляров](./backup-introduction-to-azure-backup.md#what-is-a-protected-instance)?

### <a name="how-many-recoveries-can-i-perform-on-hello-data-that-is-backed-up-tooazurebr"></a>Количество операций восстановления можно выполнять на hello данных, резервная копия tooAzure?<br/>
Нет ограничений на число hello операции восстановления из резервной копии Azure.

### <a name="when-restoring-data-do-i-pay-for-hello-egress-traffic-from-azure-br"></a>При восстановлении данных, я плачу за hello исходящий трафик из Azure? <br/>
Нет. В операции восстановления являются бесплатными и не взиматься плата за исходящий трафик hello.

## <a name="azure-backup-encryption"></a>Шифрование службы архивации Azure
### <a name="is-hello-data-sent-tooazure-encrypted-br"></a>Отправляются ли данные hello tooAzure шифрование? <br/>
Да. Данные шифруются на клиент/сервер/SCDPM hello на локальном компьютере с помощью AES256 и hello данные передаются через безопасное HTTPS-канала.

### <a name="is-hello-backup-data-on-azure-encrypted-as-wellbr"></a>Такое hello резервного копирования данных в Azure, как зашифрованные?<br/>
Да. Hello данные, отправляемые tooAzure остается зашифрованным (при хранении). Корпорация Майкрософт не выполняет расшифровку hello резервного копирования данных в любой момент. При резервном копировании виртуальной Машины Azure, резервное копирование Azure зависит от шифрования hello виртуальной машины. Например если ВМ шифруется с помощью шифрования диска Azure, или некоторые другие технологии шифрования, резервного копирования Azure использует toosecure, шифрование данных.

### <a name="what-is-hello-minimum-length-of-encryption-key-used-tooencrypt-backup-data-br"></a>Что hello минимальную длину ключа шифрования используется tooencrypt резервных копий данных? <br/>
Hello ключ шифрования должен быть менее 16 знаков, при использовании агента резервного копирования Azure. Для виртуальных машин Azure нет не toolength предел ключей, используемых Azure KeyVault. 

### <a name="what-happens-if-i-misplace-hello-encryption-key-can-i-recover-hello-data-or-can-microsoft-recover-hello-data-br"></a>Что произойдет, если я потеряли ключ шифрования hello? Выполнить восстановление данных hello (или) Майкрософт данные можно восстановить hello? <br/>
Hello ключа используется tooencrypt hello резервного копирования данных присутствует только в локальной среде клиента hello. Корпорация Майкрософт не сохраняет копию в Azure и не имеет ключа toohello любой доступ. Если клиент hello misplaces ключ hello, Microsoft невозможно восстановить данные резервного копирования hello.
