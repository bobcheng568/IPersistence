# IPersistence

测试工程地址：https://github.com/bobcheng568/IPersistence_test

###Q&A

Q1、Mybatis动态sql是做什么的？都有哪些动态sql？简述一下动态sql的执行原理？

A1：Mybatis常用的动态sql标签有：if、where、foreach、when等等。动态sql标签可以完成逻辑判断并动态地拼接sql。基本原理是通过OGNL表达式从参数对象中取值，并根据表达式做逻辑判断，根据判断结果来拼接sql。



Q2、Mybatis是否支持延迟加载？如果支持，它的实现原理是什么？

A2：Mybatis支持延迟加载，基本原理是通过动态代理生成代理实体类，只查询实体类的主属性。当通过getXXX方法获取副属性的值时，再通过sql去数据库查询副属性，并将结果setXXX给副属性。



Q3、Mybatis都有哪些Executor执行器？它们之间的区别是什么？

A3：Mybatis有SimpleExecutor、CachingExecutor、BatchExecutor等。当开启二级缓存时，会调用CachingExecutor作为执行器；当进行批量操作时，会调用BatchExecutor作为执行器；默认是调用SimpleExecutor作为执行器。



Q4、简述下Mybatis的一级、二级缓存（分别从存储结构、范围、失效场景。三个方面来作答）？

A4：Mybatis一级缓存的存储结构是MAP，作用范围是sqlSession，当同一sqlSession进行了增删改操作后失效；Mybatis二级缓存的存储结构也是MAP，作用范围是namespace，当同一namespace进行了增删改操作后失效。一级缓存默认开启，二级缓存默认关闭，一般用Redis作为Mybatis分布式缓存。一级缓存中缓存的是实体对象，二级缓存中缓存的不是对象而是数据。



Q5、简述Mybatis的插件运行原理，以及如何编写一个插件？

A5：Mybatis插件类似于拦截器，对Executor、StatementHandler、ParameterHandler、ResultSetHandler四大对象进行拦截，增强他们的方法。自定义插件需要实现Interceptor接口，实现intercept方法。指定当前插件拦截的是哪个对象的哪个方法（@Intercepts、@Signature）。在sqlMapConfig.xml中进行注册。