---
title: "aaaRun задачи запуска в облачных службах Azure | Документы Microsoft"
description: "Задачи запуска помогают подготовить среду облачной службы для приложения. Это объясняется, как рабочих задач запуска и как toomake их"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 3391a5d7434164f59972b8e497e5c34e33409543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a>Выполнение задач запуска tooconfigure и выполнения для облачной службы
Можно использовать операции tooperform запуска задачи до запуска роли. Операции, вы можете tooperform включают установки компонента, регистрация компонентов COM, установка разделов реестра или запуск длительного процесса.

> [!NOTE]
> При запуске задачи не машины tooVirtual применимо, только tooCloud Service Web и рабочих ролей.
> 
> 

## <a name="how-startup-tasks-work"></a>Как работают задачи запуска
Задачи запуска — действия, выполняемые до роли begin и определены в hello [ServiceDefinition.csdef] файла с помощью hello [задачи] элемент в пределах hello [запуска]элемент. Часто задачи запуска — это пакетные файлы, но они также могут быть консольными приложениями или пакетными файлами, запускающими сценарии PowerShell.

Переменные среды передают сведения в задачу запуска, и локальное хранилище можно использовать toopass сведения из задачи запуска. Например, переменная среды можно указать hello путь tooa программы требуется tooinstall, а файлы могут быть записаны toolocal хранилище, могут считываться позже вашей роли.

Задача запуска может записывать сведения и ошибки toohello каталог, заданный параметром hello **TEMP** переменной среды. Во время выполнения задачи запуска hello, hello **TEMP** переменной среды устраняет toohello *C:\\ресурсов\\temp\\[guid]. [ roleName]\\RoleTemp* каталог при выполнении в облаке hello.

Кроме того, задачи запуска могут выполняться несколько раз между перезагрузками. Например hello задача запуска будет выполняться при каждом перезапуске роли hello и они могут не всегда связано с перезагрузкой. Задачи запуска должен быть написан таким образом, их toorun несколько раз без проблем.

Задачи запуска должны заканчиваться **errorlevel** (или кодом выхода) ноль toocomplete процесс запуска hello. Если задача запуска оканчивается ненулевым **errorlevel**, hello роль не запускается.

## <a name="role-startup-order"></a>Порядок запуска роли
Hello ниже приведена процедура запуска роли hello в Azure.

1. Hello экземпляр помечен как **запуск** и не принимает трафика.
2. Все задачи запуска выполняются в соответствии с tootheir **taskType** атрибута.
   
   * Hello **простой** задачи выполняются синхронно, по одному.
   * Hello **фона** и **переднего плана** задачи — задача запуска работает асинхронно, параллельные toohello.  
     
     > [!WARNING]
     > Службы IIS могут не полностью настроен во время этапа запуска задач hello в процессе запуска hello, поэтому данные, зависящие от роли могут быть недоступны. Для задач запуска, требующих данные, относящиеся к роли, следует использовать [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).
     > 
     > 
3. запускается процесс размещения роли Hello и в службах IIS создается узел hello.
4. Hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) вызывается метод.
5. Hello экземпляр помечен как **готовности** и трафика перенаправленное toohello экземпляра.
6. Hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) вызывается метод.

## <a name="example-of-a-startup-task"></a>Пример задачи запуска
Задачи запуска определяются в hello [ServiceDefinition.csdef] файла в hello **задачи** элемента. Hello **commandLine** атрибут указывает имя hello и параметры hello пакетный файл или с помощью консоли команду, hello **executionContext** атрибут задает hello права доступа для запуска hello Задача и hello **taskType** атрибут указывает, каким образом будет выполняться задача hello.

В этом примере переменной среды **MyVersionNumber**, создается для задачи запуска hello и задать значение toohello "**1.0.0.0**».

**ServiceDefinition.csdef**:

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

В следующем примере hello, hello **Startup.cmd** пакетный файл записывает строку hello «hello текущая версия — 1.0.0.0» файл StartupLog.txt toohello в каталоге hello, указанном в переменной среды TEMP hello. Hello `EXIT /B 0` строки гарантирует, что hello задача запуска оканчивается **errorlevel** равно нулю.

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> В Visual Studio hello **скопируйте каталог tooOutput** свойства для пакетного файла запуска должно быть установлено слишком**всегда Копировать** toobe, убедитесь, что пакетный файл запуска должным образом развернут tooyour проекта в Azure (**approot\\bin** для веб-ролей и **approot** для рабочих ролей).
> 
> 

## <a name="description-of-task-attributes"></a>Описание атрибутов задачи
Hello ниже описываются атрибуты hello hello **задачи** элемент в hello [ServiceDefinition.csdef] файла:

**Командная строка** -указывает hello командной строки для запуска задачи hello:

