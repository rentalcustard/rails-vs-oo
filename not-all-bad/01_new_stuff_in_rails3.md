!SLIDE 
# **It's not all bad** #

!SLIDE center

![Trollface](trollface.png)

!SLIDE
# Custom validators #
    @@@ruby
    class Order < ActiveRecord::Base
      validates_with OrderValidator
    end

    class OrderValidator
      def validate(record)
        record[:errors] #do stuff with it
      end
    end

!SLIDE smaller
# Custom responders #
    @@@ruby
    class OrdersController < ActionController::Base
      protected
      def responder
        CachingResponder
      end
    end

    class CachingResponder < ActionController::Responder
      def to_html
        if get? && resource.respond_to?(:updated_at)
          updated = resource.updated_at.utc
          return if controller.
                      fresh_when(:last_modified => updated)
        end
          super
        end
      end
    end

!SLIDE
# Other stuff post-Rails 3? #
