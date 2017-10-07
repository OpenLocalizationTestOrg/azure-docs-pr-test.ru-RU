---
title: "aaaCreate первый веб-приложения Java в Azure"
description: "Узнайте, как toorun веб-приложений в службе приложений путем развертывания базовое приложение Java."
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a>Создание первого веб-приложения Java в Azure

Hello [веб-приложений](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) функция [службе приложений Azure](../app-service/app-service-value-prop-what-is.md) предоставляет высокую степень масштабируемости, самостоятельно исправления веб-службе размещения. Краткого руководства показано, как toodeploy Java веб-приложения tooApp службы с помощью hello [интегрированной среды разработки Eclipse для разработчиков Java EE](http://www.eclipse.org/).

!["Hello Azure!" Пример веб-приложения](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a>Предварительные требования

toocomplete краткого руководства, установить:

* Hello свободного [интегрированной среды разработки Eclipse для разработчиков Java EE](http://www.eclipse.org/downloads/). В этом кратком руководстве используется Eclipse Neon.
* Hello [средств Azure для Eclipse](/azure/azure-toolkit-for-eclipse-installation).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a>Создание динамических веб-проектов в Eclipse

В Eclipse щелкните **File** (Файл) > **New** (Создать) > **Dynamic Web Project** (Динамический веб-проект).

В hello **динамический веб-проект** диалоговое окно, имя проекта hello **MyFirstJavaOnAzureWebApp**и выберите **Готово**.
   
![Диалоговое окно создания динамического веб-проекта](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a>Добавление страницы JSP

Если обозреватель проектов не отображается, разверните его.

![Рабочая область Java EE для Eclipse](./media/app-service-web-get-started-java/pe.png)

В обозревателе проектов разверните hello **MyFirstJavaOnAzureWebApp** проекта.
Щелкните правой кнопкой мыши **WebContent**, а затем щелкните **New** (Создать) > **JSP File** (JSP-файл).

![Меню для нового JSP-файла в обозревателе проектов](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

В hello **Создание JSP-файла** диалоговое окно:

* Имя файла hello **index.jsp**.
* Выберите **Готово**.

  ![Диалоговое окно New JSP File (Создание JSP-файла)](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

В файле index.jsp hello замените hello `<body></body>` элемент с hello следующая разметка:

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

Сохраните изменения hello.

## <a name="publish-hello-web-app-tooazure"></a>Публикация приложения tooAzure hello web

В обозревателе решений, правой кнопкой мыши проект hello и выберите **Azure** > **опубликовать как веб-приложения Azure**.

![Контекстное меню Publish as Azure Web App (Опубликовать как веб-приложение Azure)](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

В hello **входа в Azure** диалоговое окно, поддержания hello **Interactive** , а затем установите **входа**.

Следуйте инструкциям hello вход.

### <a name="deploy-web-app-dialog-box"></a>Диалоговое окно развертывания веб-приложения

После входа в учетную запись Azure tooyour hello **развертывание веб-приложения** откроется диалоговое окно.

Нажмите кнопку **Создать**.

![Диалоговое окно развертывания веб-приложения](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a>Диалоговое окно "Создание службы приложений"

Hello **Создание приложения службы** откроется диалоговое окно со значениями по умолчанию. Здравствуйте, номер **170602185241** показано в следующих hello изображения отличается диалогового окна.

![Диалоговое окно "Создание службы приложений"](./media/app-service-web-get-started-java/cas1.png)

В hello **Создание приложения службы** диалоговое окно:

* Оставьте имя hello созданный для веб-приложения hello. Это имя должно быть уникальным в Azure. Имя Hello является частью hello URL-адрес для веб-приложения hello. Например: Если имя веб-приложения hello **MyJavaWebApp**, URL-адрес является hello *myjavawebapp.azurewebsites.net*.
* Сохраните контейнер web по умолчанию hello.
* Выберите подписку Azure.
* На hello **план обслуживания приложений** вкладки:

  * **Создать новый**: сохранить по умолчанию hello, которое является именем hello объекта hello план служб приложений.
  * **Location** (Расположение): Выберите **West Europe** (Западная Европа) или ближайшее расположение.
  * **Ценовая категория**: выберите hello свободного параметр. Сведения о функциях см. на странице [цен на службу приложений](https://azure.microsoft.com/pricing/details/app-service/).

   ![Диалоговое окно "Создание службы приложений"](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a>Вкладка Resource group (Группа ресурсов)

Выберите hello **группы ресурсов** вкладки. Оставьте значение по умолчанию создается hello hello группы ресурсов.

![Вкладка Resource group (Группа ресурсов)](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

Нажмите кнопку **Создать**.

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

Hello набора средств Azure создает веб-приложение hello и отображает диалоговое окно хода выполнения.

![Диалоговое окно Create App Service Progress (Прогресс создания службы приложений)](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a>Диалоговое окно развертывания веб-приложения

В hello **развертывание веб-приложения** выберите **развертывание tooroot**. Если вы создали службу приложений в *wingtiptoys.azurewebsites.net* и не следует развертывать toohello корень, hello веб-приложения с именем **MyFirstJavaOnAzureWebApp** развертывается слишком *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.

![Диалоговое окно развертывания веб-приложения](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

показывает диалоговое окно приветствия hello Azure, JDK и выбора контейнера web.

Выберите **развернуть** toopublish hello web app tooAzure.

По завершении публикации hello выберите hello **опубликовано** ссылку в hello **журнал действий Azure** диалоговое окно.

![Диалоговое окно "Журнал действий Azure"](./media/app-service-web-get-started-java/aal.png)

Поздравляем! Успешно завершены вашей tooAzure web app. 

!["Hello Azure!" Пример веб-приложения](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a>Обновить веб-приложение hello

Изменение hello образец JSP кода tooa другое сообщение.

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

Сохраните изменения hello.

В обозревателе решений, правой кнопкой мыши проект hello и выберите **Azure** > **опубликовать как веб-приложения Azure**.

Hello **развертывание веб-приложения** откроется диалоговое окно и отображает hello службы приложений, созданный ранее. 

> [!NOTE]
> Выберите **развертывание tooroot** каждый раз при публикации.
>

Выберите веб-приложение hello и выберите **развернуть**, который публикует изменения hello.

Здравствуйте, когда **публикации** появляется ссылка, выберите его toobrowse toohello веб-приложение и просмотреть изменения hello.

## <a name="manage-hello-web-app"></a>Управление веб-приложения hello

Go toohello <a href="https://portal.azure.com" target="_blank">портал Azure</a> toosee hello веб-приложения, созданный вами.

Hello в левом меню, выберите **групп ресурсов**.

![Tooresource группы переходов портала](media/app-service-web-get-started-java/rg.png)

Выберите группу ресурсов hello. Страница приветствия показывает hello ресурсы, созданные в этом кратком руководстве.

![Группа ресурсов myresourcegroup.](media/app-service-web-get-started-java/rg2.png)

Выберите hello веб-приложения (**170602193915 веб-приложение** в hello предшествующий изображения).

Hello **Обзор** появится страница. Эта страница позволяет получить представление о том, как это приложение hello. Вы можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление. закладки Hello hello левой части страницы приветствия показывают hello различных конфигураций, которые можно открыть. 

![Страница службы приложений на портале Azure](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Сопоставление пользовательского домена](app-service-web-tutorial-custom-domain.md)
