---
title: "aaaCreate и управлять гибридных подключений | Документы Microsoft"
description: "Узнайте, как управление hello подключения toocreate гибридное подключение и установить hello диспетчер гибридного подключения. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: aac0546b-3bae-41e0-b874-583491a395ea
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: 561d8f3dd97318130a05c3bb2874ee8022e7f417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-hybrid-connections"></a>Создание гибридных подключений и управление ими

> [!IMPORTANT]
> Гибридные подключения BizTalk больше не используются. Они заменены гибридными подключениями службы приложений. Дополнительные сведения, включая toomanage существующего гибридного подключения BizTalk, см. в [гибридные подключения служб приложения Azure](../app-service/app-service-hybrid-connections.md).


## <a name="overview-of-hello-steps"></a>Этапы hello
1. Создайте гибридное подключение, введя hello **имя узла** или **полное доменное имя** hello локального ресурса в частной сети.
2. Свяжите ваш веб-приложениях Azure или Azure мобильных приложений toohello гибридного подключения.
3. Установка hello диспетчера гибридных подключений для локального ресурса и подключение toohello конкретного гибридного подключения. Hello портал Azure предоставляет tooinstall взаимодействие одним щелчком и подключения.
4. Управление гибридными подключениями и их ключами.

В этом разделе перечислены эти действия. 

> [!IMPORTANT]
> Это возможно tooset гибридного подключения конечной точки tooan IP-адрес. При использовании IP-адрес может выполняться или не может связаться hello локального ресурса, в зависимости от клиента. Hello гибридного подключения зависит от клиента hello выполнив поиск в DNS. В большинстве случаев hello **клиента** код вашего приложения. Если hello клиент не выполняет поиск в DNS, (он пытается tooresolve hello IP-адрес как в случае доменного имени (x.x.x.x)), а затем трафик не отправляется через hello гибридного подключения.
> 
> Например, вы задали **10.4.5.6** в качестве локального хоста (это псевдокод):
> 
> **Привет, выполнив сценарий работает:**  
> `Application code -> GetHostByName("10.4.5.6") -> Resolves too127.0.0.3 -> Connect("127.0.0.3") -> Hybrid Connection -> on-prem host`
> 
> **не работает Hello следующие сценарии:**  
> `Application code -> Connect("10.4.5.6") -> ?? -> No route toohost`
> 
> 

## <a name="CreateHybridConnection"></a>Создание гибридного подключения
Гибридное подключение может быть создано в hello портал Azure с помощью веб-приложений **или** с помощью служб BizTalk. 

**toocreate гибридные подключения с помощью веб-приложений**, в разделе [tooan подключения веб-приложениях Azure локального ресурса](../app-service-web/web-sites-hybrid-connection-get-started.md). Также можно установить hello диспетчер гибридного подключения (HCM) из веб-приложения, hello предпочтительный метод. 

**Гибридные подключения в службах BizTalk toocreate**:

