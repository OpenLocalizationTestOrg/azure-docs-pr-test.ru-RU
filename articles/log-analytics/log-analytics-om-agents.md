---
title: "Operations Manager aaaConnect tooLog Analytics | Документы Microsoft"
description: "toomaintain существующие инвестиции в System Center Operations Manager и использовать расширенные возможности с помощью аналитики журналов, Operations Manager можно интегрировать с рабочей областью OMS."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 245ef71e-15a2-4be8-81a1-60101ee2f6e6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: magoedte
ms.openlocfilehash: b2841c7aa209fec7357dc4c8b1ff4325fdaa37ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-operations-manager-toolog-analytics"></a>Подключение Operations Manager tooLog аналитика
toomaintain существующие инвестиции в System Center Operations Manager и использовать расширенные возможности с помощью аналитики журналов, Operations Manager можно интегрировать с рабочей областью OMS.  Это позволяет использовать возможности hello объекта OMS продолжая toouse Operations Manager на:

* Продолжить наблюдение за работоспособностью hello ИТ-служб с помощью Operations Manager
* управление интеграцией с решениями ITSM, поддерживающими управление различными инцидентами и неполадками;
* Управление жизненным циклом hello tooon агенты, развернутые в локальной и общедоступного облака IaaS виртуальных машин, которые нужно контролировать с помощью Operations Manager

Интеграция с System Center Operations Manager добавляет стратегия операций обслуживания tooyour значение с помощью hello скорость и эффективность OMS в сбора, хранения и анализа данных из Operations Manager.  OMS позволяет скоррелируйте и работы для выявления ошибок hello проблем и распределение результатов повторениями для поддержки процесс управления существующие проблемы.   Hello гибкость hello search engine tooexamine производительности, событий и предупреждений с данными и многофункциональных панелей мониторинга и отчетов возможности tooexpose эти данные эффективными способами, демонстрирует hello стойкость OMS вводит в Operations Manager это означает.

агенты Hello отчеты группы управления Operations Manager toohello сбор данных с серверов на основе источников данных для анализа журналов hello и решений, которые вы выбрали в вашей подписке OMS.  В зависимости от решения hello, которые вы выбрали данные из этих решений, либо передается непосредственно с сервера управления Operations Manager, toohello OMS веб-службы или из-за hello объем данных, собранных в системе управляемые hello отправляются напрямую из hello агента tooOMS веб-службы. сервер управления Hello пересылает данные OMS hello, напрямую toohello OMS веб-службы; они никогда не записываются toohello базы данных OperationsManager или OperationsManagerDW.  Сервер управления теряет связь с веб-службу OMS hello, кэширует данные hello локально до связи восстановления с OMS.  Если сервер управления hello отключен из-за обслуживания tooplanned или незапланированного простоя, другой сервер управления в группе управления hello возобновляет соединение с OMS.  

Hello следующая диаграмма изображает hello соединения между серверами управления hello и агентов в группе управления System Center Operations Manager и OMS, включая направление hello и порты.   

![oms-operations-manager-integration-diagram](./media/log-analytics-om-agents/oms-operations-manager-connection.png)

Если ИТ политики безопасности не допускают компьютеров на toohello tooconnect вашей сети Интернет, серверов управления можно сведения о конфигурации настроенного tooconnect toohello шлюза OMS tooreceive и отправки собранных данных, в зависимости от решения hello вы включить.  Дополнительные сведения и инструкции по tooconfigure toocommunicate группы управления в Operations Manager, через службу OMS toohello шлюза OMS. в статье [подключения tooOMS компьютеров с помощью шлюза OMS hello](log-analytics-oms-gateway.md).  

## <a name="system-requirements"></a>Требования к системе
Прежде чем начать, просмотрите следующие сведения tooverify выполняются требования hello.

