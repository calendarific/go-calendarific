# go-calendarific

Official Go library for Calendarific Global Holiday API

# Installation

```
dep ensure -add https://github.com/calendarific/go-calendarific
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

