---
title: "Как использовать пакет SDK для мобильных приложений Azure в клиенте Android | Документация Майкрософт"
description: "Сведения об использовании пакета SDK для мобильных приложений Azure в клиенте Android."
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
ms.openlocfilehash: 4b15d024ca6d5bbafe83d321a64021aecd78c4a8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="4019b-103">Как использовать пакет SDK для мобильных приложений Azure в клиенте Android</span><span class="sxs-lookup"><span data-stu-id="4019b-103">How to use the Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="4019b-104">В этом руководстве показано, как использовать пакет SDK для мобильных приложений для клиентов Android, чтобы реализовать распространенные сценарии, в том числе:</span><span class="sxs-lookup"><span data-stu-id="4019b-104">This guide shows you how to use the Android client SDK for Mobile Apps to implement common scenarios, such as:</span></span>

* <span data-ttu-id="4019b-105">запрос данных (вставка, обновление и удаления);</span><span class="sxs-lookup"><span data-stu-id="4019b-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="4019b-106">аутентификация;</span><span class="sxs-lookup"><span data-stu-id="4019b-106">Authentication.</span></span>
* <span data-ttu-id="4019b-107">обработка ошибок;</span><span class="sxs-lookup"><span data-stu-id="4019b-107">Handling errors.</span></span>
* <span data-ttu-id="4019b-108">настройка клиента.</span><span class="sxs-lookup"><span data-stu-id="4019b-108">Customizing the client.</span></span>

<span data-ttu-id="4019b-109">В этом руководстве описано использование клиентского пакета Android SDK.</span><span class="sxs-lookup"><span data-stu-id="4019b-109">This guide focuses on the client-side Android SDK.</span></span>  <span data-ttu-id="4019b-110">См. дополнительные сведения о серверных пакетах SDK для мобильных приложений, включая сведения о [работе с серверными пакетами SDK для .NET][10] и [использовании серверного пакета SDK для Node.js][11].</span><span class="sxs-lookup"><span data-stu-id="4019b-110">To learn more about the server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How to use the Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="4019b-111">Справочная документация</span><span class="sxs-lookup"><span data-stu-id="4019b-111">Reference Documentation</span></span>

<span data-ttu-id="4019b-112">[Справочник Javadocs по API][12] клиентской библиотеки Android см. на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="4019b-112">You can find the [Javadocs API reference][12] for the Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="4019b-113">Поддерживаемые платформы</span><span class="sxs-lookup"><span data-stu-id="4019b-113">Supported Platforms</span></span>

<span data-ttu-id="4019b-114">Пакет SDK для мобильных приложений Azure в клиенте Android поддерживает API уровней 19–24 (от KitKat до Nougat). Это применяется к телефонам и планшетам.</span><span class="sxs-lookup"><span data-stu-id="4019b-114">The Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="4019b-115">В процессе проверки подлинности, в частности, применяется общий метод сбора учетных данных, используемый на веб-платформах.</span><span class="sxs-lookup"><span data-stu-id="4019b-115">Authentication, in particular, utilizes a common web framework approach to gather credentials.</span></span>  <span data-ttu-id="4019b-116">Серверный поток проверки подлинности не работает на устройствах малого форм-фактора, таких как часы.</span><span class="sxs-lookup"><span data-stu-id="4019b-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="4019b-117">Настройка и необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="4019b-117">Setup and Prerequisites</span></span>

