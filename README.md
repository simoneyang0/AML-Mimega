########### ATLAS ###########

Processa i dati :

https://cernbox.cern.ch/rootjs/public/mFmKHpc4psg1H6b/data24_13p6TeV.00484074.physics_Main.merge.NTUP_MUTEST.f1512_m2250_c1404_m2220._0037.1.root?contextRouteName=files-public-link&contextRouteParams.driveAliasAndItem=public%2FmFmKHpc4psg1H6b&items-per-page=100

Modello GNN per predire tracce di muoni all'interno della "small wheel" di ATLAS

Vengono passati al modello i parametri: 

- carica totale in un cluster, 

- tempo del cluster (media pesata sui tempi delle strip in un cluster), 

- posizione locale lungo la direzione x di un cluster (media pesata sulle x delle strip in un cluster), 

- numero di strip accese in un cluster.

Ad ogni cluster viene associato un nodo e i collegamenti tra questi sono stati ottenuti con un k-NearestNeighbors.

Labels:

- segnale: viene assegnata una label 1 ai cluster appartenenti a eventi di muoni già identificati da un algoritmo ("mmOnTrack"),
  inoltre viene richiesto che il momento sia maggiore di una certa soglia (muons_pt ≥ 15) e che sia presente solo una traccia di muoni (muons_author = 1).

- rumore: ad ogni evento Atlas salva inoltre i dati di un settore dove non è passato un muone in modo casuale (mmPRDRandomSectorDumped),
  a questi viene assegnato una label 0.

Il modello impara ad essegnare una label 1 ai cluster di muoni.

Struttura small wheel Atlas:

Sono presenti 2 small wheel, ognuno dei quali è diviso in 16 settori, ogni settore ha 4 rilevatori da 4 layer.

A causa della geometria e della posizione delle camere, per una maggiore consistenza nei dati, si sceglie di analizzare solo le camere appartenenti ai settorei "piccoli" (mmOnTrack_stationIndex = 55 nel caso di segnale, mmPRDRandomSectorDumped % 2 = 0 nel caso di rumore) e ai 2 dei 4 rilevatori che si trovano in "basso" (mmOnTrack_stationEta ± 1 nel caso di segnale, PRD_MM_stationEta ± 1 nel caso di rumore). 
  
########### MIMEGA ###########

Modello GNN per predire cluster di muoni all'interno di una singola camera micromegas

La camera è composta da 360 strip e a ognuna di queste è associata una carica.
Ogni strip è considerata come un nodo, collegato solo con le altre strip adiacenti.

Viene dunque fatto passare nel modello solo l'informazione sulla carica di ogni strip.

I dati sono divisi in acquisizioni fatti con un trigger interno ed uno esterno. 
Nel primo caso questi sono considerati tutti strip di rumore e quindi viene assegnata una label 0 a tutte le strip.
Nel secondo caso viene usato un algoritmo classico per individuare i cluster associati ai muoni, viene assegnato una label 1 alle strip appartenenti a questi cluster e 0 alle restanti strip.

Il modello impara ad assegnare una label 1 alle strip associati ai cluster dei muoni.
