---
title: "Элемент пользовательского интерфейса FileUpload управляемого приложения Azure | Документация Майкрософт"
description: "Сведения об элементе пользовательского интерфейса Microsoft.Common.FileUpload управляемых приложений Azure"
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
ms.openlocfilehash: 217e9e63eb7cd198f70cee42b418867df9f1f993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="ff9cf-103">Элемент пользовательского интерфейса Microsoft.Common.FileUpload</span><span class="sxs-lookup"><span data-stu-id="ff9cf-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="ff9cf-104">Элемент управления, который позволяет пользователю указать один или несколько файлов для отправки.</span><span class="sxs-lookup"><span data-stu-id="ff9cf-104">A control that allows a user to specify one or more files to upload.</span></span> <span data-ttu-id="ff9cf-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="ff9cf-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="ff9cf-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="ff9cf-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="ff9cf-108">Схема</span><span class="sxs-lookup"><span data-stu-id="ff9cf-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="ff9cf-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="ff9cf-109">Remarks</span></span>
- <span data-ttu-id="ff9cf-110">`constraints.accept` — указывает типы файлов, которые отображаются в файловом диалоговом окне браузера.</span><span class="sxs-lookup"><span data-stu-id="ff9cf-110">`constraints.accept` specifies the types of files that are shown in the browser's file dialog.</span></span> <span data-ttu-id="ff9cf-111">Сведения о допустимых значениях см. в [спецификации HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept).</span><span class="sxs-lookup"><span data-stu-id="ff9cf-111">See the [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="ff9cf-112">Значение по умолчанию — **null**.</span><span class="sxs-lookup"><span data-stu-id="ff9cf-112">The default value is **null**.</span></span>
- <span data-ttu-id="ff9cf-113">Если `options.multiple` имеет значение **true**, пользователь может выбрать несколько файлов в файловом диалоговом окне браузера.</span><span class="sxs-lookup"><span data-stu-id="ff9cf-113">If `options.multiple` is set to **true**, the user is allowed to select more than one file in the browser's file dialog.</span></span> <span data-ttu-id="ff9cf-114">Значение по умолчанию — **false**.</span><span class="sxs-lookup"><span data-stu-id="ff9cf-114">The default value is **false**.</span></span>
- <span data-ttu-id="ff9cf-115">Этот элемент поддерживает отправку файлов в двух режимах, которые задаются в параметре `options.uploadMode`.</span><span class="sxs-lookup"><span data-stu-id="ff9cf-115">This element supports uploading files in two modes based on the value of `options.uploadMode`.</span></span> <span data-ttu-id="ff9cf-116">Если указан **file**, тогда выходные данные предоставляют содержимое файла в виде большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="ff9cf-116">If **file** is specified, the output contains the contents of the file as a blob.</span></span> <span data-ttu-id="ff9cf-117">Если указан **url**, тогда файл отравляется во временное расположение и выходные данные содержат URL-адрес большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="ff9cf-117">If **url** is specified, then the file is uploaded to a temporary location, and the output contains the URL of the blob.</span></span> <span data-ttu-id="ff9cf-118">Временные большие двоичные объекты очищаются через 24 часа.</span><span class="sxs-lookup"><span data-stu-id="ff9cf-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="ff9cf-119">Значение по умолчанию — **file**.</span><span class="sxs-lookup"><span data-stu-id="ff9cf-119">The default value is **file**.</span></span>
- <span data-ttu-id="ff9cf-120">Значение `options.openMode` определяет режим, в котором открывается файл.</span><span class="sxs-lookup"><span data-stu-id="ff9cf-120">The value of `options.openMode` determines how the file is read.</span></span> <span data-ttu-id="ff9cf-121">Если предполагается, что файл содержит обычный текст, укажите **text**. В противном случае укажите **binary**.</span><span class="sxs-lookup"><span data-stu-id="ff9cf-121">If the file is expected to be plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="ff9cf-122">Значение по умолчанию — **text**.</span><span class="sxs-lookup"><span data-stu-id="ff9cf-122">The default value is **text**.</span></span>
- <span data-ttu-id="ff9cf-123">Если `options.uploadMode` имеет значение **file**, а `options.openMode` имеет значение **binary**, то выходные данные закодированы в формате Base64.</span><span class="sxs-lookup"><span data-stu-id="ff9cf-123">If `options.uploadMode` is set to **file** and `options.openMode` is set to **binary**, the output is base64-encoded.</span></span>
- <span data-ttu-id="ff9cf-124">`options.encoding` — указывает кодирование, которое используется при чтении файла.</span><span class="sxs-lookup"><span data-stu-id="ff9cf-124">`options.encoding` specifies the encoding to use when reading the file.</span></span> <span data-ttu-id="ff9cf-125">Значение по умолчанию — **UTF-8**, которое используется только если для параметра `options.openMode` задано значение **text**.</span><span class="sxs-lookup"><span data-stu-id="ff9cf-125">The default value is **UTF-8**, and is used only when `options.openMode` is set to **text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="ff9cf-126">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="ff9cf-126">Sample output</span></span>
<span data-ttu-id="ff9cf-127">Если options.multiple имеет значение false и options.uploadMode — file, тогда выходные данные предоставляют содержимое файла в виде строки JSON:</span><span class="sxs-lookup"><span data-stu-id="ff9cf-127">If options.multiple is false and options.uploadMode is file, then the output contains the contents of the file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="ff9cf-128">Если options.multiple имеет значение true и options.uploadMode — file, тогда выходные данные предоставляют содержимое файла в виде массива JSON:</span><span class="sxs-lookup"><span data-stu-id="ff9cf-128">If options.multiple is true and\`options.uploadMode is file, then the output contains the contents of the files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="ff9cf-129">Если options.multiple имеет значение false и uploadMode — url, тогда выходные данные содержат ULR-адрес в виде строки JSON:</span><span class="sxs-lookup"><span data-stu-id="ff9cf-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="ff9cf-130">Если options.multiple имеет значение true и uploadMode — url, тогда выходные данные содержат список ULR-адресов в виде массива JSON:</span><span class="sxs-lookup"><span data-stu-id="ff9cf-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="ff9cf-131">При тестировании определения CreateUiDefinition некоторые браузеры (например, Google Chrome) обрезают ULR-адреса, созданные элементом Microsoft.Common.FileUpload, в консоли браузера.</span><span class="sxs-lookup"><span data-stu-id="ff9cf-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by the Microsoft.Common.FileUpload element in the browser console.</span></span> <span data-ttu-id="ff9cf-132">Чтобы скопировать полные URL-адреса, вам может потребоваться щелкнуть правой кнопкой мыши отдельные ссылки.</span><span class="sxs-lookup"><span data-stu-id="ff9cf-132">You may need to right-click individual links to copy the full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ff9cf-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ff9cf-133">Next steps</span></span>
* <span data-ttu-id="ff9cf-134">Общие сведения об управляемых приложениях Azure см. в [этой статье](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ff9cf-134">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="ff9cf-135">Общие сведения о создании определений пользовательского интерфейса см. в статье [Начало работы с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ff9cf-135">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="ff9cf-136">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="ff9cf-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
