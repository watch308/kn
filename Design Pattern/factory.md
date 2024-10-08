#### 简单工厂
* 抽象产品
* 具体产品
* 工厂类
```
public interface People {
    void set();
}

public class PeopleB implements People {
    @Override
    public void set() {
        System.out.println("b");
    }
}

public class PeopleA implements People {
    @Override
    public void set() {
        System.out.println("a");
    }
}

public class SimpleFactory {
    private final People peopleA = new PeopleA();
    public People get(String s){
        if("a".equals(s))return peopleA;
        else return new PeopleB();
    }
}
```


#### 工厂模式
* 抽象工厂
* 具体工厂
* 抽象产品
* 具体产品

