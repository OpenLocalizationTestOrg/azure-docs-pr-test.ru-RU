---
title: "aaaSecurity рекомендации по SQL Server в Azure | Документы Microsoft"
description: "В этом разделе приведены общие указания по обеспечению безопасности сервера SQL Server, работающего на виртуальной машине Azure."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: d710c296-e490-43e7-8ca9-8932586b71da
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/02/2017
ms.author: jroth
ms.openlocfilehash: 14c3d828fa87446da67beea6d28886de254afe15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-sql-server-in-azure-virtual-machines"></a>Вопросы безопасности SQL Server на виртуальных машинах Azure

Этот раздел содержит общие рекомендации по безопасности, которые помогут обеспечить экземпляров сервера tooSQL безопасного доступа в Azure виртуальной машины (VM).

Azure соответствует ряду отраслевых норм и стандартов, которые можно одновременно toobuild решении совместимые с SQL Server, запущенный на виртуальной машине. Сведения о соответствии нормам Azure см. в [центре управления безопасностью Azure](https://azure.microsoft.com/support/trust-center/).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="control-access-toohello-sql-vm"></a>Элемент управления доступа toohello виртуальной Машины SQL

При создании виртуальной машины SQL Server, необходимо учитывайте как toocarefully контролировать, кто имеет доступ toohello компьютера и tooSQL сервера. Как правило, вам следует hello следующее:

- Ограничьте доступ tooSQL серверных tooonly hello приложений и клиентов, которым она необходима.
- придерживаться рекомендаций по управлению учетными записями пользователей и паролями.

Hello в следующих разделах предоставляют подсказки на анализ через эти точки.

## <a name="secure-connections"></a>Защита подключений

При создании виртуальной машины с SQL Server с помощью образа коллекции hello **связи SQL Server** параметр дает hello Выбор **локальной (в виртуальной Машине)**, **закрытый (в виртуальной сети)** , или **общей (Интернет)**.

![Подключение к серверу SQL Server](./media/virtual-machines-windows-sql-security/sql-vm-connectivity-option.png)

В целях повышения безопасности hello вариант hello наиболее строгие для вашего сценария. Например, при запуске приложения, которое работает на SQL Server hello одной виртуальной Машины, затем **локального** наиболее безопасный вариант hello. При запуске приложения Azure, требуется доступ toohello SQL Server, то **закрытый** защищает tooSQL связи сервера только в пределах указанного hello [виртуальной сети Azure](../../../virtual-network/virtual-networks-overview.md). Если требуется **открытый** toohello (internest) доступа к виртуальной Машине SQL Server, затем убедитесь, что toofollow других рекомендаций в этой статье tooreduce контактную зону.

Hello выбранные параметры на портале hello использовать правила безопасности для входящего трафика на виртуальные машины hello [сетевой группы безопасности](../../../virtual-network/virtual-networks-nsg.md) tooallow (NSG) или запрещать сетевой трафик tooyour виртуальной машины. Можно изменить или создать новые правила для входящих подключений NSG порт SQL Server toohello tooallow трафика (по умолчанию 1433). Можно также указать конкретные IP-адреса, разрешенные toocommunicate через этот порт.

![Правила группы безопасности сети](./media/virtual-machines-windows-sql-security/sql-vm-network-security-group-rules.png)

В дополнение к этому tooNSG правила toorestrict сетевого трафика, можно также использовать hello брандмауэра Windows на виртуальной машине hello.

При использовании конечных точек с hello классической модели развертывания удалите конечные точки на виртуальной машине hello, если они не используются. Инструкции по использованию списков ACL с конечными точками, см. в разделе [управление hello ACL в конечной точке](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint). Это не требуется для виртуальных машин, использующих hello диспетчера ресурсов.

Наконец можно включить зашифрованные соединения для экземпляра hello hello SQL Server Database Engine в виртуальной машине Azure. Настройте новый экземпляр SQL Server с подписанным сертификатом. Дополнительные сведения см. в разделе [toohello Включение шифрования соединений СУБД](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine) и [синтаксис строки соединения](https://msdn.microsoft.com/library/ms254500.aspx).

## <a name="use-a-non-default-port"></a>Использование нестандартного порта

По умолчанию сервер SQL Server ожидает передачи данных через стандартный порт 1433. Для повышения безопасности следует настройте toolisten SQL Server на нестандартный порт, например 1401. Если вы подготовить образ SQL Server коллекции в hello портал Azure, можно указать этот порт в hello **параметры SQL Server** колонку.

tooconfigure этот после подготовки, у вас есть два варианта:

- Для виртуальных машин диспетчера ресурсов, можно выбрать **конфигурации SQL Server** из колонки Обзор hello виртуальной Машины. Это позволяет toochange hello порта.

  ![Изменение TCP-порта на портале](./media/virtual-machines-windows-sql-security/sql-vm-change-tcp-port.png)

- Для классических виртуальных машин или виртуальные машины SQL Server, не были подготовлены при помощи портала hello можно вручную настроить порт hello посредством удаленного подключения toohello виртуальной Машины. Действия по настройке hello, см. [Настройка tooListen сервера определенного порта TCP](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port). Если вы используете этот способ вручную, необходимо также tooadd брандмауэра Windows правило tooallow входящий трафик на TCP-порта.

> [!IMPORTANT]
> Указание порта не по умолчанию имеет смысл, если порт SQL Server откройте toopublic подключения к Интернету.

Если SQL Server прослушивает порт не по умолчанию, необходимо указать hello порт при подключении. Например, рассмотрим сценарий, где 13.55.255.255 IP-адрес сервера hello и SQL Server прослушивает порт 1401. tooSQL tooconnect сервера, следует указать `13.55.255.255,1401` в строке подключения hello.

## <a name="manage-accounts"></a>Управление учетными записями

Вы не хотите злоумышленники tooeasily предположением счета имена и пароли. Используйте следующие советы toohelp hello.

- Создайте уникальную локальную учетную запись администратора с именем, отличным от **Administrator**.

- Используйте сложные надежные пароли для всех учетных записей. Дополнительные сведения о том, как toocreate надежный пароль. в разделе [создать надежный пароль](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password) статьи.

- По умолчанию во время настройки виртуальной машины SQL Server в Azure выбирается проверка подлинности Windows. Здравствуйте, поэтому **SA** входа будет отключена, а пароль присваивается программой установки. Мы рекомендуем, hello **SA** входа не следует использовать или включена. Если необходимо иметь учетные данные SQL, воспользуйтесь одним из следующих стратегий hello:

  - Создайте учетную запись SQL с уникальным именем, являющуюся участником роли **sysadmin**. Включив это можно сделать через портал hello **проверки подлинности SQL** во время инициализации.

    > [!TIP] 
    > Если не включить проверку подлинности SQL во время подготовки, необходимо вручную изменить режим проверки подлинности hello слишком**SQL Server и режим проверки подлинности Windows**. Дополнительные сведения см. в статье [Изменение режима проверки подлинности сервера](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode).

  - Если необходимо использовать hello **SA** входа, входа hello enable после подготовки и назначить новый надежный пароль.

## <a name="follow-on-premises-best-practices"></a>Рекомендации по локальной среде

Кроме toohello и рекомендации, описанные в этом разделе, рекомендуется изучить и реализовать рекомендации по обеспечению безопасности в локальном hello, где это возможно. Дополнительные сведения см. в статье [Вопросы безопасности при установке SQL Server](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation).

## <a name="next-steps"></a>Дальнейшие действия

Если вам также интересны рекомендации по повышению производительности, ознакомьтесь со статьей [Рекомендации по оптимизации производительности SQL Server в виртуальных машинах Azure](virtual-machines-windows-sql-performance.md).

Другие разделы, посвященные toorunning SQL Server в виртуальных машинах Azure, см. в разделе [SQL Server на виртуальных машинах Azure Обзор](virtual-machines-windows-sql-server-iaas-overview.md).

