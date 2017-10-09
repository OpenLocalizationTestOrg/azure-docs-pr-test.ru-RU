---
title: "aaaSet копирование промежуточных сред для веб-приложений в службе приложений Azure | Документы Microsoft"
description: "Узнайте, как toouse промежуточное публикации для веб-приложений в службе приложений Azure."
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a>Настройка промежуточных сред в службе приложений Azure
<a name="Overview"></a>

При развертывании вашего веб-приложения, веб-приложения на мобильных серверной части и приложения API Linux слишком[службы приложений](http://go.microsoft.com/fwlink/?LinkId=529714), можно развернуть tooa отдельный слот развертывания вместо производственный слот по умолчанию hello при работе в hello **стандарт**или **Premium** режиме плана служб приложений. Слоты развертывания фактически являются динамическими приложениями со своими собственными именами узлов. Элементы содержимого и конфигурации приложения можно переключать между двумя слотами развертывания, включая производственный слот hello. Развертывание ваш слот развертывания приложения tooa имеет hello следующие преимущества:

* Можно проверить изменения приложения в промежуточном слоте развертывания, прежде чем переключаться hello производственный слот.
* Сначала развертывание разъем tooa приложения и переключаться на производственный гарантирует активированию перед идет переключение в рабочей среде все экземпляры слота hello. Это позволит вам избежать простоя при развертывании приложения. Hello перенаправление трафика не вызывает затруднений, а запросы не теряются в результате операций переключения. Весь этот рабочий процесс можно автоматизировать, настроив функцию [автоматического переноса](#Auto-Swap) , когда проверка перед переносом не требуется.
* После переключения hello слот с ранее подготовленный приложение теперь имеет предыдущего рабочего приложения hello. Если изменения hello в производственный слот hello не соответствуют ожидаемым вы, можно выполнить приветствия же замены немедленно tooget вашей «последнего проверенного узла» резервное.

Каждый режим плана службы приложений поддерживает разное количество слотов развертывания. поддерживает режим приложения toofind out hello Число слотов см. в разделе [цены на службу приложения](https://azure.microsoft.com/pricing/details/app-service/).

* Если приложение имеет несколько слотов, нельзя изменить режим hello.
* Масштабирование для веб-сайтов, не находящихся в производственной области, недоступно.
* Для непроизводственных областей управление связанными ресурсами недоступно. В hello [портала Azure](http://go.microsoft.com/fwlink/?LinkId=529715) только это потенциальное воздействие на производственный слот можно избежать, временно перемещение hello не производственный слот tooa другого приложения службы плана режима. Примечание, слот нерабочей hello снова должны совместно использовать hello же режим hello производственный слот, прежде чем можно переключить слоты hello двух.

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a>Добавление слота развертывания
приложение Hello должна быть запущена в hello **Стандартная** или **Premium** режим в порядок tooenable вас несколько слотов развертывания.

1. В hello [портала Azure](https://portal.azure.com/), откройте ваше приложение [колонки ресурсов](../azure-resource-manager/resource-group-portal.md#manage-resources).
2. Выберите hello **слоты развертывания** параметр, а затем нажмите кнопку **добавить слот**.
   
    ![Добавить новый слот развернутого приложения][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > Если приложение hello уже не hello **Стандартная** или **Premium** режиме, вы получите сообщение hello поддерживается режимов, позволяющих включить промежуточную публикацию. На этом этапе, что у вас есть параметр tooselect hello **обновление** и перейдите toohello **шкалы** вкладку приложения перед продолжением.
   > 
   > 
3. В hello **Добавление слота** , имя слота hello и, при необходимости выберите ли конфигурация tooclone приложения из другого существующего слота развертывания. Щелкните флажок toocontinue hello.
   
    ![Источник конфигурации][ConfigurationSource1]
   
    Hello Добавление слота, первый раз будет имеется только два варианта: конфигурации клона из области по умолчанию hello в рабочей среде или вообще.
    После создания несколько слотов будут конфигурации может tooclone из слота, кроме одного hello в рабочей среде.
   
    ![Источники конфигураций][MultipleConfigurationSources]
4. В свое приложение с колонкой ресурсов, нажмите кнопку **слоты развертывания**, щелкните слот развертывания tooopen колонки ресурсов, область памяти, с набором метрик и конфигурации так же, как любое другое приложение. Hello имя слота hello отображается вверху hello tooremind hello колонку, вы просматриваете hello слот развертывания.
   
    ![Название области развертывания][StagingTitle]
5. Щелкните URL-адрес приложения hello в колонке слот hello. Обратите внимание hello слот развертывания имеет свое имя сервера, а также является динамическим приложением. слот развертывания toohello toolimit общего доступа, в разделе [приложения службы веб-приложения — слоты развертывания рабочей toonon доступа web блока](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).

В созданном слоте развертывания изначально нет содержимого. Вы можете развернуть слот toohello из другого репозитория ветвь или другую системную репозитория. Можно также изменить конфигурацию слота hello. Используйте hello опубликовать профиль или развертывания учетные данные, связанные с hello слот развертывания для обновлений содержимого.  Например, вы можете [публикации toothis слот с git](app-service-deploy-local-git.md).

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a>Конфигурация слотов развертывания
При клонировании конфигурации из другой слот развертывания hello клонированных доступен для редактирования. Кроме того некоторые элементы конфигурации, последует содержимое hello через swap (не слот конкретных) пока другие элементы конфигурации будут оставаться в hello же слот после переключения (слот конкретных). Hello следующих списках приведены hello конфигурацию, которая будет изменяться при переключить слоты.

**Переносимые параметры**:

* Общие параметры, например версия платформы, 32/64-разрядная версия, веб-сокеты
* Параметры приложения (может быть настроенный toostick tooa слот)
* Строки подключения (может быть настроенный toostick tooa слот)
* Сопоставления обработчиков
* Настройки диагностики и мониторинга
* Содержимое веб-заданий

**Непереносимые параметры**:

* Конечные точки публикации
* Имена пользовательских доменов
* SSL-сертификаты и SSL-привязки
* Параметры масштабирования
* Планировщики веб-заданий

tooconfigure приложения параметр или соединения строки toostick tooa разъем (не перемещаются) hello доступа **параметры приложения** колонку для определенной области памяти, а затем выберите hello **параметр слот** поле для hello элементы конфигурации, которые следует придерживаться слот hello. Обратите внимание, что пометки элемента конфигурации как слот конкретных приводит hello настройке этого элемента в качестве не замены через все слоты развертывания hello, связанные с приложением hello.

![Параметры слота][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a>Переключение слотов развертывания 
Можно менять слоты развертывания в hello **Обзор** или **слоты развертывания** представление части колонки ресурсов приложения.

> [!IMPORTANT]
> Перед подкачки приложение из слота развертывания в рабочей среде, убедитесь, что все определенные параметры не слот настроены так, как toohave его в целевой области подкачки hello.
> 
> 

1. Слоты развертывания tooswap, щелкните hello **замены** на панели команд hello слота развертывания или в командной строке hello приложение hello.
   
    ![Кнопка "Переключить"][SwapButtonBar]

2. Убедитесь в том, hello переключения источника и замены ориентированных указаны правильно. Как правило, hello целевого слота переключения выступает производственный слот hello. Нажмите кнопку **ОК** toocomplete hello операции. По завершении операции hello слоты развертывания hello меняться местами.

    ![Полное переключение](./media/web-sites-staged-publishing/SwapImmediately.png)

    Для hello **переключение с предварительным просмотром** замены типа см. в разделе [переключение с предварительным просмотром (многоэтапный подкачка)](#Multi-Phase).  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a>Переключение с предварительным просмотром (многофазное переключение)

Переключение с предварительным просмотром, называемое также многофазным переключением, упрощает проверку настроек, определяемых слотами, таких как строки подключения.
Для критически важных рабочих нагрузок, требуется toovalidate, приложение hello работает надлежащим образом при применении конфигурации hello производственный слот, и необходимо выполнить подобную проверку *перед* приложение hello сбрасывается в производственной среде. Для этого используется переключение с предварительным просмотром.

> [!NOTE]
> Переключения с предварительным просмотром не поддерживаются в веб-приложениях Linux.

При использовании hello **переключения с предварительным просмотром** параметр (см. [переключение слотов развертывания](#Swap)), службы приложения hello следующие:

- Не влияет на сохраняет hello целевой слот без изменений поэтому существующие рабочей нагрузки на этом слоте (например, производство).
- Применяет элементы конфигурации hello hello слот toohello источника слоте назначения, включая строки подключения для конкретного слот hello и параметров приложения.
- Перезапускает hello рабочих процессов на hello исходный слот с помощью этих элементов конфигурации, упомянутых выше.
- После завершения замены hello: Перемещает hello warmed-up исходный слот в слоте назначения hello. Hello целевого слота, перемещается в исходный слот hello как вручную замены.
- При отмене hello swap: повторно применяет элементы конфигурации hello hello исходный слот toohello источника слот.

Можно просмотреть только приложение hello поведения с помощью конфигурации целевого слота hello. После завершения проверки, выполнения замены hello отдельно. Этот шаг имеет hello дополнительное преимущество hello исходный слот уже активированию с настройкой требуемого hello, что клиенты не будут сталкиваться простоев.  

Образцы для hello командлетов Azure PowerShell для замены многоэтапный включаются в hello командлетов Azure PowerShell для раздела слотов развертывания.

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a>Настройка автоматического переключения
Ускоряет процесс замены автоматически DevOps сценарии, где требуется toocontinuously развернуть приложение с нуля холодный запуск и обеспечит нулевое время простоя для конечных пользователей приложения hello. Когда слот развертывания настроена для автоматического переключения в производственной среде, каждый раз при принудительной гнезда toothat обновление кода, приложение службы автоматически поменяет приложение hello в производственной среде после его уже подготовлен в слоте hello.

> [!IMPORTANT]
> При включении автоматическое переключение для слота убедитесь, что конфигурации слота hello является точно hello конфигурации, предназначенное для hello целевого слота (обычно hello производственный слот).
> 
> 

> [!NOTE]
> Автоматическое переключение не поддерживается в веб-приложениях Linux.

Настроить автоматический перенос для слота очень просто. Выполните следующие действия hello.

1. В списке **слотов развертывания** выберите слот, не являющийся рабочим, и выберите **Параметры приложения** в колонке ресурсов этого слота.  
   
    ![][Autoswap1]
2. Выберите **на** для **автоматическое переключение**выберите нужного целевого слота hello в **замены слота автоматического**и нажмите кнопку **Сохранить** hello панели команд. Убедитесь, что конфигурация для слота hello является точно hello предназначен для целевого слота hello.
   
    Hello **уведомления** вкладка будет мигать зеленым **успех** после завершения операции hello.
   
    ![][Autoswap2]
   
   > [!NOTE]
   > tootest автоматическое переключение для вашего приложения, можно сначала выбрать ячейку в непроизводственной целевой **замены слота автоматического** toobecome знакомы с функцией hello.  
   > 
   > 
3. Выполнение слота развертывания toothat принудительной кода. Через некоторое время происходит автоматического переключения и hello обновления будут отражены в URL-адрес целевого слота.

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a>toorollback производственного приложения после переключения
В случае ошибки в производственной среде после переключения слотов, накат слоты hello задней tootheir до переключения состояния путем замены hello же двух слотов немедленно.

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a>Пользовательский прогрев перед заменой
Некоторые приложения могут потребовать пользовательских действий прогрева перед заменой. Hello `applicationInitialization` элемента конфигурации в файле web.config позволяет вам toospecify пользовательскую инициализацию действий toobe выполнять до поступает запрос. Операция замены Hello будет ожидать toocomplete этот пользовательский прогрева. Ниже приведен пример фрагмента файла web.config.

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a>toodelete слота развертывания
В колонке hello для слота развертывания, слот развертывания Привет открыть колонку, щелкните **Обзор** (страница по умолчанию hello) и нажмите кнопку **удалить** hello панели команд.  

![Удаление слота развертывания][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a>Командлеты Azure PowerShell для слотов развертывания
Azure PowerShell — это модуль, который предоставляет toomanage командлеты Azure через Windows PowerShell, включая поддержку управления слоты развертывания в службе приложений Azure.

* Сведения об установке и настройке Azure PowerShell, а также на проверке подлинности Azure PowerShell с подпиской Azure см. в разделе [как tooinstall и настройка Microsoft Azure PowerShell](/powershell/azure/overview).  

- - -
### <a name="create-a-web-app"></a>Создание веб-приложения
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a>Создание слота развертывания
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a>Инициировать переключение с просмотра (многоэтапный подкачка) и применить слоте toosource конфигурации слота назначения
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a>Отмена промежуточного переключения (переключения с предварительным просмотром) и восстановление конфигурации исходного слота
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a>Переключение слотов развертывания
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a>Удаление слота развертывания
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a>Команды интерфейса командной строки Azure (Azure CLI) для слотов развертывания
Hello Azure CLI предоставляет межплатформенных команд для работы с Azure, включая поддержку для управления слоты развертывания служб приложений.

* Для указания по установке и настройке hello Azure CLI, включая сведения о том, как Azure CLI tooconnect tooyour подписки Azure в разделе [Установка и настройка hello Azure CLI](../cli-install-nodejs.md).
* Вызовите toolist, hello, команд, доступных для службы приложений Azure в hello Azure CLI `azure site -h`.

> [!NOTE] 
> Чтобы ознакомиться с командами [Azure CLI 2.0](https://github.com/Azure/azure-cli) для слотов развертывания, выполните команду [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).

- - -
### <a name="azure-site-list"></a>azure site list
Сведения о приложениях hello в текущей подписке hello вызвать **список сайтов azure**, как показано в следующий пример hello.

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a>azure site create
Вызовите toocreate слота развертывания, **узел azure создать** и укажите имя существующего приложения hello и имя hello toocreate слот hello, как следующий пример hello.

`azure site create webappslotstest --slot staging`

tooenable системы управления версиями для нового слота hello, используйте hello **--git** параметр как следующий пример hello.

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a>azure site swap
toomake hello развертывания слот hello рабочее приложение, используйте hello **swap azure сайта** tooperform команда операции замены, как следующий пример hello. приложение Hello производства будет в любое время простоя, а также будут подвергнуты холодный запуск.

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a>azure site delete
toodelete слот развертывания, которые больше не требуется, используйте hello **удаления сайта azure** команду, как следующий пример hello.

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> Веб-приложение можно увидеть в действии. [Попробуйте службу приложений](https://azure.microsoft.com/try/app-service/) — в ней можно быстро создать кратковременное приложение начального уровня. Для этого не потребуется ни кредитная карта, ни какие-либо обязательства.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
[Azure службы приложений веб-приложения — блокировать слоты развертывания web access toonon рабочей](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[tooApp введение службы в Linux](./app-service-linux-intro.md)
[бесплатной пробной версии Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

