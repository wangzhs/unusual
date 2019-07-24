* [日常异常](#日常异常)
    * [JAVA](#java)
        * [java继承对象使用lombok @Data注解错误](#java继承对象使用lombok-data注解错误)
        * [spring打包jar读取resource资源读取为空](#spring打包jar读取resource资源读取为空)
    * [数据库](#数据库)
      * [MONGO](#mongo)
        * [未创建索引分页查询最后一页导致500错误](#未创建索引分页查询最后一页导致500错误)

            
# 日常异常

## JAVA

#### java继承对象使用lombok @Data注解错误

**问题原因**:在子类对象使用@Data注解，但是未重写equals和hashcode方法，导致只比较子类对象是否相等，不关注父类属性

**解决方法**:在子类对象上加 @EqualsAndHashCode(callSuper = true)

#### spring打包jar读取resource资源读取为空

**问题原因**:打包后Spring试图访问文件系统路径，但无法访问JAR中的路径

**解决方法**:可以使用如下代码读取  必须是**InputStream**

```
ClassPathResource resource = new ClassPathResource("application.yml"); // resource下文件
InputStream inputStream = resource.getInputStream();
```

## 数据库

### MONGO

#### 未创建索引分页查询最后一页导致500错误

**问题异常**:
```
com.mongodb.MongoQueryException: Query failed with error code 17144 and error message
 'Plan executor error during find: Overflow sort stage buffered data usage
of 33568115 bytes exceeds internal limit of 33554432 bytes' 
```

**问题原因**:mongodb的sort操作是把数据拿到内存中再进行排序的，为了节约内存，默认给sort操作限制了最大内存为32Mb，当数据量越来越大直到超过32Mb的时候就抛出异常了.

**解决方法**:给mongo数据库对应字段创建索引。

### CASSANDRA

#### 一次性插入数据量过大导致,大于默认配置的大小

**问题异常**
```
Batch too large
```

**问题原因**:(默认: 每一批50KB) 任何批量大小超过该值的都会失败。默认的值是10 Xbatch_size_warn_threshold_in_kb的值。

**解决方法**:修改 batch_size_fail_threshold_in_kb 默认配置，但是要注意吞吐量

**原文参考**: [Cassandra 3.x官方文档 翻译](https://blog.csdn.net/qq_32523587/article/details/53982900)
