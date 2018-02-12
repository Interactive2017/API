# API

This repository gives information about the API to openCPU.

# Ocpu-API
API for connection to openCPU

With this connection the endpoint to openCPU is provided. The platform can get access to the openCPU library and will be able to run R scripts. 
Additional Information can be found [here](https://www.opencpu.org/api.html) at the site with HTTP API of openCPU.

## Run script

`POST /api/v1/ocpu/library/:id/R/run*`

Request parameter

- `id` - id of the ERC

This request will pass the URL `localhost/api/v1/ocpu/*` to the openCPU endpoint `localhost/ocpu/*`.
The id of the ERC has to be provided by the user. Then openCPU will run the R script of the package (that has the same name), to calculate the original data of the package. This original data will be saved to the metadata of the given ERC.

## Example:

### Request (for timeseries)

`POST /api/v1/ocpu/library/t5UH3/R/run`

Request body parameters for executing R script

```json
{
 x: 2.7
}
```

- `x` parameter that has been changed (with value)

### Response

Response after running openCPU

```json
{
 ...
 data: "/ocpu/tmp/x07acffa77a/R/run\n/ocpu/tmp/x07acffa77a/R/.val\n/ocpu/tmp/x07acffa77a/graphics/1\n/ocpu/tmp/x07acffa77a/stdout\n/ocpu/tmp/x07acffa77a/source\n/ocpu/tmp/x07acffa77a/console\n/ocpu/tmp/x07acffa77a/info\n/ocpu/tmp/x07acffa77a/files/DESCRIPTION\n"
 ...
}
```

- `data` - String containing URLs to retrieve information of the calculation from openCPU

### Request (for maps)

`POST /api/v1/ocpu/library/z5jF9/R/run`

Request body parameters for executing R script

```json
{
 y: 2001
}
```

- `y` parameter that has been changed (with value)

### Response

Response after running openCPU

```json
{
 ...
 data: "/ocpu/tmp/x05b16d5b4d/R/run2\n/ocpu/tmp/x05b16d5b4d/R/.val\n/ocpu/tmp/x05b16d5b4d/graphics/1\n/ocpu/tmp/x05b16d5b4d/stdout\n/ocpu/tmp/x05b16d5b4d/source\n/ocpu/tmp/x05b16d5b4d/console\n/ocpu/tmp/x05b16d5b4d/info\n/ocpu/tmp/x05b16d5b4d/files/DESCRIPTION\n/ocpu/tmp/x05b16d5b4d/files/figure1.Rdata\n"
 ...
}
```

- `data` - String containing URLs to retrieve information of the calculation from openCPU

## Get result

### Request (for timeseries)

`/ocpu/tmp/ + tempId + /R/.val/json`

Request parameters

- `tempId` - id of the openCPU calculation (which is retrieved by the run script POST request)

### Response

```json
{
 ...
 data: [
  [
    {
    	PANEL: 1,
	colour: "black",
	group: 1,
	linetype: "solid",
	size: 1,
	x: 1,
	y: 0.8631,
    },
    ...
  ]
 ]
 ...
}
```

- `data` - an array containing at first place (`data[0]`) an array with timeseries plot data

### Request (for maps)

`/ocpu/tmp/ + tempId + /graphics/1/png`

Request parameters

- `tempId` - id of the openCPU calculation (which is retrieved by the run script POST request)

### Response

```json
{
 ...
 config: {
  ...
  url: "http://localhost/api/v1/ocpu/tmp/x05b16d5b4d/graphics/1/png"
  ...
 }
 ...
}
```

- `config`
 - `url` - url to retrieve the calculated map as png

