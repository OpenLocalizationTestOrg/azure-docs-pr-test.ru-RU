---
title: "hello tooUse aaaHow Engagement API для Windows Universal."
description: "Как tooUse hello Engagement API для Windows Universal."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: bb501fca-9cfe-4495-81df-b5efd6e0137b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0256b839c28e4ef6c530106408d744038fa711ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-universal"></a>Как tooUse hello Engagement API для Windows Universal.
Этот документ является документом надстройку toohello [как tooIntegrate участия в универсальное приложение для Windows](mobile-engagement-windows-store-integrate-engagement.md): он предоставляет сведения о как toouse hello Engagement API tooreport статистике приложения.

Имейте в виду, что если требуется только Engagement tooreport приложения сеансы, действия, сбои и технические сведения, затем hello самым простым способом является toomake все вашей `Page` вложенные классы наследуют от hello `EngagementPage` класса.

Если требуется toodo дополнительные, например, если вам требуется tooreport приложения определенных событий, ошибок и задания или при наличии tooreport действия приложения по-другому, чем один реализованный в hello hello `EngagementPage` классов, то вы должны toouse hello Engagement API.

Hello Engagement API обеспечивается hello `EngagementAgent` класса. Вы можете обратиться к методам toothose через `EngagementAgent.Instance`.

Даже если модуль агентом hello не был инициализирован, каждый вызов API toohello откладывается и будет выполнена повторно при hello доступен.

## <a name="engagement-concepts"></a>Основные понятия Engagement
Hello следующие части уточнения hello Общие [Mobile Engagement понятия](mobile-engagement-concepts.md) для платформы универсальных Windows hello.

### <a name="session-and-activity"></a>`Session` и `Activity`
*Действия* обычно связана с одной страницы приложения hello, toosay hello *действия* начинается, когда страница приветствия отображается и прекращается после закрытия страницы приветствия: hello случае при hello Engagement SDK интегрирован с помощью hello `EngagementPage` класса.

Но *действия* может также осуществляться вручную с помощью Engagement API hello. Это позволяет toosplit данной странице в нескольких sub tooget частей Дополнительные сведения об использовании hello этой страницы (например tooknow как часто и как долго диалоговые окна используются внутри этой страницы).

## <a name="reporting-activities"></a>Уведомление о действиях
### <a name="user-starts-a-new-activity"></a>Запуск нового действия пользователем
#### <a name="reference"></a>Справочные материалы
            void StartActivity(string name, Dictionary<object, object> extras = null)

Требуется toocall `StartActivity()` каждое действие пользователя hello время изменяется. функции Hello первый вызов toothis начинает новый сеанс пользователя.

> [!IMPORTANT]
> пакет SDK для Hello автоматически вызывает метод hello действие завершения, при закрытии приложения hello. Таким образом настоятельно рекомендуется метод StartActivity toocall hello всякий раз, когда меняется hello действий пользователя hello и завершен вызов tooNEVER hello метод действие завершения, с момента вызова этого метода заставляет toobe hello текущего сеанса.
> 
> 

#### <a name="example"></a>Пример
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a>Завершение текущего действия пользователем
#### <a name="reference"></a>Справочные материалы
            void EndActivity()

Действие hello и hello сеанс будет завершен. Не следует вызывать этот метод, если не вполне ясно, что он делает.

#### <a name="example"></a>Пример
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a>Уведомление о заданиях
### <a name="start-a-job"></a>Запустите задание
#### <a name="reference"></a>Справочные материалы
            void StartJob(string name, Dictionary<object, object> extras = null)

Tootrack certains hello рабочих заданий можно использовать за период времени.

#### <a name="example"></a>Пример
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a>Конец задания
#### <a name="reference"></a>Справочные материалы
            void EndJob(string name)

Сразу после завершения задачи, отслеживаются с помощью задания hello EndJob метод следует вызывать для данного задания, указав имя задания hello.

#### <a name="example"></a>Пример
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a>Уведомление о событиях
Существует три типа событий:

* Изолированные события
* События сеанса
* События задания

### <a name="standalone-events"></a>Изолированные события
#### <a name="reference"></a>Справочные материалы
            void SendEvent(string name, Dictionary<object, object> extras = null)

Автономный события могут происходить за пределами hello контекст сеанса.

#### <a name="example"></a>Пример
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a>События сеанса
#### <a name="reference"></a>Справочные материалы
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

События сеанса — это обычно используется tooreport hello действия, выполняемые пользователем во время сеанса.

#### <a name="example"></a>Пример
**Без данных:**

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

**С данными:**

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a>События задания
#### <a name="reference"></a>Справочные материалы
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

Задания события, обычно используемых tooreport hello действия, выполняемые пользователем во время выполнения задания.

#### <a name="example"></a>Пример
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a>Уведомление об ошибках
Существует три типа ошибок:

* Изолированные ошибки
* Ошибки сеанса
* Ошибки заданий

