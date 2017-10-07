---
title: "aaaContinuous доставки с Visual Studio Team Services в Azure и Git | Документы Microsoft"
description: "Узнайте, как tooconfigure в Visual Studio Team Services командные проекты toouse Git tooautomatically построение и развертывание компонентов toohello веб-приложения в службе приложений Azure или облачных служб."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a>TooAzure непрерывной доставки с использованием Visual Studio Team Services и Git
Можно использовать Visual Studio Team Services командных проектов toohost репозитория исходного кода и автоматически построения и развертывания tooAzure веб-приложений или облачных служб при принудительной фиксации репозитория toohello.

Вам потребуется Visual Studio 2013 и hello установленный пакет SDK Azure. Если у вас еще нет Visual Studio 2013, загрузите ее, выбрав hello **начните бесплатно** связи [www.visualstudio.com](http://www.visualstudio.com). Здравствуйте, установка пакета Azure SDK с [здесь](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> Требуется учетная запись Visual Studio Team Services toocomplete этого учебника: вы можете [открыть учетную запись Visual Studio Team Services бесплатно](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

tooset копирование tooautomatically облачной службы построения и развертывания tooAzure с помощью Visual Studio Team Services, выполните следующие действия.

## <a name="1-create-a-git-repository"></a>1. Создание репозитория Git
1. Если у вас еще нет учетной записи Visual Studio Team Services, [создайте ее](http://go.microsoft.com/fwlink/?LinkId=397665). При создании командного проекта выберите Git в качестве системы управления версиями. Выполните инструкции hello tooconnect tooyour Visual Studio командного проекта.
2. В **Team Explorer**, выберите hello **клонировать этот репозиторий** ссылку.
   
    ![][3]
3. Укажите расположение hello hello локальную копию, а затем выберите hello **клон** кнопки.

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a>2: Создание проекта и его сохранения toohello репозитория
1. В **Team Explorer**, в hello **решения** выберите hello **New** связать toocreate новый проект в локальном хранилище hello.
   
    ![][4]
2. Можно развернуть веб-приложения или облачной службы (приложение Azure), hello следующие шаги в этом пошаговом руководстве. Создайте новый проект облачной службы Azure или новый проект MVC ASP.NET. Убедитесь, что целевых объектов проекта hello hello .NET Framework 4 или более поздней версии. Если вы создаете проект облачной службы, добавьте рабочую роль и веб-роль MVC ASP.NET.
   Если вы хотите toocreate веб-приложения, выберите hello **веб-приложение ASP.NET** шаблон проекта, а затем выберите **MVC**. Дополнительные сведения см. в статье [Развертывание веб-приложения ASP.NET в службе приложений Azure с помощью Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).
3. Откройте контекстное меню hello hello решения и выберите **зафиксировать**.
   
    ![][7]
4. Если это первый раз, вы уже использовали Git в Visual Studio Team Services hello потребуется tooprovide некоторые сведения tooidentify самостоятельно в Git. В hello **ожидающие изменения** область **Team Explorer**введите свое имя пользователя и адрес электронной почты. Введите комментарий для фиксации hello и выберите hello **фиксации** кнопки.
   
    ![][8]
5. Обратите внимание, tooinclude параметры hello или исключить определенных изменений при возврате. При изменении hello, вы хотите исключаются, выберите **включить все**.
6. Вы уже теперь hello зафиксированные изменения в локальной копии репозитория hello. Затем синхронизировать изменения с сервера hello, выбрав hello **синхронизации** ссылку.

## <a name="3-connect-hello-project-tooazure"></a>3: hello проекта tooAzure подключения
1. Теперь, когда репозитория в Visual Studio Team Services с помощью исходного кода, в нем используется tooconnect готовности вашей tooAzure репозитория git.  В hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885)выберите облачной службы или веб-приложения, или создать новый, выбрав значок в левом нижнем hello и выбрав + hello **облачной службы** или **веб-приложения**и затем **быстрое создание**.
   
    ![][9]
2. Для облачных служб выберите hello **Настройка публикации с использованием Visual Studio Team Services** ссылку. Для веб-приложений выберите hello **настроить развертывание из системы управления версиями** ссылку.
   
    ![][10]
3. В мастер hello, введите в текстовом поле hello hello имя вашей учетной записи Visual Studio Team Services и выберите hello **авторизовать теперь** ссылку. Вас попросят toosign в.
   
    ![][11]
4. В hello **запроса на подключение** всплывающем диалоговом окне выберите **Accept** tooauthorize Azure tooconfigure командного проекта в Visual Studio Team Services.
   
    ![][12]
5. После завершения авторизации появится раскрывающийся список, содержащий ваши командные проекты Visual Studio Team Services.  Выберите имя командного проекта, созданного на предыдущих этапах hello hello и нажмите кнопку флажок приветствия мастера.
   
    ![][13]
   
    Hello принудительной фиксации tooyour репозитория, Visual Studio Team Services при очередном создаст и развернет ваш проект tooAzure.

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4. Запуск процессов повторного построения и развертывания проекта
1. Откройте файл в Visual Studio и измените его. Например, измените файл hello `_Layout.cshtml` в области представления hello\\общая папка в веб-роли MVC.
   
    ![][17]
2. Изменить текст нижнего колонтитула hello hello сайта и сохраните файл hello.
   
    ![][18]
3. В **обозревателе решений**, откройте контекстное меню hello для hello узел решения, проекта или hello файл можно изменить и выберите **зафиксировать**.
4. Введите комментарий и нажмите кнопку **Зафиксировать**.
   
    ![][20]
5. Выберите hello **синхронизации** ссылку.
   
    ![][38]
6. Выберите hello **Push** связать toopush репозиторий toohello фиксации в Visual Studio Team Services. (Можно также использовать hello **синхронизации** кнопку toocopy репозиторий toohello фиксации. Hello различие состоит в том **синхронизации** также переносит hello последние изменения из репозитория hello.)
   
    ![][39]
7. Выберите hello **домашней** toohello tooreturn кнопку **Team Explorer** домашней страницы.
   
    ![][21]
8. Выберите **строит** tooview hello сборки в данный момент.
   
    ![][22]
   
    **Team Explorer** отображается информация о том, что для вашего возврата запущен процесс сборки.
   
    ![][23]
9. tooview подробный журнал hello сборки по мере того, дважды щелкните имя hello hello построения выполняется.
10. Пока сборка hello в процессе выполнения, взгляните на определение сборки hello, который был создан при использовании tooAzure toolink приветствия мастера.  Откройте контекстное меню определения сборки hello hello и выберите **Редактировать определение построения**.
    
    ![][25]
11. В hello **триггер** вкладку, вы увидите, определение сборки hello toobuild на каждом возврате по умолчанию имеет значение. (Для облачной службы, Visual Studio Team Services строит и развертывает toohello hello главную ветвь, автоматически промежуточной среде. Вы по-прежнему иметь toodo ручной шаг сайт динамической toodeploy toohello. Для веб-приложения, у которого нет промежуточной среде она развертывает hello главную ветвь, напрямую toohello работающий узел.
    
    ![][26]
12. В hello **процесс** вкладку, вы увидите установки среды развертывания hello toohello имя облачной службы или веб-приложения.
    
     ![][27]
13. Укажите значения для свойств hello различных значений, чем значения по умолчанию hello. Hello свойства для публикации Azure находятся в hello **развертывания** раздела, а также могут потребоваться tooset параметры MSBuild. Например, в проект облачной службы toospecify конфигурации службы, отличное от «Облака», задайте параметры MSbuild hello слишком`/p:TargetProfile=[YourProfile]` где *[YourProfile]* соответствующий файл конфигурации службы с именем, например ServiceConfiguration. *YourProfile*.cscfg.
    
     Hello следующей таблице показаны доступные свойства hello в hello **развертывания** раздела:
    
    | Свойство | Значение по умолчанию |
    | --- | --- |
    | Разрешить недоверенные сертификаты |Если установлено значение false, то SSL-сертификаты должны быть подписаны корневым центром сертификации. |
    | Разрешить обновление |Позволяет tooupdate развертывания hello существующего развертывания вместо создания нового. Сохраняет hello IP-адрес. |
    | Не удалять |Если установлено значение true, не разрешена перезапись существующего несвязанного развертывания (обновление разрешено). |
    | Путь tooDeployment параметры |Hello путь tooyour pubxml-файл для веб-приложения, относительного toohello корневой папки репозитория hello. Для облачных служб игнорируется. |
    | Среда развертывания Sharepoint |Здравствуйте таким же, как имя службы hello. |
    | Среда развертывания Azure |Hello имя веб-приложения или облачной службы. |
14. К этому моменту процесс построения должен быть успешно завершен.
    
     ![][28]
15. Если дважды щелкнуть имя сборки hello, Visual Studio отображает **сводки построения**, включая результатов теста из связанных проектов модульных тестов.
    
     ![][29]
16. В hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885), вы можете просмотреть связанные hello развертывания на hello **развертываний** вкладке при выборе hello в промежуточной среде.
    
     ![][30]
17. URL-адрес сайта tooyour обзора. Для веб-приложения, просто выберите hello **Обзор** кнопку hello портала. Для облачной службы, выберите URL-адрес hello в hello **быстрый обзор** раздел hello **мониторинга** страницы, отображающей hello промежуточной среде.
    
    Развертывания с непрерывной интеграции для облачных служб — опубликованных toohello промежуточной среды по умолчанию. Это можно изменить, установка hello **альтернативное окружение облачной службы** свойство слишком**рабочей**. Здесь находится URL-адрес сайта hello на странице панели мониторинга hello облачной службы.
    
    ![][31]
    
    На новой вкладке браузера откроется tooreveal выполнение веб-узла.
    
    ![][32]
18. При внесении другие изменения tooyour проекта, то триггер более строит и накапливаются несколько развертываний. Здравствуйте, последняя версия один помечен как активный.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5. Повторное развертывание предыдущей сборки
Этот шаг не является обязательным. В hello классический портал Azure, выберите более ранних развертывания и выберите **повторно развернуть** toorewind вашего сайта tooan ранее возврата. Обратите внимание, что при этом в TFS будет запущен новый процесс сборки, а в историю развертывания будет добавлена новая запись.

![][34]

## <a name="6-change-hello-production-deployment"></a>6: изменение hello рабочего развертывания
Когда будете готовы, вы можете повысить уровень hello промежуточной toohello рабочей среды, выбрав **замены** в hello классический портал Azure. вновь развернуть Hello промежуточной среды tooProduction повышенного уровня, а hello предыдущей рабочей среде, если таковые имеются, становится промежуточной среде. Hello активное развертывание может быть разным для hello производственной и промежуточной сред, но История развертывания hello последних построений hello одинаково независимо от среды.

![][35]

## <a name="7-deploy-from-a-working-branch"></a>7. Развертывание из рабочей ветви
При использовании Git обычно внести изменения в рабочую ветвь и интегрировать в главную ветвь hello достижении состоянии завершения разработки. Во время стадии разработки проекта hello вам требуется toobuild и развернуть ветвь tooAzure hello рабочий.

1. В **Team Explorer**, выберите hello **Главная** кнопку и выберите hello **ветви** кнопки.
   
    ![][40]
2. Выберите hello **новой ветви** ссылку.
   
    ![][41]
3. Введите имя hello hello ветвь, например «работает» и выберите **создать ветвь**. Будет создана новая локальная ветвь.
   
    ![][42]
4. Опубликуйте ветвь hello. Выберите имя ветви hello в **неопубликованных ветвей**и выберите **публикации**.
   
    ![][44]
5. По умолчанию изменяется только триггер главную ветвь toohello непрерывном режиме построения. tooset копирование непрерывном режиме построения для рабочую ветвь, выберите hello **строит** страницы в **Team Explorer**и выберите **Редактировать определение построения**.
6. Откройте hello **параметры источника** вкладки. В разделе **отслеживаемые ветви для непрерывной интеграции и построения**, выберите **tooadd новой строки щелкните здесь**.
   
    ![][47]
7. Укажите hello ветви, которую вы создали, например refs/heads/работа.
   
    ![][48]
8. Внести изменения в коде hello Привет открыть контекстное меню для файла hello изменен, а затем выберите **зафиксировать**.
   
    ![][43]
9. Выберите hello **несинхронизированные фиксации** ссылку и выберите hello **синхронизации** кнопки или hello **Push** hello toocopy ссылку изменяет toohello копию hello рабочую ветвь в Visual Studio Team Services.
   
   ![][45]
10. Перейдите toohello **строит** Просмотр и поиск сборки hello, есть только вызвавшей hello рабочую ветвь.

## <a name="next-steps"></a>Дальнейшие действия
см. Дополнительные советы по использованию Git в Visual Studio Team Services toolearn [разработка и совместного использования кода в Git, с помощью Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) и сведения об использовании репозитория, который не находится под управлением toopublish Visual Studio Team Services tooAzure, в разделе [tooAzure непрерывного развертывания службы приложений](../app-service-web/app-service-continuous-deployment.md). Дополнительные сведения о Visual Studio Team Services см. [здесь](http://go.microsoft.com/fwlink/?LinkId=253861).

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
