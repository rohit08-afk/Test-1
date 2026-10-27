
{
  "$schema": "https://vega.github.io/schema/vega/v5.json",
  "description": "Supplier readiness by category family",
  "width": 580,
  "height": 310,
  "padding": 0,
  "autosize": "none",
  "background": "transparent",
  "data": [
    {
      "name": "source",
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
          "expr": "isValid(datum['Attendance Rate']) ? toNumber(datum['Attendance Rate']) : 0"
        },
        {
          "type": "formula",
          "as": "Overall",
          "expr": "isValid(datum['Overall Attendance Rate']) ? toNumber(datum['Overall Attendance Rate']) : 0"
        },
        {
          "type": "aggregate",
          "groupby": ["Category"],
          "fields": ["Rate", "Overall"],
          "ops": ["max", "max"],
          "as": ["Rate", "Overall"]
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
          "ops": ["row_number"],
          "as": ["Row"]
        },
        {
          "type": "formula",
          "as": "Y",
          "expr": "73 + (datum.Row - 1) * 20"
        }
      ]
    },
    {
      "name": "columns",
      "values": [
        {"x": 135, "x2": 200, "fill": "#E5F2FF"},
        {"x": 200, "x2": 270, "fill": "#E5F6EC"},
        {"x": 270, "x2": 375, "fill": "#FFF4DD"},
        {"x": 375, "x2": 440, "fill": "#FFF0DD"},
        {"x": 440, "x2": 510, "fill": "#EEEEFF"},
        {"x": 510, "x2": 580, "fill": "#E2F7F7"}
      ]
    },
    {
      "name": "stages",
      "values": [
        {
          "x": 135,
          "x2": 200,
          "label": "S1 Reach",
          "fill": "#1555AB",
          "color": "#FFFFFF"
        },
        {
          "x": 200,
          "x2": 375,
          "label": "S2 Acknowledge",
          "fill": "#07954B",
          "color": "#FFFFFF"
        },
        {
          "x": 375,
          "x2": 440,
          "label": "S3 Commit",
          "fill": "#FFC21A",
          "color": "#17365D"
        },
        {
          "x": 440,
          "x2": 510,
          "label": "S4 Prove",
          "fill": "#273F91",
          "color": "#FFFFFF"
        },
        {
          "x": 510,
          "x2": 580,
          "label": "S5 Ready",
          "fill": "#08AFB2",
          "color": "#FFFFFF"
        }
      ]
    },
    {
      "name": "subheaders",
      "values": [
        {"x": 167.5, "line1": "Email", "line2": "Coverage"},
        {"x": 235, "line1": "RO", "line2": "Attendance"},
        {"x": 322.5, "line1": "Supplier Webinar", "line2": "Attendance"},
        {"x": 407.5, "line1": "Commit", "line2": ""},
        {"x": 475, "line1": "Prove", "line2": "Capability"},
        {"x": 545, "line1": "Ready to", "line2": "Operate"}
      ]
    },
    {
      "name": "cells",
      "source": "source",
      "transform": [
        {
          "type": "fold",
          "fields": [
            "Reach",
            "RO",
            "Supplier",
            "Commit",
            "Prove",
            "Ready"
          ],
          "as": ["Stage", "Unused"]
        }
      ]
    },
    {
      "name": "total",
      "source": "source",
      "transform": [
        {
          "type": "aggregate",
          "fields": ["Overall"],
          "ops": ["max"],
          "as": ["Rate"]
        }
      ]
    }
  ],
  "signals": [
    {
      "name": "totalY",
      "update": "73 + length(data('source')) * 20 + 7"
    }
  ],
  "marks": [
    {
      "type": "rect",
      "from": {"data": "columns"},
      "encode": {
        "update": {
          "x": {"field": "x"},
          "x2": {"field": "x2"},
          "y": {"value": 42},
          "y2": {"signal": "totalY + 14"},
          "fill": {"field": "fill"}
        }
      }
    },
    {
      "type": "rect",
      "from": {"data": "stages"},
      "encode": {
        "update": {
          "x": {"field": "x"},
          "x2": {"field": "x2"},
          "y": {"value": 0},
          "height": {"value": 32},
          "fill": {"field": "fill"},
          "cornerRadius": {"value": 4}
        }
      }
    },
    {
      "type": "text",
      "from": {"data": "stages"},
      "encode": {
        "update": {
          "x": {
            "signal": "(datum.x + datum.x2) / 2"
          },
          "y": {"value": 16},
          "text": {"field": "label"},
          "align": {"value": "center"},
          "baseline": {"value": "middle"},
          "fontSize": {"value": 9},
          "fontWeight": {"value": "bold"},
          "fill": {"field": "color"}
        }
      }
    },
    {
      "type": "text",
      "encode": {
        "update": {
          "x": {"value": 4},
          "y": {"value": 52},
          "text": {"value": "Category Family"},
          "fontSize": {"value": 9},
          "fontWeight": {"value": "bold"},
          "fill": {"value": "#17365D"}
        }
      }
    },
    {
      "type": "text",
      "from": {"data": "subheaders"},
      "encode": {
        "update": {
          "x": {"field": "x"},
          "y": {"value": 47},
          "text": {"field": "line1"},
          "align": {"value": "center"},
          "fontSize": {"value": 8},
          "fontWeight": {"value": "bold"},
          "fill": {"value": "#17365D"}
        }
      }
    },
    {
      "type": "text",
      "from": {"data": "subheaders"},
      "encode": {
        "update": {
          "x": {"field": "x"},
          "y": {"value": 58},
          "text": {"field": "line2"},
          "align": {"value": "center"},
          "fontSize": {"value": 8},
          "fill": {"value": "#17365D"}
        }
      }
    },
    {
      "type": "text",
      "from": {"data": "source"},
      "encode": {
        "update": {
          "x": {"value": 4},
          "y": {"field": "Y"},
          "text": {"field": "Category"},
          "fontSize": {"value": 8},
          "limit": {"value": 127},
          "baseline": {"value": "middle"},
          "fill": {"value": "#17365D"}
        }
      }
    },
    {
      "type": "symbol",
      "from": {"data": "source"},
      "encode": {
        "update": {
          "x": {"value": 151},
          "y": {"field": "Y"},
          "size": {"value": 45},
          "fill": {"value": "#2BA878"}
        }
      }
    },
    {
      "type": "text",
      "from": {"data": "source"},
      "encode": {
        "update": {
          "x": {"value": 167},
          "y": {"field": "Y"},
          "text": {"value": "100%"},
          "fontSize": {"value": 8},
          "baseline": {"value": "middle"},
          "fill": {"value": "#17365D"}
        }
      }
    },
    {
      "type": "text",
      "from": {"data": "source"},
      "encode": {
        "update": {
          "x": {"value": 235},
          "y": {"field": "Y"},
          "text": {"value": "—"},
          "align": {"value": "center"},
          "baseline": {"value": "middle"},
          "fontSize": {"value": 8},
          "fill": {"value": "#777777"}
        }
      }
    },
    {
      "type": "symbol",
      "from": {"data": "source"},
      "encode": {
        "update": {
          "x": {"value": 292},
          "y": {"field": "Y"},
          "size": {"value": 45},
          "fill": {
            "signal": "datum.Rate === 0 ? '#F05252' : '#FFBF36'"
          }
        }
      }
    },
    {
      "type": "text",
      "from": {"data": "source"},
      "encode": {
        "update": {
          "x": {"value": 306},
          "y": {"field": "Y"},
          "text": {
            "signal": "format(datum.Rate, '.0%')"
          },
          "fontSize": {"value": 8},
          "baseline": {"value": "middle"},
          "fill": {"value": "#17365D"}
        }
      }
    },
    {
      "type": "symbol",
      "from": {"data": "source"},
      "encode": {
        "update": {
          "x": {"value": 393},
          "y": {"field": "Y"},
          "size": {"value": 25},
          "fill": {"value": "#D3D7DE"}
        }
      }
    },
    {
      "type": "symbol",
      "from": {"data": "source"},
      "encode": {
        "update": {
          "x": {"value": 457},
          "y": {"field": "Y"},
          "size": {"value": 25},
          "fill": {"value": "#D3D7DE"}
        }
      }
    },
    {
      "type": "symbol",
      "from": {"data": "source"},
      "encode": {
        "update": {
          "x": {"value": 527},
          "y": {"field": "Y"},
          "size": {"value": 25},
          "fill": {"value": "#D3D7DE"}
        }
      }
    },
    {
      "type": "text",
      "from": {"data": "source"},
      "encode": {
        "update": {
          "x": {"value": 408},
          "y": {"field": "Y"},
          "text": {"value": "—"},
          "fontSize": {"value": 8},
          "baseline": {"value": "middle"},
          "fill": {"value": "#777777"}
        }
      }
    },
    {
      "type": "text",
      "from": {"data": "source"},
      "encode": {
        "update": {
          "x": {"value": 472},
          "y": {"field": "Y"},
          "text": {"value": "—"},
          "fontSize": {"value": 8},
          "baseline": {"value": "middle"},
          "fill": {"value": "#777777"}
        }
      }
    },
    {
      "type": "text",
      "from": {"data": "source"},
      "encode": {
        "update": {
          "x": {"value": 542},
          "y": {"field": "Y"},
          "text": {"value": "—"},
          "fontSize": {"value": 8},
          "baseline": {"value": "middle"},
          "fill": {"value": "#777777"}
        }
      }
    },
    {
      "type": "rule",
      "encode": {
        "update": {
          "x": {"value": 0},
          "x2": {"value": 580},
          "y": {"signal": "totalY - 10"},
          "stroke": {"value": "#D1D5DB"}
        }
      }
    },
    {
      "type": "text",
      "encode": {
        "update": {
          "x": {"value": 4},
          "y": {"signal": "totalY"},
          "text": {"value": "Total"},
          "fontSize": {"value": 9},
          "fontWeight": {"value": "bold"},
          "baseline": {"value": "middle"},
          "fill": {"value": "#17365D"}
        }
      }
    },
    {
      "type": "text",
      "encode": {
        "update": {
          "x": {"value": 167},
          "y": {"signal": "totalY"},
          "text": {"value": "100%"},
          "fontSize": {"value": 9},
          "fontWeight": {"value": "bold"},
          "baseline": {"value": "middle"},
          "fill": {"value": "#17365D"}
        }
      }
    },
    {
      "type": "text",
      "from": {"data": "total"},
      "encode": {
        "update": {
          "x": {"value": 306},
          "y": {"signal": "totalY"},
          "text": {
            "signal": "format(datum.Rate, '.0%')"
          },
          "fontSize": {"value": 9},
          "fontWeight": {"value": "bold"},
          "baseline": {"value": "middle"},
          "fill": {"value": "#17365D"}
        }
      }
    }
  ]
}
