---
title: "выдает шлюз управления данными aaaTroubleshoot | Документы Microsoft"
description: "Предоставляет советы tootroubleshoot проблемы связанные tooData Management Gateway."
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a>Устранение неполадок в работе шлюза управления данными
В этой статье приводятся сведения об устранении неполадок в работе шлюза управления данными.

> [!NOTE]
> В разделе hello [шлюз управления данными](data-factory-data-management-gateway.md) статье подробные сведения о шлюзе hello. В разделе hello [перемещение данных между локальными и облачными](data-factory-move-data-between-onprem-and-cloud.md) статье пошаговое перемещения данных из tooMicrosoft базы данных SQL Server локального хранилища больших двоичных объектов Azure с помощью шлюза hello.
>
>

## <a name="failed-tooinstall-or-register-gateway"></a>Не удалось tooinstall или регистрация шлюза
### <a name="1-problem"></a>1. Проблема
Вы видите это сообщение об ошибке при установке и регистрации шлюза, в частности, при загрузке файла установки шлюза hello.

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a>Причина:
Сбой toodownload hello последний шлюза файл установки из центра загрузки hello из-за проблемы в сети tooa Hello компьютера, на котором вы пытаетесь tooinstall hello шлюза.

#### <a name="resolution"></a>Способы устранения:
Проверьте наличие вашей toosee параметры брандмауэра сервера прокси-сервера hello параметры блокируют hello сетевого подключения от компьютера toohello hello [центре загрузки](https://download.microsoft.com/)и обновите параметры hello соответствующим образом.

Кроме того, можно загрузить последнюю версию шлюза hello в файле установки hello hello [центре загрузки](https://www.microsoft.com/download/details.aspx?id=39717) на других компьютерах, которые могут обращаться к hello центра загрузки. После этого можно копировать hello установщика toohello шлюза главного компьютера и запустите его вручную tooinstall и обновление шлюза hello.

### <a name="2-problem"></a>2. Проблема
Эта ошибка появляется пытаются tooinstall шлюза, нажав кнопку **установки непосредственно на этом компьютере** в hello портал Azure.

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a>Причина:
Шлюз уже установлен на компьютере hello.

#### <a name="resolution"></a>Способы устранения:
Удалите существующий шлюз hello на машине hello, нажмите кнопку hello **установки непосредственно на этом компьютере** ссылку еще раз.

### <a name="3-problem"></a>3. Проблема
Эта ошибка может возникнуть при регистрации нового шлюза.

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a>Причина:
Может появиться это сообщение по одной из следующих причин hello:

* Недопустимый формат ключа шлюза hello Hello.
* ключ шлюза Hello является недействительным.
* ключ шлюза Hello была повторно создана из портала hello.  

#### <a name="resolution"></a>Способы устранения:
Проверьте, используется ли ключ hello правой шлюза с портала hello. При необходимости повторно создать ключ и использовать шлюз hello ключа tooregister hello.

### <a name="4-problem"></a>4. Проблема
Может появиться следующие сообщение об ошибке, при регистрации шлюза hello.

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![Недопустимое содержимое или формат ключа](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a>Причина:
Hello содержимое или формат ключа шлюза входной hello неверный. Одной из причин hello может быть, что копируются только части ключа hello hello портала или вы используете недопустимый ключ.

#### <a name="resolution"></a>Способы устранения:
Создайте ключ шлюза на портале hello и использовать hello копирования кнопки toocopy hello весь ключ. Затем вставьте его в этот шлюз hello tooregister окна.

### <a name="5-problem"></a>5. Проблема
Может появиться следующие сообщение об ошибке, при регистрации шлюза hello.

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![Ключ шлюза является недопустимым или пустым](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a>Причина:
ключ шлюза Hello была повторно создана или hello шлюз был удален в hello портал Azure. Он также может произойти, если программа установки шлюза управления данными hello не является последней.

#### <a name="resolution"></a>Способы устранения:
Проверьте, если Настройка шлюза управления данными hello не последнюю версию hello, можно найти последнюю версию hello на hello Microsoft [центре загрузки](https://go.microsoft.com/fwlink/p/?LinkId=271260).

Если настройка текущего / последней, и шлюз по-прежнему существует на портале, ключ шлюза hello hello портал Azure, повторно использовать hello копирования кнопки toocopy hello весь ключ и вставьте его в этот шлюз hello tooregister окна. В противном случае повторного создания шлюза hello и начать заново.

### <a name="6-problem"></a>6. Проблема
Может появиться следующие сообщение об ошибке, при регистрации шлюза hello.

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![Ключ шлюза является недопустимым или пустым](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a>Причина:
Эта ошибка может происходить, когда шлюз hello удален или ключ соответствующего шлюза hello была повторно создана.

#### <a name="resolution"></a>Способы устранения:
Hello шлюз удален, повторно создать шлюз hello из портала hello, откройте **зарегистрировать**, скопируйте hello ключ с портала hello, вставьте его и повторите tooregister hello шлюза.

Если шлюз hello по-прежнему существует, но его ключ была повторно создана, используйте hello нового ключа tooregister hello шлюза. Если у вас нет ключа hello, повторно создать ключ hello снова с портала hello.

### <a name="7-problem"></a>7. Проблема
При регистрации шлюза может потребоваться tooenter путь и пароль для сертификата.

![Выбор сертификата](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a>Причина:
Hello шлюза на других компьютерах, прежде чем был зарегистрирован. Во время первоначальной регистрации hello шлюза сертификат шифрования была связана с hello шлюза. Hello сертификата можно самостоятельно созданный hello шлюза или предоставленный пользователем hello.  Этот сертификат является используется tooencrypt учетные данные хранилища данных hello (связанной службы).  

![Экспорт сертификата](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

Если восстановление hello шлюза на другой компьютер запрашивает мастер регистрации hello toodecrypt этот сертификат учетных данных для ранее зашифрован с помощью этого сертификата.  Без этого сертификата не удалось расшифровать учетные данные hello новый шлюз hello и последующие действия обработка, связанная с этой новый шлюз завершится ошибкой.  

#### <a name="resolution"></a>Способы устранения:
Если сертификат учетных данных hello были экспортированы из hello исходную машину шлюза с помощью hello **Экспорт** кнопку на hello **параметры** вкладке в данных диспетчера конфигурации шлюза управления, используйте hello сертификат.

Нельзя пропускать этот шаг при восстановлении шлюза. Если отсутствует сертификат hello, требуется toodelete hello шлюза с портала hello и повторно создать шлюз.  Кроме того можно обновите все связанные службы, которые шлюза toohello, связанные с повторный ввод учетных данных.

### <a name="8-problem"></a>8. Проблема
Может появиться сообщение об ошибке после hello.

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a>Причина:
Эта ошибка возникает, если шлюз в среде, которая требует tooaccess прокси-сервера HTTP Интернет-ресурсов, или изменить пароль для проверки подлинности на прокси-сервера, но не обновляется соответствующим образом в шлюз.

#### <a name="resolution"></a>Способы устранения:
Следуйте инструкциям hello hello [рекомендации по server прокси](#proxy-server-considerations) раздела этого статей и настройка параметров прокси-сервера с помощью диспетчера шлюза управления данными конфигурации.

## <a name="gateway-is-online-with-limited-functionality"></a>Шлюз находится в сети с ограниченной функциональностью
### <a name="1-problem"></a>1. Проблема
Можно просмотреть состояние hello шлюза hello в оперативном режиме с ограниченной функциональностью.

#### <a name="cause"></a>Причина:
Появится hello состояния hello шлюз в сети с ограниченной функциональностью, по одной из следующих причин hello:

* Шлюз нельзя подключиться toocloud службы с помощью Azure Service Bus.
* Облачная служба не удается подключиться toogateway через служебную шину.

Если hello шлюз находится в режиме с ограниченной функциональностью, может оказаться конвейеры может toouse hello мастер копирования фабрики данных toocreate данных для копирования данных tooor из локальных хранилищ данных. Чтобы избежать этого можно использовать редактор фабрики данных hello портале, Visual Studio или Azure PowerShell.

#### <a name="resolution"></a>Способы устранения:
Для устранения этой ошибки (сети с ограниченной функциональностью) на основе ли hello шлюза не может подключиться toohello облачной службы или hello другим способом. Hello в следующих разделах предоставить эти разрешения.

### <a name="2-problem"></a>2. Проблема
Появится следующая ошибка hello.

`Error: Gateway cannot connect toocloud service through service bus`

![Шлюз не удается подключиться к службе toocloud](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a>Причина:
Шлюз нельзя подключиться toohello облачной службы с помощью Service Bus.

#### <a name="resolution"></a>Способы устранения:
Выполните эти шаги tooget hello шлюза обратно в оперативный режим.

1. Разрешить IP-адрес правила для исходящих подключений на компьютере шлюза hello и hello корпоративного брандмауэра. Можно найти IP-адресов из журнала событий Windows hello (идентификатор == 401): попытка внесенные tooaccess сокет образом запрещено XX правами доступа. XX. XX. XX:9350.
* Настройте параметры прокси-сервера на шлюзе hello. В разделе hello [рекомендации по server прокси](#proxy-server-considerations) подробные сведения см.
* Разрешить исходящие порты 5671 и 9350 – 9354 на обоих hello брандмауэра Windows на компьютере шлюза hello и hello корпоративного брандмауэра. В разделе hello [порты и брандмауэр](#ports-and-firewall) подробные сведения см. Это делать не обязательно, но рекомендуется из соображений производительности.

### <a name="3-problem"></a>3. Проблема
Появится следующая ошибка hello.

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a>Причина:
Временная ошибка подключения к сети.

#### <a name="resolution"></a>Способы устранения:
Выполните эти шаги tooget hello шлюза обратно в оперативный режим.

1. Подождите несколько минут, hello подключения будут автоматически восстановлены при hello ошибка отсутствует.
* Если hello ошибка будет повторяться, перезапустите службу шлюза hello.

## <a name="failed-tooauthor-linked-service"></a>Сбой tooauthor связанные службы
### <a name="problem"></a>Проблема
Эта ошибка может появиться при попытке toouse диспетчер учетных данных учетные данные портала tooinput hello для новой связанной службы, или обновить учетные данные для существующей связанной службы.

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

При появлении этой ошибки, страница параметров hello объекта данных диспетчера конфигурации шлюза управления может выглядеть после экрана приветствия.

![Не удается получить доступ к базе данных](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a>Причина:
Возможно, на компьютере шлюза hello была потеряна Hello SSL-сертификат. компьютер с установленным шлюзом Hello не удалось загрузить сертификат hello в момент, используемый для шифрования SSL. Может также появиться сообщение об ошибке в журнал событий hello, аналогичные toohello следующие сообщения.

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a>Способы устранения:
Выполните эти шаги toosolve hello проблему.

1. Запустите диспетчер конфигураций шлюза управления данными.
2. Переключение toohello **параметры** вкладки.  
3. Нажмите кнопку hello **изменений** кнопку toochange hello SSL-сертификат.

   ![Кнопка "Изменить" для сертификата](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. Выберите новый сертификат как сертификат SSL hello. Вы можете использовать собственный или корпоративный SSL-сертификат.

   ![Выбор сертификата](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a>Сбой действия копирования
### <a name="problem"></a>Проблема
Можно заметить hello после сбоя «UserErrorFailedToConnectToSqlserver» после настройки конвейера hello портала.

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a>Причина:
Она может возникнуть по разным причинам, от которых зависят и способы ее устранения.

#### <a name="resolution"></a>Способы устранения:
Разрешите исходящие соединения TCP через порт TCP/1433 на hello шлюз управления данными на стороне клиента перед подключением tooan базы данных SQL.

Если база данных hello целевой базы данных Azure SQL, проверьте SQL Server параметры брандмауэра для Azure также.

В разделе hello, следуя tootest раздел hello toohello подключения к локальному хранилищу данных.

## <a name="data-store-connection-or-driver-related-errors"></a>Ошибки, связанные с подключением к хранилищу данных или с драйверами
Если вы видите данные хранить соединения или ошибки, связанные с драйвером, выполните hello следующие шаги.

1. Запустите диспетчер конфигурации шлюза управления данными на компьютере шлюза hello.
2. Переключение toohello **диагностики** вкладки.
3. В **проверить подключение**, добавьте значения группы hello шлюза.
4. Нажмите кнопку **тест** toosee при подключении toohello локального источника данных с компьютера hello шлюза с помощью hello сведения о соединении и учетные данные. Если hello проверить подключение по-прежнему происходит сбой в работе драйвера, перезапустите hello шлюза для него toopick копирование hello последнее изменение.

![Раздел "Проверить подключение" на вкладке "Диагностика"](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a>Журналы шлюза
### <a name="send-gateway-logs-toomicrosoft"></a>Отправить журналы tooMicrosoft шлюза
При обращении в службу технической поддержки Майкрософт tooget справки при устранении неполадок шлюза, вас попросят tooshare журналы шлюза. В выпуске hello hello шлюза могут совместно использовать журналы требуется шлюз с двумя отдельными щелчками кнопки в данных диспетчера конфигурации шлюза управления.    

1. Переключение toohello **диагностики** вкладку в диспетчера шлюза управления данными конфигурации.

    ![Вкладка "Диагностика"в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. Нажмите кнопку **отправить журналы** toosee hello следующие диалоговое окно.

    ![Кнопка "Отправить журналы" в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. (Необязательно) Нажмите кнопку **Просмотр журналов** tooreview журналах в обозревателе событий hello.
4. (Необязательно) Нажмите кнопку **конфиденциальности** tooreview Microsoft web services заявление о конфиденциальности.
5. Если вы удовлетворены Каковы о tooupload, нажмите кнопку **отправить журналы** tooactually отправлять журналы hello с hello последние семь дней tooMicrosoft для устранения неполадок. Вы увидите hello состояние операции отправки журналов hello, как показано на следующий снимок экрана приветствия.

    ![Состояние отправки журналов в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. По завершении операции hello появиться диалоговое окно, как показано в следующий снимок экрана приветствия.

    ![Состояние отправки журналов в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. Сохранить hello **идентификатор отчета** и использовать их совместно со службой поддержки Майкрософт. Идентификатор отчета Hello — журналы шлюза используется toolocate hello, загруженные для устранения неполадок.  Идентификатор Hello отчета сохраняется в средстве просмотра событий hello.  Можно найти его на событие с Идентификатором hello «25» и проверьте hello даты и времени.

    ![Идентификатор отчета об отправке журналов в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a>Архивация журналов шлюза на хост-компьютере шлюза
Существует несколько сценариев, в которых при наличии проблем в работе шлюза вы не можете передать журналы шлюза напрямую:

* Вручную установите hello шлюза и зарегистрируйте шлюз hello.
* Попробуйте tooregister hello шлюза с повторно созданный ключ в диспетчера шлюза управления данными конфигурации.
* Повторите toosend журналы и служба узла шлюза hello не может быть подключен.

В таких случаях можно сохранить журналы шлюза в ZIP-файл и предоставить их при обращении в службу поддержки Майкрософт. Например если произошла ошибка во время регистрации шлюза hello, как показано в следующий снимок экрана приветствия.   

![Ошибка регистрации в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

Нажмите кнопку hello **архивирование журналов шлюза** связать tooarchive и сохранить журналы и совместно использовать hello ZIP-файл со службой поддержки Майкрософт.

![Архивация журналов в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a>Поиск журналов шлюза
Шлюз подробные данные журнала можно найти в журналах событий Windows hello.

1. Запустите **средство просмотра событий** Windows.
2. Найдите журналы в hello **журналы приложений и служб** > **шлюз управления данными** папки.

 При устранении неполадок проблем, связанных с шлюзом, найдите события уровня ошибки в средстве просмотра событий hello.

![Журналы в средстве просмотра событий в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
