
{
  "$schema": "https://vega.github.io/schema/vega/v5.json",
  "description": "Supplier readiness matrix by category family",
  "background": "transparent",
  "autosize": {
    "type": "none",
    "contains": "padding"
  },
  "padding": 0,
  "width": 1215,
  "height": 360,
  "signals": [
    {
      "name": "rowHeight",
      "value": 21
    },
    {
      "name": "bodyTop",
      "value": 77
    },
    {
      "name": "totalY",
      "update": "bodyTop + length(data('categories')) * rowHeight + 10"
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
          "type": "formula",
          "as": "ROCompletion",
          "expr": "isValid(datum['RO Overall Completion %']) ? toNumber(datum['RO Overall Completion %']) : null"
        },
        {
          "type": "aggregate",
          "groupby": ["Category"],
          "fields": ["Rate", "ROCompletion"],
          "ops": ["max", "max"],
          "as": ["Rate", "ROCompletion"]
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
        },
        {
          "type": "formula",
          "as": "ROLabel",
          "expr": "datum.ROCompletion == null ? '—' : format(datum.ROCompletion, '.0%')"
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
          "type": "formula",
          "as": "OverallRO",
          "expr": "isValid(datum['RO Overall Completion %']) ? toNumber(datum['RO Overall Completion %']) : null"
        },
        {
          "type": "aggregate",
          "fields": ["Overall", "OverallRO"],
          "ops": ["max", "max"],
          "as": ["Overall", "OverallRO"]
        },
        {
          "type": "formula",
          "as": "Label",
          "expr": "datum.Overall == null ? '—' : format(datum.Overall, '.0%')"
        },
        {
          "type": "formula",
          "as": "ROLabel",
          "expr": "datum.OverallRO == null ? '—' : format(datum.OverallRO, '.0%')"
        }
      ]
    },
    {
      "name": "columns",
      "values": [
        {"x": 0, "x2": 200, "fill": "#FFFFFF"},
        {"x": 200, "x2": 335, "fill": "#E5F2FF"},
        {"x": 335, "x2": 480, "fill": "#E5F6EC"},
        {"x": 480, "x2": 710, "fill": "#E5F6EC"},
        {"x": 710, "x2": 855, "fill": "#FFF6DD"},
        {"x": 855, "x2": 1010, "fill": "#E9EEFA"},
        {"x": 1010, "x2": 1165, "fill": "#E2F7F7"}
      ]
    },
    {
      "name": "stages",
      "values": [
        {"x": 200, "x2": 335, "label": "S1 Reach", "fill": "#1555AB", "color": "#FFFFFF"},
        {"x": 335, "x2": 710, "label": "S2 Acknowledge", "fill": "#07954B", "color": "#FFFFFF"},
        {"x": 710, "x2": 855, "label": "S3 Commit", "fill": "#FFC21A", "color": "#17365D"},
        {"x": 855, "x2": 1010, "label": "S4 Prove", "fill": "#273F91", "color": "#FFFFFF"},
        {"x": 1010, "x2": 1165, "label": "S5 Ready", "fill": "#08AFAF", "color": "#FFFFFF"}
      ]
    },
    {
      "name": "subheaders",
      "values": [
        {"x": 267.5, "label": "Email", "line2": "Coverage"},
        {"x": 407.5, "label": "RO", "line2": "Attendance"},
        {"x": 595, "label": "Supplier Webinar", "line2": "Attendance"},
        {"x": 782.5, "label": "Commit", "line2": ""},
        {"x": 932.5, "label": "Prove", "line2": "Capability"},
        {"x": 1087.5, "label": "Ready to", "line2": "Operate"}
      ]
    },
    {
      "name": "cells",
      "source": "categories",
      "transform": [
        {
          "type": "formula",
          "as": "Items",
          "expr": "[{'x':267.5,'label':'100%','dot':'#20A56C'},{'x':407.5,'label':datum.ROLabel,'dot':datum.ROCompletion == null ? '#BFC3C8' : datum.ROCompletion == 0 ? '#FF5757' : '#FFBF3C'},{'x':595,'label':datum.SupplierLabel,'dot':datum.Rate == null ? '#BFC3C8' : datum.Rate == 0 ? '#FF5757' : '#FFBF3C'},{'x':782.5,'label':'—','dot':'#BFC3C8'},{'x':932.5,'label':'—','dot':'#BFC3C8'},{'x':1087.5,'label':'—','dot':'#BFC3C8'}]"
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
          "y2": {"signal": "totalY + 14"},
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
          "fontSize": {"value": 12},
          "fontWeight": {"value": "bold"},
          "fill": {"field": "color"}
        }
      }
    },
    {
      "type": "text",
      "encode": {
        "enter": {
          "x": {"value": 4},
          "y": {"value": 55},
          "text": {"value": "Category Family"},
          "fontSize": {"value": 12},
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
          "fontSize": {"value": 11},
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
          "fontSize": {"value": 11},
          "fill": {"value": "#17365D"}
        }
      }
    },
    {
      "type": "text",
      "from": {"data": "categories"},
      "encode": {
        "enter": {
          "x": {"value": 4},
          "y": {"field": "cy"},
          "text": {"field": "Category"},
          "baseline": {"value": "middle"},
          "fontSize": {"value": 11},
          "fill": {"value": "#17365D"},
          "limit": {"value": 190}
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
          "fontSize": {"value": 11},
          "fill": {"value": "#17365D"}
        }
      }
    },
    {
      "type": "rule",
      "encode": {
        "enter": {
          "x": {"value": 0},
          "x2": {"value": 1165},
          "y": {"signal": "totalY - 12"},
          "stroke": {"value": "#CCD5DF"}
        }
      }
    },
    {
      "type": "text",
      "encode": {
        "enter": {
          "x": {"value": 4},
          "y": {"signal": "totalY"},
          "text": {"value": "Total"},
          "baseline": {"value": "middle"},
          "fontSize": {"value": 11},
          "fontWeight": {"value": "bold"},
          "fill": {"value": "#17365D"}
        }
      }
    },
    {
      "type": "text",
      "encode": {
        "enter": {
          "x": {"value": 267.5},
          "y": {"signal": "totalY"},
          "text": {"value": "100%"},
          "align": {"value": "center"},
          "baseline": {"value": "middle"},
          "fontSize": {"value": 11},
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
          "x": {"value": 407.5},
          "y": {"signal": "totalY"},
          "text": {"field": "ROLabel"},
          "align": {"value": "center"},
          "baseline": {"value": "middle"},
          "fontSize": {"value": 11},
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
          "x": {"value": 595},
          "y": {"signal": "totalY"},
          "text": {"field": "Label"},
          "align": {"value": "center"},
          "baseline": {"value": "middle"},
          "fontSize": {"value": 11},
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
