## Install Docker on Windows

## Build Windows Docker Container
Create work directory with PowerShell
```powershell
mkdir C:\dockeragent
cd C:\dockeragent
```

Create file `Dockerfile` with no extension
```yaml
FROM mcr.microsoft.com/windows/servercore:ltsc2019

WORKDIR /azp

SHELL ["powershell"]

# Install Visual Studio
RUN Invoke-WebRequest "https://aka.ms/vs/16/release/vs_community.exe" -OutFile "$Env:TEMP\vs_community.exe" -UseBasicParsing; \
    & "$Env:TEMP\vs_community.exe" --add Microsoft.VisualStudio.Workload.Azure --quiet --wait --norestart --noUpdateInstaller | Out-Default; \
    & 'C:/Program Files (x86)/Microsoft Visual Studio/2019/Community/MSBuild/Current/Bin/MSBuild.exe' /version

# Install Git
RUN Invoke-WebRequest 'https://github.com/git-for-windows/git/releases/download/v2.12.2.windows.2/MinGit-2.12.2.2-64-bit.zip' -OutFile "$Env:TEMP\MinGit.zip"; \
    Expand-Archive "$Env:TEMP\MinGit.zip" -DestinationPath C:\MinGit; \
    $Env:PATH = $Env:PATH + ';C:\MinGit\cmd\;C:\MinGit\cmd'; \
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Environment\' -Name Path -Value $Env:PATH

# Copy agent package into image
COPY agent.zip .

# Copy startup script into image
COPY start.ps1 .

CMD powershell .\start.ps1
```

Create PowerShell script `start.ps1`  
You can use this powershell command to create the script first then edit the file with a text editor
```powershell
echo '' > start.ps1
```
```powershell
if (-not (Test-Path Env:AZP_AUTH_TYPE)) {
  # Default authentication type set to 'Integrated'
  $Env:AZP_AUTH_TYPE = "Integrated"
}
if (-not ($Env:AZP_AUTH_TYPE -eq 'PAT' -or $Env:AZP_AUTH_TYPE -eq 'Integrated')) {
  Write-Error "error: AZP_AUTH_TYPE environment variable should be either 'PAT' or 'Integrated'"
  exit 1
}
Write-Host "The agent authentication type is `"$Env:AZP_AUTH_TYPE`""

