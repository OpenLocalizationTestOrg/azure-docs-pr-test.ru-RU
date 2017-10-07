---
title: "Шифрование дисков для Windows и Linux ВМ IaaS aaaAzure | Документы Microsoft"
description: "В этой статье приведен обзор шифрования дисков Microsoft Azure для виртуальных машин IaaS под управлением Windows и Linux."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a>Дисковое шифрование Azure для виртуальных машин IaaS под управлением Windows и Linux
Microsoft Azure прилагает все усилия tooensuring конфиденциальность данных независимости данных и позволяет toocontrol, размещенной в Azure данные в диапазоне tooencrypt перспективных технологий для управления ключами шифрования, управления и аудита доступа к данным. Это обеспечивает клиентам Azure hello гибкость toochoose hello решение, которое наилучшим образом соответствует потребностям бизнеса. В этом документе вы ознакомитесь tooa новое технологическое решение «Шифрование диска Azure для Windows и ВМ IaaS Linux» toohelp защиты и защиты вашего toomeet данных организации свои обязательства по безопасности и соответствия требованиям. Подробное руководство по способ шифрования toouse hello диска Azure функции в том числе hello поддерживается сценарии и взаимодействия с пользователем hello Hello бумаги.

> [!NOTE]
> Выполнение некоторых приведенных рекомендаций может привести к более интенсивному использованию данных, сети или вычислительных ресурсов, а следовательно к дополнительным затратам на лицензии или подписки.

