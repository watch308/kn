### 整合 MyBabtis 

添加依赖。
定义 mapper 接口。
定义 mapper 映射文件。
定义 mybatis 配置文件（可选）。
在 application.properties 中配置数据源、配置 mybatis 配置文件的位置、指定 mapper 映射文件的扫描路径。
在启动类上定义 @MapperScan 注解，通过 basePackages 属性指定 mapper 接口所在的包、通过 annotationClass 属性指定 mapper 接口使用的注解。
**在application.properties中做如下配置：


* xml的namespace指向对应的接口  
* 接口与xml名字相同  
* 接口的方法名与xml的id相同
* 在application.properties中配置mapper.xml的包地址
    * mybatis.mapper-locations=classpath:/mapper/*.xml**
* 将xxxxmapper.xml的包暴露

### 原生
