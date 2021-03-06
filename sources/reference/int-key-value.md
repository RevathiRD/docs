main_section: Reference
sub_section: Integrations
page_title: Key-value integration

# Key-value pair integration

A key-value pair integration is a custom integration where you can give any key-value pairs.

##Adding your Key-Value Pair integration

-  Go to your **Account Settings** by clicking on the gear icon in the top navigation bar.

<img src="../../images/reference/integrations/account-settings.png" alt="Add key-values">

-  Click on **Integrations** in the left sidebar menu and then click on **Add integration**
-  Locate **Key-Value pair** in the list and click on **Create Integration**
-  Name your integration and enter your key-value pairs
-  Choose the Subscription which contains the repository for which you want to use this integration
-  Click **Save**

<img src="../../images/reference/integrations/key-value-integration.png" alt="Add Key-Value pair credentials">

##Using Key-Value pair integration in CI

To use key-value pair integration in CI builds, you need to add it in your `shippable.yml` under `generic` integrations section. You just need to provide the name of the integration.
```
# shippable.yml
integrations:
  generic:
    - integrationName: "key-value-integration"
```

When you run a build for this project, your key-value pairs will be available as environment variables.

<img src="../../images/reference/integrations/key-value-ci-jobConsoles.png" alt="ci jobConsoles">

##Using Key-Value pair integration in Pipelines

You can only use a key-value pair integration in your runSh and runCLI jobs.

* Create an integration resource with key-value pair integration.
```
# shippable.resources.yml
resources:
  - name: key-values
    type: integration
    integration: "key-value-integration"
```

* Add this resource as an `IN` to your `runSh`/`runCLI` job.
```
# shippable.jobs.yml
jobs:
  - name: runSh-job
    type: runSh
    steps:
      - IN: key-values
      - TASK:
        - script: echo $API_KEY
        - script: echo $API_URL
```

When you run a build for this job, your key-value pairs will be available as environment variables.

<img src="../../images/reference/integrations/key-value-pipelines-buildJobConsoles.png" alt="pipelines buildJobConsoles">

##Editing your Key-Value pair integration

You can go to your **Account Settings** at any time, click on **Integrations** in the left sidebar menu, and click the **Edit** button for your Key-Value pair integration. You can then change integration name,  update keys or values and add or delete key-value pairs.

However, you cannot edit the list of Subscriptions that are allowed to use the integration from this page. To add your integration to additional Subscriptions, read our Adding your integration to additional Subscriptions section

##Deleting your Key-Value pair integration

If you no longer need the integration, you can delete it by following the steps below. Please note that if any projects are using this integration in their `yml` files, builds will fail after deleting the integration:

-  Go to your **Account Settings** by clicking on the gear icon in the top navigation bar.

<img src="../../images/reference/integrations/account-settings.png" alt="Account settings">

-  Click on **Integrations** in the left sidebar menu.
- Locate the integration you want to delete and click on the **Delete** button.
- If there are no Subscriptions using this integration, you will be able to delete it by clicking on **Yes**. You are done at this point.

<img src="../../images/reference/integrations/confirm-delete-integration.png" alt="Delete integration confirmation screen">

- If your integration is being used by any Subscriptions, you will see a message telling you which Subscriptions are still using the integration.

<img src="../../images/reference/integrations/cannot-delete-integration.png" alt="Cannot delete integration because of dependencies">

- Go to each Subscription listed in the dependencies and delete it from each.
    - From the Subsciption dropdown menu at the top left of your Dashboard, click on the dependent Subscription.

    <img src="../../images/reference/integrations/list-subscriptions.png" alt="List subscriptions">

    - Go to the **Settings** tab and click on **Integrations** in the left sidebar.
    - Delete the integration.
- Once you have delete the integration from all Subscriptions, you can go back to **Account Settings** and delete the integration.
