---
title: Activer le chiffrement basé sur l’hôte sur Azure Kubernetes Service (AKS)
description: Découvrez comment configurer un chiffrement basé sur l’hôte dans un cluster Azure Kubernetes service (AKS)
services: container-service
ms.topic: article
ms.date: 03/03/2021
ms.custom: devx-track-azurepowershell
ms.openlocfilehash: 7eb3215aeb1f7c6508092d18fbebd90f852efe63
ms.sourcegitcommit: 4b0e424f5aa8a11daf0eec32456854542a2f5df0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/20/2021
ms.locfileid: "107772916"
---
# <a name="host-based-encryption-on-azure-kubernetes-service-aks-preview"></a>Activer le chiffrement basé sur l’hôte sur Azure Kubernetes Service (AKS) (préversion)

Avec le chiffrement basé sur l’hôte, les données stockées sur l’hôte de machine virtuelle des machines virtuelles de vos nœuds d’agent AKS sont chiffrées au repos et les flux sont chiffrés dans le service de stockage. Cela signifie que les disques temporaires sont chiffrés au repos avec des clés gérées par la plateforme. Le cache du système d’exploitation et des disques de données est chiffré au repos avec des clés gérées par le client ou par la plateforme, selon le type de chiffrement défini sur ces disques. Par défaut, lorsque vous utilisez AKS, le système d’exploitation et les disques de données sont chiffrés au repos avec des clés gérées par la plateforme, ce qui signifie que les caches de ces disques sont également chiffrés au repos par défaut avec des clés gérées par la plateforme.  Vous pouvez spécifier vos propres clés gérées à l’aide de [Bring your own keys (BYOK) avec des disques Azure dans Azure Kubernetes service](azure-disk-customer-managed-keys.md). Le cache de ces disques sera également chiffré à l’aide de la clé que vous spécifiez au cours de cette étape.


## <a name="before-you-begin"></a>Avant de commencer

Cette fonctionnalité ne peut être définie qu’au moment de la création du cluster ou de la création du pool de nœuds.

> [!NOTE]
> Le chiffrement basé sur l’hôte est disponible dans les [régions Azure][supported-regions] qui prennent en charge le chiffrement côté serveur des disques managés Azure et uniquement avec des [tailles de machine virtuelle spécifiques prises en charge][supported-sizes].

### <a name="prerequisites"></a>Prérequis

- Vérifiez que l'extension CLI `aks-preview` version 0.4.73 ou ultérieure est installée.
- Vérifiez que l’indicateur de fonctionnalité `EnableEncryptionAtHostPreview` sous `Microsoft.ContainerService` est activé.

Vous devez activer la fonctionnalité pour votre abonnement avant d’utiliser la propriété EncryptionAtHost pour votre cluster Azure Kubernetes Service. Suivez les étapes ci-dessous pour activer la fonctionnalité pour votre abonnement :

1. Exécutez la commande suivante pour inscrire la fonctionnalité pour votre abonnement

```azurecli-interactive
Register-AzProviderFeature -FeatureName "EncryptionAtHost" -ProviderNamespace "Microsoft.Compute"
```
2. Vérifiez que l’état de l’inscription est Inscrit (cela prend quelques minutes) à l’aide de la commande ci-dessous avant d’essayer la fonctionnalité.

```azurecli-interactive
Get-AzProviderFeature -FeatureName "EncryptionAtHost" -ProviderNamespace "Microsoft.Compute"
```

### <a name="install-aks-preview-cli-extension"></a>Installer l’extension CLI de préversion d’aks

Pour créer un cluster AKS qui héberge le chiffrement basé sur l’hôte, vous avez besoin de la dernière extension CLI *aks-preview*. Installez l’extension Azure CLI *aks-preview* à l’aide de la commande [az extension add][az-extension-add], ou recherchez toutes les mises à jour disponibles à l’aide de la commande [az extension update][az-extension-update] :

```azurecli-interactive
# Install the aks-preview extension
az extension add --name aks-preview

# Update the extension to make sure you have the latest version installed
az extension update --name aks-preview
```

### <a name="limitations"></a>Limites

- Ne peut être activé que sur les nouveaux pools de nœuds.
- Ne peut être activé que dans les [régions Azure][supported-regions] qui prennent en charge le chiffrement côté serveur des disques managés Azure et uniquement avec des [tailles de machine virtuelle spécifiques prises en charge][supported-sizes].
- Requiert un cluster AKS et un pool de nœuds basés sur Virtual Machine Scale Sets (VMSS) comme *type d’ensemble de machines virtuelles*.

## <a name="use-host-based-encryption-on-new-clusters-preview"></a>Utiliser le chiffrement basé sur l’hôte sur les nouveaux clusters (préversion)

Configurez les nœuds de l’agent de cluster pour utiliser le chiffrement basé sur l’hôte lorsque le cluster est créé. 

```azurecli-interactive
az aks create --name myAKSCluster --resource-group myResourceGroup -s Standard_DS2_v2 -l westus2 --enable-encryption-at-host
```

Si vous souhaitez créer des clusters sans chiffrement basé sur l'hôte, vous pouvez le faire en omettant le paramètre `--enable-encryption-at-host`.

## <a name="use-host-based-encryption-on-existing-clusters-preview"></a>Utiliser le chiffrement basé sur l’hôte sur les clusters existants (préversion)

Vous pouvez activer le chiffrement basé sur l’hôte sur les clusters existants en ajoutant un nouveau pool de nœuds à votre cluster. Configurez un nouveau pool de nœuds pour utiliser le chiffrement basé sur l'hôte à l'aide du paramètre `--enable-encryption-at-host`.

```azurecli
az aks nodepool add --name hostencrypt --cluster-name myAKSCluster --resource-group myResourceGroup -s Standard_DS2_v2 -l westus2 --enable-encryption-at-host
```

Si vous souhaitez créer de nouveaux pools de nœuds sans la fonctionnalité de chiffrement basé sur l'hôte, vous pouvez le faire en omettant le paramètre `--enable-encryption-at-host`.

## <a name="next-steps"></a>Étapes suivantes

Passez en revue les [meilleures pratiques pour la sécurité du cluster AKS][best-practices-security] En savoir plus sur le [chiffrement basé sur l’hôte](../virtual-machines/disk-encryption.md#encryption-at-host---end-to-end-encryption-for-your-vm-data).


<!-- LINKS - external -->

<!-- LINKS - internal -->
[az-extension-add]: /cli/azure/extension#az_extension_add
[az-extension-update]: /cli/azure/extension#az_extension_update
[best-practices-security]: ./operator-best-practices-cluster-security.md
[supported-regions]: ../virtual-machines/disk-encryption.md#supported-regions
[supported-sizes]: ../virtual-machines/disk-encryption.md#supported-vm-sizes
[azure-cli-install]: /cli/azure/install-azure-cli
[az-feature-register]: /cli/azure/feature#az_feature_register
[az-feature-list]: /cli/azure/feature#az_feature_list
[az-provider-register]: /cli/azure/provider#az_provider_register
