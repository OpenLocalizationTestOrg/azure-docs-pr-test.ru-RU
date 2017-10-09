---
title: "aaaManage Windows Azure Pack виртуальных машин из стека Azure | Документы Microsoft"
description: "Узнайте, как toomanage виртуальных машин Windows Azure Pack (MAP) из пользовательского портала hello Azure стека."
services: azure-stack
documentationcenter: 
author: walterov
manager: byronr
editor: 
ms.assetid: 213c2792-d404-4b44-8340-235adf3f8f0b
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: walterov
ms.openlocfilehash: 97dbe34055667a72fddc8507ae389562e885a32e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-windows-azure-pack-virtual-machines-from-azure-stack"></a>Управление виртуальными машинами Windows Azure Pack из стека Azure
В hello пакет средств разработки стек Azure вы можете включить доступ из hello Azure стека пользователя портала tootenant виртуальных машин, работающих на Windows Azure Pack. Клиенты могут использовать toomanage портала Azure стека hello их существующие виртуальные машины IaaS и виртуальных сетей. Эти ресурсы становятся доступными в Windows Azure Pack через hello базовых Service Provider Foundation (SPF) и Virtual Machine Manager (VMM) компонента. В частности клиенты могут:

* Просмотр ресурсов
* Просмотр значений конфигурации
* Остановка или запуск виртуальной машины
* Подключите виртуальную машину tooa через протокол удаленного рабочего стола (RDP)
* Создание и управление контрольными точками
* Удалите виртуальные машины и виртуальные сети

Эта функциональность обеспечивается hello соединителя пакет Windows Azure для стека Azure (Предварительная версия). В этой статье показано, как tooconfigure hello соединитель для среды стека Azure с одним узлом.

В этой предварительной версии соединителя hello помните о следующих hello.
* Используйте hello соединителя пакет Windows Azure только в тестовых сред (стек Azure и пакета Windows Azure), а не в производственной среде.
* Необходимо иметь Windows Azure Pack набор исправлений (UR) 9.1 или более поздней версии и System Center SPF и VMM с НАКОПИТЕЛЬНЫМ пакетом обновления 9 или более поздней версии.
* Hello VMM и SPF компонентов может быть System Center 2012 R2 или System Center 2016.
* На обоих стек Azure и пакета Windows Azure необходимо выполнить действия по настройке.
* Hello инструкции применяются toonon облачных сред Platform System (CPS).
* tooreview hello известные проблемы см. в разделе [Устранение неполадок Microsoft Azure стека](azure-stack-troubleshooting.md).


## <a name="architecture"></a>Архитектура
Hello следующей схеме показаны основные компоненты hello hello соединителя пакет Windows Azure.

![компоненты Windows Azure Pack Connector Hello](media/azure-stack-manage-wap/image1.png)

Обратите внимание, hello, приведенные ниже сведения:
* пользовательский портал Azure стека Hello обращается к hello сведения о ресурсах из обоих облаков (стек Azure и пакета Windows Azure).
* Hello пользователь должен иметь учетную запись, которая является допустимым в обеих средах.
* Hello Azure стека пользовательский портал должен иметь toohello компонентов доступа к сети, работающих на Windows Azure Pack.
* В hello **WAP** раздела схемы hello hello новый соединитель пакет Windows Azure модули (расширения WAP и соединителя) и получить hello существующих API Windows Azure Pack клиента с компонентами VMM и SPF.


## <a name="identity-management"></a>Управление удостоверениями
Hello API клиента Windows Azure Pack должен доверять hello службы маркеров безопасности Azure стека (STS).

Когда пользователь выполняет действие через портал Azure стека hello, ориентированном ресурсов пакета Windows Azure, портал hello использует hello API клиента Windows Azure Pack. Таким образом предоставляемые hello маркер проверки подлинности должны поступать из доверенных маркеров безопасности. В разделе hello, следующая схема:

![Схема проверки подлинности соединителя пакет Windows Azure](media/azure-stack-manage-wap/image2.png)

В среде комплект средств для разработки hello, пакет Windows Azure и Azure стека имеют независимых поставщиков. Пользователям, обращающимся к обеих средах с портала Azure стека hello должен иметь имя того же основного имени пользователя (UPN) в обоих поставщиков удостоверений hello. Например, hello учетной записи  *azurestackadmin@azurestack.local*  должны также существовать в hello STS для Windows Azure Pack. Где AD FS не настроен toosupport исходящих доверительных отношений, будут устанавливать отношения доверия из hello Windows Azure Pack компонентов (API клиента) toohello стека Azure экземпляра AD FS.

