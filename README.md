########### ATLAS ###########

Processa i dati :

https://cernbox.cern.ch/rootjs/public/mFmKHpc4psg1H6b/data24_13p6TeV.00484074.physics_Main.merge.NTUP_MUTEST.f1512_m2250_c1404_m2220._0037.1.root?contextRouteName=files-public-link&contextRouteParams.driveAliasAndItem=public%2FmFmKHpc4psg1H6b&items-per-page=100

Modello GNN per predire tracce di muoni all'interno della "small wheel" di ATLAS

Vengono passati al modello i parametri: 

- carica totale in un cluster, 

- tempo del cluster (media sui tempi delle strip accese nel cluster), 

- posizione locale lungo la direzione x di un cluster (media sulle x delle strip accese nel cluster), 

- numero di strip accese in un cluster.

Labels:

- segnale: viene assegnata una label 1 ai cluster appartenenti a eventi di muoni già identificati da un algoritmo ("mmOnTrack"),
  inoltre viene richiesto che il momento sia maggiore di una certa soglia (muons_pt ≥ 15) e che sia presente solo una traccia di muoni (muons_author = 1).

- rumore: ad ogni evento Atlas salva inoltre i dati di un settore dove non è passato un muone in modo casuale (mmPRDRandomSectorDumped),
  a questi viene assegnato una label 0.

Struttura small wheel Atlas:

Sono presenti 2 small wheel, ognuno dei quali è diviso in 16 settori, ogni settore ha 4 rilevatori da 4 layer.

A causa della geometria e della posizione delle camere, per una maggiore consistenza nei dati, si sceglie di analizzare solo le camere appartenenti ai settorei "piccoli" (mmOnTrack_stationIndex = 55 nel caso di segnale, mmPRDRandomSectorDumped % 2 = 0 nel caso di rumore) e ai 2 dei 4 rilevatori che si trovano in "basso" (mmOnTrack_stationEta ± 1 nel caso di segnale, PRD_MM_stationEta ± 1 nel caso di rumore). 
  
########### MIMEGA ###########

Modello GNN per predire cluster di muoni all'interno di una singola camera micromegas
