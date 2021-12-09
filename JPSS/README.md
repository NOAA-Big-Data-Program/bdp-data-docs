Data from NOAA Joint Polar Satellites (JPSS) is availble on Amazon S3. Satellites in the JPSS constellation gather global measurements of atmospheric, terrestrial and oceanic conditions, including sea and land surface temperatures, vegetation, clouds, rainfall, snow and ice cover, fire locations and smoke plumes, atmospheric temperature, water vapor and ozone. JPSS delivers key observations for the Nation's essential products and services, including forecasting severe weather like hurricanes, tornadoes and blizzards days in advance, and assessing environmental hazards such as droughts, forest fires, poor air quality and harmful coastal waters. Further, JPSS will provide continuity of critical, global observations of Earth’s atmosphere, oceans and land through 2038.

This page includes information on data structure; you can find [more detailed information about JPSS Series data from NOAA](http://www.jpss.noaa.gov/).

Examples of how to access the objects via the AWS CLI can be seen below.

`aws s3 ls noaa-jpss --no-sign-request`

`aws s3 cp s3://noaa-jpss/<Satellite>/<Instrument>/<Product>/<Year>/<Month>/<Day>/<Filename> . --no-sign-request`
