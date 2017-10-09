---
title: "Общие сведения о виртуальных машинах aaaWindows | Документы Microsoft"
description: "Узнайте о создании виртуальных машинах Windows в Azure и управлении ими."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: fbae9c8e-2341-4ed0-bb20-fd4debb2f9ca
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 8015b1aa4bcdaac2e721f25d85a5bc995a22f0f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-windows-virtual-machines-in-azure"></a>Обзор виртуальных машин Windows в Azure

Виртуальные машины Azure — один из нескольких типов [запрашиваемых масштабируемых вычислительных ресурсов](../../app-service-web/choose-web-site-cloud-service-vm.md), которые предоставляет Azure. Как правило когда требуется больший контроль над hello вычислительную среду, чем hello другие варианты предлагать выберите виртуальной Машины. В этой статье содержатся сведения о том, что следует учитывать перед созданием виртуальной машины, а также инструкции по созданию виртуальной машины и управлению ею.

Виртуальная машина Azure предоставляет hello гибкие возможности виртуализации без необходимости toobuy и поддерживать hello физическое оборудование, запускает его. Однако по-прежнему требуются toomaintain hello виртуальной Машины, выполнив действия, такие как настройка, исправление и установке hello программное обеспечение, которое выполняется на нем.

Виртуальные машины Azure можно использовать разными способами. Ниже приведены некоторые примеры.

* **Разработки и тестирования** — виртуальные машины Azure предлагают быстро и легко toocreate компьютер с определенных конфигураций необходимые toocode и тестирования приложения.
* **Приложения в облаке hello** — поскольку спрос на ваше приложение может меняться, может быть toorun экономической точки зрения его на виртуальной Машине в Azure. Вы платите за дополнительные виртуальные машины, если они вам нужны, и отключаете их, если они не нужны.
* **Расширенные центра обработки данных** — виртуальные машины в виртуальной сети Azure может быть легко подключенных tooyour корпоративной сети.

Hello число виртуальных машин, которые приложение использует можно увеличивать масштаб и ожидания toowhatever является обязательным toomeet вашим потребностям.

