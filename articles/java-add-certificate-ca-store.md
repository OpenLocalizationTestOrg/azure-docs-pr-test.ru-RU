---
title: "хранилище сертификатов ЦС Java toohello aaaAdd | Документы Microsoft"
description: "Узнайте, как tooadd сертификат центра сертификации (ЦС) сертификат toohello Java сертификат ЦС (cacerts) хранения для Twilio службы или шины обслуживания Azure."
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
ms.openlocfilehash: 030e43129580023942dee662e72d2f443167f308
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-certificate-toohello-java-ca-certificates-store"></a>Добавление сертификата toohello хранилище сертификатов ЦС Java
Здравствуй, следующие шаги показывают, как tooadd сертификат центра сертификации (ЦС) сертификат toohello Java сертификат ЦС (cacerts) хранения. пример Hello используется для сертификата ЦС hello требуется hello Twilio службы. Далее в разделе hello описываются как hello tooinstall ЦС сертификат для hello Azure Service Bus. 

JDK и добавив его tooyour проекта Azure можно использовать toozipping предыдущего сертификата ЦС hello tooadd keytool **approot** папки, или может запустить задачу Azure при запуске, которая использует keytool tooadd hello сертификат. В этом примере предполагается, что вы добавите предыдущих toohello каталога сертификат ЦС JDK ZIP-архиве. Кроме того конкретного сертификата ЦС будет использоваться в примере hello, но hello действия получения другой сертификат ЦС и импортировав их в hello cacerts хранилища будет выглядеть.

## <a name="tooadd-a-certificate-toohello-cacerts-store"></a>сохранить сертификат toohello cacerts tooadd
1. В командной строке, имеет значение tooyour JDK **jdk\jre\lib\security** запуска hello toosee, какие сертификаты установлены следующие папки:
   
    `keytool -list -keystore cacerts`
   
    Вам будет выведен для hello хранить пароль. пароль по умолчанию Hello — **changeit**. (Если требуется пароль toochange hello, см. в документации по keytool hello в <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) В этом примере предполагается hello сертификата с MD5 отпечатков пальцев 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 отсутствует в списке, и что требуется tooimport ИТ (это определенный сертификат требуется hello Twilio API-службы).
2. Получить сертификат hello hello список сертификатов, перечисленных в [GeoTrust корневые сертификаты](http://www.geotrust.com/resources/root-certificates/). Щелкните правой кнопкой мыши ссылку hello для hello сертификат с серийным номером 35:DE:F4:CF и сохраните его toohello **jdk\jre\lib\security** папки. Для этого примера, он был сохранен файл tooa с именем **Equifax\_Secure\_сертификат\_Authority.cer**.
3. Импортируйте сертификат hello через hello следующую команду:
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    При появлении запроса о tootrust этот сертификат hello сертификат имеет Отпечаток MD5 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 ответ, введя **y**.
4. Выполнения hello, следующая команда tooensure hello ЦС сертификата успешно импортировано:
   
    `keytool -list -keystore cacerts`
5. ZIP-архив hello JDK и добавить его tooyour проекта Azure в **approot** папки.

Дополнительные сведения о keytool см. по адресу <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.

## <a name="azure-root-certificates"></a>Корневые сертификаты Azure
Приложения, использующие службы Azure (например, Azure Service Bus) требуется сертификат Baltimore CyberTrust Root tootrust hello. (Начиная 15 апреля 2013 г., Azure начала миграции с hello глобальной основы CyberTrust GTE toohello Baltimore CyberTrust Root. Эта миграция заняла toocomplete несколько месяцев).

Hello Baltimore сертификатов могут быть уже установлены в хранилище cacerts, поэтому необходимо учитывать toorun hello **keytool-список** команды первого toosee, если он уже существует.

Если вам требуется tooadd hello Baltimore CyberTrust Root, она имеет 02:00:00:b9 серийный номер и c d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2 отпечаток SHA1: 78:db:28:52:ca:e4:74. Ее можно загрузить из <https://cacert.omniroot.com/bc2025.crt>, сохраняемый tooa локальный файл с расширением **CER-файл**, а затем импортировать с помощью **keytool** как показано выше.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о hello корневые сертификаты, используемые в Azure см. в разделе [Azure корневой сертификат миграции](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).

Дополнительные сведения о Java см. в разделе [Azure for Java developers](/java/azure) (Azure для разработчиков Java).

