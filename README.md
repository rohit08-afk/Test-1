
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "description": "Supplier Readiness Data Test",
  "data": {
    "name": "dataset"
  },
  "width": 350,
  "height": {
    "step": 22
  },
  "transform": [
    {
      "calculate": "isValid(datum['Attendance Rate']) ? datum['Attendance Rate'] : null",
      "as": "Rate"
    },
    {
      "calculate": "datum.Rate == null ? '—' : format(datum.Rate, '.0%')",
      "as": "Rate Label"
    }
  ],
  "mark": {
    "type": "text",
    "fontSize": 12,
    "color": "#17365D",
    "align": "left"
  },
  "encoding": {
    "y": {
      "field": "Category Family",
      "type": "nominal",
      "sort": "ascending",
      "axis": {
        "title": null,
        "labelFontSize": 10,
        "labelLimit": 190,
        "domain": false,
        "ticks": false
      }
    },
    "x": {
      "value": 20
    },
    "text": {
      "field": "Rate Label",
      "type": "nominal"
    }
  },
  "config": {
    "view": {
      "stroke": null
    },
    "font": "Segoe UI"
  }
}
