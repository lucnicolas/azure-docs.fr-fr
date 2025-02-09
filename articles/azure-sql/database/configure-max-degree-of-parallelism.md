---
title: Configurer le degré maximal de parallélisme (MAXDOP)
titleSuffix: Azure SQL Database
description: Apprenez-en davantage sur le degré maximal de parallélisme (MAXDOP).
ms.date: 03/29/2021
services: sql-database
dev_langs:
- TSQL
ms.service: sql-database
ms.subservice: performance
ms.custom: ''
ms.devlang: tsql
ms.topic: conceptual
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.reviewer: ''
ms.openlocfilehash: 31ddf15975abdce70ea02b5de64ea5611e7e72b3
ms.sourcegitcommit: 5fd1f72a96f4f343543072eadd7cdec52e86511e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/01/2021
ms.locfileid: "106110946"
---
# <a name="configure-the-max-degree-of-parallelism-maxdop-in-azure-sql-database"></a>Configurer le degré maximal de parallélisme (MAXDOP) dans Azure SQL Database
[!INCLUDE[appliesto-sqldb](../includes/appliesto-sqldb.md)]

  Cet article décrit le **degré maximal de parallélisme (MAXDOP)** dans Azure SQL Database, et comment il peut être configuré. 

> [!NOTE]
> **Ce contenu est axé sur Azure SQL Database.** Azure SQL Database est basé sur la dernière version stable du moteur de base de données Microsoft SQL Server. Une grande partie du contenu est donc similaire, même si les options de résolution des problèmes et de configuration diffèrent. Pour plus d’informations sur MAXDOP dans SQL Server, consultez [Configurer l’option de configuration serveur du degré maximal de parallélisme](/sql/database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option).

## <a name="overview"></a>Vue d’ensemble
  Dans Azure SQL Database, le paramètre MAXDOP par défaut pour chaque nouvelle base de données et base de données de pool élastique est 8. Cela signifie que le moteur de base de données peut exécuter des requêtes à l’aide de plusieurs threads. Contrairement à SQL Server, où le MAXDOP par défaut au niveau du serveur est 0 (illimité), par défaut, les nouvelles bases de données dans Azure SQL Database sont définies sur MAXDOP 8. Cette valeur par défaut empêche toute utilisation inutile des ressources et garantit une expérience utilisateur cohérente. Il n’est généralement pas nécessaire de configurer plus précisément les charges de travail MAXDOP dans Azure SQL Database, mais cela peut fournir des avantages en tant qu’exercice de réglage des performances avancé.

