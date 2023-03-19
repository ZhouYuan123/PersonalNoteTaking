### 动态代理

1. 静态代理
2. 动态代理 (JDK 代理)
3. Cglib代理

```java
// 被代理类
public class Renter implements Person{
	@Override
	public void rentHouse() {
		System.out.println("租客租房成功！");
	}
}

public class RenterInvocationHandler<T> implements InvocationHandler{
	//被代理类的对象
	private T target;
	public RenterInvocationHandler(T target){
		this.target = target;
	}
	/**
     * proxy: 动态代理对象
     * method：正在执行的方法
     * args：调用目标方法时传入的实参
     */
	@Override
	public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
		//代理过程中插入其他操作
		System.out.println("租客和中介交流");
		Object result = method.invoke(target, args);
		return result;
	}
}

public class ProxyTest {
	public static void main(String[] args) {
		//创建被代理的实例对象
		Person renter = new Renter();
		//创建InvocationHandler对象
		InvocationHandler renterHandler = new RenterInvocationHandler<Person>(renter);
		//创建代理对象,代理对象的每个执行方法都会替换执行Invocation中的invoke方法
		Person renterProxy = (Person) Proxy.newProxyInstance(
            Person.class.getClassLoader(), new Class<?>[]{Person.class}, renterHandler);
		renterProxy.rentHouse();
		
		//也可以使用下面的方式创建代理类对象，Proxy.newProxyInstance其实就是对下面代码的封装
		/*try {
			//使用Proxy类的getProxyClass静态方法生成一个动态代理类renterProxy 
			Class<?> renterProxyClass = Proxy.getProxyClass(Person.class.getClassLoader(), new Class<?>[]{Person.class});
			//获取代理类renterProxy的构造器，参数为InvocationHandler
			Constructor<?> constructor = renterProxyClass.getConstructor(InvocationHandler.class);
			//使用构造器创建一个代理类实例对象
			Person renterProxy = (Person)constructor.newInstance(renterHandler);
			renterProxy.rentHouse();
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}*/
	}

}

```

