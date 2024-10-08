##### execution
```
execution([访问控制权限修饰符] 返回值类型 [全限定类名]方法名(形式参数列表) [异常])
访问控制权限修饰符：
● 没写，就是4个权限都包括。
● 写public就表示只包括公开的方法。
返回值类型：
● * 表示返回值类型任意.
全限定类名：
● 两个点“..”代表当前包以及子包下的所有类。
● 省略时表示所有的类。
方法名：
● *表示所有方法。
● set*表示所有的set方法。
形式参数列表：
● () 表示没有参数的方法
● (..) 参数类型和个数随意的方法
● (*) 只有一个参数的方法
● (*, String) 第一个参数类型随意，第二个参数是String的。
异常：
● 省略时表示任意异常类型。
```
##### 通知类型
* 前置通知：@Before 目标方法执行之前的通知
* 后置通知：@AfterReturning 目标方法执行之后的通知
* 环绕通知：@Around 目标方法之前添加通知，同时目标方法执行之后添加通知。
* 异常通知：@AfterThrowing 发生异常之后执行的通知
* 最终通知：@After 放在finally语句块中的通知
eg.
```
@Component
@Aspect
public class LogAspect {
@Before("execution(* dpx..*(..))")
    public void aspect(){
        System.out.println("aspect");
    }
}
<context:component-scan base-package="dpx"/>
<aop:aspectj-autoproxy/>
```

###### 先后顺序
@Order注解的value指定一个整数型的数字，数字越小，优先级越高。
###### 通用切点
@Pointcut注解来定义独立的切点表达式。

```
@Pointcut("execution(* dpx..*(..))")
public void fun(){}
@Component
@Aspect
public class LogAspect {
@Before("fun()")
    public void aspect(){
        System.out.println("aspect");
    }
}
```
