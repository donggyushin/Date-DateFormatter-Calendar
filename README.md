# Date-DateFormatter-Calendar
Learn basic concepts of Date, DateFormatter, Calendar in Swift

<img src="https://miro.medium.com/max/1400/0*E3ZZxQUJix7E234-" width=300 />
<br />

## Date
> A specific point in time, independent of any calendar or time zone.

어떤 역법이나 시간대와 독립적으로 특정 시점에 대한 정보를 가지고 있다. 표준 시간대에 맞추어 시간 데이터를 저장하는 객체이다. 

## DateFormatter
실제로 작업을 할때에 우리는 `2022-02-05 15:58:00 + 0000` 이런식으로 보고싶은 경우는 그닥 없다. 그래서 애플은 우리가 원하는대로 형식을 맞추어 문구를 출력할 수 있는 기능을 제공하고 있는데, 그걸 위한 클래스가 바로 <b>DateFormatter</b> 이다. 

만약 한국에서 5월 11일 21시 34분 59초에 하나의 Date 객체를 만들고 해당 Date 객체를 `print` 해보면 5월 11일 12시 34분 59초로 나온다. 이를 한국 시간대를 기준으로 출력하고 싶다면, <br /><br />

```
let now = Date()
let dateFormatter = DateFormatter()
dateFormatter.locale = Locale(identifier: "ko_KR")
dateFormatter.dateFormat = "yyyy년 MM월 dd일 HH시 mm분 s초"

print(dateFormatter.string(from: now))

==> 2022년 05월 11일 21시 30분 12초
```

이런 식으로 `dateFormat` 를 설정해주니 우리가 원하는 시간이 나온다. <br><br>

`dateFormat` 을 보면 알겠지만 문자열 속에 우리가 자의적으로 넣어둔 `yyyy`, `MM`, `dd` 같은 문구를 사용하면 그에 맞추어 숫자를 넣어준다. 만약에 `yy` 로 작성했다면 22 가 나왔을 것이다. <br><br>

대소문자에 따라 바뀌는 것도 있는데 만약 `HH` 를 작성했다면 시간을 24시간 기준으로 표현하고, `hh` 로 작성했다면 12시간 기준으로 표현한다. 만약 `M` 만 작성한다면 05월이 아니라 5월이라고 나올 것이다. 물론 12월이라면 12월 그대로 나온다. <br><br>

DateFormatter는 Date 객체를 String 으로 바꾸어줄 뿐만 아니라 그 반대도 가능하다. <br><br>

만약 서버에서 `2022년 1월 21일 21시 00분 00초` 이런 식으로 시간을 보내준다고 가정해보자. 해당 시간대는 한국 시간대 기준이고, 우리는 저 string이 가르키고 있는 표준 시간대의 date 객체를 만들어서 저장하려고 한다면

```
let dateString = "2022년 01월 21일 21시 00분 00초"
let dateFormatter = DateFormatter()
dateFormatter.locale = Locale(identifier: "ko_KR")
dateFormatter.dateFormat = "yyyy년 MM월 dd일 HH시 mm분 s초"

let date = dateFormatter.date(from: dateInfo) ?? Date()
print(date)
==> 2022-01-21 12:00:00 +0000
```

## Calendar

Calendar는 개인적으로 조금 생소한 개념이었다. 기본적으로 Calendar는 현재 시점을 우리가 원하는 역법에 맞추어 달력을 구성해주는 역할을 한다. 
<br><br>

```
let calendar = Calendar.current

print(calendar)
=> gregorian (current)
print(calendar.timeZone)
=> Asia/Seoul (fixed (equal to current))
```

