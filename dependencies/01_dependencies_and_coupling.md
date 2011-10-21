!SLIDE 
# Dependencies #

!SLIDE bullets incremental
# Explicit dependencies bad #
* Hard to test
* Increase coupling
* SRP - reasons to change!

!SLIDE bullets
# Hard to test #
* Fuck it, it's Ruby, we can test anything

!SLIDE bullets
# Increase coupling #
* Why? Well...
* Some code, take it through a couple of iterations

!SLIDE bullets
# SRP #
* 3 explicit dependencies
* Change implementation of one...
* OSNAP

!SLIDE bullets
# How to fix? #
* If controllers only responsible for one thing, have them create service objects and inject those dependencies.
* lol slides
