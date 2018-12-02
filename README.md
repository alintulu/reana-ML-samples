# reana-ML-samples

Tracker hits are low-level information that are used to reconstruct tracks and are not present in the data format available to analysts (e.g AOD, MINIAOD or NANOAOD). This code saves information of reconstructed hits in the tracker, plus some other useful variables for machine learnign studies.

## Categories of the tree

  - *hit_** are variables refering to the reconstructed hits in the tracker. E.g. position, position error, sub detector and *an attempt to** associate the reconstructed hit to a generator level particle, simulated track, or a generated jet
  - *simtrack_** are variables associated to the simulated tracks. They are used as an intermediate step to associate a reconstrcuted hit to a generated particle.
  - *genpart_** are variables linked to generator level particles
  - *genjets_** are variables refering to jets clustered with generated particles
  - *track_** are variables linked to reconstructed tracks
  - *track_hit_** are variables describing reconstructed hits associated to reconstructed tracks

## Workflow

```
        +---------+
        | GEN-SIM |       
        +---------+
             |
             v
  +----------------------+
  | DIGI,L1,DIGI2RAW,HLT |     In addition to standard, add Pixel and SiStrip sim digis
  +----------------------+     needed for RecHit <—> SimTrack matching
            |
            v
  +----------------------+
  | RAW2DIGI,L1Reco,RECO |     In addition to the standard data format definition, 
  +----------------------+     keep Pixel clusters, SiStrip clusters, SimTracks, 
            |                  TrackExtra for generalTracks, and tracker digis
            v
      +------------+
      | ntupalizer |           Save rechits with truth information
      +------------+
 ```
 **step0**
 
 **step1**
 
 **step2** 
 
   - Pixel and SiStrip clusters are necessary to recreate RecHits (*reconstructed hits*) on the fly in the ntuplization step (RecHits are transient)
   - SimTracks are needed to link *truth* information on RecHits
   - TrackExtra is needed to run the track refitter to access the global position of the rechits extracted from the track hit pattern (rechit global positions are transient)
   
 **step3**
 
   - The config file runs cluster parameter estimators to produce rechits as well as the track refitter
   - The ntuplizer itsellf needs the tracker digis to match rechits and simtracks
