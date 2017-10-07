---
title: "Шлюз управления для фабрики данных aaaData | Документы Microsoft"
description: "Настройка шлюза данных toomove данных между локальными и hello облака. Используйте шлюз управления данными в toomove фабрики данных Azure данные."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a>Шлюз управления данными
Шлюз управления данными Hello установлен агент клиента, который необходимо установить в локальной среде toocopy данных между облачных и локальных хранилищ данных. Hello локальных данных хранилища, поддерживаемый фабрики данных, перечислены в hello [поддерживаемых источников данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) раздела.

В этой статье дополняет hello пошагового руководства hello [перемещение данных между локальными и облачными хранилищами данных](data-factory-move-data-between-onprem-and-cloud.md) статьи. В примере hello Создание конвейера, который использует данные toomove шлюза hello tooan базы данных SQL Server в локальной среде BLOB-объектов Azure. В этой статье подробно подробные hello шлюз управления данными. 

Шлюз управления данными можно масштабировать, объединяя несколько локальных компьютеров с hello шлюза. Чтобы увеличить масштаб, увеличьте число заданий перемещения данных, которые могут выполняться одновременно на узле. Эта функция также доступна для логического шлюза с одним узлом. Дополнительные сведения см. в статье [Шлюз управления данными: высокий уровень доступности и масштабируемость (предварительная версия)](data-factory-data-management-gateway-high-availability-scalability.md).

> [!NOTE]
> В настоящее время шлюз поддерживает только действие копирования hello и действие хранимой процедуры в фабрике данных. Нет шлюза hello возможных toouse из источников данных в локальной tooaccess пользовательского действия.      

## <a name="overview"></a>Обзор
### <a name="capabilities-of-data-management-gateway"></a>Возможности шлюза управления данными
Шлюз управления данными предоставляет hello следующие возможности:

* Модели локальные источники данных и облачных источников данных в пределах hello же фабрику данных и перемещения данных.
* Иметь унифицированного для мониторинга и управления с видимостью в состояние шлюза со страницы приветствия фабрики данных.
* Безопасно управлять доступа tooon локальные источники данных.
  * Изменения не требуется toocorporate брандмауэра. Исходящие подключения по протоколу HTTP tooopen только принимаются шлюзом Интернета.
  * Учетные данные для ваших локальных хранилищ данных можно шифровать с помощью личного сертификата.
* Эффективно перемещать данные: данные передаются в параллельных, надежных toointermittent проблемы с сетевым логику автоматического повтора.

### <a name="command-flow-and-data-flow"></a>Поток команд и поток данных
При использовании копирование действия toocopy данных между локальными и облачными hello использует tootransfer шлюз данных из источника toocloud локальных данных и наоборот.

Вот hello общий поток данных для и Сводка действий для копирования данных шлюза: ![потока данных с помощью шлюза](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)

