---
title: "aaaIssuer имя и ключ поставщика в службах BizTalk | Документы Microsoft"
description: "Дополнительные сведения о том, как tooretrieve имя издателя и ключ издателя для шины обслуживания или управления доступом (ACS) в службах BizTalk. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a>Службы BizTalk: имя и ключ издателя

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Службы BizTalk Azure использует hello имя издателя шины обслуживания и ключ издателя и hello имя издателя контроля доступа и ключ издателя. В частности:

| Задача | Используемые имя и ключ издателя |
| --- | --- |
| Развертывание приложения из Visual Studio |Имя и ключ издателя для службы Access Control |
| Настройка hello портале служб BizTalk Azure |Имя и ключ издателя для службы Access Control |
| Создание ретрансляции больших двоичных ОБЪЕКТОВ с hello службы адаптера BizTalk в Visual Studio |Имя и ключ издателя шины обслуживания |

В этом разделе перечислены hello действия tooretrieve hello имя издателя и ключ издателя. 

## <a name="access-control-issuer-name-and-issuer-key"></a>Имя и ключ издателя для службы Access Control
Hello имя издателя контроля доступа и ключ издателя используются hello следующее:

* Приложение службы Azure BizTalk, созданных в Visual Studio: toosuccessfully развернуть приложение службы BizTalk в Visual Studio tooAzure, введите имя издателя контроля доступа hello и ключ издателя. 
* Hello портале служб BizTalk Azure: при создание службы BizTalk откройте hello портале служб BizTalk, имя издателя управления доступом и ключ издателя автоматически регистрируются для развертываний с hello одинаковые значения для управления доступом.

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a>Получить hello имя издателя контроля доступа и ключ издателя

toouse ACS для проверки подлинности и get Здравствуйте значения имени издателя и ключ издателя, hello общие шаги включают:

1. Установка hello [командлетов Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
2. Добавьте учетную запись Azure: `Add-AzureAccount`.
3. Получите имя подписки: `get-azuresubscription`.
4. Выберите свою подписку: `select-azuresubscription <name of your subscription>`. 
5. Создайте пространство имен: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`.

    Пример:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`
      
5. Когда создается новое пространство имен ACS hello (это может занять несколько минут), hello имя издателя и ключ издателя значения перечислены в строке подключения hello: 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

toosummarize:  
имя издателя — SharedSecretIssuer;  
ключ издателя — SharedSecretKey.

Подробнее об hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) командлета. 

## <a name="service-bus-issuer-name-and-issuer-key"></a>Имя и ключ издателя шины обслуживания
Имя и ключ издателя шины обслуживания используются службами адаптера BizTalk. В проекте службы BizTalk в Visual Studio используйте Line of Business (LOB) hello службы адаптера BizTalk tooconnect tooan в локальной системе. tooconnect, создать hello посредника LOB и введите свои данные системы LOB. При этом также введите имя издателя шины обслуживания hello и ключ издателя.

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a>hello tooretrieve имя издателя шины обслуживания и ключ издателя
1. Войдите в toohello [классический портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. В области навигации слева hello выберите **Service Bus**.
3. Выберите пространство имен. На панели задач hello, выберите **сведения о соединении**. При этом отображаются hello **поставщика по умолчанию** (имя поставщика) и **ключ по умолчанию** (ключ). Эти значения можно скопировать.  

toosummarize:  
Имя издателя = издатель по умолчанию  
Ключ издателя = ключ по умолчанию

## <a name="next"></a>Далее
Дополнительная информация о службах BizTalk в Azure

* [Установка пакета SDK служб BizTalk Azure hello](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Руководства по службам BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [Как я запустить с помощью hello пакета SDK служб BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Службы BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>См. также
* [Как: использование службы управления ACS tooConfigure удостоверения службы](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [Службы BizTalk. Диаграмма выпусков Developer, Basic, Standard и Premium](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [Службы BizTalk: подготовка с использованием классического портала Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [Службы BizTalk. Диаграмма состояния подготовки](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [Службы BizTalk: вкладки «Панель мониторинга», «Монитор» и «Масштаб»](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [Службы BizTalk: резервное копирование и восстановление](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [Службы BizTalk: регулирование](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

