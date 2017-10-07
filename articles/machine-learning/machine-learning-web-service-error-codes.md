---
title: "коды ошибок API-интерфейса REST обучения машины aaaAzure | Документы Microsoft"
description: "Эти коды ошибок могут быть возвращены операцией с веб-службой машинного обучения Azure."
keywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 0923074b-3728-439d-a1b8-8a7245e39be4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 11/16/2016
ms.author: garye
ms.openlocfilehash: 9495c8ef16e684d3c8978bcd11747cf95227b091
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-rest-api-error-codes"></a>Коды ошибок REST API машинного обучения
 
Hello следующие коды ошибок могут возвращаться операцией в веб-службы машинного обучения Azure.
 
## <a name="badargument-http-status-code-400"></a>BadArgument (код состояния HTTP: 400)
 
Указан недопустимый аргумент.
 
Ошибки этого класса означают, что указанный где-то аргумент является недопустимым. Возможно, учетные данные или расположение хранилища Azure toosomething передан toohello веб-службы. См. в поле ошибки «код» hello в toodiagnose раздела «подробности» hello, какой из аргументов недопустим.
 
| Код ошибки | Сообщение для пользователя |
| ---------- |--------------|
| BadParameterValue | Указанное значение параметра Hello не удовлетворяет hello правило параметра на параметр hello |
| BadSubscriptionId | Подписка Hello идентификатор, используемый tooscore не присутствует в ресурсе hello hello |
| BadVersionCall | Недопустимая версия параметр был передан во время вызова hello API: {0}. Проверьте hello страницы справки для передачи hello правильную версию API и повторите попытку. |
| BatchJobInputsNotSpecified | следующие необходимые входными данными Hello не были указаны с запросом hello: {0}. Убедитесь, что указаны все входные данные, и повторите попытку. |
| BatchJobInputsTooManySpecified | запрос Hello указать несколько входов, не определенной в службе hello. Список принимаемых входных данных: {0}. Убедитесь, что все входные данные указаны правильно, и повторите попытку. |
| BlobNameTooLong | Указан слишком длинный путь к хранилищу BLOB-объектов Azure для выходных диагностических данных: {0}. Сократите путь hello и повторите попытку. |
| BlobNotFound | Не удается tooaccess hello предоставленные Azure blob - {0}.  Сообщение об ошибке Azure: {1}. |
| ContainerIsEmpty | Не указано имя контейнера службы хранилища Azure. Укажите допустимое имя контейнера и повторите попытку. |
| ContainerSegmentInvalid | Недопустимое имя контейнера. Укажите допустимое имя контейнера и повторите попытку. |
| ContainerValidationFailed | Проверка контейнера BLOB-объектов завершилась следующей ошибкой: {0}. |
| DataTypeNotSupported | Указаны данные неподдерживаемого типа. Укажите данные допустимых типов и повторите попытку. |
| DuplicateInputInBatchCall | Hello пакетный запрос является недопустимым. Невозможно указать одного и нескольких ввода данных на hello же время. Удалите один из этих элементов из запроса hello и повторите попытку. |
| ExpiryTimeInThePast | Время истечения срока действия находится в прошлом hello: {0}. Укажите время окончания срока действия в будущем в формате UTC и повторите попытку. toonever срок действия, в качестве tooNULL время истечения срока действия. |
| IncompleteSettings | Параметры диагностики являются неполными. |
| InputBlobRelativeLocationInvalid | Не указано имя большого двоичного объекта службы хранилища Azure. Укажите допустимое имя большого двоичного объекта и повторите попытку. |
| InvalidBlob | Недопустимая спецификация большого двоичного объекта: {0}. Убедитесь в правильности строки подключения и относительного пути или спецификации маркера SAS и повторите попытку. |
| InvalidBlobConnectionString | Здравствуйте, строка подключения, указанная для одного из больших двоичных объектов ввода вывода hello недопустимое: {0}. Исправьте ее и повторите попытку. |
| InvalidBlobExtension | Здравствуйте большого двоичного объекта ссылка: {0} недопустим или отсутствует файл имеет расширение. Для этого типа выходных данных поддерживаются следующие расширения файла: "{1}". |
| InvalidInputNames | Недопустимый входной имена, указанный в запросе hello: {0}. Сопоставьте hello ввода toohello правильной службе входные данные и повторите попытку. |
| InvalidOutputOverrideName | Недопустимое переопределяемое имя выходных данных: {0}. Служба Hello не имеет выходной узел с таким именем. Передайте в toooverride правильных выходных данных для имени узла (применяется чувствительность к регистру). |
| InvalidQueryParameter | Недопустимый параметр запроса "{0}". {1} |
| MissingInputBlobInformation | Отсутствуют сведения о большом двоичном объекте службы хранилища Azure. Укажите допустимую строку подключения и относительный путь или универсальный код ресурса (URI) и повторите попытку. |
| MissingJobId | Идентификатор задания не указан. Задание идентификатора возвращается при отправке задания для hello первый раз. Проверьте hello идентификатор задания указано правильно и повторите попытку. |
| MissingKeys | Ключи не указаны, либо не предоставлен первичный или вторичный ключ. |
| MissingModelPackage | Не указан идентификатор пакета модели или пакет модели. Укажите допустимый идентификатор пакета модели или пакет модели и повторите попытку. |
| MissingOutputOverrideSpecification | Hello в запросе отсутствует спецификация hello больших двоичных объектов для переопределения вывода {0}. Укажите расположение большого двоичного объекта допустимым с запросом hello, или удалите hello выходной спецификации при необходимости расположение переопределение. |
| MissingRequestInput | Hello веб-служба ожидает входных данных, но не ввод был предоставлен. Убедитесь приведены допустимые входные данные с учетом hello опубликованные входные порты в модели hello и повторите попытку. |
| MissingRequiredGlobalParameters | Указаны не все необходимые параметры веб-службы. Проверьте параметры hello для hello модули указаны правильно и повторите попытку. |
| MissingRequiredOutputOverrides | При вызове зашифрованные конечной точки службы, он является обязательным toopass в выходные данные переопределения для выходных данных все службы hello. Сейчас отсутствуют переопределения следующих выходных данных: {0} |
| MissingWebServiceGroupId | Не указан идентификатор группы веб-службы. Укажите допустимый идентификатор группы веб-службы и повторите попытку. |
| MissingWebServiceId | Не указан идентификатор веб-службы. Укажите допустимый идентификатор веб-службы и повторите попытку. |
| MissingWebServicePackage | Не указан пакет веб-службы. Укажите допустимый пакет веб-службы и повторите попытку. |
| MissingWorkspaceId | Не указан идентификатор рабочей области. Укажите допустимый идентификатор рабочей области и повторите попытку. |
| ModelConfigurationInvalid | Недопустимая модель конфигурации в пакете модели hello. Убедитесь, конфигурация модели hello определением выходные данные конечные точки, ошибка std конечной точки и std системы конечной точки и повторите попытку. |
| ModelPackageIdInvalid | Недопустимый идентификатор пакета модели. Проверьте правильность этого пакет модели hello идентификатор и повторите попытку. |
| RequestBodyInvalid | Не предоставлен текст запроса или Ошибка десериализации тела запроса hello. |
| RequestIsEmpty | Запрос не указан. Укажите допустимый запрос и повторите попытку. |
| UnexpectedParameter | Указан непредвиденный параметр. Проверьте, что имена всех параметров указаны правильно и что передаются только ожидаемые параметры, после чего повторите попытку. |
| UnknownError | Произошла неизвестная ошибка. |
| UserParameterInvalid | {0} |
| WebServiceConcurrentRequestRequirementInvalid | Не удается изменить требуемое число одновременных запросов для веб-службы {0}. |
| WebServiceIdInvalid | Указан недопустимый идентификатор веб-службы. Идентификатором веб-службы должен быть допустимый идентификатор GUID. |
| WebServiceTooManyConcurrentRequestRequirement | Не удается задать toomore требование одновременных запросов, чем {0}. |
| WebServiceTypeInvalid | Указан недопустимый тип веб-службы. Убедитесь, что hello допустимый веб-службы используется правильный и повторите попытку. Допустимые типы веб-службы: {0}. |
 
