# LiquidHaskell: Refinement Types for Haskell

## Proposals 

### Internals (Expressiveness - Theory)

- I have a program in Coq or Dependent Haskell. Can I tranlsate it in liquidHaskell? No. One major obstacle:
  _Mutliparameter measures_.
   
     ```
     hasElem :: a -> [a] -> Bool
     hasElem _ []     = False
     hasElem y (x:xs) | x == y    = True
                      | otherwise = hasElem y xs
    ```
    
    Refines types of data list type constructor to
    
    ```
    []  :: forall y:a. {v:[a] | not (hasELem y v)}
    (:) :: forall y:a. x:a -> xs:[a] -> {v:[a] | hasELem y v <=> y == x || hasElem y xs}
    ```
    
    - Setting up semantics of `forall y:a` types
    - Examples, i.e. `denote :: Memory -> Statement -> Value`
    - Keep on with the translation (refinements cannot now depend on types)
    - The other direction? Coq cannot have diverging expressions.
    


### Usability (Error reporting)

  - SAFE? Yes: Code is Safe, No:
  - TARGET found counter-example? Yes: Code is Unsafe, No:
  - Then what?
      - Imprecise Specifications :
      
         ```
         foo :: Int -> Int 
         foo x = x + 1 
         
         bar :: x:Int -> {v:Int | v > x}
         bar x = foo x
         ```
         
      - Imprecise Theories, e.g. `(*)` is uninterpreted
      
      - Missing Qualifiers, etc
      
      How to help the programmer identify the error?
        - ML to classify what category the error belongs to
        - [Abductive Reasoning](http://www.cs.utexas.edu/~isil/pldi022-dillig.pdf) to figure out missing hypothesis?
        
      

### Applications

- Verify invariants in Machine Learning Programming.
 Kmeans has two steps
  - *Assignment step:* Assign each observation to the cluster whose mean yields the least within-cluster sum of squares (WCSS). Since the sum of squares is the squared Euclidean distance, this is intuitively the "nearest" mean.(*) 
  - *Update step:* Calculate the new means to be the centroids of the observations in the new clusters.
Since the arithmetic mean is a least-squares estimator, this also minimizes the within-cluster sum of squares (WCSS) objective.

To prove that at each step the error in kmeans is decreasing we need to prove that each of these steps decreases the error.

- Verify requests in [Haxl](https://github.com/facebook/Haxl/).

  Haxl has this concurrent [GenHaxl Monad](https://github.com/facebook/Haxl/blob/master/Haxl/Core/Monad.hs#L138-L138) that wrapps data fetches and then usses the [instantiation of Applicative](https://github.com/facebook/Haxl/blob/master/Haxl/Core/Monad.hs#L166-L183) to cuncurrenly run data fetches. 
  Users of Haxl (like a wrapper to the facebook API) perform datafetches using the [datafetch function.](https://github.com/facebook/Haxl/blob/master/example/facebook/FB.hs)
  If we give [datafetch](https://github.com/facebook/Haxl/blob/master/Haxl/Core/Monad.hs#L325) the appropriate preconditions, we can verify that all requests that are procced specify certain conditions.

 On this project, we can also use liquidHaskell (or dependent typing) to verify that coersing is actually safe.
Thought it seems that they are already using [dynamic checks] (https://github.com/facebook/Haxl/blob/master/Haxl/Core/StateStore.hs#L57).
This check is required because of the existential type of the [data cache](https://github.com/facebook/Haxl/blob/master/Haxl/Core/StateStore.hs#L40).



## Current Work

### Intro
  - Haskell
     - is it compiles it works
     - well typed programs cannot go wrong
     - well typed programs go wrong (div, sort)
### Measures
### Abstract Refinement Types
### Bounded Refinement Types
### Evaluation 
   - numbers 
   - Users (Colin)
