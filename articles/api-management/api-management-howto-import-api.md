---
title: "aaaImport API в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как tooimport API и операций в API управления Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a>Как tooimport hello определение API и операций в службе управления API Azure
В службе управления API можно создать новые интерфейсы API и операции hello добавлять вручную или hello API могут быть импортированы вместе с операциями hello за один шаг.

API-интерфейсы и связанных с ними операций можно импортировать с помощью hello следующие форматы.

* WADL
* Swagger

В этом руководстве показано, как создать новый API и импортировать его операции за один шаг. Сведения для создания вручную API и добавление операций в разделе [как toocreate API-интерфейсы] [ How toocreate APIs] и [как tooan tooadd операций API] [ How tooadd operations tooan API].

## <a name="import-api"> </a>Импорт API
API-интерфейсы создаются и настраиваются на портале hello издателя. tooaccess hello издателя, щелкните **портал издателя** в hello портала Azure для службы управления API. Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.

![Портал издателя][api-management-management-console]

Нажмите кнопку **API-интерфейсы** из hello **API управления** меню hello слева, а затем нажмите **импорта API**.

![Импортировать API][api-management-import-apis]

Hello **импорта API** окно имеет три вкладки, которые соответствуют toohello тремя способами tooprovide hello API спецификации.

* **Из буфера обмена** позволяет toopaste hello API спецификации в hello указанного текстового поля.
* **Из файла** позволяет toobrowse tooand hello, выберите файл, содержащий спецификацию hello API.
* **С URL-адреса** позволяет спецификации toohello toosupply hello URL-адрес для hello API.

![Формат импорта API][api-management-import-api-clipboard]

После предоставления hello API спецификации, используйте переключатели hello hello правой tooindicate hello спецификации формата. поддерживаются следующие форматы Hello.

* WADL
* Swagger

Затем, введите **Суффикс URL-адреса веб-API**. Это присоединенных toohello базовый URL-адрес для службы управления API. Hello базовый URL-адрес является общим для всех интерфейсов API, размещенных на каждом экземпляре служб управления API. API управления API-интерфейсы отличает их суффикс и поэтому должно быть уникальным для каждый API в конкретном экземпляре служб управления API суффикс hello.

После ввода всех значений нажмите кнопку **Сохранить** toocreate hello API и hello связанные операции. 

> [!NOTE]
> Инструкции по импорту API базового калькулятора в формате Swagger см. в статье [Начало работы со службой управления Azure API](api-management-get-started.md).
> 
> 

## <a name="export-api"> </a> Экспорт API
В дополнение tooimporting новые интерфейсы API, можно экспортировать определения hello собственные интерфейсы API из портала издателя hello. toodo таким образом, нажмите кнопку **экспорта API** из hello **вкладка со сводкой** из вашего **API**.

![Экспорт API][api-management-export-api]

Интерфейсы API можно экспортировать в формате WADL или Swagger. Выберите нужный формат hello, щелкните **Сохранить**и выберите местоположение hello в какой файл toosave hello.

![Формат экспорта API][api-management-export-api-format]

## <a name="next-steps"> </a>Дальнейшие действия
После создания API и hello операции импорта, можно просмотреть и настроить дополнительные параметры, добавьте tooa hello API продукта и опубликовать его, чтобы он был доступен для разработчиков. Дополнительные сведения см. в разделе hello следующие руководства.

* [Как параметры tooconfigure API][How tooconfigure API settings]
* [Как toocreate и публикация продукта][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings
