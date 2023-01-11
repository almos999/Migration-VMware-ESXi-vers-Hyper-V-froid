
# Introduction

#### Nous devons migrer les machines virtuelles du serveur **VMware ESXi** vers le service de virtualisation **Hyper-V** de chez Microsoft  *(Windows Server 2022)*. Les logiciels utilisés seront :

**VMware vCenter Converter Standalone** *(pour récuperer les disques virutels)*
**Vmdk2Vhd** *(pour convertir les disques VMDK vers VHD)*.

Avant de débuter l'installation il faudra *"Microsoft .NET Framework 3.5"* d'installé pour faire fonctionner Vmdk2Vhd.

[Download Microsoft .NET Framework 3.5](https://www.microsoft.com/fr-fr/download/details.aspx?id=21)

# 1] Installation de *VCCS*

Pour installer *VCCS*, il faudra un compte VMware. VMware vCenter Converter Standalone fournit une solution facile à utiliser qui automatise le processus de copie de machines virtuelles VMware depuis des machines physiques (exécutant Windows et Linux) et d'autres formats de machines virtuelles.

[VMware vCenter Converter Standalone - VMware Customer Connect](https://customerconnect.vmware.com/en/downloads/details?downloadGroup=VCENTER_STANDALONE_630_GA&productId=1355&rPId=95099)

### Procédure d'installation :

<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062034199856558121/image.png">

Ici on clique sur "Next" pour poursuivre l'installation

<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062034506766368778/image.png">
<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062036746021384192/image.png">

Ici on accepte la licence et on clique sur "Next"

<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062036995582480525/image.png">

Ici on sélectionne le répertoire d'installation de *(VMware vCenter Converter Standalone)*

<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062037327922335825/image.png">

On choisis une installation local pour convertir sur cette machine 

<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062037626699399218/image.png">

On installe *VCCS*.


# 2] Copie du disque *VMware*

## A] Source System

Pour copier un disque VMware il faudra lancer le logiciel **VMware vCenter Converter Standalone**.

Il faudra cliqué en haut a droite sur *'Convert machine'*, séléctionné *'Powered off'* et dans l'onglet déroulant *'VMware Infrastructure virtual machine'*.

Après ça, il faudra rentrer les informations de connexion au serveur *VMware ESXi* et cliquer sur *'Next'*. Vous devrez peut-être ignorer l'alerte de certificat qui indique que votre certificat n'est pas valide car il n'est pas signé par une autorité de certification.

<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062276496892362752/image.png">

Ensuite, dans la section *'Source Machine'*, vous allez sélectionner la machine que vous voulez copier. Il est important de savoir que la machine doit être hors fonction. Si c'est le cas, le statut de la machine sera affiché dans la section *'Power state'* et sera indiqué comme étant *'Powered off'*.

Vous devrez cliquer sur *'Next'* quand votre machine sera séléctionné.

## B] Source Machine


<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062280296860491848/image.png">

## C] Destination System

Dans l'onglet *'Destination System'*, vous devrez choisir le chemin de destination où le disque de la machine virtuelle sera copié, le nom du dossier, ainsi que le produit VMware. Vous sélectionnerez alors **VMware Workstation 16.x**.

<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062283385235578910/image.png">

## D] Options

Dans les options, on aura un récapitulatif de base de la configuration de la machine virtuelle. Il est également possible de modifier les ressources utilisées par la machine virtuelle.

<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062285048730095667/image.png">

## E] Summary

Dans la section "Summary", on aura maintenant un récapitulatif complet de la machine virtuelle que nous voulons copier.

<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062286411585306635/image.png">

Enfin, nous pouvons cliquer sur le bouton "Finish" pour copier le disque. La copie n'est pas instantanée, il faudra attendre. Le temps sera affiché dans l'onglet *'End Time'*

# 3] Convertion du disque VMDK vers VHD

Pour convertir le disque il faudra le logiciel **[Vmdk2Vhd](https://www.softpedia.com/get/System/File-Management/Vmdk2Vhd.shtml)**

Une fois le logiciel installé, vous le lancez et vous devrez sélectionner le disque source (disque VMware) et la destination où votre disque Hyper-V converti sera enregistré. Après, cliquez sur *'Convert'* pour convertir le disque.

<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062290887390003261/image.png">


# 4] Utilisation du disque sur Hyper-V

Pour utiliser le disque sur Hyper-V, il faudra créer une machine virtuelle en ajoutant le disque déjà existant (le disque copié).

Pour créer une machine virtuelle sur Hyper-V, tout en haut à droite, vous devrez cliquer sur :

	- New
	- Virtual Machine...

<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062293892508164136/image.png">


<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062295172781719633/image.png">

Ici, vous donnerez un nom à votre machine virtuelle.

<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062295896781496380/image.png">

Si votre machine virtuelle disposait de l'UEFI sur VMware, utilisez la génération 2. Sinon, gardez la génération 1.

<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062296649885556766/image.png">

Vous allez devoir attribuer de la mémoire RAM à votre machine virtuelle. Vous pouvez lui donner la même configuration que celle que vous aviez sur VMware ESXi.

<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062297760046522429/image.png">

Vous allez maintenant sélectionner votre interface réseau.

<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062298365674672128/image.png">

Ensuite, vous sélectionnerez un disque dur virtuel existant (VHD) et vous lui donnerez le chemin de votre disque que vous avez converti. Après, vous pourrez exécuter la machine virtuelle et vérifier si tout fonctionne.

<img src="https://cdn.discordapp.com/attachments/1029113801003511859/1062301428951027802/image.png">
