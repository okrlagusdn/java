

# java

자바 공부



### DAY1

#### Calendar 클래스

Calendar 클래스는 추상 클래스이므로 객체를 직접 생성할 수는 없지만, getInstance() 메소드를 이용하여 시스템의 날짜와 시간 정보를 표현할 수 있다.

##### Calendar 클래스의 주요 상수

|           상수           |        사용방법        |                설명                |
| :----------------------: | :--------------------: | :--------------------------------: |
|     static int YEAR      |     Calendar.YEAR      |       현재 년도를 가져온다.        |
|     static int MONTH     |     Calendar.MONTH     |    현재 월을 가져온다.(1월은 0)    |
|     static int DATE      |     Calendar.DATE      |     현재 월의 날짜를 가져온다.     |
| static int WEEK_OF_YEAR  | Calendar.WEEK_OF_YEAR  |        현재 년도의 몇 째 주        |
| static int WEEK_OF_MONTH | Calendar.WEEK_OF_MONTH |         현재 월의 몇 째주          |
|  static int DAY_OF_YEAR  |  Calendar.DAY_OF_YEAR  |          현재 년도의 날짜          |
| static int DAY_OF_MONTH  | Calendar.DAY_OF_MONTH  |    현재 월의 날짜(DATE와 동일)     |
|  static int DAY_OF_WEEK  |  Calendar.DAY_OF_WEEK  | 현재 요일 (일요일은 1, 토요일은 7) |
|     static int HOUR      |     Calendar.HOUR      |        현재 시간 (12시간제)        |
|  static int HOUR_OF_DAY  |  Calendar.HOUR_OF_DAY  |        현재 시간 (24시간제)        |
|    static int MINUTE     |    Calendar.MINUTE     |              현재 분               |
|    static int SECOND     |    Calendar.SECOND     |              현재 초               |

	import java.util.Calendar;
	
	public class CalendarTest {
	    public static void main(String[] args) {
	        Calendar cal = Calendar.getInstance();
	        int year = cal.get(Calendar.YEAR);
	        int mon = cal.get(Calendar.MONTH);
	        int day = cal.get(Calendar.DAY_OF_MONTH);
	        int hour = cal.get(Calendar.HOUR_OF_DAY);
	        int min = cal.get(Calendar.MINUTE);
	        int sec = cal.get(Calendar.SECOND);
	        System.out.println("현재 시간 : ");
	        System.out.println(year+"년 "+(mon+1)+"월 "+day+"일");
	        System.out.println(hour+"시 "+min+"분 "+sec+"초");
	    }
	}
##### 실행 결과

```
현재 시간 : 
2020년 10월 29일
9시 57분 46초
```

##### 

##### Calendar 클래스 메소드

| Calendar 클래스의 메소드                                     | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| boolean after(Object when)                                   | when과 비교하여 현재 날짜 이후이면 true, 아니면 false를 반환한다. |
| boolean before(Object when)                                  | when과 비교하여 현재 날짜 이전이면 true, 아니면 false를 반환한다. |
| boolean equals(Object obj)                                   | 같은 날짜값인지 비교하여 true, false를 반환한다.             |
| int get(int field)                                           | 현재 객체의 주어진 값의 필드에 해당하는 상수 값을 반환한다. 이 상수 값은 Calendar 클래스의 상수 중에 가진다. |
| static Calendar getInstance()                                | 현재 날짜와 시간 정보를 가진 Calendar 객체를 생성한다.       |
| Date getTime()                                               | 현재의 객체를 Date 객체로 변환한다.                          |
| long getTimeInMills()                                        | 객체의 시간을 1/1000초 단위로 변경하여 반환한다.             |
| void set(int field, int value)                               | 현재 객체의 특정 필드를 다른 값으로 설정한다.                |
| void set(int year, int month, int date)                      | 현재 객체의 년, 월, 일 값을 다른 값으로 설정한다.            |
| void set(int year, int month, int date, int hour, int minute, int second) | 현재 객체의 년, 월, 일, 시, 분, 초 값을 다른 값으로 설정한다. |
| void setTime(Date date)                                      | date 객체의 날짜와 시간 정보를 현재 객체로 생성한다.         |
| void setTimeInMills(long mills)                              | 현재 객체를 1/1000초 단위의 주어진 매개변수 시간으로 설정한다. |
| int getActualMinimum(int field)                              | 현재 객체의 특정 필드의 최소 값을 반환한다.                  |
| int getActualMaximum(int field)                              | 현재 객체의 특정 필드의 최대 값을 반환한다.                  |



##### SimpleDateFormat

날짜를 원하는 포맷으로 파싱시켜 주는 역할

