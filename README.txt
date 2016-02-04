This project was built by Colin Averill. It pairs soils data to FIA composition and growth data, and bins composition by plant mycorrhizal type. It is distinct from the FIA_Cstorage project in that it calculates tree growth, rather than just tree composition. It creates two growth and composition outputs- one for all observations in the FIA that match search criteria, and one for the subset of FIA data that have appropriate soils data. It takes advantage of code written by Trevor Andrews' "Empirical Successional Mapping" and Ryan Kelly's FIA database in PSQL format. Much of Trevor Andrew's original code was modified by Ryan Kelly so that it queried the PSQL FIA database hosted on the BU server. The "required_products_utilities" directory contains some utilities for PSQL to work in R, lists of PFTs and mycorrhizal types by FIA species codes, as well as .bil and .hdr files for PRISM climate products. "FIA_soils" contains the FIA soils products. 


The first script requires access to an FIA database. There's one on the BU server, or you can see Ryan Kelly's fia_psql project for more information on creating one:

  https://github.com/ryankelly-uiuc/fia_psql


Contents:
- FIA_soils
  - FIA soils database in .csv format (they are not very big)

-required_products_utilities
  - has PSQL_utils.R, which is a standalone version of some of PEcAn's DB tools.
  - has .bil and .hdr files for PRISM 30 year climate normals of temp and precip
  - has files that pair FIA species codes to PFTs and mycorrhizal types.
  
- Scripts
  - Sequential scripts to extract FIA data and filtering to isolate forested sites that have no evidence of past cutting/logging, and then calculate growth. Soils scripts calculates soil variables on an aerial basis. There is also a script to extract climate data from PRISM data products. 


GOALS:
- build a data set that has plot level total basa area, absolute basal area separated by myc type and PFT, and relative basal area of each PFT and myc type. 
- pair that with all the sites that have growth data. Bin growth data as total basal area increment at the plot scale, and then separate absolute basal area increment by PFT/myctype, and relative basal area increment by PFT and myc type. 
- finally merge in soils data for sites that have soils. 
-move on from data construction to data analysis.


CURRENT STATUS:
- Colin needs to choose the set of plot design codes that match our definition of 'forest'. Previously we only included design code 1 (which specifies this is gold standard totally just forest), however there are other design codes in the soils database that are certainly forested with extra information specifying its near a fucking lake or something. These are certainly chill. In the past I just took all the design codes in the soils database and said all of those were chill. However, there may be more codes that are chill that are not found in the soils database just because. I want these. Gotta figure out which they are. 

- I need to break the growth/abundance data into two scripts. One that incldues all sites, wheteher they have been remeasured or not. Grab most recent observation, characterize basal area as described above. Remove duplicates that are remeasurement observations.

- second data product that is remeasurement, from most recent remeasurement to newest. 

- pair growth data with newest observation standing basal area data.

- I think I can totally remove the GRM table, and use the previous diameter table avalues in the TREE table to move ahead. I don't care about trees per acre, only trees basal area. If I know plot size I can get TPA for the tree table.

- WHERE DO I FIND PLOT AREA??? Probably those damn designcd values. 