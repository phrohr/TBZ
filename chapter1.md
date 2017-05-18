# VLAN \(**Virtual Local Area Network\)**

# VLAN-Einführung

Ein VLAN ist ein _**logisches Teilnetz **\(siehe _[_Die Unterschiede zwischen physischer und logischer Netzwerk-Adressierung_](/die-unterschiede-zwischen-physischer-und-logischer-netzwerk-adressierung.md)\) innerhalb eines physischen Netzwerks. Es kann sich über einen oder mehrere Switches hinweg ausdehnen. Ein VLAN _**trennt physische Netze in Teilnetze**_ auf, indem es dafür sorgt, dass VLAN-fähige Switches die Datenpakete eines VLAN’s nicht in ein anderes VLAN weiterleiten, obwohl die Teilnetze an gemeinsamen Switches angeschlossen sein können.

Jedes VLAN bildet \(wie ein normales, physisch separiertes Netzwerksegment\) eine eigene Broadcast-Domäne. Um den Verkehr zwischen den VLANs transparent zu vermitteln, benötigt man einen _**Router**_. Moderne Switches stellen diese Funktion intern zur Verfügung. Man spricht dann von einem _**Layer-3-Switch**_.

_Man kann sich das VLAN in einem Kabel oder einer Glasfaser so vorstellen, dass innerhalb eines Kupferdrahtes **mehrere virtuelle Kupferdrähte** angeordnet sind und im Innern des Switches jeder Kupferdraht separat geswitcht wird. Jeder Port des Switches hat somit unterschiedliche VLANs aufgeschaltet. Aus diesem Grund darf **niemals ein Kabel** von einem Port am VLAN-Switch, **ohne Rekonfiguration** der Ports am Switch, **umgesteckt** werden. Sonst kann es geschehen, dass die VLANs an die falschen Geräte und Switches weitergeleitet werden und die Dienste nicht dort zur Verfügung stehen, wo sie sollten. Daraus lässt sich ableiten, dass Switches mit VLANs entsprechend vor Fremdzugriff geschützt werden müssen. Zusätzlich erleichtert eine entsprechende Bechriftung und Dokumentation der Ports die Administration des Netzwerks.  
_

Wie schon angedeutet, muss der Switch VLAN’s unterstützen. Aber auch die Netzwerkkarte im Server/PC kann VLAN-fähig und somit über verschiedene VLAN’s erreichbar sein.

# 2.2 Warum VLAN?

Lokale Netze werden mit auf OSI-Ebene 2 arbeitenden Switches aufgebaut, deren Anschlüsse kollisionsfrei und im Duplexmode sehr perfomant arbeiten. Dadurch ist es möglich, grosse LAN’s mit mehreren hundert PC’s aufzubauen. Eine Unterteilung solcher Netze in virtuelle Netze hat folgende Vorteile:

* _**Flexibilität**_
   bei der Zuordnung von Endgeräten zu Netzwerksegmenten, unabhängig vom Standort der Basisstation.
* _**Priorisierung**_
   von bestimmtem Datenverkehr wie z.B. VoIP. Verkleinerung der Broadcast- Domänen.
* Mehr Dienste im Netz \(IP-Telefonie, IP-TV, IP-Radio\) etc.\) ziehen auch eine grössere Komplexität nach sich. Diese 
  _**Komplexität**_
   kann man reduzieren, indem man konsequent für jeden Dienst ein eigenes VLAN im Netz bezeichnet.
* Die  
  _**Abhörsicherheit**_  
   ist bei VLAN’s besser als bei geswitchten Netzen, wo verschiedene Angriffsszenarios wie MAC-Flooding / MAC-Spoofing existieren. Zur Verbindung von VLAN’s kommen Router zum Einsatz, die gegen Layer-2-Attacken unempfindlich sind. Zusätzlich bietet Routing die Möglichkeit, Firewalls auf Layer-3-Basis einzusetzen. Diesen Vorteil könnten auch segmentierte LAN’s bieten. Dabei ist man aber im Gegensatz zu VLAN’s von der physischen Verkabelung abhängig

  Vorsicht bei dynamischen VLAN’s: Diese lassen sich analog zu Switches ebenfalls kompromittieren.

