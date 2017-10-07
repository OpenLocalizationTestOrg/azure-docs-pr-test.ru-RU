---
title: "aaaHow toouse hello Azure ведомый подключаемого модуля в непрерывной интеграции Hudson | Документы Microsoft"
description: "Описывает, как подчиненного подключаемого модуля в непрерывной интеграции Hudson toouse hello Azure."
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a>Как toouse hello Azure подчиненного подключаемого модуля в непрерывной интеграции Hudson
Hello Azure ведомый подключаемого модуля для Hudson включает узлы ведомый tooprovision в Azure при построении выполнения распределенных.

## <a name="install-hello-azure-slave-plug-in"></a>Установка hello Azure ведомый подключаемого модуля
1. В hello Hudson панели мониторинга щелкните **управление Hudson**.
2. В hello **управление Hudson** щелкните **управление подключаемыми модулями**.
3. Нажмите кнопку hello **доступно** вкладки.
4. Нажмите кнопку **поиска** и тип **Azure** toolimit hello список toorelevant подключаемых модулей.
   
    В случае tooscroll через hello список доступных подключаемых модулей, вы найдете hello Azure ведомый подключаемого модуля в разделе hello **управления кластером и распределенных построения** раздела hello **другие** вкладку.
5. Установите флажок hello для **подключаемый модуль Azure ведомый**.
6. Щелкните **Install**(Установить).
7. Перезапустите Hudson.

Теперь, "hello" подключаемый модуль установлен, hello дальнейшие действия будет tooconfigure hello подключаемого модуля с помощью профиля подписки Azure и toocreate шаблона, который будет использоваться при создании hello виртуальной Машины для узла ведомый hello.

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a>Настройка hello Azure ведомый подключаемого модуля с помощью профиля подписки
Профиль подписки также назывались tooas параметры публикации, XML-файл, содержащий ваши учетные данные и Дополнительные сведения, вам потребуется toowork с Azure в среде разработки. tooconfigure hello Azure ведомый подключаемый модуль, необходимо:

* идентификатор подписки;
* сертификат управления подпиской.

Эти сведения можно найти в [профиле подписки]. Ниже приведен пример профиля подписки.

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

Получив профиле подписки, выполните эти шаги tooconfigure hello Azure ведомый подключаемого модуля.

1. В hello Hudson панели мониторинга щелкните **управление Hudson**.
2. Щелкните **Configure System**(Настройка системы).
3. Прокрутите вниз hello toofind страницы приветствия **облака** раздела.
4. Щелкните **Add new cloud > Microsoft Azure** (Добавить новое облако > Microsoft Azure).
   
    ![добавление нового облака][add new cloud]
   
    При этом будут отображены поля hello, где требуется tooenter сведениях о подписке.
   
    ![настройка профиля][configure profile]
5. Скопировать hello ИД подписки и управления сертификат профиля подписки и вставьте их в соответствующие поля hello.
   
    При копировании hello ИД подписки и управления сертификат, **не** используйте кавычки hello, заключите hello значения.
6. Щелкните **Verify configuration**(Проверить конфигурацию).
7. После проверки конфигурации hello щелкните **Сохранить**.

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a>Настройка шаблона виртуальной машины для hello Azure ведомый подключаемого модуля
Шаблон виртуальной машины определяет параметры hello hello подключаемый модуль будет использовать toocreate подчиненного узла в Azure. В следующие шаги hello будут созданы шаблон для Виртуальной машине Ubuntu.

1. В hello Hudson панели мониторинга щелкните **управление Hudson**.
2. Щелкните **Configure System**(Настройка системы).
3. Прокрутите вниз hello toofind страницы приветствия **облака** раздела.
4. В рамках hello **облака** найдите **добавить шаблон виртуальной машины Azure** и нажмите кнопку hello **добавить** кнопки.
   
    ![добавление шаблона виртуальной машины][add vm template]
