---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-10"

---



{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 권한 부여
{: #grant_permissions}

{{site.data.keyword.Bluemix}}에서 사용자에게 하나 이상의 역할을 지정할 수 있습니다. 이러한 역할은 사용자가 {{site.data.keyword.loganalysisshort}} 서비스를 사용하여 수행할 수 있는 태스크를 정의합니다.
{:shortdesc}



## {{site.data.keyword.Bluemix_notm}} UI를 통해 사용자에게 IAM 정책 지정
{: #grant_permissions_ui_account}

계정 로그를 보고 관리하는 권한을 사용자에게 부여하려면 이 사용자가 계정에서 {{site.data.keyword.loganalysisshort}} 서비스를 사용하여 수행할 수 있는 조치를 설명하는 해당 사용자에 대한 정책을 추가해야 합니다. 계정 소유자만 사용자에게 개별 정책을 지정할 수 있습니다.

{{site.data.keyword.Bluemix_notm}}에서 {{site.data.keyword.loganalysisshort}} 서비스로 작업할 수 있는 권한을 사용자에게 부여하려면 다음 단계를 완료하십시오. 

1. {{site.data.keyword.Bluemix_notm}} 콘솔에 로그인하십시오. 

    웹 브라우저를 열고 {{site.data.keyword.Bluemix_notm}} 대시보드를 실행하십시오. [http://bluemix.net ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://bluemix.net){:new_window} 
	
	사용자 ID 및 비밀번호를 사용하여 로그인하면 {{site.data.keyword.Bluemix_notm}} UI가 열립니다. 

2. 메뉴 표시줄에서 **관리 > 계정 > 사용자**를 클릭하십시오.  

    *사용자* 창에 현재 선택한 계정의 이메일 주소와 함께 사용자 목록이 표시됩니다. 
	
3. 사용자가 계정의 구성원인 경우 목록에서 사용자 이름을 선택하거나 *조치* 메뉴에서 **사용자 관리**를 클릭하십시오. 

    사용자가 계정의 구성원이 아닌 경우 [사용자 초대](/docs/iam/iamuserinv.html#iamuserinv)를 참조하십시오. 

4. **액세스 정책** 섹션에서 **서비스 정책 지정**을 클릭한 후 **리소스에 대한 액세스 권한 지정**을 선택하십시오.

    *사용자에 리소스 액세스 권한 지정** 창이 열립니다.

5. 정책에 대한 정보를 입력하십시오. 다음 표는 정책을 정의하는 데 필요한 필드를 나열합니다.  

    <table>
	  <caption>IAM 정책을 구성하는 필드 목록입니다. </caption>
	  <tr>
	    <th>필드</th>
		<th>값</th>
	  </tr>
	  <tr>
	    <td>서비스</td>
		<td>*IBM Cloud Log Analysis*</td>
	  </tr>	  
	  <tr>
	    <td>지역</td>
		<td>사용자에게 로그 작업을 수행하기 위한 액세스 권한을 부여할 지역을 지정할 수 있습니다. 하나 이상의 지역을 개별적으로 선택하거나 **모든 현재 지역**을 선택하여 모든 지역에 대한 액세스 권한을 부여하십시오.</td>
	  </tr>
	  <tr>
	    <td>서비스 인스턴스</td>
		<td>*모든 서비스 인스턴스*를 선택하십시오.</td>
	  </tr>
	  <tr>
	    <td>역할</td>
		<td>하나 이상의 IAM 역할을 선택하십시오. <br>올바른 역할: *관리자*, *운영자*, *편집자* 및 *뷰어*. <br>각 역할에 허용되는 조치에 대한 자세한 정보는 [IAM 역할](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles)을 참조하십시오.
		</td>
	  </tr>
     </table>
	
6. **정책 지정**을 클릭하십시오. 
	
구성하는 정책을 선택한 지역에 적용할 수 있습니다. 

## 명령행을 사용하여 사용자에게 IAM 정책 지정
{: #grant_permissions_commandline}

계정 로그를 보고 관리하는 권한을 사용자에게 부여하려면 사용자에게 IAM 역할을 부여해야 합니다. IAM 역할 및 역할에 따라 {{site.data.keyword.loganalysisshort}} 서비스로 수행할 수 있는 작업에 대한 자세한 정보는 [IAM 역할](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles)을 참조하십시오. 

이 조작은 계정 소유자만 수행할 수 있습니다.

명령행을 통해 계정 로그를 볼 수 있는 액세스 권한을 사용자에게 부여하려면 다음 단계를 완료하십시오. 

1. 계정 ID를 가져오십시오.  

    다음 명령을 실행하여 계정 ID를 가져오십시오. 

    ```
	bx iam accounts
	```
    {: codeblock}	

	해당 GUID가 포함된 계정 목록이 표시됩니다.
	
	사용자에게 권한을 부여하려는 계정의 계정 ID를 `$acct_id`와 같은 쉘 변수로 내보내십시오. 예를 들어 다음과 같습니다.
	
	```
	export acct_id="1234567891234567812341234123412"
	```
	{: screen}

2. 권한을 부여하려는 사용자의 {{site.data.keyword.Bluemix_notm}} ID를 가져오십시오.

    1. 계정과 연관된 사용자를 표시하십시오. 다음 명령을 실행하십시오.

    ```
		bx iam account-users
		```
		{: codeblock}
		
	2. 사용자의 GUID를 가져오십시오. **참고:** 이 단계는 권한을 부여할 대상 사용자가 완료해야 합니다.
	
	    예를 들어 사용자 ID를 가져오려면 해당 사용자가 다음 명령을 실행하도록 요청하십시오.
		
		IAM 토큰을 가져오십시오. 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} CLI를 사용하여 IAM 토큰 가져오기](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli)를 참조하십시오.

        IAM 토큰의 처음 두 개의 점 사이에 있는 IAM 토큰에서 데이터를 가져오십시오. 데이터를 `$user_data`와 같은 쉘 변수로 내보내십시오.
		
		```
	    export user_data="xxxxxxxxxxxxxxxxxxxxxxxxxxx"
	    ```
	    {: screen}
		
		예를 들어 사용자 ID를 가져오려면 다음 명령을 실행하십시오. 이 명령은 해당 샘플에서 jq를 사용하여 정보를 JSON 형식화된 텍스트로 디코딩합니다.
		
		```
		echo $user_data | base64 -d | jq
		```
		{: codeblock}
		
		이 명령을 실행하면 출력은 다음과 같습니다.
		
		```
		$ echo $user_data | base64 -d | jq
        {
        "iam_id": "IBMid-xxxxxxxxxx",
        "id": "IBMid-xxxxxxxxxx",
        "realmid": "IBMid",
        ......
		}
        ```
	    {: screen}
		
		계정 소유자에게 사용자 ID를 보내십시오.
		
	3. 사용자 ID를 `$user_ibm_id`와 같은 쉘 변수로 내보내십시오. 
	
		```
		export user_ibm_id="IBMid-xxxxxxxxxx"
		```
		{: codeblock}

3. 사용자가 아직 구성원이 아닌 경우 사용자를 계정에 초대하십시오. 자세한 정보는 [사용자 초대](/docs/iam/iamuserinv.html#iamuserinv)를 참조하십시오. 

    예를 들어 다음 명령을 실행하여 사용자 xxx@yyy.com을 계정 zzz@ggg.com으로 초대하십시오. 
	
	```
	bx iam account-user-invite xxx@yyy.com zzz@ggg.com OrgAuditor dev SpaceDeveloper
	```
	{: codeblock}
		
4. 정책 파일 이름을 작성하십시오.  

    예를 들어 다음 템플리트를 사용하여 US 남부 지역의 보기 권한을 부여하십시오.
	
	```
	{
		"roles" : [
			{
				"id": "crn:v1:bluemix:public:iam::::role:Editor" 
			}
		],
		"resources": [
			{
				"serviceName": "ibmcloud-log-analysis",
				"region": "us-south"
			}
		]
	}
	```
	{: codeblock}
	
	정책 파일 이름을 지정하십시오. `policy.json`
	
5. 사용자 ID의 IAM 토큰을 가져오십시오. 

    자세한 정보는 [{{site.data.keyword.Bluemix_notm}} CLI를 사용하여 IAM 토큰 가져오기](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli)를 참조하십시오.

    IAM 토큰을 `$iam_token`과 같은 쉘 변수로 내보내십시오. 예를 들어 다음과 같습니다. 
	
	```
	export iam_token="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
	
6. {{site.data.keyword.loganalysisshort}} 서비스에 대한 작업 권한을 사용자에게 부여하십시오.  

   다음 cURL 명령을 사용하여 US 남부 지역의 권한을 부여하십시오. 
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.ng.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}
	
	다음 cURL 명령을 사용하여 영국 지역의 권한을 부여하십시오.
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.eu-gb.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}

	
사용자에게 권한을 부여하면 사용자가 {{site.data.keyword.Bluemix_notm}}에 로그인하여 계정 레벨 로그를 볼 수 있습니다.



## {{site.data.keyword.Bluemix_notm}} UI를 사용하여 사용자에게 영역 로그를 볼 수 있는 권한 부여
{: #grant_permissions_ui_space}

사용자에게 영역 로그를 볼 수 있는 권한을 부여하려면 해당 사용자가 영역에서 {{site.data.keyword.loganalysisshort}} 서비스에 대한 작업을 수행할 수 있는 조치를 설명하는 Cloud Foundry 역할을 지정해야 합니다.

{{site.data.keyword.loganalysisshort}} 서비스에 대한 작업을 수행할 권한을 사용자에게 부여하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} 콘솔에 로그인하십시오.

    웹 브라우저를 열고 {{site.data.keyword.Bluemix_notm}} 대시보드를 실행하십시오. [http://bluemix.net ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://bluemix.net){:new_window}
	
	사용자 ID 및 비밀번호를 사용하여 로그인하면 {{site.data.keyword.Bluemix_notm}} UI가 열립니다.

2. 메뉴 표시줄에서 **관리 > 계정 > 사용자**를 클릭하십시오.

    *사용자* 창에 현재 선택한 계정의 이메일 주소와 함께 사용자 목록이 표시됩니다.
	
3. 사용자가 계정의 구성원인 경우 목록에서 사용자 이름을 선택하거나 *조치* 메뉴에서 **사용자 관리**를 클릭하십시오.

    사용자가 계정의 구성원이 아닌 경우 [사용자 초대](/docs/iam/iamuserinv.html#iamuserinv)를 참조하십시오.

4. **Cloud Foundry 액세스**를 선택한 후 조직을 선택하십시오.

    해당 조직에서 사용 가능한 영역의 목록이 나열됩니다.

5. 하나의 영역을 선택하십시오. 그런 다음 메뉴 조치에서 **영역 역할 편집**을 선택하십시오.

6. 하나 이상의 영역 역할을 선택하십시오. 올바른 역할은 *관리자*, *개발자* 및 *감사자*입니다.
	
7. **역할 저장**을 클릭하십시오.