## <a name="prerequisites"></a>Предварительные требования

### <a name="download-hello-windows-azure-pack-connector"></a>Загрузите hello соединителя пакет Windows Azure
На hello [центра загрузки Майкрософт](https://aka.ms/wapconnectorazurestackdlc), загрузите файл .exe hello и извлеките его tooyour локального компьютера. Более поздней версии необходимо скопировать hello содержимое tooa компьютера, можно получить доступ к вашей среде Windows Azure Pack.

### <a name="deployment-option-requirement"></a>Параметр требования развертывания
toointegrate с пакетом Windows Azure, Azure стека можно развернуть с помощью параметр hello AD FS или Azure Active Directory hello.

### <a name="connectivity-requirements"></a>Требований к подключению
1. С hello компьютера, на котором доступ hello Azure стека пользовательского портала убедитесь в том, что можно обращаться из портала клиента Windows Azure Pack hello hello веб-браузера.
2. Виртуальная машина Hello AzS WASP01 стек Azure должна быть портала компьютер клиента Windows Azure Pack может tooconnect toohello. Используйте Ping.exe tooverify сетевое подключение. 
3.  Необходимо иметь действительные сертификаты для hello новый соединитель служб. Эти сертификаты SSL должен быть выдан доверенным центром сертификации (ЦС). Нельзя использовать самозаверяющие сертификаты. Hello SSL-сертификаты должны быть доверенными Azure стека (в частности hello AzS WASP01 ВМ) и любым другим компьютером, hello клиента может использовать tooaccess hello Azure стека пользовательского портала.
 
    >[!NOTE]
    Поскольку AzS WASP01 выполняется hello вариант установки основных серверных компонентов Windows Server, можно использовать средство командной строки, такие как Certutil.ext tooimport hello сертификат. Например, можно скопировать tooc:\temp файл .cer hello на AzS WASP01 и выполните команду hello **certutil - addstore «Калифорния» «c:\temp\certname.cer»**.

4.  tooWindows подключение RDP tooestablish виртуальных машин Azure Pack клиента через портал Azure стека hello, среды Windows Azure Pack hello должны разрешать виртуальные машины клиента toohello трафика удаленного рабочего стола.
5.  Для связи между Azure стека клиента виртуальных машин и виртуальных машин клиента Windows Azure Pack их внешних IP-адресов должно быть маршрутизируемым для hello двух средах. Эта связь также может включать связывание имена DNS-серверов tooresolve виртуальной машины между средами hello.

### <a name="iis-requirements"></a>Требования к IIS
Hello компьютера, на котором размещен портал клиента Windows Azure Pack hello (который может быть физического узла, виртуальной машины или несколько виртуальных машин) должен иметь после установки расширения IIS перепишите URL-адрес hello. Если не установлен, его можно загрузить из [здесь](https://www.iis.net/downloads/microsoft/url-rewrite). Если несколько виртуальных машин разместить портал клиента hello, установите расширение hello на каждой виртуальной машины.

## <a name="configure-azure-stack"></a>Настройка стек Azure
Прежде чем настраивать hello соединителя пакет Windows Azure, необходимо включить режим несколько компонентов в облаке на пользовательском портале hello Azure стека. Этот режим позволяет пользователям tooselect из tooaccess какие облачные ресурсы.

режим tooenable несколько компонентов в облаке, необходимо запустить hello AzurePackConnector.ps1 добавить скрипт после развертывания Azure стека. Hello в следующей таблице описаны параметры сценария hello.


|  Параметр | Описание | Пример |   
| -------- | ------------- | ------- |  
| AzurePackClouds | URI hello соединители пакет Windows Azure. Эти URI должен соответствовать toohello порталы клиентами Windows Azure Pack. | @{CloudName = «AzurePack1»; CloudEndpoint = «https://waptenantportal1:40005"},@{CloudName = «AzurePack2»; CloudEndpoint = «https://waptenantportal2:40005»}<br><br>  (По умолчанию hello значение порта не является 40005.) |  
| AzureStackCloudName | Метка toorepresent hello Azure стека облака.| «AzureStack» |
| DisableMultiCloud | Переключите режим несколько компонентов в облаке toodisable.| Недоступно |
| | |

Hello AzurePackConnector.ps1 добавить скрипт можно запустить сразу после развертывания, или более поздней версии. toorun Здравствуйте сразу после развертывания скрипт, используйте hello же сеанса Windows PowerShell, где развертывания Azure стека. В противном случае можно открыть новый сеанс Windows PowerShell с правами администратора (выполнили вход как учетная запись azurestackadmin hello).

1. Запустите сценарий hello AzurePackConnector.ps1 добавить с помощью hello, следующие команды (со средой определенные tooyour значения). Обратите внимание, hello AzurePackConnector добавить сценарий позволяет вам tooadd более одной конечной точки соединителя пакет Windows Azure.
 
 ```powershell
    $cred = New-Object System.Management.Automation.PSCredential("cloudadmin@azurestack.local", `
    (ConvertTo-SecureString -String "<password>" -AsPlainText -Force))
    $session = New-PSSession -ComputerName 'azs-ercs01' `
     -Credential $cred `
     -ConfigurationName PrivilegedEndpoint `
     -Authentication Credssp

    # Enable Multicloud
    Invoke-Command -Session $session -ScriptBlock { Add-AzurePackConnector -AzurePackClouds `
    @{CloudName = "AzurePack_1"; CloudEndpoint = "https://waptenantportal1:40005"},`
    @{CloudName = "AzurePack_2"; CloudEndpoint = "https://waptenantportal2:40005" } `
    -AzureStackCloudName "AzureStack" }

 ```
> [!NOTE]
> В текущем построении hello имеется проблема при окончании hello AzurePackConnector добавить скрипт остается в цикл опроса для длительного времени (несколько минут) до завершения. После появления сообщения hello **VERBOSE: шага «Настройка соединителя Azure Pack» состояние: «Успех»**, можно остановить hello сценарий или подождать, пока он перестает сам по себе. Он не будет провести различие, поскольку hello конфигурации уже завершилась успешно.

2. Запишите hello выходные файлы, созданные с помощью этого сценария, один для каждой среды Windows Azure Pack, указанный вами. Hello файлы расположены в: \\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput. Эти файлы содержат hello сведения, необходимые tooconfigure hello целевых Windows Azure Pack средах. Передать этот файл как сценарий tooa параметр позднее в этих инструкциях. Этот файл содержит hello следующую информацию:

    * **AzurePackConnectorEndpoint**: содержит toohello соединителя пакет Windows Azure hello конечной точки службы.
    * **AuthenticationIdentityProviderPartner**: содержит hello следующие пары значение:
        * Сертификат, который hello API клиента Windows Azure Pack для подписи маркера проверки подлинности должен tootrust tooaccept вызовы из hello расширения портала Azure стека.

        * Здравствуйте, «Области», связанной с hello сертификата для подписи. Например: https://adfs.local.azurestack.global.external/adfs/c1d72562-534e-4aa5-92aa-d65df289a107/.

3.  Обзор toohello папку, которая содержит hello выходные файлы (\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput) и копировать файлы hello tooyour локального компьютера. файлы Hello будет выглядеть аналогично toothis: AzurePack-06-27-15-50.txt.

4.  Конфигурация теста hello.

    а. Откройте в браузере и войдите в портал пользователей Azure стека toohello (https://portal.local.azurestack.external/).
    
    b. После входа в качестве клиента и hello портала загружает вы увидите ошибку в отсутствии подписок может toofetch или расширения из hello облако Azure Pack. Нажмите кнопку **ОК** tooclose эти сообщения. (Эти сообщения об ошибках исчезнут после настройки Windows Azure Pack.)

    c. Обратите внимание hello **облака** раскрывающегося списка в левом верхнем углу hello hello портала.

    ![Селектор облака Hello в пользовательском интерфейсе hello стек Azure](media/azure-stack-manage-wap/image3.png)

## <a name="configure-windows-azure-pack"></a>Настройка Windows Azure Pack
Для этого соединителя предварительной версии пакета Windows Azure требуется ручная настройка.

>[!IMPORTANT]
Для этой предварительной версии используйте hello соединителя пакет Windows Azure только в тестовой среде, а не в производственной среде.

1.  Установите соединитель MSI-файлы на приветствия Windows Azure Pack портала виртуальная машина клиента и установить сертификаты. (При наличии нескольких виртуальных машин портала клиента, необходимо выполнить это действие для каждой виртуальной машины.)

    а. В проводнике, скопируйте hello **WAPConnector** (что был загружен ранее) tooa папку с именем **c:\temp** hello клиента портала виртуальной машине.

    b. Откройте консоль или RDP соединение toohello портала виртуальной машины клиента.

    c. Измените каталоги слишком**c:\temp\wapconnector\setup\scripts**и выполнения hello **Connector.ps1 установки** tooinstall три MSI файлы сценариев. Параметры не требуются.

     ```powershell
    cd C:\temp\wapconnector\setup\scripts\

    .\Install-Connector.ps1
    ```
     d. Измените каталоги слишком**c:\inetpub** и проверки установки hello три новых сайтов:

       * Соединитель MgmtSvc

       * MgmtSvc ConnectorExtension

       * MgmtSvc ConnectorController

    д. Из hello же **c:\temp\wapconnector\setup\scripts** папки, запустите hello **Certificates.ps1 Настройка** скрипт tooinstall сертификаты. По умолчанию, он будет использовать hello одного сертификата, доступного для узла портала клиента hello в Windows Azure Pack. Убедитесь в том, что это действительный сертификат (доверенным для виртуальной машины Azure стека AzS-WASP01 hello и любого клиентского компьютера, получающего hello Azure стека портала). В противном случае связи не будут работать. (Кроме того, можно явно передать отпечаток сертификата как параметр с помощью hello - параметр отпечатка.)

     ```powershell
        cd C:\temp\wapconnector\setup\scripts\

        .\Configure-Certificates.ps1
    ```

    f. Конфигурация hello toofinish эти три службы запуска hello **WapConnector.ps1 Настройка** параметры файла Web.config hello tooupdate сценария.

    |  Параметр | Описание | Пример |   
    | -------- | ------------- | ------- |  
    | TenantPortalFQDN | портал клиента Windows Azure Pack Hello полное доменное имя. | tenant.contoso.com | 
    | TenantAPIFQDN | Здравствуйте, полное доменное имя Windows Azure Pack клиента API. | tenantapi.contoso.com  |
    | AzureStackPortalFQDN | пользовательский портал Azure стека Hello полное доменное имя. | Portal.local.azurestack.external |
    | | |
    
     ```powershell
    .\Configure-WapConnector.ps1 -TenantPortalFQDN "tenant.contoso.com" `
         -TenantAPIFQDN "tenantapi.contoso.com" `
         -AzureStackPortalFQDN "portal.local.azurestack.external"
    ```
    ж. При наличии нескольких виртуальных машин портала клиента, повторите шаг 1 для каждого из этих виртуальных машин.

2. Установка hello новый MSI API клиента на каждой виртуальной машине API клиента Windows Azure Pack.

    а. Если используется подсистемой балансировки нагрузки, вы можете toomark hello виртуальной машины как автономные.

    b. В проводнике, скопируйте hello **WAPConnector** tooa папка с именем **c:\temp** на каждом компьютере, API клиента.

    c. Копирование файла hello AzurePackConnectorOutput.txt сохраненный ранее, слишком**c:\temp\WAPConnector**.

    d. Откройте консоль или RDP соединение toohello виртуальных Машин API клиента, скопированные файлы hello.
    
    д. Измените каталоги слишком**c:\temp\wapconnector\setup\scripts**и запустите **TenantAPI.ps1 обновление**. Эту новую версию API клиента WAP hello содержит tooenable изменение отношения доверия не только с текущей STS hello, но также с hello экземпляр AD FS в Azure стека.

     ```powershell
    cd C:\temp\wapconnector\setup\packages\

    .\Update-TenantAPI.ps1
    ```

    f.  Повторите шаг 2 на другой виртуальной машине под управлением hello API клиента.
3. Из **только один** hello виртуальных машин API клиента, выполняли tooadd сценария hello TrustAzureStack.ps1 Настройка отношения доверия между hello API клиента и экземпляр hello AD FS стек Azure. Необходимо использовать учетную запись с базы данных Microsoft.MgmtSvc.Store toohello доступа sysadmin. Этот сценарий состоит из hello следующие параметры:

    | Параметр | Описание | Пример |
    | --------- | ------------| ------- |
   | SqlServer | имя SQL Server, содержащий базы данных Microsoft.MgmtSvc.Store hello hello Hello. Этот параметр является обязательным. | SQLServer | 
   | файл данных | Hello выходной файл, который был создан во время настройки hello режима несколько компонентов в облаке Azure стека hello ранее. Этот параметр является обязательным. | AzurePack-06-27-15-50.txt | 
   | PromptForSqlCredential | Указывает, что скрипт hello должен запросить интерактивно toouse учетных данных проверки подлинности SQL при подключении экземпляра SQL Server toohello. Hello, учитывая учетных данных необходимо иметь достаточные разрешения toouninstall баз данных, схемы и удалить имена входа пользователя. Если не указан, hello сценарии предполагается, что этот контекст текущего пользователя есть доступ. | Значение не требуется. |
   |  |  |

    Если вы не знаете toouse hello SQL Server, вы можете узнать. Подключите компьютер toohello API клиента и использовать файл Web.config интерфейса API клиента hello toounprotect команд hello Unprotect MgmtSvc hello, имя сервера в строке подключения hello. Снова помните toorun MgmtSvc защитить файл Web.config интерфейса API клиента tooprotect hello.

  ```powershell
  cd C:\temp\wapconnector\setup\scripts\

 .\Configure-TrustAzureStack.ps1 -SqlServer "SQLServer" `
       -DataFile "C:\temp\wapconnector\AzurePackConnectorOutput.txt"
  ```

## <a name="example"></a>Пример
Hello следующем примере показано полное развертывание соединителя пакет Windows Azure одним узлом стек Azure и две установки пакета Windows Azure Express. (Каждый экспресс-установки находится на одном компьютере с именами пример hello *wapcomputer1* и*wapcomputer2*.)

```powershell
# Run hello following script on hello Azure Stack host
$cred = New-Object System.Management.Automation.PSCredential("cloudadmin@azurestack.local",`
     (ConvertTo-SecureString -String "p@ssw0rd" -AsPlainText -Force))
