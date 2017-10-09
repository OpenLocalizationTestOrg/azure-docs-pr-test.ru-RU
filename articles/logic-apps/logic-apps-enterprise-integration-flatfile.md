---
title: "aaaEncode или декодировать неструктурированных файлов в приложения логики Azure | Документы Microsoft"
description: "Как toouse hello файл файл кодировщиком или декодером в hello пакет интеграции Enterprise в свои приложения логики"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 82152dab-c7ad-43df-b721-596559703be8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 2c295586625fd84366ec7cbafdcebf0489ba234d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-enterprise-integration-with-flat-files"></a>Обзор интеграции Enterprise с неструктурированными файлами

Вы можете tooencode XML содержимого перед отправкой tooa деловых партнеров в сценарии бизнес бизнес (B2B). В приложении логики можно использовать hello неструктурированного файла, кодировку соединитель toodo это. Hello создаваемого логику приложения может получать XML содержимое из разнообразных источников, включая с триггером запроса HTTP, из другого приложения или даже от одного из hello многие [соединители](../connectors/apis-list.md). Дополнительные сведения о логике приложения. в разделе hello [логику приложения документации](logic-apps-what-are-logic-apps.md "Дополнительные сведения о приложении логики").  

## <a name="create-hello-flat-file-encoding-connector"></a>Создание соединителя кодирования неструктурированного файла hello
Выполните эти шаги tooadd неструктурированного файла, кодировку соединитель tooyour логику приложения.

1. Создание приложения логики и [связать его учетной записи интеграции tooyour](logic-apps-enterprise-integration-accounts.md "узнать toolink tooa логики интеграции учетной записи приложения"). Эта учетная запись содержит схему hello, будет использоваться hello tooencode XML-данных.  
2. Добавить **запрос — при HTTP-запрос получен** триггер tooyour логику приложения.  
   ![Снимок экрана tooselect триггера](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
3. Добавьте hello неструктурированного файла, кодировку действие, следующим образом:
   
    а. Выберите hello **, а также** входа.
   
    b. Выберите hello **добавить действие** связи (появляется после выбора hello "плюс").
   
    c. Введите в поле поиска hello, *плоский* toofilter все hello один toohello действия, которые должны toouse.
   
    d. Выберите hello **кодирования неструктурированного файла** параметр из списка hello.   
   ![Снимок экрана с параметром "Кодирование неструктурированного файла"](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
4. На hello **кодирования неструктурированного файла** диалоговое окно, выберите hello **содержимого** текстовое поле.  
   ![Снимок экрана с текстовым полем "Содержимое"](media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)  
5. Выберите тег текст hello в качестве содержимого, которое следует tooencode hello. тег текст Hello будет заполнять поля "контент" hello.     
   ![Снимок экрана с тегом body](media/logic-apps-enterprise-integration-flatfile/flatfile-4.png)  
6. Выберите hello **имя схемы** поле, а затем выберите hello схемы требуется toouse tooencode hello входного содержимого.    
   ![Снимок экрана с полем списка "Имя схемы"](media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)  
7. Сохраните результаты своих действий.   
   ![Снимок экрана со значком "Сохранить"](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)  

На этом настройка соединителя для кодирования неструктурированных файлов завершена. В реальных приложениях вы можете toostore hello закодированные данные в бизнес-приложений, таких как Salesforce. Или вы можете отправлять этой tooa закодированные данные торгового партнера. Можно легко добавить выходные данные hello toosend действие hello кодирование tooSalesforce действие или tooyour торгового партнера, с помощью любого из hello других разъемам.

Теперь можно проверить соединителя путем создания конечной точки HTTP запроса toohello и включая hello XML-содержимого в тексте hello hello запроса.  

## <a name="create-hello-flat-file-decoding-connector"></a>Создание соединителя декодирование неструктурированного файла hello

> [!NOTE]
> toocomplete эти шаги, необходимые toohave файл схемы уже отправлен во внимание интеграции.

1. Добавить **запрос — при HTTP-запрос получен** триггер tooyour логику приложения.  
   ![Снимок экрана tooselect триггера](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
2. Добавьте неструктурированного файла hello декодирования действия, как показано ниже:
   
    а. Выберите hello **, а также** входа.
   
    b. Выберите hello **добавить действие** связи (появляется после выбора hello "плюс").
   
    c. Введите в поле поиска hello, *плоский* toofilter все hello один toohello действия, которые должны toouse.
   
    d. Выберите hello **декодирование неструктурированного файла** параметр из списка hello.   
   ![Снимок экрана с параметром "Декодирование неструктурированного файла".](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
3. Выберите hello **содержимого** элемента управления. Это позволяет создать список содержимого hello из предыдущих шагах, которые можно использовать в качестве содержимого toodecode hello. Обратите внимание, что hello *текст* из hello Входящий HTTP-запрос — доступные toobe используется как hello toodecode содержимого. Можно также ввести непосредственно в hello hello содержимого toodecode **содержимого** элемента управления.     
4. Выберите hello *текст* тег. Уведомление тега body hello стал hello **содержимого** элемента управления.
5. Выберите имя hello hello схемы, которые должны toouse toodecode hello содержимого. Hello следующем снимке экрана показано, что *OrderFile* — имя выбранной схеме hello. Это имя схемы будут переданы в учетной записи интеграции hello ранее.
   
   ![Снимок экрана с диалоговым окном "Декодирование неструктурированного файла"](media/logic-apps-enterprise-integration-flatfile/flatfile-decode-1.png)    
6. Сохраните результаты своих действий.  
   ![Снимок экрана со значком "Сохранить"](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)    

На этом настройка соединителя для декодирования неструктурированных файлов завершена. В реальных приложениях вы можете toostore hello декодирования данных в бизнес приложениях, таких как Salesforce. Можно легко добавить выходные данные hello toosend действие hello декодирования tooSalesforce действие.

Теперь можно проверить соединителя, делая конечной точки HTTP запроса toohello и включая hello XML-содержимого нужно toodecode в тексте hello hello запроса.  

## <a name="next-steps"></a>Дальнейшие действия
* [Дополнительные сведения о hello пакет интеграции Enterprise](logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции Enterprise").  

