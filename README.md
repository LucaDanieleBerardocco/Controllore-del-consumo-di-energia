# PROGETTO_FINALE
 
## Descrizione del progetto
 
Questo progetto implementa in linguaggio **C++** un **sistema domotico** da linea di comando, che gestisce un insieme di dispositivi di una casa (lavatrice, lavastoviglie, frigorifero, impianto fotovoltaico, ecc.).  
Tramite comandi testuali l'utente può accendere e spegnere i dispositivi, impostare dei timer, far avanzare l'orario del sistema e consultare i consumi. Il sistema controlla inoltre che la potenza totale assorbita non superi il limite massimo, e registra tutti gli eventi sia a schermo sia in un file di log.
 
Il progetto è stato sviluppato in gruppo per il corso di **Laboratorio di Programmazione** (progetto finale).
 
---
 
## Struttura del Progetto
 
PROGETTO_FINALE/
    ├── CMakeLists.txt
    ├── include/
    │   ├── Dispositivo.h
    │   ├── DispositivoCiclico.h
    │   ├── Logger.h
    │   ├── SistemaDomotico.h
    ├── src/
    │   ├── Dispositivo.cpp
    │   ├── DispositivoCiclico.cpp
    │   ├── Logger.cpp
    │   ├── SistemaDomotico.cpp
    │   ├── main.cpp
    ├── log/
    │   ├── log.txt
    │   ├── log2.txt
 
 
Descrizione delle classi:
 
Dispositivo:
Classe base che rappresenta un dispositivo, individuato da nome, id e consumo. Gestisce lo stato (acceso/spento), il tempo totale di accensione, il calcolo del consumo totale e i timer di accensione e spegnimento.
 
DispositivoCiclico:
Classe derivata da 'Dispositivo' che rappresenta un dispositivo con un ciclo di durata prefissata (ad esempio la lavatrice). Tiene traccia del tempo rimanente del ciclo e si spegne automaticamente quando il ciclo termina. Per questi dispositivi è possibile impostare solo il timer di accensione.
 
Logger:
Si occupa di registrare gli eventi: ogni messaggio viene scritto nel file di log (con l'orario) e stampato a schermo.
 
SistemaDomotico:
Classe centrale del progetto. Contiene la lista dei dispositivi, l'orario corrente del sistema e la potenza massima. Gestisce l'esecuzione dei comandi, l'avanzamento del tempo, i timer, i reset e il controllo della potenza.
 
main.cpp:
Crea il 'Logger' e il 'SistemaDomotico', aggiunge i dispositivi e gestisce il ciclo di lettura dei comandi inseriti dall'utente.
 
---
 
## Dispositivi disponibili
 
Il consumo è espresso in kW; per i dispositivi ciclici è indicata anche la durata del ciclo.
 
- Impianto_Fotovoltaico (consumo -1.5, cioè produce energia)
- Lavatrice (2.0, ciclo di 110 minuti)
- Lavastoviglie (1.5, ciclo di 195 minuti)
- Pompa_di_Calore+Termostato (2.0)
- Tapparelle_Elettriche (0.3, ciclo di 1 minuto)
- Scaldabagno (1.0)
- Frigorifero (0.4)
- Forno_a_Microonde (0.8, ciclo di 2 minuti)
- Asciugatrice (0.5, ciclo di 60 minuti)
- Televisore (0.2, ciclo di 60 minuti)
 
---
 
## Comandi
 
- 'set <dispositivo> on' / 'set <dispositivo> off': accende o spegne un dispositivo.
- 'set <dispositivo> <hh:mm>': imposta il timer di accensione.
- 'set <dispositivo> <hh:mm> <hh:mm>': imposta il timer di accensione e di spegnimento (non consentito per i dispositivi ciclici).
- 'rm <dispositivo>': rimuove il timer di un dispositivo.
- 'show': mostra produzione e consumo totali e il consumo di ogni dispositivo.
- 'show <dispositivo>': mostra il consumo di un solo dispositivo.
- 'set time <hh:mm>': fa avanzare l'orario del sistema fino all'orario indicato (che deve essere successivo a quello corrente).
- 'reset time': riporta l'orario a 00:00 e spegne tutti i dispositivi, mantenendo i timer.
- 'reset timers': rimuove tutti i timer.
- 'reset all': riporta il sistema alle condizioni iniziali.
- 'exit': chiude il programma.
 
---
 
## Funzionamento
 
- **Orario:**  
  Il sistema parte alle 00:00. L'orario avanza solo con il comando 'set time', minuto per minuto: a ogni minuto vengono aggiornati i tempi di accensione dei dispositivi e vengono controllati i timer. Gli eventi (accensioni e spegnimenti) avvenuti durante l'avanzamento vengono stampati alla fine.
 
- **Controllo della potenza:**  
  La potenza massima del sistema è di 3.5 kW. Se la somma dei consumi dei dispositivi accesi supera il limite, i dispositivi vengono spenti in ordine inverso rispetto a quello di accensione (tramite una pila), finché il consumo torna sotto il limite. In questa procedura il frigorifero non viene mai spento. L'impianto fotovoltaico, avendo consumo negativo, riduce il consumo totale.
 
- **Dispositivi ciclici:**  
  All'accensione il ciclo parte con la durata prefissata; il dispositivo si spegne da solo quando il tempo rimanente arriva a zero.
 
- **Fine giornata:**  
  Con 'set time 23:59' il programma stampa il riepilogo dei consumi e termina.
 
---
 
## Documentazione
 
- Il codice è commentato direttamente nei file sorgente e negli header.
 
---
 
## Autori
 
Luca Daniele Berardocco  
Tommaso  
Marco  
 
Suddivisione del lavoro:
- 'SistemaDomotico.h' e 'SistemaDomotico.cpp': Luca Daniele Berardocco
- 'Dispositivo.h', 'Dispositivo.cpp', 'DispositivoCiclico.h' e 'DispositivoCiclico.cpp': Tommaso 
- 'Logger.h', 'Logger.cpp' e 'main.cpp': Marco 
 
Corso: Laboratorio di Programmazione  
A.A. 2024/2025
