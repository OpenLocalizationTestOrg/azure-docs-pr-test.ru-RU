---
title: "aaaSSL подключения для базы данных Azure для MySQL | Документы Microsoft"
description: "Сведения о настройке базы данных Azure для MySQL и связанные с ними приложения tooproperly использовать подключения SSL"
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6fca7c88fc0f1fd6058d68fcff90fd409abd97a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a>SSL-соединения в базе данных Azure для MySQL
База данных Azure для MySQL поддерживает подключение приложения tooclient сервера базы данных с помощью Secure Sockets Layer (SSL). Принудительное SSL-подключений между сервером базы данных и клиентские приложения помогает защитить от атак «злоумышленник в середине hello» путем шифрования hello потока данных между сервером hello и приложения.

## <a name="default-settings"></a>Параметры по умолчанию
По умолчанию hello службы базы данных должно быть toorequire настроенный SSL-подключения при подключении tooMySQL.  Рекомендуется избежать отключения hello параметр SSL, когда это возможно. 

При подготовке новой базы данных Azure для сервера MySQL через портал Azure hello и интерфейс командной строки, принудительное выполнение SSL-соединений включен по умолчанию. 

Аналогичным образом строки подключения, предварительно определенные в параметрах «Строки соединения» hello в области сервера в hello портал Azure включают hello необходимые параметры для общий языков tooconnect tooyour сервер баз данных с помощью протокола SSL. Hello SSL параметра различается в зависимости от соединителя hello, например «ssl = true» или «sslmode = требуют» или» sslmode = необходимые» и др..

как tooenable или отключите SSL-подключение при разработке приложения, см. слишком toolearn[как tooconfigure SSL](howto-configure-ssl.md).

## <a name="next-steps"></a>Дальнейшие действия
[Библиотеки подключений для базы данных Azure для MySQL](concepts-connection-libraries.md)
