---
title: "Устранение сбоя службы Azure Backup: состояние гостевого агента \"Недоступно\" | Документация Майкрософт"
description: "Симптомы, причины и способы устранения проблем в работе службы Azure Backup, связанных с агентом, расширением или дисками."
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
ms.topic: troubleshooting
ms.date: 09/08/2017
ms.author: genli;markgal;
ms.openlocfilehash: f3195fa83479986a3e605abce618c78bcdb64dac
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="troubleshoot-azure-backup-failure-issues-with-agent-andor-extension"></a>Устранение неполадок службы Azure Backup: проблемы с агентом и/или расширением

В этой статье описано, как устранять неполадки службы архивации, связанные с ошибками связи с агентом виртуальной машины и расширением.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="vm-agent-unable-to-communicate-with-azure-backup"></a>Агенту виртуальной машины не удается установить связь со службой Azure Backup
После регистрации виртуальной машины в службе Azure Backup и добавления ее в расписание служба архивации инициирует задание, взаимодействуя с агентом виртуальной машины, чтобы создать моментальный снимок. Любое из следующих условий может помешать активации создания моментального снимка, что может привести к сбою службы Backup. Выполните инструкции по устранению неполадок в указанном порядке и повторите операцию.
##### <a name="cause-1-the-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Причина 1. [У виртуальной машины нет доступа к Интернету](#the-vm-has-no-internet-access)
##### <a name="cause-2-the-agent-is-installed-in-the-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Причина 2. [Агент установлен на виртуальной машине, но не отвечает (для виртуальных машин Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-the-agent-installed-in-the-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Причина 3. [Устарел агент, установленный на виртуальной машине (для виртуальных машин Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Причина 4. [Не удалось получить состояние моментального снимка или создать моментальный снимок](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-the-backup-extension-fails-to-update-or-loadthe-backup-extension-fails-to-update-or-load"></a>Причина 5. [Не удалось обновить или загрузить расширение резервного копирования](#the-backup-extension-fails-to-update-or-load)

## <a name="snapshot-operation-failed-due-to-no-network-connectivity-on-the-virtual-machine"></a>Сбой операции моментального снимка, отсутствует сетевое подключение у виртуальной машины
После регистрации виртуальной машины в службе архивации Azure и добавления ее в расписание служба архивации инициирует задание, взаимодействуя с расширением виртуальной машины, чтобы создать моментальный снимок. Любое из следующих условий может помешать активации создания моментального снимка, что может привести к сбою службы Backup. Выполните инструкции по устранению неполадок в указанном порядке и повторите операцию.
##### <a name="cause-1-the-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Причина 1. [У виртуальной машины нет доступа к Интернету](#the-vm-has-no-internet-access)
##### <a name="cause-2-the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Причина 2. [Не удалось получить состояние моментального снимка или создать моментальный снимок](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-3-the-backup-extension-fails-to-update-or-loadthe-backup-extension-fails-to-update-or-load"></a>Причина 3. [Не удалось обновить или загрузить расширение резервного копирования](#the-backup-extension-fails-to-update-or-load)

## <a name="vmsnapshot-extension-operation-failed"></a>Не удалось выполнить операцию с расширением моментального снимка виртуальной машины

После регистрации виртуальной машины в службе архивации Azure и добавления ее в расписание служба архивации инициирует задание, взаимодействуя с расширением виртуальной машины, чтобы создать моментальный снимок. Любое из следующих условий может помешать активации создания моментального снимка, что может привести к сбою службы Backup. Выполните инструкции по устранению неполадок в указанном порядке и повторите операцию.
##### <a name="cause-1-the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Причина 1. [Не удалось получить состояние моментального снимка или создать моментальный снимок](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-2-the-backup-extension-fails-to-update-or-loadthe-backup-extension-fails-to-update-or-load"></a>Причина 2. [Не удалось обновить или загрузить расширение резервного копирования](#the-backup-extension-fails-to-update-or-load)
##### <a name="cause-3-the-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Причина 3. [У виртуальной машины нет доступа к Интернету](#the-vm-has-no-internet-access)
##### <a name="cause-4-the-agent-is-installed-in-the-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Причина 4. [Агент установлен на виртуальной машине, но не отвечает (для виртуальных машин Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-5-the-agent-installed-in-the-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Причина 5. [Устарел агент, установленный на виртуальной машине (для виртуальных машин Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)