1. Войдите в toohello [классический портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. В области навигации слева hello выберите **службы BizTalk** и выберите службу BizTalk. 
   
    Если служба BizTalk отсутствует, можно создать ее с помощью команды [Создать службу BizTalk](biztalk-provision-services.md).
3. Выберите hello **гибридных подключений** вкладки:  
   ![вкладка "Гибридные подключения"][HybridConnectionTab]
4. Выберите **создать гибридное подключение** или выберите hello **добавить** кнопки на панели задач hello. Введите hello следующие данные:
   
   | Свойство | Описание |
   | --- | --- |
   | Имя |Hello гибридного подключения, имя должно быть уникальным и не может быть hello одинаковые имена, как hello службы BizTalk. Можно ввести любое имя, но рекомендуется использовать специальные имена, соответствующие назначению подключения. Примеры таких ошибок: <br/><br/>Payroll*SQLServer*<br/>SupplyList*SharepointServer*<br/>Customers*OracleServer* |
   | Имя компьютера |Введите hello полное доменное имя узла, только имя узла hello, или hello IPv4-адрес локального ресурса hello. Примеры приведены ниже.<br/><br/>mySQLServer<br/>*mySQLServer*.*Domain*.corp.*yourCompany*.com<br/>*myHTTPSharePointServer*<br/>*myHTTPSharePointServer*.*yourCompany*.com<br/>10.100.10.10<br/><br/>При использовании hello IPv4-адрес, обратите внимание, что коде клиента или приложения не может разрешить hello IP-адрес. Hello важно см. Примечание в hello верхней части этого раздела. |
   | Порт |Введите номер порта hello hello локального ресурса. Например если вы используете веб-приложения, введите порт 80 или 443. Если вы используете SQL Server, введите порт 1433. |
5. Выберите настройку hello toocomplete флажок hello. 

#### <a name="additional"></a>Дополнительно
* Можно создать несколько гибридных подключений. В разделе hello [службы BizTalk: выпусков](biztalk-editions-feature-chart.md) для hello допустимое число подключений. 
* Каждое гибридное подключение создается с помощью пары строк подключения: ключи приложений, которые ОТПРАВЛЯЮТ и локальные ключи, которые ПРОСЛУШИВАЮТ. В каждой паре есть первичный и вторичный ключи. 

## <a name="LinkWebSite"></a>Связывание веб-приложения службы приложений Azure или мобильного приложения
Выберите toolink веб-приложения или мобильного приложения в службе приложений Azure tooan существующего гибридного подключения **использование существующего гибридного подключения** в колонке hello гибридных подключений. См. статью [Доступ к локальным ресурсам с помощью гибридных подключений в службе приложений Azure](../app-service-web/web-sites-hybrid-connection-get-started.md).

## <a name="InstallHCM"></a>Установка hello диспетчера гибридных подключений в локальной среде
После создания гибридного подключения установите hello диспетчер гибридного подключения на hello локального ресурса. Его можно скачать из веб-приложения Azure или из службы BizTalk. Действия, выполняемые в службе BizTalk: 

1. Войдите в toohello [классический портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. В области навигации слева hello выберите **службы BizTalk** и выберите службу BizTalk. 
3. Выберите hello **гибридных подключений** вкладки:  
   ![вкладка "Гибридные подключения"][HybridConnectionTab]
4. На панели задач hello, выберите **локальной установки**:  
   ![программу локальной установки][HCOnPremSetup]
5. Выберите **Установка и настройка** toorun или загрузки hello диспетчер гибридного подключения на hello в локальной системе. 
6. При выборе установки hello toostart флажок hello. 

<!--
You can also download hello Hybrid Connection Manager MSI file and copy hello file tooyour on-premises resource. Specific steps:

1. Copy hello on-premises primary Connection String. See [Manage Hybrid Connections](#ManageHybridConnection) in this topic for hello specific steps.
2. Download hello Hybrid Connection Manager MSI file. 
3. On hello on-premises resource, install hello Hybrid Connection Manager from hello MSI file. 
4. Using Windows PowerShell, type: 
> Add-HybridConnection -ConnectionString “*Your On-Premises Connection String that you copied*” 
--> 

#### <a name="additional"></a>Дополнительно
* Диспетчер гибридного подключения может устанавливаться на hello следующие операционные системы:
  
  * Windows Server 2008 R2 (требуются .NET Framework 4.5 или более поздней версии и Windows Management Framework 4.0 или более поздней версии);
  * Windows Server 2012 (требуется Windows Management Framework 4.0 или более поздней версии).
  * Windows Server 2012 R2
* После установки диспетчера гибридных подключений hello происходит hello следующее: 
  
  * Hello гибридного подключения, размещенные в Azure — hello автоматически настроенного toouse строка подключения основного приложения. 
  * Hello локальному ресурсу — автоматически настроенного toouse hello основной строки подключения в локальной среде.
* Hello диспетчер гибридного подключения необходимо использовать строку подключения допустимым локальным для авторизации. Hello Azure веб-приложения и мобильные приложения необходимо использовать строку подключения допустимое приложение для авторизации.
* Гибридные подключения можно масштабировать путем установки другого экземпляра hello диспетчер гибридного подключения на другом сервере. Настройка hello локального прослушивателя toouse hello же адрес в качестве первого локального прослушивателя hello. В этом случае трафик hello — случайно распределенными (циклический перебор) между hello active локальным прослушивателям. 

## <a name="ManageHybridConnection"></a>Управление гибридными подключениями
toomanage гибридных подключений, вы можете:

* Использовать портал Azure hello и перейти tooyour службы BizTalk. 
* Использование интерфейсов [REST API](http://msdn.microsoft.com/library/azure/dn232347.aspx).

#### <a name="copyregenerate-hello-hybrid-connection-strings"></a>Скопируйте или сформируйте hello гибридного подключения
1. Войдите в toohello [классический портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. В области навигации слева hello выберите **службы BizTalk** и выберите службу BizTalk. 
3. Выберите hello **гибридных подключений** вкладки:  
   ![вкладка "Гибридные подключения"][HybridConnectionTab]
4. Выберите hello гибридного подключения. На панели задач hello, выберите **Управление подключением**:  
   ![Управление параметрами][HCManageConnection]
   
    **Управление подключения** списки hello приложения и для локальной строки подключения. Можно скопировать hello строки подключения или повторно создать ключ доступа используются в строке подключения hello hello. 
   
    **При выборе повторно создайте**, hello общий ключ доступа в пределах hello, строка подключения изменилась. Здравствуйте, следующие:
   
   * В hello классический портал Azure, выберите **синхронизация ключей** в hello приложения Azure.
   * Повторно запустите hello **локальной установки**. При повторном выполнении hello локальной установки, приветствия локальных ресурсов будет автоматически настроен toouse hello обновлены основная строка подключения.

#### <a name="use-group-policy-toocontrol-hello-on-premises-resources-used-by-a-hybrid-connection"></a>С помощью групповой политики toocontrol hello локальные ресурсы, используемые гибридного подключения
1. Загрузите hello [диспетчер гибридного подключения административные шаблоны](http://www.microsoft.com/download/details.aspx?id=42963).
2. Извлеките файлы hello.
3. На компьютере hello, изменяет групповой политики hello следующие:  
   
   * Скопируйте hello. Файлов ADMX toohello *%WINROOT%\PolicyDefinitions* папки.
   * Скопируйте hello. ADML файлы toohello *%WINROOT%\PolicyDefinitions\en-us* папки.

После копирования можно использовать редактор групповой политики toochange hello политики.

## <a name="next"></a>Далее
[Подключение веб-приложениях Azure tooan локальных ресурсов](../app-service-web/web-sites-hybrid-connection-get-started.md)  
[Подключение локальной tooon SQL Server из веб-приложения Azure](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)   
[Обзор гибридных подключений](integration-hybrid-connection-overview.md)

## <a name="see-also"></a>См. также
[REST API для управления службами BizTalk в Microsoft Azure](http://msdn.microsoft.com/library/azure/dn232347.aspx)  
[Службы BizTalk: диаграмма выпусков](biztalk-editions-feature-chart.md)  
[Создание службы BizTalk с помощью классического портала Azure](biztalk-provision-services.md)  
[Службы BizTalk: вкладки «Панель мониторинга», «Монитор» и «Масштаб»](biztalk-dashboard-monitor-scale-tabs.md)

[HybridConnectionTab]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionManageConn.png 
