---
title: "aaaAzure облачные службы ролей часто задаваемые вопросы | Документы Microsoft"
description: "Часто задаваемые вопросы об облачных службах Azure. Ответы на некоторые распространенные вопросы о сертификатах, веб-ролях и рабочих ролях."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a>Часто задаваемые вопросы об облачных службах
В этой статье содержатся ответы на некоторые часто задаваемые вопросы об облачных службах Microsoft Azure. Также можно посетить hello [вопросы и ответы поддержки Azure](http://go.microsoft.com/fwlink/?LinkID=185083) Общие сведения Azure цены и поддержки. Кроме того, можно обратиться к hello [страницы размер виртуальной Машины облачных служб](cloud-services-sizes-specs.md) для сведений о размере.

## <a name="certificates"></a>Сертификаты
### <a name="where-should-i-install-my-certificate"></a>Где следует разместить мой сертификат?
* **My**  
  Сертификаты приложений с закрытым ключом (\*.pfx, \*.p12).
* **CA**  
  — в это хранилище помещаются все промежуточные сертификаты (политики и вложенные ЦС).
* **ROOT**  
  Hello корневого центра сертификации магазина, поэтому следует здесь срок действия вашего сертификата корневого ЦС.

### <a name="i-cant-remove-expired-certificate"></a>Не удается удалить сертификат с истекшим сроком действия
Azure не позволяет удалить сертификат, пока он используется. Необходимо tooeither delete hello, использующего сертификат hello, или обновление hello развертывания с помощью различных или обновленного сертификата.

### <a name="delete-an-expired-certificate"></a>Удаление сертификата с истекшим сроком действия
При условии, что сертификат hello не используется, можно использовать hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) tooremove командлет PowerShell сертификат.

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a>Истек срок действия сертификатов с именем "Службы управления Windows Azure для расширений"
Эти сертификаты создаются каждый раз, когда расширение добавляется toohello облачной службы, например hello расширения удаленного рабочего стола. Эти сертификаты используются только для шифрования и расшифровки hello закрытой конфигурации расширения hello. Не страшно, если срок их действия истечет. Дата окончания срока действия Hello не проверяется.

### <a name="certificates-i-have-deleted-keep-reappearing"></a>Удаленные сертификаты снова появляются
Такое обычно происходит из-за используемых средств, например Visual Studio. Всякий раз при подключении с помощью инструмента, использует сертификат, он будет повторно отправленного tooAzure.

### <a name="my-certificates-keep-disappearing"></a>Мои сертификаты исчезают
При перезапуске экземпляра виртуальной машины hello, все локальные изменения будут потеряны. Используйте [задачи запуска](cloud-services-startup-tasks.md) tooinstall сертификаты toohello виртуальная машина запустится, каждая роль hello времени.

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a>Не удается найти сертификаты управления портала hello
[Сертификаты управления](../azure-api-management-certs.md) доступны только в hello классический портал Azure. Hello текущей версией портала Azure не использует сертификаты управления. 

### <a name="how-can-i-disable-a-management-certificate"></a>Как можно отключить сертификат управления?
[Сертификаты управления](../azure-api-management-certs.md) нельзя отключить. Будут удалены через hello классический портал Azure не их следует использовать toobe.

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a>Как можно создать SSL-сертификат для конкретного IP-адреса?
Следуйте приведенным инструкциям hello hello [создать сертификат Учебник](cloud-services-certs-create.md). Используйте IP-адрес hello как hello DNS-имя.

## <a name="security"></a>Безопасность
### <a name="disable-ssl-30"></a>Отключение SSL 3.0
toodisable SSL 3.0 и использовать средства безопасности TLS, создать задачу запуска, который описан в этой записи блога: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/

### <a name="add-nosniff-tooyour-website"></a>Добавить **nosniff** tooyour веб-сайта
Клиенты tooprevent из сканирование hello типов MIME, добавьте параметр в вашей *web.config* файла.

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

Его можно также добавить как параметр в службах IIS. Используйте следующие hello команды с hello [общие задачи запуска](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) статьи.

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a>Настройка IIS для веб-роли
Используйте сценарий запуска IIS hello из hello [общие задачи запуска](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) статьи.

## <a name="scaling"></a>Масштабирование
### <a name="i-cannot-scale-beyond-x-instances"></a>Не удается выполнить масштабирование на более чем X экземпляров
Подписки Azure имеет ограничение на количество ядер, которые можно использовать в hello. Масштабирование не будет работать при использовании всех доступных ядер hello. Например, если установлено ограничение в 100 ядер, это означает, что в облачной службе можно создать 100 экземпляров виртуальной машины размера A1 или 50 экземпляров виртуальной машины размера A2.

## <a name="networking"></a>Сеть
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>Не удается зарезервировать IP-адрес в облачной службе с несколькими виртуальными IP-адресами
Во-первых убедитесь, что этот экземпляр виртуальной машины hello, который вы пытаетесь tooreserve hello IP-адрес для включен. Во-вторых убедитесь, что вы используете зарезервированных IP-адресов для беспокойства hello промежуточного и рабочего развертываний. **Нет** изменить параметры hello, пока обновление развертывания hello.

## <a name="remote-desktop"></a>Удаленный рабочий стол
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Как использовать удаленный рабочий стол при наличии NSG?
Добавление правила toohello NSG, разрешить трафик через порты **3389** и **20000**.  Удаленный рабочий стол использует порт **3389**.  Экземпляров облачной службы, распределяются, поэтому не может напрямую управлять какой экземпляр tooconnect для.  Hello *RemoteForwarder* и *RemoteAccess* агенты управления трафиком протокола удаленного рабочего СТОЛА и разрешить toosend клиента hello куки-файл протокола удаленного рабочего СТОЛА и tooconnect отдельного экземпляра, чтобы указать.  Hello *RemoteForwarder* и *RemoteAccess* агенты имеют этот порт **20000*** открыть, который может блокироваться, если у вас есть NSG.
