!SLIDE
# Views aren't objects :'( #

!SLIDE bullets incremental
# View logic progression #
* Logic in the view
* Logic in a helper
* Logic from helper -> model
* Logic from model -> presenter

!SLIDE
# Logic in the view #
    @@@haml
    - @widgets.each do |widget|
      %p= widget.name
      - if widget.owned_by?(current_user)
        %p= widget.details

!SLIDE
# View -> helper #
    @@@ruby
    def display_widget(widget)
      html = ""
      html << "<p>#{widget.title}</p>"
      if widget.owned_by?(current_user)
        html << "<p>#{widget.details</p>"
      end
      html
    end

!SLIDE
# Helper -> model #
    @@@ruby
    class Widget < ActiveRecord::Base
      def details_for(user)
        if self.owned_by?(user)
          self.details
        else
          ""
        end
      end
    end

!SLIDE
# Model -> Presenter #
    @@@ruby
    class WidgetPresenter
      def initialize(widget)
        @widget = widget
      end

      def details(user)
        #old logic here
      end
    end

!SLIDE bullets incremental
# Why? #
  * Watch your models' BMI    
  * Presenters can look like models
  * Presenters control access to their data
