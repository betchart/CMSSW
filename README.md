## Setup

```bash
cmsrel CMSSW_5_3_7
cd CMSSW_5_3_7/src/
cmsenv
cvs co Configuration/GenProduction
scram b -j 4
```

## Step 0

```bash
cmsDriver.py Configuration/GenProduction/python/EightTeV/POWHEG_PYTHIA6_top_tauola_SemileptonicNonGG_cff.py -s GEN --filein=lhe:5882 --conditions START53_V7C::All --beamspot Realistic8TeVCollision --datatier GEN-SIM --eventcontent RAWSIM -n 1000 --no_exec
cmsRun POWHEG_PYTHIA6_top_tauola_SemileptonicNonGG_cff_GEN.py
```

## Step 1

```bash
cmsDriver.py Configuration/GenProduction/python/EightTeV/POWHEG_PYTHIA6_top_tauola_SemileptonicNonGG_cff.py -s GEN,SIM --filein=lhe:5882 --conditions START52_V9::All --beamspot Realistic8TeVCollision --pileup NoPileUp --datatier GEN-SIM --eventcontent RAWSIM -n 10 --no_exec
echo 'process.Timing=cms.Service("Timing", summaryOnly=cms.untracked.bool(True))' >> POWHEG_PYTHIA6_top_tauola_SemileptonicNonGG_cff_GEN_SIM.py
cmsRun POWHEG_PYTHIA6_top_tauola_SemileptonicNonGG_cff_GEN_SIM.py
```
