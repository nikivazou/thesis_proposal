# LiquidHaskell: Refinement Types for Haskell

- Verify requests in [Haxl](https://github.com/facebook/Haxl/)
  Haxl has this concurrent [GenHaxl Monad](https://github.com/facebook/Haxl/blob/master/Haxl/Core/Monad.hs#L138-L138) that wrapps data fetches and then usses the [instantiation of Applicative](https://github.com/facebook/Haxl/blob/master/Haxl/Core/Monad.hs#L166-L183) to cuncurrenly run data fetches. 
  Users of Haxl (like a wrapper to the facebook API) perform datafetches using the [datafetch function.](https://github.com/facebook/Haxl/blob/master/example/facebook/FB.hs)
  If we give [datafetch](https://github.com/facebook/Haxl/blob/master/Haxl/Core/Monad.hs#L325) the appropriate preconditions, we can verify that all requests that are procced specify certain conditions.

 On this project, we can also use liquidHaskell (or dependent typing) to verify that coersing is actually safe.
Thought it seems that they are already using [dynamic checks] (https://github.com/facebook/Haxl/blob/master/Haxl/Core/StateStore.hs#L57).
This check is required because of the existential type of the [data cache](https://github.com/facebook/Haxl/blob/master/Haxl/Core/StateStore.hs#L40).
