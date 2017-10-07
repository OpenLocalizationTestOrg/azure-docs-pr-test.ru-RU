---
title: "заметки о aaaRelease для служб BizTalk Azure | Документы Microsoft"
description: "Hello перечислены известные проблемы для служб BizTalk Azure"
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: f4906fdc-4cd9-4a57-a007-a88c2e51a18f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: ea53d6c40ed58badf4141453dc77d28dcfc6407f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-biztalk-services"></a>Заметки о выпуске служб Azure BizTalk

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

заметки о выпуске Hello для служб BizTalk Microsoft Azure hello содержат известные проблемы в этом выпуске hello.

## <a name="whats-new-in-hello-november-update-of-biztalk-services"></a>Новые возможности hello ноябрьским обновлением служб BizTalk
* Можно включить шифрование при хранении в hello портале служб BizTalk. Ознакомьтесь с разделом [Включение шифрование в местах хранения на портале служб BizTalk](https://msdn.microsoft.com/library/azure/dn874052.aspx).

## <a name="update-history"></a>Журнал обновлений
### <a name="october-update"></a>Октябрьское обновление
* Поддержка учетных записей организации  
  * **Сценарий**. Вы зарегистрировали развернутую службу BizTalk с помощью учетной записи Майкрософт (например, user@live.com). В этом сценарии только учетной записи Майкрософт, пользователи могут управлять hello службы BizTalk с помощью портала служб BizTalk hello. Учетную запись организации для этого использовать нельзя.  
  * **Сценарий**. Вы зарегистрировали развернутую службу BizTalk с помощью учетной записи организации в Azure Active Directory (например, user@fabrikam.com или user@contoso.com). В этом сценарии только пользователи Azure Active Directory в пределах одной организации могут управлять приветствия hello службы BizTalk с помощью портала служб BizTalk hello. Учетную запись Майкрософт для этого использовать нельзя.  
* При создании службы BizTalk в hello классического портала Azure вы автоматически регистрируется в hello портале служб BizTalk.
  * **Сценарий**: вход в hello классический портал Azure, создайте службу BizTalk, а затем выберите **управление** для hello первый раз. При открытии портала служб BizTalk hello hello службы BizTalk автоматически регистрирует и готов для развертываний.  
    В разделе [регистрация и обновление развертывания службы BizTalk на портале служб BizTalk Здравствуйте,](https://msdn.microsoft.com/library/azure/hh689837.aspx).  

### <a name="august-14-update"></a>Обновление от 14 августа
* Соглашения и мост разделения — торговых партнеров соглашения и мосты теперь привязано в hello портале служб BizTalk. Теперь вы создания соглашения и мосты отдельно и в мосты среды выполнения разрешения tooan соглашение на основании значений hello в приветственное сообщение EDI. Ознакомьтесь со статьями [Создание соглашений в службах Azure BizTalk](https://msdn.microsoft.com/library/azure/hh689908.aspx), [Создание моста EDI с помощью портала служб BizTalk](https://msdn.microsoft.com/library/azure/dn793986.aspx), [Создание моста AS2 с помощью портала служб BizTalk](https://msdn.microsoft.com/library/azure/dn793993.aspx) и [Разрешение мостов в соглашения во время выполнения](https://msdn.microsoft.com/library/azure/dn794001.aspx).  
* Hello параметр toocreate шаблонов для соглашений больше не поддерживается.  
* Для соглашение на стороне отправителя hello теперь можно указать разные наборы разделителей для каждой схемы. Эта конфигурация задается в разделе параметров протокола для соглашения отправляющей стороны. Дополнительные сведения см. в статьях [Создание соглашения X12 в службах BizTalk Azure](https://msdn.microsoft.com/library/azure/hh689847.aspx) и [Создание соглашения EDIFACT в службах BizTalk Azure](https://msdn.microsoft.com/library/azure/dn606267.aspx). Toohello TPM OM API для hello также добавляются две новые сущности той же цели. Ознакомьтесь с разделами [X12DelimiterOverrides](https://msdn.microsoft.com/library/azure/dn798749.aspx) и [EDIFACTDelimiterOverride](https://msdn.microsoft.com/library/azure/dn798748.aspx).  
* Теперь поддерживаются стандартные конструкции XSD, включая производные типы. Ознакомьтесь с разделами [Использование стандартных конструкций XSD в картах](https://msdn.microsoft.com/library/azure/dn793987.aspx) и [Использование производных типов в сценариях и примерах сопоставлений](https://msdn.microsoft.com/library/azure/dn793997.aspx).  
* AS2 поддерживает новые алгоритмы MIC для подписи сообщений и новые алгоритмы шифрования. Ознакомьтесь с разделом [Создание соглашения AS2 в службах Azure BizTalk](https://msdn.microsoft.com/library/azure/hh689890.aspx).  
  ## <a name="know-issues"></a>Известные проблемы.

### <a name="connectivity-issues-after-biztalk-services-portal-update"></a>Проблемы подключения после обновления портала служб BizTalk
  Если у вас есть Привет открыть портал служб BizTalk, при обновлении служб BizTalk tooroll в изменяет toohello службы, могут появиться проблемы подключения hello портале служб BizTalk.  
  Чтобы избежать этого может перезапустить браузер hello, удалить кэш браузера hello или запустить портал hello в частном режиме.  

### <a name="visual-studio-ide-cannot-locate-hello-artifact-if-you-click-an-error-or-warning-in-a-biztalk-services-project"></a>Интегрированная среда разработки Visual Studio не удается найти hello артефакта, если щелкнуть ошибку или предупреждение в проекте служб BizTalk
Установите hello Visual Studio 2012 обновление 3 версии-Кандидата 1 toofix hello проблему.  

### <a name="custom-binding-project-reference"></a>Ссылки на проект пользовательской привязки
Рассмотрим следующие ситуации с проектом служб BizTalk в решении Visual Studio hello.  

* В Здравствуйте одного решения Visual Studio, проект служб BizTalk и настраиваемый проект привязки. Hello проекта службы BizTalk содержит файл ссылки toothis пользовательской привязки проекта.
* Hello проекта службы BizTalk имеет ссылку tooa настраиваемой привязки/поведения DLL.

«Построение» вы успешно hello решения в Visual Studio. Затем «Перестроить» или «Очистить» решение hello. После этого при перестроения или очистки снова hello следующие возникает ошибка:  
  Файл не удается toocopy <Path tooDLL> too"bin\Debug\FileName.dll». процесс Hello hello файл «bin\Debug\FileName.dll» недоступен, так как он используется другим процессом.  

#### <a name="workaround"></a>Возможное решение
* Если [Visual Studio 2012 с обновлением 3](https://www.microsoft.com/download/details.aspx?id=39305) будет установлен, у вас есть hello следующих двух вариантов:
  
  * перезапустить Visual Studio;
  * Перезапустите решение hello. Затем можно выполните только построение решения hello.  
* Если [Visual Studio 2012 с обновлением 3](https://www.microsoft.com/download/details.aspx?id=39305) — не установлена, откройте диспетчер задач, щелкните вкладку "процессы" hello, выберите процесс MSBuild.exe hello и нажмите кнопку hello завершить процесс.  

### <a name="routing-toobasichttprelay-endpoints-is-not-supported-from-bridges-and-biztalk-services-portal-if-non-printable-characters-are-promoted-as-http-headers"></a>Маршрутизация tooBasicHttpRelay конечные точки не поддерживается из мостов и портале служб BizTalk Если непечатаемые символы передаются как заголовки HTTP
При использовании непечатаемые символы как часть свойств с повышенным уровнем для сообщений, эти сообщения не может быть перенаправленное toorelay назначения, использующие привязку BasicHttpRelay hello. Кроме того hello распространяемых свойств, доступных как часть отслеживания, URL-адреса для больших двоичных объектов и без кодировки для назначений.  

### <a name="mdn-is-sent-asynchronously-even-if-hello-send-asynchronous-mdn-option-is-unchecked"></a>MDN отправляется асинхронно, даже если hello отправлять асинхронные MDN не установлен
Рассмотрим следующий сценарий – при выборе hello **отправлять асинхронные MDN** флажок и укажите URL-адрес toosend hello асинхронные MDN и отмените выбор hello **отправлять асинхронные MDN** флажок снова hello MDN по-прежнему URL-адрес указан в toohello отправленные, несмотря на то, что не выбран hello параметр toosend асинхронных MDN.  
Чтобы избежать этого, необходимо очистить hello указан URL-адрес перед снятием hello **отправлять асинхронные MDN** флажок, а затем развернуть соглашение hello AS2.  

### <a name="whitespace-characters-beyond-a-valid-interchange-cause-an-empty-message-toobe-sent-toohello-suspend-endpoint"></a>Символы пробела вне допустимого обмена вызывают пустое сообщение отправлено toobe toohello приостановки конечной точки
Если обнаруживаются сегмента IEA, hello дизассемблер воспринимает это как конец текущего обмена и рассматривает hello следующий ряд пробелов как следующее сообщение. Поскольку это Недопустимый обмен, вы заметите, что одно успешное сообщение отправляется toohello назначение маршрутизации, а одно пустое сообщение отправляется hello приостановить конечной точки.  

### <a name="tracking-in-biztalk-services-portal"></a>Отслеживание на портале служб BizTalk
События отслеживания записываются toohello обработки сообщений EDI и любой корреляции. Если сообщение не за пределами hello этапе протокола, отслеживание будет отображаться как успешное. В этой ситуации см. раздел ЖУРНАЛА toohello под hello **сведения** столбца в **отслеживания** сведения об ошибке.
Hello X12 параметров получения и отправки ([X12 создайте соглашение в службах BizTalk Azure](https://msdn.microsoft.com/library/azure/hh689847.aspx)) предоставляют сведения о hello этапе протокола.  

### <a name="update-agreement"></a>Соглашение обновления
Hello портале служб BizTalk можно toomodify hello квалификатор идентификатора при настройке соглашения. Это может привести к несоответствию свойств. Например имеется соглашение с квалификатором zz: 1234567 и zz: 7654321 hello квалификатор. В параметрах профиля hello портале служб BizTalk измените квалификатором zz: 1234567 toobe 01:ChangedValue. Откройте соглашение hello и 01:ChangedValue отображается вместо квалификатором zz: 1234567.
Обновить toomodify hello квалификатор идентификатора, соглашение hello delete, **удостоверения** в hello профиль партнера, а затем повторно создайте соглашение hello.  

> AZURE.WARNING. Это поведение влияет на X12 и AS2.  
> 
> 

### <a name="as2-attachments"></a>Вложения AS2
Вложения в сообщения AS2 не поддерживаются в операциях отправки или получения. В частности вложения игнорируются без уведомления и тело сообщения hello обрабатывается как обычное сообщение AS2.  

### <a name="resources-remembering-path"></a>Ресурсы: запоминание пути
При добавлении **ресурсов**, hello диалоговое окно может не помнить путь, использованный ранее hello tooadd ресурса. tooremember hello ранее использовавшийся путь, попытайтесь добавить веб-сайт портала служб BizTalk hello слишком**надежных узлов** в Internet Explorer.  

### <a name="if-you-rename-hello-entity-name-of-a-bridge-and-close-hello-project-without-saving-changes-opening-hello-entity-again-results-in-an-error"></a>При переименовании hello имя сущности моста и закрыть hello проект без сохранения изменений, снова открыть hello объекта приводит к возникновению ошибки
Рассмотрим сценарий в hello последовательностью.  

* Добавление моста (например односторонний мост XML) tooa проекта службы BizTalk  
* Переименуйте hello моста, указав значение для hello свойство имени сущности. Будет переименован hello связанный brigeconfig-файл с указанным именем hello.  
* Закройте hello BCS-файл (закрыв вкладку hello в Visual Studio) без сохранения изменений hello.  
* Снова откройте BCS-файл hello из hello в обозревателе решений.  
  Обратите внимание, что хотя hello связанный brigeconfig-файл имеет указанное имя нового hello, hello имя сущности в область конструирования hello по-прежнему hello старое имя. При попытке hello tooopen конфигурации моста, дважды щелкните компонент моста hello, вы получаете hello следующая ошибка:  
  `‘<old name>’ Entity’s associated file ‘<old name>.bridgeconfig’ does not exist`tooavoid, работающие в этом сценарии обязательно сохраняйте изменения после переименования сущностей hello в проекте службы BizTalk.  
  
### <a name="biztalk-service-project-builds-successfully-even-if-an-artifact-has-been-excluded-from-a-visual-studio-project"></a>Построение проекта службы BizTalk выполняется успешно, даже если артефакт исключен из проекта Visual Studio
Рассмотрим сценарий, где добавить tooa артефакта (например, XSD-файл) проекта службы BizTalk, включается в конфигурацию моста hello (например, путем задания его в качестве типа сообщения-запроса) и затем исключить его из проекта Visual Studio hello. В этом случае сборка проекта hello будет не возникнут ошибки, при условии, что удален hello артефакт доступен на диске hello в hello то расположение, из которого он был включен в проект Visual Studio hello.
  
### <a name="hello-biztalk-service-project-does-not-check-for-schema-availability-while-configuring-hello-bridges"></a>Hello проекта службы BizTalk не проверяет доступность схемы при настройке мостов hello
В проекте службы BizTalk Если схему, которая добавляется в проект toohello импортирует другую схему, hello проекта службы BizTalk не проверяет добавляется ли импортированная схема hello toohello проекта. При попытке toobuild такой проект, не получают все ошибки сборки.
  
### <a name="hello-response-message-for-a-xml-request-reply-bridge-is-always-of-charset-utf-8"></a>всегда является приветственное сообщение ответа для моста запрос-ответ XML в кодировке UTF-8
В этом выпуске charset hello объекта hello ответное сообщение от моста запрос-ответ XML всегда имеет значение tooUTF-8.
  
### <a name="user-defined-datatypes"></a>Определяемые пользователем типы данных
адаптеры Hello пакет адаптера BizTalk в функции hello службы адаптера BizTalk может использовать определяемые пользователем типы данных для операций адаптера.
При использовании определяемых пользователем типов данных, скопируйте файлы (.dll) hello toodrive:\Program Files\Microsoft BizTalk Adapter Service\BAServiceRuntime\bin\ или toohello глобальный кэш сборок (GAC) на сервере hello hello службы адаптера BizTalk службы. В противном случае на приветствия клиента может возникнуть следующая ошибка hello:  
```
<s:Fault xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
<faultcode>s:Client</faultcode>
<faultstring xml:lang="en-US">hello UDT with FullName "File, FileUDT, Version=Value, Culture=Value, PublicKeyToken=Value" could not be loaded. Try placing hello assembly containing hello UDT definition in hello Global Assembly Cache.</faultstring>
<detail>
  <AFConnectRuntimeFault xmlns="http://Microsoft.ApplicationServer.Integration.AFConnect/2011" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <ExceptionCode>ERROR_IN_SENDING_MESSAGE</ExceptionCode>
  </AFConnectRuntimeFault>
</detail>
</s:Fault>
```  
  
> [!IMPORTANT]
> Это рекомендуемый toouse GACUtil.exe tooinstall файла в глобальный кэш сборок hello. GACUtil.exe документы как toouse этот инструмент и hello параметры командной строки Visual Studio.  
> 
> 

### <a name="restarting-hello-biztalk-adapter-service-web-site"></a>Перезапуск hello веб-сайт службы адаптера BizTalk
Установка hello **среда выполнения службы адаптера BizTalk*** создает hello **службы адаптера BizTalk** веб-сайта в IIS, которая содержит hello **BAService** приложения. **BAService** приложения внутренним образом использует reach hello tooextend привязки ретрансляции облака toohello конечной точки службы в локальной среде. Для службы, размещенной локально hello, соответствующая конечная точка ретрансляции будет зарегистрирована в hello Service Bus только тогда, когда hello локального запуска службы.  

Если остановить и запустить приложение hello конфигурация для автозапуска приложения соблюдаться не будет. Поэтому если **BAService** будет остановлена, вы всегда должны перезапускать hello **службы адаптера BizTalk** вместо веб-сайт. Запуск или остановка не hello **BAService** приложения.

### <a name="special-characters-should-not-be-used-for-address-and-entity-names-of-lob-components"></a>В адресах и именах сущностей бизнес-компонентов не следует применять специальные символы
Не рекомендуется использовать специальные символы в адресах и именах сущностей бизнес-компонентов. Если сделать это, вы получите ошибку при развертывании hello проекта службы BizTalk. Некоторые символы, такие как «%», веб-сайта службы адаптера BizTalk hello может перейти в остановленном состоянии и будет иметь toomanually запустите ее.

### <a name="test-map-with-get-context-property"></a>Тестирование сопоставления с получением контекстного свойства
Если файл преобразования содержит операцию сопоставления **свойства получения контекста**, то **тестирование сопоставления** завершится ошибкой. Для временного решения проблемы, замените hello **получение свойства контекста** операции сопоставления с операция объединения строк карты с фиктивными данными. Это заполнит целевую схему hello и позволит выполнить тестирование остальной функциональности преобразования.

### <a name="test-map-property-does-not-display"></a>Не отображается свойство тестирования сопоставления
Hello **тестового сопоставления** свойства не отображаются в Visual Studio. Это может произойти, если hello **свойства** окна и hello **обозревателе решений** не закреплены одновременно. tooresolve hello, закрепление **свойства** и hello **обозревателе решений** windows.  

### <a name="datetime-reformat-drop-down-is-grayed-out"></a>Неактивен раскрывающийся список переформатирования типа DateTime
При добавлении операция сопоставления переформатировать DateTime toohello разработать hello поверхности и настроен, формат может быть неактивен раскрывающегося списка. Это может произойти, если hello экрана компьютера установлен **средний — 125%** или **больше — 150%**. tooresolve, значение hello отображение слишком**мелкий — 100% (по умолчанию)** с помощью hello шаги:  

1. Откройте hello **панели управления** и нажмите кнопку **оформление и персонализация**.
2. Откройте элемент **Экран**.
3. Выберите **Небольшой — 100% (по умолчанию)** и нажмите кнопку **Применить**.

Hello **формат** раскрывающегося списка теперь должен работать соответствующим образом.

### <a name="duplicate-agreements-in-hello-biztalk-services-portal"></a>Повторяющиеся соглашения в hello портале служб BizTalk
Рассмотрим следующие сценарии hello.

1. Создайте соглашение с помощью API OM hello между торговыми партнерами.
2. Откройте соглашение hello в hello портале служб BizTalk в двух разных вкладках.
3. Развертывание соглашения hello из обеих вкладок hello.
4. Поэтому оба соглашения hello развертывания на повторяющиеся записи в hello портале служб BizTalk

**Возможное решение**. Откройте один из повторяющихся соглашений hello в hello портале служб BizTalk и отменить развертывание.  

### <a name="bridges-do-not-use-updated-certificate-even-after-a-certificate-has-been-updated-in-hello-artifact-store"></a>Мосты не используют обновленные сертификаты даже в том случае, после обновления сертификата в хранилище артефактов hello
Рассмотрим следующие сценарии hello.  

**Сценарий 1: Использование сертификаты на основе отпечатка для защиты передачи сообщений из конечной точки службы tooa моста**  
Рассмотрим ситуацию, когда в своем проекте службы BizTalk вы используете сертификаты на основе отпечатков. Обновить сертификат hello в портале служб BizTalk hello hello таким же именем, но другого отпечатка, но не обновлять hello проекта службы BizTalk, соответствующим образом. В таком сценарии мост hello может по-прежнему сообщений hello tooprocess поскольку hello старые данные сертификата еще могут находиться в кэш каналов hello. После этого происходит сбой обработки сообщений.  

**Инструкции по решению**: обновить сертификат hello в hello проекта службы BizTalk и повторно развернуть проект hello.  

**Сценарий 2: Использование поведения на основе имени tooidentify сертификатов для защиты передачи сообщений от конечной точки службы tooa моста**

Рассмотрим сценарий, где используется поведение на основе имени tooidentify сертификаты в проекте службы BizTalk. Обновить сертификат hello в hello портале служб BizTalk, но не обновить hello проекта службы BizTalk, соответствующим образом. В таком сценарии мост hello может по-прежнему сообщений hello tooprocess поскольку hello старые данные сертификата еще могут находиться в кэш каналов hello. После этого происходит сбой обработки сообщений.  

**Инструкции по решению**: обновить сертификат hello в hello проекта службы BizTalk и повторно развернуть проект hello.  

### <a name="bridges-continue-tooprocess-messages-even-when-hello-sql-database-is-offline"></a>Мосты продолжить tooprocess сообщения, даже в том случае, если база данных SQL hello находится в автономном режиме
Hello мостов служб BizTalk продолжить tooprocess сообщения на некоторое время, даже если hello Microsoft Azure SQL Database (где хранятся hello под управлением сведения, такие как развернутые артефакты и конвейеры) находится в автономном режиме. Это так, как службы BizTalk использует hello кэшированные артефакты и конфигурацию мостов.
Если не требуется tooprocess мосты hello сообщения при hello базы данных SQL в автономном режиме, можно воспользоваться toostop командлеты PowerShell служб BizTalk hello или приостановить hello службы BizTalk. В разделе [пример управления службой BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=329019) для операций toomanage командлеты Windows PowerShell hello.  

### <a name="reading-hello-xml-message-within-a-bridges-custom-code-component-includes-an-extra-bom-character"></a>Чтение приветственное сообщение XML в компоненте настраиваемого кода моста содержит лишний символ BOM
Рассмотрим сценарий, где требуется tooread сообщение XML в настраиваемом коде моста. При использовании hello .NET API System.Text.Encoding.UTF8.GetString(bytes) в выходных данных hello в начале приветственное сообщение hello включается лишний символ BOM. Таким образом, если нежелательно hello вывода tooinclude hello лишний символ BOM, необходимо использовать ```System.IO.StreamReader().ReadToEnd()```.

### <a name="sending-messages-tooa-bridge-using-wcf-does-not-scale"></a>Отправка сообщений в мост tooa, с помощью WCF не масштабируется
Отправленные сообщения tooa мост с помощью WCF не масштабируется. Для создания масштабируемого клиента следует использовать HttpWebRequest.

### <a name="upgrade-token-provider-error-after-upgrading-from-biztalk-services-preview-toogeneral-availability-ga"></a>ОБНОВЛЕНИЯ: Ошибка поставщика токена после обновления с предварительной версии служб BizTalk tooGeneral доступность (GA)
Имеется соглашение EDI или AS2 с активными пакетами. При обновлении с предварительной версии tooGA hello службы BizTalk может возникнуть hello следующее:

* Ошибка: hello поставщик маркеров не удается tooprovide маркер безопасности. Поставщик токенов возвратил сообщение: не удалось разрешить имя удаленного hello.
* Пакетные задачи отменяются».

**Инструкции по решению**: после hello службы BizTalk обновленные tooGeneral доступность (GA), повторно развернуть соглашение hello.  

### <a name="upgrade-toolbox-shows-hello-old-bridge-icons-after-upgrading-hello-biztalk-services-sdk"></a>ОБНОВЛЕНИЕ: Панели инструментов отображаются hello старые значки мостов после обновления hello пакета SDK служб BizTalk
После обновления более ранней версии пакета SDK служб BizTalk, который был hello мосты представлялись старыми значками, hello hello элементов продолжается tooshow hello старые значки мостов hello. Тем не менее если добавить мост tooBizTalk службы проекта конструктора hello области отображается новый значок hello.  

**Возможное решение**. Можно обойти эту проблему, удалив hello TBD-файлы в <system drive>: \Users\<пользователя > \AppData\Local\Microsoft\VisualStudio\11.0.  

### <a name="upgrade-biztalk-portal-update-from-preview-tooga-might-show-an-error-indicating-that-hello-edi-capability-is-not-available"></a>ОБНОВЛЕНИЕ: При обновлении портала BizTalk от предварительной версии tooGA может показывать ошибку, указывающую, что hello возможность EDI недоступна
Если вы вошли в hello портале служб BizTalk, при обновлении служб BizTalk hello tooGA предварительной версии, может появиться следующая ошибка на портале hello hello:  

Эта функция недоступна в текущем выпуске служб Microsoft Azure BizTalk. toouse эти возможности переключения tooan соответствующий выпуск.  

**Разрешение**: выход из портала hello, hello закрыть и открыть браузер и войти в портал hello.  

### <a name="upgrade-new-tracking-data-does-not-show-up-after-biztalk-services-is-upgraded-tooga"></a>ОБНОВЛЕНИЕ: Новые данные отслеживания не отображается после tooGA обновленной службы BizTalk
Рассмотрим сценарий, когда есть мост XML, развернутый в рамках подписки на предварительную версию служб BizTalk. Toohello мост отправки сообщений и соответствующие данные отслеживания hello доступна на портале служб BizTalk hello. Теперь, если бит hello портале служб BizTalk и службы BizTalk среды выполнения обновленной tooGA и отправить сообщение toohello, же конечную точку моста, развернутую ранее, hello данные отслеживания не отображается для сообщений, отправленных после обновления.  

### <a name="pipelines-versus-bridges"></a>Конвейеры и мосты
В этом документе hello термины «конвейеры» и «мосты» взаимозаменяемы. Оба по существу означает hello же самое, являющийся, единицу обработки сообщения, развернутый на службы BizTalk.  

### <a name="concepts"></a>Основные понятия
[Службы BizTalk](https://msdn.microsoft.com/library/azure/hh689864.aspx)   

