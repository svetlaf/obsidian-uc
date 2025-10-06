---
fields:
  - name: fecha
    type: Date
    options:
      dateShiftInterval: 1 day
      dateFormat: DD-MM-YYYY
      defaultInsertAsLink: false
      linkPath: ""
    path: ""
    id: hgaLJO
  - name: Completitud
    type: Boolean
    options: {}
    path: ""
    id: m1TOcD
  - name: asignatura
    type: Multi
    options:
      sourceType: ValuesList
      valuesList:
        "1": derecho-procesal1
        "2": derecho-civil2
        "3": derecho-laboral
        "4": derecho-internacional-publico
        "5": teologia
    path: ""
    id: ObVbIT
  - name: presente/ausente
    type: Select
    options:
      sourceType: ValuesList
      valuesList:
        "1": presente
        "2": ausente
    path: ""
    id: O6XLra
version: "2.15"
limit: 20
mapWithTag: false
icon: notebook-pen
tagNames: 
filesPaths: 
bookmarksGroups: 
excludes: 
extends: 
savedViews: []
favoriteView: 
fieldsOrder:
  - O6XLra
  - ObVbIT
  - hgaLJO
  - m1TOcD
---