### <a name="standalone-errors"></a>Изолированные ошибки
#### <a name="reference"></a>Справочные материалы
            void SendError(string name, Dictionary<object, object> extras = null)

Ошибки противоположные toosession автономный ошибки могут возникать за пределами hello контекст сеанса.

#### <a name="example"></a>Пример
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a>Ошибки сеанса
#### <a name="reference"></a>Справочные материалы
            void SendSessionError(string name, Dictionary<object, object> extras = null)

Ошибки сеанса это обычно используется tooreport hello ошибки, влияющие на hello пользователя во время сеанса.

#### <a name="example"></a>Пример
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a>Ошибки заданий
#### <a name="reference"></a>Справочные материалы
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

Ошибки могут быть связанные tooa выполнения задания, а связанные с toohello текущий сеанс пользователя.

#### <a name="example"></a>Пример
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a>Сбои отчетов
агент Hello предоставляет два toodeal методы сбоев.

### <a name="send-an-exception"></a>Отправка исключения
#### <a name="reference"></a>Справочные материалы
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a>Пример
Исключение можно отправить в любое время, вызвав:

            EngagementAgent.Instance.SendCrash(aCatchedException);

Также можно использовать сеанс необязательный параметр hello tooterminate engagement момент hello то же время, чем отправка hello аварийного завершения. Таким образом, вызов toodo:

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

Если это сделать, сеанс hello и заданий будет закрыто сразу после отправки hello аварийного завершения.

### <a name="send-an-unhandled-exception"></a>Отправка необработанного исключения
#### <a name="reference"></a>Справочные материалы
            void SendCrash(Exception e)

Engagement предоставляет метод toosend необработанных исключений, если у вас есть **отключено** Engagement automatic **аварийного завершения** отчетов. Это особенно полезно при использовании внутри обработчика событий UnhandledException приложения hello.

Этот метод будет **всегда** завершить сеанс engagement hello и задания после вызова.

#### <a name="example"></a>Пример
Его можно использовать tooimplement UnhandledExceptionEventArgs обработчик. Например, добавить hello `Current_UnhandledException` метод hello `App.xaml.cs` файла:

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

В файле App.xaml.cs в Public App(){} добавьте следующее:

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a>Идентификатор устройства
            String EngagementAgent.Instance.GetDeviceId()

Идентификатор устройства engagement hello можно получить путем вызова данного метода.

## <a name="extras-parameters"></a>Дополнительные параметры
Произвольные данные могут быть tooan вложенное событие, ошибка, действия или задания. Эти данные можно структурировать по словарю. Ключи и значения могут принадлежать к любому типу.

Вспомогательные элементы данных сериализуются, поэтому если требуется tooinsert свой собственный тип в дополнения tooadd контракт данных для этого типа.

### <a name="example"></a>Пример
Создадим новый класс Person.

            using System.Runtime.Serialization;

            namespace Microsoft.Azure.Engagement
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

Затем мы добавим `Person` дополнительных tooan экземпляра.

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> Если поместить другие типы объектов, убедитесь, что их метода ToString() — реализовано tooreturn удобную для восприятия строку.
> 
> 

### <a name="limits"></a>Ограничения
#### <a name="keys"></a>ключей
Каждый ключ в hello объекта должно соответствовать hello следующее регулярное выражение:

`^[a-zA-Z][a-zA-Z_0-9]*$`

Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).

#### <a name="size"></a>Размер
Дополнения ограничены слишком**1024** знаков в каждом вызове.

## <a name="reporting-application-information"></a>Уведомление о данных приложения
### <a name="reference"></a>Справочные материалы
            void SendAppInfo(Dictionary<object, object> appInfos)

Можно вручную сообщить отслеживания сведения (или любые другие сведения о приложении), с помощью функции SendAppInfo() hello.

Обратите внимание, что эти данные можно отправить постепенно: hello только последнее значение для указанного ключа, которые будут храниться для данного устройства. Как дополнения событий и использовать словарь\<объекта, объект\> tooattach данных.

### <a name="example"></a>Пример
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a>Ограничения
#### <a name="keys"></a>ключей
Каждый ключ в hello объекта должно соответствовать hello следующее регулярное выражение:

`^[a-zA-Z][a-zA-Z_0-9]*$`

Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).

#### <a name="size"></a>Размер
Сведения о приложении ограничено слишком**1024** знаков в каждом вызове.

В hello предыдущего примера hello JSON, отправленных сервером toohello является 44 символов:

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a>Ведение журналов
### <a name="enable-logging"></a>Включение ведения журналов
Hello SDK может быть настроенный tooproduce журналы тестирования в консоли hello интегрированной среды разработки.
По умолчанию эти журналы не активированы. toocustomize hello, обновить свойство `EngagementAgent.Instance.TestLogEnabled` tooone hello значения, доступные из hello `EngagementTestLogLevel` перечисления, например:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

