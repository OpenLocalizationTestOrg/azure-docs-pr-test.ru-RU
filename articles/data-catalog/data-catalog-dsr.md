---
title: "Источники данных aaaSupported в каталоге данных Azure | Документы Microsoft"
description: "В этой статье перечислены спецификации источников данных в настоящее время поддерживается hello."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: jstevens
editor: 
tags: 
ms.assetid: fd4345ca-2ed8-4c5e-9c4b-f954be2fc9f9
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 4bfcabf31bf9fd781c939a5026abc42a5407df32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="supported-data-sources-in-azure-data-catalog"></a>Источники данных, поддерживаемые в каталоге данных Azure

Можно публиковать метаданные с помощью открытого API-средства регистрации один раз, или путем ввода вручную сведения непосредственно toohello каталога данных Azure, веб-портала. Hello следующей таблице перечислены все источники данных, поддерживаемых каталога hello сегодня и hello возможностей публикации для каждого. Кроме того, содержатся hello внешние данные, предназначенные для каждого источника данных можно запустить из опыта наших портала «открыть в». Вторая таблица Hello содержит более подробные технические спецификации для каждого свойства соединения источника данных.


## <a name="list-of-supported-data-sources"></a>Список поддерживаемых источников данных

<table>
    <tr>
       <td><b>Объект источника данных</b></td>
       <td><b>API</b></td>
       <td><b>Ручной ввод</b></td>
       <td><b>Средство регистрации</b></td>
       <td><b>Средства Open-In</b></td>
       <td><b>Примечания</b></td>
    </tr>
    <tr>
      <td>Каталог Azure Data Lake Store</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Файл Azure Data Lake Store</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Хранилище больших двоичных объектов Azure</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2>Power BI</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Каталог службы хранилища Azure</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2>Power BI</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Таблица служба хранилища Azure</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td>
        <font size="2"></font>
      </td>
      <td>
        <font size="2"></font>
      </td>
    </tr>
    <tr>
      <td>Каталог HDFS</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Файл HDFS</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Таблица Hive</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓</td>
      <td><font size=2>Excel</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Представление Hive</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓</td>
      <td><font size=2>Excel</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Таблица MySQL</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Представление MySQL</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Таблица базы данных Oracle</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Представление базы данных Oracle</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Другие (универсальный ресурс)</td>
      <td>✓ </td>
      <td>✓ </td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Таблица хранилища данных SQL Azure</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2>Excel, Power BI, SQL Server Data Tools</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Представление хранилища данных SQL</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2>Excel, Power BI, SQL Server Data Tools</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Размерность SQL Server Analysis Services</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Ключевые показатели эффективности SQL Server Analysis Services</td>
      <td>✓</td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Измерение SQL Server Analysis Services</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Таблица SQL Server Analysis Services</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2>Excel, Power BI</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Отчет для служб SQL Server Reporting Services</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓</td>
      <td><font size=2>"Обзор"</font></td>
      <td><font size=2>Только серверы в основном режиме. Режим SharePoint не поддерживается.</font></td>
    </tr>
    <tr>
      <td>Таблица SQL Server</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2>Excel, Power BI, SQL Server Data Tools</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Представление SQL Server</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2>Excel, Power BI, SQL Server Data Tools</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Таблица Teradata</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓</td>
      <td><font size=2>Excel</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Представление Teradata</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓</td>
      <td><font size=2>Excel</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Представление SAP Hana</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2>Power BI</font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Таблица DB2</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Представление DB2</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Файл файловой системы</td>
      <td>✓ </td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Каталог FTP</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Файл FTP</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Отчет HTTP</td>
      <td>✓ </td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Конечная точка HTTP</td>
      <td>✓ </td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Файл HTTP</td>
      <td>✓ </td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Набор сущностей OData</td>
      <td>✓ </td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Функция OData</td>
      <td>✓ </td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Таблица PostgreSQL</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Представление PostgreSQL</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Представление SAP Hana</td>
      <td>✓ </td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td> Объект SalesForce</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Список SharePoint </td>
      <td>✓ </td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Коллекция Azure Cosmos DB</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Универсальная таблица ODBC</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Универсальное представление ODBC</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Таблица Cassandra</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2>Публикация в качестве ресурса ODBC</font></td>
    </tr>
    <tr>
      <td>Представление Cassandra</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2>Публикация в качестве ресурса ODBC</font></td>
    </tr>
    <tr>
      <td>Таблица Sybase</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Представление Sybase</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td>Таблица MongoDB</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2>Публикация в качестве ресурса ODBC</font></td>
    </tr>
    <tr>
      <td>Представление MongoDB</td>
      <td>✓ </td>
      <td>✓ </td>
      <td>✓ </td>
      <td><font size=2></font></td>
      <td><font size=2>Публикация в качестве ресурса ODBC</font></td>
    </tr>
