## 动态代理

```java
public class JdkProxySubject implements InvocationHandler{
    //引入要代理的真实对象
    private RealSubject realSubject;
    
    //用构造器注入目标方法，给我们要代理的真实对象赋初值
    public JdkProxySubject(RealSubject realSubject){
       this.realSubJect=realSubject;
    }
    
    //实现接口的方法
    @Override
    public Object invoke(Object proxy, Method method, Object[] args)throws Throwable{
        System.out.println("before");
        Object result = null;
        try{
        //当代理对象调用真实对象的方法时，其会自动的跳转到代理对象关联的handler对象的invoke方法来进行调用
       		result=method.invoke(realSubject, args);
        }catch(Exception e){
        	System.out.println("ex:"+e.getMessage());
        	throw e; 
        }finally{
            System.out.println("after");
        }
        return result;
    }
}
public class Client{
  public static void main(String[] args){
    // 使用Proxy构造对象参数
    // java泛型需要转换一下
   	// 第一个参数getClassLoader()，我们这里使用Client这个类的ClassLoader对象来加载我们的代理对象
    // 第二个参数表示我要代理的是该真实对象，这样我就能调用这组接口中的方法了
    // 第三个参数handler，我们这里将这个代理对象关联到了上方的 InvocationHandler这个对象上
    Subject subject = 
       (Subject)java.lang.reflect.Proxy.newProxyInstance(Client.class.getClassLoader(),
                new Class[]{Subject.class},new JdkProxySubject(new RralSubject()));
    // 调用方法
     subject.test;
  }
}
```

