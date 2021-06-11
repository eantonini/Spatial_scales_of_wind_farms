This folder contains setup files and instructions to reproduce the numerical results of the paper using WRF 4.2.1.


## Downloading WRF

WRF 4.2.1 can be downloaded from https://github.com/wrf-model/WRF/releases/tag/v4.2.1


## Setting up WRF cases

Copy `module_initialize_ideal.F` into `$WRF_ROOT_DIRECTORY/dyn_em/`

Copy

* `input_sounding_neutral` (or `input_sounding_conv-neutral`)
* `doamin1_namelist.input` (or `doamin2_namelist.input`, `doamin3_namelist.input`)
* `wind-turbine-1.tbl`
* `domain1_windturbines-ij.txt` (or one of the other `*windturbines-ij.txt` files)

into `$WRF_ROOT_DIRECTORY/test/em_convrad/`

Then change

* `input_sounding_neutral` (or `input_sounding_conv-neutral`) to `input_sounding`
* `doamin1_namelist.input` (or `doamin2_namelist.input`, `doamin3_namelist.input`) to `namelist.input`
* `domain1_windturbines-ij.txt` (or one of the other `*windturbines-ij.txt` files) to `windturbines-ij.txt`


## Changing WRF setup files

In the paper, we performed simulations with different combinations of geostrophic winds, Coriolis parameters, and layouts.

The setup files included in this repository are for a geostrophic wind of 12 m/s, Coriolis parameter of 1.05 x 10^(-4) rad/s.

To change the geostrophic wind, insert the desired value in the fourth column of `input_sounding`.

To change the Coriolis parameter, insert the desired value at line 419 of `module_initialize_ideal.F`. Every time `module_initialize_ideal.F` is changed, you must re-compile WRF.

To change the layout, select the desired file among the `*windturbines-ij.txt` files.


## Compiling WRF

Please follow the instructions at https://www2.mmm.ucar.edu/wrf/OnLineTutorial/compilation_tutorial.php to install the required libraries.

The following commands should then be run from the WRF root directory:

* `>> ./clean  &> log.clean1`
* `>> ./clean -a &> log.clean2`
* `>> ./configure &> log.configure` with options 34 and 1
* `>> ./compile em_convrad >& log.compile`


## Running WRF

Run from the WRF root directory:

* `>> cd test/em_convrad/`
* `>> ./run_me_first.csh`
* `>> rm ozone*`
* `>> rm RRTMG_*`
* `>> ./ideal.exe`
* `>> ./wrf.exe`
