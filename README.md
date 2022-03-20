# IDS-Suricata-sur-un-raspberry-Pi
<h1>1) Prerequis </h1>
Suricata est un système de détection d'intrusion (IDS) réseau (network-based) et un système de prévention d'intrusion (IPS) open source. Site: https://suricata.io/

**Pourquoi utilise des systèmes IDS / IPS**
Un réseau d'entreprise typique possède plusieurs points d'accès à d'autres réseaux, notamment des réseaux publics et des réseaux privés. L'enjeu est d'assurer la sécurité de ces réseaux tout en les gardant ouverts aux clients. Les attaques d'aujourd'hui sont si complexes qu'elles peuvent contourner les meilleurs systèmes de sécurité, en particulier ceux qui ne sont protégés que par un cryptage ou des pare-feu. Malheureusement, ces technologies ne peuvent à elles seules empêcher les attaques d'aujourd'hui.  

**Qu’est ce que IDS/IPS**
IDS est un système de détection d'intrusion et IPS un système de prévention d’instruction.
Les deux comparent les paquets du réseau à une base de données contenant des signatures connues de cyberattaques.
La plus grosse différence entre les deux est que l’IPS est un système de contrôle alors que l’IDS est un système de surveillance.
Sois IDS (Intrusion Detection Systems) : surveille et analyse le trafic pour vérifier que les paquets ne sont pas vérolés selon une base de données connue. Ils comparent aussi l’activité réseau en cours avec une base de données et les scanners de port.
Pour IPS (Intrusion Prevention Systems) : il n’agit pas sur le réseau, mais entre le monde extérieur et le réseau interne.
ll y en a deux type, soit HIDS (basé sur l'hôte) ou NIDS (base sur le réseau ).

**Quelle sont les différences entre HIDS et NIDS ?**
 * HIDS - Host Based:
Soit HIDS est un système de détection d'intrusion basé sur l'hôte , il est capable de surveiller et d'analyser les éléments internes d'un système informatique ainsi que les paquets réseau sur ses interfaces réseau, comme un système de détection d'intrusion basé sur le réseau (NIDS) fonctionne
Les systèmes de détection d'intrusion basés sur l'hôte aident à surveiller les processus et les applications s'exécutant sur des appareils tels que des serveurs et des postes de travail. Les technologies HIDS sont « passive », ce qui signifie que leur objectif est d'identifier les activités suspectes et non de les empêcher. Pour obtenir une visibilité plus approfondie de la sécurité, les systèmes de détection d'intrusion basés sur l'hôte sont généralement déployés parallèlement aux systèmes de détection d'intrusion basés sur le réseau et aux solutions SIEM, qui regroupent et analysent les événements de sécurité provenant de plusieurs sources.
Les avantages : bien que les HID puissent sembler être une mauvaise solution, ils présentent au départ de nombreux avantages. Pour commencer, ils peuvent empêcher les attaques de faire des dégâts. Par exemple, si un fichier malveillant tente de réécrire un document, le HID lui coupera les droits et le mettra en quarantaine. Les systèmes de détection d'intrusion basés sur l'hôte peuvent protéger les ordinateurs portables et personnels chaque fois qu'ils sont retirée d'un réseau ou qu'ils se rendent sur le terrain. En bref, les HID constituent la dernière ligne de défense utilisée pour parer à certaines attaques qui sont manquées par les NID.
![alt text](https://github.com/Flovflo/IDS-Suricata-sur-un-raspberry-Pi/blob/main/Image/schema/HIDS.png)

 * NIDS - Network Based:
Un système de détection d'intrusion basé sur le réseau (NIDS) utilise des capteurs NIDS pour surveiller et analyser les comportements suspects et les menaces réelles dans le trafic réseau. Il analyse le contenu et les informations d'en-tête de tous les paquets de données transmis sur le réseau.
Des capteurs NIDS sont placés à des points clés du réseau pour vérifier le trafic de tous les appareils du réseau. Par exemple, les capteurs NIDS sont installés sur le même sous-réseau que le pare-feu pour détecter le déni de service (DoS) et d'autres attaques de ce type.
les avantages : Les NID sont excellentes et ont la capacité de protéger d'innombrables dispositifs informatiques. C'est la meilleure option, qui est plus simple à déployer et moins coûteuse. Les NID fournissent également une évaluation plus large d'un grand réseau d'entreprise par le biais de scans et de sondes. En outre, les administrateurs sont en mesure de protéger d'autres dispositifs tels que les serveurs d'impression, les pare-feu, les routeurs et les concentrateurs VPN. Les NID sont flexibles avec plusieurs systèmes d'exploitation et dispositifs et protègent le réseau des inondations de bande passante ainsi que des attaques DoS.
![alt text](https://github.com/Flovflo/IDS-Suricata-sur-un-raspberry-Pi/blob/main/Image/schema/NIDS.png)


**Qu'est-ce qu'un IPS ?**

Un IPS (Système de Prévention des Intrusions) est une sécurité pour repérer et réprimer les menaces déterminées.
Les IPS inspectent et surveillent constamment notre réseau, analysent des comportements douteux malveillants et prennent en compte des informations à leur sujet.
L’ IPS avertit ces incidents à l’administrateur système et prend des mesures défensives, comme l'arrêt du point d’accès et la reconfiguration du pare-feu pour détourner de futures attaques.
Les solutions IPS peuvent en outre être utilisées pour déterminer les différents problèmes liés aux politiques de sécurité de l’entreprise pour empêcher les employés et les visiteurs de franchir les règles incluses dans les politiques.

**Quelle est la différence entre un IDS et un IPS ?**  
Examinons donc la différence entre IPS et IDS, la grande différence entre IPS et IDS réside dans l'action prise quand une potentielle menace est détecté. L’IPS (systèmes de prévention des intrusions) comme ils contrôlent l'accès au réseau informatique et peuvent, rejette des abus et des attaques. Ces systèmes sont créés pour observer les données intrusives et prendre des mesures pour empêcher les attaques de se produire. Au contraire, les IDS (systèmes de détection d'intrusion) ne sont pas conçus pour empêcher les attaques. Ils ne font que surveiller le réseau et envoient des alertes lorsqu'une menace potentielle est détectée, et donc IDS requière un Humain ou un autre système pour prendre la décision de filtre ou pas.


**Pourquoi utiliser suricata :**

Premièrement, Suricate est open source donc gratuit, il gère aussi la détection d'intrusion (IDS), la prévention d'intrusion (IPS) mais surtout, il est très rapide et performant.
De plus, il est assez simple à mettre en œuvre.
Et il peut s'installer sur énormément d'appareils / d'écosystèmes.
Même si Suricata a des concurrents comme Zeek , Sweet Security ou Snort, mais Suricata est gratuit et à une énorme communauté active donc les nouvelles informations sur les menaces sont souvent disponibles en premier dans un format compatible avec Suricata , de même si vous avez un problème il y a de fortes chances que quelqu'un d'autre a déjà eu ces problèmes et qu'il a donné la solution sur un forum sur Internet.
C'est donc pour cela que nous choisissions Suricata. 


**Schéma d'installation**
![image](https://user-images.githubusercontent.com/86321847/148235773-baf631ee-091e-428a-863b-576a7d5eedfc.png)

Utilisation d’un commutateur ou d’un switch avec port mirroring pour que tout le trafic puissent être vu par notre raspberry pu avec Suricata 
Pour nous avec du cisco il faut :
Pour dupliser tout les packet du port fastEthernet 0/1
```
monitor session 1 source interface fa 0/1 both
```

ET pour le renvoyer sur l’interace fastEthernet 0/2 
```
monitor session 1 destination interface fa0/2
```

**Raspberry Pi** : Le Raspberry Pi est un nano-ordinateur monocarte à processeur ARM qui fonctionne en 32 et 64 bits. Il fut créé pour pouvoir donner accès plus facilement aux ordinateurs. C’est très accessible dû au faible prix et aux logiciels libres. Le Raspberry Pi permet l’installation et l’exécution de plusieurs systèmes d’exploitation libre et compatible comme GNU, Linux et Debian. Il fonctionne également sur le système d’exploitation Windows 10.
Le Raspberry Pi est fourni nu. Donc il n’y a ni boîtier, ni câble d’alimentation, de clavier, de souris, d’écran, pour diminuer les coûts.

<h1>2) Mise en Pratique  </h1>
  <h2> 1) Installation de Raspbian Lite </h2>
    <h3> 1) Raspbian Lite </h3>
Pour commencer, nous installons un OS sur le raspberry pi.
Nous choisissons donc raspbian car c'est la distribution la plus adaptée pour raspberry pi, et nous prenons la version light car nous n'avons pas besoin d'interface graphique et aussi pour éviter de consommer de l'énergie et des ressources.

Je télécharge l'instaleur raspbian sur le site de la fondation [Raspberrry](https://raspberry-pi.fr/telechargements/) .  

Ensuite après que l’ISO est téléchargé , je l'installe sur une micro SD avec [balenaEtcher](https://www.balena.io/etcher/) .

Mais d'abord avant d'insérer la carte SD dans le raspberry pi, je vais créer un fichier et ssh dans le dossier boot de la carte SD pour que le SSH soit activé (pour ne pas devoir brancher un écran et un clavier au raspberry pi et devoir l'activer manuellement)
<p align="center">
  <img src="https://user-images.githubusercontent.com/86321847/140617622-02c0eb09-5f9c-4476-8520-bd8eac2ce010.png" />
</p>


Je peux donc maintenant mettre la carte SD dans le raspberry pi , attendre quelques minutes qu'il démarre et aller sur l'interface d'administration de ma box pour trouver l'adresse IP assignée au raspberry pi.
<p align="center">
  <img src="https://user-images.githubusercontent.com/86321847/140617918-2419c910-c0e5-431e-a432-4f471c839fa0.png" />
</p>


Le IP privé de mon raspberry pi et donc 192.168.0.23 soite mje peux maintenant lancer une connexion ssh depuis mon ordinateur pour contrôler le raspberry pi.
<p align="center">
  <img src="https://user-images.githubusercontent.com/86321847/140617727-0470b759-7dba-4932-9914-9f724b6f6e59.png" />
</p>

   <h3> 2) Accès à distance </h3>
Pour pouvoir accéder au raspberry pi depuis l'IUT et pour la configuration et par la suite la maintenance et la supervision, il est donc important de pouvoir avoir un accès au raspberry pi, mais de manière sécurisée, c'est pour cela que nous avons fait un vpn WIREGUARD pour avoir de très bonnes performances tout en restant très sécurisé.  
Nous sommes prêts à passer à l'étape 2.


   <h2> 2) Installation de Suricata </h2>
   
   On commence donc à préparer l'installation , en installant les dépendances nécessaires :
```
sudo apt install libpcre3 libpcre3-dbg libpcre3-dev build-essential libpcap-dev libyaml-0-2 libyaml-dev pkg-config zlib1g zlib1g-dev make libmagic-dev libjansson-dev rustc cargo python3-yaml liblua5.1-dev
```

Télécharger les sources de Suricata :
```
wget https://www.openinfosecfoundation.org/download/suricata-6.0.1.tar.gz
```

Décompresser les sources :
```
tar -xvf suricata-6.0.1.tar.gz
```

Se placer dans le dossier Suricata :

```
cd $HOME/pi/suricata-6.0.1/
```
Configurer l’installation du logiciel :
```
./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var --enable-nfqueue --enable-lua
```

Pour la ompiler suricata :
```
make
```

ensuite installer suricata :
```
sudo make install
```

<img width="801" alt="image" src="https://user-images.githubusercontent.com/86321847/140886787-93c54373-070c-4da6-b744-4f122303aab6.png">

Se placer dans le dossier suricata-update :
```
cd $HOME/pi/suricata-6.0.1/suricata-update/
```

Compiler suricata-update :
```
sudo python setup.py build
```

Installer suricata-update :
```
sudo python setup.py install
```
Se placer dans le dossier Suricata :
```
cd ..
```

Finaliser l’installation de suricata en y incluant ses règles :
```
sudo make install-full
```
Mettre à jour les règles de suricata :
```
sudo suricata-update
```
<img width="773" alt="image" src="https://user-images.githubusercontent.com/86321847/140889091-68077d2a-27ea-404d-8730-af53e026805f.png">

<h3> Configurer Suricata </h3>
 Configurer suricata en éditant le fichier suricata.yaml :  
 

```
sudo nano /etc/suricata/suricata.yaml
```

Modifier la variable HOME_NET afin qu’elle contienne votre réseau local, par exemple :
 
 <img width="773" alt="image" src="https://user-images.githubusercontent.com/86321847/140889530-09e0470e-b145-4850-b17b-295de73dbb45.png">


<h3> Maintenant lancer Suricata </h3>

Lancer suricata avec la commande suivante :
```
sudo suricata -c /etc/suricata/suricata.yaml -i eth0 -S /var/lib/suricata/rules/suricata.rules
```
Soit avec :  

 * ```-c /etc/suricata/suricata.yaml``` : fichier de configuration à utiliser

 * ```-i eth0``` : interface Ethernet à surveiller

 * ```-S /var/lib/suricata/rules/suricata.rules ```: fichier contenant les règles à utiliser

Maintenant que suricata est bien installé , on peut tester Suricata
<h3> Teste Suricata </h3>
Pour vérifier le bon fonctionnement de Suricata , j’ajoute  une règle qui affiche un avertissement à chaque réception d’un ICMP Echo (ping).

lancer suricata.rules :
```
nano /var/lib/suricata/rules/suricata.rules
```
pour ajouter la regle suivant  : 
```
alert icmp any any -> any any (msg: "ICMP Packet found"; sid: 1; rev: 1;)
``` 

<img width="773" alt="image" src="https://user-images.githubusercontent.com/86321847/140893000-00264fdb-29d4-40d2-8fcc-c92baeebf808.png">

<h1> 3)Suricata en mode service </h1>
Pour pouvoir utiliser suricata en tant que service Suricata en tant que service, il faut créer ce fichier   

