#  rubymine version controller

rubymine自带的version controller在使用时给了我们很大的方便,可以让你轻松的找到刚刚生成或者刚刚修改的文件,而不必去茫茫的文件海中去找.


可是有一天,我突然发现我的rubymine的version controller失灵了,每次修改文件都没有记录,而且这种情况还是不确定的,时好时坏.我就一直怀疑是rubymine本身的问题,或者是java-jdk的问题.在open-jdk和oracle-jdk之间切来切去,然而并没有什么结果.

直到昨天,我灵机一动说换一个项目打开看看,诶!竟然是能用的.于是我今天就想重新把项目clone下来应该就好了.就在我把新项目弄下来后打算打开看看时,又重新打开老项目拷贝database.yml的时候,发现竟然可以用了.


**最后发现的真相是:不要通过打开项目目录的上层目录来打开项目,否则就会出现上述情况.估计rubymine是直接识别顶层目录下直接的.git文件来跟踪版本的**