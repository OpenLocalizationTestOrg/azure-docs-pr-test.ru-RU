---
title: "aaaMonitor и устранение неполадок защиты для виртуальных машин и физических серверов | Документы Microsoft"
description: "Azure Site Recovery координирует hello репликации, отработки отказа и восстановления виртуальных машин, размещенных на локальных серверах tooAzure или вторичный центр обработки данных. Используйте этот toomonitor статьи и устранение неполадок защиты сайта Hyper-V или Virtual Machine Manager."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 0fc8e368-0c0e-4bb1-9d50-cffd5ad0853f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: d790375db5f30e98f009c8d8272558188c51934c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-troubleshoot-protection-for-virtual-machines-and-physical-servers"></a>Мониторинг и устранение неполадок защиты виртуальных машин и физических серверов
Это наблюдение и устранение неполадок помогает руководства вы узнаете, как tootrack работоспособность репликации и устранение неполадок методы для Azure Site Recovery.

## <a name="understand-hello-components"></a>Понимать, какие hello компонентов
### <a name="vmware-virtual-machine-or-physical-server-site-deployment-for-replication-between-on-premises-and-azure"></a>Развертывание сайта на виртуальной машине VMware или физическом сервере для репликации между локальными средами и Azure
tooset настройки восстановления базы данных между виртуальной машины VMware в локальной или физического сервера и Azure должны tooset hello конфигурации сервера, главный целевой сервер и компоненты процесса сервера на виртуальной машине или на сервере. При включении защиты для сервера исходного hello Azure Site Recovery устанавливается hello мобильные приложения Microsoft Azure приложения службы. После сбоя в локальной среде и hello исходного сервера отработке отказа tooAzure клиенты должны tooset сервера обработки в Azure и главный целевой сервер на исходном сервере hello локальный toorebuild на локальном компьютере.

