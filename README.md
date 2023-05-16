# KeyKeep
A self-hosted password manager for companies and privates.
The self-hosted section of the application is a group of microservices that can be deployed on a Kubernetes cluster/docker.
Accessible with a desktop application, a web interface, a browser extension and a mobile app.
The main services of the application are:
- user management
- group management
- team management
- password management
- password sharing
- password sharing by groups
- password generation
- password grouping by tags
- cryptography
- Smtp/pop domain with user mail 
- 2FA
- password renewal
- password history

## Technologies
- C# .NET 6 (8 future releases) (services)
- ocelot (api gateway)
- MySQL/MariaDB (database)
- Angular LTS (web interface, desktop application)
- Kotlin (mobile app)
- JavasScript (browser extension)
  

## Schema 
https://s.icepanel.io/bpeUw2ZAtI1XCG/sx00


## Microservices
### User Management (Gestione Utenti): 
Questo dominio gestisce tutte le funzionalità legate alla registrazione degli utenti, l'autenticazione, la gestione dei profili utente e le operazioni di recupero password.

### Group Management (Gestione Gruppi): 
Questo dominio si occupa della creazione, modifica e eliminazione dei gruppi di utenti. Fornisce funzionalità per assegnare utenti ai gruppi e gestire i permessi di accesso ai dati del gruppo.

### Team Management (Gestione Team):
 Questo dominio gestisce la creazione, modifica e eliminazione dei team all'interno dell'applicazione. Fornisce funzionalità per assegnare utenti ai team e gestire le autorizzazioni specifiche per i team.

### Password Management (Gestione Password): 
Questo dominio si occupa di tutte le funzionalità legate alla gestione delle password. Include la creazione, modifica ed eliminazione delle password, la visualizzazione e la ricerca delle password esistenti, nonché la gestione della sicurezza delle password.

### Password Sharing (Condivisione Password): 
Questo dominio gestisce la condivisione sicura delle password tra gli utenti. Include la possibilità di condividere le password con singoli utenti o con gruppi specifici.

### Password Generation (Generazione Password): 
Questo dominio fornisce funzionalità per la generazione di password sicure in base a criteri definiti dall'utente, come lunghezza, complessità e caratteri ammessi.

### Cryptography (Crittografia): 
Questo dominio si occupa della crittografia e decrittografia delle password salvate nell'applicazione, garantendo la sicurezza dei dati sensibili.

### SMTP/POP Domain with User Mail (Dominio SMTP/POP con Mail Utente): 
Questo dominio gestisce l'integrazione con i server SMTP/POP per l'invio e la ricezione delle email associate agli account utente.

### Two-Factor Authentication (Autenticazione a Due Fattori):
 Questo dominio si occupa dell'implementazione dell'autenticazione a due fattori per un ulteriore livello di sicurezza nell'accesso all'applicazione.

### Password Renewal (Rinnovo Password): 
Questo dominio gestisce la possibilità per gli utenti di rinnovare le proprie password periodicamente, migliorando la sicurezza.

### Password History (Cronologia Password): 
Questo dominio tiene traccia della cronologia delle password utilizzate dagli utenti, consentendo la visualizzazione delle password precedenti e il monitoraggio dei cambiamenti.

## Mermaid
``` mermaid
graph LR

subgraph KeyKeep
  subgraph Frontend
    WebInterface
    DesktopApplication
    BrowserExtension
    MobileApp
  end
  subgraph Backend
    LoadBalancer
    subgraph ServiceCluster
      UserManagementService
      GroupManagementService
      TeamManagementService
      PasswordManagementService
      PasswordSharingService
      PasswordGenerationService
      CryptographyService
      SmtpPopDomainService
      TwoFactorAuthService
      PasswordRenewalService
      PasswordHistoryService
    end
    LoadBalancer --> APGateway
    APGateway --> UserManagementService
    APGateway --> GroupManagementService
    APGateway --> TeamManagementService
    APGateway --> PasswordManagementService
    APGateway --> PasswordSharingService
    APGateway --> PasswordGenerationService
    APGateway --> CryptographyService
    APGateway --> SmtpPopDomainService
    APGateway --> TwoFactorAuthService
    APGateway --> PasswordRenewalService
    APGateway --> PasswordHistoryService
    APGateway --> RabbitMQ
  end
end

WebInterface --> LoadBalancer
DesktopApplication --> LoadBalancer
BrowserExtension --> LoadBalancer
MobileApp --> LoadBalancer

RabbitMQ --> UserManagementService
RabbitMQ --> GroupManagementService
RabbitMQ --> TeamManagementService
RabbitMQ --> PasswordManagementService
RabbitMQ --> PasswordSharingService
RabbitMQ --> PasswordGenerationService
RabbitMQ --> CryptographyService
RabbitMQ --> SmtpPopDomainService
RabbitMQ --> TwoFactorAuthService
RabbitMQ --> PasswordRenewalService
RabbitMQ --> PasswordHistoryService

```
