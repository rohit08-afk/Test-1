
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "description": "Supplier readiness stage matrix",
  "data": {"name": "dataset"},
  "background": "transparent",
  "width": {"step": 82},
  "height": {"step": 19},
  "transform": [
    {
      "calculate": "datum['Category Family']",
      "as": "Category"
    },
    {
      "calculate": "isValid(datum['Attendance Rate']) ? datum['Attendance Rate'] : null",
      "as": "Rate"
    },
    {
      "calculate": "datum.Rate == null ? '—' : format(datum.Rate, '.0%')",
      "as": "Supplier Label"
    },
    {
      "calculate": "'100%'",
      "as": "Reach"
    },
    {
      "calculate": "'—'",
      "as": "RO"
    },
    {
      "calculate": "datum['Supplier Label']",
      "as": "Supplier"
    },
    {
      "calculate": "'—'",
      "as": "Commit"
    },
    {
      "calculate": "'—'",
      "as": "Prove"
    },
    {
      "calculate": "'—'",
      "as": "Ready"
    },
    {
      "fold": [
        "Reach",
        "RO",
        "Supplier",
        "Commit",
        "Prove",
        "Ready"
      ],
      "as": ["Stage", "Value"]
    },
    {
      "calculate": "datum.Stage == 'Reach' ? '#E5F2FF' : datum.Stage == 'RO' || datum.Stage == 'Supplier' ? '#E5F6EC' : datum.Stage == 'Commit' ? '#FFF6DD' : datum.Stage == 'Prove' ? '#E9EEFA' : '#E2F7F7'",
      "as": "Cell Color"
    },
    {
      "calculate": "datum.Stage == 'Reach' ? '#20A56C' : datum.Stage == 'Supplier' ? '#FFBF3C' : '#BFC3C8'",
      "as": "Dot Color"
    }
  ],
  "encoding": {
    "x": {
      "field": "Stage",
      "type": "ordinal",
      "sort": [
        "Reach",
        "RO",
        "Supplier",
        "Commit",
        "Prove",
        "Ready"
      ],
      "axis": {
        "title": null,
        "labelFontSize": 9,
        "labelAngle": 0,
        "labelLimit": 90,
        "ticks": false,
        "domain": false
      }
    },
    "y": {
      "field": "Category",
      "type": "nominal",
      "sort": "ascending",
      "axis": {
        "title": "Category Family",
        "titleFontSize": 10,
        "labelFontSize": 8,
        "labelLimit": 165,
        "labelPadding": 5,
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
        "xOffset": -20
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
        "fontWeight": "normal",
        "color": "#17365D",
        "xOffset": 10
      },
      "encoding": {
        "text": {
          "field": "Value",
          "type": "nominal"
        }
      }
    }
  ],
  "config": {
    "view": {"stroke": null},
    "font": "Segoe UI"
  }
}
