!SLIDE 
# **ActiveRecord** #

!SLIDE bullets incremental
# ActiveRecord vs SRP #
* Class needs to change when...
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
* No more than anything else in Rails

!SLIDE
# Some code #

!SLIDE smaller
    @@@ruby
    class OrdersController < ActionController::Base
      def close
        order = Order.find(params[:id])
        if params[:method] = "card"
          order.closed = true
          CardPaymentUtil.new.charge(params[:card])
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
        order = Order.find(params[:id])
        order.close!(params[:method], params[:card])
        Delivery.create! :status => :pending,
                         :order => order
        #render order success page
      rescue
        #redirect back with error
      end
    end

    class Order < ActiveRecord::Base
      def close!(method, card_details=nil)
        if method == "card"
          CardPaymentUtil.new.charge(card_details)
        end
        self.closed = true
        self.save!
      end
    end

!SLIDE smaller
    @@@ruby
    class OrdersController < ActionController::Base
      def close
        order = Order.find(params[:id])
        reconciler = OrderReconciler.new(order)
        reconciler.close(params[:method], params[:card])
        #render order success page
      rescue
        #redirect back with error
      end
    end

    class OrderReconciler
      def initialize(order); @order = order; end

      def close(method, card_details=nil)
        if method = "card"
          CardPaymentUtil.new.charge(card_details)
        end
        @order.closed = true
        Delivery.create! :status => :pending, :order => @order
        @order.save!
      end
    end

!SLIDE smaller
    @@@ruby
    class OrdersController < ActionController::Base
      def close
        order = Order.find(params[:id])
        payment_handler = PaymentHandler.for(params[:method], 
                                              params[:card])
        reconciler = OrderReconciler.new(order, payment_handler)
        reconciler.close
        #render order success page
      rescue
        #redirect back with error
      end
    end

!SLIDE smaller

    @@@ruby
    class PaymentHandler
      def self.for(method, card_details=nil)
        if method == "card"
          CardPaymentUtil.new(card_details)
        else
          new
        end
      end
      
      #default payment handling code
    end

    class OrderReconciler
      def close
        @payment_handler.handle_payment
        Delivery.create! :status => :pending, :order => @order
        @order.close!
      end
    end
    
!SLIDE smaller
    @@@ruby
    class Order < ActiveRecord::Base
      def close!
        self.closed = true
        self.save!
      end
    end