# 2.3 Zuordnung von Datenverkehr zu VLAN’s

Die Zuordnung der Teilnetze zu einem VLAN kann…

* statisch über Portzuordnung an den Switches erfolgen
* über spezielle Markierungen an den Paketen \(Tags\) realisiert sein
* oder dynamisch erfolgen, zum Beispiel durch MAC-Adressen, IP-Adressen bis hin zu TCP- und UDP-Ports und höheren Protokollen.

Jedes VLAN bildet \(wie ein normales, physisch separiertes Netzwerksegment\) eine eigene Broadcast-Domäne. Um den Verkehr zwischen den VLAN’s transparent zu vermitteln, benötigt man einen Router. Moderne Switches stellen diese Funktion intern zur Verfügung. Man spricht dann von einem Layer-3-Switch. Die Überlegenheit von VLAN’s im Vergleich zur physischen Zuordnung zu verschiedenen Subnetzen basiert darauf, dass ein Wechsel von einem VLAN in ein anderes am Kopplungselement \(Multilayerswitch, Router\) geschehen kann, ohne dass eine physische Verbindung geändert werden muss.

# 2.4 Verbindung von VLAN-Switches

Wenn sich ein VLAN über mehrere Switches erstreckt, ist zu deren Verbindung entweder für jedes VLAN ein eigener Link \(Kabel\) erforderlich, oder es kommen sogenannte VLAN-Trunks \(VLT\) zum Einsatz. Das Verfahren entspricht einem asynchronen Multiplexing. Deshalb dient ein VLT dazu, Daten der unterschiedlichen VLAN’s über eine einzige Verbindung weiterzuleiten. Hierzu können sowohl einzelne Ports als auch gebündelte Ports \(siehe Link Aggregation\) zum Einsatz kommen.

Beispiel eines einfachen VLAN-Netzwerks:

![](/assets/import.png)

# 2.5 VLAN-Typen

Ältere VLAN-fähige Switches beherrschen nur portbasiertes VLAN, das statisch konfiguriert werden muss. Später entwickelten sich dynamische VLANs und proprietäre tagged VLANs. Schließlich entstanden aus den proprietären tagged VLAN’s die heute dominierenden standardisierten Tagged VLANs nach IEEE 802.1q.

* _**Portbasierte VLAN’s:**_

  Urform der VLAN’s. Hier wird ein managebarer Switch portweise in mehrere logische Switches segmentiert – alternativ können sich portbasierte VLAN’s auch über mehrere Switches hinweg ausdehnen. Ein Port gehört dann immer nur zu einem VLAN oder ist ein Trunk-Port. Um die so segmentierten Netze bei Bedarf zu verbinden, kommt z. B. ein Router zum Einsatz. Ferner gehören sie zu den statischen VLAN-Konfigurationen und bilden sozusagen einen Gegenpol zu den dynamischen VLAN’s und zu den tagged VLAN’s. Überall dort, wo eine bessere Übersicht gefordert ist und ein höherer Ressourcenverbrauch \(Platz, Energie\) vermieden werden muss, kommen statische, portbasierte VLAN’s zum Einsatz.