```
nano /etc/systemd/system/suricata.service
```
   
```
# Exemple de fichier d'unité systemd de Suricata.
[Unit]
Description=Suricata Intrusion Detection Service
After=network.target syslog.target
[Service]
ExecStart=/usr/bin/suricata -c /etc/suricata/suricata.yaml -i eth0 -S /var/lib/suricata/rules/suricata.rules
ExecReload=/bin/kill -HUP $MAINPID
ExecStop=/bin/kill $MAINPID
[Install]
WantedBy=multi-user.target
```

soit pour activer notre nouveau service suricata on utilise la commande commande :   
```
systemctl enable suricata.service
```   

Maintenant suricata peut etre utiliser en tant que service :   
```
systemctl start suricata.service
```


Pour le stopper :  

```
systemctl stop suricata.service
```

Pour le relancer :
```
systemctl restart suricata.service
```

Pour vérifier l’état du service :
```
systemctl status suricata.service
```




Maintenant le service se démarre automatiquement au démarrage du raspberry pi
on verifie que le service est bien lancer.
![image](https://user-images.githubusercontent.com/86321847/144584735-4173c3f0-2fc9-4bec-adc1-551f65f289b0.png)

Le service se lancera maintenant automatiquement au démarrage du Raspberry Pi.
<h1> 4) Les Regles Suricata  </h1>
Il faut à la fois éviter les faux positifs et s'assurer que les règles utilisées sont à jour et permettent la détection de menaces récentes.
Les règles activées par défaut de Suricata génèrent de nombreux faux positifs (alertes qui ne sont pas de vrais problèmes). 
Par exemple, si vous utilisez Dropbox ou Skype sur votre réseau, vous devrez désactiver les règles correspondantes afin de ne pas générer d'alertes inutiles pour votre réseau.
Pour plus de sécurité de votre installation, vous pouvez ajouter de nouvelles sources de règles ou créer vos propres règles. Il est donc bon de savoir que chaque règle Suricata suit le modèle suivant :
action l’en-tête options
L'action correspond à l'action effectuée en cas de détection (alerte, abandon, passage...).

