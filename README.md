
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {
    "name": "dataset"
  },
  "transform": [
    {
      "calculate": "isValid(datum['Attended']) ? +datum['Attended'] : 0",
      "as": "Attended Count"
    },
    {
      "calculate": "isValid(datum['Not Attended']) ? +datum['Not Attended'] : 0",
      "as": "Not Attended Count"
    },
    {
      "calculate": "isValid(datum['Attended %']) ? (datum['Attended %'] <= 1 ? format(datum['Attended %'], '.0%') : format(datum['Attended %'], '.0f') + '%') : '—'",
      "as": "Rate Label"
    },
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
    }
  ],
  "spacing": 8,
  "hconcat": [
    {
      "width": 310,
      "height": {
        "step": 24
      },
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
          "field": "Count",
          "type": "quantitative",
          "stack": "zero",
          "axis": null
        },
        "order": {
          "field": "Sort Order",
          "type": "quantitative",
          "sort": "ascending"
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
                "symbolSize": 90
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
            "color": {
              "value": "#FFFFFF"
            },
            "text": {
              "field": "Count",
              "type": "quantitative",
              "format": ".0f"
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
      "transform": [
        {
          "filter": "datum['Attendance Status'] == 'Attended'"
        }
      ],
      "mark": {
        "type": "text",
        "fontSize": 12,
        "fontWeight": "bold",
        "color": "#17365D",
        "align": "center",
        "baseline": "middle"
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
