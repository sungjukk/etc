## Spring에서 스케줄러 설정 방법
---
### Annotation
1. XML 설정
```xml
<beans
    xmlns:task="http://www.springframework.org/schema/task"
    xsi:schemaLocation="
        http://www.springframework.org/schema/task
        http://www.springframework.org/schema/task/spring-task-3.0.xsd">
<task:annotation-driven />    
</beans>
```
`spring-context.xml`에 추가

2. Annotation 사용
```java

@Service 
public class testSchedule {

    @Scheduled(cron="0 0 12 * * *")
    public void test(){
        System.out.println("스케줄");
    }
}
```
### XML 설정
1. XML 설정
```xml
<task:scheduler id="scheduler" pool-size="2"/>
<task:scheduled-tasks scheduler="scheduler" >
    <task:scheduled ref="TaskTestService" method= "doJob" cron="0/4 * * * * ?" />
</task:scheduled-tasks>  
```
2. Java
```java
@Service
public class TaskTestService {
    public void doJob(){
        System.out.println("스케줄링 중~~~!");
    }
} 
```

### value
1. cron : 초 분 시간 일 월 년 순으로 적으면 해당 시간에 맞춰 실행된다.
Seconds | 0 ~ 59
--------- | ---------