<span data-ttu-id="4019b-118">Ознакомьтесь с [кратким учебником по мобильным приложениям](app-service-mobile-android-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="4019b-118">Complete the [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="4019b-119">Выполнение данной задачи гарантирует, что будут соблюдены все предварительные требования для разработки мобильных приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="4019b-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="4019b-120">Кроме того, этот краткий учебник поможет вам настроить учетную запись и создать свою первую серверную часть мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="4019b-120">The Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="4019b-121">Если вы решите не изучать краткий учебник, то выполните следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="4019b-121">If you decide not to complete the Quickstart tutorial, complete the following tasks:</span></span>

* <span data-ttu-id="4019b-122">[Создайте серверную часть мобильного приложения][13] для использования с приложением Android.</span><span class="sxs-lookup"><span data-stu-id="4019b-122">[create a Mobile App backend][13] to use with your Android app.</span></span>
* <span data-ttu-id="4019b-123">В Android Studio [обновите файлы сборки Gradle](#gradle-build).</span><span class="sxs-lookup"><span data-stu-id="4019b-123">In Android Studio, [update the Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="4019b-124">[Включение разрешение INTERNET](#enable-internet).</span><span class="sxs-lookup"><span data-stu-id="4019b-124">[Enable internet permission](#enable-internet).</span></span>

### <span data-ttu-id="4019b-125"><a name="gradle-build"></a>Обновление файла сборки Gradle</span><span class="sxs-lookup"><span data-stu-id="4019b-125"><a name="gradle-build"></a>Update the Gradle build file</span></span>

<span data-ttu-id="4019b-126">Измените оба файла **build.gradle** :</span><span class="sxs-lookup"><span data-stu-id="4019b-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="4019b-127">Добавьте следующий код в файл *build.gradle* уровня **Project** внутри тега *buildscript*.</span><span class="sxs-lookup"><span data-stu-id="4019b-127">Add this code to the *Project* level **build.gradle** file inside the *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="4019b-128">Добавьте следующий код в файл *build.gradle* уровня **Module app** внутри тега *dependencies*.</span><span class="sxs-lookup"><span data-stu-id="4019b-128">Add this code to the *Module app* level **build.gradle** file inside the *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    <span data-ttu-id="4019b-129">Сейчас последней версией является 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="4019b-129">Currently the latest version is 3.3.0.</span></span> <span data-ttu-id="4019b-130">Поддерживаемые версии см. на сайте [Bintray][14].</span><span class="sxs-lookup"><span data-stu-id="4019b-130">The supported versions are listed [on bintray][14].</span></span>

### <span data-ttu-id="4019b-131"><a name="enable-internet"></a>Включение разрешения INTERNET</span><span class="sxs-lookup"><span data-stu-id="4019b-131"><a name="enable-internet"></a>Enable internet permission</span></span>

<span data-ttu-id="4019b-132">Для доступа к Azure вам нужно включить для приложения разрешение INTERNET.</span><span class="sxs-lookup"><span data-stu-id="4019b-132">To access Azure, your app must have the INTERNET permission enabled.</span></span> <span data-ttu-id="4019b-133">Если оно не включено, добавьте следующую строку кода в файл **AndroidManifest.xml** :</span><span class="sxs-lookup"><span data-stu-id="4019b-133">If it's not already enabled, add the following line of code to your **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="4019b-134">Создание подключения клиента</span><span class="sxs-lookup"><span data-stu-id="4019b-134">Create a Client Connection</span></span>

<span data-ttu-id="4019b-135">Служба мобильных приложений Azure предоставляет четыре функции для мобильных приложений:</span><span class="sxs-lookup"><span data-stu-id="4019b-135">Azure Mobile Apps provides four functions to your mobile application:</span></span>

* <span data-ttu-id="4019b-136">доступ к данным и их синхронизация в автономном режиме со службой мобильных приложений Azure;</span><span class="sxs-lookup"><span data-stu-id="4019b-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="4019b-137">вызов настраиваемых API-интерфейсов, написанных с использованием пакета SDK для сервера мобильных приложений Azure;</span><span class="sxs-lookup"><span data-stu-id="4019b-137">Call Custom APIs written with the Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="4019b-138">проверка подлинности с помощью функции проверки подлинности и авторизации в службе приложений Azure;</span><span class="sxs-lookup"><span data-stu-id="4019b-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="4019b-139">регистрация push-уведомлений в Центрах уведомлений.</span><span class="sxs-lookup"><span data-stu-id="4019b-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="4019b-140">Чтобы использовать каждую из этих функций, сначала необходимо создать объект `MobileServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="4019b-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="4019b-141">В мобильном клиенте необходимо создать только один объект `MobileServiceClient` (то есть следует использовать шаблон с одним элементом).</span><span class="sxs-lookup"><span data-stu-id="4019b-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="4019b-142">Чтобы создать объект `MobileServiceClient`, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="4019b-142">To create a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with the Site URL
    this);                  // Your application Context
```

<span data-ttu-id="4019b-143">Параметр `<MobileAppUrl>` — это строка или URL-адрес, указывающий на серверную часть мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="4019b-143">The `<MobileAppUrl>` is either a string or a URL object that points to your mobile backend.</span></span>  <span data-ttu-id="4019b-144">Если серверная часть мобильного приложения расположена в службе приложений Azure, используйте безопасную версию `https://` URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="4019b-144">If you are using Azure App Service to host your mobile backend, then ensure you use the secure `https://` version of the URL.</span></span>

<span data-ttu-id="4019b-145">Клиенту требуется доступ к классу Activity или Context. В приведенном примере кода за это отвечает параметр `this`.</span><span class="sxs-lookup"><span data-stu-id="4019b-145">The client also requires access to the Activity or Context - the `this` parameter in the example.</span></span>  <span data-ttu-id="4019b-146">Создание объекта MobileServiceClient должно начаться в методе `onCreate()` класса Activity, указанного в файле `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="4019b-146">The MobileServiceClient construction should happen within the `onCreate()` method of the Activity referenced in the `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="4019b-147">Мы советуем абстрагировать связь сервера в собственный класс (шаблон с одним элементом).</span><span class="sxs-lookup"><span data-stu-id="4019b-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="4019b-148">В этом случае следует передавать класс Activity в конструктор, чтобы соответствующим образом настроить службу.</span><span class="sxs-lookup"><span data-stu-id="4019b-148">In this case, you should pass the Activity within the constructor to appropriately configure the service.</span></span>  <span data-ttu-id="4019b-149">Например:</span><span class="sxs-lookup"><span data-stu-id="4019b-149">For example:</span></span>

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

<span data-ttu-id="4019b-150">Теперь вы можете вызвать `AzureServiceAdapter.Initialize(this);` в методе `onCreate()` основного действия.</span><span class="sxs-lookup"><span data-stu-id="4019b-150">You can now call `AzureServiceAdapter.Initialize(this);` in the `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="4019b-151">Другие методы, которым нужен доступ к клиенту, используют `AzureServiceAdapter.getInstance();`, чтобы получить ссылку на адаптер службы.</span><span class="sxs-lookup"><span data-stu-id="4019b-151">Any other methods needing access to the client use `AzureServiceAdapter.getInstance();` to obtain a reference to the service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="4019b-152">Операции с данными</span><span class="sxs-lookup"><span data-stu-id="4019b-152">Data Operations</span></span>

<span data-ttu-id="4019b-153">Ядро пакета SDK для мобильных приложений Azure предоставляет доступ к данным, сохраненным в SQL Azure в серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="4019b-153">The core of the Azure Mobile Apps SDK is to provide access to data stored within SQL Azure on the Mobile App backend.</span></span>  <span data-ttu-id="4019b-154">Доступ к этим данным можно получить, используя классы со строгим типом (предпочтительный способ) или нетипизированные запросы (нерекомендуемый способ).</span><span class="sxs-lookup"><span data-stu-id="4019b-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="4019b-155">Основная часть этого раздела посвящена использованию классов со строгим типом.</span><span class="sxs-lookup"><span data-stu-id="4019b-155">The bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="4019b-156">Определение клиентских классов данных</span><span class="sxs-lookup"><span data-stu-id="4019b-156">Define client data classes</span></span>

<span data-ttu-id="4019b-157">Для доступа к данным из таблиц SQL Azure вам нужно определить клиентские классы данных, которые соответствуют таблицам в серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="4019b-157">To access data from SQL Azure tables, define client data classes that correspond to the tables in the Mobile App backend.</span></span> <span data-ttu-id="4019b-158">В примерах этого раздела используется таблица с именем **MyDataTable**, которая содержит следующие столбцы:</span><span class="sxs-lookup"><span data-stu-id="4019b-158">Examples in this topic assume a table named **MyDataTable**, which has the following columns:</span></span>

* <span data-ttu-id="4019b-159">id</span><span class="sxs-lookup"><span data-stu-id="4019b-159">id</span></span>
* <span data-ttu-id="4019b-160">текст</span><span class="sxs-lookup"><span data-stu-id="4019b-160">text</span></span>
* <span data-ttu-id="4019b-161">complete</span><span class="sxs-lookup"><span data-stu-id="4019b-161">complete</span></span>

<span data-ttu-id="4019b-162">Соответствующий типизированный клиентский объект находится в файле **MyDataTable.java**:</span><span class="sxs-lookup"><span data-stu-id="4019b-162">The corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="4019b-163">Включите методы Getter или Setter в каждое добавленное поле.</span><span class="sxs-lookup"><span data-stu-id="4019b-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="4019b-164">Если таблица SQL Azure содержит больше столбцов, в этот класс необходимо добавить соответствующие поля.</span><span class="sxs-lookup"><span data-stu-id="4019b-164">If your SQL Azure table contains more columns, you would add the corresponding fields to this class.</span></span>  <span data-ttu-id="4019b-165">Например, если объект переноса данных (DTO) содержал целочисленный столбец Priority, то вы можете добавить это поле вместе с методами получения и задания.</span><span class="sxs-lookup"><span data-stu-id="4019b-165">For example, if the DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

```java
private Integer priority;

/**
* Returns the item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets the item priority
*
* @param priority
*            priority to set
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

<span data-ttu-id="4019b-166">См. дополнительные сведения о создании дополнительных таблиц в серверной части мобильных приложений, включая сведения об [определении контроллера таблиц][15] (серверная часть .NET) и [определении таблиц с помощью динамической схемы][16] (серверная часть Node.js).</span><span class="sxs-lookup"><span data-stu-id="4019b-166">To learn how to create additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="4019b-167">В таблице серверной части мобильных приложений Azure определено пять специальных полей, четыре из которых доступны клиентам:</span><span class="sxs-lookup"><span data-stu-id="4019b-167">An Azure Mobile Apps backend table defines five special fields, four of which are available to clients:</span></span>

* <span data-ttu-id="4019b-168">`String id` — глобальный уникальный идентификатор записи.</span><span class="sxs-lookup"><span data-stu-id="4019b-168">`String id`: The globally unique ID for the record.</span></span>  <span data-ttu-id="4019b-169">Мы советуем сделать этот идентификатор представлением строки объекта [UUID][17].</span><span class="sxs-lookup"><span data-stu-id="4019b-169">As a best practice, make the id the String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="4019b-170">`DateTimeOffset updatedAt` — дата и время последнего обновления.</span><span class="sxs-lookup"><span data-stu-id="4019b-170">`DateTimeOffset updatedAt`: The date/time of the last update.</span></span>  <span data-ttu-id="4019b-171">Поле updatedAt устанавливается на сервере и никогда не должно задаваться в коде клиента.</span><span class="sxs-lookup"><span data-stu-id="4019b-171">The updatedAt field is set by the server and should never be set by your client code.</span></span>
* <span data-ttu-id="4019b-172">`DateTimeOffset createdAt` — дата и время создания объекта.</span><span class="sxs-lookup"><span data-stu-id="4019b-172">`DateTimeOffset createdAt`: The date/time that the object was created.</span></span>  <span data-ttu-id="4019b-173">Поле createdAt устанавливается на сервере и никогда не должно задаваться в коде клиента.</span><span class="sxs-lookup"><span data-stu-id="4019b-173">The createdAt field is set by the server and should never be set by your client code.</span></span>
* <span data-ttu-id="4019b-174">`byte[] version` — обычно это поле представлено в виде строки. Версия также устанавливается на сервере.</span><span class="sxs-lookup"><span data-stu-id="4019b-174">`byte[] version`: Normally represented as a string, the version is also set by the server.</span></span>
* <span data-ttu-id="4019b-175">`boolean deleted` — указывает, что запись была удалена, но еще не очищена.</span><span class="sxs-lookup"><span data-stu-id="4019b-175">`boolean deleted`: Indicates that the record has been deleted but not purged yet.</span></span>  <span data-ttu-id="4019b-176">Не используйте `deleted` в качестве свойства класса.</span><span class="sxs-lookup"><span data-stu-id="4019b-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="4019b-177">Поле `id` является обязательным.</span><span class="sxs-lookup"><span data-stu-id="4019b-177">The `id` field is required.</span></span>  <span data-ttu-id="4019b-178">Поля `updatedAt` и `version` используются при синхронизации в автономном режиме (для добавочной синхронизации и устранения конфликтов соответственно).</span><span class="sxs-lookup"><span data-stu-id="4019b-178">The `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="4019b-179">`createdAt` — это эталонное поле. Оно не используется клиентом.</span><span class="sxs-lookup"><span data-stu-id="4019b-179">The `createdAt` field is a reference field and is not used by the client.</span></span>  <span data-ttu-id="4019b-180">Имена свойств можно передавать по сети. Они не изменяются.</span><span class="sxs-lookup"><span data-stu-id="4019b-180">The names are "across-the-wire" names of the properties and are not adjustable.</span></span>  <span data-ttu-id="4019b-181">Но вы можете создать сопоставление между своим объектом и этими именами, используя библиотеку [gson][3].</span><span class="sxs-lookup"><span data-stu-id="4019b-181">However, you can create a mapping between your object and the "across-the-wire" names using the [gson][3] library.</span></span>  <span data-ttu-id="4019b-182">Например:</span><span class="sxs-lookup"><span data-stu-id="4019b-182">For example:</span></span>

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

### <a name="create-a-table-reference"></a><span data-ttu-id="4019b-183">Создание ссылки на таблицу</span><span class="sxs-lookup"><span data-stu-id="4019b-183">Create a Table Reference</span></span>

<span data-ttu-id="4019b-184">Для доступа к таблице сначала создайте объект [MobileServiceTable][8], вызвав метод **getTable** объекта [MobileServiceClient][9].</span><span class="sxs-lookup"><span data-stu-id="4019b-184">To access a table, first create a [MobileServiceTable][8] object by calling the **getTable** method on the [MobileServiceClient][9].</span></span>  <span data-ttu-id="4019b-185">У этого метода две перегрузки.</span><span class="sxs-lookup"><span data-stu-id="4019b-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="4019b-186">В следующем коде **mClient** — это ссылка на объект MobileServiceClient.</span><span class="sxs-lookup"><span data-stu-id="4019b-186">In the following code, **mClient** is a reference to your MobileServiceClient object.</span></span>  <span data-ttu-id="4019b-187">Первая перегрузка используется при быстром запуске, когда имя класса и имя таблицы одинаковы.</span><span class="sxs-lookup"><span data-stu-id="4019b-187">The first overload is used where the class name and the table name are the same, and is the one used in the Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="4019b-188">Вторая перегрузка используется, когда имя таблицы отличается от имени типа (первый параметр — это имя таблицы).</span><span class="sxs-lookup"><span data-stu-id="4019b-188">The second overload is used when the table name is different from the class name: the first parameter is the table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <span data-ttu-id="4019b-189"><a name="query"></a>Запрос таблицы серверной части</span><span class="sxs-lookup"><span data-stu-id="4019b-189"><a name="query"></a>Query a Backend Table</span></span>

<span data-ttu-id="4019b-190">Сначала получите ссылку на таблицу.</span><span class="sxs-lookup"><span data-stu-id="4019b-190">First, obtain a table reference.</span></span>  <span data-ttu-id="4019b-191">Затем выполните запрос к ссылке на таблицу.</span><span class="sxs-lookup"><span data-stu-id="4019b-191">Then execute a query on the table reference.</span></span>  <span data-ttu-id="4019b-192">Запрос сочетает в себе следующее:</span><span class="sxs-lookup"><span data-stu-id="4019b-192">A query is any combination of:</span></span>

* <span data-ttu-id="4019b-193">[предложение фильтра](#filtering) `.where()`;</span><span class="sxs-lookup"><span data-stu-id="4019b-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="4019b-194">[предложение упорядочения](#sorting) `.orderBy()`;</span><span class="sxs-lookup"><span data-stu-id="4019b-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="4019b-195">[предложение выбора поля](#selection) `.select()`;</span><span class="sxs-lookup"><span data-stu-id="4019b-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="4019b-196">`.skip()` и `.top()` для [страничных результатов](#paging).</span><span class="sxs-lookup"><span data-stu-id="4019b-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="4019b-197">Предложения должны располагаться в таком же порядке.</span><span class="sxs-lookup"><span data-stu-id="4019b-197">The clauses must be presented in the preceding order.</span></span>

### <span data-ttu-id="4019b-198"><a name="filter"></a> Фильтрация результатов</span><span class="sxs-lookup"><span data-stu-id="4019b-198"><a name="filter"></a> Filtering Results</span></span>

<span data-ttu-id="4019b-199">Запрос выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4019b-199">The general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts the async into a sync result
```

<span data-ttu-id="4019b-200">Приведенный выше пример возвращает все результаты (вплоть до максимального размера страницы, заданного на сервере).</span><span class="sxs-lookup"><span data-stu-id="4019b-200">The preceding example returns all results (up to the maximum page size set by the server).</span></span>  <span data-ttu-id="4019b-201">Метод `.execute()` выполняет запрос в серверной части.</span><span class="sxs-lookup"><span data-stu-id="4019b-201">The `.execute()` method executes the query on the backend.</span></span>  <span data-ttu-id="4019b-202">Перед передачей в серверную часть мобильных приложений этот запрос преобразовывается в запрос [OData v3][19].</span><span class="sxs-lookup"><span data-stu-id="4019b-202">The query is converted to an [OData v3][19] query before transmission to the Mobile Apps backend.</span></span>  <span data-ttu-id="4019b-203">После получения этот запрос преобразовывается в серверной части в инструкцию SQL перед выполнением его на экземпляре SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4019b-203">On receipt, the Mobile Apps backend converts the query into an SQL statement before executing it on the SQL Azure instance.</span></span>  <span data-ttu-id="4019b-204">Так как сетевая активность занимает некоторое время, метод `.execute()` возвращает [`ListenableFuture<E>`][18].</span><span class="sxs-lookup"><span data-stu-id="4019b-204">Since network activity takes some time, The `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <span data-ttu-id="4019b-205"><a name="filtering"></a>Фильтрация возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="4019b-205"><a name="filtering"></a>Filter returned data</span></span>

<span data-ttu-id="4019b-206">Следующий запрос при выполнении возвращает все элементы из таблицы **ToDoItem**, где для переменной **complete** задано значение **false**.</span><span class="sxs-lookup"><span data-stu-id="4019b-206">The following query execution returns all items from the **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="4019b-207">**mToDoTable** — это ссылка на таблицу мобильной службы, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="4019b-207">**mToDoTable** is the reference to the mobile service table that we created previously.</span></span>

<span data-ttu-id="4019b-208">Для определения фильтра вызовите метод **where** для ссылки на таблицу.</span><span class="sxs-lookup"><span data-stu-id="4019b-208">Define a filter using the **where** method call on the table reference.</span></span> <span data-ttu-id="4019b-209">После метода **where** вызывается метод **field**, а затем — метод, который определяет логический предикат.</span><span class="sxs-lookup"><span data-stu-id="4019b-209">The **where** method is followed by a **field** method followed by a method that specifies the logical predicate.</span></span> <span data-ttu-id="4019b-210">Возможные методы предиката: **eq** (равно), **ne** (не равно), **gt** (больше), **ge** (больше или равно), **lt** (меньше), **le** (меньше или равно).</span><span class="sxs-lookup"><span data-stu-id="4019b-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="4019b-211">Эти методы позволяют сравнивать числовые и строковые поля с указанными значениями.</span><span class="sxs-lookup"><span data-stu-id="4019b-211">These methods let you compare number and string fields to specific values.</span></span>

<span data-ttu-id="4019b-212">Фильтровать данные можно по датам.</span><span class="sxs-lookup"><span data-stu-id="4019b-212">You can filter on dates.</span></span> <span data-ttu-id="4019b-213">Следующие методы позволяют сравнить поле даты целиком или частично: **year**, **month**, **day**, **hour**, **minute** и **second**.</span><span class="sxs-lookup"><span data-stu-id="4019b-213">The following methods let you compare the entire date field or parts of the date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="4019b-214">В следующем примере добавляется фильтр для элементов, *дата выполнения* которых равна 2013.</span><span class="sxs-lookup"><span data-stu-id="4019b-214">The following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="4019b-215">Следующие методы поддерживают применение сложных фильтров к строковым полям: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim** и **length**.</span><span class="sxs-lookup"><span data-stu-id="4019b-215">The following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="4019b-216">В следующем примере отфильтровываются строки таблицы, в которых столбец *text* начинается с PRI0.</span><span class="sxs-lookup"><span data-stu-id="4019b-216">The following example filters for table rows where the *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="4019b-217">Следующие методы оператора поддерживают использование числовых полей: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling** и **round**.</span><span class="sxs-lookup"><span data-stu-id="4019b-217">The following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="4019b-218">В следующем примере отфильтровываются строки таблицы, в которых значение **duration** является четным числом.</span><span class="sxs-lookup"><span data-stu-id="4019b-218">The following example filters for table rows where the **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="4019b-219">Предикаты можно объединять с помощью логических методов **and**, **or** и **not**.</span><span class="sxs-lookup"><span data-stu-id="4019b-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="4019b-220">В следующем примере объединяются два приведенных выше примера.</span><span class="sxs-lookup"><span data-stu-id="4019b-220">The following example combines two of the preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="4019b-221">Группирование и вложение логических операторов.</span><span class="sxs-lookup"><span data-stu-id="4019b-221">Group and nest logical operators:</span></span>

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

<span data-ttu-id="4019b-222">Более подробное описание и примеры фильтрации см. в статье [Exploring the richness of the Mobile Services Android client query model][20] (Исследование возможностей модели запросов клиента мобильных служб Android).</span><span class="sxs-lookup"><span data-stu-id="4019b-222">For more detailed discussion and examples of filtering, see [Exploring the richness of the Android client query model][20].</span></span>

### <span data-ttu-id="4019b-223"><a name="sorting"></a>Сортировка возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="4019b-223"><a name="sorting"></a>Sort returned data</span></span>

<span data-ttu-id="4019b-224">Следующий код возвращает все элементы из таблицы **ToDoItem** , упорядоченные по полю *text* .</span><span class="sxs-lookup"><span data-stu-id="4019b-224">The following code returns all items from a table of **ToDoItems** sorted ascending by the *text* field.</span></span> <span data-ttu-id="4019b-225">*mToDoTable* — это ссылка на таблицу серверной части, созданную ранее:</span><span class="sxs-lookup"><span data-stu-id="4019b-225">*mToDoTable* is the reference to the backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="4019b-226">Первый параметр метода **orderBy** — это строка, совпадающая с именем поля, по которому выполняется сортировка.</span><span class="sxs-lookup"><span data-stu-id="4019b-226">The first parameter of the **orderBy** method is a string equal to the name of the field on which to sort.</span></span> <span data-ttu-id="4019b-227">Второй параметр использует перечисление **QueryOrder** , чтобы определить порядок сортировки (по возрастанию или убыванию).</span><span class="sxs-lookup"><span data-stu-id="4019b-227">The second parameter uses the **QueryOrder** enumeration to specify whether to sort ascending or descending.</span></span>  <span data-ttu-id="4019b-228">Если используется фильтрация с помощью метода ***where***, то метод ***where*** необходимо вызывать до метода ***orderBy***.</span><span class="sxs-lookup"><span data-stu-id="4019b-228">If you are filtering using the ***where*** method, the ***where*** method must be invoked before the ***orderBy*** method.</span></span>

### <span data-ttu-id="4019b-229"><a name="selection"></a>Выбор определенных столбцов</span><span class="sxs-lookup"><span data-stu-id="4019b-229"><a name="selection"></a>Select specific columns</span></span>

<span data-ttu-id="4019b-230">В следующем фрагменте кода показано, как получить все элементы из таблицы **ToDoItems**, в которой отображаются только поля **complete** и **text**.</span><span class="sxs-lookup"><span data-stu-id="4019b-230">The following code illustrates how to return all items from a table of **ToDoItems**, but only displays the **complete** and **text** fields.</span></span> <span data-ttu-id="4019b-231">**mToDoTable** — это ссылка на таблицу серверной части, созданную ранее:</span><span class="sxs-lookup"><span data-stu-id="4019b-231">**mToDoTable** is the reference to the backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="4019b-232">Параметры функции select являются строковыми именами столбцов таблицы, которые требуется вернуть.</span><span class="sxs-lookup"><span data-stu-id="4019b-232">The parameters to the select function are the string names of the table's columns that you want to return.</span></span>  <span data-ttu-id="4019b-233">Метод **select** должен следовать за такими методами, как **where** и **orderBy**.</span><span class="sxs-lookup"><span data-stu-id="4019b-233">The **select** method needs to follow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="4019b-234">Затем можно вызывать такие методы разбивки на страницы, как **skip** и **top**.</span><span class="sxs-lookup"><span data-stu-id="4019b-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <span data-ttu-id="4019b-235"><a name="paging"></a>Возврат данных на страницах</span><span class="sxs-lookup"><span data-stu-id="4019b-235"><a name="paging"></a>Return data in pages</span></span>

<span data-ttu-id="4019b-236">Данные **всегда** возвращаются на страницах.</span><span class="sxs-lookup"><span data-stu-id="4019b-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="4019b-237">Максимальное число возвращаемых записей устанавливается на сервере.</span><span class="sxs-lookup"><span data-stu-id="4019b-237">The maximum number of records returned is set by the server.</span></span>  <span data-ttu-id="4019b-238">Если клиент запрашивает большее число записей, сервер возвращает только установленное максимальное количество записей.</span><span class="sxs-lookup"><span data-stu-id="4019b-238">If the client requests more records, then the server returns the maximum number of records.</span></span>  <span data-ttu-id="4019b-239">По умолчанию максимальный размер страницы на сервере составляет 50 записей.</span><span class="sxs-lookup"><span data-stu-id="4019b-239">By default, the maximum page size on the server is 50 records.</span></span>

<span data-ttu-id="4019b-240">Первый пример показывает, как выбрать пять верхних элементов из таблицы.</span><span class="sxs-lookup"><span data-stu-id="4019b-240">The first example shows how to select the top five items from a table.</span></span> <span data-ttu-id="4019b-241">Следующий запрос возвращает элементы из таблицы **ToDoItem**.</span><span class="sxs-lookup"><span data-stu-id="4019b-241">The query returns the items from a table of **ToDoItems**.</span></span> <span data-ttu-id="4019b-242">**mToDoTable** — это ссылка на таблицу серверной части, созданную ранее:</span><span class="sxs-lookup"><span data-stu-id="4019b-242">**mToDoTable** is the reference to the backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="4019b-243">Приведенный ниже запрос пропускает первые пять элементов, возвращая следующие пять элементов.</span><span class="sxs-lookup"><span data-stu-id="4019b-243">Here's a query that skips the first five items, and then returns the next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="4019b-244">Если вы хотите получить все записи в таблице, реализуйте код для выполнения итерации по всех страницах:</span><span class="sxs-lookup"><span data-stu-id="4019b-244">If you wish to get all records in a table, implement code to iterate over all pages:</span></span>

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

<span data-ttu-id="4019b-245">При выполнении запроса всех записей с помощью этого метода создается как минимум два запроса к серверной части мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="4019b-245">A request for all records using this method creates a minimum of two requests to the Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="4019b-246">Выбор правильного размера страницы — это соотношение между использованием памяти во время выполнения запроса, потреблением пропускной способности и задержкой получения всех данных.</span><span class="sxs-lookup"><span data-stu-id="4019b-246">Choosing the right page size is a balance between memory usage while the request is happening, bandwidth usage and delay in receiving the data completely.</span></span>  <span data-ttu-id="4019b-247">Значение по умолчанию (50 записей) подходит для всех устройств.</span><span class="sxs-lookup"><span data-stu-id="4019b-247">The default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="4019b-248">Если вы работаете на устройствах с большим объемом памяти, увеличьте это значение до 500.</span><span class="sxs-lookup"><span data-stu-id="4019b-248">If you exclusively operate on larger memory devices, increase up to 500.</span></span>  <span data-ttu-id="4019b-249">Мы пришли к выводу, что при увеличении размера страницы до более 500 записей возникают недопустимые задержки и большие проблемы с памятью.</span><span class="sxs-lookup"><span data-stu-id="4019b-249">We have found that increasing the page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <span data-ttu-id="4019b-250"><a name="chaining"></a>Практическое руководство. Объединение методов запросов</span><span class="sxs-lookup"><span data-stu-id="4019b-250"><a name="chaining"></a>How to: Concatenate query methods</span></span>

<span data-ttu-id="4019b-251">Методы, используемые в запросах таблиц серверной части, можно сцепить.</span><span class="sxs-lookup"><span data-stu-id="4019b-251">The methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="4019b-252">Цепочка методов запроса позволяет, например, выбирать определенные столбцы отфильтрованных строк, которые сортируются и разбиваются на страницы.</span><span class="sxs-lookup"><span data-stu-id="4019b-252">Chaining query methods allows you to select specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="4019b-253">Можно создавать сложные логические фильтры.</span><span class="sxs-lookup"><span data-stu-id="4019b-253">You can create complex logical filters.</span></span>  <span data-ttu-id="4019b-254">Каждый метод запроса возвращает объект Query.</span><span class="sxs-lookup"><span data-stu-id="4019b-254">Each query method returns a Query object.</span></span> <span data-ttu-id="4019b-255">Чтобы завершить серию методов и фактически выполнить запрос, вызовите метод **execute** .</span><span class="sxs-lookup"><span data-stu-id="4019b-255">To end the series of methods and actually run the query, call the **execute** method.</span></span> <span data-ttu-id="4019b-256">Например:</span><span class="sxs-lookup"><span data-stu-id="4019b-256">For example:</span></span>

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

<span data-ttu-id="4019b-257">Методы запроса в цепочке должны быть упорядочены следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4019b-257">The chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="4019b-258">методы фильтрации (**где**);</span><span class="sxs-lookup"><span data-stu-id="4019b-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="4019b-259">методы сортировки (**orderBy**);</span><span class="sxs-lookup"><span data-stu-id="4019b-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="4019b-260">методы выборки (**выберите**);</span><span class="sxs-lookup"><span data-stu-id="4019b-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="4019b-261">методы разбиения по страницам (**skip** и **top**).</span><span class="sxs-lookup"><span data-stu-id="4019b-261">paging (**skip** and **top**) methods.</span></span>

## <span data-ttu-id="4019b-262"><a name="binding"></a>Привязка данных к пользовательскому интерфейсу</span><span class="sxs-lookup"><span data-stu-id="4019b-262"><a name="binding"></a>Bind data to the user interface</span></span>

<span data-ttu-id="4019b-263">Привязка данных состоит из трех компонентов:</span><span class="sxs-lookup"><span data-stu-id="4019b-263">Data binding involves three components:</span></span>

* <span data-ttu-id="4019b-264">источник данных;</span><span class="sxs-lookup"><span data-stu-id="4019b-264">The data source</span></span>
* <span data-ttu-id="4019b-265">макет экрана;</span><span class="sxs-lookup"><span data-stu-id="4019b-265">The screen layout</span></span>
* <span data-ttu-id="4019b-266">адаптер, который связывает два эти компонента.</span><span class="sxs-lookup"><span data-stu-id="4019b-266">The adapter that ties the two together.</span></span>

<span data-ttu-id="4019b-267">В нашем примере кода мы возвращаем данные из таблицы **ToDoItem** SQL Azure мобильных приложений в массив.</span><span class="sxs-lookup"><span data-stu-id="4019b-267">In our sample code, we return the data from the Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="4019b-268">Это действие типично для приложений для обработки данных.</span><span class="sxs-lookup"><span data-stu-id="4019b-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="4019b-269">Запросы к базе данных часто возвращают набор строк, которые клиент получает в виде списка или массива.</span><span class="sxs-lookup"><span data-stu-id="4019b-269">Database queries often return a collection of rows that the client gets in a list or array.</span></span> <span data-ttu-id="4019b-270">В этом примере массив является источником данных.</span><span class="sxs-lookup"><span data-stu-id="4019b-270">In this sample, the array is the data source.</span></span>  <span data-ttu-id="4019b-271">Код указывает макет экрана, который определяет представление данных, отображаемых на устройстве.</span><span class="sxs-lookup"><span data-stu-id="4019b-271">The code specifies a screen layout that defines the view of the data that appears on the device.</span></span>  <span data-ttu-id="4019b-272">Два компонента соединяются адаптером, который в этом коде является расширением класса **ArrayAdapter&lt;ToDoItem&gt;**.</span><span class="sxs-lookup"><span data-stu-id="4019b-272">The two are bound together with an adapter, which in this code is an extension of the **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <span data-ttu-id="4019b-273"><a name="layout"></a>Определение макета</span><span class="sxs-lookup"><span data-stu-id="4019b-273"><a name="layout"></a>Define the Layout</span></span>

<span data-ttu-id="4019b-274">Макет определяется несколькими фрагментами XML-кода.</span><span class="sxs-lookup"><span data-stu-id="4019b-274">The layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="4019b-275">С учетом существующего макета приведенный ниже код представляет объект **ListView** , который требуется заполнить данными с сервера.</span><span class="sxs-lookup"><span data-stu-id="4019b-275">Given an existing layout, the following code represents the **ListView** we want to populate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="4019b-276">В приведенном выше коде атрибут *listitem* указывает идентификатор макета для отдельной строки в списке.</span><span class="sxs-lookup"><span data-stu-id="4019b-276">In the preceding code, the *listitem* attribute specifies the id of the layout for an individual row in the list.</span></span> <span data-ttu-id="4019b-277">Этот код задает флажок и связанный с ним текст, при этом экземпляры создаются для каждого элемента в списке.</span><span class="sxs-lookup"><span data-stu-id="4019b-277">This code specifies a check box and its associated text and gets instantiated once for each item in the list.</span></span> <span data-ttu-id="4019b-278">В этом макете поле **id** не отображается. В более сложном макете указываются дополнительные поля на экране.</span><span class="sxs-lookup"><span data-stu-id="4019b-278">This layout does not display the **id** field, and a more complex layout would specify additional fields in the display.</span></span> <span data-ttu-id="4019b-279">Этот код находится в файле **row_list_to_do.xml**.</span><span class="sxs-lookup"><span data-stu-id="4019b-279">This code is in the **row_list_to_do.xml** file.</span></span>

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

#### <span data-ttu-id="4019b-280"><a name="adapter"></a>Определение адаптера</span><span class="sxs-lookup"><span data-stu-id="4019b-280"><a name="adapter"></a>Define the adapter</span></span>
<span data-ttu-id="4019b-281">Источник данных нашего представления — это массив объектов **ToDoItem**, поэтому мы создадим адаптер как подкласс **ArrayAdapter&lt;ToDoItem&gt;**.</span><span class="sxs-lookup"><span data-stu-id="4019b-281">Since the data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="4019b-282">Этот подкласс создаст представление для каждого объекта **ToDoItem** с помощью макета **row_list_to_do**.</span><span class="sxs-lookup"><span data-stu-id="4019b-282">This subclass produces a View for every **ToDoItem** using the **row_list_to_do** layout.</span></span>  <span data-ttu-id="4019b-283">В коде мы определили следующий класс, который представляет собой расширение класса **ArrayAdapter&lt;E&gt;**:</span><span class="sxs-lookup"><span data-stu-id="4019b-283">In our code, we define the following class that is an extension of the **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="4019b-284">Переопределите метод **getView** адаптера.</span><span class="sxs-lookup"><span data-stu-id="4019b-284">Override the adapters **getView** method.</span></span> <span data-ttu-id="4019b-285">Например:</span><span class="sxs-lookup"><span data-stu-id="4019b-285">For example:</span></span>

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

<span data-ttu-id="4019b-286">Мы создаем экземпляр этого класса в действии следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4019b-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="4019b-287">Второй параметр конструктора ToDoItemAdapter — это ссылка на макет.</span><span class="sxs-lookup"><span data-stu-id="4019b-287">The second parameter to the ToDoItemAdapter constructor is a reference to the layout.</span></span> <span data-ttu-id="4019b-288">Теперь можно создать экземпляр **ListView** и назначить адаптер в **ListView**.</span><span class="sxs-lookup"><span data-stu-id="4019b-288">We can now instantiate the **ListView** and assign the adapter to the **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <span data-ttu-id="4019b-289"><a name="use-adapter"></a>Привязка данных к пользовательскому интерфейсу с помощью адаптера</span><span class="sxs-lookup"><span data-stu-id="4019b-289"><a name="use-adapter"></a>Use the Adapter to Bind to the UI</span></span>

<span data-ttu-id="4019b-290">Теперь вы можете использовать привязку данных.</span><span class="sxs-lookup"><span data-stu-id="4019b-290">You are now ready to use data binding.</span></span> <span data-ttu-id="4019b-291">Ниже приведен код, в котором показано, как получить элементы из таблицы и заполнить локальный адаптер возвращенными элементами.</span><span class="sxs-lookup"><span data-stu-id="4019b-291">The following code shows how to get items in the table and fills the local adapter with the returned items.</span></span>

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

<span data-ttu-id="4019b-292">Адаптер вызывается при каждом изменении таблицы **ToDoItem** .</span><span class="sxs-lookup"><span data-stu-id="4019b-292">Call the adapter any time you modify the **ToDoItem** table.</span></span> <span data-ttu-id="4019b-293">Так как изменения выполняются на уровне отдельных записей, обрабатываться будут отдельные строки, а не коллекция.</span><span class="sxs-lookup"><span data-stu-id="4019b-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="4019b-294">При вставке элемента вызывается метод **add** адаптера, а при удалении — метод **remove**.</span><span class="sxs-lookup"><span data-stu-id="4019b-294">When you insert an item, call the **add** method on the adapter; when deleting, call the **remove** method.</span></span>

<span data-ttu-id="4019b-295">Полный пример можно найти в [проекте быстрого запуска для Android][21].</span><span class="sxs-lookup"><span data-stu-id="4019b-295">You can find a complete example in the [Android Quickstart Project][21].</span></span>

## <span data-ttu-id="4019b-296"><a name="inserting"></a>Вставка данных в серверную часть</span><span class="sxs-lookup"><span data-stu-id="4019b-296"><a name="inserting"></a>Insert data into the backend</span></span>

<span data-ttu-id="4019b-297">Создайте экземпляр класса *ToDoItem* и задайте его свойства.</span><span class="sxs-lookup"><span data-stu-id="4019b-297">Instantiate an instance of the *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="4019b-298">Затем с помощью **insert()** вставьте объект.</span><span class="sxs-lookup"><span data-stu-id="4019b-298">Then use **insert()** to insert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="4019b-299">Возвращаемая сущность соответствует данным, вставленным в таблицу серверной части, в том числе идентификатору и другим значениям (например, поля `createdAt`, `updatedAt` и `version`), заданным в серверной части.</span><span class="sxs-lookup"><span data-stu-id="4019b-299">The returned entity matches the data inserted into the backend table, included the ID and any other values (such as the `createdAt`, `updatedAt`, and `version` fields) set on the backend.</span></span>

<span data-ttu-id="4019b-300">Для таблиц мобильных приложений требуется столбец первичного ключа **id**.</span><span class="sxs-lookup"><span data-stu-id="4019b-300">Mobile Apps tables require a primary key column named **id**.</span></span> <span data-ttu-id="4019b-301">Этот столбец должен быть строкой.</span><span class="sxs-lookup"><span data-stu-id="4019b-301">This column must be a string.</span></span> <span data-ttu-id="4019b-302">По умолчанию столбец идентификаторов содержит значения GUID.</span><span class="sxs-lookup"><span data-stu-id="4019b-302">The default value of the ID column is a GUID.</span></span>  <span data-ttu-id="4019b-303">Можно указать другие уникальные значения, в том числе электронные адреса или имена пользователей.</span><span class="sxs-lookup"><span data-stu-id="4019b-303">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="4019b-304">Если строковое значение идентификатора для вставленной записи не предусмотрено, то серверная часть создает новое значение GUID.</span><span class="sxs-lookup"><span data-stu-id="4019b-304">When a string ID value is not provided for an inserted record, the backend generates a new GUID.</span></span>

<span data-ttu-id="4019b-305">Использование строковых значений идентификаторов связано с такими преимуществами.</span><span class="sxs-lookup"><span data-stu-id="4019b-305">String ID values provide the following advantages:</span></span>

* <span data-ttu-id="4019b-306">Идентификаторы можно создавать без обмена данными с базой данных.</span><span class="sxs-lookup"><span data-stu-id="4019b-306">IDs can be generated without making a round trip to the database.</span></span>
* <span data-ttu-id="4019b-307">Можно легко объединять записи из разных таблиц или баз данных.</span><span class="sxs-lookup"><span data-stu-id="4019b-307">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="4019b-308">Значения идентификаторов удобнее интегрировать с логикой приложения.</span><span class="sxs-lookup"><span data-stu-id="4019b-308">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="4019b-309">Строковые значения идентификатора **НЕОБХОДИМЫ** для поддержки автономной синхронизации.</span><span class="sxs-lookup"><span data-stu-id="4019b-309">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="4019b-310">После сохранения идентификатора в серверной базе данных его изменить невозможно.</span><span class="sxs-lookup"><span data-stu-id="4019b-310">You cannot change an Id once it is stored in the backend database.</span></span>

## <span data-ttu-id="4019b-311"><a name="updating"></a>Обновление данных в мобильном приложении</span><span class="sxs-lookup"><span data-stu-id="4019b-311"><a name="updating"></a>Update data in a mobile app</span></span>

<span data-ttu-id="4019b-312">Чтобы обновить данные в таблице, передайте новый объект в метод **update()** .</span><span class="sxs-lookup"><span data-stu-id="4019b-312">To update data in a table, pass the new object to the **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="4019b-313">В этом примере *item* — это ссылка на строку в таблице *ToDoItem*, в которую были внесены изменения.</span><span class="sxs-lookup"><span data-stu-id="4019b-313">In this example, *item* is a reference to a row in the *ToDoItem* table, which has had some changes made to it.</span></span>  <span data-ttu-id="4019b-314">Строка с таким же значением **id** обновится.</span><span class="sxs-lookup"><span data-stu-id="4019b-314">The row with the same **id** is updated.</span></span>

## <span data-ttu-id="4019b-315"><a name="deleting"></a>Удаление данных в мобильном приложении</span><span class="sxs-lookup"><span data-stu-id="4019b-315"><a name="deleting"></a>Delete data in a mobile app</span></span>

<span data-ttu-id="4019b-316">В следующем коде показано, как удалить данные из таблицы, указав объект данных.</span><span class="sxs-lookup"><span data-stu-id="4019b-316">The following code shows how to delete data from a table by specifying the data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="4019b-317">Удалить элемент также можно, указав поле **id** удаляемой строки.</span><span class="sxs-lookup"><span data-stu-id="4019b-317">You can also delete an item by specifying the **id** field of the row to delete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <span data-ttu-id="4019b-318"><a name="lookup"></a>Поиск определенного элемента по идентификатору</span><span class="sxs-lookup"><span data-stu-id="4019b-318"><a name="lookup"></a>Look up a specific item by Id</span></span>

<span data-ttu-id="4019b-319">Найдите элемент с определенным значением в поле **id** с помощью метода **lookUp()**.</span><span class="sxs-lookup"><span data-stu-id="4019b-319">Look up an item with a specific **id** field with the **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <span data-ttu-id="4019b-320"><a name="untyped"></a>Практическое руководство. Работа с нетипизированными данными</span><span class="sxs-lookup"><span data-stu-id="4019b-320"><a name="untyped"></a>How to: Work with untyped data</span></span>

<span data-ttu-id="4019b-321">Нетипизированная модель программирования предоставляет точный контроль над сериализацией JSON.</span><span class="sxs-lookup"><span data-stu-id="4019b-321">The untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="4019b-322">Существует несколько распространенных сценариев, в которых может потребоваться использовать нетипизированную модель программирования.</span><span class="sxs-lookup"><span data-stu-id="4019b-322">There are some common scenarios where you may wish to use an untyped programming model.</span></span> <span data-ttu-id="4019b-323">Например, если таблица серверной части содержит много столбцов, и вам нужно указать ссылку только на их подмножество.</span><span class="sxs-lookup"><span data-stu-id="4019b-323">For example, if your backend table contains many columns and you only need to reference a subset of the columns.</span></span>  <span data-ttu-id="4019b-324">Для использования типизированной модели необходимо определить все столбцы, заданные в серверной части мобильных приложений в классе данных.</span><span class="sxs-lookup"><span data-stu-id="4019b-324">The typed model requires you to define all the columns defined in the Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="4019b-325">Большая часть вызовов интерфейса API для доступа к данным аналогична вызовам в типизированной модели.</span><span class="sxs-lookup"><span data-stu-id="4019b-325">Most of the API calls for accessing data are similar to the typed programming calls.</span></span> <span data-ttu-id="4019b-326">Основное различие заключается в том, что в нетипизированной модели методы вызываются для объекта **MobileServiceJsonTable**, а не **MobileServiceTable**.</span><span class="sxs-lookup"><span data-stu-id="4019b-326">The main difference is that in the untyped model you invoke methods on the **MobileServiceJsonTable** object, instead of the **MobileServiceTable** object.</span></span>

### <span data-ttu-id="4019b-327"><a name="json_instance"></a>Создание экземпляра нетипизированной таблицы</span><span class="sxs-lookup"><span data-stu-id="4019b-327"><a name="json_instance"></a>Create an instance of an untyped table</span></span>

<span data-ttu-id="4019b-328">Аналогично типизированной модели сначала вы получаете ссылку на таблицу, но в данном случае это объект **MobileServicesJsonTable** .</span><span class="sxs-lookup"><span data-stu-id="4019b-328">Similar to the typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="4019b-329">Чтобы получить ссылку, вызовите метод **getTable** для экземпляра клиента.</span><span class="sxs-lookup"><span data-stu-id="4019b-329">Obtain the reference by calling the **getTable** method on an instance of the client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="4019b-330">После создания экземпляр **MobileServiceJsonTable**обладает практически таким же API, что и в типизированной модели программирования.</span><span class="sxs-lookup"><span data-stu-id="4019b-330">Once you have created an instance of the **MobileServiceJsonTable**, it has virtually the same API available as with the typed programming model.</span></span> <span data-ttu-id="4019b-331">В некоторых случаях методы принимают нетипизированный параметр вместо типизированного.</span><span class="sxs-lookup"><span data-stu-id="4019b-331">In some cases, the methods take an untyped parameter instead of a typed parameter.</span></span>

### <span data-ttu-id="4019b-332"><a name="json_insert"></a>Вставка данных в нетипизированную таблицу</span><span class="sxs-lookup"><span data-stu-id="4019b-332"><a name="json_insert"></a>Insert into an untyped table</span></span>
<span data-ttu-id="4019b-333">В следующем коде показано, как вставить данные.</span><span class="sxs-lookup"><span data-stu-id="4019b-333">The following code shows how to do an insert.</span></span> <span data-ttu-id="4019b-334">Первый шаг — создание объекта [JsonObject][1], который является частью библиотеки [gson][3].</span><span class="sxs-lookup"><span data-stu-id="4019b-334">The first step is to create a [JsonObject][1], which is part of the [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="4019b-335">Затем с помощью **insert()** вставьте нетипизированный объект в таблицу.</span><span class="sxs-lookup"><span data-stu-id="4019b-335">Then, Use **insert()** to insert the untyped object into the table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="4019b-336">Если необходимо получить идентификатор вставленного объекта, используйте метод **getAsJsonPrimitive()** .</span><span class="sxs-lookup"><span data-stu-id="4019b-336">If you need to get the ID of the inserted object, use the **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <span data-ttu-id="4019b-337"><a name="json_delete"></a>Удаление данных из нетипизированной таблицы</span><span class="sxs-lookup"><span data-stu-id="4019b-337"><a name="json_delete"></a>Delete from an untyped table</span></span>
<span data-ttu-id="4019b-338">В следующем коде показано, как удалить экземпляр, в этом случае тот же экземпляр объекта **JsonObject** , который был создан в предыдущем примере *вставки* .</span><span class="sxs-lookup"><span data-stu-id="4019b-338">The following code shows how to delete an instance, in this case, the same instance of a **JsonObject** that was created in the prior *insert* example.</span></span> <span data-ttu-id="4019b-339">Код будет таким же, как и в случае типизированной таблицы, но метод будет иметь другую сигнатуру, так как он ссылается на **JsonObject**.</span><span class="sxs-lookup"><span data-stu-id="4019b-339">The code is the same as with the typed case, but the method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="4019b-340">Вы также можете удалить экземпляр напрямую с помощью идентификатора:</span><span class="sxs-lookup"><span data-stu-id="4019b-340">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <span data-ttu-id="4019b-341"><a name="json_get"></a>Получение всех строк из нетипизированной таблицы</span><span class="sxs-lookup"><span data-stu-id="4019b-341"><a name="json_get"></a>Return all rows from an untyped table</span></span>
<span data-ttu-id="4019b-342">В следующем коде показано, как получить всю таблицу.</span><span class="sxs-lookup"><span data-stu-id="4019b-342">The following code shows how to retrieve an entire table.</span></span> <span data-ttu-id="4019b-343">Поскольку вы используете таблицы Json, можно выборочно вывести лишь некоторые столбцы таблицы.</span><span class="sxs-lookup"><span data-stu-id="4019b-343">Since you are using a JSON Table, you can selectively retrieve only some of the table's columns.</span></span>

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

<span data-ttu-id="4019b-344">Для нетипизированной модели доступен тот же набор средств фильтрации, то есть методы фильтрации и разбиения по страницам, что и для типизированной модели.</span><span class="sxs-lookup"><span data-stu-id="4019b-344">The same set of filtering, filtering and paging methods that are available for the typed model are available for the untyped model.</span></span>

## <span data-ttu-id="4019b-345"><a name="offline-sync"></a>Реализация синхронизации в автономном режиме</span><span class="sxs-lookup"><span data-stu-id="4019b-345"><a name="offline-sync"></a>Implement Offline Sync</span></span>

<span data-ttu-id="4019b-346">Пакет SDK для клиента мобильных приложений Azure также реализует синхронизацию данных в автономном режиме. Это стало возможным благодаря хранению копии данных сервера локально в базе данных SQLite.</span><span class="sxs-lookup"><span data-stu-id="4019b-346">The Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database to store a copy of the server data locally.</span></span>  <span data-ttu-id="4019b-347">Операции в автономной таблице выполняются без подключения к мобильному приложению.</span><span class="sxs-lookup"><span data-stu-id="4019b-347">Operations performed on an offline table do not require mobile connectivity to work.</span></span>  <span data-ttu-id="4019b-348">Синхронизация данных в автономном режиме повышает устойчивость и производительность за счет более сложной логики устранения конфликтов.</span><span class="sxs-lookup"><span data-stu-id="4019b-348">Offline sync aids in resilience and performance at the expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="4019b-349">Пакет SDK для клиента мобильных приложений Azure реализует следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="4019b-349">The Azure Mobile Apps Client SDK implements the following features:</span></span>

* <span data-ttu-id="4019b-350">Добавочная синхронизация. Загружаются только обновленные и новые записи. Это позволяет уменьшить потребление пропускной способности и памяти.</span><span class="sxs-lookup"><span data-stu-id="4019b-350">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="4019b-351">Оптимистичный параллелизм. Операции рассматриваются как успешные.</span><span class="sxs-lookup"><span data-stu-id="4019b-351">Optimistic Concurrency: Operations are assumed to succeed.</span></span>  <span data-ttu-id="4019b-352">Устранение конфликтов откладывается до выполнения обновлений на сервере.</span><span class="sxs-lookup"><span data-stu-id="4019b-352">Conflict Resolution is deferred until updates are performed on the server.</span></span>
* <span data-ttu-id="4019b-353">Устранение конфликтов. Пакет SDK обнаруживает время внесения конфликтного изменения на сервере и предоставляет обработчики для отправки уведомлений пользователю.</span><span class="sxs-lookup"><span data-stu-id="4019b-353">Conflict Resolution: The SDK detects when a conflicting change has been made at the server and provides hooks to alert the user.</span></span>
* <span data-ttu-id="4019b-354">Обратимое удаление. Удаленные записи помечаются как удаленные, что позволяет другим устройствам обновить их автономный кэш.</span><span class="sxs-lookup"><span data-stu-id="4019b-354">Soft Delete: Deleted records are marked deleted, allowing other devices to update their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="4019b-355">Инициализация синхронизации в автономном режиме</span><span class="sxs-lookup"><span data-stu-id="4019b-355">Initialize Offline Sync</span></span>

<span data-ttu-id="4019b-356">Перед использованием каждую автономную таблицу необходимо определить в автономном кэше.</span><span class="sxs-lookup"><span data-stu-id="4019b-356">Each offline table must be defined in the offline cache before use.</span></span>  <span data-ttu-id="4019b-357">Как правило, определение таблицы выполняется сразу после создания клиента:</span><span class="sxs-lookup"><span data-stu-id="4019b-357">Normally, table definition is done immediately after the creation of the client:</span></span>

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

                // Create a table definition.  As a best practice, store this with the model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define the table in the local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize the local store
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

### <a name="obtain-a-reference-to-the-offline-cache-table"></a><span data-ttu-id="4019b-358">Получение ссылки на автономную таблицу кэша</span><span class="sxs-lookup"><span data-stu-id="4019b-358">Obtain a reference to the Offline Cache Table</span></span>

<span data-ttu-id="4019b-359">Для таблицы в Интернете используйте `.getTable()`,</span><span class="sxs-lookup"><span data-stu-id="4019b-359">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="4019b-360">а для автономной таблицы — `.getSyncTable()`:</span><span class="sxs-lookup"><span data-stu-id="4019b-360">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="4019b-361">Все методы, доступные для таблиц в Интернете (в том числе методы фильтрации, разбиения по страницам, сортировки, вставки, обновления и удаления данных), работают одинаково хорошо и с автономными таблицами.</span><span class="sxs-lookup"><span data-stu-id="4019b-361">All the methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-the-local-offline-cache"></a><span data-ttu-id="4019b-362">Синхронизация локального автономного кэша</span><span class="sxs-lookup"><span data-stu-id="4019b-362">Synchronize the Local Offline Cache</span></span>

<span data-ttu-id="4019b-363">Синхронизация выполняется под управлением приложения.</span><span class="sxs-lookup"><span data-stu-id="4019b-363">Synchronization is within the control of your app.</span></span>  <span data-ttu-id="4019b-364">Ниже приведен пример метода синхронизации.</span><span class="sxs-lookup"><span data-stu-id="4019b-364">Here is an example synchronization method:</span></span>

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

<span data-ttu-id="4019b-365">Если в метод `.pull(query, queryname)` добавить имя запроса, тогда выполняется добавочная синхронизация и возвращаются только записи, созданные или измененные с момента последнего успешного запроса.</span><span class="sxs-lookup"><span data-stu-id="4019b-365">If a query name is provided to the `.pull(query, queryname)` method, then incremental sync is used to return only records that have been created or changed since the last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="4019b-366">Обработка конфликтов во время синхронизации в автономном режиме</span><span class="sxs-lookup"><span data-stu-id="4019b-366">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="4019b-367">Если конфликт происходит во время выполнения операции `.push()`, возникает исключение `MobileServiceConflictException`.</span><span class="sxs-lookup"><span data-stu-id="4019b-367">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="4019b-368">В это исключение внедрен выданный сервером элемент, который можно извлечь, добавив в исключение метод `.getItem()`.</span><span class="sxs-lookup"><span data-stu-id="4019b-368">The server-issued item is embedded in the exception and can be retrieved by `.getItem()` on the exception.</span></span>  <span data-ttu-id="4019b-369">Настройте принудительную отправку, добавив в объект MobileServiceSyncContext следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="4019b-369">Adjust the push by calling the following items on the MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="4019b-370">Когда все конфликты будут помечены должным образом, вызовите метод `.push()`, чтобы устранить их.</span><span class="sxs-lookup"><span data-stu-id="4019b-370">Once all conflicts are marked as you wish, call `.push()` again to resolve all the conflicts.</span></span>

## <span data-ttu-id="4019b-371"><a name="custom-api"></a>Вызов настраиваемого интерфейса API</span><span class="sxs-lookup"><span data-stu-id="4019b-371"><a name="custom-api"></a>Call a custom API</span></span>

<span data-ttu-id="4019b-372">Настраиваемый интерфейс API позволяет определить пользовательские конечные точки, которые предоставляют функциональные возможности сервера, не сопоставляемые с операциями вставки, обновления, удаления или чтения.</span><span class="sxs-lookup"><span data-stu-id="4019b-372">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="4019b-373">При использовании настраиваемого интерфейса API вы получаете больше возможностей для управления сообщениями, в том числе для чтения и установки заголовков HTTP-сообщений, а также определения форматов текста сообщений, отличных от JSON.</span><span class="sxs-lookup"><span data-stu-id="4019b-373">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="4019b-374">Вызовите из клиента Android метод **invokeApi** для вызова конечной точки настраиваемого API.</span><span class="sxs-lookup"><span data-stu-id="4019b-374">From an Android client, you call the **invokeApi** method to call the custom API endpoint.</span></span> <span data-ttu-id="4019b-375">В следующем примере показано, как вызвать конечную точку API с именем **completeAll**, которая возвращает класс коллекции с именем **MarkAllResult**.</span><span class="sxs-lookup"><span data-stu-id="4019b-375">The following example shows how to call an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

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

<span data-ttu-id="4019b-376">Метод **invokeApi** вызывается на стороне клиента, что приводит к отправке запроса POST новому настраиваемому API.</span><span class="sxs-lookup"><span data-stu-id="4019b-376">The **invokeApi** method is called on the client, which sends a POST request to the new custom API.</span></span> <span data-ttu-id="4019b-377">Результат, возвращаемый настраиваемым интерфейсом API, отображается в диалоговом окне сообщения, как и любые ошибки.</span><span class="sxs-lookup"><span data-stu-id="4019b-377">The result returned by the custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="4019b-378">Другие версии метода **invokeApi** позволяют при необходимости отправить объект в тексте запроса, указать метод HTTP и отправить параметры запроса вместе с запросом.</span><span class="sxs-lookup"><span data-stu-id="4019b-378">Other versions of **invokeApi** let you optionally send an object in the request body, specify the HTTP method, and send query parameters with the request.</span></span> <span data-ttu-id="4019b-379">Кроме того, доступны нетипизированные версии **invokeApi** .</span><span class="sxs-lookup"><span data-stu-id="4019b-379">Untyped versions of **invokeApi** are provided as well.</span></span>

## <span data-ttu-id="4019b-380"><a name="authentication"></a>Добавление проверки подлинности в приложение</span><span class="sxs-lookup"><span data-stu-id="4019b-380"><a name="authentication"></a>Add authentication to your app</span></span>

<span data-ttu-id="4019b-381">Процесс добавления этих компонентов подробно описан в руководствах.</span><span class="sxs-lookup"><span data-stu-id="4019b-381">Tutorials already describe in detail how to add these features.</span></span>

<span data-ttu-id="4019b-382">Служба приложений поддерживает [проверку подлинности пользователей приложения](app-service-mobile-android-get-started-users.md) с помощью разных внешних поставщиков удостоверений: Facebook, Google, учетной записи Майкрософт, Twitter и Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4019b-382">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="4019b-383">Можно задать разрешения таблиц, чтобы предоставить доступ к определенным операциям только пользователям, прошедшим проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="4019b-383">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="4019b-384">Удостоверения пользователей, прошедших проверку подлинности, также можно применять для реализации правил авторизации в серверной части.</span><span class="sxs-lookup"><span data-stu-id="4019b-384">You can also use the identity of authenticated users to implement authorization rules in your backend.</span></span>

<span data-ttu-id="4019b-385">Поддерживаются два потока аутентификации: **серверный** и **клиентский**.</span><span class="sxs-lookup"><span data-stu-id="4019b-385">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="4019b-386">Серверный поток обеспечивает самый простой способ аутентификации, так как он использует веб-интерфейс поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="4019b-386">The server flow provides the simplest authentication experience, as it relies on the identity providers web interface.</span></span>  <span data-ttu-id="4019b-387">Для реализации аутентификации серверного потока не нужны дополнительные пакеты SDK.</span><span class="sxs-lookup"><span data-stu-id="4019b-387">No additional SDKs are required to implement server flow authentication.</span></span> <span data-ttu-id="4019b-388">Аутентификация серверного потока не обеспечивает тесную интеграцию с мобильным устройством и рекомендуется только для подтверждения концепции.</span><span class="sxs-lookup"><span data-stu-id="4019b-388">Server flow authentication does not provide a deep integration into the mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="4019b-389">Клиентский поток обеспечивает более тесную интеграцию с возможностями устройства, такими как единый вход, так как использует пакеты SDK, предоставляемые конкретным поставщиком удостоверений.</span><span class="sxs-lookup"><span data-stu-id="4019b-389">The client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by the identity provider.</span></span>  <span data-ttu-id="4019b-390">Например, можно интегрировать пакет SDK для Facebook в мобильное приложение.</span><span class="sxs-lookup"><span data-stu-id="4019b-390">For example, you can integrate the Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="4019b-391">Мобильный клиент переключается на приложение Facebook и подтверждает ваш вход, прежде чем переключиться обратно на мобильное приложение.</span><span class="sxs-lookup"><span data-stu-id="4019b-391">The mobile client swaps into the Facebook app and confirms your sign-on before swapping back to your mobile app.</span></span>

<span data-ttu-id="4019b-392">Чтобы включить аутентификацию в приложении, необходимо выполнить четыре действия:</span><span class="sxs-lookup"><span data-stu-id="4019b-392">Four steps are required to enable authentication in your app:</span></span>

* <span data-ttu-id="4019b-393">Регистрация приложения для аутентификации в поставщике удостоверений.</span><span class="sxs-lookup"><span data-stu-id="4019b-393">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="4019b-394">Настройка серверной части службы приложений.</span><span class="sxs-lookup"><span data-stu-id="4019b-394">Configure your App Service backend.</span></span>
* <span data-ttu-id="4019b-395">Ограничение разрешений таблицы только аутентифицированными пользователями.</span><span class="sxs-lookup"><span data-stu-id="4019b-395">Restrict table permissions to authenticated users only on the App Service backend.</span></span>
* <span data-ttu-id="4019b-396">Добавление кода проверки подлинности в приложение.</span><span class="sxs-lookup"><span data-stu-id="4019b-396">Add authentication code to your app.</span></span>

<span data-ttu-id="4019b-397">Можно задать разрешения таблиц, чтобы предоставить доступ к определенным операциям только пользователям, прошедшим проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="4019b-397">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="4019b-398">Также можно использовать идентификатор безопасности пользователя, прошедшего проверку, чтобы изменять запросы.</span><span class="sxs-lookup"><span data-stu-id="4019b-398">You can also use the SID of an authenticated user to modify requests.</span></span>  <span data-ttu-id="4019b-399">Дополнительную информацию см. в разделе [Приступая к работе с проверкой подлинности] и справочной документации по пакету SDK для сервера.</span><span class="sxs-lookup"><span data-stu-id="4019b-399">For more information, review [Get started with authentication] and the Server SDK HOWTO documentation.</span></span>

### <span data-ttu-id="4019b-400"><a name="caching"></a>Серверный поток проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="4019b-400"><a name="caching"></a>Authentication: Server Flow</span></span>

<span data-ttu-id="4019b-401">Следующий код запускает процесс входа серверного потока с помощью поставщика Google.</span><span class="sxs-lookup"><span data-stu-id="4019b-401">The following code starts a server flow login process using the Google provider.</span></span>  <span data-ttu-id="4019b-402">Из-за требований к безопасности поставщика Google необходимо выполнить дополнительную конфигурацию:</span><span class="sxs-lookup"><span data-stu-id="4019b-402">Additional configuration is required because of the security requirements for the Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="4019b-403">Кроме того, добавьте в основной класс Activity следующий метод:</span><span class="sxs-lookup"><span data-stu-id="4019b-403">In addition, add the following method to the main Activity class:</span></span>

```java
// You can choose any unique number here to differentiate auth providers from each other. Note this is the same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check the request code matches the one we send in the login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check the error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

<span data-ttu-id="4019b-404">Параметр `GOOGLE_LOGIN_REQUEST_CODE`, определенный в основном классе Activity, используется в методе `login()` и `onActivityResult()`.</span><span class="sxs-lookup"><span data-stu-id="4019b-404">The `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for the `login()` method and within the `onActivityResult()` method.</span></span>  <span data-ttu-id="4019b-405">Вы можете выбрать любое уникальное число, если оно будет одинаковым в методе `login()` и `onActivityResult()`.</span><span class="sxs-lookup"><span data-stu-id="4019b-405">You can choose any unique number, as long as the same number is used within the `login()` method and the `onActivityResult()` method.</span></span>  <span data-ttu-id="4019b-406">Если вы абстрагировали код клиента в адаптер службы (как показано выше), необходимо вызвать соответствующие методы этого адаптера.</span><span class="sxs-lookup"><span data-stu-id="4019b-406">If you abstract the client code into a service adapter (as shown earlier), you should call the appropriate methods on the service adapter.</span></span>

<span data-ttu-id="4019b-407">Кроме того, необходимо также настроить проект настраиваемых вкладок.</span><span class="sxs-lookup"><span data-stu-id="4019b-407">You also need to configure the project for customtabs.</span></span>  <span data-ttu-id="4019b-408">Сначала укажите URL-адрес перенаправления.</span><span class="sxs-lookup"><span data-stu-id="4019b-408">First specify a redirect-URL.</span></span>  <span data-ttu-id="4019b-409">Добавьте в файл `AndroidManifest.xml` следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="4019b-409">Add the following snippet to `AndroidManifest.xml`:</span></span>

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

<span data-ttu-id="4019b-410">Добавьте параметр **redirectUriScheme** в файл `build.gradle` приложения:</span><span class="sxs-lookup"><span data-stu-id="4019b-410">Add the **redirectUriScheme** to the `build.gradle` file for your application:</span></span>

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

<span data-ttu-id="4019b-411">Наконец, добавьте `com.android.support:customtabs:23.0.1` в список зависимостей в файле `build.gradle`:</span><span class="sxs-lookup"><span data-stu-id="4019b-411">Finally, add `com.android.support:customtabs:23.0.1` to the dependencies list in the `build.gradle` file:</span></span>

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

<span data-ttu-id="4019b-412">Получите идентификатор вошедшего в систему пользователя из **MobileServiceUser** с помощью метода **getUserId**.</span><span class="sxs-lookup"><span data-stu-id="4019b-412">Obtain the ID of the logged-in user from a **MobileServiceUser** using the **getUserId** method.</span></span> <span data-ttu-id="4019b-413">Пример использования Futures для вызова API асинхронного входа см. в статье [Приступая к работе с проверкой подлинности].</span><span class="sxs-lookup"><span data-stu-id="4019b-413">For an example of how to use Futures to call the asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="4019b-414">В упомянутой схеме URL-адресов учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="4019b-414">The URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="4019b-415">Убедитесь, что во всех вхождениях `{url_scheme_of_you_app}` используется один и тот же регистр.</span><span class="sxs-lookup"><span data-stu-id="4019b-415">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <span data-ttu-id="4019b-416"><a name="caching"></a>Кэширование токенов проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="4019b-416"><a name="caching"></a>Cache authentication tokens</span></span>

<span data-ttu-id="4019b-417">Для этого необходимо сохранить идентификатор пользователя и маркер аутентификации локально на устройстве.</span><span class="sxs-lookup"><span data-stu-id="4019b-417">Caching authentication tokens requires you to store the User ID and authentication token locally on the device.</span></span> <span data-ttu-id="4019b-418">При следующем запуске приложения проверьте кэш — если эти значения существуют, то можно пропустить процедуру входа и повторно заполнить клиент этими данными.</span><span class="sxs-lookup"><span data-stu-id="4019b-418">The next time the app starts, you check the cache, and if these values are present, you can skip the log in procedure and rehydrate the client with this data.</span></span> <span data-ttu-id="4019b-419">Однако это конфиденциальные данные и они должны храниться в зашифрованном виде, чтобы обеспечить безопасность в случае кражи телефона.</span><span class="sxs-lookup"><span data-stu-id="4019b-419">However this data is sensitive, and it should be stored encrypted for safety in case the phone gets stolen.</span></span>  <span data-ttu-id="4019b-420">См. полный пример [кэширования маркеров аутентификации][7].</span><span class="sxs-lookup"><span data-stu-id="4019b-420">You can see a complete example of how to cache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="4019b-421">При попытке использовать маркер с истекшим сроком действия вы получите ответ *401 не санкционировано* .</span><span class="sxs-lookup"><span data-stu-id="4019b-421">When you try to use an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="4019b-422">Ошибки аутентификации можно обрабатывать с помощью фильтров.</span><span class="sxs-lookup"><span data-stu-id="4019b-422">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="4019b-423">Фильтры перехватывают запросы к серверной части службы приложений.</span><span class="sxs-lookup"><span data-stu-id="4019b-423">Filters intercept requests to the App Service backend.</span></span> <span data-ttu-id="4019b-424">Код фильтра проверяет наличие ответа 401, инициирует вход в систему и возобновляет запрос, породивший ответ 401.</span><span class="sxs-lookup"><span data-stu-id="4019b-424">The filter code tests the response for a 401, triggers the sign-in process, and then resumes the request that generated the 401.</span></span>

### <span data-ttu-id="4019b-425"><a name="refresh"></a>Использование токенов обновления</span><span class="sxs-lookup"><span data-stu-id="4019b-425"><a name="refresh"></a>Use Refresh Tokens</span></span>

<span data-ttu-id="4019b-426">Время существования токена, возвращенного функцией проверки подлинности и авторизации в службе приложений Azure, составляет один час.</span><span class="sxs-lookup"><span data-stu-id="4019b-426">The token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="4019b-427">По истечении этого периода необходимо повторно выполнить проверку подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="4019b-427">After this period, you must reauthenticate the user.</span></span>  <span data-ttu-id="4019b-428">При использовании токена с долгим временем существования, полученного в клиентском потоке проверки подлинности, это можно сделать с помощью функции проверки подлинности и авторизации в службе приложений Azure, используя этот же токен.</span><span class="sxs-lookup"><span data-stu-id="4019b-428">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using the same token.</span></span>  <span data-ttu-id="4019b-429">В процессе создается другой токен службы приложений Azure с новым временем существования.</span><span class="sxs-lookup"><span data-stu-id="4019b-429">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="4019b-430">Вы также можете зарегистрировать поставщик для использования токенов обновления.</span><span class="sxs-lookup"><span data-stu-id="4019b-430">You can also register the provider to use Refresh Tokens.</span></span>  <span data-ttu-id="4019b-431">Токен обновления не всегда доступен.</span><span class="sxs-lookup"><span data-stu-id="4019b-431">A Refresh Token is not always available.</span></span>  <span data-ttu-id="4019b-432">В этом случае необходимо выполнить дополнительную настройку:</span><span class="sxs-lookup"><span data-stu-id="4019b-432">Additional configuration is required:</span></span>

* <span data-ttu-id="4019b-433">Для приложения **Azure Active Directory** настройте секрет клиента.</span><span class="sxs-lookup"><span data-stu-id="4019b-433">For **Azure Active Directory**, configure a client secret for the Azure Active Directory App.</span></span>  <span data-ttu-id="4019b-434">Укажите секрет клиента в службе приложений Azure при настройке проверки подлинности Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4019b-434">Specify the client secret in the Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="4019b-435">При вызове метода `.login()` передайте `response_type=code id_token` как параметр:</span><span class="sxs-lookup"><span data-stu-id="4019b-435">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="4019b-436">Для **Google** передайте `access_type=offline` как параметр:</span><span class="sxs-lookup"><span data-stu-id="4019b-436">For **Google**, pass the `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="4019b-437">Для **учетной записи Майкрософт** выберите область `wl.offline_access`.</span><span class="sxs-lookup"><span data-stu-id="4019b-437">For **Microsoft Account**, select the `wl.offline_access` scope.</span></span>

<span data-ttu-id="4019b-438">Чтобы обновить токен, вызовите метод `.refreshUser()`:</span><span class="sxs-lookup"><span data-stu-id="4019b-438">To refresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="4019b-439">Мы советуем создать фильтр, который определяет ответ 401 от сервера и пытается обновить токен пользователя.</span><span class="sxs-lookup"><span data-stu-id="4019b-439">As a best practice, create a filter that detects a 401 response from the server and tries to refresh the user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="4019b-440">Вход в систему с использованием клиентского потока проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="4019b-440">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="4019b-441">Общая процедура входа в систему с использованием клиентского потока проверки подлинности состоит из следующих этапов:</span><span class="sxs-lookup"><span data-stu-id="4019b-441">The general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="4019b-442">Настройка функции проверки подлинности и авторизации в службе приложений Azure, как и при серверном потоке проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4019b-442">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="4019b-443">Интеграция пакета SDK поставщика проверки подлинности для создания маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="4019b-443">Integrate the authentication provider SDK for authentication to produce an access token.</span></span>
* <span data-ttu-id="4019b-444">Вызов метода `.login()` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4019b-444">Call the `.login()` method as follows:</span></span>

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

<span data-ttu-id="4019b-445">Замените метод `onSuccess()` на любой код, который следует использовать для успешного входа.</span><span class="sxs-lookup"><span data-stu-id="4019b-445">Replace the `onSuccess()` method with whatever code you wish to use on a successful login.</span></span>  <span data-ttu-id="4019b-446">В строке `{provider}` необходимо указать допустимое значение поставщика, например **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount** или **twitter**.</span><span class="sxs-lookup"><span data-stu-id="4019b-446">The `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="4019b-447">При реализации пользовательской проверки подлинности вы также можете использовать тег поставщика проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4019b-447">If you have implemented custom authentication, then you can also use the custom authentication provider tag.</span></span>

### <span data-ttu-id="4019b-448"><a name="adal"></a>Проверка подлинности пользователей с помощью библиотеки проверки подлинности Active Directory (ADAL)</span><span class="sxs-lookup"><span data-stu-id="4019b-448"><a name="adal"></a>Authenticate users with the Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="4019b-449">Библиотеку проверки подлинности Active Directory (ADAL) можно использовать для входа пользователей в приложение с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4019b-449">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="4019b-450">Использование входа посредством клиентского потока является более предпочтительным, чем использование методов `loginAsync()` , так как он обеспечивает более естественный интерфейс входа для пользователя и позволяет выполнять дополнительную настройку.</span><span class="sxs-lookup"><span data-stu-id="4019b-450">Using a client flow login is often preferable to using the `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="4019b-451">Настройте серверную часть мобильного приложения для входа с помощью AAD, следуя указаниям в руководстве [Настройка приложения службы приложений для использования службы входа Azure Active Directory][22].</span><span class="sxs-lookup"><span data-stu-id="4019b-451">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="4019b-452">Обязательно выполните дополнительный этап регистрации собственного клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="4019b-452">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="4019b-453">Установите ADAL, добавив в файл build.gradle следующие определения.</span><span class="sxs-lookup"><span data-stu-id="4019b-453">Install ADAL by modifying your build.gradle file to include the following definitions:</span></span>

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

1. <span data-ttu-id="4019b-454">Добавьте указанный ниже код в приложение, выполнив следующие замены.</span><span class="sxs-lookup"><span data-stu-id="4019b-454">Add the following code to your application, making the following replacements:</span></span>

* <span data-ttu-id="4019b-455">Замените строку **INSERT-AUTHORITY-HERE** именем клиента, в котором подготовлено приложение.</span><span class="sxs-lookup"><span data-stu-id="4019b-455">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="4019b-456">Формат должен быть следующим: https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="4019b-456">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="4019b-457">Замените текст **INSERT-RESOURCE-ID-HERE** идентификатором клиента для серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="4019b-457">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="4019b-458">Идентификатор клиента можно скопировать на портале в разделе **Настройки Azure Active Directory** на вкладке **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="4019b-458">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
* <span data-ttu-id="4019b-459">Замените текст **INSERT-CLIENT-ID-HERE** идентификатором клиента, скопированным из собственного клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="4019b-459">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
* <span data-ttu-id="4019b-460">Замените текст **INSERT-REDIRECT-URI-HERE** конечной точкой сайта */.auth/login/done* , используя схему HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4019b-460">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="4019b-461">Это значение должно быть похоже на *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="4019b-461">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

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

## <span data-ttu-id="4019b-462"><a name="filters"></a>Настройка связи между клиентом и сервером</span><span class="sxs-lookup"><span data-stu-id="4019b-462"><a name="filters"></a>Adjust the Client-Server Communication</span></span>

<span data-ttu-id="4019b-463">Как правило, клиент использует HTTP-подключение на основе базовой библиотеки HTTP, входящей в пакет SDK для Android.</span><span class="sxs-lookup"><span data-stu-id="4019b-463">The Client connection is normally a basic HTTP connection using the underlying HTTP library supplied with the Android SDK.</span></span>  <span data-ttu-id="4019b-464">Используя другой тип подключения, вы сможете:</span><span class="sxs-lookup"><span data-stu-id="4019b-464">There are several reasons why you would want to change that:</span></span>

* <span data-ttu-id="4019b-465">использовать альтернативную библиотеку HTTP для настройки времени ожидания;</span><span class="sxs-lookup"><span data-stu-id="4019b-465">You wish to use an alternate HTTP library to adjust timeouts.</span></span>
* <span data-ttu-id="4019b-466">предоставить индикатор выполнения;</span><span class="sxs-lookup"><span data-stu-id="4019b-466">You wish to provide a progress bar.</span></span>
* <span data-ttu-id="4019b-467">добавить пользовательский заголовок для поддержки функции управления API;</span><span class="sxs-lookup"><span data-stu-id="4019b-467">You wish to add a custom header to support API management functionality.</span></span>
* <span data-ttu-id="4019b-468">настроить перехват неудачных ответов, что позволит повторно выполнить проверку подлинности;</span><span class="sxs-lookup"><span data-stu-id="4019b-468">You wish to intercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="4019b-469">записывать серверные запросы в службу аналитики.</span><span class="sxs-lookup"><span data-stu-id="4019b-469">You wish to log backend requests to an analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="4019b-470">Использование альтернативной библиотеки HTTP</span><span class="sxs-lookup"><span data-stu-id="4019b-470">Using an alternate HTTP Library</span></span>

<span data-ttu-id="4019b-471">После создания ссылки на клиент вызовите метод `.setAndroidHttpClientFactory()`.</span><span class="sxs-lookup"><span data-stu-id="4019b-471">Call the `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="4019b-472">Это, например, позволит установить время ожидания подключения в 60 секунд (по умолчанию 10 секунд).</span><span class="sxs-lookup"><span data-stu-id="4019b-472">For example, to set the connection timeout to 60 seconds (instead of the default 10 seconds):</span></span>

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

### <a name="implement-a-progress-filter"></a><span data-ttu-id="4019b-473">Реализация фильтра хода выполнения</span><span class="sxs-lookup"><span data-stu-id="4019b-473">Implement a Progress Filter</span></span>

<span data-ttu-id="4019b-474">Реализовав атрибут `ServiceFilter`, вы сможете настроить перехват каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="4019b-474">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="4019b-475">Например, следующий код позволяет обновить стандартный индикатор выполнения:</span><span class="sxs-lookup"><span data-stu-id="4019b-475">For example, the following updates a pre-created progress bar:</span></span>

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

<span data-ttu-id="4019b-476">Этот фильтр можно присоединить к клиенту следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4019b-476">You can attach this filter to the client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="4019b-477">Настройка заголовков запросов</span><span class="sxs-lookup"><span data-stu-id="4019b-477">Customize Request Headers</span></span>

<span data-ttu-id="4019b-478">Используйте атрибут `ServiceFilter` и присоедините фильтр точно так же, как и атрибут `ProgressFilter`:</span><span class="sxs-lookup"><span data-stu-id="4019b-478">Use the following `ServiceFilter` and attach the filter in the same way as the `ProgressFilter`:</span></span>

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

### <span data-ttu-id="4019b-479"><a name="conversions"></a>Настройка автоматической сериализации</span><span class="sxs-lookup"><span data-stu-id="4019b-479"><a name="conversions"></a>Configure Automatic Serialization</span></span>

<span data-ttu-id="4019b-480">Можно указать стратегию преобразования, которая применяется к каждому столбцу, с помощью API из библиотеки [gson][3].</span><span class="sxs-lookup"><span data-stu-id="4019b-480">You can specify a conversion strategy that applies to every column by using the [gson][3] API.</span></span> <span data-ttu-id="4019b-481">Клиентская библиотека Android использует [gson][3] для сериализации объектов Java в данные JSON перед отправкой данных в службу приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="4019b-481">The Android client library uses [gson][3] behind the scenes to serialize Java objects to JSON data before the data is sent to Azure App Service.</span></span>  <span data-ttu-id="4019b-482">В следующем коде используется метод **setFieldNamingStrategy()** для задания стратегии.</span><span class="sxs-lookup"><span data-stu-id="4019b-482">The following code uses the **setFieldNamingStrategy()** method to set the strategy.</span></span> <span data-ttu-id="4019b-483">Этот пример удалит начальный знак ("m"), а затем преобразует следующий знак в нижний регистр для каждого имени поля.</span><span class="sxs-lookup"><span data-stu-id="4019b-483">This example will delete the initial character (an "m"), and then lower-case the next character, for every field name.</span></span> <span data-ttu-id="4019b-484">Например, он преобразует "mId" в "id".</span><span class="sxs-lookup"><span data-stu-id="4019b-484">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="4019b-485">Реализуйте стратегию преобразования, чтобы снизить потребность в аннотациях `SerializedName()` в большинстве полей.</span><span class="sxs-lookup"><span data-stu-id="4019b-485">Implement a conversion strategy to reduce the need for `SerializedName()` annotations on most fields.</span></span>

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

<span data-ttu-id="4019b-486">Этот код необходимо выполнить перед созданием ссылки на мобильный клиент с помощью **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="4019b-486">This code must be executed before creating a mobile client reference using the **MobileServiceClient**.</span></span>

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
<span data-ttu-id="4019b-487">[Приступая к работе с проверкой подлинности]: app-service-mobile-android-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="4019b-487">[Get started with authentication]: app-service-mobile-android-get-started-users.md</span></span>
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
