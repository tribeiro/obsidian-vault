h1. Justification

This test is designed to cross-check the performance of the Curvature Wavefront Sensing (CWFS) algorithm against a classical "focus sweep" approach.

It requires that the optics in a good enough state that the sources can be well described by psf. Therefore, we may have to wait until a couple iterations of the optical alignment is executed, and we are somewhat familiarized with the standard CWFS procedure.

h1. Description

The idea is to take a series of images offsetting one of the hexapods in a single degree of freedom (x, y or z) at a time.

It is important that the "optimum position" is inside the range of offsets executed in a series. The offsets should also be small enough that the sources can still be described by a psf (e.g. not donuts and low aberration).

We will probably want to minimize the telescope movement, in order to give us enough time to take data and analyze it without significant changes in the optical state. One possibility is to select a target close to the South Pole. However, these low elevations might accentuate any issue with the optics. If we need to select targets at higher elevations, it might be best to select target that are 1-1.5 hours from crossing the meridian at intermediary elevations.

This can be done using the {{mtcs.find_target}} method or {{mtcs.radec_from_azel}}. A good Az/El position for this test would be 

{noformat}
az=170.0 deg
el=50.0 deg
{noformat}

This would point the telescope about 1.5 hours before transit, and would be good for about 3 hours of observations, before the elevation starts to change considerably.

Once in position, the idea is to take observations moving one of the hexapods in one axis (x, y or z) in a uniform range (e.g. +/- 0.1 mm in steps of 0.025mm).

h2. Execution

This test can most likely be executed by a pair of SAL Scripts; one to find/track a target and another to take the data.

We can probably use the existing {{maintel/track_target.py}} standard SAL Script to find/track a target.

Taking the data will require a new SAL Script that receives:

1. Which hexapod to offset.
2. Which axis to offset.
3. Offset configuration:
	1. Minimum/Maximum/Step.
4. Exposure configuration.

h2. Data Analysis

We will need psf measurements for the sources in the images and a way to aggregate that information with the hexapod position.

Then we will need to fit a polynomial function and extract the parameters. 