## <a name="baduserargument-http-status-code-400"></a>BadUserArgument (код состояния HTTP: 400)
 
Указан недопустимый аргумент пользователя.
 
| Код ошибки | Сообщение для пользователя |
| ---------- |--------------|
| InputMismatchError | Входные данные не соответствует схеме входного порта. |
| InputParseError | Произошла ошибка анализа входного вектора.  Убедитесь, что входной вектор hello имеет hello правильное количество столбцов и типов данных.  Дополнительная информация: {0}. |
| MissingRequiredGlobalParameters | Отсутствуют параметры ожидаемый hello веб-службы. Проверьте правильность всех параметров требуется hello, ожидаемый hello веб-службы и повторите попытку. |
| UnexpectedParameter | Убедитесь, что были переданы параметры, ожидаемые веб-службой hello обязательные только hello и повторите попытку. |
| UserParameterInvalid | {0} |
 
## <a name="invalidoperation-http-status-code-400"></a>InvalidOperation (код состояния HTTP: 400)
 
Недопустимый запрос Hello в текущем контексте hello.
 
| Код ошибки | Сообщение для пользователя |
| ---------- |--------------|
| CannotStartJob | Hello задания невозможен, так как он находится в состоянии {0}. |
| IncompatibleModel | модель Hello несовместима с версией hello запроса. версия запроса Hello поддерживает только одной datatable выходные данные модели. |
| MultipleInputsNotAllowed | модель Hello не допускает несколько входов. |
 
