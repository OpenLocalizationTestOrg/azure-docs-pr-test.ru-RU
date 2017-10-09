---
title: "hello tooUse aaaHow API Engagement для Android"
description: "Новейшую версию пакета SDK Android - как tooUse hello API Engagement для Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 09b62659-82ae-4a55-8784-fca0b6b22eaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: article
ms.date: 07/25/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e0b2d484616c0c7874e77c5283d94c3063949ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-android"></a>Как tooUse hello API Engagement для Android
Этот документ является документом надстройку toohello [Reporting Дополнительные параметры для Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md). Он предоставляет сведения о как toouse hello Engagement API tooreport статистики вашего приложения.

Имейте в виду, что если требуется только Engagement tooreport приложения сеансы, действия, сбои и технические сведения, затем hello самым простым способом является toomake все вашей `Activity` вложенные классы наследуются от соответствующего hello `EngagementActivity` класса.

Если требуется toodo дополнительные, например, если вам требуется tooreport приложения определенных событий, ошибок и задания или при наличии tooreport действия приложения по-другому, чем один реализованный в hello hello `EngagementActivity` классов, то вы должны toouse hello Engagement API.

Hello Engagement API обеспечивается hello `EngagementAgent` класса. Экземпляр этого класса можно получить путем вызова hello `EngagementAgent.getInstance(Context)` статическим методом (Обратите внимание, что hello `EngagementAgent` возвращаемый объект — единственное значение).

## <a name="engagement-concepts"></a>Основные понятия Engagement
Hello следующие части уточнения hello Общие [Mobile Engagement концепции](mobile-engagement-concepts.md), для платформы Android hello.

### <a name="session-and-activity"></a>`Session` и `Activity`
Если пользователь hello остается несколько секунд простоя между двумя *действия*, затем эта последовательность *действия* разбивается на два отдельных *сеансы*. Эти несколько секунд, называются hello «время ожидания сеанса».

*Действия* обычно связана с одного экрана приложения hello, toosay hello *действия* начинается, когда экран приветствия отображается и останавливается при закрытии экрана приветствия: это hello случай, когда Hello Engagement SDK интегрирован с помощью hello `EngagementActivity` классы.

Но *действия* может также осуществляться вручную с помощью Engagement API hello. Это позволяет toosplit указанными экранными несколько частей tooget sub, Дополнительные сведения о hello использования данного экрана (например tooknown как часто и как долго диалоговые окна используются внутри этот экран).

## <a name="reporting-activities"></a>Уведомление о действиях
> [!IMPORTANT]
> Не требуется tooreport действий, как описано в этом разделе, если вы используете hello `EngagementActivity` класс и его вариантов, как описано в hello как tooIntegrate Engagement для Android документа.
> 
> 

### <a name="user-starts-a-new-activity"></a>Запуск нового действия пользователем
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

Требуется toocall `startActivity()` каждое действие пользователя hello время изменяется. функции Hello первый вызов toothis начинает новый сеанс пользователя.

Здравствуйте, наиболее toocall месте, эта функция используется для каждого действия `onResume` обратного вызова.

### <a name="user-ends-his-current-activity"></a>Завершение текущего действия пользователем
            EngagementAgent.getInstance(this).endActivity();

Требуется toocall `endActivity()` по крайней мере один раз в том случае, когда пользователь hello завершается его последнее действие. Это позволяет сообщить hello Engagement SDK hello пользователя находится в режиме ожидания, что необходимость toobe hello пользовательский сеанс закрыт после hello время ожидания сеанса истекает (Если вы вызываете `startActivity()` до истечения времени ожидания сеанса hello, просто возобновить сеанс hello).

Здравствуйте, наиболее toocall месте, эта функция используется для каждого действия `onPause` обратного вызова.

## <a name="reporting-events"></a>Уведомление о событиях
### <a name="session-events"></a>События сеанса
События сеанса — это обычно используется tooreport hello действия, выполняемые пользователем во время сеанса.

**Пример без дополнительных данных:**

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

**Пример с дополнительными данными:**

            public MyActivity extends EngagementActivity {
              [...]
              @Override
              public boolean onMenuItemSelected(int featureId, MenuItem item) {
                Bundle extras = new Bundle();
                extras.putInt("id", item.getItemId());
                getEngagementAgent().sendSessionEvent("menu_selected", extras);
              }
              [...]
            }

### <a name="standalone-events"></a>Изолированные события
События противоположные toosession автономный события могут происходить за пределами hello контекст сеанса.

**Пример**

