Ioc核心

零碎知识：

1.@Nullable：如果可以传入NULL值，则标记为@Nullable，如果不可以，则标注为@Nonnull

2.Object是所有类的基类，这个你可以查询[jdk](https://www.baidu.com/s?wd=jdk&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)文档了解，所有类都继承自Object。Object ...objects这种参数定义是在不确定方法参数的情况下的一种多态表现形式。即这个方法可以传递多个参数，这个参数的个数是不确定的。这样你在方法体中需要相应的做些处理。因为Object是基类，所以使用Object ...objects这样的参数形式，允许一切继承自Object的对象作为参数。这种方法在实际中应该还是比较少用的。Object[] obj这样的形式，就是一个Object数组构成的参数形式。说明这个方法的参数是固定的，是一个Object数组，至于这个数组中存储的元素，可以是继承自Object的所有类的对象。
这些基础东西建议你[多看](https://www.baidu.com/s?wd=多看&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)几遍"Think in java"

BeanFactory：

作用：生产bean的工厂，生产和管理各个bean的实例；

方法有：

```java
Object getBean(String var1) throws BeansException;

<T> T getBean(String var1, Class<T> var2) throws BeansException;

Object getBean(String var1, Object... var2) throws BeansException;

<T> T getBean(Class<T> var1) throws BeansException;

<T> T getBean(Class<T> var1, Object... var2) throws BeansException;

<T> ObjectProvider<T> getBeanProvider(Class<T> var1);

<T> ObjectProvider<T> getBeanProvider(ResolvableType var1);

boolean containsBean(String var1);

boolean isSingleton(String var1) throws NoSuchBeanDefinitionException;

boolean isPrototype(String var1) throws NoSuchBeanDefinitionException;

boolean isTypeMatch(String var1, ResolvableType var2) throws NoSuchBeanDefinitionException;

boolean isTypeMatch(String var1, Class<?> var2) throws NoSuchBeanDefinitionException;

@Nullable
Class<?> getType(String var1) throws NoSuchBeanDefinitionException;

@Nullable
Class<?> getType(String var1, boolean var2) throws NoSuchBeanDefinitionException;

String[] getAliases(String var1);
```

ListableBeanFactory：获取多个bean

方法有：

```java
boolean containsBeanDefinition(String var1);

int getBeanDefinitionCount();

String[] getBeanDefinitionNames();

String[] getBeanNamesForType(ResolvableType var1);

String[] getBeanNamesForType(ResolvableType var1, boolean var2, boolean var3);

String[] getBeanNamesForType(@Nullable Class<?> var1);

String[] getBeanNamesForType(@Nullable Class<?> var1, boolean var2, boolean var3);

<T> Map<String, T> getBeansOfType(@Nullable Class<T> var1) throws BeansException;

<T> Map<String, T> getBeansOfType(@Nullable Class<T> var1, boolean var2, boolean var3) throws BeansException;

String[] getBeanNamesForAnnotation(Class<? extends Annotation> var1);

Map<String, Object> getBeansWithAnnotation(Class<? extends Annotation> var1) throws BeansException;

@Nullable
<A extends Annotation> A findAnnotationOnBean(String var1, Class<A> var2) throws NoSuchBeanDefinitionException;
```

![2](https://www.javadoop.com/blogimages/spring-context/2.png)

AOP核心：将将那些与业务无关，却为业务模块所共同调用的逻辑或责任（例如事务处理，日志管理，权限控制）封装起来，便于减少系统重复的代码，降低模块耦合度，并有利于未来的可拓展性和可维护性。

aop的动态代理

SpringMVC：模型，视图，控制器，核心思想是通过业务逻辑，数据，显示分离来组织代码

1. 客户端（浏览器）发送请求，直接请求到 `DispatcherServlet`。
2. `DispatcherServlet` 根据请求信息调用 `HandlerMapping`，解析请求对应的 `Handler`。
3. 解析到对应的 `Handler`（也就是我们平常说的 `Controller` 控制器）后，开始由 `HandlerAdapter` 适配器处理。
4. `HandlerAdapter` 会根据 `Handler`来调用真正的处理器开处理请求，并处理相应的业务逻辑。
5. 处理器处理完业务后，会返回一个 `ModelAndView` 对象，`Model` 是返回的数据对象，`View` 是个逻辑上的 `View`。
6. `ViewResolver` 会根据逻辑 `View` 查找实际的 `View`。
7. `DispaterServlet` 把返回的 `Model` 传给 `View`（视图渲染）。
8. 把 `View` 返回给请求者（浏览器）

