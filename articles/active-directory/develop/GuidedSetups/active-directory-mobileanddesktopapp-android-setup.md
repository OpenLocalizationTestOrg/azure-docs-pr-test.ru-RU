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
## <a name="set-up-your-project"></a>Настройка проекта

> Предпочтение toodownload проект Android Studio в этом примере вместо этого? [Загрузка проекта](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) и пропустить toohello [шаг настройки](#create-an-application-express) образец кода hello tooconfigure перед выполнением.


### <a name="create-a-new-project"></a>Создание нового проекта 
1.  Откройте Android Studio и перейдите к: `File` > `New` > `New Project`.
2.  Присвойте имя приложению и щелкните `Next`.
3.  Убедитесь, что tooselect *API 21 или более новой (Android 5.0)* и нажмите кнопку`Next`
4.  Выйдите из раздела `Empty Activity`, щелкните `Next`, а затем — `Finish`.


### <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>Добавление проекта tooyour hello библиотеки проверки подлинности Microsoft (MSAL)
1.  Откройте Android Studio и перейдите к: `Gradle Scripts` > `build.gradle (Module: app)`.
2.  Копировать и вставить hello следующий код под `Dependencies`:

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a>Об этом пакете

пакет Hello выше устанавливает hello библиотеки проверки подлинности Microsoft (MSAL). MSAL обрабатывает получение, кэширование и обновление tooaccess пользователя маркеры, используемые интерфейсы API, защищенные Azure Active Directory v2 конечной точкой.
<!--end-collapse-->

## <a name="create-your-applications-ui"></a>Создание пользовательского интерфейса приложения

1.  Откройте `activity_main.xml` (в `res` > `layout`).
2.  Изменение макета действие hello из `android.support.constraint.ConstraintLayout` или другие слишком`LinearLayout`
3.  Добавить `android:orientation="vertical"` свойство слишком`LinearLayout` узла
4.  Копировать и вставить hello следующий код в hello `LinearLayout` узел, заменив текущее содержимое hello:

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

