---
title: "aaaAzure AD v2 JS SPA интерактивной установки — Настройка | Документы Microsoft"
description: "В этой статье описано, как приложения JavaScript SPA могут вызывать API, которому необходимы маркеры доступа, с помощью конечной точки Azure Active Directory версии 2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a>Регистрация приложения

Существует несколько способов toocreate приложения, выберите один из них:

### <a name="option-1-register-your-application-express-mode"></a>Вариант 1. Регистрация приложения (экспресс-режим).
Теперь необходимо приложение hello tooregister *портала регистрации приложения Microsoft*:

1.  Зарегистрировать приложение через hello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)
2.  Введите имя для приложения и адрес электронной почты.
3.  Убедитесь, что параметр hello *интерактивной установки* проверяется
4.  Выполните код приложения hello tooobtain инструкции hello и вставьте его в коде

### <a name="option-2-register-your-application-advanced-mode"></a>Вариант 2. Регистрация приложения (расширенный режим).

1. Go toohello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister приложения
2. Введите имя для приложения и адрес электронной почты. 
3. Убедитесь, что параметр hello *интерактивной установки* не установлен
4.  Щелкните `Add Platform`, а затем выберите `Web`.
5. Добавить hello `Redirect URL` , соответствующие URL-адрес toohello приложения на основе веб-сервера. В разделах hello ниже инструкции о том, как tooset / получить URL-адрес перенаправления hello в Visual Studio и Python.
6. Нажмите кнопку *Сохранить*

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>Инструкции Visual Studio для получения URL-адреса перенаправления
> Выполните инструкции tooobtain hello перенаправление URL-адреса.
> 1.    В *обозревателе решений*, выберите проект hello и просмотрите hello `Properties` окна (Если вы не видите окно «Свойства», нажмите клавишу `F4`)
> 2.    Скопируйте значение hello из `URL` toohello буфер обмена:<br/> ![Свойства проекта](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    Перейдите назад toohello *портала регистрации приложения* и вставьте значение hello как `Redirect URL` и нажмите кнопку «Сохранить»

<p/>

> #### <a name="setting-redirect-url-for-python"></a>Настройка URL-адреса перенаправления для Python
> Для Python можно задать порт веб-сервера hello через командную строку. Эта интерактивная программа установки использует hello порт 8080 для ссылки, но чувствовать себя свободного toouse все порты доступны. В любом случае следуйте инструкциям hello ниже tooset копирование URL-адрес перенаправления сведения о регистрации приложения hello.<br/>
> - Переключиться назад toohello *портала регистрации приложения* и задайте `http://localhost:8080/` как `Redirect URL`, или используйте `http://localhost:[port]/` при использовании другой номер порта TCP (где *[порт]* — hello пользовательские TCP-порт номер) и нажмите кнопку «Сохранить»


#### <a name="configure-your-javascript-spa"></a>Настройка одностраничного приложения JavaScript

1.  Создайте файл с именем `msalconfig.js` со сведениями о регистрации приложения hello. Если вы используете Visual Studio, выберите hello проектов (корневой папки проекта,), щелкните правой кнопкой мыши и выберите: `Add`  >  `New Item`  >  `JavaScript File`. Назовите класс `msalconfig.js`.
2.  Добавьте следующий код tooyour hello `msalconfig.js` файла:

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
Замените <code>Enter_the_Application_Id_here</code> с только что зарегистрирован идентификатор приложения hello
</li>
</ol>
