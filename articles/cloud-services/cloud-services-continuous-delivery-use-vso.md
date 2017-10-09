---
title: "aaaContinuous доставки с Visual Studio Team Services в Azure | Документы Microsoft"
description: "Узнайте, как tooconfigure в Visual Studio Team Services командные проекты tooautomatically построение и развертывание компонентов toohello веб-приложения в службе приложений Azure или облачных служб."
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
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a>TooAzure непрерывной поставки с помощью Visual Studio Team Services
Можно настроить сборку tooautomatically командных проектов Visual Studio Team Services и развернуть tooAzure веб-приложений или облачных служб.  (Дополнительные сведения о предоставлении tooset вверх непрерывное построение и развертывание с помощью системы *локальной* Team Foundation Server. в разделе [непрерывная доставка для облачных служб в Azure](cloud-services-dotnet-continuous-delivery.md).)

В учебнике предполагается, что у вас есть Visual Studio 2013 и hello установленный пакет SDK Azure. Если у вас еще нет Visual Studio 2013, загрузите ее, выбрав hello **начните бесплатно** связи [www.visualstudio.com](http://www.visualstudio.com). Здравствуйте, установка пакета Azure SDK с [здесь](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> Требуется учетная запись Visual Studio Team Services toocomplete этого учебника: вы можете [открыть учетную запись Visual Studio Team Services бесплатно](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

tooset копирование tooautomatically облачной службы построения и развертывания tooAzure с помощью Visual Studio Team Services, выполните следующие действия.

## <a name="1-create-a-team-project"></a>1. Создание командного проекта
Следуйте инструкциям hello [здесь](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate вашего командного проекта и связать его tooVisual Studio. В этом руководстве в качестве системы управления версиями применяется Team Foundation Version Control (TFVC). Если требуется toouse Git для управления версиями. в разделе [hello Git версию данного пошагового руководства](http://go.microsoft.com/fwlink/p/?LinkId=397358).

## <a name="2-check-in-a-project-toosource-control"></a>2: проверка в элементе управления toosource проекта
1. В Visual Studio откройте решение hello toodeploy, или создайте новый.
   Можно развернуть веб-приложения или облачной службы (приложение Azure), hello следующие шаги в этом пошаговом руководстве.
   Если вы хотите toocreate новое решение, создайте новый проект облачной службы Azure или новый проект ASP.NET MVC. Проверьте правильность hello нацелен проект .NET Framework 4 или 4.5 и при создании проекта облачной службы, добавьте веб-роль ASP.NET MVC и рабочей роли и выберите веб-приложение hello веб-роли. При появлении запроса выберите **Интернет-приложение**.
   Если вы хотите toocreate веб-приложения, выбрав шаблон проекта веб-приложения ASP.NET hello и выберите MVC. Ознакомьтесь со сведениями в статье [Развертывание веб-приложения ASP.NET в службе приложений Azure с помощью Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).
   
   > [!NOTE]
   > В настоящее время Visual Studio Team Services поддерживают только развертывания непрерывной интеграции веб-приложений Visual Studio. Проекты веб-сайтов выходят за эти рамки.
   > 
   > 
2. Откройте контекстное меню решения hello hello и выберите **tooSource добавить решение управления**.
   
    ![][5]
3. Принять или изменить значения по умолчанию hello и выбрать hello **ОК** кнопки. После завершения процесса hello значки системы управления версиями появляются в **обозревателе решений**.
   
    ![][6]
4. Откройте контекстное меню hello hello решения и выберите **вернуть**.
   
    ![][7]
5. В hello **ожидающие изменения** область **Team Explorer**, введите комментарий для возврата hello и выберите hello **вернуть** кнопки.
   
    ![][8]
   
    Обратите внимание, tooinclude параметры hello или исключить определенных изменений при возврате. При необходимости изменения исключаются выберите hello **включить все** ссылку.
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a>3: hello проекта tooAzure подключения
1. Теперь, когда командного проекта VS Team Services с помощью исходного кода, в нем используется готов tooconnect командного проекта tooAzure.  В hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885)выберите облачной службы или веб-приложения, или создать новый, выбрав hello  **+**  значок в левом нижнем hello и выбрав **облачной службы** или **веб-приложения** и затем **быстрое создание**. Выберите hello **Настройка публикации с использованием Visual Studio Team Services** ссылку.
   
    ![][10]
2. В мастере hello, введите в текстовом поле hello hello имя вашей учетной записи Visual Studio Team Services, а затем нажмите кнопку hello **авторизовать теперь** ссылку. Вас попросят toosign в.
   
    ![][11]
3. В hello **запроса на подключение** всплывающем диалоговом окне выберите hello **Accept** tooauthorize кнопку Azure tooconfigure командного проекта в VS Team Services.
   
    ![][12]
4. После успешной авторизации появится раскрывающийся список, в котором будут представлены ваши командные проекты Visual Studio Team Services. Выберите имя командного проекта, созданного на предыдущих этапах hello hello и нажмите кнопку флажок приветствия мастера.
   
    ![][13]
5. После связывания проекта, вы увидите некоторые инструкции по возврату изменений tooyour Visual Studio Team Services командного проекта.  На следующем возвратом Visual Studio Team Services создаст и развернет ваш проект tooAzure.  Попробуйте сейчас, щелкнув hello **возврата из Visual Studio** связь, а затем hello **запуска Visual Studio** ссылки (или эквивалентное hello **Visual Studio** кнопку внизу hello Hello экрана портала).
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4. Запуск процессов повторного построения и развертывания проекта
1. В Visual Studio **Team Explorer**, выберите hello **обозревателя управления исходным кодом** ссылку.
   
    ![][15]
2. Файл решения tooyour перейдите и откройте его.
   
    ![][16]
3. Откройте и измените файл в **обозревателе решений**. Например, измените файл hello `_Layout.cshtml` в области представления hello\\общая папка в веб-роли MVC.
   
    ![][17]
4. Эмблема hello hello сайта и затем выберите **Ctrl + S** toosave hello файла.
   
    ![][18]
5. В **Team Explorer**, выберите hello **ожидающие изменения** ссылку.
   
    ![][19]
6. Введите комментарий и нажмите кнопку hello **вернуть** кнопки.
   
    ![][20]
7. Выберите hello **домашней** toohello tooreturn кнопку **Team Explorer** домашней страницы.
   
    ![][21]
8. Выберите hello **строит** hello tooview ссылка сборки в данный момент.
   
    ![][22]
   
    **Team Explorer** отображается информация о том, что для вашего возврата запущен процесс сборки.
   
    ![][23]
9. Дважды щелкните имя hello построения hello в ход выполнения tooview подробный журнал hello процессе построения.
   
    ![][24]
10. Пока сборка hello в процессе выполнения, взгляните на определение сборки hello, который был создан при компоновке TFS tooAzure с помощью мастера hello.  Откройте контекстное меню определения сборки hello hello и выберите **Редактировать определение построения**.
    
     ![][25]
    
     В hello **триггер** вкладку, вы увидите, определение сборки hello toobuild на каждом возврате по умолчанию имеет значение.
    
     ![][26]
    
     В hello **процесс** вкладку, вы увидите установки среды развертывания hello toohello имя облачной службы или веб-приложения. При работе с веб-приложения hello свойства, отображаемые будет отличаться от тех, которые здесь показаны.
    
     ![][27]
11. Укажите значения для свойств hello различных значений, чем значения по умолчанию hello. Hello свойства для публикации Azure находятся в hello **развертывания** раздела.
    
     Hello следующей таблице показаны доступные свойства hello в hello **развертывания** раздела:
    
    | Свойство | Значение по умолчанию |
    | --- | --- |
    | Разрешить недоверенные сертификаты |Если установлено значение false, то SSL-сертификаты должны быть подписаны корневым центром сертификации. |
    | Разрешить обновление |Позволяет tooupdate развертывания hello существующего развертывания вместо создания нового. Сохраняет hello IP-адрес. |
    | Не удалять |Если установлено значение true, не разрешена перезапись существующего несвязанного развертывания (обновление разрешено). |
    | Путь tooDeployment параметры |Hello путь tooyour pubxml-файл для веб-приложения, относительного toohello корневой папки репозитория hello. Для облачных служб игнорируется. |
    | Среда развертывания Sharepoint |Здравствуйте таким же, как имя службы hello. |
    | Среда развертывания Azure |Hello имя веб-приложения или облачной службы. |
12. Если вы используете несколько конфигураций службы (cscfg-файлы), можно указать hello соответствующей конфигурации в hello **сборки, Дополнительно, Аргументы MSBuild** параметр. Например, toouse ServiceConfiguration.Test.cscfg, задайте аргументы MSBuild параметр строки `/p:TargetProfile=Test`.
    
     ![][38]
    
     К этому моменту процесс построения должен быть успешно завершен.
    
     ![][28]
13. Если дважды щелкнуть имя сборки hello, Visual Studio отображает **сводки построения**, включая результатов теста из связанных проектов модульных тестов.
    
     ![][29]
14. В hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885), вы можете просмотреть связанные hello развертывания на hello **развертываний** вкладке при выборе hello в промежуточной среде.
    
     ![][30]
15. URL-адрес сайта tooyour обзора. Для веб-приложения, просто щелкните hello **Обзор** кнопки на панели команд hello. Для облачной службы, выберите URL-адрес hello в hello **быстрый обзор** раздел hello **мониторинга** страницы, отображающей hello промежуточной среде для облачной службы. Развертывания с непрерывной интеграции для облачных служб — опубликованных toohello промежуточной среды по умолчанию. Это можно изменить, установка hello **альтернативное окружение облачной службы** свойство слишком**рабочей**. Этом снимке экрана показана там, где hello URL-адрес сайта находится на странице панели мониторинга hello облачной службы.
    
    ![][31]
    
    На новой вкладке браузера откроется tooreveal выполнение веб-узла.
    
    ![][32]
    
    Для облачных служб при внесении других изменений tooyour проекта, то триггер более строит и накапливаются несколько развертываний. Hello последнего помечен как активный.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5. Повторное развертывание предыдущей сборки
Этот шаг применяется toocloud службы и является необязательным. В hello классический портал Azure, выберите более ранних развертывания и выберите hello **повторно развернуть** кнопку toorewind вашего сайта tooan ранее возврата.  Обратите внимание, что при этом в TFS будет запущен новый процесс сборки, а в историю развертывания будет добавлена новая запись.

![][34]

## <a name="6-change-hello-production-deployment"></a>6: изменение hello рабочего развертывания
Этот шаг применяется только toocloud службы, не веб-приложений. Когда будете готовы, вы можете повысить уровень hello промежуточной toohello рабочей среды, выбрав hello **замены** кнопку в hello классический портал Azure. вновь развернуть Hello промежуточной среды tooProduction повышенного уровня, а hello предыдущей рабочей среде, если таковые имеются, становится промежуточной среде. Hello активное развертывание может быть разным для hello производственной и промежуточной сред, но История развертывания hello последних построений hello одинаково независимо от среды.

![][35]

## <a name="7-run-unit-tests"></a>7. Выполнение модульных тестов
Этот шаг применяется только tooweb приложения, не облачных служб. tooput условия качества вашего развертывания, можно выполнять модульные тесты, и если они завершаются с ошибкой, можно остановить развертывание hello.

1. В Visual Studio добавьте проект модульного теста.
   
   ![][39]
2. Добавьте проект toohello ссылки проекта, требуется tootest.
   
   ![][40]
3. Добавьте модульные тесты. tooget запущена, попробуйте пустой тест, который всегда будет передавать.
   
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
4. Измените определение сборки hello, выберите hello **процесс** и разверните hello **тест** узла.
5. Набор hello **сбой сборки при ошибке теста** tooTrue. Это означает, что развертывание hello не появляется, если hello тесты проходят успешно.
   
   ![][41]
6. Поставьте новую сборку в очередь.
   
   ![][42]
   
   ![][43]
7. Во время построения hello продолжить, проверки хода выполнения.
   
    ![][44]
   
    ![][45]
8. После завершения построения hello, проверьте результаты теста hello.
   
    ![][46]
   
    ![][47]
9. Попробуйте создать тест, который выдаст отрицательный результат. Добавьте новый тест, скопировав hello первый, переименовать его и закомментируйте строку hello кода о том, что NotImplementedException является ожидаемое исключение.
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. Возврат изменений tooqueue hello новую сборку.
    
     ![][48]
11. Просмотр hello toosee сведения о результатах теста о сбое hello.
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о модульном тестировании в Visual Studio Team Services см. в разделе [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474) (Выполнение тестов в процессе сборки). Если вы используете Git, см. раздел [совместного использования кода в Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) и [tooAzure непрерывного развертывания службы приложений](../app-service-web/app-service-continuous-deployment.md).  Дополнительные сведения о Visual Studio Team Services см. [здесь](http://go.microsoft.com/fwlink/?LinkId=253861).

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
