# API
This repository gives information about the API to openCPU and the API to save and get metadata.

---

# Metadata API
API for connection to the database for getting data of the last session to rerun and for saving data to the database.

## GET session

### Request

`GET /api/v1/interactivegp/:id/metadata/:figure_id/:session_id`

### Response

```
200 OK

{
  "session_id": "String",
  "param_values": { //name & values of parameters sent to openCPU, resulting in this result
      "x": "numeric",
      "y": "numeric" 
}
```

### URL parameters for session

- `id` - if of the compendium in which a manipulation with interactive figures has been made
- `figure_id` - id of the figure that has been manipulated
- `session_id` - id of the session to identify this special manipulation

## SAVE session

### Request

`POST /api/v1/interactivegp/:id/metadata/:figure_id`

input of request-body
```
{
  "param_values": {
      "x": "numeric",
      "y": "numeric" 
}
```

### Request body properties

- `param_values` - parameters that can be manipulated in an interactive figure
- `x` - for example the x-Axis of a timeseries plot
- `y` - for example the y-Axis of a timeseries plot

### Response

```
201 CREATED

{
  "id": "String",
}
```

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

´´´
  list of libraries provided by openCPU
´´´