## <a name="overview"></a>Обзор
Шифрование дисков Azure — это новая функция, которая помогает зашифровать диски виртуальных машин IaaS под управлением Windows и Linux. Azure шифрование диска использует отраслевой стандарт hello [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) компонента Windows, а также hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) функции шифрования тома tooprovide Linux для hello ОС и дисков данных hello. решение Hello интегрировано с [хранилище ключей Azure](https://azure.microsoft.com/documentation/services/key-vault/) toohelp управления и управление ключами шифрования диска hello и секретные данные в вашей подписке хранилища ключей. Hello решение также обеспечивает шифрование всех данных на диски виртуальной машины hello хранятся в службе хранилища Azure.

Теперь **общедоступная версия** шифрования дисков Azure представлена во всех общедоступных регионах Azure и регионах AzureGov для виртуальных машин IaaS с ОС Windows и Linux уровня "Стандартный" или c хранилищем класса "Премиум".

### <a name="encryption-scenarios"></a>Сценарии шифрования
Hello решения по шифрованию диска Azure поддерживает следующие сценарии клиента hello:

* включение шифрования для новых виртуальных машин IaaS, для создания которых используются предварительно зашифрованные виртуальные жесткие диски и ключи шифрования;
* Включить шифрование на новые виртуальные машины IaaS, созданных из образов коллекции Azure поддерживается hello
* включение шифрования в имеющихся виртуальных машинах IaaS, запущенных в Azure;
* отключение шифрования на виртуальных машинах IaaS под управлением Windows;
* отключение шифрования на дисках данных виртуальных машин IaaS под управлением Linux;
* включение шифрования виртуальных машин с управляемыми дисками;
* изменение параметров шифрования существующей зашифрованной виртуальной машины с хранилищем не класса "Премиум";
* резервное копирование и восстановление виртуальных машин, зашифрованных с помощью ключа шифрования.

решение Hello поддерживает следующие сценарии для ВМ IaaS, если они включены в Microsoft Azure hello:

* интеграция с хранилищем ключей Azure;
* виртуальные машины IaaS серий [A, D, DS, G, GS, F и т. д.](https://azure.microsoft.com/pricing/details/virtual-machines/) уровня "Стандартный";
* Включить шифрование в Windows и Linux ВМ IaaS и управляемого диска виртуальных машин из hello поддерживается образов коллекции Azure
* отключение шифрования на дисках данных и в операционной системе виртуальных машин IaaS с ОС Windows и виртуальных машин с управляемыми дисками;
* отключение шифрования на дисках данных виртуальных машин IaaS с ОС Windows и виртуальных машин с управляемыми дисками;
* включение шифрования на виртуальных машинах IaaS под управлением клиентской ОС Windows;
* включение шифрования для томов с путями подключения.
* включение шифрования на виртуальных машинах Linux с чередованием дисков RAID с помощью программы mdadm;
* включение шифрования на виртуальных машинах Linux с использованием диспетчера логических томов для дисков данных;
* включение шифрования на виртуальных машинах Windows с дисковыми пространствами;
* изменение параметров шифрования существующей зашифрованной виртуальной машины с хранилищем не класса "Премиум";
* поддерживаются все общедоступные регионы Azure и регионы AzureGov.

решение Hello не поддерживает следующие сценарии, функции и технологии hello:

* виртуальные машины уровня "Базовый";
* отключение шифрования диска ОС виртуальных машин IaaS под управлением Linux;
* Отключение шифрования на диске с данными при шифровании hello диска ОС ВМ Iaas Linux
* Виртуальные машины IaaS, созданных с помощью метода создания виртуальной Машины классический hello
* включение шифрования для виртуальных машин IaaS под управлением Windows и Linux, созданных из пользовательских образов НЕ поддерживается. Включение шифрования для диска ОС в операционной системе Linux LVM в настоящее время не поддерживается. Поддержка будет обеспечена в ближайшее время.
* интеграция с локальной службой управления ключами;
* служба файлов Azure (общая файловая система), NFS, динамические тома, виртуальные машины Windows с программными системами RAID.
* резервное копирование и восстановление виртуальных машин, зашифрованных без использования ключа шифрования;
* изменение параметров шифрования существующей зашифрованной виртуальной машины с хранилищем класса "Премиум".

> [!NOTE]
> Резервное копирование и восстановление виртуальных машин, зашифрованные поддерживается только для виртуальных машин, которые шифруются с помощью ключа обмена Ключами конфигурации hello. Виртуальные машины, зашифрованные без ключа шифрования ключей, не поддерживаются. KEK — это необязательный параметр для включения шифрования виртуальных машин. Поддержка ожидается в ближайшем будущем.
> Изменение параметров шифрования существующей зашифрованной виртуальной машины с хранилищем класса "Премиум" не поддерживается. Поддержка ожидается в ближайшем будущем.

### <a name="encryption-features"></a>Функции шифрования
При включении и развернуть шифрование диска Azure ВМ IaaS Azure hello следующие возможности включены, в зависимости от конфигурации hello:

* Шифрование тома hello ОС тома tooprotect hello загрузки хранятся в хранилище
* Шифрование тома данных hello tooprotect тома данных хранятся в хранилище
* Отключение шифрования на hello операционной системы и данных дисков ВМ IaaS Windows
* Отключение шифрования для данных hello дисков для виртуальных машин Linux IaaS (если ОС диск является не шифруются)
* Защита ключей шифрования hello и секретные данные в вашей подписке хранилища ключей
* Отчеты о состоянии шифрования hello объекта hello зашифрованные ВМ IaaS
* Удаление параметров конфигурации шифрование диска от виртуальной машины IaaS hello
* Резервное копирование и восстановление виртуальных машин, зашифрованные с помощью службы архивации Azure hello

> [!NOTE]
> Резервное копирование и восстановление виртуальных машин, зашифрованные поддерживается только для виртуальных машин, которые шифруются с помощью ключа обмена Ключами конфигурации hello. Виртуальные машины, зашифрованные без ключа шифрования ключей, не поддерживаются. KEK — это необязательный параметр для включения шифрования виртуальных машин.

Решения для шифрования дисков Azure для виртуальных машин IaaS под управлением Windows и Linux включает в себя следующее:

* расширение шифрование диска Windows Hello.
* Hello шифрование диска расширения для Linux.
* командлеты PowerShell Hello шифрование диска.
* Здравствуйте шифрования диска командлеты Azure командной строки (CLI).
* шаблоны Azure Resource Manager Hello шифрование диска.

Hello решения по шифрованию диска Azure поддерживается на виртуальных машинах IaaS, работающих под управлением ОС Windows или Linux. Дополнительные сведения о hello поддерживаемых операционных системах см. в разделе hello «необходимые условия» раздела.

> [!NOTE]
> Дополнительная плата за шифрование дисков Azure для виртуальных машин не взимается.

### <a name="value-proposition"></a>Предлагаемые преимущества
При применении решения hello Управление шифрованием диска Azure может удовлетворять hello следующие бизнес-требований:

* Виртуальные машины IaaS, защищены неактивные, поскольку можно использовать стандартные технологии tooaddress организации безопасности и соответствия требованиям требования к шифрованию.
* Загрузка виртуальных машин IaaS выполняется в соответствии с ключами и политиками, которыми управляет клиент. Можно также проводить аудит их использования в хранилище ключей.

### <a name="encryption-workflow"></a>Рабочий процесс шифрования
Шифрование диска tooenable для Windows и виртуальных машин Linux hello следующие:

1. Выберите сценарии шифрования на один из предыдущих сценариев шифрования hello.
2. Включить шифрование диска tooenabling посредством шаблона диспетчера ресурсов шифрования диска Azure hello, командлеты PowerShell или интерфейса командной и укажите конфигурацию шифрования hello.

   * Для шифрования клиента сценария виртуального жесткого диска: hello передачи учетной записи хранилища tooyour виртуальный жесткий ДИСК зашифрован hello и hello шифрования ключа tooyour материала ключа хранилища. Укажите конфигурации tooenable hello шифрование на новую виртуальную Машину IaaS.
   * Для новых виртуальных машин, созданными на hello Marketplace и существующих виртуальных машин, которые уже запущены в Azure предоставляют tooenable конфигурации hello шифрование на hello ВМ IaaS.

3. Предоставление доступа к toohello платформы Azure tooread hello ключ шифрования материалы (ключи шифрования BitLocker для систем Windows) и парольную фразу для Linux из вашего хранилища ключей шифрования tooenable hello ВМ IaaS.

4. Укажите hello Azure Active Directory (Azure AD) приложения удостоверение toowrite hello шифрования ключа материала tooyour хранилища ключей. Это позволяет включить шифрование на hello ВМ IaaS для сценариев hello, упомянутых в шаге 2.

5. Azure обновляет модель службы hello виртуальной Машины с помощью шифрования и настройки хранилища ключей hello и устанавливает зашифрованные ВМ.

 ![Антивредоносное ПО Майкрософт в Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a>Рабочий процесс расшифровки
Шифрование диска toodisable ВМ IaaS, полный hello следующие общие действия:

1. Выберите toodisable шифрования (расшифровки) на работающей ВМ в Azure IaaS через hello шаблона диспетчера ресурсов шифрования диска Azure или командлеты PowerShell и указать конфигурацию расшифровки hello.

 Этот шаг отключает шифрование тома данных ОС или hello hello, или на запуск виртуальной Машины IaaS Windows hello. Тем не менее как упоминалось в предыдущем разделе hello, отключение шифрования диска операционной системы для Linux не поддерживается. этап расшифровки Hello допустим только для дисков с данными на виртуальных машинах Linux, при условии, что диск ОС hello не шифруются.
2. Обновления Azure hello модели службы виртуальной Машины, а hello ВМ IaaS помечается расшифрованы. содержимое Hello hello ВМ больше не шифруются при хранении.

> [!NOTE]
> Операция отключения шифрования Hello не удаляет вашего ключа хранилища и hello основы ключа шифрования (ключи шифрования BitLocker для систем Windows) или парольную фразу для Linux.
 > Отключение шифрования диска операционной системы для Linux не поддерживается. этап расшифровки Hello допустим только для дисков с данными на виртуальных машинах Linux.
Отключение шифрования диска данных для Linux не поддерживается, если шифрование hello диска операционной системы.

## <a name="prerequisites"></a>Предварительные требования
Прежде чем включить шифрование диска Azure на виртуальные машины IaaS Azure для hello поддерживается сценариев, которые были описаны в разделе «Обзор» hello, см. следующие необходимые условия hello:

* Необходимо иметь действующая Активная подписка Azure toocreate ресурсы в Azure в регионах hello поддерживается.
* Azure диска шифрование поддерживается для следующих версий Windows Server hello: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 и Windows Server 2016.
* В следующих клиентских версий Windows hello поддерживается Azure шифрование диска: клиента Windows 8 и Windows 10.

> [!NOTE]
> Для Windows Server 2008 R2 перед включением шифрования в Azure требуется установить .NET Framework 4.5. Можно установить его из центра обновления Windows, установив необязательное обновление hello Microsoft .NET Framework 4.5.2 для x64-разрядных систем Windows Server 2008 R2 ([KB2901983](https://support.microsoft.com/kb/2901983)).

* Поддерживается Azure шифрование диска на hello следующие коллекции Azure на основе сервера дистрибутивах Linux и версиях:

| Дистрибутив Linux | Version (версия) | Тип тома, для которого поддерживается шифрование|
| --- | --- |--- |
| Ubuntu | 16.04-DAILY-LTS | Диск операционной системы и данных |
| Ubuntu | 14.04.5-DAILY-LTS | Диск операционной системы и данных |
| Ubuntu | 12.10 | Диск данных |
| Ubuntu | 12.04 | Диск данных |
| RHEL | 7.3 | Диск операционной системы и данных |
| RHEL | 7,2 | Диск операционной системы и данных |
| RHEL | 6,8 | Диск операционной системы и данных |
| RHEL | 6.7 | Диск данных |
| CentOS | 7.3 | Диск операционной системы и данных |
| CentOS | 7.2n | Диск операционной системы и данных |
| CentOS | 6,8 | Диск операционной системы и данных |
| CentOS | 7.1. | Диск данных |
| CentOS | 7.0 | Диск данных |
| CentOS | 6.7 | Диск данных |
| CentOS | 6.6 | Диск данных |
| CentOS | 6,5 | Диск данных |
| openSUSE | 13.2 | Диск данных |
| SLES | 12 с пакетом обновления 1 (SP1) | Диск данных |
| SLES | 12-SP1 (Премиум) | Диск данных |
| SLES | HPC 12 | Диск данных |
| SLES | 11-SP4 (Премиум) | Диск данных |
| SLES | 11 SP4 | Диск данных |

* Требуется Azure шифрование данных на диске, хранилище ключей и виртуальные машины находились в hello же регионе Azure и подписки.

> [!NOTE]
> Настройка ресурсов hello в отдельные области вызывает сбой включить функцию шифрования диска Azure hello.

* tooset и Настройка хранилища ключей для шифрования диска Azure, см. раздел **задать и Настройка хранилища ключей для шифрования диска Azure** в hello *необходимые компоненты* этой статьи.
* tooset и настройка приложения Azure AD в Azure Active directory для шифрования диска Azure, см. раздел **настройки приложения hello Azure AD в Azure Active Directory** в hello *необходимых компонентов* части этой статьи.
* tooset и настройка политики доступа hello хранилища ключей для приложения hello Azure AD, см. раздел **настроить политику доступа hello хранилища ключей для приложения hello Azure AD** в hello *необходимые компоненты* раздела в этой статье.
* tooprepare предварительно зашифрованный VHD Windows, см. раздел **подготовить предварительно зашифрованный ФАЙЛ Windows** в hello *приложение*.
* tooprepare предварительно зашифрованный VHD Linux, см. раздел **подготовить предварительно зашифрованный ФАЙЛ Linux** в hello *приложение*.
* Hello платформы Azure требует ключи шифрования toohello доступа или секреты в хранилище ключей toomake их доступных toohello виртуальной машины при его загрузке и расшифровывает hello тома ОС виртуальной машины. разрешения tooAzure toogrant платформы, набор hello **EnabledForDiskEncryption** свойство в хранилище ключей hello. Дополнительные сведения см. в разделе **задать и Настройка хранилища ключей для шифрования диска Azure** в приложение hello.
* Для URL-адресов секрета и ключа шифрования ключей (KEK) хранилища ключей необходимо включить управление версиями. Это требование Azure. Действительный секретный и KEK URL-адреса см. следующие примеры hello.

  * Пример допустимого URL-адреса секрета: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*.
  * Пример допустимого ключа шифрования ключей: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*.

* Шифрование дисков Azure не поддерживает указание номеров портов в URL-адресах секрета и ключа шифрования ключей для хранилища ключей. Примеры URL-адреса не поддерживается и поддерживаемых хранилища ключей см. в следующем hello:

  * Недопустимый URL-адрес хранилища ключей: *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*.
  * Допустимый URL-адрес хранилища ключей: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*.

* функция шифрования диска Azure tooenable hello, hello ВМ IaaS должен удовлетворять hello следующие требования к конфигурации конечной точки сети.
  * tooget маркеров tooconnect tooyour хранилища ключей, hello ВМ IaaS должна быть конечной точкой Azure Active Directory может tooconnect tooan, \[login.microsoftonline.com\].
  * toowrite hello шифрования ключей tooyour хранилища ключей, hello ВМ IaaS должна быть конечной точкой хранилища ключей toohello может tooconnect.
  * Hello ВМ IaaS должно быть конечной точки может tooconnect tooan хранилища Azure, узлы hello репозиторий расширений Azure и учетной записью хранения Azure, что узлы hello VHD-файлы.

  > [!NOTE]
  > Если политика безопасности ограничивает доступ из виртуальных машин Azure toohello Интернета, можно решить hello, предшествующий URI и настроить toohello исходящие подключения tooallow конкретного правила IP-адресов.
  >
  >tooconfigure и доступа к хранилищу ключей Azure за брандмауэром (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)

* Используйте последнюю версию пакета SDK для Azure PowerShell версии tooconfigure шифрование диска Azure hello. Загрузка последней версии hello объекта [выпуска Azure PowerShell](https://github.com/Azure/azure-powershell/releases)

 > [!NOTE]
  > Шифрование дисков Azure не поддерживается в [пакете SDK для Azure PowerShell версии 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016). Если вы получили ошибку toousing Azure PowerShell 1.1.0, связанные с. в разделе [tooAzure связанные ошибки шифрования диска Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).

* toorun любую команду Azure CLI и связать ее с подпиской Azure, необходимо сначала установить Azure CLI:
  * tooinstall Azure CLI и связать ее с подпиской Azure см. в разделе [как tooinstall и настройка Azure CLI](../cli-install-nodejs.md).
  * toouse Azure CLI для Mac, Linux и Windows с помощью диспетчера ресурсов Azure в разделе [команды Azure CLI в режим диспетчера ресурсов](../virtual-machines/azure-cli-arm-commands.md).

* При шифровании управляемого диска, он является обязательной к установке tootake моментальный снимок hello управляемого диска или из резервной копии диска hello за пределами предыдущего tooenabling шифрования шифрование диска Azure.  Без резервной копии в месте любой непредвиденный сбой во время шифрования может сделать hello диск и виртуальная машина недоступными без параметра восстановления.  Набор AzureRmVMDiskEncryptionExtension в настоящее время не резервное копирование управляемых дисков и появится сообщение об ошибке, если используется для управляемого диска, если не был указан параметр - skipVmBackup hello.  Этот параметр является небезопасным toouse, если резервной копии уже были внесены за пределами Azure шифрование диска.   Если указан параметр - skipVmBackup hello, командлет hello не сделает резервную копию предыдущего tooencryption hello управляемого диска.  По этой причине считается обязательным к установке toomake, убедиться, что требуется резервная копия hello управляемого диска, который виртуальная машина находится в месте предыдущих tooenabling шифрование диска Azure, в случае восстановления является более поздней версии.  
> [!NOTE]
 > никогда не следует использовать Hello - skipVmBackup параметр, если моментальный снимок или резервная копия уже выполнен за пределами Azure шифрование диска. 

* Hello решения по шифрованию диска Azure использует предохранитель внешнего ключа BitLocker hello ВМ IaaS Windows. Если виртуальные машины присоединены к домену, не применяйте групповые политики, требующие использования предохранителей TPM. Сведения о групповой политике hello «Разрешить использование BitLocker без совместимого TPM» в разделе [Справочник по групповой политики BitLocker](https://technet.microsoft.com/library/ee706521).
* Политики BitLocker на виртуальных машинах, присоединенных к домену с помощью пользовательской групповой политики необходимо включить следующий параметр hello: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` шифрование диска Azure не сможет пользовательские параметры политики для Bitlocker несовместимы. На компьютерах, не имеющие hello может потребоваться правильный параметр политики, применение hello новой политики, принудительное hello tooupdate новой политики (gpupdate.exe/force) и повторный запуск.  
* toocreate приложения Azure AD, Создание хранилища ключей, или настроить существующие хранилища ключей и включения шифрования см. в разделе hello [шифрование диска Azure готовности сценарий PowerShell](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
* tooconfigure необходимых компонентов шифрование диска с помощью Azure CLI hello. в разделе [этот скрипт Bash](https://github.com/ejarvi/ade-cli-getting-started).
* tooback службы toouse hello резервное копирование и восстановление шифрование виртуальных машин, при включении шифрования с помощью шифрования диска Azure, зашифровать виртуальные машины с помощью настройки ключей шифрования диска Azure hello. Hello службы резервного копирования поддерживает виртуальные машины, которые зашифрованы с помощью ключа обмена Ключами конфигурации только. В разделе [способ tooback копирования и восстановления шифрования виртуальных машин с помощью шифрования резервной копии Azure](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).

* При шифровании тома операционной системы Linux, обратите внимание, что перезагрузка виртуальной Машины требуются в данный момент в конце hello hello процесса. Это можно сделать через портал hello, powershell или интерфейс командной строки.   Ход hello tootrack шифрования, периодически опрашивать hello возвращаемый Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus сообщение о состоянии.  После завершения шифрования возвращенный этой командой сообщение о состоянии hello hello сообщит об этом.  Например «ProgressMessage: успешно шифрование диска операционной системы, выполните перезагрузку hello виртуальной Машины» в этой точке hello ВМ можно перезапустить и использовать.  

* Azure шифрование диска для Linux требует toohave диски данных подключенная файловая система в предыдущих tooencryption Linux

* Рекурсивно подключенных данных не поддерживает диски hello шифрование диска Azure для Linux. Например если hello целевой системе монтирования диска на /foo/bar и затем еще одну на /foo/bar/baz шифрования hello /foo/bar/baz будет успешным, но шифрования/foo/полосы завершится ошибкой. 

* Azure шифрование диска поддерживается только в коллекции Azure поддерживается изображения, соответствующие требованиям упомянутой выше hello. Клиент пользовательских образов из-за toocustom схемы секционирования и процесс поведения, которые могут существовать в эти образы не поддерживаются. Кроме того, даже виртуальные машины, созданные по образу из коллекции, который изначально соответствовал предварительным требованиям, но был изменен во время создания, могут быть несовместимы.  Для причине hello предлагаемые процедуры для шифрования ВМ Linux — toostart из чистой коллекции образов, зашифровать hello виртуальной Машины и программного обеспечения или toohello данных виртуальной Машины, при необходимости добавить.  

> [!NOTE]
> Резервное копирование и восстановление виртуальных машин, зашифрованные поддерживается только для виртуальных машин, которые шифруются с помощью ключа обмена Ключами конфигурации hello. Виртуальные машины, зашифрованные без ключа шифрования ключей, не поддерживаются. KEK — это необязательный параметр для включения виртуальных машин.

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a>Настройка hello приложения Azure AD в Azure Active Directory
Если вам требуется toobe шифрование включено на работающей ВМ в Azure, шифрование диска Azure создает и записывает хранилища ключей tooyour ключей шифрования hello. Для управления ключами шифрования в хранилище ключей требуется аутентификация Azure AD.

Для этой цели создайте приложение Azure AD. Можно найти подробные инструкции по регистрации приложения в разделе «Получение удостоверения приложения hello» hello hello блога [хранилище ключей Azure — шаг за шагом](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx). В этой записи вы также найдете несколько полезных примеров подготовки и настройки хранилища ключей. Можно использовать аутентификацию на основе секрета клиента или на основе сертификата клиента в Azure AD.

#### <a name="client-secret-based-authentication-for-azure-ad"></a>Аутентификация в Azure AD на основе секрета клиента
Hello разделах, помогут настроить на основе секрет проверки подлинности клиента для Azure AD.

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a>Создание приложения Azure AD с помощью Azure PowerShell
Используйте следующий командлет PowerShell toocreate приложения Azure AD hello.

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> $azureAdApplication.ApplicationId — hello Azure AD ClientID, $aadClientSecret hello секрет клиента, что необходимо использовать более поздней версии tooenable шифрование диска Azure. Защита секрет клиента Azure AD hello соответствующим образом.

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a>Настройка hello Azure AD идентификатор клиента и секрет из hello классический портал Azure
Также можно выполнить настройку идентификатор клиента Azure AD и секрет с помощью hello [классический портал Azure]( https://manage.windowsazure.com). tooperform это задача, hello следующие:

1. Нажмите кнопку hello **Active Directory** вкладки.

 ![Дисковое шифрование Azure](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. Нажмите кнопку **добавить приложение**и выберите имя приложения hello типа.

 ![Дисковое шифрование Azure](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. Нажмите кнопку со стрелкой hello, а затем настройте свойства приложения hello.

 ![Дисковое шифрование Azure](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. Щелкните флажок hello в нижнем левом углу toofinish hello. Откроется страница настройки приложения Hello и идентификатор клиента Azure AD hello отображается внизу hello страницы приветствия.

 ![Дисковое шифрование Azure](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. Сохранить секрет клиента hello Azure AD, установив hello **Сохранить** кнопки. Обратите внимание, секрет клиента hello Azure AD в текстовом поле hello ключей. Храните его с соблюдением мер предосторожности.

 ![Дисковое шифрование Azure](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > Hello предшествующий потока не поддерживается на hello классический портал Azure.

##### <a name="use-an-existing-application"></a>Использование существующего приложения
tooexecute hello, следующие команды, получения и использования hello [модуля Azure AD PowerShell](https://technet.microsoft.com/library/jj151815.aspx).

> [!NOTE]
> Hello следующие команды должен выполняться из нового окна PowerShell. Не использовать Azure PowerShell или команды hello tooexecute окно диспетчера ресурсов Azure hello. Такой подход рекомендуется из-за этих командлетов в модуле MSOnline hello или Azure AD PowerShell.

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a>Аутентификация на основе сертификата в Azure AD
> [!NOTE]
> В настоящее время аутентификация на основе сертификата Azure AD на виртуальных машинах Linux не поддерживается.

Здравствуйте разделах Показать как tooconfigure проверку подлинности на основе сертификатов для Azure AD.

##### <a name="create-an-azure-ad-application"></a>Создание приложения Azure AD
toocreate приложения Azure AD, выполните следующие командлеты PowerShell hello:

> [!NOTE]
> Замените следующую hello `yourpassword` строка, в которой безопасного пароля и защиты паролем hello.

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

После завершения этого этапа Отправка хранилища ключей tooyour файл PFX и включить toodeploy политики, необходимый для доступа к hello, сертификат tooa виртуальной Машины.

##### <a name="use-an-existing-azure-ad-application"></a>Использование существующего приложения Azure AD
При настройке проверки подлинности на основе сертификатов для существующего приложения, используйте командлеты PowerShell hello, показано ниже. Быть tooexecute убедиться, что с помощью нового окна PowerShell.

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

После завершения этого этапа, передайте хранилища ключей tooyour файл PFX и включить политику доступа hello достаточно toodeploy hello сертификат tooa виртуальной Машины.

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a>Отправка хранилища ключей tooyour файла PFX
Подробное описание этого процесса см. в разделе [hello официальный блог группы хранилища Azure ключ](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx). Однако следующие командлеты PowerShell hello, все, что требуется для задачи «hello». Быть tooexecute убедиться, что их из консоли Azure PowerShell.

> [!NOTE]
> Замените следующую hello `yourpassword` строка, в которой безопасного пароля и защиты паролем hello.

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a>Развертывание сертификата в вашей tooan хранилища ключей существующей виртуальной Машины
После завершения передачи hello PFX, разверните сертификат в существующей виртуальной Машины с hello следующих tooan хранилища ключей hello.
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a>Настройте политику доступа hello хранилища ключей для приложения hello Azure AD
Azure AD приложению права tooaccess hello ключей или секреты в хранилище hello. Используйте hello [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) командлет toogrant разрешения toohello приложение, используя идентификатор клиента hello (который был создан при регистрации приложения hello) как hello _ServicePrincipalName —_ значение параметра. hello записи блога, см. toolearn [хранилище ключей Azure — шаг за шагом](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx). Ниже приведен пример как tooperform это задачи через PowerShell:

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> Azure шифрование диска требуются следующие доступ политики tooyour Azure AD клиентское приложение hello tooconfigure: _WrapKey_ и _задать_ разрешения.

## <a name="terminology"></a>Терминология
Некоторые из основных терминах hello используется эта технология используется hello в следующей таблице терминология toounderstand:

| Терминология | Определение |
| --- | --- |
| Azure AD | Azure AD — это сокращенное обозначение [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/). Учетная запись Azure AD необходима для аутентификации, хранения секретов в хранилище ключей и извлечения их из него. |
| Хранилище ключей Azure | Key Vault представляет собой службу управления криптографическими ключами. Она основана на аппаратных модулях безопасности, соответствующих Федеральному стандарту обработки информации (FIPS), и позволяет надежно хранить криптографические ключи и конфиденциальные данные. Дополнительные сведения см. в документации по [Key Vault](https://azure.microsoft.com/services/key-vault/). |
| ARM | Диспетчер ресурсов Azure |
| BitLocker |[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) является отрасли Windows тома технологии шифрования, использовал шифрование диска tooenable на виртуальных машинах IaaS Windows. |
| BEK | Ключи шифрования BitLocker, используемые tooencrypt hello ОС загрузочного тома и тома данных. в хранилище ключей в виде секретов об ключи BitLocker Hello. |
| Интерфейс командной строки | Ознакомьтесь с разделом [Интерфейс командной строки Azure](../cli-install-nodejs.md). |
| DM-Crypt |[Интеллектуальный анализ данных Crypt](https://en.wikipedia.org/wiki/Dm-crypt) — подсистема диска шифрования на основе Linux, прозрачный hello использовал шифрование диска tooenable на виртуальных машинах IaaS Linux. |
| KEK | Ключ шифрования ключа — hello асимметричного ключа (RSA 2048) можно использовать tooprotect или перенос секрет hello. Вы можете использовать защищенный HSM-ключ или ключ с программной защитой. Дополнительные сведения см. в документации по [Azure Key Vault](https://azure.microsoft.com/services/key-vault/). |
| Командлеты PS | Ознакомьтесь с [командлетами Azure PowerShell](/powershell/azure/overview). |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a>Установка и настройка хранилища ключей для шифрования дисков Azure
Azure шифрование диска помогает защитить hello шифрование диска ключи и секретные данные в хранилище ключей. tooset копирование хранилища ключей для шифрования диска Azure hello завершения действия в каждом hello в следующих разделах.

#### <a name="create-a-key-vault"></a>Создайте хранилище ключей.
toocreate хранилища ключей, используйте один из следующих вариантов hello:

* [Шаблон Resource Manager 101-Key-Vault-Create](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [командлеты Azure PowerShell для хранилища ключей](/powershell/module/azurerm.keyvault/#key_vault);
* Диспетчер ресурсов Azure
* Как слишком[безопасного хранилища ключей](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)

> [!NOTE]
> Если вы уже настроили хранилища ключей для вашей подписки, пропустите следующий раздел toohello.

![Хранилище ключей Azure](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a>Настройка ключа шифрования ключей (необязательно)
Если требуется дополнительный уровень безопасности для ключей шифрования BitLocker hello toouse ключа обмена Ключами, добавьте хранилище ключей tooyour ключа обмена Ключами. Используйте hello [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) toocreate командлет ключа шифрования ключа в хранилище ключей hello. Кроме того, KEK можно импортировать из своего локального модуля HSM службы управления ключами. Дополнительные сведения см. в [документации по Key Vault](https://azure.microsoft.com/documentation/services/key-vault/).

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

Можно добавить hello ключа обмена Ключами, перейдя tooAzure диспетчера ресурсов, либо с помощью интерфейса хранилища ключей.

![Хранилище ключей Azure](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a>Задание разрешений хранилища ключей
Hello платформы Azure требует ключи шифрования toohello доступа или секреты в хранилище ключей toomake их доступных toohello ВМ для загрузки и расшифровки hello тома. разрешения toogrant toohello платформы Azure, набор hello **EnabledForDiskEncryption** свойство hello ключа в хранилище с помощью командлета PowerShell hello хранилища ключей:

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

Можно также задать hello **EnabledForDiskEncryption** свойства, перейдя по адресу hello [обозревателя ресурсов Azure](https://resources.azure.com).

Как упоминалось ранее, необходимо задать hello **EnabledForDiskEncryption** свойства в хранилище ключей. В противном случае произойдет сбой развертывания hello.

Можно настроить политики доступа для приложения Azure AD из интерфейса hello хранилища ключей, как показано ниже:

![Хранилище ключей Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Хранилище ключей Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

На hello **политики расширенного доступа** , убедитесь, что хранилище ключей включено шифрование диска Azure:

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a>Сценарии развертывания шифрования дисков и взаимодействие с пользователем
Можно включить множество сценариев шифрования диска и hello шаги могут различаться соответствующим toohello сценария. Hello следующих разделах описаны сценарии hello более подробно.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a>Включить шифрование на новые виртуальные машины IaaS, созданными на Marketplace hello
Можно включить шифрование диска на новой виртуальной Машины IaaS Windows из hello Marketplace в Azure с помощью hello [шаблона диспетчера ресурсов](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).

1. Hello Azure краткое шаблон, нажмите кнопку **развертывание tooAzure**, введите конфигурацию шифрования hello на hello **параметры** и, при необходимости нажмите кнопку **ОК**.

2. Выберите подписку hello, группы ресурсов, расположение группы ресурсов, условия и соглашения и нажмите кнопку **создать** tooenable шифрование на новую виртуальную Машину IaaS.

> [!NOTE]
> Этот шаблон создает новое зашифрованное виртуальной Машине Windows, использующего коллекции образ Windows Server 2012 hello.

Шифрование дисков на новой виртуальной машине IaaS под управлением RedHat Linux 7.2 с 200 ГБ массивом RAID-0 можно включить с помощью этого [шаблона Resource Manager](https://aka.ms/fde-rhel). После развертывания шаблона hello, проверьте состояние шифрования hello виртуальной Машины с помощью hello `Get-AzureRmVmDiskEncryptionStatus` командлет, как описано в [диска шифрования ОС на работающей ВМ Linux](#encrypting-os-drive-on-a-running-linux-vm). Если машины hello возвращается в состояние _VMRestartPending_, перезапустите hello виртуальной Машины.

Hello следующей таблице перечислены параметры шаблона диспетчера ресурсов hello для новых виртуальных машин из Marketplace сценарий hello, с помощью идентификатора клиента Azure AD.

| Параметр | Описание |
| --- | --- |
| adminUserName | Имя пользователя администратора для виртуальной машины hello. |
| adminPassword | Пароль пользователя администратора для виртуальной машины hello. |
| newStorageAccountName | Имя toostore учетной записи хранилища hello ОС и виртуальных жестких дисков данных. |
| vmSize | Размер hello виртуальной Машины. Сейчас поддерживаются только серии A, D и G уровня "Стандартный". |
| virtualNetworkName | Имя виртуальной сети, сетевой Адаптер виртуальной Машины hello hello должны принадлежать. |
| subnetName | Имя подсети hello в hello виртуальной сети, hello сетевого Адаптера виртуальной Машины должны принадлежать. |
| AADClientID | Идентификатор клиента приложения hello Azure AD с хранилище ключей tooyour секреты toowrite разрешения. |
| AADClientSecret | Секрет клиента приложения Azure AD hello хранилища ключей tooyour секреты toowrite разрешения. |
| keyVaultURL | URL-адрес hello ключ хранилища, должна быть передана ключ BitLocker hello. Его можно получить с помощью командлета hello `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`. |
| keyEncryptionKeyURL | URL-адрес ключа шифрования ключа hello, используемые tooencrypt hello созданный ключ BitLocker (необязательно). |
| keyVaultResourceGroup | Группа ресурсов хранилища ключей hello. |
| vmName | Hello виртуальной Машины, операция шифрования hello называется toobe блокировкой. |

> [!NOTE]
> _KeyEncryptionKeyURL_ является необязательным параметром. Собственные KEK toofurther защиты hello ключ шифрования данных (секрет парольную фразу) можно импортировать в хранилище ключей.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a>Включение шифрования для новых виртуальных машин IaaS, при создании которых используются пользовательские зашифрованные виртуальные жесткие диски и ключи шифрования
В этом сценарии можно включить шифрование с помощью шаблона диспетчера ресурсов hello, командлеты PowerShell или команды CLI. Hello следующих разделах объясняется в шаблона диспетчера ресурсов hello больше сведений и командах CLI.

Следуйте инструкциям Привет одному из этих разделов Подготовка предварительно зашифрованный образов, которые могут использоваться в Azure. После создания образа hello hello действия можно использовать в toocreate далее разделе hello зашифрованные ВМ Azure.

* [Подготовка предварительно зашифрованного виртуального жесткого диска Windows](#preparing-a-pre-encrypted-windows-vhd)
* [Подготовка предварительно зашифрованного виртуального жесткого диска Linux](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a>С помощью шаблона диспетчера ресурсов hello
Можно включить шифрование диска на зашифрованные им с помощью hello [шаблона диспетчера ресурсов](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).

1. Hello Azure краткое шаблон, нажмите кнопку **развертывание tooAzure**, введите конфигурацию шифрования hello на hello **параметры** и, при необходимости нажмите кнопку **ОК**.

2. Выберите подписку hello, группы ресурсов, расположение группы ресурсов, условия и соглашения и нажмите кнопку **создать** tooenable шифрование на hello новой виртуальной Машины IaaS.

Hello следующей таблице перечислены параметры шаблона диспетчера ресурсов hello для вашего зашифрованные виртуального жесткого диска.

| Параметр | Описание |
| --- | --- |
| newStorageAccountName | Имя hello toostore учетной записи хранилища hello шифруются виртуального жесткого диска операционной системы. Эта учетная запись должна уже были созданы в hello же группу ресурсов и местоположения hello виртуальной Машины. |
| osVhdUri | URI hello виртуального жесткого диска операционной системы из учетной записи хранения hello. |
| osType | Тип продукта ОС (Windows, Linux). |
| virtualNetworkName | Имя виртуальной сети, сетевой Адаптер виртуальной Машины hello hello должны принадлежать. Hello имя должна уже быть создана в hello же группу ресурсов и местоположения hello виртуальной Машины. |
| subnetName | Имя подсети hello на hello виртуальной сети, hello сетевого Адаптера виртуальной Машины должны принадлежать. |
| vmSize | Размер hello виртуальной Машины. Сейчас поддерживаются только серии A, D и G уровня "Стандартный". |
| keyVaultResourceID | Hello ResourceID, который определяет ресурсы хранилища ключей hello в диспетчере ресурсов Azure. Его можно получить с помощью командлета PowerShell hello `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`. |
| keyVaultSecretUrl | URL-адрес ключа шифрования диска hello, установлены в хранилище ключей hello. |
| keyVaultKekUrl | URL-адрес ключа hello ключа шифрования для шифрования hello создается ключ шифрования диска. |
| vmName | Имя ВМ IaaS hello. |

#### <a name="using-powershell-cmdlets"></a>Использование командлетов PowerShell
Можно включить шифрование диска на зашифрованные им с помощью командлета PowerShell hello [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).  

#### <a name="using-cli-commands"></a>Использование команд интерфейса командной строки
Шифрование диска tooenable для этого сценария с помощью команды CLI hello следующие:

1. Задайте политики доступа в хранилище ключей.

   * Набор hello **EnabledForDiskEncryption** флаг:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * Набор разрешений tooAzure AD приложения toowrite секреты tooyour хранилища ключей:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. шифрование tooenable на виртуальной Машине существующий или не запущены, тип:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. Получите состояние шифрования, введя следующую команду.

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. шифрование tooenable на новой виртуальной Машины с зашифрованного диска, hello используйте следующие параметры с hello `azure vm create` команды:

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a>Включение шифрования на виртуальной машине IaaS Windows, которая уже существует или работает в Azure
В этом сценарии можно включить шифрование с помощью шаблона диспетчера ресурсов hello, командлеты PowerShell или команды CLI. Hello ниже описаны более подробно как tooenable его с помощью hello шаблона диспетчера ресурсов и команд CLI.

#### <a name="using-hello-resource-manager-template"></a>С помощью шаблона диспетчера ресурсов hello
Можно включить шифрование диска на существующие или виртуальным машинам IaaS Windows в Azure с помощью hello [шаблона диспетчера ресурсов](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).

1. Hello Azure краткое шаблон, нажмите кнопку **развертывание tooAzure**, введите конфигурацию шифрования hello на hello **параметры** и, при необходимости нажмите кнопку **ОК**.

2. Выберите подписку hello, группы ресурсов, расположение группы ресурсов, условия и соглашения и нажмите кнопку **создать** tooenable шифрование на hello существующий или под управлением ВМ IaaS.

Hello следующей таблице перечислены параметры шаблона диспетчера ресурсов hello для существующих или работающих виртуальных машин, использующих идентификатор клиента Azure AD.

| Параметр | Описание |
| --- | --- |
| AADClientID | Идентификатор клиента приложения hello Azure AD с хранилище ключей toohello секреты toowrite разрешения. |
| AADClientSecret | Секрет клиента приложения Azure AD hello хранилища ключей toohello секреты toowrite разрешения. |
| keyVaultName | Имя ключа hello хранилища, должна быть передана ключ BitLocker hello. Его можно получить с помощью командлета hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`. |
|  keyEncryptionKeyURL | URL-адрес ключа шифрования ключа hello, используемые tooencrypt hello созданный ключ BitLocker. Этот параметр является необязательным, если выбрать **nokek** hello UseExistingKek раскрывающегося списка. При выборе **kek** hello UseExistingKek раскрывающегося списка, необходимо ввести hello _keyEncryptionKeyURL_ значение. |
| volumeType | Тип тома, для которого выполняется операция шифрования hello. Допустимые значения: _OS_, _Data_ и _All_. |
| sequenceVersion | Версия последовательности hello операции BitLocker. Этот номер версии увеличивается, каждый раз, шифрование диска операции на hello одной виртуальной Машины. |
| vmName | Hello виртуальной Машины, операция шифрования hello называется toobe блокировкой. |

> [!NOTE]
> _KeyEncryptionKeyURL_ является необязательным параметром. Вы можете воплощать свои собственные KEK toofurther защиты hello ключ шифрования данных (секрета шифрования BitLocker) в хранилище ключей hello.

#### <a name="using-powershell-cmdlets"></a>Использование командлетов PowerShell
Сведения о включении шифрования с помощью шифрования диска Azure с помощью командлетов PowerShell см. в блогах hello [исследовать шифрование диска Azure с использованием Azure PowerShell, часть 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) и [исследовать шифрование диска Azure с помощью Azure PowerShell — часть 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).

#### <a name="using-cli-commands"></a>Использование команд интерфейса командной строки
шифрование tooenable на существующие или ВМ IaaS Windows в Azure с помощью команды CLI hello следующие:

1. tooset политики доступа в хранилище ключей hello:
   * Набор hello **EnabledForDiskEncryption** флаг:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * Набор разрешений tooAzure AD приложения toowrite секреты tooyour хранилища ключей:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. шифрование tooenable на Виртуальной машине существующий или не запущены:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. состояние шифрования tooget:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. шифрование tooenable на новой виртуальной Машины с зашифрованного диска, hello используйте следующие параметры с hello `azure vm create` команды:

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a>Включение шифрования на виртуальной машине IaaS под управлением Linux, которая уже существует или работает в Azure
Можно включить шифрование диска на виртуальной Машине Linux IaaS существующих или работает в Azure с помощью hello [шаблона диспетчера ресурсов](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).

1. Нажмите кнопку **развертывание tooAzure** на шаблоне hello Azure краткое введите конфигурацию шифрования hello на hello **параметры** и, при необходимости нажмите кнопку **ОК**.

2. Выберите подписку hello, группы ресурсов, расположение группы ресурсов, условия и соглашения и нажмите кнопку **создать** tooenable шифрование на hello существующий или под управлением ВМ IaaS.

Привет, в следующей таблице перечислены параметры шаблона диспетчера ресурсов для существующих или работающих виртуальных машин, использующих идентификатор клиента Azure AD.

| Параметр | Описание |
| --- | --- |
| AADClientID | Идентификатор клиента приложения hello Azure AD с хранилище ключей toohello секреты toowrite разрешения. |
| AADClientSecret | Секрет клиента приложения Azure AD hello хранилища ключей tooyour секреты toowrite разрешения. |
| keyVaultName | Имя ключа hello хранилища, должна быть передана ключ BitLocker hello. Его можно получить с помощью командлета hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`. |
|  keyEncryptionKeyURL | URL-адрес ключа шифрования ключа hello, используемые tooencrypt hello созданный ключ BitLocker. Этот параметр является необязательным, если выбрать **nokek** hello UseExistingKek раскрывающегося списка. При выборе **kek** hello UseExistingKek раскрывающегося списка, необходимо ввести hello _keyEncryptionKeyURL_ значение. |
| volumeType | Тип тома, для которого выполняется операция шифрования hello. Поддерживаемые допустимые значения: _OS_ или _All_ (для RHEL 7.2, CentOS 7.2 и Ubuntu 16.04) и _Data_ (для всех остальных дистрибутивов). |
| sequenceVersion | Версия последовательности hello операции BitLocker. Этот номер версии увеличивается, каждый раз, шифрование диска операции на hello одной виртуальной Машины. |
| vmName | Hello виртуальной Машины, операция шифрования hello называется toobe блокировкой. |
| passPhrase | Введите ключ шифрования данных hello надежную парольную фразу. |

> [!NOTE]
> _KeyEncryptionKeyURL_ является необязательным параметром. Собственные KEK toofurther защиты hello ключ шифрования данных (секрет парольную фразу) можно импортировать в хранилище ключей.

#### <a name="cli-commands"></a>Команды интерфейса командной строки
Можно включить шифрование диска на зашифрованные им при установке и использовании hello [команду CLI](../cli-install-nodejs.md). шифрование tooenable на существующие или виртуальным машинам IaaS Linux в Azure с помощью команд CLI hello следующие:

1. Задать политику доступа в хранилище ключей hello:

 * Набор hello **EnabledForDiskEncryption** флаг:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * Набор разрешений tooAzure AD приложения toowrite секреты tooyour хранилища ключей:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. шифрование tooenable на Виртуальной машине существующий или не запущены:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. Получите состояние шифрования, введя следующую команду.

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. шифрование tooenable на новой виртуальной Машины с зашифрованного диска, hello используйте следующие параметры с hello `azure vm create` команды:
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a>Получить состояние шифрования зашифрованных ВМ IaaS hello
Состояние шифрования hello можно получить с помощью диспетчера ресурсов Azure, [командлеты PowerShell](/powershell/azure/overview), или команды CLI. Hello в следующих разделах объясняется, как toouse hello классический портал Azure и tooget команд CLI hello состояние шифрования.

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a>Получить состояние шифрования hello зашифрованные виртуальной машины Windows с помощью диспетчера ресурсов Azure
Состояние шифрования hello hello ВМ IaaS из диспетчера ресурсов Azure можно получить, выполнив hello ниже:

1. Вход toohello [классический портал Azure](https://portal.azure.com/), а затем нажмите кнопку **виртуальные машины** в левой области hello toosee сводное представление hello виртуальных машин в вашей подписке. Вы можете фильтровать представление виртуальных машин hello, выбрав имя подписки hello в hello **подписки** раскрывающегося списка.

2. Вверху hello hello **виртуальные машины** щелкните **столбцы**.

3. На hello **Выбор столбца** колонке выберите **шифрование диска**и нажмите кнопку **обновление**. Вы увидите состояние шифрования для столбца отображение hello шифрование диска hello _включено_ или _не включена_ для каждой виртуальной Машины, как показано в следующий рисунок hello:

 ![Антивредоносное ПО Майкрософт в Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a>Состояние шифрования hello зашифрованные ВМ IaaS (Windows или Linux) можно получить с помощью командлета PowerShell hello шифрование диска
Состояние шифрования hello hello ВМ IaaS можно получить из командлета PowerShell шифрование диска hello `Get-AzureRmVMDiskEncryptionStatus`. параметры шифрования hello tooget для виртуальной Машины, введите hello следующие данные:

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

Можно просмотреть выходные данные hello _Get AzureRmVMDiskEncryptionStatus_ для шифрования ключа URL-адреса.

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

Hello OSVolumeEncrypted и значения параметров DataVolumesEncrypted задаются too_Encrypted_, показывающий, что обоих томов, шифруются с помощью шифрования диска Azure. Сведения о включении шифрования с помощью шифрования диска Azure с помощью командлетов PowerShell см. в блогах hello [исследовать шифрование диска Azure с использованием Azure PowerShell, часть 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) и [исследовать шифрование диска Azure с помощью Azure PowerShell — часть 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).

> [!NOTE]
> На виртуальных машинах Linux, он принимает три минуты toofour для hello `Get-AzureRmVMDiskEncryptionStatus` состояние шифрования hello tooreport командлета.

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a>Получить состояние шифрования hello hello ВМ IaaS из команду CLI hello шифрование диска
Состояние шифрования hello hello ВМ IaaS можно получить с помощью команды CLI шифрование диска hello `azure vm show-disk-encryption-status`. параметры шифрования hello tooget для виртуальной Машины, введите ваш сеанс Azure CLI:

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a>Отключение шифрования на работающей виртуальной машине IaaS под управлением Windows
Можно отключить шифрование на запуск Windows или Linux ВМ IaaS через hello шаблона диспетчера ресурсов шифрования диска Azure или командлеты PowerShell и указать конфигурацию расшифровки hello.

##### <a name="windows-vm"></a>Виртуальная машина Windows
Hello отключение шифрования шаг отключает шифрование hello ОС hello объем данных, и на выполнение ВМ IaaS Windows hello. Невозможно отключить hello тома операционной системы и оставьте шифрованием hello данных тома. При выполнении шага hello disable шифрования hello Azure классической модели развертывания обновляет hello модели службы ВМ и ВМ IaaS Windows hello помечен расшифрованные. содержимое Hello hello ВМ больше не шифруются при хранении. Расшифровка Hello не удаляет вашего ключа хранилища и hello основы ключа шифрования (ключи шифрования BitLocker для Windows и парольную фразу для Linux).

##### <a name="linux-vm"></a>Виртуальная машина Linux
Hello отключение шифрования шаг отключает шифрование тома данных hello hello под управлением Linux ВМ IaaS. Этот шаг работает только в том случае, если диск ОС hello не шифруются.

> [!NOTE]
> Отключение шифрования на диске ОС hello не допускается на виртуальных машинах Linux.

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>Отключение шифрования на существующей или запущенной виртуальной машине IaaS
Можно отключить шифрование диска на работающих виртуальных машин IaaS Windows с помощью hello [шаблона диспетчера ресурсов](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).

1. Hello Azure краткое шаблон, нажмите кнопку **развертывание tooAzure**, введите hello расшифровки конфигурации на hello **параметры** и, при необходимости нажмите кнопку **ОК**.

2. Выберите подписку hello, группы ресурсов, расположение группы ресурсов, условия и соглашения и нажмите кнопку **создать** tooenable шифрование на новую виртуальную Машину IaaS.

Для виртуальных машин Linux, можно отключить шифрование с помощью hello [отключить шифрование на работающей ВМ Linux](https://aka.ms/decrypt-linuxvm) шаблона.

Hello следующей таблице перечислены параметры шаблона диспетчера ресурсов для отключения шифрования на работающей ВМ IaaS.

| Параметр | Описание |
| --- | --- |
| vmName | Hello виртуальной Машины, операция шифрования hello называется toobe блокировкой.
| volumeType | Тип тома, для которого будет выполняться расшифровка. Допустимые значения: _OS_, _Data_ и _All_. Невозможно отключить шифрование на под управлением ОС ВМ IaaS Windows или загрузочного тома без отключения шифрования hello _данные_ тома. Также Обратите внимание, что отключение шифрования на диске ОС hello не разрешен на виртуальных машинах Linux. |
| sequenceVersion | Версия последовательности hello операции BitLocker. Этот номер версии увеличивается, каждый раз операции расшифровки диска выполняется на hello одной виртуальной Машины. |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>Отключение шифрования на существующей или запущенной виртуальной машине IaaS
toodisable шифрования на виртуальной Машине IaaS существующих или не запущены с помощью командлета PowerShell hello, в разделе [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption). Этот командлет поддерживает виртуальные машины Linux и Windows. шифрование toodisable устанавливаются расширения на виртуальной машине hello. Если hello _имя_ параметр не указан, расширения с именем по умолчанию hello _AzureDiskEncryption ВМ_ создается.

На виртуальных машинах Linux используется hello AzureDiskEncryptionForLinux расширения.

> [!NOTE]
> Этот командлет перезагружает hello виртуальной машины.

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a>Включение шифрования для предварительно зашифрованной виртуальной машины IaaS с управляемым диском Azure
Используйте hello ARM диска управляемых Azure шаблона toocreate зашифрованные виртуальной Машины на основе предварительно зашифрованный VHD с помощью шаблона hello ARM, расположенный в   
[Создание зашифрованного управляемого диска на основе предварительно зашифрованного виртуального жесткого диска или BLOB-объекта] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a>Включение шифрования для новой виртуальной машины IaaS с ОС Linux и управляемым диском Azure
Используйте hello ARM диска управляемых Azure шаблона toocreate новое зашифрованное ВМ IaaS Linux с помощью шаблона hello ARM, расположенный в   
[Развертывание RHEL 7.2 с полным шифрованием дисков] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a>Включение шифрования для новой виртуальной машины IaaS с ОС Windows и управляемым диском Azure
 Используйте hello ARM диска управляемых Azure шаблона toocreate новое зашифрованное ВМ IaaS Linux с помощью шаблона hello ARM, расположенный в   
 [Создание зашифрованной виртуальной машины IaaS с ОС Windows и управляемым диском на основе образа из коллекции] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)

  > [!NOTE]
  >Это обязательный toosnapshot и/или резервного копирования управляемого диска на основе экземпляра виртуальной Машины за пределами и предыдущих tooenabling шифрование диска Azure.  Моментальный снимок hello управляемого диска могут браться из портала hello или Azure Backup может использоваться.  Резервные копии убедитесь, что параметр восстановления возможно в случае, когда hello любой непредвиденный сбой во время шифрования.  После выполнения резервной копии командлет hello AzureRmVMDiskEncryptionExtension набор может быть дисков используется tooencrypt управляемых с помощью параметра - skipVmBackup hello.  Эта команда будет завершаться ошибкой при использовании с виртуальными машинами на основе управляемых дисков, пока не будет сделана резервная копия и указан определенный параметр.    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a>Изменение параметров шифрования существующей зашифрованной виртуальной машины не класса "Премиум"
  Используйте hello существующие диск Azure поддерживает шифрование интерфейсы для запуска виртуальной Машины [командлеты PS, CLI или ARM шаблонов] tooupdate hello параметры шифрования, например клиента AAD ID и секретный ключ шифрования ключа [KEK], ключ шифрования BitLocker для виртуальной Машины Windows или парольную фразу для Виртуальная машина Linux т. д. hello обновления шифрования параметр поддерживается только для виртуальных машин, поддерживаемый хранения Premium-класса. Оно не поддерживается для виртуальных машин на основе хранилища класса "Премиум".

## <a name="appendix"></a>Приложение
### <a name="connect-tooyour-subscription"></a>Подключение tooyour подписки
Прежде чем продолжить, просмотрите hello *необходимые компоненты* этой статьи. Убедившись, что выполнены все необходимые компоненты, подключите tooyour подписки, выполнив следующие hello:

1. Запустите сеанс Azure PowerShell и войдите в учетную запись Azure tooyour с hello следующую команду:

    `Login-AzureRmAccount`

2. Если есть несколько подписок и требуется один toouse toospecify, введите hello, следуя toosee hello подписки для учетной записи:

    `Get-AzureRmSubscription`

3. toospecify hello подписку toouse, тип:

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. правильность настройки подписки hello tooverify, введите:

    `Get-AzureRmSubscription`

5. hello tooconfirm установлены командлеты, шифрование диска Azure типа:

    `Get-command *diskencryption*`

6. После вывода Hello подтверждает hello Azure PowerShell шифрования диска установки:

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a>Подготовка предварительно зашифрованного виртуального жесткого диска Windows
Hello разделах являются необходимые tooprepare предварительно зашифрованный виртуального жесткого диска Windows для развертывания в виде зашифрованного виртуального жесткого диска в Azure IaaS. Использовать сведения tooprepare hello и загрузите новую Windows виртуальной Машины (VHD) на Azure или Azure Site Recovery.

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a>Обновление групповой политики tooallow без НЕГО для защиты операционной системы
Настройте параметр групповой политики BitLocker hello **шифрования диска BitLocker**, его можно найти в разделе **политика локального компьютера** > **Конфигурация компьютера**  >  **Административные шаблоны** > **компоненты Windows**. Изменить этот параметр слишком**диски операционной системы** > **требуется дополнительная проверка подлинности при запуске** > **разрешить использование BitLocker без совместимого TPM**, как показано в следующий рисунок hello:

![Антивредоносное ПО Майкрософт в Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a>Установка компонентов BitLocker
Windows Server 2012 и более поздних версий используйте hello следующую команду:

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

Для Windows Server 2008 R2 используйте hello следующую команду:

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a>Подготовьте hello тома операционной системы с помощью BitLocker`bdehdcfg`
toocompress hello раздела операционной системы и подготовка машины hello для BitLocker, выполните следующую команду hello.

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a>Защита hello тома операционной системы с помощью BitLocker
Используйте hello [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) шифрование tooenable команды на hello загрузочного тома с помощью внешнего средства защиты ключа. Также можно поместите hello внешнего ключа (.bek-файл) на hello внешний диск или том. После следующей перезагрузки hello включено шифрование для hello системный или загрузочный том.

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> Подготовьте hello виртуальной Машины с отдельной или ресурса данных виртуального жесткого диска для получения hello внешнего ключа с помощью BitLocker.

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a>Шифрование диска ОС на работающей виртуальной машине Linux
После распределения hello поддерживается шифрования диска операционной системы на работающей виртуальной Машины Linux:

* RHEL 7.2;
* CentOS 7.2;
* Ubuntu 16.04.

##### <a name="prerequisites-for-os-disk-encryption"></a>Предварительные требования для шифрования диска ОС

* Hello ВМ должны быть созданы из образа Marketplace hello в диспетчере ресурсов Azure.
* Виртуальная машина Azure по крайней мере с 4 ГБ ОЗУ (рекомендуемый размер — 7 ГБ).
* (Для RHEL и CentOS.) Отключите SELinux. toodisable SELinux, в разделе «4.4.2. Отключение SELinux» в hello [руководство администратора и пользователя SELinux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) на hello виртуальной Машины.
* После отключения SELinux перезагрузите hello ВМ по крайней мере один раз.

##### <a name="steps"></a>Действия
1. Создайте виртуальную Машину с помощью одного из распределения hello, указанном ранее.

 Для CentOS 7.2 шифрование диска операционной системы можно включить через специальный образ. toouse это изображения, укажите «7.2n» как hello SKU при создании hello виртуальной Машины:
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. Настройте соответствующим требованиям tooyour hello виртуальной Машины. Если вы собираетесь tooencrypt все диски hello (ОС + данные), диски с данными hello должны toobe указанного и подключить из/etc/fstab.

 > [!NOTE]
 > Используйте UUID =... toospecify дисках с данными в/etc/fstab вместо указания имени устройства hello блока (например, / dev/sdb1). Во время шифрования hello порядок изменений дисков на hello виртуальной Машины. Если ВМ зависит от определенного порядка блочные устройства, то возникнет ошибка toomount их после шифрования.

3. Выйдите из сеансов SSH hello.

4. hello tooencrypt операционной системы, укажите volumeType как **все** или **ОС** при вы [включить шифрование](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).

 > [!NOTE]
 > Все пользовательские процессы, не запущенные как службы `systemd`, необходимо завершить с помощью `SIGKILL`. Перезагрузите hello виртуальной Машины. В случае включения шифрования диска ОС на работающей виртуальной запланируйте период простоя.

5. Периодически отслеживать ход hello шифрования с помощью инструкции hello в hello [разделу](#monitoring-os-encryption-progress).

6. После Get AzureRmVmDiskEncryptionStatus показывает «VMRestartPending», перезапуск виртуальной Машины при входе в tooit или с помощью портала hello, PowerShell или интерфейс командной строки.
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
До перезагрузки, рекомендуется сохранить [загрузки диагностики](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) из hello виртуальной Машины.

#### <a name="monitoring-os-encryption-progress"></a>Мониторинг хода выполнения шифрования операционной системы
Мониторинг хода выполнения шифрования ОС можно выполнять тремя способами.

* Используйте hello `Get-AzureRmVmDiskEncryptionStatus` командлета и проверьте поля ProgressMessage hello:
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 После hello виртуальной Машины достигает «На диске ОС шифрования к работе», занимает около 40 минут too50 хранилища Premium резервного виртуальной Машины.

 В связи с [ошибкой № 388](https://github.com/Azure/WALinuxAgent/issues/388) в WALinuxAgent в некоторых дистрибутивах `OsVolumeEncrypted` и `DataVolumesEncrypted` отображаются как `Unknown`. В WALinuxAgent 2.1.5 и более поздних версиях эта проблема исправляется автоматически. Если вы видите `Unknown` в выходных данных hello, можно проверить состояние шифрования диска с помощью hello обозревателя ресурсов Azure.

 Go слишком[обозревателя ресурсов Azure](https://resources.azure.com/), а затем разверните эту иерархию в область выбора hello слева:

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 Hello InstanceView прокрутите вниз toosee hello состояние шифрования дисков.

 ![Представление экземпляра виртуальной машины](./media/azure-security-disk-encryption/vm-instanceview.png)

* Просмотрите [диагностические данные загрузки](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/). Сообщения от hello ADE расширение должно начинаться с `[AzureDiskEncryption]`.

* Войдите в toohello виртуальной Машины по протоколу SSH и получить журнал hello расширения из:

    /var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux

 Мы рекомендуем, что вы не выполняют вход в toohello виртуальной Машины во время шифрования операционной системы. Копировать журналы hello, только когда hello других двух методов завершились ошибкой.

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a>Подготовка предварительно зашифрованного виртуального жесткого диска Linux
##### <a name="ubuntu-16"></a>Ubuntu 16
Настройка шифрования во время установки распространения hello, выполнив hello ниже:

1. Выберите **Настройка зашифрованных томов** при секционировании hello дисков.

 ![Настройка Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. Создайте отдельный загрузочный диск (незашифрованный). Зашифруйте корневой диск.

 ![Настройка Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. Укажите парольную фразу. Это hello парольную фразу, передаче toohello хранилища ключей.

 ![Настройка Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. Завершите настройку разделов.

 ![Настройка Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. При загрузке hello виртуальной Машины и требуется указать парольную фразу, используйте hello парольную фразу, что на шаге 3.

 ![Настройка Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. Подготовка виртуальной Машины hello для передачи в Azure с помощью [эти инструкции](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/). Еще не запущены на последнем шаге hello (hello списания виртуальной Машины).

Настройка шифрования toowork с Azure, выполнив hello ниже:

1. Создайте файл /usr/local/sbin/azure_crypt_key.sh, с содержимым hello в hello, выполнив сценарий. Обратите внимание toohello имя файла, так как это имя файла hello парольную фразу, используемые в Azure.

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. Изменение конфигурации crypt hello в *crypttab/etc/*. Результат будет выглядеть так:
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. Если вы изменяете *azure_crypt_key.sh* в Windows и скопировать его tooLinux, запустите `dos2unix /usr/local/sbin/azure_crypt_key.sh`.

4. Добавьте скрипт toohello исполняемый файл разрешений:
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. Измените */etc/initramfs-tools/modules*, добавив приведенные ниже строки.
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. Запустите `update-initramfs -u -k all` initramfs toomake tooupdate hello hello `keyscript` вступили в силу.

7. Теперь можно сделать hello виртуальной Машины.

 ![Настройка Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. Продолжить toohello следующий шаг и [отправить им](#upload-encrypted-vhd-to-an-azure-storage-account) в Azure.

##### <a name="opensuse-132"></a>openSUSE 13.2
шифрование tooconfigure во время установки распространения hello hello следующие:
1. При секционировании hello дисков выберите **шифрования группы томов**, а затем введите пароль. Это hello пароль, который будет передан tooyour хранилища ключей.

 ![Настройка openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. Загрузите hello виртуальную Машину с помощью пароля.

 ![Настройка openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. Подготовка hello виртуальной Машины для передачи в соответствии с инструкциями hello в tooAzure [Подготовка виртуальной машины SLES или openSUSE для Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131). Еще не запущены на последнем шаге hello (hello списания виртуальной Машины).

tooconfigure toowork шифрования с помощью Azure hello следующие:
1. Измените hello /etc/dracut.conf и добавьте hello, следующей строкой:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. Закомментируйте эти строки концу hello hello файла /usr/lib/dracut/modules.d/90crypt/module-setup.sh:
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. Добавьте hello, следующей строкой в начале hello hello /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh файла:
 ```
    DRACUT_SYSTEMD=0
 ```
Затем измените все вхождения
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
на:
```
    if [ 1 ]; then
```
4. Изменить /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh и добавьте к нему слишком «# откройте LUKS устройства»:

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. Запустите `/usr/sbin/dracut -f -v` tooupdate hello initrd.

6. Теперь можно hello виртуальной Машины и [отправить им](#upload-encrypted-vhd-to-an-azure-storage-account) в Azure.

##### <a name="centos-7"></a>CentOS 7
шифрование tooconfigure во время установки распространения hello hello следующие:
1. Во время настройки разделов дисков выберите **Encrypt my data** (Шифрование личных данных).

 ![Настройка CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. Включите шифрование для корневого раздела (параметр **Encrypt**).

 ![Настройка CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. Укажите парольную фразу. Это hello парольная фраза будет отправлять tooyour хранилища ключей.

 ![Настройка CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. При загрузке hello виртуальной Машины и требуется указать парольную фразу, используйте hello парольную фразу, что на шаге 3.

 ![Настройка CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. Hello подготовки виртуальной Машины для передачи в Azure с помощью инструкции «CentOS 7.0 +» hello в [Подготовка виртуальной машины на основе CentOS для Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70). Еще не запущены на последнем шаге hello (hello списания виртуальной Машины).

6. Теперь можно hello виртуальной Машины и [отправить им](#upload-encrypted-vhd-to-an-azure-storage-account) в Azure.

tooconfigure toowork шифрования с помощью Azure hello следующие:

1. Измените hello /etc/dracut.conf и добавьте hello, следующей строкой:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. Закомментируйте эти строки концу hello hello файла /usr/lib/dracut/modules.d/90crypt/module-setup.sh:
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. Добавьте hello, следующей строкой в начале hello hello /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh файла:
```
    DRACUT_SYSTEMD=0
```
Затем измените все вхождения
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
значение
```
    if [ 1 ]; then
```
4. Измените /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh и добавить это после «# откройте LUKS device» hello:
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. Запустите hello «/ usr/sbin/dracut - f - v» tooupdate hello initrd.

![Настройка CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a>Отправка зашифрованного учетной записи хранилища Azure tooan виртуального жесткого диска
После включения шифрования BitLocker или Crypt интеллектуальный анализ данных для шифрования локальных hello шифруются учетной записи хранилища tooyour toobe отправлен потребностей виртуального жесткого диска.

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a>Отправка hello секрет шифрование диска для hello предварительно зашифрованный ВМ tooyour хранилища ключей
секрет Hello шифрование диска, полученный ранее должен быть передан как секрет в хранилище ключей. хранилище ключей Hello должен toohave шифрования диска и разрешениями, назначенными для вашего клиента Azure AD.

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a>Секрет дискового шифрования не шифруется с помощью KEK
tooset копирование hello секрет в хранилище ключей, используйте [AzureKeyVaultSecret набор](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret). При наличии виртуальной машины Windows hello bek файл кодируется в виде строки base64, а затем загружается tooyour хранилища ключей с помощью hello `Set-AzureKeyVaultSecret` командлета. Для Linux парольную фразу hello кодируется в виде строки base64 и затем загружается toohello хранилища ключей. Кроме того убедитесь, что этот hello следующие теги задаются при создании hello секрет в хранилище ключей hello.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

Используйте hello `$secretUrl` hello на следующем шаге для [присоединение диска hello ОС без использования KEK](#without-using-a-kek).

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a>Секрет дискового шифрования, зашифрованный с помощью KEK
Перед отправкой хранилища ключей секретный toohello hello, вы можете зашифровать с помощью ключа шифрования. Используйте hello wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst шифрования с помощью ключа шифрования ключа hello секрет hello. Hello этой операции wrap выводится строка URL-адреса в кодировке base64 можно затем передать как секрета с помощью hello [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) командлета.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

Используйте `$KeyEncryptionKey` и `$secretUrl` hello на следующем шаге для [присоединение диска hello операционной системы с помощью ключа обмена Ключами](#using-a-kek).

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a>Указание URL-адреса секрета при подключении диска ОС
#### <a name="without-using-a-kek"></a>Без использования ключа шифрования ключа
Во время присоединения диска hello ОС, необходимо toopass `$secretUrl`. Hello URL-адрес был создан в разделе «Шифрование диска не зашифрован с помощью ключа обмена Ключами секрет» hello.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a>С использованием ключа шифрования ключа
При подключении диска hello ОС, передайте `$KeyEncryptionKey` и `$secretUrl`. Hello URL-адрес был создан в разделе «Шифрование диска не зашифрован с помощью ключа обмена Ключами секрет» hello.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a>Загрузка руководства
Это руководство можно загрузить из hello [коллекции TechNet](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).

## <a name="for-more-information"></a>Дополнительные сведения
[Explore Azure Disk Encryption with Azure PowerShell](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0) (Изучение возможностей шифрования дисков Azure с помощью PowerShell)  
[Изучение возможностей дискового шифрования Azure с помощью Azure PowerShell — часть 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
