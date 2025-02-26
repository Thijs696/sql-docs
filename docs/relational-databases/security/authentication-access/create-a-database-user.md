---
title: "Create a database user"
description: Learn how to create the most common types of database users by using SQL Server Management Studio or Transact-SQL.
author: VanMSFT
ms.author: vanto
ms.reviewer: randolphwest
ms.date: 07/18/2024
ms.service: sql
ms.subservice: security
ms.topic: conceptual
f1_keywords:
  - "sql13.swb.user.securables.f1"
  - "SQL13.SWB.DATABASEUSER.GENERAL.F1"
helpviewer_keywords:
  - "database users, creating"
  - "creating users with Management Studio"
  - "mapping users"
  - "users [SQL Server], creating"
  - "database user additions [SQL Server]"
  - "database users, mapping"
  - "CREATE USER [Management Studio]"
  - "users [SQL Server], adding"
  - "mapping database users"
monikerRange: ">=aps-pdw-2016 || =azuresqldb-current || =azure-sqldw-latest || >=sql-server-2016 || >=sql-server-linux-2017 || =azuresqldb-mi-current"
---
# Create a database user

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

This article describes how to create the most common types of database users. There are 13 types of users. The complete list is provided in the article [CREATE USER](../../../t-sql/statements/create-user-transact-sql.md). All varieties of [!INCLUDE [ssNoVersion](../../../includes/ssnoversion-md.md)] support database users, but not necessarily all types of users.

