---
title: "aaaAzure AD v2 JS SPA интерактивной установки — Настройка (ARP) | Документы Microsoft"
description: "В этой статье описано, как приложения JavaScript SPA могут вызывать API, которому необходимы маркеры доступа, с помощью конечной точки Azure Active Directory версии 2 (ARP)."
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
ms.openlocfilehash: 157f4e342cd684294e24da6ee1fad8a7c2fc266a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Добавить tooyour сведения о регистрации приложения hello приложения

На этом шаге требуется tooconfigure hello перенаправления URL-адрес приложения регистрационную информацию и затем добавить приложения JavaScript SPA tooyour идентификатор приложения hello.

### <a name="configure-redirect-url"></a>Настройка URL-адреса перенаправления

Настройка hello `Redirect URL` поле выше URL-адрес hello index.html страницы на основе веб-сервера, а затем щелкните *обновление*.


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>Инструкции Visual Studio для получения URL-адреса перенаправления
> tooobtain перенаправления URL-адрес, выполните приведенные ниже инструкции hello:
> 1.    В *обозревателе решений*, выберите проект hello и просмотрите hello `Properties` окна (Если вы не видите окно «Свойства», нажмите клавишу `F4`)
> 2.    Скопируйте значение hello из `URL` toohello буфер обмена:<br/> ![Свойства проекта](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    Вставьте значение hello как `Redirect URL` на hello верхней части этой страницы, нажмите кнопку`Update`

<p/>

> #### <a name="setting-redirect-url-for-python"></a>Настройка URL-адреса перенаправления для Python
> Для Python можно задать порт веб-сервера hello через командную строку. Эта интерактивная программа установки использует hello порт 8080 для ссылки, но чувствовать себя свободного toouse все порты доступны. В любом случае следуйте инструкциям hello ниже tooset копирование URL-адрес перенаправления сведения о регистрации приложения hello.<br/>
> Задать `http://localhost:8080/` как `Redirect URL` hello верхней части этой страницы, или использовать `http://localhost:[port]/` при использовании другой номер порта TCP (где *[порт]* — hello пользовательский номер порта TCP) и нажмите кнопку «Обновить»

### <a name="configure-your-javascript-spa-application"></a>Настройка одностраничного приложения JavaScript

1.  Создайте файл с именем `msalconfig.js` со сведениями о регистрации приложения hello. Если вы используете Visual Studio, выберите hello проектов (корневой папки проекта,), щелкните правой кнопкой мыши и выберите: `Add`  >  `New Item`  >  `JavaScript File`. Назовите класс `msalconfig.js`.
2.  Добавьте следующий код tooyour hello `msalconfig.js` файла:

```javascript
var msalconfig = {
    clientID: "[Enter hello application Id here]",
    redirectUri: location.origin
};
``` 
