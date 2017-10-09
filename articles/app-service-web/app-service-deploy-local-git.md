---
title: "Развертывание Git aaaLocal tooAzure службы приложений"
description: "Узнайте, как развертывание tooAzure tooenable локальный Git службы приложений."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a>Локальные развертывания Git tooAzure службы приложений
В этом учебнике показано как toodeploy приложения слишком[службе приложений Azure] из репозитория Git на локальном компьютере. Службы приложений поддерживает такой подход с hello **Local Git** вариант развертывания в hello [портала Azure].  
Многие из описанных в этой статье команды Git hello выполняются автоматически при создании приложения службы приложений с помощью hello [интерфейса командной строки Azure] как описано [здесь](app-service-web-get-started.md).

## <a name="prerequisites"></a>Предварительные требования
toocomplete этого учебника, необходимо:

* Git. Вы можете загрузить двоичный установки hello [здесь](http://www.git-scm.com/downloads).  
* Базовые знания о Git.
* Учетная запись Microsoft Azure. Если у вас нет учетной записи, [подпишитесь на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial) или [активируйте преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать приложение кратковременных начальный в службе приложений. Никаких кредитных карт и обязательств.  
> 
> 

## <a name="Step1"></a>Шаг 1. Создание локального репозитория
Выполните следующие задачи toocreate новый репозиторий Git hello.

1. Запустите программу командной строки, например **GitBash** (Windows) или **Bash** (оболочка Unix). В системах OS X можно обращаться из командной строки hello hello **терминалов** приложения.
2. Перейдите в каталог toohello, где будет располагаться содержимого toodeploy hello.
3. Используйте hello, следующая команда tooinitialize новый репозиторий Git.

```bash  
git init
```

## <a name="Step2"></a>Шаг 2. Фиксация содержимого
Служба приложений поддерживает приложения, созданные с использованием различных языков программирования. 

1. Если репозиторий уже включает содержимое пропустить эту точку при перемещении toopoint 2 ниже. Если репозиторий пуст, заполните его статическим HTML-файлом, как показано ниже. 
   
   * В текстовом редакторе создайте новый файл с именем **index.html** hello корню репозитория Git hello
   * Добавить после текста, как содержимое hello для hello index.html файл и сохраните его hello: *Hello Git!*
2. Из командной строки hello убедитесь, что в корне hello репозиторий Git. Затем используйте hello, следующая команда tooadd файлы tooyour репозитория:

```bash  
git add -A
```
3. Далее, фиксации hello изменения toohello репозитория с помощью hello следующую команду:

```bash  
git commit -m "Hello Azure App Service"
```  

## <a name="Step3"></a>Шаг 3: Включение hello репозитория приложения служб приложений
Выполните следующие шаги tooenable репозитория для приложения службы приложений hello.

1. Войдите в toohello [портала Azure].
2. В колонке приложения службы приложений выберите **Параметры > Источник развертывания**. Щелкните **Выбрать источник**, затем выберите **Локальный репозиторий Git** и нажмите кнопку **OK**.  
   
    ![Локальный репозиторий Git](./media/app-service-deploy-local-git/local_git_selection.png)
3. Если это ваш первый подготовку в репозитории в Azure, для него необходимо toocreate учетные данные для входа. Используется их toolog в hello Azure репозитория и изменения из локального репозитория Git. В колонке приложения щелкните **Параметры > Учетные данные развертывания**, а затем настройте имя пользователя и пароль развертывания. Закончив, нажмите кнопку **Сохранить**.
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <a name="Step4"></a>Шаг 4. Развертывание проекта
Используйте следующие шаги toopublish hello tooApp вашего приложения службы с помощью Local Git.

1. В колонке приложения в hello портала Azure щелкните **параметры > свойства** для hello **URL-адрес Git**.
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    **URL-адрес Git** является toofrom toodeploy hello удаленную ссылку на ваш локальный репозиторий. Вы будете использовать этот URL-адрес в hello следующие шаги.
2. С помощью командной строки hello, убедитесь, что находятся в корне hello ваш локальный репозиторий Git.
3. Используйте `git remote` tooadd hello удаленную ссылку в **URL-адрес Git** из шага 1. Команда будет выглядеть примерно toohello следующее:
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > Hello **удаленного** команда добавляет в удаленном репозитории tooa именованную ссылку. В этом примере создается ссылка с именем azure для репозитория вашего веб-приложения.
   > 
   > 
4. Push вашего содержимого tooApp службы с помощью нового hello **azure** удаленного вы только что создали.

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. Вы можете вернуться tooyour приложения hello портала Azure. Запись журнала последней передачу должны отображаться в hello **развертываний** колонку. 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. Нажмите кнопку hello **Обзор** кнопку вверху hello приложение hello колонке tooverify hello содержимого был развернут. 

## <a name="Step5"></a>Устранение неполадок
Hello ниже приведены ошибок или проблем, обычно возникающих при использовании Git toopublish tooan приложением служб приложений в Azure.

- - -
**Симптом**: не удается tooaccess [siteURL]: не удалось выполнить tooconnect слишком [scmAddress]

**Причина**: Эта ошибка может возникать, если приложение hello не запущен и работает.

**Разрешение**: приложения hello запуска в hello портала Azure. Развертывание Git не будет работать, пока не будет запущен приложение hello. 

- - -
**Симптом**: не удается разрешить hostname узла.

**Причина**: Эта ошибка может произойти, если ввести сведения hello адрес при создании hello удаленного «azure» неверно.

**Разрешение**: hello используйте `git remote -v` команды toolist все удаленные элементы, связанные hello URL-адресом. Проверьте правильность URL-адрес hello hello «azure» на удаленном. При необходимости удалите и повторно создайте этот удаленный с помощью hello правильный URL-адрес.

- - -
**Симптом**: нет ссылок и ничего не указано; ничего не выполняется. Возможно, следует указать ветвь, например master.

**Причина**: Эта ошибка может возникать, если не указать ветви, при выполнении операции git push и иметь не набор hello push.default значение, используемое Git.

**Разрешение**: выполнить hello принудительную попытку, указав hello главную ветвь. Например:

```bash  
git push azure master
```
- - -
**Симптом**: src refspec [имя_ветви] не соответствует никакой ветви.

**Причина**: Эта ошибка может возникать при попытке toopush tooa ветвь, кроме master на hello «azure» на удаленном.

**Разрешение**: выполнить hello принудительную попытку, указав hello главную ветвь. Например:

```bash  
git push azure master
```
- - -
**Симптом**. Сбой RPC, результат — 22, код HTTP — 502.

**Причина**: Эта ошибка может возникать при попытке toopush больших репозитория по протоколу HTTPS.

**Разрешение**: изменение конфигурации git hello на hello локального компьютера toomake hello postBuffer больше

```bash  
git config --global http.postBuffer 524288000
```
- - -
**Симптом**: ошибка - репозитория tooremote зафиксированные изменения, кроме веб-приложения не обновляется.

**Причина**: эта ошибка может возникнуть при развертывании приложения Node.js, содержащего файл package.json, в котором указаны дополнительные необходимые модули.

**Решение.** До этой ошибки должны быть зарегистрированы должно быть toothis журнал предыдущих ошибок и может предоставить дополнительный контекст при сбое hello. Hello следующие известные причины этой ошибки и hello соответствующий «npm ERR!» сообщение:

* **Malformed package.json file**: npm ERR! Couldn't read dependencies (не удалось прочитать зависимости).
* **Собственный модуль, не имеющий двоичного дистрибутива для Windows**:
  
  * npm ERR! \`cmd "/c" "node-gyp rebuild"\` failed with 1 (команда cmd "/c" "node-gyp rebuild" привела к сбою с 1)
    
      ИЛИ
  * npm ERR! [modulename@version] preinstall: \`make || gmake\`

## <a name="additional-resources"></a>дополнительные ресурсы.
* [Документация по Git](http://git-scm.com/documentation)
* [Документация по проекту Kudu](https://github.com/projectkudu/kudu/wiki)
* [TooAzure непрерывного развертывания служб приложений](app-service-continuous-deployment.md)
* [Как toouse PowerShell для Azure](/powershell/azure/overview)
* [Как toouse hello интерфейса командной строки Azure](../cli-install-nodejs.md)

[службе приложений Azure]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[портала Azure]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[интерфейса командной строки Azure]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
