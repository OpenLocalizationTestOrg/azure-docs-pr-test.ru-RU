## <a name="next-steps"></a><span data-ttu-id="53caa-101">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="53caa-101">Next steps</span></span>

<span data-ttu-id="53caa-102">После включения интеграции хранилища ключей Azure вы сможете включить шифрование SQL Server на своей виртуальной машине с SQL.</span><span class="sxs-lookup"><span data-stu-id="53caa-102">After enabling Azure Key Vault Integration, you can enable SQL Server encryption on your SQL VM.</span></span> <span data-ttu-id="53caa-103">Во-первых необходимо будет toocreate асимметричного ключа в хранилище ключей и симметричного ключа в SQL Server на виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="53caa-103">First, you will need toocreate an asymmetric key inside your key vault and a symmetric key within SQL Server on your VM.</span></span> <span data-ttu-id="53caa-104">Затем можно шифрования tooenable инструкции T-SQL может tooexecute для баз данных и резервных копий.</span><span class="sxs-lookup"><span data-stu-id="53caa-104">Then, you will be able tooexecute T-SQL statements tooenable encryption for your databases and backups.</span></span>

<span data-ttu-id="53caa-105">Существует несколько способов шифрования, преимуществами которых вы можете воспользоваться.</span><span class="sxs-lookup"><span data-stu-id="53caa-105">There are several forms of encryption you can take advantage of:</span></span>

* [<span data-ttu-id="53caa-106">Прозрачное шифрование данных (TDE)</span><span class="sxs-lookup"><span data-stu-id="53caa-106">Transparent Data Encryption (TDE)</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="53caa-107">Зашифрованные резервные копии</span><span class="sxs-lookup"><span data-stu-id="53caa-107">Encrypted backups</span></span>](https://msdn.microsoft.com/library/dn449489.aspx)
* [<span data-ttu-id="53caa-108">Шифрование на уровне столбцов (CLE)</span><span class="sxs-lookup"><span data-stu-id="53caa-108">Column Level Encryption (CLE)</span></span>](https://msdn.microsoft.com/library/ms173744.aspx)

<span data-ttu-id="53caa-109">Hello следующие сценарии Transact-SQL содержатся примеры для каждого из этих областей.</span><span class="sxs-lookup"><span data-stu-id="53caa-109">hello following Transact-SQL scripts provide examples for each of these areas.</span></span>

### <a name="prerequisites-for-examples"></a><span data-ttu-id="53caa-110">Предварительные требования для примеров</span><span class="sxs-lookup"><span data-stu-id="53caa-110">Prerequisites for examples</span></span>

<span data-ttu-id="53caa-111">Каждый пример основан на предварительные условия двух hello: вызывается асимметричного ключа из хранилища ключей **CONTOSO_KEY** и учетные данные, созданные hello хранилищем ключей AZURE Integration называемую **Azure_EKM_TDE_cred**.</span><span class="sxs-lookup"><span data-stu-id="53caa-111">Each example is based on hello two prerequisites: an asymmetric key from your key vault called **CONTOSO_KEY** and a credential created by hello AKV Integration feature called **Azure_EKM_TDE_cred**.</span></span> <span data-ttu-id="53caa-112">Hello следующие команды Transact-SQL эти необходимые компоненты установки для запуска примеров hello.</span><span class="sxs-lookup"><span data-stu-id="53caa-112">hello following Transact-SQL commands setup these prerequisites for running hello examples.</span></span>

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

### <a name="transparent-data-encryption-tde"></a><span data-ttu-id="53caa-113">Прозрачное шифрование данных (TDE)</span><span class="sxs-lookup"><span data-stu-id="53caa-113">Transparent Data Encryption (TDE)</span></span>

1. <span data-ttu-id="53caa-114">Создать toobe входа SQL Server, используемые hello компонента Database Engine для прозрачного шифрования данных, а затем добавить tooit hello учетных данных.</span><span class="sxs-lookup"><span data-stu-id="53caa-114">Create a SQL Server login toobe used by hello Database Engine for TDE, then add hello credential tooit.</span></span>

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

1. <span data-ttu-id="53caa-115">Создайте ключ шифрования базы данных hello, который будет использоваться для прозрачного шифрования данных.</span><span class="sxs-lookup"><span data-stu-id="53caa-115">Create hello database encryption key that will be used for TDE.</span></span>

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

### <a name="encrypted-backups"></a><span data-ttu-id="53caa-116">Зашифрованные резервные копии</span><span class="sxs-lookup"><span data-stu-id="53caa-116">Encrypted backups</span></span>

1. <span data-ttu-id="53caa-117">Создайте toobe входа SQL Server, используемые hello СУБД для шифрования резервных копий и добавьте tooit hello учетных данных.</span><span class="sxs-lookup"><span data-stu-id="53caa-117">Create a SQL Server login toobe used by hello Database Engine for encrypting backups, and add hello credential tooit.</span></span>

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

1. <span data-ttu-id="53caa-118">Hello резервного копирования базы данных, указав шифрование с асимметричным ключом hello хранятся в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="53caa-118">Backup hello database specifying encryption with hello asymmetric key stored in hello key vault.</span></span>

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a><span data-ttu-id="53caa-119">Шифрование на уровне столбцов (CLE)</span><span class="sxs-lookup"><span data-stu-id="53caa-119">Column Level Encryption (CLE)</span></span>

<span data-ttu-id="53caa-120">Этот скрипт создает симметричный ключ, защищенный асимметричным ключом hello в хранилище ключей hello, а затем использует данные hello tooencrypt симметричного ключа в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="53caa-120">This script creates a symmetric key protected by hello asymmetric key in hello key vault, and then uses hello symmetric key tooencrypt data in hello database.</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="53caa-121">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="53caa-121">Additional resources</span></span>

<span data-ttu-id="53caa-122">Дополнительные сведения о toouse этих функций шифрования в статье [с помощью расширенного управления Ключами с функциями шифрования SQL Server](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span><span class="sxs-lookup"><span data-stu-id="53caa-122">For more information on how toouse these encryption features, see [Using EKM with SQL Server Encryption Features](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span></span>

<span data-ttu-id="53caa-123">Обратите внимание, что hello в этой статье предполагается, что уже есть SQL Server на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="53caa-123">Note that hello steps in this article assume that you already have SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="53caa-124">Если нет, см. статью [Подготовка виртуальной машины с SQL Server в Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="53caa-124">If not, see [Provision a SQL Server virtual machine in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="53caa-125">Другие темы, связанные с запуском SQL Server на виртуальных машинах Azure, см. в статье [Общие сведения об SQL Server на виртуальных машинах Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="53caa-125">For other guidance on running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
