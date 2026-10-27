
Overall Attendance Rate =
CALCULATE(
    [Attendance Rate],
    REMOVEFILTERS('GL1 Webinar Measures'[Category Family])
)



{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {"name": "dataset"},
  "background": "transparent",
  "spacing": 2,
  "transform": [
    {
      "calculate": "datum['Category Family']",
      "as": "Category"
    },
    {
      "calculate": "isValid(datum['Attendance Rate']) ? datum['Attendance Rate'] : 0",
      "as": "Supplier Rate"
    },
    {
      "calculate": "isValid(datum['Overall Attendance Rate']) ? datum['Overall Attendance Rate'] : 0",
      "as": "Overall Rate"
    }
  ],
  "vconcat": [
    {
      "width": {"step": 75},
      "height": 30,
      "data": {
        "values": [
          {"Stage": "Reach", "Order": 1, "Heading": "S1 Reach", "Color": "#1555A3"},
          {"Stage": "RO Readiness", "Order": 2, "Heading": "S2 RO", "Color": "#07954B"},
          {"Stage": "Supplier", "Order": 3, "Heading": "S2 Supplier", "Color": "#07954B"},
          {"Stage": "Commit", "Order": 4, "Heading": "S3 Commit", "Color": "#FFC21A"},
          {"Stage": "Prove", "Order": 5, "Heading": "S4 Prove", "Color": "#273F91"},
          {"Stage": "Ready", "Order": 6, "Heading": "S5 Ready", "Color": "#08AFB2"}
        ]
      },
      "encoding": {
        "x": {
          "field": "Stage",
          "type": "ordinal",
          "sort": ["Reach", "RO Readiness", "Supplier", "Commit", "Prove", "Ready"],
          "axis": null
        }
      },
      "layer": [
        {
          "mark": {"type": "rect", "cornerRadius": 3},
          "encoding": {
            "color": {
              "field": "Color",
              "type": "nominal",
              "scale": null,
              "legend": null
            }
          }
        },
        {
          "mark": {
            "type": "text",
            "fontSize": 9,
            "fontWeight": "bold",
            "color": "white"
          },
          "encoding": {
            "text": {"field": "Heading"}
          }
        }
      ]
    },
    {
      "width": {"step": 75},
      "height": {"step": 16},
      "transform": [
        {"calculate": "'100%'", "as": "Reach"},
        {"calculate": "'-'", "as": "RO Readiness"},
        {
          "calculate": "format(datum['Supplier Rate'], '.0%')",
          "as": "Supplier"
        },
        {"calculate": "'-'", "as": "Commit"},
        {"calculate": "'-'", "as": "Prove"},
        {"calculate": "'-'", "as": "Ready"},
        {
          "fold": ["Reach", "RO Readiness", "Supplier", "Commit", "Prove", "Ready"],
          "as": ["Stage", "Value"]
        },
        {
          "calculate": "datum.Stage == 'Reach' ? '#E5F2FF' : datum.Stage == 'RO Readiness' || datum.Stage == 'Supplier' ? '#E5F6EC' : datum.Stage == 'Commit' ? '#FFF6DD' : datum.Stage == 'Prove' ? '#E9EEFA' : '#E2F7F7'",
          "as": "Cell Color"
        },
        {
          "calculate": "datum.Stage == 'Reach' ? '#20A56C' : datum.Stage == 'Supplier' ? '#F05252' : '#BFC3C8'",
          "as": "Dot Color"
        }
      ],
      "encoding": {
        "x": {
          "field": "Stage",
          "type": "ordinal",
          "sort": ["Reach", "RO Readiness", "Supplier", "Commit", "Prove", "Ready"],
          "axis": null
        },
        "y": {
          "field": "Category",
          "type": "nominal",
          "sort": "ascending",
          "axis": {
            "title": null,
            "labelFontSize": 8,
            "labelLimit": 165,
            "labelPadding": 4,
            "ticks": false,
            "domain": false
          }
        }
      },
      "layer": [
        {
          "mark": {
            "type": "rect",
            "stroke": "#DDE4EC",
            "strokeWidth": 0.4
          },
          "encoding": {
            "color": {
              "field": "Cell Color",
              "type": "nominal",
              "scale": null,
              "legend": null
            }
          }
        },
        {
          "mark": {
            "type": "circle",
            "size": 35,
            "xOffset": -19
          },
          "encoding": {
            "color": {
              "field": "Dot Color",
              "type": "nominal",
              "scale": null,
              "legend": null
            }
          }
        },
        {
          "mark": {
            "type": "text",
            "fontSize": 8,
            "fontWeight": "normal",
            "color": "#17365D",
            "xOffset": 7
          },
          "encoding": {
            "text": {"field": "Value"}
          }
        }
      ]
    },
    {
      "width": {"step": 75},
      "height": 19,
      "transform": [
        {
          "aggregate": [
            {"op": "max", "field": "Overall Rate", "as": "Overall Rate"}
          ]
        },
        {"calculate": "'100%'", "as": "Reach"},
        {"calculate": "'-'", "as": "RO Readiness"},
        {
          "calculate": "format(datum['Overall Rate'], '.0%')",
          "as": "Supplier"
        },
        {"calculate": "'-'", "as": "Commit"},
        {"calculate": "'-'", "as": "Prove"},
        {"calculate": "'-'", "as": "Ready"},
        {
          "fold": ["Reach", "RO Readiness", "Supplier", "Commit", "Prove", "Ready"],
          "as": ["Stage", "Value"]
        },
        {
          "calculate": "datum.Stage == 'Reach' ? '#E5F2FF' : datum.Stage == 'RO Readiness' || datum.Stage == 'Supplier' ? '#E5F6EC' : datum.Stage == 'Commit' ? '#FFF6DD' : datum.Stage == 'Prove' ? '#E9EEFA' : '#E2F7F7'",
          "as": "Cell Color"
        },
        {
          "calculate": "datum.Stage == 'Reach' ? '#20A56C' : datum.Stage == 'Supplier' ? '#F05252' : '#BFC3C8'",
          "as": "Dot Color"
        }
      ],
      "encoding": {
        "x": {
          "field": "Stage",
          "type": "ordinal",
          "sort": ["Reach", "RO Readiness", "Supplier", "Commit", "Prove", "Ready"],
          "axis": null
        }
      },
      "layer": [
        {
          "mark": {
            "type": "rect",
            "stroke": "#DDE4EC",
            "strokeWidth": 0.5
          },
          "encoding": {
            "color": {
              "field": "Cell Color",
              "type": "nominal",
              "scale": null,
              "legend": null
            }
          }
        },
        {
          "mark": {
            "type": "circle",
            "size": 35,
            "xOffset": -19
          },
          "encoding": {
            "color": {
              "field": "Dot Color",
              "type": "nominal",
              "scale": null,
              "legend": null
            }
          }
        },
        {
          "mark": {
            "type": "text",
            "fontSize": 9,
            "fontWeight": "bold",
            "color": "#17365D",
            "xOffset": 7
          },
          "encoding": {
            "text": {"field": "Value"}
          }
        }
      ]
    }
  ],
  "resolve": {
    "scale": {"x": "shared"}
  },
  "config": {
    "view": {"stroke": null},
    "font": "Segoe UI"
  }
}
