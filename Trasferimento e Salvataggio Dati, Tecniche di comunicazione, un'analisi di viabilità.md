## Per implementare i tre principi fondamentali della cybersecurity, la nostra architettura sarà conforme ai seguenti principi:

### - *Principio di Minor Privilegio*
<p style="font-size: 15;">
Esisteranno diversi livelli di autenticazione, permettendo agli utenti di visualizzare/inserire/rimuovere solo file a cui gli è concesso. (ad esempio, gli amministratori dovrebbero essere in grado di rimuovere dati, i creatori possono fornire nuovi dati mentre i semplici utenti possono solo visualizzare).
</p>

### - *Principio di Separazione delle Responsabilità*
<p style="font-size: 15;">
La parola chiave qui è: <b>distribuzione</b>. L'architettura è fondamentalmente divisa in 3 strati: client, gateway e servizi. La responsabilità principale del client è di offrire un modo per gli utenti di visualizzare e interagire coi dati, il gateway si occuperà di dirigere i dati tra gli endpoints, infine ai servizi sono delegati tutte le azioni che operano direttamente sui dati; tra questi servizi includiamo un'istanza di <i>CassandraDB</i> come base di dati e un servizio di autenticazione implementato ad-hoc per supportare cifratura sullo standard militare.
</p>

### - *Principio di Fallimento in Sicurezza*
<p style="font-size: 15;">
Gli errori inaspettati sono una continua minaccia all'integrità, sicurezza e confidenzialità dei dati, indi per cui i meccanismi di mitigazione devono essere integrati nel design. Il miglior modo per prevenire distribuzione impropria di dati è introdurre l'idea di un "fallimento in sicurezza": qualora non fosse possibile dimostrare la catena di custodia dei dati, o se l'accesso dai servizi venisse ostacolato, il sistema non fornirà dati a nessuno degli endpoint, reindirizzando la navigazione ad uno stato di default (home page / sign-in page).
</p>

### - *Principio del Design Trasparente*
<p style="font-size: 15;">
Quando si parla di criptografia, la forza e sicurezza degli algoritmi derivano dal design trasparente, privi di "ricette segrete" o modi occulti di aggirarli. Intendiamo progettare il nostro sistema di cifratura usando strategie in linea con gli standard riconosciuti, tra cui: algoritmo di cifratura SHA256, credenziali "salted", autenticazione a 2 fattori di default, comunicazioni esclusivamente tramite HTTPS, database basato su blockchain, ridondanza degli errori e correzione degli errori di design.
</p>

### - *Principio di Minimizzazione della Superficie d'Attacco*
<p style="font-size: 15;">
Il principio fondamentale di una buona difesa è essere consapevoli dei punti di vulnerabilità e difenderle dagli attacchi; questo diventa estremamente più fattibile quando si minimizzano i punti di interazione: ad esempio, i database non possono essere interrogati manualmente, ma solo tramite autenticazione presente lato client, stesso concetto si applica anche col gateway. Inoltre, registrazioni di nuovi profili e livelli di accesso saranno gestiti lato server, allo scopo di evitare infiltrazioni, con la possibilità di implementare un ulteriore livello di sicurezza se necessario, ovvero garantire la cifratura tramite password dei file scaricati. 
</p>

---
## Architettura Proposta:
### - [CassandraDB](https://cassandra.apache.org/_/index.html) come Base di Dati
### - [SHA256](https://en.wikipedia.org/wiki/SHA-2) con Salt + Pepper + Hash per la cifratura
### - [t3](https://github.com/t3-oss/create-t3-app) per le tecnologie web e gateway
### - [JWT](https://jwt.io) + HTTPS per trasferimento dati sicuro e affidabile
