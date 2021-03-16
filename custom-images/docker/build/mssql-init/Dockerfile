# escape=`
ARG BASE_IMAGE
ARG MODULE_ASSETS

FROM ${MODULE_ASSETS} as module_assets

FROM $BASE_IMAGE as final

ARG MODULE_NAME

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

COPY --from=module_assets C:\module\db c:\resources\$MODULE_NAME

ENTRYPOINT .\DeployDatabases.ps1 -ResourcesDirectory c:\resources\$env:MODULE_NAME -SqlServer $env:SQL_SERVER -SqlAdminUser $env:SQL_ADMIN_LOGIN -SqlAdminPassword $env:SQL_ADMIN_PASSWORD -SkipStartingServer