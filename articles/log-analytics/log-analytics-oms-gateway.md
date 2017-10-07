---
title: "с помощью tooOMS компьютеров aaaConnect hello шлюза OMS | Документы Microsoft"
description: "Связь устройства, управляемые OMS и компьютеров, отслеживаемых Operations Manager со службой OMS toohello данных toosend hello OMS шлюза, если они не имеют доступа к Интернету."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ae9a1623-d2ba-41d3-bd97-36e65d3ca119
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: magoedte
ms.openlocfilehash: 0cfa8f2fb66016e494f22c780e328be472b5fdee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-computers-without-internet-access-toooms-using-hello-oms-gateway"></a>Подключение компьютеров без tooOMS доступа Интернета с помощью hello шлюза OMS

В этом документе описывается, как ваш управляемых OMS и System Center Operations Manager мониторинг компьютеров могут отправлять службой OMS toohello данных при отсутствии доступа к Интернету. Hello OMS шлюз, который прямой прокси-сервер HTTP, поддерживающий туннелирование HTTP с помощью команды HTTP CONNECT hello, можно собирать данные и отправить службе OMS toohello от их имени.  

Hello OMS шлюз поддерживает:

* Гибридные компоненты Runbook Worker в службе автоматизации Azure  
* Компьютеры Windows с Microsoft Monitoring Agent hello непосредственно подключенные tooan рабочей области OMS
* Компьютеры Linux с hello агента OMS для Linux, напрямую подключенном tooan рабочей области OMS  
* System Center Operations Manager 2012 с пакетом обновления 1 (SP1) и накопительным пакетом обновления 7 (UR7), Operations Manager 2012 R2 с накопительным пакетом обновления 3 (UR3) или группу управления Operations Manager 2016, интегрируемую с OMS.  

Если ИТ политики безопасности не допускают компьютеры вашей toohello tooconnect сети Интернет, таких как точки продажи (POS) устройства или серверах, поддерживающих ИТ-служб, но необходимо tooconnect toomanage их tooOMS и отслеживать их, они могут быть настроены toocommunicate непосредственно с конфигурацией tooreceive шлюза OMS hello и отправлять данные от их имени.  Если эти компьютеры должны быть настроены toodirectly агента OMS hello подключиться tooan рабочей области OMS, все компьютеры вместо этого будут взаимодействовать с OMS шлюза hello.  Hello шлюз передает данные из агентов tooOMS hello напрямую, он не анализирует hello данных во время передачи.

При интеграции группы управления Operations Manager с OMS hello серверов управления можно настроенных tooconnect toohello сведения о конфигурации шлюза OMS tooreceive и отправки собранных данных в зависимости от решения hello, которые вы выбрали.  Агенты Operations Manager отправить некоторые данные, например предупреждения, оценки конфигурации, пространство экземпляра и сервера управления toohello емкости данных Operations Manager. Другие большие объемы данных, таких как журналы IIS, производительности и событий безопасности отправляются напрямую toohello OMS шлюза.  Если у вас есть один или шлюз Operations Manager задействовать дополнительные серверы, в сети Периметра или других toomonitor изолированной сети ненадежных систем, ему не удается связаться со шлюзом OMS.  Серверы Operations Manager шлюза может только сервер управления tooa отчетов.  Группы управления Operations Manager является настроенным toocommunicate с hello шлюза OMS, сведения о конфигурации прокси-сервера hello при автоматически распространяться tooevery управляемого агентом компьютера, настроенного toocollect данные для анализа журналов, даже если параметр Hello пуст.    

tooprovide высокого уровня доступности для прямого подключения или группы операций управления, взаимодействовать с OMS через шлюз hello, можно использовать tooredirect компонента балансировки сетевой нагрузки и распределять hello трафик через несколько серверов шлюзов.  Если один сервер шлюза выходит из строя, трафик hello — перенаправленный tooanother доступный узел.  

Рекомендуется установить агент OMS hello на компьютере hello hello шлюза OMS программного обеспечения toomonitor hello шлюза OMS и анализ данных производительности или события. Кроме того hello помогает hello агента OMS шлюза идентификации hello службы конечных точек, которые ему необходимы toocommunicate с.

