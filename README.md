Table of Contents  git支持3个空格，本地支持2个空格
=================

   * [日常异常](#日常异常)
         * [JAVA相关](#java相关)
            * [java继承对象使用lombok @Data注解错误](#java继承对象使用lombok-data注解错误)
            * [spring打包jar读取resource资源读取为空](#spring打包jar读取resource资源读取为空)
            
# 日常异常

### JAVA相关

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