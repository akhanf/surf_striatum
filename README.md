# surf_striatum
Pipeline for surface-based connectivity and morphometry in the striatum


## Dependencies:
* vasst-dev (github.com/akhanf/vasst-dev)
	* FSL, niftyreg, ...
* Use neuroglia-vasst-dev Singularity container
* neuroglia-helpers

## to do:

* run matlab script, trim extraneous parts



## Steps:
00_runAll




# sub-steps
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

8.3_computeMaxProbDiffParcVolumeLeftRight   <no batch, depends on 7.1>
	-generates  striatum_withRostralMotor.maxProbDiffusionParcVolume.byHemi.csv   <-- striatum parcellation volumes in MNI space

9.0_runSurfDisplacementTemplate  <depends on 2.0>
	-quick: only takes a few seconds to prepare the template files (no need to run cluster job)

9.1_runSurfDisplacementTargets   <depends on 9.0>
	-runs LDDMM -- use sharcnetPipe (request at least 8-16GB memory - sharcnetPipe2 or sharcnetPipe4)

9.2_runSurfBasedTractography	<depends on 9.1 and 4.0>
	-runs tractography from surface vertices in subject space  - use sharcnetPipe2