## <a name="what-do-i-need-toothink-about-before-creating-a-vm"></a>Что нужно сделать toothink о перед созданием виртуальной Машины?
При создании инфраструктуры приложения в Azure всегда нужно учитывать множество [рекомендаций по проектированию](/architecture/reference-architectures/virtual-machines-linux?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Эти компоненты виртуальной Машины не важные toothink о перед началом:

* имена Hello ресурсами приложения
* Hello расположение, где хранятся ресурсы hello
* размер Hello hello виртуальной Машины
* Максимальное число виртуальных машин, которые могут быть созданы для Hello
* запускает Hello операционной системы, которая hello виртуальной Машины
* Конфигурация Hello hello виртуальной Машины после ее запуска
* Hello ресурсы, связанные с этой виртуальной Машины должен hello

### <a name="naming"></a>Именование
Виртуальная машина имеет [имя](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) назначенный tooit и он имеет имя настроена как часть hello операционной системы. Hello имя виртуальной машины может быть вверх too15 символов.

Если используется диск операционной системы hello Azure toocreate, hello имя компьютера и имя виртуальной машины hello hello таким же. Если вы [передавать и использовать собственное изображение](upload-generalized-managed.md) , содержащий ранее настроенный операционной системы и использовать его toocreate виртуальной машины, hello имена могут быть разными. Рекомендуется при передаче файла изображения, принять hello имя компьютера в операционной системе hello и имя виртуальной машины hello hello таким же.

### <a name="locations"></a>Расположения
Все ресурсы, созданные в Azure распределены между несколькими [географических регионов](https://azure.microsoft.com/regions/) вокруг Здравствуй, мир. Как правило, называется hello области **расположение** при создании виртуальной Машины. Для виртуальной Машины местоположение hello указывает, где хранятся hello виртуальных жестких дисков.

В этой таблице показано несколько способов hello можно получить список доступных расположений.

| Метод | Описание |
| --- | --- |
| Портал Azure |Выберите расположение из списка hello при создании виртуальной Машины. |
| Azure PowerShell |Используйте hello [Get AzureRmLocation](/powershell/module/azurerm.resources/get-azurermlocation) команды. |
| Интерфейс REST API |Используйте hello [список расположений](https://docs.microsoft.com/rest/api/resources/subscriptions#Subscriptions_ListLocations) операции. |

### <a name="vm-size"></a>Размер виртуальной машины
Hello [размер](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello виртуальная машина, которую вы используете определяется hello рабочей нагрузкой, которые должны toorun. затем Hello размеру, выбранному определяет факторы, например электропитания, памяти и хранилища производительности обработки. Azure предлагает широкий спектр размеры toosupport многие типы задач.

Azure взимает плату [почасовую оплату](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) на основе размера ВМ hello и операционной системы. Неполного использования часа Azure расходов только для минут, hello. Плата за использование хранилища взимается отдельно.

### <a name="vm-limits"></a>Ограничения виртуальной машины
Ваша подписка имеет по умолчанию [квоты](../../azure-subscription-service-limits.md) в месте, которое может повлиять на развертывание hello много виртуальных машин для проекта. Привет текущее ограничение на каждой подписки — 20 виртуальных машин в одном регионе. Чтобы увеличить квоту, следует отправить соответствующий запрос в службу поддержки.

### <a name="operating-system-disks-and-images"></a>Диски и образы операционной системы
Виртуальные машины используют [виртуальные жесткие диски (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toostore их операционной системы (ОС) и данных. Виртуальные жесткие диски, также используются для образов hello, выбранный из tooinstall ОС. 

Azure предоставляет множество [marketplace образов](https://azure.microsoft.com/marketplace/virtual-machines/) toouse с различными версиями и операционных системах Windows Server. Образы из Marketplace определяются по издателю, предложению, SKU и версии (обычно указывается последняя версия). 

В этой таблице показано несколько способов, которые можно найти сведения о hello для изображения.

| Метод | Описание |
| --- | --- |
| Портал Azure |При выборе образа toouse Hello значения будут автоматически заданы автоматически. |
| Azure PowerShell |[Get-AzureRMVMImagePublisher](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimagepublisher). Параметр -Location указывает расположение.<BR>[Get-AzureRMVMImageOffer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimageoffer). Параметр -Location указывает расположение, -PublisherName — издателя.<BR>[Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku). Параметр -Location указывает расположение, -PublisherName — издателя, а -Offer — предложение. |
| Интерфейсы API REST |[Получение списка издателей образов](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publishers)<BR>[Получение списка предложений для образа](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offers)<BR>[Получение списка SKU для образа](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offer-skus) |

Вы можете слишком[передавать и использовать собственное изображение](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account) и при этом имя издателя hello, предложения и sku не используются.

### <a name="extensions"></a>расширения.
[Расширения](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) виртуальных машин предоставляют дополнительные возможности за счет настройки после развертывания и автоматизированных задач.

С помощью расширений можно выполнить такие стандартные задачи:

* **Запустить пользовательские скрипты** — hello [расширение пользовательского скрипта](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) позволяет настраивать рабочие нагрузки на hello виртуальной Машины, выполнив сценарий, когда hello подготавливается виртуальная машина.
* **Развертывание и управление конфигурациями** — hello [расширения конфигурации требуемого состояния (DSC) PowerShell](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) помогает настроить DSC на toomanage ВМ конфигурациями и средами.
* **Собирать данные диагностики** — hello [расширения системы диагностики Azure](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) помогает настроить hello toocollect ВМ диагностические данные можно использовать toomonitor hello работоспособности приложения.

### <a name="related-resources"></a>Связанные ресурсы
Hello ресурсов в этой таблице используются hello ВМ и должны tooexist или при создании hello виртуальной Машины.

| Ресурс | Обязательно | Description (Описание) |
| --- | --- | --- |
| [Группа ресурсов](../../azure-resource-manager/resource-group-overview.md) |Да |Hello ВМ должны содержаться в группе ресурсов. |
| [Учетная запись хранения](../../storage/common/storage-create-storage-account.md) |Да |Hello виртуальной Машины должен toostore учетной записи хранилища hello ее виртуальные жесткие диски. |
| [Виртуальная сеть](../../virtual-network/virtual-networks-overview.md) |Да |Hello виртуальная машина должна входить в виртуальной сети. |
| [Общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) |Нет |Hello виртуальная машина может иметь открытый IP-адреса, назначенного tooit tooremotely доступ к нему. |
| [Сетевой интерфейс](../../virtual-network/virtual-network-network-interface.md) |Да |Hello виртуальной Машины должен hello сетевой интерфейс toocommunicate в сети hello. |
| [Диски данных](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |Нет |Hello ВМ могут включать возможности хранилища tooexpand дисков данных. |

## <a name="how-do-i-create-my-first-vm"></a>Как создать первую виртуальную машину?
Существует несколько способов создания виртуальной машины. Hello выбор, производимый зависит от среды hello, указываются в. 

Эта таблица предоставляет сведения tooget вы начали создание виртуальной Машины.

| Метод | Статья |
| --- | --- |
| Портал Azure |[Создание виртуальной машины под управлением Windows, с помощью портала hello](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Шаблоны |[Создание виртуальной машины Windows с использованием шаблона диспетчера ресурсов](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Azure PowerShell |[Создание виртуальной машины Windows с помощью PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Клиентские пакеты SDK |[Развертывание ресурсов Azure с помощью языка C#](csharp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Интерфейсы API REST |[Создание или обновление виртуальной машины](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-create-or-update) |

Так или иначе, иногда вы будете сталкиваться с проблемами. Если в такой ситуации tooyou взгляните hello данные [Устранение неполадок диспетчера ресурсов проблем развертывания с созданием виртуальной машины Windows в Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="how-do-i-manage-hello-vm-that-i-created"></a>Как управлять hello виртуальная машина, созданная?
Управление виртуальными машинами осуществляется с помощью браузерного портала, программ командной строки с поддержкой создания скриптов или напрямую с помощью интерфейсов API. Некоторые стандартные административные задачи, которые можно выполнять получение сведений о виртуальной Машины, вход в систему tooa виртуальной Машины, управление доступности и выполнение резервного копирования.

### <a name="get-information-about-a-vm"></a>Получение информации о виртуальной машине
В этой таблице показаны некоторые способы hello, можно получить сведения о виртуальной Машине.

| Метод | Описание |
| --- | --- |
| Портал Azure |Hello концентратора меню **виртуальные машины** и выберите из списка hello hello виртуальной Машины. В колонке hello для hello виртуальной Машины у вас есть toooverview доступа к данным, значения параметров и показателей мониторинга. |
| Azure PowerShell |Сведения об использовании виртуальных машин toomanage PowerShell см. в разделе [Создание и управление виртуальными машинами Windows с помощью модуля Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |
| Интерфейс REST API |Используйте hello [получить ВМ сведения](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) операции tooget сведения о виртуальной Машине. |
| Клиентские пакеты SDK |Сведения об использовании виртуальных машин toomanage C# см. в разделе [управление виртуальных машин Azure с помощью диспетчера ресурсов Azure и C#](csharp-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |

### <a name="log-on-toohello-vm"></a>Войдите на toohello виртуальной Машины
Использование кнопки "Подключиться" hello в hello портал Azure слишком[запуск сеанса удаленного рабочего стола (RDP)](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Могут иногда возникнуть проблемы при попытке toouse удаленного подключения. Если в такой ситуации tooyou извлечь hello справочной информации в [tooan подключения удаленного рабочего стола на устранение неполадок Azure виртуальную машину под управлением Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="manage-availability"></a>Управление доступностью
Очень важно для вас toounderstand как слишком[обеспечения высокого уровня доступности](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) для вашего приложения. Эта конфигурация состоит в создании нескольких tooensure виртуальные машины, на котором выполняется по крайней мере один.

Чтобы tooqualify вашего развертывания для наших 99.95 соглашения уровня службы виртуальной Машины, необходимо toodeploy двух или более виртуальных машин, запущенных внутри рабочей нагрузки [набор доступности](tutorial-availability-sets.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Такая конфигурация гарантирует, что виртуальные машины распределяются по нескольким доменам сбоя, а также развертываются на узлах с разными периодами обслуживания. Полный Hello [соглашения об уровне ОБСЛУЖИВАНИЯ Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/) объясняет hello гарантируется доступность Azure в целом.

### <a name="back-up-hello-vm"></a>Резервное копирование hello виртуальной Машины
Объект [хранилище служб восстановления](../../backup/backup-introduction-to-azure-backup.md) tooprotect используемых данных и средств в службах архивации Azure и Azure Site Recovery. Можно также использовать хранилище служб восстановления[развертывания и управления резервными копиями для развертывания диспетчера ресурсов виртуальных машин с помощью PowerShell](../../backup/backup-azure-vms-automation.md). 

## <a name="next-steps"></a>Дальнейшие действия
* Если вашей целью является toowork с виртуальных машин Linux, посмотрите [Azure и Linux](../linux/overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Дополнительные сведения о hello рекомендации по настройке инфраструктуры в hello [Пошаговое руководство инфраструктуры Azure пример](infrastructure-example.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
