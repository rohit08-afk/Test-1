
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {
    "name": "dataset"
  },
  "transform": [
    {
      "calculate": "isValid(datum['GL1 Webinar Attended']) ? +datum['GL1 Webinar Attended'] : 0",
      "as": "Attended Count"
    },
    {
      "calculate": "isValid(datum['GL1 Webinar Not Attended']) ? +datum['GL1 Webinar Not Attended'] : 0",
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
  "spacing": 5,
  "hconcat": [
    {
      "width": 230,
      "height": {
        "step": 24
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
            "labelFontSize": 10,
            "labelLimit": 145,
            "ticks": false,
            "domain": false,
            "labelPadding": 5
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
            "height": 16
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
                "labelFontSize": 10,
                "symbolSize": 90,
                "offset": 2
              }
            }
          }
        },
        {
          "mark": {
            "type": "text",
            "fontSize": 11,
            "fontWeight": "bold",
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
              "value": "#FFFFFF"
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
      "width": 55,
      "height": {
        "step": 24
      },
      "mark": {
        "type": "text",
        "fontSize": 12,
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
        "fontSize": 11,
        "fontWeight": "bold",
        "color": "#17365D"
      }
    },
    {
      "width": 55,
      "height": {
        "step": 24
      },
      "mark": {
        "type": "text",
        "fontSize": 12,
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
        "fontSize": 11,
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
