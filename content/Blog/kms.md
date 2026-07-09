---
title: Key Management Service (KMS)
tags:
  - windows
  - os
publish: true
---
# Introduction à KMS (Key Management Service) : Guide pour Débutant

Le **Key Management Service (KMS)** est une méthode d'activation légitime créée par Microsoft. Elle est conçue pour les entreprises, les écoles ou les organisations (licences en volume) afin de leur permettre d'activer massivement des ordinateurs sur un réseau local sans avoir à contacter les serveurs de Microsoft pour chaque machine.

## 1. Comment fonctionne KMS ?

Au lieu que chaque PC Windows vérifie sa clé de licence individuellement sur Internet auprès de Microsoft, le processus se fait en interne :

- **Le Serveur Hôte KMS :** Un ordinateur de l'organisation (souvent un serveur) est configuré comme "serveur d'activation" local grâce à une clé spéciale fournie par Microsoft.

- **Les Clients KMS :** Les ordinateurs des utilisateurs (Windows 10 ou 11) se connectent à ce serveur local pour s'activer.

- **La validité des 180 jours :** Une activation KMS n'est **pas définitive**. Elle est valable **180 jours**. Le PC Windows tente discrètement de recontacter le serveur KMS toutes les semaines pour renouveler cette période et repartir pour 180 jours. Si un PC reste déconnecté du réseau de l'entreprise pendant plus de 6 mois, Windows affichera un message indiquant qu'il n'est plus activé.

## 2. Où se procurer KMS ?

Il faut d'abord distinguer la fonctionnalité officielle de Microsoft des outils tiers que l'on trouve sur le web :

### La méthode officielle (Professionnelle / Académique)

Si vous êtes administrateur réseau dans une organisation :

- **Le serveur hôte :** Le rôle _Volume Activation Services_ s'installe directement depuis Windows Server. La clé hôte KMS s'obtient sur le **Centre d'administration Microsoft 365** (rubrique Facturation > Vos produits).

- **Les clés clients (GVLK) :** Microsoft fournit **gratuitement et publiquement** les clés d'installation génériques (appelées clés GVLK) pour chaque version de Windows (Pro, Enterprise, Education). Ces clés indiquent simplement à Windows : _"Cherche un serveur KMS sur le réseau pour t'activer"_.

### Note de sécurité concernant "KMS Tools" sur Internet

Si vous cherchez à activer un PC personnel à la maison, vous tomberez souvent sur des logiciels tiers téléchargeables (comme _KMSpico_, _KMS Tools_, etc.).

> ⚠️ **Mise en garde :** Ces outils contournent le système de licence officiel en simulant un faux serveur KMS directement sur votre machine. Ils sont massivement modifiés par des pirates pour inclure des logiciels malveillants (malwares, chevaux de Troie, publicitaires). De plus, l'utilisation de ces outils pour valider un Windows personnel sans posséder de licence en volume enfreint les conditions d'utilisation de Microsoft.

## 3. Usage et commandes de base (Comment l'utiliser)

Sur un réseau disposant d'un serveur KMS fonctionnel, l'activation se fait très simplement à l'aide de l'**Invite de commandes (CMD)** exécutée en mode administrateur. Les commandes reposent sur l'utilitaire Windows `slmgr.vbs` (Software Licensing Manager).

Voici les trois étapes standard pour l'usage de KMS :

### Étape 1 : Installer la clé générique KMS (Clé GVLK)

Il faut d'abord configurer Windows pour qu'il accepte l'activation KMS en lui injectant la clé publique officielle fournie par Microsoft.

- _Exemple pour Windows 10/11 Professionnel :_

```cmd
slmgr /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX
```
  
_(La commande `/ipk` signifie "Install Product Key")._

### Étape 2 : Définir l'adresse du serveur KMS

Vous devez indiquer à votre ordinateur l'adresse IP ou le nom de domaine du serveur KMS de votre organisation.

```
slmgr /skms adresse.du.serveur.kms
```

_(La commande `/skms` signifie "Set KMS Server")._

### Étape 3 : Lancer l'activation

Enfin, vous demandez à Windows de forcer la liaison et de s'activer immédiatement.

```
slmgr /ato
```

_(La commande `/ato` signifie "Activate Operating System")._

### Étape bonus : Vérifier le statut de l'activation

Pour vous assurer que la licence est bien valide et voir combien de jours il reste avant le prochain renouvellement automatique, utilisez :

```
slmgr /dlv
```

## Résumé des clés officielles pour Windows 10 et 11

Voici les clés d'installation client (GVLK) officielles et publiques de Microsoft les plus courantes pour orienter un système vers un serveur KMS :

|**Édition de Windows**|**Clé client KMS officielle (Microsoft)**|
|---|---|
|**Windows 10 / 11 Professionnel**|`W269N-WFGWX-YVC9B-4J6C9-T83GX`|
|**Windows 10 / 11 Entreprise**|`NPPR9-FWDCX-D2C8J-H872K-2YT43`|
|**Windows 10 / 11 Éducation**|`NW6C2-QMPVW-D7KKK-3GKT6-VCFB2`|
|**Windows 10 / 11 Famille (Home)**|`TX9XD-98N7V-6WMQ6-BX7FG-H8Q99`|