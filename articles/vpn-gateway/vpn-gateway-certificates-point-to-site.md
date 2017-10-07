---
title: "Создание и экспорт сертификатов для подключений типа \"точка-сеть\" в Azure с помощью PowerShell | Документы Майкрософт"
description: "В этой статье содержатся действия toocreate самозаверяющий корневой сертификат, экспортируйте открытый ключ hello и создания сертификатов клиента с помощью PowerShell на Windows 10."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 11dda015368cda5ce9799fcc4f01d7c542b84fe8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a>Создание и экспорт сертификатов для подключений типа "точка-сеть" с помощью PowerShell в Windows 10

Точка-сеть соединения используют tooauthenticate сертификаты. В этой статье показано, как toocreate a самозаверяющий корневой сертификат и создания сертификатов клиента с помощью PowerShell на Windows 10. Если вам нужны дополнительные действия по настройке точки сайтами, таких как как список tooupload корневые сертификаты, выберите один из статей hello "Настройка точка-сеть" из hello следующие:

> [!div class="op_single_selector"]
> * [Создание самозаверяющих сертификатов с помощью PowerShell](vpn-gateway-certificates-point-to-site.md)
> * [Создание и экспорт сертификатов для подключений типа "точка — сеть" с помощью MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Настройка подключения "точка — сеть" модели Resource Manager на портале Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [Настройка подключения "точка-сеть" — Resource Manager — PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Настройка подключения "точка —сеть" классической модели на портале Azure](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


В этой статье на компьютере под управлением Windows 10, необходимо выполнить действия hello. командлеты PowerShell Hello использовать toogenerate сертификаты являются частью операционной системы Windows 10 hello и не работают в других версиях Windows. компьютер Hello Windows 10 — только сертификаты, необходимые toogenerate hello. После hello сертификаты создаются, можно загрузить их или установить их на любых поддерживаемых клиентских операционных систем. 

Если у вас компьютер Windows 10 tooa доступа, можно использовать [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate сертификаты. Hello сертификаты, создаваемые с помощью любого метода можно установить на любом [поддерживается](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) клиентской операционной системы.

## <a name="rootcert"></a>Создание самозаверяющего корневого сертификата

Используйте toocreate командлет New-SelfSignedCertificate hello самозаверяющего корневого сертификата. Дополнительные сведения о параметре см. в разделе [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

1. На компьютере под управлением Windows 10 откройте консоль Windows PowerShell с повышенными привилегиями.
2. Используйте следующий пример toocreate hello самозаверяющий корневой сертификат hello. Hello пример создает самозаверяющий корневой сертификат, с именем «P2SRootCert», который автоматически устанавливается в «Сертификаты — текущий пользователь\личные\сертификаты». Hello сертификата можно просмотреть, открыв *certmgr.msc*, или *Управление сертификатами пользователей*.

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <a name="cer"></a>Экспорт hello открытого ключа (CER)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

Hello exported.cer файл должен быть загруженного tooAzure. Дополнительные сведения см. в разделе [Подготовка CER-файла корневого сертификата к передаче](vpn-gateway-howto-point-to-site-rm-ps.md#upload). tooadd дополнительных доверенный корневой сертификат [в этом разделе](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) hello статьи.

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a>Экспорт самозаверяющего корневого сертификата hello и открытого ключа toostore его (необязательно)

Вы можете tooexport hello самозаверяющий корневой сертификат и безопасно хранить. При необходимости позднее можно будет установить его на другом компьютере и создать дополнительные сертификаты клиента или экспортировать другой CER-файл. tooexport hello самозаверяющий корневой сертификат как PFX-файл, выберите hello корневой сертификат или использовать hello же действия, как описано в [Экспорт сертификата клиента](#clientexport).

## <a name="clientcert"></a>Создание сертификата клиента

Каждый клиентский компьютер, который подключается tooa виртуальной сети с помощью точка-сайт должен иметь установленный сертификат клиента. Создайте сертификат клиента из hello самозаверяющий корневой сертификат и затем экспортировать и установите сертификат клиента hello. Если сертификат клиента hello не установлен, не пройдет проверку подлинности. 

Hello следующие шаги описывают создание клиентский сертификат из самозаверяющего корневого сертификата. Можно создать несколько сертификатов из hello выдачи корневых сертификатов. При создании клиентских сертификатов, используя приведенные ниже действия hello hello сертификат клиента автоматически устанавливается на компьютере hello использования сертификата toogenerate hello. Если требуется tooinstall сертификата клиента на другой компьютер, можно экспортировать сертификат hello.

Hello примерах используется toogenerate командлет New-SelfSignedCertificate hello сертификат клиента, срок действия истекает через один год. Дополнительные сведения о параметре, например установку другой срок для сертификата клиента hello, в разделе [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

### <a name="example-1"></a>Пример 1

В этом примере используется переменная «$cert» hello в предыдущем разделе объявлена hello. Если консоль PowerShell hello закрыто, после создания hello самозаверяющий корневой сертификат или создаете дополнительные клиентские сертификаты в новом сеансе консоли PowerShell, выполните шаги hello в [пример 2](#ex2).

Изменения и выполнения toogenerate пример hello сертификат клиента. При запуске hello следующий пример без изменения его результат hello — сертификат клиента с именем «P2SChildCert».  Tooname hello дочерний сертификат либо другие, измените значение CN hello. Не изменяйте hello TextExtension при запуске данного примера. Hello сертификат клиента, который создается автоматически устанавливается в «Сертификаты — текущий пользователь\личные\сертификаты» на компьютере.

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <a name="ex2"></a>Пример 2

При создании дополнительных клиентских сертификатов, или не используя hello же сеанс PowerShell, используемые toocreate самозаверяющий корневой сертификат, используйте hello следующие шаги:

1. Определите hello самозаверяющего корневого сертификата, установленного на компьютере hello. Этот командлет возвращает список сертификатов, установленных на компьютере.

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. Найдите имя субъекта hello hello возвращается список, а затем копировать hello отпечаток, найти следующее вхождение текста tooa tooit файл. В следующем примере hello существует два сертификата. Hello CN-имя — имя hello hello самозаверяющего корневого сертификата, из которого нужно toogenerate дочерний сертификат. В данном случае это P2SRootCert.

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. Объявите переменную для hello корневого сертификата, с помощью отпечатка hello из предыдущего шага hello. Замените ОТПЕЧАТОК отпечаток hello hello корневого сертификата, из которого нужно toogenerate дочерний сертификат.

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  Например переменная hello с помощью отпечатка hello для P2SRootCert в предыдущем шаге hello, выглядит следующим образом:

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  Изменения и выполнения toogenerate пример hello сертификат клиента. При запуске hello следующий пример без изменения его результат hello — сертификат клиента с именем «P2SChildCert». Tooname hello дочерний сертификат либо другие, измените значение CN hello. Не изменяйте hello TextExtension при запуске данного примера. Hello сертификат клиента, который создается автоматически устанавливается в «Сертификаты — текущий пользователь\личные\сертификаты» на компьютере.

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <a name="clientexport"></a>Экспорт сертификата клиента   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <a name="install"></a>Установка экспортированного сертификата клиента

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>Дальнейшие действия

Продолжайте настраивать параметры конфигурации типа "точка-сеть". 

* Для **диспетчера ресурсов** модели шагов развертывания см. в разделе [Настройка tooa подключение точка-сайт виртуальной сети](vpn-gateway-howto-point-to-site-resource-manager-portal.md). 
* Для **классический** модели шагов развертывания см. в разделе [Настройка tooa подключение точка-сеть VPN виртуальной сети (классические)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
