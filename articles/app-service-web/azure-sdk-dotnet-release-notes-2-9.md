---
title: "aaaAzure SDK .NET 2.9 заметки о выпуске"
description: "Заметки о выпуске пакета SDK для Azure для .NET 2.9"
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
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a>Заметки о выпуске пакета Azure SDK для .NET 2.9

В этой статье содержатся заметки о выпуске для версий 2.9 и 2.9.6 пакета Azure SDK для .NET.

##<a name="azure-sdk-for-net-296-release-summary"></a>Сведения о выпуске Azure SDK для .NET 2.9.6

Дата выпуска: 16.11.2016
 
В этом выпуске были введены нет критические изменения toohello Azure SDK 2.9. Имеется также tooleverage нет необходимости процесса обновления этот пакет SDK с существующие проекты облачной службы.

### <a name="visual-studio-2017-release-candidate"></a>релиз-кандидат Visual Studio 2017

- В Visual Studio RC 2017 г. Этот выпуск hello Azure SDK для .NET встроенная hello Azure рабочей нагрузки. Все hello инструменты разработки Azure toodo будет входить в состав Visual Studio 2017 г. версия-кандидат Забегая вперед. Для Visual Studio 2015 и Visual Studio 2013 hello SDK по-прежнему доступны через WebPI. Когда Visual Studio 2017 будет выпущен в качестве конечного продукта, версии пакета Azure SDK для .NET больше не будут доступны для Visual Studio 2013. Следуйте этой связи toodownload версии-Кандидата Visual Studio 2017 г.: https://www.visualstudio.com/vs/visual-studio-2017-rc/

### <a name="azure-diagnostics"></a>Диагностика Azure

- Измененные hello поведение tooonly хранить частичную строку соединения с ключом hello заменяется маркер для строки подключения к хранилищу диагностики облачных служб. ключ фактического хранения Hello теперь хранится в папке профиля пользователя hello, можно контролировать доступ к нему. Visual Studio прочитает hello ключ хранилища из папке профиля пользователя для локальной отладки и процесс публикации. 
- В ответ toohello изменений, описанных выше Visual Studio Online team улучшенные hello шаблона задачи развертывания облачных служб Azure, пользователи могут указать hello ключ хранилища для настройки расширения системы диагностики при публикации tooAzure в непрерывной интеграции и развертывания.
- Мы уже сделали возможных toostore строку безопасного соединения и разметки для Azure Diagnostics (WAD), toohelp через environements устранить проблемы с конфигурацией.
 
### <a name="windows-server-2016-virtual-machines"></a>Виртуальные машины Windows Server 2016

- Visual Studio теперь поддерживает развертывание облачных служб tooOS семейство 5 (Windows Server 2016) виртуальных машин. Для существующих облачных служб можно изменить ваш tootarget параметры hello новое семейство ОС. Если при создании новых облачных служб, выберите службу hello toocreate, с помощью .net 4.6 или более поздней версии, то по умолчанию hello службы toouse 5 семейства ОС.  Дополнительные сведения можно просмотреть hello [семейства гостевых ОС поддерживает таблицу](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).

#### <a name="known-issues"></a>Известные проблемы

- Ограничение, и блокирует развертывание проектов, с помощью tooany платформ (таких как .NET 4.6) не поддерживается .NET семейства ОС появился Azure .NET SDK 2.9.6 < 5. Обходной путь описан [здесь](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).

 
### <a name="azure-in-role-cache"></a>Кэш роли Azure 

- Поддержка кэша роли Azure закончилась 30 ноября 2016 года. Дополнительные сведения см. [здесь](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).

### <a name="azure-resource-manager-templates-for-azure-stack"></a>Шаблоны Azure Resource Manager для Azure Stack

- Мы представляем Azure Stack как целевой объект развертывания для шаблонов Azure Resource Manager.


## <a name="azure-sdk-for-net-29-summary"></a>Сводка о пакете Azure SDK для .NET 2.9

## <a name="overview"></a>Обзор
Этот документ содержит заметки о выпуске hello для hello Azure SDK для .NET 2.9 выпуска. 

Подробные сведения об обновлениях в этом выпуске см. в разделе hello [post объявления Azure SDK 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a>Azure SDK 2.9 для Visual Studio 2015 с обновлением 2 и Visual Studio "15" (предварительная версия)
Это обновление содержит следующие исправления hello.

* Выдача связанные tooREST создание клиента API в в какой строке hello «Неизвестный тип» будет отображаться как hello имя папки генерация кода hello и/или hello имя пространства имен hello в hello созданный код.
* Выполните веб-задания связанных tooScheduled строя сведения о проверке подлинности в какой hello toobe передан процесса подготовки toohello планировщика.

Это обновление содержит следующие новые функции hello.

* Поддержка дополнительного приложения служб на вкладке «Службы» Привет hello диалоговое окно подготовки службы приложений. 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a>Средства озера данных Azure для Visual Studio 2015 с обновлением 2
Это обновление включает hello следующие:

* **Инструменты Azure Озера данных** для Visual Studio теперь объединены в hello Azure SDK для .NET версии. Программа Hello автоматически устанавливается при установке пакета SDK Azure. 
  
    Средство Hello часто обновляется, переход [здесь](http://aka.ms/datalaketool) tooget hello обновлений.
* **Обозреватель серверов** теперь позволяет tooview все и создать некоторые сущности метаданных U-SQL. Дополнительную информацию см. в [этом](https://azure.microsoft.com/documentation/services/data-lake-analytics/) блоге.

## <a name="hdinsight-tools"></a>Средства HDInsight
**Средства HDInsight** для Visual Studio теперь поддерживают HDInsight версии 3.3, включая показ графики Tez и другие языковые исправления.

## <a name="azure-resource-manager"></a>Диспетчер ресурсов Azure
В этом выпуске добавлена поддержка [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) для шаблонов Resource Manager.

## <a name="see-also"></a>Дополнительные материалы
[Объявление о пакете SDK Azure 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

