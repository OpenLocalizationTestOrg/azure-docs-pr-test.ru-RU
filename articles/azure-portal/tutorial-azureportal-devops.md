---
title: "Учебник: DevOps с hello портал Azure | Документы Microsoft"
description: "Дополнительные сведения hello различных рабочих процессов DevOps в hello портала Azure."
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: 4c32dbbd4e4b1c3809ef4b01e1496e350183ebde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-devops-with-hello-azure-portal"></a>Учебник: DevOps с hello портала Azure
гибкие рабочие процессы DevOps полон Hello платформы Azure. В этом учебнике вы узнаете, как возможности hello tooleverage toodevelop hello портал Azure, тестирования, развертывания, устранение неполадок, мониторинга и управления выполняющихся приложений. Этот учебник посвящен hello следующее:

1. Создание веб-приложения и включение непрерывного развертывания.
2. Разработка и тестирование приложений.
3. Мониторинг и устранение неполадок приложений.
4. Общие задачи управления приложениями.

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a>Создание веб-приложения и включение непрерывного развертывания.
Создать веб-приложение с [службе приложений Azure](https://azure.microsoft.com/services/app-service/), которая будет использоваться в hello конца данного учебника. Кроме того, изначально потребуется включить непрерывное развертывание из репозитория исходного кода в выполняемую среду Azure.

1. Здравствуйте, вход в портал Azure
2. Выберите **службы приложений** &gt; **добавить значок** и введите имя, выберите подписку и создайте новый tooserve группы ресурсов в качестве hello контейнера для службы hello.
   
   Группы ресурсов позволяют toomanage различных аспектов решения hello, например выставление счетов, развертывания и мониторинга все как одну группу через [диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md).
   
   ![рисунок 1][image1]
3. Через некоторое время будет создана служба приложений. Занять несколько минут tooexplore hello различных параметров меню для службы hello hello портала.
   
   ![рисунок 2][image2]    
4. Щелкните URL-адрес hello. Обратите внимание, hello различных доступных вариантов для репозиториев и средства. Можно также использовать hello языки и платформы по своему усмотрению, включая .NET, Java и Ruby.
   
   ![image3][image3]    
5. Hello портал Azure делает непрерывного развертывания, это простой процесс, который включает в себя несколько простых шагов. В hello портал Azure выберите параметры значок hello hello приложения службы, которую вы только что создали.
   
   ![image4][image4]
   
   Из колонки hello открывшемся hello вправо прокрутите toohello публикации раздела.
   
   ![рисунок 5][image5]
6. Настройте некоторые параметры tooenable непрерывное развертывание приложения hello. Щелкните "Источник развертывания", а затем выберите "Выбор источника". Обратите внимание, hello разнообразные параметры, вами источникам репозиториев.
   
   ![рисунок 6][image6]
7. Для этого примера выберите источник GitHub. При необходимости выберите выбранный вами репозиторий hello и настроить учетные данные авторизации hello.
   
   ![рисунок 7][image7]
8. После авторизации tooyour репозитория затем выберите проектов и нужно toodeploy ветви. Ниже приведено несколько примеров.
   
   ![рисунок 8][image8]
9. Закончив, нажмите кнопку "OК". Необходимо запустить уведомления toosee развертывания.
   
   ![image9][image9]
10. Перейдите назад tooGitHub toosee hello webhook, который был создан источник управления toointegrate hello репозитория с Azure. Hello портала Azure обеспечивает интеграцию с GitHub с помощью нескольких простых шагов.
    
    ![image10][image10]
11. toodemonstrate непрерывного развертывания, быстро добавить некоторые toohello содержимого репозитория. Простой пример добавьте пример текстового файла tooa в репозитории GitHub. Вы являетесь свободного toouse .NET, Ruby, Python или другого типа приложения в службе приложений. Чувствовать себя свободного tooadd текстовый файл, ASP.NET MVC, Java и Ruby репозитория toohello приложения по своему усмотрению.
    
    ![image11][image11]
12. После фиксации изменений tooyour репозитория, можно увидеть новый инициировать развертывания в области уведомлений портала hello. Нажмите кнопку синхронизации, если вы не видите быстро изменения после фиксации tooyour репозитория.
    
    ![image12][image12]
13. На этом этапе Если повторите и загрузить страницу приветствия для службы приложения hello, может появиться ошибка 403. В этом примере это потому, что не настраивать документа обычно по умолчанию используется для hello страницы, например файл как index.htm или default.html. Это можно быстро исправить с hello в hello портала Azure для работы с проектами.  В портале Azure hello выберите параметры &gt; параметры приложения.
    
     ![image13][image13]
14. Откроется колонка "Параметры приложения". Введите имя hello hello страницы «SamplePage.html» и нажмите кнопку Сохранить. Занять несколько минут tooexplore hello другие параметры.
    
    ![рисунок 14][image14]
15. При необходимости обновите tooensure URL-адрес вашего браузера, ожидается hello изменения. В этом случае имеется простой текст, теперь заполнение страницы приветствия. Каждого репозитория toohello дополнительных изменений приведет к новой автоматического развертывания.
    
    ![рисунок 15][image15]
    
    Включение непрерывное развертывание с портала Azure hello является простой интерфейс. Кроме того, можно также строить более сложные конвейеры выпуска и использовать другие методы с существующие системы управления версиями и tooAzure toodeploy непрерывной интеграции систем, таких как использование автоматизированной сборки и выпуска системы управления.

## <a name="develop-and-test-an-app"></a>Разработка и тестирование приложений
Затем внести некоторые изменения кода toohello базового и быстрое развертывание этих изменений. Будет также настроить некоторые тестирование производительности для веб-приложения hello.

1. Выберите приложение службы hello области навигации в hello портала Azure и найдите приложение службы.
   
   ![рисунок 16][image16]
2. Щелкните пункт "Инструменты".
   
   ![рисунок 17][image17]
3. Обратите внимание, hello категории в составе средств разработки. Существует несколько полезных инструментов здесь, позволяющие toowork с приложениями, не выходя из hello портала Azure. Затем щелкните пункт "Консоль".
   
   ![рисунок 18][image18]
4. В окне консоли hello можно будет выполнять динамическую команды для вашего приложения. Команда dir типа hello и нажмите клавишу ВВОД. Обратите внимание, что здесь не работают команды, требующие повышенных привилегий.
   
   ![рисунок 19][image19]
5. Категории разработка toohello переход назад и выберите Visual Studio Online. Примечание. Visual Studio Online теперь называется Visual Studio Team Services.
   
   ![рисунок 20][image20]
6. Переключение на hello возможности редактирования в браузере для вашего приложения.
   
   ![рисунок 21][image21]
7. Установите для вашего приложения веб-расширение. Расширения быстро и легко добавлять tooapps функциональность в Azure. Обратите внимание, некоторые hello других типов расширений, доступных в снимке hello.
   
   ![рисунок 22][image22]
8. После установки расширения Visual Studio Online hello нажмите Перейти.
   
   ![рисунок 23][image23]
9. Браузер откроется, где вы видите разработки (IDE) непосредственно в браузере hello вкладка. Обратите внимание hello представленным ниже находится в Chrome.
   
   ![рисунок 24][image24]
10. Можно выполнить несколько действий, таких как редактировать файлы, добавление файлов и папок и загрузки содержимого из hello действующем сайте. Сделайте файл SamplePage.html toohello быстрого редактирования.
    
    ![рисунок 25][image25]
11. Через несколько секунд hello будут автоматически сохранены. Если перейти назад toohello страницы, можно заметить изменения hello. Помните, что такие изменения в реальном времени, скорее всего, не поддерживаются в рабочих средах. Однако средства hello его очень легко toomake быстрого внесения изменений для разработки и тестовую среду.
    
    ![рисунок 26][image26]
    
    ![рисунок 27][image27]
12. Переход назад toohello средства колонки и категории разработка hello щелкните тест производительности.
    
    ![рисунок 28][image28]
13. Необходимо tooset учетной записи team services. Дополнительные сведения о создании учетной записи Team Services. см. [здесь](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).
14. Щелкните новый toocreate теста производительности.
    
    ![рисунок 29][image29]
    
    Настройка hello различные значения и нажмите кнопку Запустить тест внизу hello tooinitiate диалоговой hello теста производительности.
    
    ![рисунок 30][image30]
    
    ![рисунок 31][image31]
15. Как только начнется выполнение теста hello, вы можете отслеживать состояние hello.
    
    ![рисунок 32][image32]
    
    После завершения выполнения теста hello, щелкните hello результат, чтобы отобразить дополнительные сведения см.
    
    ![рисунок 33][image33]
16. В этом примере вы создали небольшой тестового запуска, поэтому существует tooanalyze только данные, но вы можно просматривать различные показатели, а также повторно выполнить тест из этого представления. Hello портала Azure делает создание, выполнение и анализ просто веб-тестов производительности. снимки экрана приветствия ниже отображать данные о производительности hello.
    
    ![рисунок 34][image34]
    
    ![рисунок 35][image35]
    
    ![рисунок 36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a>Мониторинг и устранение неполадок приложений.
В Azure доступно множество средств для мониторинга и устранения неполадок приложений.

1. В hello портала Azure для наших веб-приложения выберите инструментов.
   
   ![рисунок 37][image37]
2. Устранение неполадок категории hello Обратите внимание hello различные способы использования средств tootroubleshoot потенциальных проблем с запущенным приложением. Здесь можно отследить динамический HTTP-трафик, включить самовосстановление, просмотреть журналы и многое другое.
   
   ![рисунок 38][image38]
3. Выберите представление некоторых кодов HTTP-get tooquickly метрики сайта.
   
   ![рисунок 39][image39]
4. Щелкните "Диагностика как услуга". Выберите тип приложения и нажмите кнопку "Запустить".
   
   ![рисунок 40][image40]
   
   Начнется сбор данных.
   
   ![рисунок 41][image41]
5. Вы можете hello соответствующего журнала toodiagnose потенциальные проблемы. Необходимо toosee tooenable ведения журнала, все доступные данные hello параметры, такие как журналы HTTP.
   
   ![рисунок 42][image42]
   
   Щелкнув файл дампа памяти hello можно загрузить и проанализировать DebugDiag toohelp отчета анализа обнаружение возможных проблем.
   
   ![рисунок 43][image43]
6. tooview больше данных требуется более подробное ведение журнала tooenable. В hello портал Azure перейдите toohello веб-приложения и выберите параметры.
   
   ![рисунок 44][image44]
7. Прокрутите вниз категории функций toohello и выберите журналы диагностики.
   
      ![рисунок 45][image45]
8. Обратите внимание: hello различные параметры для ведения журнала. Включите ведение журнала веб-сервера и нажмите кнопку "Сохранить".
   
   ![рисунок 46][image46]
9. Возврат toohello области средств для приложения hello выберите диагностики как услуги и нажмите кнопку выполнения toorerun hello данных коллекции.
   
   ![рисунок 47][image47]
10. Параметр ведения журнала hello HTTP включен, теперь увидеть данные, собранные для журналов HTTP.
    
    ![рисунок 48][image48]
11. Нажимая кнопку hello HTML файл журнала, можно создать полнофункциональный отчет на основе браузера для дальнейшего изучения.
    
    ![рисунок 49][image49]
12. Переместите toohello средства раздела hello портала Azure для приложения hello. Прокрутите раздел средств toohello и выберите команду Process Explorer.
    
    ![рисунок 50][image50]
13. Параметр "Обозреватель процессов" позволяет просматривать сведения о запущенных процессах. Обратите внимание, ниже можно детализировать процессы и даже завершать процессы из hello портала Azure.
    
    ![рисунок 51][image51]
    
    ![рисунок 52][image52]
14. Переход назад колонку параметров toohello hello левой части экрана. Щелкните "Новый запрос в службу поддержки".
    
    ![рисунок 53][image53]
15. Из колонки hello на правом hello заполните сведения о проблемах hello, введите контактные данные и даже Отправка диагностических данных. Hello портал Azure позволяет работать со службой поддержки Майкрософт эффективной работы.
    
    ![рисунок 54][image54]
    
    ![рисунок 55][image55]
    
    Hello портала Azure помогает обеспечить эффективная и привычная монитор toohelp опыт работы с проектами и устранение неполадок нашей выполняющихся приложений. Вы также являются действие tootake может быстро, выполнив действия, такие как перезапуск процессов, включение и отключение различные коллекции данных и даже интеграция с технической поддержки Майкрософт.

## <a name="general-application-management"></a>Общие задачи управления приложениями
Управление приложениями, часто требуется tooperform различные действия, такие как настройка стратегии резервного копирования, реализации и управлении поставщиками удостоверений и настройки управления доступом на основе ролей. Как с hello другие виды взаимодействия с DevOps, hello платформы Azure интегрируется эти задачи непосредственно в портал hello.

1. веб-приложения hello tooensure программы от потери данных необходимы резервные tooconfigure. Перейдите в область параметров toohello для веб-приложения.
   
   ![рисунок 56][image56]
2. В колонке hello на правом hello прокрутите вниз toohello категории функций.
   
    ![рисунок 57][image57]
3. Выберите резервные копии; на правом hello открывается стоечный модуль.
   
   ![рисунок 58][image58]
4. Нажмите кнопку настроить, выберите учетную запись хранения из колонки hello на hello вправо.
   
   ![рисунок 59][image59]
5. Теперь создайте и выберите toohold контейнер хранения резервных копий. Нажмите кнопку Создать hello нижней части колонки hello. Выберите контейнер hello.
   
   ![рисунок 60][image60]
6. После выбора контейнера hello, можно настроить расписания, а также настройки резервного копирования для баз данных. Для этого сценария щелкните hello сохранить значок.
   
    ![рисунок 61][image61]
7. После сохранения прокрутки колонки задней toohello слева hello для резервных копий. Нажмите кнопку Создать резервную копию приложения hello tooback.
   
    ![рисунок 62][image62]
8. Через несколько секунд появится созданная резервная копия. Обратите внимание hello восстановить параметр на снимке экрана ниже hello.
   
    ![рисунок 63][image63]
9. Нажмите кнопку Восстановить и просмотрите колонки toohello параметры hello на правом hello. Можно выбрать соответствующий резервного копирования и легко tooan восстановления ранее состояние при необходимости. Hello портал Azure помогли нам легко включить стратегии приложение hello простой аварийного восстановления.
   
    ![рисунок 64][image64]
10. Возврат колонку параметров toohello hello левой части экрана, а также в разделе функции и выберите проверку подлинности и авторизации.
    
     ![рисунок 65][image65]
11. В колонке hello на hello справа выберите проверку подлинности службы приложения. Обратите внимание, hello разнообразные параметры, которые можно настроить с помощью популярных поставщиков.
    
     ![рисунок 66][image66]
12. Выберите hello поставщика по вашему выбору и обратите внимание hello параметры области hello. Можно указать идентификатор приложения и секрет приложения и быстро включить проверку подлинности Facebook для приложения hello. Hello портала Azure включает проверку подлинности как готовое к использованию решение для приложения.
    
     ![рисунок 67][image67]
13. Переход назад toohello колонку параметров и выберите пользователей, управление ресурсами категории hello.
    
     ![рисунок 68][image68]
14. В колонке hello на правом hello проанализировать hello различные параметры для добавления ролей и пользователей. Hello портал Azure позволяет легко управлять RBAC (Управление доступом на основе ролей) для приложения hello.
    
     ![рисунок 69][image69]

## <a name="summary"></a>Сводка
Этот учебник рассмотренные некоторые hello питания с hello платформы Azure быстро Включение непрерывное развертывание веб-приложения, выполнение различных разработки и тестирования действий, мониторинг и устранение неполадок является динамическим приложением и наконец управлении ключами стратегии аварийного восстановления, удостоверений и управления доступом на основе ролей. Hello платформы Azure обеспечивает единство подхода для этих рабочих процессов DevOps и эффективной работы всегда остается в контекст для поставленной задачи hello.

## <a name="next-steps"></a>Дальнейшие действия
* Диспетчер ресурсов Azure важно для включения DevOps на hello платформы Azure.  более посетите toolearn [Обзор диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md).
* Дополнительные сведения о развертывании службы приложения Azure посетите toolearn [развертывание вашего приложения tooAzure службы приложений](../app-service-web/web-sites-deploy.md)

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
