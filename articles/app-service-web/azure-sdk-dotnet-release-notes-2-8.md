---
title: "aaaAzure SDK .NET 2.8 заметки о выпуске"
description: "Заметки о выпуске пакета SDK Azure для .NET 2.8"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: de7207ff-ba4f-4008-9141-8742fcaa3254
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 2722dcdd27bf9ab65b48e91dcdb545536f987dd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-28-281-and-282"></a>Пакеты SDK Azure для .NET 2.8, 2.8.1 и 2.8.2
## <a name="overview"></a>Обзор
В этой статье содержатся заметки о выпуске hello, (, включая известные проблемы и критические изменения) для hello Azure SDK 2.8 .NET, 2.8.1 и 2.8.2 выпусках. 

Полный список новых возможностей и обновлений, внесенные в этом выпуске см. в разделе hello [2.8 Azure SDK для Visual Studio 2013 и Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/) объявления. 

## <a name="azure-sdk-for-net-28"></a>Пакет SDK Azure для .NET 2.8
### <a name="download-azure-sdk-for-net-28"></a>Загрузить пакет SDK Azure для .NET 2.8
[Пакет SDK Azure для .NET 2.8 и Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkId=699285) 

[Пакет SDK Azure для .NET 2.8 и Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkId=699287)

### <a name="net-452-support"></a>Поддержка .NET 4.5.2
#### <a name="known-issues"></a>Известные проблемы
Azure .NET SDK 2.8 позволяет вам toocreate .NET 4.5.2 пакеты облачной службы. Однако .NET 4.5.2 framework не будут устанавливаться на выпуске гостевой ОС изображения до января 2016 г. Гостевая ОС по умолчанию hello. До того момента .NET Framework 4.5.2 можно будет установить только с помощью отдельной версии гостевой ОС — ноябрь 2015-02. В разделе hello [выпуски гостевой ОС Azure и Матрица совместимости пакетов SDK](../cloud-services/cloud-services-guestos-update-matrix.md) tootrack страницы при hello изображения будут выпущены.  После снятия hello ноября 2015-02 изображения можно toouse этот образ путем обновления файла конфигурации (.cscfg) файл облачной службы. В конфигурации службы hello файл задать атрибут osVersion hello строки toohello элемент ServiceConfiguration hello «WA-ГОСТЯ-OS-4.26_201511-02». Если выбрать tooopt в toouse этот образ будет больше не получить toohello автоматических обновлений гостевой ОС. необходимо задать автоматическое обновление hello tooget hello osVersion слишком «*» и .NET 4.5.2 будут доступны только через автоматические обновления в январе 2016 г.

### <a name="azure-data-factory"></a>Фабрика данных Azure
#### <a name="known-issues"></a>Известные проблемы
Во время **шаблон фабрики данных** проект создания связанные с образцом данных, а azure сценарий PowerShell, может произойти ошибка azure power shell версии установленных на компьютере hello после 0.9.8.

В порядке toosuccessfully создание этого типа проекта, необходимо установить [azure power shell версии 0.9.8](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi).

### <a name="azure-resource-manager-tools"></a>Средства диспетчера ресурсов Azure
#### <a name="breaking-changes"></a>Критические изменения
в этот выпуск toowork с помощью новых командлетов Azure PowerShell версии 1.0 hello был обновлен Hello сценария PowerShell, предоставленного hello проекта группы ресурсов Azure.  Этот новый скрипт будет недоступны из Visual Studio при использовании версии too2.8 предыдущий пакет SDK для hello.  

Скрипты из проектов, созданных в более ранних версиях пакета SDK для hello не будет выполняться из среды Visual Studio при с помощью пакета SDK 2.8 "hello".  Все сценарии продолжит toowork вне Visual Studio с соответствующей версии hello hello командлетов Azure PowerShell.  