* OMS поддерживает только Operations Manager 2016, Operations Manager 2012 с пакетом обновления 1 (SP1) и накопительным пакетом обновления 6 (UR6) и более поздней версии, а также Operations Manager 2012 R2 с накопительным пакетом обновления 2 (UR2) и более поздней версии.  Поддержка прокси-сервера была добавлена в Operations Manager 2012 с пакетом обновления 1 (SP1) и накопительным пакетом обновления 7 (UR7) и в Operations Manager 2012 R2 с накопительным пакетом обновления 3 (UR3).
* Все агенты Operations Manager должны удовлетворять минимальным требованиям поддержки. Убедитесь, что агенты имеют hello минимального обновления, в противном случае трафик агент Windows может завершиться ошибкой и много ошибок может быть заполнен hello журнал событий Operations Manager.
* Наличие подписки OMS.  Дополнительные сведения см. в статье [Начало работы с Log Analytics](log-analytics-get-started.md).

### <a name="network"></a>Сеть
сведения о Hello ниже список hello прокси-сервера и брандмауэра детали конфигурации, необходимые для агента Operations Manager hello, серверов управления и toocommunicate консоли операций с OMS.  Трафик от каждого компонента является исходящим из службы OMS toohello сети.     

|Ресурс | Номер порта| Обход проверки HTTP|  
|---------|------|-----------------------|  
|**Агент**|||  
|\*.ods.opinsights.azure.com| 443 |Да|  
|\*.oms.opinsights.azure.com| 443|Да|  
|\*.blob.core.windows.net| 443|Да|  
|\*.azure-automation.net| 443|Да|  
|**Сервер управления**|||  
|\*.service.opinsights.azure.com| 443||  
|\*.blob.core.windows.net| 443| Да|  
|\*.ods.opinsights.azure.com| 443| Да|  
|*.azure-automation.net | 443| Да|  
|**TooOMS консоли Operations Manager**|||  
|service.systemcenteradvisor.com| 443||  
|\*.service.opinsights.azure.com| 443||  
|\*.live.com| 80 и 443||  
|\*microsoft.com| 80 и 443||  
|\*.microsoftonline.com| 80 и 443||  
|\*.mms.microsoft.com| 80 и 443||  
|login.windows.net| 80 и 443||  


## <a name="connecting-operations-manager-toooms"></a>Подключение tooOMS Operations Manager
Выполнение после последовательности шагов tooconfigure hello вашей tooone Operations Manager management группы tooconnect рабочих областей OMS.

1. В консоли Operations Manager hello выберите hello **администрирования** рабочей области.
2. Разверните узел Operations Management Suite hello и щелкните **соединения**.
3. Нажмите кнопку hello **зарегистрировать tooOperations Management Suite** ссылку.
4. На hello **мастер выставления набора Operations Management Suite: проверка подлинности** введите hello адрес электронной почты или номер телефона и пароль учетной записи администратора hello, связанный с вашей подпиской OMS и нажмите кнопку  **Войдите в**.
5. После вы успешно проходят проверку, на hello **мастер выставления набора Operations Management Suite: Выбор рабочей области** , страницы, запрос tooselect рабочей области OMS.  При наличии более чем одной рабочей области, выберите hello рабочей области будет tooregister с группы управления Operations Manager hello hello раскрывающемся списке и нажмите кнопку **Далее**.
   
   > [!NOTE]
   > Одновременно в Operations Manager поддерживается только одна рабочая область OMS. подключение Hello и hello компьютеров, которые были зарегистрированных tooOMS с предыдущей рабочей областью hello, удаляются из OMS.
   > 
   > 
6. На hello **мастер выставления набора Operations Management Suite: Сводка** Подтвердите параметры и если они верны, щелкните **создать**.
7. На hello **мастер выставления набора Operations Management Suite: Готово** щелкните **закрыть**.

### <a name="add-agent-managed-computers"></a>Добавление управляемых агентом компьютеров
После настройки интеграции с рабочей областью OMS, при этом только устанавливается подключение к OMS, данные не собираются из агентов hello reporting tooyour группы управления. Для этого необходимо указать определенные управляемые агентом компьютеры, которые будут собирать данные для Log Analytics. Можно либо выбрать объекты компьютеров hello по отдельности или выбрать группу, которая содержит объекты-компьютеры Windows. Нельзя выбрать группу, в которой содержатся экземпляры другого класса, например логические диски или базы данных SQL.