## <a name="unable-to-perform-the-operation-as-the-vm-agent-is-not-responsive"></a>Не удалось выполнить операцию, так как агент виртуальной машины не отвечает

После регистрации виртуальной машины в службе архивации Azure и добавления ее в расписание служба архивации инициирует задание, взаимодействуя с расширением виртуальной машины, чтобы создать моментальный снимок. Любое из следующих условий может помешать активации создания моментального снимка, что может привести к сбою службы Backup. Выполните инструкции по устранению неполадок в указанном порядке и повторите операцию.
##### <a name="cause-1-the-agent-is-installed-in-the-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Причина 1. [Агент установлен на виртуальной машине, но не отвечает (для виртуальных машин Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-2-the-agent-installed-in-the-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Причина 2. [Устарел агент, установленный на виртуальной машине (для виртуальных машин Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-3-the-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Причина 3. [У виртуальной машины нет доступа к Интернету](#the-vm-has-no-internet-access)

## <a name="backup-failed-with-an-internal-error---please-retry-the-operation-in-a-few-minutes"></a>Произошла внутренняя ошибка службы Backup. Повторите операцию через несколько минут

После регистрации виртуальной машины в службе архивации Azure и добавления ее в расписание служба архивации инициирует задание, взаимодействуя с расширением виртуальной машины, чтобы создать моментальный снимок. Любое из следующих условий может помешать активации создания моментального снимка, что может привести к сбою службы Backup. Выполните инструкции по устранению неполадок в указанном порядке и повторите операцию.
##### <a name="cause-1-the-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Причина 1. [У виртуальной машины нет доступа к Интернету](#the-vm-has-no-internet-access)
##### <a name="cause-2-the-agent-installed-in-the-vm-but-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Причина 2. [Агент установлен на виртуальной машине, но не отвечает (для виртуальных машин Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-the-agent-installed-in-the-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Причина 3. [Устарел агент, установленный на виртуальной машине (для виртуальных машин Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Причина 4. [Не удалось получить состояние моментального снимка или создать моментальный снимок](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-the-backup-extension-fails-to-update-or-loadthe-backup-extension-fails-to-update-or-load"></a>Причина 5. [Не удалось обновить или загрузить расширение резервного копирования](#the-backup-extension-fails-to-update-or-load)

## <a name="the-specified-disk-configuration-is-not-supported"></a>Указанная конфигурация диска не поддерживается

