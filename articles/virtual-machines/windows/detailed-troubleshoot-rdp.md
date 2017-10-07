---
title: "удаленный рабочий стол aaaDetailed Устранение неполадок в Azure | Документы Microsoft"
description: "Просмотрите сведения об устранении неполадок для удаленного рабочего стола ошибок, где вы не можете tooa виртуальных машинах в Azure"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
keywords: "не удается подключиться tooremote рабочего стола, устранение неполадок удаленного рабочего стола удаленного рабочего стола не удается подключиться, удаленного рабочего стола устранения неполадок, удаленного рабочего стола ошибок, проблем удаленного рабочего стола"
ms.assetid: 9da36f3d-30dd-44af-824b-8ce5ef07e5e0
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: fcb0d06aa66b748f3ebbbbe3431471d3cbe7c60d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-troubleshooting-steps-for-remote-desktop-connection-issues-toowindows-vms-in-azure"></a>Сведения об устранении неполадок подключения к удаленному рабочему столу выдает tooWindows ВМ в Azure
Этой статье содержатся сведения об устранении неполадок toodiagnose и исправление ошибок сложных удаленного рабочего стола для Windows Azure виртуальных машин под управлением.

> [!IMPORTANT]
> Здравствуйте, наиболее часто встречающихся ошибок удаленного рабочего стола, убедитесь, что tooread tooeliminate [Основные статьи по устранению неполадок hello для удаленного рабочего стола](troubleshoot-rdp-connection.md) перед продолжением.

