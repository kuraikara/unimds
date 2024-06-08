## JEE

### Java Enterprise Edition: Cos'è, Descrizione Dettagliata e Modifiche allo Spyke

JEE è una piattaforma di sviluppo per applicazioni enterprise che fornisce un modello di programmazione per lo sviluppo e l'esecuzione di applicazioni distribuite e multi-tier. JEE è basato su Java Standard Edition (JSE) e fornisce API per l'accesso ai database, la gestione delle transazioni, la sicurezza, la connettività di rete e altro ancora.

È composta da J2SE, JEE e J2ME. J2SE è la piattaforma standard per lo sviluppo di applicazioni desktop e server-side. J2EE è una piattaforma per lo sviluppo di applicazioni enterprise. J2ME è una piattaforma per lo sviluppo di applicazioni mobili.

Sul piano dell'architettura di JEE abbiamo:

- **Web server**: Servlet/JSP, SOAP engine (predecessore di REST) o RMI (no interfaccia web, connesso direttamente al backend) lato front-end.
- **EJB**: Lato back-end business logic.
- **Database**: Lato storage tra cui ERP (gestionali proprietari), RDBMS (con JDBC) e JMS MOM (Message Oriented Middleware).

#### Quando Usare Enterprise Beans

Usiamo Enterprise Beans quando abbiamo bisogno di scalabilità, transazioni con integrità dei dati e molteplici client che accedono ai dati. Gli Enterprise Beans sono componenti che gestiscono la logica di business e sono indipendenti dalla piattaforma. Vengono eseguiti all'interno di un container EJB.

#### Le Funzionalità di JEE

- **Enterprise Java Beans (EJB)**: Componenti che aiutano a costruire la logica di business di un'applicazione. Sono eseguiti all'interno di un container EJB e sono di tre tipi: session beans, entity beans e message-driven beans.
- **Java Naming and Directory Interface (JNDI)**: API per accedere ai servizi di directory e naming su diverse macchine.
- **Remote Method Invocation (RMI)**: API per la comunicazione tra processi distribuiti.
- **Servlets**: Presentazione dinamica e gestione delle sessioni client web.
- **Java Server Pages (JSP)**: Pagine web dinamiche.
- **Java Message Service (JMS)**: API per la messaggistica asincrona con modelli point-to-point e publish/subscribe.
- **Java Transaction API (JTA)**: API per la gestione delle transazioni distribuite (XA o CORBA OTS).
- **Java Database Connectivity (JDBC)**: API per l'accesso ai database relazionali.
- **Java Authentication and Authorization Service (JAAS)**: API per l'autenticazione e l'autorizzazione.
- **JavaMail**: API per l'invio e la ricezione di email.

### Livelli di JEE

- **Client Tier**: Interfaccia utente, browser, applet, client Java.
- **Web Tier**: Servlets, JSP, JavaBeans, JavaMail, JNDI.
- **Business Tier**: EJB, JMS, JTA, JCA.
- **Enterprise Information System (EIS) Tier**: Database, ERP, RDBMS, JMS MOM.

### EJBs (Enterprise Java Beans)

Sono componenti che implementano la logica di business e sono eseguiti all'interno di un container EJB. Sono di tre tipi: session beans, entity beans e message-driven beans.

#### Session Beans

Fanno da intermediari tra i client e le entity beans. Sono di due tipi: stateful e stateless.

- **Stateful**: Il client rimane lo stesso per tutta la sessione.
- **Stateless**: Il client cambia ad ogni richiesta (anche diversi client).

Si rimuovono delle funzionalità dalle servlets e si mettono nei session beans. Possono gestire tutte le invocazioni di un client. Ricevono dati da JPA e li processano per mandarli alle servlets.

#### Entity Beans

Rappresentano i dati persistenti. Creano una tabella alla prima esecuzione per poi aggiornarla ad ogni richiesta.

- **Session EJB e Singleton EJB**: Sono per un singolo client, vivono per tutta la sessione del client e implementano logica di business indipendente dal client.
- **Message Driven EJB**: Sono per più client, attivati da un messaggio asincrono JMS e vivono per tutta la sessione del messaggio.

#### Quando Usare un Session Bean?

- Se solo un client ha accesso ad un'istanza di bean.
- Se lo stato del bean non è persistente.
- Se il bean implementa un web service.

**Tipi di Session Bean:**

- **Stateful**: Il client rimane lo stesso per tutta la sessione, il bean mantiene lo stato della conversazione (più costoso, occupa più memoria).
- **Stateless**: Il client cambia ad ogni richiesta, il bean non mantiene lo stato della conversazione.

#### Singleton EJB

Un Singleton EJB è equivalente nel middleware al pattern Singleton di GOF: memorizza dati condivisi che non dipendono dalla sessione con l'utente.

### EJB Server

Il server EJB è un server applicativo che fornisce un ambiente di runtime per gli EJB. Il server EJB fornisce servizi come la Java Virtual Machine (JVM), le classi di supporto per gli EJB, funzioni base di ORB (Object Request Broker) e TP Monitor, funzioni di accesso al DB e bilanciamento del carico.

### EJB Container

Il container EJB è un ambiente di runtime per gli EJB. Fornisce servizi come la gestione del ciclo di vita degli EJB, la gestione della transazione, la sicurezza, la gestione delle eccezioni, la gestione della persistenza e la gestione delle chiamate remote.

### Remote Client

Un client remoto è un client che accede agli EJB da un'altra JVM. Utilizza il protocollo RMI per comunicare con il server EJB.

### JMS (Java Message Service)

JMS è un'API per la messaggistica asincrona. Fornisce due modelli di messaggistica: point-to-point e publish/subscribe. Permette la comunicazione tra applicazioni distribuite e eterogenee come fanno i MOM. È reliable: se il mittente non riceve conferma di ricezione del messaggio, lo rimanda. È una libreria che si utilizza con i Message Driven Beans, che sono attivati da un messaggio asincrono JMS e vivono per tutta la sessione del messaggio.

**Modelli di Messaggistica:**

- **Point-to-Point**: Un solo mittente e un solo destinatario.
- **Publish/Subscribe**: Un solo mittente e più destinatari, con un topic e una coda di messaggi.

### Entità

Un'entità è un oggetto che rappresenta un'istanza di una tabella di database. È una classe Java annotata con @Entity e gestita dal framework ORM JPA (Java Persistence API). Ogni istanza è una riga nella tabella del database. Finché non viene reso persistente, vive nello heap come tutte le variabili di istanza.

### EJB Remote

Un EJB remoto è un EJB che può essere chiamato da un client remoto. Implementa un'interfaccia remota che il client utilizza per chiamare i metodi dell'EJB, coordinando transazioni e sicurezza.

### Dependency Injection

La Dependency Injection è un design pattern che permette di iniettare le dipendenze di un oggetto in un altro oggetto. Viene utilizzata per ridurre le dipendenze tra i componenti di un'applicazione e per iniettare le dipendenze di un EJB in un altro EJB, utilizzando le annotazioni.

### Entity Manager

L'Entity Manager è un'interfaccia per l'interazione con il database. È utilizzato per eseguire operazioni CRUD (Create, Read, Update, Delete) sulle entità, gestire le transazioni e la persistenza delle entità, e per eseguire query JPQL (Java Persistence Query Language) sulle entità.
