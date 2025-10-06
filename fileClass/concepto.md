---
fields:
  - name: autor o creador
    type: File
    options: {}
    path: ""
    id: ERLIsK
  - name: fecha-creación-o-descubrimiento
    type: Date
    options:
      dateShiftInterval: 1 day
      dateFormat: yyyy
      defaultInsertAsLink: false
      linkPath: ""
    path: ""
    id: L9rfU2
  - name: concepto-padre
    type: MultiFile
    options: {}
    path: ""
    id: ncdU6l
  - name: concepto-hijo
    type: Lookup
    options:
      autoUpdate: true
      dvQueryString: |-
        dv.pages().where(p => {
          const frontmatterClasses = dv.array(p.fileClass).flatMap(c => typeof c === "string" ? c.split(/,\s*/) : []);
          const inlineClasses = dv.array(p["fileClass"]).flatMap(c => typeof c === "string" ? c.split(/,\s*/) : []);
          return [...frontmatterClasses, ...inlineClasses].includes("concepto");
        })
      targetFieldName: concepto-padre
      outputType: LinksList
      builtinSummarizingFunction: Count
      customListFunction: page.file.name
      customSummarizingFunction: return pages.length
      summarizedFieldName: ""
    path: ""
    id: I9RutY
version: "2.23"
limit: 20
mapWithTag: false
icon: book-a
tagNames: 
filesPaths: 
bookmarksGroups: 
excludes:
  - Completitud
extends: clase
savedViews: []
favoriteView: 
fieldsOrder:
  - I9RutY
  - ncdU6l
  - ERLIsK
  - L9rfU2
---