## <a name="libraryexecutionerror-http-status-code-400"></a>LibraryExecutionError (код состояния HTTP: 400)
 
При выполнении модуля произошла внутренняя ошибка библиотеки.
 
 
## <a name="moduleexecutionerror-http-status-code-400"></a>ModuleExecutionError (код состояния HTTP: 400)
 
Ошибка выполнения модуля.
 
 
## <a name="webservicepackageerror-http-status-code-400"></a>WebServicePackageError (код состояния HTTP: 400)
 
Указан недопустимый пакет веб-службы. Проверьте правильность предоставленных веб-службы hello пакета и повторите попытку.
 
| Код ошибки | Сообщение для пользователя |
| ---------- |--------------|
| FormatError | Hello веб-службы пакет имеет неправильный формат. Дополнительные сведения: {0}. |
| RuntimesError | Недопустимый граф пакета службы web Hello. Дополнительные сведения: {0}. |
| ValidationError | Недопустимый граф пакета службы web Hello. Дополнительные сведения: {0}. |
 
## <a name="unauthorized-http-status-code-401"></a>Unauthorized (код состояния HTTP: 401).
 
Запрос является несанкционированного tooaccess ресурсов.
 
| Код ошибки | Сообщение для пользователя |
| ---------- |--------------|
| AdminRequestUnauthorized | Не авторизовано |
| ManagementRequestUnauthorized | Не авторизовано |
| ScoreRequestUnauthorized | Указаны недопустимые учетные данные. |
 
## <a name="notfound-http-status-code-404"></a>NotFound (код состояния HTTP: 404)
 
Ресурс не найден.
 
| Код ошибки | Сообщение для пользователя |
| ---------- |--------------|
| ModelPackageNotFound | Пакет модели не найден. Проверьте пакет модели hello идентификатор указано правильно и повторите попытку. |
| WebServiceIdNotFoundInWorkspace | Веб-служба в этой рабочей области не найдена. Существует несоответствие между hello webServiceId и hello ИД рабочей области. Проверьте веб-службу hello предоставленный является частью рабочей области hello и повторите попытку. |
| WebServiceNotFound | Веб-служба не найдена. Проверьте веб-службу hello идентификатор указано правильно и повторите попытку. |
| WorkspaceNotFound | Рабочая область не найдена. Проверьте рабочую область hello идентификатор указано правильно и повторите попытку. |
 
## <a name="requesttimeout-http-status-code-408"></a>RequestTimeout (код состояния HTTP: 408)
 
не удается завершить операцию Hello за hello допускается времени.
 
| Код ошибки | Сообщение для пользователя |
| ---------- |--------------|
| RequestCanceled | Запрос был отменен клиентом hello. |
| ScoreRequestTimeout | Истекло время ожидания выполнения запроса. |
 
## <a name="conflict-http-status-code-409"></a>Conflict (код состояния HTTP: 409)
 
Ресурс уже существует.
 
| Код ошибки | Сообщение для пользователя |
| ---------- |--------------|
| ModelOutputMetadataMismatch | Недопустимое имя параметра вывода. С помощью столбцов toorename модуля редактора метаданных hello и повторите попытку. |
 
## <a name="memoryquotaviolation-http-status-code-413"></a>MemoryQuotaViolation (код состояния HTTP: 413)
 
модель Hello превышения квоты памяти hello, назначенный tooit.
 
| Код ошибки | Сообщение для пользователя |
| ---------- |--------------|
| OutOfMemoryLimit | модель Hello потребляет больше памяти, чем было appropriated для него. Максимальный допустимый объем памяти для модели hello составляет {0} МБ. Проверьте модель на наличие проблем. |
 
## <a name="internalerror-http-status-code-500"></a>InternalError (код состояния HTTP: 500)
 
При выполнении обнаружена внутренняя ошибка.
 
