
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {
    "name": "dataset"
  },
  "transform": [
    {
      "calculate": "isValid(datum['Webinar Attended']) ? +datum['Webinar Attended'] : 0",
      "as": "Attended Count"
    },
    {
      "calculate": "isValid(datum['Webinar Not Attended']) ? +datum['Webinar Not Attended'] : 0",
      "as": "Not Attended Count"
    },
    {
      "calculate": "datum['Attended Count'] + datum['Not Attended Count']",
      "as": "Calculated Total"
    },
    {
      "calculate": "isValid(datum['Suppliers in scope']) ? +datum['Suppliers in scope'] : datum['Calculated Total']",
      "as": "Supplier Total"
    },
    {
      "calculate": "datum['Calculated Total'] > 0 ? format(datum['Attended Count'] / datum['Calculated Total'], '.0%') : '0%'",
      "as": "Rate Label"
    }
  ],
  "spacing": 3,
  "hconcat": [
    {
      "width": 150,
      "height": {
        "step": 13
      },
      "transform": [
        {
          "fold": [
            "Attended Count",
            "Not Attended Count"
          ],
          "as": [
            "Status",
            "Count"
          ]
        },
        {
          "calculate": "datum.Status == 'Attended Count' ? 'Attended' : 'Not Attended'",
          "as": "Attendance Status"
        },
        {
          "calculate": "datum.Status == 'Attended Count' ? 0 : 1",
          "as": "Sort Order"
        },
        {
          "stack": "Count",
          "groupby": [
            "Category Family"
          ],
          "sort": [
            {
              "field": "Sort Order",
              "order": "ascending"
            }
          ],
          "as": [
            "x0",
            "x1"
          ]
        },
        {
          "calculate": "(datum.x0 + datum.x1) / 2",
          "as": "Label Midpoint"
        }
      ],
      "encoding": {
        "y": {
          "field": "Category Family",
          "type": "nominal",
          "sort": "ascending",
          "axis": {
            "title": null,
            "labelFontSize": 8,
            "labelLimit": 115,
            "ticks": false,
            "domain": false,
            "labelPadding": 3
          }
        },
        "x": {
          "field": "x1",
          "type": "quantitative",
          "axis": null,
          "scale": {
            "zero": true
          }
        },
        "tooltip": [
          {
            "field": "Category Family",
            "type": "nominal"
          },
          {
            "field": "Attendance Status",
            "type": "nominal"
          },
          {
            "field": "Count",
            "type": "quantitative",
            "format": ".0f"
          }
        ]
      },
      "layer": [
        {
          "mark": {
            "type": "bar",
            "height": 8
          },
          "encoding": {
            "x2": {
              "field": "x0"
            },
            "color": {
              "field": "Attendance Status",
              "type": "nominal",
              "scale": {
                "domain": [
                  "Attended",
                  "Not Attended"
                ],
                "range": [
                  "#16A085",
                  "#F28C45"
                ]
              },
              "legend": {
                "orient": "top",
                "title": null,
                "labelFontSize": 8,
                "symbolSize": 50,
                "offset": 2
              }
            }
          }
        },
        {
          "mark": {
            "type": "text",
            "fontSize": 8,
            "fontWeight": "normal",
            "align": "center",
            "baseline": "middle"
          },
          "encoding": {
            "x": {
              "field": "Label Midpoint",
              "type": "quantitative"
            },
            "text": {
              "field": "Count",
              "type": "quantitative",
              "format": ".0f"
            },
            "color": {
              "value": "#000000"
            },
            "opacity": {
              "condition": {
                "test": "datum.Count > 0",
                "value": 1
              },
              "value": 0
            }
          }
        }
      ]
    },
    {
      "width": 45,
      "height": {
        "step": 13
      },
      "mark": {
        "type": "text",
        "fontSize": 9,
        "fontWeight": "bold",
        "align": "center",
        "baseline": "middle",
        "color": "#17365D"
      },
      "encoding": {
        "y": {
          "field": "Category Family",
          "type": "nominal",
          "sort": "ascending",
          "axis": null
        },
        "text": {
          "field": "Supplier Total",
          "type": "quantitative",
          "format": ".0f"
        }
      },
      "title": {
        "text": "Total Suppliers",
        "fontSize": 9,
        "fontWeight": "bold",
        "color": "#17365D"
      }
    },
    {
      "width": 45,
      "height": {
        "step": 13
      },
      "mark": {
        "type": "text",
        "fontSize": 9,
        "fontWeight": "bold",
        "align": "center",
        "baseline": "middle",
        "color": "#17365D"
      },
      "encoding": {
        "y": {
          "field": "Category Family",
          "type": "nominal",
          "sort": "ascending",
          "axis": null
        },
        "text": {
          "field": "Rate Label",
          "type": "nominal"
        }
      },
      "title": {
        "text": "Attendance Rate",
        "fontSize": 9,
        "fontWeight": "bold",
        "color": "#17365D"
      }
    }
  ],
  "resolve": {
    "scale": {
      "y": "shared"
    }
  },
  "config": {
    "view": {
      "stroke": null
    },
    "background": "transparent"
  }
}
