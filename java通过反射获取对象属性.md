java通过反射获取对象属性

```java
//格式化对象中BigDecimal类型的数据，四舍五入去除小数位
    public static Object formatBigDecimalObject(Object model) throws NoSuchMethodException, InvocationTargetException, IllegalAccessException, IntrospectionException {
        //获取实体类的所有属性
        Field[] declaredFields = model.getClass().getDeclaredFields();
        for (int i = 0; i < declaredFields.length; i++) {
            //获取属性的名字
            String name = declaredFields[i].getName().trim();
            String n = name.substring(0,1).toUpperCase()+name.substring(1);

            //获取属性的类型
            String type = declaredFields[i].getGenericType().toString();
            
            if (type.equals("class java.math.BigDecimal")){
                Method m = model.getClass().getMethod("get" + n);//getter方法
                BigDecimal value = (BigDecimal) m.invoke(model);
                if (value != null){
                    PropertyDescriptor pd = new PropertyDescriptor(name, model.getClass());
                    Method setMethod = pd.getWriteMethod();
                    setMethod.invoke(model,new Object[] {value.setScale(0,RoundingMode.HALF_UP)});//设置属性值，setter方法
                }
            }
        }
        return model;
    }
```

