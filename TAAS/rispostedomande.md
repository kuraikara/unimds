# Cloud Computing

Definizione: Fornitura di risorse computazionali, software, di accesso ai dati e di memorizzazione distribuite in rete che non richiedono all’utente finale una conoscenza della locazione fisica dell’hardware utilizzato e della configurazione del sistema che fornisce i servizi

-Nato grazie allo sviluppo delle reti e dei browser sempre più potenti

## aspetti:

- infinita potenza comutazionale
- no investimenti iniziali
- pay per use
- possibile scalare velocemente
- software per la gestione con contabilità
- hardware più grossi, consumi di energia in base all’uso

## Data center enormi su 3 dimensioni:

- modelli di servizio
- modelli di deploy
- caratteristiche essenziali(monitoraggio e orchestrazione del mio servizio)

### Modelli di servizio

- Infrastructure as a Service:
- Platform
- Software
- Data
- Hardware
- Container
- Function

Ci sono anche degli overlap

### Modelli di deploy

- Private cloud
- Community
- Hybrid
- Public

### Caratteristiche essenziali

- Network access: Risorse in rete accessibili ovunque e con qualsiasi dispositivo
- Misurazioni: risorse continuamente controllate e ottimizzate
- self service: utente può richiedere risorse senza interazione umana
- Pooling di risorse: risorse in pool che servono più utenti e vengono assegnate in modo dinamico al bisogno, utente non ha controllo
- elasticità: La capacità di calcolo, memorizzazione, … può essere aumentata o diminuita velocemente in base alle esigenze

## Architettura

- frontend: come gli utenti accedono al servizio
- backend: il data center con le risorse e le app cloud

## Problemi

- disponibilità
- migrazione
- privacy
- rallentamenti sul trasferimento
- pagamenti licenze

## Applicazioni

- accesso da mobile a grandi dati
- batch in parallelo
- analisi dati
- calcolo intrensivo e grafica
- app di produttività online

# Pattern saga

In un sistema a microservizi che utilizza messaggi asyncroni per la sincronizzazione devo in qualche modo garantire la data consistency, voglio che i dati ripetuti cambino insieme, vorrei un sistema di **_transazioni distribuite_** in modo che se un servizio fallisce posso fare il rollback.

Ne esistono principalmente due tipi:
• events/choreography → nessun coordinatore, i servizi portano avanti la saga senza avere qualcuno che li controlli, ma lavorando insieme
• commands/orchestration → controllo centralizzato, gestito da un orchestratore

Ciclo di vita:

1. arriva la richiesta
2. viene creato un file di log
3. il **saga execution coordinator (SEC)** invia le richieste ai servizi e aspetta le risposte
4. se tutto va bene il SEC scrive nel log e termina
5. se qualcosa fallisce il SEC invia una richiesta di compensazione e fa l'undo delle operazioni fatte

Implementazione tramite **_REST_** e **_JSON_**

## Eventual consistency

magari non voglio dover ricevere rispsote anche per quell iche vanno a buon fine, ricevo tanti 0 come rispsote

- non uso le transazione
- prendo un rischio e aggiungo controlli per gestire a posteriori la consistenza
- solo se le inconsistenze sono rare
- faccio una catch quando avviene linconsistenza

# Kubernetes

_Kubernetes fornisce un framework per far funzionare i sistemi distribuiti in modo resiliente, si occupa della scalabilità, failover, distribuzione delle applicazioni._

_Quindi Kubernetes è di fatto un Orchestratore di container (Docker)._

## Benefici

- **Orchestratore di container**: Kubernetes permette di gestire i container in modo efficiente
- **Zero downtime**: Kubernetes permette di aggiornare le applicazioni senza downtime
- **Self-healing**: Kubernetes si occupa di riavviare i container in caso di crash
- **Scalabilità**: Kubernetes permette di scalare orizzontalmente le applicazioni

## Componenti

- **Cluster**: insieme di nodi che eseguono applicazioni containerizzate
  - un cluster ha almeno un Worker Node
- **Worker Node**: componente che ospita i Pod
- **Pod**: unità minima di esecuzione in Kubernetes, contiene uno o più container (generalmente uno) (guscio esterno del container)
  - Network: ogni Pod ha un indirizzo IP univoco
  - Storage: ogni Pod ha un filesystem condiviso tra i container all'interno del Pod
  - Status: un Pod è in uno dei seguenti stati: Pending, Running, Succeeded, Failed
- **Kubelet**: agente che gira su ogni Worker Node e si occupa di inizializzare i Pod e ne controlla lo stato
- **Kube-proxy**: componente che si occupa di gestire il networking tra i Pod
- **Services**: fungono da singolo punto di accesso per uno o più Pod
  - Risolvono il problema dei pod che cambiano indirizzo IP ogni volta che vengono riavviati
  - Un Service ha un indirizzo IP fisso
  - Possono funzionare da Load Balancer e da API Gateway

# API Gateway

Un **_servizio REST_** che permette che la parte client non debba conoscere tutti i servizi ma solo il gateway che si occupa di fare il routing

Può racchiudere funzioni di load balancer, sicurezza, autenticazione, autorizzazione, rate limiting, caching ecc.(kubernetes ha già queste funzionalità)

- Ho solo una porta di ingresso per il client
- Fa da intermediario tra il client e i servizi attraverso le diverse porte
- Servizio rest
- Fa da fitro, wrapper a gli altri servizi

# TP monitor

Middleware che forniscono supporto alle transazioni

Caratteristiche:

- Proprità **ACID**
- Sincronizzazione **2PC**
- CLient interagiscono con sistemi che possono essere composti da più processi e macchine
- Load balancing
- Pool di risorse
- High availability
- Funnelling

Vantaggi:

- Scalabilità e tuning per grandi sistemi
- Adatti per mission critical

Limiti:

- pochi standard = poca produttività
- uso limitato dei linguaggi 4gl

## Salabilità

A seconda della dimensione del sistema, che si vuole creare bisogno introdure nuove teconologie e nuovi paradigmi

# Rabbit MQ

Message broker che permette di inviare e ricevere messaggi tra diverse applicazioni o componenti di un sistema distribuito.

## Componenti