Предположим, что требуется tooreport события, происходящие при запуске широковещательных получателя:

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a>Уведомление об ошибках
### <a name="session-errors"></a>Ошибки сеанса
Ошибки сеанса это обычно используется tooreport hello ошибки, влияющие на hello пользователя во время сеанса.

**Пример**

            /** hello user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* hello user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a>Изолированные ошибки
Ошибки противоположные toosession автономный ошибки могут возникать за пределами hello контекст сеанса.

**Пример**

Hello следующем примере показано, как работает tooreport ошибку при нехватке памяти hello на телефоне hello во время процесса приложения.

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a>Уведомление о заданиях
### <a name="example"></a>Пример
Предположим, что требуется длительность hello tooreport процесс входа в систему:

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a>Уведомление об ошибках при выполнении задания
Ошибки могут быть связанные tooa выполнения задания, а связанные с toohello текущий сеанс пользователя.

**Пример**

Предположим, что нужно tooreport Ошибка входа в систему процесс:

[...] public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try toosign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report hello error tooEngagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a>Отчеты о событиях во время выполнения задания
События могут быть связанные tooa выполнения задания, а связанные с toohello текущий сеанс пользователя.

**Пример**

Предположим, что у нас есть социальных сетей, мы используем задания tooreport hello общее время во время которого hello пользователь является toohello подключенного сервера. Hello пользователя может оставаться на связи в фоновом режиме даже в том случае, если он используется другим приложением или при hello телефон находится в спящем режиме, поэтому нет сеанса.

Hello пользователя может получать сообщения от его друзей, это событие задания.

            [...]
            public void signin(Context context, ...) {
              [...Sign in code...]
              EngagementAgent.getInstance(context).startJob("connection", null);
            }
            [...]
            public void signout(Context context) {
              [...Sign out code...]
              EngagementAgent.getInstance(context).endJob("connection");
            }
            [...]
            public void onMessageReceived(Context context) {
              [...Notify in status bar...]
              EngagementAgent.getInstance(context).sendJobEvent("message_received", "connection", null);
            }
            [...]

## <a name="extra-parameters"></a>Дополнительные параметры
Произвольные данные могут быть вложенные tooevents, ошибок, действий и заданий.

Эти данные могут быть структурированы, здесь используется класс пакета Android (на самом деле он работает в качестве дополнительных параметров в целях Android). Обратите внимание, что пакет может содержать массивы или экземпляры другого пакета.

> [!IMPORTANT]
> Если поместить в параметрах parcelable или serializable, убедитесь, что их `toString()` метод является реализовано tooreturn читаемую пользователем строку. Сериализуемые классы, содержащие непереходные поля, которые не сериализуются, приведут к сбою Android при вызове `bundle.putSerializable("key",value);`
> 
> [!WARNING]
> Разреженные массивы в дополнительных параметрах не поддерживаются, то есть не сериализуется как массив. Их следует преобразовать в стандартные массивы перед использованием в дополнительных параметрах.
> 
> 

### <a name="example"></a>Пример
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a>Ограничения
#### <a name="keys"></a>ключей
Каждый ключ в hello `Bundle` должно соответствовать hello следующее регулярное выражение:

`^[a-zA-Z][a-zA-Z_0-9]*`

Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).

#### <a name="size"></a>Размер
Дополнения ограничены слишком**1024** символов на вызов (один раз в кодировке JSON службой Engagement hello).

В hello предыдущего примера hello JSON, отправленных сервером toohello является 58 символов:

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Уведомление о данных приложения
Можно вручную сообщить отслеживания сведения (или любые другие сведения о приложении), с помощью hello `sendAppInfo()` функции.

Обратите внимание, что эти данные могут быть отосланы постепенно: hello только последнее значение для указанного ключа, которые будут храниться для данного устройства.

Как дополнения событий hello класса набора сведений о приложении используется tooabstract, обратите внимание, что массивы или вложенным объединяет будет рассматриваться как плоский строки (с помощью сериализации JSON).

### <a name="example"></a>Пример
Ниже приведен Пол пользователя toosend образец кода и birthdate.

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a>Ограничения
#### <a name="keys"></a>ключей
Каждый ключ в hello `Bundle` должно соответствовать hello следующее регулярное выражение:

`^[a-zA-Z][a-zA-Z_0-9]*`

Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).

#### <a name="size"></a>Размер
Сведения о приложении ограничены слишком**1024** символов на вызов (один раз в кодировке JSON службой Engagement hello).

В hello предыдущего примера hello JSON, отправленных сервером toohello является 44 символов:

            {"expiration":"2016-12-07","status":"premium"}
