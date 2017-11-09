{{{
  "title": "Download Anywhere Server Installer",
  "date": "11-07-2017",
  "author": "Anil Palepu",
  "attachments": [],
  "sticky": "false"
}}}

Downloads a Simple Backup Anywhere Server agent installer. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to download the SBS Anywhere Server installation package 

## URL

### Structure

    POST https://api.backup.ctl.io/clc-backup-api/api/createInstallerScript

### Example

    POST https://api.backup.ctl.io/clc-backup-api/api/createInstallerScript

## Request

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| provisioningToken | string | The provisioning token is given when a server is registered as Anywhere Server  | Yes |

### Examples

#### JSON

    {
      "provisioningToken": "PROVISIONbdb54aa4-a4fc-43a3-b452-3b4afda66096"
    }

    
## Response

## Headers

| Name | Type | Description |
| --- | --- | --- | --- |
| x-filename | string | This is the script name |
| Content-Type | string | The script is returned in text/plain;charset=UTF-8 format| 

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| data | text/plain | This is the agent installation script returned for specific provisioning token sent in the request |

### Examples


#### plain/text
```
# ==========================================================================================================
# sbs-windows-install-BAAD-DELETEMESERVER-67.ps1    Version 2.0   Created Date: 1510169782942
# ==========================================================================================================

#
# If this script is not able to execute, please run Powershell 3.0 or later as ADMINISTRATOR
#
# Check you ExecutionPolicy in Powershell.
# Example: Get-ExecutionPolicy -list
#
# You may need to allow an UnRestricted ExecutionPolicy while installing SBS
# Example: echo . | powershell Set-ExecutionPolicy UnRestricted -FORCE
#
# After installing SBS you can return the ExecutionPolicy to the former value.
# Example: echo . | powershell Set-ExecutionPolicy UnDefined -FORCE
#
# Please use an internet search of "echo . | powershell Set-ExecutionPolicy UnRestricted -FORCE"
# for additional information.
#

#Setting up a log mechanism that displays and logs
Function Log-Message([string]$stringData)
{
   Write-Output $stringData
}

function IsNullOrEmpty($str) {if ($str) {$False} else {$True}}

#####################################################
# FakeCurl - used to download a file like *nix curl #
#####################################################
function FakeCurl {
	param ( $url, $file )

	Write-Output "Downloading $file from $url"
	$storageDir = $pwd
	$webclient = New-Object System.Net.WebClient
	$filepathname = "$storageDir\$file"
	$webclient.DownloadFile($url, $filepathname)
	Write-Output "Downloaded to $filepathname"
	$global:RETURN=$filepathname
}

################
# MAIN PROGRAM #
################
Function Main()
{
	Set-PSDebug -Strict
	Set-PSDebug -Trace 0

	$DATETIME=Get-Date -Format g
	Log-Message "sbs-windows-install-BAAD-DELETEMESERVER-67.ps1     Version 2.0"
	Log-Message "Script Created by anil.baad on 1510169782942"
	Log-Message "Execution Time: $DATETIME"

#
# Set variables
#
	$USERNAME="anil.baad"
	$ACCOUNTALIAS="BAAD"
	$HOSTNAME="DELETEMESERVER-67"
	$SBS_PROVISIONING_TOKEN="PROVISIONbdb54aa4-a4fc-43a3-b452-3b4afda66096"

#
# Display powershell version -- 3+ required
#	
	$PSVersionTable
	if ($PSVersionTable.PSVersion.Major -lt 3)
	{
		Log-Message "This script requires Powershell Version 3.0+"
		exit 0
	}

#
# Setup TLS1.2 for all HTTPS traffic
#
	Log-Message "Setup TLS1.2 for all HTTPS traffic in script..."
	[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12

#	
# Setup proxy for windows
#
	Log-Message "Use netsh to setup proxy using IE as the source..."
	netsh winhttp import proxy source=ie 

#
# Download the sbs-windows-install.ps1 file
#		
	$SBS_INSTALL_SCRIPT = "sbs-windows-install.ps1"
	$SBS_INSTALL_URL = "https://s3.amazonaws.com/sbs-agent/$SBS_INSTALL_SCRIPT"
	$SBS_INSTALL_FILE = "$SBS_INSTALL_SCRIPT"
	FakeCurl -url $SBS_INSTALL_URL -file $SBS_INSTALL_FILE	
	$file = $RETURN
	Log-Message "Check download file $file..."
	
	If ( -not ( Test-Path -path "$file" ) )
	{
		Log-Message "$SBS_INSTALL_SCRIPT FAILED to download and was not used to install SBS"
		exit 0
	}

#
# Requires hard-coded script name
#
	Log-Message ".\sbs-windows-install.ps1 -accountalias $ACCOUNTALIAS -hostname $HOSTNAME -sbs_provisioning_token $SBS_PROVISIONING_TOKEN -DEVQAPROD DEV"
	.\sbs-windows-install.ps1 -accountalias $ACCOUNTALIAS -hostname $HOSTNAME -sbs_provisioning_token $SBS_PROVISIONING_TOKEN -DEVQAPROD DEV

}

Main

Exit 0
```