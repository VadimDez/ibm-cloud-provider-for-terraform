---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-19"

keywords: terraform provider plugin, terraform api gateway

subcollection: ibm-cloud-provider-for-terraform

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}



# API Gateway data sources
{: #api-gw-data-sources}

Review the data sources that you can use to retrieve information about your API Gateway resources. All data sources are imported as read-only information. You can reference the output parameters for each data source by using Terraform on {{site.data.keyword.cloud_notm}} interpolation syntax.

Before you start working with your data source, make sure to review the [required parameters](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#required-parameters) that you need to specify in the `provider` block of your Terraform on {{site.data.keyword.cloud_notm}} configuration file. 
{: important}

## `ibm_api_gateway`
{: #api-gw}

Retrieve information about an existing API Gateway instance. 
{: shortdesc}

### Sample Terraform on {{site.data.keyword.cloud_notm}} code
{: #api-gw-sample}

```
data "ibm_api_gateway" "apigateway" {
    service_instance_crn = ibm_resource_instance.apigateway.id
    
}
```
{: codeblock}

### Input parameters
{: #api-gw-input}

Review the input parameters that you can specify for your resource. 
{: shortdesc}

| Input parameter | Data type | Required / optional | Description |
| ------------- |-------------| ----- | -------------- |
|`service_instance_crn`|String|Required|The CRN of the API Gateway service instance. |


### Output parameters
{: #api-gw-output}

Review the output parameters that you can access after your resource is created. 
{: shortdesc}

| Output parameter | Data type | Description |
| ------------- |-------------| -------------- |
|`endpoints`|List of API Gateway endpoints|A list of API Gateway endpoints that are associated with the service instance.|
|`endpoints.endpoint_id`|String|The ID of the endpoint.|
|`endpoints.name`|String|The name of the endpoint.|
|`endpoints.managed`|Boolean|If set to **true**, the endpoint is online. If set to **false**, the endpoint is offline.|
|`endpoints.shared`|String|The shared status of the endpoint.|
|`endpoints.base_path`|String|The base path of the endpoint.|
|`endpoints.routes`|Array of string|A list of routes that can be invoked for the endpoint.|
|`endpoints.provider_id`|String|The provider ID of the endpoint.|
|`endpoints.managed_url`|String|The managed URL of an endpoint.|
|`endpoints.alias_url`|String|The alias URL of an endpoint.|
|`endpoints.open_api_doc`|String|The Open API document of the endpoint.|
|`endpoints.subscriptions`|List of endpoint subscriptions|A list of subscriptions that you created for your endpoint.|
|`endpoints.subscriptions.client_id`|String|The client ID of a subscription.|
|`endpoints.subscriptions.name`|String|The name of the subscription.|
|`endpoints.subscriptions.type`|String|The type of subscription. Supported values are `bluemix` and `external`.|
|`endpoints.subscriptions.secret_provided`|Boolean|If set to **true**, the client secret is provided. If set to **false**, the client secret is not provided.|