* _**Tagged VLAN’s:**_

  Das heute fast ausschliesslich verwendete Ethernet-Datenblockformat Ethernet-II nach IEEE 802.3 mit 802.1Q VLAN-Tag:

  ![](http://www.teklounge.ch/wp-content/uploads/vlantutorial/VLAN.jpg)

  Die  
  _**paketbasierten tagged VLAN’s**_  
   stehen im Unterschied zu den älteren markierungslosen,  
  _**portbasierten VLAN’s**_  
  .  
  _Der Ausdruck tagged leitet sich vom englischen Ausdruck «Material Tags» ab \(Anhänger, mit denen Waren markiert werden\)._  
  Es handelt sich also bei tagged VLAN’s um Netzwerke, die Netzwerkpakete verwenden, welche eine  
  _**zusätzliche VLAN-Markierung**_  
   tragen.Ein  
  _**Tagging**_  
   in VLANs kommt auch dann zum Einsatz, wenn sich VLAN’s z. B.  
  _**über mehrere Switches**_  
   hinweg erstrecken, etwa über  
  _**Trunkports**_  
  . Hier tragen die Frames eine Markierung, welche die Zugehörigkeit zum jeweiligen VLAN anzeigt.Durch die Tags werden VLAN-spezifische Informationen zum Frame hinzugefügt. Zu dieser Gattung gehören die VLANs nach  
  _**IEEE 802.1q**_  
  . Damit die VLAN-Technik nach 802.1q auch für  
  _**ältere Rechner**_  
   und Systeme in einem Netz transparent bleibt, müssen Switches diese  
  _**Tags**_  
   bei Bedarf  
  _**hinzufügen**_  
   und auch wieder  
  _**entfernen**_  
   können.

  _Bei portbasierten VLAN’s \(d. h. bei Paketen, die kein Tag besitzen\) wird zum Weiterleiten eines Datenpakets über einen Trunk hinweg üblicherweise vor dem Einspeisen in den Trunk ein VLAN-Tag hinzugefügt, welches kennzeichnet, zu welchem VLAN das Paket gehört. Der Switch auf Empfängerseite muss dieses wieder entfernen. Bei Tagged VLAN’s nach IEEE 802.1q hingegen werden die Pakete entweder vom Endgerät \(z. B. Taggingfähigem Server\) oder vom Switch am Einspeiseport mit dem Tag versehen. Daher kann ein Switch ein Paket ohne jegliche Änderung in einen Trunk einspeisen. Empfängt ein Switch auf einem VLT-Port \(Trunkport\) einen Frame mit VLAN-Tag nach IEEE 802.1q, kann auch dieser es unverändert weiterleiten. Lediglich der Switch am Empfangsport muss unterscheiden, ob er ein Tagging-fähiges Endgerät beliefert \(dann muss das Frame unverändert bleiben\) oder ob es sich um ein nicht Tagging-fähiges Endgerät handelt, welches zu dem aktuellen VLAN gehört \(dann ist das Tag zu entfernen\). Hierzu muss die zugehörige VLAN-ID im Switch hinterlegt sein._  
  _ _  
   Da nach IEEE 802.1Q alle Pakete mit VLAN-Tags markiert sind, müssen einem Trunk entweder alle  
  _**VLAN-ID’s**_  
  , die er weiterleiten soll, hinterlegt werden, oder er ist zur Weiterleitung aller VLAN’s konfiguriert. Werden Pakete ohne Tag auf einem Trunk-Port empfangen, können diese je nach Konfiguration entweder einem  
  _**Default-VLAN**_  
   zugeordnet werden \(der Switch bringt das Tag nachträglich an\), oder sie werden verworfen. Empfängt ein Switch auf einem seiner Ports z. B. von einem älteren Endgerät Pakete ohne VLAN-Tags \(auch native Frames genannt\), so muss er selbst für das Anbringen des Tags sorgen. Hierzu wird dem betreffenden Port entweder per Default oder per Management eine VLAN-ID zugeordnet. Der Switch, der das Paket ausliefert, muss analog verfahren, wenn das Zielsystem nicht mit Tags umgehen kann \(das Tag muss entfernt werden\). Das automatische Lernen der zu den VLT’s \(Trunkports\) gehörenden Einstellungen ist heute Standard bei den meisten VLAN-fähigen Switches. Dabei muss ein Switch mit einem Mischbetrieb sowohl von Paketen, die keine Tags kennen und enthalten, als auch von Paketen, die bereits Tags besitzen, umgehen können. Das Erlernen der VLT’s erfolgt analog zum Erlernen der MAC-Adressen: Empfängt der Switch ein Paket mit VLAN-ID, so ordnet er den Port zunächst diesem VLAN zu. Empfängt er an einem Port innerhalb kurzer Zeit Pakete mit unterschiedlichen VLAN-IDs, so wird dieser Port als VLT identifiziert und als Trunk genutzt. Einfache Switches ohne Verwaltungsmöglichkeit bilden üblicherweise ein zusätzliches natives VLAN für alle Pakete, die keine Tags enthalten. Solche Pakete werden meist belassen wie sie sind. Ein Trunkport wird hier wie ein normaler \(Uplink-\)Port behandelt. Alternativ kann auch ein Default-Tag angefügt werden. Der Begriff Trunk wird im Unterschied zu VLT häufig auch mit einer ganz anderen Bedeutung verwendet, siehe auch Bündelung \(Datenübertragung\). Generell sollte man Sicherheit aber nicht mehr zu den Tagged-VLAN-Features zählen. Switches lassen sich auf zahlreichen Wegen kompromittieren, müssen folglich immer als  
  _**unsicher**_  
   eingestuft werden. Man kann aber auch direkt bei der Verkabelung ansetzen. Es gibt beispielsweise Messklemmen als Zubehör zu Profi-Netzwerkanalysegeräten, die äusserlich direkt an ein Kabel angeschlossen werden und das geringe elektromagnetische Feld messen. So kann völlig unbemerkt der gesamte über dieses Kabel laufende Datenverkehr mitgelesen und aufgezeichnet werden. Dagegen hilft nur eine  
  _**starke Verschlüsselung**_  
   \(z.B. mit IPsec\), die manche LAN-Karten direkt in Hardware implementieren.

* _**Statische VLAN’s**_  
  :

  Hier wird einem Switch-Port  
  _**fest eine VLAN-Konfiguration**_  
   zugeordnet. Er gehört dann zu einem portbasierten VLAN, zu einem untagged VLAN oder er ist ein Port, der zu mehreren VLANs gehört. Die Konfiguration eines Ports ist bei statischen VLAN’s fest durch den Administrator vorgegeben. Sie hängt nicht vom Inhalt der Pakete ab und steht im Gegensatz zu den dynamischen VLAN’s unveränderlich fest. Damit ist eine Kommunikation des Endgerätes an einem Port nur noch mit den zugeordneten VLAN’s möglich. Gehört ein Port zu mehreren VLAN’s, ist er ein VLAN-Trunk und dient dann meist zur Ausdehnung der VLAN’s über mehrere Switches hinweg.Durch die Möglichkeit, einen Port mehreren VLAN’s zuzuordnen, können zum Beispiel auch Router und Server über einen einzelnen Anschluss an mehrere VLAN’s angebunden werden, ohne dass für jedes Teilnetz eine physische Netzwerkschnittstelle vorhanden sein muss. Somit kann ein einzelnes Gerät – auch ohne Router – seine Dienste in mehreren VLANs anbieten, ohne dass die Stationen der verschiedenen VLAN’s miteinander kommunizieren können. Diese VLAN-Trunk’s dürfen nicht mit den Trunk’s im Sinne von Link Aggregation verwechselt werden, bei denen mehrere physische Übertragungswege zur Durchsatzsteigerung gebündelt werden.

* _**Dynamische VLAN’s**_  
  :

  Bei der dynamischen Implementierung eines VLAN’s wird die Zugehörigkeit eines Frames zu einem VLAN anhand bestimmter Inhalte des Frames getroffen. Da sich alle Inhalte von Frames praktisch beliebig manipulieren lassen, sollte in  
  _**sicherheitsrelevanten Einsatzbereichen**_  
   auf den  
  _**Einsatz von dynamischen VLAN’s verzichtet**_  
   werden. Dynamische VLAN’s stehen im Gegensatz zu den statischen VLAN’s. Die Zugehörigkeit kann beispielsweise auf der Basis der MAC- oder IP-Adressen geschehen, auf Basis der Protokoll-Typen oder auch auf Anwendungsebene nach den TCP-/UDP-Portnummern.In der Wirkung entspricht dies einer automatisierten Zuordnung eines Switchports zu einem VLAN. Durch Dynamische VLAN’s kann zum Beispiel auch erreicht werden, dass ein mobiles Endgerät immer einem bestimmten VLAN angehört – unabhängig von der Netzwerkdose, an die es angeschlossen wird. Eine andere Möglichkeit besteht darin, einen bestimmten Teil des Datenverkehrs in ein spezielles VLAN zu leiten.



