# go-calendarific

Official Go library for Calendarific Global Holiday API

# Installation

```
dep ensure -add https://github.com/faisaltheparttimecoder/go-calendarific
```

# Usage / Example

+ Create a file called **main.go** & insert a script like below
    ```
    package main
    
    import (
        "fmt"
        "github.com/faisaltheparttimecoder/go-calendarific"
    )
    
    func main() {
        cp := calendarific.CalParameters {
            ApiKey: "<MY SECRET API KEY>",
            Country: "US",
            Year: 2019,
        }
        fmt.Println(cp.CalData())
    }
    ```

+ Run the program for data
    ```
    go run main.go
    ```