Удаленный рабочий стол, охваченных сообщение об ошибке, не похож hello специальные сообщения об ошибках могут возникнуть [hello базового удаленного рабочего стола, руководство по устранению неполадок](troubleshoot-rdp-connection.md). Выполните эти шаги toodetermine, почему hello клиента удаленного рабочего стола (RDP) — служба протокола удаленного рабочего СТОЛА не удается tooconnect toohello на виртуальной Машине Azure hello.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello экспертов Azure на [hello MSDN Azure и hello переполнения стека форумы](https://azure.microsoft.com/support/forums/). Кроме того, можно зарегистрировать обращение в службу поддержки Azure. Go toohello [сайте поддержки Azure](https://azure.microsoft.com/support/options/) и нажмите кнопку **Get Support**. Сведения об использовании поддержки Azure см. в статье hello [ответы поддержки Microsoft Azure](https://azure.microsoft.com/support/faq/).

## <a name="components-of-a-remote-desktop-connection"></a>Компоненты подключения к удаленному рабочему столу
следующие компоненты Hello участвуют в RDP-подключение.

![](./media/detailed-troubleshoot-rdp/tshootrdp_0.png)

Прежде чем продолжить, будет полезно toomentally проверьте, что были изменены с момента hello последнего успешного удаленного рабочего стола подключения toohello виртуальной Машины. Например:

* Здравствуйте, общедоступный IP-адрес hello виртуальной Машины или hello облачной службе, содержащей hello виртуальной Машины (также называется hello виртуальный IP-адрес [виртуальных IP-адресов](https://en.wikipedia.org/wiki/Virtual_IP_address)) был изменен. Hello RDP сбоя может быть вызвано DNS кэша клиента по-прежнему содержит hello *старый IP-адрес* зарегистрирован для hello DNS-имени. Очистить кэш клиента DNS и повторите попытку подключения hello виртуальной Машины. Или попробуйте подключиться напрямую с hello новый виртуальный IP-адрес.
* Вместо использования hello соединение, созданное hello портал Azure используют toomanage приложений сторонних разработчиков подключений к удаленному рабочему столу. Убедитесь, что в этой конфигурации приложения hello включает hello правильный TCP-порт для трафика удаленного рабочего стола hello. Вы можете проверить этот порт для классической виртуальной машины в hello [портал Azure](https://portal.azure.com), щелкнув параметры виртуальной Машины hello > конечные точки.

## <a name="preliminary-steps"></a>Предварительные действия
Прежде чем продолжить toohello подробные сведения об устранении,

* Проверьте состояние виртуальной машины hello в hello портала Azure по вопросам очевидным hello.
* Выполните hello [быстрого исправления для типичных ошибок протокола удаленного рабочего СТОЛА в hello устранение основных неполадок представлены инструкции](troubleshoot-rdp-connection.md#quick-troubleshooting-steps).

Выполните повторное подключение toohello виртуальной Машине через удаленный рабочий стол после выполнения этих шагов.

## <a name="detailed-troubleshooting-steps"></a>Подробное описание устранения неполадок
Клиент удаленного рабочего стола Hello не может быть службы удаленного рабочего стола hello может tooreach на виртуальной Машине Azure hello из-за tooissues на hello следующие источники:

* [Компьютер с клиентом удаленного рабочего стола](#source-1-remote-desktop-client-computer)
* [Пограничное устройство интрасети организации](#source-2-organization-intranet-edge-device)
* [Конечная точка облачной службы и список управления доступом (ACL)](#source-3-cloud-service-endpoint-and-acl)
* [Группы безопасности сети](#source-4-network-security-groups)
* [Виртуальная машина Azure под управлением Windows](#source-5-windows-based-azure-vm)

## <a name="source-1-remote-desktop-client-computer"></a>Источник 1: компьютер с клиентом удаленного рабочего стола
Убедитесь, что ваш компьютер может предоставить удаленного рабочего стола подключений tooanother локально, компьютер под управлением Windows.

![](./media/detailed-troubleshoot-rdp/tshootrdp_1.png)

Если это невозможно, проверьте следующие параметры на компьютере hello.

* Настройки локального брандмауэра, которые могут блокировать обмен данными с удаленным рабочим столом.
* Наличие локального программного обеспечения с функциями прокси-сервера, которое не позволяет установить подключение к удаленному рабочему столу.
* Наличие локального программного обеспечения для мониторинга сети, которое не позволяет установить подключение к удаленному рабочему столу.
* Наличие других программ для обеспечения безопасности, которые ведут мониторинг трафика либо разрешают и запрещают трафик определенных типов, поэтому могут блокировать подключение к удаленному рабочему столу.

Во всех этих случаях временно отключить hello программное обеспечение и попробуйте tooconnect tooan на локальном компьютере через удаленный рабочий стол. Если вы можете найти действительную причину hello таким образом, работаете с вашей сетевой администратор toocorrect hello программного обеспечения параметры tooallow подключений удаленного рабочего стола.

## <a name="source-2-organization-intranet-edge-device"></a>Источник 2: пограничное устройство интрасети организации
Убедитесь, что компьютер подключен напрямую toohello Интернет освободить tooyour подключения удаленного рабочего стола виртуальной машины Azure.

![](./media/detailed-troubleshoot-rdp/tshootrdp_2.png)

Если у вас компьютер, который подключен напрямую toohello Интернет, создайте и протестируйте с новой виртуальной машины Azure в ресурс группы или облачной службы. Дополнительные сведения см. в статье [Создание виртуальной машины Windows в среде Azure](../virtual-machines-windows-hero-tutorial.md). Hello виртуальной машины и группы ресурсов hello или hello облачной службы, можно удалить после тестирования hello.

Если можно создать подключения удаленного рабочего стола с компьютером, присоединенные непосредственно toohello Интернет, проверьте устройство пограничного интрасети организации для:

* Внутренняя брандмауэр, блокирует toohello HTTPS подключения к Интернету.
* прокси-сервера, который не позволяет установить подключение к удаленному рабочему столу;
* программного обеспечения для обнаружения атак и мониторинга сети, которое работает на устройствах в вашей сети периметра и блокирует подключения к удаленным рабочим столам.

Работать с параметры сети toocorrect администратора hello вашей организации интрасети пограничного устройства tooallow удаленного рабочего стола на основе HTTPS соединений toohello Интернета.

## <a name="source-3-cloud-service-endpoint-and-acl"></a>Источник 3: конечная точка облачной службы и список управления доступом (ACL)
Виртуальные машины, созданные с помощью hello классической модели развертывания, убедитесь, что другой виртуальной Машиной Azure, в hello же облачной службе или виртуальной сети можно сделать tooyour подключения удаленного рабочего стола виртуальной Машины Azure.

![](./media/detailed-troubleshoot-rdp/tshootrdp_3.png)

> [!NOTE]
> Для виртуальных машин, созданных в диспетчере ресурсов, пропустить слишком[источника 4: группы безопасности сети](#source-4-network-security-groups).

Если у вас другой виртуальной машины в Здравствуйте одной облачной службе или виртуальной сети, создайте его. Следуйте указаниям hello [создать виртуальную машину под управлением Windows в Azure](../virtual-machines-windows-hero-tutorial.md). Удалите hello тестовой виртуальной машины после завершения теста hello.

При подключении через удаленный рабочий стол tooa виртуальной машины в hello же облачной службе или виртуальной сети, проверьте следующие параметры:

* Hello конфигурации конечной точки для трафика удаленного рабочего стола на целевом сервере hello виртуальной Машины: hello частный порт TCP hello конечной точки должно соответствовать какие hello службы удаленного рабочего стола Виртуальной машины прослушивает порт TCP hello (по умолчанию — 3389).
* Hello ACL для конечной точки трафика hello удаленного рабочего стола на целевом сервере hello виртуальной Машины: списки управления доступом позволяют toospecify разрешает или запрещает входящий трафик от hello Интернет IP-адреса источника. Неправильно настроенные ACL можно предотвратить входящих конечной точки toohello трафика удаленного рабочего стола. Проверьте вашей tooensure списки управления доступом разрешен входящий трафик от общих IP-адреса прокси-сервера или других пограничный сервер. Дополнительные сведения см. в статье [Список управления доступом (ACL) конечной точки](../../virtual-network/virtual-networks-acl.md).

Если конечная точка hello hello источник проблемы hello, toocheck удалить hello текущей конечной точки и создайте новую, выбрав случайный порт в диапазон hello 49152 – 65535 для внешнего порта hello. Дополнительные сведения см. в разделе [как tooset конечные точки tooa виртуальной машины](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="source-4-network-security-groups"></a>Источник 4: группы безопасности сети
Группы безопасности сети позволяют точнее настраивать параметры разрешенного входящего и исходящего трафика. Можно создавать правила, которые распространяются на подсети и облачные службы в виртуальной сети Azure.

Используйте [проверить поток IP](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm, если правила в группе безопасности сети блокирует tooor трафик от виртуальной машины. Можно также просмотреть действующие безопасности группы, которую правила входящих подключений tooensure NSG «разрешить» правило существует и приоритет для порта протокола удаленного рабочего СТОЛА (по умолчанию 3389). Дополнительные сведения см. в разделе [поток трафика с помощью действующие правила безопасности tootroubleshoot виртуальной Машины](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).

## <a name="source-5-windows-based-azure-vm"></a>Источник 5: виртуальная машина Azure под управлением Windows
![](./media/detailed-troubleshoot-rdp/tshootrdp_5.png)

Следуйте инструкциям в разделе hello [в этой статье](reset-rdp.md). В этой статье сбрасывает hello службы удаленного рабочего стола на виртуальной машине hello:

* Включите hello «Удаленный рабочий стол» правило брандмауэра Windows по умолчанию (порт TCP 3389).
* Включите подключения удаленного рабочего стола, задав too0 значение реестра HKLM\System\CurrentControlSet\Control\Terminal Server\fDenyTSConnections hello.

Попробуйте hello с компьютера попытку подключения. Если вы по-прежнему не удается tooconnect через удаленный рабочий стол, проверьте следующие возможные проблемы hello:

* Hello службы удаленного рабочего стола не запущена на целевом сервере hello виртуальной Машины.
* Hello службы удаленного рабочего стола не прослушивает TCP-порт 3389.
* В брандмауэре Windows или другом локальном брандмауэре есть правило для исходящего трафика, блокирующее трафик удаленных рабочих столов.
* Обнаружение вторжений или сетевого мониторинга программного обеспечения на виртуальной машине Azure hello препятствует подключений удаленного рабочего стола.

Для виртуальных машин, созданных с помощью hello классической модели развертывания можно использовать удаленный toohello сеанс Azure PowerShell виртуальной машины Azure. Во-первых необходимо tooinstall сертификат для размещения облачной службы hello виртуальной машины. Go слишком[tooAzure Настройка безопасного удаленного PowerShell доступа виртуальных машин](http://gallery.technet.microsoft.com/scriptcenter/Configures-Secure-Remote-b137f2fe) и загрузите hello **InstallWinRMCertAzureVM.ps1** сценария файла tooyour локального компьютера.

Затем установите Azure PowerShell, если еще не сделали этого. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

Далее откройте командную строку Azure PowerShell и измените текущее расположение toohello папки hello объекта hello **InstallWinRMCertAzureVM.ps1** файла скрипта. toorun сценария Azure PowerShell, необходимо задать правильное выполнение политики hello. Запустите hello **Get-ExecutionPolicy** команды toodetermine текущий уровень политики. Сведения о настройке соответствующий уровень hello. в разделе [Set-ExecutionPolicy](https://technet.microsoft.com/library/hh849812.aspx).

Затем заполните имя подписки Azure, hello имя облачной службы и имя виртуальной машины (удаляя hello < и > символов) и затем выполните следующие команды.

```powershell
$subscr="<Name of your Azure subscription>"
$serviceName="<Name of hello cloud service that contains hello target virtual machine>"
$vmName="<Name of hello target virtual machine>"
.\InstallWinRMCertAzureVM.ps1 -SubscriptionName $subscr -ServiceName $serviceName -Name $vmName
```

Hello правильное имя подписки можно получить из hello *Имя_подписки* свойство отображения hello hello **Get-AzureSubscription** команды. Можно получить имя hello облачной службы для виртуальной машины hello hello *ServiceName* столбец в вывод hello hello **Get-AzureVM** команды.

Проверьте наличие нового сертификата hello. Откройте оснастку сертификатов для текущего пользователя hello и найдите в hello **доверенного корневого Certification Authorities\Certificates** папки. Вы увидите сертификат с DNS-имя облачной службы в hello toocolumn Кому выдан hello (пример: cloudservice4testing.cloudapp.net).

Затем инициируйте удаленный сеанс Azure PowerShell с помощью следующих команд.

```powershell
$uri = Get-AzureWinRMUri -ServiceName $serviceName -Name $vmName
$creds = Get-Credential
Enter-PSSession -ConnectionUri $uri -Credential $creds
```

После ввода действительные учетные данные администратора, вы увидите, что-нибудь подобное toohello следующие командной строке Azure PowerShell:

```powershell
[cloudservice4testing.cloudapp.net]: PS C:\Users\User1\Documents>
```

Первая часть Hello этот запрос является имя облачной службы, содержащий hello целевой виртуальной Машины, которая может отличаться от «cloudservice4testing.cloudapp.net». Теперь можно команд Azure PowerShell для этого облака вышеперечисленных неполадок hello tooinvestigate службы и исправьте конфигурацию hello.

### <a name="toomanually-correct-hello-remote-desktop-services-listening-tcp-port"></a>правильный hello toomanually прослушивания TCP-порт служб удаленных рабочих столов
Hello удаленного сеанса строке Azure PowerShell выполните следующую команду.

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

Свойство PortNumber Hello показывает hello текущий номер порта. При необходимости измените hello удаленного рабочего стола номеров tooits назад по умолчанию значение порта (3389) с помощью этой команды.

```powershell
Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber" -Value 3389
```

Убедиться в устранении hello порт too3389 измененные с помощью этой команды.

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

Выйдите из hello удаленный сеанс Azure PowerShell с помощью этой команды.

```powershell
Exit-PSSession
```

Убедитесь, что этой конечной точки удаленного рабочего стола для виртуальной Машины Azure hello hello также использует TCP-порт 3398 как свой внутренний порт. Перезапустите hello Azure VM и повторите попытку подключения удаленного рабочего стола hello.

## <a name="additional-resources"></a>Дополнительные ресурсы
[Как службы tooreset пароль или hello удаленного рабочего стола для виртуальных машин Windows](reset-rdp.md)

[Как tooinstall и настройка Azure PowerShell](/powershell/azure/overview)

[Устранение неполадок Secure Shell (SSH) подключения tooa под управлением Linux Azure виртуальные машины](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Устранение неполадок доступа tooan приложение, работающее на виртуальной машине Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

