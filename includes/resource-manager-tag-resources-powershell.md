<span data-ttu-id="7d53e-101">Версии 3.0 модуль AzureRm.Resources hello включены существенные изменения в том, как работать с тегами.</span><span class="sxs-lookup"><span data-stu-id="7d53e-101">Version 3.0 of hello AzureRm.Resources module included significant changes in how you work with tags.</span></span> <span data-ttu-id="7d53e-102">Прежде чем продолжить, проверьте версию:</span><span class="sxs-lookup"><span data-stu-id="7d53e-102">Before you proceed, check your version:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="7d53e-103">Если результаты показывают версии 3.0 или более поздней версии, hello примеры в этом разделе работать с вашей средой.</span><span class="sxs-lookup"><span data-stu-id="7d53e-103">If your results show version 3.0 or later, hello examples in this topic work with your environment.</span></span> <span data-ttu-id="7d53e-104">Если у вас более старая версия, [обновите ее](/powershell/azureps-cmdlets-docs/), используя коллекцию PowerShell или установщик веб-платформы, прежде чем продолжать работу с этой статьей.</span><span class="sxs-lookup"><span data-stu-id="7d53e-104">If you do not have version 3.0 or later, [update your version](/powershell/azureps-cmdlets-docs/) by using PowerShell Gallery or Web Platform Installer before you proceed with this topic.</span></span>

```powershell
Version
-------
3.5.0
```

<span data-ttu-id="7d53e-105">существующие теги для hello toosee *группы ресурсов*, используйте:</span><span class="sxs-lookup"><span data-stu-id="7d53e-105">toosee hello existing tags for a *resource group*, use:</span></span>

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

<span data-ttu-id="7d53e-106">Этот скрипт возвращает hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="7d53e-106">That script returns hello following format:</span></span>

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

<span data-ttu-id="7d53e-107">существующие теги для hello toosee *ресурс, который имеет идентификатор указанного ресурса*, использовать:</span><span class="sxs-lookup"><span data-stu-id="7d53e-107">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

<span data-ttu-id="7d53e-108">Или toosee hello существующие теги для *ресурс с указанным имени и группе ресурсов*, используйте:</span><span class="sxs-lookup"><span data-stu-id="7d53e-108">Or, toosee hello existing tags for a *resource that has a specified name and resource group*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

<span data-ttu-id="7d53e-109">tooget *групп ресурсов, которые имеют определенный тег*, используйте:</span><span class="sxs-lookup"><span data-stu-id="7d53e-109">tooget *resource groups that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

<span data-ttu-id="7d53e-110">tooget *ресурсы, имеющие определенный тег*, используйте:</span><span class="sxs-lookup"><span data-stu-id="7d53e-110">tooget *resources that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

<span data-ttu-id="7d53e-111">Каждый раз при применении теги tooa ресурс или группу ресурсов, вы перезаписать существующие теги hello на этот ресурс или группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7d53e-111">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="7d53e-112">Таким образом необходимо использовать другой подход, в зависимости от того, имеет ли hello ресурс или группа ресурсов существующие теги.</span><span class="sxs-lookup"><span data-stu-id="7d53e-112">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="7d53e-113">tooadd теги tooa *группы ресурсов без существующие теги*, используйте:</span><span class="sxs-lookup"><span data-stu-id="7d53e-113">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

<span data-ttu-id="7d53e-114">tooadd теги tooa *группу ресурсов с существующие теги*, получить существующие теги hello, добавьте новый тег hello и заново hello теги:</span><span class="sxs-lookup"><span data-stu-id="7d53e-114">tooadd tags tooa *resource group that has existing tags*, retrieve hello existing tags, add hello new tag, and reapply hello tags:</span></span>

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

<span data-ttu-id="7d53e-115">tooadd теги tooa *ресурс без существующие теги*, используйте:</span><span class="sxs-lookup"><span data-stu-id="7d53e-115">tooadd tags tooa *resource without existing tags*, use:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="7d53e-116">tooadd теги tooa *ресурс с существующие теги*, используйте:</span><span class="sxs-lookup"><span data-stu-id="7d53e-116">tooadd tags tooa *resource that has existing tags*, use:</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="7d53e-117">tooapply все теги из ресурсов tooits группы ресурсов, и *не сохранять существующие теги ресурсов hello*, используйте следующий сценарий hello:</span><span class="sxs-lookup"><span data-stu-id="7d53e-117">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

<span data-ttu-id="7d53e-118">tooapply все теги из ресурсов tooits группы ресурсов, и *сохранить существующие теги на ресурсы, которые не являются дубликатами*, используйте следующий сценарий hello:</span><span class="sxs-lookup"><span data-stu-id="7d53e-118">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources that are not duplicates*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    if ($g.Tags -ne $null) {
        $resources = Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName 
        foreach ($r in $resources)
        {
            $resourcetags = (Get-AzureRmResource -ResourceId $r.ResourceId).Tags
            foreach ($key in $g.Tags.Keys)
            {
                if ($resourcetags.ContainsKey($key)) { $resourcetags.Remove($key) }
            }
            $resourcetags += $g.Tags
            Set-AzureRmResource -Tag $resourcetags -ResourceId $r.ResourceId -Force
        }
    }
}
```

<span data-ttu-id="7d53e-119">tooremove всех тегов, передайте пустые хэш-таблицы:</span><span class="sxs-lookup"><span data-stu-id="7d53e-119">tooremove all tags, pass an empty hash table:</span></span>

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



