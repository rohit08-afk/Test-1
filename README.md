
{
  "data": {"name": "dataset"},
  "transform": [
    {
      "calculate": "datum['Attended'] + datum['Not Attended']",
      "as": "Total"
    },
    {
      "calculate": "datum['Attended %'] <= 1 ? format(datum['Attended %'], '.0%') : format(datum['Attended %'], '.0f') + '%'",
      "as": "Rate Label"
    }
  ],
  "spacing": 8,
  "hconcat": [
    {
      "width": 340,
      "height": {"step": 38},
      "transform": [
        {
          "fold": ["Attended", "Not Attended"],
          "as": ["Status", "Count"]
        }
      ],
      "mark": {
        "type": "bar",
        "height": 23
      },
      "encoding": {
        "y": {
          "field": "Category Family",
          "type": "nominal",
          "sort": "ascending",
          "axis": {
            "title": null,
            "labelFontSize": 11,
            "labelLimit": 150,
            "ticks": false,
            "domain": false
          }
        },
        "x": {
          "field": "Count",
          "type": "quantitative",
          "stack": "zero",
          "axis": {
            "title": null,
            "grid": false
          }
        },
        "color": {
          "field": "Status",
          "type": "nominal",
          "scale": {
            "domain": ["Attended", "Not Attended"],
            "range": ["#16A085", "#F28C45"]
          },
          "legend": {
            "orient": "top",
            "title": null
          }
        },
        "order": {
          "field": "Status",
          "sort": "ascending"
        },
        "tooltip": [
          {"field": "Category Family"},
          {"field": "Status"},
          {"field": "Count"}
        ]
      }
    },
    {
      "width": 65,
      "height": {"step": 38},
      "mark": {
        "type": "text",
        "fontSize": 13,
        "fontWeight": "bold",
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
