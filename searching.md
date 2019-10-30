---

copyright:

  years: 2015, 2019
lastupdated: "2019-10-30"

keywords: search, find,

subcollection: resources, find resources

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}


# Searching for resources
{: #searching-for-resources}

You can search for provisioned resources that you expect to find in the resource list and offerings in the catalog from anywhere in the {{site.data.keyword.cloud}} console. Enter the resource or tag in the search field from the console menu bar. You can also use the {{site.data.keyword.Bluemix_notm}} command-line interface (CLI) to search across your resources. The CLI searches for distributed applications and service instances across locations and data centers.
{:shortdesc}

## Refining your search results
{: #results}

<dl>
<dt>View all resource results</dt>
<dd>Use this option to view a filtered resource list that automatically populates the name field within the resource list, giving you the most relevant results. The returned search displays the first 10 resource results. If you know that there are more results, you can see them all from the resource list. This option appears if it matches a resource result or tag search. If it doesn't match a resource result name or tag, it doesn't appear.</dd>
<dt>View all catalog results</dt>
<dd>Use this option to view a filtered catalog search. The first five results are displayed by name. If you want a more detailed search criteria for catalog entries, such as searching the description, you can click this link and get a filtered catalog results view. This option helps you find the offerings that you want to create faster. This appears if it matches to a catalog result. This field doesn't appear if your search query starts with `tag:`.</dd>
<dt>Search support cases</dt>
<dd>Use this option to filter by your open support cases across the platform, including infrastructure resources. This shows up at the end of the search if you search for anything, including if you search by `tag:`.</dd>
<dt>Search in IBM Cloud docs</dt>
<dd>Use this option to get a filtered search of the documentation. This shows up at the end of the search if you search for anything, including if you search by `tag:`.</dd>
</dl>

Press the Forward Slash key (/) to navigate your cursor to the search field.
{: tip}


## Searching with the CLI
{: #searching-cl}

You can also search across all your resources by using Lucene query syntax, with a single command by using the {{site.data.keyword.Bluemix_notm}} CLI, starting with version 0.6.7.


You can search for the following attributes:

<dl>
<dt>`name`</dt>
<dd> The user-defined name of the resource.</dd>
<dt>`region`</dt>
<dd>The geographical location where the resource is provisioned. The allowed values are `us-south`, `us-east`, `au-syd`, `eu-gb`, `eu-de`, and `jp-tok`.</dd>
<dt>`service_name`</dt>
<dd>The name of the service as it appears in the Name column of the output of `ibmcloud catalog service-marketplace`.</dd>
<dt>`family`</dt>
<dd>The cloud component to which your resource belongs. The allowed values are `cloud_foundry`, `containers`, `vmware`, `resource_controller` or `ims`.</dd></dd>
<dt>`organization_id`</dt>
<dd>The Cloud Foundry organization GUID.</dd>
<dt>`doc.space_id`</dt>
<dd>The Cloud Foundry space GUID.</dd>
<dt>`doc.resource_group_id`</dt>
<dd>The ID of the resource group.</dd>
<dt>`type`</dt>
<dd>The resource type. The allowed values are `k8-cluster`, `cf-service-instance`, `cf-user-provided-service-instance`, `cf-organization`, `cf-service-binding`, `cf-space`, `cf-application`, `resource-instance`, `resource-alias`, `resource-binding`, `resource-group`, `vmware-solutions`, `cloud-object-storage-infrastructure`, `block-storage`, `file-storage`, `cloud-backup` .</dd>
<dt>`creation_date`</dt>
<dd>The date on which the resource is created.</dd>
<dt>`modification_date`</dt>
<dd> The last modification date of the resource.</dd>
<dt>`tags`</dt>
<dd>The tags that have been attached to the resource </dd>
<dt>`tagReferences.tag.name`</dt>
<dd>The tags that have been attached to a classic infrastructure resource. Requires you to specify `-p classic-infrastructure` parameter. </dd>  
<dt>`_objectType:`</dt>
<dd>The object type of the classic infrastructure resource. Allowed values are: `SoftLayer_Virtual_DedicatedHost`, `SoftLayer_Hardware`, `SoftLayer_Network_Application_Delivery_Controller`, `SoftLayer_Network_Subnet_IpAddress`, `SoftLayer_Network_Vlan`, `SoftLayer_Network_Vlan_Firewall`, `SoftLayer_Virtual_Guest`. Requires you to specify `-p classic-infrastructure` parameter. </dd> 
</dl>

### Search examples
{: #resource-name}


The following examples can help you search for account resources.

* To search for all your resources named `ABC`, enter the following command:
    `ibmcloud resource search ‘name:ABC’`
  
* To search for all Cloud Foundry applications named `MyResource`, enter the following command:

    `ibmcloud resource search 'name:my* AND type:cf-application'`

* To search for all service instances of Message Hub, enter the following command:

    `ibmcloud resource search 'service_name:messagehub'`

* To search for all resources in either the `a07181ca-f917-4ee6-af22-b2c0c2a2d5d7` Cloud Foundry organization or the `c900d9671b235c00461c5e311a8aeced` resource group in the `us-south` region, enter the following command:
    `ibmcloud resource search (organization_id:a07181ca-f917-4ee6-af22-b2c0c2a2d5d7 OR doc.resource_group_id:c900d9671b235c00461c5e311a8aeced) AND 'region:us-south'`
    

* To search for resources that are not classic infrastructure that were created between 16 May 2018 and 20 May 2018, enter the following command:
    `ibmcloud resource search "creation_date:[2018-05-16T00:00:00Z TO 2018-05-20T00:00:00Z]"`
    
* To search for resources that are not classic infrastructure whose name starts with "my", ordered by type, enter the following command:

    `ibmcloud resource search 'name:my*' -s type`
    
* To search for resources that are not classic infrastructure and have been tagged with `MyTag`, , enter the following command:
    `ibmcloud resource search 'tags:MyTag'`
    
* To search for all classic infrastructure resources that have been tagged with `MyTag`, enter the following command:
    `ibmcloud resource search 'tagReferences.tag.name:MyTag' -p classic-infrastructure'`
    
* To search for all classic infrastructure of type `Softlayer_Hardware`
    `ibmcloud resource search '_objectType:SoftLayer_Hardware' -p classic-infrastructure'`
  

