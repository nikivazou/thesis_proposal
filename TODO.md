- Verification Conditions
Alex : Code->Typing : show the subtyping relation first and give it some intuition. It's not clear what the VC's mean or why they are important. All we know at this point is that there is something called a VC - we need to know what these constraints correspond to
me: maybe get rid of the recification conditions? do we need them? refine this section

- 31: Add Ord to data [a] with ...<= ... even if it's not implemented.


- Panos Haxl things

  - Is there any additional challenges that arise in this setting? 
It seems that you can just rename some predicates you had in 
earlier examples and carefully setup the privacy primitives you 
described.
  - How would LH be able to reason about cryptographic/serialization 
functions? (these could arise through credential that are sent over REST
calls and validated at the server side)
  - Is multi-threading an issue for LH?
  - Could there be a way of describing the privacy/security policies in 
_one_ place instead of having to go through every exposed function 
and carefully annotating input and output types.

- John on Haxl

* You explained a lot of stuff about Haxl without explaining why LH would be
  useful here. Maybe move the privacy verification stuff to the beginning of the
  Haxl stuff?
  Also, could you present the Haxl material at a higher level (i.e., less code
  or no code)? Maybe:
    Haxl provides these ops:
      * X Y Z
    LH can verify using these predicate ideas:
      * X -> P1
        Y -> P2
        Z -> P3
        