1. Данных разработчик создает шлюз для фабрики данных Azure, используя либо hello [портал Azure](https://portal.azure.com) или [командлета PowerShell](https://msdn.microsoft.com/library/dn820234.aspx).
2. Данных разработчик создает связанной службы локального хранилища данных, указав hello шлюза. При настройке hello связанной службы, разработчик данных использует задать учетные данные приложения hello toospecify-типы проверки подлинности и учетные данные.  Параметр Hello учетные данные, которые диалоговое окно приложения взаимодействует с данными hello хранить tootest соединения и hello шлюза toosave учетные данные.
3. Шлюз шифрует учетные данные hello сертификатом hello, связанной со шлюзом hello (указанного в данных разработчика), перед сохранением hello учетные данные в облаке hello.
4. Служба фабрики данных взаимодействует с hello шлюз для планирования и управление заданиями через канал управления, который использует очередь общего Azure service bus. Когда задание копирования действие должно toobe запущена и фабрики данных очереди hello запроса, а также учетные данные. Шлюз запускает задание hello после опроса очереди hello.
5. шлюз Hello расшифровывает hello учетные данные с hello же сертификата, а затем подключается toohello к локальному хранилищу данных с типом надлежащую проверку подлинности и учетные данные.
6. шлюз Hello копирует данные из локального хранилища tooa облачного хранилища, или наоборот в зависимости от того, как hello действие копирования настроено в конвейере данных hello. Для выполнения этого шага шлюз hello непосредственно взаимодействует со службами облачного хранилища таких как хранилище больших двоичных объектов Azure по безопасному каналу (HTTPS).

### <a name="considerations-for-using-gateway"></a>Рекомендации по использованию шлюза
* Для нескольких локальных источников данных можно использовать один шлюз управления данными. Тем не менее **один экземпляр шлюза — одна фабрика данных Azure равноценных tooonly** и не может совместно использоваться другой фабрики данных.
* На компьютере может быть установлен **только один экземпляр шлюза управления данными**. Предположим, что у вас есть два фабрик данных, требующих tooaccess локальных источников данных, необходимо tooinstall шлюзов на двух локальных компьютерах. Другими словами шлюз является равноценных tooa конкретную фабрику данных
* Hello **шлюз не требуется toobe на компьютер же, как источник данных hello hello**. Однако наличие источника данных toohello ближе шлюз уменьшает hello время для источника данных toohello tooconnect шлюза hello. Рекомендуется устанавливать hello шлюз на компьютере, который отличается от одного источника данных локальных узлов hello. Когда hello шлюз и источник данных находятся на разных компьютерах, hello шлюза не конкурируют за ресурсы с источником данных.
* Может иметь **несколько шлюзов на разных компьютерах, соединение toohello одного источника данных в локальной**. Например имеется два шлюза, обслуживающий фабрики данных, но hello же локальному источнику данных, зарегистрированные с фабриками данных обоих hello.
* Если вы уже установили шлюз на компьютер, который обслуживает сценарий **Power BI**, установите **отдельный шлюз для фабрики данных Azure** на другой компьютер.
* Шлюз необходимо использовать, даже если используется **ExpressRoute**.
* Источник данных следует считать локальным (то есть защищенным брандмауэром), даже если используется **ExpressRoute**. Используйте hello шлюза tooestablish подключения между службой hello и hello источника данных.
* Вы должны **использовать шлюз hello** даже если hello, то хранилище данных в облаке hello на **ВМ IaaS Azure**.

## <a name="installation"></a>Установка
### <a name="prerequisites"></a>Предварительные требования
* Hello поддерживается **операционной системы** версии, Windows 7, Windows 8 и 8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2. Установка hello шлюз управления данными на контроллере домена в настоящее время не поддерживается.
* Требуется .NET Framework 4.5.1 или более поздней версии. При установке шлюза на компьютере под управлением Windows 7 установите .NET Framework 4.5 или более поздней версии. Дополнительные сведения см. в разделе [Требования к системе для .NET Framework](https://msdn.microsoft.com/library/8z6watww.aspx).
* Рекомендуется Hello **конфигурации** для hello компьютер шлюза имеет по крайней мере 2 ГГц, 4 ядра, 8 ГБ ОЗУ и диск 80 ГБ.
* Если хост-компьютере hello перейдет в спящий режим, hello шлюза не отвечает toodata запросов. Таким образом, настроить соответствующий **управления питанием** на компьютере hello перед установкой шлюза hello. Если машина hello настроенных toohibernate, установка шлюза hello предлагает сообщение.
* Необходимо иметь права администратора на машине tooinstall hello и настроить шлюз управления данными hello успешно. Можно добавить дополнительных пользователей toohello **шлюз управления данными пользователей** локальной группе Windows. Hello члены этой группы являются hello может toouse **диспетчера конфигурации шлюза управления данными** средство tooconfigure hello шлюза.

Копировать запуске действия происходят на тактовую частоту, hello использование ресурсов (ЦП, памяти) на компьютере hello также учитывает hello же шаблон с максимальной нагрузки и временем простоя. Использование ресурсов также сильно зависит hello объем данных, перемещаемых. Когда выполняется несколько заданий копирования, в пиковые периоды уровень использования ресурсов системы повышается.

### <a name="installation-options"></a>Параметры установки
Можно установить шлюз управления данными в hello следующих способов:

* Загрузить пакет установки MSI из hello [центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=39717).  Hello MSI-ФАЙЛ также может быть используется tooupgrade существующие данных управления шлюза toohello последнюю версию, обо всех параметрах, сохраняются.
* Щелкнуть ссылку **Скачивание и установка шлюза данных** в разделе "Установка вручную" или ссылку **Установка непосредственно на этот компьютер** в разделе "Экспресс-установка". В разделе [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) приведены пошаговые инструкции по экспресс-установке. выполнить ручное действие Hello принимает toohello центра загрузки.  в следующем разделе hello являются Hello инструкции по загрузке и установке шлюза hello из центра загрузки Майкрософт.

### <a name="installation-best-practices"></a>Рекомендации по установке
1. Настройте схему управления питанием на хост-компьютере hello hello шлюза, чтобы hello компьютера не удается. Если хост-компьютере hello перейдет в спящий режим, hello шлюза не отвечает toodata запросов.
2. Создайте резервную копию сертификата hello, связанной со шлюзом hello.

### <a name="install-hello-gateway-from-download-center"></a>Установить шлюз hello из центра загрузки Майкрософт
1. Перейдите в слишком[страницы загрузки шлюз управления данными Майкрософт](https://www.microsoft.com/download/details.aspx?id=39717).
2. Нажмите кнопку **загрузки**, выберите hello соответствующую версию (**32-разрядных** vs. **64-разрядную**) и нажмите кнопку **Далее**.
3. Запустите hello **MSI** напрямую или сохранить его tooyour жесткий диск и запустите.
4. На hello **приветствия** выберите **язык** щелкните **Далее**.
5. **Принять** hello лицензионное соглашение и нажмите кнопку **Далее**.
6. Выберите **папки** tooinstall hello шлюза и нажмите кнопку **Далее**.
7. На hello **готовности tooinstall** щелкните **установить**.
8. Нажмите кнопку **Готово** toocomplete установки.
9. Получение ключа hello из hello портал Azure. Hello следующего раздела приведены пошаговые инструкции в разделе.
10. На hello **регистрации шлюза** страница **диспетчера конфигурации шлюза управления данными** выполняется на компьютере, hello следующие действия:
    1. Вставьте ключ hello в тексте hello.
    2. При необходимости щелкните **Показать ключ шлюза** ключа текста hello toosee.
    3. Щелкните **Зарегистрировать**.

### <a name="register-gateway-using-key"></a>Регистрация шлюза с помощью ключа
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a>Если вы еще не создали логических шлюза hello портала
toocreate шлюз в ключе hello hello портал и get из hello **Настройка** страницы, повторите шаги с пошаговым руководством hello [перемещение данных между локальными и облачными](data-factory-move-data-between-onprem-and-cloud.md) статьи.    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a>Если уже создали hello логических шлюза на портале hello
1. На портале Azure перейдите toohello **фабрики данных** и нажмите кнопку **связанные службы** плитки.

    ![Страница "Фабрика данных"](media/data-factory-data-management-gateway/data-factory-blade.png)
2. В hello **связанные службы** страницы выберите hello логических **шлюза** вы создали на портале hello.

    ![Логический шлюз](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. В hello **шлюз данных** щелкните **загрузить и установить шлюз данных**.

    ![Ссылка на портале hello для загрузки](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. В hello **Настройка** щелкните **повторно создайте ключ**. Нажмите кнопку Да в предупреждающее сообщение hello после их считывания внимательно.

    ![Повторное создание ключа](media/data-factory-data-management-gateway/recreate-key-button.png)
5. Нажмите кнопку Далее ключ toohello копирования кнопки. ключ Hello — скопированный toohello буфер обмена.

    ![Копирование ключа](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a>Значки и уведомления в области уведомлений
Hello следующем рисунке показаны некоторые hello значки, отображаемые на панели задач.

![значки на панели задач](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

Если навести курсор на панели задач значок/уведомления hello системного сообщения будут отображаться сведения о состоянии операции шлюза или обновления hello во всплывающем окне приветствия.

### <a name="ports-and-firewall"></a>Порты и брандмауэр
Существует два брандмауэры должны tooconsider: **корпоративного брандмауэра** под управлением центра маршрутизатора hello организации hello и **брандмауэра Windows** настроен как управляющая программа на локальном компьютере hello, где hello шлюз установлен.  

![брандмауэры](./media/data-factory-data-management-gateway/firewalls2.png)

На уровне корпоративный брандмауэр, необходимо настроить следующие hello домены и исходящие порты:

| Имена доменов | порты; | Описание |
| --- | --- | --- |
| *.servicebus.windows.net |443, 80 |Используется для связи с серверной частью службы перемещения данных. |
| *.core.windows.net |443 |Используется для промежуточного копирования с помощью большого двоичного объекта Azure (если оно настроено).|
| *.frontend.clouddatahub.net |443 |Используется для связи с серверной частью службы перемещения данных. |


Эти исходящие порты, как правило, включены на уровне брандмауэра Windows. Если нет, можно настроить домены hello и порты соответствующим образом на компьютере шлюза.

> [!NOTE]
> 1. В зависимости от источника или приемники, возможно, toowhitelist дополнительные домены и исходящие порты в брандмауэре организации или Windows.
> 2. Для некоторых баз данных в облаке (например: [базы данных SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Озера данных Azure](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), т. д.), может потребоваться toowhitelist IP-адрес компьютера шлюза на их конфигурации брандмауэра.
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a>Копирование данных из хранилища данных приемник tooa источника данных хранилища
Убедитесь, что правильно включать hello правила брандмауэра на hello корпоративный брандмауэр, брандмауэр Windows на компьютере шлюза hello и самого хранилища данных hello. Включение этих правил позволяет hello шлюза tooconnect tooboth источника и приемника успешно. Включите правила для каждого хранилища данных, которая участвует в операции копирования hello.

Например, toocopy из **приемник локальной tooan хранилище данных базы данных SQL Azure или приемника хранилища данных SQL Azure**, hello следующие действия:

* Разрешите исходящий трафик **TCP** через порт **1433** для брандмауэра Windows и корпоративного брандмауэра.
* Настройте параметры брандмауэра hello Azure SQL tooadd hello IP-адрес сервера hello машины шлюза toohello список разрешенных IP-адресов.

> [!NOTE]
> Если брандмауэр блокирует исходящий порт 1433, то шлюз не сможет напрямую получить доступ к SQL Azure. В этом случае можно использовать [промежуточное копирования](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL базы данных SQL Azure и хранилища данных SQL Azure. В этом сценарии вы только потребуется HTTPS (порт 443) для перемещения данных hello.
>
>


### <a name="proxy-server-considerations"></a>Рекомендации для прокси-сервера
Если вашей организации сетевой среде используется прокси-сервер сервера tooaccess Здравствуйте Интернета, Настройка параметров шлюза toouse соответствующие прокси-сервера для данных управления. Hello прокси-сервера можно задать во время этапа первоначальной регистрации hello.

![Настройка прокси-сервера при регистрации](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

Шлюз использует hello прокси-сервера tooconnect toohello облачной службы. Щелкните ссылку **Изменить** во время начальной настройки. Вы видите hello **параметры прокси-сервера** диалогового окна.

![Настройка прокси-сервера с помощью диспетчера конфигурации](media/data-factory-data-management-gateway/SetProxySettings.png)

Доступны три варианта конфигурации.

* **Не использовать прокси-сервер**: шлюза явным образом не используйте любой службы toocloud tooconnect прокси-сервера.
* **Использовать прокси-сервер системы**: шлюза использует hello прокси-сервер, то есть параметр настроены в diahost.exe.config и diawp.exe.config.  Если ни один прокси настроен в diahost.exe.config и diawp.exe.config, toocloud службы подключение шлюза напрямую без прохода через прокси-сервера.
* **Использовать пользовательский прокси-сервер**: Настройка toouse параметр hello HTTP прокси-сервера для шлюза, а не с помощью конфигураций в diahost.exe.config и diawp.exe.config.  Необходимо указать адрес и порт.  Имя пользователя и пароль являются необязательными и указываются в зависимости от настроек аутентификации прокси-сервера.  Все параметры шифруются с hello сертификат учетных данных шлюза hello и хранятся локально на компьютере размещения шлюза hello.

Шлюз управления данными Hello хост-служба автоматически перезапускается после сохранения параметров прокси-сервера обновлены hello.

После шлюз успешно зарегистрирован, если требуется tooview или обновить параметры прокси-сервера, используйте диспетчер конфигурации шлюза управления данными.

1. Запустите **диспетчер конфигурации шлюза управления данными**.
2. Переключение toohello **параметры** вкладки.
3. Нажмите кнопку **изменений** ссылку в **прокси-сервера HTTP** hello раздел toolaunch **задать прокси-сервер HTTP** диалогового окна.  
4. После нажатия кнопки hello **Далее** кнопку, отображается диалоговое окно с предупреждением, задать для параметра прокси hello toosave разрешение и перезапустите hello служба узла шлюза.

При помощи диспетчера конфигурации можно просмотреть и обновить HTTP-прокси.

![Настройка прокси-сервера с помощью диспетчера конфигурации](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> Если настройка прокси-сервер с проверкой подлинности NTLM, служба узла шлюза выполняется под учетной записью домена hello. Если изменить пароль hello hello учетной записи домена позже, помнить tooupdate параметры конфигурации для службы hello и перезапустите его соответствующим образом. Из-за toothis требование мы рекомендуем использовать выделенной доменной учетной записи tooaccess hello прокси-сервер, не требует пароля hello tooupdate часто.
>
>

### <a name="configure-proxy-server-settings"></a>Настройка параметров прокси-сервера
При выборе **использовать прокси-сервер системы** Установка для прокси-сервера hello HTTP шлюз использует параметр в diahost.exe.config и diawp.exe.config hello прокси.  Если в diahost.exe.config и diawp.exe.config без прокси-сервера не указано, шлюз подключается toocloud службы непосредственно, без прохода через прокси-сервера. Hello следующей процедуре представлены инструкции по обновлению файла diahost.exe.config hello.  

1. В проводнике составляющих защищенной копии данных управления C:\Program Files\Microsoft Gateway\2.0\Shared\diahost.exe.config tooback hello исходного файла.
2. Запустите файл Notepad.exe с правами администратора и откройте текстовый файл с путем C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. Вы можете найти тег по умолчанию hello для system.net, как показано в hello, следующий код:

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   Затем можно добавить сведения о сервере прокси-сервера, как показано в следующий пример hello:

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   Дополнительные свойства могут использоваться внутри hello тег toospecify hello требуется прокси-сервер как scriptLocation. См. слишком[прокси-сервера (параметры сети) элемент](https://msdn.microsoft.com/library/sa91de1e.aspx) на синтаксис.

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. Сохраните файл конфигурации hello в исходное расположение hello, а затем перезапустите службу узла шлюза управления данными, которая принимает изменения, внесенные hello hello. Служба hello toorestart: с помощью "службы" из панели управления hello или hello **диспетчера конфигурации шлюза управления данными** > щелкните hello **остановить службу** , а затем нажмите кнопку hello **Запуск службы**. Если служба hello не запускается, вполне вероятно, что неправильный синтаксис тега XML был добавлен в файл конфигурации приложения hello, который был изменен.

> [!IMPORTANT]
> Не забудьте tooupdate **оба** diahost.exe.config и diawp.exe.config.  


В дополнение к этому toothese точек, необходимо также toomake том, что Microsoft Azure в белом списке вашей компании. Список Hello допустимым Microsoft IP-адресов Azure можно загрузить из hello [центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=41653).

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a>Возможные признаки проблем, связанных с брандмауэром и прокси-сервером
При возникновении ошибки аналогичные toohello следующих областей, вполне вероятно, из-за конфигурации tooimproper hello брандмауэра или прокси-сервер, который блокирует шлюза из соединения tooauthenticate фабрики tooData сам. См. в разделе tooensure tooprevious, брандмауэра и прокси-сервера настроены правильно.

1. При попытке tooregister hello шлюза вы получаете hello следующая ошибка: «сбой tooregister hello шлюза ключ. Перед повторной попыткой ключ шлюза hello tooregister Подтверждение запуска шлюза управления данными находится в подключенном состоянии hello и hello служба узла шлюза управления данными.»
2. При открытии диспетчера конфигурации отображается состояние "Отключено" или "Подключение". При просмотре журналов событий Windows, в разделе «Просмотр событий» > «Журналы приложений и служб» > «Шлюз управления данными», вы видите сообщения об ошибках, таких как hello следующая ошибка:`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`

### <a name="open-port-8050-for-credential-encryption"></a>Открытие порта 8050 для шифрования учетных данных
Hello **задать учетные данные** использует приложение hello входящий порт **8050** toorelay шлюза toohello учетные данные при настройке локальной связанной службы в hello портал Azure. Во время установки шлюза по умолчанию установка шлюза hello открывает его на компьютере шлюза hello.

Если вы используете брандмауэр сторонних разработчиков, можно вручную открыть порт hello 8050. Если возникли проблемы брандмауэра во время установки шлюза, попробуйте использовать следующие команды tooinstall hello шлюза без настройки брандмауэра hello hello.

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

Если не tooopen hello порт 8050 на компьютере шлюза hello, использовать механизмы без использования hello **задать учетные данные** данные приложения tooconfigure хранить учетные данные. Например, можно использовать командлет PowerShell [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx). Дополнительные сведения о настройке учетных данных хранилища данных см. в разделе [Настройка учетных данных и безопасность](#set-credentials-and-securityy).

## <a name="update"></a>Блокировка изменений
По умолчанию шлюз управления данными обновляется автоматически при доступна более новая версия шлюза hello. шлюз Hello не обновляется, пока все hello запланированных задач. Последующие задачи не обрабатываются шлюзом hello до завершения операции обновления hello. В случае обновления hello шлюза выполняется откат toohello старую версию.

Отображается время hello запланированные обновления в следующих местах hello:

* Страница свойств шлюза Hello в hello портал Azure.
* Домашняя страница hello диспетчера конфигурации шлюза управления данными
* сообщение в области уведомлений.

Вкладка домашней Hello hello диспетчера конфигурации шлюза управления данными отображает расписание обновления hello и hello последнее время hello шлюза был установлен или обновлена.

![запланировать обновления](media/data-factory-data-management-gateway/UpdateSection.png)

Можно сразу установить обновление hello или дождитесь toobe шлюза hello, автоматически обновляются во время запланированного hello. Например показано изображение hello уведомлений сообщение, показанное на hello диспетчера конфигурации шлюза вместе с hello кнопкой "Обновить", можно щелкнуть tooinstall его сразу же после hello.

![Обновление диспетчера конфигураций DMG](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

сообщение Hello уведомления hello панели задач будет выглядеть, как показано в hello после изображения:

![Сообщение на панели задач](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

Можно просмотреть состояние hello операции обновления (вручную или автоматически) hello панели задач. При запуске диспетчера конфигурации шлюза следующий раз появится сообщение на панель, шлюз hello уведомления hello была обновлена со ссылкой слишком[возможности новый раздел](data-factory-gateway-release-notes.md).

### <a name="toodisableenable-auto-update-feature"></a>функция toodisable Включение автоматического обновления
Вы можете включить или отключить hello функция автоматического обновления, выполнив следующие шаги hello:

(Для шлюза с одним узлом)
1. Запустите Windows PowerShell на компьютере шлюза hello.
2. Перейдите в папку C:\Program Files\Microsoft данных управления Gateway\2.0\PowerShellScript toohello.
3. Выполнения hello после автоматического обновления команда hello tooturn компонентов OFF (отключено).   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. tooturn его обратно на:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
([Для высокодоступного и масштабируемого шлюза с несколькими узлами (предварительная версия)](data-factory-data-management-gateway-high-availability-scalability.md))
1. Запустите Windows PowerShell на компьютере шлюза hello.
2. Перейдите в папку C:\Program Files\Microsoft данных управления Gateway\2.0\PowerShellScript toohello.
3. Выполнения hello после автоматического обновления команда hello tooturn компонентов OFF (отключено).   

    Для шлюза с функцией высокой доступности (предварительная версия) требуется дополнительный параметр AuthKey.
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. tooturn его обратно на:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
При доступе к hello портал с компьютера, отличном от компьютера шлюза hello, убедитесь, что приложение hello диспетчер учетных данных могут подключаться toohello компьютере шлюза. Приложение hello не могут получить доступ на компьютере шлюза hello, он не позволяет tooset учетные данные для источника данных hello и источника данных toohello tootest соединения.  

При использовании hello **задать учетные данные** приложения, портал hello шифрует учетные данные hello hello сертификат, указанный в hello **сертификат** вкладка hello **шлюза Configuration Manager** на компьютере шлюза hello.

Если вы ищете подход на основе API для шифрования учетных данных hello, можно использовать hello [New AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) учетные данные tooencrypt командлета PowerShell. Hello командлет использует hello сертификата, что шлюз находится настроенный toouse tooencrypt hello, учетные данные. Добавьте зашифрованные учетные данные toohello **EncryptedCredential** элемент hello **connectionString** в hello JSON. Использовать hello JSON с hello [New AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) командлета или в hello редактор фабрики данных.

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

Для настройки учетных данных при помощи редактора фабрики данных существует еще один способ. При создании связанного сервера SQL службы с помощью редактора hello и введите учетные данные в виде обычного текста, hello, учетные данные шифруются с помощью сертификата, которому принадлежит служба фабрики данных hello. Он не использует этот шлюз является настроенным toouse сертификатов hello. Хотя этот способ работает быстрее в некоторых случаях, он менее безопасен. Поэтому мы рекомендуем использовать его только для целей разработки и тестирования.

## <a name="powershell-cmdlets"></a>Командлеты PowerShell
В этом разделе описываются как toocreate и зарегистрируйте шлюз с помощью командлетов Azure PowerShell.

1. Запустите модуль **Azure PowerShell** в режиме администратора.
2. Войдите в учетную запись Azure tooyour, выполнив hello следующую команду и введите учетные данные Azure.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Используйте hello **New AzureRmDataFactoryGateway** toocreate командлет логических шлюза следующим образом:

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    **Пример команды и выходных данных**:

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. В Azure PowerShell, перейдите в папку toohello: **данных управления C:\Program Files\Microsoft Gateway\2.0\PowerShellScript\**. Запустите **RegisterGateway.ps1** связанный с локальной переменной hello **$Key** как показано в hello следующую команду. Этот сценарий регистрирует агента клиента hello установлены на компьютере со шлюзом логических hello, созданные ранее.

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    Hello шлюза на удаленном компьютере можно зарегистрировать с помощью параметра IsRegisterOnRemoteMachine hello. Пример:

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. Можно использовать hello **Get AzureRmDataFactoryGateway** командлет tooget hello список шлюзов в вашей фабрике данных. Здравствуйте, когда **состояние** показывает **online**, это означает, что ваш шлюз является готов toouse.

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
Можно удалить шлюз с помощью hello **удаление AzureRmDataFactoryGateway** описание командлета и обновления для шлюза, используя hello **AzureRmDataFactoryGateway набор** командлетов. Дополнительную информацию о синтаксисе и другую информацию об этих командлетах см. в "Справочных материалах по командлетам фабрики данных".  

### <a name="list-gateways-using-powershell"></a>Вывод списка шлюзов с помощью PowerShell

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a>Удаление шлюза с помощью PowerShell

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a>Дальнейшие действия
* В разделе [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) . В примере hello Создание конвейера, который использует данные toomove шлюза hello tooan базы данных SQL Server в локальной среде BLOB-объектов Azure.  
