---
title: "aaaAzure список учетных записей хранения"
description: "Управление параметров учетной записи хранилища с помощью hello набора средств Azure для Eclipse"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a>Список учетных записей хранения Azure
Включение учетных записей хранилища Azure Загрузите toobe расположения, используемые для JDK, сервера приложений и произвольных компонентов, а также для хранения состояния при использовании кэширования. Eclipse ведет список известных учетных записей хранения, доступные tooyour проектов в рабочей области Eclipse. tooopen hello **учетные записи хранения** отправной точкой является используется toomanage, список, в Eclipse, щелкните **окна**, нажмите кнопку **предпочтения**, разверните **Azure** , а затем нажмите кнопку **учетные записи хранения**.

Hello ниже показан hello **учетные записи хранения** диалогового окна.

![][ic719496]

Это диалоговое окно можно также открыть из **учетные записи** ссылку в диалоговых окнах, использующих учетные записи хранения, например hello следующее:

* Hello **JDK** вкладка hello **конфигурации сервера** диалогового окна.
* Hello **сервера** вкладка hello **конфигурации сервера** диалогового окна.
* Hello **добавить компонент** диалогового окна.
* Hello **кэширование** диалоговое окно свойств.

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a>tooimport хранилищем учетных записей с помощью файла параметров публикации
1. В рамках hello **учетные записи хранения** диалоговое окно, нажмите кнопку **импорта данных из файла параметров публикации**.

2. (Пропустите этот шаг при сохранении публикации параметров файла tooyour локальном компьютере.) В hello **Импорт сведений о подписке** диалоговое окно, нажмите кнопку **загрузить файл параметров публикации**. Если вы еще не выполнили вход в учетную запись Azure, появится запрос toolog в. Затем вам будет предложено toosave Azure файл параметров публикации. (Можно игнорировать hello инструкции, приведенные на страницах входа hello - они предоставляются hello портал Azure и предназначены для пользователей Visual Studio.) Сохраните tooyour локального компьютера.

3. По-прежнему в hello **Импорт сведений о подписке** диалоговое окно, нажмите кнопку hello **Обзор** кнопку, выберите hello опубликовать файл параметров, который ранее сохранили локально и нажмите кнопку **откройте**.

4. Нажмите кнопку **ОК** tooclose hello **Импорт сведений о подписке** диалогового окна.

## <a name="toocreate-a-new-storage-account"></a>toocreate новой учетной записи хранения
1. В рамках hello **учетные записи хранения** диалоговое окно, нажмите кнопку **добавить**.

2. В рамках hello **добавления учетной записи хранения** диалоговое окно, нажмите кнопку **New**.

3. В рамках hello **новой учетной записи хранения** диалогового окна, укажите значения для следующего hello:

   * имя учетной записи хранения;

   * Расположение учетной записи хранилища hello.

   * Описание учетной записи хранилища hello.

   * Учетная запись хранения Hello подписки toowhich hello принадлежит.

4. Нажмите кнопку **ОК** tooclose hello **новой учетной записи хранения** диалогового окна.

Он может занять несколько минут для создания учетной записи toobe вашего хранилища система. После его создания, нажмите кнопку **ОК** tooclose hello **добавления учетной записи хранения** диалоговое окно и учетной записи хранилища будут добавлены toohello список доступных учетных записей хранилища.

## <a name="tooadd-an-existing-storage-account-toohello-list"></a>tooadd существующего списка toohello учетной записи хранилища
1. Если вы еще нет учетной записи, создайте его с хранилища Azure hello действий перечислены в hello **toocreate новый раздел учетной записи хранилища** выше. (Кроме того, можно создать новую учетную запись хранения в hello [портала управления Azure][Azure Management Portal].)

2. В рамках hello **учетные записи хранения** диалоговое окно, нажмите кнопку **добавить**.

3. В рамках hello **добавления учетной записи хранения** диалоговое окно, введите значения для **имя** и **ключ доступа**. Hello учетной записи имя и ключ доступа должен быть существующей учетной записи хранилища Azure. Используйте hello **хранения** раздел hello [портала управления Azure] [ Azure Management Portal] tooview вашей учетной записи хранения имен и ключей. Ваш **добавления учетной записи хранения** диалоговое окно будет выглядеть аналогично toohello следующее.
   
   ![][ic719497]

4. Нажмите кнопку **ОК** tooclose hello **добавления учетной записи хранения** диалогового окна.

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a>toomodify toouse учетной записи хранилища новый ключ доступа
1. В рамках hello **учетные записи хранения** диалоговое окно, выберите учетную запись хранилища hello tooedit и нажмите кнопку **изменить**.

2. В рамках hello **изменения ключа доступа учетной записи хранения** диалогового окна, изменения hello **ключ доступа** значение.

3. Нажмите кнопку **ОК** tooclose hello **изменения ключа доступа учетной записи хранения** диалогового окна.

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a>tooremove учетную запись хранилища из списка hello, поддерживаемого в Eclipse
1. В рамках hello **учетные записи хранения** диалоговое окно, выберите учетную запись хранилища hello tooedit и нажмите кнопку **удалить**.

2. Нажмите кнопку **ОК** при запрашиваемые tooremove hello учетной записи хранилища.

> [!NOTE]
> Удаление учетной записи хранения hello через hello **учетные записи хранения** диалогового окна удаляется только из hello список учетных записей хранения, можно просмотреть в Eclipse. Не удаляет hello учетной записи хранилища из подписки Azure. Кроме того учетной записи хранилища hello может снова появиться в списке после Eclipse перезагрузит hello сведения о вашей подписке.
> 
> 

## <a name="see-also"></a>См. также
[Набор средств Azure для Eclipse][Azure Toolkit for Eclipse]

[Установка средств Azure для Eclipse hello][Installing hello Azure Toolkit for Eclipse] 

[Создание приложения Hello World для Azure в Eclipse][Creating a Hello World Application for Azure in Eclipse]

Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
