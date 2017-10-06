---
title: "пакет SDK для .NET 3.0 заметки о выпуске aaaAzure | Документы Microsoft"
description: "Заметки о выпуске пакета Azure SDK для .NET 3.0"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: 8970b4c9b64de40dc29a33d69006a00ae5e38a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a>Заметки о выпуске пакета Azure SDK для .NET 3.0

Этот раздел содержит заметки о выпуске для версии 3.0 hello Azure SDK для .NET.

##<a name="azure-sdk-for-net-30-release-summary"></a>Сводные данные о выпуске пакета Azure SDK для .NET 3.0

Дата выпуска: 07.03.2017
 
В этом выпуске были введены нет критические изменения toohello Azure SDK 3.0. Имеется также tooleverage нет необходимости процесса обновления этот пакет SDK с существующие проекты облачной службы. Использование tooallow hello Azure SDK 3.0 без необходимости процесса обновления Azure SDK 3.0 устанавливает toohello же каталоги, что пакет Azure SDK 2.9. Большинство компонентов hello не изменился с 2.9 hello основной номер версии, но вместо обновляться hello номер сборки.

## <a name="visual-studio-2017-rtw"></a>Visual Studio 2017 RTW

- Этот выпуск hello Azure SDK для .NET в Visual Studio 2017 г., встроенной в toohello рабочей нагрузки Azure. Все hello инструменты разработки Azure toodo будет частью Visual Studio Забегая вперед 2017 г. Для Visual Studio 2015 hello SDK по-прежнему доступны через WebPI. Мы вывели из использования выпуски пакета Azure SDK для .NET для Visual Studio 2013, так как теперь вышла версия Visual Studio 2017.

### <a name="azure-diagnostics"></a>Диагностика Azure

- Измененные hello поведение tooonly хранить частичную строку соединения с ключом hello заменяется маркер для строки подключения к хранилищу диагностики облачных служб. ключ фактического хранения Hello теперь хранится в папке профиля пользователя hello, можно контролировать доступ к нему. Visual Studio прочитает hello ключ хранилища из папке профиля пользователя для локальной отладки и процесс публикации. 
- В ответ toohello изменений, описанных выше Visual Studio Online team улучшенные hello шаблона задачи развертывания облачных служб Azure, пользователи могут указать hello ключ хранилища для настройки расширения системы диагностики при публикации tooAzure в непрерывной интеграции и развертывания.
- Мы уже сделали возможных toostore строку безопасного соединения и разметки для Azure Diagnostics (WAD), toohelp через environements устранить проблемы с конфигурацией.
 
### <a name="windows-server-2016-virtual-machines"></a>Виртуальные машины Windows Server 2016

- Visual Studio теперь поддерживает развертывание облачных служб tooOS семейство 5 (Windows Server 2016) виртуальных машин. Для существующих облачных служб можно изменить ваш tootarget параметры hello новое семейство ОС. Если при создании новых облачных служб, выберите службу hello toocreate, с помощью .net 4.6 или более поздней версии, то по умолчанию hello службы toouse 5 семейства ОС.  Дополнительные сведения можно просмотреть hello [семейства гостевых ОС поддерживает таблицу](../cloud-services/cloud-services-guestos-update-matrix.md).

### <a name="known-issues"></a>Известные проблемы

- В пакете SDK Azure 3.0 для .NET возникала проблема при удалении Visual Studio 2017 в параллельной конфигурации с Visual Studio 2015.  При наличии hello пакет Azure SDK для Visual Studio 2015 hello эмулятор хранилища Microsoft Azure и эмулятор вычислений Microsoft Azure будут удалены при удалении Visual Studio 2017 г.  Это приведет к ошибке при создании и отладке новых проектов облачных служб в Visual Studio 2015. В заказ toofix эту проблему, переустановите hello Azure SDK из hello установщика веб-платформы.  Hello проблема будет устранена в следующей версии Visual Studio 2017 г.  .

 
### <a name="azure-in-role-cache"></a>Кэш роли Azure 

- Поддержка кэша роли Azure завершилась 30 ноября 2016 года. Дополнительные сведения см. [здесь](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).




