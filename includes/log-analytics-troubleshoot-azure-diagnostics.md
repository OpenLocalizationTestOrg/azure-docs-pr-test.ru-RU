### <a name="troubleshoot-azure-diagnostics"></a>Устранение неполадок системы диагностики Azure

Если появляется сообщение об ошибке после hello поставщика ресурсов помощью Microsoft.insights hello не зарегистрирована:

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

поставщик ресурсов hello tooregister выполнения шагов в hello портал Azure hello:

1.  Hello hello левой панели навигации щелкните *подписки*
2.  Выберите подписку hello, указанной в сообщении об ошибке hello
3.  Щелкните *Поставщики ресурсов*.
4.  Найти hello *помощью Microsoft.insights* поставщика
5.  Нажмите кнопку hello *зарегистрировать* ссылку

![Регистрация поставщика ресурсов microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

Здравствуйте, один раз *помощью Microsoft.insights* зарегистрирован поставщик ресурсов, повторите настройку диагностики.


В PowerShell при получении hello следующие сообщение об ошибке, вы должны tooupdate ваша версия PowerShell.

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

Обновление версии PowerShell toohello ноября 2016 г. (v2.3.0) или более поздней версии, выпуска с помощью инструкций hello в hello [приступить к работе с помощью командлетов Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) статьи.