* Hello команда с необязательными параметрами командной строки, которая начинает задачу запуска hello.
* Часто это имя файла hello .cmd или .bat пакетный файл.
* Задача Hello — относительный toohello AppRoot\\папка Bin для развертывания hello. Переменные среды не будут развернуты при определении пути hello и задачи «hello». Если требуется расширение среды, можно создать небольшой CMD-файл сценария, который вызывает задачу запуска.
* Может быть консольным приложением или пакетным файлом, который запускает [сценарий PowerShell](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).

**executionContext** -указывает hello уровень прав доступа для запуска задачи hello. уровень прав доступа Hello можно ограничены или с повышенными привилегиями:

* **limited**  
  Hello задача запуска выполняется с одинаковыми правами как роль hello hello. Здравствуйте, когда **executionContext** атрибут для hello [среды выполнения] элемент является также **ограниченный**, то используются права доступа пользователя.
* **elevated**  
  Hello задача запуска выполняется с правами администратора. Это позволяет задачи запуска программы tooinstall, внести изменения в конфигурацию IIS, выполнять изменения в реестр, а также другие административные задачи без увеличения hello права доступа для самой роли hello.  

> [!NOTE]
> Hello уровень прав доступа задачи запуска не требуется toobe Здравствуйте таким же, как сама роль hello.
> 
> 

**Тип задачи** -указывает, выполняется hello, каким образом задачи запуска.

* **Простые**  
  Задачи выполняются синхронно, одновременно в порядке hello, указываемой hello [ServiceDefinition.csdef] файла. Если в одном **простой** задача запуска оканчивается **errorlevel** равна нулю, hello рядом **простой** выполнения задачи запуска. Если больше нет **простой** задач запуска tooexecute, а затем запускается сама роль hello.   
  
  > [!NOTE]
  > Если hello **простой** задача оканчивается с ненулевым **errorlevel**, hello экземпляр блокируется. Последующие **простой** задачи запуска и сама роль hello не запустится.
  > 
  > 
  
    tooensure, которая заканчивается пакетный файл **errorlevel** равна нулю, выполните команду hello `EXIT /B 0` конце hello процесса пакетного файла.
* **background**  
  Задачи выполняются асинхронно, параллельно с запуска hello hello роли.
* **переднего плана**  
  Задачи выполняются асинхронно, параллельно с запуска hello hello роли. Здравствуйте, основное отличие между **переднего плана** и **фона** том, что **переднего плана** задача позволяет роли hello из перезапуск или завершение работы, пока не получит задачу hello завершено. Hello **фона** задачи не имеют этого ограничения.

## <a name="environment-variables"></a>Переменные среды
Переменные среды — задача запуска tooa способом toopass сведения. Например можно поместить hello путь tooa blob, содержащий tooinstall программы или номера портов, которые будет использовать роль или параметров функций toocontrol задачей запуска.

Существует два типа переменных среды для задачи запуска; статические переменные среды и переменные среды на основе членов hello [ RoleEnvironment] класса. Обе они находятся в hello [среды] раздел hello [ServiceDefinition.csdef] файл и оба hello используйте [переменных] элемент и **имя** атрибут.

Hello использует переменные среды статических **значение** атрибут hello [переменных] элемента. Приведенный выше пример Hello создает переменную среды hello **MyVersionNumber** содержит статическое значение «**1.0.0.0**». Другим примером может служить toocreate **StagingOrProduction** переменной среды, которую можно установить вручную, toovalues из «**промежуточных**«или»**рабочей**» tooperform различных действий запуска на основе hello значения hello **StagingOrProduction** переменной среды.

Не используйте переменные среды на основе членов класса RoleEnvironment hello hello **значение** атрибут hello [переменных] элемента. Вместо этого hello [RoleInstanceValue] дочерний элемент с hello соответствующие **XPath** значение атрибута, будут использоваться toocreate переменной среды, в зависимости от конкретного члена hello [ RoleEnvironment] класса. Значения для hello **XPath** атрибута tooaccess различных [ RoleEnvironment] значения можно найти [здесь](cloud-services-role-config-xpath.md).

К примеру, toocreate переменной среды, "**true**» при запуске hello в эмуляторе вычислений hello, и"**false**» при работе в облаке hello используйте следующие hello [переменных] и [RoleInstanceValue] элементов:

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create hello environment variable that informs hello startup task whether it is running
                in hello Compute Emulator or in hello cloud. "%ComputeEmulatorRunning%"=="true" when
                running in hello Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in hello cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a>Дальнейшие действия
Узнайте, как tooperform некоторые [общие задачи запуска](cloud-services-startup-tasks-common.md) с облачной службой.

[Упакуйте](cloud-services-model-and-package.md) облачную службу.  

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[задачи]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[запуска]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[среды выполнения]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[среды]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[переменных]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[ RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
