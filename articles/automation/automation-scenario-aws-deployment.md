---
title: "aaaAutomating развертывания виртуальной машины в Amazon Web Services | Документы Microsoft"
description: "В этой статье показано, как toouse автоматизации Azure tooautomate создания виртуальной машины Amazon Web Service"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 1d85c01a-d795-4523-8194-84fc15b53838
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/14/2017
ms.author: tiandert; bwren
ms.openlocfilehash: dd1f3af47d8700ced85a3ee5a406dde1c1311990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---provision-an-aws-virtual-machine"></a>Сценарий службы автоматизации Azure: подготовка виртуальной машины AWS
В этой статье мы демонстрируют, как можно использовать службы автоматизации Azure tooprovision виртуальной машины в вашей подписке Amazon Web Service (AWS) и предоставить эту виртуальную Машину определенное имя какие AWS ссылается tooas «теги» hello виртуальной Машины.

## <a name="prerequisites"></a>Предварительные требования
В целях hello данной статьи необходимо toohave учетную запись службы автоматизации Azure и подписку на AWS. Дополнительные сведения о настройке учетной записи службы автоматизации Azure и об указании в ней учетных данных подписки AWS см. в статье [Проверка подлинности модулей Runbook с помощью Amazon Web Services](automation-configure-aws-account.md).  Эта учетная запись должна создать или обновить с помощью учетных данных подписки AWS, прежде чем продолжить, как мы будет ссылаться на эту учетную запись в hello описанные ниже действия.

## <a name="deploy-amazon-web-services-powershell-module"></a>Развертывание модуля PowerShell для Amazon Web Services
Наш runbook подготовки виртуальной Машины будет использовать toodo модуль AWS PowerShell hello свою работу. Выполните следующие шаги tooadd hello модуля tooyour автоматизации учетная запись, настроенная с учетными данными подписки AWS hello.  

