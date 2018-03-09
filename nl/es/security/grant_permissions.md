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


# Concesión de permisos
{: #grant_permissions}

En {{site.data.keyword.Bluemix}}, puede asignar uno o varios roles a los usuarios. Estos roles definen qué tareas están habilitadas para dicho usuario para trabajar con el servicio de {{site.data.keyword.loganalysisshort}}.{:shortdesc}



## Asignación de una política de IAM a un usuario mediante la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} 
{: #grant_permissions_ui_account}

Para otorgar permisos a un usuario para ver y gestionar registros de cuentas, debe añadir una política para dicho usuario que describe las acciones que puede realizar con el servicio de {{site.data.keyword.loganalysisshort}} en la cuenta. Solo los propietarios de cuentas pueden asignar políticas individuales para los usuarios.

En {{site.data.keyword.Bluemix_notm}}, complete los pasos siguientes para otorgar permisos a un usuario para trabajar con el servicio de {{site.data.keyword.loganalysisshort}}:

1. Inicie sesión en la consola de {{site.data.keyword.Bluemix_notm}}.

    Abra un navegador web y lance el panel de control de {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://bluemix.net){:new_window}
	
	Cuando inicia sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.

2. En la barra de menús, pulse **Gestionar > Cuenta > Usuarios**. 

    La ventana *Usuarios* muestra una lista de usuarios con sus direcciones de correo electrónico para la cuenta seleccionada actualmente.
	
3. Si el usuario es un miembro de la cuenta, seleccione el nombre de usuario de la lista, o pulse **Gestionar usuario** del menú *Acciones*.

    Si el usuario no es un miembro de la cuenta, consulte [Invitación a usuarios](/docs/iam/iamuserinv.html#iamuserinv).

4. En la sección **Políticas de acceso**, pulse **Asignar políticas de servicio** y, a continuación, seleccione **Asignar acceso a recursos**..

    Se abrirá la ventana *Asignar acceso de recursos al usuario**.

5. Especifique la información sobre la política. La tabla siguiente lista los campos necesarios para definir una política: 

    <table>
	  <caption>Lista de campos para configurar una política IAM.</caption>
	  <tr>
	    <th>Campo</th>
		<th>Valor</th>
	  </tr>
	  <tr>
	    <td>Servicios</td>
		<td>*IBM Cloud Log Analysis*</td>
	  </tr>	  
	  <tr>
	    <td>Regiones</td>
		<td>Puede especificar las regiones en las que se otorgará acceso al usuario para trabajar con registros. Seleccione una o varias regiones individualmente, o seleccione **Todas las regiones actuales** para otorgar acceso a todas las regiones.</td>
	  </tr>
	  <tr>
	    <td>Instancia de servicio</td>
		<td>Seleccione *Todas las instancias de servicio*.</td>
	  </tr>
	  <tr>
	    <td>Roles</td>
		<td>Seleccione uno o varios roles de IAM. <br>Los roles válidos son: *administrador*, *operador*, *editor*, y *visor*. <br>Para obtener más información sobre las acciones que están permitidas por rol, consulte [Roles de IAM](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles).</td>
	  </tr>
     </table>
	
6. Pulse **Asignar política**.
	
La política que configure es aplicable a las regiones seleccionadas. 

## Asignación de una política de IAM a un usuario mediante la línea de mandatos
{: #grant_permissions_commandline}

Para otorgar permisos a un usuario para ver y gestionar registros de cuentas, debe otorgar al usuario un rol de IAM. Para obtener más información sobre los roles de IAM y sobre las tareas que habilita cada rol para trabajar con el servicio {{site.data.keyword.loganalysisshort}}, consulte [Roles de IAM](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles).

Esta operación solamente puede realizarla el propietario de cuenta.

Siga los pasos siguientes para otorgar a un usuario acceso para ver registros de cuenta mediante la línea de mandatos:

1. Obtenga el ID de cuenta. 

    Ejecute el mandato siguiente para obtener el ID de cuenta:

    ```
	bx iam accounts
	```
    {: codeblock}	

	Una lista de cuentas en las que se visualiza los GUID.
	
	Exporte el ID de la cuenta sobre la que piensa otorgar permisos a un usuario a una variable de shell coo `$acct_id`, por ejemplo: 	
	```
	export acct_id="1234567891234567812341234123412"
	```
	{: screen}

2. Obtenga el ID de {{site.data.keyword.Bluemix_notm}} del usuario al que desea otorgar permisos.

    1. Visualice los usuarios que están asociados con la cuenta. Ejecute el mandato siguiente:

    ```
		bx iam account-users
		```
		{: codeblock}
		
	2. Obtenga el GUID del usuario. **Nota:** Debe llevar a cabo este paso el usuario al que va a otorgar permisos. 	
	    Por ejemplo, solicite al usuario que ejecute los mandatos siguientes para obtener su ID de usuario:
		
		Obtenga la señal de IAM. Para obtener más información, consulte [Obtención de la señal de IAM mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli).

        Obtenga los datos de la señal de IAM que se encuentran entre los dos primeros puntos en la señal de IAM. Exporte los datos a una variable de shell como `$user_data`.
		
		```
	    export user_data="xxxxxxxxxxxxxxxxxxxxxxxxxxx"
	      ```
	    {: screen}
		
		Ejecute el mandato siguiente, por ejemplo, para obtener el ID de usuario. Este mandato utiliza jq en este ejemplo para descodificar la información en texto con formato de JSON:
		
		```
		echo $user_data | base64 -d | jq
		```
		{: codeblock}
		
		La salida de la ejecución de este mandato es la siguiente:
		
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
		
		Envíe el ID de usuario al propietario de la cuenta.
		
	3. Exporte el ID de usuario en una variable de shell como `$user_ibm_id`.
	
		```
		export user_ibm_id="IBMid-xxxxxxxxxx"
		```
		{: codeblock}

3. Invite el usuario a la cuenta si no es un miembro. Para obtener más información, consulte [Invitación a usuarios](/docs/iam/iamuserinv.html#iamuserinv).

    Por ejemplo, ejecute el mandato siguiente para invitar al usuario xxx@yyy.com a la cuenta zzz@ggg.com:
	
	```
	bx iam account-user-invite xxx@yyy.com zzz@ggg.com OrgAuditor dev SpaceDeveloper
	```
	{: codeblock}
		
4. Cree un nombre de archivo de política. 

    Por ejemplo, utilice la plantilla siguiente para otorgar permisos en la región EE.UU. sur:
	
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
	
	Nombre del archivo de política: `policy.json`
	
5. Obtenga la señal de IAM para su ID de usuario.

    Para obtener más información, consulte [Obtención de la señal de IAM mediante la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli).

    Exporte la señal de IAM a una variable de shell como, por ejemplo, `$iam_token`:
	
	```
	export iam_token="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
	
6. Otorgue los permisos de usuario para trabajar con el servicio de {{site.data.keyword.loganalysisshort}}. 

   Ejecute el siguiente mandato cURL para otorgar permisos en la región EE.UU. sur:
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.ng.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}
	
	Ejecute el siguiente mandato cURL para otorgar permisos en la región Reino Unido:
	
 ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.eu-gb.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}

	
Después de otorgar permisos a un usuario, el usuario puede iniciar una sesión en {{site.data.keyword.Bluemix_notm}} y ver registros a nivel de cuenta.

## Concesión de permisos a un usuario para ver registros del espacio mediante la IU de {{site.data.keyword.Bluemix_notm}}
{: #grant_permissions_ui_space}

Para otorgar a un usuario permisos para ver los registros de un espacio, debe asignar al usuario un rol de Cloud Foundry que describa las acciones que puede realizar este usuario con el servicio {{site.data.keyword.loganalysisshort}} en el espacio.

Complete los pasos siguientes para otorgar permisos a un usuario para trabajar con el servicio de {{site.data.keyword.loganalysisshort}}:

1. Inicie la sesión en la consola de {{site.data.keyword.Bluemix_notm}}.

  Abra un navegador web e inicie el panel de control de {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://bluemix.net){:new_window}
	
	Cuando inicia sesión con su ID de usuario y su contraseña, se abre la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.

2. En la barra de menús, pulse **Gestionar > Cuenta > Usuarios**.

  La ventana *Usuarios* muestra una lista de usuarios con las direcciones de correo electrónico para la cuenta seleccionada actualmente.
	
3. Si el usuario es un miembro de la cuenta, seleccione el nombre de usuario de la lista, o pulse **Gestionar usuario** del menú *Acciones*.

  Si el usuario no es un miembro de la cuenta, consulte [Invitación a usuario] (/docs/iam/iamuserinv.html#iamuserinv).

4. Seleccione **Acceso de Cloud Foundry** y, a continuación, seleccione la organización.

    Se listará la lista de espacios disponibles en dicha organización.

5. Elija un espacio. A continuación, desde la acción de menú, seleccione **Editar rol de espacio**.

6. Seleccione uno o más roles de espacio. Los roles válidos son: *Gestor*, *Desarrollador* y *Auditor*
	
7. Pulse **Guardar rol**.




