FROM apprenticeshipsdevops/azure-pipelines-base-agent-win:latest

ENV chocolateyUseWindowsCompression=false
RUN @powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"

RUN choco config set cachelocation C:\chococache \
  && choco feature disable -name showDownloadProgress

RUN choco install \
  git  \
  powershell-core \
  dacfx-18 \
  --confirm \
  --limit-output \
  --timeout 216000 \
  && rmdir /S /Q C:\chococache

RUN  @powershell -NoProfile -Command "Install-PackageProvider -Name NuGet -Force"
RUN  @powershell -NoProfile -Command "Install-Module AzureRm -Force"
RUN  @powershell -NoProfile -Command "Install-Module Azure -AllowClobber -Force"
RUN  @powershell -NoProfile -Command "Install-Module Az -AllowClobber -Force"

RUN  @pwsh -NoProfile -Command "Install-Module Az -Force"

RUN  @powershell -NoProfile -Command "Install-Module SqlServer, AzTable, Az.CosmosDb -Force"

#Cleanup
RUN  @powershell -NoProfile -Command "Uninstall-Module -Name AzureRM.profile -RequiredVersion 5.8.3"
