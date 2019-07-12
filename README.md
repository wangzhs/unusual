# 日常异常

[TOC]

### JAVA相关

#### java继承对象使用lombok @Data注解错误
**问题原因**:在子类对象使用@Data注解，但是未重写equals和hashcode方法，导致只比较子类对象是否相等，不关注父类属性

**解决方法**:在子类对象上加 @EqualsAndHashCode(callSuper = true)