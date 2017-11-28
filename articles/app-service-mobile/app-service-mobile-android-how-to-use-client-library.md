---
title: "aaaHow toouse hello Azure мобильных приложений и пакет SDK для Android | Документы Microsoft"
description: "Как toouse hello пакет SDK Azure Mobile приложений для Android"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: glenga
ms.openlocfilehash: 56eb73c4e1703d69877be499a09fc2130f1d68e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="bc89a-103">Как toouse hello пакет SDK Azure Mobile приложений для Android</span><span class="sxs-lookup"><span data-stu-id="bc89a-103">How toouse hello Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="bc89a-104">В этом руководстве показано, как toouse hello Android пакет SDK для клиента в распространенных сценариях tooimplement мобильные приложения, такие как:</span><span class="sxs-lookup"><span data-stu-id="bc89a-104">This guide shows you how toouse hello Android client SDK for Mobile Apps tooimplement common scenarios, such as:</span></span>

* <span data-ttu-id="bc89a-105">запрос данных (вставка, обновление и удаления);</span><span class="sxs-lookup"><span data-stu-id="bc89a-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="bc89a-106">аутентификация;</span><span class="sxs-lookup"><span data-stu-id="bc89a-106">Authentication.</span></span>
* <span data-ttu-id="bc89a-107">обработка ошибок;</span><span class="sxs-lookup"><span data-stu-id="bc89a-107">Handling errors.</span></span>
* <span data-ttu-id="bc89a-108">Настройка клиента hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-108">Customizing hello client.</span></span>

<span data-ttu-id="bc89a-109">Это руководство посвящено hello клиентского пакета SDK для Android.</span><span class="sxs-lookup"><span data-stu-id="bc89a-109">This guide focuses on hello client-side Android SDK.</span></span>  <span data-ttu-id="bc89a-110">toolearn Подробнее о hello серверные пакеты SDK для мобильных приложений см. в разделе [работать с серверной части .NET SDK] [ 10] или [как toouse hello серверной Node.js SDK] [ 11].</span><span class="sxs-lookup"><span data-stu-id="bc89a-110">toolearn more about hello server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How toouse hello Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="bc89a-111">Справочная документация</span><span class="sxs-lookup"><span data-stu-id="bc89a-111">Reference Documentation</span></span>

<span data-ttu-id="bc89a-112">Можно найти hello [Справочник по Javadocs API] [ 12] для hello Android клиентской библиотеки на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="bc89a-112">You can find hello [Javadocs API reference][12] for hello Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="bc89a-113">Поддерживаемые платформы</span><span class="sxs-lookup"><span data-stu-id="bc89a-113">Supported Platforms</span></span>

<span data-ttu-id="bc89a-114">Hello Azure мобильных приложений и пакет SDK для Android поддерживает уровни API 19 до 24 (KitKat через Nougat) для телефонов и планшетных ПК форм-факторов.</span><span class="sxs-lookup"><span data-stu-id="bc89a-114">hello Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="bc89a-115">Проверка подлинности, в частности, использует общий подход framework web toogather учетные данные.</span><span class="sxs-lookup"><span data-stu-id="bc89a-115">Authentication, in particular, utilizes a common web framework approach toogather credentials.</span></span>  <span data-ttu-id="bc89a-116">Серверный поток проверки подлинности не работает на устройствах малого форм-фактора, таких как часы.</span><span class="sxs-lookup"><span data-stu-id="bc89a-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="bc89a-117">Настройка и необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="bc89a-117">Setup and Prerequisites</span></span>

