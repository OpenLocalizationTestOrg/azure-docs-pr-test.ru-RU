---
title: "aaaProtect Active Directory и DNS с помощью Azure Site Recovery | Документы Microsoft"
description: "В этой статье описывается как tooimplement решение аварийного восстановления для Active Directory с помощью Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: af1d9b26-1956-46ef-bd05-c545980b72dc
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 7/20/2017
ms.author: pratshar
ms.openlocfilehash: 49903e54f6d6e1839b0571b7a852c6d7517f0aa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="protect-active-directory-and-dns-with-azure-site-recovery"></a>Защита Active Directory и DNS с Azure Site Recovery
Корпоративных приложений, таких как SharePoint, Dynamics AX и SAP зависят от Active Directory и инфраструктуры DNS toofunction правильно. При создании решения аварийного восстановления для приложений является важным tooremember требуется tooprotect и восстановления Active Directory и DNS до hello другие компоненты приложения, tooensure, вещей правильной после аварии.

Site Recovery — это служба Azure, которая обеспечивает аварийное восстановление, управляя процессами репликации, отработки отказа и восстановления виртуальных машин. Site Recovery поддерживает ряд tooconsistently защита сценариев репликации и без проблем отработки отказа виртуальных машин и приложений tooprivate, public или поставщика услуг размещения облака.

С помощью Site Recovery можно создать полностью автоматизированный план аварийного восстановления для Active Directory. При прерывании работы отработку отказа можно запустить из любого места в течение нескольких секунд и таким образом восстановить работоспособность Active Directory за считанные минуты. Если вы развернули Active Directory для нескольких приложений, таких как SharePoint и SAP на основном сайте, и хотите toofail узла, а полный hello, можно выполнить переход первой с помощью Active Directory Site Recovery, а затем переход hello других приложений с помощью планов восстановления конкретного приложения.

В этой статье объясняется, как toocreate решение аварийного восстановления для Active Directory, как tooperform плановой, незапланированной и тестовой отработки отказа плана восстановления одним щелчком с помощью hello поддерживаемые конфигурации и необходимые компоненты.  Перед началом работы необходимо ознакомиться с Active Directory и Azure Site Recovery.

## <a name="replicating-domain-controller"></a>Репликация контроллера домена