Hello 2,8 SDK требует наличия hello командлетов Azure PowerShell версии 1.0.  Всем другим версиям hello SDK требуется версия 0.9.8 hello командлетов Azure PowerShell.  Дополнительную информацию см. в [этом](http://go.microsoft.com/fwlink/?LinkID=623011) блоге.

### <a name="web-tools-extensions"></a>Расширения веб-инструментов
#### <a name="known-issues"></a>Известные проблемы
Hello следующие известные проблемы будут учтены в hello после выпуска.

* Жест облака и обозревателя серверов, связанных с облачной службой, не работает с нерабочими средами (например, с клиентами Azure China или Azure Stack). Для клиентов в этих затронутых областях загрузка hello публикации профиля из hello портал Azure будет включена возможность публикации. В будущей версии такие жесты, как подключение отладчика и просмотр журналов потоковой передачи, будут исправлены и станут доступны для клиентов Azure China и Stack. 
* Клиенты могут возникнуть ошибки во время создания, если подробные сведения о приложении hello экземпляра toowhich, они развертываются находится в регионе, отличном от Восток США службы приложений. В этих сценариях, созданию приложения службы в портале hello и скачивание hello публикации профиль включит сценариев публикации. 

### <a name="azure-hdinsight-tools"></a>Средства Azure HDInsight
#### <a name="new-updates"></a>Новые обновления
* Можно выполнить запрос Hive в кластере hello через HiveServer2 с почти отсутствие дополнительных расходов на и см. задания hello журналы в режиме реального времени.
* С помощью hello новый Hive задач представление выполнения можно детализировать задание глубокого анализа, получить дополнительные сведения и идентификации потенциальных проблем.

Чтобы узнать больше, ознакомьтесь с [пакетом SDK Azure 2.8 для Visual Studio 2013 и Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/). 

## <a name="azure-sdk-for-net-281"></a>Пакет SDK Azure для .NET 2.8.1
### <a name="known-issues-for-visual-studio-2013-and-visual-studio-2015"></a>Известные проблемы в Visual Studio 2013 и Visual Studio 2015
1. Инициированные веб-задания публикует tooslots будет отображать и ошибки и не будет набор расписания, но он будет передавать tooAzure hello веб-задания. Пользователям, которым необходимы запланированное задание можно использовать tooset портала Azure hello настроить расписание hello для hello веб-задания. 
2. Клиенты, использующие Python, могут столкнуться с проблемами отладчика. Вводит команды службы исправления для этого, но если подвержены, пожалуйста, сообщите корпорации Майкрософт известно форумах hello, или в блоге объявления hello или разделе комментариев заметки о выпуске. 
3. Клиенты в определенных регионах (например, Южной Индии) могут столкнуться с ошибками подготовки службы приложений. Это согласуется с портала hello и при возникновении этой проблемы можно использовать hello Azure портала toorequest доступа toopublish toothese географических регионов. После они запрашивают toothese области доступа, с помощью портала Azure подготовки hello должна работать. 

## <a name="azure-sdk-for-net-282"></a>Пакет Azure SDK для .NET 2.8.2
После установки средств hello 2.8.2 hello можно столкнуться hello следующие проблемы.         

* Если вы используете Windows 10 и Internet Explorer не установлен, может появиться ошибка "Internet Explorer не найден".
  tooresolve hello проблему, установите Internet Explorer с помощью hello Add/Remove диалоговое окно компоненты Windows.

Если вы заметили, эту проблему, используйте tooreport функции hello отправки в смайлик его.

Дополнительную информацию см. в [этой](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-2-for-net/) записи.

## <a name="other-updates"></a>Другие обновления
О других изменениях читайте в [публикации о пакете SDK Azure 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).

## <a name="also-see"></a>См. также:
[Объявление о пакете SDK Azure 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)

[Поддержка и сведения о требованиях для hello Azure SDK для .NET и API-интерфейсы](https://msdn.microsoft.com/library/azure/dn479282.aspx)

