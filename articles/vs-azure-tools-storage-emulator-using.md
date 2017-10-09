---
title: "aaaConfiguring и с помощью эмулятора хранилища с помощью Visual Studio \"hello\" | Документы Microsoft"
description: "Настройка и использование hello эмулятора хранилища с помощью Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: c8e7996f-6027-4762-806e-614b93131867
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/17/2017
ms.author: kraigb
ms.openlocfilehash: d590f21146c86bcb7bfa6b6164b92c6df5938d5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-hello-storage-emulator-with-visual-studio"></a>Настройка и использование hello эмулятора хранилища с помощью Visual Studio
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Обзор
среда разработки Hello Azure SDK включает эмулятор хранилища hello, программа, которая имитирует hello больших двоичных объектов, очередей и таблиц хранения служб в Azure на локальном компьютере разработчика. При построении облачной службы, которое использует службы хранилища Azure hello или записи внешнего приложения hello, вызовов служб хранилища, возможность тестировать код локально с hello эмулятора хранилища. Управление эмулятор хранилища hello интегрировать Hello Azure Tools для Microsoft Visual Studio в Visual Studio. Средства Azure Hello инициализации hello база данных эмулятора хранилища при первом использовании, запускает hello служба эмулятора хранения при запуске или отладке кода в Visual Studio и предоставляет доступ только для чтения данных эмулятора хранения toohello через hello обозреватель хранилища Azure.

Подробные сведения о hello эмулятор хранилища, включая требования к системе и инструкции по пользовательской настройке, см. [hello использование эмулятора хранилища Azure для разработки и тестирования](storage/common/storage-use-emulator.md).

> [!NOTE]
> Существуют некоторые различия в функциональных возможностях между моделированием эмулятора хранилища hello и служб хранилища Azure hello. В разделе [различия между hello эмулятора хранилища и служб хранилища Azure](storage/common/storage-use-emulator.md) в документации по пакету SDK Azure сведения о различиях hello hello.
> 
> 

## <a name="configuring-a-connection-string-for-hello-storage-emulator"></a>Настройка строки подключения для эмулятора хранилища hello
tooaccess hello эмулятор хранилища из кода в рамках роли, вы будете tooconfigure соединение строку, эмулятор хранилища toohello точек и более поздней версии, который может быть tooan измененные toopoint учетной записи хранилища Azure. Строка подключения — параметр конфигурации, который может быть прочитан ролью в учетной записи хранилища tooa tooconnect среды выполнения. Дополнительные сведения о том, как toocreate строки подключения, в разделе [hello Настройка приложения Azure](https://msdn.microsoft.com/library/azure/2da5d6ce-f74d-45a9-bf6b-b3a60c5ef74e#BK_SettingsPage).

> [!NOTE]
> Может возвращать ссылки учетной записи эмулятора toohello хранилища из кода с помощью hello **DevelopmentStorageAccount** свойство. Такой подход работает корректно, если вы хотите tooaccess hello эмулятор хранилища из кода, но если планируется toopublish tooAzure вашего приложения, может потребоваться toocreate tooaccess строка подключения учетной записи хранилища Azure и изменить toouse ваш код, Строка подключения перед его публикацией. Если вы часто переключаться между учетной записи эмулятора хранилища hello и учетная запись хранилища Azure, строка подключения упростит этот процесс.
> 
> 

## <a name="initializing-and-running-hello-storage-emulator"></a>Инициализация и запуск эмулятора хранилища hello
Можно указать, что при запуске или отладке службы в Visual Studio, Visual Studio автоматически запускает эмулятор хранилища hello. В обозревателе решений откройте контекстное меню hello вашей **Azure** проект и выберите **свойства**. На hello **разработки** hello на вкладке **Запуск эмулятора хранилища Azure** выберите **True** (если он еще не задано значение toothat).

Hello при первом запуске или отладке службы из Visual Studio, hello эмулятор хранилища запустится процесс инициализации. Этот процесс резервирует локальные порты для эмулятора хранилища hello и создает базу данных эмулятора hello. После завершения этого процесса не обязательно toorun снова, если не удалить базу данных эмулятора hello.

> [!NOTE]
> Начиная с выпуска июня 2012 hello hello инструментов Azure, hello эмулятор хранилища работает, по умолчанию в SQL Express LocalDB. В предыдущих версиях служб hello инструментов Azure эмулятор хранилища hello работает на экземпляр по умолчанию SQL Express 2005 или 2008, которой необходимо установить перед установкой hello Azure SDK. Можно также запустить эмулятор хранилища hello для именованного экземпляра SQL Express или именованный или по умолчанию экземпляра Microsoft SQL Server. Найти toorun эмулятора хранения hello tooconfigure от экземпляра, отличного от экземпляра по умолчанию hello в разделе [hello использование эмулятора хранилища Azure для разработки и тестирования](storage/common/storage-use-emulator.md).
> 
> 

Эмулятор хранилища Hello представлены сведения о состоянии hello tooview интерфейса пользователя служб локального хранилища hello и toostart, остановки и сброса их. После запуска служба эмулятора хранения hello можно отображать hello пользовательский интерфейс или запустить или остановить службу hello, щелкнув правой кнопкой мыши значок в области уведомлений hello для hello эмулятор Microsoft Azure в панели задач Windows hello.

## <a name="viewing-storage-emulator-data-in-server-explorer"></a>Просмотр данных эмулятора хранения в обозревателе сервера
Hello узел хранилища Azure в обозревателе серверов позволяет tooview данных и изменения параметров для больших двоичных объектов и данные таблицы в учетные записи хранения, включая hello эмулятор хранилища. Дополнительные сведения см. в статье [Управление ресурсами хранилища BLOB-объектов Azure с помощью обозревателя хранилищ (предварительная версия)](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).