</table>

Если необходима поддержка дополнительных источников отправки запроса компонент toohello [форуме каталога данных Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).


## <a name="data-source-reference-specification"></a>Спецификация ссылки на источник данных
> [!NOTE]
> Hello **структуры DSL** столбце hello в следующей таблице перечислены только hello свойства соединения для «address» в контейнере свойств, используемых каталога данных Azure. То есть контейнер свойств «адрес» может содержать другие свойства соединения источника данных hello, которое каталога данных Azure сохраняется, но не использует.

<table>
    <tr>
       <td><b>Тип источника</b></td>
       <td><b>Тип ресурса</b></td>
       <td><b>Типы объектов</b></td>
       <td><b>Структура DSL<b></td>
    </tr>
    <tr>
      <td>Хранилище озера данных Azure</td>
      <td>Контейнер</td>
      <td>Озеро данных</td>
      <td>
        <font size=2> Протокол: webhdfs <br>Аутентификация: {basic, oauth} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </td>
    </tr>
    <tr>
      <td>Хранилище озера данных Azure</td>
      <td>Таблица</td>
      <td>Каталог, файл</td>
      <td>
        <font size=2> Протокол: webhdfs <br>Аутентификация: {basic, oauth} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </td>
    </tr>
    <tr>
      <td>Хранилище Azure</td>
      <td>Контейнер</td>
      <td>Контейнер</td>
      <td>
        <font size=2> Протокол: azure-blobs <br>Аутентификация: {azure-access-key} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </td>
    </tr>
    <tr>
      <td>Хранилище Azure</td>
      <td>Таблица</td>
      <td>Большой двоичный объект, каталог</td>
      <td>
        <font size=2> Протокол: azure-blobs <br>Аутентификация: {azure-access-key} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </td>
    </tr>
    <tr>
      <td>Хранилище Azure</td>
      <td>Контейнер</td>
      <td>Контейнер</td>
      <td>
        <font size=2> Протокол: azure-tables <br>Аутентификация: {azure-access-key} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </td>
    </tr>
    <tr>
      <td>Хранилище Azure</td>
      <td>Таблица</td>
      <td>Таблица</td>
      <td>
        <font size=2> Протокол: azure-tables <br>Аутентификация: {azure-access-key} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </td>
    </tr>
    <tr>
      <td>Cosmos</td>
      <td>Контейнер</td>
      <td>Виртуальный кластер</td>
      <td>
        <font size=2> Протокол: cosmos <br>Аутентификация: {basic, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </td>
    </tr>
    <tr>
      <td>Cosmos</td>
      <td>Таблица</td>
      <td>Поток, набор потоков, представление</td>
      <td>
        <font size=2> Протокол: cosmos <br>Аутентификация: {basic, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </td>
    </tr>
    <tr>
      <td>DataZen</td>
      <td>Контейнер</td>
      <td>Сайт</td>
      <td>
        <font size=2> Протокол: http <br>Аутентификация: {none, basic, windows, oauth} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </td>
    </tr>
    <tr>
      <td>DataZen</td>
      <td>Отчет</td>
      <td>Отчет, панель мониторинга</td>
      <td>
        <font size=2> Протокол: http <br>Аутентификация: {none, basic, windows, oauth} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </td>
    </tr>
    <tr>
      <td>DB2</td>
      <td>Контейнер</td>
      <td>База данных</td>
      <td>
        <font size=2> Протокол: DB2 <br>Аутентификация: {basic, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </td>
    </tr>
    <tr>
      <td>DB2</td>
      <td>Таблица</td>
      <td>Таблица, представление</td>
      <td>
        <font size=2> Протокол: DB2 <br>Аутентификация: {basic, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </td>
    </tr>
    <tr>
      <td>Файловая система</td>
      <td>Таблица</td>
      <td>Файл</td>
      <td>
        <font size=2> Протокол: файл <br>Аутентификация: {none, basic, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </td>
    </tr>
    <tr>
      <td>FTP</td>
      <td>Таблица</td>
      <td>Каталог, файл</td>
      <td>
        <font size=2> Протокол: ftp <br>Аутентификация: {none, basic, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </td>
    </tr>
    <tr>
      <td>Распределенная файловая система Hadoop</td>
      <td>Контейнер</td>
      <td>HDInsight</td>
      <td>
        <font size=2> Протокол: webhdfs <br>Аутентификация: {basic, oauth} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </td>
    </tr>
    <tr>
      <td>Распределенная файловая система Hadoop</td>
      <td>Таблица</td>
      <td>Каталог, файл</td>
      <td>
        <font size=2> Протокол: webhdfs <br>Аутентификация: {basic, oauth} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </td>
    </tr>
    <tr>
      <td>Hive</td>
      <td>Контейнер</td>
      <td>База данных</td>
      <td>
        <font size=2> Протокол: hive <br>Аутентификация: {hdinsight, basic, username, none} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>connectionProperties: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </td>
    </tr>
    <tr>
      <td>Hive</td>
      <td>Таблица</td>
      <td>Таблица, представление</td>
      <td>
        <font size=2> Протокол: hive <br>Аутентификация: {hdinsight, basic, username, none} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object <br>connectionProperties: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </td>
    </tr>
    <tr>
      <td>HTTP</td>
      <td>Контейнер</td>
      <td>Сайт</td>
      <td>
        <font size=2> Протокол: http <br>Аутентификация: {none, basic, windows, oauth} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </td>
    </tr>
    <tr>
      <td>HTTP</td>
      <td>Отчет</td>
      <td>Отчет, панель мониторинга</td>
      <td>
        <font size=2> Протокол: http <br>Аутентификация: {none, basic, windows, oauth} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </td>
    </tr>
    <tr>
      <td>HTTP</td>
      <td>Таблица</td>
      <td>Конечная точка, файл</td>
      <td>
        <font size=2> Протокол: http <br>Аутентификация: {none, basic, windows, oauth} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </td>
    </tr>
    <tr>
      <td>MySQL</td>
      <td>Контейнер</td>
      <td>База данных</td>
      <td>
        <font size=2> Протокол: mysql <br>Аутентификация: {protocol, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </td>
    </tr>
    <tr>
      <td>MySQL</td>
      <td>Таблица</td>
      <td>Таблица, представление</td>
      <td>
        <font size=2> Протокол: mysql <br>Аутентификация: {protocol, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </td>
    </tr>
    <tr>
      <td>OData</td>
      <td>Контейнер</td>
      <td>Контейнер сущностей</td>
      <td>
        <font size=2> Протокол: odata <br>Аутентификация: {none, basic, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </td>
    </tr>
    <tr>
      <td>OData</td>
      <td>Таблица</td>
      <td>Набор сущностей, функция</td>
      <td>
        <font size=2> Протокол: odata <br>Аутентификация: {none, basic, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </td>
    </tr>
    <tr>
      <td>База данных Oracle</td>
      <td>Контейнер</td>
      <td>База данных</td>
      <td>
        <font size=2> Протокол: oracle <br>Аутентификация: {protocol, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </td>
    </tr>
    <tr>
      <td>База данных Oracle</td>
      <td>Таблица</td>
      <td>Таблица, представление</td>
      <td>
        <font size=2> Протокол: oracle <br>Аутентификация: {protocol, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </td>
    </tr>
    <tr>
      <td>PostgreSQL</td>
      <td>Контейнер</td>
      <td>База данных</td>
      <td>
        <font size=2> Протокол: postgresql <br>Аутентификация: {basic, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </td>
    </tr>
    <tr>
      <td>PostgreSQL</td>
      <td>Таблица</td>
      <td>Таблица, представление</td>
      <td>
        <font size=2> Протокол: postgresql <br>Аутентификация: {basic, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </td>
    </tr>
    <tr>
      <td>Power BI</td>
      <td>Контейнер</td>
      <td>Сайт</td>
      <td>
        <font size=2> Протокол: http <br>Аутентификация: {none, basic, windows, oauth} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </td>
    </tr>
    <tr>
      <td>Power BI</td>
      <td>Отчет</td>
      <td>Отчет, панель мониторинга</td>
      <td>
        <font size=2> Протокол: http <br>Аутентификация: {none, basic, windows, oauth} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </td>
    </tr>
    <tr>
      <td>Power Query</td>
      <td>Таблица</td>
      <td>Гибридные данные</td>
      <td>
        <font size=2> Протокол: power-query <br>Аутентификация: {oauth} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </td>
    </tr>
    <tr>
      <td>Salesforce</td>
      <td>Таблица</td>
      <td>Объект</td>
      <td>
        <font size=2> Протокол: salesforce-com <br>Аутентификация: {basic, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </td>
    </tr>
    <tr>
      <td>SAP HANA</td>
      <td>Контейнер</td>
      <td>сервер;</td>
      <td>
        <font size=2> Протокол: sap-hana-sql <br>Аутентификация: {protocol, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </td>
    </tr>
    <tr>
      <td>SAP HANA</td>
      <td>Таблица</td>
      <td>Просмотр</td>
      <td>
        <font size=2> Протокол: sap-hana-sql <br>Аутентификация: {protocol, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </td>
    </tr>
    <tr>
      <td>SharePoint</td>
      <td>Таблица</td>
      <td>список</td>
      <td>
        <font size=2> Протокол: sharepoint-list <br>Аутентификация: {basic, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </td>
    </tr>
    <tr>
      <td>Хранилище данных SQL</td>
      <td>Команда</td>
      <td>Хранимая процедура</td>
      <td>
        <font size=2> Протокол: tds <br>Аутентификация: {protocol, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </td>
    </tr>
    <tr>
      <td>Хранилище данных SQL</td>
      <td>TableValuedFunction</td>
      <td>Функция с табличным значением</td>
      <td>
        <font size=2> Протокол: tds <br>Аутентификация: {protocol, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </td>
    </tr>
    <tr>
      <td>Хранилище данных SQL</td>
      <td>Контейнер</td>
      <td>База данных</td>
      <td>
        <font size=2> Протокол: tds <br>Аутентификация: {protocol, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </td>
    </tr>
    <tr>
      <td>Хранилище данных SQL</td>
      <td>Таблица</td>
      <td>Таблица, представление</td>
      <td>
        <font size=2> Протокол: tds <br>Аутентификация: {protocol, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </td>
    </tr>
    <tr>
      <td>SQL Server</td>
      <td>Команда</td>
      <td>Хранимая процедура</td>
      <td>
        <font size=2> Протокол: tds <br>Аутентификация: {protocol, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </td>
    </tr>
    <tr>
      <td>SQL Server</td>
      <td>TableValuedFunction</td>
      <td>Функция с табличным значением</td>
      <td>
        <font size=2> Протокол: tds <br>Аутентификация: {protocol, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </td>
    </tr>
    <tr>
      <td>SQL Server</td>
      <td>Контейнер</td>
      <td>База данных</td>
      <td>
        <font size=2> Протокол: tds <br>Аутентификация: {protocol, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </td>
    </tr>
    <tr>
      <td>SQL Server</td>
      <td>Таблица</td>
      <td>Таблица, представление</td>
      <td>
        <font size=2> Протокол: tds <br>Аутентификация: {protocol, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </td>
    </tr>
    <tr>
      <td>Многомерная модель служб SQL Server Analysis Services</td>
      <td>Контейнер</td>
      <td>Модель</td>
      <td>
        <font size=2> Протокол: analysis-services <br>Аутентификация: {windows, basic, anonymous, none} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </td>
    </tr>
    <tr>
      <td>Многомерная модель служб SQL Server Analysis Services</td>
      <td>Ключевой показатель эффективности</td>
      <td>Ключевой показатель эффективности</td>
      <td>
        <font size=2> Протокол: analysis-services <br>Аутентификация: {windows, basic, anonymous, none} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </td>
    </tr>
    <tr>
      <td>Многомерная модель служб SQL Server Analysis Services</td>
      <td>Measure</td>
      <td>Measure</td>
      <td>
        <font size=2> Протокол: analysis-services <br>Аутентификация: {windows, basic, anonymous, none} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </td>
    </tr>
    <tr>
      <td>Многомерная модель служб SQL Server Analysis Services</td>
      <td>Таблица</td>
      <td>Измерение</td>
      <td>
        <font size=2> Протокол: analysis-services <br>Аутентификация: {windows, basic, anonymous, none} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </td>
    </tr>
    <tr>
      <td>Таблица SQL Server Analysis Services</td>
      <td>Контейнер</td>
      <td>Модель</td>
      <td>
        <font size=2> Протокол: analysis-services <br>Аутентификация: {windows, basic, anonymous, none} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </td>
    </tr>
    <tr>
      <td>Таблица SQL Server Analysis Services</td>
      <td>Ключевой показатель эффективности</td>
      <td>Ключевой показатель эффективности</td>
      <td>
        <font size=2> Протокол: analysis-services <br>Аутентификация: {windows, basic, anonymous, none} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </td>
    </tr>
    <tr>
      <td>Таблица SQL Server Analysis Services</td>
      <td>Measure</td>
      <td>Measure</td>
      <td>
        <font size=2> Протокол: analysis-services <br>Аутентификация: {windows, basic, anonymous, none} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </td>
    </tr>
    <tr>
      <td>Таблица SQL Server Analysis Services</td>
      <td>Таблица</td>
      <td>Таблица</td>
      <td>
        <font size=2> Протокол: analysis-services <br>Аутентификация: {windows, basic, anonymous, none} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </td>
    </tr>
    <tr>
      <td>Службы отчетов SQL Server</td>
      <td>Контейнер</td>
      <td>сервер;</td>
      <td>
        <font size=2> Протокол: reporting-services <br>Аутентификация: {windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </td>
    </tr>
    <tr>
      <td>Службы отчетов SQL Server</td>
      <td>Отчет</td>
      <td>Отчет</td>
      <td>
        <font size=2> Протокол: reporting-services <br>Аутентификация: {windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </td>
    </tr>
    <tr>
      <td>Teradata</td>
      <td>Контейнер</td>
      <td>База данных</td>
      <td>
        <font size=2> Протокол: teradata <br>Аутентификация: {protocol, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </td>
    </tr>
    <tr>
      <td>Teradata</td>
      <td>Таблица</td>
      <td>Таблица, представление</td>
      <td>
        <font size=2> Протокол: teradata <br>Аутентификация: {protocol, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </td>
    </tr>
    <tr>
      <td>SQL Server Master Data Services</td>
      <td>Контейнер</td>
      <td>Модель</td>
      <td>
        <font size="2"> Протокол: mssql-mds <br>Аутентификация: {windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </td>
    </tr>
    <tr>
      <td>SQL Server Master Data Services</td>
      <td>Таблица</td>
      <td>Сущность</td>
      <td>
        <font size="2"> Протокол: mssql-mds <br>Аутентификация: {windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </td>
    </tr>
    <tr>
      <td>Azure Cosmos DB</td>
      <td>Контейнер</td>
      <td>База данных</td>
      <td>
        <font size=2> Протокол: document-db <br>Аутентификация: {azure-access-key} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </td>
    </tr>
    <tr>
      <td>Azure Cosmos DB</td>
      <td>Коллекция</td>
      <td>Коллекция</td>
      <td>
        <font size=2> Протокол: document-db <br>Аутентификация: {azure-access-key} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </td>
    </tr>
    <tr>
      <td>Универсальные данные ODBC</td>
      <td>Контейнер</td>
      <td>База данных</td>
      <td>
        <font size=2> Протокол: odbc <br>Аутентификация: {basic, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </td>
    </tr>
    <tr>
      <td>Универсальные данные ODBC</td>
      <td>Таблица</td>
      <td>Таблица, представление</td>
      <td>
        <font size=2> Протокол: odbc <br>Аутентификация: {basic, windows} <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </td>
    </tr>
    <tr>
      <td>Sybase</td>
      <td>Контейнер</td>
      <td>База данных</td>
      <td>
        <font size=2> Протокол: sybase <br>Проверка подлинности: {basic, windows} <br>адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </td>
    </tr>
    <tr>
      <td>Sybase</td>
      <td>Таблица</td>
      <td>Таблица, представление</td>
      <td>
        <font size=2> Протокол: sybase <br>Проверка подлинности: {basic, windows} <br>адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </td>
    </tr>
    <tr>
      <td>Другой (нет для hello выше)</td>
      <td>\*</td>
      <td>\*</td>
      <td>
        <font size=2> Протокол: generic-asset <br>Адрес: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </td>
    </tr>
</table>