1. Привет открыть консоль Operations Manager и выберите hello **администрирования** рабочей области.
2. Разверните узел Operations Management Suite hello и щелкните **соединения**.
3. Нажмите кнопку hello **добавить компьютер или группу** ссылку в разделе hello действия заголовок на hello правой панели «hello».
4. В hello **поиск компьютера** диалоговое окно, можно выполнить поиск компьютеров или групп, отслеживаемых Operations Manager. Выберите tooOMS tooonboard компьютеров или групп, нажмите кнопку **добавить**, а затем нажмите кнопку **ОК**.

Вы можете просмотреть компьютеры и настроенных групп toocollect данные из управляемых компьютеров hello в узле Operations Management Suite в hello **администрирования** рабочей области консоли управления hello.  Здесь также можно при необходимости добавлять или удалять компьютеры и группы.

### <a name="configure-oms-proxy-settings-in-hello-operations-console"></a>Настройка параметров прокси-сервера OMS в консоли управления hello
Выполните hello, выполнив действия, если внутренние прокси-сервер между группой управления hello и веб-службу OMS.  Эти параметры являются централизованно управлять из группы управления hello и распределенных tooagent управляемых системах, включенных в hello области toocollect данных для OMS.  Это полезно для обхода при определенных решений управления hello server и отправки данных непосредственно tooOMS веб-службы.

1. Привет открыть консоль Operations Manager и выберите hello **администрирования** рабочей области.
2. Разверните узел Operations Management Suite и щелкните **Подключения**.
3. В hello представление подключения к OMS, щелкните **Настройка прокси-сервера**.
4. На **мастер Operations Management Suite: прокси-сервер** выберите **использовать hello tooaccess сервера прокси-сервера Operations Management Suite**, а затем введите URL-адрес hello с номером порта hello, например, http:// corpproxy:80 и нажмите кнопку **Готово**.

Если прокси-сервер требует проверки подлинности, выполните следующие hello действия tooconfigure учетные данные и параметры, которые должны toopropagate toomanaged компьютеров, которые tooOMS в группе управления hello в отчете.

