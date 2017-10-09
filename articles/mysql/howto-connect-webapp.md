---
title: "aaaConnect существующей службы приложений Azure tooAzure базы данных MySQL | Документы Microsoft"
description: "Инструкции о том, как tooproperly подключаться существующей службы приложений Azure tooAzure базы данных для MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a>Подключение к MySQL server существующей службы приложений Azure tooAzure базы данных
В этом документе объясняется, как tooconnect существующей службы приложений Azure tooyour базы данных Azure для сервера MySQL.

## <a name="before-you-begin"></a>Перед началом работы
Войдите в toohello [портал Azure](https://portal.azure.com). Создайте базу данных Azure для сервера MySQL. Дополнительные сведения приведены слишком[как toocreate базы данных Azure для сервера MySQL с портала](quickstart-create-mysql-server-database-using-azure-portal.md) или [как toocreate базы данных Azure для MySQL server, используя интерфейс командной строки](quickstart-create-mysql-server-database-using-azure-cli.md).

В настоящее время существует два tooenable доступа решений, службе приложений Azure tooan базы данных Azure для MySQL. Оба решения включают настройку правил брандмауэра уровня сервера.

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a>Решение 1 - создать правило брандмауэра tooallow все IP-адреса
База данных Azure для MySQL обеспечивает управление доступом с помощью tooprotect брандмауэра данных. При подключении из службы приложений Azure tooAzure базы данных для сервера MySQL следует помнить, что hello исходящих IP-адреса службы приложений являются динамическими по своей природе. 

доступность hello tooensure службе приложений Azure, мы рекомендуем использовать это решение tooallow все IP-адреса.

> [!NOTE]
> Корпорация Майкрософт работает для долгосрочного tooavoid решения, позволяя все IP-адреса для служб Azure tooconnect tooAzure базы данных MySQL.

1. В колонке сервера MySQL hello в разделе Параметры щелкните **безопасности подключения** tooopen hello безопасности подключения колонке hello базы данных Azure для MySQL.

   ![Портал Azure: щелчок пункта "Безопасность подключения"](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Введите значения в полях **ИМЯ ПРАВИЛА**, **НАЧАЛЬНЫЙ IP-АДРЕС** и **КОНЕЧНЫЙ IP-АДРЕС**. Нажмите кнопку **Сохранить**.
   - Имя правила: Allow-All-IPs
   - Начальный IP-адрес: 0.0.0.0
   - Конечный IP-адрес: 255.255.255.255

   ![Портал Azure — добавление всех IP-адресов](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a>Решение 2 - создать брандмауэр tooexplicitly правила Разрешить исходящие IP-адресов
Можно явно добавить, что все hello исходящий IP-адреса службы приложения Azure.

1. В колонке hello свойства приложения службы, откройте ваш **ИСХОДЯЩИЙ IP-адрес**.

   ![Портал Azure — просмотр исходящих IP-адресов](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. В колонке безопасности подключение к MySQL hello добавьте исходящий IP-адресов по одному.

   ![Портал Azure — добавление явных IP-адресов](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. Помните, слишком**Сохранить** правил брандмауэра.

Хотя hello службы приложений Azure пытается tookeep IP адресов константа со временем, существуют случаи, где hello IP-адреса могут измениться. Например, когда hello перезапускает приложение возникает, операции масштабирования, или при добавлении новых компьютеров в данных Azure региональные центры tooincrease hello емкости. При изменения hello IP-адресов, приложение hello может простаивать в событии hello, больше не может подключиться toohello MySQL server. При выборе одной из предыдущих решения hello, рассмотрите возможность этой возможности.

## <a name="ssl-configuration"></a>Настройка SSL
Протокол SSL по умолчанию включен для базы данных Azure для MySQL. Если приложение не использует SSL tooconnect toohello, базы данных, то необходимо toodisable SSL на сервер MySQL. Дополнительные сведения о том, как tooconfigure SSL, см. в разделе [использование SSL с базой данных Azure для MySQL](howto-configure-ssl.md).

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о строках соединения см. в разделе слишком[строки подключения](howto-connection-string.md).