Каждый агент должен иметь шлюз tooits подключения к сети, чтобы агенты автоматически перенести tooand данных из шлюза hello. Установка шлюза hello на контроллере домена не рекомендуется.

Следующая схема Hello показан поток данных из tooOMS прямой агентов с помощью сервера шлюза hello.  Агенты должны имеет их прокси-сервера конфигурации соответствия hello же hello порта шлюза OMS является настроенным toocommunicate с tooOMS.  

![Схема взаимодействия прямого агента с OMS](./media/log-analytics-oms-gateway/oms-omsgateway-agentdirectconnect.png)

Hello следующей схеме показан поток данных из tooOMS группы управления Operations Manager.   

![Схема взаимодействия Operations Manager с OMS](./media/log-analytics-oms-gateway/oms-omsgateway-opsmgrconnect.png)

## <a name="prerequisites"></a>Предварительные требования

При указании типа hello toorun компьютера шлюза OMS, этот компьютер должен иметь hello следующее:

* Windows 10, Windows 8.1, Windows 7
* Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008
* .NET Framework 4.5;
* 4-ядерный процессор и 8 ГБ памяти (минимальные требования).

### <a name="language-availability"></a>Доступность языковых версий

Hello шлюза OMS доступна hello следующие языки:

- Китайский (упрощенное письмо)
- Китайский (традиционное письмо)
- Чешский
- Нидерландский
- Английский
- Французский
- Немецкий
- Венгерский
- Итальянский
- Японский
- Корейский
- Польский
- Португальский (Бразилия)
- Португальский (Португалия)
- Русский
- испанский (международный).

## <a name="download-hello-oms-gateway"></a>Загрузите hello шлюза OMS

Существует три способа tooget hello последнюю версию файла установки шлюза OMS hello.

1. Загрузить hello [центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=54443).

2. Загрузите с портала OMS hello.  После входа в рабочую область OMS tooyour перейдите слишком**параметры** > **подключенные источники** > **серверов Windows** и нажмите кнопку **Загрузить шлюза OMS**.

