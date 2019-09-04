# go-calendarific

Official Go library for Calendarific Global Holiday API

# Installation

```
dep ensure -add github.com/calendarific/go-calendarific
```

# Usage / Example

+ Create a file called **main.go** & insert a script like below
    ```
    package main
    
    import (
    	"fmt"
    	"github.com/calendarific/go-calendarific"
    	"os"
    )
    
    func main() {
    
        // Loading the paramater struct
    	cp := calendarific.CalParameters{
    		ApiKey:  "<MY SECRET API KEY>",
    		Country: "US",
    		Year:    2019,
    	}
    	
    	// It returns a response struct
    	holidays, err := cp.CalData()
    	if err != nil {
    		fmt.Println(err)
    		os.Exit(1)
    	}
    	
    	fmt.Println(holidays)
    }
    ```

    Check out the [file](https://github.com/calendarific/go-calendarific/blob/master/main.go) for parameter struct and response struct.

+ Run the program for data
    ```
    go run main.go
    ```

**Bonus**

In case your project needs the states data, you might use the below example on how to Interpretate a state interface type.

    ```
    package main

    import (
        "fmt"
        "github.com/calendarific/go-calendarific"
        "github.com/ryanuber/columnize"
        "os"
    )

    func main() {

        // Initialize a column format display
        var output []string

        // Parameters
        cp := calendarific.CalParameters{
            ApiKey:  "MY SECRET",
            Country: "US",
            Year:    2019,
        }

        // Response
        holidays, err := cp.CalData()
        if err != nil {
            fmt.Printf("Encountered error: %v", err)
            os.Exit(1)
        }

        // Reading the response and formatting the state struct
        // State struct is arbitrary datatype, some of the data is of
        // string format and some are of array, so we use the below procedure 
        // to check what kind datatype is it and take necessary action.
        for _, pv := range holidays.Response.Holidays {
            s := pv.States
            switch val := s.(type) {
            case string:
                // Its a string
                output = append(output, fmt.Sprintf("%s|%s|%s", pv.Name, pv.Date.Iso, pv.States))
            case int:
                // Its an integer
                output = append(output, fmt.Sprintf("%s|%s|%d", pv.Name, pv.Date.Iso, pv.States))
            case []interface{}:
                // Its an array
                for _, v := range val {
                    j := v.(map[string]interface{})
                    output = append(output, fmt.Sprintf("%s%s|%s|%s", " ├── ", pv.Name, pv.Date.Iso, j["name"]))
                }
            default:
                output = append(output, fmt.Sprintf("%s|%s|%s", pv.Name, pv.Date.Iso, "Unknown Type"))
            }
        }

        // Format configuration to print
        // the data in a column forat
        config := columnize.DefaultConfig()
        config.NoTrim = true

        // Print the output on column format
        result := columnize.Format(output, config)
        fmt.Println(result)
    }
    ```
