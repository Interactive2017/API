# API
This repository gives information about the API to openCPU and the API to save and get metadata.

---

# Metadata API
API for connection to the database for getting data of the last session to rerun and for saving data to the database.

## GET figure

### Request

`GET /api/v1/interactivegp/:id/:figure_id`

### Response

```
200 OK

{
  "figure_id": "String",
  "type": "timeseries/map",
  "widgets": [
      {
          "type": "slider",
          "default_value": "numeric",
          "min_value": "numeric",
          "max_value": "numeric",
          "param_name": "String",
          "steps_size": "numeric",
          "description": "String"
      }
  ],
  "original": "path/to/original/image",
  "endpoint": "openCPU/link/for/function",
  "results": [
      {
          "session_id": "String",
          "param_values": {
              "x": "numeric",
              "y": "numeric" 
          },
          "graphic": "link/to/the/resulting/image",
          "object": "Object"
          "endpoints": []
      }
  ]
}
```

### URL parameters for figure

- `id` - if of the compendium in which a manipulation with interactive figures has been made
- `figure_id` - id of the figure that has been manipulated

## POST figure

### Request

`POST /api/v1/interactivegp`

input of request-body
```
{
  "id": "compendium_id",
  "figure": "figure_id",
  "data": {
    "figure_id": "String",
    "type": "timeseries/map",
    "widgets": [
        {
            "type": "slider",
            "default_value": "numeric",
            "min_value": "numeric",
            "max_value": "numeric",
            "param_name": "String", //name of the parameter in R function
            "steps_size": "numeric",
            "description": "String" //caption of the slider
        }
    ],
    "original": "path/to/original/image",
    "endpoint": "openCPU/link/for/function",
    "results": [
        {
            "session_id": "String",
            "param_values": {
                "x": "numeric",
                "y": "numeric" 
            },
            "graphic": "link/to/the/resulting/image",
            "object": "Object",
            "endpoints": []
        }
    ]
  }
}
```

### Request body properties
- `data` - object of figure data
  - `figure_id` - id of the figure that was manipulated
  - `type` - type of figure
  - `widgets` - type of interaction possibilities
    - `type` - type of the widget
    - `default_value` - default value of the widget
    - `min_value` - minimum value of the widget
    - `max_value` - maximum value of the widget
    - `param_name` - name of the parameter in R function
    - `steps_size` - 
    - `description` - caption of the widget
  - `original` - original path of the image
  - `endpoint` - openCPU link for the figure/computation
  - `results` - see save session

### Response

```
201 CREATED

{
  "id": "figure_id",
}
```

## GET session

### Request

`GET /api/v1/interactivegp/:id/:figure_id/:session_id`

### Response

```
200 OK
{
  "figureData": {
      "figure_id": "String",
      "type": "timeseries/map",
      "widgets": [
          {
              "type": "slider",
              "default_value": "numeric",
              "min_value": "numeric",
              "max_value": "numeric",
              "param_name": "String",
              "steps_size": "numeric",
              "description": "String"
          }
      ],
      "original": "path/to/original/image",
      "endpoint": "openCPU/link/for/function"
  }
  "sessionData": {
      "session_id": "session_id",
      "param_values": {
          "x": "numeric",
          "y": "numeric" 
      },
      "graphic": "link/to/the/resulting/image",
      "object": "Object"
      "endpoints": []
  }
}
```

### URL parameters for session

- `id` - if of the compendium in which a manipulation with interactive figures has been made
- `figure_id` - id of the figure that has been manipulated
- `session_id` - id of the session to identify this special manipulation

## POST session

### Request

`POST /api/v1/interactivegp`

input of request-body
```
{
  "id": "compendium_id",
  "figure": "figure_id",
  "data": {
    "session": "session_id",
    "param_values": {
        "x": "numeric",
        "y": "numeric" 
    "graphic": "link/to/the/resulting/image",
    "object": "Object",
    "endpoints": []
  }
}
```

### Request body properties

- `data` - object of session data
  - `session` - id of session, provided by openCPU
  - `param_values` - parameters that can be manipulated in an interactive figure
    - `x` - for example the x-Axis of a timeseries plot
    - `y` - for example the y-Axis of a timeseries plot
  - `graphic` - (optional) link to the resulting image
  - `object` - (optional) returned object from openCPU (.val)
  - `endpoints` - array of links to the results of the execution of the script

### Response

```
201 CREATED

{
  "id": "session_id",
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

```
  list of libraries provided by openCPU
```
