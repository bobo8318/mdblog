* gradle 移除依赖冲突

  * Gradle的依赖分析功能

  > ./gradlew dependencyInsight --dependency slf4j-api

  * 解决冲突办法

  ```
  // project用括号包裹住
  compile (project(':uisdk:Library:facebook')) {
      exclude group: 'com.android.support', module: 'appcompat-v7'
  }
  
  遇到了exclude无效的问题，使用全局移除就正常了:
  // 排除掉V4包中引入的android.arch.lifecycle:runtime导致构建失败
  configurations.all {
      exclude group: 'android.arch.lifecycle', module: 'runtime'
  }
  
  compile ('org.avaje.ebeanorm:avaje-ebeanorm:7.9.1') {
    exclude group: 'org.slf4j', module: 'slf4j-api'
    exclude group: 'ch.qos.logback', module: 'logback-classic'
  }
  ```

  