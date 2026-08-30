# API client for [CAMS radiation service](http://www.soda-pro.com/web-services/radiation/cams-radiation-service)

API client for [CAMS radiation
service](http://www.soda-pro.com/web-services/radiation/cams-radiation-service)

## Usage

``` r
cams_api(lat, lng, date_begin, date_end, alt = -999,
  time_step = "PT01H", time_ref = "UT", verbose = FALSE,
  service = "get_cams_radiation", format = "application/csv",
  filename = "")
```

## Arguments

- lat:

  Latitude, in decimal degrees. Required

- lng:

  Longitude, in decimal degrees. Required

- date_begin:

  Start date as 'yyyy-mm-dd' string. Required

- date_end:

  End date as 'yyyy-mm-dd' string. Required

- alt:

  Altitude in meters, use -999 to let CAMS decide. Default -99

- time_step:

  Aggregation: 'PT01M' for minutes, 'PT15M' for 15 minutes, 'PT01H' for
  hourly, 'P01D' for daily, 'P01M' for monthly. Deafult 'PT01H'

- time_ref:

  Time reference:'UT' for universal time, 'TST' for true solar time.
  Default 'UT'

- verbose:

  TRUE for verbose output. Default "FALSE"

- service:

  'get_mcclear' for CAMS McClear data, 'get_cams_radiation' for CAMS
  radiation data. Default 'get_cams_radiation'

- format:

  'application/csv', 'application/json', 'application/x-netcdf' or
  'text/csv'. Default 'application/csv'

- filename:

  path to file on disk to write to. If empty, data is kept in memory.
  Default empty

## Value

list(ok=TRUE/FALSE, response=response). If ok=TRUE, response is the
response from httr::GET. If ok=FALSE, response holds exception text

## Examples

``` r
if (FALSE) { # \dontrun{
library(ncdf4)

filename <- paste0(tempfile(), ".nc")

# API call to CAMS
r <- cams_api(
  60, 15,                       # latitude=60, longitude=15
  "2016-06-01", "2016-06-10",   # for 2016-06-01 to 2016-06-10
  time_step="PT01H",            # hourly data
  service="get_cams_radiation", # CAMS radiation
  format="application/x-netcdf",# netCDF format
  filename=filename)            # file to save to

# Access the on disk stored ncdf4 file
nc <- nc_open(filename)
# list names of available variables
names(nc$var)

# create data.frame with timestamp and global horizontal irradiation
df <- data.frame(datetime=as.POSIXct(nc$dim$time$vals, "UTC",
                                     origin="1970-01-01"),
                 GHI = ncvar_get(nc, "GHI"))

plot(df, type="l")

nc_close(nc)
} # }
```
