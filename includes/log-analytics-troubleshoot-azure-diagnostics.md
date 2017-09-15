### <a name="troubleshoot-azure-diagnostics"></a><span data-ttu-id="82098-101">Устранение неполадок системы диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="82098-101">Troubleshoot Azure Diagnostics</span></span>

<span data-ttu-id="82098-102">Если появляется следующее сообщение об ошибке, это значит, что поставщик ресурсов Microsoft.insights не зарегистрирован:</span><span class="sxs-lookup"><span data-stu-id="82098-102">If you receive the following error message, the Microsoft.insights resource provider is not registered:</span></span>

`Failed to update diagnostics for 'resource'. {"code":"Forbidden","message":"Please register the subscription 'subscription id' with Microsoft.Insights."}`

<span data-ttu-id="82098-103">Чтобы зарегистрировать поставщик ресурсов, сделайте следующее на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="82098-103">To register the resource provider, perform the following steps in the Azure portal:</span></span>

1.  <span data-ttu-id="82098-104">Слева в области навигации щелкните *Подписки*.</span><span class="sxs-lookup"><span data-stu-id="82098-104">In the navigation pane on the left, click *Subscriptions*</span></span>
2.  <span data-ttu-id="82098-105">Выберите подписку, указанную в сообщении об ошибке.</span><span class="sxs-lookup"><span data-stu-id="82098-105">Select the subscription identified in the error message</span></span>
3.  <span data-ttu-id="82098-106">Щелкните *Поставщики ресурсов*.</span><span class="sxs-lookup"><span data-stu-id="82098-106">Click *Resource Providers*</span></span>
4.  <span data-ttu-id="82098-107">Найдите поставщика *Microsoft.insights*.</span><span class="sxs-lookup"><span data-stu-id="82098-107">Find the *Microsoft.insights* provider</span></span>
5.  <span data-ttu-id="82098-108">Щелкните ссылку *Зарегистрировать*.</span><span class="sxs-lookup"><span data-stu-id="82098-108">Click the *Register* link</span></span>

![Регистрация поставщика ресурсов microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

<span data-ttu-id="82098-110">Зарегистрировав поставщик ресурсов *Microsoft.insights*, повторите настройку диагностики.</span><span class="sxs-lookup"><span data-stu-id="82098-110">Once the *Microsoft.insights* resource provider is registered, retry configuring diagnostics.</span></span>


<span data-ttu-id="82098-111">Если появляется следующее сообщение об ошибке, необходимо обновить версию PowerShell:</span><span class="sxs-lookup"><span data-stu-id="82098-111">In PowerShell, if you receive the following error message, you need to update your version of PowerShell:</span></span>

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

<span data-ttu-id="82098-112">Обновите PowerShell до версии за ноябрь 2016 г. (версия 2.3.0) и выше с помощью инструкций из статьи [Приступая к работе с командлетами Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="82098-112">Update your version of PowerShell to the November 2016 (v2.3.0), or later, release using the instructions in the [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) article.</span></span>
