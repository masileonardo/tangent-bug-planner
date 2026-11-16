# Simulazione Navigazione Autonoma: Tangent Bug

*Project Work Magistrale | Università degli Studi di Firenze | 2026* · [English version](README.md)

<p align="center">
  <img src="showcase/mixed/seed%2067/Prova_1_TB_Seed67_SR1.0_Radius0.1_Rays360.gif" width="850" alt="Simulazione Tangent Bug">
</p>

Questo progetto implementa un ambiente di simulazione 2D per l'algoritmo di navigazione **Tangent Bug**. Il sistema modella un robot dotato di un sensore (simile a un LIDAR) incaricato di raggiungere un obiettivo (Goal) navigando in un ambiente pieno di ostacoli generati casualmente.

Tutti i parametri della simulazione (grandezza del robot, raggio del sensore, numero di ostacoli, velocità, ecc.) sono **completamente configurabili** in modo semplice tramite il file `config.py`.

## Caratteristiche Principali

* **Logica a Due Stati:** Il robot alterna in modo autonomo due comportamenti principali per trovare la strada:
  * *Move-to-Goal*: Il robot si muove direttamente verso il traguardo o verso lo spigolo visibile che lo avvicina di più.
  * *Boundary-Following*: Se il robot finisce in un vicolo cieco (minimo locale), inizia a seguire il perimetro dell'ostacolo per aggirarlo.
* **Mappe Casuali ma Sicure:** La mappa viene generata dinamicamente ad ogni avvio. Gli ostacoli vengono posizionati in modo casuale ma intelligente, assicurando che non si sovrappongano al punto di partenza o al traguardo.
* **Sensore Simulato:** Il robot calcola le distanze dagli ostacoli in tempo reale e individua gli spigoli liberi per capire dove può passare.
* **Grafica in Tempo Reale:** L'interfaccia mostra la mappa 2D, la visuale del sensore e un pannello con tutti i dati in tempo reale (distanze, stato attuale del robot).
* **Esportazione Automatica:** Alla conclusione della prova con successo, il sistema salva automaticamente una GIF animata della traiettoria nella cartella `media/`.

## Pseudo-codice dell'Algoritmo

**Ripetere il comportamento 1: move to goal**

1. Calcolare i punti di discontinuità $O_k$.
2. Muoversi verso il goal, se raggiungibile; altrimenti dirigersi verso il punto di discontinuità con distanza euristica minima $h_k(q)$.

*Finché non si verifica una delle seguenti condizioni:*
* il goal viene raggiunto; oppure
* la distanza euristica minima $h_k(q)$ inizia ad aumentare.

---

**Ripetere il comportamento 2: boundary following**

1. Calcolare i punti di discontinuità $O_k$ e le distanze $d_{\text{reach}}$ e $d_{\text{followed}}$.
2. Seguire il bordo mantenendo la stessa direzione di percorrenza adottata in precedenza.

*Finché non si verifica una delle seguenti condizioni:*
* il goal viene raggiunto; oppure
* viene completato un ciclo completo (il goal è irraggiungibile); oppure
* $d_{\text{reach}} < d_{\text{followed}}$.


## Struttura del Progetto

* `main.py`: Il file da avviare per far partire il programma.
* `config.py`: Il pannello di controllo dove puoi modificare tutte le impostazioni e i parametri del mondo e del robot.
* `simulation.py`: Gestisce il ciclo di vita della simulazione (muove il robot e aggiorna lo schermo).
* `robot.py`: Il "cervello" del robot e le sue regole di movimento.
* `worldgen.py`: Si occupa di creare la mappa e disegnare gli ostacoli.
* `geometry.py`: Contiene i calcoli matematici e verifica se il robot sbatte contro i muri.
* `sim_render.py` & `sim_playback.py`: Gestiscono la grafica a schermo e il salvataggio dell'animazione GIF.
* `sim_types.py`: Contenitori di dati per tenere traccia in modo ordinato di cosa succede nella simulazione.

## Installazione

Si consiglia di utilizzare un ambiente virtuale (come `venv` o `conda`). Per installare le librerie necessarie, apri il terminale ed esegui:

```bash
pip install -r requirements.txt
```

## Avvio

```bash
git clone https://github.com/masileonardo/tangent-bug-planner.git
cd tangent-bug-planner
pip install -r requirements.txt
python main.py
```

Si apre una finestra con la simulazione. Quando il robot raggiunge il goal, la GIF viene salvata nella cartella `media/`.

## Risultati

Nella cartella `showcase/` ci sono le GIF delle prove, divise per tipo di ostacolo (rettangoli, poligoni concavi, blob convessi e concavi). Nella cartella `showcase/mixed/` la stessa mappa è ripetuta cambiando il raggio del sensore (`SR`) e il numero di raggi del LiDAR (`Rays`).

## Team

Progetto di gruppo sviluppato con i miei compagni per il corso AAIR della Laurea Magistrale in Robotics, Automation and Electrical Engineering, Università degli Studi di Firenze.

## Contatti

Leonardo Masi

- Portfolio: https://masileonardo.github.io/#tangent-bug
- LinkedIn: https://www.linkedin.com/in/leonardo-masi-b09b28219/
