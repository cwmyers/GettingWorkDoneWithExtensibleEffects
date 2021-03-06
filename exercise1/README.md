# Exercise 1: File Scanner without Eff

This implementation uses regular Scala features to build a large file scanner:

- File system operations are done directly inline, primarily using the `java.nio.file.Files` API provided in Java 8. This
is preferable to the operations offered through the older `java.io.File` API because error conditions are signalled by an
exception rather than simply returning an uninformative `null`.

- Error handling is by throwing exceptions which will bubble to the top.

## Tasks

### :arrow_forward: _Run Code_

Run the scanner on current directory with `solutionExercise1/run .`  Does the result seem correct?

Try it on some larger directory of your computer.

### :mag: _Study Code_

Study the algorithm used by the scanner. The key data structure is a `PathScan`, which contains a sorted list of the
largest N files and their sizes in bytes, plus a count of total files scanned and total bytes across all files.

Note how the scanner must combine `PathScan`s of differing subdirectories together to yield
a single `PathScan` that summarizes both the *top N* files and *total* files visited. This combine operation has a
[Monoid](http://typelevel.org/cats/typeclasses/monoid.html) structure.

### :pencil: _Write Code_

Complete the [Monoid instance for PathScan](src/main/scala/scan/Scanner.scala#L42).

### :arrow_forward: _Run Code_

Run the unit tests with `exercise1/test` to verify your Monoid implementation.

### :mag: _Study Code_

Examine the [ScannerSpec](src/test/scala/scan/ScannerSpec.scala).

Note how much of the test is involved with creating- and cleaning up- actual files. It would be nice
is we could separate testing the algorithm from the filesystem. How should this be done?
