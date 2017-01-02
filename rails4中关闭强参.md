# rails 4中关闭Strong Parameters

在config/application.rb中配置如下就可以关闭强参

~~~~
 config.action_controller.permit_all_parameters = true
 
~~~~

~~~~

module ActiveModel
  module ForbiddenAttributesProtection
    protected
      def sanitize_for_mass_assignment(attributes)
          attributes
      end
      alias :sanitize_forbidden_attributes :sanitize_for_mass_assignment
  end
end

~~~~