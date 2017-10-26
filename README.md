# surf_striatum
Pipeline for surface-based connectivity and morphometry in the striatum


## Dependencies:
* vasst-dev (github.com/akhanf/vasst-dev)
* FSL, niftyreg, ...

## Steps:

importData

2.0_processT1

4.0_preprocDTI

QC (no need to wait for 4.0)
<manual check for QC>

2.1_processT1_regFail <for failed reg subj>

QC again if needed

4.1_genParcellation <depends on 4.0 and 2.1>

4.2_warpParcellationsToMNI <depends on 4.1>

7.1_computeIndivParcMapLeftRight  <depends on 4.2>

8.3_computeMaxProbDiffParcVolumeLeftRight  
	-generates  striatum_withRostralMotor.maxProbDiffusionParcVolume.byHemi.csv   <-- striatum parcellation volumes in MNI space

9.0_runSurfDisplacementTemplate
	-quick: only takes a few seconds to prepare the template files (no need to run cluster job)

9.1_runSurfDisplacementTargets
	-runs LDDMM -- use sharcnetPipe (request at least 8-16GB memory - sharcnetPipe2 or sharcnetPipe4)

9.2_runSurfBasedTractography
	-runs tractography from surface vertices in subject space  - use sharcnetPipe2



