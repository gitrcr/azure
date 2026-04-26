# Azure: crear cuenta de servicio
__Objetivo__: acceso, crear cuenta de servicio, datos de acceso para Aplicaciones.

__Ubicación cuentas de servicio__: _Entra ID/App registrations (All applications)_

## Acceso Azure
* Acceder a cuenta de Azure
* Abrir "Cloud Shell"

### Script configuración automática
Expone el bloque de código para terraform.tf

https://github.com/gitrcr/azure/blob/main/bin/sp_account.sh
```bash
wget https://raw.githubusercontent.com/gitrcr/terraform/refs/heads/main/scripts/new-az-sp.sh
chmod +x new-az-sp.sh
./new-az-sp.sh
```

### Procedimiento manual
Extracción de datos y creación del usuario del servicio.

```bash
az account show

# datos de la cuenta
{
  "environmentName": "AzureCloud",
  "homeTenantId": "5c989652-xxxxx",
  "id": "8d3e52c6-xxxx",
  "isDefault": true,
  "managedByTenants": [],
  "name": "Azure subscription 1",
  "state": "Enabled",
  "tenantId": "5c989652-",
  "user": {
    "cloudShellID": true,
    "name": "theboss@lala.onmicrosoft.com",
    "type": "user"
  }
}

# Crear usuario de servicio
# revisar --name y --role. Suscription="id"

az ad sp create-for-rbac --name "terraform-sp" --role="Contributor" --scopes="/subscriptions/8d3e52c6-xxxx
{
  "appId": "b9548ea1-xxxxx",
  "displayName": "terraform-sp",
  "password": "Dyq8Q~qxhE.xxxxxx",
  "tenant": "5c989652xxxxx"
}
```
Configurar terraform.tf

