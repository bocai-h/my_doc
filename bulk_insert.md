# rails后台处理批量数据(bulk_insert) 

通过循环插入数据到数据库导致了大量的io消耗,因此效率很低下.bulk_insert通过处理时将生成的sql一起发送到数据库,所以减少了大量的io,效率也就因此提升了.

[bulk_insert文档地址](http://www.rubydoc.info/gems/bulk_insert/1.2.1)