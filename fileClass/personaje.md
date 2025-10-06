---
limit: 20
mapWithTag: false
icon: user
tagNames: 
filesPaths: 
bookmarksGroups: 
excludes:
  - fecha
extends: clase
savedViews: []
favoriteView: 
fieldsOrder:
  - w3FYF1
  - WMHsB7
version: "2.17"
fields:
  - name: época
    type: Date
    options:
      dateShiftInterval: 1 day
      dateFormat: YYYY-YYYY
      defaultInsertAsLink: false
      linkPath: ""
    path: ""
    id: WMHsB7
  - name: conceptos-o-creaciones
    type: Lookup
    options:
      autoUpdate: true
      dvQueryString: dv.pages('').where(p => p.fileClass == 'concepto')
      targetFieldName: autor o creador
      outputType: LinksList
      builtinSummarizingFunction: Count
      customListFunction: page.file.name
      customSummarizingFunction: return pages.length
      summarizedFieldName: ""
    path: ""
    id: w3FYF1
---
