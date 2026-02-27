# Angular Employee Management: CRUD & Advanced Pagination

Sistema avanzato di gestione del personale sviluppato in **Angular**, integrato con servizi RESTful per operazioni di recupero, eliminazione e navigazione dinamica tra i record.

## Descrizione
L'applicazione evolve il concetto di comunicazione HTTP implementando una logica di paginazione lato client che sincronizza le richieste al backend. Oltre alla visualizzazione dei dati anagrafici (ID, Nome, Genere, Date), il sistema permette la rimozione fisica dei record tramite il metodo DELETE e la navigazione fluida attraverso un set di dati potenzialmente infinito grazie al controllo degli indici di pagina.



## Funzionamento del Sistema:
* **Dynamic Pagination Logic**: Implementazione di funzioni per il cambio pagina (`firstPage`, `lastPage`, `changePage`). Il sistema calcola dinamicamente l'indice basandosi sui metadati restituiti dal server (`data.page.totalPages`).
* **HTTP CRUD Operations**:
    * **GET**: Recupero parametrizzato (`page`, `size`) per ottimizzare il carico dei dati.
    * **DELETE**: Rimozione dei dipendenti tramite ID con sottoscrizione all'osservabile per confermare l'operazione.
    * **POST**: Predisposizione nel Service per l'invio di nuovi oggetti "Employee" al database.
* **State & Navigation Control**: Utilizzo di variabili di stato (`page`, `size`) per mantenere la coerenza della vista durante la navigazione. Il pulsante "Previous" viene disabilitato automaticamente alla pagina 0 tramite Property Binding.
* **HATEOAS Integration**: Gestione fluida di risposte JSON complesse, navigando all'interno della struttura `_embedded` tipica dei backend Spring Data REST.
* **Component Interaction**: Architettura basata su un Service centralizzato (`EmployeeService`) iniettato nel componente della tabella per garantire la separazione tra UI e logica di rete.

## Tecnologie e Concetti
* **Angular Services**: Utilizzo di `@Injectable` per gestire il ciclo di vita delle chiamate HTTP.
* **RxJS Subscriptions**: Gestione asincrona delle risposte del server.
* **Dynamic Template Strings**: Costruzione degli URL delle API concatenando variabili di pagina e ID.
* **UI Feedback**: Utilizzo di direttive strutturali (`*ngIf`, `*ngFor`) per gestire il rendering della tabella e dei controlli di navigazione.

## Dashboard di Navigazione
| Azione | Metodo Componente | Logica |
| :--- | :--- | :--- |
| **First** | `firstPage()` | Reset dell'indice a `0` e ricaricamento dati. |
| **Previous** | `changePage(-1)` | Decremento dell'indice (se `> 0`). |
| **Next** | `changePage(1)` | Incremento dell'indice e fetch dei nuovi dati. |
| **Last** | `lastPage()` | Salto diretto all'indice `totalPages - 1`. |
| **Delete** | `deleteEmployee(id)` | Chiamata DELETE seguita da reload della vista. |

---
*Progetto focalizzato sulla gestione di grandi volumi di dati e sull'interazione completa con API RESTful professionali.*
