---
title: "Создание и экспорт сертификатов для подключений типа \"точка — сеть\" в Azure с помощью MakeCert | Документация Майкрософт"
description: "В этой статье содержатся действия toocreate самозаверяющий корневой сертификат, экспортируйте открытый ключ hello и создания сертификатов клиента с помощью средства MakeCert."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 0b795ccf74f1f97fbd3de8a0dc339f9cb0b48183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-makecert"></a>Создание и экспорт сертификатов для подключений типа "точка — сеть" с помощью MakeCert

Точка-сеть соединения используют tooauthenticate сертификаты. В этой статье показано, как toocreate a самозаверяющий корневой сертификат и создания сертификатов клиента с помощью средства MakeCert. Если вам нужны дополнительные действия по настройке точки сайтами, таких как как список tooupload корневые сертификаты, выберите один из статей hello "Настройка точка-сеть" из hello следующие:

> [!div class="op_single_selector"]
> * [Создание самозаверяющих сертификатов с помощью PowerShell](vpn-gateway-certificates-point-to-site.md)
> * [Создание и экспорт сертификатов для подключений типа "точка — сеть" с помощью MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Настройка подключения "точка — сеть" модели Resource Manager на портале Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [Настройка подключения "точка-сеть" — Resource Manager — PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Настройка подключения "точка —сеть" классической модели на портале Azure](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 

Хотя мы рекомендуем использовать hello [действия Windows 10 PowerShell](vpn-gateway-certificates-point-to-site.md) toocreate сертификаты, мы предоставляем эти инструкции MakeCert необязательный метод. Hello сертификаты, создаваемые с помощью любого метода, которые можно установить на [любых поддерживаемых клиентских операционных систем](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq). Однако MakeCert имеет следующие ограничения hello.

* Мы не рекомендуем использовать MakeCert. Это значит, что средство может быть удалено в любой момент. Если MakeCert больше недоступен, это никак не повлияет на сертификаты, созданные с помощью этого средства. MakeCert не только сертификаты используется toogenerate hello как механизм проверки.

## <a name="rootcert"></a>Создание самозаверяющего корневого сертификата

Привет, следующие шаги показывают, как toocreate a самозаверяющий сертификат с помощью средства MakeCert. Они не зависят от модели развертывания. Они подходят как для модели с использованием диспетчера ресурсов, так и для классической модели.

1. Скачайте и установите [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx).
2. После установки, обычно можно найти служебной программы makecert.exe hello в этом пути: "C:\Program Files (x86) \Windows Kits\10\bin\<arch >". Однако это возможно, было установленных tooanother расположение. Откройте командную строку от имени администратора и перейдите в расположение toohello hello программа MakeCert. Можно использовать hello следующий пример, настраивая для соответствующего местоположения hello.

  ```cmd
  cd C:\Program Files (x86)\Windows Kits\10\bin\x64
  ```
3. Создайте и установите сертификат в хранилище личных сертификатов hello на вашем компьютере. Hello следующий пример создает соответствующий *.cer* отправить tooAzure при настройке P2S файла. Замените имя hello требуется toouse для сертификата hello «P2SRootCert» и «P2SRootCert.cer». Hello сертификат находится в «Сертификаты — текущий пользователь\личные\сертификаты».

  ```cmd
  makecert -sky exchange -r -n "CN=P2SRootCert" -pe -a sha256 -len 2048 -ss My
  ```

## <a name="cer"></a>Экспорт hello открытого ключа (CER)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

Hello exported.cer файл должен быть загруженного tooAzure. Дополнительные сведения см. в разделе [Подготовка CER-файла корневого сертификата к передаче](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile). tooadd дополнительных доверенный корневой сертификат в разделе [в этом разделе](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add) hello статьи.

### <a name="export-hello-self-signed-certificate-and-private-key-toostore-it-optional"></a>Экспортировать hello самозаверяющего сертификата и закрытого ключа toostore его (необязательно)

Вы можете tooexport hello самозаверяющий корневой сертификат и безопасно хранить. При необходимости позднее можно будет установить его на другом компьютере и создать дополнительные сертификаты клиента или экспортировать другой CER-файл. tooexport hello самозаверяющий корневой сертификат как PFX-файл, выберите hello корневой сертификат или использовать hello же действия, как описано в [Экспорт сертификата клиента](#clientexport).

## <a name="create-and-install-client-certificates"></a>Создание и установка сертификатов клиента

Не устанавливайте самозаверяющий сертификат hello непосредственно на клиентском компьютере hello. Необходимо toogenerate сертификат клиента из hello самозаверяющий сертификат. Вы затем экспортировать и установите hello клиентского сертификата toohello клиентском компьютере. следующие шаги Hello не зависят от модели развертывания. Они подходят как для модели с использованием диспетчера ресурсов, так и для классической модели.

### <a name="clientcert"></a>Создание сертификата клиента

Каждый клиентский компьютер, который подключается tooa виртуальной сети с помощью точка-сайт должен иметь установленный сертификат клиента. Создайте сертификат клиента из hello самозаверяющий корневой сертификат и затем экспортировать и установите сертификат клиента hello. Если сертификат клиента hello не установлен, не пройдет проверку подлинности. 

Hello следующие шаги описывают создание клиентский сертификат из самозаверяющего корневого сертификата. Можно создать несколько сертификатов из hello выдачи корневых сертификатов. При создании клиентских сертификатов, используя приведенные ниже действия hello hello сертификат клиента автоматически устанавливается на компьютере hello использования сертификата toogenerate hello. Если требуется tooinstall сертификата клиента на другой компьютер, можно экспортировать сертификат hello.
 
1. На hello же компьютере, что вы использовали toocreate hello самоподписанный сертификат, откройте командную строку от имени администратора.
2. Изменения и запуска образца toogenerate hello сертификат клиента.
  * Изменение *«P2SRootCert»* toohello имя, для которого создается hello клиентский сертификат из самозаверяющего корневого hello. Убедитесь, что вы используете имя hello hello корневой сертификат, который является любой hello "CN =" значение было указано при создании самозаверяющего корневого hello.
  * Изменение *P2SChildCert* toohello имя, которое будет toogenerate toobe сертификат клиента.

  При запуске hello следующий пример без изменения его результат hello — сертификат клиента с именем P2SChildcert в хранилище личных сертификатов, который был создан из корневого сертификата P2SRootCert.

  ```cmd
  makecert.exe -n "CN=P2SChildCert" -pe -sky exchange -m 96 -ss My -in "P2SRootCert" -is my -a sha256
  ```

### <a name="clientexport"></a>Экспорт сертификата клиента

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

### <a name="install"></a>Установка экспортированного сертификата клиента

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>Дальнейшие действия

Продолжайте настраивать параметры конфигурации типа "точка-сеть". 

* Для **диспетчера ресурсов** модели шагов развертывания см. в разделе [Настройка tooa подключение точка-сайт виртуальной сети](vpn-gateway-howto-point-to-site-resource-manager-portal.md).
* Для **классический** модели шагов развертывания см. в разделе [Настройка tooa подключение точка-сеть VPN виртуальной сети (классические)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
