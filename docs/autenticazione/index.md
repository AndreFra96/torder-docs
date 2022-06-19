# Autenticazione

In questo progetto è necessario che gli utenti abbiano accesso ai diversi componenti e che i componenti possano identificare qual'è l'utente con il quale sta lavorando al momento per gestirne correttamente i privilegi e le preferenze.

## Auth0

Il servizio utilizzato per la gestione degli utenti è Auth0 che utilizza lo standard Oauth 2.0 per la gestione dell'autenticazione tramite Access Token in formato JSON Web Token

## JSON Web Token (JWT)

!!! quote "Definizione da https://jwt.io/"

    JSON Web Tokens are an open, industry standard [RFC 7519](https://datatracker.ietf.org/doc/html/rfc7519) method for representing claims securely between two parties.

Un Token non è nient'altro che una particolare stringa di lunghezza variabile contenente diverse informazioni legate ad uno specifico utente, che viene firmata in modo tale da non permetterne la modifica.

Questo token viene passato insieme alle richieste e permette non solo di stabilire se l'utente ha accesso ad una risorsa ma anche di estrarre immediatamente diverse informazioni come: privilegi, preferenze o altro.