1. Привет открыть консоль Operations Manager и выберите hello **администрирования** рабочей области.
2. В разделе **Конфигурация запуска от имени** выберите **Профили**.
3. Откройте hello **System Center Advisor прокси профиля запуска от** профиля.
4. В hello мастера запуска от имени профиля нажмите кнопку Добавить toouse учетная запись запуска от имени. Можно создать [учетную запись запуска от имени](https://technet.microsoft.com/library/hh321655.aspx) или использовать существующую. Эта учетная запись должна toohave достаточные разрешения toopass hello прокси-сервер.
5. tooset Здравствуйте toomanage учетной записи, выберите **выбранный класс, группу или объект**, нажмите кнопку **выберите...** а затем нажмите кнопку **Группа…**, tooopen hello **группы поиска** поле.
6. Найдите и выберите **группу серверов мониторинга Microsoft System Center Advisor**.  Нажмите кнопку **ОК** после выбора hello группы tooclose hello **группы поиска** поле.
7. Нажмите кнопку **ОК** tooclose hello **добавить учетную запись запуска от имени** поле.
8. Нажмите кнопку **Сохранить** toocomplete hello мастер и сохраните изменения.

После создания соединения hello и настроить какие агенты будут сбора и составления отчетов tooOMS данных, hello следующая конфигурация применяется в группе управления hello, не обязательно в порядке:

* Hello учетная запись запуска от **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate** создается.  Он связан с профилем запуска от имени hello **System Center помощник по настройке ядра выполнения как профиль больших двоичных объектов Microsoft** и предназначен для двух классов - **сервер сбора** и **группы управления Operations Manager** .
* Будут созданы два соединителя.  Hello сначала называется **Microsoft.SystemCenter.Advisor.DataConnector** и автоматически настраивается с помощью подписки, которая пересылает все предупреждения, созданные на основе экземпляров всех классов tooOMS группы управления hello журнала Аналитические данные. второй соединитель Hello **Advisor Connector**, который отвечает за взаимодействия с веб-службу OMS и обмена данными.
* Агентов и групп, что выбран toocollect данных в группе управления hello добавляется toohello **группу серверов мониторинга в помощник по настройке ядра для Microsoft System Center**.

## <a name="management-pack-updates"></a>Обновления пакета управления
После завершения настройки группы управления Operations Manager hello устанавливает соединение с hello службой OMS.  сервер управления Hello синхронизируется с hello веб-службу и получения обновленных сведений о конфигурации в виде hello пакетов управления для решения hello, которые вы выбрали, интегрируемые с Operations Manager.   Operations Manager проверяет наличие обновлений для этих пакетов управления, автоматически скачивает и импортирует их.  Существует два правила для управления этими действиями:

* **Microsoft.SystemCenter.Advisor.MPUpdate** -обновляет пакеты управления OMS базовый hello. По умолчанию выполняется каждые 12 часов.
* **Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** : обновляет пакеты управления решения, включенные в рабочую область. По умолчанию выполняется каждые 5 (пять) минут.

Можно переопределить эти два правила tooeither предотвратить автоматическую загрузку путем отключения их или изменить частоту hello сервера управления синхронизируется с OMS toodetermine Если доступен новый пакет управления и следует ли загружать частоту hello.  Выполните действия hello [как tooOverride правило или монитор](https://technet.microsoft.com/library/hh212869.aspx) toomodify hello **частоты** со значением в секундах toochange hello расписание синхронизации или измените hello **включено**  правил hello toodisable параметров.  Целевой hello переопределяет tooall объектов класса группы управления Operations Manager.

Следует toocontinue следующие существующие процесса управления изменениями для контроля версий пакета управления в вашей рабочей группе управления можно отключить правила hello и включить их в определенное время, когда обновления разрешены. При наличии в среде разработки или QA группы управления и имеет toohello подключения к Интернету, можно настроить эту группу управления с toosupport рабочей области OMS этот сценарий.  Это позволяет вам tooreview и оценки hello итеративный выпуски пакетов управления OMS hello, прежде чем освободить их в вашей рабочей группе управления.

## <a name="switch-an-operations-manager-group-tooa-new-oms-workspace"></a>Переключение tooa группы Operations Manager новую рабочую область OMS
1. Войдите в OMS tooyour подписку и создайте рабочую область в [Microsoft Operations Management Suite](http://oms.microsoft.com/).
2. Привет открыть консоль Operations Manager с учетной записью, которая является членом роли администраторов Operations Manager hello и выберите hello **администрирования** рабочей области.
3. Разверните узел Operations Management Suite и выберите **Подключения**.
4. Выберите hello **повторной настройки операции Management Suite** ссылку на hello среднего стороне панели «hello».
5. Выполните hello **мастер выставления набора Operations Management Suite** и введите hello электронной почты адрес или номер телефона и пароль учетной записи администратора hello, связанный с новой рабочей областью OMS.
   
   > [!NOTE]
   > Hello **мастер выставления набора Operations Management Suite: Выбор рабочей области** странице представлен hello существующей рабочей области, который используется.
   > 
   > 

## <a name="validate-operations-manager-integration-with-oms"></a>Проверка интеграции Operations Manager с OMS
Существует несколько способов, можно проверить, ваш OMS tooOperations интеграция с диспетчером успешно.

### <a name="tooconfirm-integration-from-hello-oms-portal"></a>Интеграция tooconfirm через портал OMS hello
1. На портале OMS hello щелкните hello **параметры** плитки
2. Выберите **Connected Sources** (Подключенные источники).
3. В таблице hello под hello раздела System Center Operations Manager вы увидите hello имя группы управления hello, отмечены hello число агентов и состояние, время последнего получения данных.
   
   ![oms-settings-connectedsources](./media/log-analytics-om-agents/oms-settings-connectedsources.png)
4. Примечание hello **идентификатор рабочей области** значение в списке слева от hello параметры страницы приветствия.  Его нужно будет проверить на соответствие группе управления Operations Manager.  

### <a name="tooconfirm-integration-from-hello-operations-console"></a>Интеграция tooconfirm из консоли управления hello
1. Привет открыть консоль Operations Manager и выберите hello **администрирования** рабочей области.
2. Выберите **пакетов управления** и в hello **искать:** введите **помощник по настройке ядра** или **аналитики**.
3. В зависимости от решения hello, которые вы выбрали вы увидите соответствующего пакета управления, перечисленные в результатах поиска hello.  Например при наличии hello решение для управления оповещениями, пакет управления hello предупреждения управления Microsoft System Center Advisor — в списке hello.
4. Из hello **мониторинг** просмотреть, перейдите toohello **Suite\Health состояние операций управления** представления.  Выберите сервер управления в группе hello **состояние сервера управления** области и в hello **подробное представление** области подтвердить hello значение для свойства **URI службы проверки подлинности** совпадает с идентификатором hello рабочей области OMS.
   
   ![oms-opsmgr-mg-authsvcuri-property-ms](./media/log-analytics-om-agents/oms-opsmgr-mg-authsvcuri-property-ms.png)

## <a name="remove-integration-with-oms"></a>Удаление интеграции с OMS
При интеграции между вашей группы управления Operations Manager и рабочей областью OMS больше не требуется, существуют несколько шагов, необходимых tooproperly remove hello соединении и конфигурации в группе управления hello. Hello следующая процедура имеет можно обновить рабочую область OMS, удаляя ссылку hello группы управления, удалите соединители OMS hello и затем удалить пакеты управления, поддерживающие OMS.   

Пакеты управления для решения hello, которые вы выбрали, интегрируемые с Operations Manager и интеграция toosupport необходимые пакеты управления hello с hello службой OMS нельзя удалить из группы управления hello легко.  Это, поскольку некоторые пакеты управления OMS hello зависят от других пакетов управления.  пакеты управления toodelete зависимость от других пакетов управления, загрузите скрипт hello [удалить пакет управления с зависимостями](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e) из центра сценариев TechNet.  

1. Откройте hello командная оболочка Operations Manager, используя учетную запись, которая является членом роли администраторов Operations Manager hello.
   
    > [!WARNING]
    > Проверьте у вас все пользовательские пакеты управления с слово hello ядра СУБД или IntelligencePack в имени hello, прежде чем продолжить, в противном случае hello указанные действия удалить их из группы управления hello.
    > 

2. Из командной оболочки hello введите:`Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
3. Затем введите `Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
4. пакеты tooremove пакеты управления, оставшихся которого имеют зависимость от других управления System Center Advisor, используйте сценарий hello *RecursiveRemove.ps1* загруженный из более ранних версий hello центра сценариев TechNet.  
 
    > [!NOTE]
    > Не удаляйте hello пакетов управления Microsoft System Center Advisor или внутренней помощник по настройке ядра Microsoft System Center.  
    >  

5. Откройте консоль управления Operations Manager hello с учетной записью, которая является членом роли администраторов Operations Manager hello.
6. В разделе **администрирования**выберите hello **пакетов управления** узел и в hello **искать:** введите **помощник по настройке ядра** и проверьте hello в группе управления по-прежнему импортируются следующие пакеты управления:
   
   * Microsoft System Center Advisor;
   * Microsoft System Center Advisor Internal.
7. На портале OMS hello щелкните hello **параметры** плитки.
8. Выберите **Подключенные источники**.
9. В таблице hello под hello раздела System Center Operations Manager, вы увидите hello имя группы управления hello требуется tooremove из рабочей области hello.  В столбце hello **последние данные**, нажмите кнопку **удалить**.  
   
    > [!NOTE]
    > Hello **удалить** ссылка будет недоступен до через 14 дней Если активности не обнаружено из hello подключенной группы управления.  
    > 

10. Откроется окно с приглашением tooconfirm, что требуется tooproceed удаления hello.  Нажмите кнопку **Да** tooproceed. 

toodelete hello два соединителя - Microsoft.SystemCenter.Advisor.DataConnector и соединителя Advisor, сохраните сценарий PowerShell hello ниже tooyour компьютер и выполнить с использованием hello следующие примеры:

```
    .\OM2012_DeleteConnector.ps1 “Advisor Connector” <ManagementServerName>
    .\OM2012_DeleteConnectors.ps1 “Microsoft.SytemCenter.Advisor.DataConnector” <ManagementServerName>
```

> [!NOTE]
> Hello компьютера, к которому выполняется этот сценарий из, если он не является сервером управления, должен быть установлен в зависимости от версии hello группы управления Operations Manager командную hello.
> 
> 

```
    `param(
    [String] $connectorName,
    [String] $msName="localhost"
    )
    $mg = new-object Microsoft.EnterpriseManagement.ManagementGroup $msName
    $admin = $mg.GetConnectorFrameworkAdministration()
    ##########################################################################################
    # Configures a connector with hello specified name.
    ##########################################################################################
    function New-Connector([String] $name)
    {
         $connectorForTest = $null;
         foreach($connector in $admin.GetMonitoringConnectors())
    {
    if($connectorName.Name -eq ${name})
    {
         $connectorForTest = Get-SCOMConnector -id $connector.id
    }
    }
    if ($connectorForTest -eq $null)
    {
         $testConnector = New-Object Microsoft.EnterpriseManagement.ConnectorFramework.ConnectorInfo
         $testConnector.Name = $name
         $testConnector.Description = "${name} Description"
         $testConnector.DiscoveryDataIsManaged = $false
         $connectorForTest = $admin.Setup($testConnector)
         $connectorForTest.Initialize();
    }
    return $connectorForTest
    }
    ##########################################################################################
    # Removes a connector with hello specified name.
    ##########################################################################################
    function Remove-Connector([String] $name)
    {
        $testConnector = $null
        foreach($connector in $admin.GetMonitoringConnectors())
       {
        if($connector.Name -eq ${name})
       {
         $testConnector = Get-SCOMConnector -id $connector.id
       }
      }
     if ($testConnector -ne $null)
     {
        if($testConnector.Initialized)
     {
     foreach($alert in $testConnector.GetMonitoringAlerts())
     {
       $alert.ConnectorId = $null;
       $alert.Update("Delete Connector");
     }
     $testConnector.Uninitialize()
     }
     $connectorIdForTest = $admin.Cleanup($testConnector)
     }
    }
    ##########################################################################################
    # Delete a connector's Subscription
    ##########################################################################################
    function Delete-Subscription([String] $name)
    {
      foreach($testconnector in $admin.GetMonitoringConnectors())
      {
      if($testconnector.Name -eq $name)
      {
        $connector = Get-SCOMConnector -id $testconnector.id
      }
    }
    $subs = $admin.GetConnectorSubscriptions()
    foreach($sub in $subs)
    {
      if($sub.MonitoringConnectorId -eq $connector.id)
      {
        $admin.DeleteConnectorSubscription($admin.GetConnectorSubscription($sub.Id))
      }
     }
    }
    #New-Connector $connectorName
    write-host "Delete-Subscription"
    Delete-Subscription $connectorName
    write-host "Remove-Connector"
    Remove-Connector $connectorName
```

В будущем hello Если планируется повторное подключение OMS рабочей tooan вашей группы управления необходимо hello импорта toore `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` файл пакета управления из последнего накопительного пакета обновления hello применения tooyour группы управления.  Этот файл можно найти в hello `%ProgramFiles%\Microsoft System Center 2012` или hello `System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups` папки.

## <a name="next-steps"></a>Дальнейшие действия
функциональные возможности tooadd и сбор данных, см. [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).