L'en-tête permet de définir le protocole (tcp, http, ftp, dns, tls...) ainsi que l'adresse IP et le port de source et de destination du trafic concerné par l'alerte.

Les options de la règle sont indiquées entre parenthèses et séparées par des virgules. Certaines options ont des paramètres, qui sont spécifiés par leur mot clé, suivi de deux points et de la valeur du paramètre.
Les règles sont identifiées par leur identifiant de signature, le paramètre sid.

Par exemple:
drop tcp $HOME_NET any -> $EXTERNAL_NET any (msg:”ET TROJAN Likely Bot Nick in IRC (USA +..)”; flow:established,to_server; flowbits:isset,is_proto_irc; content:”NICK “; pcre:”/NICK .*USA.*[0-9]{3,}/i”; reference:url,doc.emergingthreats.net/2008124; classtype:trojan-activity; sid:2008124; rev:2;)

L’action 
-	alerte - générer une alerte
-	pass - arrête l'inspection ultérieure du paquet
-	drop - supprime le paquet et génère une alerte (drop pour ici)
-	rejet - envoie l'erreur d'accès RST/ICMP à l'expéditeur du paquet correspondant.
-	rejettesrc - identique à simplement rejeter
-	rejettedst - envoie le paquet d'erreur RST/ICMP au récepteur du paquet correspondant.
-	Rejectboth - envoyer des paquets d'erreur RST/ICMP aux deux côtés de la conversation.
Dans l’en-tête,on peut y choisir :
Le Protocol (tcp)
Ce mot-clé dans une signature indique à Suricata de quel protocole il s'agit. Vous pouvez choisir entre quatre protocoles de base :
-	TCP (pour le trafic TCP)
-	UDP
-	ICMP
-	ip (ip signifie 'all' ou 'any')
ou bien même des protocoles de couche application
-	http
-	ftp
-	DNS
Etc

