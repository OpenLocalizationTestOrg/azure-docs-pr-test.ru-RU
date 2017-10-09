---
title: "aaaAzure AD v2 Android начало работы — Настройка | Документы Microsoft"
description: "Получение маркера доступа для приложения Android и вызов API Microsoft Graph или API, которые требуют маркеры доступа, из конечной точки Azure Active Directory версии 2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: df2670d6d35b7a9a81158d4d7eb190540ca9c695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="c616f-103">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="c616f-103">Set up your project</span></span>

> <span data-ttu-id="c616f-104">Предпочтение toodownload проект Android Studio в этом примере вместо этого?</span><span class="sxs-lookup"><span data-stu-id="c616f-104">Prefer toodownload this sample's Android Studio project instead?</span></span> <span data-ttu-id="c616f-105">[Загрузка проекта](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) и пропустить toohello [шаг настройки](#create-an-application-express) образец кода hello tooconfigure перед выполнением.</span><span class="sxs-lookup"><span data-stu-id="c616f-105">[Download a project](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing    .</span></span>


### <a name="create-a-new-project"></a><span data-ttu-id="c616f-106">Создание нового проекта</span><span class="sxs-lookup"><span data-stu-id="c616f-106">Create a new project</span></span> 
1.  <span data-ttu-id="c616f-107">Откройте Android Studio и перейдите к: `File` > `New` > `New Project`.</span><span class="sxs-lookup"><span data-stu-id="c616f-107">Open Android Studio, go to: `File` > `New` > `New Project`</span></span>
2.  <span data-ttu-id="c616f-108">Присвойте имя приложению и щелкните `Next`.</span><span class="sxs-lookup"><span data-stu-id="c616f-108">Name your application and click `Next`</span></span>
3.  <span data-ttu-id="c616f-109">Убедитесь, что tooselect *API 21 или более новой (Android 5.0)* и нажмите кнопку`Next`</span><span class="sxs-lookup"><span data-stu-id="c616f-109">Make sure tooselect *API 21 or newer (Android 5.0)* and click `Next`</span></span>
4.  <span data-ttu-id="c616f-110">Выйдите из раздела `Empty Activity`, щелкните `Next`, а затем — `Finish`.</span><span class="sxs-lookup"><span data-stu-id="c616f-110">Leave `Empty Activity`, click `Next`, then `Finish`</span></span>


### <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="c616f-111">Добавление проекта tooyour hello библиотеки проверки подлинности Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="c616f-111">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1.  <span data-ttu-id="c616f-112">Откройте Android Studio и перейдите к: `Gradle Scripts` > `build.gradle (Module: app)`.</span><span class="sxs-lookup"><span data-stu-id="c616f-112">In Android Studio, go to: `Gradle Scripts` > `build.gradle (Module: app)`</span></span>
2.  <span data-ttu-id="c616f-113">Копировать и вставить hello следующий код под `Dependencies`:</span><span class="sxs-lookup"><span data-stu-id="c616f-113">Copy and paste hello following code under `Dependencies`:</span></span>

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a><span data-ttu-id="c616f-114">Об этом пакете</span><span class="sxs-lookup"><span data-stu-id="c616f-114">About this package</span></span>

<span data-ttu-id="c616f-115">пакет Hello выше устанавливает hello библиотеки проверки подлинности Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="c616f-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="c616f-116">MSAL обрабатывает получение, кэширование и обновление tooaccess пользователя маркеры, используемые интерфейсы API, защищенные Azure Active Directory v2 конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="c616f-116">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by Azure Active Directory v2 endpoint.</span></span>
<!--end-collapse-->

## <a name="create-your-applications-ui"></a><span data-ttu-id="c616f-117">Создание пользовательского интерфейса приложения</span><span class="sxs-lookup"><span data-stu-id="c616f-117">Create your application’s UI</span></span>

1.  <span data-ttu-id="c616f-118">Откройте `activity_main.xml` (в `res` > `layout`).</span><span class="sxs-lookup"><span data-stu-id="c616f-118">Open: `activity_main.xml` under `res` > `layout`</span></span>
2.  <span data-ttu-id="c616f-119">Изменение макета действие hello из `android.support.constraint.ConstraintLayout` или другие слишком`LinearLayout`</span><span class="sxs-lookup"><span data-stu-id="c616f-119">Change hello activity layout from `android.support.constraint.ConstraintLayout` or other too`LinearLayout`</span></span>
3.  <span data-ttu-id="c616f-120">Добавить `android:orientation="vertical"` свойство слишком`LinearLayout` узла</span><span class="sxs-lookup"><span data-stu-id="c616f-120">Add `android:orientation="vertical"` property too`LinearLayout` node</span></span>
4.  <span data-ttu-id="c616f-121">Копировать и вставить hello следующий код в hello `LinearLayout` узел, заменив текущее содержимое hello:</span><span class="sxs-lookup"><span data-stu-id="c616f-121">Copy and paste hello following code into hello `LinearLayout` node, replacing hello current content:</span></span>

```xml
<TextView
    android:text="Welcome, "
    android:textColor="#3f3f3f"
    android:textSize="50px"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginLeft="10dp"
    android:layout_marginTop="15dp"
    android:id="@+id/welcome"
    android:visibility="invisible"/>

<Button
    android:id="@+id/callGraph"
    android:text="Call Microsoft Graph"
    android:textColor="#FFFFFF"
    android:background="#00a1f1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="200dp"
    android:textAllCaps="false" />

<TextView
    android:text="Getting Graph Data..."
    android:textColor="#3f3f3f"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginLeft="5dp"
    android:id="@+id/graphData"
    android:visibility="invisible"/>

<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="0dip"
    android:layout_weight="1"
    android:gravity="center|bottom"
    android:orientation="vertical" >

    <Button
        android:text="Sign Out"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="15dp"
        android:textColor="#FFFFFF"
        android:background="#00a1f1"
        android:textAllCaps="false"
        android:id="@+id/clearCache"
        android:visibility="invisible" />
</LinearLayout>
```

