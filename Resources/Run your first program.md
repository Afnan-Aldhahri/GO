


Now, after we covered the basics of GO ,let’s use   [The Little Go Book  ](http://openmymind.net/assets/go/go.pdf) to start a simple GO program and try to compile and execute it. 

* Open your favorite text editor and write the following code:
    
    package main
    func main() {
     println("it's over 9000!")
    }

* Save the file as main.go.

* Save it anywhere you want; we don’t need to work with Go’s workspace for simple example.

* Open a command prompt and change the directory to where you saved the file. 

* Finally, run the program by entering:
    
    go run main.go

If everything worked, you should see it’s over 9000!.


*go run* is a handy command that compiles and runs your code. 

 It uses a *temporary* directory to build the program, executes it and then cleans itself up. 
 
If you want to see the location of the temporary file,run :

    go run --work main.go

To explicitly compile code, use go build:

    go build main.go

This will generate an executable main which you can run. 

Note :
**On Linux / OSX **, don’t forget that you need to prefix the executable with *dot-slash*,

so you need to type *./main*.


