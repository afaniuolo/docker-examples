# escape=`

ARG BASE_IMAGE
ARG SXA_IMAGE
ARG SPE_IMAGE
ARG SFE_IMAGE

FROM ${SPE_IMAGE} as spe
FROM ${SXA_IMAGE} as sxa
FROM ${SFE_IMAGE} as sfe
FROM ${BASE_IMAGE}

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# Add SPE module
COPY --from=spe \module\db \spe_data
RUN C:\DeployDatabases.ps1 -ResourcesDirectory C:\spe_data; `
    Remove-Item -Path C:\spe_data -Recurse -Force;

# Add SXA module
COPY --from=sxa \module\db \sxa_data
RUN C:\DeployDatabases.ps1 -ResourcesDirectory C:\sxa_data; `
    Remove-Item -Path C:\sxa_data -Recurse -Force;

# Add SFE module
COPY --from=sfe \module\db \sfe_data
RUN C:\DeployDatabases.ps1 -ResourcesDirectory C:\sfe_data; `
    Remove-Item -Path C:\sfe_data -Recurse -Force;