You can create a database user by using [!INCLUDE [ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] or by using [!INCLUDE [tsql](../../../includes/tsql-md.md)].

## Understand the types of users

[!INCLUDE [ssManStudio](../../../includes/ssmanstudio-md.md)] presents six options when creating a database user. The following diagram shows the six options in the green box, and indicates what they represent.

:::image type="content" source="media/typesofusers.png" alt-text="Diagram that explains the different types of users.":::

### Select the type of user

If you're new to [!INCLUDE [ssNoVersion](../../../includes/ssnoversion-md.md)], it can be difficult to determine what type of user you want to create. First ask yourself, does the person or group that needs to access the database have a login?

#### Create a user with a login

Logins in the `master` database are common for the people who manage the [!INCLUDE [ssNoVersion](../../../includes/ssnoversion-md.md)] and for people who need to access many or all of the database on the instance of [!INCLUDE [ssNoVersion](../../../includes/ssnoversion-md.md)]. For this situation, create a **SQL user with login**. The database user is the identity of the login when it connects to a database. The database user can use the same name as the login, but that isn't required. This article assumes that a login already exists in [!INCLUDE [ssNoVersion](../../../includes/ssnoversion-md.md)]. For information about how to create a login, see [Create a Login](create-a-login.md).

#### Create user without a login

If the person or group that needs to access the database doesn't have a login and if they only need access to one or few databases, create a **Windows user** or a **SQL user with password**. Also called a [contained database user](../contained-database-users-making-your-database-portable.md). A contained database user isn't associated with a login in the `master` database. This is an excellent choice when you want to be able to easily move your database between instances of [!INCLUDE [ssNoVersion](../../../includes/ssnoversion-md.md)]. To use this option on [!INCLUDE [ssNoVersion](../../../includes/ssnoversion-md.md)], an administrator must first enable contained databases for the [!INCLUDE [ssNoVersion](../../../includes/ssnoversion-md.md)], and the database be enabled for containment. For more information, see [Make your database portable by using contained databases](../contained-database-users-making-your-database-portable.md).

> [!IMPORTANT]  
> When connecting as a contained database user, you must provide the name of the database as part of the connection string. To specify the database in [!INCLUDE [ssmanstudiofull-md](../../../includes/ssmanstudiofull-md.md)] (SSMS), in the **Connect to** dialog box, select **Options**, and then select the **Connection Properties** tab.

Select **SQL user with password** or a **SQL user with login** based on a **SQL Server authentication login**, when the person connecting can't authenticate with Windows authentication. This is common when people outside of your organization (for example, customers) are connecting to your [!INCLUDE [ssNoVersion](../../../includes/ssnoversion-md.md)].

> [!TIP]  
> For people inside your organization, Windows authentication is a better choice, because they won't have to remember an additional password, and because Windows authentication offers additional security features such as Kerberos.

## Background

A user is a database level security principal. Logins must be mapped to a database user to connect to a database. A login can be mapped to different databases as different users but can only be mapped as one user in each database. In a partially contained database, a user can be created that doesn't have a login. For more information about contained database users, see [CREATE USER](../../../t-sql/statements/create-user-transact-sql.md). If the guest user in a database is enabled, a login that isn't mapped to a database user can enter the database as the guest user.

> [!IMPORTANT]  
> The guest user is ordinarily disabled. Don't enable the guest user unless it's necessary.

As a security principal, permissions can be granted to users. The scope of a user is the database. To connect to a specific database on the instance of [!INCLUDE [ssNoVersion](../../../includes/ssnoversion-md.md)], a login must be mapped to a database user. Permissions inside the database are granted and denied to the database user, not the login.

## Permissions

Requires `ALTER ANY USER` permission on the database.

## <a id="SSMSProcedure"></a> Create a user with SSMS

1. In Object Explorer, expand the **Databases** folder.

1. Expand the database in which to create the new database user.

1. Right-click the **Security** folder, point to **New**, and select **User...**.

1. In the **Database User - New** dialog box, on the **General** page, select one of the following user types from the **User type** list:

   - **SQL user with login**
   - **SQL user with password** (when contained database is enabled)
   - **SQL user without login**
   - **User mapped to a certificate**
   - **User mapped to an asymmetric key**
   - **Windows user**

1. When you select an option, the remaining options in the dialog might change. Some options only apply to specific types of database users. Some options can be left blank and use a default value.

   - **User name**

     Enter a name for the new user. If you chose **Windows user** from the **User type** list, you can also select the ellipsis **(...)** to open the **Select User or Group** dialog box.

   - **Login name**

     Enter the login for the user. Alternately, select the ellipsis **(...)** to open the **Select Login** dialog box. **Login name** is available if you select either **SQL user with login** or **Windows user** from the **User type** list.

   - **Password** and **Confirm password**

     Enter a password for users who authenticate at the database.

   - **Default language**

     Enter the default language of the user.

   - **Default schema**

     Enter the schema that will own objects created by this user. Alternately, select the ellipsis **(...)** to open the **Select Schema** dialog box. **Default schema** is available if you select either **SQL user with login**, **SQL user without login**, or **Windows user** from the **User type** list.

   - **Certificate name**

     Enter the certificate to be used for the database user. Alternately, select the ellipsis **(...)** to open the **Select Certificate** dialog box. **Certificate name** is available if you select **User mapped to a certificate** from the **User type** list.

   - **Asymmetric key name**

     Enter the key to be used for the database user. Alternately, select the ellipsis **(...)** to open the **Select Asymmetric Key** dialog box. **Asymmetric key name** is available if you select **User mapped to an asymmetric key** from the **User type** list.

1. Select **OK**.

### Additional options

The **Database User - New** dialog box also offers options on four other pages: **Owned Schemas**, **Membership**, **Securables**, and **Extended Properties**.

- The **Owned Schemas** page lists all possible schemas that can be owned by the new database user. To add schemas to or remove them from a database user, under **Schemas owned by this user**, select or clear the check boxes next to the schemas.

- The **Membership** page lists all possible database membership roles that can be owned by the new database user. To add roles to or remove them from a database user, under **Database role membership**, select or clear the check boxes next to the roles.

- The **Securables** page lists all possible securables and the permissions on those securables that can be granted to the login.

- The **Extended properties** page allows you to add custom properties to database users. The following options are available on this page.

  - **Database**

    Displays the name of the selected database. This field is read-only.

  - **Collation**

    Displays the collation used for the selected database. This field is read-only.

  - **Properties**

    View or specify the extended properties for the object. Each extended property consists of a name/value pair of metadata associated with the object.

  - **Ellipsis (...)**

    Select the ellipsis **(...)** after **Value** to open the **Value for Extended Property** dialog box. Type or view the value of the extended property in this larger location. For more information, see [Value for Extended Property Dialog Box](../../databases/value-for-extended-property-dialog-box.md).

  - **Delete**

    Removes the selected extended property.

## <a id="TsqlProcedure"></a> Create a user using T-SQL

1. In **Object Explorer**, connect to an instance of [!INCLUDE [ssDE](../../../includes/ssde-md.md)].

1. On the **Standard** bar, select **New Query**.

1. Copy and paste the following example into the query window and select **Execute**.

   ```sql
   -- Creates the login AbolrousHazem with password '340$Uuxwp7Mcxo7Khy'.
   CREATE LOGIN AbolrousHazem
   WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';
   GO

   -- Creates a database user for the login created previously.
   CREATE USER AbolrousHazem
   FOR LOGIN AbolrousHazem;
   GO
   ```

For more information, see [CREATE USER](../../../t-sql/statements/create-user-transact-sql.md), which contains many more [!INCLUDE [tsql](../../../includes/tsql-md.md)] examples.

## Related content

- [Principals (Database Engine)](principals-database-engine.md)
- [Create a Login](create-a-login.md)
- [CREATE LOGIN (Transact-SQL)](../../../t-sql/statements/create-login-transact-sql.md)
