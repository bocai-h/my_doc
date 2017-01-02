# 批量导入Gem

批量导入是一件非常耗服务器性能的操作,大量数据的导入可能会导致服务器响应缓慢,操作超时等问题.这无异于一次ddos攻击.特别是直接通过rails的model一条条插入数据,产生的大量的io操作,而且还必须通过model层的事物来保证数据的一致性.如果能把所有的插入操作变成一次插入操作,不仅能提升效率,还可以避免数据一致性的问题.


rubygems里出现了一个不错的工具 BulkInsert可以达到我们的需求

~~~~
gem 'bulk_insert'

~~~~

[doc地址](http://www.rubydoc.info/gems/bulk_insert/1.2.1)