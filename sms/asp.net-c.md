---
description: ASP.NET(C#)를 이용한 SMS 웹 서비스 이용방법을 안내합니다.
---

# ASP.NET(C#)을 이용한 예제

### ASP.NET(C#)를 이용한 SMS 웹 서비스 이용방법

{% file src="../.gitbook/assets/sendsms_sample_aspnet.zip" %}
ASP.NET(C#)를 이용한 예제소스 다운로드
{% endfile %}

#### 1. Visual Studio.NET을 열어 새로운 프로젝트를 생성합니다.

![](../.gitbook/assets/aspnet\_2.png)

#### 2. 솔루션 탐색기에서 마우스 오른쪽을 클릭하여 웹 참조 메뉴를 선택합니다.

![](<../.gitbook/assets/asp_vb\_2 (2) (2) (2).png>)

#### 3. 아래 DpSms 웹 서비스URL을 입력하고 웹 참조 이름을 결정한 후 참조 추가 버튼을 누릅니다.

> SMS 웹 참조 URL : [http://websvc.nesolution.com/sms/sms.asmx](http://websvc.nesolution.com/sms/sms.asmx)

![](<../.gitbook/assets/asp_vb\_3 (2) (2) (2).png>)

![](<../.gitbook/assets/asp_vb\_4 (2) (2) (2) (1).png>)

![](<../.gitbook/assets/asp_vb\_5 (2) (2) (2).png>)

#### 4. 아래와 같이 SMS발송 정보를 입력 받을 폼을 작성합니다. (예제소스에 포함)

![](<../.gitbook/assets/asp_vb\_6 (2) (2) (2).png>)

#### 5. 메시지 전송 버튼을 더블 클릭하여 btnSend_Click 이벤트에 아래의 소스 코드를 삽입합니다.

```csharp
private void btnSend_Click(object sender, System.EventArgs e)
{
    //Sms 웹 서비스 개체 생성
    WebSvc_Sms.SMS oSms = new WebSvc_Sms.SMS();

    //첨부파일 처리
    string stringBase64files =  string.Empty;
    if (Request.Files != null)
    {
        for (int i = 0; i < Request.Files.Count; i++)
        {
            HttpPostedFile file = Request.Files[i];
            stringBase64files += ParseCv(file) + ",";    //콤마(',')로 구분 합니다.
        }
    }

    //메시지 발송 메서드 호출
    string sResult = oSms.SendSms(txtTranPhone.Text,         //받는사람
            txtTranCallback.Text,         //보내는사람
            txtTranDate.Text,              //예약전송 일시
            txtTranMsg.Text,               //메시지
            txtGuestNo.Text,                //계정번호
            txtGuestAuthKey.Text,      //계정 인증키
            comType.SelectedValue,    //전송타입(SMS,LMS,MMS)
            txtSubject,                  // 메시지 제목(LMS/MMS)
            stringBase64files);   // (MMS)첨부파일 '콤마(",")로 구분' 최대3개
    //전송결과
    lblResult.Text = sResult;
}

 /// 첨부파일 Base64String 형식으로 변환 후 string 형식으로 리턴
private  string ParseCv(HttpPostedFile fileBase)
{
    byte[] fileInBytes = new byte[fileBase.ContentLength];
    using (BinaryReader theReader = new BinaryReader(fileBase.InputStream))
    {
        fileInBytes = theReader.ReadBytes(fileBase.ContentLength);
    }
    string fileAsString = Convert.ToBase64String(fileInBytes);

    return fileAsString;
}
```

> #### **파라미터** ✔

| **파라미터**       | **설명**                                                                                                                                                                         |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| stran_phone    | <p>수신자 전화번호(생략불가), 여러번호일 경우에는 ;으로 구분.</p><p>전화번호 구분자 대쉬(-)는 있거나 없거나 상관없음</p>                                                                                                   |
| stran_callback | 송신자 전화번호(생략불가)                                                                                                                                                                 |
| stran_date     | <p>예약 전송시에만 사용, 포맷은 시분까지 포함된 날짜 포맷.</p><p>생략시에는 즉시 전송(예.2003-01-01 13:01)</p>                                                                                                  |
| stran_msg      | <p>전송 메시지(생략불가).</p><p>SMS : 최대 80byte (용량이 넘으면 짤려서 전송)</p><p>LMS/MMS : 최대 2,000byte</p>                                                                                       |
| guest_no       | 계정번호(예.000001)                                                                                                                                                                 |
| guest_key      | <p>관리자 계정과 암호를 이용해 생성한 계정 인증 키</p><p>(회원전용 사이트에서 확인 가능)</p>                                                                                                                    |
| type           | <p>메시지 전송 타입. "SMS" / "LMS" / "MMS" / "AUTO" 중에서 선택.</p><p>LMS/MMS 사용 시 서비스 신청이 되어 있어야 함</p><p>빈 값을 넘기면 "SMS"형식으로 발송</p><p>"AUTO"는 메시지의 길이를 체크하여 80byte를 초과 시 자동으로 LMS로 발송</p> |
| subject        | <p>LMS/MMS 메시지의 메시지 제목.</p><p>LMS/MMS 방식을 사용하는 경우 필수.</p>                                                                                                                      |
| files          | <p>MMS 첨부 이미지 파일명.</p><p>첨부 파일이 2개 이상인 경우 컴마(,)로 구분</p><p>MMS의 경우 필수</p><p>최대 3개 까지 지정 가능, 최대 50kb gif,png,jpg 파일형식</p>                                                        |

> #### **반환 값** ✔

{% hint style="success" %}
#### 성공 시    "OK"
{% endhint %}

{% hint style="danger" %}
**실패 시 "Exception: 에러메시지"**
{% endhint %}

####

#### 6. 실행결과 화면입니다.

> 정상적으로 메시지가 발송되었을 경우

![](<../.gitbook/assets/asp_vb\_7 (2) (2) (2) (1).png>)

> 오류로 인하여 메시지를 발송하지 못했을 경우

![](<../.gitbook/assets/asp_vb\_8 (2) (2) (2) (1).png>)

![](<../.gitbook/assets/asp_vb\_9 (2) (2) (2) (2).png>)
