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
### dbms 작업 조회
```
SELECT * FROM USER_JOBS;
```
### dbms 작업 삭제
```
EXECUTE DBMS_JOB.REMOVE(183);
COMMIT;
```