Требуется toosetup [Site Recovery репликации](#enable-protection-using-site-recovery) на по крайней мере одну виртуальную машину, размещение контроллера домена и DNS. Если у вас есть [нескольких контроллеров домена](#environment-with-multiple-domain-controllers) в вашей среде, кроме tooreplicating hello виртуальную машину контроллера домена с Site Recovery, также необходимо будет tooset копирование [дополнительного контроллера домена](#protect-active-directory-with-active-directory-replication) на целевом сайте hello (Azure или в дополнительный локальный центр обработки данных). 

### <a name="single-domain-controller-environment"></a>Среда с одним контроллером домена
Если у вас есть несколько приложений и только один контроллер домена и требуется toofail всего узла hello вместе, то рекомендуется использовать контроллер домена hello tooreplicate Site Recovery toohello вторичного сайта (ли отработка отказа tooAzure или tooa вторичного сайта). Hello же реплицированных домена, контроллера или DNS виртуальной машины можно использовать для [тестовая отработка отказа](#test-failover-considerations) также.

### <a name="environment-with-multiple-domain-controllers"></a>Среда с несколькими контроллерами доменов
Если у вас есть множество приложений и имеется более одного контроллера домена в среде hello или если планируется toofail через несколько приложений одновременно, рекомендуется, кроме виртуального контроллера домена hello tooreplicating машины с Site Recovery можно также Настройка [дополнительного контроллера домена](#protect-active-directory-with-active-directory-replication) на целевом сайте hello (Azure или в дополнительный локальный центр обработки данных). Для [тестовая отработка отказа](#test-failover-considerations), используется контроллер домена реплицирован с Site Recovery и перехода на другой ресурс, hello дополнительного контроллера домена на целевом сайте hello. 


Hello следующих разделах объясняется, как tooenable защиты для контроллера домена в Site Recovery и как tooset контроллера домена в Azure.

## <a name="prerequisites"></a>Предварительные требования
* Локально развернутые Active Directory и DNS-сервер.
* Хранилище служб Azure Site Recovery в подписке Microsoft Azure.
* Если выполняется репликация tooAzure, запустите средство оценки готовности виртуальной машины Azure hello на виртуальные машины tooensure они совместимы с виртуальными машинами Azure и служб Azure Site Recovery.

## <a name="enable-protection-using-site-recovery"></a>Включение защиты с помощью Site Recovery
### <a name="protect-hello-virtual-machine"></a>Защита виртуальной машины hello
Включите защиту виртуальной машины контроллера или DNS-hello домена в Site Recovery. Настройте параметры Site Recovery, на основе типа виртуальной машины hello (Hyper-V или VMware). контроллер домена Hello, реплицируемые с помощью восстановления сайта используется для [тестовая отработка отказа](#test-failover-considerations). Убедитесь, что она соответствует hello следующие требования:

1. Hello контроллер домена является сервером глобального каталога
2. Hello контроллер домена должен быть владельцем роли FSMO hello для роли, которые потребуются во время тестовой отработки отказа (в противном случае эти роли потребуется toobe [захвачен](http://aka.ms/ad_seize_fsmo) после отработки отказа hello)

### <a name="configure-virtual-machine-network-settings"></a>Настройка сетевых параметров виртуальной машины
Для виртуальной машины контроллера или DNS-домена hello Настройка параметров сети в Site Recovery, чтобы hello виртуальная машина будет вложенного toohello правильной сети после отработки отказа. 

![Параметры сети виртуальных машин](./media/site-recovery-active-directory/DNS-Target-IP.png)

## <a name="protect-active-directory-with-active-directory-replication"></a>Защита Active Directory с помощью репликации Active Directory
### <a name="site-to-site-protection"></a>Защита "сайт-сайт"
Создание контроллера домена на вторичном сайте hello. После повышения роли контроллера домена tooa сервера hello, укажите имя hello Привет одному домену, который используется на первичном сайте hello. Можно использовать hello **Active Directory — сайты и службы** оснастки параметры tooconfigure на связь сайтов hello объекта добавляются сайты toowhich hello. Настраивая параметры связи между сайтами, можно указать время и периодичность репликации между двумя или несколькими сайтами. Дополнительные сведения см. в статье [Расписание репликации между сайтами](https://technet.microsoft.com/library/cc731862.aspx).

### <a name="site-to-azure-protection"></a>Защита "сайт-Azure"
Следуйте инструкциям hello слишком[создания контроллера домена в виртуальной сети Azure](../active-directory/active-directory-install-replica-active-directory-domain-controller.md). После повышения роли контроллера домена tooa сервера hello укажите hello таким же именем домена, используемый на первичном сайте hello.

Затем [перенастроить hello DNS-сервера для виртуальной сети hello](../active-directory/active-directory-install-replica-active-directory-domain-controller.md#reconfigure-dns-server-for-the-virtual-network), toouse hello DNS-сервер в Azure.

![Сеть Azure](./media/site-recovery-active-directory/azure-network.png)

**DNS в рабочей сети Azure**

## <a name="test-failover-considerations"></a>Рекомендации по тестированию отработки отказа
Тестовая отработка отказа проводится в сети, изолированной от рабочей сети, чтобы не мешать выполнению рабочих нагрузок.

В большинстве приложений также требуется наличие hello контроллера домена и toofunction сервера DNS. Таким образом до отказа приложения hello, контроллер домена должен toobe, созданные в toobe hello изолированной сети, для тестовой отработки отказа. Здравствуйте, наиболее простым способом toodo это tooreplicate с Site Recovery виртуальную машину контроллера или DNS-домена. Запустите тестовую отработку отказа виртуальной машины контроллера домена hello перед запуском тестовой отработки отказа плана восстановления hello для приложения hello. Вот как это сделать:

1. [Реплицировать](site-recovery-replicate-vmware-to-azure.md) hello виртуальную машину контроллера или DNS-домена с помощью Site Recovery.
1. Создайте изолированную сеть. Любая виртуальная сеть, созданная в Azure, по умолчанию изолируется от другой сети. Рекомендуется, hello диапазон IP-адресов для этой сети совпадает с таковой рабочей сети. Не включайте для этой сети подключение между сайтами.
1. Укажите IP-адрес DNS в сети hello создан в качестве hello IP-адрес, что предполагается tooget виртуальной машины DNS hello. При реплицировании tooAzure, затем укажите hello IP-адрес для виртуальной Машины, который используется при отработке отказа в hello **целевой IP-адрес** в **вычисления и сеть** параметры. 

    ![Целевой IP-адрес](./media/site-recovery-active-directory/DNS-Target-IP.png) **Целевой IP-адрес**

    ![Тестовая сеть Azure](./media/site-recovery-active-directory/azure-test-network.png)

    **DNS в тестовой сети Azure**

> [!TIP]
> Site Recovery пытается toocreate тестовые виртуальные машины в подсети тем же именем и с помощью hello IP-адрес, предоставленный в качестве **вычисления и сеть** параметры hello виртуальной машины. Если подсеть с таким же именем в hello виртуальной сети Azure, предоставленный для теста отработки отказа, недоступен, то тестовая виртуальная машина создается в первом подсети hello в алфавитном порядке. Если hello целевой IP-адрес является частью выбранной подсети hello, Site Recovery попытается toocreate hello теста отработки отказа виртуальной машины с помощью hello целевой IP-адрес. Если hello целевой IP-адрес не является частью выбранной подсети hello, затем тестовой отработки отказа виртуальной машины создается с помощью любой доступный IP-адрес в hello выбранной подсети. 
>
>


1. Если выполняется репликация на локальном сайте tooanother и вы используете DHCP, следуйте инструкциям hello слишком[Установка DNS и DHCP для тестовой отработки отказа](site-recovery-test-failover-vmm-to-vmm.md#prepare-dhcp)
1. Выполните тестовую отработку отказа hello виртуальную машину контроллера домена в изолированной сети hello. Используйте последние доступные **согласованием приложений** точки восстановления hello домена контроллера toodo hello теста отработки отказа виртуальной машины. 
1. Запустите тестовую отработку отказа для плана восстановления hello, содержащем виртуальные машины приложения hello. 
1. После завершения тестирования **очистку тестовой отработки отказа** на виртуальной машине контроллера домена hello. Этот шаг удаляет hello контроллера домена, который был создан для тестовой отработки отказа.


### <a name="removing-reference-tooother-domain-controllers"></a>Удаление контроллеры домена tooother ссылки
При выполнении тестовой отработки отказа не перевести все контроллеры домена hello в тестовой сети hello. Справочник по tooremove hello других контроллеров домена, которые существуют в вашей рабочей среде, может потребоваться слишком[изменения размера ролей FSMO Active Directory](http://aka.ms/ad_seize_fsmo) и выполните [очистку метаданных](https://technet.microsoft.com/library/cc816907.aspx) для домена отсутствует контроллеры. 



> [!IMPORTANT]
> Некоторые конфигурации hello, описанные в следующем разделе hello не конфигураций контроллеров домена по умолчанию standard hello. Если вы не хотите toomake контроллера домена рабочей среде эти изменения tooa, то можно создать toobe выделенной контроллера домена, используется для восстановления сайта тестовой отработки отказа и внести эти изменения toothat.  
>
>

### <a name="issues-because-of-virtualization-safeguards"></a>Вопросы, связанные с мерами по обеспечению безопасности виртуализации 

Начиная с Windows Server 2012 в [Active Directory Domain Services предусмотрены дополнительные меры безопасности](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100). Эти меры безопасности помогают защитить виртуализированные контроллеры домена от отката USN, при условии, что базовая платформа низкоуровневой оболочки hello поддерживает ИД создания Виртуальной машины. Azure поддерживает VM-GenerationID, это означает, что контроллеры домена под управлением Windows Server 2012 или более поздней версии на виртуальных машинах Azure hello дополнительные меры безопасности. 


При сбросе hello Виртуальной машины также сбрасывается invocationID hello базы данных hello AD DS, удаляется пул RID hello и SYSVOL помечается как не заслуживающий доверия. Дополнительные сведения см. в разделе [tooActive введение виртуализация](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100) и [безопасная виртуализация DFSR](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)

Переход tooAzure может привести сброса Виртуальной машины и, будет запущено hello дополнительные меры безопасности при запуске виртуальной машины контроллера домена hello в Azure. Это может привести к **значительной задержкой** в виртуальную машину контроллера домена может toologin toohello пользователя. Так как этот контроллер домена будет использоваться только для тестовой отработки отказа, меры безопасности виртуализации не обязательны. tooensure, ИД создания Виртуальной машины для виртуальной машины контроллера домена hello не меняется, то можно изменить значение hello следующие too4 DWORD в hello на локальном контроллере домена.

        
        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\gencounter\Start
 

#### <a name="symptoms-of-virtualization-safeguards"></a>Признаки применения мер по обеспечению безопасности виртуализации
 
Если меры безопасности виртуализации применены после тестовой отработки отказа, вы увидите один или несколько следующих признаков.  

Изменение идентификатора создания

![Изменение идентификатора создания](./media/site-recovery-active-directory/Event2170.png)

Изменение идентификатора вызова

![Изменение идентификатора вызова](./media/site-recovery-active-directory/Event1109.png)

Общие папки Sysvol и Netlogon не доступны

![Общая папка Sysvol](./media/site-recovery-active-directory/sysvolshare.png)

![Ntfrs Sysvol](./media/site-recovery-active-directory/Event13565.png)

Удалена база данных DFSR

![Удаление базы данных DFSR](./media/site-recovery-active-directory/Event2208.png)


> [!IMPORTANT]
> Некоторые конфигурации hello, описанные в следующем разделе hello не конфигураций контроллеров домена по умолчанию standard hello. Если вы не хотите toomake контроллера домена рабочей среде эти изменения tooa, то можно создать toobe выделенной контроллера домена, используется для восстановления сайта тестовой отработки отказа и внести эти изменения toothat.  
>
>


### <a name="troubleshooting-domain-controller-issues-during-test-failover"></a>Устранение неполадок контроллера домена при тестовой отработке отказа


Запустите командную строку hello, следующая команда toocheck ли папки SYSVOL и NETLOGON являются общими:

    NET SHARE

На hello командной строки выполните следующую команду, что tooensure, hello контроллер домена работает правильно hello.

    dcdiag /v > dcdiag.txt

В журнал выходные данные hello найдите следующий текст tooconfirm, hello контроллер домена работает нормально. 

* "passed test Connectivity"
* "passed test Advertising"
* "passed test MachineAccount"

Если hello выше условия выполнены, весьма вероятно, этот контроллер домена hello работает нормально. Если нет, попробуйте сделать следующее.


* Выполните принудительное восстановление контроллера домена hello.
    * Несмотря на то, что он является [не рекомендуется репликации toouse FRS](https://blogs.technet.microsoft.com/filecab/2014/06/25/the-end-is-nigh-for-frs/), но если по-прежнему используют ее, а затем выполните инструкции hello [здесь](https://support.microsoft.com/kb/290762) toodo принудительное восстановление. Можно прочитать дополнительные сведения о Burflags говорили о ссылке на предыдущую hello [здесь](https://blogs.technet.microsoft.com/janelewis/2006/09/18/d2-and-d4-what-is-it-for/).
    * При использовании DFSR репликации выполните hello действия доступны [здесь](https://support.microsoft.com/kb/2218556) toodo принудительное восстановление. Для этой цели также можно использовать функции Powershell, доступные по этой [ссылке](https://blogs.technet.microsoft.com/thbouche/2013/08/28/dfsr-sysvol-authoritative-non-authoritative-restore-powershell-functions/). 
    
* Обойдите требование начальной синхронизации, задав следующие too0 ключа реестра в hello на локальном контроллере домена. Если параметр DWORD не существует, его можно создать в узле Parameters. Подробнее об этом можно прочитать [здесь](https://support.microsoft.com/kb/2001093).

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Repl Perform Initial Synchronizations

* Отключите требование hello, что сервер глобального каталога является доступных toovalidate входа пользователя, задав следующие too1 ключа реестра в hello на локальном контроллере домена. Если параметр DWORD не существует, его можно создать на узле Lsa. Подробнее об этом можно прочитать [здесь](http://support.microsoft.com/kb/241789).

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\IgnoreGCFailures



### <a name="dns-and-domain-controller-on-different-machines"></a>Контроллер домена и DNS на разных компьютерах
Если DNS не включена в hello одну виртуальную машину контроллера домена hello, должен иметь toocreate DNS виртуальной Машины для тестовой отработки отказа hello. Если они Здравствуйте одной виртуальной Машины, этот раздел можно пропустить.

Можно использовать новый DNS-сервер и создать все необходимые hello зоны. Например если вашим доменом Active Directory — contoso.com, можно создать зону DNS с именем contoso.com hello. Hello записи, соответствующие tooActive каталога необходимо обновить в DNS, следующим образом:

1. Убедитесь, что эти параметры действуют до появится другой виртуальной машине в плане восстановления hello.
   
   * Hello зона должна быть названа корневое имя леса hello.
   * Hello зону должно быть резервного файла.
   * зоне Hello, должны быть включены безопасные и небезопасные обновления.
   * разрешения Hello виртуальную машину контроллера домена hello должна указывать IP-адрес toohello hello DNS виртуальной машины.
2. Выполните следующую команду на виртуальной машине контроллера домена hello.
   
    `nltest /dsregdns`
3. Добавление зоны на DNS-сервере hello, разрешить небезопасные обновления и добавить запись для него tooDNS:
   
        dnscmd /zoneadd contoso.com  /Primary
        dnscmd /recordadd contoso.com  contoso.com. SOA %computername%.contoso.com. hostmaster. 1 15 10 1 1
        dnscmd /recordadd contoso.com %computername%  A <IP_OF_DNS_VM>
        dnscmd /config contoso.com /allowupdate 1

## <a name="next-steps"></a>Дальнейшие действия
Чтение [какие рабочие нагрузки защитить?](site-recovery-workload.md) toolearn Дополнительные сведения о защите рабочих нагрузок предприятия с помощью Azure Site Recovery.