$session = New-PSSession -ComputerName 'azs-ercs01' -Credential $cred `
     -ConfigurationName PrivilegedEndpoint -Authentication Credssp
 
# Enable Multicloud
invoke-command -Session $session -ScriptBlock { Add-AzurePackConnector -AzurePackClouds `
     @{CloudName = "AzurePack_1"; CloudEndpoint = "https://wapcomputer1.contoso.com:40005"},`
     @{CloudName = "AzurePack_2"; CloudEndpoint = "https://wapcomputer2.contoso.com:40005"}`
     -AzureStackCloudName "AzureStack" }  

```
Загрузите файл .exe hello из hello [центра загрузки Майкрософт](https://aka.ms/wapconnectorazurestackdlc), извлеките его и скопируйте папку tooa hello WAPConnector **c:\temp** папку на компьютере Windows Azure Pack hello. Скопируйте файлы hello, которые были созданы в качестве выходных данных в предыдущем сценарии hello (расположенный в \\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput) toohello **c:\temp\WAPConnector** папки. (hello файлы будут выглядит примерно toothis: AzurePack-06-27-15-50.txt.) Затем выполните следующий сценарий один раз в экземпляр Windows Azure Pack hello:

 ```powershell
# Install Connector components
cd C:\temp\WAPConnector\Setup\Scripts
.\Install-Connector.ps1

