# Liquibase Installation & Local Setup Guide

## Quick Start

```powershell
choco install Liquibase
```

## 1. Install Liquibase Locally

On Windows, the easiest method is **Chocolatey**:

```powershell
choco install liquibase
```

Alternatively, download directly from [liquibase.com](https://liquibase.com)

> **Note:** Liquibase requires Java, so make sure you have it installed.

## 2. Install the SQL Server JDBC Driver

Liquibase needs the Microsoft JDBC driver to connect to SQL Server.

**Download from Microsoft:**
https://learn.microsoft.com/en-us/sql/connect/jdbc/download-microsoft-jdbc-driver-for-sql-server?view=sql-server-ver17

**Expected file:**
```
mssql-jdbc-12.x.x.jre8.jar
```

**Place it in:**
```
C:\liquibase\drivers\
```

## 3. Create a Liquibase Project Folder

A simple starter layout:

```
C:\liquibase-project\
  liquibase.properties
  db\
    changelog\
      master.xml
      001-create-customer-table.xml
```

## 4. Configure liquibase.properties

This file tells Liquibase how to connect to your local SQL Server.

**Example:**
```properties
classpath=C:/liquibase/drivers/mssql-jdbc-12.6.1.jre8.jar
changeLogFile=db/changelog/master.xml
url=jdbc:sqlserver://localhost:1433;databaseName=MyTestDb
username=sa
password=YourStrongPassword123
```

> **Tip:** If you use Windows Authentication, you can configure that too, but SQL auth is simpler for practice.

## 5. Create Your Master Changelog

**db/changelog/master.xml:**

```xml
<databaseChangeLog>
    <include file="001-create-customer-table.xml"/>
</databaseChangeLog>
```

## 6. Create Your First Changeset

**db/changelog/001-create-customer-table.xml:**

```xml
<changeSet id="001" author="Jeff Loomis">
    <createTable tableName="Customer">
        <column name="CustomerId" type="INT">
            <constraints primaryKey="true" nullable="false"/>
        </column>
        <column name="FirstName" type="NVARCHAR(100)" />
        <column name="LastName" type="NVARCHAR(100)" />
    </createTable>
</changeSet>
```

## 7. Run Liquibase Manually

Open a terminal in your project folder:

```powershell
liquibase update
```

Liquibase will:
- Connect to your local SQL Server
- Create the DATABASECHANGELOG table
- Apply your changeset
- Create the Customer table

This is the same behavior you'd get in CI/CD — just executed manually.

## What You Can Practice Locally

- ✅ Creating tables
- ✅ Adding columns
- ✅ Modifying columns
- ✅ Adding indexes
- ✅ Adding foreign keys
- ✅ Data migrations
- ✅ Rollbacks
- ✅ Multi-file changelog organization
- ✅ Validating changesets
- ✅ Dry-run SQL generation

All without touching CI/CD!

## Helpful Commands

### Validate your changelog
```powershell
liquibase validate
```

### See the SQL without running it
```powershell
liquibase updateSQL
```

### Roll back the last change
```powershell
liquibase rollbackCount 1
```

### Mark changes as executed without running them
```powershell
liquibase changelogSync
```

## Summary

You can practice Liquibase locally with:

- Local SQL Server
- Liquibase CLI
- JDBC driver
- A simple folder structure
- Manual `liquibase update` commands

This gives you the full Liquibase experience without needing CI/CD.

## Next Steps

Consider creating:
- A complete starter project folder structure
- A PowerShell script to automate local Liquibase runs
- A practice roadmap (beginner → advanced)
- A set of exercises to master Liquibase quickly
