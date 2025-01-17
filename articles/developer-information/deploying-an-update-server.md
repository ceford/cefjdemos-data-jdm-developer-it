<!-- Filename: Deploying_an_Update_Server / Display title: Aggiorna server -->

## Contesto

Esiste una buona descrizione dei Server di Aggiornamento nella Documentazione per Programmatori di Joomla! copiata su [questo sito](jdocmanual?article=docus/install-update/update-server) o disponibile nella [fonte originale](https://manual.joomla.org/docs/building-extensions/install-update/update-server/).

## Risoluzione dei problemi

- **Lo script di aggiornamento SQL non viene eseguito durante l'aggiornamento.**

Se lo script di aggiornamento SQL (ad esempio, nella cartella `sql/updates/mysql`) non viene eseguito durante il processo di aggiornamento, potrebbe essere perché non c'è un numero di versione nella tabella `#_schemas` per questa estensione *prima dell'aggiornamento*. Questo valore è determinato dall'ultimo nome di script nella cartella degli aggiornamenti SQL. Se questo valore è vuoto, nessuno script SQL verrà eseguito durante quel ciclo di aggiornamento. Per assicurarti che questo valore sia impostato correttamente, assicurati di avere uno script SQL in questa cartella con il suo nome come numero di versione (ad esempio, 1.2.3.sql se la versione è 1.2.3). Il file può essere vuoto o avere solo una linea di commento SQL. Questo dovrebbe essere fatto nella vecchia versione — quella prima dell'aggiornamento. In alternativa, puoi aggiungere questo valore al `#_schemas` utilizzando una query SQL.

*Tradotto da openai.com*

