# Testing

As we study in Software Engineering class , a significant part of the software development process is testing. 

programmers some time make **errors**(mistakes) usually by misunderstanding the requirements .

Errors appears in our code as **faults(bugs)**.

Writing **test cases** help us to surface the **failures**(wrong behavior) in our programs ,so we can then connect every failure with its fault , and finally correct them.

Now lets use [An Introduction to Programming in Go by Caleb Doxsey](https://www.golang-book.com/books/intro) to take a look of **Testing** with GO :

Writing test cases is a good way to ensure quality and improve reliability.

Go includes a special program that makes writing tests easier.

The 'go test' command will look for any tests in any of the files in the current folder and run them. 

so let's create some tests in this example:

package math

import "testing"

    func TestAverage(t *testing.T) {
    var v float64
    v = Average([]float64{1,2})
    if v != 1.5 {
    t.Error("Expected 1.5, got ", v)
     }
    }

Now run this command:

    go test
You should see this:

    $ go test
    PASS

Tests are identified by starting a function with the word Test and taking one argument of type *testing.T.

 because we're testing the Average function, we name the test function *TestAverage*.


let's now test different combination of numbers :

    package math
    import "testing"
    type testpair struct {
    values []float64
    average float64
    }
    var tests = []testpair{
     { []float64{1,2}, 1.5 },
     { []float64{1,1,1,1,1,1}, 1 },
     { []float64{-1,1}, 0 },
    }
    func TestAverage(t *testing.T) {
    for _, pair := range tests {
    v := Average(pair.values)
    if v != pair.average {
      t.Error(
        "For", pair.values,
        "expected", pair.average,
        "got", v,
      )
    }
    }
    }

[Previous] (https://github.com/Afnan-Aldhahri/GO/blob/master/Resources/Run%20your%20first%20program.md ) - 
[Home] (https://github.com/Afnan-Aldhahri/GO/blob/master/README.md ) -
[ Next](https://github.com/Afnan-Aldhahri/GO/blob/master/Resources/How%20GO%20related%20to%20our%20class%20:%20Software%20Engineering.md)
