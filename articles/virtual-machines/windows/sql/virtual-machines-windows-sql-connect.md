---
title: "aaaConnect tooa виртуальной машины SQL Server (диспетчер ресурсов) | Документы Microsoft"
description: "Узнайте, как tooconnect tooSQL Server работает на виртуальной машине в Azure. В этом разделе использует hello классической модели развертывания. сценарии Hello отличаться в зависимости от конфигурации сети hello и расположению hello hello клиента."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a>Подключение tooa виртуальной машины SQL Server в Azure (диспетчера ресурсов)
> [!div class="op_single_selector"]
> * [Диспетчер ресурсов](virtual-machines-windows-sql-connect.md)
> * [Классический](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>Обзор

В этом разделе описывается, как tooconnect tooyour SQL Server экземпляр запущен на виртуальной машине Azure. Сначала рассматриваются некоторые [общие сценарии подключения](#connection-scenarios), а затем предоставляются [подробные инструкции по настройке подключений SQL Server на виртуальной машине Azure](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Если вы предпочитаете полное пошаговое руководство по подготовке и подключению, то см. статью [Подготовка виртуальной машины SQL Server на портале Azure](virtual-machines-windows-portal-sql-server-provision.md).

## <a name="connection-scenarios"></a>Сценарии подключения

способ Hello клиент подключается tooSQL сервер, работающий на виртуальной машине отличается в зависимости от расположения hello hello клиента и конфигурации сети hello.

Подготовка к работе виртуальную Машину SQL Server в hello портал Azure, у вас есть параметр hello определения типа hello **подключения SQL**.

![Общедоступное подключение SQL во время подготовки](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

Варианты подключения:

| Параметр | Описание |
|---|---|
| **Общедоступное** | Подключение tooSQL сервера через hello Интернета |
| **Частное** | Подключение tooSQL сервера в hello одной виртуальной сети |
| **Локальное** | Подключение tooSQL Server локально на hello одной виртуальной машине | 

Hello ниже разделы содержат определение hello **открытый** и **закрытый** параметры более подробно.

## <a name="connect-toosql-server-over-hello-internet"></a>Подключение tooSQL сервера через Интернет hello

Tooconnect tooyour SQL Server database engine от hello Интернет, установите **открытый** для hello **подключения SQL** типа hello портала во время инициализации. Hello портал автоматически hello следующие действия:

* Включает hello протокол TCP/IP для SQL Server.
* Настраивает hello tooopen правила брандмауэра SQL Server TCP-порт (по умолчанию 1433).
* включение аутентификации SQL Server, требуемой для предоставления общего доступа;
* Настраивает hello сетевой группы безопасности на hello ВМ tooall TCP-трафика на hello порт SQL Server.

> [!IMPORTANT]
> выпуски Express и Hello образы виртуальных машин для SQL Server Developer Привет автоматически не включайте hello TCP/IP-протокол. В выпусках Developer и Express, необходимо использовать диспетчер конфигурации SQL Server слишком[вручную включить протокол hello TCP/IP](#manualtcp) после создания hello виртуальной Машины.

Любой клиент с доступом в Интернет может подключаться toohello экземпляр SQL Server, указав hello общедоступный IP-адрес виртуальной машины hello или любую метку DNS toothat IP-адресом. Если hello порт SQL Server — 1433, не обязательно toospecify его в строке подключения hello. Привет, следующая строка подключения подключается tooa виртуальной Машине SQL с именем DNS из `sqlvmlabel.eastus.cloudapp.azure.com` с использованием проверки подлинности SQL (можно также использовать hello общедоступный IP-адрес).

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

Несмотря на то, что это позволяет подключения клиентов через Интернет Здравствуйте, это не означает, что любой пользователь может подключиться tooyour SQL Server. Внешним клиентам иметь toohello правильное имя пользователя и пароль. Тем не менее для обеспечения дополнительной безопасности можно избежать hello известный порт 1433. Например если вы настроили toolisten SQL Server для порта 1500 и установленное правильную брандмауэра и правил группы безопасности сети, удалось подключиться путем добавления имени сервера номеров toohello hello порта. Hello следующий пример изменяет предыдущий hello, добавив собственный номер порта, **1500**, toohello имя сервера:

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> При выполнении запроса SQL Server на виртуальной машине через hello Интернета, все данные, исходящие из hello Azure центра обработки данных — тема toonormal [Ценообразование на исходящую передачу данных](https://azure.microsoft.com/pricing/details/data-transfers/).

## <a name="connect-toosql-server-within-a-virtual-network"></a>Подключение tooSQL Server в виртуальной сети

При выборе **закрытый** для hello **подключения SQL** типа hello портала Azure настраивает большая часть параметров hello идентичные слишком**открытый**. Единственным отличием Hello является не tooallow сетевой безопасности группы правил за пределами трафик через порт SQL Server hello (по умолчанию 1433).

> [!IMPORTANT]
> выпуски Express и Hello образы виртуальных машин для SQL Server Developer Привет автоматически не включайте hello TCP/IP-протокол. В выпусках Developer и Express, необходимо использовать диспетчер конфигурации SQL Server слишком[вручную включить протокол hello TCP/IP](#manualtcp) после создания hello виртуальной Машины.

Частное подключение часто используется в сочетании с [виртуальной сетью](../../../virtual-network/virtual-networks-overview.md), что позволяет реализовать несколько сценариев. Можно подключить виртуальные машины в одной виртуальной сети, даже если эти виртуальные машины существует в разных группах ресурсов hello. Если используется [VPN типа «сеть-сеть»](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), можно создать гибридную архитектуру, обеспечивающую подключение виртуальных машин к локальным сетям и компьютерам.

Виртуальные сети включите вы toojoin домена tooa виртуальных машинах Azure. Это hello единственным способом toouse проверку подлинности Windows tooSQL сервера. Hello другие варианты подключения требуется проверка подлинности SQL с именами пользователей и пароли.

Предположим, что вы настроили DNS в виртуальной сети, можно подключиться tooyour экземпляр SQL Server, указав имя компьютера виртуальной Машины SQL Server hello в строке подключения hello. Следующий пример также Hello предполагается, что также настроена проверка подлинности Windows и предоставлены пользователю, hello, экземпляр SQL Server toohello доступа.

```
Server=mysqlvm;Integrated Security=true
```

## <a id="change"></a> Изменение параметров подключения к SQL

Можно изменить параметры подключения к hello для виртуальной машины SQL Server в hello портал Azure.

1. В hello портал Azure, выберите **виртуальные машины**.

2. Выберите виртуальную машину SQL Server.

3. В разделе **Параметры** щелкните **Конфигурация SQL Server**.

4. Изменение hello **уровня подключения SQL** tooyour требуется настройка. При необходимости можно использовать этот hello toochange области порт SQL Server или параметры проверки подлинности SQL hello.

   ![Изменение параметров подключения к SQL](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. Подождите несколько минут для обновления toocomplete hello.

   ![Уведомление об обновлении виртуальной машины SQL](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <a id="manualtcp"></a> Включение TCP/IP для выпусков Developer и Express

При изменении параметров подключения к SQL Server, Azure не происходит автоматического включения hello TCP/IP-протокола для разработчиков SQL Server и выпусках Express. описанные действия Hello, как включить toomanually TCP/IP, чтобы удаленно подключиться по IP-адресу.

Сначала подключите toohello машины SQL Server с помощью удаленного рабочего стола.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

Затем включите протокол hello TCP/IP с **диспетчер конфигурации SQL Server**.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a>Подключение с помощью SSMS

Hello следующее Показать, как toocreate необязательно DNS метка для ВМ Azure и подключитесь с помощью SQL Server Management Studio (SSMS).

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a>Дальнейшие действия

инструкции подготовки toosee вместе с следующее подключение. в разделе [подготовки виртуальной машины SQL Server в Azure](virtual-machines-windows-portal-sql-server-provision.md).

Другие разделы, посвященные toorunning SQL Server в виртуальных машинах Azure, см. в разделе [SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-server-iaas-overview.md).