La Source and destination ( $HOME_NET  $EXTERNAL_NET)
Avec source et destination, vous spécifiez respectivement la source du trafic et la destination du trafic. Vous pouvez attribuer des adresses IP (IPv4 et IPv6 sont pris en charge) et des plages IP. Ceux-ci peuvent être combinés avec des opérateurs :

OPERATEUR	DESCRIPTION
../..	IP ranges (CIDR notation)
!	exception/negation
[.., ..]	regroupement

Normalement, vous utiliserez également des variables, telles que $HOME_NETet $EXTERNAL_NET. Le fichier de configuration spécifie les adresses IP concernées et ces paramètres seront utilisés à la place des variables dans vos règles. Voir Rule-vars pour plus d'informations.
Par exemple :

EXEMPLE	SIGNIFICATION
! 1.1.1.1	Toutes les adresses IP sauf 1.1.1.1
![1.1.1.1, 1.1.1.2]	Toutes les adresses IP sauf 1.1.1.1 et 1.1.1.2


Le Ports (source and destination) (any)
Le trafic entre et sort par les ports. Différents ports ont des numéros de port différents. Par exemple, le port par défaut pour HTTP est 80 alors que 443 est généralement le port pour HTTPS. 

Les ports mentionnés ci-dessus sont généralement les ports de destination. Les ports sources, c'est-à-dire l'application qui a envoyé le paquet, se voient généralement attribuer un port aléatoire par le système d'exploitation. 

Lors de la configuration des ports, vous pouvez également utiliser des opérateurs spéciaux, comme décrit ci-dessus. Des signes comme :

OPERATEUR	DESCRIPTION
:	port ranges
!	exception/negation
[.., ..]	regroupement

La direction (->)

La direction indique de quelle manière la signature doit correspondre. Presque chaque signature a une flèche vers la droite( ->). Cela signifie que seuls les paquets avec la même direction peuvent correspondre. Cependant, il est également possible qu'une règle corresponde dans les deux sens ( <>) :

source -> destination
source <> destination (les deux directions)






<h1> 5) Exploiter les fichiers de logs  </h1>
Il enregistre le trafic réseau détecté et des activités suspectes, Suricata enregistre également des informations de service et des statistiques de trafic réseau. D’ailleurs, il faut faire attention, car ces logs prennent vite de la place, ils peuvent facilement remplir la carte sd sur raspberry pi et aussi un carte sd ne sont pas conçues pour des lectures, écritures intensives et elles peuvent échouer après un certain temps. Donc pour une raison de fiabilité et avoir un système de stockage et de sauvegarde performant, nous n’allons pas utiliser une carte sd. 

Suricata enregistre 4 type de log  :

* ``` suricata.log ``` : messages de démarrage de Suricata
* ``` stats.log ``` : statistiques sur le trafic réseau
* ``` fast.log ``` : activités suspectes 
* ``` eve.json ``` : trafic de votre réseau local ainsi que les activités suspectes au format JSON