# Configure Certificates for hello new Connector services
.\Configure-Certificates.ps1

# Configure hello Connector services
.\Configure-WapConnector.ps1 -TenantPortalFQDN "wapcomputer1.contoso.com" `
     -TenantAPIFQDN "wapcomputer1.contoso.com" `
     -AzureStackPortalFQDN "portal.local.azurestack.external"

# Install hello updated TenantAPI
.\Update-TenantAPI.ps1

# Establish trust with hello Azure Stack AD FS
.\Configure-TrustAzureStack.ps1 -SqlServer "wapcomputer1" `
     -DataFile "C:\temp\wapconnector\AzurePack-06-27-15-50.txt" 

```
## <a name="troubleshooting-tips"></a>Советы по устранению неполадок
1.  Убедитесь, что имеется сетевое соединение между стек Azure и пакета Windows Azure. Это подключение должно быть между любой компьютере клиента, который обращается к портала Azure стека hello и hello Windows Azure Pack портала виртуальная машина клиента запущенным hello новый соединитель служб.
2.  Убедитесь, что все указанные правильность полных доменных имен.
3.  Убедитесь, что hello SSL-сертификатов, используемых в новые службы соединителя hello доверия со стороны Azure стека (в частности hello AzS WASP01 ВМ) и любым другим клиентом hello компьютер может использовать tooaccess hello Azure стека пользовательского портала.
4. Известные проблемы см. в разделе [Устранение неполадок Microsoft Azure стека](azure-stack-troubleshooting.md).


## <a name="next-steps"></a>Дальнейшие действия
[С помощью hello порталы администратора и пользователя в стек Azure](azure-stack-manage-portals.md)
