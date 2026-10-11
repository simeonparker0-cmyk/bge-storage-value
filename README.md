# BGE Storage Value Project 



What is a 4-hour battery worth in the BGE zone and how much of that value comes from congestion? 



## Data 



Source: PJM Data Miner 2, downloaded manually on 10.10.2026



* Day-ahead hourly LMPs (`da_hrl_lmps`) 2025, pnode BGE (zone) and WESTERN HUB 
* Real-time hourly LMPs (`rt_hrl_lmps`), 2025, same nodes
* Filtered by Pnode Name (not Zone, which returns every bus in the zone)



Raw files go in `data/raw` and are not tracked in Git. Re-download using the settings above.



## Status



Work in progress (Week 1: data loading and cleaning).

