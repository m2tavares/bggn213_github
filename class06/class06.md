# class06
Maria Tavares (PID A69036242)

- [A second function](#a-second-function)
- [A protein generating function](#a-protein-generating-function)

All functions in R have at least 3 things: - A **name**, we pick this
and use it to call our function, - Input **arguments** (there can be
multiple), - The **body** lines of R code that do the work. \##Maria’s
first R function Write a function to add some numbers:

``` r
add <- function (x, y=1) {
x+y
}
```

Now we can call this function:

``` r
add(10, 100)
```

    [1] 110

## A second function

Write a function to generate random nucleotide sequences of a user
specified length: The ‘sample()’ function can be helpful here.

``` r
sample (c("A", "C", "G","T"), size=5, replace = TRUE)
```

    [1] "A" "G" "C" "G" "C"

I want the a 1 element long character vector that

``` r
v <- sample (c("A", "C", "G", "T"), size = 50, replace = TRUE)
paste(v, collapse = "")
```

    [1] "GTTATATGGAGATCGCCGCTGCATGAAGTCTCTAGCAGCTCTCCGAATGC"

Turn this into my first wee function

``` r
generate_dna <- function(size = 50) {
  v <- sample(c("A", "C", "G", "T"), size = size, replace = TRUE)
  paste (v, collapse = "")
}
```

Test it

``` r
generate_dna(60)
```

    [1] "GCTCAGTGAGTGGAAAAATTAAATCCCGTTGTTAAATTTCTGAGACAAGCCCCACAGTTC"

``` r
fasta <- FALSE
if(fasta) {
  cat("HELLO You!")
}
```

Add the ability to return a multi-element f=vector or a single element
fasta like vector.

``` r
generate_fasta <- function(size = 50, fasta = TRUE) {
  v <- sample(c("A", "C", "G", "T"), size = size, replace = TRUE)
  s <- paste (v, collapse = "")
  
  if(fasta) {
    return (s)
  } else { 
    return (v)
  }
}
```

``` r
generate_fasta(10, fasta=TRUE)
```

    [1] "TCCTAGCGCA"

## A protein generating function

``` r
generate_protein <- function(size = 50, fasta = TRUE) {
  aa <- c("A", "R", "N", "D", "C", "Q", "E", "G", "H", "I", 
          "L", "K", "M", "F", "P", "S", "T", "W", "Y", "V")
  v <- sample(aa, size = size, replace = TRUE)
  s <- paste(v, collapse = "")
  
  if(fasta) {
    return(s)
  } else {
    return(v)
  }
}
```

``` r
generate_protein(6)
```

    [1] "PVYCVH"

Use our new `generate_protein()` function to make random protein
sequences of lenght 6 to 12 (one length 6, one length 7…etc)

One way to do this is “brute force”

``` r
generate_protein(6)
```

    [1] "TKRCAG"

``` r
generate_protein(7)
```

    [1] "MSCWFFK"

``` r
generate_protein(8)
```

    [1] "GYNRLWSA"

A second way is to use a `for()` loop:

``` r
lenghts <- 6:12
lenghts 
```

    [1]  6  7  8  9 10 11 12

``` r
for (i in lenghts) {
  cat(">", i, "\n", sep = "")
  aa <- generate_protein(i)
  cat(aa)
  cat("\n")
}
```

    >6
    HQWDVQ
    >7
    QLTEEMM
    >8
    IAFYMILS
    >9
    DYLVGRECK
    >10
    YCKDMQPDQH
    >11
    QEVWNSVWLIC
    >12
    FLRIRECSHGLC

A third, and better way to solve this is the `apply()` family of
functiond, specifically `sapply()` function in this case.

``` r
sapply(6:12, generate_protein)
```

    [1] "WCFSQY"       "SCSKENC"      "DLDWWSRL"     "NRFWDYNML"    "MRHDPSRSTA"  
    [6] "KQCQKTHRHST"  "GHSSQATWITDG"
