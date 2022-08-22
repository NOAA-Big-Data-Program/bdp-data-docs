# Update to GHCN Prefixes
The NODD team is working on improving performance and access to the GHCNd data and will be implementing an updated prefix structure.  If you have questions, comments, or feedback, please reach out to nodd@noaa.gov with GHCN in the subject line.  
## Details
To expand and improve access to GHCNd data, the NODD team will be making these data available both by station and by year in three formats: csv.gz, csv, and parquet.  
The availability of GHCNd station data should facilitate longitudinal queries by stations or groups of stations without needing to access the entire dataset.  
The parquet files will be partitioned using Hive patterning either by station or by year and by GHCNd Element (variable measured).  This will facilitate parallel access, push-down filtering, and lazy loading.  
## New Structure:
noaa-ghcn-pds/
   csv.gz/
      by_station/
         station1.csv.gz
         station2.csv.gz
         ...
      by_year/
         ...
         2000.csv.gz
         2001.csv.gz
         ...
    csv/
      by_station/
         station1.csv
         station2.csv
         ...
      by_year/
         ...
         2000.csv
         2001.csv
         ...
    parquet/
      by_station/
         STATION=ID1/
            *.snappy.parquet
         STATION=ID2/
            *.snappy.parquet
         ...
      by_year/
         ...
         YEAR=2000/
            *.snappy.parquet
         YEAR=2001/
            *.snappy.parquet
         ...
