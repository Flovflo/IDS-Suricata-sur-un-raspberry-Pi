# IDS-Suricata-sur-un-raspberry-Pi
Suricata est un système de détection d'intrusion (IDS) réseau (network-based) et un système de prévention d'intrusion (IPS) open source. Site: https://suricata.io/

**Pourquoi utilise des systèmes IDS / IPS**
Un réseau d'entreprise typique possède plusieurs points d'accès à d'autres réseaux, notamment des réseaux publics et des réseaux privés. L'enjeu est d'assurer la sécurité de ces réseaux tout en les gardant ouverts aux clients. Les attaques d'aujourd'hui sont si complexes qu'elles peuvent contourner les meilleurs systèmes de sécurité, en particulier ceux qui ne sont protégés que par un cryptage ou des pare-feu. Malheureusement, ces technologies ne peuvent à elles seules empêcher les attaques d'aujourd'hui.

**Qu’est ce que IDS/IPS**
IDS est un système de détection d'intrusion et IPS un système de prévention d’instruction
les deux comparent les paquets du réseau à une base de données contenant des signatures connues de cyberattaques 
La plus grosse différence entre les deux est que l’IPS est un système de contrôle alors que l’IDS est un système de surveillance.
soit IDS (Intrusion Detection Systems) : surveillent et analysent le trafic pour vérifier que les paquets ne sont pas vérolés selon une base de données connue . Ils comparent aussi l’activité réseau en cours avec une base de données et les scanners de port.
Pour IPS (Intrusion Prevention Systems) : il n’agit pas sur le réseaux mais entre le monde extérieur et le réseau interne 

**Quelle sont les différences entre HIDS et NIDS ?**  
  * HIDS host base
Un système de détection d'intrusion basé sur l'hôte ( HIDS ) est un système de détection d'intrusion capable de surveiller et d'analyser les éléments internes d'un système informatique ainsi que les paquets réseau sur ses interfaces réseau, de la même manière qu'un système de détection d'intrusion basé sur le réseau (NIDS) fonctionne  
Les systèmes de détection d'intrusion basés sur l'hôte aident à surveiller les processus et les applications s'exécutant sur des appareils tels que des serveurs et des postes de travail. Les technologies HIDS sont « passive », ce qui signifie que leur objectif est d'identifier les activités suspectes et non de les empêcher. Pour  obtenir une visibilité plus approfondie de la sécurité, les systèmes de détection d'intrusion basés sur l'hôte sont généralement déployés parallèlement aux systèmes de détection d'intrusion basés sur le réseau et aux solutions SIEM, qui regroupent et analysent les événements de sécurité provenant de plusieurs sources.  
Les avantages : Bien que les HID puissent sembler être une mauvaise solution, ils présentent au départ de nombreux avantages. Pour commencer, ils peuvent empêcher les attaques de faire des dégâts. Par exemple, si un fichier malveillant tente de réécrire un document, le HID lui coupera les droits et le mettra en quarantaine. Les systèmes de détection d'intrusion basés sur l'hôte peuvent protéger les ordinateurs portables et personnels chaque fois qu'ils sont retirés d'un réseau ou qu'ils se rendent sur le terrain. En bref, les HID constituent la dernière ligne de défense utilisée pour parer à certaines attaques qui sont manquées par les NID.

 * NIDS Network based  
Un système de détection d'intrusion basé sur le réseau (NIDS) utilise des capteurs NIDS pour surveiller et analyser les comportements suspects et les menaces réelles dans le trafic réseau. Il analyse le contenu et les informations d'en-tête de tous les paquets de données transmis sur le réseau.
Des capteurs NIDS sont placés à des points clés du réseau pour vérifier le trafic de tous les appareils du réseau. Par exemple, les capteurs NIDS sont installés sur le même sous-réseau que le pare-feu pour détecter le déni de service (DoS) et d'autres attaques de ce type.  
Les avantages : les NID sont excellentes et ont la capacité de protéger d'innombrables dispositifs informatiques. C'est la meilleure option, qui est plus simple à déployer et moins coûteuse. Les NID fournissent également une évaluation plus large d'un grand réseau d'entreprise par le biais de scans et de sondes. En outre, les administrateurs sont en mesure de protéger d'autres dispositifs tels que les serveurs d'impression, les pare-feu, les routeurs et les concentrateurs VPN. Les NID sont flexibles avec plusieurs systèmes d'exploitation et dispositifs et protègent le réseau des inondations de bande passante ainsi que des attaques DoS.

**Pourquoi utiliser suricat :**

**Raspberry Pi** : Le Raspberry Pi est un nano-ordinateur monocarte à processeur ARM qui fonctionne en 32 et 64 bits. Il fut créé pour pouvoir donner accès plus facilement aux ordinateurs. C’est très accessible dû au faible prix et aux logiciels libres. Le Raspberry Pi permet l’installation et l’exécution de plusieurs systèmes d’exploitation libre et compatible comme GNU, Linux et Debian. Il fonctionne également sur le système d’exploitation Windows 10.
Le Raspberry Pi est fourni nu. Donc il n’y a ni boîtier, ni câble d’alimentation, de clavier, de souris, d’écran, pour diminuer les coûts.