<h2> Gestion des fichiers de logs sur NAS </h2>
Nous choisissions le nas pour une raison de fiabilité êtres sur de ne pas perdre les logs, mais vous pouvez très bien utiliser un disque dur externe branché en USB
N’ayant pas de NAS à disposition, j’utilise une vm  [https://xpenology.club/](xpenology) pour simuler un nas synology
pour ce faire nous allons monter un système de fichiers distant sur le Pi à l'aide d'iSCSI.
creer une cible iscsi sur le NAS synology.  

<h3> Proxmox </h3>

N'ayant pas de NAS à la maison, mais un serveur, j'avais d'abord pensé et fait une VM avec XPEinology qui simulait donc un nas synology dans Virtual box mais cela consommer énormément de ressources pour un résultat très peu concluant et très instable.
Nous avons donc choisi la solution de l'hyperviseur de type 1
Ce qui permet d'avoir une bien meilleure émulation, pouvoir le utilisation à distance et aussi surtout pour une question de sécurité il est très simple de faire des sauvegardes d'avoir des serveurs de réplication
Nous avons donc choisi proxmox , mais proxmox, c’est quoi ?
Proxmox (Proxmox Virtual Environment) est une solution de virtualisation basée sur Linux KVM (Debian 64 bits) qui permet la création de machines virtuelles de type OpenVZ et KVM. Il s'agit d'une solution de type bare metal (bare metal en français), au sens de tourner directement sur la machine, c'est-à-dire sans OS. Le nom signifie un hyperviseur de type 1 (également appelé natif), où un hyperviseur minimaliste simplifié et optimisé se comporte comme un moniteur qui démarre le matériel, se connecte à un réseau et démarre une machine virtuelle. Le serveur ESX de VMware, le LPAR d'IBM ou Hyper-V de Microsoft sont des hyperviseurs de type 1. Proxmox est géré via une interface web (```https://serverur_proxmox:8006```) et fournit une vue d'ensemble de toutes les VM installées. En plus de cette interface web, des scripts peuvent être créés pour automatiser certaines tâches et il est totalement gratuit.
Donc je pars prendre ma clé téléchargée l'iso sur le site officiel et commencer à booster mon serveur sur la clé usb, je suis bien l'installation ensuite l'installation finie mon serveur démarre sur proxmox , il m'invite à aller sur l'interface web ```https://192.3168.0.45:8006```,
Je m'y rends et on me demande mon nom et mot de passe je me log donc en root

  ![image](https://user-images.githubusercontent.com/86321847/158821188-b33338ee-4227-47de-9a5e-ebc70801cb68.png)
     
  D'ailleurs pour des soucis d'énergie comme c'était un ordinateur portable l'écran reste en permanence allumé et si je rappelle capot l'ordinateur se met en veille donc pour contrer ce problème voici la commande : ```systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target```
  
Je configure simplement et je me lance dans l'installation de la VM
Je commence part téléchargé et uplaod les fichiers de conf
https://drive.google.com/drive/folders/120qSow3L5XTYqhO3AkgngmBEXv3x0LTj
Puis je crée ma vm et je poursuis l’installation après que tout soit fini, je peux avoir accès a l’interface graphique. 

![image](https://user-images.githubusercontent.com/86321847/158827338-aa4b0e74-9b9e-46d3-8ec0-7e47c77e0bd3.png)



![image](https://user-images.githubusercontent.com/86321847/158824975-f93c3385-5d10-4615-83b7-d60b217ee090.png)

je prends en main le interface et installe le service iscsi

![image](https://user-images.githubusercontent.com/86321847/158825152-c6913383-5793-46cb-b6e5-7c8596e82945.png)

![image](https://user-images.githubusercontent.com/86321847/147881337-43603476-cd1c-4e88-baa9-830fbf963b92.png)
![image](https://user-images.githubusercontent.com/86321847/158569547-5ac09389-37a3-40c6-8e7d-74a579aa016d.png)
![image](https://user-images.githubusercontent.com/86321847/158569898-35474000-b43e-490f-a82a-86fc142ff304.png)
 



  

ensuite j'install et demarre le service iscsi sur le raspberry
```
apt install open-iscsi
systemctl start open-iscsi
```
![image](https://user-images.githubusercontent.com/86321847/158570629-0f2119db-9a8e-4793-8044-2c2412210425.png)

Laissez le système "découvrir" la cible iSCSI sur le NAS, notez/copiez le dans de la cible et attachez-la à votre système :   
```
sudo iscsiadm --mode discovery --type sendtargets --portal 192.168.0.33
sudo iscsiadm --mode node --targetname <fqdn of the target as returned by the command above> --portal 192.168.0.33 --login
```

À ce stade, j'exécute ``` fidsk -l ```  
![image](https://user-images.githubusercontent.com/86321847/158571795-fe47663b-7bcf-4523-916a-cbcd962ff694.png)

pour identifiez le périphérique qui a été attribué à la cible iSCSI, dans mon cas, c'était ``` /dev/sda ``` . 
Puis je formatez le périphérique via la commande : ```  mkfs.ext4 /dev/sda ``` . je peux maintenant le monter ou je veux (j'ai choisi /mnt/nas-iscsi) :
``` mount /dev/sda /mnt/nas-iscsi/ ```

<img width="612" alt="image" src="https://user-images.githubusercontent.com/86321847/158605907-ff078e5d-07fa-441a-a35b-614d46250ed0.png">


pour que le disque soit automatiquement monté au démarrage :  ``` blkid /dev/sda "l'UUID de votre périphérique" ```

Epusi j'edite le fichier de configuration de la cible iSCSI situé dans ``` /etc/iscsi/node/<fqdn>/<nom court>/default ``` et modifiez-le apr ``` node.startup = automatic ```
<img width="983" alt="image" src="https://user-images.githubusercontent.com/86321847/158608301-861e2986-b88c-4756-aa3e-1b24ea7b6a40.png">

Ajoutez à ``` /etc/fstab ``` :
``` UUID=<UUID de votre périphérique> /mnt/nas-iscsi ext4 defaults,_netdev 0 0 ```
<img width="864" alt="image" src="https://user-images.githubusercontent.com/86321847/158610562-08770a65-095e-4c65-9ac8-696c6f779f68.png">

je vais sur l'interface de mon nas et je vois que le lecteur est bien connecter a mon raspberry et qu'il est fonctionnel 
![image](https://user-images.githubusercontent.com/86321847/158826896-ef4890f1-b4b3-4a90-b972-16aac85bfaf3.png)


Créez un répertoire pour les logs de Suricata ``` mkdir /mnt/nas-iscsi/suricata_logs ```
j'arrêtez le service Suricata et j'editez son fichier de configuration 
``` nano /etc/suricata/suricata.yml ``` et indiquez le répertoire de logs par défaut :
``` default-log-dir : /mnt/nas-iscsi/suricata_logs/ ``` .
<img width="864" alt="image" src="https://user-images.githubusercontent.com/86321847/158643373-9b9b37d8-880e-4e76-b22d-1481e95aaae4.png">


Redémarrez Suricata ``` systemctl start suricata.service ``` et vérifiez que les fichiers journaux de Suricata sont créés dans le nouvel emplacement.
Voila mon fichier mes log sont maintenant stoke sur mon serveur NAS 



<h1> 6) Installation d'une interface graphique  </h1>
<h2> Installation ELK </h2>


Maintenant que nous avons des alertes de journalisation Suricata, concentrons-nous sur l'extrémité destinataire. Nous devons configurer le moteur Elasticsearch qui ingérera et indexera les alertes et Kibana qui sera utilisé pour visualiser les alertes, construire de beaux écrans de tableau de bord, etc.

Nous allons donc utiliser ELK 
Mais qu’est ce que ELK , ELK est un acronyme upour décrire une pile qui comprend trois projets open source:
-	 Elasticsearch
-	 Logstash 
-	 Kibana
     
     
     
C’est la principal source de gestion des logs pour les entreprises qui souhaitent bénéficier des avantages d'une solution de journalisation centralisée.
En effet, les outils : Elasticsearch, Logstash et Kibana, lorsqu'ils sont utilisés ensemble car vous pouvez aussi les utiliser séparément et avec d’autre outils mais ils forment une pile de bout en bout qui offre une analyse de données dont des logs en temps réel afin de fournir des informations exploitables à partir de presque tout type de source de données structurée et non structurée. 
On verra plus tard que chaque élément joue un rôle important. Ils peuvent être utilisés pour des projets simples ou complexe car ils prennent en charge des opérations avance et simple.
Il est important de dissocier le rôle de ces 3 outils afin de mieux comprendre le rôle et la communication de l'ensemble de ces composants :
-	__Elasticsearch__ : prend en charge de l'indexation et du stockage de vos informations sur une base de données NoSQL qui est basé sur le moteur de recherche Apache Lucene et il est construit pour fournir des APIS rest. 
Il est facile simple et fiable. Il propose également des requêtes avancées pour effectuer une analyse détaillée et stocke toutes les données de manière centralisée. Il est également utilisé sur de nombreux projets hors la suite ELK car il permet d'exécuter une recherche rapide des documents.
-	__Logstash__ : l’outil d'intégration de données open source qui permet de collecter des données à partir d'une variété de sources, de les filtrer, les transformer et de les envoyer à la destination souhaitée (ex: Elasticsearch). Son but est de rassembler et conformer des données provenant de différentes sources et de les rendre disponibles pour une utilisation ultérieure.
-	__Kibana__ : outil de visualisation de données qui complète la pile ELK , c'est une couche de visualisation qui fonctionne au-dessus d'Elasticsearch, CA donne a l’utilisateurs la possibilité d'analyser et de visualiser les données récupérées Elasticsearch. C'est un outil puissant offrant pour vos tableaux de bord divers diagrammes interactifs, données géographiques et graphiques pour visualiser les données les plus complexes. Donne un tableau de bord très complet pour visualiser rapidement des données qui peuvent être complexes
   
   

   
Cela correspond parfaitement a notre projet et il est aussi énormément utilisé en entreprise comme : 
- NetFlix s'appuie fortement sur la pile ELK. L'entreprise utilise la pile ELK pour surveiller et analyser les logs de sécurité des opérations du service client. Il leur permet d'indexer, de stocker et de rechercher des documents à partir de plus de quinze clusters qui comprennent près de 800 nœuds.
- Ou linkedIn utilise la pile ELK pour surveiller leurs performances et leur sécurité. L'équipe informatique a intégré ELK à Kafka pour comprendre leur charge en temps réel. Leur opération ELK comprend plus de 100 clusters dans six datacenters différents.



Heureusement, il existe de très bonnes images Docker prêtes à l'emploi pour Elasticsearch et Kibana, utilisons-les pour économiser du temps et des efforts. Ces images sont conservées par Idriss Neumann et sont disponibles ici : https://gitlab.comwork.io/oss/elasticstack/elasticstack-arm

Installer Docker :
```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER
```
<h3> Doker ?  </h3> 
Nous allons donc utiliser de docker donc un petit point sur qu'est-ce que le docker
   
Avec la technologie Docker, vous pouvez traiter les conteneurs comme des machines virtuelles très légères et modulaires. En outre, ces conteneurs vous offrent une grande flexibilité : vous pouvez les créer, déployer, copier et déplacer d'un environnement à un autre.
   
__Comment ça fonctionne__

La technologie Docker utilise le noyau Linux et des fonctions de ce noyau, telles que les groupes de contrôle cgroups et les espaces de noms, pour séparer les processus afin qu'ils puissent s'exécuter de façon indépendante. Ce qui est l'objectif des conteneurs : exécuter plusieurs processus et applications séparément les uns des autres afin d'optimiser l'utilisation de votre infrastructure tout en bénéficiant du même niveau de sécurité que celui des systèmes distincts.
   
Les outils de conteneurs, y compris Docker, sont associés à un modèle de déploiement basé sur une image (container). Il est ainsi plus simple de partager une application ou un ensemble de services, avec toutes leurs dépendances, entre plusieurs environnements.
   
Docker offre donc pas mal d’avantage modularité, sécurité, simplicité et rapidité.
mais fessons un petit point sur les commande a connaître lorsque vous utilisez Docker.    

```docker ps (-a)``` : cela vous montre  toutes les instances de docker en cours d'exécution dans votre environnement. Si vous ajoutez l'option -a, vous verrez même des conteneurs arrêtés.  

```docker images (-a)```: la commande montre les images que vous avez construites, et le -a vous montre les images intermédiaires.

```docker network ls ``` : La commande docker network ls liste les différents réseaux 
      
Déconnexion et reconnectez-vous au Raspberry. Ensuite, extrayez les images Docker que nous utiliserons et créez un réseau Docker pour laisser les deux conteneurs d'Elasticsearch et de Kibana parler ensemble :
```
docker pull comworkio/elasticsearch:latest-arm
docker pull comworkio/kibana:latest-arm
docker network create elastic
```

Nous voulons également stocker les journaux et les données d'Elasticsearch et de Kibana sur la cible iSCSI du NAS. Pour ce faire, créez les répertoires :
```
mkdir /mnt/nas-iscsi/es01_logs
mkdir /mnt/nas-iscsi/es01_data
mkdir /mnt/nas-iscsi/kib01_logs
mkdir /mnt/nas-iscsi/kib01_data
```

On lance les conteneur , nommés ES01 et KIB01, et mappez les répertoires hôtes créés ci-dessus :
```
docker run --name es01 --net elastic -p 9200:9200 -p 9300:9300 -v /mnt/nas-iscsi/es01_data:/usr/share/elasticsearch/data -v /mnt/nas-iscsi/es01_logs:/usr/share/elasticsearch/logs -e "discovery.type=single-node" comworkio/elasticsearch:latest-arm &
docker run --name kib01 --net elastic -p 5601:5601 -v /mnt/nas-iscsi/kib01_data:/usr/share/kibana/data -v /mnt/nas-iscsi/kib01_logs:/var/log -e "ELASTICSEARCH_HOSTS=http://es01:9200" -e “ES_HOST=es01” comworkio/kibana:latest-arm &
```

Important :
Il y a un petit bug dans l'image Kibana et que l'adresse IP du serveur Elasticsearch n'est pas correctement configurée.   
Pour corriger cela, entrez dans le conteneur (```docker exec -it kib01 bash```) et modifiez le fichier ```nano /usr/share/kibana/config/kibana.yml```. Sur la dernière ligne, il y a une adresse IP de serveur qui est codée en dur, remplacez-la par es01. Changez également la destination de journalisation par défaut et enregistrez le fichier, cela devrait ressembler à :

<img width="570" alt="image" src="https://user-images.githubusercontent.com/86321847/158650443-7298528d-f61e-4f56-b587-cdf5e4acaff1.png">



Redémarrez le conteneur Kibana :
```docker stop kib01; docker start kib01```
Bravo, maintenant le moteur Kibana devrait fonctionner correctement et être connecté au serveur Elasticsearch. Essayez-le en parcourant l'adresse http://<IP de votre >Raspberry>:5601 pour moi http://192.168.0.33:5601.

  
  <h1> 7) Installation Fluent Bit </h1>
Fluent Bit comblera le fossé entre les producteurs de grumes (Suricata) et les consommateurs de grumes (ElasticSearch et Kibana). Entre les deux, Fluent Bit va enrichir les logs avec la géolocalisation des adresses IP pour pouvoir visualiser la source ou la destination des paquets ayant déclenché l'alerte sur une carte du monde.

On a opté pour Fluent Bit car il est le plus léger en termes d'utilisation de la mémoire (-200/300 Mo par rapport à Logstash basé sur Java), un peu plus convivial pour le processeur, et a également utilisé une base de données GeoLiteCity2 plus précise et à jour que dans ma précédente itération basée sur Logstash de l'ancienne base de données GeoLiteCity.
Pour commencer, nous devons ajouter un nouveau dépôt APT pour en extraire le paquet :
  ```
 curl https://packages.fluentbit.io/fluentbit.key | sudo apt-key add - 
  ```
  
Editez le fichier /etc/apt/sources.listet ajoutez la ligne suivante :
  ```
 deb https://packages.fluentbit.io/raspbian/buster buster main 
  ```
  <img width="696" alt="image" src="https://user-images.githubusercontent.com/86321847/157396854-5d650827-4b35-4d82-8502-49f1bc188e07.png">

Exécutez ensuite les commandes suivantes :
  ```
 apt-get update 
 apt-get install td-agent-bit 
  ```
  
À ce stade, td-agent-bit  est installé et doit encore être configuré.
On configure le fichier /etc/td-agent-bit/td-agent-bit.conf (nano /etc/td-agent-bit/td-agent-bit.conf) avec cette configuration (adaptez l'IP du réseau interne à votre propre réseau - encore une fois dans mon cas, c'est 192.168.0.X et changez l'IP externe pour permettre aux alertes qui sont purement internes au LAN d'être géolocalisées sans erreur) :

  ```
  [SERVICE]
    Flush           5
    Daemon          off
    Log_Level       error
    Parsers_File    parsers.conf


[INPUT]
    Name tail
    Tag  eve_json
    Path /mnt/nas_iscsi/suricata_logs/eve.json
    Parser myjson
    Db /mnt/nas_iscsi/fluentbit_logs/sincedb

[FILTER]
    Name  modify
    Match *
    Condition Key_Value_Does_Not_Match src_ip 192.168.0.*
    Copy src_ip ip

[FILTER]
    Name modify
    Match *
    Condition Key_Value_Does_Not_Match dest_ip 192.168.0.*
    Copy dest_ip ip

[FILTER]
    Name modify
    Match *
    Condition Key_Value_Matches dest_ip 192.168.0.*
    Condition Key_Value_Matches src_ip 192.168.0.*
    Add ip <ENTER YOUR PUBLIC IP HERE OR A FIXED IP FROM YOUR ISP>

[FILTER]
    Name  geoip2
    Database /usr/share/GeoIP/GeoLite2-City.mmdb
    Match *
    Lookup_key ip
    Record lon ip %{location.longitude}
    Record lat ip %{location.latitude}
    Record country_name ip %{country.names.en}
    Record city_name ip %{city.names.en}
    Record region_code ip %{postal.code}
    Record timezone ip %{location.time_zone}
    Record country_code3 ip %{country.iso_code}
    Record region_name ip %{subdivisions.0.iso_code}
    Record latitude ip %{location.latitude}
    Record longitude ip %{location.longitude}
    Record continent_code ip %{continent.code}
    Record country_code2 ip %{country.iso_code}

[FILTER]
    Name nest
    Match *
    Operation nest
    Wildcard country
    Wildcard lon
    Wildcard lat
    Nest_under location


[FILTER]
    Name nest
    Match *
    Operation nest
    Wildcard country_name
    Wildcard city_name
    Wildcard region_code
    Wildcard timezone
    Wildcard country_code3
    Wildcard region_name
    Wildcard ip
    Wildcard latitude
    Wildcard longitude
    Wildcard continent_code
    Wildcard country_code2
    Wildcard location
    Nest_under geoip

[OUTPUT]
    Name  es
    Match *
    Host  127.0.0.1
    Port  9200
    Index logstash
    Logstash_Format on
   ```
  <img width="899" alt="image" src="https://user-images.githubusercontent.com/86321847/157398513-17e40212-af76-43f7-8a46-5c05badfafa7.png">

Créez le fichier db utilisé pour enregistrer la position du décalage dans le fichier source :
  ```
mkdir -p /mnt/nas_iscsi/fluentbit_logs/
touch /mnt/nas_iscsi/fluentbit_logs/sincedb
  ```
Créer un compte sur https://dev.maxmind.com/geoip/geolocate-an-ip/databases et télécharger la base de données GoeLiteCity2, pour la mettre dans /usr/share/GeoIP/GeoLite2-City.mmdb
Créez un fichier de configuration de l'analyseur : ```nano /etc/td-agent-bit/parsers.conf```
  ```
[PARSER]
    Nom monjson
    Format json
    Time_Key timestamp
    Time_Format %Y-%m-%dT%H:%M:%S.%L%z
  ```
Tout est terminé , je peux démarrer le deamon Fluent Bit  ``` service td-agent-bit start ```

Ok, maintenant tout devrait fonctionner à ce stade. Connectez-vous à Kibana à l'adresse http://192.168.0.23:5601 et utilisez la fonction Discover pour afficher votre index Logstash et toutes les données poussées de Logstash vers Elasticsearch.

Maintenant pour avoir de beau visuel 

j'utilse des templates de https://github.com/StamusNetworks/KTS7
et avec ce template cela donne acces a 28 tableaux de bord pour Kibana 7.x et Elasticsearch 7.x à utiliser avec le système Suricata IDS/IPS/NSM - Détection des intrusions, prévention des intrusions et surveillance de la sécurité du réseau
  
  pour l'installer 
  
```
CD API-KIBANA7 curl -X POST "192.168.0.23:5601/api/saved_objects/_import" -H 'kbn-xsrf: true' --form file=@index-pattern.ndjson curl -X POST "192.168.0.23:5601/api/saved_objects/_import" -H 'kbn-xsrf: true' --form file=@search.ndjson curl -X POST "192.168.0.23:5601/api/saved_objects/_import" -H 'kbn-xsrf: true' --form file=@visualization.ndjson curl -X POST "192.168.0.23:5601/api/saved_objects/_import" -H 'kbn-xsrf: true' --form file=@dashboard.ndjson curl -X POST "localhost:5601/api/saved_objects/_import" -H 'kbn-xsrf: true' --form file=@query.ndjson service de redémarrage de kibana
```
  et
```
  CD API-KIBANA7 curl -X POST "192.168.0.23:5601/api/saved_objects/_import? overwrite=true" -H 'kbn-xsrf: true' --form file=@index-pattern.ndjson curl -X POST "192.168.0.23:5601/api/saved_objects/_import? overwrite=true" -H 'kbn-xsrf: true' --form file=@search.ndjson curl -X POST "192.168.0.23:5601/api/saved_objects/_import? overwrite=true" -H 'kbn-xsrf: true' --form file=@visualization.ndjson curl -X POST "192.168.0.23:5601/api/saved_objects/_import? overwrite=true" -H 'kbn-xsrf: true' --form file=@dashboard.ndjson curl -X POST "192.168.0.23:5601/api/saved_objects/_import? overwrite=true" -H 'kbn-xsrf: true' --form file=@query.ndjson service de redémarrage de kibana
```

et voila notre système est opérationnel 

<img width="884" alt="Capture d’écran 2022-03-20 à 14 51 55" src="https://user-images.githubusercontent.com/86321847/159166477-e3ebad77-9aff-49c6-a494-41287542461a.png">



Source : https://www.reddit.com/r/raspberry_pi/comments/np1a8f/building_my_home_intrusion_detection_system/  
       : https://jufajardini.wordpress.com/2021/02/15/suricata-on-your-raspberry-pi/  
       : https://www.framboise314.fr/detection-dintrusion-ids-avec-suricata-sur-raspberry-pi/  
