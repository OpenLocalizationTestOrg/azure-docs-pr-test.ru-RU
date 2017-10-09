---
title: "события жизненного цикла облачной службы aaaHandle | Документы Microsoft"
description: "Узнайте, как можно использовать методы жизненного цикла hello роли облачной службы в .NET"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 39b30acd-57b9-48b7-a7c4-40ea3430e451
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: cc0ccc5f055b965202b6e081a6ab72ad5d39b034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-lifecycle-of-a-web-or-worker-role-in-net"></a>Настройка hello жизненным циклом рабочих и веб-роли в .NET
При создании рабочей роли, можно расширить hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) класс, который предоставляет методы для вас toooverride, которые позволяют реагировать toolifecycle события. Для веб-ролей этот класс является необязательным, поэтому вы должны использовать toorespond toolifecycle события.

## <a name="extend-hello-roleentrypoint-class"></a>Расширение класса RoleEntryPoint hello
Hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) класс содержит методы, которые вызываются Azure при его **запускает**, **выполняется**, или **останавливает** рабочих и веб-роли. При необходимости можно переопределить эти методы toomanage роли инициализации, последовательность завершения работы роли или hello потоком выполнения роли hello. 

При расширении **RoleEntryPoint**, следует помнить о следующих поведений методов hello hello:

* Hello [OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) и [OnStop](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) методы возвращают логическое значение, поэтому вполне возможно tooreturn **false** из этих методов.
  
   Если код возвращает **false**, hello роль процесса немедленно завершается, запуская любая последовательность завершения работы имеется на месте. В общем случае следует возвращать **false** из hello **OnStart** метод.
* При любом неперехваченном исключении при перегрузке **RoleEntryPoint** метод рассматривается как необработанное исключение.
  
   При возникновении исключения в одном из методов жизненного цикла hello Azure отправит событие hello [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) события, и затем hello процесс завершается. После перевода вашей роли в автономный режим Azure перезапустит ее. При возникновении необработанного исключения, hello [остановка](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.stopping.aspx) событие не возникает и hello **OnStop** метод не вызывается.

Если ваша роль не запускается или перезапуска между hello инициализации, занятости и остановки состояния, код может вызывает необработанное исключение в одном из событий жизненного цикла hello каждой роли hello время перезагрузки компьютера. В этом случае использовать hello [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) toodetermine событий hello причиной исключения hello и выполнить соответствующую обработку. Роли могут также возвращает значение из hello [запуска](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) метод, который вызывает toorestart роли hello. Дополнительные сведения о состоянии развертывания см. в разделе [tooRecycle типичных проблем которой причина ролей](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).

> [!NOTE]
> Если вы используете hello **средства Azure для Microsoft Visual Studio** toodevelop приложения hello шаблоны проекта роли автоматически расширяют hello **RoleEntryPoint** класса, в hello *WebRole.cs* и *WorkerRole.cs* файлов.
> 
> 

## <a name="onstart-method"></a>Метод OnStart
Hello **OnStart** метод вызывается, когда экземпляр роли переводится в оперативный режим в Azure. Пока hello код метода OnStart, экземпляр роли hello помечен как **Busy** и внешний трафик не будет направленной tooit подсистемой балансировки нагрузки hello. Можно переопределить этот метод tooperform инициализации работы, например реализации обработчиков событий и запуска [диагностики Azure](cloud-services-how-to-monitor.md).

Если **OnStart** возвращает **true**, hello экземпляр инициализирован успешно и Azure вызывает метод hello **RoleEntryPoint.Run** метод. Если **OnStart** возвращает **false**, hello роль немедленно завершается без выполнения любой запланированных последовательностей завершения работы.

Здравствуйте, следуя примере кода показано, как toooverride hello **OnStart** метод. Этот метод настраивает и запускает монитор диагностики при запуске экземпляра роли hello и передачу данных учетной записи хранилища tooa ведения журнала:

```csharp
public override bool OnStart()
{
    var config = DiagnosticMonitor.GetDefaultInitialConfiguration();

    config.DiagnosticInfrastructureLogs.ScheduledTransferLogLevelFilter = LogLevel.Error;
    config.DiagnosticInfrastructureLogs.ScheduledTransferPeriod = TimeSpan.FromMinutes(5);

    DiagnosticMonitor.Start("DiagnosticsConnectionString", config);

    return true;
}
```

## <a name="onstop-method"></a>Метод OnStop
Hello **OnStop** метод вызывается после экземпляра роли переведены в автономный режим Azure и до завершения процесса hello. Можно переопределить этот метод toocall код, требуемый для вашей роли экземпляра toocleanly, завершение работы.

> [!IMPORTANT]
> Код, выполняющийся в hello **OnStop** метод имеет toofinish ограниченное время, когда он вызывается по причине остановки, инициированной пользователем. По истечении этого времени hello процесс завершается, поэтому вы должны убедиться, что этот код в hello **OnStop** метод выполняется быстро и допускает toocompletion не запущена. Hello **OnStop** метод вызывается после hello **остановки** события.
> 
> 

## <a name="run-method"></a>Метод Run
Можно переопределить hello **запуска** метод tooimplement длительно выполняемого потока для экземпляра роли.

Переопределение hello **запуска** метод не является обязательным; реализация по умолчанию hello запускает постоянно спящий поток. При переопределении hello **запуска** метод, код должен блокироваться бесконечно. Если hello **запуска** методом hello роль автоматически перезапускается; другими словами, Azure отправляет hello **остановка** событий и вызовов hello **OnStop** метод, может выполнить последовательность завершения работы до выключения роли hello.

### <a name="implementing-hello-aspnet-lifecycle-methods-for-a-web-role"></a>Реализация методов жизненного цикла ASP.NET hello для веб-роли
Можно использовать методы жизненного цикла ASP.NET hello, кроме предоставляемых hello toothose **RoleEntryPoint** класса toomanage последовательности инициализации и завершения работы для веб-роли. Это может быть полезным для обеспечения совместимости при переносе существующего tooAzure приложения ASP.NET. Hello методы жизненного цикла ASP.NET вызываются из внутри hello **RoleEntryPoint** методы. Hello **приложения\_запустить** метод вызывается после hello **RoleEntryPoint.OnStart** метод завершения. Hello **приложения\_окончания** метод вызывается перед hello **RoleEntryPoint.OnStop** вызывается метод.

## <a name="next-steps"></a>Дальнейшие действия
Узнайте, каким образом слишком[создать пакет облачной службы](cloud-services-model-and-package.md).

