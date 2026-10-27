{
  "$schema": "https://vega.github.io/schema/vega/v5.json",
  "description": "Supplier readiness by category family - corrected formatted Vega specification",
  "background": "transparent",
  "autosize": {
    "type": "pad",
    "contains": "padding"
  },
  "padding": 0,
  "width": 700,
  "height": 340,
  "data": [
    {
      "name": "dataset"
    },
    {
      "name": "rows",
      "source": "dataset",
      "transform": [
        {
          "type": "formula",
          "as": "Category",
          "expr": "datum['Category Family']"
        },
        {
          "type": "formula",
          "as": "Rate",
          "expr": "isValid(datum['Attendance Rate']) ? toNumber(datum['Attendance Rate']) : null"
        },
        {
          "type": "formula",
          "as": "Overall",
          "expr": "isValid(datum['Overall Attendance Rate']) ? toNumber(datum['Overall Attendance Rate']) : null"
        },
        {
          "type": "aggregate",
          "groupby": [
            "Category"
          ],
          "fields": [
            "Rate",
            "Overall"
          ],
          "ops": [
            "max",
            "max"
          ],
          "as": [
            "Rate",
            "Overall"
          ]
        },
        {
          "type": "collect",
          "sort": {
            "field": "Category",
            "order": "ascending"
          }
        },
        {
          "type": "window",
          "ops": [
            "row_number"
          ],
          "as": [
            "Row"
          ]
        },
        {
          "type": "formula",
          "as": "cy",
          "expr": "62 + (datum.Row - 0.5)*19"
        },
        {
          "type": "formula",
          "as": "labelX",
          "expr": "170"
        }
      ]
    },
    {
      "name": "columns",
      "values": [
        {
          "x0": 0,
          "x1": 175,
          "fill": "#F5F7FA"
        },
        {
          "x0": 175,
          "x1": 250,
          "fill": "#E5F2FF"
        },
        {
          "x0": 250,
          "x1": 330,
          "fill": "#E5F6EC"
        },
        {
          "x0": 330,
          "x1": 410,
          "fill": "#E5F6EC"
        },
        {
          "x0": 410,
          "x1": 490,
          "fill": "#FFF6DD"
        },
        {
          "x0": 490,
          "x1": 595,
          "fill": "#E9EEFA"
        },
        {
          "x0": 595,
          "x1": 700,
          "fill": "#E2F7F7"
        }
      ]
    },
    {
      "name": "stages",
      "values": [
        {
          "x0": 175,
          "x1": 250,
          "cx": 212.5,
          "cy": 15,
          "label": "S1 Reach",
          "fill": "#1555A3"
        },
        {
          "x0": 250,
          "x1": 410,
          "cx": 330.0,
          "cy": 15,
          "label": "S2 Acknowledge",
          "fill": "#07954B"
        },
        {
          "x0": 410,
          "x1": 490,
          "cx": 450.0,
          "cy": 15,
          "label": "S3 Commit",
          "fill": "#FFC21A"
        },
        {
          "x0": 490,
          "x1": 595,
          "cx": 542.5,
          "cy": 15,
          "label": "S4 Prove Capability",
          "fill": "#273F91"
        },
        {
          "x0": 595,
          "x1": 700,
          "cx": 647.5,
          "cy": 15,
          "label": "S5 Ready to Operate",
          "fill": "#08AFB2"
        }
      ]
    },
    {
      "name": "stagewords",
      "values": [
        {
          "x": 212.5,
          "y": 15,
          "label": "S1 Reach"
        },
        {
          "x": 330,
          "y": 15,
          "label": "S2 Acknowledge"
        },
        {
          "x": 450,
          "y": 15,
          "label": "S3 Commit"
        },
        {
          "x": 542.5,
          "y": 10,
          "label": "S4 Prove"
        },
        {
          "x": 542.5,
          "y": 21,
          "label": "Capability"
        },
        {
          "x": 647.5,
          "y": 10,
          "label": "S5 Ready to"
        },
        {
          "x": 647.5,
          "y": 21,
          "label": "Operate"
        }
      ]
    },
    {
      "name": "subheads",
      "values": [
        {
          "x": 87.5,
          "y": 44,
          "label": "Category Family"
        },
        {
          "x": 212.5,
          "y": 44,
          "label": "Email Coverage"
        },
        {
          "x": 290,
          "y": 44,
          "label": "RO Attendance"
        },
        {
          "x": 370,
          "y": 38,
          "label": "Supplier Webinar"
        },
        {
          "x": 370,
          "y": 50,
          "label": "Attendance"
        },
        {
          "x": 450,
          "y": 44,
          "label": "Commit"
        },
        {
          "x": 542.5,
          "y": 38,
          "label": "Prove Capability"
        },
        {
          "x": 647.5,
          "y": 38,
          "label": "Ready to"
        },
        {
          "x": 647.5,
          "y": 50,
          "label": "Operate"
        }
      ]
    },
    {
      "name": "cells",
      "source": "rows",
      "transform": [
        {
          "type": "cross",
          "with": "columns",
          "as": [
            "r",
            "c"
          ]
        },
        {
          "type": "formula",
          "as": "x0",
          "expr": "datum.c.x0"
        },
        {
          "type": "formula",
          "as": "x1",
          "expr": "datum.c.x1"
        },
        {
          "type": "formula",
          "as": "fill",
          "expr": "datum.c.fill"
        },
        {
          "type": "formula",
          "as": "y",
          "expr": "datum.r.cy - 9.5"
        }
      ]
    },
    {
      "name": "dots",
      "source": "rows",
      "transform": [
        {
          "type": "fold",
          "fields": [
            "Category",
            "Rate"
          ],
          "as": [
            "kind",
            "unused"
          ]
        },
        {
          "type": "filter",
          "expr": "datum.kind == 'Category' || datum.kind == 'Rate'"
        },
        {
          "type": "formula",
          "as": "x",
          "expr": "datum.kind == 'Category' ? 190 : 344"
        },
        {
          "type": "formula",
          "as": "y",
          "expr": "datum.cy"
        },
        {
          "type": "formula",
          "as": "fill",
          "expr": "datum.kind == 'Category' ? '#20A56C' : '#FFBF3C'"
        }
      ]
    },
    {
      "name": "values",
      "source": "rows",
      "transform": [
        {
          "type": "fold",
          "fields": [
            "Category",
            "Rate"
          ],
          "as": [
            "kind",
            "unused"
          ]
        },
        {
          "type": "formula",
          "as": "x",
          "expr": "datum.kind == 'Category' ? 216 : 375"
        },
        {
          "type": "formula",
          "as": "y",
          "expr": "datum.cy"
        },
        {
          "type": "formula",
          "as": "label",
          "expr": "datum.kind == 'Category' ? '100%' : (isValid(datum.Rate) ? format(datum.Rate,'.0%') : '—')"
        }
      ]
    },
    {
      "name": "pending",
      "source": "rows",
      "transform": [
        {
          "type": "cross",
          "with": "pendingcolumns",
          "as": [
            "r",
            "c"
          ]
        },
        {
          "type": "formula",
          "as": "x",
          "expr": "datum.c.x"
        },
        {
          "type": "formula",
          "as": "y",
          "expr": "datum.r.cy"
        },
        {
          "type": "formula",
          "as": "label",
          "expr": "'—'"
        }
      ]
    },
    {
      "name": "pendingcolumns",
      "values": [
        {
          "x": 290
        },
        {
          "x": 450
        },
        {
          "x": 542.5
        },
        {
          "x": 647.5
        }
      ]
    },
    {
      "name": "totalcells",
      "source": "columns",
      "transform": [
        {
          "type": "formula",
          "as": "y",
          "expr": "62 + length(data(\"rows\"))*19"
        }
      ]
    },
    {
      "name": "totallabels",
      "values": [
        {
          "x": 170,
          "label": "Total"
        },
        {
          "x": 216,
          "label": "100%"
        },
        {
          "x": 290,
          "label": "—"
        },
        {
          "x": 375,
          "label": ""
        },
        {
          "x": 450,
          "label": "—"
        },
        {
          "x": 542,
          "label": "—"
        },
        {
          "x": 647,
          "label": "—"
        }
      ],
      "transform": [
        {
          "type": "formula",
          "as": "y",
          "expr": "62 + length(data(\"rows\"))*19 + 11"
        },
        {
          "type": "formula",
          "as": "label",
          "expr": "datum.x == 375 ? (length(data('rows')) > 0 && isValid(data('rows')[0].Overall) ? format(data('rows')[0].Overall,'.0%') : '—') : datum.label"
        }
      ]
    }
  ],
  "marks": [
    {
      "type": "rect",
      "name": "stage-header",
      "from": {
        "data": "stages"
      },
      "encode": {
        "enter": {
          "x": {
            "field": "x0"
          },
          "x2": {
            "field": "x1"
          },
          "y": {
            "value": 0
          },
          "y2": {
            "value": 30
          },
          "fill": {
            "field": "fill"
          },
          "cornerRadius": {
            "value": 3
          }
        }
      }
    },
    {
      "type": "text",
      "name": "stage-label",
      "from": {
        "data": "stagewords"
      },
      "encode": {
        "enter": {
          "x": {
            "field": "x"
          },
          "y": {
            "field": "y"
          },
          "text": {
            "field": "label"
          },
          "font": {
            "value": "Segoe UI"
          },
          "fontSize": {
            "value": 9
          },
          "fontWeight": {
            "value": "bold"
          },
          "align": {
            "value": "center"
          },
          "baseline": {
            "value": "middle"
          },
          "fill": {
            "value": "#FFFFFF"
          }
        }
      }
    },
    {
      "type": "rect",
      "name": "subheader-background",
      "from": {
        "data": "columns"
      },
      "encode": {
        "enter": {
          "x": {
            "field": "x0"
          },
          "x2": {
            "field": "x1"
          },
          "y": {
            "value": 30
          },
          "y2": {
            "value": 62
          },
          "fill": {
            "field": "fill"
          },
          "cornerRadius": {
            "value": 0
          }
        }
      }
    },
    {
      "type": "text",
      "name": "subheader-label",
      "from": {
        "data": "subheads"
      },
      "encode": {
        "enter": {
          "x": {
            "field": "x"
          },
          "y": {
            "field": "y"
          },
          "text": {
            "field": "label"
          },
          "font": {
            "value": "Segoe UI"
          },
          "fontSize": {
            "value": 8
          },
          "fontWeight": {
            "value": "bold"
          },
          "align": {
            "value": "center"
          },
          "baseline": {
            "value": "middle"
          },
          "fill": {
            "value": "#17365D"
          }
        }
      }
    },
    {
      "type": "rect",
      "from": {
        "data": "cells"
      },
      "encode": {
        "enter": {
          "x": {
            "field": "x0"
          },
          "x2": {
            "field": "x1"
          },
          "y": {
            "field": "y"
          },
          "height": {
            "value": 19
          },
          "fill": {
            "field": "fill"
          },
          "stroke": {
            "value": "#DDE4EC"
          },
          "strokeWidth": {
            "value": 0.35
          }
        }
      }
    },
    {
      "type": "text",
      "name": "category-label",
      "from": {
        "data": "rows"
      },
      "encode": {
        "enter": {
          "x": {
            "field": "labelX"
          },
          "y": {
            "field": "cy"
          },
          "text": {
            "field": "Category"
          },
          "font": {
            "value": "Segoe UI"
          },
          "fontSize": {
            "value": 8
          },
          "fontWeight": {
            "value": "normal"
          },
          "align": {
            "value": "right"
          },
          "baseline": {
            "value": "middle"
          },
          "fill": {
            "value": "#17365D"
          }
        }
      }
    },
    {
      "type": "symbol",
      "from": {
        "data": "dots"
      },
      "encode": {
        "enter": {
          "x": {
            "field": "x"
          },
          "y": {
            "field": "y"
          },
          "size": {
            "value": 34
          },
          "shape": {
            "value": "circle"
          },
          "fill": {
            "field": "fill"
          }
        }
      }
    },
    {
      "type": "text",
      "name": "value-labels",
      "from": {
        "data": "values"
      },
      "encode": {
        "enter": {
          "x": {
            "field": "x"
          },
          "y": {
            "field": "y"
          },
          "text": {
            "field": "label"
          },
          "font": {
            "value": "Segoe UI"
          },
          "fontSize": {
            "value": 9
          },
          "fontWeight": {
            "value": "normal"
          },
          "align": {
            "value": "center"
          },
          "baseline": {
            "value": "middle"
          },
          "fill": {
            "value": "#17365D"
          }
        }
      }
    },
    {
      "type": "text",
      "name": "pending-labels",
      "from": {
        "data": "pending"
      },
      "encode": {
        "enter": {
          "x": {
            "field": "x"
          },
          "y": {
            "field": "y"
          },
          "text": {
            "field": "label"
          },
          "font": {
            "value": "Segoe UI"
          },
          "fontSize": {
            "value": 9
          },
          "fontWeight": {
            "value": "normal"
          },
          "align": {
            "value": "center"
          },
          "baseline": {
            "value": "middle"
          },
          "fill": {
            "value": "#A5ABB4"
          }
        }
      }
    },
    {
      "type": "rect",
      "from": {
        "data": "totalcells"
      },
      "encode": {
        "enter": {
          "x": {
            "field": "x0"
          },
          "x2": {
            "field": "x1"
          },
          "y": {
            "field": "y"
          },
          "height": {
            "value": 22
          },
          "fill": {
            "field": "fill"
          },
          "stroke": {
            "value": "#B8C6D6"
          },
          "strokeWidth": {
            "value": 0.7
          }
        }
      }
    },
    {
      "type": "text",
      "name": "total-labels",
      "from": {
        "data": "totallabels"
      },
      "encode": {
        "enter": {
          "x": {
            "field": "x"
          },
          "y": {
            "field": "y"
          },
          "text": {
            "field": "label"
          },
          "font": {
            "value": "Segoe UI"
          },
          "fontSize": {
            "value": 9
          },
          "fontWeight": {
            "value": "bold"
          },
          "align": {
            "value": "center"
          },
          "baseline": {
            "value": "middle"
          },
          "fill": {
            "value": "#17365D"
          }
        }
      }
    }
  ],
  "config": {
    "text": {
      "font": "Segoe UI"
    }
  }
}
