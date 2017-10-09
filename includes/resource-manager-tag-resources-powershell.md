Версии 3.0 модуль AzureRm.Resources hello включены существенные изменения в том, как работать с тегами. Прежде чем продолжить, проверьте версию:

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

Если результаты показывают версии 3.0 или более поздней версии, hello примеры в этом разделе работать с вашей средой. Если у вас более старая версия, [обновите ее](/powershell/azureps-cmdlets-docs/), используя коллекцию PowerShell или установщик веб-платформы, прежде чем продолжать работу с этой статьей.

```powershell
Version
-------
3.5.0
```

существующие теги для hello toosee *группы ресурсов*, используйте:

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

Этот скрипт возвращает hello следующий формат:

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

существующие теги для hello toosee *ресурс, который имеет идентификатор указанного ресурса*, использовать:

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

Или toosee hello существующие теги для *ресурс с указанным имени и группе ресурсов*, используйте:

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

tooget *групп ресурсов, которые имеют определенный тег*, используйте:

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

tooget *ресурсы, имеющие определенный тег*, используйте:

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

Каждый раз при применении теги tooa ресурс или группу ресурсов, вы перезаписать существующие теги hello на этот ресурс или группа ресурсов. Таким образом необходимо использовать другой подход, в зависимости от того, имеет ли hello ресурс или группа ресурсов существующие теги. 

tooadd теги tooa *группы ресурсов без существующие теги*, используйте:

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

tooadd теги tooa *группу ресурсов с существующие теги*, получить существующие теги hello, добавьте новый тег hello и заново hello теги:

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

tooadd теги tooa *ресурс без существующие теги*, используйте:

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooadd теги tooa *ресурс с существующие теги*, используйте:

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooapply все теги из ресурсов tooits группы ресурсов, и *не сохранять существующие теги ресурсов hello*, используйте следующий сценарий hello:

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

tooapply все теги из ресурсов tooits группы ресурсов, и *сохранить существующие теги на ресурсы, которые не являются дубликатами*, используйте следующий сценарий hello:

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

tooremove всех тегов, передайте пустые хэш-таблицы:

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



