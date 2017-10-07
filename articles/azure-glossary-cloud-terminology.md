---
title: "Глоссарий aaaAzure - словаря Azure | Документы Microsoft"
description: "Используйте toounderstand облака hello Azure глоссарий терминов hello платформы Azure. Краткий словарь Azure, содержащий определения основных терминов по облакам в Azure."
keywords: "словарь Azure, облачная терминология, словарь терминов Azure, определения терминов, облачные термины"
services: na
documentationcenter: na
author: MonicaRush
manager: jhubbard
editor: 
ms.assetid: d7ac12f7-24b5-4bcd-9e4d-3d76fbd8d297
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: monicar
ms.openlocfilehash: 486bbbfc71a48a6ebc39b14f7ab71f8604b7a6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-glossary-a-dictionary-of-cloud-terminology-on-hello-azure-platform"></a>Глоссарий для Microsoft Azure: словарь терминов облака на платформе Azure hello

Глоссарий Hello Microsoft Azure — это короткие словарь облачной терминологии для hello платформы Azure. См. также:

* [Microsoft Azure и веб-службы Amazon](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/) — определения служб Azure и их аналогов в AWS.<!-- I propose toolink toohttps://azure.microsoft.com/en-us/services/ instead of this -->
* [Термины облачных вычислений](https://azure.microsoft.com/overview/cloud-computing-dictionary/) — общие термины облачной индустрии.

## <a name="account"></a>учетная запись
Учетная запись использовала tooaccess, управлять подпиской Azure. Он часто называют учетной записи Azure, несмотря на то, что учетная запись может быть любой из этих tooas: существующую рабочую, учебный или личной учетной записи Майкрософт, или Office 365 имя пользователя и пароль. Можно также создать toomanage учетной записи подписки Azure при регистрации для hello [бесплатной пробной версии](https://azure.microsoft.com).  
В разделе [зарегистрироваться для получения подписки Azure с учетной записью Office 365](billing/billing-use-existing-office-365-account-azure-subscription.md) и [учетные записи, можно использовать toosign в](active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="api-app"></a>Приложение API
Другое название [приложения службы приложений](#app-service-app).

## <a name="app-service-app"></a>Приложение службы приложений
Здравствуйте, вычислительные ресурсы, [службе приложений Azure](app-service/app-service-value-prop-what-is.md) предоставляет для размещения [веб-сайта или веб-приложения](app-service-web/app-service-web-overview.md), [веб-API](app-service-api/app-service-api-apps-why-best-platform.md), или [внутреннего сервера мобильного приложения](app-service-mobile/app-service-mobile-value-prop.md). Приложения служб приложений, также назывались tooas *службы приложений*, *веб-приложений*, *приложения API*, и *мобильных приложений*.

## <a name="availability-set"></a>группа доступности
Коллекции виртуальных машин, управляемых вместе tooprovide приложения избыточность и надежность. Использование Hello группу доступности гарантирует, что во время любого запланированного или незапланированного обслуживания события доступен по крайней мере одну виртуальную машину.  
В разделе [управлять доступностью виртуальных машин Windows hello](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) и [управлять доступностью hello виртуальных машин Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="classic-model"></a>классическая модель развертывания Azure
Одним из двух [модели развертывания](resource-manager-deployment-model.md) используемых ресурсов toodeploy в Azure (hello новой модели — диспетчера ресурсов Azure). Некоторые службы Azure поддерживают только модель развертывания диспетчера ресурсов hello, некоторые поддерживают только hello классической модели развертывания, а некоторые оба. Hello документации для каждой службы Azure указывает, какие модели, они поддерживают.

## <a name="cli"></a>интерфейс командной строки Azure (CLI)
Интерфейс командной строки, который можно использовать toomanage службы Azure из Windows, macOS и Linux.  Некоторые службы и функции службы можно управлять только через PowerShell или hello CLI. См. статью [Azure CLI 2.0](/cli/azure/overview).

## <a name="powershell"></a>Azure PowerShell
Toomanage интерфейс командной строки служб Azure через командную строку с компьютеров Windows. Некоторые службы и функции службы можно управлять только через PowerShell или hello CLI.
В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview)

## <a name="arm-model"></a>модель развертывания с помощью Azure Resource Manager
Одним из двух [модели развертывания](resource-manager-deployment-model.md) используемых ресурсов toodeploy в Microsoft Azure (hello других — hello классической модели развертывания). Некоторые службы Azure поддерживают только модель развертывания диспетчера ресурсов hello, некоторые поддерживают только hello классической модели развертывания, а некоторые оба. Hello документации для каждой службы Azure указывает, какие модели, они поддерживают.

## <a name="fault-domain"></a>домен сбоя
Здравствуйте коллекции виртуальных машин в наборе доступности, возможно не выполняются в hello же время. Примером может послужить группа установленных в стойку машин с общим источником питания и сетевым коммутатором. В Azure hello виртуальные машины в наборе доступности автоматически разделены по разным доменам отказоустойчивости.  
В разделе [управлять доступностью виртуальных машин Windows hello](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) или [управлять доступностью hello виртуальных машин Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)  

## <a name="geo"></a>геообъект
Определенная граница для резидентства данных, которое обычно включает два или несколько регионов. Hello границы может быть внутри или за пределами границ государств и влияют стабилизации налога. Каждый геообъект включает как минимум один регион. Примеры геообъектов: Азиатско-Тихоокеанский регион и Япония. Еще одно название — *география*.  
См. статью [Регионы Azure](best-practices-availability-paired-regions.md).

## <a name="geo-replication"></a>георепликация
процесс автоматически реплицировать данные больших двоичных объектов, таблиц и очередей в паре региональные Hello.  
См. статью [Активная георепликация для базы данных SQL Azure](sql-database/sql-database-geo-replication-overview.md).
<!-- hello meaning of "geo" in this term seems toobe different than hello meaning provided in hello "geo" entry -->

## <a name="image"></a>изображение
Файл, содержащий hello операционной системы и конфигурации приложения, который можно использовать toocreate любое количество виртуальных машин. В Azure можно использовать два типа образов — образ виртуальной машины и образ ОС. Образ ВМ содержит операционную систему и все диски подключены tooa виртуальной машины при создании образа hello. Образ ОС содержит только общие сведения об операционной системе и не включает конфигурации дисков данных.  
В разделе [перейдите и выберите образы виртуальных машин Windows в Azure с помощью PowerShell или hello CLI](virtual-machines/windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="limits"></a>ограничения
количество ресурсов, которые могут быть созданы или hello тестирования производительности, которую можно достичь Hello. Ограничения обычно связаны с подписками, службами и предложениями.  
См. статью [Подписка Azure, границы, квоты и ограничения службы](azure-subscription-service-limits.md).

## <a name="load-balancer"></a>подсистема балансировки нагрузки
Ресурс, который распределяет входящий трафик между компьютерами в сети. В Azure подсистемы балансировки нагрузки распределяет трафик toovirtual машины, определенным в наборе балансировки нагрузки. [Балансировщик нагрузки](load-balancer/load-balancer-overview.md) может быть внутренним или с выходом в Интернет.  

## <a name="mobile-app"></a>мобильное приложение
Другое название [приложения службы приложений](#app-service-app).

## <a name="offer"></a>offer
Здравствуйте, цены, кредиты и связанных терминов применимо tooan подписки Azure.  
В разделе hello [страница сведений о предложение Azure](https://azure.microsoft.com/support/legal/offer-details/)

## <a name="portal"></a>портал
Hello безопасных веб-портала используется toodeploy и управления службами Azure.  Существует два портала: hello [портал Azure](http://portal.azure.com/) и hello [классический портал](http://manage.windowsazure.com/). Некоторые службы доступны в обоих порталов, тогда как другие доступны только в одном или другом hello. Hello [диаграммы доступности Azure портала](https://azure.microsoft.com/features/azure-portal/availability/) списки, доступные в портала службы.

## <a name="region"></a>region
Область геообъекта, не пересекающая национальные границы и содержащая один или несколько центров обработки данных. Цены, региональные службы и типы предложений, предоставляются на уровне области hello. Область обычно связана с другой области, который может быть вверх tooseveral сотни километров от. Пары регионов можно использовать как механизм для аварийного восстановления и сценариев высокой доступности. Также называется tooas *расположение*.  
См. статью [Регионы Azure](best-practices-availability-paired-regions.md).

## <a name="resource"></a>resource
Элемент, который является частью решения Azure. Каждая служба Azure позволяет toodeploy различных типов ресурсов, таких как базы данных или виртуальные машины.   
См. статью [Общие сведения о диспетчере ресурсов Azure](azure-resource-manager/resource-group-overview.md).

## <a name="resource-group"></a>resource group
Контейнер в диспетчере ресурсов, содержащий связанные ресурсы для приложения. Hello группы ресурсов может включать все ресурсы приложения hello, или только те ресурсы, которые логически сгруппированы. Можно решить, как ресурсы tooallocate группы tooresource основаны на то, что hello больше смысла для вашей организации.  
См. статью [Общие сведения о диспетчере ресурсов Azure](azure-resource-manager/resource-group-overview.md).

## <a name="arm-template"></a>шаблон Resource Manager
Файл JSON, декларативно определяет один или несколько ресурсов Azure и который определяет зависимости между hello развернуты ресурсы. Hello шаблон может быть используется toodeploy hello ресурсы, постоянно и многократно.  
См. статью [Создание шаблонов диспетчера ресурсов Azure](resource-group-authoring-templates.md).

## <a name="resource-provider"></a>поставщик ресурсов
Служба, предоставляющая hello ресурсы можно развернуть и управлять ими через диспетчер ресурсов. Каждый поставщик ресурсов предоставляет операции для работы с ресурсами hello, которые развертываются. Поставщики ресурсов может осуществляться через hello портал Azure, Azure PowerShell и нескольких пакетах SDK программирования.  
См. статью [Общие сведения о диспетчере ресурсов Azure](azure-resource-manager/resource-group-overview.md).

## <a name="role"></a>role
Средства для управления доступом, которое может быть назначено toousers, групп и служб. Роли, может tooperform действия, такие как создание, управление и чтения в ресурсах Azure.  
См. статью [RBAC: встроенные роли](active-directory/role-based-access-built-in-roles.md).

## <a name="sla"></a>соглашение об уровне обслуживания (SLA)
Hello соглашение, описывающее обязательства корпорации Майкрософт для подключения к и время работы. В каждой службе Azure есть отдельный SLA.  
См. статью [Соглашения об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/).

## <a name="sas"></a>подписанный URL-адрес (SAS)
Цифровую подпись, которая позволяет toogrant ограниченный доступ tooa ресурсов, без предоставления ключа учетной записи. Например [хранилище Azure использует SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) tooobjects toogrant клиента доступа, таких как большие двоичные объекты. [Центр IoT использует SAS](iot-hub/iot-hub-devguide-security.md#security-tokens) toogrant устройств разрешение toosend телеметрии.

## <a name="storage-account"></a>запись хранения Azure
Учетную запись, которая позволяет получить доступ к службам больших двоичных объектов Azure, очереди, таблицы и файла toohello в хранилище Azure. Имя учетной записи хранения Hello определяет hello уникальное пространство имен для объектов данных в хранилище Azure.  
См. статью [Об учетных записях хранения Azure](storage/common/storage-create-storage-account.md).

## <a name="subscription"></a>Подписка
Клиента соглашения с корпорацией Майкрософт, который позволяет им tooobtain Azure службы. Расценки подписки Hello и связанные условия управляются предложение hello, выбранного для подписки hello.
См. [Соглашение о подписке Microsoft Online](https://azure.microsoft.com/support/legal/subscription-agreement/) и статью [Связь между подписками Azure и службой Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="tag"></a>tag
Индексирования термин, который позволяет toocategorize ресурсы в соответствии с tooyour требования к управлению или выставления счетов. При наличии сложных коллекцию ресурсов, можно использовать теги toovisualize эти ресурсы hello способом, который больше смысла hello. Например, можно снабдить тегами ресурсы, которые выполняют ту же роль в организации или принадлежат toohello же отдела.  
В разделе [Using теги tooorganize ресурсами Azure](resource-group-using-tags.md)

## <a name="update-domain"></a>домен обновления
Здравствуйте, Коллекция виртуальных машин в наборе доступности, обновляемых hello то же время. Виртуальные машины в hello в одном домене обновления перезапускаются вместе во время планового обслуживания. Azure не перезапускает больше одного домена обновления за один раз. Также называется tooas домена обновления.  
В разделе [управлять доступностью виртуальных машин Windows hello](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) и [управлять доступностью hello виртуальных машин Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vm"></a>виртуальная машина
Программная реализация Hello физическом компьютере с операционной системой. Несколько виртуальных машин можно запустить одновременно в hello такое же оборудование. В Azure виртуальные машины могут быть разных размеров.  
См. [документацию по виртуальным машинам](https://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="vm-extension"></a>расширение виртуальной машины
Ресурс, который реализует поведение или функции, которые либо помогают другие программы работать или обеспечивать возможность hello toointeract с работающего компьютера. Например можно использовать tooreset расширения доступа к ВМ hello или изменения значений удаленного доступа на виртуальной машине Azure.
<!-- This definition seems obscure toome; maybe a list of examples would work better than a conceptual definition? -->
См. статью [Обзор расширений и компонентов виртуальной машины под управлением Windows](virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) или [Обзор расширений и компонентов виртуальных машин под управлением Linux](virtual-machines/linux/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vnet"></a>виртуальная сеть
Сеть, обеспечивающая соединение между ресурсами Azure и изолированная от всех клиентов Azure. С помощью [VPN-шлюза Azure](vpn-gateway/vpn-gateway-about-vpngateways.md) ее можно подключить к другой виртуальной сети, а также к [локальной сети](vpn-gateway/vpn-gateway-plan-design.md). Кроме того, можно полностью настраивать hello блоки IP-адресов, параметры DNS, политики безопасности и таблицы маршрутов в виртуальной сети.  
См. статью [Виртуальная сеть Azure](virtual-network/virtual-networks-overview.md).  

## <a name="web-app"></a>Веб-приложение
Другое название [приложения службы приложений](#app-service-app).

## <a name="see-also"></a>См. также

* [Приступая к работе с Azure](https://azure.microsoft.com/get-started/)
* [Центр облачных ресурсов](https://azure.microsoft.com/resources/)  
* [Azure для бизнес-приложений](https://azure.microsoft.com/overview/business-apps-on-azure/)
* [Azure в вашем центре обработки данных](https://azure.microsoft.com/overview/business-apps-on-azure/)