| Letter | Date or Time Component | Presentation | Examples      |
| ------ | ---------------------- | ------------ | ------------- |
| y      | 년                     | Year         | 1996; 96      |
| M      | 월                     | Month        | July; Jul; 07 |
| d      | 일                     | Number       | 10            |
| H      | 시간(24시간)           | Number       | 0             |
| h      | 시간(am/pm)            | Number       | 12            |
| m      | 분                     | Number       | 30            |
| s      | 초                     | Number       | 55            |



	import java.text.SimpleDateFormat;
	import java.util.Calendar;
	
	public class CalendarTest2 {
	    public static void main(String[] args) {
	        SimpleDateFormat f = new SimpleDateFormat("yyyy/MM/dd");
	        Calendar cal1 = Calendar.getInstance();
	        Calendar cal2 = Calendar.getInstance();		
	        cal1.set(1, 2021);
	        System.out.println(f.format(cal1.getTime()));
	        if(cal1.after(cal2)) {
	            System.out.println("cal1이 뒤");//cal1은 2021/10/29, cal2는 2020/10/29
	        }
	        cal1.set(1, 2020);
	        if(cal1.equals(cal2)) {
	            System.out.println("같은 날!");
	        }
	        System.out.println(cal1.get(1));//해당 필드 반환
	        System.out.println(cal1.getTime());//Date객체로 변환
	        System.out.println(cal1.getTimeInMillis());
	        cal1.set(1993, 11, 7, 11, 65, 59);//분이 60이상이면 시간을 증가시켜준다.
	        System.out.println(cal1.getTime());
	        System.out.println(cal1.getActualMaximum(1));
	        System.out.println(cal1.getActualMinimum(1));
	    }
	}
##### 실행 결과

```
2021/10/29
cal1이 뒤
같은 날!
2020
Thu Oct 29 11:12:11 KST 2020
1603937531127
Tue Dec 07 12:05:59 KST 1993
292278993
1
```



##### 시간차이 계산

```
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class CalendarTest3 {

	public static void main(String[] args) throws ParseException {
		SimpleDateFormat f = new SimpleDateFormat("yyyy-MM-dd HH:mm");
		String endDate = "2020-10-29 14:06";
		Date startDate = new Date();
		String sd = "2020-10-29 13:59";
		startDate = f.parse(sd);
		Date ed = f.parse(endDate);
		System.out.println((ed.getTime()-startDate.getTime())/60000+"분 차이");
		
		SimpleDateFormat f2 = new SimpleDateFormat("yyyy-MM-dd");
		String start = "2020-09-26";
		String end = "2020-10-29";
		Date s = f2.parse(start);
		Date e = f2.parse(end);
		System.out.println((e.getTime()-s.getTime())/60000/60+"시간 차이");
		System.out.println((e.getTime()-s.getTime())/60000/60/24+"일 차이");
	}
}
```

##### 실행 결과

```
7분 차이
792시간 차이
33일 차이
```





------

### DAY2

#### 문자열

| 문자열 메소드 종류                                           | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| char charAt(int index)                                       | 지정된 인덱스의 한 문자를 반환                               |
| int compareTo(String antherString)                           | 두 문자열의 사전적 우선 순위 비교                            |
| int compareToIgnoreCase(String str)                          | 대소문자를 구분하지 않는 사전적 비교                         |
| boolean contains(CharSequence s)                             | 문자열을 포함하고 있는지 확인                                |
| boolean endsWith(String suffix)                              | 문자열의 끝이 인자로 주어진 문자열인지 확인                  |
| boolean equals(Object anObject)                              | 같은 내용의 문자열인지 비교                                  |
| boolean equalsIgnoreCase(String anotherString)               | 대소문자를 구분하지 않고 비교                                |
| byte[] getBytes()                                            | 플랫폼 기본 캐릭터셋으로 인코딩된 바이트 배열을 링크한다.    |
| byte[] getBytes(String charsetName)                          | 인자로 주어진 캐릭터 셋으로 인코딩된 바이트 배열을 반환      |
| int indexOf(char ch)                                         | 인자로 주어진 문자가 있는 위치를 반환, 없으면 음수를 반환    |
| boolean isEmpty()                                            | 빈문자열인지 확인                                            |
| int lastIndexOf(char ch)                                     | 인자로 주어진 문자가 마지막으로 나타난 위치를 반환, 없으면 음수를 반환 |
| int length()                                                 | 문자열의 길이를 반환                                         |
| boolean matches(String regex)                                | 인자로 주어진 정규식에 매치되는지 확인                       |
| String replace(char oldChar, char newChar)                   | 문자열에서 첫번째 인자의 문자를 두번째 인자의 문자로 바꿈    |
| String replace(CharSequence target, CharSequence replacement) | 문자열을 바꿈                                                |
| String replaceAll(String regex, String replacement)          | 정규식을 사용하여 매치되는 문자열을 바꿈.                    |
| String[] split(String regex)                                 | 정규식에 매치되는 부분을 구분자로 문자열을 분할              |
| String[] split(String regex, int limit)                      | 문자열 분할시 두번째 인자로 마지막 빈 요소 처리 및 분할할 개수를 지정 |
| boolean startsWith(String prefix)                            | 인자로 주어진 문자열로 시작하는지 확인                       |
| String substring(int beginIndex)                             | 문자열에서 인자로 주어진 인덱스 이후의 문자열을 추출         |
| String substring(int beginIndex, int endIndex)               | 인자로 주어진 인덱스 사이의 문자열을 반환                    |
| String toLowerCase()                                         | 소문자로 변경                                                |
| String toUpperCase()                                         | 대문자로 변경                                                |
| String trim()                                                | 문자열 앞, 뒤의 whitespace를 제거                            |

