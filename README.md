# API
This repository gives information about the API to openCPU and the API to get metadata of a specific compendium.

---

# o2r-API
API for requesting metadata of a specific compendium
The complete documentation can be found on the [o2r-webpage](http://o2r.info/o2r-web-api).

## Get metadata

`GET /api/v1/compendium/:id/metadata`

This request will reply the metadata of the requested ID of the compendium.
More detailed information can be found [here](http://o2r.info/o2r-web-api/compendium/metadata/).

---

# ocpu-API
API for connection to openCPU

With this connection the endpoint to openCPU is provided. The platform cann get access to the openCPU library and more. 
Additional Information can be found [here](https://www.opencpu.org/api.html) at the site with HTTP API of openCPU.

## Get information

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
