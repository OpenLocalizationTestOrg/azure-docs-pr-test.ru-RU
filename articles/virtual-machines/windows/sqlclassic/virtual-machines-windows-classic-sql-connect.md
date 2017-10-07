---
title: "aaaConnect tooa виртуальной машины SQL Server в Azure (классические) | Документы Microsoft"
description: "Узнайте, как tooconnect tooSQL Server работает на виртуальной машине в Azure. В этом разделе использует hello классической модели развертывания. сценарии Hello отличаться в зависимости от конфигурации сети hello и расположению hello hello клиента."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: 416948af-454f-4cfe-8fd2-7cf971cbd3e9
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: jroth
experimental_id: d51f3cc6-753b-4e
ms.openlocfilehash: 4fff3936ad0bcfd3a56855a8436991e19b92522b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-classic-deployment"></a>Подключение tooa виртуальной машины SQL Server в Azure (классические развертывание)
> [!div class="op_single_selector"]
> * [Диспетчер ресурсов](../sql/virtual-machines-windows-sql-connect.md)
> * [Классический](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>Обзор
В этом разделе описывается, как tooconnect tooyour SQL Server экземпляр запущен на виртуальной машине Azure. Сначала рассматриваются некоторые [общие сценарии подключения](#connection-scenarios), а затем предоставляются [подробные инструкции по настройке подключений SQL Server на виртуальной машине Azure](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. При использовании виртуальных машин диспетчера ресурсов. в разделе [подключения виртуальной машины SQL Server в Azure с помощью диспетчера ресурсов tooa](../sql/virtual-machines-windows-sql-connect.md).

## <a name="connection-scenarios"></a>Сценарии подключения
способ Hello клиент подключается tooSQL сервер, работающий на виртуальной машине отличается в зависимости от расположения hello hello клиента и конфигурации hello машины в сети. Ниже приведены соответствующие сценарии.

* [Подключение сервера tooSQL в hello же облачной службе](#connect-to-sql-server-in-the-same-cloud-service)
* [Подключение tooSQL сервера через hello Интернета](#connect-to-sql-server-over-the-internet)
* [Подключение tooSQL сервера в hello одной виртуальной сети](#connect-to-sql-server-in-the-same-virtual-network)

> [!NOTE]
> Перед подключением с любого из этих методов необходимо соблюдать hello [шаги в этой статье tooconfigure подключения](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).
> 
> 

### <a name="connect-toosql-server-in-hello-same-cloud-service"></a>Подключение сервера tooSQL в hello же облачной службе
Несколько виртуальных машин могут создаваться в hello же облачной службе. toounderstand эту виртуальную машины сценарии, в разделе [как tooconnect виртуальных машин с помощью виртуальной сети или облачной службы](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service). Этот сценарий является при работы Server tooSQL tooconnect попыток клиента на одну виртуальную машину на другой виртуальной машины в hello же облачной службе.

В этом сценарии можно подключиться при помощи hello ВМ **имя** (также показано, как **имя компьютера** или **hostname** hello портале). Это имя hello, заданное для hello виртуальной Машины во время создания. Например, если имя виртуальной Машины SQL **mysqlvm**, клиент ВМ в одной облачной службе может использовать hello hello следующие tooconnect строка подключения:

    "Server=mysqlvm;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

### <a name="connect-toosql-server-over-hello-internet"></a>Подключение tooSQL сервера через Интернет hello
Tooconnect tooyour SQL Server database engine от hello Интернета, создать конечную точку виртуальной машины для входящей связи TCP. Этот шаг настройки Azure направляет входящий TCP порт трафика tooa TCP-порт, доступный toohello виртуальной машины.

Здравствуйте, tooconnect через Интернет, должны использовать hello ВМ DNS имя и hello ВМ конечную точку номер порта (настроен далее в этой статье). hello toofind DNS-имя перейдите toohello Azure портала и выберите **виртуальные машины (классические)**. Затем выберите свою виртуальную машину. Hello **DNS-имя** отображается в hello **Обзор** раздела.

Например, рассмотрим классическую виртуальную машину **mysqlvm** с DNS-именем **mysqlvm7777.cloudapp.net** и конечной точкой **57500**. При условии, что правильно настроенного подключения, hello, следующая строка подключения может быть используется tooaccess hello виртуальной машины из любого места на hello Интернета:

    "Server=mycloudservice.cloudapp.net,57500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

Несмотря на то, что это позволяет подключения клиентов через Интернет Здравствуйте, это не означает, что любой пользователь может подключиться tooyour SQL Server. Внешним клиентам иметь toohello правильное имя пользователя и пароль. Для обеспечения дополнительной безопасности не используют hello известный порт 1433 для hello общей конечной точки виртуальной машины. И, если это возможно, рассмотрите возможность добавления ACL на клиентах только toohello toorestrict трафика конечной точки, чтобы разрешить. Инструкции по использованию списков ACL с конечными точками, см. в разделе [управление hello ACL в конечной точке](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

> [!NOTE]
> Важно toonote, что при использовании этого метода toocommunicate с SQL Server, все данные, исходящие из hello центра обработки данных Azure субъекта toonormal [Ценообразование на исходящую передачу данных](https://azure.microsoft.com/pricing/details/data-transfers/).
> 
> 

### <a name="connect-toosql-server-in-hello-same-virtual-network"></a>Подключение tooSQL сервера в hello одной виртуальной сети
[Виртуальная сеть](../../../virtual-network/virtual-networks-overview.md) поддерживает дополнительные сценарии. Можно подключить виртуальные машины в одной виртуальной сети, даже если эти виртуальные машины существуют в разных облачных службах hello. Если используется [VPN типа «сеть-сеть»](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), можно создать гибридную архитектуру, обеспечивающую подключение виртуальных машин к локальным сетям и компьютерам.

Виртуальных сетей также позволяет вам toojoin домена tooa виртуальных машинах Azure. Это hello единственным способом toouse проверку подлинности Windows tooSQL сервера. Hello другие варианты подключения требуется проверка подлинности SQL с именами пользователей и пароли.

Будет tooconfigure среде домена и проверки подлинности Windows, не обязательно toouse hello шаги в данном tooconfigure статье hello общедоступную конечную точку или hello проверки подлинности SQL и имена входа. В этом сценарии можно подключиться tooyour экземпляр SQL Server, указав имя виртуальной Машины SQL Server hello в строке подключения hello. Следующий пример Hello предполагается, что также настроена проверка подлинности Windows и предоставлены пользователю, hello, экземпляр SQL Server toohello доступа.

    "Server=mysqlvm;Integrated Security=true"

## <a name="steps-for-configuring-sql-server-connectivity-in-an-azure-vm"></a>Действия по настройке подключения к SQL Server на виртуальной машине Azure
Привет, следующие шаги показывают, как экземпляр SQL Server toohello tooconnect над hello Интернет с помощью SQL Server Management Studio (SSMS). Однако hello же действия относятся toomaking вашей виртуальной машины SQL Server, доступных для ваших приложений под управлением как локально, так и в Azure.

Перед подключение toohello экземпляр SQL Server из другой виртуальной Машиной или hello Интернета, необходимо выполнить hello, выполнив задачи, описанные в последующих разделах hello.

* [Создайте конечную точку TCP для виртуальной машины hello](#create-a-tcp-endpoint-for-the-virtual-machine)
* [Откройте TCP-порты в брандмауэре Windows hello](#open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine)
* [Настройка SQL Server toolisten на hello протокола TCP](#configure-sql-server-to-listen-on-the-tcp-protocol)
* [Настройка SQL Server для аутентификации в смешанном режиме](#configure-sql-server-for-mixed-mode-authentication)
* [Создание имен входа для аутентификации SQL Server](#create-sql-server-authentication-logins)
* [Определите DNS-имя виртуальной машины hello hello](#determine-the-dns-name-of-the-virtual-machine)
* [Подключения toohello компонент Database Engine с другого компьютера](#connect-to-the-database-engine-from-another-computer)

путь подключения Hello сформирована hello, следующая схема:

![Подключение виртуальной машины SQL Server tooa](../../../../includes/media/virtual-machines-sql-server-connection-steps/SQLServerinVMConnectionMap.png)

[!INCLUDE [Connect tooSQL Server in a VM Classic TCP Endpoint](../../../../includes/virtual-machines-sql-server-connection-steps-classic-tcp-endpoint.md)]

[!INCLUDE [Connect tooSQL Server in a VM](../../../../includes/virtual-machines-sql-server-connection-steps.md)]

[!INCLUDE [Connect tooSQL Server in a VM Classic Steps](../../../../includes/virtual-machines-sql-server-connection-steps-classic.md)]

## <a name="next-steps"></a>Дальнейшие действия
Если планируется использовать toouse группы доступности AlwaysOn для высокой доступности и аварийного восстановления, вы должны учитывать при реализации прослушивателя. Базы данных клиенты подключаются toohello прослушивателя, а не непосредственно tooone hello экземпляров SQL Server. Hello прослушивателя маршруты клиентов toohello первичной реплики в группе доступности hello. Дополнительные сведения см. в статье [Настройка прослушивателя внутренней подсистемы балансировки нагрузки для группы доступности AlwaysOn в Azure](../classic/ps-sql-int-listener.md).

Это важные tooreview все hello безопасности советы и рекомендации по SQL Server на виртуальной машине Azure. Дополнительные сведения см. в статье [Вопросы безопасности SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-sql-security.md).

[Просмотр hello план обучения](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) для SQL Server на виртуальных машинах Azure. 

Другие разделы, посвященные toorunning SQL Server в виртуальных машинах Azure, см. в разделе [SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

