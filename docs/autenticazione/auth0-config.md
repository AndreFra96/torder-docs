# Configurazione Auth0

Auth0 è stato configurato appositamente per la gestione dei diversi componenti.

## Tenant

Uno dei concetti principali di Auth0 è il tenant, un tenant non è nient'altro che un contenitore per tutte le configurazioni dedicate ad una applicazione.

Diverse applicazioni possono condividere lo stesso tenant condividendo in questo modo anche gli utenti e permettendogli con un unico accesso di utilizzare tutte le applicazioni ad esso collegate.

Il tenant utilizzato è denominato <b> rca-api </b> e al suo interno contiene 2 api e 2 applicazioni.

### Api

All'interno di Auth0 un'Api è un'entità che rappresenta una risorsa capace di accettare e rispondere a richieste protette effettuate dalle Applicazioni.

#### RcaApi

Rappresenta il backend come risorsa, permette di definire i privilegi con i quali i vari utenti hanno accesso al software di backend e alle risorse in esso contenute.

#### Auth0 Management Api

Questa Api rappresenta un entità di Auth0 e non può essere modificata, questa entità serve per ottenere informazioni sugli utenti memorizzati ed effettuare altre operazioni su Auth0 da un'applicazione esterna.

### Applicazioni

Il termine applicazione o app in Auth0 non implica particolari caratteristiche di implementazione.

Ad esempio, potrebbe essere un'app nativa eseguita su un dispositivo mobile, una Single Page Application eseguita su un browser o una normale applicazione Web eseguita su un server.

#### T-Order

(Single Page Application - neJrFUZ5g8aD4hDHLMxiiyY2xLvuOGmB)

Questa applicazione rappresenta il software di frontend ed è una Single Page Application che viene eseguita direttamente del browser.

Utilizza un plugin fornito da Auth0 per gestire l'autenticazione.

!!! note

    Quando viene richiesto un token di accesso al backend tramite invio di username e password il backend si identifica come questa applicazione per effettuare la richiesta del token ad Auth0.

#### RcaApi

(Machine to Machine - pZOMvk3hvJfEAyxObluzciFQvnpb66tH)

Il Software di backend per poter avere accesso agli utenti del tenant deve identificarsi come un'applicazione che ha accesso ad Auth0 Management Api, per questo motivo è stata configurata questa Machine to Machine application a nome della quale il software di backend effettua le richieste.
