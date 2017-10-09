---
title: "Общие сведения о разработке приложений aaaDatabase для базы данных Azure для MySQL | Документы Microsoft"
description: "Появились вопросы проектирования, разработчику необходимо следовать при написании приложения код tooconnect tooAzure базы данных для MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: f08df605eba21b4ba4b43565c0a7ded95779a171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a>Обзор разработки приложений для базы данных Azure для MySQL 
В этой статье рассматриваются вопросы проектирования, разработчику необходимо следовать при написании приложения код tooconnect tooAzure базы данных для MySQL 

> [!TIP]
> Учебник отображение вы toocreate server, создать брандмауэр на основе сервера, просмотр свойств сервера, создание базы данных, подключение и запрос с использованием рабочей среды и mysql.exe см [проектирование первой базы данных MySQL в Azure](tutorial-design-database-using-portal.md)

## <a name="language-and-platform"></a>Язык и платформа
Доступны примеры кода на разных языках программирования и для разных платформ. Toohello образцов кода можно найти следующие ссылки: [библиотек подключений используется tooconnect tooAzure базы данных для MySQL](concepts-connection-libraries.md)

## <a name="tools"></a>Средства
База данных Azure для MySQL использует hello MySQL community версии, совместимой с MySQL стандартные инструменты управления, таких как Workbench или MySQL служебные программы, например mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql)и др. Также можно использовать hello портал Azure, Azure CLI и toointeract API-интерфейс REST со службой hello базы данных.

## <a name="resource-limitations"></a>Ограничения ресурсов
База данных MySQL в Azure управляет hello ресурсы доступны tooa сервера с помощью двух разных механизмов: 
- управление ресурсами; 
- принудительное применение ограничений.

## <a name="security"></a>Безопасность
База данных Azure MySQL предоставляет ресурсы для ограничения доступа, защиты данных, настройки пользователей и ролей и мониторинга действий в базе данных MySQL.

## <a name="authentication"></a>Аутентификация
База данных Azure MySQL поддерживает аутентификацию пользователей и имен входа на сервере.

## <a name="resiliency"></a>Устойчивость
В случае временная ошибка при подключении базы данных tooMySQL кода следует повторить вызов hello. Используйте логику повторных попыток hello отхода логику, рекомендуется, чтобы он не перегрузки hello базы данных SQL с повтором одновременно несколькими клиентами.

- Примеры кода: образцы кода, иллюстрирующие логику повторных попыток, в разделе примеров для hello язык в: [библиотек подключений используется tooconnect tooAzure базы данных для MySQL](concepts-connection-libraries.md)

## <a name="managing-connections"></a>Управление подключениями
Подключения к базе данных являются ограниченным ресурсом, поэтому рекомендуется получить понятное использования подключений при доступе к базе данных MySQL tooachieve более высокую производительность.
- База данных Access hello с использованием пулов соединений или постоянные подключения.
- База данных hello доступ с помощью коротких подключения срока действия. 
- Используйте логику повторных попыток в приложении в момент hello попытки подключения hello, toocatch сбоев из-за tooconcurrent подключений достигли hello максимально допустимое. В hello логику повторных попыток, задайте небольшую задержку и дождитесь случайное время до попытки hello дополнительные подключения.
