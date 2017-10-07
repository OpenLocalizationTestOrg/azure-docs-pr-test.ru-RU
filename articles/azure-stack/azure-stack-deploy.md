---
title: "Необходимые условия для развертывания пакета средств разработки стека aaaAzure | Документы Microsoft"
description: "Представление hello среды и требования к оборудованию для пакета средств разработки Azure стека (оператор облака)."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 32a21d9b-ee42-417d-8e54-98a7f90f7311
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/11/2017
ms.author: erikje
ms.openlocfilehash: 126c851651354b6f3d61c4627ab0c1de9da12ba9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-deployment-prerequisites"></a>Подготовка к развертыванию Azure стека
Перед развертыванием Azure стека [Development Kit](azure-stack-poc.md), убедитесь, что компьютер соответствует hello следующие требования:


## <a name="hardware"></a>Оборудование
| Компонент | Минимальная | Рекомендуется |
| --- | --- | --- |
| Диски: операционная система |1 диск операционной системы с минимальным объемом 200 ГБ для системного раздела (SSD или жесткий диск). |1 диск операционной системы с минимальным объемом 200 ГБ для системного раздела (SSD или жесткий диск). |
| Дисковые накопители: Общая разработка набора данных * |4 диска. Каждый емкостью не меньше 140 ГБ (SSD или жесткие диски). Все доступные диски будут использоваться. |4 диска. Каждый диск содержит менее 250 ГБ (SSD или HDD). Все доступные диски будут использоваться. |
| Вычислительные ресурсы: ЦП |Двумя процессорными разъемами: 12 физических ядер (всего) |Двумя процессорными разъемами: 16 физических ядер (всего) |
| Вычислительные ресурсы: память |ОЗУ 96 ГБ. |128 ГБ ОЗУ (это поставщики ресурсов hello минимальное toosupport PaaS).|
| Вычислительные ресурсы: BIOS |С поддержкой Hyper-V (с поддержкой SLAT). |С поддержкой Hyper-V (с поддержкой SLAT). |
| Сетевые ресурсы: сетевая карта |Для сетевой карты требуется сертификация Windows Server 2012 R2; специальные функции не требуются. |Для сетевой карты требуется сертификация Windows Server 2012 R2; специальные функции не требуются. |
| Информация о сертификации на эмблеме оборудования |[Сертифицировано для Windows Server 2012 R2](http://windowsservercatalog.com/results.aspx?&chtext=&cstext=&csttext=&chbtext=&bCatID=1333&cpID=0&avc=79&ava=0&avq=0&OR=1&PGS=25&ready=0) |[Сертифицировано для Windows Server 2012 R2](http://windowsservercatalog.com/results.aspx?&chtext=&cstext=&csttext=&chbtext=&bCatID=1333&cpID=0&avc=79&ava=0&avq=0&OR=1&PGS=25&ready=0) |

\*Необходимо будет больше, чем это рекомендуется емкости, если планируется добавление многие hello [элементы marketplace](azure-stack-download-azure-marketplace-item.md) из Azure.

**Конфигурация диска данных:** все данные, должен иметь диски hello того же типа (все SAS или SATA все) и емкость. При использовании дисков SAS hello жестких дисков должен быть подключен через один путь (не MPIO поддержки многопутевых указан).

**Параметры конфигурации адаптера ШИНЫ**

* (Рекомендуется) Простой адаптера ШИНЫ
* RAID HBA — адаптер должен быть настроен в режиме «проходить через»
* Адаптер ШИНЫ RAID-диски должны быть настроены как одним диском, RAID-0

**Поддерживаемые сочетания шины и типа носителя**

* Жесткий диск SATA
* Жесткий диск SAS
* Жесткий диск RAID
* RAID SSD (если не указан неизвестный тип носителя hello\*)
* SSD SATA + жесткий диск SATA
* SSD SAS + жесткий диск SAS

\*RAID-контроллеров без возможности к серверу не удалось распознать тип носителя hello. Такие контроллеры пометят жесткий диск и SSD как неопределенный. В этом случае hello SSD будет использоваться в качестве постоянного хранилища вместо кэширование устройств. Таким образом можно развернуть пакет средств разработки hello на этих SSD.

**Примеры HBA**: LSI 9207-8i, LSI 9300-8i или LSI-9265-8i в сквозном режиме.

Доступны примеры конфигураций OEM.

## <a name="operating-system"></a>операционная система
|  | **Требования** |
| --- | --- |
| **Версия ОС** |Windows Server 2012 R2 или более поздней версии. версия операционной системы Hello не являются критическими до начала развертывания hello, как hello главный компьютер будет загружен в hello VHD, который включен в установку hello Azure стека. Hello операционной системы и все необходимые обновления уже интегрированы в образ hello. Не используйте tooactivate все ключи, все экземпляры Windows Server, используемые в пакете средств разработки hello. |

## <a name="deployment-requirements-check-tool"></a>Средство проверки требований к развертыванию
После установки операционной системы hello, можно использовать hello [проверки развертывания в Azure стека](https://gallery.technet.microsoft.com/Deployment-Checker-for-50e0f51b) tooconfirm, что оборудование соответствует всем требованиям hello.

## <a name="account-requirements"></a>Требования к учетной записи
Как правило с подключением к Интернету, в которой можно подключиться tooMicrosoft Azure развертывается пакет средств разработки hello. В этом случае необходимо настроить Azure Active Directory (Azure AD) учетной записи toodeploy hello пакет средств разработки.

Если среда не toohello подключенной к Интернету или вы не хотите toouse Azure AD, Azure стека можно развернуть с помощью служб федерации Active Directory (AD FS). пакет средств разработки Hello содержит свой собственный экземпляров службы федерации Active Directory и доменные службы Active Directory. При развертывании с помощью этого параметра, не нужно tooset учетных записей заранее.

>[!NOTE]
При развертывании с помощью параметра hello AD FS, необходимо повторно развернуть tooAzure tooswitch стека Azure AD.

### <a name="azure-active-directory-accounts"></a>Учетные записи Azure Active Directory
toodeploy стек Azure с помощью учетной записи Azure AD, необходимо подготовить учетную запись Azure AD, прежде чем запускать сценарий PowerShell развертывания hello. Эта учетная запись становится hello глобального администратора для клиента Azure AD hello. Он использовал tooprovision и делегат приложений и субъектов-служб для всех служб Azure стека, взаимодействующих с Azure Active Directory и Graph API. Он также используется в качестве владельца hello подписки поставщика по умолчанию hello (который можно изменить). Вы можете войти портал администратора системы tooyour стек Azure с помощью этой учетной записи.

1. Создайте учетную запись Azure AD, Здравствуйте, администратор каталога для по крайней мере один Azure AD. Если это уже сделано, можно использовать. В противном случае можно создать один бесплатно в [http://azure.microsoft.com/en-us/pricing/free-trial/](http://azure.microsoft.com/pricing/free-trial/) (в Китае, посетите <http://go.microsoft.com/fwlink/?LinkID=717821> вместо). Если планируется toolater [Azure стеком регистров с помощью Azure](azure-stack-register.md), также необходимо иметь подписку в только что созданное учетной записи.
   
    Сохранить эти учетные данные для использования в шаге 6 процедуры [развертывания пакета средств разработки hello](azure-stack-run-powershell-script.md#deploy-the-development-kit). Это *администратора службы* учетную запись можно настроить и управлять облака ресурсов, учетные записи пользователей, планы для клиентов, квоты и Расценки. На портале hello они создавать облака веб-сайтов, Частные облака виртуальных машин, создавать планы и управлять подписками пользователя.
2. [Создание](azure-stack-add-new-user-aad.md) по крайней мере одну учетную запись, чтобы вы могли войти в пакете средств разработки toohello как клиента.
   
   | **Учетная запись Azure Active Directory** | **Поддерживается?** |
   | --- | --- |
   | Рабочая учетная запись с общей подпиской Azure |Да |
   | Учетная запись Майкрософт с действительной общедоступной подпиской Azure |Да |
   | Рабочая учетная запись с подпиской Azure для Китая |Да |
   | Рабочая учетная запись с допустимым нам государственных подписки Azure |Да |

## <a name="network"></a>Сеть
### <a name="switch"></a>Switch
Один порт коммутатора для машины комплект средств для разработки hello.  

подключения доступа к порту коммутатора tooa или магистрали порт, который поддерживается компьютером комплект средств для разработки Hello. Нет специальные функциональные возможности необходимы на коммутаторе hello. Если вы используете магистрали порт или если требуется tooconfigure VLAN ID, у вас есть tooprovide hello VLAN ID в качестве параметра развертывания. Можно просмотреть примеры в hello [список параметров развертывания](azure-stack-run-powershell-script.md).

### <a name="subnet"></a>Подсеть
Не подключайте hello комплект средств для разработки машины toohello следующих подсетей:

* 192.168.200.0/24
* 192.168.100.0/27
* 192.168.101.0/26
* 192.168.102.0/24
* 192.168.103.0/25
* 192.168.104.0/25

Эти подсети резервируются для hello внутренних сетей в среде комплект средств для разработки hello.

### <a name="ipv4ipv6"></a>IPv4 или IPv6
Поддерживается только протокол IPv4. Создать сети IPv6 нельзя.

### <a name="dhcp"></a>DHCP
Убедитесь, что имеется hello сети DHCP-сервер, сетевой Адаптер подключается к приветствия. Если протокол DHCP недоступен, необходимо подготовить дополнительных статического IPv4-сети помимо hello, используемый узлом. Необходимо указать этот IP-адрес и шлюз в качестве параметра развертывания. Можно просмотреть примеры в hello [список параметров развертывания](azure-stack-run-powershell-script.md).

### <a name="internet-access"></a>Доступ к Интернету
Стек Azure требует toohello доступа к Интернету, либо непосредственно, либо с помощью прозрачного прокси. Стек Azure не поддерживает конфигурацию hello web прокси tooenable доступ к Интернету. Назначить toohello они НАЗЫВАЛИСЬ-BGPNAT01 (по DHCP или статические IP-адреса), необходимо будет tooaccess Интернета, IP-узле hello и hello новый IP-адрес. В доменах hello graph.windows.net и login.microsoftonline.com используются порты 80 и 443.

## <a name="telemetry"></a>Телеметрия

Данные телеметрии помогают нам фигуры будущих версий Azure стека. Он позволяет быстро реагировать на них toofeedback, предоставляет пользователям новые возможности и улучшения качества. Стека Microsoft Azure включает в себя Windows Server 2016 и SQL Server 2014. По умолчанию ни один из этих продуктов изменены, и оба описаны hello заявление о конфиденциальности Microsoft Enterprise. Стек Azure также содержит программное обеспечение открытым исходным кодом, которое еще не измененные toosend tooMicrosoft телеметрии. Ниже приведены некоторые примеры данные телеметрии Azure стека.

- сведения о регистрации развертывания
- При открытии и закрытии оповещения
- Hello количество сетевых ресурсов

поток данных телеметрии toosupport, порт 443 (HTTPS) должен быть открыт в сети. Конечная точка клиента Hello — https://vortex-win.data.microsoft.com.

Если вы не хотите tooprovide телеметрии для стека Azure, его можно отключить на узле комплект средств для разработки hello и hello инфраструктуры виртуальных машин, как описано ниже.

### <a name="turn-off-telemetry-on-hello-development-kit-host-optional"></a>Отключить функцию телеметрии на узле комплект средств для разработки hello (необязательно)

>[!NOTE]
Если требуется tooturn отключение телеметрии для узла комплект средств для разработки hello вы необходимо сделать перед запуском скрипта развертывания hello.

Прежде чем [выполнения сценария asdk installer.ps1 hello]() toodeploy hello development kit узла, загрузку в hello CloudBuilder.vhdx и hello выполнения следующих сценариев в PowerShell с повышенными привилегиями:
```powershell
### Get current AllowTelmetry value on DVM Host
(Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name AllowTelemetry).AllowTelemetry
### Set & Get updated AllowTelemetry value for ASDK-Host 
Set-ItemProperty-Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name "AllowTelemetry" -Value '0'  
(Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name AllowTelemetry).AllowTelemetry
```

Установка **AllowTelemetry** too0 отключение телеметрии для развертывания Windows и стек Azure. Отправляются только критические события hello операционной системы. параметр Hello управляет телеметрии Windows на всех узлах и инфраструктуры виртуальных машин и повторно toonew узлов и виртуальных машин если выполняются операции масштабирования.


### <a name="turn-off-telemetry-on-hello-infrastructure-virtual-machines-optional"></a>Отключить функцию телеметрии на виртуальных машинах hello инфраструктуры (необязательно)

После hello развертывание может быть hello успешно, запустите следующие скрипт в окне PowerShell с повышенными привилегиями (как hello AzureStack\AzureStackAdmin пользователя) на узле комплект средств для разработки hello.

```powershell
$AzSVMs= get-vm |  where {$_.Name -like "AzS-*"}
### Show current AllowTelemetry value for all AzS-VMs
invoke-command -computername $AzSVMs.name {(Get-ItemProperty -Path `
"HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" -Name AllowTelemetry).AllowTelemetry}
### Set & Get updated AllowTelemetry value for all AzS-VMs
invoke-command -computername $AzSVMs.name {Set-ItemProperty -Path `
"HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" -Name "AllowTelemetry" -Value '0'}
invoke-command -computername $AzSVMs.name {(Get-ItemProperty -Path `
"HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" -Name AllowTelemetry).AllowTelemetry}
```

tooconfigure телеметрии SQL Server в разделе [как tooconfigure SQL Server 2016](https://support.microsoft.com/en-us/help/3153756/how-to-configure-sql-server-2016-to-send-feedback-to-microsoft).

### <a name="usage-reporting"></a>Отчеты об использовании

Посредством регистрации стек Azure также является tooAzure сведения об использовании настроенных tooforward. Отчеты об использовании контролируются независимо от телеметрии. Можно отключить отчетов при использовании [регистрации](azure-stack-register.md) с помощью скрипта hello на сайте Github. Просто набор hello **$reportUsage** параметр слишком**$false**.

Данные об использовании форматируется как описано в hello [tooAzure данных об использовании отчетов Azure стека](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-usage-reporting). Пользователей стека пакет средств разработки Azure фактически не взимается. Эти функциональные возможности включены в пакете средств разработки hello, благодаря чему можно протестировать toosee, как работает отчеты об использовании. 


## <a name="next-steps"></a>Дальнейшие действия
[Загрузить пакет hello Azure стека разработки комплект средств для развертывания](https://azure.microsoft.com/overview/azure-stack/try/?v=try)

[Развертывание пакета средств разработки стек Azure](azure-stack-run-powershell-script.md)

