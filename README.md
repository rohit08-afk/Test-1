
{
  "$schema": "https://vega.github.io/schema/vega/v5.json",
  "description": "Supplier readiness by category family",
  "background": "transparent",
  "autosize": {
    "type": "pad",
    "contains": "padding"
  },
  "padding": 2,
  "width": 790,
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
        {
          "x": 0,
          "x2": 190,
          "fill": "#FFFFFF"
        },
        {
          "x": 190,
          "x2": 280,
          "fill": "#E5F2FF"
        },
        {
          "x": 280,
          "x2": 375,
          "fill": "#E5F6EC"
        },
        {
          "x": 375,
          "x2": 505,
          "fill": "#E5F6EC"
        },
        {
          "x": 505,
          "x2": 595,
          "fill": "#FFF6DD"
        },
        {
          "x": 595,
          "x2": 690,
          "fill": "#E9EEFA"
        },
        {
          "x": 690,
          "x2": 790,
          "fill": "#E2F7F7"
        }
      ]
    },
    {
      "name": "stages",
      "values": [
        {
          "x": 190,
          "x2": 280,
          "label": "S1 Reach",
          "fill": "#1555AB",
          "color": "#FFFFFF"
        },
        {
          "x": 280,
          "x2": 505,
          "label": "S2 Acknowledge",
          "fill": "#07954B",
          "color": "#FFFFFF"
        },
        {
          "x": 505,
          "x2": 595,
          "label": "S3 Commit",
          "fill": "#FFC21A",
          "color": "#17365D"
        },
        {
          "x": 595,
          "x2": 690,
          "label": "S4 Prove",
          "fill": "#273F91",
          "color": "#FFFFFF"
        },
        {
          "x": 690,
          "x2": 790,
          "label": "S5 Ready",
          "fill": "#08AFAF",
          "color": "#FFFFFF"
        }
      ]
    },
    {
      "name": "subheaders",
      "values": [
        {
          "x": 235,
          "label": "Email",
          "line2": "Coverage"
        },
        {
          "x": 327,
          "label": "RO",
          "line2": "Attendance"
        },
        {
          "x": 440,
          "label": "Supplier Webinar",
          "line2": "Attendance"
        },
        {
          "x": 550,
          "label": "Commit",
          "line2": ""
        },
        {
          "x": 642,
          "label": "Prove",
          "line2": "Capability"
        },
        {
          "x": 740,
          "label": "Ready to",
          "line2": "Operate"
        }
      ]
    },
    {
      "name": "cells",
      "source": "categories",
      "transform": [
        {
          "type": "formula",
          "as": "Items",
          "expr": "[{'x':235,'label':'100%','dot':'#20A56C'},{'x':327,'label':'—','dot':'#BFC3C8'},{'x':440,'label':datum.SupplierLabel,'dot':'#FFBF3C'},{'x':550,'label':'—','dot':'#BFC3C8'},{'x':642,'label':'—','dot':'#BFC3C8'},{'x':740,'label':'—','dot':'#BFC3C8'}]"
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
      "from": {
        "data": "columns"
      },
      "encode": {
        "enter": {
          "x": {
            "field": "x"
          },
          "x2": {
            "field": "x2"
          },
          "y": {
            "value": 38
          },
          "y2": {
            "value": 340
          },
          "fill": {
            "field": "fill"
          }
        }
      }
    },
    {
      "type": "rect",
      "from": {
        "data": "stages"
      },
      "encode": {
        "enter": {
          "x": {
            "field": "x"
          },
          "x2": {
            "field": "x2"
          },
          "y": {
            "value": 0
          },
          "height": {
            "value": 34
          },
          "cornerRadius": {
            "value": 5
          },
          "fill": {
            "field": "fill"
          }
        }
      }
    },
    {
      "type": "text",
      "from": {
        "data": "stages"
      },
      "encode": {
        "enter": {
          "x": {
            "signal": "(datum.x + datum.x2)/2"
          },
          "y": {
            "value": 17
          },
          "text": {
            "field": "label"
          },
          "align": {
            "value": "center"
          },
          "baseline": {
            "value": "middle"
          },
          "font": {
            "value": "Segoe UI"
          },
          "fontSize": {
            "value": 11
          },
          "fontWeight": {
            "value": "bold"
          },
          "fill": {
            "field": "color"
          }
        }
      }
    },
    {
      "type": "text",
      "encode": {
        "enter": {
          "x": {
            "value": 5
          },
          "y": {
            "value": 55
          },
          "text": {
            "value": "Category Family"
          },
          "fontSize": {
            "value": 11
          },
          "fontWeight": {
            "value": "bold"
          },
          "fill": {
            "value": "#17365D"
          }
        }
      }
    },
    {
      "type": "text",
      "from": {
        "data": "subheaders"
      },
      "encode": {
        "enter": {
          "x": {
            "field": "x"
          },
          "y": {
            "value": 49
          },
          "text": {
            "field": "label"
          },
          "align": {
            "value": "center"
          },
          "fontSize": {
            "value": 9
          },
          "fontWeight": {
            "value": "bold"
          },
          "fill": {
            "value": "#17365D"
          }
        }
      }
    },
    {
      "type": "text",
      "from": {
        "data": "subheaders"
      },
      "encode": {
        "enter": {
          "x": {
            "field": "x"
          },
          "y": {
            "value": 62
          },
          "text": {
            "field": "line2"
          },
          "align": {
            "value": "center"
          },
          "fontSize": {
            "value": 9
          },
          "fill": {
            "value": "#17365D"
          }
        }
      }
    },
    {
      "type": "text",
      "from": {
        "data": "categories"
      },
      "encode": {
        "enter": {
          "x": {
            "value": 5
          },
          "y": {
            "field": "cy"
          },
          "text": {
            "field": "Category"
          },
          "baseline": {
            "value": "middle"
          },
          "fontSize": {
            "value": 9
          },
          "fill": {
            "value": "#17365D"
          },
          "limit": {
            "value": 180
          }
        }
      }
    },
    {
      "type": "symbol",
      "from": {
        "data": "cells"
      },
      "encode": {
        "enter": {
          "x": {
            "signal": "datum.cx - 22"
          },
          "y": {
            "field": "cy"
          },
          "size": {
            "value": 48
          },
          "fill": {
            "field": "dot"
          }
        }
      }
    },
    {
      "type": "text",
      "from": {
        "data": "cells"
      },
      "encode": {
        "enter": {
          "x": {
            "signal": "datum.cx + 7"
          },
          "y": {
            "field": "cy"
          },
          "text": {
            "field": "label"
          },
          "align": {
            "value": "center"
          },
          "baseline": {
            "value": "middle"
          },
          "fontSize": {
            "value": 9
          },
          "fill": {
            "value": "#17365D"
          }
        }
      }
    },
    {
      "type": "rule",
      "encode": {
        "enter": {
          "x": {
            "value": 0
          },
          "x2": {
            "value": 790
          },
          "y": {
            "value": 315
          },
          "stroke": {
            "value": "#CCD5DF"
          }
        }
      }
    },
    {
      "type": "text",
      "encode": {
        "enter": {
          "x": {
            "value": 5
          },
          "y": {
            "value": 330
          },
          "text": {
            "value": "Total"
          },
          "fontSize": {
            "value": 10
          },
          "fontWeight": {
            "value": "bold"
          },
          "fill": {
            "value": "#17365D"
          }
        }
      }
    },
    {
      "type": "text",
      "encode": {
        "enter": {
          "x": {
            "value": 235
          },
          "y": {
            "value": 330
          },
          "text": {
            "value": "100%"
          },
          "align": {
            "value": "center"
          },
          "fontSize": {
            "value": 10
          },
          "fontWeight": {
            "value": "bold"
          },
          "fill": {
            "value": "#17365D"
          }
        }
      }
    },
    {
      "type": "text",
      "from": {
        "data": "total"
      },
      "encode": {
        "enter": {
          "x": {
            "value": 440
          },
          "y": {
            "value": 330
          },
          "text": {
            "field": "Label"
          },
          "align": {
            "value": "center"
          },
          "fontSize": {
            "value": 10
          },
          "fontWeight": {
            "value": "bold"
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
