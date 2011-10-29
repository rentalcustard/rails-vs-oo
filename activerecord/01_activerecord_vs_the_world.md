!SLIDE 
# **ActiveRecord** #

!SLIDE bullets incremental
# ActiveRecord vs SRP #
* Typical AR model needs to change when...
* database schema changes
* business logic changes
* we want to present it differently

!SLIDE bullets
# ActiveRecord vs LSP #
* class Post is-a ActiveRecord::Base?!

!SLIDE bullets
# ActiveRecord vs ISP #
* Skinny controller, fat model?

!SLIDE bullets
# ActiveRecord vs DI and OCP? #
* OK AR, I'll let you off this one.

!SLIDE
# Some code #

!SLIDE smaller
    @@@ruby
    class OrdersController < ActionController::Base
      def close
        order = Order.find(params[:id])
        if params[:method] = "card"
          ExternalPaymentService.new.charge(params[:card])
        end
        order.closed = true
        order.save!
        Delivery.create! :status => :pending,
                         :order => order
        #render order success page
      rescue
        #redirect back with error
      end
    end

!SLIDE smaller
    @@@ruby
    class OrdersController < ActionController::Base
      def close
        #retrieval
        order.close!(params[:method], params[:card])
        Delivery.create! :status => :pending,
                         :order => order
        #rendering
      end
    end

    class Order < ActiveRecord::Base
      def close!(method, card_details=nil)
        if method == "card"
          ExternalPaymentService.new.charge(card_details)
        end
        self.closed = true
        self.save!
      end
    end

!SLIDE smaller
    @@@ruby
    class OrdersController < ActionController::Base
      def close
        #retrieval
        process = OrderProcess.new(order)
        process.close(params[:method], params[:card])
        #rendering 
      end
    end

    class OrderProcess
      def close(method, card_details=nil)
        if method == "card"
          ExternalPaymentService.new.charge(card_details)
        end
        Delivery.create! :status => :pending, :order => @order
        @order.close!
      end
    end

!SLIDE smaller
    @@@ruby
    class OrdersController < ActionController::Base
      def close
        #retrieval
        payment_handler = Payment.for(params[:method], 
                                              params[:card])
        process = OrderProcess.new(order, payment_handler)
        process.close
        #rendering
      end
    end

!SLIDE smaller

    @@@ruby
    class Payment
      def self.for(method, card_details=nil)
        if method == "card"
          CardPayment.new(card_details)
        else
          new
        end
      end

      #default payment handling code
    end

    class OrderProcess
      def close
        @payment_handler.handle_payment
        Delivery.create! :status => :pending, :order => @order
        @order.close!
      end
    end