![Развертывание сайта VMware или физического сайта для репликации между локальной средой и Azure](media/site-recovery-monitoring-and-troubleshooting/image18.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-sites"></a>Развертывание сайта Virtual Machine Manager для репликации между локальными сайтами
tooset настройки восстановления базы данных между двумя локальными расположения, требуется поставщика Azure Site Recovery toodownload hello и установите его на сервере диспетчера виртуальных машин hello. Поставщик Hello должен tooensure подключения к Интернету, все операции hello, запускаемые из портала Azure hello переведенные tooon локальной операции get.

![Развертывание сайта Virtual Machine Manager для репликации между локальными сайтами](media/site-recovery-monitoring-and-troubleshooting/image1.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>Развертывание сайта Virtual Machine Manager для репликации между локальными расположениями и Azure
При настройке восстановления базы данных между расположениями в локальной среде и Azure требуется поставщика Azure Site Recovery toodownload hello и установите его на сервере диспетчера виртуальных машин hello. Необходимо также tooinstall hello агента служб восстановления Azure, требующий toobe устанавливаются на каждом узле Hyper-V. Дополнительные сведения см. [здесь](site-recovery-hyper-v-azure-architecture.md).

![Развертывание сайта Virtual Machine Manager для репликации между локальными расположениями и Azure](media/site-recovery-monitoring-and-troubleshooting/image2.png)

### <a name="hyper-v-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>Развертывание сайта Hyper-V для репликации между локальными расположениями и Azure
Этот процесс является аналогичные развертывание tooVirtual Machine Manager. Hello единственным отличием является hello поставщика Azure Site Recovery и агента служб восстановления Azure устанавливаются на самом узле Hyper-V hello. [Подробнее](site-recovery-hyper-v-azure-architecture.md). .

## <a name="monitor-configuration-protection-and-recovery-operations"></a>Мониторинг операций настройки, защиты и восстановления
Каждая операция в Azure Site Recovery для аудита и отслеживаются в hello **ЗАДАНИЙ** вкладки. Для конфигурации, защиты и ошибка восстановления, перейдите toohello **задания** и найдите сбоев.

![Фильтр сбой Hello в вкладку задания hello](media/site-recovery-monitoring-and-troubleshooting/image3.png)

Если найти ошибки в разделе hello **ЗАДАНИЙ** , щелкните задание hello и нажмите кнопку **сведения об ОШИБКЕ** для этого задания.

![сведения об ОШИБКЕ кнопку Hello](media/site-recovery-monitoring-and-troubleshooting/image4.png)

сведения об ошибке Hello поможет вам определить возможные причины и рекомендации для hello проблемы.

![Диалоговое окно со сведениями об ошибке для задания](media/site-recovery-monitoring-and-troubleshooting/image5.png)

В предыдущем примере hello другая операция, которая выполняется кажется toobe вызывает toofail конфигурации защиты hello. Устраните проблему hello, на основе рекомендации hello и нажмите кнопку **RESART** tooinitiate hello операцию.

![Кнопка ПЕРЕЗАГРУЗКИ Hello во вкладке "задания" hello](media/site-recovery-monitoring-and-troubleshooting/image6.png)

Hello **ПЕРЕЗАПУСТИТЕ** параметр доступен не для всех операций. Если операция не имеет hello **ПЕРЕЗАПУСТИТЕ** параметра, объект toohello вернуться назад и повторить попытку hello. Можно отменить любые задания, выполняемые с помощью hello **ОТМЕНИТЬ** кнопки.

![Кнопка "Отмена" Hello](media/site-recovery-monitoring-and-troubleshooting/image7.png)

## <a name="monitor-replication-health-for-virtual-machines"></a>Мониторинг работоспособности репликации для виртуальных машин
Можно использовать монитор Azure Site Recovery hello Azure tooremotely портала поставщиков для каждой сущности защищенных hello. Перейдите на вкладку **Защищенные элементы** и выберите вкладку **Облака VMM** или **Группы защиты**. Hello **ОБЛАКА VMM** вкладка доступна только для развертываний, которые основаны на диспетчере виртуальных машин. Для других сценариев hello защищенные объекты находятся в hello **ГРУПП защиты** вкладки.

![Параметры облака VMM и ГРУПП защиты Hello](media/site-recovery-monitoring-and-troubleshooting/image8.png)

Пункт hello соответствующих облако или защиты группы toosee всех доступных операций отображаются в нижней части окна hello защищенного объекта.

![Параметры, доступные для выбранного защищенного объекта](media/site-recovery-monitoring-and-troubleshooting/image9.png)

Как показано в предыдущем снимке экрана hello hello состояние виртуальной машины — **критическое**. Можно щелкнуть hello **сведения об ОШИБКЕ** кнопку на hello нижней toosee hello ошибки. В зависимости от hello **возможные причины ее возникновения** и **рекомендации**, устранить проблему hello.

![сведения об ошибке кнопку Hello](media/site-recovery-monitoring-and-troubleshooting/image10.png)

![Ошибки и рекомендации, приведенные в диалоговое окно «сведения об ошибке hello»](media/site-recovery-monitoring-and-troubleshooting/image11.png)

> [!NOTE]
> Если все активные операции выполняются или не удалось, перейдите к toohello **ЗАДАНИЙ** представления в виде упомянутых ранее ошибки hello tooview для конкретного задания.
>
>

## <a name="troubleshoot-on-premises-hyper-v-issues"></a>Устранение неполадок локальной среды Hyper-V
Подключите toohello локальной консоли диспетчера Hyper-V, выберите hello виртуальной машины и проверять работоспособность репликации hello.

![Работоспособность репликации tooview параметр в консоли диспетчера Hyper-V hello](media/site-recovery-monitoring-and-troubleshooting/image12.png)

В этом случае параметр **Работоспособность репликации** имеет значение **Критическое**. Щелкните правой кнопкой мыши hello виртуальной машины и нажмите кнопку **репликации** > **Показать работоспособность репликации** toosee hello сведения.

![Работоспособность репликации для конкретной виртуальной машины](media/site-recovery-monitoring-and-troubleshooting/image13.png)

Если для виртуальной машины hello, репликация приостановлена, щелкните правой кнопкой мыши hello виртуальной машины и нажмите кнопку **репликации** > **возобновить репликацию**.

![Параметр tooresume репликации в консоли диспетчера Hyper-V hello](media/site-recovery-monitoring-and-troubleshooting/image19.png)

При миграции виртуальной машины новый узел Hyper-V, который находится в пределах кластера hello или автономную машину и узел Hyper-V hello настроена с помощью Azure Site Recovery, не будет влиять репликации для виртуальной машины hello. Убедитесь, что hello нового узла Hyper-V отвечает всем необходимым требованиям hello и настраивается с помощью Azure Site Recovery.

### <a name="event-log"></a>Журнал событий
| Источники событий | Сведения |
| --- |:--- |
| **Applications and Service Logs/Microsoft/VirtualMachineManager/Server/Admin** (сервер Virtual Machine Manager) |Предоставляет множество различных проблем Virtual Machine Manager tootroubleshoot полезно ведения журнала. |
| **Applications and Service Logs/MicrosoftAzureRecoveryServices/Replication** (узел Hyper-V) |Предоставляет полезные ведения журнала tootroubleshoot многие проблемы агента служб восстановления Microsoft Azure. <br/> ![Расположение источника события репликации для узла Hyper-V](media/site-recovery-monitoring-and-troubleshooting/eventviewer03.png) |
| **Applications and Service Logs/Microsoft/Azure Site Recovery/Provider/Operational** (узел Hyper-V) |Предоставляет множество проблем службе Microsoft Azure Site Recovery tootroubleshoot полезно ведения журнала. <br/> ![Расположение источника операционного события для узла Hyper-V](media/site-recovery-monitoring-and-troubleshooting/eventviewer02.png) |
| **Applications and Service Logs/Microsoft/Windows/Hyper-V-VMMS/Admin** (узел Hyper-V) |Предоставляет полезные ведения журнала tootroubleshoot многие проблемы управления виртуальной машины Hyper-V. <br/> ![Расположение источника событий Virtual Machine Manager для узла Hyper-V](media/site-recovery-monitoring-and-troubleshooting/eventviewer01.png) |

### <a name="hyper-v-replication-logging-options"></a>Параметры ведения журнала репликации Hyper-V
Все события, имеющие отношение репликации tooHyper V записываются в hello Hyper-V-VMMS\\входа администратора, расположенный в узле журналы приложений и служб\\Microsoft\\Windows. Кроме того можно включить Аналитический журнал для hello служба управления виртуальными машинами Hyper-V. tooenable это вход, сначала следует hello аналитический и журнале отладки можно просматривать в hello в окне просмотра событий. Откройте средство просмотра событий и выберите элементы **Представление** > **Отобразить аналитический и отладочный журналы**.

![параметр Отобразить аналитический и отладочный журналы Hello](media/site-recovery-monitoring-and-troubleshooting/image14.png)

Аналитический журнал отображается в группе **Hyper-V-VMMS**.

![Hello Аналитический журнал в дереве просмотра событий hello](media/site-recovery-monitoring-and-troubleshooting/image15.png)

В hello **действия** области, нажмите кнопку **включить журнал**. После включения журнал отображается в **системном мониторе** как **сеанс трассировки событий** в области **Группы сборщиков данных**.

![Сеансы трассировки событий в дереве hello системного монитора](media/site-recovery-monitoring-and-troubleshooting/image16.png)

tooview hello собранные сведения, сначала необходимо остановить сеанс трассировки hello, отключив hello журнала. Сохранить журнал hello и открыть его в средстве просмотра событий или использовать другие средства tooconvert его в случае необходимости.

## <a name="reach-out-for-microsoft-support"></a>Служба технической поддержки Майкрософт
### <a name="log-collection"></a>Сбор журналов
Защита сайта диспетчера виртуальных машин, см. в разделе слишком[сбор журналов Azure Site Recovery с помощью средства поддержки диагностики платформы (SDP)](http://social.technet.microsoft.com/wiki/contents/articles/28198.asr-data-collection-and-analysis-using-the-vmm-support-diagnostics-platform-sdp-tool.aspx) toocollect hello необходимые журналы.

Для защиты сайта Hyper-V, загрузите [средство](https://dcupload.microsoft.com/tools/win7files/DIAG_ASRHyperV_global.DiagCab) и выполнить его на журналы hello toocollect узла hello Hyper-V.

VMware и физических серверов, см. в разделе слишком[сбор журналов Azure Site Recovery для VMware и физических узла защиты](http://social.technet.microsoft.com/wiki/contents/articles/30677.azure-site-recovery-log-collection-for-vmware-and-physical-site-protection.aspx) toocollect hello необходимые журналы.

Hello инструмент собирает журналы hello локально в произвольным именем вложенной папки в каталоге % LocalAppData%\ElevatedDiagnostics.

![В примере показана защита сайта Hyper-V.](media/site-recovery-monitoring-and-troubleshooting/animate01.gif)

### <a name="open-a-support-ticket"></a>Открытие запроса в службу поддержки
обращение в службу поддержки для Azure Site Recovery tooraise направляться tooAzure поддержки с помощью URL-адрес в <http://aka.ms/getazuresupport>.

## <a name="kb-articles"></a>Статьи базы знаний
* [Как toopreserve hello буква защищенных виртуальных машин, которые отработку отказа или перенести tooAzure](http://support.microsoft.com/kb/3031135)
* [Как toomanage локальной пропускной способности сети защиты tooAzure](https://support.microsoft.com/kb/3056159)
* [Ошибка Azure Site Recovery: «hello кластерный ресурс не найден» при попытке tooenable защиты для виртуальной машины](http://support.microsoft.com/kb/3010979)
* [Общие сведения и руководство по устранению неполадок репликации Hyper-V](http://social.technet.microsoft.com/wiki/contents/articles/21948.hyper-v-replica-troubleshooting-guide.aspx)

## <a name="common-azure-site-recovery-errors-and-their-resolutions"></a>Распространенные ошибки ASR и способы их устранения
Ниже приведены распространенные ошибки и способы их устранения. Каждая ошибка описана на отдельной вики-странице.

### <a name="general"></a>Общие сведения
* <span style="color:green;">НОВОЕ</span> [Задания завершаются с ошибкой "Выполняется операция". Ошибка 505, 514, 532.](http://social.technet.microsoft.com/wiki/contents/articles/32190.azure-site-recovery-jobs-failing-with-error-an-operation-is-in-progress-error-505-514-532.aspx)
* <span style="color:green;">НОВЫЙ</span> [задания произошел сбой с ошибкой «Сервер не подключенных toohello Интернет». Ошибка 25018.](http://social.technet.microsoft.com/wiki/contents/articles/32192.azure-site-recovery-jobs-failing-with-error-server-isn-t-connected-to-the-internet-error-25018.aspx)

### <a name="setup"></a>Настройка
* [не удается зарегистрировать сервер диспетчера виртуальных машин Hello из-за внутренней ошибки tooan. Дополнительные сведения об ошибке hello обратитесь toohello представление задания на портале Site Recovery hello. Запустите программу установки еще раз tooregister hello server.](http://social.technet.microsoft.com/wiki/contents/articles/25570.the-vmm-server-cannot-be-registered-due-to-an-internal-error-please-refer-to-the-jobs-view-in-the-site-recovery-portal-for-more-details-on-the-error-run-setup-again-to-register-the-server.aspx)
* [Соединение не может быть установленного toohello хранилище диспетчера восстановления Hyper-V. Проверьте параметры прокси-сервера hello или повторите попытку позже.](http://social.technet.microsoft.com/wiki/contents/articles/25571.a-connection-cant-be-established-to-the-hyper-v-recovery-manager-vault-verify-the-proxy-settings-or-try-again-later.aspx)

### <a name="configuration"></a>Конфигурация
* [Не удается toocreate группы защиты: произошла ошибка при получении списка серверов hello.](http://blogs.technet.com/b/somaning/archive/2015/08/12/unable-to-create-the-protection-group-in-azure-site-recovery-portal.aspx)
* [Кластер узлов Hyper-V содержит по крайней мере один статический сетевой адаптер или не подключенных адаптеров, настроенных toouse DHCP.](http://social.technet.microsoft.com/wiki/contents/articles/25498.hyper-v-host-cluster-contains-at-least-one-static-network-adapter-or-no-connected-adapters-are-configured-to-use-dhcp.aspx)
* [Virtual Machine Manager не имеет разрешения toocomplete действие.](http://social.technet.microsoft.com/wiki/contents/articles/31110.vmm-does-not-have-permissions-to-complete-an-action.aspx)
* [Невозможно выбрать hello учетной записи хранилища в рамках подписки hello во время настройки защиты.](http://social.technet.microsoft.com/wiki/contents/articles/32027.can-t-select-the-storage-account-within-the-subscription-while-configuring-protection.aspx)

### <a name="protection"></a>Защита
* <span style="color:green;">НОВЫЙ</span> [включить защиту, произошел сбой с ошибкой «Не удалось настроить защиту для виртуальной машины hello». Ошибка 60007, 40003.](http://social.technet.microsoft.com/wiki/contents/articles/32194.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-configured-for-the-virtual-machine-error-60007-40003.aspx)
* <span style="color:green;">НОВЫЙ</span> [включить защиту, произошел сбой с ошибкой «Не удалось включить защиту для виртуальной машины hello.» Ошибка 70094.](http://social.technet.microsoft.com/wiki/contents/articles/32195.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-enabled-for-the-virtual-machine-error-70094.aspx)
* <span style="color:green;">НОВЫЙ</span> [динамической миграции ошибка 23848 - hello виртуальной машины будет перенесена с использованием типа Live toobe. Это может нарушить состояние защиты восстановления hello hello виртуальной машины.](http://social.technet.microsoft.com/wiki/contents/articles/32021.live-migration-error-23848-the-virtual-machine-is-going-to-be-moved-using-type-live-this-could-break-the-recovery-protection-status-of-the-virtual-machine.aspx)
* [Включение защиты не выполнено, так как на компьютере не установлен агент.](http://social.technet.microsoft.com/wiki/contents/articles/31105.enable-protection-failed-since-agent-not-installed-on-host-machine.aspx)
* [Не удается найти подходящий узел для виртуальной машины реплики hello - из-за toolow вычислительные ресурсы.](http://social.technet.microsoft.com/wiki/contents/articles/25501.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-low-compute-resources.aspx)
* [Не удается найти подходящий узел для виртуальной машины реплики hello - из-за toono подключенные к логической сети.](http://social.technet.microsoft.com/wiki/contents/articles/25502.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-no-logical-network-attached.aspx)
* [Не удается подключиться к хост-компьютера реплики toohello - не удается установить подключение.](http://social.technet.microsoft.com/wiki/contents/articles/31106.cannot-connect-to-the-replica-host-machine-connection-could-not-be-established.aspx)

### <a name="recovery"></a>Восстановление
* Virtual Machine Manager не удалось выполнить операцию узла hello:
  * [Отработка отказа toohello выбранной точки восстановления для виртуальной машины: Ошибка доступа.](http://social.technet.microsoft.com/wiki/contents/articles/25504.fail-over-to-the-selected-recovery-point-for-virtual-machine-general-access-denied-error.aspx)
  * [Сбой toofail Hyper-V через toohello выбранной точки восстановления для виртуальной машины: операция прервана.  Укажите более новую точку восстановления. (0x80004004).](http://social.technet.microsoft.com/wiki/contents/articles/25503.hyper-v-failed-to-fail-over-to-the-selected-recovery-point-for-virtual-machine-operation-aborted-try-a-more-recent-recovery-point-0x80004004.aspx)
  * Подключение к серверу hello не удалось установленное (0x00002EFD).
    * [Hyper-V не удалось tooenable обратной репликации для виртуальной машины.](http://social.technet.microsoft.com/wiki/contents/articles/25505.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-reverse-replication-for-virtual-machine.aspx)
    * [Hyper-V не удалось выполнить репликацию tooenable для виртуальной машины виртуальной машины.](http://social.technet.microsoft.com/wiki/contents/articles/25506.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-replication-for-virtual-machine-virtual-machine.aspx)
  * [Не удалось выполнить отработку отказа для виртуальной машины.](http://social.technet.microsoft.com/wiki/contents/articles/25508.could-not-commit-failover-for-virtual-machine.aspx)
* [Hello план восстановления содержит виртуальные машины, которые еще не готовы для плановой отработки отказа.](http://social.technet.microsoft.com/wiki/contents/articles/25509.the-recovery-plan-contains-virtual-machines-which-are-not-ready-for-planned-failover.aspx)
* [Hello виртуальная машина не готова к плановой отработке отказа.](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* [Виртуальная машина не запущена и не отключена.](http://social.technet.microsoft.com/wiki/contents/articles/25510.virtual-machine-is-not-running-and-is-not-powered-off.aspx)
* [На виртуальной машине произошла незапланированная операция, и не удалось выполнить отработку отказа.](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* Тестовая отработка отказа
  * [Не удалось начать отработку отказа, так как выполняется тестовая отработка отказа.](http://social.technet.microsoft.com/wiki/contents/articles/31111.failover-could-not-be-initiated-since-test-failover-is-in-progress.aspx)
* <span style="color:green;">НОВЫЙ</span> отработки отказа время ожидания, и «Задача PreFailoverWorkflow WaitForScriptExecutionTaskTimeout» из-за toohello параметры конфигурации для сетевой группы безопасности связанного с hello виртуальной машины или hello подсети toowhich hello машины hello принадлежит. См. слишком[«task PreFailoverWorkflow WaitForScriptExecutionTaskTimeout»](https://aka.ms/troubleshoot-nsg-issue-azure-site-recovery) подробные сведения.

### <a name="configuration-server-process-server-master-target"></a>Сервер конфигурации, сервер обработки, главный целевой сервер
* [с фиолетовым экраном смерти сбоя узла ESXi Hello, на какие hello PS/CS размещается в виде виртуальной Машины.](http://social.technet.microsoft.com/wiki/contents/articles/31107.vmware-esxi-host-experiences-a-purple-screen-of-death.aspx)

### <a name="remote-desktop-troubleshooting-after-failover"></a>Устранение неполадок после отработки отказа удаленного рабочего стола
* Многие пользователи сталкиваются toohello tooconnect проблемы отработку отказа виртуальной машины в Azure. [Устранение неполадок tooRDP документа к виртуальной машине hello hello используйте](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

#### <a name="adding-a-public-ip-on-a-resource-manager-virtual-machine"></a>Добавление общедоступного IP-адреса в виртуальную машину диспетчера ресурсов
Если hello **Connect** кнопка hello портала становится недоступной, а не tooAzure, подключенных через VPN-подключения Express Route или сайт-сайт, требуется toocreate и назначить общедоступный IP-адрес вашей виртуальной машины, прежде чем использовать удаленное Оболочка или общего рабочего стола. Затем можно добавить общедоступный IP-адрес в сетевом интерфейсе hello hello виртуальной машины.  

![Добавление общедоступного IP-адреса сетевого интерфейса hello отработку отказа виртуальной машины](media/site-recovery-monitoring-and-troubleshooting/createpublicip.gif)
