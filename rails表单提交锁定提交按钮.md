#  rails表单提交锁定提交按钮

添加data-disable-with属性

~~~~
 button_tag(desc1, class: 'btn btn-primary', type: :submit, 'data-disable-with' => "#{I18n.t(:submiting)}") + button_tag(desc2, class: 'btn btn-white', type: :button, onclick: 'history.back()')
 
~~~~