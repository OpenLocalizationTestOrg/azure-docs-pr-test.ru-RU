---
title: "Устранение сбоя службы Azure Backup: состояние гостевого агента \"Недоступно\" | Документация Майкрософт"
description: "Признаки, причины и устранения связанных tooerror сбои резервного копирования Azure: не удалось связаться с агентом ВМ hello"
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
keywords: Azure backup; VM agent; Network connectivity;
ms.assetid: 4b02ffa4-c48e-45f6-8363-73d536be4639
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: genli;markgal;
ms.openlocfilehash: 724c61ba80d0a9ef91a5f8543ae72bb86968881b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-backup-failure-issues-with-agent-andor-extension"></a>Устранение неполадок службы Azure Backup: проблемы с агентом и/или расширением

Эта статья содержит tooproblems в связи с агентом ВМ и расширения, связанные с по устранению неполадок toohelp шаги устранения сбоев резервного копирования.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="vm-agent-unable-toocommunicate-with-azure-backup"></a>Не удается toocommunicate агент виртуальной Машины в службе архивации Azure
После регистрации и запланировать виртуальной Машины для службы архивации Azure hello, резервное копирование инициирует задание hello путем взаимодействия с hello tootake агента ВМ моментальный снимок в момент. Любой из следующих условий hello может блокировать hello моментального снимка из запустилась, что в свою очередь, может вызвать сбой tooBackup. Следуйте ниже устранения неполадок в hello, используя порядок и повторите операцию.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Причина 1: [hello виртуальная машина имеет доступ к Интернету отсутствует](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Причина 2: [hello агент установлен в hello виртуальной Машины, но не отвечает (для ВМ Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Причина 3: [hello агент, установленный в hello виртуальной Машины является устаревшим (для виртуальных машин Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Причина 4: [не удается получить состояние hello моментальных снимков или моментальный снимок не может быть выполнено](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Причина 5: [hello расширение резервного копирования завершается с ошибкой tooupdate или нагрузки](#the-backup-extension-fails-to-update-or-load)

## <a name="snapshot-operation-failed-due-toono-network-connectivity-on-hello-virtual-machine"></a>Сбой операции моментальных снимков из-за toono сетевого подключения на виртуальной машине hello
После регистрации и запланировать виртуальную Машину для hello службы резервного копирования Azure, резервное копирование инициирует задание hello путем взаимодействия с hello расширение резервного копирования виртуальной Машины tootake на момент времени, моментальный снимок. Любой из следующих условий hello может блокировать hello моментального снимка из запустилась, что в свою очередь, может вызвать сбой tooBackup. Следуйте ниже устранения неполадок в hello, используя порядок и повторите операцию.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Причина 1: [hello виртуальная машина имеет доступ к Интернету отсутствует](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Причина 2: [не удается получить состояние hello моментальных снимков или моментальный снимок не может быть выполнено](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-3-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Причина 3: [hello расширение резервного копирования завершается с ошибкой tooupdate или нагрузки](#the-backup-extension-fails-to-update-or-load)

## <a name="vmsnapshot-extension-operation-failed"></a>Не удалось выполнить операцию с расширением моментального снимка виртуальной машины

После регистрации и запланировать виртуальную Машину для hello службы резервного копирования Azure, резервное копирование инициирует задание hello путем взаимодействия с hello расширение резервного копирования виртуальной Машины tootake на момент времени, моментальный снимок. Любой из следующих условий hello может блокировать hello моментального снимка из запустилась, что в свою очередь, может вызвать сбой tooBackup. Следуйте ниже устранения неполадок в hello, используя порядок и повторите операцию.
##### <a name="cause-1-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Причина 1: [не удается получить состояние hello моментальных снимков или моментальный снимок не может быть выполнено](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-2-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Причина 2: [hello расширение резервного копирования завершается с ошибкой tooupdate или нагрузки](#the-backup-extension-fails-to-update-or-load)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Причина 3: [hello виртуальная машина имеет доступ к Интернету отсутствует](#the-vm-has-no-internet-access)
##### <a name="cause-4-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Причина 4: [hello агент установлен в hello виртуальной Машины, но не отвечает (для ВМ Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-5-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Причина 5: [hello агент, установленный в hello виртуальной Машины является устаревшим (для виртуальных машин Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)

## <a name="unable-tooperform-hello-operation-as-hello-vm-agent-is-not-responsive"></a>Не удается tooperform hello операцию, так как hello агент ВМ не отвечает

После регистрации и запланировать виртуальную Машину для hello службы резервного копирования Azure, резервное копирование инициирует задание hello путем взаимодействия с hello расширение резервного копирования виртуальной Машины tootake на момент времени, моментальный снимок. Любой из следующих условий hello может блокировать hello моментального снимка из запустилась, что в свою очередь, может вызвать сбой tooBackup. Следуйте ниже устранения неполадок в hello, используя порядок и повторите операцию.
##### <a name="cause-1-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Причина 1: [hello агент установлен в hello виртуальной Машины, но не отвечает (для ВМ Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Причина 2: [hello агент, установленный в hello виртуальной Машины является устаревшим (для виртуальных машин Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Причина 3: [hello виртуальная машина имеет доступ к Интернету отсутствует](#the-vm-has-no-internet-access)

## <a name="backup-failed-with-an-internal-error---please-retry-hello-operation-in-a-few-minutes"></a>Сбой резервного копирования с внутренней ошибкой — и повторите операцию hello через несколько минут

После регистрации и запланировать виртуальную Машину для hello службы резервного копирования Azure, резервное копирование инициирует задание hello путем взаимодействия с hello расширение резервного копирования виртуальной Машины tootake на момент времени, моментальный снимок. Любой из следующих условий hello может блокировать hello моментального снимка из запустилась, что в свою очередь, может вызвать сбой tooBackup. Следуйте ниже устранения неполадок в hello, используя порядок и повторите операцию.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Причина 1: [hello виртуальная машина имеет доступ к Интернету отсутствует](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Причина 2: [hello агента, установленного hello виртуальной Машины, но не отвечает (для ВМ Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Причина 3: [hello агент, установленный в hello виртуальной Машины является устаревшим (для виртуальных машин Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Причина 4: [не удается получить состояние hello моментальных снимков или моментальный снимок не может быть выполнено](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Причина 5: [hello расширение резервного копирования завершается с ошибкой tooupdate или нагрузки](#the-backup-extension-fails-to-update-or-load)


## <a name="causes-and-solutions"></a>Причины и решения

### <a name="hello-vm-has-no-internet-access"></a>Hello виртуальная машина имеет доступ к Интернету отсутствует
Каждого требования развертывания hello hello виртуальная машина имеет доступ к Интернету отсутствует или имеет ограничения на месте, запрещающие доступ toohello инфраструктуры Azure.

toofunction правильно, требуется расширение резервного копирования hello toohello подключения к Azure открытый IP-адресов. модуль Hello отправляет команды tooan хранилища Azure (URL-адреса HTTP) конечной точки toomanage hello моментальные снимки hello виртуальной Машины. Если расширение hello не toohello доступа к общедоступной сети Интернет, в конечном итоге резервное копирование завершается с ошибкой.

####  <a name="solution"></a>Решение
tooresolve hello проблему, выполните одно из перечисленных ниже методов hello.
##### <a name="allow-access-toohello-azure-datacenter-ip-ranges"></a>Разрешить доступ диапазоны IP-адресов центра обработки данных Azure toohello

1. Получить hello [список центра обработки данных Azure IP-адреса](https://www.microsoft.com/download/details.aspx?id=41653) tooallow доступ к.
2. Разблокировать hello IP-адреса, выполнив hello **New-NetRoute** командлета в hello виртуальной Машины Azure в окне PowerShell с повышенными привилегиями. Используйте командлет hello с правами администратора.
3. toohello доступа tooallow IP-адресов, добавьте правила toohello сетевой группы безопасности, если таковой имеется.

##### <a name="create-a-path-for-http-traffic-tooflow"></a>Создать путь для tooflow трафик HTTP

1. При наличии ограничений сетевого на месте (например, группы безопасности сети), разверните HTTP-прокси сервера tooroute hello трафика.
2. toohello доступа tooallow Интернет из hello прокси-сервер HTTP, добавьте правила toohello сетевой группы безопасности, если таковой имеется.

tooset копирование HTTP-прокси для резервных копий виртуальной Машины, в статье toolearn [подготовки вашей среды tooback копирование виртуальных машин Azure](backup-azure-vms-prepare.md#using-an-http-proxy-for-vm-backups).

В случае, если вы используете управляемый диски, может потребоваться дополнительный порт (8443) открывается на брандмауэрах hello.

### <a name="hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vms"></a>Hello агента, установленного hello виртуальной Машины, но не отвечает (для ВМ Windows)

#### <a name="solution"></a>Решение
Hello агент ВМ был поврежден или hello службы были остановлены. Повторно Установка агента ВМ hello помогает получить последнюю версию hello и перезапустите hello связи.

1. Проверьте hello ли гостевой агент Windows служба, запущенная в служб (services.msc) для виртуальной машины. Попробуйте перезапустить службу Windows гостевой агент hello и инициировать hello резервного копирования<br>
2. Если она не отображается в списке служб, проверьте в разделе "Программы и компоненты", установлена ли служба гостевого агента Windows.
4. Если вы не можете tooview в hello удаления программы и компоненты Windows гостевого агента.
5. Загрузите и установите hello [последнюю версию агента MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Требуется установка hello toocomplete права администратора.
6. Затем следует службам Windows гостевой агент может tooview служб
7. Попробуйте запустить, нажав кнопку «Создать резервную копию сейчас» hello портала по запросу и нерегламентированном резервном копировании.

Также проверьте, обладает виртуальной машины  **[.NET 4.5, установленные в системе hello](https://docs.microsoft.com/en-us/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed)**. Это необходимо для hello toocommunicate агента ВМ со службой hello

### <a name="hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vms"></a>Hello агент, установленный в hello виртуальной Машины является устаревшим (для виртуальных машин Linux)

#### <a name="solution"></a>Решение
Большая часть неполадок, связанных с агентом или расширением на виртуальных машинах Linux, вызваны проблемами с устаревшим агентом виртуальной машины. tootroubleshoot эту проблему, следуйте следующим рекомендациям:

1. Следуйте инструкциям hello [обновление hello агент виртуальной Машины Linux](../virtual-machines/linux/update-agent.md).

 >[!NOTE]
 >Мы *настоятельно рекомендуется* обновлении агента hello только с помощью распространения репозитория. Не рекомендуется загрузить код агента hello непосредственно из GitHub и ее обновления. Недоступность hello последнюю версию агента для распространения, обратитесь в службу поддержки распространения инструкции о том, как tooinstall его. toocheck hello последних агента, последовательно выберите toohello [Windows Azure Linux agent](https://github.com/Azure/WALinuxAgent/releases) страницы в репозитории GitHub hello.

2. Убедитесь, что hello Azure агент выполняется на hello виртуальной Машины, выполнив следующую команду hello.`ps -e`

 Если hello процесс не запущен, перезапустите его с помощью hello, следующие команды.

 * Для Ubuntu: `service walinuxagent start`.
 * Для других дистрибутивов: `service waagent start`.

3. [Настройка hello автоматического перезапуска агента](https://github.com/Azure/WALinuxAgent/wiki/Known-Issues#mitigate_agent_crash).
4. Снова запустите резервное копирование для проверки. Если hello ошибка продолжает появляться, соберите следующие журналы из виртуальной Машины клиента hello hello:

   * /var/lib/waagent/*.xml
   * /var/log/waagent.log
   * /var/log/azure/*

Если нам потребуется подробное ведение журнала для waagent, выполните следующие действия.

1. Найдите в файле /etc/waagent.conf hello следующей строкой hello: **включите подробное ведение журнала (y | n)**
2. Изменение hello **Logs.Verbose** значение из  *n*  слишком*y*.
3. Сохранить изменение hello, а затем перезапустите waagent следуя hello предыдущие шаги в этом разделе.

### <a name="hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>не удается получить состояние Hello моментальных снимков или моментальный снимок не может быть выполнено
резервное копирование виртуальных Машин Hello зависит от того, выдачи моментального снимка команда toohello базовой учетной записи хранилища. Резервное копирование может произойти сбой, у него нет учетной записи хранения toohello доступа или откладывается hello выполнение задачи моментальных снимков hello.

#### <a name="solution"></a>Решение
Привет, следующие условия могут вызвать сбой задачи моментальных снимков:

| Причина: | Решение |
| --- | --- |
| Hello виртуальной Машины имеет настройки резервного копирования SQL Server. | По умолчанию hello ВМ архивация выполняется полное резервное копирование VSS на виртуальных машинах Windows. Если на виртуальной машине запущен сервер на основе SQL Server и настроена архивация SQL Server, то при создании моментального снимка может возникнуть задержка.<br><br>При возникновении сбоя резервного копирования из-за проблем с моментального снимка, задайте hello следующий раздел реестра:<br><br>**[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT] "USEVSSCOPYBACKUP"="TRUE"** |
| состояние виртуальной Машины Hello возникает неправильно из-за hello виртуальной Машины будет выполнено завершение работы протокола удаленного рабочего СТОЛА. | При выключении hello ВМ в протокол удаленного рабочего стола (RDP), проверьте наличие портала toodetermine hello hello состояние виртуальной Машины указано правильно. Если это не так, завершите работу hello ВМ на портале hello с помощью hello **завершение работы** параметр на панели мониторинга виртуальной Машины hello. |
| Много виртуальных машин из hello одной облачной службе, настроенной, tooback на hello то же время. | Это наиболее toospread рекомендаций out hello расписания резервного копирования для виртуальных машин из hello же облачной службе. |
| Hello виртуальная машина работает на высокую загруженность ЦП или памяти. | Если hello виртуальная машина работает на высокая загрузка ЦП (более 90%) или использовании большого объема памяти, задачу hello моментальных снимков в очереди и отложенной и ее время ожидания истекает. В таких ситуациях попробуйте использовать архивацию по запросу. |
| Hello виртуальной Машины не удается получить hello и структура узла адрес у DHCP-сервера. | DHCP должна быть включена в гостевой системе hello для резервного копирования toowork ВМ IaaS hello.  Если hello виртуальной Машины не может получить hello и структура узла адрес из ответа DHCP 245, не может загружать или выполнения каких-либо расширений. Если вам требуется статический частных IP-адрес, его следует настроить посредством hello. Здравствуйте, DHCP-параметра внутри приветствия следует оставить ВМ включен. Дополнительные сведения см. в статье [Как задать статический внутренний частный IP-адрес с помощью PowerShell (классическая модель)](../virtual-network/virtual-networks-reserved-private-ip.md). |

### <a name="hello-backup-extension-fails-tooupdate-or-load"></a>расширение резервного копирования Hello завершается с ошибкой tooupdate или нагрузки
Если не удается загрузить расширения, получить моментальный снимок состояния невозможно, и архивация завершится сбоем.

#### <a name="solution"></a>Решение

**Для гостевых систем Windows:** убедитесь, что служба iaasvmprovider hello включен и имеет тип запуска *автоматического*. Если служба hello не настроена таким образом, включите toodetermine ли следующая резервная копия hello завершается успешно.

**Для гостевых систем Linux:** проверьте hello последняя версия VMSnapshot для Linux (расширение hello использовался резервной копии) — 1.0.91.0.<br>


Если расширение резервного копирования hello по-прежнему не tooupdate или нагрузки, можно принудительно hello VMSnapshot расширения toobe перезагружен путем удаления расширения hello. Hello следующей резервной копии попытки перезагрузит hello расширения.

toouninstall Здравствуйте расширения, hello следующие:

1. Go toohello [портал Azure](https://portal.azure.com/).
2. Найдите hello виртуальной Машины с резервного копирования проблемы.
3. Щелкните **Параметры**.
4. Щелкните **Расширения**.
5. Щелкните **Vmsnapshot Extension** (Расширение Vmsnapshot).
6. Нажмите кнопку **Удалить**.

При выполнении этой процедуры повторной установки во время следующего резервного копирования hello toobe расширения hello.

