# Retrieve McClear clear sky solar radiation data

Retrieve McClear clear sky solar radiation data

## Usage

``` r
cams_get_mcclear(lat, lng, date_begin, date_end, time_step = "PT01H",
  alt = -999, verbose = FALSE)
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

- time_step:

  Aggregation: 'PT01M' for minutes, 'PT15M' for 15 minutes, 'PT01H' for
  hourly, 'P01D' for daily, 'P01M' for monthly. Deafult 'PT01H'

- alt:

  Altitude in meters, use -999 to let CAMS decide. Default -99

- verbose:

  TRUE for verbose output. Default "FALSE"

## Value

A data frame with requested solar data

## Examples

``` r
if (FALSE) { # \dontrun{
df <- cams_get_mcclear(
  lat=60, lng=15, date_begin="2016-01-01", date_end="2016-01-15")
print(head(df))
} # }
```
