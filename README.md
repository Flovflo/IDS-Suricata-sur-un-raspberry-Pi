# IDS-Suricata-sur-un-raspberry-Pi
<h1>1) Prerequis </h1>
Suricata est un système de détection d'intrusion (IDS) réseau (network-based) et un système de prévention d'intrusion (IPS) open source. Site: https://suricata.io/

**Pourquoi utilise des systèmes IDS / IPS**
Un réseau d'entreprise typique possède plusieurs points d'accès à d'autres réseaux, notamment des réseaux publics et des réseaux privés. L'enjeu est d'assurer la sécurité de ces réseaux tout en les gardant ouverts aux clients. Les attaques d'aujourd'hui sont si complexes qu'elles peuvent contourner les meilleurs systèmes de sécurité, en particulier ceux qui ne sont protégés que par un cryptage ou des pare-feu. Malheureusement, ces technologies ne peuvent à elles seules empêcher les attaques d'aujourd'hui.

**Qu’est ce que IDS/IPS**
IDS est un système de détection d'intrusion et IPS un système de prévention d’instruction
les deux comparent les paquets du réseau à une base de données contenant des signatures connues de cyberattaques 
La plus grosse différence entre les deux est que l’IPS est un système de contrôle alors que l’IDS est un système de surveillance.
soit IDS (Intrusion Detection Systems) : surveillent et analysent le trafic pour vérifier que les paquets ne sont pas vérolés selon une base de données connue . Ils comparent aussi l’activité réseau en cours avec une base de données et les scanners de port.
Pour IPS (Intrusion Prevention Systems) : il n’agit pas sur le réseaux mais entre le monde extérieur et le réseau interne 
ll y en a deux type soit HIDS (basé sur l'hôte) ou NIDS (base sur le réseaux ).


**Quelle sont les différences entre HIDS et NIDS ?**  
  * HIDS - Host Based:
Soit HIDS est un système de détection d'intrusion basé sur l'hôte , il est capable de surveiller et d'analyser les éléments internes d'un système informatique ainsi que les paquets réseau sur ses interfaces réseau, comme un système de détection d'intrusion basé sur le réseau (NIDS) fonctionne
Les systèmes de détection d'intrusion basés sur l'hôte aident à surveiller les processus et les applications s'exécutant sur des appareils tels que des serveurs et des postes de travail. Les technologies HIDS sont « passive », ce qui signifie que leur objectif est d'identifier les activités suspectes et non de les empêcher. Pour  obtenir une visibilité plus approfondie de la sécurité, les systèmes de détection d'intrusion basés sur l'hôte sont généralement déployés parallèlement aux systèmes de détection d'intrusion basés sur le réseau et aux solutions SIEM, qui regroupent et analysent les événements de sécurité provenant de plusieurs sources. 
Les avantages : Bien que les HID puissent sembler être une mauvaise solution, ils présentent au départ de nombreux avantages. Pour commencer, ils peuvent empêcher les attaques de faire des dégâts. Par exemple, si un fichier malveillant tente de réécrire un document, le HID lui coupera les droits et le mettra en quarantaine. Les systèmes de détection d'intrusion basés sur l'hôte peuvent protéger les ordinateurs portables et personnels chaque fois qu'ils sont retirés d'un réseau ou qu'ils se rendent sur le terrain. En bref, les HID constituent la dernière ligne de défense utilisée pour parer à certaines attaques qui sont manquées par les NID.
![alt text](https://github.com/Flovflo/IDS-Suricata-sur-un-raspberry-Pi/blob/main/Image/schema/HIDS.png)

 * NIDS - Network Based:
Un système de détection d'intrusion basé sur le réseau (NIDS) utilise des capteurs NIDS pour surveiller et analyser les comportements suspects et les menaces réelles dans le trafic réseau. Il analyse le contenu et les informations d'en-tête de tous les paquets de données transmis sur le réseau.
Des capteurs NIDS sont placés à des points clés du réseau pour vérifier le trafic de tous les appareils du réseau. Par exemple, les capteurs NIDS sont installés sur le même sous-réseau que le pare-feu pour détecter le déni de service (DoS) et d'autres attaques de ce type.
les avantages: Les NID sont excellentes et ont la capacité de protéger d'innombrables dispositifs informatiques. C'est la meilleure option, qui est plus simple à déployer et moins coûteuse. Les NID fournissent également une évaluation plus large d'un grand réseau d'entreprise par le biais de scans et de sondes. En outre, les administrateurs sont en mesure de protéger d'autres dispositifs tels que les serveurs d'impression, les pare-feu, les routeurs et les concentrateurs VPN. Les NID sont flexibles avec plusieurs systèmes d'exploitation et dispositifs et protègent le réseau des inondations de bande passante ainsi que des attaques DoS.
![alt text](https://github.com/Flovflo/IDS-Suricata-sur-un-raspberry-Pi/blob/main/Image/schema/NIDS.png)



**Qu'est-ce qu'un IPS ?**  

Un IPS (Système de Prévention des Intrusions) est une sécurité pour repérer et réprimer les menaces déterminés.
Les IPS inspectent et surveillent constamment notre réseau, analysent des comportements douteux malveillants et prennent en compte des informations à leur sujet.
L’ IPS avertit ces incidents à l’administrateur système et prend des mesures défensives, comme l'arrêt du point d’accès et la reconfiguration du pare-feu pour détourner de futures attaques.
Les solutions IPS peuvent en outre être utilisées pour déterminer les différents problèmes liés aux politiques de sécurité de l’entreprise pour empêcher les employés et les visiteurs de franchir les règles incluses dans les politiques.  

**Quelle est la différence entre un IDS et un IPS ?**  
Examinons donc la différence entre IPS et IDS, la principale différence entre IPS et IDS réside dans l'action entreprise lorsqu'un problème potentiel est détecté.
Les systèmes de prévention des intrusions contrôlent l'accès au réseau informatique et l'immunise des abus et des attaques. Ces systèmes sont créés pour observer les données intrusives et prendre des mesures pour empêcher les attaques de se produire.
Les systèmes de détection d'intrusion ne sont pas conçus pour empêcher les attaques. Ils surveillent simplement le réseau et envoient des alertes à l'administrateur lorsqu'une menace potentielle est détectée.


**Pourquoi utiliser suricata :**  
Premièrement Suricata est open source donc gratuit, il gère aussi la détection d'intrusion (IDS), la prévention d'intrusion (IPS) mais surtout il est très rapide et performant
De plus il est assez simple à mettre en œuvre
Et il peut s'installer sur énormément d'appareils / d'écosystèmes
même si Suricata a des concurrents comme Zeek , Sweet Security ou Snort mais Suricata est gratuit et à une énorme communauté active donc les nouvelles informations sur les menaces sont souvent disponibles en premier dans un format compatible avec Suricata , de même si vous avez un problème il y a de fortes chances que quelqu'un d'autre a déjà eu ces problèmes et qu'il a donné la solution sur un forum sur internet.
C'est donc pour cela que nous choisissions Suricata. 


**Schéma d'installation**
![alt text](https://github.com/Flovflo/IDS-Suricata-sur-un-raspberry-Pi/blob/main/Image/schema/Sans%20titre.png)

**Raspberry Pi** : Le Raspberry Pi est un nano-ordinateur monocarte à processeur ARM qui fonctionne en 32 et 64 bits. Il fut créé pour pouvoir donner accès plus facilement aux ordinateurs. C’est très accessible dû au faible prix et aux logiciels libres. Le Raspberry Pi permet l’installation et l’exécution de plusieurs systèmes d’exploitation libre et compatible comme GNU, Linux et Debian. Il fonctionne également sur le système d’exploitation Windows 10.
Le Raspberry Pi est fourni nu. Donc il n’y a ni boîtier, ni câble d’alimentation, de clavier, de souris, d’écran, pour diminuer les coûts.

<h1>2) Mise en Pratique  </h1>
  <h2> 1) Installation de Raspbian Lite </h2>

Pour commencer, nous installons un OS sur le raspberry pi.
Nous choisissons donc raspbian car c'est la distribution la plus adaptée pour raspberry pi, et nous prenons la version light car nous n'avons pas besoin d'interface graphique et aussi pour éviter de consommer de l'énergie et des ressources.

Je télécharge l'instaleur raspbian sur le site de la fondation [Raspberrry](https://raspberry-pi.fr/telechargements/) .  

Ensuite après que l’ISO est téléchargé , je l'installe sur une micro SD avec [balenaEtcher](https://www.balena.io/etcher/) .

Ensuite j insère la carte SD dans le raspberry pi et je démarre le raspberry pi , je boot bien sûr raspbian lite donc nous sommes prêts à passer à l'étape 2.

   <h2> 2) Installation de Suricata </h2>
