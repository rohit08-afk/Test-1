
{
  "$schema": "https://vega.github.io/schema/vega/v5.json",
  "description": "Compact supplier readiness matrix",
  "background": "transparent",
  "autosize": {
    "type": "pad",
    "contains": "padding"
  },
  "padding": 2,
  "width": 575,
  "height": 360,
  "signals": [
    {
      "name": "rowHeight",
      "value": 21
    },
    {
      "name": "bodyTop",
      "value": 77
    }
  ],
  "data": [
    {
      "name": "dataset"
    },
    {
      "name": "categories",
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
          "type": "aggregate",
          "groupby": ["Category"],
          "fields": ["Rate"],
          "ops": ["max"],
          "as": ["Rate"]
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
          "as": "cy",
          "expr": "bodyTop + (datum.Row - 0.5) * rowHeight"
        },
        {
          "type": "formula",
          "as": "SupplierLabel",
          "expr": "datum.Rate == null ? '—' : format(datum.Rate, '.0%')"
        }
      ]
    },
    {
      "name": "total",
      "source": "dataset",
      "transform": [
        {
          "type": "formula",
          "as": "Overall",
          "expr": "isValid(datum['Overall Attendance Rate']) ? toNumber(datum['Overall Attendance Rate']) : null"
        },
        {
          "type": "aggregate",
          "fields": ["Overall"],
          "ops": ["max"],
          "as": ["Overall"]
        },
        {
          "type": "formula",
          "as": "Label",
          "expr": "datum.Overall == null ? '—' : format(datum.Overall, '.0%')"
        }
      ]
    },
    {
      "name": "columns",
      "values": [
        {"x": 0, "x2": 155, "fill": "#FFFFFF"},
        {"x": 155, "x2": 215, "fill": "#E5F2FF"},
        {"x": 215, "x2": 280, "fill": "#E5F6EC"},
        {"x": 280, "x2": 375, "fill": "#E5F6EC"},
        {"x": 375, "x2": 435, "fill": "#FFF6DD"},
        {"x": 435, "x2": 505, "fill": "#E9EEFA"},
        {"x": 505, "x2": 575, "fill": "#E2F7F7"}
      ]
    },
    {
      "name": "stages",
      "values": [
        {"x": 155, "x2": 215, "label": "S1 Reach", "fill": "#1555AB", "color": "#FFFFFF"},
        {"x": 215, "x2": 375, "label": "S2 Acknowledge", "fill": "#07954B", "color": "#FFFFFF"},
        {"x": 375, "x2": 435, "label": "S3 Commit", "fill": "#FFC21A", "color": "#17365D"},
        {"x": 435, "x2": 505, "label": "S4 Prove", "fill": "#273F91", "color": "#FFFFFF"},
        {"x": 505, "x2": 575, "label": "S5 Ready", "fill": "#08AFAF", "color": "#FFFFFF"}
      ]
    },
    {
      "name": "subheaders",
      "values": [
        {"x": 185, "label": "Email", "line2": "Coverage"},
        {"x": 247, "label": "RO", "line2": "Attendance"},
        {"x": 327, "label": "Supplier Webinar", "line2": "Attendance"},
        {"x": 405, "label": "Commit", "line2": ""},
        {"x": 470, "label": "Prove", "line2": "Capability"},
        {"x": 540, "label": "Ready to", "line2": "Operate"}
      ]
    },
    {
      "name": "cells",
      "source": "categories",
      "transform": [
        {
          "type": "formula",
          "as": "Items",
          "expr": "[{'x':185,'label':'100%','dot':'#20A56C'},{'x':247,'label':'—','dot':'#BFC3C8'},{'x':327,'label':datum.SupplierLabel,'dot':datum.Rate == null ? '#BFC3C8' : datum.Rate == 0 ? '#FF5757' : '#FFBF3C'},{'x':405,'label':'—','dot':'#BFC3C8'},{'x':470,'label':'—','dot':'#BFC3C8'},{'x':540,'label':'—','dot':'#BFC3C8'}]"
        },
        {
          "type": "flatten",
          "fields": ["Items"],
          "as": ["Item"]
        },
        {
          "type": "formula",
          "as": "cx",
          "expr": "datum.Item.x"
        },
        {
          "type": "formula",
          "as": "label",
          "expr": "datum.Item.label"
        },
        {
          "type": "formula",
          "as": "dot",
          "expr": "datum.Item.dot"
        }
      ]
    }
  ],
  "marks": [
    {
      "type": "rect",
      "from": {"data": "columns"},
      "encode": {
        "enter": {
          "x": {"field": "x"},
          "x2": {"field": "x2"},
          "y": {"value": 38},
          "y2": {"value": 340},
          "fill": {"field": "fill"}
        }
      }
    },
    {
      "type": "rect",
      "from": {"data": "stages"},
      "encode": {
        "enter": {
          "x": {"field": "x"},
          "x2": {"field": "x2"},
          "y": {"value": 0},
          "height": {"value": 34},
          "cornerRadius": {"value": 5},
          "fill": {"field": "fill"}
        }
      }
    },
    {
      "type": "text",
      "from": {"data": "stages"},
      "encode": {
        "enter": {
          "x": {"signal": "(datum.x + datum.x2)/2"},
          "y": {"value": 17},
          "text": {"field": "label"},
          "align": {"value": "center"},
          "baseline": {"value": "middle"},
          "font": {"value": "Segoe UI"},
          "fontSize": {"value": 9},
          "fontWeight": {"value": "bold"},
          "fill": {"field": "color"}
        }
      }
    },
    {
      "type": "text",
      "encode": {
        "enter": {
          "x": {"value": 5},
          "y": {"value": 55},
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
        "enter": {
          "x": {"field": "x"},
          "y": {"value": 49},
          "text": {"field": "label"},
          "align": {"value": "center"},
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
        "enter": {
          "x": {"field": "x"},
          "y": {"value": 62},
          "text": {"field": "line2"},
          "align": {"value": "center"},
          "fontSize": {"value": 9},
          "fill": {"value": "#17365D"}
        }
      }
    },
    {
      "type": "text",
      "from": {"data": "categories"},
      "encode": {
        "enter": {
          "x": {"value": 5},
          "y": {"field": "cy"},
          "text": {"field": "Category"},
          "baseline": {"value": "middle"},
          "fontSize": {"value": 8},
          "fill": {"value": "#17365D"},
          "limit": {"value": 145}
        }
      }
    },
    {
      "type": "symbol",
      "from": {"data": "cells"},
      "encode": {
        "enter": {
          "x": {"signal": "datum.cx - 18"},
          "y": {"field": "cy"},
          "size": {"value": 40},
          "fill": {"field": "dot"}
        }
      }
    },
    {
      "type": "text",
      "from": {"data": "cells"},
      "encode": {
        "enter": {
          "x": {"signal": "datum.cx + 8"},
          "y": {"field": "cy"},
          "text": {"field": "label"},
          "align": {"value": "center"},
          "baseline": {"value": "middle"},
          "fontSize": {"value": 8},
          "fill": {"value": "#17365D"}
        }
      }
    },
    {
      "type": "rule",
      "encode": {
        "enter": {
          "x": {"value": 0},
          "x2": {"value": 575},
          "y": {"value": 315},
          "stroke": {"value": "#CCD5DF"}
        }
      }
    },
    {
      "type": "text",
      "encode": {
        "enter": {
          "x": {"value": 5},
          "y": {"value": 330},
          "text": {"value": "Total"},
          "fontSize": {"value": 9},
          "fontWeight": {"value": "bold"},
          "fill": {"value": "#17365D"}
        }
      }
    },
    {
      "type": "text",
      "encode": {
        "enter": {
          "x": {"value": 185},
          "y": {"value": 330},
          "text": {"value": "100%"},
          "align": {"value": "center"},
          "fontSize": {"value": 9},
          "fontWeight": {"value": "bold"},
          "fill": {"value": "#17365D"}
        }
      }
    },
    {
      "type": "text",
      "from": {"data": "total"},
      "encode": {
        "enter": {
          "x": {"value": 327},
          "y": {"value": 330},
          "text": {"field": "Label"},
          "align": {"value": "center"},
          "fontSize": {"value": 9},
          "fontWeight": {"value": "bold"},
          "fill": {"value": "#17365D"}
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