1. Откройте браузер и перейдите toohello [коллекции PowerShell](http://www.powershellgallery.com/packages/AWSPowerShell/) и щелкнет hello **кнопку автоматизации развертывания tooAzure**.<br><br> ![Импорт модуля AWS PS](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)
2. Вы попадаете toohello страницы входа Azure и после проверки подлинности будет перенаправленное toohello портала Azure и предоставляет следующие колонке hello.<br><br> ![Колонка "Импорт модуля"](./media/automation-scenario-aws-deployment/deploy-aws-powershell-module-parameters.png)
3. Выберите hello группу ресурсов из hello **группы ресурсов** раскрывающегося списка и в колонке параметров hello, предоставляют hello следующую информацию:
   
   * Из hello **New или существующую учетную запись автоматизации (string)** раскрывающемся списке выберите **существующие**.  
   * В hello **имя учетной записи автоматизации (string)** введите точное имя hello объекта учетной записи автоматизации, включающий hello учетные данные для вашей подписки AWS hello.  Например, если вы создали выделенную учетную запись с именем **AWSAutomation**, это значение является то, что при вводе в поле hello.
   * Здравствуйте, выберите соответствующий регион из hello **расположение учетной записи автоматизации** раскрывающегося списка.
4. После завершения ввода данных требуется hello щелкните **создать**.
   
   > [!NOTE]
   > Во время импорта модуля PowerShell в службе автоматизации Azure, он также извлечения командлеты hello и эти действия не будет отображаться до импорта и извлечение hello командлеты модуля hello полностью завершено. Это может занять несколько минут.  
   > <br>
   > 
   > 
5. Откройте в hello портал Azure, ваша учетная запись автоматизации, указанные в шаге 3.
6. Щелкните hello **активы** плитку и на hello **активы** колонки, выберите hello **модули** плитки.
7. На hello **модули** колонку, вы увидите hello **AWSPowerShell** модуль в списке hello.

## <a name="create-aws-deploy-vm-runbook"></a>Создание модуля Runbook для развертывания виртуальной машины в AWS
Один раз hello, которое был развернут модуль PowerShell AWS, мы теперь можно создать tooautomate runbook, подготовку виртуальной машины в AWS, с помощью сценария PowerShell. Приведенные ниже действия Hello покажем, как tooleverage собственный сценарий PowerShell в службе автоматизации Azure.  

> [!NOTE]
> Дополнительные параметры и сведения, касающиеся этого скрипта, посетите hello [коллекции PowerShell](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript).
> 

1. Загрузите скрипт PowerShell hello New AwsVM с hello коллекции PowerShell откройте сеанс PowerShell и введите следующие hello:<br>
   ```
   Save-Script -Name New-AwsVM -Path <path>
   ```
   <br>
2. Откройте учетную запись автоматизации hello портал Azure и щелкните hello **Runbooks** плитки.  
3. Из hello **Runbooks** колонке выберите **добавить модуль runbook**.
4. На hello **добавить модуль runbook** колонке выберите **быстрое создание** (Создание модуля runbook).
5. На hello **Runbook** колонку свойств, введите имя в поле "имя" hello, для модуля runbook, а hello **тип Runbook** раскрывающемся списке выберите **PowerShell**и нажмите кнопку  **Создание**.<br><br> ![Колонка "Импорт модуля"](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)
6. При появлении колонки редактировать PowerShell Runbook hello, скопируйте и вставьте сценарий PowerShell hello в разработка холст hello runbook.<br><br> ![Сценарий PowerShell для модуля Runbook](./media/automation-scenario-aws-deployment/runbook-powershell-script.png)<br>
   
    > [!NOTE]
    > Имейте в виду следующие hello при работе с hello пример сценария PowerShell:
    > 
    > * Hello runbook содержит несколько значений параметров по умолчанию. Проверьте все значения по умолчанию и при необходимости обновите их.
    > * Если как актива учетных данных с различными именами чем хранимые учетные данные AWS **AWScred**, необходимо будет tooupdate hello скрипт на строке 57 toomatch соответствующим образом.  
    > * При работе с hello команды AWS CLI в PowerShell, особенно в этот пример runbook, необходимо указать область AWS hello. В противном случае не удастся командлеты hello.  Представление раздела AWS [Укажите регион AWS](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html) в hello AWS средства PowerShell документа для получения дополнительных сведений.  
    >

7. tooretrieve список имен изображения из подписки AWS запуска интегрированной среды Сценариев PowerShell и импортируйте модуль PowerShell AWS hello.  Пройдите аутентификацию в AWS, заменив в среде ISE **Get-AutomationPSCredential** на **AWScred = Get-Credential**.  Это предложит ввести учетные данные, и можно задать вашей **кода доступа** для имени пользователя hello и **секретный ключ доступа** hello пароля.  См. ниже пример hello.  

        #Sample tooget hello AWS VM available images
        #Please provide hello path where you have downloaded hello AWS PowerShell module
        Import-Module AWSPowerShell
        $AwsRegion = "us-west-2"
        $AwsCred = Get-Credential
        $AwsAccessKeyId = $AwsCred.UserName
        $AwsSecretKey = $AwsCred.GetNetworkCredential().Password
   
        # Set up hello environment tooaccess AWS
        Set-AwsCredentials -AccessKey $AwsAccessKeyId -SecretKey $AwsSecretKey -StoreAs AWSProfile
        Set-DefaultAWSRegion -Region $AwsRegion
   
        Get-EC2ImageByName -ProfileName AWSProfile

    Hello следующие выходные данные возвращаются в:<br><br>
   ![Получение образов AWS](./media/automation-scenario-aws-deployment/powershell-ise-output.png)<br>  
8. Скопируйте и вставьте hello одно из имен изображения hello в переменной автоматизации, как указано в runbook hello как **$InstanceType**. Поскольку в этом примере мы используем hello свободного AWS многоуровневого подписки, мы будем использовать **t2.micro** для нашего примера модуля runbook.  
9. Сохранить hello runbook, а затем нажмите кнопку **публикации** toopublish hello runbook и затем **Да** при появлении запроса.

### <a name="testing-hello-aws-vm-runbook"></a>Тестирование runbook AWS ВМ hello
Прежде чем мы продолжить тестирование runbook hello, нам нужна tooverify несколько вещей. В частности:  

* Средства для проверки подлинности в AWS будет создана вызываемой **AWScred** или hello скрипт был обновленные tooreference hello имя актива учетных данных.    
* После импорта модуля AWS PowerShell Hello в службе автоматизации Azure  
* Создан новый модуль Runbook, а значения параметров проверены и при необходимости обновлены.  
* **Ведение журнала подробных сообщений** и при необходимости **ведения записей журнала** под приветствия runbook **ведения журнала и трассировки** были заданы слишком**на**.<br><br> ![Ведение журнала и трассировка для модуля Runbook](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)  

1. Мы должны toostart hello runbook, нажмите **запустить** и нажмите кнопку **ОК** при открытии колонке hello запустить Runbook.
2. В колонке запустить Runbook hello, предоставляют **VMname**.  Примите значения по умолчанию hello для hello других параметров, которые вы предварительно настроен в скрипт hello ранее.  Нажмите кнопку **ОК** задание runbook toostart hello.<br><br> ![Запуск модуля Runbook: New-AwsVM](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)
3. Открывается область задание для hello задание runbook, который мы только что создали. Закройте эту область.
4. Можно просматривать ход выполнения задания и представления вывода hello **потоки** , выбрав hello **все журналы** плитки из колонки задания runbook hello.<br><br> ![Раздел "Поток": выходные данные](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)
5. tooconfirm приветствия подготавливается виртуальная машина, войдите hello AWS консоли управления, если вы не вошли в настоящее время.<br><br> ![Консоль AWS: развернутая виртуальная машина](./media/automation-scenario-aws-deployment/aws-instances-status.png)

## <a name="next-steps"></a>Дальнейшие действия
* tooget к работе с графический Runbook в разделе [Мой первый графический runbook](automation-first-runbook-graphical.md)
* tooget к работе с PowerShell модули Runbook рабочего процесса, в разделе [Мой первый runbook рабочего процесса PowerShell](automation-first-runbook-textual.md)
* в разделе tooknow Дополнительные сведения о типах runbook, их преимущества и ограничения, [типов runbook службы автоматизации Azure](automation-runbook-types.md)
* Дополнительные сведения о функции поддержки скриптов PowerShell см. в статье [Announcing Native PowerShell Script Support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/) (Встроенная поддержка скриптов PowerShell в службе автоматизации Azure).

