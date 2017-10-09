---
title: "aaaIntegrate учетной записи хранилища Azure с Azure CDN | Документы Microsoft"
description: "Узнайте, как содержимое toouse hello Azure сеть доставки содержимого (CDN) toodeliver высокой пропускной способностью путем кэширования больших двоичных объектов из хранилища Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a>Интеграция учетной записи хранения Azure с Azure CDN
CDN может быть включено toocache содержимого из вашего хранилища Azure. Он предлагает разработчикам глобальное решение по доставке контента с высокой пропускной способностью путем кэширования BLOB-объекты и статическое содержимое вычислительных экземпляров в физических узлах в hello США, Европе, Азии, Австралии и Южной Америки.

## <a name="step-1-create-a-storage-account"></a>Шаг 1. Создание учетной записи хранения
Используйте следующие процедуры toocreate новой учетной записи хранения для подписки Azure hello. Учетная запись хранения предоставляет доступ к службам хранилища Azure. Hello учетной записи хранилища представляет высший уровень hello hello пространство имен для доступа ко всем hello компоненты службы хранилища Azure: BLOB-объект службы, службы очередей и таблиц. Дополнительные сведения см. в разделе toohello [tooMicrosoft введение хранилища Azure](../storage/common/storage-introduction.md).

toocreate учетной записи хранилища, необходимо быть Здравствуйте, администратор служб или администратором hello связанные подписки.

> [!NOTE]
> Существует несколько способов, которые можно использовать toocreate учетной записи хранилища, включая hello портала Azure и Powershell.  В этом учебнике мы будем работать с hello портала Azure.  
> 
> 

**toocreate учетную запись хранения для подписки Azure**

1. Войдите в toohello [портала Azure](https://portal.azure.com).
2. В верхнем левом углу hello, выберите **New**. В hello **New** диалоговое окно, выберите **данные + хранилище**, нажмите кнопку **учетной записи хранилища**.
    
    Hello **создать учетную запись хранения** колонке отображается.   

    ![Учетная запись хранения][create-new-storage-account]  

3. В hello **имя** введите имя дочернего домена. Запись может содержать от 3 до 24 строчных букв и цифр.
   
    Это значение становится именем узла hello в URI, который используется для адресации ресурсов больших двоичных объектов, очередей или таблиц для подписки hello hello. Для обращения к ресурсу контейнера в hello службы BLOB-объектов, необходимо использовать URI в hello следующая формата, где  *&lt;StorageAccountLabel&gt;*  ссылается toohello значения, введенного в **введите URL-адрес**:
   
    http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;мой_контейнер&gt;*
   
    **Важно:** hello URL-адрес метки формы hello дочерний домен учетной записи хранения hello URI и должно быть уникальным среди всех размещенных служб в Azure.
   
    Это значение также используется как hello имя этой учетной записи хранения в портале hello, или если программный доступ к этой учетной записи.
4. Оставьте значения по умолчанию hello для **модель развертывания**, **учетной записи kind**, **производительности**, и **репликации**. 
5. Выберите hello **подписки** использование учетной записи хранилища hello со.
6. Выберите или создайте **группу ресурсов**.  Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Выберите расположение для вашей учетной записи хранения.
8. Щелкните **Создать**. Создание учетной записи хранения hello Hello процесс может занять несколько минут toocomplete.

## <a name="step-2-enable-cdn-for-hello-storage-account"></a>Шаг 2: Включение CDN для учетной записи хранения hello

Благодаря интеграции новейшие hello теперь можно включить CDN для вашей учетной записи, не выходя из портала модуля хранилища. 

1. Выберите учетную запись хранения hello, поиск «CDN» или прокрутки вниз от hello левом меню навигации, а затем нажмите кнопку «Azure CDN».
    
    Hello **Azure CDN** колонке отображается.

    ![Навигация для включения CDN][cdn-enable-navigation]
    
2. Создайте новую конечную точку, введя hello необходимые сведения
    - **Профиль CDN**. Вы можете создать новый профиль или использовать существующий.
    - **Ценовая категория**: достаточно tooselect ценовую категорию, если создается новый профиль CDN.
    - **Имя конечной точки CDN**. Введите имя конечной точки.

    > [!TIP]
    > Конечная точка CDN Hello создан использует имя узла hello учетной записи как источник по умолчанию.

    ![cdn new endpoint creation][cdn-new-endpoint-creation]

3. После создания новой конечной точки hello будут отображаться в список конечных точек hello выше.

    ![Новая конечная точка хранилища CDN][cdn-storage-new-endpoint]

> [!NOTE]
> Вы можете перейти tooAzure CDN расширения tooenable CDN. [Учебника](#Tutorial-cdn-create-profile).
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a>Шаг 3. Включение дополнительных функций CDN

Из колонки «Azure CDN» учетной записи хранилища щелкните конечную точку CDN hello из hello список tooopen CDN конфигурации колонки. Можно включить дополнительные функции CDN, например сжатие, строку запроса, геофильтрацию. Кроме того, можно также добавить конечную точку CDN tooyour сопоставления пользовательского домена и включить пользовательский домен HTTPS.
    
![Конфигурация CDN хранилища CDN][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a>Шаг 4. Доступ к содержимому CDN
tooaccess кэшированного содержимого на hello CDN, hello используйте URL-адрес CDN указано на портале hello. Hello адрес кэшированного BLOB-объекта будет примерно toohello следующее:

http://<*имя_конечной_точки*\>.azureedge.net/<*общедоступный_контейнер*\>/<*имя_большого_двоичного_объекта*\>

> [!NOTE]
> После включения учетной записи хранилища CDN доступ tooa все общедоступные объекты могут быть кэшированы пограничное кэширование CDN. Если изменить объект, который в настоящее время кэшированных в hello CDN hello новое содержимое будет недоступен через hello CDN пока hello CDN обновляет его содержимое по окончании периода содержимого time-to-live hello в кэше.
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a>Шаг 5: Удаление содержимого из CDN hello
Если вы больше не хотите toocache объекта в hello Azure доставки содержимого сети (CDN), можно выполнить одно из hello следующие шаги:

* Можно сделать hello контейнер закрытым, а не открытым. В разделе [управления toocontainers анонимный доступ для чтения и большие двоичные объекты](../storage/blobs/storage-manage-access-to-resources.md) для получения дополнительной информации.
* Можно отключить или удалить конечную точку CDN hello, с помощью портала управления hello.
* Вы можете изменить вашей размещенной службы toono дольше ответ toorequests для hello объекта.

Объект, уже кэшированный в hello CDN будет остаются в кэше до истечения периода времени жизни hello объекта hello, или пока не будет очищено hello конечной точки. По истечении периода времени существования hello hello CDN проверяет toosee ли конечная точка CDN hello все еще действительна, hello объекта применимым для анонимного доступа. Если это не так, затем hello объекта больше не кэшируются.

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Как tooMap содержимого CDN tooa пользовательского домена](cdn-map-content-to-custom-domain.md)
* [Включение протокола HTTPS для личного домена Azure CDN](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
