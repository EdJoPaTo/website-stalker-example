Cloud

Block Storage
für Cloud Server
==========

 Flexibles Hochskalieren bis 10TB

 Redundante Speicherung

 Niedrige Latenz und hohe I/O-Eignung

 Zusätzlicher Speicher für deine
Cloud-Projekte
----------

### Volumes bieten dir die Möglichkeit deine Cloud-Server mit SSD-basiertem Block Storage zu erweitern. ###

Volumes lassen sich jederzeit und unkompliziert auf bis zu 10 TB hochskalieren. Pro Cloud-Server sind bis zu 16 Volumes möglich. Jeder Datenblock wird auf drei verschiedenen physischen Servern gespeichert. Diese Redundanz sorgt für hohe Ausfall- und Datensicherheit.

[Jetzt loslegen](https://console.hetzner.com/)

 Flexible Erweiterung

Hochskalierbar auf bis zu 10 TB und 16 Volumes je Cloud-Server

 Einfache Einbindung

Automatische und manuelle Mounting-Optionen, volle Dateisystem‑Funktionen

 Sicher & schnell

Hochverfügbarer SSD-Speicher und redundante Speicherung

 Kosteneffizient

Günstige und stundenbasierte Preise

 Block Storage vs. Object Storage
----------

### Was ist der Unterschied zwischen Volumes und Object Storage? ###

Volumes (Block Storage) und Object Storage unterscheiden sich vor allem im Datenmodell und im Zugriff. Block Storage verhält sich wie eine lokal eingebundene Festplatte: Es wird an einen Cloud-Server gemountet, bietet sehr geringe Latenz und eignet sich für Workloads mit hohen I/O-Anforderungen wie Datenbanken. Object Storage hingegen speichert Daten als einzelne Objekte in S3-kompatiblen Buckets, erreichbar per HTTPS/API. Objekte werden nicht in-place verändert, sondern neu versioniert. Während Block Storage feste, erweiterbare Volumes nutzt, skaliert Object Storage praktisch unbegrenzt und ist ideal für Backups, Medien oder globale Distribution.

[Mehr über Object Storage erfahren](https://www.hetzner.com/storage/object-storage/)

Häufig gestellte Fragen
----------

* **Was sind Hetzner Cloud-Volumes und wofür eignen sie sich?**

   Hetzner Cloud-Volumes sind SSD-basierter, netzwerkgebundener Block Storage, den Sie flexibel an Ihre Cloud Server anhängen können, um deren Speicherplatz zu erweitern. Sie verhalten sich wie eine zusätzliche Festplatte und eignen sich besonders für datenintensive Anwendungen, Datenbanken oder Logs.

* **Welche Größen sind möglich und kann ich ein Volume später ändern?**

   Ein Volume kann zwischen 10 GB und 10 TB groß sein. Sie können die Größe jederzeit nach oben anpassen, ein Verkleinern ist jedoch nicht möglich; nach der Vergrößerung muss das Dateisystem im Betriebssystem manuell erweitert werden.

* **Wie sorgt Hetzner bei Volumes für Ausfallsicherheit meiner Daten?**

  Jeder Datenblock eines Volumes wird in den Hetzner Rechenzentren auf drei unterschiedlichen physischen Servern gespeichert (dreifache Replikation). Dadurch bleiben Ihre Daten auch dann verfügbar, wenn einzelne Hardware-Komponenten ausfallen.

* **Wie viele Volumes kann ich pro Cloud Server nutzen und kann ein Volume mehrere Server gleichzeitig bedienen?**

  Sie können bis zu 16 Volumes an einem einzelnen Hetzner Cloud Server nutzen. Ein Volume kann allerdings immer nur an genau einen Server gleichzeitig angehängt werden und ist nicht parallel von mehreren Servern beschreibbar.

* **In welchen Umgebungen kann ich Volumes verwenden?**

  Volumes sind speziell für die Hetzner Cloud konzipiert und lassen sich nur an Cloud Servern einsetzen. Eine direkte Nutzung an Dedicated Servern ist nicht möglich.

Block Storage: Die Perfekte Ergänzung
zu unseren Cloud Tarifen
----------

Shared: Cost Optimized

startet ab  max/mo.

[Produkt entdecken](https://www.hetzner.com/cloud/cost-optimized/)

Shared: Regular Performance

startet ab  max/mo.

[Produkt entdecken](https://www.hetzner.com/cloud/regular-performance/)

Dedicated: General Purpose

startet ab  max/mo.

[Produkt entdecken](https://www.hetzner.com/cloud/general-purpose/)
