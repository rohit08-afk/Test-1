
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "description": "Supplier Readiness by Category Family",
  "data": {
    "name": "dataset"
  },
  "background": "transparent",
  "autosize": {
    "type": "pad",
    "contains": "padding"
  },
  "padding": 0,
  "spacing": 0,
  "transform": [
    {
      "calculate": "datum['Category Family']",
      "as": "Category"
    },
    {
      "calculate": "isValid(datum['Attendance Rate']) ? toNumber(datum['Attendance Rate']) : null",
      "as": "Supplier Rate"
    },
    {
      "calculate": "isValid(datum['Overall Attendance Rate']) ? toNumber(datum['Overall Attendance Rate']) : null",
      "as": "Overall Rate"
    }
  ],
  "vconcat": [
    {
      "width": 650,
      "height": 28,
      "data": {
        "values": [
          {"Stage": "S1 Reach", "x0": 170, "x1": 250, "Color": "#1555A3"},
          {"Stage": "S2 Acknowledge", "x0": 250, "x1": 410, "Color": "#07954B"},
          {"Stage": "S3 Commit", "x0": 410, "x1": 490, "Color": "#FFC21A"},
          {"Stage": "S4 Prove Capability", "x0": 490, "x1": 570, "Color": "#273F91"},
          {"Stage": "S5 Ready to Operate", "x0": 570, "x1": 650, "Color": "#08AFB2"}
        ]
      },
      "layer": [
        {
          "mark": {
            "type": "rect",
            "cornerRadius": 3
          },
          "encoding": {
            "x": {
              "field": "x0",
              "type": "quantitative",
              "scale": {"domain": [0, 650]},
              "axis": null
            },
            "x2": {"field": "x1"},
            "color": {
              "field": "Color",
              "type": "nominal",
              "scale": null,
              "legend": null
            }
          }
        },
        {
          "transform": [
            {
              "calculate": "(datum.x0 + datum.x1) / 2",
              "as": "Center"
            }
          ],
          "mark": {
            "type": "text",
            "fontSize": 9,
            "fontWeight": "bold",
            "align": "center",
            "baseline": "middle"
          },
          "encoding": {
            "x": {
              "field": "Center",
              "type": "quantitative",
              "scale": {"domain": [0, 650]},
              "axis": null
            },
            "text": {"field": "Stage"},
            "color": {
              "condition": {
                "test": "datum.Stage == 'S3 Commit'",
                "value": "#17365D"
              },
              "value": "#FFFFFF"
            }
          }
        }
      ]
    },
    {
      "width": 650,
      "height": 32,
      "data": {
        "values": [
          {"Label": "Category Family", "x0": 0, "x1": 170, "Color": "#F5F7FA"},
          {"Label": "Email Coverage", "x0": 170, "x1": 250, "Color": "#E5F2FF"},
          {"Label": "RO Attendance", "x0": 250, "x1": 330, "Color": "#E5F6EC"},
          {"Label": "Supplier Webinar Attendance", "x0": 330, "x1": 410, "Color": "#E5F6EC"},
          {"Label": "Commit", "x0": 410, "x1": 490, "Color": "#FFF6DD"},
          {"Label": "Prove Capability", "x0": 490, "x1": 570, "Color": "#E9EEFA"},
          {"Label": "Ready to Operate", "x0": 570, "x1": 650, "Color": "#E2F7F7"}
        ]
      },
      "layer": [
        {
          "mark": {
            "type": "rect",
            "stroke": "#DDE4EC",
            "strokeWidth": 0.5
          },
          "encoding": {
            "x": {
              "field": "x0",
              "type": "quantitative",
              "scale": {"domain": [0, 650]},
              "axis": null
            },
            "x2": {"field": "x1"},
            "color": {
              "field": "Color",
              "type": "nominal",
              "scale": null,
              "legend": null
            }
          }
        },
        {
          "transform": [
            {
              "calculate": "(datum.x0 + datum.x1) / 2",
              "as": "Center"
            }
          ],
          "mark": {
            "type": "text",
            "fontSize": 8,
            "fontWeight": "bold",
            "align": "center",
            "baseline": "middle",
            "color": "#17365D"
          },
          "encoding": {
            "x": {
              "field": "Center",
              "type": "quantitative",
              "scale": {"domain": [0, 650]},
              "axis": null
            },
            "text": {"field": "Label"}
          }
        }
      ]
    },
    {
      "width": 650,
      "height": {"step": 16},
      "transform": [
        {
          "calculate": "datum.Category",
          "as": "Row Category"
        },
        {
          "calculate": "datum['Supplier Rate'] == null ? '—' : format(datum['Supplier Rate'], '.0%')",
          "as": "Supplier Label"
        },
        {
          "calculate": "'100%'",
          "as": "Reach Label"
        },
        {
          "fold": [
            "Reach Label",
            "RO",
            "Supplier Label",
            "Commit",
            "Prove",
            "Ready"
          ],
          "as": ["Stage", "Value"]
        },
        {
          "calculate": "datum.Stage == 'Reach Label' ? 1 : datum.Stage == 'RO' ? 2 : datum.Stage == 'Supplier Label' ? 3 : datum.Stage == 'Commit' ? 4 : datum.Stage == 'Prove' ? 5 : 6",
          "as": "Stage Order"
        },
        {
          "calculate": "datum.Stage == 'Reach Label' ? '#E5F2FF' : datum.Stage == 'RO' || datum.Stage == 'Supplier Label' ? '#E5F6EC' : datum.Stage == 'Commit' ? '#FFF6DD' : datum.Stage == 'Prove' ? '#E9EEFA' : '#E2F7F7'",
          "as": "Cell Color"
        },
        {
          "calculate": "datum.Stage == 'Reach Label' ? '#20A56C' : datum.Stage == 'Supplier Label' ? '#FFBF3C' : '#BFC3C8'",
          "as": "Dot Color"
        },
        {
          "calculate": "datum.Stage == 'Reach Label' ? '100%' : datum.Stage == 'Supplier Label' ? datum['Supplier Label'] : '—'",
          "as": "Display Value"
        }
      ],
      "encoding": {
        "x": {
          "field": "Stage Order",
          "type": "ordinal",
          "sort": "ascending",
          "axis": null
        },
        "y": {
          "field": "Row Category",
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
            "xOffset": -18
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
            "xOffset": 9
          },
          "encoding": {
            "text": {
              "field": "Display Value"
            }
          }
        }
      ]
    },
    {
      "width": 650,
      "height": 20,
      "transform": [
        {
          "aggregate": [
            {
              "op": "max",
              "field": "Overall Rate",
              "as": "Overall Rate"
            }
          ]
        },
        {
          "calculate": "datum['Overall Rate'] == null ? '—' : format(datum['Overall Rate'], '.0%')",
          "as": "Total Supplier Label"
        },
        {
          "calculate": "'100%'",
          "as": "Reach Label"
        },
        {
          "fold": [
            "Reach Label",
            "RO",
            "Total Supplier Label",
            "Commit",
            "Prove",
            "Ready"
          ],
          "as": ["Stage", "Value"]
        },
        {
          "calculate": "datum.Stage == 'Reach Label' ? 1 : datum.Stage == 'RO' ? 2 : datum.Stage == 'Total Supplier Label' ? 3 : datum.Stage == 'Commit' ? 4 : datum.Stage == 'Prove' ? 5 : 6",
          "as": "Stage Order"
        },
        {
          "calculate": "datum.Stage == 'Reach Label' ? '#E5F2FF' : datum.Stage == 'RO' || datum.Stage == 'Total Supplier Label' ? '#E5F6EC' : datum.Stage == 'Commit' ? '#FFF6DD' : datum.Stage == 'Prove' ? '#E9EEFA' : '#E2F7F7'",
          "as": "Cell Color"
        },
        {
          "calculate": "datum.Stage == 'Reach Label' ? '#20A56C' : datum.Stage == 'Total Supplier Label' ? '#FFBF3C' : '#BFC3C8'",
          "as": "Dot Color"
        },
        {
          "calculate": "datum.Stage == 'Reach Label' ? '100%' : datum.Stage == 'Total Supplier Label' ? datum['Total Supplier Label'] : '—'",
          "as": "Display Value"
        }
      ],
      "encoding": {
        "x": {
          "field": "Stage Order",
          "type": "ordinal",
          "sort": "ascending",
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
            "xOffset": -18
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
            "xOffset": 9
          },
          "encoding": {
            "text": {
              "field": "Display Value"
            }
          }
        }
      ]
    }
  ],
  "resolve": {
    "scale": {
      "x": "independent"
    }
  },
  "config": {
    "view": {
      "stroke": null
    },
    "font": "Segoe UI"
  }
}
