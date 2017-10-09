## <a name="next-steps"></a>Дальнейшие действия

После включения интеграции хранилища ключей Azure вы сможете включить шифрование SQL Server на своей виртуальной машине с SQL. Во-первых необходимо будет toocreate асимметричного ключа в хранилище ключей и симметричного ключа в SQL Server на виртуальной Машине. Затем можно шифрования tooenable инструкции T-SQL может tooexecute для баз данных и резервных копий.

Существует несколько способов шифрования, преимуществами которых вы можете воспользоваться.

* [Прозрачное шифрование данных (TDE)](https://msdn.microsoft.com/library/bb934049.aspx)
* [Зашифрованные резервные копии](https://msdn.microsoft.com/library/dn449489.aspx)
* [Шифрование на уровне столбцов (CLE)](https://msdn.microsoft.com/library/ms173744.aspx)

Hello следующие сценарии Transact-SQL содержатся примеры для каждого из этих областей.

### <a name="prerequisites-for-examples"></a>Предварительные требования для примеров

Каждый пример основан на предварительные условия двух hello: вызывается асимметричного ключа из хранилища ключей **CONTOSO_KEY** и учетные данные, созданные hello хранилищем ключей AZURE Integration называемую **Azure_EKM_TDE_cred**. Hello следующие команды Transact-SQL эти необходимые компоненты установки для запуска примеров hello.

``` sql
USE master;
GO

sp_configure [show advanced options], 1;
GO
RECONFIGURE;
GO

-- Enable EKM provider
sp_configure [EKM provider enabled], 1;
GO
RECONFIGURE;

--create provider
CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov
FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';
GO

--create credential
CREATE CREDENTIAL sysadmin_ekm_cred
    WITH IDENTITY = 'keytestvault', --keyvault
    SECRET = '<<SECRET>>'
FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;


--must have sysadmin
ALTER LOGIN [TDE_Login]
ADD CREDENTIAL sysadmin_ekm_cred;


CREATE ASYMMETRIC KEY CONTOSO_KEY
FROM PROVIDER [AzureKeyVault_EKM_Prov]
WITH PROVIDER_KEY_NAME = 'keytestvault',  --key name
CREATION_DISPOSITION = OPEN_EXISTING;
```

### <a name="transparent-data-encryption-tde"></a>Прозрачное шифрование данных (TDE)

1. Создать toobe входа SQL Server, используемые hello компонента Database Engine для прозрачного шифрования данных, а затем добавить tooit hello учетных данных.

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it loads a database
   -- encrypted by TDE.
   CREATE LOGIN TDE_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello TDE Login tooadd hello credential for use by the
   -- Database Engine tooaccess hello key vault
   ALTER LOGIN TDE_Login
   ADD CREDENTIAL Azure_EKM_TDE_cred;
   GO
   ```

1. Создайте ключ шифрования базы данных hello, который будет использоваться для прозрачного шифрования данных.

   ``` sql
   USE ContosoDatabase;
   GO

   CREATE DATABASE ENCRYPTION KEY 
   WITH ALGORITHM = AES_128 
   ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello database tooenable transparent data encryption.
   ALTER DATABASE ContosoDatabase
   SET ENCRYPTION ON;
   GO
   ```

### <a name="encrypted-backups"></a>Зашифрованные резервные копии

1. Создайте toobe входа SQL Server, используемые hello СУБД для шифрования резервных копий и добавьте tooit hello учетных данных.

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it is encrypting hello backup.
   CREATE LOGIN Backup_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello Encrypted Backup Login tooadd hello credential for use by
   -- hello Database Engine tooaccess hello key vault
   ALTER LOGIN Backup_Login
   ADD CREDENTIAL Azure_EKM_Backup_cred ;
   GO
   ```

1. Hello резервного копирования базы данных, указав шифрование с асимметричным ключом hello хранятся в хранилище ключей hello.

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a>Шифрование на уровне столбцов (CLE)

Этот скрипт создает симметричный ключ, защищенный асимметричным ключом hello в хранилище ключей hello, а затем использует данные hello tooencrypt симметричного ключа в базе данных hello.

``` sql
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
WITH ALGORITHM=AES_256
ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open hello symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data tooencrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close hello symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="additional-resources"></a>Дополнительные ресурсы

Дополнительные сведения о toouse этих функций шифрования в статье [с помощью расширенного управления Ключами с функциями шифрования SQL Server](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).

Обратите внимание, что hello в этой статье предполагается, что уже есть SQL Server на виртуальной машине Azure. Если нет, см. статью [Подготовка виртуальной машины с SQL Server в Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md). Другие темы, связанные с запуском SQL Server на виртуальных машинах Azure, см. в статье [Общие сведения об SQL Server на виртуальных машинах Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).
