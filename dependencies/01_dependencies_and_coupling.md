!SLIDE 
# **Dependencies** #

!SLIDE bullets incremental
# Explicit dependencies bad #
* Hard to test
* Increase coupling
* SRP - reasons to change!

!SLIDE bullets
# Hard to test #
* Fuck it, it's Ruby, we can test anything

!SLIDE bullets
# Increased coupling #
* Some code, take it through a couple of iterations

!SLIDE bullets
# How to fix? #
* Small objects encapsulating behaviours in reusable fashion

!SLIDE

    @@@ruby
    class SavingsCalculator
      include CurrencyFormatting
      def initialize(tasks)
        @tasks = tasks
      end

      def total
        @tasks.sum(&:saved_amount)
      end

      def formatted_total
        format(total)
      end
    end

