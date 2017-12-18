# API
This repository gives information about the API to openCPU and the API to get metadata of a specific compendium.

---

# O2r-API
API for requesting and saving metadata of a specific compendium
The complete documentation can be found on the [o2r-webpage](http://o2r.info/o2r-web-api).

## Upload R package for execution in ocpu

### GET metadata

To upload a R package it is necessary to get the metadata of the choosen compendium. This will be handled by a GET request provided by the o2r-API.

`GET /api/v1/compendium/:id/`

This request will reply the metadata of the requested ID of the compendium.
More detailed information can be found [here](http://o2r.info/o2r-web-api/compendium/view/#view-single-compendium).


## PUT metadata

To save the needed data of the R package a PUT request is used provided by the o2r-API.

`PUT /api/v1/compendium/:id/metadata`

This request will reply the metadata of the requested ID of the compendium.
More detailed information can be found [here](http://o2r.info/o2r-web-api/compendium/metadata/).

### Request

```
metdata.o2r =>
{
  ...
  interaction:
  [
    {
  
      figure_id: STRING,
      type: "map",  // "map" or "timeseries" (fix)
      endpoint: STRING,
      widgets:
      [
        {
          type: "slider",  // (fix)
          default_value: NUMBER,
          min_value: NUMBER,
          max_value: NUMBER,
          param_name: STRING,
          steps_size: NUMBER,
          desciption: STRING
        },
        ...
      ]
    },
    ...
  ],
  ...
}
```

### Input parameters

- figure_id - {String} title of the figure, unique within the compendium metadata
- type - {STRING} type of the figure, fixed to be "map" or "timeseries"
- endpoint - {STRING} url to call function in openCPU
- widgets - {ARRAY} information to a specific widget of the figure
  - type - {STRING} type of the widget, fixed to be "slider"
  - default_value - {NUMBER} default value for the changed parameter
  - min_value - {NUMBER} minimum value for the changed parameter
  - max_value - {NUMBER} maximum value for the changed parameter
  - param_name - {NUMBER} name of the parameter
  - steps_size - {NUMBER} size of the steps
  - description - {STRING} additional description of the widget

---

# Ocpu-API
API for connection to openCPU

With this connection the endpoint to openCPU is provided. The platform cann get access to the openCPU library and more. 
Additional Information can be found [here](https://www.opencpu.org/api.html) at the site with HTTP API of openCPU.

## GET information

`GET /api/v1/ocpu/*`

This request will pass the URL `localhost/api/v1/ocpu/*` to the openCPU endpoint `localhost/ocpu/*`, 
where there is no changing funtionality compared to the [openCPU API page](https://www.opencpu.org/api.html).

## Example:

### Request

`GET /api/v1/ocpu/library/`

### Response

```
  list of libraries provided by openCPU
```
