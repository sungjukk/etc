## oracle 스케줄러
### 생성
```
BEGIN
    DBMS_SCHEDULER.CREATE_JOB (
            job_name => '"SMARTAPP"."TSCHEDULER4"', -- 작업 이름
            job_type => 'STORED_PROCEDURE', -- 작업 종류
            job_action => 'SMARTAPP.PROCEDURE1', -- 작업 내용
            number_of_arguments => 0,
            start_date => NULL, -- 시작 날짜
            repeat_interval => 'FREQ=DAILY;BYHOUR=14;BYMINUTE=40;BYSECOND=0', -- 인터벌 설정
            end_date => NULL,
            enabled => TRUE, -- 사용 여부
            auto_drop => FALSE,
            comments => '');
END;
```
### dbms 작업 생성
```
 DECLARE jobno numeric; 
 BEGIN dbms_job.submit(jobno, what          => 'A.TESTPROC;'

     ,next_date   => to_date('22-02-2018 11:00:00','dd/mm/yyyy hh24:mi:ss')

     ,interval      => 'TRUNC(SYSDATE+1)+3/24'

     ,no_parse   => TRUE); END;
```
### interval 종류
* SYSDATE+7 : 7일에 한번 씩 job 수행

* SYSDATE+1/24 : 1시간에 한번 씩 job 수행

* SYSDATE+30/ : 30초에 한번 씩 job 수행(24: 시간 당, 1440(24x60):분 당, 86400(24x60x60):초 당 )

* TRUNC(SYSDATE, 'MI')+8/24 : 최초 job 수행시간이 12:29분 일 경우 매시 12:29분에 job 수행

* TRUNC(SYSDATE+1) : 매일 밤 12시에 job 수행

* TRUNC(SYSDATE+1)+3/24 : 매일 오전 3시 job 수행

* NEXT_DAY(TRUNC(SYSDATE),'MONDAY')+15/25 : 매주 월요일 오후 3시 정각에 job 수행

* TRUNC(LAST_DAY(SYSDATE))+1 : 매월 1일 밤 12시에 job 수행

* TRUNC(LAST_DAY(SYSDATE))+1+8/24+30/1440 : 매월 1일 오전 8시 30분
### dbms 작업 조회
```
SELECT * FROM USER_JOBS;
```
### dbms 작업 삭제
```
EXECUTE DBMS_JOB.REMOVE(183);
COMMIT;
```
