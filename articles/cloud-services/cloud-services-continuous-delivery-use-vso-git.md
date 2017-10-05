---
title: "Непрерывная поставка в Azure с использованием Visual Studio Team Services и Git | Документация Майкрософт"
description: "Узнайте, как с помощью Git настроить автоматическое создание и развертывание веб-приложений и облачных служб Azure в командных проектах Visual Studio Team Services."
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
ms.openlocfilehash: f4f5f231536bc381d17898ff2c592be821168a65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services-and-git"></a>Непрерывная доставка в Azure с использованием Visual Studio Team Services и Git
С помощью командных проектов Visual Studio Team Services можно размещать репозиторий Git для исходного кода и выполнять автоматическое построение и развертывание в веб-приложениях Azure или в облачных службах при каждой операции фиксации в репозитории.

В данном учебнике требуются установленные Visual Studio 2013 и пакет SDK Azure. Чтобы загрузить Visual Studio 2013, щелкните ссылку **Начните работу бесплатно** на сайте [www.visualstudio.com](http://www.visualstudio.com). Пакет SDK Azure можно установить по [этой ссылке](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> Для работы с этим руководством необходима учетная запись Visual Studio Team Services. Вы можете [бесплатно зарегистрировать учетную запись Visual Studio Team Services](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

Чтобы настроить автоматическое выполнение сборки и развертывания облачной службы в Azure с использованием Visual Studio Team Services, выполните следующие действия.

## <a name="1-create-a-git-repository"></a>1. Создание репозитория Git
1. Если у вас еще нет учетной записи Visual Studio Team Services, [создайте ее](http://go.microsoft.com/fwlink/?LinkId=397665). При создании командного проекта выберите Git в качестве системы управления версиями. Выполните следующие инструкции для подключения Visual Studio к командному проекту.
2. В обозревателе **Team Explorer** выберите ссылку **Клонировать этот репозиторий**.
   
    ![][3]
3. Укажите расположение локальной копии и нажмите кнопку **Клонировать** .

## <a name="2-create-a-project-and-commit-it-to-the-repository"></a>2. Создание проекта и сохранение его в репозитории
1. В **Team Explorer** в разделе **Решения** щелкните ссылку **Создать**, чтобы создать новый проект в локальном репозитории.
   
    ![][4]
2. В этом пошаговом руководстве представлены инструкции по развертыванию веб-приложения или облачной службы (приложение Azure). Создайте новый проект облачной службы Azure или новый проект MVC ASP.NET. Убедитесь в том, что проект предназначен для платформы .NET Framework 4 или более поздней версии. Если вы создаете проект облачной службы, добавьте рабочую роль и веб-роль MVC ASP.NET.
   Если вы хотите создать веб-приложение, выберите шаблон проекта **Веб-приложение ASP.NET**, а затем — **MVC**. Дополнительные сведения см. в статье [Развертывание веб-приложения ASP.NET в службе приложений Azure с помощью Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).
3. Откройте контекстное меню для этого решения и выберите пункт **Зафиксировать**.
   
    ![][7]
4. Если вы впервые используете Git в Visual Studio Team Services, необходимо предоставить некоторые сведения для вашей идентификации в Git. В области **ожидающих изменений** в **Team Explorer** укажите свое имя пользователя и адрес почты. Введите комментарий для фиксации, а затем нажмите кнопку **Зафиксировать** .
   
    ![][8]
5. Обратите внимание на варианты для включения или исключения определенных изменений при настройке. Если нужные изменения исключены, выберите **Включить все**.
6. Теперь изменения зафиксированы в локальной копии репозитория. Далее следует синхронизировать эти изменения с сервером. Для этого выберите ссылку **Синхронизировать**.

## <a name="3-connect-the-project-to-azure"></a>3. Подключение проекта к Azure
1. Теперь, когда имеется репозиторий Git в Visual Studio Team Services, содержащий некоторый исходный код, можно подключить этот репозиторий к Azure.  Войдите на [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885) и выберите существующую облачную службу или веб-приложение. Вы также можете создать новые объекты, щелкнув в нижнем левом углу значок "+", а затем выбрав **Облачная служба** или **Веб-приложение** и **Быстрое создание**.
   
    ![][9]
2. Для облачных служб щелкните ссылку **Настройка публикации в Visual Studio Team Services** . Для веб-приложений нажмите ссылку **Настроить развертывание из системы управления версиями** .
   
    ![][10]
3. В мастере введите имя учетной записи Visual Studio Team Services в соответствующем поле и нажмите ссылку **Авторизовать сейчас** . Может появиться запрос на вход в систему.
   
    ![][11]
4. Во всплывающем диалоговом окне **Connection Request** (Запрос на подключение) нажмите кнопку **Принять**, чтобы предоставить Azure полномочия для настройки командного проекта в Visual Studio Team Services.
   
    ![][12]
5. После завершения авторизации появится раскрывающийся список, содержащий ваши командные проекты Visual Studio Team Services.  Щелкните имя созданного на предыдущих шагах командного проекта и нажмите кнопку с галочкой в мастере.
   
    ![][13]
   
    При следующей фиксации в репозитории Visual Studio Team Services будет выполнять построение и развертывание проекта в Azure.

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4. Запуск процессов повторного построения и развертывания проекта
1. Откройте файл в Visual Studio и измените его. Например, вы можете изменить файл `_Layout.cshtml` в папке Views\\Shared веб-роли MVC.
   
    ![][17]
2. Измените текст нижнего колонтитула для сайта и сохраните файл.
   
    ![][18]
3. В **обозревателе решений** откройте контекстное меню узла решения, узла проекта или файла, который был изменен, и выберите команду **Зафиксировать**.
4. Введите комментарий и нажмите кнопку **Зафиксировать**.
   
    ![][20]
5. Нажмите ссылку **Синхронизация** .
   
    ![][38]
6. Нажмите ссылку **Отправить** , чтобы отправить фиксацию в репозиторий в Visual Studio Team Services. (Можно также использовать кнопку **Синхронизация** , чтобы скопировать фиксации в репозиторий. Разница в том, что **синхронизация** также запрашивает последние изменения в репозитории.)
   
    ![][39]
7. Нажмите кнопку **Домашняя страница**, чтобы вернуться на домашнюю страницу **Team Explorer**.
   
    ![][21]
8. Щелкните **Сборки** , чтобы просмотреть выполняющиеся сборки.
   
    ![][22]
   
    **Team Explorer** отображается информация о том, что для вашего возврата запущен процесс сборки.
   
    ![][23]
9. Дважды щелкните имя выполняемого построения, чтобы просмотреть подробный журнал процесса построения.
10. В процессе построения вы можете просмотреть определение сборки, созданное во время привязки к Azure с помощью мастера.  Откройте контекстное меню определения сборки и выберите команду **Редактировать определение сборки**.
    
    ![][25]
11. На вкладке **Триггер** вы увидите, что в определении сборки по умолчанию задано выполнение сборки при каждом возврате. (Для облачной службы Visual Studio Team Services автоматически выполняет построение и развертывание главной ветви в промежуточной среде. Развертывание на рабочем сайте необходимо будет выполнить вручную. Для веб-приложения, у которого нет промежуточной среды, развертывание главной ветви выполняется непосредственно на работающем сайте.
    
    ![][26]
12. На вкладке **Процесс** вы увидите, что в среде развертывания задано имя вашей облачной веб-службы или веб-сайта.
    
     ![][27]
13. При необходимости измените установленные по умолчанию значения свойств. Свойства публикации в Azure доступны в разделе **Развертывание** ; также может потребоваться установка параметров MSBuild. Например, чтобы указать в проекте облачной службы конфигурацию, отличную от Cloud, установите для параметров MSbuild значение `/p:TargetProfile=[YourProfile]`, где *[YourProfile]* соответствует файлу конфигурации службы с именем типа ServiceConfiguration.*YourProfile*.cscfg.
    
     В следующей таблице приводятся доступные свойства в разделе **Развертывание** :
    
    | Свойство | Значение по умолчанию |
    | --- | --- |
    | Разрешить недоверенные сертификаты |Если установлено значение false, то SSL-сертификаты должны быть подписаны корневым центром сертификации. |
    | Разрешить обновление |Разрешает обновление существующего развертывания вместо создания нового. Сохраняет IP-адрес. |
    | Не удалять |Если установлено значение true, не разрешена перезапись существующего несвязанного развертывания (обновление разрешено). |
    | Путь к параметрам развертывания |Путь к PUBXML-файлу для веб-приложения относительно корневой папки репозитория. Для облачных служб игнорируется. |
    | Среда развертывания Sharepoint |Совпадает с именем службы. |
    | Среда развертывания Azure |Имя веб-приложения или облачной службы. |
14. К этому моменту процесс построения должен быть успешно завершен.
    
     ![][28]
15. Если дважды щелкнуть имя сборки, Visual Studio отобразит **сводку сборки**, включающую все результаты тестирования из соответствующих проектов модульного теста.
    
     ![][29]
16. На [классическом портале Azure](http://go.microsoft.com/fwlink/?LinkID=213885)можно увидеть соответствующее развертывание на вкладке **Развертывания** , выбрав промежуточную среду.
    
     ![][30]
17. Перейдите по URL-адресу вашего сайта. Для веб-приложения достаточно нажать на портале кнопку **Обзор**. Для облачной службы выберите URL-адрес в разделе **Сводка** страницы **Панель мониторинга**, показывающей промежуточную среду.
    
    Развертывания из решений непрерывной интеграции для облачных служб по умолчанию публикуются в промежуточной среде. Чтобы изменить это поведение, присвойте свойству **Альтернативная среда облачной службы** значение **Рабочая среда**. На этом снимке экрана показано, где на панели мониторинга облачной службы находится URL-адрес сайта:
    
    ![][31]
    
    Сайт откроется на новой вкладке браузера.
    
    ![][32]
18. При внесении других изменений в проект запускаются дополнительные процессы построения, в результате чего создается несколько развертываний. Последнее из них отмечается как активное.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5. Повторное развертывание предыдущей сборки
Этот шаг не является обязательным. Чтобы восстановить состояние сайта на момент более раннего возврата, выберите предыдущее развертывание на классическом портале Azure и нажмите кнопку **Повторное развертывание** . Обратите внимание, что при этом в TFS будет запущен новый процесс сборки, а в историю развертывания будет добавлена новая запись.

![][34]

## <a name="6-change-the-production-deployment"></a>6. Изменение развертывания в рабочей среде
Выполнив все необходимые действия, вы можете повысить промежуточную среду до рабочей с помощью кнопки **Переключить** на классическом портале Azure. Вновь развернутая промежуточная среда повышается до уровня рабочей, а ранее установленная рабочая среда становится промежуточной. Рабочая и промежуточная среды могут использовать разные активные развертывания, однако история развертывания последних сборок будет содержать одинаковые записи независимо от выбранной среды.

![][35]

## <a name="7-deploy-from-a-working-branch"></a>7. Развертывание из рабочей ветви
При использовании Git изменения обычно вносятся в рабочей ветви и интегрируются в главную ветвь, когда развертывание достигает завершенного состояния. На этапе развертывания проекта можно выполнить построение и развертывание рабочей ветви в Azure.

1. В обозревателе **Team Explorer** нажмите кнопку **Домашняя страница**, а затем — **Ветви**.
   
    ![][40]
2. Выберите ссылку **Новая ветвь** .
   
    ![][41]
3. Введите имя ветви, например "working", и нажмите кнопку **Создать ветвь**. Будет создана новая локальная ветвь.
   
    ![][42]
4. Опубликуйте эту ветвь. Выберите имя ветви в разделе **Неопубликованные ветви** и нажмите кнопку **Опубликовать**.
   
    ![][44]
5. По умолчанию только изменения главной ветви вызывают непрерывное построение. Чтобы настроить непрерывную сборку для рабочей ветви, перейдите на **страницу сборок** в **Team Explorer** и выберите **Редактировать определение сборки**.
6. Перейдите на вкладку **исходных параметров** . В разделе **Monitored branches for continuous integration and build** (Отслеживаемые ветви для сборок с непрерывной интеграцией и периодических сборок) выберите **Щелкните здесь для добавления строки**.
   
    ![][47]
7. Укажите созданную ветвь, например, refs/heads/working.
   
    ![][48]
8. Внесите изменения в код, откройте контекстное меню измененного файла и выберите команду **Зафиксировать**.
   
    ![][43]
9. Выберите ссылку **Несинхронизированные фиксации** и нажмите кнопку **Синхронизировать** или выберите ссылку **Отправить**, чтобы скопировать изменения в копию рабочей ветви в Visual Studio Team Services.
   
   ![][45]
10. Перейдите в представление **построений** и найдите построение, которое только что было вызвано для рабочей ветви.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные советы по использованию Git в Visual Studio Team Services см. в статье с описанием [совместного использования кода в Git](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017), а сведения об использовании для публикации в Azure репозитория Git, не управляемого с помощью Visual Studio Team Services, — в статье [Непрерывное развертывание в службе приложений Azure](../app-service-web/app-service-continuous-deployment.md). Дополнительные сведения о Visual Studio Team Services см. [здесь](http://go.microsoft.com/fwlink/?LinkId=253861).

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
