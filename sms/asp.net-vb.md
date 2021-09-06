---
description: ASP.NET(VB)를 이용한 SMS 웹 서비스 이용방법을 안내합니다.
---

# ASP.NET\(VB\)을 이용한 예제

## ASP.NET\(VB\)를 이용한 SMS 웹 서비스 이용방법

{% file src="../.gitbook/assets/sendsms\_sample\_vb\_aspnet.zip" caption="ASP.NET\(VB\)를 이용한 예제소스 다운로드" %}

### 1. Visual Studio.NET을 열어 새로운 프로젝트를 생성합니다.

![](../.gitbook/assets/asp_vb_1.png)

### 2. 솔루션 탐색기에서 마우스 오른쪽을 클릭하여 웹 참조 메뉴를 선택합니다.

![](../.gitbook/assets/asp_vb_2.png)

### 3. 아래 DpSms 웹 서비스URL을 입력하고 웹 참조 이름을 결정한 후 참조 추가 버튼을 누릅니다.

> DpSms 웹 참조 URL : [http://websvc.nesolution.com/sms/sms.asmx](http://websvc.nesolution.com/sms/sms.asmx)​

![](../.gitbook/assets/asp_vb_3.png)

![](../.gitbook/assets/asp_vb_4.png)

![](../.gitbook/assets/asp_vb_5.png)

### 4. 아래와 같이 SMS발송 정보를 입력 받을 폼을 작성합니다. \(예제소스에 포함\)

![](../.gitbook/assets/asp_vb_6.png)

### 5. 메시지 전송 버튼을 더블 클릭하여 btnSend\_Click 이벤트에 아래의 소스 코드를 삽입합니다.

```text
private void btnSend_Click(object sender, System.EventArgs e){    WebSvc_Sms.SMS oSms = new WebSvc_Sms.SMS();​    string stringBase64files =  string.Empty;    if (Request.Files != null)    {        for (int i = 0; i < Request.Files.Count; i++)        {            HttpPostedFile file = Request.Files[i];            stringBase64files += ParseCv(file) + ",";            }    }​    string sResult = oSms.SendSms(txtTranPhone.Text,                     txtTranCallback.Text,                     txtTranDate.Text,                          txtTranMsg.Text,                           txtGuestNo.Text,                            txtGuestAuthKey.Text,                  comType.SelectedValue,                txtSubject,                              stringBase64files);       lblResult.Text = sResult;}​private  string ParseCv(HttpPostedFile fileBase){    byte[] fileInBytes = new byte[fileBase.ContentLength];    using (BinaryReader theReader = new BinaryReader(fileBase.InputStream))    {        fileInBytes = theReader.ReadBytes(fileBase.ContentLength);    }    string fileAsString = Convert.ToBase64String(fileInBytes);​    return fileAsString;}
```

> ## **파라미터** ✅  <a id="undefined"></a>

> ## **반환 값** ✅  <a id="undefined-1"></a>

## 6. 실행결과 화면입니다. <a id="6"></a>

![](https://gblobscdn.gitbook.com/assets%2F-Mi_8LPPppX55FEwiSXr%2F-MitjzRZvtLoYKG1sP4Z%2F-MitkuNWdiRRkQoDnWrV%2Faspnet_8.png?alt=media&token=86418e41-759c-4c63-856a-4843f26b554b)

![](https://gblobscdn.gitbook.com/assets%2F-Mi_8LPPppX55FEwiSXr%2F-MitjzRZvtLoYKG1sP4Z%2F-MitkuNXMMyJJ4oWr20t%2Faspnet_9.png?alt=media&token=ba1fbb17-ff42-4c12-bb6f-e21a9dc04729)

![](https://gblobscdn.gitbook.com/assets%2F-Mi_8LPPppX55FEwiSXr%2F-MitjzRZvtLoYKG1sP4Z%2F-MitkuNYhpaUzYrDQ2nf%2Faspnet_10.png?alt=media&token=a4aa77e4-bf0f-4081-aaeb-60dc11c2ae24)

