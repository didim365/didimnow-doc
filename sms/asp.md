---
description: ASP를 이용한 SMS 웹 서비스 이용방법을 안내합니다.
---

# ASP를 이용한 예제

### ASP를 이용한 SMS 웹 서비스 이용방법 <a href="asp-net-vb-sms" id="asp-net-vb-sms"></a>

{% file src="../.gitbook/assets/sendsms_sample_asp (1).zip" %}
ASP를 이용한 예제소스 다운로드
{% endfile %}

#### 1. SMS발송 정보를 입력 받을 폼을 작성합니다. (예제소스에 포함) <a href="1-visual-studio-net" id="1-visual-studio-net"></a>

> 계정 인증키는 \[계정관리 > 호스팅 계정정보]에서 확인 하실 수 있습니다.​

![](../.gitbook/assets/asp\_1.png)

#### 2. 편집기를 이용해 아래의 소스코드를 작성하여 SendSms.asp로 저장합니다. <a href="2" id="2"></a>

> 하단의 예제는 MSXML 6.0을 사용합니다.                                                           ** **[**MSXML 6.0 다운로드**](https://www.microsoft.com/ko-kr/download/search.aspx?q=MSXML)****

```markup
<%
'받는사람 핸드폰 번호
sTranPhone = Request("txtTranPhone")

'보내는사람 핸드폰 번호
sTranCallback = Request("txtTranCallback")

'예약전송 일시(생략시 즉시전송)
sTranDate = Request("txtTranDate")

'전송 메시지
sTranMsg = Request("txtTranMsg")

'계정번호
sGuestNo = Request("txtGuestNo")

'계정 인증키
sGuestAuthKey = Request("txtGuestAuthKey")

'발송구분 (SMS/LMS/MMS)
sType = Request("comType")

'LMS/MMS일 경우 제목
sSubject = Request("txtSubject")

 '*======================================================================*\
 ' MMS일 경우 첨부파일 처리
 ' 서버&로컬 에 저장된 이미지 파일 읽어올때.
 ' 웹경로,로컬경로 모두 가능 합니다.
'\*======================================================================*/

'웹경로
'imgPath = "http://websvc.nesolution.com/sms/MMSAttachFiles/M050085/20180510145947.jpg"
'로컬경로
imgPath ="d:\img\test.jpg"

 '"," 콤마로 구분 최대 3개 첨부 가능 합니다.
stringBase64files = GetStringBase64files(imgPath)&_
   ","&GetStringBase64files(imgPath)&","&GetStringBase64files(imgPath)


Function GetStringBase64files(imgPath)
    imgPath = LCase(imgPath)

    if LEFT(imgPath,4) ="http" THEN
         Set Http= CreateObject("MSXML2.ServerXMLHTTP")
          Http.Open "GET", imgPath, false
          Http.Send()
          binData = Http.ResponseBody
          GetStringBase64files = Base64encode(binData)
        Set Http = Nothing
    ELSE
          Dim inputStream
          Set inputStream = CreateObject("ADODB.Stream")
          inputStream.Open
          inputStream.Type = 1  ' adTypeBinary
          inputStream.LoadFromFile imgPath
          Dim bytes: bytes = inputStream.Read
         GetStringBase64files =Base64Encode(bytes)
    END IF
End Function

Function Base64Encode(sText)
    Dim oXML, oNode
    Set oXML = CreateObject("Msxml2.DOMDocument.3.0")
    Set oNode = oXML.CreateElement("base64")
    oNode.dataType = "bin.base64"
    oNode.nodeTypedValue = sText
    Base64Encode = oNode.text
    Set oNode = Nothing
    Set oXML = Nothing
End Function

'*======================================================================*\
' MMS일 경우 첨부파일 처리
 '프론트에서 이미지 파일을 base64로 생성후 post로 받아 올때.
'\*======================================================================*/
'첨부파일
'stringBase64files = Request("Base64files")
'stringBase64files = Replace(stringBase64files,"\t","+")


sParam = "cmd=SendSms"
sParam = sParam + "&guest_no=" + sGuestNo
sParam = sParam + "&guest_key=" + sGuestAuthKey
sParam = sParam + "&tran_phone=" + sTranPhone
sParam = sParam + "&tran_callback=" + sTranCallback
sParam = sParam + "&tran_date=" + sTranDate
sParam = sParam + "&tran_msg=" + Server.URLEncode(sTranMsg)
sParam = sParam + "&type=" + sType

If sType = "LMS" Or sType = "MMS" Then
    sParam = sParam + "&subject=" + Server.URLEncode(sSubject)    '제목
End IF

If sType = "MMS" Then
    sParam = sParam + "&files=" + Server.URLEncode(stringBase64files)    '파일
End IF

sResponse = SendPOST("http://websvc.nesolution.com/SMS/SMS.aspx", sParam)

function SendPOST(parm_url, parm_post)
    Set xmlHttp = Server.Createobject("MSXML2.ServerXMLHTTP.6.0")
    xmlHttp.Open "POST", parm_url, False
    xmlHttp.setRequestHeader "User-Agent", "asp httprequest"
    xmlHttp.setRequestHeader "content-type", "application/x-www-form-urlencoded"
    xmlHttp.Send parm_post
    SendPOST = xmlHttp.responseText
    xmlHttp.abort()
    set xmlHttp = Nothing
end function

%>

<HTML>
<HEAD>
    <TITLE>New Document</TITLE>
    <meta http-equiv="Content-Type" content="text/html; charset=ks_c_5601-1987">
    <style type="text/css">
    <!--
      .unnamed1 { font-family:"굴림"; font-size:9pt; line-height:12pt}
    //-->
    </style>
</HEAD>
<BODY>
    <div align="center">
      <h2>SMS 예제소스(asp)</h2>
      <br>
      <span class="unnamed1">전송결과 : <b><%=sResponse%></b></span>
    </div>
</BODY>
</HTML>
```

> #### **파라미터** ✔ <a href="undefined" id="undefined"></a>

| **파라미터**      | **설명**                                                                                                                                                                         |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| tran_phone    | <p>수신자 전화번호(생략불가), 여러번호일 경우에는 ;으로 구분.</p><p>전화번호 구분자 대쉬(-)는 있거나 없거나 상관없음</p>                                                                                                   |
| tran_callback | 송신자 전화번호(생략불가)                                                                                                                                                                 |
| tran_date     | <p>예약 전송시에만 사용, 포맷은 시분까지 포함된 날짜 포맷.</p><p>생략시에는 즉시 전송(예.2003-01-01 13:01)</p>                                                                                                  |
| tran_msg      | <p>전송 메시지(생략불가).</p><p>SMS : 최대 80byte (용량이 넘으면 짤려서 전송)</p><p>LMS/MMS : 최대 2,000byte</p>                                                                                       |
| guest_no      | 계정번호(예.000001)                                                                                                                                                                 |
| guest_key     | <p>관리자 계정과 암호를 이용해 생성한 계정 인증 키</p><p>(회원전용 사이트에서 확인 가능)</p>                                                                                                                    |
| type          | <p>메시지 전송 타입. "SMS" / "LMS" / "MMS" / "AUTO" 중에서 선택.</p><p>LMS/MMS 사용 시 서비스 신청이 되어 있어야 함</p><p>빈 값을 넘기면 "SMS"형식으로 발송</p><p>"AUTO"는 메시지의 길이를 체크하여 80byte를 초과 시 자동으로 LMS로 발송</p> |
| subject       | <p>LMS/MMS 메시지의 메시지 제목.</p><p>LMS/MMS 방식을 사용하는 경우 필수.</p>                                                                                                                      |
| files         | <p>MMS 첨부 이미지 파일명.</p><p>첨부 파일이 2개 이상인 경우 컴마(,)로 구분</p><p>MMS의 경우 필수</p><p>최대 3개 까지 지정 가능, 최대 50kb gif,png,jpg 파일형식</p>                                                        |

> ### **반환 값** ✔ <a href="undefined-1" id="undefined-1"></a>

{% hint style="success" %}
#### 성공 시    "OK"
{% endhint %}

{% hint style="danger" %}
**실패 시 "Exception: 에러메시지"**
{% endhint %}

####

#### 3. 실행결과 화면입니다.

> 정상적으로 메시지가 발송되었을 경우

![](../.gitbook/assets/asp\_2.png)

> 오류로 인하여 메시지를 발송하지 못했을 경우

![](../.gitbook/assets/asp\_3.png)
