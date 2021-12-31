---
description: PHP를 이용한 SMS 웹 서비스 이용방법을 안내합니다.
---

# PHP를 이용한 예제

### PHP를 이용한 SMS 웹 서비스 이용방법 <a href="#asp-net-vb-sms" id="asp-net-vb-sms"></a>

{% file src="../.gitbook/assets/sendsms_sample_asp.zip" %}
PHP를 이용한 예제소스 다운로드
{% endfile %}

#### 1. SMS발송 정보를 입력 받을 폼을 작성합니다. (예제소스에 포함) <a href="#1-visual-studio-net" id="1-visual-studio-net"></a>

> 계정 인증키는 \[계정관리 > 호스팅 계정정보]에서 확인 하실 수 있습니다.​

![](../.gitbook/assets/php\_1.png)

#### 2. 편집기를 이용해 아래의 소스코드를 작성하여 SendSms.asp로 저장합니다. <a href="#2" id="2"></a>

> PHP로 DpSms 웹 서비스를 이용하여 메시지를 보내기 위해서는 [**Snoopy.php**](https://sourceforge.net/projects/snoopy/) 파일을 참조해야만 합니다.

```php
<?php
include “Snoopy.class.php”;
$snoopy = new Snoopy;

/*======================================================================*\
// euc-kr 인코딩을 사용할 경우
// POST 방식
\*======================================================================*/
$cmd = “SendSms”;
$tran_phone = urlencode(iconv(‘EUC-KR’, ‘UTF-8’, $_POST[“tran_phone”]));//받는사람 핸드폰 번호
$tran_callback=urlencode(iconv(‘EUC-KR’,’UTF-8′,$_POST[“tran_callback”]));//보내는사람 핸드폰 번호
$tran_date=urlencode(iconv(‘EUC-KR’,’UTF-8′,$_POST[“tran_date”]));//예약전송 일시(생략시 즉시전송)
$tran_msg = urlencode(iconv(‘EUC-KR’,’UTF-8′,$_POST[“tran_msg”]));//전송 메시지
$guest_no = urlencode(iconv(‘EUC-KR’,’UTF-8′,$_POST[“guest_no”]));//계정번호
$guest_key = urlencode(iconv(‘EUC-KR’,’UTF-8′,$_POST[“guest_key”]));//계정 인증키
$type = urlencode(iconv(‘EUC-KR’,’UTF-8′,$_POST[“com_type”]));//발송구분
$subject = urlencode(iconv(‘EUC-KR’,’UTF-8′,$_POST[“subject”]));//LMS / MMS 발송시 제목
/*======================================================================*\
// MMS일 경우 첨부파일 처리
// 서버&로컬 에 저장된 이미지 파일 읽어올때.
// 웹경로 ,로컬경로 모두 가능 합니다.
\*======================================================================*/
//1. 웹경로
//$img_source = ‘http://websvc.nesolution.com/sms/MMSAttachFiles/M050085/20180510145947.jpg’;
//2. 로컬경로
$img_source = ‘./img/test.jpg’;

$img = file_get_contents($img_source);
$Base64files = base64_encode($img);

//”,” 콤마로 구분 최대 3개.가능합니다.
$files = $Base64files .”,”.$Base64files .”,”.$Base64files ;

/*======================================================================*\
// MMS일 경우 첨부파일 처리
// 프론트에서 이미지 파일을 base64로 생성후 post로 받아 올때.
// POST 방식
\*======================================================================*/
/*
$files = $_POST[“Base64files”];//MMS 발송시 첨부파일
*/

/*======================================================================*\
// utf-8 인코딩을 사용할 경우
// POST 방식
\*======================================================================*/
/*
$cmd = “SendSms”;
$tran_phone = urlencode($_POST[“tran_phone”]); //받는사람 핸드폰 번호
$tran_callback = urlencode($_POST[“tran_callback”]); //보내는사람 핸드폰 번호
$tran_date = urlencode($_POST[“tran_date”]); //예약전송 일시(생략시 즉시전송)
$tran_msg = urlencode($_POST[“tran_msg”]); //전송 메시지
$guest_no = urlencode($_POST[“guest_no”]); //계정번호
$guest_key = urlencode($_POST[“guest_key”]); //계정 인증키
$type = urlencode($_POST[“com_type”]); //발송구분
$subject = urlencode($_POST[“subject”]); //LMS / MMS 발송시 제목
$files = $_POST[“Base64files”];//MMS 발송시 첨부파일
*/

if($type != “MMS”)
{
/*======================================================================*\
// GET 으로 호출
이미지 첨부시 에러 발생함니다. post 로 전송하세요.
\*======================================================================*/
$method = “GET”;
$url = “http://websvc.nesolution.com/SMS/SMS.aspx?cmd=$cmd&method=$method&”;
$url = $url . “guest_no=$guest_no&guest_key=$guest_key&tran_phone=$tran_phone&”;
$url = $url . “tran_callback=$tran_callback&tran_date=$tran_date&tran_msg=$tran_msg&”;
$url = $url . “type=$type&subject=$subject”; // LMS 또는 MMS 일경우 제목 필수

$snoopy->fetchtext($url);
// 출력 페이지가 euc-kr 일때
$send_result = $snoopy->results;
// 출력 페이지가 utf-8 일때
//$send_result = iconv(‘EUC-KR’, ‘UTF-8’, $snoopy->results);
}
else
{
/*======================================================================*\
// $snoopy 사용 POST 발송(MMS 파일첨부시)
\*======================================================================*/

$formvars[“cmd”] =$cmd;
$formvars[“guest_no”] = $guest_no;
$formvars[“guest_key”] = $guest_key;
$formvars[“tran_phone”] = $tran_phone;
$formvars[“tran_callback”] = $tran_callback;
$formvars[“tran_date”] = $tran_date;
$formvars[“tran_msg”] = $tran_msg;
$formvars[“type”] = $type;
$formvars[“subject”] = $subject;
$formvars[“files”] = $files;

$snoopy->httpmethod = “POST”;
$snoopy->submit(“http://websvc.nesolution.com/SMS/SMS.aspx”,$formvars );

//출력 페이지가 euc-kr 일때
$send_result = $snoopy->results;
// 출력 페이지가 utf-8 일때
//$send_result = iconv(‘EUC-KR’, ‘UTF-8’, $snoopy->results);
?>

<HTML>
<HEAD>
<TITLE>SMS 전송 결과</TITLE>
<meta http-equiv=”Content-Type” content=”text/html; charset=ks_c_5601-1987″>
<style type=”text/css”>
<!–
.unnamed1 { font-family:”굴림”; font-size:9pt; line-height:12pt}
//–>
</style>
</HEAD>
<BODY>
<div align=”center”>
<h2>SMS 예제소스(php)</h2>
<br>
<span class=”unnamed1″>전송결과 : <b><? echo($send_result); ?></b></span>
</div>
</BODY>
</HTML>
```

> #### **파라미터** ✔ <a href="#undefined" id="undefined"></a>

| **파라미터**       | **설명**                                                                                                                                                                         |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| cmd            | 명                                                                                                                                                                              |
| tran\_phone    | <p>수신자 전화번호(생략불가), 여러번호일 경우에는 ;으로 구분.</p><p>전화번호 구분자 대쉬(-)는 있거나 없거나 상관없음</p>                                                                                                   |
| tran\_callback | 송신자 전화번호(생략불가)                                                                                                                                                                 |
| tran\_date     | <p>예약 전송시에만 사용, 포맷은 시분까지 포함된 날짜 포맷.</p><p>생략시에는 즉시 전송(예.2003-01-01 13:01)</p>                                                                                                  |
| tran\_msg      | <p>전송 메시지(생략불가).</p><p>SMS : 최대 80byte (용량이 넘으면 짤려서 전송)</p><p>LMS/MMS : 최대 2,000byte</p>                                                                                       |
| guest\_no      | 계정번호(예.000001)                                                                                                                                                                 |
| guest\_key     | <p>관리자 계정과 암호를 이용해 생성한 계정 인증 키</p><p>(회원전용 사이트에서 확인 가능)</p>                                                                                                                    |
| type           | <p>메시지 전송 타입. "SMS" / "LMS" / "MMS" / "AUTO" 중에서 선택.</p><p>LMS/MMS 사용 시 서비스 신청이 되어 있어야 함</p><p>빈 값을 넘기면 "SMS"형식으로 발송</p><p>"AUTO"는 메시지의 길이를 체크하여 80byte를 초과 시 자동으로 LMS로 발송</p> |
| subject        | <p>LMS/MMS 메시지의 메시지 제목.</p><p>LMS/MMS 방식을 사용하는 경우 필수.</p>                                                                                                                      |
| files          | <p>MMS 첨부 이미지 파일명.</p><p>첨부 파일이 2개 이상인 경우 컴마(,)로 구분</p><p>MMS의 경우 필수</p><p>최대 3개 까지 지정 가능, 최대 50kb gif,png,jpg 파일형식</p>                                                        |

> #### **반환 값** ✔ <a href="#undefined-1" id="undefined-1"></a>

{% hint style="success" %}
#### 성공 시    "OK"
{% endhint %}

{% hint style="danger" %}
**실패 시 "Exception: 에러메시지"**
{% endhint %}

#### 3. 실행결과 화면입니다.

> 정상적으로 메시지가 발송되었을 경우

![](../.gitbook/assets/php\_2.png)

> 오류로 인하여 메시지를 발송하지 못했을 경우

![](../.gitbook/assets/php\_3.png)
