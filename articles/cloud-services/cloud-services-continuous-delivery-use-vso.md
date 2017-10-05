---
title: "Непрерывная поставка в Azure с использованием Visual Studio Team Services | Документация Майкрософт"
description: "Узнайте, как настроить командные проекты Visual Studio Team Services для автоматического выполнения сборки и развертывания в веб-приложения в службе приложений Azure и облачные службы."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: d80ce63eb7ddfd7c45726be887a772f9a7594b28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services"></a>Непрерывная доставка в Azure с использованием Visual Studio Team Services
Вы можете настроить командные проекты Visual Studio Team Services для автоматического выполнения сборки и развертывания в облачные службы или веб-приложения Azure.  (Дополнительные сведения о настройке непрерывного процесса сборки и развертывания системы с использованием *локального* решения Team Foundation Server см. в статье [Непрерывная поставка для облачных служб в Azure](cloud-services-dotnet-continuous-delivery.md).)

В данном учебнике предполагается, что у вас установлены решения Visual Studio 2013 и пакет SDK Azure. Чтобы загрузить Visual Studio 2013, щелкните ссылку **Начните работу бесплатно** на сайте [www.visualstudio.com](http://www.visualstudio.com). Пакет SDK Azure можно установить по [этой ссылке](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> Для работы с этим руководством необходима учетная запись Visual Studio Team Services. Вы можете [бесплатно зарегистрировать учетную запись Visual Studio Team Services](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

Чтобы настроить автоматическое выполнение сборки и развертывания облачной службы в Azure с использованием Visual Studio Team Services, выполните следующие действия.

## <a name="1-create-a-team-project"></a>1. Создание командного проекта
Следуйте указаниям, приведенным [здесь](http://go.microsoft.com/fwlink/?LinkId=512980), чтобы создать командный проект и связать его с Visual Studio. В этом руководстве в качестве системы управления версиями применяется Team Foundation Version Control (TFVC). Если для управления версиями вы хотите использовать Git, см. [версию этого руководства для Git](http://go.microsoft.com/fwlink/p/?LinkId=397358).

## <a name="2-check-in-a-project-to-source-control"></a>2. Регистрация проекта в системе управления версиями
1. В Visual Studio откройте решение, которое вы хотите развернуть, или создайте новое.
   В этом пошаговом руководстве представлены инструкции по развертыванию веб-приложения или облачной службы (приложение Azure).
   Чтобы создать новое решение, создайте новый проект облачной службы Azure или новый проект MVC ASP.NET. Убедитесь, что в проекте используется платформа .NET Framework 4 или 4.5 и создается проект облачной службы, добавьте рабочую роль и веб-роль ASP.NET MVC, после чего выберите интернет-приложение для веб-роли. При появлении запроса выберите **Интернет-приложение**.
   Чтобы создать веб-приложение, выберите шаблон проекта "Веб-приложение ASP.NET" и затем выберите MVC. Ознакомьтесь со сведениями в статье [Развертывание веб-приложения ASP.NET в службе приложений Azure с помощью Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).
   
   > [!NOTE]
   > В настоящее время Visual Studio Team Services поддерживают только развертывания непрерывной интеграции веб-приложений Visual Studio. Проекты веб-сайтов выходят за эти рамки.
   > 
   > 
2. Откройте контекстное меню решения и выберите **Добавить решение в систему управления версиями**.
   
    ![][5]
3. Примите предлагаемые по умолчанию параметры или измените их, после чего нажмите кнопку **ОК** . По завершении обработки в **обозревателе решений**появится значок системы управления версиями.
   
    ![][6]
4. Откройте контекстное меню решения и выберите пункт **Регистрация**.
   
    ![][7]
5. В области **Ожидающие изменения** в обозревателе **Team Explorer** введите примечание для регистрации и нажмите кнопку **Регистрация**.
   
    ![][8]
   
    Обратите внимание на варианты для включения или исключения определенных изменений при настройке. Если нужные изменения исключаются, нажмите ссылку **Включить все** .
   
    ![][9]

## <a name="3-connect-the-project-to-azure"></a>3. Подключение проекта к Azure
1. Теперь, когда создан командный проект VS Team Services с определенным исходным кодом, вы можете подключить его к Azure.  Войдите на [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885) и выберите существующую облачную службу или веб-приложение. Вы также можете создать новые объекты, щелкнув в нижнем левом углу значок **+**, а затем выбрав **Облачная служба** или **Веб-приложение** и **Быстрое создание**. Щелкните ссылку **Set up publishing with Visual Studio Team Services** (Настройка публикации в Visual Studio Team Services).
   
    ![][10]
2. В мастере введите имя учетной записи Visual Studio Team Services в соответствующем поле и щелкните ссылку **Авторизовать сейчас** . Может появиться запрос на вход в систему.
   
    ![][11]
3. Во всплывающем диалоговом окне **Connection Request** (Запрос на подключение) нажмите кнопку **Принять**, чтобы предоставить Azure полномочия для настройки командного проекта в Visual Studio Team Services.
   
    ![][12]
4. После успешной авторизации появится раскрывающийся список, в котором будут представлены ваши командные проекты Visual Studio Team Services. Щелкните имя созданного на предыдущих шагах командного проекта и нажмите кнопку с галочкой в мастере.
   
    ![][13]
5. После привязки проекта появятся инструкции по проверке изменений в командном проекте Visual Studio Team Services.  При следующем возврате данных после изменения Visual Studio Team Services выполнит сборку и развертывание вашего проекта в Azure.  Чтобы проверить реализованное поведение, щелкните ссылку **Check In from Visual Studio** (Регистрация из Visual Studio), а затем ссылку **Launch Visual Studio** (Запустить Visual Studio) (или аналогичную кнопку **Visual Studio** в нижней части окна портала).
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4. Запуск процессов повторного построения и развертывания проекта
1. В обозревателе **Visual Studio Team Explorer** щелкните ссылку **Обозреватель управления исходным кодом**.
   
    ![][15]
2. Перейдите к файлу решения и откройте его.
   
    ![][16]
3. Откройте и измените файл в **обозревателе решений**. Например, вы можете изменить файл `_Layout.cshtml` в папке Views\\Shared веб-роли MVC.
   
    ![][17]
4. Измените логотип сайта и сохраните этот файл с помощью клавиш **CTRL + S** .
   
    ![][18]
5. В обозревателе **Team Explorer** щелкните ссылку **Ожидающие изменения**.
   
    ![][19]
6. Введите комментарий и нажмите кнопку **Регистрация** .
   
    ![][20]
7. Нажмите кнопку **Домашняя страница**, чтобы вернуться на домашнюю страницу **Team Explorer**.
   
    ![][21]
8. Щелкните ссылку **Сборки** , чтобы просмотреть выполняющиеся сборки.
   
    ![][22]
   
    **Team Explorer** отображается информация о том, что для вашего возврата запущен процесс сборки.
   
    ![][23]
9. Дважды щелкните имя выполняемой сборки, чтобы просмотреть подробный журнал процесса построения.
   
    ![][24]
10. В процессе построения вы можете просмотреть определение сборки, созданное во время привязки TFS к Azure с помощью мастера.  Откройте контекстное меню определения сборки и выберите **Редактировать определение сборки**.
    
     ![][25]
    
     На вкладке **Триггер** указывается, что в определении сборки настроено выполнение сборки по умолчанию при каждой регистрации.
    
     ![][26]
    
     На вкладке **Процесс** указывается, что в среде разработки настроено имя ваших облачной веб-службы или веб-сайта. При работе с веб-приложениями здесь будут показаны другие свойства.
    
     ![][27]
11. При необходимости измените установленные по умолчанию значения свойств. Свойства публикации Azure находятся в разделе **Развертывание** .
    
     В следующей таблице приводятся доступные свойства в разделе **Развертывание** :
    
    | Свойство | Значение по умолчанию |
    | --- | --- |
    | Разрешить недоверенные сертификаты |Если установлено значение false, то SSL-сертификаты должны быть подписаны корневым центром сертификации. |
    | Разрешить обновление |Разрешает обновление существующего развертывания вместо создания нового. Сохраняет IP-адрес. |
    | Не удалять |Если установлено значение true, не разрешена перезапись существующего несвязанного развертывания (обновление разрешено). |
    | Путь к параметрам развертывания |Путь к PUBXML-файлу для веб-приложения относительно корневой папки репозитория. Для облачных служб игнорируется. |
    | Среда развертывания Sharepoint |Совпадает с именем службы. |
    | Среда развертывания Azure |Имя веб-приложения или облачной службы |
12. Если используется несколько конфигураций служб (CSCFG-файлов), можно указать желаемую конфигурацию службы в параметрах **Сборка, Дополнительно, Аргументы MSBuild** . Например, чтобы использовать файл ServiceConfiguration.Test.cscfg, задайте аргумент командной строки MSBuild `/p:TargetProfile=Test`.
    
     ![][38]
    
     К этому моменту процесс построения должен быть успешно завершен.
    
     ![][28]
13. Если дважды щелкнуть имя сборки, Visual Studio отобразит **сводку сборки**, включающую все результаты тестирования из соответствующих проектов модульного теста.
    
     ![][29]
14. На [классическом портале Azure](http://go.microsoft.com/fwlink/?LinkID=213885)можно увидеть соответствующее развертывание на вкладке **Развертывания** , выбрав промежуточную среду.
    
     ![][30]
15. Перейдите по URL-адресу вашего сайта. Для веб-приложения достаточно нажать кнопку **Обзор** на панели команд. Для облачной службы выберите URL-адрес в разделе **Сводка** на странице **Панель мониторинга**, где отображается промежуточная среда для облачной службы. Развертывания из решений непрерывной интеграции для облачных служб по умолчанию публикуются в промежуточной среде. Чтобы изменить это поведение, присвойте свойству **Альтернативная среда облачной службы** значение **Рабочая среда**. На этом снимке экрана показано местонахождение URL-адреса сайта на странице панели мониторинга облачной службы:
    
    ![][31]
    
    Сайт откроется на новой вкладке браузера.
    
    ![][32]
    
    При внесении других изменений в проект для облачных служб запускаются дополнительные процессы построения, в результате чего создается несколько развертываний, последнее из которых отмечается как активное.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5. Повторное развертывание предыдущей сборки
Этот шаг необязателен и применяется к облачным службам. Чтобы восстановить состояние сайта на момент более ранней версии, выберите на классическом портале Azure какое-либо предыдущее развертывание и нажмите кнопку **Повторное развертывание** .  Обратите внимание, что при этом в TFS будет запущен новый процесс сборки, а в историю развертывания будет добавлена новая запись.

![][34]

## <a name="6-change-the-production-deployment"></a>6. Изменение развертывания в рабочей среде
Этот шаг применяется только к облачным службам и недоступен для веб-приложений. Выполнив все необходимые действия, можно повысить промежуточную среду до рабочей с помощью кнопки **Переключить** классического портала Azure. Вновь развернутая промежуточная среда повышается до уровня рабочей, а ранее установленная рабочая среда становится промежуточной. Рабочая и промежуточная среды могут использовать разные активные развертывания, однако история развертывания последних сборок будет содержать одинаковые записи независимо от выбранной среды.

![][35]

## <a name="7-run-unit-tests"></a>7. Выполнение модульных тестов
Этот шаг применяется только к веб-приложениям, не облачным службам. Чтобы поместить условия качества вашего развертывания, можно выполнять модульные тесты и, если они не могут остановить развертывание.

1. В Visual Studio добавьте проект модульного теста.
   
   ![][39]
2. Добавление ссылки на проект в проект, который требуется проверить.
   
   ![][40]
3. Добавьте модульные тесты. Сначала попробуйте фиктивный тест, который всегда выдает положительный результат.
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. Измените определение сборки, выберите вкладку **Процесс** и разверните узел **Test**.
5. Установите для параметра **Завершить сборку при ошибке теста** значение True. Это означает, что развертывание не будет происходить, если тест не будет пройден положительно.
   
   ![][41]
6. Поставьте новую сборку в очередь.
   
   ![][42]
   
   ![][43]
7. По мере обработки сборки проверяйте ход выполнения.
   
    ![][44]
   
    ![][45]
8. По завершению сборки проверьте результаты теста.
   
    ![][46]
   
    ![][47]
9. Попробуйте создать тест, который выдаст отрицательный результат. Добавьте новый тест путем копирования первой, переименовать его и закомментируйте строку кода, о том, что NotImplementedException является ожидаемое исключение.
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. Примените изменения, чтобы поставить в очередь новую сборку.
    
     ![][48]
11. Просмотрите результаты теста и подробности отрицательного результата.
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о модульном тестировании в Visual Studio Team Services см. в разделе [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474) (Выполнение тестов в процессе сборки). При использовании Git см. статьи с описанием [совместного использования кода в Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) и [непрерывного развертывания в службе приложений Azure](../app-service-web/app-service-continuous-deployment.md).  Дополнительные сведения о Visual Studio Team Services см. [здесь](http://go.microsoft.com/fwlink/?LinkId=253861).

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
