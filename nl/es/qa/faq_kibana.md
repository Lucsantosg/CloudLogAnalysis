---

copyright:
  years: 2017

lastupdated: "2017-07-19"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Preguntas más comunes sobre Kibana
{: #faq_kibana}

A continuación encontrará las respuestas a preguntas comunes sobre cómo utilizar las funciones de registro de {{site.data.keyword.Bluemix}}. {:shortdesc}

* [¿Qué puedo hacer si no veo datos en la página Descubrir en Kibana](/docs/services/CloudLogAnalysis/qa/faq_kibana.html##logging_qa_no_data_discover_kibana)
* [¿Qué puedo hacer si recibo una excepción de autenticación?](/docs/services/CloudLogAnalysis/qa/faq_kibana.html##logging_qa_no_data_dashboard_kibana)
* [¿Cómo inicio Kibana 3?](/docs/services/CloudLogAnalysis/qa/faq_kibana.html##logging_qa_kibana3)
* [¿Por qué veo el símbolo ? en campos de la página Descubrir de Kibana? ](/docs/services/CloudLogAnalysis/qa/faq_kibana.html##logging_qa_kibana_question)
* [Recibo un error 403 cuando intento cambiar el patrón de índice predeterminado](/docs/services/CloudLogAnalysis/qa/faq_kibana.html#error_403)

## ¿Qué puedo hacer si no veo datos en la página Descubrir en Kibana
{: #logging_qa_no_data_discover_kibana}

Hay diferentes situaciones en las que es posible que no vea datos en Kibana:

1. Cuando se inicia Kibana, es posible que no vea datos en la página Descubrir. Recibirá el mensaje siguiente: **No se han encontrado resultados.**. 
2. Si está trabajando en la página Descubrir en Kibana, es posible que, tras un breve periodo de tiempo, reciba el mensaje: **No se han encontrado resultados.** cuando intente realizar una tarea en Kibana.

Para solucionar este problema, siga estos pasos:

1. Consulte el *Selector de tiempo* definido en la página Descubrir y aumente el periodo de tiempo. 

    **Nota**: De forma predeterminada, en {{site.data.keyword.Bluemix_notm}}, el *Selector de tiempo* está definido que muestre datos correspondientes a los 15 últimos minutos.

    Para obtener más información sobre cómo definir el *Selector de tiempo*, consulte [Establecimiento de un filtro de tiempo](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter).
       
2. Pulse la lupa que se encuentra en la barra de búsqueda de la página *Descubrir*. Los datos de la página se renuevan en función de la consulta de búsqueda predeterminada.

    Como alternativa, puede establecer un periodo de *Renovación automática*.

    **Nota**: De forma predeterminada, en {{site.data.keyword.Bluemix_notm}}, el periodo de *Renovación automática* está desactivado (**OFF**).
    
    Para obtener más información sobre cómo habilitarlo, consulte el apartado sobre [Renovación automática de los datos](/docs/services/CloudLogAnalysis/kibana/analize_logs_interactively.html#discover_view_refresh_interval).



## ¿Qué puedo hacer si recibo una excepción de autenticación?
{: #logging_qa_no_data_dashboard_kibana}

Si no puede ver datos en las visualizaciones de una página Panel de control y recibe el mensaje de error: **Error: Excepción de autorización.**, compruebe los permisos para ver los datos de cada visualización.

Tenga en cuenta la información siguiente: puede configurar una o varias visualizaciones en la página Panel de control. Si la página Panel de control realiza una solicitud para recopilar los datos que se muestran en dichas visualizaciones, solo se emite una solicitud para todas las visualizaciones. Si no tienen permisos para ver los datos de una de las visualizaciones, toda la solicitud falla.

Para solucionar este problema, siga estos pasos:

1. Identifique las visualizaciones para las que no tiene permisos.

    1. Pulse el icono de *lápiz* de una visualización en la página *Panel de control*. La visualización se abre en la página *Visualizar*. Como alternativa, en la página *Visualizar* cargue una visualización. 
    2. Verifique que puede ver datos.
    
    Repita estos pasos para cada visualización.

2. Solicite acceso para ver datos en dichas visualizaciones al administrador de la nube.

3. Cree una nueva página Panel de control que excluya las visualizaciones para los que no dispone de permisos mientras se le asigna acceso para ver los datos de las visualizaciones que causan el problema. 

    Si comparte el Panel de control, no suprima visualizaciones ya que esto afectaría a otros miembros del equipo que utilicen el mismo panel de control.

## ¿Cómo inicio Kibana 3?
{: #logging_qa_kibana3}

**Nota:** Kibana 3 está en desuso.

Kibana 3 se puede iniciar desde un navegador.

Complete el siguiente paso para iniciar Kibana 3 desde un navegador:

1. Abra [https://logmet.ng.bluemix.net](https://logmet.ng.bluemix.net) para iniciar una sesión en la interfaz de usuario de Kibana.
    
2. Seleccione la versión de Kibana que desea utilizar para analizar los registros.
    * Seleccione el separador **Kibana 4** para trabajar con Kibana 4. Se abrirá la página Descubrir. Para obtener más información, consulte [Análisis interactivo de registros en Kibana](/docs/services/CloudLogAnalysis/qa/faq_kibana.html#logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).
    * Seleccione el separador **Kibana 3** para trabajar con Kibana 3. Se abrirá el panel de control de Kibana predeterminado. Para obtener información sobre cómo utilizar Kibana 3 para analizar registros, consulte [Análisis de registros en Kibana 3 (en desuso)](docs/monitor_log/kibana3/logging_view_kibana3.html#analyzing_logs_Kibana3). Para obtener más información sobre cómo personalizar un panel de control de Kibana 3, consulte [este artículo del blog ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/ "Icono de enlace externo"){: new_window}.
     

## ¿Por qué veo el símbolo ? en campos de la página Descubrir en Kibana?
{: #logging_qa_kibana_question}

Cuando abra la página Descubrir en Kibana, podría ver un signo de interrogación `?` en los campos que aparecen listados en la sección de campos disponibles en lugar del carácter `t`. Cuando vuelva a cargar la lista de campos, se analizará el tipo de los campos y el signo de interrogación `?` se sustituirá por el carácter `t`. Para obtener más información consulte [Cómo volver a cargar la lista de campos](/docs/services/CloudLogAnalysis/kibana/analize_logs_interactively.html#discover_view_reload_fields).


## Recibo un error 403 cuando intento cambiar el patrón de índice predeterminado
{: #error_403}

El patrón de índice predeterminado no se puede cambiar. 

Si intenta definir un patrón de índice diferente como nuevo predeterminado, recibirá el error siguiente: `Config: Error 403 Prohibido`


