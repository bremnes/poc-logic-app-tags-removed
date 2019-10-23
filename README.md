# Logic App tags removed after ARM deployment

By definition ARM templates are declarative, and they should add or reconfigure settings when deployed in `incremental` mode.

However, when deploying logic apps through ARM template the `tags` are deleted from the logic app resource even though they are not defined in the logic app. Expected behaviour would be that they stay as before.

For other resources, such as storage accounts, they keeps the previous value if not defined/overridden in the ARM template.

## Steps to reproduce bug/odd behaviour

1. Deploy the provided ARM template into a resource group. This will create two new resources:
    * An empty logic app
    * A storage account
2. Assign Azure tags to both resources in the portal or through script (_don't change the ARM template_).
3. Redeploy the provided ARM template.
4. Inspect the tags on the resources, notice that the storage account has kept its previously set tags, but the logic app now has zero tags.