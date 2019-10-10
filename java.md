title:关于一些java的内容
date: 2019-9-22
Category: java
Tags: java
Authors: openui
Summary:记录一些java知识

### java

* java 8

  * stream lambda

    * filter

      ```
      List<Person> data = new ArrayList<>();
      List<Person> result = data.stream().filter(
      	person -> {
      		if(person.age == 20){
      			return true;
      		}else{
      			return false;
      		}
      	}
      ).collect(toList());
      ```

      

    * map 一对一

      ```
      List<Person> data = new ArrayList<>();
      List<Person> result = data.stream().map(
      	person -> {
      		return person.getName();
      	}
      ).collect(toList());
      
      // 方法1
      person -> person.getName()
      // 方法2
      person -> {
      		return person.getName();
      	}
      // 方法3
      Person::getName
      
      ```

      

    * Flatmap 一对多

      ```
      .flatmap(person->Arrays.stream(person.getName.split(" "))).collect(toList());
      
      // map 方式
      .map(person->person.getName().splite(" "))
      .flatmap(Arrays::stream).collect(toList());
      // 另一种方式
      .map(person->person.getName().splite(" "))
      .flatmap(str -> Arrays.asList(str).stream()).collect(toList());
      ```

      

    * reduce 类似递归

      ```
      
      ```

      

    * Collect  在流中生成列表，map常用数据结构

      * toList() toSet() toMap()

      * 自定义方法

        ```
        
        ```

    * Optional:替换null