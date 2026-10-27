
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {"name": "dataset"},
  "background": "transparent",
  "spacing": 14,
  "transform": [
    {
      "calculate": "datum['GL1 Webinar Attended'] == null ? 0 : datum['GL1 Webinar Attended']",
      "as": "Attended"
    },
    {
      "calculate": "datum['GL1 Webinar Not Attended'] == null ? 0 : datum['GL1 Webinar Not Attended']",
      "as": "Not Attended"
    },
    {
      "calculate": "datum['Suppliers in scope'] == null ? 0 : datum['Suppliers in scope']",
      "as": "Total"
    },
    {
      "calculate": "datum['Attendance Rate'] == null ? 0 : datum['Attendance Rate']",
      "as": "Rate"
    },
    {
      "calculate": "format(datum.Rate, '.0%')",
      "as": "Rate Label"
    },
    {
      "fold": ["Attended", "Not Attended"],
      "as": ["Status", "Count"]
    }
  ],
  "hconcat": [
    {
      "width": 360,
      "height": {"step": 34},
      "layer": [
        {
          "mark": {"type": "bar", "height": 18},
          "encoding": {
            "y": {
              "field": "Category Family",
              "type": "nominal",
              "sort": null,
              "axis": {
                "title": null,
                "labelFontSize": 11,
                "labelLimit": 180,
                "ticks": false,
                "domain": false
              }
            },
            "x": {
              "field": "Count",
              "type": "quantitative",
              "stack": "zero",
              "axis": null
            },
            "color": {
              "field": "Status",
              "type": "nominal",
              "scale": {
                "domain": ["Attended", "Not Attended"],
                "range": ["#16A085", "#F28C45"]
              },
              "legend": {
                "title": null,
                "orient": "top",
                "direction": "horizontal"
              }
            },
            "order": {
              "field": "Status",
              "sort": "ascending"
            },
            "tooltip": [
              {"field": "Category Family"},
              {"field": "Status"},
              {"field": "Count", "format": ",.0f"}
            ]
          }
        },
        {
          "mark": {
            "type": "text",
            "fontSize": 10,
            "color": "white"
          },
          "encoding": {
            "y": {
              "field": "Category Family",
              "type": "nominal",
              "sort": null
            },
            "x": {
              "field": "Count",
              "type": "quantitative",
              "stack": "zero"
            },
            "detail": {"field": "Status"},
            "text": {
              "condition": {
                "test": "datum.Count > 0",
                "field": "Count",
                "format": ".0f"
              },
              "value": ""
            },
            "order": {
              "field": "Status",
              "sort": "ascending"
            }
          }
        }
      ]
    },
    {
      "width": 85,
      "height": {"step": 34},
      "transform": [
        {
          "aggregate": [{"op": "max", "field": "Total", "as": "Total"}],
          "groupby": ["Category Family"]
        }
      ],
      "title": {
        "text": "Total Suppliers",
        "fontSize": 11,
        "color": "#315B85"
      },
      "mark": {"type": "text", "fontSize": 12},
      "encoding": {
        "y": {
          "field": "Category Family",
          "type": "nominal",
          "sort": null,
          "axis": null
        },
        "text": {"field": "Total", "format": ",.0f"}
      }
    },
    {
      "width": 95,
      "height": {"step": 34},
      "transform": [
        {
          "aggregate": [{"op": "max", "field": "Rate", "as": "Rate"}],
          "groupby": ["Category Family"]
        }
      ],
      "title": {
        "text": "Attendance Rate",
        "fontSize": 11,
        "color": "#315B85"
      },
      "mark": {"type": "text", "fontSize": 12},
      "encoding": {
        "y": {
          "field": "Category Family",
          "type": "nominal",
          "sort": null,
          "axis": null
        },
        "text": {"field": "Rate", "format": ".0%"}
      }
    }
  ],
  "resolve": {"scale": {"y": "shared"}},
  "config": {
    "view": {"stroke": null},
    "axis": {"grid": false},
    "font": "Segoe UI"
  }
}
