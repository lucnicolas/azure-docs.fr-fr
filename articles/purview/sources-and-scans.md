---
title: Sources de données et types de fichiers pris en charge
description: Cet article fournit des informations conceptuelles relatives aux sources de données et types de fichiers pris en charge dans Purview.
author: viseshag
ms.author: viseshag
ms.service: purview
ms.subservice: purview-data-catalog
ms.topic: conceptual
ms.date: 11/24/2020
ms.custom: references_regions
ms.openlocfilehash: 3b19fab33d0c8f53025605fd14fe65f08e660392
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2021
ms.locfileid: "101677914"
---
# <a name="supported-data-sources-and-file-types-in-azure-purview"></a>Sources de données et types de fichiers pris en charge dans Azure Purview

Cet article traite des sources de données et types de fichiers pris en charge, ainsi que des concepts d’analyse dans Purview.

## <a name="supported-data-sources"></a>Sources de données prises en charge

Azure Purview prend en charge les sources suivantes :

| Type de magasin | Type d’authentification pris en charge | Configurer des analyses via UX/PowerShell |
| ---------- | ------------------- | ------------------------------ |
| SQL Server local                   | Authentification SQL                        | UX                                |
| Azure Synapse Analytics (anciennement SQL DW)            | Authentification SQL, principal de service, MSI               | UX                             |
| Azure SQL Database (DB)                  | Authentification SQL, principal de service, MSI               | UX |
| Azure SQL Database Managed Instance      | Authentification SQL, principal de service, MSI               | UX    |
| Stockage Blob Azure                       | Clé de compte, principal de service, MSI | UX            |
| Explorateur de données Azure                      | Principal de service                              | UX            |
| Compte Azure Data Lake Storage Gen1 (ADLS Gen1) | Principal du service, MSI                              | UX            |
| Azure Data Lake Storage Gen2 (ADLS Gen2) | Clé de compte, principal de service, MSI            | UX            |
| Azure Cosmos DB                          | Clé du compte                                    | UX            |


> [!Note]
> Azure Data Lake Storage Gen2 est maintenant en disponibilité générale. Nous vous recommandons de commencer à l’utiliser dès aujourd'hui. Pour plus d’informations, consultez la [page du produit](https://azure.microsoft.com/en-us/services/storage/data-lake-storage/).

## <a name="file-types-supported-for-scanning"></a>Types de fichiers pris en charge pour l’analyse

Les types de fichiers suivants sont pris en charge pour l’analyse, ainsi que pour l’extraction et la classification des schémas, le cas échéant :

- Formats de fichiers structurés pris en charge par l’extension : AVRO, ORC, PARQUET, CSV, JSON, PSV, SSV, TSV, TXT, XML, GZIP
- Formats de fichiers de document pris en charge par l’extension : DOC, DOCM, DOCX, DOT, ODP, ODS, ODT, PDF, POT, PPS, PPSX, PPT, PPTM, PPTX, XLC, XLS, XLSB, XLSM, XLSX, XLT
- Purview prend également en charge les extensions de fichiers personnalisées et les analyseurs personnalisés.
 
> [!Note]
> Chaque fichier Gzip doit être mappé à un seul fichier csv contenu. Les fichiers Gzip sont soumis à des règles système et personnalisées de classification. Actuellement, nous ne prenons pas en charge l’analyse d’un fichier gzip mappé à plusieurs fichiers contenus, ou à n’importe quel autre type de fichier qui n’est pas csv. 

## <a name="sampling-within-a-file"></a>Échantillonnage dans un fichier

Dans la terminologie Purview,
- Analyse L1 : Extrait des informations et des métadonnées de base, telles que le nom de fichier, la taille et le nom complet
- Analyse L2 : Extrait le schéma pour les types de fichiers structurés et les tables de base de données
- Analyse L3 : Extrait le schéma, le cas échéant, et soumet le fichier échantillonné au système et aux règles de classification personnalisées

Pour tous les formats de fichiers structurés, l’analyseur Purview échantillonne les fichiers comme suit :

- Pour les types de fichiers structurés, il échantillonne 128 lignes dans chaque colonne ou 1 Mo, selon la valeur la plus faible.
- Pour les formats de fichiers de document, il échantillonne 20 Mo de chaque fichier.
    - Un fichier de document dont la taille est supérieure à 20 Mo n’est pas soumis à une analyse détaillée (sous réserve de classification). Dans ce cas, Purview capture uniquement les métadonnées de base, telles que le nom de fichier et le nom complet.

## <a name="resource-set-file-sampling"></a>Échantillonnage de fichiers de jeu de ressources

Dans Purview, un dossier ou un groupe de fichiers de partition est détecté en tant qu’*ensemble de ressources* s’il correspond à une stratégie d’ensemble de ressources système ou à une stratégie d’ensemble de ressources définie par le client. Si un ensemble de ressources est détecté, Purview échantillonne chaque dossier qu’il contient. Apprenez-en davantage sur les ensembles de ressources [ici](concept-resource-sets.md).

Échantillonnage de fichiers pour les ensembles de ressources par types de fichiers :

- **Fichiers délimités (CSV, PSV, SSV, TSV)** - 1 fichier sur 100 est échantillonné (analyse L3) dans un dossier ou groupe de fichiers de partition considérés comme « ensemble de ressources »
- **Types de fichiers Data Lake (Parquet, Avro, Orc)** - 1 fichier des 18446744073709551615 (longueur maximale) est échantillonné (analyse L3) dans un dossier ou groupe de fichiers de partition considérés comme *ensemble de ressources*
- **Autres types de fichiers structurés (JSON, XML, TXT)** - 1 fichier sur 100 est échantillonné (analyse L3) dans un dossier ou groupe de fichiers de partition considérés comme « ensemble de ressources »
- **Objets SQL et entités CosmosDB** - chaque fichier est soumis à une analyse L3.
- **Types de fichiers de document** - chaque fichier est soumis à un analyse L3. Les modèles d’ensembles de ressources ne s’appliquent pas à ces types de fichiers.

## <a name="scan-regions"></a>Analyser des régions
Voici une liste de toutes les régions de la source de données Azure (centre de données) sur lesquelles l’analyseur Purview s’exécute. Si votre source de données Azure se trouve dans une région qui ne figure pas dans cette liste, l’analyseur s’exécutera dans la région de votre instance de Purview.
 
### <a name="purview-scanner-regions"></a>Régions de l’analyseur Purview

- EastUs
- EastUs2 
- SouthCentralUS
- WestUs
- WestUs2
- AsieSudEst
- WestEurope
- NorthEurope
- UkSouth
- AustraliaEast
- CanadaCentral
- BrazilSouth
- CentralIndia
- JaponEst
- SouthAfricaNorth
- FranceCentral

## <a name="classification"></a>classification ;

Toutes les règles de classification système 105 s’appliquent aux formats de fichiers structurés. Seules les règles de classification MCE s’appliquent aux types de fichiers de document (et non aux modèles regex natifs d’analyse des données, de détection basée sur les filtres). Pour plus d’informations sur les classifications prises en charge, consultez [Classifications prises en charge dans Azure Purview](supported-classifications.md).

## <a name="next-steps"></a>Étapes suivantes

- [Tutoriel : Exécuter le starter kit et analyser les données](tutorial-scan-data.md)
- [Gérer des sources de données dans Azure Purview (préversion)](manage-data-sources.md)