Сейчас служба Azure Backup не поддерживает размер диска [больше 1023 ГБ](https://docs.microsoft.com/azure/backup/backup-azure-arm-vms-prepare#limitations-when-backing-up-and-restoring-a-vm). 
- При наличии дисков, размер которых больше 1 ТБ, [подключите новые диски](https://docs.microsoft.com/azure/virtual-machines/windows/attach-managed-disk-portal), размер которых меньше 1 ТБ. <br>
- Затем скопируйте данные с диска, размер которого больше 1 ТБ, на недавно созданные диски размером меньше 1 ТБ. <br>
- Убедитесь, что все данные скопированы, и удалите диски размером больше 1 ТБ.
- Запустите резервное копирование.

## <a name="causes-and-solutions"></a>Причины и решения

### <a name="the-vm-has-no-internet-access"></a>У виртуальной машины нет доступа к Интернету
Согласно требованиям к развертыванию виртуальная машина не имеет доступа к Интернету или существуют ограничения на доступ к инфраструктуре Azure.

Для правильной работы расширения службы архивации требуется возможность подключения к общедоступным IP-адресам Azure. Для управления моментальными снимками виртуальной машины это расширение отправляет команды к конечной точке службы хранилища Azure (URL-адрес HTTP). Если расширение не имеет доступа к общедоступному Интернету, архивация завершится сбоем.

####  <a name="solution"></a>Решение
Для устранения этой проблемы воспользуйтесь одним из указанных ниже способов.
##### <a name="allow-access-to-the-azure-datacenter-ip-ranges"></a>Разрешение доступа к диапазонам IP-адресов центра обработки данных Azure

1. Получите [список IP-адресов центра обработки данных Azure](https://www.microsoft.com/download/details.aspx?id=41653), чтобы разрешить доступ к ним.
2. Разблокируйте IP-адреса, выполнив командлет **New-NetRoute** на виртуальной машине Azure в окне PowerShell с повышенными привилегиями. Выполните этот командлет с привилегиями администратора.
3. Чтобы разрешить доступ к этим IP-адресам, добавьте соответствующие правила в группу безопасности сети (если она настроена).

##### <a name="create-a-path-for-http-traffic-to-flow"></a>Создание пути для прохождения трафика HTTP

1. При наличии каких-либо ограничений сети (например, группы безопасности сети) разверните прокси-сервер HTTP для маршрутизации трафика.
2. Если вы используете группу безопасности сети, добавьте в нее правила, чтобы разрешить доступ к Интернету с прокси-сервера HTTP.

Чтобы узнать, как настроить прокси-сервер HTTP для архивации виртуальных машин, ознакомьтесь с разделом [Подготовка среды для резервного копирования виртуальных машин Azure](backup-azure-vms-prepare.md#using-an-http-proxy-for-vm-backups).

В случае если вы используете управляемые диски, может потребоваться открыть в брандмауэрах дополнительный порт (8443).

### <a name="the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Агент установлен на виртуальной машине, но не отвечает (для виртуальных машин Windows)

#### <a name="solution"></a>Решение
Возможно, агент виртуальной машины может быть поврежден или служба остановлена. Повторная установка агента виртуальной машины поможет получить последнюю версию и возобновить обмен данными.

1. Проверьте, запущена ли служба гостевого агента Windows в службах компьютера (services.msc) на виртуальной машине. Попробуйте перезапустить службу гостевого агента Windows и запустите резервное копирование<br>
2. Если она не отображается в списке служб, проверьте в разделе "Программы и компоненты", установлена ли служба гостевого агента Windows.
4. Если вы можете просматривать раздел "Программы и компоненты", удалите гостевой агент Windows.
5. Скачайте и установите [последнюю версию файла MSI агента](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Чтобы выполнить установку, необходимо иметь права администратора.
6. Затем можно будет просмотреть службу гостевого агента Windows в службах.
7. Попробуйте выполнить резервное копирование по запросу или нерегламентированное резервное копирование, щелкнув "Моментальная архивация" на портале.

Также проверьте, установлен ли на виртуальной машине компонент **[.NET 4.5](https://docs.microsoft.com/en-us/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed)**. Он необходим для взаимодействия агента виртуальной машины со службой.

### <a name="the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Устарел агент, установленный на виртуальной машине (для виртуальных машин Linux)

#### <a name="solution"></a>Решение
Большая часть неполадок, связанных с агентом или расширением на виртуальных машинах Linux, вызваны проблемами с устаревшим агентом виртуальной машины. Чтобы устранить эту проблему, следуйте приведенным ниже общим рекомендациям.

1. Выполните указания по [обновлению агента виртуальной машины Linux ](../virtual-machines/linux/update-agent.md).

 >[!NOTE]
 >Мы *настоятельно рекомендуем* обновлять агент только посредством репозитория дистрибутивов. Мы не рекомендуем скачивать код агента непосредственно с портала GitHub и обновлять его. Если последняя версия агента для вашего дистрибутива недоступна, обратитесь в службу поддержки дистрибутива, чтобы получить инструкции по установке последней версии агента. Чтобы проверить наличие последней версии агента, перейдите на страницу [агента Linux для Microsoft Azure](https://github.com/Azure/WALinuxAgent/releases) в репозитории GitHub.

2. Убедитесь, что на виртуальной машине запущен агент Azure, выполнив команду `ps -e`.

 Если нужный процесс не запущен, используйте следующие команды для его перезапуска.

 * Для Ubuntu: `service walinuxagent start`.
 * Для других дистрибутивов: `service waagent start`.

3. [Настройте автоматический перезапуск агента](https://github.com/Azure/WALinuxAgent/wiki/Known-Issues#mitigate_agent_crash).
4. Снова запустите резервное копирование для проверки. Если ошибка не исчезла, извлеките следующие журналы из виртуальной машины клиента:

   * /var/lib/waagent/*.xml
   * /var/log/waagent.log
   * /var/log/azure/*

Если нам потребуется подробное ведение журнала для waagent, выполните следующие действия.

1. В файле /etc/waagent.conf найдите такую строку: **Enable verbose logging (y|n)**.
2. Для параметра **Logs.Verbose** измените значение с *n* на *y*.
3. Сохраните изменения и перезапустите waagent, как описано выше в этом разделе.

### <a name="the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Не удалось получить состояние моментального снимка или создать моментальный снимок
Архивация виртуальных машин зависит от команды создания моментального снимка в базовой учетной записи хранения. Сбой службы архивации может произойти, если она не имеет доступа к учетной записи хранения или выполнение задачи создания моментального снимка задерживается.

#### <a name="solution"></a>Решение
Сбой задачи создания снимка может быть вызван следующими условиями.

| Причина: | Решение |
| --- | --- |
| Для виртуальной машины настроена архивация SQL Server. | По умолчанию при архивации виртуальной машины выполняется полная архивация VSS на виртуальных машинах Windows. Если на виртуальной машине запущен сервер на основе SQL Server и настроена архивация SQL Server, то при создании моментального снимка может возникнуть задержка.<br><br>Если у вас возникают ошибки архивации из-за проблемы с моментальными снимками, настройте приведенный ниже ключ реестра.<br><br>**[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT] "USEVSSCOPYBACKUP"="TRUE"** |
| Состояние виртуальной машины отображается неправильно из-за того, что работа виртуальной машины была завершена в сеансе удаленного рабочего стола. | Когда вы завершаете работу виртуальной машины в сеансе удаленного рабочего стола (RDP), проверьте, правильно ли отображается состояние виртуальной машины на портале. Если это не так, завершите работу виртуальной машины на портале с помощью операции **Завершение работы** на панели мониторинга виртуальной машины. |
| Для нескольких виртуальных машин из одной облачной службы резервное копирование выполняется в одно и то же время. | Рекомендуется распределить архивацию виртуальных машин из одной облачной службы так, чтобы она выполнялась в разное время. |
| Виртуальная машина использует большие ресурсы процессора или памяти. | Если виртуальная машина работает с высоким уровнем загрузки ЦП (более 90 %) или использует большой объем памяти, задача создания моментального снимка помещается в очередь и время ее ожидания истекает. В таких ситуациях попробуйте использовать архивацию по запросу. |
| Виртуальная машина не может получить адрес узла или структуры по протоколу DHCP. | Чтобы архивация виртуальной машины IaaS работала, в гостевой учетной записи нужно включить протокол DHCP.  Если виртуальная машина не может получить адрес узла или структуры в виде ответа DHCP 245, то она не сможет скачать или запустить какие-либо расширения. Если вам нужен статический частный IP-адрес, следует настроить его через платформу. DHCP для виртуальной машины следует оставить включенным. Дополнительные сведения см. в статье [Как задать статический внутренний частный IP-адрес с помощью PowerShell (классическая модель)](../virtual-network/virtual-networks-reserved-private-ip.md). |

### <a name="the-backup-extension-fails-to-update-or-load"></a>Не удалось обновить или загрузить расширение резервного копирования
Если не удается загрузить расширения, получить моментальный снимок состояния невозможно, и архивация завершится сбоем.

#### <a name="solution"></a>Решение

**Для гостевых систем Windows:** убедитесь, что служба iaasvmprovider включена и для нее установлен *автоматический* тип запуска. Если это не так, включите эту службу и проверьте, будет ли успешно выполнена следующая архивация.

**Для гостевых систем Linux:** убедитесь, что последняя версия Linux VMSnapshot (расширение, используемое службой архивации) — 1.0.91.0.<br>


Если расширение резервной копии по-прежнему не удается обновить или загрузить, попробуйте принудительно перезагрузить расширение VMSnapshot, удалив это расширение. Расширение будет перезагружено при следующей попытке резервного копирования.

Чтобы удаление расширение, выполните следующее.

1. Перейдите на [портал Azure](https://portal.azure.com/).
2. Найдите виртуальную машину, с архивацией которой возникли проблемы.
3. Щелкните **Параметры**.
4. Щелкните **Расширения**.
5. Щелкните **Vmsnapshot Extension** (Расширение Vmsnapshot).
6. Нажмите кнопку **Удалить**.

После этого расширение будет повторно установлено при следующей архивации.

