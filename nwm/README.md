# NOAA National Water Model Reanalysis Model Data

In the field of Earth System Modeling, a reanalysis is a model
simulation that joins modern modeling technologies and newer, more
complete, datasets to obtain a better understanding of past
environments. For example, in weather forecasting, it can be thought of
as running a weather forecast model in the past. In such a scenario it
could mean the running of a weather model for a period when no data
existed in order to get a better understanding of the state of the
weather from that period. This same type of historical run can be
conducted for other types of models as well, including water models.

The NOAA National Water Model Reanalysis dataset contains input and output from multi-decade retrospective simulations. These simulations used observed rainfall as input and ingested other required meteorological input fields from a weather reanalysis dataset. The output frequency and fields available in this historical NWM dataset differ from those contained in the real-time forecast model. One application of this dataset is to provide historical context to current near real-time streamflow, soil moisture and snowpack conditions. The reanalysis data can be used to infer flow frequencies and perform temporal analyses with hourly streamflow output and 3-hourly land surface output. This  dataset can also be used in the development of end user applications which require a long baseline of data for system training or verification purposes. This dataset contains output from two retrospective simulations. Currently there are three versions of the dataset. Version 1.2 output files are available in netcdf (all variables). Version 2.0 output files are available in both netcdf (all variables) and zarr (channel routing variables) formats. While, the third version 2.1 input and output files are available in both netcdf and zarr for the following data types:

channel routing (chrtout)

subsurface (gwout)

lake (lakeout)

land surface (ldasout)

precipitation (precip) and 

terrain routing (rtout)

For the current three versions of the dataset we have: A 25-year (January 1993 through December 2017) retrospective simulation using version 1.2 of the National Water Model, a 26-year (January 1993 through December 2018) retrospective simulation using version 2.0 of the National Water Model and a 41-year (February 1979 through December 2020) retrospective simulation using version 2.1 of the National Water Model.


