
RO Overall Completion % =
VAR TotalTopics = 4
VAR CompletedROTopics =
    SUMX(
        VALUES('GL1 RO Attendance Mapping'[RO]),
        VAR CurrentRO = 'GL1 RO Attendance Mapping'[RO]
        RETURN
            CALCULATE(
                DISTINCTCOUNT('GL1 RO Session Attendance unique'[Topic]),
                'GL1 RO Session Attendance unique'[Attended] = 1,
                TREATAS(
                    {CurrentRO},
                    'GL1 RO Session Attendance unique'[RO]
                )
            )
    )
RETURN
    DIVIDE(
        CompletedROTopics,
        [Total ROs] * TotalTopics,
        0
    )





{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {
    "name": "dataset"
  },
  "background": "transparent",
  "spacing": 8,
  "transform": [
    {
      "calculate": "isValid(datum['RO Attended']) ? +datum['RO Attended'] : 0",
      "as": "Attended Count"
    },
    {
      "calculate": "isValid(datum['RO Not Attended']) ? +datum['RO Not Attended'] : 0",
      "as": "Not Attended Count"
    },
    {
      "calculate": "isValid(datum['Total ROs']) ? +datum['Total ROs'] : datum['Attended Count'] + datum['Not Attended Count']",
      "as": "RO Total"
    },
    {
      "calculate": "isValid(datum['RO Overall Completion %']) ? format(+datum['RO Overall Completion %'], '.0%') : '0%'",
      "as": "Rate Label"
    }
  ],
  "hconcat": [
    {
      "width": 250,
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
            "labelLimit": 155,
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
            "fontSize": 7,
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
                "test": "datum.Count > 0 && (datum.x1 - datum.x0) >= 8",
                "value": 1
              },
              "value": 0
            }
          }
        }
      ]
    },
    {
      "width": 75,
      "height": {
        "step": 13
      },
      "mark": {
        "type": "text",
        "fontSize": 9,
        "fontWeight": "normal",
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
          "field": "RO Total",
          "type": "quantitative",
          "format": ".0f"
        }
      },
      "title": {
        "text": "Total ROs",
        "fontSize": 9,
        "fontWeight": "bold",
        "color": "#17365D"
      }
    },
    {
      "width": 90,
      "height": {
        "step": 13
      },
      "mark": {
        "type": "text",
        "fontSize": 9,
        "fontWeight": "normal",
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
        "text": "Overall Completion",
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
    "axis": {
      "grid": false
    },
    "font": "Segoe UI"
  }
}
