# LabeledLoop

A simple package for R providing a support for labeled loop.
The semantics is similar with Java's labeled loop.
The labeled loops can be nested.

Here is a basic example:

    . %._.% for(i in 1:3) {  
      foo %._.% for (j in 1:3) {
        orz %._.% for (k in 1:3) {
          print(c(i, j, k))
          
          if (i == 3 && j == 3 && k == 2) {
            cat("escape from outmost loop\n")
            ._.() # break
          }
    
          if (i == 2 && j == 2) {
            cat("escape from innermost loop (orz)\n")
            ._.(orz) # break
          }
    
          if (i == 1 && j == 1 && k == 2) {
            cat("escape from foo\n")
            ._.(foo) # break
          }
        }
      }
    }

Then, the output looks like:

    [1] 1 1 1
    [1] 1 1 2
    escape from foo
    [1] 2 1 1
    [1] 2 1 2
    [1] 2 1 3
    [1] 2 2 1
    escape from innermost loop (orz)
    [1] 2 3 1
    [1] 2 3 2
    [1] 2 3 3
    [1] 3 1 1
    [1] 3 1 2
    [1] 3 1 3
    [1] 3 2 1
    [1] 3 2 2
    [1] 3 2 3
    [1] 3 3 1
    [1] 3 3 2
    escape from outmost loop