3. Загрузить hello [портал Azure](https://portal.azure.com).  После входа сделайте следующее:  

   1. Обзор hello список служб, а затем выберите **анализа журналов**.  
   2. Выберите рабочую область.
   3. В колонке рабочей области в разделе **Общие** щелкните **Быстрый запуск**.
   4. В разделе **Выбор рабочей области данных источника tooconnect toohello**, нажмите кнопку **компьютеров**.
   5. В hello **Direct Agent** колонка, щелкните **загрузить шлюза OMS**.<br><br> ![скачивание шлюза OMS](./media/log-analytics-oms-gateway/download-gateway.png)


## <a name="install-hello-oms-gateway"></a>Установка шлюза OMS hello

tooinstall шлюз, выполните следующие шаги hello.  При установке предыдущей версии называвшиеся *сервера пересылки аналитика журналов*, он будет обновлен toothis выпуска.  

1. Папка назначения hello, дважды щелкните **OMS Gateway.msi**.
2. На hello **приветствия** щелкните **Далее**.<br><br> ![Мастер установки шлюза](./media/log-analytics-oms-gateway/gateway-wizard01.png)<br>
3. На hello **лицензионное соглашение** выберите **я принимаю условия соглашения hello в hello лицензионное соглашение** tooagree toohello лицензионное соглашение и нажмите кнопку **Далее**.
4. На hello **порт и прокси-адрес** страницы:
   1. Toobe номер порта TCP hello тип, используемый для шлюза hello. Программа установки настроит правило входящего трафика с этим номером порта в брандмауэре Windows.  значение по умолчанию Hello — 8080.
      Допустимый диапазон Hello hello номер порта — от 1 до 65535. Если входные данные hello не попадает в этот диапазон, появится сообщение об ошибке.
   2. Если hello сервера, где hello шлюз установлен toocommunicate потребностей через прокси, введите адрес прокси-сервера hello, где hello шлюз должен tooconnect. Например, `http://myorgname.corp.contoso.com:80`.  Если этот параметр пуст, hello шлюза попытается tooconnect toohello Internet напрямую.  Если ваш прокси-сервер требует проверки подлинности, введите имя пользователя и пароль.<br><br> ![Настройка прокси-сервера в мастере установки шлюза](./media/log-analytics-oms-gateway/gateway-wizard02.png)<br>   
   3. Щелкните **Далее**.
5. Если у вас Центр обновления Майкрософт включен, hello страницы центра обновления Майкрософт появляется здесь можно выбрать tooenable его. Сделайте выбор и нажмите кнопку **Далее**. В противном случае продолжайте toohello следующий шаг.
6. На hello **конечная папка** страницу, либо оставить hello расположение папки по умолчанию C:\Program Files\OMS шлюза или типа hello который нужно tooinstall шлюз и нажмите кнопку **Далее**.
7. На hello **готовности tooinstall** щелкните **установить**. Контроль учетных записей пользователей может появиться запрос tooinstall разрешение. Чтобы продолжить, нажмите кнопку **Да**.
8. После завершения установки нажмите кнопку **Готово**. Можно проверить, работает, открыв оснастку hello services.msc и убедитесь, что службы hello **шлюза OMS** отображается в списке hello службы и его состояние — **под управлением**.<br><br> ![Службы — шлюз OMS](./media/log-analytics-oms-gateway/gateway-service.png)  

## <a name="configure-network-load-balancing"></a>Настройка балансировки сетевой нагрузки
Можно настроить шлюз hello для обеспечения высокой доступности с помощью балансировки сетевой нагрузки (NLB) с помощью сети балансировку нагрузки Майкрософт (NLB) или подсистемы балансировки нагрузки на основе оборудования.  Hello балансировки нагрузки управляет трафика, перенаправляя hello запрошенных подключения из hello агенты OMS, а также серверы управления Operations Manager по его узлов. Если один сервер шлюза выходит из строя, hello трафика получает перенаправленный tooother узлы.

toolearn как toodesign и развертывания кластера балансировки сетевой нагрузки Windows Server 2016 см. в разделе [балансировки сетевой нагрузки](https://technet.microsoft.com/windows-server-docs/networking/technologies/network-load-balancing).  Hello следующие шаги описывают как tooconfigure Microsoft network кластера с балансировкой нагрузки.  

1.  Войдите на сервер Windows hello, которая является членом кластера балансировки сетевой Нагрузки hello с правами администратора.  
2.  Откройте диспетчер балансировки сетевой нагрузки в диспетчере сервера, щелкните **Инструменты**, а затем — **Диспетчер балансировки сетевой нагрузки**.
3. Щелкните правой кнопкой мыши IP-адрес кластера hello tooconnect сервер шлюза OMS с hello Microsoft Monitoring Agent установлен и нажмите кнопку **tooCluster добавить узел**.<br><br> ![Диспетчер балансировки нагрузки сети — Добавление tooCluster узла](./media/log-analytics-oms-gateway/nlb02.png)<br>
4. Введите IP-адрес сервера шлюза hello, что требуется tooconnect hello.<br><br> ![Диспетчер балансировки нагрузки сети — Добавление узла tooCluster: подключение](./media/log-analytics-oms-gateway/nlb03.png)

## <a name="configure-oms-agent-and-operations-manager-management-group"></a>Настройка агента OMS и группы управления Operations Manager
Hello следующем разделе описываются шаги на как tooconfigure непосредственно подключенные агенты OMS, группы управления Operations Manager и автоматизации Azure гибридные рабочие роли Runbook с toocommunicate hello OMS шлюза с OMS.  

toounderstand требования и шаги на как tooinstall hello агент OMS на компьютерах Windows, напрямую подключаясь tooOMS, в разделе [tooOMS компьютеров подключения Windows](log-analytics-windows-agents.md) или Linux компьютеров см. в разделе [подключение компьютеров с Linux tooOMS](log-analytics-linux-agents.md).

### <a name="configuring-hello-oms-agent-and-operations-manager-toouse-hello-oms-gateway-as-a-proxy-server"></a>Настройка агента OMS hello и hello toouse Operations Manager OMS шлюза в качестве прокси-сервера

### <a name="configure-standalone-oms-agent"></a>Настройка автономного агента OMS
В разделе [Настройка параметров прокси-сервера и брандмауэра с помощью Microsoft Monitoring Agent hello](log-analytics-proxy-firewall.md) сведения о настройке агента toouse прокси-сервера, который в данном случае является hello шлюза.  При развертывании нескольких серверов шлюзов в подсистему балансировки нагрузки сети hello OMS прокси-сервера используется конфигурация агента hello виртуальный IP-адрес hello балансировки сетевой Нагрузки:<br><br> ![Свойства Microsoft Monitoring Agent — настройки прокси-сервера](./media/log-analytics-oms-gateway/nlb04.png)

### <a name="configure-operations-manager---all-agents-use-hello-same-proxy-server"></a>Настройка Operations Manager — все агенты используйте hello один прокси-сервер
Можно настроить сервер шлюза hello tooadd Operations Manager.  Hello Operations Manager, конфигурация прокси-сервера будет автоматически примененную агенты tooall tooOperations диспетчера отчетов, даже если приветствия пуст.

toouse hello toosupport шлюза Operations Manager, необходимо иметь:

* Microsoft Monitoring Agent (версия агента — **8.0.10900.0** и более поздних версиях) устанавливается на сервере шлюза hello и настраивается для рабочих областей OMS hello, которые следует использовать toocommunicate.
* Hello шлюза необходимо иметь подключение к Интернету или подключенных tooa прокси-сервер, выполняющий.

> [!NOTE]
> Если указать значение для шлюза hello tooall агенты помещаются в стек пустые значения.


1. Консоль Operations Manager откройте hello и в разделе **Operations Management Suite**, нажмите кнопку **подключения** и нажмите кнопку **Настройка прокси-сервера**.<br><br> ![Operations Manager — настройка прокси-сервера](./media/log-analytics-oms-gateway/scom01.png)<br>
2. Выберите **использовать hello tooaccess сервера прокси-сервера Operations Management Suite** и введите IP-адрес сервера шлюза OMS hello hello или виртуальный IP-адрес hello балансировки сетевой Нагрузки. Убедитесь, что начинаются с Привет `http://` префикс.<br><br> ![Operations Manager — адрес прокси-сервера](./media/log-analytics-oms-gateway/scom02.png)<br>
3. Нажмите кнопку **Готово** Сервер Operations Manager — подключенных tooyour рабочей области OMS.

### <a name="configure-operations-manager---specific-agents-use-proxy-server"></a>Настройка Operations Manager (определенные агенты используют прокси-сервер)
Для больших или сложных средах вы можете только определенные серверы (или группы) toouse hello сервер шлюза OMS.  Для этих серверов не удается обновить hello Operations Manager агент напрямую как это значение перезаписывается hello глобальное значение для группы управления hello.  Вместо этого необходимо toopush правило, используемое hello toooverride эти значения.

> [!NOTE]
> Этот же метод конфигурации может быть использовано tooallow hello несколько серверов шлюзов OMS в вашей среде.  Например могут потребоваться определенные toobe серверы шлюза OMS, указано отдельно для каждого региона.

1. Привет открыть консоль Operations Manager и выберите hello **Authoring** рабочей области.  
2. В рабочей области разработка hello, выберите **правила** и нажмите кнопку hello **область** кнопку на панели инструментов Operations Manager hello. Если это кнопка недоступна, проверьте toomake том, что выбран объект, не папка в панели "Мониторинг" hello. Hello **ориентация объектов пакета управления** диалоговое окно отображает список распространенных целевых классов, групп или объектов.
3. Тип **службы работоспособности** в hello **искать** поле и выберите его из списка hello.  Нажмите кнопку **ОК**.  
4. Найдите правило hello **правилу параметр прокси-сервера помощник по настройке ядра** и инструментов консоли управления hello, щелкните **переопределяет** и затем слишком**переопределение hello Rule\For конкретного объекта данного класса: работоспособности Служба** и выберите из списка hello объекта.  При необходимости можно создать пользовательскую группу, содержащую hello объекта службы работоспособности серверов hello вы хотите tooapply tooand это переопределение, примените hello переопределение toothat группы.
5. В hello **свойства переопределения** диалоговое окно щелкните флажок в hello tooplace **переопределить** toohello следующего столбца **WebProxyAddress** параметр.  В hello **значение переопределения** введите hello URL-адрес обеспечения сервера шлюза OMS hello, начинающихся с hello `http://` префикс.
   >[!NOTE]
   > Правило tooenable hello не обязательно как автоматически уже управляются с помощью переопределения, содержащихся в пакете Microsoft System Center Advisor Secure Reference Override управления hello, предназначенных для hello группу серверов мониторинга в помощник по настройке ядра для Microsoft System Center.
   >
6. Выберите пакет управления из hello **выберите целевой пакет управления** базу данных или создайте новый незапечатанный пакет управления, щелкнув **New**.
7. После внесения необходимых изменений нажмите кнопку **ОК**.

### <a name="configure-for-automation-hybrid-workers"></a>Настройка поддержки гибридных рабочих ролей службы автоматизации
При наличии гибридных рабочих ролей Runbook службы автоматизации в вашей среде hello, выполнив действия предоставляют hello шлюз вручную, временные обходные пути tooconfigure toosupport их.

Привет, выполнив действия необходимо tooknow hello регион Azure, где находится hello учетной записи автоматизации. расположение hello toolocate:

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Выберите службу автоматизации Azure hello.
3. Выберите hello соответствующей учетной записи службы автоматизации Azure.
4. Просмотрите ее регион в разделе **Расположение**.<br><br> ![Портал Azure — расположение учетной записи автоматизации](./media/log-analytics-oms-gateway/location.png)  

Используйте следующий URL-адрес hello tooidentify таблицы для каждого расположения hello.

**URL-адреса службы Job Runtime Data**

| **расположение** | **URL-адрес** |
| --- | --- |
| Северо-центральный регион США |ncus-jobruntimedata-prod-su1.azure-automation.net |
| Западная Европа |we-jobruntimedata-prod-su1.azure-automation.net |
| Южно-центральный регион США |scus-jobruntimedata-prod-su1.azure-automation.net |
| Восток США 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| Центральная Канада |cc-jobruntimedata-prod-su1.azure-automation.net |
| Северная Европа |ne-jobruntimedata-prod-su1.azure-automation.net |
| Юго-Восточная Азия |sea-jobruntimedata-prod-su1.azure-automation.net |
| Центральная Индия |cid-jobruntimedata-prod-su1.azure-automation.net |
| Япония |jpe-jobruntimedata-prod-su1.azure-automation.net |
| Австралия |ase-jobruntimedata-prod-su1.azure-automation.net |

**URL-адреса службы агента**

| **расположение** | **URL-адрес** |
| --- | --- |
| Северо-центральный регион США |ncus-agentservice-prod-1.azure-automation.net |
| Западная Европа |we-agentservice-prod-1.azure-automation.net |
| Южно-центральный регион США |scus-agentservice-prod-1.azure-automation.net |
| Восток США 2 |eus2-agentservice-prod-1.azure-automation.net |
| Центральная Канада |cc-agentservice-prod-1.azure-automation.net |
| Северная Европа |ne-agentservice-prod-1.azure-automation.net |
| Юго-Восточная Азия |sea-agentservice-prod-1.azure-automation.net |
| Центральная Индия |cid-agentservice-prod-1.azure-automation.net |
| Япония |jpe-agentservice-prod-1.azure-automation.net |
| Австралия |ase-agentservice-prod-1.azure-automation.net |

Если компьютер автоматически регистрируется как гибридной рабочей роли Runbook для внесения исправлений с помощью решения управления обновлениями hello, выполните следующие действия.

1. Добавьте список узлов допускается toohello URL-адреса служб hello данных времени выполнения задания на hello OMS шлюза. Например: `Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
2. Перезапустите службу hello OMS шлюза с помощью hello, выполнив командлет PowerShell:`Restart-Service OMSGatewayService`

Если компьютер находится в борьбе tooAzure автоматизации с помощью командлета регистрации гибридной рабочей ролью Runbook hello, выполните следующие действия.

1. Добавьте hello агента службы регистрации URL-адрес узла допускается toohello список на hello OMS шлюза. Например: `Add-OMSGatewayAllowedHost ncus-agentservice-prod-1.azure-automation.net`
2. Добавьте список узлов допускается toohello URL-адреса служб hello данных времени выполнения задания на hello OMS шлюза. Например: `Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
3. Перезапустите службу шлюза OMS hello.
    `Restart-Service OMSGatewayService`

## <a name="useful-powershell-cmdlets"></a>Полезные командлеты PowerShell
Командлеты, которые помогут выполнить задачи, которые являются параметрами конфигурации шлюза для необходимых tooupdate hello OMS. Перед их использованием выполните следующее:

1. Установите hello OMS шлюза (MSI).
2. Откройте окно консоли PowerShell.
3. модуль tooimport hello, введите следующую команду:`Import-Module OMSGateway`
4. Если ошибки не возникают в предыдущем шаге hello, модуль hello успешно импортированы, и можно использовать командлеты hello. Введите `Get-Module OMSGateway`.
5. После внесения изменений с помощью командлетов hello убедитесь перезапуска службы шлюза hello.

При появлении ошибки в шаге 3 hello модуль не был импортирован. Hello ошибка может возникать, когда PowerShell работает модуль не удается toofind hello. Его можно найти в пути установки шлюза hello: *C:\Program Files\Microsoft OMS Gateway\PowerShell*.

| **Командлет** | **Параметры** | **Описание** | **Пример** |
| --- | --- | --- | --- |  
| `Get-OMSGatewayConfig` |Ключ |Возвращает конфигурацию hello hello службы |`Get-OMSGatewayConfig` |  
| `Set-OMSGatewayConfig` |Ключ (обязательно) <br> Значение |Здравствуйте, изменения конфигурации службы hello |`Set-OMSGatewayConfig -Name ListenPort -Value 8080` |  
| `Get-OMSGatewayRelayProxy` | |Возвращает hello адрес ретрансляции (вышестоящего) прокси-сервера |`Get-OMSGatewayRelayProxy` |  
| `Set-OMSGatewayRelayProxy` |Адрес<br> Имя пользователя<br> Пароль |Задает hello адреса (и учетных данных) (вышестоящего) ретрансляции прокси-сервера |1. Задайте прокси-сервер ретрансляции и учетные данные:<br> `Set-OMSGatewayRelayProxy`<br>`-Address http://www.myproxy.com:8080`<br>`-Username user1 -Password 123` <br><br> 2. Задайте прокси-сервер ретрансляции, для которого не требуется проверка подлинности: `Set-OMSGatewayRelayProxy`<br> `-Address http://www.myproxy.com:8080` <br><br> 3. Очистить hello ретрансляции параметры прокси-сервера:<br> `Set-OMSGatewayRelayProxy` <br> `-Address ""` |  
| `Get-OMSGatewayAllowedHost` | |В настоящее время возвращает hello разрешен узла (только для hello локально настроенных разрешенных узлов, не включает автоматически загружаемые допустимый узлов) |`Get-OMSGatewayAllowedHost` |
| `Add-OMSGatewayAllowedHost` |Узел (обязательно) |Добавляет в список разрешенных toohello узла hello |`Add-OMSGatewayAllowedHost -Host www.test.com` |  
| `Remove-OMSGatewayAllowedHost` |Узел (обязательно) |Удаляет из списка разрешенных hello hello узла |`Remove-OMSGatewayAllowedHost`<br> `-Host www.test.com` |  
| `Add-OMSGatewayAllowedClientCertificate` |Субъект (обязательно) |Добавляет в список разрешенных субъекта toohello hello клиентских сертификатов |`Add-OMSGatewayAllowed`<br>`ClientCertificate` <br> `-Subject mycert` |  
| `Remove-OMSGatewayAllowedClientCertificate` |Субъект (обязательно) |Удаляет из списка разрешенных hello hello субъекта сертификата клиента |`Remove-OMSGatewayAllowed` <br> `ClientCertificate` <br> `-Subject mycert` |  
| `Get-OMSGatewayAllowedClientCertificate` | |Возвращает hello разрешенные клиента субъектам сертификатов (только локально hello компьютер разрешенные субъекты, не включает автоматически загружаемые допустимый темы) |`Get-`<br>`OMSGatewayAllowed`<br>`ClientCertificate` |  

## <a name="troubleshooting"></a>Устранение неполадок
toocollect события, записанные hello шлюз, необходимо tooalso установлен агент OMS hello.<br><br> ![Средство просмотра событий — журнал шлюза OMS](./media/log-analytics-oms-gateway/event-viewer.png)

**Идентификаторы и описания событий шлюза OMS**

Hello следующей таблице приведены hello событий идентификаторы и описания для OMS шлюза журнала событий.

| **Идентификатор** | **Описание** |
| --- | --- |
| 400 |Любая ошибка приложения без определенного идентификатора |
| 401 |Неправильная конфигурация. Например, для параметра listenPort задано значение text вместо integer |
| 402 |Исключение при анализе сообщений подтверждения TLS |
| 403 |Сетевая ошибка. Например: не удается подключиться к серверу tootarget |
| 100 |Общие сведения |
| 101 |Служба запущена |
| 102 |Служба остановлена |
| 103 |Получена команда HTTP CONNECT от клиента |
| 104 |Команда HTTP CONNECT не получена |
| 105 |Целевой сервер не входит в список разрешенных или порт назначения hello не безопасного порта (443) <br> <br> Убедитесь, что агента MMA hello на вашем сервере шлюза и взаимодействия с hello шлюза агенты hello, подключенных toohello одной рабочей областью аналитики журналов. |
| 105 |Ошибка TCP-подключения — недопустимый сертификат клиента: CN=Gateway <br><br> Убедитесь в следующем: <br>    <br> &#149; используется шлюз версии 1.0.395.0 или более поздней; <br> &#149; Hello MMA агента на вашем сервере шлюза и взаимодействия с hello шлюза агенты hello, подключенных toohello одной рабочей областью аналитики журналов. |
| 106 |Какой-либо причине сеанса TLS hello подозрительных и отклоненных |
| 107 |сеанс TLS Hello проверен. |

**Toocollect счетчики производительности**

Hello следующей таблице показаны hello счетчики производительности, доступные для hello OMS шлюза. Можно добавить счетчики hello, с помощью системного монитора.

| **Имя** | **Описание** |
| --- | --- |
| Шлюз OMS — Active Client Connection (Активные клиентские подключения) |Количество активных сетевых подключений клиента (TCP) |
| Шлюз OMS — Error Count (Количество ошибок) |Количество ошибок |
| Шлюз OMS — Connected Client (Подключенные клиенты) |Количество подключенных клиентов |
| Шлюз OMS — Rejection Count (Количество отклонений) |Количество отклонений из-за ошибки проверки tooany TLS |

![Счетчики производительности шлюза OMS](./media/log-analytics-oms-gateway/counters.png)

## <a name="get-assistance"></a>Получение справки
Когда вы будете toohello вход в портал Azure, можно создать запрос для получения помощи hello OMS шлюза или другие службы Azure и функций службы.
помощь toorequest щелкните символ вопросительного знака hello в верхнем правом углу hello hello портала, а затем нажмите кнопку **New поддерживает запрос**. Завершите hello новую форму запроса поддержки.

![Новый запрос на техническую поддержку](./media/log-analytics-oms-gateway/support.png)

Также можно оставить отзыв о OMS или анализа журналов на hello [форуме обратной связи Microsoft Azure](https://feedback.azure.com/forums/267889).

## <a name="next-steps"></a>Дальнейшие действия
* [Добавить источники данных](log-analytics-data-sources.md) toocollect данные из hello подключенные источники в рабочую область OMS и их сохранения в репозитории OMS hello.
