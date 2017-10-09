---
title: "tooCreate PowerShell aaaUse ВМ с собственного сервера отчетов в режиме | Документы Microsoft"
description: "В этом разделе описываются и предоставляются пошаговые hello развертывание и настройку сервера отчетов собственный режим служб отчетов SQL Server на виртуальной машине Azure. "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a>Использовать tooCreate PowerShell Azure ВМ с собственного режима сервера отчетов
> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

В этом разделе описываются и предоставляются пошаговые hello развертывание и настройку сервера отчетов собственный режим служб отчетов SQL Server на виртуальной машине Azure. Hello шаги в этом документе используется сочетание действий вручную toocreate hello виртуальной машины и сценарий Windows PowerShell tooconfigure Reporting Services на hello виртуальной Машины. Hello скрипт конфигурации включает Открытие порта брандмауэра для протоколов HTTP и HTTPs.

> [!NOTE]
> Если не требуется **HTTPS** на сервере отчетов hello **пропустите шаг 2**.
> 
> После создания виртуальной Машины hello в шаге 1, перейдите в раздел toohello использовать tooconfigure сценария hello сервер отчетов и HTTP. После запуска сценария hello hello сервер отчетов будет готов toouse.

## <a name="prerequisites-and-assumptions"></a>Предварительные требования и предположения
* **Подписка Azure**: Проверьте hello количество ядер, доступных для вашей подписки Azure. Если вы создаете hello, рекомендуется использовать размер виртуальной Машины **A3**, требуется **4** доступных ядер. При использовании виртуальной машины размера **A2** необходимо **2** доступных ядра.
  
  * Максимальное количество ядер hello tooverify для вашей подписки в hello классический портал Azure, щелкните параметры hello левой панели, а затем нажмите кнопку использование в верхнем меню hello.
  * tooincrease hello квоты ядер, обратитесь в службу [поддержки Azure](https://azure.microsoft.com/support/options/). Дополнительные сведения о размере виртуальной машины см. в разделе [Размеры виртуальных машин в Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* **Скрипты Windows PowerShell**: hello раздела предполагает, что основные опыт работы с Windows PowerShell. Дополнительные сведения об использовании Windows PowerShell см. в разделе hello следующее:
  
  * [Запуск Windows PowerShell в Windows Server](https://technet.microsoft.com/library/hh847814.aspx)
  * [Приступая к работе с Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a>Шаг 1. Подготовка виртуальной машины Azure
1. Обзор toohello классический портал Azure.
2. Нажмите кнопку **виртуальные машины** hello левой панели.
   
    ![виртуальные машины microsoft azure](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. Нажмите кнопку **Создать**.
   
    ![кнопка создания](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. Щелкните **Из коллекции**.
   
    ![новая виртуальная машина из коллекции](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. Нажмите кнопку **SQL Server 2014 RTM Standard — Windows Server 2012 R2** и щелкните стрелку toocontinue hello.
   
    ![Далее](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    Если вам требуются hello служб Reporting Services управляемые данными подписки, выберите **SQL Server 2014 RTM Enterprise — Windows Server 2012 R2**. Дополнительные сведения о выпусках SQL Server и поддержке функций см. в разделе [функции, поддерживаемые различными выпусками SQL Server 2012 hello](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).
6. На hello **конфигурации виртуальной машины** измените hello следующие поля:
   
   * Если имеется более одного **Дата выпуска версии**, выберите hello самой последней версии.
   * **Имя виртуальной машины**: hello имя компьютера используется на следующей странице конфигурации hello как имя DNS облачной службы по умолчанию hello. имя DNS Hello должен быть уникальным для hello службы Azure. Рассмотрите возможность hello виртуальной Машины с именем компьютера, описывающий какие hello ВМ используется для. Например, ssrsnativecloud.
   * **Уровень**: «Стандартный».
   * **Размер: A3** hello рекомендуется использовать размер виртуальной Машины для рабочих нагрузок SQL Server. Если ВМ используется только как сервер отчетов, достаточно ВМ размера А2 если только сервер отчетов hello приходится обрабатывать значительные рабочие нагрузки. Для получения информации о ценах на виртуальные машины см. страницу [Цены на виртуальные машины](https://azure.microsoft.com/pricing/details/virtual-machines/).
   * **Новое имя пользователя**: hello именем создается с правами администратора на hello виртуальной Машины.
   * **Новый пароль** и **Подтверждение**. Этот пароль используется для новой учетной записи администратора hello и рекомендуется использовать надежный пароль.
   * Щелкните **Далее**. ![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
7. На следующей странице hello измените hello следующие поля:
   
   * **Облачная служба**: выберите **Создать новую облачную службу**.
   * **Облачные службы DNS-имя**: это hello открытому DNS-имени облачной службы, связанный с виртуальной Машины hello hello. Hello по умолчанию используется имя hello, введенного в hello имя виртуальной Машины. Если на последующих этапах раздела hello Создание доверенного SSL-сертификата и затем hello DNS-имя используется для значения hello hello»**выдан**«hello сертификата.
   * **Регион, территориальная группа или виртуальная сеть**: выберите hello области ближайший tooyour конечных пользователей.
   * **Учетная запись хранения**. Используйте автоматически созданную учетную запись хранения.
   * **Группа доступности**: нет.
   * **Конечные ТОЧКИ** Keep hello **удаленного рабочего стола** и **PowerShell** конечные точки и затем добавить конечную точку HTTP или HTTPS, в зависимости от среды.
     
     * **HTTP**: hello, общие и частные порты по умолчанию **80**. Обратите внимание, что если вы используете частный порт, отличный от 80, измените **$HTTPport = 80** в скрипте http hello.
     * **HTTPS**: hello, общие и частные порты по умолчанию **443**. Рекомендации по безопасности — toochange hello частный порт и настройте ваш брандмауэр и hello отчетов сервера toouse hello частный порт. Дополнительные сведения о конечных точках см. в разделе [как tooSet Настройка обмена данными с виртуальной машиной](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Обратите внимание, что если используется другой порт, измените параметр hello **$HTTPsport = 443** в hello скрипт HTTPS.
   * Нажмите кнопку «Далее». ![Далее](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. На последней странице приветствия мастера hello, оставьте значение по умолчанию hello **установки агента виртуальной Машины hello** выбранных. Hello действия, описанные в этом разделе не используют агент виртуальной Машины hello но если планируется tookeep эту виртуальную Машину, агент ВМ hello и расширения можно будет tooenhance he CM.  Дополнительные сведения о hello агент виртуальной Машины в разделе [агент ВМ и расширения — часть 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/). Один запускающим рекламу расширения, установленные по умолчанию hello hello расширение BGINFO, который отображается на рабочем столе виртуальной Машины hello, системные сведения, такие как внутренний IP-адрес и свободного диска пространства.
9. Щелкните «Готово». ![ОК](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. Hello **состояние** из виртуальной Машины отображается в виде hello **запуск (Подготовка)** во время процесса подготовки hello, а затем отображается как **под управлением** при hello виртуальная машина провизионирована и готова toouse.

## <a name="step-2-create-a-server-certificate"></a>Шаг 2. Создание сертификата сервера
> [!NOTE]
> Если не требуется HTTPS на сервере отчетов hello, вы можете **пропустите шаг 2** и перейдите в раздел toohello **использовать сервер отчетов hello tooconfigure скрипта и HTTP**. Используйте hello HTTP сценария tooquickly Настройка сервера отчетов hello и hello отчетов, сервер будет готов toouse.

В порядке toouse HTTPS на hello виртуальной Машины необходим доверенный SSL-сертификат. В зависимости от вашего сценария можно использовать один из следующих двух методов hello:

* Допустимый SSL-сертификат, выданный центром сертификации (ЦС) и являющийся доверенным для корпорации Майкрософт. Сертификаты корневого ЦС Hello, требуется toobe распространяются через hello программы корневых сертификатов Майкрософт. Дополнительные сведения об этой программе см. в разделе [Windows и программе корневых сертификатов для 8 Windows Phone SSL (член центра сертификации)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) и [toohello введение программы корневых сертификатов Майкрософт](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).
* Самозаверяющий сертификат. Самозаверяющие сертификаты не рекомендуется использовать для рабочих сред.

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a>toouse создать сертификат доверенного центра сертификации (ЦС)
1. **Запросите сертификат сервера для веб-сайта hello в центре сертификации**. 
   
    Можно использовать любой файл запроса сертификата (Certreq.txt), следует отправить tooa центром сертификации или toogenerate запрос для сетевого центра сертификации toogenerate приветствия мастера сертификатов веб-сервера. Например, службы сертификатов Майкрософт в Windows Server 2012. В зависимости от уровня контроля идентификации, который обеспечивает сертификат сервера hello он несколько дней tooseveral месяцев в tooapprove центра сертификации hello запроса и выдачу файла сертификата. 
   
    Дополнительные сведения о запросе сертификатов сервера см. в следующем hello: 
   
   * Использование [Certreq](https://technet.microsoft.com/library/cc725793.aspx).[](https://technet.microsoft.com/library/cc725793.aspx)
   * TooAdminister средств безопасности Windows Server 2012.
     
     [TooAdminister средств безопасности Windows Server 2012](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > Hello **выдан** поле hello доверенного SSL-сертификат должен быть hello же, как hello **DNS-имя облачной службы** вы использовали для hello новой виртуальной Машины.

2. **Установка сертификата сервера hello на веб-сервере hello**. в этом случае Hello веб-сервера является hello виртуальной Машины, узлы hello сервера отчетов и веб-сайт hello создается позднее при настройке служб Reporting Services. Дополнительные сведения об установке сертификата сервера hello на hello веб-сервере с помощью оснастки Certificate MMC hello см. в разделе [установить сертификат сервера](https://technet.microsoft.com/library/cc740068).
   
    Если требуется toouse hello скрипт, приведенный в этом разделе, сервер отчетов tooconfigure hello, hello значение hello сертификатов **отпечаток** используется в качестве параметра скрипта hello. В подразделе hello Далее подробности о как tooobtain hello отпечаток сертификата hello.
3. Назначение сервера отчетов toohello сертификат сервера hello. При настройке сервера отчетов hello в следующем разделе hello завершения Hello назначения.

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a>hello toouse самозаверяющего сертификата виртуальных машин
Самозаверяющий сертификат был создан hello виртуальной Машины во время инициализации hello виртуальной Машины. Hello сертификат имеет точно такое же имя, как hello ВМ DNS-имя hello. В ошибки сертификатов tooavoid заказ, она необходима, hello сертификат является доверенным на самой ВМ hello, а также всеми пользователями сайта hello.

1. tootrust hello корневого ЦС сертификата hello на hello локальной виртуальной Машины, добавьте hello сертификат toohello **доверенные корневые центры сертификации**. Hello ниже приводится сводка необходимых шагов hello. Подробные инструкции по как tootrust hello ЦС см. в разделе [установить сертификат сервера](https://technet.microsoft.com/library/cc740068).
   
   1. Hello классический портал Azure, выберите hello виртуальную Машину и щелкните "Подключить". В зависимости от настройки браузера может быть запрос toosave RDP-файл для подключения toohello виртуальной Машины.
      
       ![подключение tooazure виртуальной машины](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Используйте имя виртуальной Машины hello пользователя, имя пользователя и пароль, настроенные при создании hello виртуальной Машины. 
      
       Например, в hello после изображения, — имя виртуальной Машины hello **ssrsnativecloud** и имя пользователя hello **testuser**.
      
       ![имя для входа включает в себя имя виртуальной машины](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. Запустите mmc.exe. Дополнительные сведения см. в разделе [как: Просмотр сертификатов с hello оснастки MMC](https://msdn.microsoft.com/library/ms788967.aspx).
   3. В консольном приложении hello **файл** меню, добавить hello **сертификаты** оснастку, выберите **учетная запись компьютера** при появлении соответствующего запроса и нажмите кнопку **Далее**.
   4. Выберите **локального компьютера** toomanage и нажмите кнопку **Готово**.
   5. Нажмите кнопку **ОК** и разверните hello **сертификаты — личных** узлов и нажмите кнопку **сертификаты**. Hello сертификат названные hello DNS-имя виртуальной Машины hello и заканчивается **cloudapp.net**. Щелкните правой кнопкой мыши имя сертификата hello и нажмите кнопку **копирования**.
   6. Разверните hello **доверенные корневые центры сертификации** узел и щелкните правой кнопкой **сертификаты** и нажмите кнопку **вставить**.
   7. toovalidate, double, щелкните имя сертификата hello под **доверенные корневые центры сертификации** и убедитесь, что отсутствуют ошибки, и вы видите свой сертификат. Если требуется toouse hello HTTPS скрипт, приведенный в этом разделе, сервер отчетов tooconfigure hello, hello значение hello сертификатов **отпечаток** используется в качестве параметра скрипта hello. **Значение отпечатка hello tooget**, выполните следующие hello. В разделе имеется также отпечаток PowerShell tooretrieve образец hello [сервер отчетов сценария tooconfigure hello и HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).
      
      1. Дважды щелкните имя сертификата hello, например ssrsnativecloud.cloudapp.net hello.
      2. Нажмите кнопку hello **сведения** вкладки.
      3. Щелкните **Отпечаток**. значение Hello hello отпечатка появится в поле сведений о hello, например a6 08 3В df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.
      4. Скопируйте отпечаток hello и сохранить значение hello на более поздний срок или изменить скрипт hello сейчас.
      5. (*) Перед запуском сценария hello, удалите hello пробелы между парами значений hello. Например hello отпечаток, отмеченный ранее, теперь будет a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.
      6. Назначение сервера отчетов toohello сертификат сервера hello. При настройке сервера отчетов hello в следующем разделе hello завершения Hello назначения.

Если вы используете самозаверяющий сертификат SSL, hello имя на сертификате hello уже соответствует hello узла hello виртуальной Машины. Таким образом hello DNS hello машины уже зарегистрирована глобально и может осуществляться из любого клиента.

## <a name="step-3-configure-hello-report-server"></a>Шаг 3: Настройка сервера отчетов hello
В этом разделе описывается настройка hello виртуальной Машины, как сервер отчетов собственного режима служб Reporting Services. Можно использовать один из следующий сервер отчетов hello tooconfigure методы hello:

* Использовать hello сценария tooconfigure hello сервер отчетов
* Здравствуйте, tooConfigure используйте диспетчер конфигурации сервера отчетов.

Подробные инструкции см. раздел hello [toohello подключение виртуальной машины и начала hello диспетчер конфигурации служб Reporting Services](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).

**Примечание о проверке подлинности:** hello, рекомендуется использовать метод проверки подлинности — проверка подлинности Windows и проверка подлинности служб Reporting Services по умолчанию hello. Только пользователи, которые настроены на hello виртуальной Машины могут обращаться к службам отчетов и назначения ролей, служб tooReporting.

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a>Использовать сценарий tooconfigure hello сервер отчетов и HTTP
toouse hello Windows PowerShell скрипт tooconfigure hello сервера отчетов, полный hello следующие шаги. Hello Настройка включает HTTP, HTTPS не:

1. Hello классический портал Azure, выберите hello виртуальную Машину и щелкните "Подключить". В зависимости от настройки браузера может быть запрос toosave RDP-файл для подключения toohello виртуальной Машины.
   
    ![подключение tooazure виртуальной машины](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Используйте имя виртуальной Машины hello пользователя, имя пользователя и пароль, настроенные при создании hello виртуальной Машины. 
   
    Например, в hello после изображения, — имя виртуальной Машины hello **ssrsnativecloud** и имя пользователя hello **testuser**.
   
    ![имя для входа включает в себя имя виртуальной машины](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. Откройте на hello виртуальной Машины, **интегрированной среды Сценариев Windows PowerShell** с правами администратора. Hello интегрированной среды Сценариев PowerShell устанавливается по умолчанию в Windows server 2012. Рекомендуется использовать hello ISE вместо стандартного окна Windows PowerShell, чтобы вставить скрипт hello в hello интегрированной среды Сценариев, измените сценарий hello и затем запустите скрипт hello.
3. В Windows PowerShell ISE щелкните hello **представление** меню и нажмите кнопку **Показать область сценариев**.
4. Скопируйте следующий скрипт hello и вставьте сценарий hello в области сценариев интегрированной среды Сценариев Windows PowerShell hello.
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. Если вы создали hello виртуальной Машины с HTTP-порт, отличный от 80, измените параметр hello $HTTPport = 80.
6. сценарий Hello в настоящее время настроен для служб Reporting Services. Скрипт hello toorun для служб Reporting Services, измените часть версии приветствия имен toohello пути hello слишком «v11» в инструкции Get-WmiObject hello.
7. Запустите сценарий hello.

**Проверка**: tooverify работы hello базовых функций сервера отчетов в разделе hello [конфигурации hello Убедитесь](#verify-the-configuration) далее в этом разделе.

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a>Сервер отчетов сценария tooconfigure hello и HTTPS
toouse Windows PowerShell tooconfigure hello сервера отчетов, полный hello следующие шаги. Конфигурация Hello включает HTTPS, а не HTTP.

1. Hello классический портал Azure, выберите hello виртуальную Машину и щелкните "Подключить". В зависимости от настройки браузера может быть запрос toosave RDP-файл для подключения toohello виртуальной Машины.
   
    ![подключение tooazure виртуальной машины](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Используйте имя виртуальной Машины hello пользователя, имя пользователя и пароль, настроенные при создании hello виртуальной Машины. 
   
    Например, в hello после изображения, — имя виртуальной Машины hello **ssrsnativecloud** и имя пользователя hello **testuser**.
   
    ![имя для входа включает в себя имя виртуальной машины](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. Откройте на hello виртуальной Машины, **интегрированной среды Сценариев Windows PowerShell** с правами администратора. Hello интегрированной среды Сценариев PowerShell устанавливается по умолчанию в Windows server 2012. Рекомендуется использовать hello ISE вместо стандартного окна Windows PowerShell, чтобы вставить скрипт hello в hello интегрированной среды Сценариев, измените сценарий hello и затем запустите скрипт hello.
3. выполнение скриптов, запустите следующую команду Windows PowerShell hello tooenable:
   
        Set-ExecutionPolicy RemoteSigned
   
    Можно выполнять следующие политики hello tooverify hello:
   
        Get-ExecutionPolicy
4. В **интегрированной среды Сценариев Windows PowerShell**, нажмите кнопку hello **представление** меню и нажмите кнопку **Показать область сценариев**.
5. Скопируйте hello следующий скрипт и вставьте его в области сценариев интегрированной среды Сценариев Windows PowerShell hello.
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. Изменение hello **$certificatehash** параметр в скрипте hello:
   
   * Это **обязательный** параметр. Если вы не сохраняли значение сертификата hello hello предыдущих шагах, используйте один из hello следующую хэш-значения методов toocopy hello сертификата из отпечатка сертификата hello.:
     
       На hello виртуальной Машины откройте Windows PowerShell ISE и выполните следующую команду hello:
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       Hello результат будет выглядеть примерно следующие toohello. Если hello скрипт возвращает пустую строку, hello виртуальная машина не имеет сертификата, настроенного для примера см. в разделе разделе hello [toouse hello самозаверяющего сертификата виртуальных машин](#to-use-the-virtual-machines-self-signed-certificate).
     
     ИЛИ
   * На hello mmc.exe запуска виртуальной Машины, а затем добавьте hello **сертификаты** оснастки.
   * В разделе hello **доверенные корневые центры сертификации** дважды щелкните имя своего сертификата. При использовании самозаверяющего сертификата ВМ hello hello сертификат hello названные hello DNS-имя виртуальной Машины hello и заканчивается **cloudapp.net**.
   * Нажмите кнопку hello **сведения** вкладки.
   * Щелкните **Отпечаток**. значение Hello hello отпечатка появится в поле сведений о hello, например af 11 60 b6 4b d 28 8 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48
   * **Перед запуском сценария hello**, удалите hello пробелы между парами значений hello. Например, af1160b64b288d890a8212ff6ba9c3664f319048.
7. Изменение hello **$httpsport** параметр: 
   
   * Если используется порт 443 для конечной точки HTTPS hello, то вам не требуется tooupdate этот параметр в скрипте hello. В противном случае используйте значение порта hello, выбранных при настройке частной конечной точки HTTPS hello на hello виртуальной Машины.
8. Изменение hello **$DNSName** параметр: 
   
   * скрипт Hello настроен для шаблона сертификата $DNSName = «+». В противном случае tooconfigure не требуется для привязки шаблона сертификата, закомментируйте $DNSName = "+ «и включите следующие линии ссылку $DNSNAme полный hello, ## $DNSName="$server.cloudapp.net hello».
     
       Измените значение hello $DNSName, если не хотите, чтобы DNS-имя toouse hello виртуальной машины для служб Reporting Services. При использовании параметра hello hello сертификат также должен использовать это имя и зарегистрировать имя hello глобально на DNS-сервер.
9. сценарий Hello в настоящее время настроен для служб Reporting Services. Скрипт hello toorun для служб Reporting Services, измените часть версии приветствия имен toohello пути hello слишком «v11» в инструкции Get-WmiObject hello.
10. Запустите сценарий hello.

**Проверка**: tooverify работы hello базовых функций сервера отчетов в разделе hello [конфигурации hello Убедитесь](#verify-the-connection) далее в этом разделе. привязки сертификата hello tooverify откройте командную строку с правами администратора и запустите hello следующую команду:

    netsh http show sslcert

Hello результат будет содержать hello следующее:

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a>Hello tooConfigure используйте диспетчер конфигурации сервера отчетов
Если не требуется toorun сценария PowerShell hello tooconfigure сервер отчетов hello, выполните действия hello в этот раздел toouse hello служб отчетов собственного режима сервера configuration manager tooconfigure hello отчета.

1. Hello классический портал Azure, выберите hello виртуальную Машину и щелкните "Подключить". Используйте hello имя пользователя и пароль, настроенные при создании hello виртуальной Машины.
   
    ![подключение tooazure виртуальной машины](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. Запустите Центр обновления Windows и установите toohello обновления виртуальной Машины. Если требуется перезагрузка hello виртуальной Машины, перезапустите hello виртуальной Машины и повторного подключения toohello виртуальной Машины из hello классический портал Azure.
3. В меню Пуск hello на hello виртуальной Машины введите **служб Reporting Services** и откройте **диспетчер конфигурации служб Reporting Services**.
4. Оставьте значения по умолчанию hello **имя сервера** и **экземпляра сервера отчетов**. Щелкните **Подключить**.
5. Hello левой панели щелкните **URL веб-службы**.
6. По умолчанию для служб Reporting Services задан HTTP-порт 80 с IP-адресом "Все назначенные". tooadd HTTPS:
   
   1. В **SSL-сертификат**: hello выберите сертификат, который будет toouse, например [имя виртуальной Машины]. cloudapp.net. Если сертификаты не указаны, в разделе hello **шаг 2: Создание сертификата сервера** сведения о hello как tooinstall и отношения доверия сертификата на hello виртуальной Машины.
   2. В поле **SSL-порт**выберите значение 443. Если вы настроили частной конечной точки HTTPS hello в hello виртуальной Машины с другой частный порт, укажите это значение здесь.
   3. Нажмите кнопку **применить** и дождитесь toocomplete операции hello.
7. Hello левой панели щелкните **базы данных**.
   
   1. Щелкните **Изменение базы данных**.
   2. Щелкните элемент **Создать новую базу данных сервера отчетов** и нажмите кнопку **Далее**.
   3. Оставьте по умолчанию hello **имя сервера**: виде hello виртуальной Машины именем и оставьте по умолчанию hello **тип проверки подлинности** как **текущего пользователя** — **встроенной безопасности**. Щелкните **Далее**.
   4. Оставьте по умолчанию hello **имя базы данных** как **ReportServer** и нажмите кнопку **Далее**.
   5. Оставьте по умолчанию hello **тип проверки подлинности** как **учетные данные службы** и нажмите кнопку **Далее**.
   6. Нажмите кнопку **Далее** на hello **Сводка** страницы.
   7. После завершения настройки hello, нажмите кнопку **Готово**.
8. Hello левой панели щелкните **URL-адрес диспетчера отчетов**. Оставьте по умолчанию hello **виртуальный каталог** как **отчеты** и нажмите кнопку **применить**.
9. Нажмите кнопку **выхода** tooclose hello диспетчер конфигурации служб Reporting Services.

## <a name="step-4-open-windows-firewall-port"></a>Шаг 4. Открытие порта в брандмауэре Windows
> [!NOTE]
> Если используется один сервер отчетов hello tooconfigure сценарии hello, этот раздел можно пропустить. скрипт Hello включено порт брандмауэра hello tooopen шаг. по умолчанию Hello был порт 80 для HTTP и порт 443 для HTTPS.
> 
> 

tooconnect удаленно tooReport Manager или hello-отчетов на hello виртуальной Машины требуется Server на виртуальной машине hello, конечной точке TCP. Это обязательный tooopen hello же порт в брандмауэре ВМ hello. Конечная точка Hello был создан во время инициализации hello виртуальной Машины.

В этом разделе приведены базовые сведения о как tooopen hello порт брандмауэра. Дополнительные сведения см. в статье [Настройка брандмауэра для доступа к серверу отчетов](https://technet.microsoft.com/library/bb934283.aspx).

> [!NOTE]
> Если используется сервер отчетов hello tooconfigure сценария hello, этот раздел можно пропустить. скрипт Hello включено порт брандмауэра hello tooopen шаг.
> 
> 

Если вы настроили частный порт для протокола HTTPS, отличный от 443, измените следующий сценарий соответствующим образом hello. порт tooopen **443** на hello брандмауэр Windows, выполните следующие hello:

1. Откройте окно Windows PowerShell с правами администратора.
2. Если используется другой порт, при настройке конечной точки HTTPS hello на hello виртуальной Машины, обновите порт hello в hello следующую команду, затем выполните команду hello:
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. После выполнения команды hello **ОК** отображается hello из командной строки.

tooverify, что открыт порт hello, откройте окно Windows PowerShell и выполнения hello следующую команду:

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a>Проверка конфигурации hello
tooverify, теперь работает hello базовых функций сервера отчетов, откройте браузер с правами администратора, и сообщала диспетчера отчетов URL-адреса для сервера ad обзора toohello следующее:

* На hello ВМ откройте URL-адрес сервера отчетов toohello.
  
        http://localhost/reportserver
* На hello ВМ откройте URL-адрес диспетчера отчетов toohello.
  
        http://localhost/Reports
* На локальном компьютере, откройте toohello **удаленного** диспетчера отчетов на hello виртуальной Машины. Обновите DNS-именем hello в hello следующий пример соответствующим образом. При появлении запроса пароля используйте hello учетные данные администратора, созданный во время инициализации hello виртуальной Машины. имя пользователя Hello уже hello [домен]\[имя пользователя] формате, где имя компьютера ВМ hello, например ssrsnativecloud\testuser hello домена. Если вы не используете HTTP**S**, удалите hello **s** в URL-АДРЕСЕ hello. В разделе hello следующего раздела приведены сведения о создании дополнительных пользователей на виртуальной Машине.
  
        https://ssrsnativecloud.cloudapp.net/Reports
* С локального компьютера перейдите на URL-адрес сервера отчетов для удаленного toohello. Обновите DNS-именем hello в hello следующий пример соответствующим образом. Если вы не используете HTTPS, удалите hello s в URL-адрес hello.
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a>Создание пользователей и назначение ролей
После настройке и проверке hello сервером отчетов, общие задачи администрирования является toocreate одного или нескольких пользователей и назначить пользователей tooReporting служб ролей. Дополнительные сведения см. в разделе hello следующее:

* [Создание локальной учетной записи пользователя](https://technet.microsoft.com/library/cc770642.aspx)
* [Предоставление пользователю доступа tooa сервера отчетов (диспетчер отчетов)](https://msdn.microsoft.com/library/ms156034.aspx))
* [Создание назначений ролей и управление ими](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate и публиковать отчеты toohello виртуальной машине Azure
Hello следующей таблице перечислены некоторые hello параметры доступные toopublish существующие отчеты с сервера отчетов toohello компьютера в локальной среде, размещенной на виртуальной машине Microsoft Azure hello:

* **Скрипт RS.exe**: RS.exe используйте скрипт toocopy отчета товары и сервер tooyour существующих отчетов виртуальной машине Microsoft Azure. Дополнительные сведения см. в разделе hello раздел «tooNative собственный режим режиме — виртуальная машина Microsoft Azure» в [tooMigrate сценарий Sample Reporting Services rs.exe содержимого между серверами отчетов](https://msdn.microsoft.com/library/dn531017.aspx).
* **Построитель отчетов**: hello виртуальной машины включает щелкните hello-версии ClickOnce построителя отчетов Microsoft SQL Server. hello построителя отчетов toostart впервые hello виртуальной машины:
  
  1. Запустите браузер с правами администратора.
  2. Обзор диспетчера tooreport на виртуальной машине hello и нажмите кнопку **построитель** на ленте «hello».
     
     Дополнительные сведения см. в статье [Установка, удаление и поддержка построителя отчетов](https://technet.microsoft.com/library/dd207038.aspx).
* **SQL Server Data Tools: ВМ**: Если вы создали hello виртуальной Машины с SQL Server 2012, то SQL Server Data Tools, установленной на виртуальной машине hello и может принимать используется toocreate **проектов сервера отчетов** и отчеты о виртуальных hello компьютер. SQL Server Data Tools можно опубликовать сервер отчетов toohello hello отчетов на виртуальной машине hello.
  
    Если вы создали hello виртуальной Машины с SQL server 2014, можно установить SQL Server Data Tools — BI для visual Studio. Дополнительные сведения см. в разделе hello следующее:
  
  * [Microsoft SQL Server Data Tools — бизнес-аналитика для Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313)
  * [Microsoft SQL Server Data Tools — Business Intelligence для Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843)
  * [SQL Server Data Tools и SQL Server Business Intelligence (SSDT-BI)](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* **SQL Server Data Tools: удаленно**. Создайте на локальном компьютере проект служб Reporting Services в SQL Server Data Tools, содержащий отчеты служб Reporting Services. Настройте URL hello проекта tooconnect toohello веб-службы.
  
    ![свойства проекта SSDT для проекта SSRS](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* **Использовать сценарий**: используйте содержимого сервера отчетов toocopy сценария. Дополнительные сведения см. в разделе [tooMigrate сценарий Sample Reporting Services rs.exe содержимого между серверами отчетов](https://msdn.microsoft.com/library/dn531017.aspx).

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a>Минимизация затрат, если вы не используете hello виртуальной Машины
> [!NOTE]
> плата за toominimize для виртуальных машин Azure не во время работы завершить работу hello виртуальной Машины из классического портала Azure hello. При использовании параметров электропитания Windows hello внутри виртуальной Машины tooshut вниз hello ВМ взимается плата hello же сумму для hello виртуальной Машины. Оплата tooreduce, требуется tooshut вниз hello виртуальной Машины в hello классический портал Azure. Если вы больше не нужна hello виртуальной Машины, запомнить hello toodelete ВМ и hello плата хранение tooavoid связанный VHD файлов. Дополнительные сведения см. раздел hello вопросы и ответы на [сведения о ценах на виртуальные машины](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="more-information"></a>Дополнительные сведения
### <a name="resources"></a>Ресурсы
* Аналогичное содержимое связанных tooa развертывания одного сервера SQL Server Business Intelligence и SharePoint 2013, см. [tooCreate с помощью Windows PowerShell ВМ Azure с SQL Server BI и SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).
* Аналогичные содержимого связанных tooa развертывания с несколькими серверами SQL Server Business Intelligence и SharePoint 2013. в разделе [развертывание SQL Server Business Intelligence в виртуальных машинах Azure](https://msdn.microsoft.com/library/dn321998.aspx).
* Дополнительные сведения см. связанные toodeployments SQL Server Business Intelligence в виртуальных машинах в Azure, [SQL Server Business Intelligence в виртуальных машинах Azure](virtual-machines-windows-classic-ps-sql-bi.md).
* Дополнительные сведения о hello стоимости вычислительных затрат Azure см. в разделе вкладка виртуальных машин hello [калькулятор цен Azure](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).

### <a name="community-content"></a>Материалы сообщества
* Пошаговые инструкции по как toocreate Reporting Services собственный режим сервера отчетов без использования скриптов см. в разделе [размещение службы SQL Reporting на виртуальной машине Azure](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a>Ссылки tooother ресурсы для SQL Server в виртуальных машинах Azure
[Обзор. SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