Learn more about the National Water Model: [http://water.noaa.gov/](http://water.noaa.gov/)

## Accessing NWM Reanalysis on AWS

The NWM Retrospective version 2.1 is stored in Zarr and NetCDF Formats in these S3 buckets:

noaa-nwm-retrospective-2-1-zarr-pds

noaa-nwm-retrospective-2-1-pds

Additional versions can also be found at https://registry.opendata.aws/nwm-archive/

The noaa-nwm-retro-v2.0-pds bucket contains the reanalysis archive organized by year starting
in 1993. The files are an internally compressed NetCDF format. They do
not need to be decompressed. Each file contains detailed metadata
describing the data stored within it.

You can use the AWS Command Line Interface to list a particular year
(2003 in this example) in the bucket like this:

`aws s3 ls s3://noaa-nwm-retro-v2.0-pds/full_physics/2003/ --no-sign-request`

`aws s3 ls nwm-archive/2003/ --no-sign-request`


or via a url constructed like this:
`https://noaa-nwm-retro-v2.0-pds.s3.amazonaws.com/?prefix=full_physics/2003`

`https://nwm-archive.s3.amazonaws.com/?prefix=2003`

Each year contains files for each hour of the year iterated over
different product types, not all products are published at hourly
intervals. The products types are listed in the table below.

  Product   Description                                                  Cycle            Example File Name
  --------- ------------------------------------------------------------ ---------------- ------------------------------------
  CHRTOUT   Streamflow values at points associated with flow lines       Every Hour       201701010000.CHRTOUT\_DOMAIN1.comp
  LAKEOUT   Output values at points associated with reservoirs (lakes)   Every Hour       201701010000.LAKEOUT\_DOMAIN1.comp
  LDASOUT   Land surface model output                                    Every 3rd Hour   201701010000.LDASOUT\_DOMAIN1.comp
  RTOUT     Ponded water and depth to soil saturation                    Every 3rd Hour   201701010000.RTOUT\_DOMAIN1.comp

Each product (data file) uses the following naming convention:
`yyyy/yyyymmddhhhh.product_DOMAIN1.comp` where:

-   `yyyy` year from 1993
-   `mm` month
-   `dd` day
-   `hhhh` hour of day
-   `product` (CHRTOUT, LAKEOUT, LDASOUT or RTOUT)
-   `DOMAIN1.comp` this is the same for all files

For example, to access the stream flow data for 12pm on May 1st 2003,
the key would be:

`2003/200305011200.CHRTOUT_DOMAIN1.comp`

To access the data, combine the key with the bucket name like this:

`s3://nwm-archive/2003/200305011200.CHRTOUT_DOMAIN1.comp`

or via HTTPS like this:

`https://nwm-archive.s3.amazonaws.com/2003/200305011200.CHRTOUT_DOMAIN1.com`

## File Contents for the NWM Retrospective Output Data Fields:

The dataset contains four products for each day. The four products are
listed below along with some of the parameters and properties of the
respective files. More details are available in the metadata contained
within each file:

**Channel Output in the CHRTOUT files (Point Type)**
| Variable Name | Description | Version |
| --- | --- | --- |
| elevation | Feature Elevation (m) | 2.1, 2.0 |
| streamflow | River Flow (m<sup>3</sup> s<sup>-1</sup>) | 2.1, 2.0, 1.2 |
| q_lateral | Total runoff into channel reach (m<sup>3</sup> s<sup>-1</sup>) | 2.1, 2.0, 1.2 |
| velocity | River velocity (m s<sup>-1</sup>) | 2.1, 2.0, 1.2 |
| qSfcLatRunoff | Runoff from terrain routing into channel (m<sup>3</sup> s<sup>-1</sup>) | 2.1, 2.0, 1.2 |
| qBucket | Flux from conceptual groundwater basin into channel (m<sup>3</sup> s<sup>-1</sup>) | 2.1, 2.0, 1.2 |
| qBtmVertRunoff | Runoff from bottom of soil column to conceptuals groundwater basin (m<sup>3</sup>) | 2.1, 2.0, 1.2 |

**Lake Output in the LAKEOUT files (Point Type)**
| Variable Name | Description | Version |
| --- | --- | --- |
| reservoir_type | 1= Level_pool, 2=USGS-persistence, 3=USACE-persistence, 4=RFC-forecasts | 2.1 |
| reservoir_assimilated_value | reservoir assimilated value | 2.1 |
| latitude | Lake latitude | 2.1, 2.0, 1.2 |
| longitude | Lake longitude | 2.1, 2.0, 1.2 |
| elevation | Water surface elevation (m) | 1.2 |
| water_sfc_elev | Water surface elevation | 2.1, 2.0, 1.2 |
| inflow | Lake inflow (m<sup>3</sup> s<sup>-1</sup>) | 2.1, 2.0, 1.2 |
| outflow | Lake outflow (m<sup>3</sup> s<sup>-1</sup>) | 2.1, 2.0, 1.2 |

**Cenceptual Nonlinear Groundwater Reservoir Output in the GWOUT files**
| Variable Name | Description | Version |
| --- | --- | --- |
| inflow | Conceptual Groundwater basin inflow | 2.1, 2.0 |
| outflow | Conceptual Groundwater basin outflow | 2.1, 2.0 |
| depth | Conceptual Groundwater basin storage depth | 2.1, 2.0 |

**Land Surface Output Variables in the LDASOUT files (Geospatial)**
| Variable Name | Description | Version |
| --- | --- | --- |
| COSZ | Cosine of zenith angle | 2.1, 2.0 |
| FSA | Total absorbed shortwave radiation (W m<sup>-2</sup>) | 2.1, 2.0, 1.2 |
| FIRA | Total net longwave radiation to atmosphere (W m<sup>-2</sup>) | 2.1, 2.0, 1.2 |
| HFX | Total sensible heat to atmosphere (W m<sup>-2</sup>) | 2.1, 2.0, 1.2 |
| LH | Total latet heat to the atmosphere (W m<sup>-2</sup>) | 2.1, 2.0, 1.2 |
| ALBEDO | Surface albedo | 2.1, 2.0 |
| UGDRNOFF | Accumulated underground runoff (mm) | 2.1, 2.0, 1.2 |
| TRAD | Surface radiative temperature (K) | 2.1, 2.0, 1.2 |
| SOIL_W | Liquid volumetric soil moisture (m<sup>3</sup> m<sup>-3</sup>) | 2.1, 2.0, 1.2 |
| SOIL_M | Volumetric soil moisture (liquid and frozen) (m<sup>3</sup> m<sup>-3</sup>) | 2.1, 2.0, 1.2 |
| SNOWH | Snow depth (m) | 2.1, 2.0, 1.2 |
| SNEQV | Snow water equivalent (kg m<sup>-2</sup>) | 2.1, 2.0, 1.2 |
| FSNO | Snow-cover fraction on the ground (fraction) | 2.1, 2.0, 1.2 |
| ACCET | Accumulated total ET (mm) | 2.1, 2.0, 1.2 |
| ALBSND | Snowpack direct-beam albedo | 2.1, 2.0 |
| ALBSNI | Snowpack diffuse-beam albedo | 2.1, 2.0 |
| EDIR | Direct evaporation flux from the surface | 2.1 |
| ACSNOM | Accumulated melting water out of snowpack bottom layer | 2.1 |
| QRAIN | Rate of liquid precipitation reaching the ground | 2.1 |
| QSNOW | Rate of frozen precipitation reaching the ground | 2.1 |

Note: For the two accumulation variables, UGDRNOFF and ACCET, the
accumulation takes place between pairs of dates: 1. 00Z January 1 -- 21Z
March 31 2. 00Z April 1 -- 21Z June 30 3. 00Z July 1 -- 21Z September 30
4. 00Z October 1 -- 21Z December 31

**Surface Terrain Routing Output Variables in the RTOUT files (Geospatial)**
| Variable Name | Description | Version |
| --- | --- | --- |
| Zwattablrt | Depth to saturation, rounded to the highest saturated layer (m)| 2.1, 2.0, 1.2 |
| sfcheadsubrt | Ponded water depth (mm) | 2.1, 2.0, 1.2 |

**NWM Forcing Inputs in the LDASIN files**
| Variable Name | Description | Version |
| --- | --- | --- |
| RAINRATE | Total Precipitation | 2.1 |
| T2D | Temperature | 2.1 |
| Q2D | Specific humidity | 2.1 |
| U2D | U-component of wind | 2.1 |
| V2D | V-component of wind | 2.1 |
| PSFC | Pressure | 2.1 |
| SWDOWN | Downward short-wave radiation flux | 2.1 |
| LWDOWN | Downward long-wave rad. flux | 2.1 |

## Document Updates

27th July 2018. Corrected the units of the following paramters: - ACCET
- from m to mm - qBucket - from m\^3\^ to m<sup>3</sup> s<sup>-1</sup> - qSfcLatRunoff -
from m\^3\^ to m<sup>3</sup> s<sup>-1</sup>

Please note that the metadata in the corresponding netCDF files may have
incorrect units for: - qBucket and qSfcLatRunoff.

The units listed above are the correct units.