<span data-ttu-id="bc89a-118">Полный hello [краткое руководство мобильные приложения](app-service-mobile-android-get-started.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="bc89a-118">Complete hello [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="bc89a-119">Выполнение данной задачи гарантирует, что будут соблюдены все предварительные требования для разработки мобильных приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="bc89a-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="bc89a-120">также Hello краткое руководство поможет вам настроить учетную запись и создать первый серверной части мобильное приложение.</span><span class="sxs-lookup"><span data-stu-id="bc89a-120">hello Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="bc89a-121">Если вы решите не toocomplete hello краткого руководства, выполните следующие задачи hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-121">If you decide not toocomplete hello Quickstart tutorial, complete hello following tasks:</span></span>

* <span data-ttu-id="bc89a-122">[Создание серверной части мобильное приложение] [ 13] toouse вместе с приложением Android.</span><span class="sxs-lookup"><span data-stu-id="bc89a-122">[create a Mobile App backend][13] toouse with your Android app.</span></span>
* <span data-ttu-id="bc89a-123">В Android Studio [файлы сборки hello обновления Gradle](#gradle-build).</span><span class="sxs-lookup"><span data-stu-id="bc89a-123">In Android Studio, [update hello Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="bc89a-124">[Включение разрешение INTERNET](#enable-internet).</span><span class="sxs-lookup"><span data-stu-id="bc89a-124">[Enable internet permission](#enable-internet).</span></span>

### <span data-ttu-id="bc89a-125"><a name="gradle-build"></a>Обновить файл сборки Gradle hello</span><span class="sxs-lookup"><span data-stu-id="bc89a-125"><a name="gradle-build"></a>Update hello Gradle build file</span></span>

<span data-ttu-id="bc89a-126">Измените оба файла **build.gradle** :</span><span class="sxs-lookup"><span data-stu-id="bc89a-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="bc89a-127">Добавьте этот код toohello *проекта* уровень **build.gradle** файла внутри hello *buildscript* тег:</span><span class="sxs-lookup"><span data-stu-id="bc89a-127">Add this code toohello *Project* level **build.gradle** file inside hello *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="bc89a-128">Добавьте этот код toohello *модуль приложения* уровень **build.gradle** файла внутри hello *зависимости* тег:</span><span class="sxs-lookup"><span data-stu-id="bc89a-128">Add this code toohello *Module app* level **build.gradle** file inside hello *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    <span data-ttu-id="bc89a-129">В настоящее время hello последняя версия — 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="bc89a-129">Currently hello latest version is 3.3.0.</span></span> <span data-ttu-id="bc89a-130">Hello поддерживаемые версии перечислены [на bintray][14].</span><span class="sxs-lookup"><span data-stu-id="bc89a-130">hello supported versions are listed [on bintray][14].</span></span>

### <span data-ttu-id="bc89a-131"><a name="enable-internet"></a>Включение разрешения INTERNET</span><span class="sxs-lookup"><span data-stu-id="bc89a-131"><a name="enable-internet"></a>Enable internet permission</span></span>

<span data-ttu-id="bc89a-132">tooaccess Azure приложения необходимо разрешение hello Интернет включено.</span><span class="sxs-lookup"><span data-stu-id="bc89a-132">tooaccess Azure, your app must have hello INTERNET permission enabled.</span></span> <span data-ttu-id="bc89a-133">Если он еще не включен, добавить hello, следующей строкой кода tooyour **AndroidManifest.xml** файла:</span><span class="sxs-lookup"><span data-stu-id="bc89a-133">If it's not already enabled, add hello following line of code tooyour **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="bc89a-134">Создание подключения клиента</span><span class="sxs-lookup"><span data-stu-id="bc89a-134">Create a Client Connection</span></span>

<span data-ttu-id="bc89a-135">Мобильные приложения Azure предоставляет четыре функции tooyour мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="bc89a-135">Azure Mobile Apps provides four functions tooyour mobile application:</span></span>

* <span data-ttu-id="bc89a-136">доступ к данным и их синхронизация в автономном режиме со службой мобильных приложений Azure;</span><span class="sxs-lookup"><span data-stu-id="bc89a-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="bc89a-137">Вызов пользовательского API, написанную hello пакет SDK для приложений мобильных сервера Azure.</span><span class="sxs-lookup"><span data-stu-id="bc89a-137">Call Custom APIs written with hello Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="bc89a-138">проверка подлинности с помощью функции проверки подлинности и авторизации в службе приложений Azure;</span><span class="sxs-lookup"><span data-stu-id="bc89a-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="bc89a-139">регистрация push-уведомлений в Центрах уведомлений.</span><span class="sxs-lookup"><span data-stu-id="bc89a-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="bc89a-140">Чтобы использовать каждую из этих функций, сначала необходимо создать объект `MobileServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="bc89a-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="bc89a-141">В мобильном клиенте необходимо создать только один объект `MobileServiceClient` (то есть следует использовать шаблон с одним элементом).</span><span class="sxs-lookup"><span data-stu-id="bc89a-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="bc89a-142">toocreate `MobileServiceClient` объекта:</span><span class="sxs-lookup"><span data-stu-id="bc89a-142">toocreate a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

<span data-ttu-id="bc89a-143">Hello `<MobileAppUrl>` — строка или объект URL-адрес, который указывает tooyour мобильной серверной части.</span><span class="sxs-lookup"><span data-stu-id="bc89a-143">hello `<MobileAppUrl>` is either a string or a URL object that points tooyour mobile backend.</span></span>  <span data-ttu-id="bc89a-144">При использовании службы приложений Azure toohost серверной части мобильных устройств, затем используйте безопасный hello `https://` версии hello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="bc89a-144">If you are using Azure App Service toohost your mobile backend, then ensure you use hello secure `https://` version of hello URL.</span></span>

<span data-ttu-id="bc89a-145">Hello клиента также требуется доступ toohello действия или контексте - hello `this` параметр в примере hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-145">hello client also requires access toohello Activity or Context - hello `this` parameter in hello example.</span></span>  <span data-ttu-id="bc89a-146">Hello построения MobileServiceClient должны быть выполнены в рамках hello `onCreate()` метод hello, на которые ссылается действие hello `AndroidManifest.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="bc89a-146">hello MobileServiceClient construction should happen within hello `onCreate()` method of hello Activity referenced in hello `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="bc89a-147">Мы советуем абстрагировать связь сервера в собственный класс (шаблон с одним элементом).</span><span class="sxs-lookup"><span data-stu-id="bc89a-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="bc89a-148">В этом случае следует передавать hello действия в конструктор tooappropriately hello настроить службу hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-148">In this case, you should pass hello Activity within hello constructor tooappropriately configure hello service.</span></span>  <span data-ttu-id="bc89a-149">Например:</span><span class="sxs-lookup"><span data-stu-id="bc89a-149">For example:</span></span>

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

<span data-ttu-id="bc89a-150">Теперь можно вызвать `AzureServiceAdapter.Initialize(this);` в hello `onCreate()` метод основных действия.</span><span class="sxs-lookup"><span data-stu-id="bc89a-150">You can now call `AzureServiceAdapter.Initialize(this);` in hello `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="bc89a-151">Использовать другие методы, создающие toohello клиента `AzureServiceAdapter.getInstance();` tooobtain адаптер службы toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="bc89a-151">Any other methods needing access toohello client use `AzureServiceAdapter.getInstance();` tooobtain a reference toohello service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="bc89a-152">Операции с данными</span><span class="sxs-lookup"><span data-stu-id="bc89a-152">Data Operations</span></span>

<span data-ttu-id="bc89a-153">Hello hello пакет SDK Azure Mobile приложений лежит toodata tooprovide доступ, хранящихся в SQL Azure серверную часть мобильное приложение hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-153">hello core of hello Azure Mobile Apps SDK is tooprovide access toodata stored within SQL Azure on hello Mobile App backend.</span></span>  <span data-ttu-id="bc89a-154">Доступ к этим данным можно получить, используя классы со строгим типом (предпочтительный способ) или нетипизированные запросы (нерекомендуемый способ).</span><span class="sxs-lookup"><span data-stu-id="bc89a-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="bc89a-155">Hello большая часть в этом разделе рассматриваются использование строго типизированных классов.</span><span class="sxs-lookup"><span data-stu-id="bc89a-155">hello bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="bc89a-156">Определение клиентских классов данных</span><span class="sxs-lookup"><span data-stu-id="bc89a-156">Define client data classes</span></span>

<span data-ttu-id="bc89a-157">tooaccess данные из таблиц SQL Azure, определяют клиентские классы данных, соответствующих таблиц toohello в серверном мобильное приложение hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-157">tooaccess data from SQL Azure tables, define client data classes that correspond toohello tables in hello Mobile App backend.</span></span> <span data-ttu-id="bc89a-158">Примеры в этом разделе предполагается, таблица с именем **MyDataTable**, который имеет hello следующие столбцы:</span><span class="sxs-lookup"><span data-stu-id="bc89a-158">Examples in this topic assume a table named **MyDataTable**, which has hello following columns:</span></span>

* <span data-ttu-id="bc89a-159">id</span><span class="sxs-lookup"><span data-stu-id="bc89a-159">id</span></span>
* <span data-ttu-id="bc89a-160">текст</span><span class="sxs-lookup"><span data-stu-id="bc89a-160">text</span></span>
* <span data-ttu-id="bc89a-161">complete</span><span class="sxs-lookup"><span data-stu-id="bc89a-161">complete</span></span>

<span data-ttu-id="bc89a-162">Hello соответствующий типизированный клиентский объект находится в файле с именем **MyDataTable.java**:</span><span class="sxs-lookup"><span data-stu-id="bc89a-162">hello corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="bc89a-163">Включите методы Getter или Setter в каждое добавленное поле.</span><span class="sxs-lookup"><span data-stu-id="bc89a-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="bc89a-164">Если таблица SQL Azure содержит больше столбцов, необходимо добавить hello соответствующего поля toothis класса.</span><span class="sxs-lookup"><span data-stu-id="bc89a-164">If your SQL Azure table contains more columns, you would add hello corresponding fields toothis class.</span></span>  <span data-ttu-id="bc89a-165">Например, если hello DTO (объект передачи данных) имеет приоритет целочисленном столбце, то можно добавить это поле, а также его методы get и set:</span><span class="sxs-lookup"><span data-stu-id="bc89a-165">For example, if hello DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

```java
private Integer priority;

/**
* Returns hello item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets hello item priority
*
* @param priority
*            priority tooset
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

<span data-ttu-id="bc89a-166">toolearn toocreate дополнительных таблиц в серверной части мобильных приложений, в статье [как: определить табличный контроллер] [ 15] (серверное приложение .NET) или [определения таблиц, с помощью динамической схемы] [ 16] (Серверное приложение Node.js).</span><span class="sxs-lookup"><span data-stu-id="bc89a-166">toolearn how toocreate additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="bc89a-167">Таблицу серверной части мобильных приложений Azure определяет пять специальные поля, четыре из которых будут доступны tooclients:</span><span class="sxs-lookup"><span data-stu-id="bc89a-167">An Azure Mobile Apps backend table defines five special fields, four of which are available tooclients:</span></span>

* <span data-ttu-id="bc89a-168">`String id`: hello глобальный уникальный идентификатор записи hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-168">`String id`: hello globally unique ID for hello record.</span></span>  <span data-ttu-id="bc89a-169">Как рекомендуется сделать hello идентификатор hello строковое представление [UUID] [ 17] объекта.</span><span class="sxs-lookup"><span data-stu-id="bc89a-169">As a best practice, make hello id hello String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="bc89a-170">`DateTimeOffset updatedAt`: hello Дата и время последнего обновления hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-170">`DateTimeOffset updatedAt`: hello date/time of hello last update.</span></span>  <span data-ttu-id="bc89a-171">поле updatedAt Hello задается сервером hello и никогда не должно задаваться в клиентской программе.</span><span class="sxs-lookup"><span data-stu-id="bc89a-171">hello updatedAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="bc89a-172">`DateTimeOffset createdAt`: hello даты и времени создания этого hello объекта.</span><span class="sxs-lookup"><span data-stu-id="bc89a-172">`DateTimeOffset createdAt`: hello date/time that hello object was created.</span></span>  <span data-ttu-id="bc89a-173">поле createdAt Hello задается сервером hello и никогда не должно задаваться в клиентской программе.</span><span class="sxs-lookup"><span data-stu-id="bc89a-173">hello createdAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="bc89a-174">`byte[] version`: Обычно представлено в виде строки, версия hello также устанавливается сервером hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-174">`byte[] version`: Normally represented as a string, hello version is also set by hello server.</span></span>
* <span data-ttu-id="bc89a-175">`boolean deleted`: Указывает, что запись hello был удален, но еще не очищаются.</span><span class="sxs-lookup"><span data-stu-id="bc89a-175">`boolean deleted`: Indicates that hello record has been deleted but not purged yet.</span></span>  <span data-ttu-id="bc89a-176">Не используйте `deleted` в качестве свойства класса.</span><span class="sxs-lookup"><span data-stu-id="bc89a-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="bc89a-177">Hello `id` поле является обязательным.</span><span class="sxs-lookup"><span data-stu-id="bc89a-177">hello `id` field is required.</span></span>  <span data-ttu-id="bc89a-178">Hello `updatedAt` поля и `version` поля используются для синхронизации в автономном режиме (для добавочной синхронизации и вступают в конфликт разрешения соответственно).</span><span class="sxs-lookup"><span data-stu-id="bc89a-178">hello `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="bc89a-179">Hello `createdAt` поле поле ссылки и не используется клиентом hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-179">hello `createdAt` field is a reference field and is not used by hello client.</span></span>  <span data-ttu-id="bc89a-180">имена Hello «на лету» имена свойств hello и не являются изменяемыми.</span><span class="sxs-lookup"><span data-stu-id="bc89a-180">hello names are "across-the-wire" names of hello properties and are not adjustable.</span></span>  <span data-ttu-id="bc89a-181">Тем не менее, можно создать сопоставление между объектом и hello имена «на лету», используя hello [gson] [ 3] библиотеки.</span><span class="sxs-lookup"><span data-stu-id="bc89a-181">However, you can create a mapping between your object and hello "across-the-wire" names using hello [gson][3] library.</span></span>  <span data-ttu-id="bc89a-182">Например:</span><span class="sxs-lookup"><span data-stu-id="bc89a-182">For example:</span></span>

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getUpdatedAt() { return mCreatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getText() { return mVersion; }
    public final void setText(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a><span data-ttu-id="bc89a-183">Создание ссылки на таблицу</span><span class="sxs-lookup"><span data-stu-id="bc89a-183">Create a Table Reference</span></span>

<span data-ttu-id="bc89a-184">tooaccess таблицы, сначала создайте [MobileServiceTable] [ 8] объект, вызывающий hello **getTable** метод hello [MobileServiceClient][9].</span><span class="sxs-lookup"><span data-stu-id="bc89a-184">tooaccess a table, first create a [MobileServiceTable][8] object by calling hello **getTable** method on hello [MobileServiceClient][9].</span></span>  <span data-ttu-id="bc89a-185">У этого метода две перегрузки.</span><span class="sxs-lookup"><span data-stu-id="bc89a-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="bc89a-186">В следующий код, hello **метод mClient** является объектом ссылки tooyour MobileServiceClient.</span><span class="sxs-lookup"><span data-stu-id="bc89a-186">In hello following code, **mClient** is a reference tooyour MobileServiceClient object.</span></span>  <span data-ttu-id="bc89a-187">первая перегрузка Hello используется где hello указаны имена класса и имя таблицы hello же Здравствуйте, и hello один служит hello краткое руководство:</span><span class="sxs-lookup"><span data-stu-id="bc89a-187">hello first overload is used where hello class name and hello table name are hello same, and is hello one used in hello Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="bc89a-188">Hello вторая перегрузка используется, когда имя таблицы hello отличается от имени класса hello: hello первым параметром является имя таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-188">hello second overload is used when hello table name is different from hello class name: hello first parameter is hello table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <span data-ttu-id="bc89a-189"><a name="query"></a>Запрос таблицы серверной части</span><span class="sxs-lookup"><span data-stu-id="bc89a-189"><a name="query"></a>Query a Backend Table</span></span>

<span data-ttu-id="bc89a-190">Сначала получите ссылку на таблицу.</span><span class="sxs-lookup"><span data-stu-id="bc89a-190">First, obtain a table reference.</span></span>  <span data-ttu-id="bc89a-191">Выполните запрос на ссылку на таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-191">Then execute a query on hello table reference.</span></span>  <span data-ttu-id="bc89a-192">Запрос сочетает в себе следующее:</span><span class="sxs-lookup"><span data-stu-id="bc89a-192">A query is any combination of:</span></span>

* <span data-ttu-id="bc89a-193">[предложение фильтра](#filtering) `.where()`;</span><span class="sxs-lookup"><span data-stu-id="bc89a-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="bc89a-194">[предложение упорядочения](#sorting) `.orderBy()`;</span><span class="sxs-lookup"><span data-stu-id="bc89a-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="bc89a-195">[предложение выбора поля](#selection) `.select()`;</span><span class="sxs-lookup"><span data-stu-id="bc89a-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="bc89a-196">`.skip()` и `.top()` для [страничных результатов](#paging).</span><span class="sxs-lookup"><span data-stu-id="bc89a-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="bc89a-197">Hello предложений должны быть представлены на предшествующий порядок hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-197">hello clauses must be presented in hello preceding order.</span></span>

### <span data-ttu-id="bc89a-198"><a name="filter"></a> Фильтрация результатов</span><span class="sxs-lookup"><span data-stu-id="bc89a-198"><a name="filter"></a> Filtering Results</span></span>

<span data-ttu-id="bc89a-199">Hello запроса выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bc89a-199">hello general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

<span data-ttu-id="bc89a-200">Hello выше пример возвращает все результаты (вверх toohello максимальный размер страницы задается hello сервера).</span><span class="sxs-lookup"><span data-stu-id="bc89a-200">hello preceding example returns all results (up toohello maximum page size set by hello server).</span></span>  <span data-ttu-id="bc89a-201">Hello `.execute()` метод выполняет запрос hello hello серверную часть.</span><span class="sxs-lookup"><span data-stu-id="bc89a-201">hello `.execute()` method executes hello query on hello backend.</span></span>  <span data-ttu-id="bc89a-202">Hello запрос является преобразованный tooan [OData v3] [ 19] запрос перед серверной части мобильных приложений toohello передачи.</span><span class="sxs-lookup"><span data-stu-id="bc89a-202">hello query is converted tooan [OData v3][19] query before transmission toohello Mobile Apps backend.</span></span>  <span data-ttu-id="bc89a-203">По получении серверной мобильные приложения hello преобразует hello запроса в инструкцию SQL перед его выполнением на экземпляр SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-203">On receipt, hello Mobile Apps backend converts hello query into an SQL statement before executing it on hello SQL Azure instance.</span></span>  <span data-ttu-id="bc89a-204">Здравствуйте, так как сетевой активности занимает некоторое время, `.execute()` возвращает [ `ListenableFuture<E>` ] [ 18].</span><span class="sxs-lookup"><span data-stu-id="bc89a-204">Since network activity takes some time, hello `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <span data-ttu-id="bc89a-205"><a name="filtering"></a>Фильтрация возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="bc89a-205"><a name="filtering"></a>Filter returned data</span></span>

<span data-ttu-id="bc89a-206">Привет, после выполнения запроса возвращает все элементы из hello **ToDoItem** таблицу, куда **завершения** равняется **false**.</span><span class="sxs-lookup"><span data-stu-id="bc89a-206">hello following query execution returns all items from hello **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="bc89a-207">**mToDoTable** таблицы мобильной службы toohello ссылка hello, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="bc89a-207">**mToDoTable** is hello reference toohello mobile service table that we created previously.</span></span>

<span data-ttu-id="bc89a-208">Определение фильтра с помощью hello **где** вызова метода в ссылку на таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-208">Define a filter using hello **where** method call on hello table reference.</span></span> <span data-ttu-id="bc89a-209">Hello **где** следуют метод **поле** метод следуют метод, который определяет логический предикат hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-209">hello **where** method is followed by a **field** method followed by a method that specifies hello logical predicate.</span></span> <span data-ttu-id="bc89a-210">Возможные методы предиката: **eq** (равно), **ne** (не равно), **gt** (больше), **ge** (больше или равно), **lt** (меньше), **le** (меньше или равно).</span><span class="sxs-lookup"><span data-stu-id="bc89a-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="bc89a-211">Эти методы позволяют сравнивать число и строку поля toospecific значения.</span><span class="sxs-lookup"><span data-stu-id="bc89a-211">These methods let you compare number and string fields toospecific values.</span></span>

<span data-ttu-id="bc89a-212">Фильтровать данные можно по датам.</span><span class="sxs-lookup"><span data-stu-id="bc89a-212">You can filter on dates.</span></span> <span data-ttu-id="bc89a-213">Hello следующие методы позволяют сравнивать hello дату полю или частей даты hello: **года**, **месяц**, **день**, **час**, **минуту**, и **второй**.</span><span class="sxs-lookup"><span data-stu-id="bc89a-213">hello following methods let you compare hello entire date field or parts of hello date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="bc89a-214">Hello пример добавления фильтра для элементов которого *срок* равно 2013.</span><span class="sxs-lookup"><span data-stu-id="bc89a-214">hello following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="bc89a-215">Hello следующие методы поддерживают сложные фильтры для полей строки: **startsWith**, **endsWith**, **concat**, **подстроки**, **indexOf**, **заменить**, **toLower**, **toUpper**, **trim**, и  **Длина**.</span><span class="sxs-lookup"><span data-stu-id="bc89a-215">hello following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="bc89a-216">Следующий пример фильтры для строки таблицы, где hello Hello *текст* столбцов начинается с «PRI0».</span><span class="sxs-lookup"><span data-stu-id="bc89a-216">hello following example filters for table rows where hello *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="bc89a-217">поддерживаются следующие методы операторов Hello числовых полей: **добавить**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, и **округления**.</span><span class="sxs-lookup"><span data-stu-id="bc89a-217">hello following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="bc89a-218">Следующий пример фильтры для строки таблицы, где hello Hello **длительность** является четным числом.</span><span class="sxs-lookup"><span data-stu-id="bc89a-218">hello following example filters for table rows where hello **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="bc89a-219">Предикаты можно объединять с помощью логических методов **and**, **or** и **not**.</span><span class="sxs-lookup"><span data-stu-id="bc89a-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="bc89a-220">Следующий пример Hello объединяет два предыдущих примерах hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-220">hello following example combines two of hello preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="bc89a-221">Группирование и вложение логических операторов.</span><span class="sxs-lookup"><span data-stu-id="bc89a-221">Group and nest logical operators:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

<span data-ttu-id="bc89a-222">Более подробные сведения и примеры фильтрации см. в разделе [изучение набора операторов hello hello Android клиентского запроса модели][20].</span><span class="sxs-lookup"><span data-stu-id="bc89a-222">For more detailed discussion and examples of filtering, see [Exploring hello richness of hello Android client query model][20].</span></span>

### <span data-ttu-id="bc89a-223"><a name="sorting"></a>Сортировка возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="bc89a-223"><a name="sorting"></a>Sort returned data</span></span>

<span data-ttu-id="bc89a-224">Hello следующий код возвращает все элементы из таблицы **ToDoItems** сортируются по возрастанию по hello *текст* поля.</span><span class="sxs-lookup"><span data-stu-id="bc89a-224">hello following code returns all items from a table of **ToDoItems** sorted ascending by hello *text* field.</span></span> <span data-ttu-id="bc89a-225">*mToDoTable* — hello toohello ссылочной серверной части таблицы, созданной ранее:</span><span class="sxs-lookup"><span data-stu-id="bc89a-225">*mToDoTable* is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="bc89a-226">Здравствуйте, первый параметр hello **orderBy** метода является именем равно toohello строку hello поля на какие toosort.</span><span class="sxs-lookup"><span data-stu-id="bc89a-226">hello first parameter of hello **orderBy** method is a string equal toohello name of hello field on which toosort.</span></span> <span data-ttu-id="bc89a-227">Второй параметр Hello использует hello **QueryOrder** toospecify перечисления ли toosort по возрастанию или убыванию.</span><span class="sxs-lookup"><span data-stu-id="bc89a-227">hello second parameter uses hello **QueryOrder** enumeration toospecify whether toosort ascending or descending.</span></span>  <span data-ttu-id="bc89a-228">Если фильтруется с использованием hello ***где*** метод, hello ***где*** метод должен вызываться перед hello ***orderBy*** метод.</span><span class="sxs-lookup"><span data-stu-id="bc89a-228">If you are filtering using hello ***where*** method, hello ***where*** method must be invoked before hello ***orderBy*** method.</span></span>

### <span data-ttu-id="bc89a-229"><a name="selection"></a>Выбор определенных столбцов</span><span class="sxs-lookup"><span data-stu-id="bc89a-229"><a name="selection"></a>Select specific columns</span></span>

<span data-ttu-id="bc89a-230">Hello следующий код показывает, как tooreturn все элементы из таблицы **ToDoItems**, но отображает только hello **завершения** и **текст** поля.</span><span class="sxs-lookup"><span data-stu-id="bc89a-230">hello following code illustrates how tooreturn all items from a table of **ToDoItems**, but only displays hello **complete** and **text** fields.</span></span> <span data-ttu-id="bc89a-231">**mToDoTable** hello toohello Справочник по серверной части таблицы, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="bc89a-231">**mToDoTable** is hello reference toohello backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="bc89a-232">Выберите функции Hello параметры toohello — имена строку hello hello таблицы столбцы, которые должны tooreturn.</span><span class="sxs-lookup"><span data-stu-id="bc89a-232">hello parameters toohello select function are hello string names of hello table's columns that you want tooreturn.</span></span>  <span data-ttu-id="bc89a-233">Hello **выберите** метод должен toofollow методы, такие как **где** и **orderBy**.</span><span class="sxs-lookup"><span data-stu-id="bc89a-233">hello **select** method needs toofollow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="bc89a-234">Затем можно вызывать такие методы разбивки на страницы, как **skip** и **top**.</span><span class="sxs-lookup"><span data-stu-id="bc89a-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <span data-ttu-id="bc89a-235"><a name="paging"></a>Возврат данных на страницах</span><span class="sxs-lookup"><span data-stu-id="bc89a-235"><a name="paging"></a>Return data in pages</span></span>

<span data-ttu-id="bc89a-236">Данные **всегда** возвращаются на страницах.</span><span class="sxs-lookup"><span data-stu-id="bc89a-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="bc89a-237">Максимальное число возвращаемых записей Hello устанавливается сервером hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-237">hello maximum number of records returned is set by hello server.</span></span>  <span data-ttu-id="bc89a-238">Если клиент hello запрашивает несколько записей, hello server возвращает hello максимальное число записей.</span><span class="sxs-lookup"><span data-stu-id="bc89a-238">If hello client requests more records, then hello server returns hello maximum number of records.</span></span>  <span data-ttu-id="bc89a-239">По умолчанию hello максимальный размер страницы на сервере hello используется значение 50 записей.</span><span class="sxs-lookup"><span data-stu-id="bc89a-239">By default, hello maximum page size on hello server is 50 records.</span></span>

<span data-ttu-id="bc89a-240">Hello в первом примере показано, как tooselect hello первые пять элементы из таблицы.</span><span class="sxs-lookup"><span data-stu-id="bc89a-240">hello first example shows how tooselect hello top five items from a table.</span></span> <span data-ttu-id="bc89a-241">Hello запрос возвращает hello элементов из таблицы **ToDoItems**.</span><span class="sxs-lookup"><span data-stu-id="bc89a-241">hello query returns hello items from a table of **ToDoItems**.</span></span> <span data-ttu-id="bc89a-242">**mToDoTable** — hello toohello ссылочной серверной части таблицы, созданной ранее:</span><span class="sxs-lookup"><span data-stu-id="bc89a-242">**mToDoTable** is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="bc89a-243">Вот запрос пропускает hello первые пять элементов, которое затем возвращает hello пяти далее:</span><span class="sxs-lookup"><span data-stu-id="bc89a-243">Here's a query that skips hello first five items, and then returns hello next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="bc89a-244">При желании tooget все записи в таблице, реализуют tooiterate кода всех страниц:</span><span class="sxs-lookup"><span data-stu-id="bc89a-244">If you wish tooget all records in a table, implement code tooiterate over all pages:</span></span>

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

<span data-ttu-id="bc89a-245">Запрос для всех записей с помощью этого метода создает как минимум два запроса toohello мобильные приложения, базы данных.</span><span class="sxs-lookup"><span data-stu-id="bc89a-245">A request for all records using this method creates a minimum of two requests toohello Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="bc89a-246">Выбор размера правая страница hello — компромисс между использования памяти во время выполняется запрос hello, пропускная способность и задержка при получении данных hello полностью.</span><span class="sxs-lookup"><span data-stu-id="bc89a-246">Choosing hello right page size is a balance between memory usage while hello request is happening, bandwidth usage and delay in receiving hello data completely.</span></span>  <span data-ttu-id="bc89a-247">по умолчанию Hello (50 записей) подходит для всех устройств.</span><span class="sxs-lookup"><span data-stu-id="bc89a-247">hello default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="bc89a-248">При эксплуатации исключительно на устройствах больше памяти, увеличьте вверх too500.</span><span class="sxs-lookup"><span data-stu-id="bc89a-248">If you exclusively operate on larger memory devices, increase up too500.</span></span>  <span data-ttu-id="bc89a-249">Обнаружено, увеличивающий размер страницы приветствия за пределами 500 записей результатов в неприемлемо задержки или проблемы большого объема памяти.</span><span class="sxs-lookup"><span data-stu-id="bc89a-249">We have found that increasing hello page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <span data-ttu-id="bc89a-250"><a name="chaining"></a>Практическое руководство. Объединение методов запросов</span><span class="sxs-lookup"><span data-stu-id="bc89a-250"><a name="chaining"></a>How to: Concatenate query methods</span></span>

<span data-ttu-id="bc89a-251">Hello методы, используемые в запросах к таблицам базы данных могут быть объединены.</span><span class="sxs-lookup"><span data-stu-id="bc89a-251">hello methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="bc89a-252">Цепочки запросов, методы позволяет tooselect определенными столбцами отфильтрованные строки, которые сортируются и разбиением на страницы.</span><span class="sxs-lookup"><span data-stu-id="bc89a-252">Chaining query methods allows you tooselect specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="bc89a-253">Можно создавать сложные логические фильтры.</span><span class="sxs-lookup"><span data-stu-id="bc89a-253">You can create complex logical filters.</span></span>  <span data-ttu-id="bc89a-254">Каждый метод запроса возвращает объект Query.</span><span class="sxs-lookup"><span data-stu-id="bc89a-254">Each query method returns a Query object.</span></span> <span data-ttu-id="bc89a-255">tooend hello ряд методов и hello фактического выполнения запроса, вызов hello **выполнение** метод.</span><span class="sxs-lookup"><span data-stu-id="bc89a-255">tooend hello series of methods and actually run hello query, call hello **execute** method.</span></span> <span data-ttu-id="bc89a-256">Например:</span><span class="sxs-lookup"><span data-stu-id="bc89a-256">For example:</span></span>

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

<span data-ttu-id="bc89a-257">Hello связанных данных запроса, который методы должны быть упорядочены следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bc89a-257">hello chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="bc89a-258">методы фильтрации (**где**);</span><span class="sxs-lookup"><span data-stu-id="bc89a-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="bc89a-259">методы сортировки (**orderBy**);</span><span class="sxs-lookup"><span data-stu-id="bc89a-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="bc89a-260">методы выборки (**выберите**);</span><span class="sxs-lookup"><span data-stu-id="bc89a-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="bc89a-261">методы разбиения по страницам (**skip** и **top**).</span><span class="sxs-lookup"><span data-stu-id="bc89a-261">paging (**skip** and **top**) methods.</span></span>

## <span data-ttu-id="bc89a-262"><a name="binding"></a>Привязка данных toohello пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="bc89a-262"><a name="binding"></a>Bind data toohello user interface</span></span>

<span data-ttu-id="bc89a-263">Привязка данных состоит из трех компонентов:</span><span class="sxs-lookup"><span data-stu-id="bc89a-263">Data binding involves three components:</span></span>

* <span data-ttu-id="bc89a-264">источник данных Hello</span><span class="sxs-lookup"><span data-stu-id="bc89a-264">hello data source</span></span>
* <span data-ttu-id="bc89a-265">макет экрана приветствия</span><span class="sxs-lookup"><span data-stu-id="bc89a-265">hello screen layout</span></span>
* <span data-ttu-id="bc89a-266">адаптер Hello, предложение WITH ties hello два друг с другом.</span><span class="sxs-lookup"><span data-stu-id="bc89a-266">hello adapter that ties hello two together.</span></span>

<span data-ttu-id="bc89a-267">В нашем примере кода мы возвращаем hello данных из таблицы мобильных приложений SQL Azure hello **ToDoItem** в массив.</span><span class="sxs-lookup"><span data-stu-id="bc89a-267">In our sample code, we return hello data from hello Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="bc89a-268">Это действие типично для приложений для обработки данных.</span><span class="sxs-lookup"><span data-stu-id="bc89a-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="bc89a-269">Запросы к базе данных часто возвращают коллекцию строк, которые hello клиент получает в список или массив.</span><span class="sxs-lookup"><span data-stu-id="bc89a-269">Database queries often return a collection of rows that hello client gets in a list or array.</span></span> <span data-ttu-id="bc89a-270">В этом образце hello массива является hello источника данных.</span><span class="sxs-lookup"><span data-stu-id="bc89a-270">In this sample, hello array is hello data source.</span></span>  <span data-ttu-id="bc89a-271">Код Hello определяет макет экрана, который определяет представление hello hello данные, отображаемые на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-271">hello code specifies a screen layout that defines hello view of hello data that appears on hello device.</span></span>  <span data-ttu-id="bc89a-272">Hello двух связанных вместе с адаптер, который этот код — это расширение hello **ArrayAdapter&lt;ToDoItem&gt;**  класса.</span><span class="sxs-lookup"><span data-stu-id="bc89a-272">hello two are bound together with an adapter, which in this code is an extension of hello **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <span data-ttu-id="bc89a-273"><a name="layout"></a>Определение hello макета</span><span class="sxs-lookup"><span data-stu-id="bc89a-273"><a name="layout"></a>Define hello Layout</span></span>

<span data-ttu-id="bc89a-274">Макет Hello определяется несколько фрагментов кода XML.</span><span class="sxs-lookup"><span data-stu-id="bc89a-274">hello layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="bc89a-275">Имея существующий макет, hello, следующий код представляет hello **ListView** мы хотим toopopulate с сервера данных.</span><span class="sxs-lookup"><span data-stu-id="bc89a-275">Given an existing layout, hello following code represents hello **ListView** we want toopopulate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="bc89a-276">В предыдущих кода hello, hello *listitem* атрибут задает идентификатор hello hello макет для отдельной строки в списке hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-276">In hello preceding code, hello *listitem* attribute specifies hello id of hello layout for an individual row in hello list.</span></span> <span data-ttu-id="bc89a-277">Этот код задает типа "флажок" и соответствующий текст и создается один раз для каждого элемента в списке hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-277">This code specifies a check box and its associated text and gets instantiated once for each item in hello list.</span></span> <span data-ttu-id="bc89a-278">Этот макет не отображает hello **идентификатор** поля, а также более сложные макеты указать дополнительные поля в экран приветствия.</span><span class="sxs-lookup"><span data-stu-id="bc89a-278">This layout does not display hello **id** field, and a more complex layout would specify additional fields in hello display.</span></span> <span data-ttu-id="bc89a-279">Этот код находится в hello **row_list_to_do.xml** файла.</span><span class="sxs-lookup"><span data-stu-id="bc89a-279">This code is in hello **row_list_to_do.xml** file.</span></span>

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <span data-ttu-id="bc89a-280"><a name="adapter"></a>Определить адаптер hello</span><span class="sxs-lookup"><span data-stu-id="bc89a-280"><a name="adapter"></a>Define hello adapter</span></span>
<span data-ttu-id="bc89a-281">Так как источник данных hello наши представления — это массив **ToDoItem**, мы подкласс нашей адаптера из **ArrayAdapter&lt;ToDoItem&gt;**  класса.</span><span class="sxs-lookup"><span data-stu-id="bc89a-281">Since hello data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="bc89a-282">Этот подкласс создает представление для каждого **ToDoItem** с помощью hello **row_list_to_do** макета.</span><span class="sxs-lookup"><span data-stu-id="bc89a-282">This subclass produces a View for every **ToDoItem** using hello **row_list_to_do** layout.</span></span>  <span data-ttu-id="bc89a-283">В приведенном коде определяется следующий класс, который является расширением hello hello **ArrayAdapter&lt;E&gt;**  класса:</span><span class="sxs-lookup"><span data-stu-id="bc89a-283">In our code, we define hello following class that is an extension of hello **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="bc89a-284">Переопределить hello адаптеров **getView** метод.</span><span class="sxs-lookup"><span data-stu-id="bc89a-284">Override hello adapters **getView** method.</span></span> <span data-ttu-id="bc89a-285">Например:</span><span class="sxs-lookup"><span data-stu-id="bc89a-285">For example:</span></span>

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

<span data-ttu-id="bc89a-286">Мы создаем экземпляр этого класса в действии следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bc89a-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="bc89a-287">Hello второй параметр toohello ToDoItemAdapter конструктор имеет toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="bc89a-287">hello second parameter toohello ToDoItemAdapter constructor is a reference toohello layout.</span></span> <span data-ttu-id="bc89a-288">Теперь мы допускающими hello **ListView** и назначить hello адаптера toohello **ListView**.</span><span class="sxs-lookup"><span data-stu-id="bc89a-288">We can now instantiate hello **ListView** and assign hello adapter toohello **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <span data-ttu-id="bc89a-289"><a name="use-adapter"></a>Используйте hello адаптера tooBind toohello пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="bc89a-289"><a name="use-adapter"></a>Use hello Adapter tooBind toohello UI</span></span>

<span data-ttu-id="bc89a-290">Теперь вы находитесь готов toouse привязки данных.</span><span class="sxs-lookup"><span data-stu-id="bc89a-290">You are now ready toouse data binding.</span></span> <span data-ttu-id="bc89a-291">Hello следующий код показывает, как tooget элементов в таблице hello и заполняет hello локальный адаптер с hello вернул элементов.</span><span class="sxs-lookup"><span data-stu-id="bc89a-291">hello following code shows how tooget items in hello table and fills hello local adapter with hello returned items.</span></span>

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

<span data-ttu-id="bc89a-292">Вызовите адаптера hello любое время изменить hello **ToDoItem** таблицы.</span><span class="sxs-lookup"><span data-stu-id="bc89a-292">Call hello adapter any time you modify hello **ToDoItem** table.</span></span> <span data-ttu-id="bc89a-293">Так как изменения выполняются на уровне отдельных записей, обрабатываться будут отдельные строки, а не коллекция.</span><span class="sxs-lookup"><span data-stu-id="bc89a-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="bc89a-294">При вставке элемента вызовите hello **добавить** метод на hello адаптер; при удалении, вызовите hello **удалить** метод.</span><span class="sxs-lookup"><span data-stu-id="bc89a-294">When you insert an item, call hello **add** method on hello adapter; when deleting, call hello **remove** method.</span></span>

<span data-ttu-id="bc89a-295">Полный пример можно найти в hello [проекта Android краткое руководство][21].</span><span class="sxs-lookup"><span data-stu-id="bc89a-295">You can find a complete example in hello [Android Quickstart Project][21].</span></span>

## <span data-ttu-id="bc89a-296"><a name="inserting"></a>Вставка данных в серверной части hello</span><span class="sxs-lookup"><span data-stu-id="bc89a-296"><a name="inserting"></a>Insert data into hello backend</span></span>

<span data-ttu-id="bc89a-297">Создайте экземпляр элемента hello *ToDoItem* класса и задать его свойства.</span><span class="sxs-lookup"><span data-stu-id="bc89a-297">Instantiate an instance of hello *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="bc89a-298">Затем с помощью **insert()** tooinsert объекта:</span><span class="sxs-lookup"><span data-stu-id="bc89a-298">Then use **insert()** tooinsert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="bc89a-299">Hello возвращаемых соответствий сущности данных hello, вставленных в таблицу hello, идентификатор включается hello и любые другие значения (например hello `createdAt`, `updatedAt`, и `version` поля) на серверной hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-299">hello returned entity matches hello data inserted into hello backend table, included hello ID and any other values (such as hello `createdAt`, `updatedAt`, and `version` fields) set on hello backend.</span></span>

<span data-ttu-id="bc89a-300">Для таблиц мобильных приложений требуется столбец первичного ключа **id**. Этот столбец должен быть строкой.</span><span class="sxs-lookup"><span data-stu-id="bc89a-300">Mobile Apps tables require a primary key column named **id**. This column must be a string.</span></span> <span data-ttu-id="bc89a-301">значение по умолчанию Hello hello идентификатор столбца — это GUID.</span><span class="sxs-lookup"><span data-stu-id="bc89a-301">hello default value of hello ID column is a GUID.</span></span>  <span data-ttu-id="bc89a-302">Можно указать другие уникальные значения, в том числе электронные адреса или имена пользователей.</span><span class="sxs-lookup"><span data-stu-id="bc89a-302">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="bc89a-303">Если строковое значение идентификатора для вставленной записи не поддерживается, серверной hello создает новый идентификатор GUID.</span><span class="sxs-lookup"><span data-stu-id="bc89a-303">When a string ID value is not provided for an inserted record, hello backend generates a new GUID.</span></span>

<span data-ttu-id="bc89a-304">Строковые значения идентификатора предоставляют hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="bc89a-304">String ID values provide hello following advantages:</span></span>

* <span data-ttu-id="bc89a-305">Идентификаторы могут создаваться без создания базы данных toohello кругового пути.</span><span class="sxs-lookup"><span data-stu-id="bc89a-305">IDs can be generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="bc89a-306">Записи, проще toomerge из различных таблиц или баз данных.</span><span class="sxs-lookup"><span data-stu-id="bc89a-306">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="bc89a-307">Значения идентификаторов удобнее интегрировать с логикой приложения.</span><span class="sxs-lookup"><span data-stu-id="bc89a-307">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="bc89a-308">Строковые значения идентификатора **НЕОБХОДИМЫ** для поддержки автономной синхронизации.</span><span class="sxs-lookup"><span data-stu-id="bc89a-308">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="bc89a-309">Невозможно изменить идентификатор, когда он хранится в базе данных серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-309">You cannot change an Id once it is stored in hello backend database.</span></span>

## <span data-ttu-id="bc89a-310"><a name="updating"></a>Обновление данных в мобильном приложении</span><span class="sxs-lookup"><span data-stu-id="bc89a-310"><a name="updating"></a>Update data in a mobile app</span></span>

<span data-ttu-id="bc89a-311">tooupdate данные в таблице, проходят hello новый объект toohello **update()** метод.</span><span class="sxs-lookup"><span data-stu-id="bc89a-311">tooupdate data in a table, pass hello new object toohello **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="bc89a-312">В этом примере *элемент* строка tooa ссылку в hello *ToDoItem* таблицы, которое имело некоторые изменения, внесенные tooit.</span><span class="sxs-lookup"><span data-stu-id="bc89a-312">In this example, *item* is a reference tooa row in hello *ToDoItem* table, which has had some changes made tooit.</span></span>  <span data-ttu-id="bc89a-313">Строка Hello с hello же **идентификатор** обновляется.</span><span class="sxs-lookup"><span data-stu-id="bc89a-313">hello row with hello same **id** is updated.</span></span>

## <span data-ttu-id="bc89a-314"><a name="deleting"></a>Удаление данных в мобильном приложении</span><span class="sxs-lookup"><span data-stu-id="bc89a-314"><a name="deleting"></a>Delete data in a mobile app</span></span>

<span data-ttu-id="bc89a-315">Привет, следующий код показывает, как toodelete данные из таблицы, указав hello объекта данных.</span><span class="sxs-lookup"><span data-stu-id="bc89a-315">hello following code shows how toodelete data from a table by specifying hello data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="bc89a-316">Можно также удалить элемент, указав hello **идентификатор** поле toodelete строку hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-316">You can also delete an item by specifying hello **id** field of hello row toodelete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <span data-ttu-id="bc89a-317"><a name="lookup"></a>Поиск определенного элемента по идентификатору</span><span class="sxs-lookup"><span data-stu-id="bc89a-317"><a name="lookup"></a>Look up a specific item by Id</span></span>

<span data-ttu-id="bc89a-318">Поиск элемента с определенным **идентификатор** с hello **Просмотр()** метод:</span><span class="sxs-lookup"><span data-stu-id="bc89a-318">Look up an item with a specific **id** field with hello **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <span data-ttu-id="bc89a-319"><a name="untyped"></a>Практическое руководство. Работа с нетипизированными данными</span><span class="sxs-lookup"><span data-stu-id="bc89a-319"><a name="untyped"></a>How to: Work with untyped data</span></span>

<span data-ttu-id="bc89a-320">модель программирования нетипизированный Hello дает точный контроль над сериализации JSON.</span><span class="sxs-lookup"><span data-stu-id="bc89a-320">hello untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="bc89a-321">Существуют некоторые распространенные сценарии, где вы можете toouse модель программирования нетипизированным.</span><span class="sxs-lookup"><span data-stu-id="bc89a-321">There are some common scenarios where you may wish toouse an untyped programming model.</span></span> <span data-ttu-id="bc89a-322">Например, если таблица базы данных содержит много столбцов, а требуется только подмножество столбцов hello tooreference.</span><span class="sxs-lookup"><span data-stu-id="bc89a-322">For example, if your backend table contains many columns and you only need tooreference a subset of hello columns.</span></span>  <span data-ttu-id="bc89a-323">типизированный модели Hello требуется toodefine все hello столбцов, определенных в серверной части мобильные приложения hello в класс данных.</span><span class="sxs-lookup"><span data-stu-id="bc89a-323">hello typed model requires you toodefine all hello columns defined in hello Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="bc89a-324">Большинство вызовов API для доступа к данным hello toohello типизированного программирования вызовов.</span><span class="sxs-lookup"><span data-stu-id="bc89a-324">Most of hello API calls for accessing data are similar toohello typed programming calls.</span></span> <span data-ttu-id="bc89a-325">Hello основное отличие заключается в модели нетипизированный hello вызвать методы hello **MobileServiceJsonTable** объекта, а не hello **MobileServiceTable** объекта.</span><span class="sxs-lookup"><span data-stu-id="bc89a-325">hello main difference is that in hello untyped model you invoke methods on hello **MobileServiceJsonTable** object, instead of hello **MobileServiceTable** object.</span></span>

### <span data-ttu-id="bc89a-326"><a name="json_instance"></a>Создание экземпляра нетипизированной таблицы</span><span class="sxs-lookup"><span data-stu-id="bc89a-326"><a name="json_instance"></a>Create an instance of an untyped table</span></span>

<span data-ttu-id="bc89a-327">Аналогичные toohello типом модели, начать с получения ссылки на таблицу, но в данном случае это **MobileServicesJsonTable** объекта.</span><span class="sxs-lookup"><span data-stu-id="bc89a-327">Similar toohello typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="bc89a-328">Получить hello ссылку с помощью вызывающему Привет **getTable** метода для экземпляра hello клиента:</span><span class="sxs-lookup"><span data-stu-id="bc89a-328">Obtain hello reference by calling hello **getTable** method on an instance of hello client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="bc89a-329">После создания экземпляра hello **MobileServiceJsonTable**, он имеет практически hello же API доступна как с моделью программирования типизированный hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-329">Once you have created an instance of hello **MobileServiceJsonTable**, it has virtually hello same API available as with hello typed programming model.</span></span> <span data-ttu-id="bc89a-330">В некоторых случаях hello методы принимают параметр нетипизированный вместо типизированных параметров.</span><span class="sxs-lookup"><span data-stu-id="bc89a-330">In some cases, hello methods take an untyped parameter instead of a typed parameter.</span></span>

### <span data-ttu-id="bc89a-331"><a name="json_insert"></a>Вставка данных в нетипизированную таблицу</span><span class="sxs-lookup"><span data-stu-id="bc89a-331"><a name="json_insert"></a>Insert into an untyped table</span></span>
<span data-ttu-id="bc89a-332">Здравствуйте, как следующий код показывает toodo инструкции insert.</span><span class="sxs-lookup"><span data-stu-id="bc89a-332">hello following code shows how toodo an insert.</span></span> <span data-ttu-id="bc89a-333">Hello первым шагом является toocreate [JsonObject][1], который является частью hello [gson] [ 3] библиотеки.</span><span class="sxs-lookup"><span data-stu-id="bc89a-333">hello first step is toocreate a [JsonObject][1], which is part of hello [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="bc89a-334">Затем с помощью **insert()** tooinsert hello нетипизированный объект в таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-334">Then, Use **insert()** tooinsert hello untyped object into hello table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="bc89a-335">Если вам требуется идентификатор hello tooget вставлены hello объекта, используйте hello **getAsJsonPrimitive()** метод.</span><span class="sxs-lookup"><span data-stu-id="bc89a-335">If you need tooget hello ID of hello inserted object, use hello **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <span data-ttu-id="bc89a-336"><a name="json_delete"></a>Удаление данных из нетипизированной таблицы</span><span class="sxs-lookup"><span data-stu-id="bc89a-336"><a name="json_delete"></a>Delete from an untyped table</span></span>
<span data-ttu-id="bc89a-337">Hello следующий код показывает, как toodelete экземпляра, в этом случае hello одного экземпляра **JsonObject** , созданных предыдущими hello *вставить* примере.</span><span class="sxs-lookup"><span data-stu-id="bc89a-337">hello following code shows how toodelete an instance, in this case, hello same instance of a **JsonObject** that was created in hello prior *insert* example.</span></span> <span data-ttu-id="bc89a-338">Код Hello-hello так же, как hello типизированные регистр, но метод hello имеет другую подпись, поскольку она ссылается на **JsonObject**.</span><span class="sxs-lookup"><span data-stu-id="bc89a-338">hello code is hello same as with hello typed case, but hello method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="bc89a-339">Вы также можете удалить экземпляр напрямую с помощью идентификатора:</span><span class="sxs-lookup"><span data-stu-id="bc89a-339">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <span data-ttu-id="bc89a-340"><a name="json_get"></a>Получение всех строк из нетипизированной таблицы</span><span class="sxs-lookup"><span data-stu-id="bc89a-340"><a name="json_get"></a>Return all rows from an untyped table</span></span>
<span data-ttu-id="bc89a-341">Здравствуйте, как следующий код показывает tooretrieve всей таблицы.</span><span class="sxs-lookup"><span data-stu-id="bc89a-341">hello following code shows how tooretrieve an entire table.</span></span> <span data-ttu-id="bc89a-342">Так как вы используете таблицу JSON, можно получить только некоторых столбцов таблицы hello выборочно.</span><span class="sxs-lookup"><span data-stu-id="bc89a-342">Since you are using a JSON Table, you can selectively retrieve only some of hello table's columns.</span></span>

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

<span data-ttu-id="bc89a-343">Hello одинаковых фильтрации, фильтрацию и разбиение по страницам методы, доступные для типизированных модели hello доступны для hello нетипизированный модели.</span><span class="sxs-lookup"><span data-stu-id="bc89a-343">hello same set of filtering, filtering and paging methods that are available for hello typed model are available for hello untyped model.</span></span>

## <span data-ttu-id="bc89a-344"><a name="offline-sync"></a>Реализация синхронизации в автономном режиме</span><span class="sxs-lookup"><span data-stu-id="bc89a-344"><a name="offline-sync"></a>Implement Offline Sync</span></span>

<span data-ttu-id="bc89a-345">Hello Azure Mobile приложения клиента SDK также реализует синхронизации данных в автономном режиме с помощью копирования данных сервера hello toostore базы данных SQLite локально.</span><span class="sxs-lookup"><span data-stu-id="bc89a-345">hello Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database toostore a copy of hello server data locally.</span></span>  <span data-ttu-id="bc89a-346">Операции, выполняемые в автономной таблице toowork мобильного подключения не требуется.</span><span class="sxs-lookup"><span data-stu-id="bc89a-346">Operations performed on an offline table do not require mobile connectivity toowork.</span></span>  <span data-ttu-id="bc89a-347">Помогает автономной синхронизации в устойчивость и производительность за счет hello объекта более сложная логика разрешения конфликтов.</span><span class="sxs-lookup"><span data-stu-id="bc89a-347">Offline sync aids in resilience and performance at hello expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="bc89a-348">Hello Azure Mobile приложения клиента SDK реализует hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="bc89a-348">hello Azure Mobile Apps Client SDK implements hello following features:</span></span>

* <span data-ttu-id="bc89a-349">Добавочная синхронизация. Загружаются только обновленные и новые записи. Это позволяет уменьшить потребление пропускной способности и памяти.</span><span class="sxs-lookup"><span data-stu-id="bc89a-349">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="bc89a-350">Оптимистический параллелизм: Operations, считаются toosucceed.</span><span class="sxs-lookup"><span data-stu-id="bc89a-350">Optimistic Concurrency: Operations are assumed toosucceed.</span></span>  <span data-ttu-id="bc89a-351">Разрешение конфликтов, откладывается до обновления выполняются на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-351">Conflict Resolution is deferred until updates are performed on hello server.</span></span>
* <span data-ttu-id="bc89a-352">Разрешение конфликтов: приветствия SDK обнаруживает, когда был сделан на сервере hello конфликтующее изменение и предоставляет подключает tooalert hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="bc89a-352">Conflict Resolution: hello SDK detects when a conflicting change has been made at hello server and provides hooks tooalert hello user.</span></span>
* <span data-ttu-id="bc89a-353">Удаление с возможностью восстановления: Удаленных записей будут помечены как удаленные, позволяя другим tooupdate устройств их автономного кэша.</span><span class="sxs-lookup"><span data-stu-id="bc89a-353">Soft Delete: Deleted records are marked deleted, allowing other devices tooupdate their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="bc89a-354">Инициализация синхронизации в автономном режиме</span><span class="sxs-lookup"><span data-stu-id="bc89a-354">Initialize Offline Sync</span></span>

<span data-ttu-id="bc89a-355">Каждая таблица вне сети должен быть определен в автономном кэше hello перед использованием.</span><span class="sxs-lookup"><span data-stu-id="bc89a-355">Each offline table must be defined in hello offline cache before use.</span></span>  <span data-ttu-id="bc89a-356">Как правило определение таблицы выполняется сразу после создания hello hello клиента:</span><span class="sxs-lookup"><span data-stu-id="bc89a-356">Normally, table definition is done immediately after hello creation of hello client:</span></span>

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with hello model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define hello table in hello local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize hello local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-toohello-offline-cache-table"></a><span data-ttu-id="bc89a-357">Получить ссылку toohello автономной таблицы кэша</span><span class="sxs-lookup"><span data-stu-id="bc89a-357">Obtain a reference toohello Offline Cache Table</span></span>

<span data-ttu-id="bc89a-358">Для таблицы в Интернете используйте `.getTable()`,</span><span class="sxs-lookup"><span data-stu-id="bc89a-358">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="bc89a-359">а для автономной таблицы — `.getSyncTable()`:</span><span class="sxs-lookup"><span data-stu-id="bc89a-359">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="bc89a-360">Здравствуйте, все методы, доступные для документации таблиц (в том числе фильтрация, сортировка, разбиение по страницам, вставка данных, обновление данных и удаление данных) работают одинаково хорошо на подключенном и автономном таблиц.</span><span class="sxs-lookup"><span data-stu-id="bc89a-360">All hello methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-hello-local-offline-cache"></a><span data-ttu-id="bc89a-361">Синхронизировать локальный кэш автономных hello</span><span class="sxs-lookup"><span data-stu-id="bc89a-361">Synchronize hello Local Offline Cache</span></span>

<span data-ttu-id="bc89a-362">Синхронизация находится в элементе управления hello приложения.</span><span class="sxs-lookup"><span data-stu-id="bc89a-362">Synchronization is within hello control of your app.</span></span>  <span data-ttu-id="bc89a-363">Ниже приведен пример метода синхронизации.</span><span class="sxs-lookup"><span data-stu-id="bc89a-363">Here is an example synchronization method:</span></span>

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

<span data-ttu-id="bc89a-364">Если указано имя запроса toohello `.pull(query, queryname)` метод, то добавочной синхронизации является tooreturn используется только записи, которые были созданы или изменены с момента последнего успешного завершения hello запросу.</span><span class="sxs-lookup"><span data-stu-id="bc89a-364">If a query name is provided toohello `.pull(query, queryname)` method, then incremental sync is used tooreturn only records that have been created or changed since hello last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="bc89a-365">Обработка конфликтов во время синхронизации в автономном режиме</span><span class="sxs-lookup"><span data-stu-id="bc89a-365">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="bc89a-366">Если конфликт происходит во время выполнения операции `.push()`, возникает исключение `MobileServiceConflictException`.</span><span class="sxs-lookup"><span data-stu-id="bc89a-366">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="bc89a-367">элемент, сформированных сервером Hello встроен в исключение hello и можно получить с `.getItem()` по исключению hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-367">hello server-issued item is embedded in hello exception and can be retrieved by `.getItem()` on hello exception.</span></span>  <span data-ttu-id="bc89a-368">Настройка принудительной hello, вызывающему Привет следующих элементов в объекте MobileServiceSyncContext hello:</span><span class="sxs-lookup"><span data-stu-id="bc89a-368">Adjust hello push by calling hello following items on hello MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="bc89a-369">Когда все конфликты, помечаются как надо, вызовите `.push()` снова tooresolve все hello конфликтов.</span><span class="sxs-lookup"><span data-stu-id="bc89a-369">Once all conflicts are marked as you wish, call `.push()` again tooresolve all hello conflicts.</span></span>

## <span data-ttu-id="bc89a-370"><a name="custom-api"></a>Вызов настраиваемого интерфейса API</span><span class="sxs-lookup"><span data-stu-id="bc89a-370"><a name="custom-api"></a>Call a custom API</span></span>

<span data-ttu-id="bc89a-371">Пользовательский API позволяет toodefine пользовательских конечных точек, предоставляющих функциональные возможности сервера, которые не сопоставляются tooan вставки, обновления, удаления или операцию чтения.</span><span class="sxs-lookup"><span data-stu-id="bc89a-371">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="bc89a-372">При использовании настраиваемого интерфейса API вы получаете больше возможностей для управления сообщениями, в том числе для чтения и установки заголовков HTTP-сообщений, а также определения форматов текста сообщений, отличных от JSON.</span><span class="sxs-lookup"><span data-stu-id="bc89a-372">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="bc89a-373">Из Android клиента, вызовите hello **invokeApi** toocall hello пользовательские API конечную точку метода.</span><span class="sxs-lookup"><span data-stu-id="bc89a-373">From an Android client, you call hello **invokeApi** method toocall hello custom API endpoint.</span></span> <span data-ttu-id="bc89a-374">Hello следующем примере показано, как toocall конечную точку API именоваться **completeAll**, который возвращает класс коллекции с именем **MarkAllResult**.</span><span class="sxs-lookup"><span data-stu-id="bc89a-374">hello following example shows how toocall an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

<span data-ttu-id="bc89a-375">Hello **invokeApi** метод будет вызван на приветствия клиента, который отправляет сообщение запроса toohello новый пользовательский интерфейс API.</span><span class="sxs-lookup"><span data-stu-id="bc89a-375">hello **invokeApi** method is called on hello client, which sends a POST request toohello new custom API.</span></span> <span data-ttu-id="bc89a-376">Hello результат, возвращаемый пользовательский API hello отображается в диалоговом окне сообщения, как ошибок.</span><span class="sxs-lookup"><span data-stu-id="bc89a-376">hello result returned by hello custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="bc89a-377">Другие версии **invokeApi** позволяют при необходимости отправлять в тексте запроса hello объекта, укажите метод hello HTTP и отправки параметров запроса с запросом hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-377">Other versions of **invokeApi** let you optionally send an object in hello request body, specify hello HTTP method, and send query parameters with hello request.</span></span> <span data-ttu-id="bc89a-378">Кроме того, доступны нетипизированные версии **invokeApi** .</span><span class="sxs-lookup"><span data-stu-id="bc89a-378">Untyped versions of **invokeApi** are provided as well.</span></span>

## <span data-ttu-id="bc89a-379"><a name="authentication"></a>Добавить приложение tooyour проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="bc89a-379"><a name="authentication"></a>Add authentication tooyour app</span></span>

<span data-ttu-id="bc89a-380">Учебники по уже подробно описано как tooadd эти функции.</span><span class="sxs-lookup"><span data-stu-id="bc89a-380">Tutorials already describe in detail how tooadd these features.</span></span>

<span data-ttu-id="bc89a-381">Служба приложений поддерживает [проверку подлинности пользователей приложения](app-service-mobile-android-get-started-users.md) с помощью разных внешних поставщиков удостоверений: Facebook, Google, учетной записи Майкрософт, Twitter и Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bc89a-381">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="bc89a-382">Можно задать разрешения для таблицы toorestrict доступ для определенных операций tooonly проверку подлинности пользователей.</span><span class="sxs-lookup"><span data-stu-id="bc89a-382">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="bc89a-383">Также можно использовать hello идентификаторов правил авторизации tooimplement прошедших проверку подлинности пользователей в серверной части.</span><span class="sxs-lookup"><span data-stu-id="bc89a-383">You can also use hello identity of authenticated users tooimplement authorization rules in your backend.</span></span>

<span data-ttu-id="bc89a-384">Поддерживаются два потока аутентификации: **серверный** и **клиентский**.</span><span class="sxs-lookup"><span data-stu-id="bc89a-384">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="bc89a-385">Hello server потока обеспечивает hello простой проверки подлинности, поскольку он основан на hello идентификаторов поставщиков веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="bc89a-385">hello server flow provides hello simplest authentication experience, as it relies on hello identity providers web interface.</span></span>  <span data-ttu-id="bc89a-386">Нет дополнительные пакеты SDK, tooimplement требуется аутентификация потока.</span><span class="sxs-lookup"><span data-stu-id="bc89a-386">No additional SDKs are required tooimplement server flow authentication.</span></span> <span data-ttu-id="bc89a-387">Аутентификация потока не обеспечивает глубокую интеграцию в мобильном устройстве hello и рекомендуется только для проверки концепции сценариев.</span><span class="sxs-lookup"><span data-stu-id="bc89a-387">Server flow authentication does not provide a deep integration into hello mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="bc89a-388">поток клиентских Hello позволяет более глубокую интеграцию с возможности конкретного устройства, такие как единый вход как зависит от пакетов SDK, предоставляемые поставщиком удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-388">hello client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by hello identity provider.</span></span>  <span data-ttu-id="bc89a-389">Например можно интегрировать hello Facebook SDK в мобильное приложение.</span><span class="sxs-lookup"><span data-stu-id="bc89a-389">For example, you can integrate hello Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="bc89a-390">Мобильный клиент Hello меняет в приложение Facebook hello и подтверждает вашему входу, прежде чем переключаться задней tooyour мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="bc89a-390">hello mobile client swaps into hello Facebook app and confirms your sign-on before swapping back tooyour mobile app.</span></span>

<span data-ttu-id="bc89a-391">Четыре действия, необходимые tooenable проверки подлинности в приложении:</span><span class="sxs-lookup"><span data-stu-id="bc89a-391">Four steps are required tooenable authentication in your app:</span></span>

* <span data-ttu-id="bc89a-392">Регистрация приложения для аутентификации в поставщике удостоверений.</span><span class="sxs-lookup"><span data-stu-id="bc89a-392">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="bc89a-393">Настройка серверной части службы приложений.</span><span class="sxs-lookup"><span data-stu-id="bc89a-393">Configure your App Service backend.</span></span>
* <span data-ttu-id="bc89a-394">Запретить пользователям tooauthenticated таблиц разрешения только на hello серверной службы приложений.</span><span class="sxs-lookup"><span data-stu-id="bc89a-394">Restrict table permissions tooauthenticated users only on hello App Service backend.</span></span>
* <span data-ttu-id="bc89a-395">Добавьте приложение tooyour код проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bc89a-395">Add authentication code tooyour app.</span></span>

<span data-ttu-id="bc89a-396">Можно задать разрешения для таблицы toorestrict доступ для определенных операций tooonly проверку подлинности пользователей.</span><span class="sxs-lookup"><span data-stu-id="bc89a-396">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="bc89a-397">Можно также использовать hello SID toomodify прошедший проверку пользователь запросов.</span><span class="sxs-lookup"><span data-stu-id="bc89a-397">You can also use hello SID of an authenticated user toomodify requests.</span></span>  <span data-ttu-id="bc89a-398">Дополнительные сведения см. в статье [приступить к работе с проверкой подлинности] и hello документации HOWTO SDK сервера.</span><span class="sxs-lookup"><span data-stu-id="bc89a-398">For more information, review [Get started with authentication] and hello Server SDK HOWTO documentation.</span></span>

### <span data-ttu-id="bc89a-399"><a name="caching"></a>Серверный поток проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="bc89a-399"><a name="caching"></a>Authentication: Server Flow</span></span>

<span data-ttu-id="bc89a-400">Hello кода ниже выполняется запуск процесса входа в систему сервера потока с помощью поставщика Google hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-400">hello following code starts a server flow login process using hello Google provider.</span></span>  <span data-ttu-id="bc89a-401">Дополнительная настройка не требуется из-за требований безопасности hello для поставщика Google hello:</span><span class="sxs-lookup"><span data-stu-id="bc89a-401">Additional configuration is required because of hello security requirements for hello Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="bc89a-402">Кроме того добавьте следующий метод toohello основной класс действие hello:</span><span class="sxs-lookup"><span data-stu-id="bc89a-402">In addition, add hello following method toohello main Activity class:</span></span>

```java
// You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check hello request code matches hello one we send in hello login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check hello error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

<span data-ttu-id="bc89a-403">Hello `GOOGLE_LOGIN_REQUEST_CODE` определен в с главным действие используется для hello `login()` метод и в пределах hello `onActivityResult()` метод.</span><span class="sxs-lookup"><span data-stu-id="bc89a-403">hello `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for hello `login()` method and within hello `onActivityResult()` method.</span></span>  <span data-ttu-id="bc89a-404">Можно выбрать любой уникальный номер, при условии, что hello этим же номером используется внутри hello `login()` метод и hello `onActivityResult()` метод.</span><span class="sxs-lookup"><span data-stu-id="bc89a-404">You can choose any unique number, as long as hello same number is used within hello `login()` method and hello `onActivityResult()` method.</span></span>  <span data-ttu-id="bc89a-405">Если абстрактный hello клиентского кода в адаптер службы (как показано выше), следует вызвать соответствующие методы hello для hello службы адаптера.</span><span class="sxs-lookup"><span data-stu-id="bc89a-405">If you abstract hello client code into a service adapter (as shown earlier), you should call hello appropriate methods on hello service adapter.</span></span>

<span data-ttu-id="bc89a-406">Необходимо также tooconfigure hello проекта для customtabs.</span><span class="sxs-lookup"><span data-stu-id="bc89a-406">You also need tooconfigure hello project for customtabs.</span></span>  <span data-ttu-id="bc89a-407">Сначала укажите URL-адрес перенаправления.</span><span class="sxs-lookup"><span data-stu-id="bc89a-407">First specify a redirect-URL.</span></span>  <span data-ttu-id="bc89a-408">Добавьте следующий фрагмент слишком hello`AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="bc89a-408">Add hello following snippet too`AndroidManifest.xml`:</span></span>

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

<span data-ttu-id="bc89a-409">Добавить hello **redirectUriScheme** toohello `build.gradle` файл для приложения:</span><span class="sxs-lookup"><span data-stu-id="bc89a-409">Add hello **redirectUriScheme** toohello `build.gradle` file for your application:</span></span>

```text
android {
    buildTypes {
        release {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
        debug {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
    }
}
```

<span data-ttu-id="bc89a-410">Наконец, добавьте `com.android.support:customtabs:23.0.1` toohello список зависимостей в hello `build.gradle` файла:</span><span class="sxs-lookup"><span data-stu-id="bc89a-410">Finally, add `com.android.support:customtabs:23.0.1` toohello dependencies list in hello `build.gradle` file:</span></span>

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.2.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

<span data-ttu-id="bc89a-411">Получить идентификатор hello hello вошедшего в систему пользователя из **MobileServiceUser** с помощью hello **getUserId** метод.</span><span class="sxs-lookup"><span data-stu-id="bc89a-411">Obtain hello ID of hello logged-in user from a **MobileServiceUser** using hello **getUserId** method.</span></span> <span data-ttu-id="bc89a-412">Пример, как toocall toouse фьючерсов hello входа асинхронные интерфейсы API, см. [приступить к работе с проверкой подлинности].</span><span class="sxs-lookup"><span data-stu-id="bc89a-412">For an example of how toouse Futures toocall hello asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="bc89a-413">Hello упомянутые схема URL-адресов с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="bc89a-413">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="bc89a-414">Убедитесь, что во всех вхождениях `{url_scheme_of_you_app}` используется один и тот же регистр.</span><span class="sxs-lookup"><span data-stu-id="bc89a-414">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <span data-ttu-id="bc89a-415"><a name="caching"></a>Кэширование токенов проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="bc89a-415"><a name="caching"></a>Cache authentication tokens</span></span>

<span data-ttu-id="bc89a-416">Кэширование маркеров проверки подлинности требует hello toostore идентификатор пользователя и маркер проверки подлинности локально на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-416">Caching authentication tokens requires you toostore hello User ID and authentication token locally on hello device.</span></span> <span data-ttu-id="bc89a-417">Hello при следующем запуске приложения hello, вы проверяете hello кэша, и если эти значения, можно пропустить журнала hello в процедуре и повторно заполнить hello клиента с этими данными.</span><span class="sxs-lookup"><span data-stu-id="bc89a-417">hello next time hello app starts, you check hello cache, and if these values are present, you can skip hello log in procedure and rehydrate hello client with this data.</span></span> <span data-ttu-id="bc89a-418">Однако конфиденциальные данные, и должны быть сохранены, шифруются в целях безопасности в случае, если телефон hello кражи.</span><span class="sxs-lookup"><span data-stu-id="bc89a-418">However this data is sensitive, and it should be stored encrypted for safety in case hello phone gets stolen.</span></span>  <span data-ttu-id="bc89a-419">Вы увидите полный пример, как маркеры проверки подлинности toocache в [кэшировать раздел токены проверки подлинности][7].</span><span class="sxs-lookup"><span data-stu-id="bc89a-419">You can see a complete example of how toocache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="bc89a-420">При попытке toouse просроченного маркера, вы получаете *401 несанкционированный* ответа.</span><span class="sxs-lookup"><span data-stu-id="bc89a-420">When you try toouse an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="bc89a-421">Ошибки аутентификации можно обрабатывать с помощью фильтров.</span><span class="sxs-lookup"><span data-stu-id="bc89a-421">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="bc89a-422">Фильтры перехватывать запросы toohello серверной службы приложений.</span><span class="sxs-lookup"><span data-stu-id="bc89a-422">Filters intercept requests toohello App Service backend.</span></span> <span data-ttu-id="bc89a-423">Код фильтра Hello проверяет ответ 401 hello, запускает hello процесса входа в и возобновляет hello запроса, создавшего hello 401.</span><span class="sxs-lookup"><span data-stu-id="bc89a-423">hello filter code tests hello response for a 401, triggers hello sign-in process, and then resumes hello request that generated hello 401.</span></span>

### <span data-ttu-id="bc89a-424"><a name="refresh"></a>Использование токенов обновления</span><span class="sxs-lookup"><span data-stu-id="bc89a-424"><a name="refresh"></a>Use Refresh Tokens</span></span>

<span data-ttu-id="bc89a-425">Hello токен, возвращенный Azure приложение службы аутентификации и авторизации имеет время жизни определенных один час.</span><span class="sxs-lookup"><span data-stu-id="bc89a-425">hello token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="bc89a-426">По истечении этого периода необходимо принудительную проверку подлинности пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-426">After this period, you must reauthenticate hello user.</span></span>  <span data-ttu-id="bc89a-427">В случае проверки подлинности службы приложения Azure с помощью долгоживущие маркер, который вы получили через проверку подлинности клиента потока, а затем можно принудительную проверку подлинности и авторизации с помощью hello тот же токен.</span><span class="sxs-lookup"><span data-stu-id="bc89a-427">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using hello same token.</span></span>  <span data-ttu-id="bc89a-428">В процессе создается другой токен службы приложений Azure с новым временем существования.</span><span class="sxs-lookup"><span data-stu-id="bc89a-428">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="bc89a-429">Можно также зарегистрировать toouse hello поставщика токенов обновления.</span><span class="sxs-lookup"><span data-stu-id="bc89a-429">You can also register hello provider toouse Refresh Tokens.</span></span>  <span data-ttu-id="bc89a-430">Токен обновления не всегда доступен.</span><span class="sxs-lookup"><span data-stu-id="bc89a-430">A Refresh Token is not always available.</span></span>  <span data-ttu-id="bc89a-431">В этом случае необходимо выполнить дополнительную настройку:</span><span class="sxs-lookup"><span data-stu-id="bc89a-431">Additional configuration is required:</span></span>

* <span data-ttu-id="bc89a-432">Для **Azure Active Directory**, настройте секрет клиента для hello приложения Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bc89a-432">For **Azure Active Directory**, configure a client secret for hello Azure Active Directory App.</span></span>  <span data-ttu-id="bc89a-433">Укажите секрет клиента hello в службе приложений Azure hello при настройке проверки подлинности Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bc89a-433">Specify hello client secret in hello Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="bc89a-434">При вызове метода `.login()` передайте `response_type=code id_token` как параметр:</span><span class="sxs-lookup"><span data-stu-id="bc89a-434">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="bc89a-435">Для **Google**, передайте hello `access_type=offline` как параметр:</span><span class="sxs-lookup"><span data-stu-id="bc89a-435">For **Google**, pass hello `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="bc89a-436">Для **учетную запись Майкрософт**выберите hello `wl.offline_access` области.</span><span class="sxs-lookup"><span data-stu-id="bc89a-436">For **Microsoft Account**, select hello `wl.offline_access` scope.</span></span>

<span data-ttu-id="bc89a-437">Вызовите toorefresh токене `.refreshUser()`:</span><span class="sxs-lookup"><span data-stu-id="bc89a-437">toorefresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="bc89a-438">Рекомендуется создайте фильтр, который обнаруживает 401 ответа от сервера hello и пытается токена пользователя toorefresh hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-438">As a best practice, create a filter that detects a 401 response from hello server and tries toorefresh hello user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="bc89a-439">Вход в систему с использованием клиентского потока проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="bc89a-439">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="bc89a-440">Общая процедура Hello вход с помощью проверки подлинности клиента поток выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bc89a-440">hello general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="bc89a-441">Настройка функции проверки подлинности и авторизации в службе приложений Azure, как и при серверном потоке проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bc89a-441">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="bc89a-442">Интеграция поставщика проверки подлинности hello пакета SDK для проверки подлинности tooproduce маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="bc89a-442">Integrate hello authentication provider SDK for authentication tooproduce an access token.</span></span>
* <span data-ttu-id="bc89a-443">Вызовите hello `.login()` метод следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bc89a-443">Call hello `.login()` method as follows:</span></span>

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

<span data-ttu-id="bc89a-444">Замените hello `onSuccess()` метод с независимо от кода, которые хотите toouse на успешного входа.</span><span class="sxs-lookup"><span data-stu-id="bc89a-444">Replace hello `onSuccess()` method with whatever code you wish toouse on a successful login.</span></span>  <span data-ttu-id="bc89a-445">Hello `{provider}` строка является действительным поставщиком: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, или **twitter**.</span><span class="sxs-lookup"><span data-stu-id="bc89a-445">hello `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="bc89a-446">При реализации пользовательской проверки подлинности можно также использовать тег поставщика hello нестандартной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bc89a-446">If you have implemented custom authentication, then you can also use hello custom authentication provider tag.</span></span>

### <span data-ttu-id="bc89a-447"><a name="adal"></a>Проверять подлинность пользователей с hello библиотеку проверки подлинности Active Directory (ADAL)</span><span class="sxs-lookup"><span data-stu-id="bc89a-447"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="bc89a-448">Пользователи toosign hello библиотеку проверки подлинности Active Directory (ADAL) можно использовать в приложении с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bc89a-448">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="bc89a-449">Использование имени входа потока клиента часто является более предпочтительным, чем toousing hello `loginAsync()` методы, как он обеспечивает более естественным согласованность UX и обеспечивает дополнительные настройки.</span><span class="sxs-lookup"><span data-stu-id="bc89a-449">Using a client flow login is often preferable toousing hello `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="bc89a-450">Настройте внутренний сервер мобильных приложений для входа в AAD, следующие hello [как tooconfigure приложения службы для имени входа Active Directory] [ 22] учебника.</span><span class="sxs-lookup"><span data-stu-id="bc89a-450">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="bc89a-451">Убедитесь, что необязательный шаг toocomplete hello регистрации собственного клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="bc89a-451">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="bc89a-452">Установка ADAL, изменив вашей hello tooinclude файл build.gradle следующие определения:</span><span class="sxs-lookup"><span data-stu-id="bc89a-452">Install ADAL by modifying your build.gradle file tooinclude hello following definitions:</span></span>

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. <span data-ttu-id="bc89a-453">Добавьте hello следующие приложения tooyour кода, благодаря чему hello после замены:</span><span class="sxs-lookup"><span data-stu-id="bc89a-453">Add hello following code tooyour application, making hello following replacements:</span></span>

* <span data-ttu-id="bc89a-454">Замените **вставки ЦЕНТРА здесь** hello имя клиента hello, в котором подготовлено приложения.</span><span class="sxs-lookup"><span data-stu-id="bc89a-454">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="bc89a-455">Hello формат должен быть https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="bc89a-455">hello format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="bc89a-456">Замените **вставки РЕСУРСОВ-идентификатор здесь** с Идентификатором hello клиент для мобильного приложения серверной части.</span><span class="sxs-lookup"><span data-stu-id="bc89a-456">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="bc89a-457">Можно получить идентификатор клиента hello hello **Дополнительно** в разделе **параметры Azure Active Directory** hello портала.</span><span class="sxs-lookup"><span data-stu-id="bc89a-457">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
* <span data-ttu-id="bc89a-458">Замените **вставки КЛИЕНТА-идентификатор здесь** с Идентификатором клиента hello, скопированные из собственного клиентского приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bc89a-458">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
* <span data-ttu-id="bc89a-459">Замените **вставки ПЕРЕНАПРАВЛЕНИЯ-URI здесь** с веб-узла */.auth/login/done* конечную точку, используя hello схему HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bc89a-459">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="bc89a-460">Это значение должно быть примерно слишком*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="bc89a-460">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <span data-ttu-id="bc89a-461"><a name="filters"></a>Настройка hello соединения клиент-сервер</span><span class="sxs-lookup"><span data-stu-id="bc89a-461"><a name="filters"></a>Adjust hello Client-Server Communication</span></span>

<span data-ttu-id="bc89a-462">Hello клиентского соединения — это обычно базовый HTTP-соединение с помощью hello базовый HTTP библиотеки, поставляемых вместе с hello пакета SDK для Android.</span><span class="sxs-lookup"><span data-stu-id="bc89a-462">hello Client connection is normally a basic HTTP connection using hello underlying HTTP library supplied with hello Android SDK.</span></span>  <span data-ttu-id="bc89a-463">Существует несколько причин, почему нужно toochange:</span><span class="sxs-lookup"><span data-stu-id="bc89a-463">There are several reasons why you would want toochange that:</span></span>

* <span data-ttu-id="bc89a-464">Вы хотите toouse альтернативный время ожидания tooadjust HTTP библиотеки.</span><span class="sxs-lookup"><span data-stu-id="bc89a-464">You wish toouse an alternate HTTP library tooadjust timeouts.</span></span>
* <span data-ttu-id="bc89a-465">Вы хотите tooprovide индикатор хода выполнения.</span><span class="sxs-lookup"><span data-stu-id="bc89a-465">You wish tooprovide a progress bar.</span></span>
* <span data-ttu-id="bc89a-466">Вы хотите tooadd функциональность toosupport API пользовательского заголовка.</span><span class="sxs-lookup"><span data-stu-id="bc89a-466">You wish tooadd a custom header toosupport API management functionality.</span></span>
* <span data-ttu-id="bc89a-467">Вы хотите toointercept сообщения об ошибке, чтобы можно было реализовать повторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bc89a-467">You wish toointercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="bc89a-468">Вы хотите toolog серверной запросов tooan analytics службы.</span><span class="sxs-lookup"><span data-stu-id="bc89a-468">You wish toolog backend requests tooan analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="bc89a-469">Использование альтернативной библиотеки HTTP</span><span class="sxs-lookup"><span data-stu-id="bc89a-469">Using an alternate HTTP Library</span></span>

<span data-ttu-id="bc89a-470">Вызовите hello `.setAndroidHttpClientFactory()` метод сразу после создания клиента справочной информации.</span><span class="sxs-lookup"><span data-stu-id="bc89a-470">Call hello `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="bc89a-471">Например tooset hello подключения too60 ожидания (а не по умолчанию hello 10 секунд):</span><span class="sxs-lookup"><span data-stu-id="bc89a-471">For example, tooset hello connection timeout too60 seconds (instead of hello default 10 seconds):</span></span>

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a><span data-ttu-id="bc89a-472">Реализация фильтра хода выполнения</span><span class="sxs-lookup"><span data-stu-id="bc89a-472">Implement a Progress Filter</span></span>

<span data-ttu-id="bc89a-473">Реализовав атрибут `ServiceFilter`, вы сможете настроить перехват каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="bc89a-473">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="bc89a-474">Например следующие hello обновляет предварительно созданной индикатор:</span><span class="sxs-lookup"><span data-stu-id="bc89a-474">For example, hello following updates a pre-created progress bar:</span></span>

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

<span data-ttu-id="bc89a-475">Можно присоединить этот клиент toohello фильтра следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bc89a-475">You can attach this filter toohello client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="bc89a-476">Настройка заголовков запросов</span><span class="sxs-lookup"><span data-stu-id="bc89a-476">Customize Request Headers</span></span>

<span data-ttu-id="bc89a-477">Используйте следующие hello `ServiceFilter` и присоединения hello фильтра hello так же, как hello `ProgressFilter`:</span><span class="sxs-lookup"><span data-stu-id="bc89a-477">Use hello following `ServiceFilter` and attach hello filter in hello same way as hello `ProgressFilter`:</span></span>

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <span data-ttu-id="bc89a-478"><a name="conversions"></a>Настройка автоматической сериализации</span><span class="sxs-lookup"><span data-stu-id="bc89a-478"><a name="conversions"></a>Configure Automatic Serialization</span></span>

<span data-ttu-id="bc89a-479">Можно указать стратегию преобразования, которая применяет tooevery столбца с помощью hello [gson] [ 3] API.</span><span class="sxs-lookup"><span data-stu-id="bc89a-479">You can specify a conversion strategy that applies tooevery column by using hello [gson][3] API.</span></span> <span data-ttu-id="bc89a-480">Hello Android клиентская библиотека использует [gson] [ 3] фоновом hello tooserialize Java объектов tooJSON данные перед отправкой данных hello tooAzure службы приложений.</span><span class="sxs-lookup"><span data-stu-id="bc89a-480">hello Android client library uses [gson][3] behind hello scenes tooserialize Java objects tooJSON data before hello data is sent tooAzure App Service.</span></span>  <span data-ttu-id="bc89a-481">Hello следующий код использует hello **setFieldNamingStrategy()** метод tooset hello стратегии.</span><span class="sxs-lookup"><span data-stu-id="bc89a-481">hello following code uses hello **setFieldNamingStrategy()** method tooset hello strategy.</span></span> <span data-ttu-id="bc89a-482">В этом примере приведет к удалению hello исходного символа («m»), а затем строчные hello следующего символа, для каждого имени поля.</span><span class="sxs-lookup"><span data-stu-id="bc89a-482">This example will delete hello initial character (an "m"), and then lower-case hello next character, for every field name.</span></span> <span data-ttu-id="bc89a-483">Например, он преобразует "mId" в "id".</span><span class="sxs-lookup"><span data-stu-id="bc89a-483">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="bc89a-484">Реализуйте необходимость преобразования стратегии tooreduce hello `SerializedName()` заметок на большинство полей.</span><span class="sxs-lookup"><span data-stu-id="bc89a-484">Implement a conversion strategy tooreduce hello need for `SerializedName()` annotations on most fields.</span></span>

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

<span data-ttu-id="bc89a-485">Этот код должен выполняться перед созданием ссылку мобильного клиента с помощью hello **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="bc89a-485">This code must be executed before creating a mobile client reference using hello **MobileServiceClient**.</span></span>

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[приступить к работе с проверкой подлинности]: app-service-mobile-android-get-started-users.md
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
