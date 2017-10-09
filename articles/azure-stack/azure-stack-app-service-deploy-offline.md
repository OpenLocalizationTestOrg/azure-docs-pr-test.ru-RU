---
title: "Развернуть в автономной среде службы приложений: стек Azure | Документы Microsoft"
description: "Подробные инструкции по способ защиты toodeploy службы приложений в отключенной среде Azure стека с помощью AD FS."
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: f7992c310532427b5ffb88555faab2679023c876
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-app-service-resource-provider-tooa-disconnected-azure-stack-environment-secured-by-ad-fs"></a>Добавить среду Azure стека, защищенным AD FS отключен tooa поставщик ресурсов службы приложений

Необходимо добавить [поставщик ресурсов в службе приложений Azure](azure-stack-app-service-overview.md) tooyour развертывания Azure стека:

* Если вы используете Azure стека в изолированной среде защищенным службами федерации Active Directory (AD FS). 
* Если вы хотите toogive web toocreate возможность hello клиентов, мобильных устройств и приложения API — и приложения Azure функции — вместе с подпиской Azure стека. 

toodo таким образом, выполните действия hello в этой статье.

## <a name="download-hello-required-components"></a>Загрузить hello необходимые компоненты

1. Загрузите hello [службы приложений Azure стека предварительной версии установщика](http://aka.ms/appsvconmasrc1installer).

2. Загрузите hello [службы приложений на скрипты поддержки развертывания Azure стека](http://aka.ms/appsvconmasrc1helper).

3. Извлеките файлы hello из hello вспомогательных сценариев ZIP-файл. Hello следующие файлы и структуру папок отображаются:

   - Создание AppServiceCerts.ps1
   - Создание IdentityApp.ps1
   - модули
      - AzureStack.Identity.psm1
      - GraphAPI.psm1

## <a name="create-an-offline-installation-package"></a>Создайте автономный пакет установки

toodeploy службы приложений в изолированной среде, необходимо создать автономный пакет установки с компьютера, который подключается toohello Интернет.

1. Выполните hello службы приложений Azure стека Предварительная версия установщика (AppService.exe) на машине подключенный toohello Интернета.

2. Нажмите кнопку hello **Дополнительно** и нажмите кнопку **создать автономный пакет установки**.

    ![Службы приложений в Azure стека создать автономный пакет установки][1]

3. Hello установщика службы приложений создает автономный пакет установки, отображает путь hello и предоставляет параметр tooopen hello папки.

   ![Службы приложений в Azure стека автономный пакет установки][2]

4. Скопируйте hello службы приложений на установщик предварительной версии Azure стека (AppService.exe) и hello автономной установки пакета toohello стека Azure хост-компьютера.

## <a name="create-certificates-required-by-app-service-on-azure-stack"></a>Создать сертификаты, необходимые для приложения службы стек Azure

Первый сценарий работает с hello Azure стека сертификат центра toocreate три сертификаты, необходимые для приложения службы. Запустить сценарий hello на узле Azure стека hello и убедитесь, что вы используете PowerShell как azurestack\administrator.

1. В сеансе PowerShell, выполняющийся как azurestack\administrator, выполнение hello **AppServiceCerts.ps1 создать** сценарий из расположения hello, которую было извлечено hello вспомогательных сценариев.  Hello скрипт создает три сертификата в hello же папке, что hello создайте скрипт сертификаты, которые требуются службы приложений.

2. Введите пароль toosecure hello PFX-файлов и запишите его. Требуется tooenter в hello службы приложений Azure стека установщика.

### <a name="create-appservicecertsps1-parameters"></a>Параметры создания AppServiceCerts.ps1

| Параметр | Обязательный или необязательный | Значение по умолчанию | Описание |
| --- | --- | --- | --- |
| PfxPassword | Обязательно | Null | Пароль, используемый tooprotect hello закрытого ключа сертификата |
| Имя домена | Обязательно | Local.azurestack.external | Суффикс области и домен для Azure стека |
| CertificateAuthority | Обязательно | AzS CA01.azurestack.local | Конечная точка центра сертификации |

## <a name="complete-hello-offline-installation-of-app-service-on-azure-stack"></a>Выполнить автономную установку службы приложений Azure стеке hello

> [!NOTE]
> Вы *должен* использовать установщик hello tooexecute с повышенными привилегиями учетную запись (локальный администратор или администратор домена). При входе в систему качестве azurestack\azurestackuser вам предложат ввести учетные данные с повышенными привилегиями.

1. Запустите appservice.exe azurestack\administrator.

2. Нажмите кнопку hello **Дополнительно** и нажмите кнопку **выполнения установки в автономном режиме**.

    ![Службы приложений на полный стек Azure автономной установки.][3]

3. Укажите расположение hello hello автономный пакет установки ранее созданного и нажмите кнопку **Далее**.

    ![Службы приложений Azure стека расположением автономный пакет установки][4]

4. Прочитайте и примите условия лицензии предварительный выпуск программного обеспечения Microsoft hello и нажмите **Далее**.

5. Прочтите и примите условия лицензии на сторонние hello и нажмите кнопку **Далее**.

6. Просмотрите hello службы приложений облачных сведения о конфигурации и нажмите кнопку **Далее**.

    ![Службы приложений Azure стека облачной конфигурации][5]

    > [!NOTE]
    > Hello службы приложений Azure стека установщика предоставляет значения по умолчанию hello для установки Azure стека одного узла. Если вы настроили параметры при развертывании Azure стека (например, суффикс домена hello), требуются tooedit hello значения в этом окне соответствующим образом. Например при использовании mycloud.com, формируются суффикс домена hello конечную точку диспетчера ресурсов Azure администратора должна toochange tooadminmanagement. [region]. mycloud.com, формируются.

7. Щелкните hello **Connect** кнопку Далее toohello **подписок Azure стека** поле. Например, введите учетной записью администратора azurestackadmin@azurestack.local. Введите пароль и нажмите кнопку **входа**.

8. Выберите подписку в hello **подписок Azure стека** поле.

9. В hello **стек расположения Azure** поле hello выберите расположение, которое соответствует области toohello вы развертываете. Например, выберите **локальной**. Щелкните **Далее**.

    ![Службы приложений для выбора подписки в стек Azure][6]

10. Введите hello **имя группы ресурсов** для развертывания приложения службы. По умолчанию установлено слишком**APPSERVICE локальной**.

11. Введите hello **имя учетной записи хранения** требуется toocreate службы приложений в процессе установки hello. По умолчанию установлено слишком**appsvclocalstor**.

12. Введите сведения о hello SQL Server для экземпляра hello с используемым toohost hello баз данных поставщика ресурсов приложения службы. Нажмите кнопку **Далее**, и hello установщик проверяет свойства соединения SQL hello.

13. Нажмите кнопку hello **Обзор** кнопку Далее toohello **файла сертификата SSL по умолчанию приложение службы** поле. Go toohello **_.appservice.local.AzureStack.external** сертификат [созданную ранее](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps). Если при создании сертификата hello указано другое расположение и суффикс домена, выберите соответствующий сертификат hello.

14. Введите пароль сертификата hello, заданный при создании сертификата hello.

15. Нажмите кнопку hello **Обзор** кнопку Далее toohello **файла SSL-сертификата поставщика ресурсов** поле. Go toohello **api.appservice.local.AzureStack.external** сертификат [созданную ранее](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps). Если при создании сертификата hello указано другое расположение и суффикс домена, выберите соответствующий сертификат hello.

16. Введите пароль сертификата hello, заданный при создании сертификата hello.

17. Нажмите кнопку hello **Обзор** кнопку Далее toohello **файл корневого сертификата для поставщика ресурсов** поле. Go toohello **AzureStackCertificationAuthority** сертификат [созданную ранее](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps).

18. Щелкните **Далее**. Установщик Hello проверяет hello пароль сертификата.

    ![Службы приложений на сведения о сертификате стек Azure][8]

19. Просмотрите hello конфигурации роли служб приложений. значения по умолчанию Hello заполняются hello минимальный рекомендуемый экземпляр номера SKU для каждой роли. Toohelp спланировать развертывание предоставляется Сводка требований к ядер и памяти. После выбора настроек нажмите кнопку **Далее**.

    - **Контроллер**: по умолчанию выбирается один экземпляр Standard A1. Это минимальный hello, мы рекомендуем. роль контроллера Hello отвечает за управление и обслуживание hello работоспособности hello облачной службы приложений.
    - **Управление**: по умолчанию выбирается один экземпляр Standard A2. При сбое tooprovide, мы рекомендуем два экземпляра. Hello роль управления отвечает за hello диспетчера ресурсов Azure для приложения службы и конечные точки API, портала расширения (администратора, клиент, функции портала) и службы данных hello.
    - **Издатель**: по умолчанию выбирается один экземпляр Standard A1. Это минимальный hello, мы рекомендуем. роль издателя Hello отвечает за публикации содержимого через FTP и веб-развертывания.
    - **Интерфейсный**: по умолчанию выбирается один экземпляр Standard A1. Это минимальный hello, мы рекомендуем. роль внешнего интерфейса Hello отвечает за маршрутизации запросов tooApp службы приложений.
    - **Общий рабочий процесс**: по умолчанию выбирается один экземпляр Standard A1, но может потребоваться несколько tooadd. Как администратор можно определить предложение и выбрать любой уровень номера SKU. уровни Hello должен иметь как минимум одно ядро. Hello роли общего рабочего процесса отвечает за размещение web, мобильных устройств, или API приложения и приложения Azure функции.

    ![Службы приложений Azure стека конфигурации роли][9]

    > [!NOTE]
    > В технических предварительных версиях hello hello установщик поставщика ресурсов службы приложений развертывает экземпляр Standard A1 toooperate как toosupport приветствия простой файл сервера диспетчера ресурсов Azure. Это продолжается для одного узла точки контакта. Для рабочих нагрузок в общедоступной hello службы приложений установщик позволяет использовать hello высокого уровня доступности файлового сервера.

20. Выберите развертывание **Windows Server 2016** образа виртуальной Машины из доступных в поставщике ресурсов вычислений hello для hello облачной службы приложений. Щелкните **Далее**. 

    ![Службы приложений на выбор образа виртуальной Машины стек Azure][10]

21. Введите имя пользователя и пароль для hello рабочих ролей, настроенные в hello облачной службы приложений. Введите имя пользователя и пароль для всех других ролей служб приложений. Щелкните **Далее**.

    ![Службы приложений для входа в учетную запись Azure стека][11]

22. Проверьте hello настроек, заданных на сводку hello. изменения toomake вернитесь через экраны hello и изменить выбранные параметры. Если конфигурация hello способ, установите флажок hello. Развертывание toostart hello, нажмите кнопку **Далее**. 

    ![Службы приложений на сводки по выбору стек Azure][12]

23. Отслеживание хода выполнения установки hello. Службы приложений Azure стеке занимает около 45 минут toodeploy too60, на основе выбранных по умолчанию hello.

    ![Службы приложений на ход выполнения установки стек Azure][13]

24. После успешного завершения работы установщика hello, нажмите кнопку **выхода**.

## <a name="configure-an-ad-fs-service-principal-for-virtual-machine-scale-set-integration-on-worker-tiers-and-sso-for-hello-azure-functions-portal-and-advanced-developer-tools"></a>Настройте участника-службы AD FS для интеграции набора масштабирования виртуальной машины на рабочие уровни и единый вход для средств разработчика портала и расширенных функций Azure hello

>[!NOTE]
> Эти шаги применимы tooAD прощелкать FS только в средах Azure стека.

Администраторы должны tooconfigure единого входа для:

* Настройте участника-службы для интеграции набора масштабирования виртуальной машины на рабочих уровнях.
* Включите дополнительные средства для разработчиков в рамках службы приложений (Kudu) hello.
* Включите использование hello взаимодействие с порталом Azure функции hello. 

Выполните следующие действия.

1. Откройте экземпляр PowerShell от azurestack\azurestackadmin.

2. Перейдите в расположение toohello скриптов hello загрузили и извлекли в hello [подготовительного шага](#Download-Required-Components).

3. [Установка](azure-stack-powershell-install.md) и [настройке среды Azure PowerShell стека](azure-stack-powershell-configure-admin.md).

4. В hello сеанс PowerShell, запустите hello **CreateIdentityApp.ps1** сценария. При запросе для идентификатора клиента Azure Active Directory (Azure AD) введите **ADFS**.

5. В hello **учетные данные** окно, введите учетную запись администратора службы AD FS и пароль. Нажмите кнопку **ОК**.

6. Введите hello путь и сертификата пароль для файла сертификата для hello [сертификат, созданный ранее](# Create certificates toobe used by App Service on Azure Stack). Hello сертификат, созданный по умолчанию для этого шага является sso.appservice.local.azurestack.external.pfx.

7. Hello скрипт создает новое приложение в клиенте hello Azure AD и создает новый скрипт PowerShell.

8. Скопируйте файл сертификата приложения удостоверение hello и hello созданный скрипт toohello **CN0 ВМ** с помощью сеансов удаленного рабочего стола.

9. Возвращает слишком**CN0 ВМ**.

10. Откройте окно администратора PowerShell и обзор каталога toohello, куда были скопированы файл скрипта hello и сертификат на шаге 7.

11. Запустите файл скрипта hello. Этот файл сценария вводит свойства hello в hello службы приложений Azure стека конфигурации и инициирует операцию восстановления всех переднего плана и управления ролями.

| Параметр | Обязательный или необязательный | Значение по умолчанию | Описание |
| --- | --- | --- | --- |
| DirectoryTenantName | Обязательно | Null | Используйте **ADFS** для среды hello AD FS |
| ManagerEndpoint TenantAzure ресурсов | Обязательно | Management.local.azurestack.external | Hello клиента конечную точку диспетчера ресурсов Azure |
| AzureStackCredential | Обязательно | Null | Здравствуйте, учетную запись администратора службы AD FS |
| Параметр | Обязательно | Null | Путь toohello удостоверение приложения сертификат созданные более ранних версий |
| CertificatePassword | Обязательно | Null | Пароль, используемый tooprotect hello закрытого ключа сертификата |
| Имя домена | Обязательно | Local.azurestack.external | Суффикс области и домен для Azure стека |
| AdfsMachineName | Необязательно | Имя машины AD FS, например, AzS ADFS01.azurestack.local |


## <a name="validate-hello-app-service-on-azure-stack-installation"></a>Проверка hello службы приложений при установке стек Azure

1. Откройте в портал администрирования hello Azure стека, toohello группы ресурсов, созданные с помощью установщика hello. По умолчанию эта группа является **APPSERVICE локальной**.

2. Найдите hello **CN0 ВМ**. tooconnect toohello виртуальной Машины, нажмите кнопку **Connect** на hello **виртуальной машины** колонку.

3. На рабочем столе hello этой виртуальной машины, дважды щелкните **управления облака веб-консоли**.

4. Go слишком**серверы, управляемые**.

5. При всех hello отображения машины **готов** для одного или нескольких сотрудников, продолжить toostep 6.

6. Закройте окно hello удаленного рабочего стола компьютера и возврата toohello машины которых выполнены hello установщик приложения службы.

    > [!NOTE]
    > Toowait не требуется один или несколько рабочих процессов toodisplay **готовности** toocomplete hello установку службы приложений Azure стек. Тем не менее требуется по крайней мере один рабочий процесс, готовы toodeploy web, мобильных устройств, или приложения API Azure функции.
    
    ![Службы приложений на состояние серверов управляемый стек Azure][14]

## <a name="test-drive-app-service-on-azure-stack"></a>Проверка службы приложений Azure стеке

После развертывания и регистрации поставщика ресурсов службы приложения hello, проверьте его toomake убедиться, что клиенты можно развернуть web, мобильных устройств и приложения API.

> [!NOTE]
> Необходимо toocreate предложение пространством имен Microsoft.Web hello в соответствии с планом hello. Затем необходимо toohave подписки клиента, который подписан toothis предложения. Дополнительные сведения см. в разделе [создать предложение](azure-stack-create-offer.md) и [создать план](azure-stack-create-plan.md).
>

Вы *должен* использования службы приложений Azure стеке приложениях toocreate подписки клиента. Hello только возможности, которые администратор службы может завершиться до hello портал администрирования, связанных toohello администрирования поставщика ресурсов приложения службы. Эти возможности включают добавления емкости, Настройка развертывания источников и добавление SKU и рабочие уровни.

Начиная с hello третьей версии technical preview, toocreate web, мобильных устройств и приложения API необходимо использовать портал клиента hello и иметь подписку клиента.  

1. На портале клиента hello Azure стека щелкните **New** > **Интернет + мобильные устройства** > **веб-приложения**.

2. На hello **веб-приложения** колонки, введите имя в hello **веб-приложение** поле.

3. В разделе **группы ресурсов**, нажмите кнопку **New**. Затем введите имя в hello **группы ресурсов** поле.

4. Щелкните **Расположение или план службы приложений** > **Создать**.

5. На hello **план служб приложений** колонки, введите имя в hello **план служб приложений** поле.

6. Нажмите кнопку **Ценовая категория** > **Free Shared** или **Shared Shared** > **выберите**  >   **ОК** > **создания**.

7. В менее чем за минуту плитки для нового веб-приложения hello появляется на панели мониторинга hello. Щелкните плитку hello.

8. На hello **веб-приложения** колонка, щелкните **Обзор** веб-сайт по умолчанию hello tooview для этого приложения.

## <a name="deploy-a-wordpress-dnn-or-django-website-optional"></a>Развертывание WordPress, DNN или Django веб-сайта (необязательно)

1. На портале клиента hello Azure стека щелкните  **+** . Go toohello Azure Marketplace, развертывание веб-сайт Django и дождитесь ее успешного завершения. Hello Django веб-платформы использует базу данных на основе системы файла. Он не требует все поставщики дополнительных ресурсов, например SQL или MySQL.

2. При развертывании поставщик ресурсов MySQL, можно развернуть веб-сайт WordPress hello Marketplace. Когда появится запрос для параметров базы данных, введите имя пользователя hello как  *User1@Server1* с именем пользователя hello и имя сервера по своему усмотрению.

3. При развертывании поставщика ресурсов SQL Server, можно развернуть веб-сайт DNN hello Marketplace. Когда появится запрос для параметров базы данных, Выбор базы данных в hello компьютера под управлением SQL Server, подключенного tooyour поставщика ресурсов.

## <a name="next-steps"></a>Дальнейшие действия

Можно также проверить другие [платформы как услуги (PaaS)](azure-stack-tools-paas-services.md).

- [Поставщик ресурсов SQL Server](azure-stack-sql-resource-provider-deploy.md)
- [Поставщик ресурсов MySQL](azure-stack-mysql-resource-provider-deploy.md)

<!--Image references-->
[1]: ./media/azure-stack-app-service-deploy-offline/app-service-offline-step1.png
[2]: ./media/azure-stack-app-service-deploy-offline/app-service-offline-step2.png
[3]: ./media/azure-stack-app-service-deploy-offline/app-service-offline-step3.png
[4]: ./media/azure-stack-app-service-deploy-offline/app-service-offline-step4.png
[5]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-cloud-configuration.png
[6]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-subscription-location-populated.png
[7]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-resource-group-SQL.png
[8]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-certificates.png
[9]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-role-configuration.png
[10]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-vm-image-selection.png
[11]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-role-credentials.png
[12]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-selection-summary.png
[13]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-installation-progress.png
[14]: ./media/azure-stack-app-service-deploy-offline/managed-servers.png


<!--Links-->
[Azure_Stack_App_Service_preview_installer]: http://go.microsoft.com/fwlink/?LinkID=717531
[App_Service_Deployment]: http://go.microsoft.com/fwlink/?LinkId=723982
[AppServiceHelperScripts]: http://go.microsoft.com/fwlink/?LinkId=733525
