---
title: "элемент пользовательского интерфейса FileUpload управляемого приложения aaaAzure | Документы Microsoft"
description: "Описывает hello элемент пользовательского интерфейса Microsoft.Common.FileUpload для управляемых приложений Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 7af5bec992e3f120afb1bdf56d8b4c19a8e5e834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="2ba8c-103">Элемент пользовательского интерфейса Microsoft.Common.FileUpload</span><span class="sxs-lookup"><span data-stu-id="2ba8c-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="2ba8c-104">Элемент управления, позволяющий toospecify пользователя один или несколько файлов tooupload.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-104">A control that allows a user toospecify one or more files tooupload.</span></span> <span data-ttu-id="2ba8c-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="2ba8c-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="2ba8c-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="2ba8c-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="2ba8c-108">Схема</span><span class="sxs-lookup"><span data-stu-id="2ba8c-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.FileUpload",
  "label": "Some file upload",
  "toolTip": "",
  "constraints": {
    "required": true,
    "accept": ".doc,.docx,.xml,application/msword"
  },
  "options": {
    "multiple": false,
    "uploadMode": "file",
    "openMode": "text",
    "encoding": "UTF-8"
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="2ba8c-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="2ba8c-109">Remarks</span></span>
- <span data-ttu-id="2ba8c-110">`constraints.accept`Указывает типы файлов, отображаемых в диалоговом окне браузера hello файл hello.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-110">`constraints.accept` specifies hello types of files that are shown in hello browser's file dialog.</span></span> <span data-ttu-id="2ba8c-111">В разделе hello [спецификации HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) для допустимых значений.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-111">See hello [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="2ba8c-112">значение по умолчанию Hello — **null**.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-112">hello default value is **null**.</span></span>
- <span data-ttu-id="2ba8c-113">Если `options.multiple` задано слишком**true**, tooselect более одного файла в диалоговом окне браузера hello файла разрешено пользователю hello.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-113">If `options.multiple` is set too**true**, hello user is allowed tooselect more than one file in hello browser's file dialog.</span></span> <span data-ttu-id="2ba8c-114">значение по умолчанию Hello — **false**.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-114">hello default value is **false**.</span></span>
- <span data-ttu-id="2ba8c-115">Этот элемент поддерживает отправку файлов в двух режимах на основе значения hello `options.uploadMode`.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-115">This element supports uploading files in two modes based on hello value of `options.uploadMode`.</span></span> <span data-ttu-id="2ba8c-116">Если **файл** указан, выходной hello содержит hello содержимое файла hello как большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-116">If **file** is specified, hello output contains hello contents of hello file as a blob.</span></span> <span data-ttu-id="2ba8c-117">Если **URL-адрес** указан, то файл hello отправленного tooa временное расположение, и результат hello содержит URL-адрес hello hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-117">If **url** is specified, then hello file is uploaded tooa temporary location, and hello output contains hello URL of hello blob.</span></span> <span data-ttu-id="2ba8c-118">Временные большие двоичные объекты очищаются через 24 часа.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="2ba8c-119">значение по умолчанию Hello — **файл**.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-119">hello default value is **file**.</span></span>
- <span data-ttu-id="2ba8c-120">Здравствуйте, значение `options.openMode` определяет, как прочитать файл hello.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-120">hello value of `options.openMode` determines how hello file is read.</span></span> <span data-ttu-id="2ba8c-121">Если файл hello ожидаемый toobe обычного текста, укажите **текст**; в противном случае, укажите **двоичных**.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-121">If hello file is expected toobe plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="2ba8c-122">значение по умолчанию Hello — **текст**.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-122">hello default value is **text**.</span></span>
- <span data-ttu-id="2ba8c-123">Если `options.uploadMode` задано слишком**файл** и `options.openMode` задано слишком**двоичных**, hello выходные данные в кодировке base64.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-123">If `options.uploadMode` is set too**file** and `options.openMode` is set too**binary**, hello output is base64-encoded.</span></span>
- <span data-ttu-id="2ba8c-124">`options.encoding`Указывает кодировки toouse hello при чтении файла hello.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-124">`options.encoding` specifies hello encoding toouse when reading hello file.</span></span> <span data-ttu-id="2ba8c-125">значение по умолчанию Hello — **UTF-8**и используется только если `options.openMode` задано слишком**текст**.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-125">hello default value is **UTF-8**, and is used only when `options.openMode` is set too**text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="2ba8c-126">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="2ba8c-126">Sample output</span></span>
<span data-ttu-id="2ba8c-127">Если options.multiple имеет значение false и options.uploadMode — файл, выходные данные содержат hello содержимое файла hello как строка JSON:</span><span class="sxs-lookup"><span data-stu-id="2ba8c-127">If options.multiple is false and options.uploadMode is file, then the output contains hello contents of hello file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="2ba8c-128">Если истинно options.multiple and'options.uploadMode файлом, то выходные данные содержат hello содержимое файлов hello как массив JSON:</span><span class="sxs-lookup"><span data-stu-id="2ba8c-128">If options.multiple is true and\`options.uploadMode is file, then the output contains hello contents of hello files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="2ba8c-129">Если options.multiple имеет значение false и uploadMode — url, тогда выходные данные содержат ULR-адрес в виде строки JSON:</span><span class="sxs-lookup"><span data-stu-id="2ba8c-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="2ba8c-130">Если options.multiple имеет значение true и uploadMode — url, тогда выходные данные содержат список ULR-адресов в виде массива JSON:</span><span class="sxs-lookup"><span data-stu-id="2ba8c-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="2ba8c-131">При тестировании CreateUiDefinition, некоторые браузеры (например, Google Chrome) приводит к усечению URL-адреса, созданные элементом Microsoft.Common.FileUpload hello в консоли браузера hello.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by hello Microsoft.Common.FileUpload element in hello browser console.</span></span> <span data-ttu-id="2ba8c-132">Может потребоваться tooright щелкните отдельные связи toocopy hello полные URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="2ba8c-132">You may need tooright-click individual links toocopy hello full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2ba8c-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2ba8c-133">Next steps</span></span>
* <span data-ttu-id="2ba8c-134">Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ba8c-134">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="2ba8c-135">Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ba8c-135">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="2ba8c-136">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="2ba8c-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
