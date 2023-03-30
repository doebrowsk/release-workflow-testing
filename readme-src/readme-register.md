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