5. Укажите имя облачной службы в hello **имя** поля. Если имя hello ссылается tooan существующей облачной службы, службы будут подготовлены hello виртуальной Машины. В противном случае Azure создаст новую службу.
6. В hello **описание** введите текст, описывающий шаблон hello, вы создаете. Эти сведения будут использоваться только в информационных целях и при подготовке виртуальной машины не учитываются.
7. В hello **метки** введите **linux**. Эта метка используется tooidentify hello шаблон, который вы создаете и впоследствии используется tooreference hello шаблона при создании задания Hudson.
8. Выберите регион, где будут создаваться hello виртуальной Машины.
9. Выберите соответствующий размер виртуальной Машины hello.
10. Укажите учетную запись хранилища, где будут создаваться hello виртуальной Машины. Убедитесь, что он находится в hello же регионе, что hello облачной службы, вы будете использовать. Если требуется новый toobe хранилища создана, это поле можно оставить пустым.
11. Время хранения указывает hello количество минут, прежде чем Hudson удаляет ведомый простоя. Оставьте значение по умолчанию hello 60.
12. В **использование**, выберите hello соответствующее условие, если будет использоваться этот подчиненный узел. На этом этапе выберите вариант **Utilize this node as much as possible**(Использовать этот узел постоянно).
    
     На этом этапе в форму будет выглядеть напоминает toothis:
    
     ![настройка шаблона][template config]
13. В **семейства или идентификатор** у вас есть toospecify какие образ системы будет установлено на виртуальной Машине. Выберите образ из списка семейств или укажите пользовательский вариант.
    
     Tooselect из списка семейств изображение, введите hello первого символа (с учетом регистра) имя семейства hello изображения. Например, если вы введете **U** , появится список семейств Ubuntu Server. После выбора из списка hello Jenkins будет использовать последнюю версию этого образ системы на основе этого семейства hello при подготовке виртуальной Машины.
    
     ![список семейств ОС][OS family list]
    
     При наличии пользовательского изображения вместо этого нужно toouse, введите имя hello этого настраиваемого образа. Имена пользовательских изображений не отображаются в списке, у вас есть что tooensure, hello имя введено правильно.    
    
     В этом учебнике введите **U** toobring список изображений Ubuntu и выберите **Ubuntu Server 14.04 LTS**.
14. В поле **Launch method** (Способ запуска) выберите **SSH**.
15. Скопируйте приведенный ниже сценарий hello и включите в hello **сценарий Init** поля.
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     Hello **сценарий Init** будет выполняться после создания ВМ hello. В этом примере hello скрипт устанавливает Java, git и ant.
16. В hello **Username** и **пароль** введите предпочтительные значения для учетной записи администратора hello, который будет создан на ВМ.
17. Щелкните **Проверка шаблона** toocheck, если выбраны параметры hello являются допустимыми.
18. Щелкните **Save**(Сохранить).

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a>Создание задания Hudson, выполняемого в подчиненном узле в Azure
В этом разделе вы узнаете, как создать задачу Hudson, которая должна выполняться в подчиненном узле в Azure.

1. В hello Hudson панели мониторинга щелкните **новое задание**.
2. Введите имя для задания hello, который вы создаете.
3. Выберите тип задания hello **задание программного обеспечения освободить стиль сборки**.
4. Нажмите кнопку **ОК**.
5. На странице конфигурации задания hello, выберите **ограничение, когда этот проект может быть выполнена**.
6. Выберите **узел и метки меню** и выберите **linux** (указываются эту метку при создании шаблона виртуальной машины hello в предыдущем разделе hello).
7. В hello **построения** щелкните **добавить шаг сборки** и выберите **выполнение оболочки**.
8. Изменить hello следующий скрипт, заменив **{имя учетной записи github}**, **{имя_проекта}**, и **{каталог проекта}** с соответствующие значения и вставьте hello изменить скрипт в hello текстовое поле, которое отображается.
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. Щелкните **Save**(Сохранить).
10. В панели мониторинга Hudson hello, найдите только что созданную задание hello и щелкните hello **запланировать построения** значок.

Hudson будет затем создайте подчиненного узла, используя шаблон hello, созданный в предыдущем разделе hello и выполнить скрипт hello, указанное на шаге hello сборки для выполнения этой задачи.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure].

<!-- URL List -->

[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[профиле подписки]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

