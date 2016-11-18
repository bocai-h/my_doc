# rails(4.2.5)升级笔记


- update_all参数变更(只有一个参数)
~~~~
  # 原写法
   Irm::BusinessObject.update_all(["auto_generate_flag =?","U"],["auto_generate_flag = ?",Irm::Constant::SYS_YES]) 
  
   #现写法
    Irm::BusinessObject.update_all("auto_generate_flag ='U',auto_generate_flag = '#{Irm::Constant::SYS_YES}'")
~~~~
- paperclip 4.0的用法发生变更(安全性上更好)
> paperclip  4.0及以上版本要求必须加入content-type和file_name验证以防止XSS攻击,如果没有会抛出Paperclip::Errors::MissingRequiredValidatorError异常

参见[paperclip安全验证](https://github.com/thoughtbot/paperclip)

- 清除编译过的资源要用
~~~~
  rake assets:clobber
  
~~~~
- ActiveRelation对象update_all写法变更,原写法会报错

~~~~
# 原写法

Irm::BusinessObject.update_all(["auto_generate_flag =?","U"],["auto_generate_flag = ?",Irm::Constant::SYS_YES])

# 新写法
Irm::BusinessObject.where("auto_generate_flag =?","U").update_all(auto_generate_flag:Irm::Constant::SYS_YES)

~~~~

- 为了系统能更好的支持多语言(针对文本信息下的错误消息提示),特别制定如下策略:
> 凡是model中的验证的message应该写成字典文件中标签,然后在各个语言环境中为其加入翻译版本,标签与普通消息的区别是带有下划线.所以如果不带下划线的消息会不经过翻译直接显示.

~~~~
  validates_attachment_content_type :avatar, content_type: /\Aimage/,message: "file_type_error"
  
  #zh.yml
    file_type_error: 文件类型错误
 #en.yml
    file_type_error: file type error
~~~~

- 现在jquery-validate是通过gem包来管理的,因此要对其提示消息进行客户化定制时不能采用原来的那种简单粗暴的方式直接改源文件了.由于尝试过在另外一个加载的js文件中写如下代码,但是却不生效,所以方案为写在header中,保证在同一个页面上设置就能生效

~~~~
  <script>
   jQuery.validator.setDefaults({
       errorPlacement: function (error, element) {
           error.insertAfter($(element).closest("span"));
       }
   });
</script>

~~~~