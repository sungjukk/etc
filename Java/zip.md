## java zip

### java.util.zip
* 기본적으로 지원해주는 api
* 한글 안됨

### jazzlib
* 한글 파일도 압축 할 때 필요함
* 한글 파일이 깨지는 경우에는 리눅스 환경 설정 의심해봐야함(정확하게는 좀 더 알아봐야함)
* 리눅스
```
locale
```

```java
public static String setZip(List files) throws Exception {
        // 압축할 폴더를 설정한다.
        String targetDir = "C://zip/";
        File zfileDir = new File(targetDir);
        zfileDir.mkdirs();
        // 현재 시간을 설정한다.
        long beginTime = System.currentTimeMillis();
        int cnt;
        byte[] buffer = new byte[BUFFER_SIZE];
        FileInputStream finput = null;
        FileOutputStream foutput;
        net.sf.jazzlib.ZipOutputStream zoutput;

        /*
         ********************************************
         * 압축할 폴더명을 얻는다. : 절대 경로가 넘어올 경우 --> 상대경로로 변경한다...
         *********************************************/
        targetDir.replace('\\', File.separatorChar);
        targetDir.replace('/', File.separatorChar);


        /*
         *****************************************************************
         * 압축할 파일 이름을 정한다.
         * 압축할 파일 명이 존재한다면 다른 이름으로 파일명을 생성한다.
         *****************************************************************/

	  	Map firstMap = (Map) files.get(0);
        
        String zfileNm = "test.zip";
        System.out.println("Zip File Path and Name : " + zfileNm);

        // Zip 파일을 만든다.
        File zfile = new File(targetDir, zfileNm);
        
        // Zip 파일 객체를 출력 스트림에 넣는다.
        foutput = new FileOutputStream(zfile);

        // 집출력 스트림에 집파일을 넣는다.
        zoutput = new net.sf.jazzlib.ZipOutputStream((OutputStream)foutput);

        net.sf.jazzlib.ZipEntry zentry = null;

        try {
    		Map tempMap = null;
    		
      	  	for (Integer i=0; i<files.size(); i++) {
                // 압축할 파일 배열 중 하나를 꺼내서 입력 스트림에 넣는다.
      	  		tempMap = (Map) files.get(i);
      	        File targetFile = new File("C://test.png");
                finput = new FileInputStream(targetFile);

                zentry = new net.sf.jazzlib.ZipEntry("test.png");
                zoutput.putNextEntry(zentry);

                /*
                 ****************************************************************
                 * 압축 레벨을 정하는것인데 9는 가장 높은 압축률을 나타냅니다.
                 * 그 대신 속도는 젤 느립니다. 디폴트는 8입니다.
                 *****************************************************************/
                zoutput.setLevel(COMPRESSION_LEVEL);

                cnt = 0;
                while ((cnt = finput.read(buffer)) != -1) {
                    zoutput.write(buffer, 0, cnt);
                }

                finput.close();
                zoutput.closeEntry();
            }
            zoutput.close();
            foutput.close();
        } catch (Exception e) {
            System.out.println("Compression Error : " + e.toString());
            /*
             **********************************************
             * 압축이 실패했을 경우 압축 파일을 삭제한다.
             ***********************************************/
            System.out.println(zfile.toString() + " : 압축이 실패하여 파일을 삭제합니다...");
            if (!zfile.delete()) {
                System.out.println(zfile.toString() + " : 파일 삭제가 실패하여 다시 삭제합니다...");
//                while(!zfile.delete()) {
//                    System.out.println(zfile.toString() + " : 삭제가 실패하여 다시 삭제합니다....");
//                }
            }
            e.printStackTrace();
            throw new Exception(e);
        } finally {
            if (finput != null) {
                finput.close();
            }
            if (zoutput != null) {
                zoutput.close();
            }
            if (foutput != null) {
                foutput.close();
            }
        }

        long msec = System.currentTimeMillis() - beginTime;

        System.out.println("Check :: >> " + msec/1000 + "." + (msec % 1000) + " sec. elapsed...");
        
        return zfileNm;
    }
```
### 
