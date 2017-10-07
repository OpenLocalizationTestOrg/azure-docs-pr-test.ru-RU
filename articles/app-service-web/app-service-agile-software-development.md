---
title: "aaaAgile разработки программного обеспечения с помощью службы приложений Azure"
description: "Узнайте, как toocreate крупномасштабных сложных приложений с помощью службы приложения Azure способом, который поддерживает гибкой разработки программного обеспечения."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: c0fdb676-36a6-4738-925f-65b4835d187f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: a1c1c78cfff711774943b0235ed762f03f48fc6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="agile-software-development-with-azure-app-service"></a>Гибкая разработка программного обеспечения с помощью службы приложений Azure.
В этом учебнике вы узнаете, как toocreate крупномасштабных сложных приложений с [службе приложений Azure](/azure/app-service/) способом, который поддерживает [гибкой разработки программного обеспечения](https://en.wikipedia.org/wiki/Agile_software_development). Предполагается, что уже известно, как слишком[развертывание сложных приложений предсказуемо в Azure](app-service-deploy-complex-application-predictably.md).

Ограничения в технических процессов часто можно было использовать в успешной реализации гибкие методологии способ hello. Служба приложений Azure с помощью таких функций, как [непрерывной публикации](app-service-continuous-deployment.md), [промежуточных сред](web-sites-staged-publishing.md) (слоты) и [мониторинг](web-sites-monitor.md), при связывании рационально с hello orchestration и Управление развертыванием в [диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md), может быть частью эффективное решение для разработчиков, развертывающие инфраструктуру гибкой разработки программного обеспечения.

Hello следующей таблице приведен краткого списка требований, связанных с гибкой разработки, и о том, как включить служб Azure, каждое из них.

| Требование | Как Azure включает его |
| --- | --- |
| - Сборка после каждой фиксации<br>- Автоматическая и быстрая сборка |При настройке с непрерывным развертыванием служба приложений Azure может работать как динамические сборки с учетом ветви разработки. Каждый раз, чтобы код передается toohello ветвь, он автоматически построения и выполнения динамическую в Azure. |
| - Самопроверка сборок |Загрузить тесты, веб-тесты, т. д., можно развернуть с помощью шаблона Azure Resource Manager hello. |
| - Выполнение тестов в клоне рабочей среды |Шаблоны Azure Resource Manager может быть используется toocreate клонов hello рабочей среде Azure (в том числе параметры приложения, шаблоны строк подключения, масштабирование, т. д.) для тестирования быстро и предсказуемо. |
| - Удобный просмотр результата последней сборки |TooAzure непрерывного развертывания из репозитория означает, что новый код можно проверить в работающем приложении сразу после сохранения изменений. |
| -Фиксации главной ветви toohello каждый день<br>-Автоматическое развертывание |Непрерывная интеграция цикла производственного приложения с главной ветви репозитория автоматически развертывает tooproduction главной ветви toohello каждый commit или слияния. |

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>Выполняемая задача
Типичный рабочий процесс разработки тест этапа производства в порядке toopublish новые изменения toohello посвящено [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) пример приложения, которое состоит из двух [веб-приложений](/services/app-service/web/), вторая клиентский (FE) и Здравствуйте, другое — серверной части веб-API (BE) и [базы данных SQL](/services/sql-database/). Будет работать с hello, следуя архитектура развертывания:

![](./media/app-service-agile-software-development/what-1-architecture.png)

изображение hello tooput на слова:

* архитектура развертывания Hello разделено на три различных сред (или [групп ресурсов](../azure-resource-manager/resource-group-overview.md) в Azure), каждый из которых свой собственный [план служб приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), [масштабирование](web-sites-scale.md) параметров, и база данных SQL. 
* Каждой средой можно управлять отдельно. Они даже могут находиться в разных подписках.
* Промежуточных и производственных реализованы в виде двух слотов hello же приложение служб приложений. Hello главную ветвь настроены для непрерывной интеграции промежуточных слотах hello.
* После проверки ветви toomaster фиксации в промежуточных слотах (с рабочими данными) hello hello проверить промежуточного приложения сбрасывается в производственный слот hello [без простоев](web-sites-staged-publishing.md).

Hello рабочей и промежуточной среды определяется шаблоном hello в [  *&lt;repository_root >*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json).

Здравствуйте, разработки и тестовых сред определяются шаблоном hello в [  *&lt;repository_root >*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json).

Вы также будете использовать стандартные стратегии ветвления hello, с кодом из ветви dev hello копирование ветвь test toohello, а затем (при перемещении вверх в качество, поэтому toospeak) главную ветвь toohello перемещение.

![](./media/app-service-agile-software-development/what-2-branches.png) 

## <a name="what-you-need"></a>Необходимые элементы
* Учетная запись Azure.
* Учетная запись [GitHub](https://github.com/) .
* Оболочка Git (устанавливается вместе с [GitHub для Windows](https://windows.github.com/))-команд позволяет вам toorun оба hello Git и PowerShell в hello же сеанса 
* Последняя версия [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) .
* Базовое представление о hello следующие средства:
  * Развертывание шаблона [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) (см. также [Предсказуемое развертывание сложного приложения в Azure](app-service-deploy-complex-application-predictably.md)).
  * [Git.](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> Требуется учетная запись Azure toocomplete этого учебника:
> 
> * Вы можете [открыть учетную запись Azure бесплатно](https://azure.microsoft.com/pricing/free-trial/) -вы получаете кредиты можно использовать tootry out платных служб Azure и даже после того, они используются hello учетной записи, можно сохранить и использовать освободить служб Azure, таких как веб-приложений.
> * Вы можете [активировать преимущества подписчика Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) — каждый месяц ваша подписка Visual Studio предоставляет вам кредиты, которые можно использовать для оплаты служб Azure.
> 
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

## <a name="set-up-your-production-environment"></a>Настройка рабочей среды
> [!NOTE]
> сценарий Hello, используемые в этом учебнике автоматически настраивает непрерывной публикации из репозитория GitHub. Это требует учетные данные GitHub уже были сохранены в Azure, в противном случае hello в скрипт развертывания завершается неудачно при попытке tooconfigure параметры системы управления версиями для веб-приложения hello. 
> 
> toostore GitHub учетные данные в Azure, создайте веб-приложения в hello [портал Azure](https://portal.azure.com/) и [настройки развертывания GitHub](app-service-continuous-deployment.md). Требуется только toodo этом один раз. 
> 
> 

В типичном сценарии DevOps у вас есть приложение, которое работает в активном состоянии в Azure и требуется toomake tooit изменения в непрерывной публикации. В этом случае когда шаблон, вы toodeploy разработки, тестирования и используемых hello рабочей среде. Он будет настроен в этом разделе.

1. Создание собственных вилки hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) репозитория. Дополнительные сведения о создании разветвления см. в статье [Fork a Repo](https://help.github.com/articles/fork-a-repo/) (Разветвление репозитория). После создания разветвления его можно просматривать в браузере.
   
    ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Откройте сеанс Git Shell. Если у вас нет Git Shell, установите [GitHub для Windows](https://windows.github.com/) .
3. Создайте локальный клон на разветвление, выполнив следующую команду hello:

        git clone https://github.com/<your_fork>/ToDoApp.git 
4. При наличии локального клона перейдите слишком*&lt;repository_root >*\ARMTemplates и deploy.ps1 hello выполнения скрипта следующим образом:
   
        .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git
5. При появлении запроса введите hello необходимое имя пользователя и пароль для доступа к базе данных.
   
   Вы увидите ход выполнения различных ресурсов Azure подготовки hello. После завершения развертывания hello сценарий запускает приложение hello в браузере hello и дают возможность понятное звукового сигнала.
   
    ![](./media/app-service-agile-software-development/production-2-app-in-browser.png)
   
   > [!TIP]
   > Взгляните на  *&lt;repository_root >*\ARMTemplates\Deploy.ps1, toosee Создание ресурсов с уникальными идентификаторами. Можно использовать же подход toocreate клона hello hello же развертывания, не беспокоясь о конфликта имен ресурсов.
   > 
   > 
6. Вернитесь в сеанс Git Shell и выполните следующую команду:
   
        .\swap –Name ToDoApp<unique_string>master
   
    ![](./media/app-service-agile-software-development/production-4-swap.png)
7. После завершения скрипта hello, вернитесь к предыдущему окну адрес внешнего интерфейса toohello toobrowse (http://ToDoApp*&lt;unique_string >*master.azurewebsites.net/) toosee приложения hello, работающего в производственной среде.
8. Войдите в toohello [портал Azure](https://portal.azure.com/) Обратите внимание на то, что создается.
   
   После этого можно будет toosee двух веб-приложений в hello одну группу ресурсов, один из которых hello `Api` суффикса в имени hello. Если взглянуть на представление группы ресурсов hello, также появятся hello базы данных SQL и сервер, hello план служб приложений и hello промежуточных слотов для hello веб-приложений. Просматривать различные ресурсы hello и сравнить их с  *&lt;repository_root >*toosee \ARMTemplates\ProdAndStage.json, как они настроены в шаблоне hello.
   
    ![](./media/app-service-agile-software-development/production-3-resource-group-view.png)

Теперь вы настроили hello рабочей среде. Далее будет начнем новое приложение toohello обновления.

## <a name="create-dev-and-test-branches"></a>Создание ветвей разработки и тестирования
Теперь, когда сложные приложения, работающего в производственной среде в Azure, вы создадите приложение tooyour обновления в соответствии с гибкой методологии. В этом разделе вы создадите hello ветви разработки и тестирования, которые понадобятся toomake hello необходимых обновлений.

1. Сначала создайте тестовую среду hello. В сеансе оболочки Git выполнения hello следующими командами toocreate hello среду для новой ветви с именем **NewUpdate**. 
   
        git checkout -b NewUpdate
        git push origin NewUpdate 
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch NewUpdate
2. При появлении запроса введите hello необходимое имя пользователя и пароль для доступа к базе данных. 
   
   После завершения развертывания hello сценарий запускает приложение hello в браузере hello и дают возможность понятное звукового сигнала. Теперь у вас есть новая ветвь с собственной тестовой средой. Выполните tooreview момент некоторые сведения о данной тестовой среды.
   
   * Вы можете создать ее в любой подписке Azure. Это означает, что hello рабочей среде можно управлять отдельно от тестовой среды.
   * Тестовая среда работает в Azure в режиме реального времени.
   * Тестовой среды — идентичные toohello рабочей среде, за исключением промежуточных слотов hello и hello, параметры масштабирования. Вы знаете, так как они отличаются hello только ProdandStage.json и Dev.json.
   * Вы можете управлять тестовой средой в ее собственном плане службы приложений с другой ценовой категорией (например, **Free**).
   * Удаление этого окружения тестирования очень похож на удаление группы ресурсов hello. Вы найдете сведения toodo это [позже](#delete).
3. Перейдите на toocreate hello ветви dev, выполнив следующие команды:
   
        git checkout -b Dev
        git push origin Dev
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch Dev
4. При появлении запроса введите hello необходимое имя пользователя и пароль для доступа к базе данных. 
   
   Выполните tooreview некоторое время на несколько моментов относительно этой среды разработки. 
   
   * Среды разработки имеет конфигурации идентичные toohello тестовой среде, так как он развертывается с помощью hello того же шаблона.
   * Каждая среда разработки могут создаваться в hello разработчика собственной подписке Azure, оставив hello тестирования среды toobe отдельно управляемые.
   * Среда разработки работает в Azure в режиме реального времени.
   * Удаление hello разработки среды очень похож на удаление группы ресурсов hello. Вы найдете сведения toodo это [позже](#delete).

> [!NOTE]
> При наличии множества разработчиков, работающих на новое обновление hello каждого из них можно легко создавать ветви и среда разработки, выделенный с hello следующие шаги:
> 
> 1. Создать свои собственные вилки hello репозитория в GitHub (см. [разветвление репозитория](https://help.github.com/articles/fork-a-repo/)).
> 2. Клонировать разветвление hello на их локальном компьютере
> 3. Запустите hello же команды toocreate собственные ветви dev и среды.
> 
> 

Когда все будет готово, ваше ветвление GitHub будет содержать три ветви:

![](./media/app-service-agile-software-development/test-1-github-view.png)

И у вас будет шесть веб-приложений (три набора по два) в трех отдельных группах ресурсов:

![](./media/app-service-agile-software-development/test-2-all-webapps.png)

> [!NOTE]
> Hello рабочей среды toouse hello указывает ProdandStage.json **Стандартная** ценовой категории, подходящем для масштабируемости hello производственного приложения.
> 
> 

## <a name="build-and-test-every-commit"></a>Добавление в сборку и тестирование каждой фиксации
Здравствуйте, файлы шаблонов ProdAndStage.json и Dev.json уже укажите параметры элемента управления источника hello, который по умолчанию настраивает непрерывной публикации для веб-приложения hello. Таким образом в каждой ветви GitHub toohello фиксации триггеры tooAzure автоматического развертывания от этой ветви. Давайте посмотрим, как работает ваша система.

1. Убедитесь в том, что вы будете в ветви Dev hello hello локального репозитория. toodo, выполнения hello следующую команду в Git оболочки:
   
        git checkout Dev
2. Внести уровень пользовательского интерфейса приложения toohello изменить, изменив toouse кода hello [начальной загрузки](http://getbootstrap.com/components/) перечислены. Откройте  *&lt;repository_root >*\src\MultiChannelToDo.Web\index.cshtml и внести hello после выделенной изменения:
   
    ![](./media/app-service-agile-software-development/commit-1-changes.png)
   
    > [!NOTE]
    > Если не считать hello предыдущем рисунке: 
    > 
    > * В строке 18 измените `check-list` слишком`list-group`.
    > * В строке 19 измените `class="check-list-item"` слишком`class="list-group-item"`.
    > 
    > 
3. Сохраните изменение hello. Вернитесь в оболочке Git выполните hello, следующие команды:
   
        cd <repository_root>
        git add .
        git commit -m "changed toobootstrap style"
        git push origin Dev
   
   Эти команды git похожи слишком «проверка кода» в другой системе управления версиями, как TFS. При выполнении `git push`, tooAzure принудительной кода, который затем перестроение hello изменение hello tooreflect приложения в среде разработки hello запускает новый фиксации hello.
4. tooverify возникшей этой среды разработки кода tooyour push, переход на страницу приложения среда разработки tooyour web и просмотрите hello **развертывания** части. Необходимо будет toosee последней фиксации сообщений существует.
   
    ![](./media/app-service-agile-software-development/commit-2-deployed.png)
5. После этого щелкните **Обзор** toosee hello новое изменение в работающем приложении hello в Azure.
   
    ![](./media/app-service-agile-software-development/commit-3-webapp-in-browser.png)
   
   Это приложение toohello незначительное изменение. Тем не менее, многие время новые изменения tooa сложных веб-приложения имеют непредусмотренные и нежелательные побочные эффекты. Тест может tooeasily каждой фиксации в динамических сборках позволяет вам toocatch эти проблемы перед их видеть ваши клиенты.

К этому моменту должно быть уверены, что справитесь с реализацией hello, разработчик hello **NewUpdate** проекта, можно создать среду разработки для себя, фиксации каждой сборки и тестирования каждой сборки.

## <a name="merge-code-into-test-environment"></a>Слияние кода в тестовой среде
Когда вы будете готовы toopush ветви tooNewUpdate ветви кода от разработчиков, это hello git стандартная процедура:

1. Все новые tooNewUpdate фиксации слияние ветви Dev hello в GitHub, например фиксации, созданные другими разработчиками. Любые новые фиксации на GitHub инициирует принудительную кода и сборки в среде разработки hello. Можно затем убедитесь, что код в ветви Dev по-прежнему работает с последней бит hello NewUpdate ветви.
2. Объедините все новые изменения из ветви разработки в ветви NewUpdate на GitHub. Это действие запускает принудительной кода и сборки в среде тестирования hello. 

Снова Обратите внимание на то, так как непрерывное развертывание уже настроен с помощью этих ветвей git, вам не стоит tootake любое действие, например запуск интеграции сборок. Необходимо просто методики управления стандартного источника tooperform, с помощью git и Azure выполняет все процессы сборки hello.

Теперь давайте push код слишком**NewUpdate** ветви. В оболочке Git выполните hello, следующие команды:

    git checkout NewUpdate
    git pull origin NewUpdate
    git merge Dev
    git push origin NewUpdate

Это все! 

Последовательно выберите toohello веб-страницы приложения для вашей toosee среды тестирования новых фиксации (слияние в ветвь NewUpdate) теперь помещено toohello тестовой среде. Нажмите кнопку **Обзор** toosee, hello изменение стиля теперь работает в активном состоянии в Azure.

## <a name="deploy-update-tooproduction"></a>Развертывание обновления tooproduction
Опубликуйте код toohello промежуточной и производственной среде должно быть не отличается от том, что вы уже сделали при передаче кода toohello тестовой среде. Это действительно просто. 

В оболочке Git выполните hello, следующие команды:

    git checkout master
    git pull origin master
    git merge NewUpdate
    git push origin master

Следует помнить, что в зависимости от настройки среды промежуточных и производственных hello в ProdandStage.json способом hello, ваш новый код помещается toohello **промежуточных** область памяти и выполняется. Поэтому при переходе URL-адрес промежуточного слота toohello см hello новый код, на нем запущена. toodo, выполнения hello, выполнив командлет оболочки Git.

    Start-Process -FilePath "http://ToDoApp<unique_string>master-Staging.azurewebsites.net"

А теперь, после проверки hello обновление в промежуточных слотах hello hello только нам остается toodo tooswap его в рабочей среде. В оболочке Git, просто запустить hello, следующие команды:

    cd <repository_root>\ARMTemplates
    .\swap.ps1 -Name ToDoApp<unique_string>master

Поздравляем! Уже успешно опубликованы новые обновления tooyour рабочей веб-приложении. Для этого вы просто создали среды разработки и тестирования и выполнили сборку и тестирование каждой фиксации. Эти процессы являются ключевыми элементами для гибкой разработки программного обеспечения.

<a name="delete"></a>

## <a name="delete-dev-and-test-environments"></a>Удаление сред разработки и тестирования
Поскольку специально разработанных вашей разработки и тестовых средах toobe самодостаточным ресурсов групп, это легко toodelete их. hello toodelete из них, созданный в этом учебнике ветви GitHub hello и артефактов, просто выполните следующие команды в оболочке Git hello:

    git branch -d Dev
    git push origin :Dev
    git branch -d NewUpdate
    git push origin :NewUpdate
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>dev-group -Force -Verbose
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>newupdate-group -Force -Verbose

## <a name="summary"></a>Сводка
Гибкой разработки программного обеспечения является необходимы для многих компаний, которые планируют tooadopt Azure в качестве платформы для приложений. В этом учебнике вы изучили, как toocreate и разделение работы точные реплики или рядом с репликами hello рабочей среде с легкостью даже для сложных приложений. Вы также узнали tooleverage toocreate этой возможности разработки обработку, построения и тестирования каждого одна фиксация в Azure. Этот учебник было надеюсь показано, как лучше всего используется службой приложений Azure и Azure Resource Manager toocreate вместе DevOps решение, которое предусматривает методологии tooagile. Теперь можно выполнить построение этого сценария, выполнив дополнительные методы DevOps, такие как [тестирование в производственной среде](app-service-web-test-in-production-get-start.md). Распространенный сценарий тестирования в производственной среде см. в статье [Развертывание в режиме фокус-тестирования (бета-тестирование) в службе приложений Azure](app-service-web-test-in-production-controlled-test-flight.md).

## <a name="more-resources"></a>Дополнительные ресурсы
* [Предсказуемое развертывание сложного приложения в Azure](app-service-deploy-complex-application-predictably.md)
* [Практика гибкой разработки: советы и рекомендации для модернизированного цикла разработки](http://channel9.msdn.com/Events/Ignite/2015/BRK3707)
* [Стратегии расширенного развертывания для веб-приложений Azure с помощью шаблонов диспетчера ресурсов](http://channel9.msdn.com/Events/Build/2015/2-620)
* [Создание шаблонов диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - hello JSON проверяющий элемент управления](http://jsonlint.com/)
* [ARMClient — Настройка публикации toosite GitHub](https://github.com/projectKudu/ARMClient/wiki/Setup-GitHub-publishing-to-Site)
* [Ветвление Git — основные ветвления и слияния](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Блог Дэвида Эббо (David Ebbo)](http://blog.davidebbo.com/)
* [Azure PowerShell](/powershell/azure/overview)
* [Кроссплатформенные программы командной строки Azure.](../cli-install-nodejs.md)
* [Создание и изменение пользователей в Azure AD](https://msdn.microsoft.com/library/azure/hh967632.aspx#BKMK_1)
* [Вики-сайт проекта Kudu](https://github.com/projectkudu/kudu/wiki)

