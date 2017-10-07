---
title: "aaaViewing и изменение имена узлов | Документы Microsoft"
description: "Как tooview и измените имена узлов для виртуальных машин Azure, веб-ролей и рабочих ролей для разрешения имен"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c668cd8e-4e43-4d05-acc3-db64fa78d828
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 17d0dd7911754a94db3f37b924b4687da1c70aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="viewing-and-modifying-hostnames"></a>Просмотр и изменение имен узлов
tooallow toobe экземпляров вашей роли ссылаться по имени узла, необходимо задать значение hello для имени узла hello в файле конфигурации службы hello для каждой роли. Для этого добавьте toohello имя узла hello требуемого **vmName** атрибут hello **роли** элемента. Здравствуйте, значение hello **vmName** атрибут используется в качестве базы для hello имени узла каждого экземпляра роли. Например если **vmName** — *webrole* существуют три экземпляра этой роли, имена узлов hello hello экземпляров будет *webrole0*, *webrole1* , и *webrole2*. Необязательно toospecify имя узла для виртуальных машин в файле конфигурации hello, так как имя узла hello для виртуальной машины заполняется на основе имени виртуальной машины hello. Дополнительные сведения о настройке службы Microsoft Azure см. в статье, посвященной [схеме конфигурации службы Azure (файл CSCFG)](https://msdn.microsoft.com/library/azure/ee758710.aspx).

## <a name="viewing-hostnames"></a>Просмотр имен узлов
Можно просмотреть hello имена узлов виртуальных машин и экземпляров ролей в облачной службе с помощью приведенных ниже средств hello.

### <a name="azure-portal"></a>Портал Azure
Можно использовать hello [портал Azure](http://portal.azure.com) имена узлов hello tooview для виртуальных машин в колонке Обзор hello для виртуальной машины. Имейте в виду, что hello колонке отображаются значения полей **имя** и **имя узла**. Хотя изначально они hello одинаковые, изменение имени узла hello не изменится имя hello hello виртуальной машины или экземпляра роли.

Экземпляры роли также можно просмотреть в hello портал Azure, но при перечислении экземпляров hello в облачной службе имя узла hello не отображается. Вы увидите имя для каждого экземпляра, но это имя не представляет имя узла hello.

### <a name="service-configuration-file"></a>Файл конфигурации службы
Можно загрузить файл конфигурации службы hello для развернутой службы hello **Настройка** колонке службы hello в hello портал Azure. Затем можно осуществлять поиск hello **vmName** атрибут для hello **имя роли** имя узла элемента toosee hello. Имейте в виду, что это имя узла используется в качестве базы для hello имени узла каждого экземпляра роли. Например если **vmName** — *webrole* существуют три экземпляра этой роли, имена узлов hello hello экземпляров будет *webrole0*, *webrole1* , и *webrole2*.

### <a name="remote-desktop"></a>удаленный рабочий стол;
После включения удаленного рабочего стола (Windows), удаленное взаимодействие Windows PowerShell (Windows) или SSH (Linux и Windows) подключения tooyour виртуальных машин или экземпляров роли, имя узла hello из активного подключения удаленного рабочего стола можно просмотреть различными способами:

* Введите имя узла hello командной строки или терминале SSH.
* Введите ipconfig/все на команду hello запрос (только Windows).
* Имя компьютера hello представления в системе hello параметров (Windows).

### <a name="azure-service-management-rest-api"></a>Интерфейс API REST управления службой Azure
В клиенте REST выполните следующие действия:

1. Убедитесь, что toohello tooconnect сертификат клиента портал Azure. tooobtain сертификат клиента, выполните действия hello, представленных в [как: загрузка и импорт параметров публикации и сведений о подписке](https://msdn.microsoft.com/library/dn385850.aspx). 
2. Задайте запись заголовка с именем x-ms-version и значением 2013-11-01.
3. Отправьте запрос в hello следующий формат: https://management.core.windows.net/\<subscrition идентификатор\>/services/hostedservices/\<имя службы\>? внедрение сведений = true
4. Найдите hello **HostName** для каждого элемента **RoleInstance** элемента.

> [!WARNING]
> Можно также просмотреть суффикс внутреннего домена hello для облачной службы из ответа на вызов REST hello, проверив hello **InternalDnsSuffix** элемент, или запустив команду ipconfig/из командной строки в сеансе удаленного рабочего стола (Windows) или путем выполнения /etc/resolv.conf cat из терминала SSH (Linux).
> 
> 

## <a name="modifying-a-hostname"></a>Изменение имени узла
Hello имя узла для любой виртуальной машины или экземпляра роли можно изменить путем передачи измененный файл конфигурации службы или переименовав компьютер hello из сеанса удаленного рабочего стола.

## <a name="next-steps"></a>Дальнейшие действия
[Разрешение имен (DNS)](virtual-networks-name-resolution-for-vms-and-role-instances.md)

[Схема конфигурации службы Azure (CSCFG-файл)](https://msdn.microsoft.com/library/windowsazure/ee758710.aspx)

[Схема настройки виртуальной сети Azure](http://go.microsoft.com/fwlink/?LinkId=248093)

[Укажите параметры DNS с помощью файлов конфигурации сети](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)

