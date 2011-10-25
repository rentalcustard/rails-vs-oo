!SLIDE 
# **ActiveRecord** #

!SLIDE
# Typical AR Class #

!SLIDE bullets incremental
# ActiveRecord vs SRP #
* Class needs to change when...
* database schema changes
* business logic changes
* we want to present it differently

!SLIDE bullets
# ActiveRecord vs SRP #
* Class needs to change when...
* Anything happens!
* 
* 

!SLIDE bullets
# ActiveRecord vs Encapsulation #
* Default accessors
* Finders open to all

!SLIDE smaller
    @@@ruby
    class LineItem < ActiveRecord::Base
      #validations
      #associations
      #presentation methods
    end

    class OrdersController < ActionController::Base
      def show
        pre_tax = @order.line_items.
                    sum {|item| item.quantity * item.price}
        @order_total = pre_tax * @order.tax_rate
      end
    end

!SLIDE smaller
    @@@ruby
    class OrdersController < ActionController::Base
      def show
        pre_tax = @order.line_items.
                    sum do |item|
                      if item.quantity > 3
                        (item.quantity * 0.75) * item.price
                      else
                        item.quantity * item.price
                      end
                    end
        @order_total = pre_tax * @order.tax_rate
      end
    end

!SLIDE smaller
    @@@ruby
    class LineItem < ActiveRecord::Base
      def total_price
        if self.quantity > 3
          self.quantity * 0.75 * self.price
        else
          self.quantity * self.price
        end
      end
    end

    class OrdersController < ActionController::Base
      def show
        pre_tax = @order.line_items.sum(&:total_price)
        @order_total = pre_tax * @order.tax_rate
      end
    end


!SLIDE smaller
    @@@ruby
    class Order < ActiveRecord::Base
      def total_price
        self.line_items.sum(&:total_price) * self.tax_rate
      end
    end

    class OrdersController < ActionController::Base
      def show
        @order_total = @order.total_price
      end
    end

!SLIDE
# Tell don't ask #

!SLIDE
# Mutate via business logic methods #

!SLIDE
# Presenters (again) #
