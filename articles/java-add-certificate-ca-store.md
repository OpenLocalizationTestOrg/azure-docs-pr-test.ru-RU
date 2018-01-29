---
title: "Добавление сертификата в хранилище центра сертификации Java | Документация Майкрософт"
description: "Узнайте, как добавить сертификат центра сертификации (ЦС) в хранилище сертификатов (cacerts) центра сертификации Java для службы Twilio или Azure Service Bus."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: b6e1a305e19415ab1c4b4c208dac98ad1e2689c6
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="adding-a-certificate-to-the-java-ca-certificates-store"></a>Добавление сертификата в хранилище сертификатов ЦС Java
Ниже показано, как добавить сертификат центра сертификации (ЦС) в хранилище сертификатов (cacerts) центра сертификации Java. Приведен пример использования сертификата ЦС, требуемого службой Twilio. Ниже в этой статье описана установка сертификата ЦС для шины обслуживания Azure. 

Чтобы добавить сертификат ЦС перед сжатием JDK и добавлением его в папку **approot** проекта Azure, можно использовать keytool или выполнить задачу запуска Azure, которая использует keytool для добавления сертификата. В этом примере предполагается, что сертификат ЦС будет добавлен перед сжатием JDK. Также в примере будет использоваться конкретный сертификат ЦС, но действия, необходимые для получения различных сертификатов центра сертификации и их импорта в хранилище cacerts, будут такими же.

## <a name="to-add-a-certificate-to-the-cacerts-store"></a>Добавление сертификата в хранилище cacerts
1. В командной строке администратора для папки JDK **jdk\jre\lib\security** выполните следующий код, чтобы узнать, какие сертификаты установлены:
   
    `keytool -list -keystore cacerts`
   
    Вам будет предложено ввести пароль хранилища. Пароль по умолчанию — **changeit**. (Сведения о том, как изменить пароль, см. в документации по keytool на странице <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) В этом примере предполагается, что сертификат с MD5 устройства отпечатков пальцев 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 отсутствует в списке и вы хотите его импортировать (этот конкретный сертификат необходим для службы API Twilio).
2. Получение сертификата из списка сертификатов, перечисленных в [корневых сертификатах GeoTrust](http://www.geotrust.com/resources/root-certificates/). Щелкните правой кнопкой мыши ссылку сертификата с серийным номером 35:DE:F4:CF и сохраните его в папке **jdk\jre\lib\security**. Для целей этого примера он сохранен в файле с именем **Equifax\_Secure\_Certificate\_Authority.cer**.
3. Импортируйте сертификат с помощью следующей команды:
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    Если выводится приглашение подтвердить доверие этому сертификату, если сертификат имеет отпечаток пальцев MD5 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, введите **y**.
4. Выполните следующую команду, чтобы убедиться, что сертификат СЦ был успешно импортирован:
   
    `keytool -list -keystore cacerts`
5. Сожмите JDK и добавьте его в папку **approot** проекта Azure.

Дополнительные сведения о keytool см. по адресу <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.

## <a name="azure-root-certificates"></a>Корневые сертификаты Azure
Приложения, использующие службы Azure (например, Azure Service Bus), должны доверять сертификату Baltimore CyberTrust Root. (С 15 апреля 2013 года Azure начала миграцию с глобальной основы GTE CyberTrust в Baltimore CyberTrust Root. Такая миграция продолжается несколько месяцев.)

Сертификат Baltimore может быть установлен в вашем хранилище cacerts, поэтому не забудьте выполнить команду **keytool -list** , чтобы проверить, существует ли он уже.

Если требуется добавить Baltimore CyberTrust Root, он имеет серийный номер 02:00:00:b9 и отпечаток пальца SHA1 d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74. Его можно скачать по адресу <https://cacert.omniroot.com/bc2025.crt>, сохранить в локальном файле с расширением **CER**, а затем импортировать с помощью **keytool**, как показано выше.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об используемых в Azure корневых сертификатах см. в записи блога [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx) (Перенос корневых сертификатов Azure).

Дополнительные сведения о Java см. в разделе [Azure for Java developers](/java/azure) (Azure для разработчиков Java).