if (-not (Test-Path Env:AZP_RUN_ONCE)) {
  # Default authentication type set to 'no'
  $Env:AZP_RUN_ONCE = "no"
}
if (-not ($Env:AZP_RUN_ONCE -eq 'yes' -or $Env:AZP_RUN_ONCE -eq 'no')) {
  Write-Error "error: AZP_RUN_ONCE environment variable should be either 'yes' or 'no'"
  exit 1
}
Write-Host "The agent run-once option is set to `"$Env:AZP_RUN_ONCE`""

if (-not (Test-Path Env:AZP_URL)) {
  Write-Error "error: missing AZP_URL environment variable"
  exit 1
}

if ($Env:AZP_AUTH_TYPE -eq 'PAT') {
  if (-not (Test-Path Env:AZP_TOKEN_FILE)) {
    if (-not (Test-Path Env:AZP_TOKEN)) {
      Write-Error "error: missing AZP_TOKEN environment variable"
      exit 1
    }

    $Env:AZP_TOKEN_FILE = "\azp\.token"
    $Env:AZP_TOKEN | Out-File -FilePath $Env:AZP_TOKEN_FILE
  }
}

if (Test-Path Env:AZP_TOKEN) {
  Remove-Item Env:AZP_TOKEN
}

if ($Env:AZP_WORK -and -not (Test-Path Env:AZP_WORK)) {
  New-Item $Env:AZP_WORK -ItemType directory | Out-Null
}

New-Item "\azp\agent" -ItemType directory | Out-Null

# Let the agent ignore the token env variables
$Env:VSO_AGENT_IGNORE = "AZP_TOKEN,AZP_TOKEN_FILE"

Set-Location agent

Write-Host "2. Installing Azure Pipelines agent..." -ForegroundColor Cyan

Expand-Archive -Path "\azp\agent.zip" -DestinationPath "\azp\agent"

Write-Host "3. Configuring Azure Pipelines agent..." -ForegroundColor Cyan
if ($Env:AZP_AUTH_TYPE -eq 'Integrated') {
  try
  {
    .\config.cmd --unattended `
      --agent "$(if (Test-Path Env:AZP_AGENT_NAME) { ${Env:AZP_AGENT_NAME} } else { ${Env:computername} })" `
      --url "$(${Env:AZP_URL})" `
      --auth $Env:AZP_AUTH_TYPE `
      --pool "$(if (Test-Path Env:AZP_POOL) { ${Env:AZP_POOL} } else { 'Default' })" `
      --work "$(if (Test-Path Env:AZP_WORK) { ${Env:AZP_WORK} } else { '_work' })" `
      --replace
    
    Write-Host "4. Running Azure Pipelines agent..." -ForegroundColor Cyan
    
    if ($Env:AZP_RUN_ONCE -eq 'yes') {
      .\run.cmd --once
    } else {
      .\run.cmd
    }
    
  }
  finally
  {
    Write-Host "Cleanup. Removing Azure Pipelines agent..." -ForegroundColor Cyan

    .\config.cmd remove --unattended `
      --auth $Env:AZP_AUTH_TYPE
  }
} elseif ($Env:AZP_AUTH_TYPE -eq 'PAT') {
  try
  {

    .\config.cmd --unattended `
      --agent "$(if (Test-Path Env:AZP_AGENT_NAME) { ${Env:AZP_AGENT_NAME} } else { ${Env:computername} })" `
      --url "$(${Env:AZP_URL})" `
      --auth $Env:AZP_AUTH_TYPE `
      --token "$(Get-Content ${Env:AZP_TOKEN_FILE})" `
      --pool "$(if (Test-Path Env:AZP_POOL) { ${Env:AZP_POOL} } else { 'Default' })" `
      --work "$(if (Test-Path Env:AZP_WORK) { ${Env:AZP_WORK} } else { '_work' })" `
      --replace

    # remove the administrative token before accepting work
    Remove-Item $Env:AZP_TOKEN_FILE
  
    Write-Host "4. Running Azure Pipelines agent..." -ForegroundColor Cyan

    if ($Env:AZP_RUN_ONCE -eq 'yes') {
      .\run.cmd --once
    } else {
      .\run.cmd
    }
    
  }
  finally
  {
    Write-Host "Cleanup. Removing Azure Pipelines agent..." -ForegroundColor Cyan

    .\config.cmd remove --unattended `
      --auth $Env:AZP_AUTH_TYPE `
      --token "$(Get-Content ${Env:AZP_TOKEN_FILE})"
  }
  
} else {
  Write-Error "error2: AZP_AUTH_TYPE environment variable should be either 'PAT' or 'Integrated'"
  exit 1
}
```

Build the image
```powershell
docker build --rm -t windows-agent:latest .
```

## Run the container
If you want to run your container with `PAT` authentication
```powershell
docker run -e AZP_AUTH_TYPE=PAT -e AZP_RUN_ONCE=no -e AZP_POOL=Default -e AZP_URL=<Azure DevOps instance> -e AZP_TOKEN=<PAT token> -e AZP_AGENT_NAME=windows-container-agent1 windows-agent:latest
```

If you want to run your container with `Integrated` authentication
```powershell
docker run -e AZP_AUTH_TYPE=Integrated -e AZP_RUN_ONCE=no -e AZP_POOL=Default -e AZP_URL=<Azure DevOps instance> -e AZP_AGENT_NAME=windows-container-agent1 windows-agent:latest
```
