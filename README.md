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

![alt text](https://github.com/Flovflo/IDS-Suricata-sur-un-raspberry-Pi/blob/main/Image/schema/Sans%20titre.png)

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
sudo apt install libpcre3 libpcre3-dbg libpcre3-dev build-essential libpcap-dev libyaml-0-2 libyaml-dev pkg-config zlib1g zlib1g-dev make libmagic-dev libjansson-dev rustc cargo python-yaml python3-yaml liblua5.1-dev
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

<h1> 3) Installation d'une interface graphique avec Fluent Bit </h1>

Maintenant que nous avons des alertes de journalisation Suricata, concentrons-nous sur la fin de la réception. Nous devons configurer le moteur Elasticsearch qui ingérera et indexera les alertes et Kibana qui sera utilisé pour visualiser les alertes, construire de beaux écrans de tableau de bord, etc.
Heureusement, il existe de très bonnes images Docker prêtes à l'emploi pour Elasticsearch et Kibana, utilisons-les pour économiser du temps et des efforts. Ces images sont conservées par Idriss Neumann et sont disponibles ici : https://gitlab.comwork.io/oss/elasticstack/elasticstack-arm

Installer Docker :
```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER
```

Déconnexion et reconnectez-vous au Raspberry. Ensuite, extrayez les images Docker que nous utiliserons et créez un réseau Docker pour laisser les deux conteneurs d'Elasticsearch et de Kibana parler ensemble :
```
docker pull comworkio/elasticsearch:latest-arm
docker pull comworkio/kibana:latest-arm
docker network create elastic
```





Source : https://www.reddit.com/r/raspberry_pi/comments/np1a8f/building_my_home_intrusion_detection_system/
       : https://jufajardini.wordpress.com/2021/02/15/suricata-on-your-raspberry-pi/
