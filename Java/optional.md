# Optional 总结  

1. **empty()**  
   - 返回一个 `Optional` 容器对象，而不是 `null`。  
   - **建议常用** ⭐⭐⭐⭐  

2. **of(T value)**  
   - 创建一个 `Optional` 对象，如果 `value` 是 `null`，则抛出 `NPE`。  
   - **不建议用** ⭐⭐  

3. **ofNullable(T value)**  
   - 同上，创建一个 `Optional` 对象，但 `value` 为空时返回 `Optional.empty()`。  
   - **推荐使用** ⭐⭐⭐⭐⭐  

4. **get()**  
   - 返回 `Optional` 中包装的值，在判空之前，千万不要直接使用！尽量别用！  
   - **评级** ⭐  

5. **orElse(T other)**  
   - 返回 `Optional` 中包装的值，但当取不到值时，返回你指定的 default。  
   - **无论如何都会执行括号中的内容**
   - **评级** ⭐⭐  

6. **orElseGet(Supplier<? extends T> other)**  
   - 返回 `Optional` 中包装的值，取不到值时，返回你指定的 default。  
   - **只有value为空才执行**
   - **评级** ⭐⭐⭐⭐⭐  

7. **orElseThrow(Supplier<? extends X> exceptionSupplier)**  
   - 返回 `Optional` 中包装的值，取不到值时抛出指定的异常。  
   - 阻塞性业务场景推荐使用  
   - **评级** ⭐⭐⭐⭐  

8. **isPresent()**  
   - 判断 `Optional` 中是否有值，返回 `boolean`，某些情况下很有用，但尽量不要用在 `if` 判断体中。  
   - **评级** ⭐⭐⭐  

9. **ifPresent(Consumer<? super T> consumer)**  
   - 判断 `Optional` 中是否有值，有值则执行 `consumer`，否则什么都不干。  
   - 日常情况下请使用