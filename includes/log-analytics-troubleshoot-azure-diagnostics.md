### <a name="troubleshoot-azure-diagnostics"></a><span data-ttu-id="e46af-101">Устранение неполадок системы диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="e46af-101">Troubleshoot Azure Diagnostics</span></span>

<span data-ttu-id="e46af-102">Если появляется сообщение об ошибке после hello поставщика ресурсов помощью Microsoft.insights hello не зарегистрирована:</span><span class="sxs-lookup"><span data-stu-id="e46af-102">If you receive hello following error message, hello Microsoft.insights resource provider is not registered:</span></span>

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

<span data-ttu-id="e46af-103">поставщик ресурсов hello tooregister выполнения шагов в hello портал Azure hello:</span><span class="sxs-lookup"><span data-stu-id="e46af-103">tooregister hello resource provider, perform hello following steps in hello Azure portal:</span></span>

1.  <span data-ttu-id="e46af-104">Hello hello левой панели навигации щелкните *подписки*</span><span class="sxs-lookup"><span data-stu-id="e46af-104">In hello navigation pane on hello left, click *Subscriptions*</span></span>
2.  <span data-ttu-id="e46af-105">Выберите подписку hello, указанной в сообщении об ошибке hello</span><span class="sxs-lookup"><span data-stu-id="e46af-105">Select hello subscription identified in hello error message</span></span>
3.  <span data-ttu-id="e46af-106">Щелкните *Поставщики ресурсов*.</span><span class="sxs-lookup"><span data-stu-id="e46af-106">Click *Resource Providers*</span></span>
4.  <span data-ttu-id="e46af-107">Найти hello *помощью Microsoft.insights* поставщика</span><span class="sxs-lookup"><span data-stu-id="e46af-107">Find hello *Microsoft.insights* provider</span></span>
5.  <span data-ttu-id="e46af-108">Нажмите кнопку hello *зарегистрировать* ссылку</span><span class="sxs-lookup"><span data-stu-id="e46af-108">Click hello *Register* link</span></span>

![Регистрация поставщика ресурсов microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

<span data-ttu-id="e46af-110">Здравствуйте, один раз *помощью Microsoft.insights* зарегистрирован поставщик ресурсов, повторите настройку диагностики.</span><span class="sxs-lookup"><span data-stu-id="e46af-110">Once hello *Microsoft.insights* resource provider is registered, retry configuring diagnostics.</span></span>


<span data-ttu-id="e46af-111">В PowerShell при получении hello следующие сообщение об ошибке, вы должны tooupdate ваша версия PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e46af-111">In PowerShell, if you receive hello following error message, you need tooupdate your version of PowerShell:</span></span>

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

<span data-ttu-id="e46af-112">Обновление версии PowerShell toohello ноября 2016 г. (v2.3.0) или более поздней версии, выпуска с помощью инструкций hello в hello [приступить к работе с помощью командлетов Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) статьи.</span><span class="sxs-lookup"><span data-stu-id="e46af-112">Update your version of PowerShell toohello November 2016 (v2.3.0), or later, release using hello instructions in hello [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) article.</span></span>
