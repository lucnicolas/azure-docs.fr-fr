---
title: Configurer votre environnement pour l’opérateur Blueprint
description: Découvrez comment configurer votre environnement Azure pour l’utiliser avec le rôle intégré Azure « Opérateur Blueprint ».
ms.date: 02/05/2021
ms.topic: how-to
ms.openlocfilehash: b43a33f4bac92903bd07454041d11850f217d480
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2021
ms.locfileid: "100558728"
---
# <a name="configure-your-environment-for-a-blueprint-operator"></a>Configurer votre environnement pour un opérateur Blueprint

La gestion de vos définitions et affectations de blueprint peut être attribuée à différentes équipes. Il arrive souvent qu'une équipe d'architectes ou de gouvernance soit en charge de la gestion du cycle de vie de vos définitions de blueprint, et une équipe d’exploitation en charge de la gestion des affectations de ces définitions de blueprint contrôlées de manière centralisée.

Le rôle intégré **Opérateur blueprint** est spécifiquement conçu pour être utilisé dans ce type de scénario. Ce rôle permet aux équipes des opérations de gérer l’affectation des définitions de blueprint, sans possibilité de les modifier. Cela implique une configuration de votre environnement Azure et cet article détaille les étapes nécessaires.

## <a name="grant-permission-to-the-blueprint-operator"></a>Accorder l’autorisation à l’opérateur Blueprint

La première étape consiste à attribuer le rôle d'**opérateur Blueprint** au compte ou groupe de sécurité (recommandé) qui sera en charge d'affecter les blueprints. Cette action doit être effectuée au plus haut niveau de la hiérarchie des groupes d'administration, qui englobe tous les groupes d’administration et abonnements pour lesquels l’équipe des opérations doit avoir un accès en matière d'affectation de blueprints. Il est recommandé de suivre le principe du privilège minimum lors de l’octroi de ces autorisations.

1. (Recommandé) [Créer un groupe de sécurité et ajouter des membres](../../../active-directory/fundamentals/active-directory-groups-create-azure-portal.md)

1. [Attribuer un rôle Azure](../../../role-based-access-control/role-assignments-portal.md) d'**d’opérateur Blueprint** au compte ou groupe de sécurité

## <a name="user-assign-managed-identity"></a>Identité managée attribuée par l'utilisateur

Une définition de blueprint peut utiliser des identités managées affectées par le système ou par l’utilisateur. Cela étant, lorsque vous utilisez le rôle d'**opérateur Blueprint**, la définition de blueprint doit être configurée pour utiliser une identité managée affectée par l’utilisateur. De plus, le compte ou groupe de sécurité qui se voit attribuer le rôle d'**opérateur Blueprint** doit se voir attribuer le rôle d'**opérateur d'identité managée** sur l'identité managée affectée par l'utilisateur. Sans cette autorisation, les affectations de blueprint échouent.

1. [Créez une identité managée affectée par l’utilisateur](../../../active-directory/managed-identities-azure-resources/how-to-manage-ua-identity-portal.md#create-a-user-assigned-managed-identity) pour l’utiliser dans le cadre d’un blueprint attribué.

1. Accordez à l’identité managée affectée par l’utilisateur toutes les autorisations ou tous les rôles requis par la définition de blueprint pour l’étendue prévue.

1. [Attribuer un rôle Azure](../../../role-based-access-control/role-assignments-portal.md)d’**Opérateur d'identité managée** au compte ou groupe de sécurité. Étendez l’attribution de rôle à la nouvelle identité managée affectée par l’utilisateur.

1. En tant qu’**opérateur Blueprint**, [attribuez un blueprint](../create-blueprint-portal.md#assign-a-blueprint) utilisant la nouvelle identité managée affectée par l’utilisateur.

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur le [cycle de vie des blueprints](../concepts/lifecycle.md)
- Comprendre comment utiliser les [paramètres statiques et dynamiques](../concepts/parameters.md).
- Apprendre à personnaliser l’[ordre de séquencement des blueprints](../concepts/sequencing-order.md).
- Découvrir comment utiliser le [verrouillage de ressources de blueprint](../concepts/resource-locking.md).
- Résoudre les problèmes durant l’affectation d’un blueprint en suivant les étapes de [dépannage général](../troubleshoot/general.md).