> [!Note]
>   En septembre 2020, basée sur des années de télémétrie dans le service Azure SQL Database, [MAXDOP 8 a été choisi](https://techcommunity.microsoft.com/t5/azure-sql/changing-default-maxdop-in-azure-sql-database-and-azure-sql/ba-p/1538528) comme valeur par défaut pour les nouvelles bases de données en tant que valeur optimale pour la plus grande variété de charges de travail client. Cette valeur par défaut a permis d’éviter les problèmes de performances dus à un parallélisme excessif. Avant cela, le paramètre par défaut pour les nouvelles bases de données était MAXDOP 0. L’option de configuration au niveau de la base de données MAXDOP n’a pas été modifiée pour les bases de données existantes créées avant septembre 2020.

  En général, si le moteur de base de données choisit d’exécuter une requête à l’aide du parallélisme, le temps d’exécution est plus rapide. Toutefois, le parallélisme excessif peut consommer des ressources de processeur excédentaires sans améliorer les performances de requête. À l’échelle, le parallélisme excédentaire peut avoir un impact négatif sur les performances de requête pour toutes les requêtes qui s’exécutent sur la même instance du moteur de base de données. Par conséquent, la définition d’une limite supérieure pour le parallélisme est un exercice de réglage des performances courant dans les charges de travail SQL Server.

  Le tableau suivant décrit le comportement du moteur de base de données lors de l’exécution de requêtes avec différentes valeurs MAXDOP :

| MAXDOP | Comportement | 
|--|--|
| = 1 | Le moteur de base de données n’exécute pas de requêtes à l’aide de plusieurs threads simultanés. | 
| > 1 | Le moteur de base de données définit une limite supérieure pour le nombre de threads parallèles. Le moteur de base de données choisit le nombre de threads de travail supplémentaires à utiliser. Le nombre total de threads de travail utilisés pour exécuter une requête peut être supérieur à la valeur MAXDOP spécifiée. |
| = 0 | Le moteur de base de données peut utiliser un certain nombre de threads parallèles avec une limite supérieure dépendante du nombre total de processeurs logiques. Le moteur de base de données choisit le nombre de threads parallèles à utiliser.| 
| | |
  
##  <a name="considerations"></a><a name="Considerations"></a> Observations  

-   Dans Azure SQL Database, vous pouvez modifier la valeur MAXDOP par défaut :
    -   Au niveau de la requête, à l’aide de l’[indicateur de requête](/sql/t-sql/queries/hints-transact-sql-query) **MAXDOP**.     
    -   Au niveau de la base de données, avec la [configuration limitée à la base de données](/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) **MAXDOP**.

-   Les considérations et [recommandations](/sql/database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option#Guidelines) à long terme MAXDOP SQL Server s’appliquent à Azure SQL Database. 

-   MAXDOP est appliqué par [tâche](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql). Il n’est pas appliqué par [requête](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql). Cela signifie que lors d’une exécution de requête parallèle, une requête unique peut générer plusieurs tâches avec une limite supérieure déterminée par MAXDOP. Pour plus d’informations, consultez la section *Planification de tâches parallèles* du [Guide de l’architecture des threads et des tâches](/sql/relational-databases/thread-and-task-architecture-guide). 
  
-   Les opérations d'index destinées à créer ou à recréer un index, voire à supprimer un index cluster, peuvent nécessiter une quantité importante de ressources. Vous pouvez remplacer la valeur de degré maximal de parallélisme de la base de données pour les opérations d'index en spécifiant l'option d'index MAXDOP dans l'instruction `CREATE INDEX` ou `ALTER INDEX`. La valeur de MAXDOP est appliquée à l'instruction au moment de son exécution et n'est pas stockée dans les métadonnées de l'index. Pour plus d’informations, consultez [Configurer des opérations d’index parallèles](/sql/relational-databases/indexes/configure-parallel-index-operations).  
  
-   En plus des requêtes et des opérations d'index, cette option de configuration au niveau de la base de données pour MAXDOP contrôle également le parallélisme de DBCC CHECKTABLE, DBCC CHECKDB et DBCC CHECKFILEGROUP. 

##  <a name="recommendations"></a><a name="Security"></a> Recommandations  

  La modification de MAXDOP pour la base de données peut avoir un impact majeur sur les performances de requête et l’utilisation des ressources, qu’il soit positif ou négatif. Toutefois, il n’existe pas de valeur MAXDOP unique optimale pour toutes les charges de travail. Les recommandations relatives à la définition de MAXDOP sont nuancées et dépendent de nombreux facteurs. 

  Certaines charges de travail simultanées peuvent mieux fonctionner avec un MAXDOP différent de celui des autres. Un MAXDOP correctement configuré devrait réduire le risque d’incidents liés aux performances et à la disponibilité et, dans certains cas, réduire les coûts en empêchant toute utilisation inutile des ressources et en réduisant ainsi la taille de l’objectif de service.

### <a name="excessive-parallelism"></a>Parallélisme excessif

  Un MAXDOP plus élevé réduit souvent la durée des requêtes gourmandes en ressources processeur. Toutefois, un parallélisme excessif peut aggraver les performances d’autres charges de travail simultanées en privant les autres requêtes de ressources du processeur et du thread de travail. Dans les cas extrêmes, le parallélisme excessif peut consommer toutes les ressources de la base de données ou du pool élastique, ce qui entraîne des délais d’expiration des requêtes, des erreurs et des interruptions de l’application. 

  Nous recommandons aux clients d’éviter MAXDOP 0 même s’il n’est apparemment pas à l’origine de problèmes. Un parallélisme excessif devient problématique lorsque le processeur et les threads de travail reçoivent plus de requêtes simultanées que ce qui peut être pris en charge par l’objectif de service. Évitez le MAXDOP 0 pour réduire le risque de problèmes futurs potentiels dus à un parallélisme excessif si une base de données est montée en puissance, ou si les générations de matériel futures dans Azure SQL Database fournissent plus de cœurs pour le même objectif de service de base de données.

### <a name="modifying-maxdop"></a>Modification de MAXDOP 

  Si vous déterminez qu’un autre paramètre MAXDOP est optimal pour votre charge de travail Azure SQL Database, vous pouvez utiliser l'`ALTER DATABASE SCOPED CONFIGURATION` instruction T-SQL. Pour obtenir des exemples, consultez la section [Exemples avec Transact-SQL](#examples) ci-dessous. Ajoutez cette étape au processus de déploiement pour modifier MAXDOP après la création de la base de données.

  Si le paramètre MAXDOP non défini par défaut n’offre qu’un sous-ensemble de requêtes dans la charge de travail, vous pouvez remplacer MAXDOP au niveau de la requête en ajoutant l’indicateur OPTION (MAXDOP). Pour obtenir des exemples, consultez la section [Exemples avec Transact-SQL](#examples) ci-dessous. 

  Testez minutieusement vos modifications de configuration MAXDOP avec les tests de charge impliquant des charges de requêtes simultanées réalistes. 

  Le MAXDOP pour les réplicas principaux et secondaires peut être configuré indépendamment pour tirer parti des différents paramètres MAXDOP optimaux pour les charges de travail en lecture-écriture et en lecture seule. Cela s’applique à l’[échelle lecture](read-scale-out.md) Azure SQL Database, à la [géoréplication](active-geo-replication-overview.md) et aux[réplicas secondaires Hyperscale Azure SQL Database](service-tier-hyperscale.md). Par défaut, tous les réplicas secondaires héritent de la configuration MAXDOP du réplica principal.

## <a name="security"></a><a name="Security"></a> Sécurité  
  
###  <a name="permissions"></a><a name="Permissions"></a> Autorisations  
  L'instruction `ALTER DATABASE SCOPED CONFIGURATION` doit être exécutée en tant qu’administrateur de serveur, en tant que membre du rôle de base de données `db_owner` ou en tant qu'utilisateur qui a reçu l'autorisation `ALTER ANY DATABASE SCOPED CONFIGURATION`.
 
## <a name="examples"></a>Exemples   

  Ces exemples utilisent la base de données la plus récente de l’exemple **AdventureWorksLT** lorsque l'option `SAMPLE` est choisie pour une nouvelle base de données unique d’Azure SQL Database.

### <a name="powershell"></a>PowerShell

#### <a name="maxdop-database-scoped-configuration"></a>Configuration MAXDOP au niveau de la base de données   

  Cet exemple montre comment utiliser l’instruction [ALTER DATABASE SCOPED CONFIGURATION](/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) pour configurer l'option `max degree of parallelism` sur `2`. Le paramètre prend immédiatement effet. L’applet de commande PowerShell [Invoke-SqlCmd](/powershell/module/sqlserver/invoke-sqlcmd) exécute les requêtes T-SQL à définir et retourne la configuration au niveau de la base de données MAXDOP. 

```powershell
$dbName = "sample" 
$serverName = <server name here>
$serveradminLogin = <login here>
$serveradminPassword = <password here>
$desiredMAXDOP = 8

$params = @{
    'database' = $dbName
    'serverInstance' =  $serverName
    'username' = $serveradminLogin
    'password' = $serveradminPassword
    'outputSqlErrors' = $true
    'query' = 'ALTER DATABASE SCOPED CONFIGURATION SET MAXDOP = ' + $desiredMAXDOP + ';
     SELECT [value] FROM sys.database_scoped_configurations WHERE [name] = ''MAXDOP'';'
  }
  Invoke-SqlCmd @params
```

Cet exemple est destiné à être utilisé avec les bases de données Azure SQL Database avec des [réplicas en échelle lecture activés](read-scale-out.md), la [géoréplication](active-geo-replication-overview.md)et les [réplicas secondaires Hyperscale Azure SQL Database](service-tier-hyperscale.md). Par exemple, le réplica principal est défini sur un autre MAXDOP par défaut que le réplica secondaire, anticipant ainsi qu’il peut y avoir des différences entre une charge de travail en lecture-écriture et une charge de travail en lecture seule.

```powershell
$dbName = "sample" 
$serverName = <server name here>
$serveradminLogin = <login here>
$serveradminPassword = <password here>
$desiredMAXDOP_primary = 8
$desiredMAXDOP_secondary_readonly = 1
 
$params = @{
    'database' = $dbName
    'serverInstance' =  $serverName
    'username' = $serveradminLogin
    'password' = $serveradminPassword
    'outputSqlErrors' = $true
    'query' = 'ALTER DATABASE SCOPED CONFIGURATION SET MAXDOP = ' + $desiredMAXDOP + ';
    ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP = ' + $desiredMAXDOP_secondary_readonly + ';
    SELECT [value], value_for_secondary FROM sys.database_scoped_configurations WHERE [name] = ''MAXDOP'';'
  }
  Invoke-SqlCmd @params
```

### <a name="transact-sql"></a>Transact-SQL
  
  Vous pouvez utiliser l'[éditeur de requête du Portail Azure](connect-query-portal.md), [SQL Server Management Studio (SSMS)](/sql/ssms/download-sql-server-management-studio-ssms) ou [Azure Data Studio](/sql/azure-data-studio/download-azure-data-studio) pour exécuter des requêtes T-SQL sur votre base de données Azure SQL Database.

1.  Connectez-vous à la base de données Azure SQL Database. Vous ne pouvez pas modifier les configurations au niveau de la base de données dans la base de données MASTER.
  
2.  Dans la barre d’outils standard, sélectionnez **Nouvelle requête**.   
  
3.  Copiez et collez l’exemple suivant dans la fenêtre de requête, puis sélectionnez **Exécuter**. 


#### <a name="maxdop-database-scoped-configuration"></a>Configuration MAXDOP au niveau de la base de données

  Cet exemple montre comment déterminer la configuration au niveau de la base de données MAXDOP dans la base de données actuelle à l’aide de l’affichage catalogue système [sys.database_scoped_configurations](/sql/relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql).

```sql
SELECT [value] FROM sys.database_scoped_configurations WHERE [name] = 'MAXDOP';
```

  Cet exemple montre comment utiliser l’instruction [ALTER DATABASE SCOPED CONFIGURATION](/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) pour configurer l'option `max degree of parallelism` sur `8`. Le paramètre prend immédiatement effet.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION SET MAXDOP = 8;
```  

Cet exemple est destiné à être utilisé avec les bases de données Azure SQL Database avec des [réplicas en échelle lecture activés](read-scale-out.md), la [géoréplication](active-geo-replication-overview.md)et les [réplicas secondaires Hyperscale Azure SQL Database](service-tier-hyperscale.md). Par exemple, le réplica principal est défini sur un autre MAXDOP par défaut que le réplica secondaire, anticipant ainsi qu’il peut y avoir des différences entre une charge de travail en lecture-écriture et une charge de travail en lecture seule. La colonne `value_for_secondary` de `sys.database_scoped_configurations` contient des paramètres pour le réplica secondaire.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET MAXDOP = 8;
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP = 1;
SELECT [value], value_for_secondary FROM sys.database_scoped_configurations WHERE [name] = 'MAXDOP';
```

#### <a name="maxdop-query-hint"></a>MAXDOP (indicateur de requête)

  Cet exemple montre comment exécuter une requête à l’aide de l’indicateur de requête pour forcer `max degree of parallelism` à `2`.  

```sql 
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM SalesLT.SalesOrderDetail  
WHERE UnitPrice < 5  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (MAXDOP 2);    
GO
```
#### <a name="maxdop-index-option"></a>MAXDOP (option d'index)

  Cet exemple montre comment reconstruire un index à l’aide de l’option d’index pour forcer `max degree of parallelism` à `12`.  

```sql 
ALTER INDEX ALL ON SalesLT.SalesOrderDetail 
REBUILD WITH 
   (     MAXDOP = 12
       , SORT_IN_TEMPDB = ON
       , ONLINE = ON);
```

## <a name="see-also"></a>Voir aussi  
* [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql)        
* [sys.database_scoped_configurations (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql)
* [Configurer des opérations d’index parallèles](/sql/relational-databases/indexes/configure-parallel-index-operations)    
* [Indicateurs de requête &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)     
* [Définir les options d’index](/sql/relational-databases/indexes/set-index-options)     
* [Comprendre et résoudre les problèmes de blocage d’Azure SQL Database](understand-resolve-blocking.md)

## <a name="next-steps"></a>Étapes suivantes

* [Surveillance et réglage des performances](/sql/relational-databases/performance/monitor-and-tune-for-performance)
