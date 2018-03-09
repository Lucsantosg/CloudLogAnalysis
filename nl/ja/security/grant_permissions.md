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


# 許可の付与
{: #grant_permissions}

{{site.data.keyword.Bluemix}} では、ユーザーに 1 つ以上の役割を割り当てることができます。 これらの役割は、{{site.data.keyword.loganalysisshort}} サービスを使用して作業するためにユーザーが使用できるタスクを定義します。 
{:shortdesc}



## {{site.data.keyword.Bluemix_notm}} UI を使用してユーザーに IAM ポリシーを割り当てる
{: #grant_permissions_ui_account}

アカウント・ログを表示および管理する許可をユーザーに付与するには、そのユーザーがアカウント内で {{site.data.keyword.loganalysisshort}} サービスを使用して実行できるアクションを記述するポリシーを追加する必要があります。 アカウント所有者のみが、個々のポリシーをユーザーに割り当てることができます。

{{site.data.keyword.Bluemix_notm}} で、{{site.data.keyword.loganalysisshort}} サービスを使用して作業する許可をユーザーに付与するには、以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} コンソールにログインします。

    Web ブラウザーを開き、{{site.data.keyword.Bluemix_notm}} ダッシュボード: [http://bluemix.net ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://bluemix.net){:new_window} を起動します。
	
	ユーザー ID とパスワードを使用してログインすると、{{site.data.keyword.Bluemix_notm}} UI が開きます。

2. メニュー・バーから、**「管理」>「アカウント」>「ユーザー」**をクリックします。 

    「*ユーザー*」ウィンドウに、現在選択されているアカウントにおけるユーザーのリストが、E メール・アドレスと共に表示されます。
	
3. ユーザーがアカウントのメンバーである場合、リストからユーザー名を選択するか、または、**「アクション」**メニューから*「ユーザーの管理」*をクリックします。

    ユーザーがアカウントのメンバーでない場合、『[ユーザーの招待](/docs/iam/iamuserinv.html#iamuserinv)』を参照してください。

4. **「アクセス・ポリシー」**セクションで、**「サービス・ポリシーの割り当て (Assign service policies)」**をクリックし、次に**「リソースへのアクセス権限の割り当て (Assign access to resources)」**を選択します。

    *「ユーザー * へのリソース・アクセス権限の割り当て (Assign resource access to user*)」* ウィンドウが開きます。

5. ポリシーに関する情報を入力します。 以下の表は、ポリシーを定義する必須のフィールドを示します。 

    <table>
	  <caption>IAM ポリシーを構成するためのフィールドのリスト。</caption>
	  <tr>
	    <th>フィールド</th>
		<th>値</th>
	  </tr>
	  <tr>
	    <td>サービス</td>
		<td>*IBM Cloud Log Analysis*</td>
	  </tr>	  
	  <tr>
	    <td>地域</td>
		<td>ユーザーがログを処理する権限を付与される地域を指定できます。 1 つ以上の地域を個々に選択するか、または、**「すべての現行地域」**を選択してすべての地域の権限を付与します。</td>
	  </tr>
	  <tr>
	    <td>サービス・インスタンス</td>
		<td>*「すべてのサービス・インスタンス」* を選択します。</td>
	  </tr>
	  <tr>
	    <td>役割</td>
		<td>1 つ以上の IAM 役割を選択してください。 <br>有効な役割は、*管理者*、*オペレーター*、*エディター*、*ビューアー*です。 <br>役割ごとの許可されるアクションについて詳しくは、『[IAM 役割](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles)』を参照してください。
		</td>
	  </tr>
     </table>
	
6. **「ポリシーの割り当て」**をクリックします。
	
構成したポリシーは、選択した地域で利用できます。 

## コマンド・ラインを使用してユーザーに IAM ポリシーを割り当てる
{: #grant_permissions_commandline}

アカウント・ログを表示および管理する許可をユーザーに付与するには、そのユーザーに IAM 役割を付与する必要があります。 IAM 役割と、{{site.data.keyword.loganalysisshort}} サービスで実行できる役割別のタスクについて詳しくは、『[IAM 役割](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles)』を参照してください。

この操作は、アカウントの所有者のみが実行できます。

コマンド・ラインを使用して、アカウント・ログを表示する権限をユーザーに付与するには、以下のステップを実行します。

1. アカウント ID を取得します。 

    以下のコマンドを実行して、アカウント ID を取得します。

    ```
	bx iam accounts
	```
    {: codeblock}	

	アカウントとその GUID のリストが表示されます。
	
	ユーザーに許可を付与しようとしているアカウントのアカウント ID を「$acct_id」などのシェル変数にエクスポートします。以下に例を示します。
	
	```
	export acct_id="1234567891234567812341234123412"
	```
	{: screen}

2. 許可を付与するユーザーの {{site.data.keyword.Bluemix_notm}} ID を取得します。

    1. アカウントに関連付けられたユーザーを表示します。 次のコマンドを実行します。
	
	    ```
		bx iam account-users
		```
		{: codeblock}
		
	2. ユーザーの GUID を取得します。 **注:** このステップは、許可を付与する予定のユーザーによって実行される必要があります。
	
	    例えば、ユーザーに自分のユーザー ID を取得するために以下のコマンドを実行するよう依頼します。
		
		IAM トークンを取得します。 詳しくは、[{{site.data.keyword.Bluemix_notm}} CLI を使用した IAM トークンの取得](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli) を参照してください。

        IAM トークンから、IAM トークンの 1 番目と 2 番目のドットの間にあるデータを取得します。 そのデータを「$user_data」などのシェル変数にエクスポートします。 
		
		```
	    export user_data="xxxxxxxxxxxxxxxxxxxxxxxxxxx"
	    ```
	    {: screen}
		
		例えば、ユーザー ID を取得する以下のコマンドを実行します。 このコマンドは、このサンプルでは jq を使用して情報を JSON の定形式テキストにデコードします。
		
		```
		echo $user_data | base64 -d | jq
		```
		{: codeblock}
		
		このコマンド実行の出力は以下のようになります。
		
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
		
		アカウント所有者にユーザー ID を送信します。
		
	3. `$user_ibm_id` のようなシェル変数にユーザー ID をエクスポートします。
	
		```
		export user_ibm_id="IBMid-xxxxxxxxxx"
		```
		{: codeblock}

3. ユーザーがアカウントのメンバーではない場合は招待します。 詳しくは、『[ユーザーの招待](/docs/iam/iamuserinv.html#iamuserinv)』を参照してください。

    例えば、以下のコマンドを実行してユーザー xxx@yyy.com をアカウント zzz@ggg.com に招待します。
	
	```
	bx iam account-user-invite xxx@yyy.com zzz@ggg.com OrgAuditor dev SpaceDeveloper
	```
	{: codeblock}
		
4. ポリシー・ファイル名を作成します。 

    例えば、米国南部地域での表示の許可を付与するには、以下のテンプレートを使用します。
	
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
	
	ポリシー・ファイルに `policy.json` という名前を付けます。
	
5. ご使用のユーザー ID の IAM トークンを取得します。

    詳しくは、『[{{site.data.keyword.Bluemix_notm}}  を使用した IAM トークンの取得](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli)』を参照してください。

    IAM トークンを `$iam_token` などのシェル変数にエクスポートします。以下に例を示します。
	
	```
	export iam_token="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
	
6. {{site.data.keyword.loganalysisshort}} サービスで作業する許可をユーザーに付与します。 

   米国南部地域での許可を付与するには、次の cURL コマンドを実行します。
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.ng.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}
	
	英国地域での許可を付与するには、次の cURL コマンドを実行します。
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.eu-gb.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}

	
ユーザーに許可を付与すると、そのユーザーは {{site.data.keyword.Bluemix_notm}} にログインし、アカウント・レベルのログを表示できるようになります。



## {{site.data.keyword.Bluemix_notm}} UI を使用して、スペース・ログを表示する許可をユーザーに付与する
{: #grant_permissions_ui_space}

スペース内のログを表示する許可をユーザーに付与するには、そのユーザーがそのスペース内で {{site.data.keyword.loganalysisshort}} サービスを使用して実行できるアクションを記述する Cloud Foundry 役割をそのユーザーに割り当てる必要があります。 

{{site.data.keyword.loganalysisshort}} サービスを使用して作業する許可をユーザーに付与するには、以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} コンソールにログインします。

    Web ブラウザーを開き、{{site.data.keyword.Bluemix_notm}} ダッシュボードを起動します。[http://bluemix.net ![外部リンク・アイコン](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}
	
	ユーザー ID とパスワードを使用してログインすると、{{site.data.keyword.Bluemix_notm}} UI が開きます。

2. メニュー・バーから、「管理」>「アカウント」>「ユーザー」をクリックします。 

    「ユーザー」ウィンドウに、現在選択されているアカウントにおけるユーザーのリストが、E メール・アドレスと共に表示されます。
	
3. ユーザーがアカウントのメンバーの場合、リストからユーザー名を選択するか、*「アクション」** メニューから**「ユーザーの管理」をクリックします。

    ユーザーがアカウントのメンバーではない場合、[ユーザーの招待](/docs/iam/iamuserinv.html#iamuserinv) を参照してください。

4. **「Cloud Foundry アクセス権限」**を選択し、次に組織を選択します。

    その組織で使用可能なスペースのリストが表示されます。

5. スペースを 1 つ選択します。次に、メニュー・アクションから、**「スペースの役割の編集」**を選択します。

6. スペースの役割を 1 つ以上選択します。有効な役割は、*管理者*、*開発者*、および*監査員* です。
	
7. **「役割の保存」**をクリックします。




