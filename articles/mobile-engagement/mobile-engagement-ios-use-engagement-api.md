---
title: "hello tooUse aaaHow Engagement API для iOS"
description: "Последние iOS SDK — как tooUse hello API участия в iOS"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1fb4509e-3804-46c1-949f-1cf727f91f9f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 7fb9b95ad319cf3b1e2de81b5d6aee5b30266069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-ios"></a>Как tooUse hello API участия в iOS
Этот документ является документом toohello надстройку как tooIntegrate Engagement на iOS: он предоставляет сведения о как toouse hello Engagement API tooreport статистики вашего приложения.

Имейте в виду, что если требуется только Engagement tooreport приложения сеансы, действия, сбои и технические сведения, затем hello простой способ основан toomake всех пользовательских `UIViewController` объекты наследуют от соответствующего hello `EngagementViewController` класса .

Если требуется toodo дополнительные, например, если вам требуется tooreport приложения определенных событий, ошибок и задания или при наличии tooreport действия приложения по-другому, чем один реализованный в hello hello `EngagementViewController` классов, то вы должны toouse hello Engagement API.

Hello Engagement API обеспечивается hello `EngagementAgent` класса. Экземпляр этого класса можно получить путем вызова hello `[EngagementAgent shared]` статическим методом (Обратите внимание, что hello `EngagementAgent` возвращаемый объект — единственное значение).

Прежде чем все вызовы API, hello `EngagementAgent` необходимо инициализировать объект с помощью вызова метода hello`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`

## <a name="engagement-concepts"></a>Основные понятия Engagement
Hello следующие части уточнения hello Общие [Mobile Engagement понятия](mobile-engagement-concepts.md) для платформы iOS hello.

### <a name="session-and-activity"></a>`Session` и `Activity`
*Действия* обычно связана с одного экрана приложения hello, toosay hello *действия* начинается, когда экран приветствия отображается и останавливается при закрытии экрана приветствия: это hello случай, когда Hello Engagement SDK интегрирован с помощью hello `EngagementViewController` классы.

Но *действия* может также осуществляться вручную с помощью Engagement API hello. Это позволяет toosplit указанными экранными несколько частей tooget sub, Дополнительные сведения о hello использования данного экрана (например tooknown как часто и как долго диалоговые окна используются внутри этот экран).

## <a name="reporting-activities"></a>Уведомление о действиях
### <a name="user-starts-a-new-activity"></a>Запуск нового действия пользователем
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

Требуется toocall `startActivity()` каждое действие пользователя hello время изменяется. функции Hello первый вызов toothis начинает новый сеанс пользователя.

### <a name="user-ends-his-current-activity"></a>Завершение текущего действия пользователем
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> Вы должны **никогда** эта функция вызывается в одиночку, за исключением того, если требуется, чтобы toosplit один из способов использования приложения в нескольких сеансах: вызов функции toothis приведет к завершению hello текущий сеанс немедленно, таким образом, следующий вызов слишком`startActivity()`начнет новый сеанс. Эта функция автоматически вызывается hello SDK при закрытии приложения.
> 
> 

## <a name="reporting-events"></a>Уведомление о событиях
### <a name="session-events"></a>События сеанса
События сеанса — это обычно используется tooreport hello действия, выполняемые пользователем во время сеанса.

**Пример без дополнительных данных:**

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:nil];
            ...
       }
       [...]
    }

**Пример с дополнительными данными:**

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        NSMutableDictionary* extras = [NSMutableDictionary dictionary];
        [extras setObject:[NSNumber numberWithInt:toInterfaceOrientation] forKey:@"to_orientation_id"];
        [extras setObject:[NSNumber numberWithDouble:duration] forKey:@"duration"];
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:extras];
            ...
       }
       [...]
    }

### <a name="standalone-events"></a>Изолированные события
Противоположные toosession события, события автономный может использоваться за пределами hello контекст сеанса.

**Пример**

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a>Уведомление об ошибках
### <a name="session-errors"></a>Ошибки сеанса
Ошибки сеанса это обычно используется tooreport hello ошибки, влияющие на hello пользователя во время сеанса.