| Код ошибки | Сообщение для пользователя |
| ---------- |--------------|
| AdminAuthenticationFailed |  |
| BackendArgumentError |  |
| BackendBadRequest |  |
| ClusterConfigBlobMisconfigured |  |
| ContainerProcessTerminatedWithSystemError | Произошел сбой с ошибкой системы процесса контейнера Hello |
| ContainerProcessTerminatedWithUnknownError | Произошел сбой вследствие неизвестной ошибки процесса контейнера Hello |
| ContainerValidationFailed | Проверка контейнера BLOB-объектов завершилась следующей ошибкой: {0}. |
| DeleteWebServiceResourceFailed |  |
| ExceptionDeserializationError |  |
| FailedGettingApiDocument |  |
| FailedStoringWebService |  |
| InvalidMemoryConfiguration | InvalidMemoryConfiguration, ConfigValue: {0} |
| InvalidResourceCacheConfiguration |  |
| InvalidResourceDownloadConfiguration |  |
| InvalidWebServiceResources |  |
| MissingTaskInstance | Не указаны аргументы. Убедитесь, что допустимые аргументы передаются, и повторите попытку. |
| ModelPackageInvalid |  |
| ModuleExecutionFailed |  |
| ModuleLoadFailed |  |
| ModuleObjectCloneFailed |  |
| OutputConversionFailed |  |
| PortDataTypeNotSupported | Неподдерживаемый тип данных для ИД порта {0}: {1}. |
| ResourceDownload |  |
| ResourceLoadFailed |  |
| ServiceUrisNotFound |  |
| SwaggerGeneration | Сбой при создании Swagger, сведения об ошибке: {0}. |
| UnexpectedScoreStatus |  |
| UnknownBackendErrorResponse |  |
| UnknownError |  |
| UnknownJobStatusCode | Неизвестный код состояния задания: {0}. |
| UnknownModuleError |  |
| UpdateWebServiceResourceFailed |  |
| WebServiceGroupNotFound |  |
| WebServicePackageInvalid | InvalidWebServicePackage, сведения: {0}. |
| WorkerAuthorizationFailed |  |
| WorkerUnreachable |  |
 
## <a name="internalerrorsystemlowonmemory-http-status-code-500"></a>InternalErrorSystemLowOnMemory (код состояния HTTP: 500)
 
При выполнении обнаружена внутренняя ошибка. В системе нехватка памяти. Повторите попытку позже.
 
 
## <a name="modelpackageformaterror-http-status-code-500"></a>ModelPackageFormatError (код состояния HTTP: 500)
 
Недопустимый пакет модели. Предоставленный пакет модели hello правильность и повторите попытку.
 
 
## <a name="webservicepackageinternalerror-http-status-code-500"></a>WebServicePackageInternalError (код состояния HTTP: 500)
 
Указан недопустимый пакет веб-службы. Проверьте веб-пакета hello указано правильно и повторите попытку.
 
| Код ошибки | Сообщение для пользователя |
| ---------- |--------------|
| ModuleError | Недопустимый граф пакета службы web Hello. Дополнительные сведения: {0}. |
 
## <a name="initializingcontainers-http-status-code-503"></a>InitializingContainers (код состояния HTTP: 503)
 
Hello запрос невозможно выполнить в качестве контейнеров инициализируются hello.
 
 
## <a name="serviceunavailable-http-status-code-503"></a>ServiceUnavailable (код состояния HTTP: 503)
 
Служба временно недоступна.
 
| Код ошибки | Сообщение для пользователя |
| ---------- |--------------|
| NoMoreResources | Нет ресурсов для запроса. |
| RequestThrottled | Запрос к конечной точке {0} был отрегулирован. Максимальная степень параллелизма для конечной точки hello Hello — {1}. |
| TooManyConcurrentRequests | Отправлено слишком много одновременных запросов. |
| TooManyHostsBeingInitialized | Слишком много узлов, инициализируемый в hello же время. Рассмотрите возможность регулирования или повторения попытки. |
| TooManyHostsBeingInitializedPerModel | Слишком много узлов, инициализируемый в hello же время. Рассмотрите возможность регулирования или повторения попытки. |
 
## <a name="gatewaytimeout-http-status-code-504"></a>GatewayTimeout (код состояния HTTP: 504)
 
не удается завершить операцию Hello за hello допускается времени.
 
| Код ошибки | Сообщение для пользователя |
| ---------- |--------------|
| BackendInitializationTimeout | не удалось выполнить инициализации службы web Hello в hello допускается времени. |
| BackendScoreTimeout | не удалось выполнить выполнения запроса службы web Hello в hello допускается времени. |
 
