---
title: "aaaUsing имена узлов tooregister динамической DNS"
description: "На этой странице приведены сведения о том, как tooset копирование имена узлов tooregister динамической DNS в DNS-серверы."
services: dns
documentationcenter: na
author: GarethBradshawMSFT
manager: timlt
editor: 
ms.assetid: c315961a-fa33-45cf-82b9-4551e70d32dd
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2017
ms.author: garbrad
ms.openlocfilehash: 8d4b44265714e6976f26bfb3446e8101aa70996a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a>Использование имен узлов tooregister динамической DNS в DNS-сервере
[Azure предоставляет разрешение имен](virtual-networks-name-resolution-for-vms-and-role-instances.md) для виртуальных машин и экземпляров ролей. Однако, если разрешение имен должно выходить за рамки возможностей Azure, вы можете предоставить свои DNS-серверы. Это дает hello power tootailor вашей toosuit решение DNS конкретных целей. Например может потребоваться tooaccess локальным ресурсам через контроллер домена Active Directory.

Когда пользовательские DNS-серверы размещены как ВМ Azure, можно передать имя узла запрашивает hello же имен узлов tooresolve tooAzure виртуальной сети. Если вы не готовы toouse этот маршрут, имена узлов вашей виртуальной Машины можно зарегистрировать в DNS-сервере с помощью динамической DNS.  Azure не имеет toodirectly возможность (например, учетные данные) hello создания записей в DNS-серверы, поэтому часто требуются альтернативные расположения. Ниже приведены некоторые распространенные сценарии и альтернативные варианты.

## <a name="windows-clients"></a>Клиенты Windows
Не входящие в домен клиенты Windows пытаются выполнить небезопасные обновления динамических DNS (DDNS) при загрузке или изменении своего IP-адреса. имя DNS Hello является hello имя узла и основной DNS-суффикс hello. Azure оставляет пустым hello основной DNS-суффикс, но это можно задать в hello виртуальной Машины, через hello [пользовательского интерфейса](https://technet.microsoft.com/library/cc794784.aspx) или [с помощью автоматизации](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).

Присоединенных к домену клиенты Windows зарегистрировать свои IP-адреса контроллера домена hello, используя безопасной динамической DNS. процесс присоединения к домену Hello задает hello основной DNS-суффикс на клиенте hello и создает и поддерживает hello доверительные отношения.

## <a name="linux-clients"></a>Клиенты Linux
Клиенты Linux обычно не регистрирует себя с помощью hello DNS-сервера при запуске, они предполагается, что hello DHCP-сервер работает. DHCP-серверов в Azure имеют способность hello или учетные данные tooregister записей в DNS-сервере.  Можно использовать инструмент, который называется *nsupdate*, входящей в пакет привязки hello, обновляет toosend динамической DNS. Поскольку Стандартизован hello протокол динамической DNS можно использовать *nsupdate* даже если вы не используете Bind на DNS-сервере hello.

Можно использовать обработчики hello, предоставляемые toocreate клиента DHCP hello и поддерживать запись для имени узла hello hello DNS-сервере. Во время цикла DHCP hello, hello клиент выполняет сценарии hello в */etc/dhcp/dhclient-exit-hooks.d/*. Это может быть использовано tooregister hello новый IP-адрес с помощью *nsupdate*. Например:

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on hello primary nic
        if [ "$interface" != "eth0" ]
        then
            return
        fi

        # when we have a new IP, perform nsupdate
        if [ "$reason" = BOUND ] || [ "$reason" = RENEW ] ||
           [ "$reason" = REBIND ] || [ "$reason" = REBOOT ]
        then
            host=`hostname`
            nsupdatecmds=/var/tmp/nsupdatecmds
              echo "update delete $host.$requireddomain a" > $nsupdatecmds
              echo "update add $host.$requireddomain 3600 a $new_ip_address" >> $nsupdatecmds
              echo "send" >> $nsupdatecmds

              nsupdate $nsupdatecmds
        fi

        
        

Можно также использовать hello *nsupdate* tooperform команда обновляет безопасного динамического DNS. Например, при использовании DNS-сервера Bind [создается](http://linux.yyz.us/nsupdate/)пара открытого и закрытого ключей.  DNS-сервер, Hello [настроен](http://linux.yyz.us/dns/ddns-server.html) с hello открытую часть ключа hello, так что он может проверить подпись hello в запросе hello. Необходимо использовать hello *-k* tooprovide параметр hello пары ключей слишком*nsupdate* в порядке для hello динамического обновления DNS подписи toobe запроса.

Если вы используете Windows DNS-сервер, можно использовать проверку подлинности Kerberos с hello *-g* параметр в *nsupdate* (недоступно в версии Windows hello *nsupdate* ). toodo это, используйте *kinit* учетные данные hello tooload (например, из [файла keytab](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)). Затем *nsupdate -g* получат hello учетные данные из кэша hello.

При необходимости можно добавить tooyour суффикс поиска DNS виртуальных машин. Указанный DNS-суффикс Hello в hello */etc/resolv.conf* файла. Большинство дистрибутивы Linux автоматически управлять hello содержимое этого файла, поэтому обычно нельзя редактировать. Тем не менее, суффикс hello можно переопределить с помощью DHCP-клиента hello *заменяет* команды. toodo это в */etc/dhcp/dhclient.conf*, добавить:

        supersede domain-name <required-dns-suffix>;

