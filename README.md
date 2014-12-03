A reader for Microsoft's [OLE Property Set Format](http://msdn.microsoft.com/en-au/library/dd942421.aspx).

Example usage:

    file, _ := os.Open("test/test.doc")
    defer file.Close()
    doc, err := mscfb.NewReader(file)
    if err != nil {
      log.Fatal(err)
    }
    props := msoleps.New()
    for entry, err := doc.Next(); err == nil; entry, err = doc.Next() {
      if msoleps.IsMSOLEPS(entry.Initial) {
        if oerr := props.Reset(doc); oerr != nil {
          log.Fatal(oerr)
        }
        for prop := range props.Property {
          fmt.Printf("Name: %s; Type: %s; Value: %v", prop.Name, prop.Type(), prop)
        }
      }
    }

Install with `go get github.com/richardlehane/msoleps`

*I'm being developed and am not yet ready...*

[![Build Status](https://travis-ci.org/richardlehane/msoleps.png?branch=master)](https://travis-ci.org/richardlehane/msoleps)