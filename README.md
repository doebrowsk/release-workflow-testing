# MY PAM Provider

The  PAM Provider allows for the use of secrets as passwords.

#### Integration status: Production - Ready for use in production environments.

## About the Keyfactor PAM Provider

Keyfactor supports the retrieval of credentials from 3rd party Privileged Access Management (PAM) solutions. Secret values can normally be stored, encrypted at rest, in the Keyfactor Platform database. A PAM Provider can allow these secrets to be stored, managed, and rotated in an external platform. This integration is usually configured on the Keyfactor Platform itself, where the platform can request the credential values when needed. In certain scenarios, a PAM Provider can instead be run on a remote location in conjunction with a Keyfactor Orchestrator to allow credential requests to originate from a location other than the Keyfactor Platform.



## Support for MY PAM Provider

MY PAM Provider is supported by Keyfactor for Keyfactor customers. If you have a support issue, please open a support ticket with your Keyfactor representative.

###### To report a problem or suggest a new feature, use the **[Issues](../../issues)** tab. If you want to contribute actual bug fixes or proposed enhancements, use the **[Pull requests](../../pulls)** tab.
___



---






### Initial Configuration of PAM Provider
In order to allow Keyfactor to use the new MY PAM Provider, the definition needs to be added to the application database.
This is done by running the provided [add_PAMProvider.sql](./add_PAMProvider.sql) script on the Keyfactor application database, which only needs to be done one time.

If you have a hosted environment or need assistance completing this step, please contact Keyfactor Support.

### Configuring Parameters
The following are the parameter names and a description of the values needed to configure the MY PAM Provider.

__Initialization Parameters for each defined PAM Provider instance__
| Initialization parameter | Display Name | Description |
| :---: | :---: | --- |
| projectId | Unique Project ID | The unique auto generated ID of your project. This is not the name you may have renamed / assigned to your project after it was created. |

__Instance Parameters for each retrieved secret field__
| Instance parameter | Display Name | Description |
| :---: | :---: | --- |
| secretId | Secret Name | The name of the secret you assigned in the Secret Manager. |
![](images/config.png)

### Configuring for PAM Usage
#### IN your PAM PROVIDER

Lorem Ipsum 

#### In Keyfactor - PAM Provider
##### Installation
In order to setup a new PAM Provider in the Keyfactor Platform for the first time, you will need to run [the SQL Installation Script](./add_PAMProvider.sql) against your Keyfactor application database.

After the installation is run, the DLLs need to be installed to the correct location for the PAM Provider to function. From the release, the MY-PAM.dll.dll should be copied to the following folder locations in the Keyfactor installation. Once the DLL has been copied to these folders, edit the corresponding config file. You will need to add a new Unity entry as follows under `<container>`, next to other `<register>` tags.

| Install Location | DLL Binary Folder | Config File |
| --- | --- | --- |
| WebAgentServices | WebAgentServices\bin\ | WebAgentServices\web.config |
| Service | Service\ | Service\CMSTimerService.exe.config |
| KeyfactorAPI | KeyfactorAPI\bin\ | KeyfactorAPI\web.config |
| WebConsole | WebConsole\bin\ | WebConsole\web.config |

When enabling a PAM provider for Orchestrators only, the first line for `WebAgentServices` is the only installation needed.

The Keyfactor service and IIS Server should be restarted after making these changes.

```xml
<register type="IPAMProvider" mapTo="Keyfactor.Extensions.Pam.MY.PAM, MY-PAM.dll" name="MY-PAM" />
```


```json
{
  "extensions": {
    "Keyfactor.Platform.Extensions.IPAMProvider": {
      "PAMProviders.MYPAM.PAMProvider": {
        "assemblyPath": "my-pam.dll",
        "TypeFullName": "Keyfactor.Extensions.Pam.My.PAM"
      }
    }
  },
  "Keyfactor:PAMProviders:MYPAM:InitializationInfo": {
    "Host": "localhost",
    "Token": "xxxxxx"
  }
}
```

##### Usage
In order to use the PAM Provider, the provider's configuration must be set in the Keyfactor Platform. In the settings menu (upper right cog) you can select the ___Priviledged Access Management___ option to configure your provider instance.

![](images/setting.png)

After it is set up, you can now use your PAM Provider when configuring certificate stores. Any field that is treated as a Keyfactor secret, such as server passwords and certificate store passwords can be retrieved from your PAM Provider instead of being entered in directly as a secret.

![](images/password.png)

---


# release-workflow-testing
A test repository for changes to GitHub actions for release workflows.

