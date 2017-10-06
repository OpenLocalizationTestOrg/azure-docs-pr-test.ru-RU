---
title: "Виртуальные машины Azure из обозревателя серверов aaaAccessing | Документы Microsoft"
description: "Обзор tooview Создание и управление виртуальными машинами Azure (ВМ) в обозревателе серверов в Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: f8326aed105a64ca558f766d712cc68701f82c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a>Доступ к виртуальным машинам Azure из обозревателя сервера
С помощью обозревателя сервера в Visual Studio можно отображать сведения о виртуальных машинах, размещенных в Azure.

## <a name="accessing-virtual-machines-in-server-explorer"></a>Доступ к виртуальным машинам из обозревателя сервера
Виртуальные машины, размещенные в Azure, можно открыть в обозревателе сервера. Необходимо сначала войти в подписку Azure tooview tooyour мобильные службы. toosign, откройте контекстное меню hello hello узла Azure в обозревателе серверов и выберите **подключения tooMicrosoft Azure**.

### <a name="tooget-information-about-your-virtual-machines"></a>tooget сведения о виртуальных машинах
1. В обозревателе серверов выберите виртуальную машину и выберите hello F4 ключа tooshow его окно свойств.
   
    Привет, в следующей таблице показано, какие свойства доступны, но это только для чтения. toochange, используйте hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
   
   | Свойство | Описание |
   | --- | --- |
   | DNS-имя |Hello URL-адрес с Интернет-адрес виртуальной машины hello hello. |
   | Среда |Для виртуальной машины hello значение этого свойства всегда равно Production. |
   | Имя |имя виртуальной машины hello Hello. |
   | Размер |размер виртуальной машины hello, которое отображает hello объем памяти и места на диске, доступном Hello. Дополнительные сведения см. в статье "Практическое руководство по настройке размеров виртуальных машин". |
   | Состояние |Возможные значения: "Запуск", "Запущено", "Остановка", "Остановлено" и "Получение состояния". Получение состояния в открывшемся hello текущее состояние неизвестно. Hello значения этого свойства отличаются от hello значения, которые используются на hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885). |
   | SubscriptionID |Hello идентификатор подписки для учетной записи Azure. Эту информацию можно отображать на hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885) путем просмотра свойств hello для подписки. |
2. Выберите узел конечной точки, а затем просмотреть hello **свойства** окна.
3. Hello следующей таблице описаны доступные свойства hello конечных точек, но они доступны только для чтения. tooadd или изменить hello конечных точек для виртуальной машины, используйте hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885). 
   
   | Свойство | Описание |
   | --- | --- |
   | Имя |Идентификатор конечной точки hello. |
   | Закрытый порт |Hello порта для сетевого доступа к внутренней tooyour приложения. |
   | Протокол |использует протокол Hello, hello транспортного уровня для этой конечной точки, TCP или UDP. |
   | Общий порт |Hello порт, который используется для общего доступа tooyour приложения. |

## <a name="next-steps"></a>Дальнейшие действия
toolearn Подробнее об использовании ролей Azure в Visual Studio в разделе [использование удаленного рабочего стола с ролями Azure](vs-azure-tools-remote-desktop-roles.md).