**Пример**

    /** hello user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* hello user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a>Изолированные ошибки
Противоположные toosession ошибки, ошибки автономный может использоваться за пределами hello контекст сеанса.

**Пример**

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a>Уведомление о заданиях
**Пример**

Предположим, что требуется длительность hello tooreport процесс входа в систему:

    [...]
    -(void)signIn
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      [... sign in ...]

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    }
    [...]

### <a name="report-errors-during-a-job"></a>Уведомление об ошибках при выполнении задания
Ошибки могут быть связанные tooa выполнения задания, а связанные с toohello текущий сеанс пользователя.

**Пример**

Предположим, требуется tooreport ошибку во время процесса входа:

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try toosign in */
        NSError* error = nil;
        [self trySigin:&error];
        success = error == nil;

        /* If an error occured report it */
        if(!success)
        {
          [[EngagementAgent shared] sendJobError:@"sign_in_error"
                         jobName:@"sign_in"
                          extras:[NSDictionary dictionaryWithObject:[error localizedDescription] forKey:@"error"]];

          /* Retry after a moment */
          [NSThread sleepForTimeInterval:20];
        }
      }

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    };
    [...]

### <a name="events-during-a-job"></a>События при выполнении задания
События могут быть связанные tooa выполнения задания, а связанные с toohello текущий сеанс пользователя.

**Пример**

Предположим, что у нас есть социальных сетей, мы используем задания tooreport hello общее время во время которого hello пользователь является toohello подключенного сервера. Hello пользователя может получать сообщения от его друзей, это событие задания.

    [...]
    - (void) signin
    {
      [...Sign in code...]
      [[EngagementAgent shared] startJob:@"connection" extras:nil];
    }
    [...]
    - (void) signout
    {
      [...Sign out code...]
      [[EngagementAgent shared] endJob:@"connection"];
    }
    [...]
    - (void) onMessageReceived
    {
      [...Notify user...]
      [[EngagementAgent shared] sendJobEvent:@"connection" jobName:@"message_received" extras:nil];
    }
    [...]

## <a name="extra-parameters"></a>Дополнительные параметры
Произвольные данные могут быть вложенные tooevents, ошибок, действий и заданий.

Эти данные могут быть структурированы. Они используют класс NSDictionary в iOS.

Обратите внимание, что дополнения могут содержать `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` или другие экземпляры `NSDictionary`.

> [!NOTE]
> Hello дополнительный параметр сериализуется в JSON. Toopass различных объектов, чем hello описанных выше моделей, реализуйте следующий метод в классе hello:
> 
> -(NSString*)JSONRepresentation;
> 
> Hello метод должен возвращать JSON-представление объекта.
> 
> 

### <a name="example"></a>Пример
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a>Ограничения
#### <a name="keys"></a>ключей
Каждый ключ в hello `NSDictionary` должно соответствовать hello следующее регулярное выражение:

`^[a-zA-Z][a-zA-Z_0-9]*`

Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).

#### <a name="size"></a>Размер
Дополнения ограничены слишком**1024** символов на вызов (один раз в кодировке JSON агентом Engagement hello).

В hello предыдущего примера hello JSON, отправленных сервером toohello является 58 символов:

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Уведомление о данных приложения
Можно вручную сообщить отслеживания сведения (или любые другие сведения о приложении), с помощью hello `sendAppInfo:` функции.

Обратите внимание, что эти данные могут быть отосланы постепенно: hello только последнее значение для указанного ключа, которые будут храниться для данного устройства.

Как дополнения событий hello `NSDictionary` класса используется tooabstract сведений о приложении, обратите внимание, что массивы или вложенные словарей будет рассматриваться как плоский строки (с помощью сериализации JSON).

**Пример**

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a>Ограничения
#### <a name="keys"></a>ключей
Каждый ключ в hello `NSDictionary` должно соответствовать hello следующее регулярное выражение:

`^[a-zA-Z][a-zA-Z_0-9]*`

Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).

#### <a name="size"></a>Размер
Сведения о приложении ограничены слишком**1024** символов на вызов (один раз в кодировке JSON агентом Engagement hello).

В hello предыдущего примера hello JSON, отправленных сервером toohello является 44 символов:

    {"birthdate":"1983-12-07","gender":"female"}
