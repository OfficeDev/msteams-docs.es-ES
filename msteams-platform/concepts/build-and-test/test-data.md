---
title: Agregar datos de prueba a su inquilino de prueba de Office 365
description: Configurar la suscripción del programa de desarrolladores de Office 365 para probar correctamente las aplicaciones de Microsoft Teams
keywords: probar los equipos del programa para desarrolladores de aplicaciones
ms.date: 11/01/2019
ms.openlocfilehash: 87e9dc280c192f013098c3e9f604f72238bfafdf
ms.sourcegitcommit: fdc50183f3f4bec9e4b83bcfe5e016b591402f7c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/24/2020
ms.locfileid: "44867105"
---
# <a name="add-test-data-to-your-office-365-test-tenant"></a><span data-ttu-id="32177-104">Agregar datos de prueba a su inquilino de prueba de Office 365</span><span class="sxs-lookup"><span data-stu-id="32177-104">Add test data to your Office 365 test tenant</span></span>

<span data-ttu-id="32177-105">Configure la suscripción del programa de desarrolladores de O365 (u otro inquilino de prueba) para que sea más fácil probar las aplicaciones que ha creado.</span><span class="sxs-lookup"><span data-stu-id="32177-105">Set up your O365 developer program subscription (or other test tenant) to make it easy for you to test the apps that you've built.</span></span>  <span data-ttu-id="32177-106">Le ayudará a:</span><span class="sxs-lookup"><span data-stu-id="32177-106">It will help you:</span></span>

- <span data-ttu-id="32177-107">Crear nuevos equipos y canales en su organización</span><span class="sxs-lookup"><span data-stu-id="32177-107">Create new teams and channels in your organization</span></span>

- <span data-ttu-id="32177-108">Agregue los usuarios que se crean mediante el paquete de contenido de usuario a esos equipos.</span><span class="sxs-lookup"><span data-stu-id="32177-108">Add the users that are created via the User content pack to those teams.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="32177-109">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="32177-109">Before you start</span></span>

<span data-ttu-id="32177-110">Si aún no tiene un inquilino de prueba, deberá unirse al programa de desarrolladores de Office 365 y registrarse para obtener una suscripción de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="32177-110">If you don't already have a test tenant, you will need to join the Office 365 developer program and sign up for a developer subscription.</span></span> <span data-ttu-id="32177-111">También tendrá que instalar los módulos de PowerShell necesarios.</span><span class="sxs-lookup"><span data-stu-id="32177-111">You'll also need to install the necessary PowerShell modules.</span></span> <span data-ttu-id="32177-112">Para cualquier inquilino que use, necesitará tener permisos de administrador global para ejecutar los scripts.</span><span class="sxs-lookup"><span data-stu-id="32177-112">For whatever tenant you use you'll need to have global administrator permissions to run the scripts.</span></span>

1. [<span data-ttu-id="32177-113">Unirse al programa de desarrolladores de Office 365</span><span class="sxs-lookup"><span data-stu-id="32177-113">Join the Office 365 Developer Program</span></span>](/office/developer-program/office-365-developer-program)
2. [<span data-ttu-id="32177-114">Configurar una suscripción de desarrollador de Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="32177-114">Set up a Microsoft 365 Developer Subscription</span></span>](/office/developer-program/office-365-developer-program-get-started)
3. [<span data-ttu-id="32177-115">Usar paquetes de datos de ejemplo con su suscripción de desarrollador de Office 365 para instalar el paquete de contenido de usuarios</span><span class="sxs-lookup"><span data-stu-id="32177-115">Use sample data packs with your Office 365 developer subscription to install the Users content pack</span></span>](/office/developer-program/install-sample-packs)
4. [<span data-ttu-id="32177-116">Instalar el módulo de PowerShell de Teams</span><span class="sxs-lookup"><span data-stu-id="32177-116">Install the Teams PowerShell module</span></span>](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2)
5. [<span data-ttu-id="32177-117">Instalar el módulo de PowerShell de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32177-117">Install the Azure AD PowerShell module</span></span>](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module)

### <a name="optional-step-allow-upload-of-custom-apps"></a><span data-ttu-id="32177-118">Paso opcional: permitir la carga de aplicaciones personalizadas</span><span class="sxs-lookup"><span data-stu-id="32177-118">Optional step: allow upload of custom apps</span></span>

<span data-ttu-id="32177-119">De forma predeterminada, solo los administradores globales o los administradores de servicios de Teams pueden cargar aplicaciones personalizadas en el catálogo de aplicaciones del espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="32177-119">By default, only global admins or teams service admins can upload custom apps into the tenant app catalog.</span></span>  <span data-ttu-id="32177-120">También puede habilitar a todos los usuarios para que carguen aplicaciones personalizadas para su propio uso o para los equipos para pruebas.</span><span class="sxs-lookup"><span data-stu-id="32177-120">You can also enable all users to upload custom apps for their own use or to teams for testing.</span></span>

<span data-ttu-id="32177-121">Para habilitar esta opción, deberá actualizar la Directiva de configuración global de la aplicación en el portal de administración de Teams.</span><span class="sxs-lookup"><span data-stu-id="32177-121">To enable this setting, you'll need to update the global App Setup Policy in your Teams Admin Portal.</span></span>

<img width="430px" src="~/assets/images/microsoft-teams-admin-center-screenshot.png" title="Captura de pantalla de la Directiva de configuración de aplicaciones" />

<span data-ttu-id="32177-123">Para obtener más información, vea:</span><span class="sxs-lookup"><span data-stu-id="32177-123">For more information see:</span></span>

 - [<span data-ttu-id="32177-124">Administrar directivas de configuración de aplicaciones en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="32177-124">Manage app setup policies in Microsoft Teams</span></span>](/microsoftteams/teams-app-setup-policies)

## <a name="create-teams-and-channels"></a><span data-ttu-id="32177-125">Crear equipos y canales</span><span class="sxs-lookup"><span data-stu-id="32177-125">Create teams and channels</span></span>

<span data-ttu-id="32177-126">Guarde el siguiente fragmento de código como XML (. xml) y tenga en cuenta dónde lo ha guardado.</span><span class="sxs-lookup"><span data-stu-id="32177-126">Save the following snippet as an XML (.xml) and note where you've saved it.</span></span>  <span data-ttu-id="32177-127">Este XML define la estructura de los equipos y canales que se crearán junto con sus miembros.</span><span class="sxs-lookup"><span data-stu-id="32177-127">This XML defines the structure of the teams and channels that will be created - along with its members.</span></span>

```xml
<?xml version="1.0"?>
<Teams>
  <Team Name="Store Portal" ID="storeportal" Description="" Type="Private" Creator="admin">
    <Members>
      <Member UserName="AlexW" IsOwner="false"/>
      <Member UserName="PattiF" IsOwner="false"/>
      <Member UserName="PradeepG" IsOwner="false"/>
      <Member UserName="JoniS" IsOwner="false"/>
      <Member UserName="JohannaL" IsOwner="false"/>
      <Member UserName="NestorW" IsOwner="false"/>
      <Member UserName="IsaiahL" IsOwner="false"/>
      <Member UserName="AdeleV" IsOwner="false"/>
      <Member UserName="LeeG" IsOwner="false"/>
      <Member UserName="MeganB" IsOwner="true"/>
      <Member UserName="LynneR" IsOwner="false"/>
      <Member UserName="GradyA" IsOwner="false"/>
      <Member UserName="LidiaH" IsOwner="false"/>
      <Member UserName="DiegoS" IsOwner="false"/>
      <Member UserName="MiriamG" IsOwner="true"/>
    </Members>
    <Channels>
      <Channel Name="Sales" ID="sales" Description="" Creator="Admin" />
      <Channel Name="Inventory" ID="inventory" Description="" Creator="Admin" />
      <Channel Name="Los Angeles Store 239" ID="losangelesstore239" Description="" Creator="Admin" />
      <Channel Name="Seattle Store 121" ID="seattlestore121" Description="" Creator="Admin" />
      <Channel Name="Online" ID="online" Description="" Creator="Admin" />
      <Channel Name="Store Layout" ID="storelayout" Description="" Creator="Admin" />
      <Channel Name="Promotions" ID="promotions" Description="" Creator="Admin" />
    </Channels>
  </Team>
  <Team Name="Mark 8 Project Team" ID="Mark8ProjectTeam" Description="Welcome to the team that we've assembled to create the Mark 8." Type="Private" Creator="admin">
    <Members>
      <Member UserName="meganb" IsOwner="true" />
      <Member UserName="alexw" IsOwner="false" />
      <Member UserName="lynner" IsOwner="false" />
      <Member UserName="isaiahl" IsOwner="false" />
      <Member UserName="leeg" IsOwner="false" />
      <Member UserName="pradeepg" IsOwner="false" />
      <Member UserName="lidiah" IsOwner="false" />
      <Member UserName="diegos" IsOwner="false" />
      <Member UserName="johannal" IsOwner="false" />
      <Member UserName="miriamg" IsOwner="false" />
      <Member UserName="adelev" IsOwner="false" />
      <Member UserName="jonis" IsOwner="false" />
      <Member UserName="nestorw" IsOwner="false" />
      <Member UserName="gradya" IsOwner="false" />
      <Member UserName="pattif" IsOwner="false" />
    </Members>
    <Channels>
      <Channel Name="Research and Development" ID="researchanddevelopment" Description="Channel for Research and Development!" Creator="meganb" />
      <Channel Name="Design" ID="design" Description="Discuss design projects." Creator="meganb" />
      <Channel Name="Digital Assets Web" ID="digitalassetsweb" Description="Discuss digital assets." Creator="meganb" />
      <Channel Name="Go to Market Plan" ID="gotomarketplan" Description="Our go-to-market plan!" Creator="meganb" />
    </Channels>
  </Team>
  <Team Name="District 9 Road Safety Audit" ID="district9roadsafetyaudit" Description="" Type="Private" Creator="admin">
    <Members>
      <Member UserName="meganb" IsOwner="true" />
      <Member UserName="alexw" IsOwner="false" />
      <Member UserName="lynner" IsOwner="false" />
      <Member UserName="isaiahl" IsOwner="false" />
      <Member UserName="leeg" IsOwner="false" />
      <Member UserName="pradeepg" IsOwner="false" />
      <Member UserName="lidiah" IsOwner="false" />
      <Member UserName="diegos" IsOwner="false" />
      <Member UserName="johannal" IsOwner="false" />
      <Member UserName="miriamg" IsOwner="false" />
      <Member UserName="adelev" IsOwner="false" />
      <Member UserName="jonis" IsOwner="false" />
      <Member UserName="nestorw" IsOwner="false" />
      <Member UserName="gradya" IsOwner="false" />
      <Member UserName="pattif" IsOwner="false" />
    </Members>
    <Channels>
      <Channel Name="Audit Planning" ID="auditplanning" Description="" Creator="Admin" />
      <Channel Name="Delivery" ID="delivery" Description="" Creator="Admin" />
      <Channel Name="Findings" ID="findings" Description="" Creator="Admin" />
      <Channel Name="Recommended Actions" ID="recommendedactions" Description="" Creator="Admin" />
      <Channel Name="Survey" ID="survey" Description="" Creator="Admin" />
    </Channels>
  </Team>
  <Team Name="ACC-1000 Product Team" ID="acc1000productteam" Description="" Type="Private" Creator="admin" >
    <Members>
      <Member UserName="meganb" IsOwner="true" />
      <Member UserName="alexw" IsOwner="false" />
      <Member UserName="lynner" IsOwner="false" />
      <Member UserName="isaiahl" IsOwner="false" />
      <Member UserName="leeg" IsOwner="false" />
      <Member UserName="pradeepg" IsOwner="false" />
      <Member UserName="lidiah" IsOwner="false" />
      <Member UserName="diegos" IsOwner="false" />
      <Member UserName="johannal" IsOwner="false" />
      <Member UserName="miriamg" IsOwner="false" />
      <Member UserName="adelev" IsOwner="false" />
      <Member UserName="jonis" IsOwner="false" />
      <Member UserName="nestorw" IsOwner="false" />
      <Member UserName="gradya" IsOwner="false" />
      <Member UserName="pattif" IsOwner="false" />
    </Members>
    <Channels>
      <Channel Name="Corporate Communication" ID="corporatecommunication" Description="" Creator="Admin" />
      <Channel Name="Lean Process Improvement" ID="corporatecommunication" Description="" Creator="Admin" />
      <Channel Name="Training and Certification" ID="trainingandcertification" Description="" Creator="Admin" />
      <Channel Name="Production" ID="production" Description="" Creator="Admin" />
      <Channel Name="Research and Development" ID="researchanddevelopment" Description="" Creator="Admin" />
      <Channel Name="Supplier Collaboration" ID="suppliercollaboration" Description="" Creator="Admin" />
    </Channels>
  </Team>
</Teams>
```

<span data-ttu-id="32177-128">Guarde el siguiente fragmento de código como un script de PowerShell (. PS1) y anote dónde lo ha guardado.</span><span class="sxs-lookup"><span data-stu-id="32177-128">Save the following snippet as a PowerShell script (.ps1) and note where you've saved it.</span></span>  <span data-ttu-id="32177-129">Este script ejecuta los pasos para crear los equipos y canales y agregar miembros a ellos.</span><span class="sxs-lookup"><span data-stu-id="32177-129">This script executes the steps to create the teams and channels and add members to them.</span></span>

```powershell
Param(
    [Parameter(Mandatory = $true)]
    
    # This specifies the location of your configuration XML.
    
    [string] $teamsFilePath 
)
    
[xml]$XmlDocument = Get-Content -Path $teamsFilePath.ToString()

if ($XmlDocument.Teams.Team.Count -gt 0) {

    try {
        
        # 1. Login with the global administrator account for your O365 Developer Program tenant.  This script will then use these credentials to connect to the powershell modules for Azure Active Directory and Microsoft Teams
        
        $creds = Get-Credential

        # Connecting to AAD PowerShell
        Connect-AzureAD -Credential $creds | Out-Null

        # Connect to Microsoft Teams PowerShell
        Connect-MicrosoftTeams -Credential $creds | Out-Null

        Write-Host "Connected to Microsoft 365 and configuring your organization with test teams and channels"

        # 2. Create the teams as specified in the XML.
        
        foreach ($team in $XmlDocument.Teams.Team ) {
            try {
                $group = New-Team -DisplayName $team.Name -Description $teams.description -visibility public 
                Write-Host "Successfully created team: " $group.DisplayName
            }
            catch {
                Write-Host "Unable to create team: $_"
            }
                
            # 3. Add users to the newly created teams.
            foreach ($user in $team.Members.Member) {
                try {
                    $newUserPrincipalName = (Get-AzureADUser -SearchString $user.UserName).UserPrincipalName

                    if($user.IsOwner -eq $true){
                        Add-TeamUser -GroupId $group.GroupId -User $newUserPrincipalName -Role Owner | Out-Null
                    }else{
                        Add-TeamUser -GroupId $group.GroupId -User $newUserPrincipalName | Out-Null
                    }

                    Write-Host "Successfully added user : " $user.UserName
                }
                catch {
                    Write-Host "Unable to add team user: $_"
                }

            }

            # 4. Add a set of channels to each newly created team
            foreach ($channel in $team.Channels.Channel) {
                try {
                    # Adding each team channel
                    New-TeamChannel -GroupId $group.GroupId -DisplayName $channel.Name -Description $channel.Description | Out-Null
                    Write-Host "Successfully created channel: " $channel.Name
                }
                catch {
                    Write-Host "Unable to add new Team Channel: $_"
                }   
            }

            Clear-Variable -Name group
        }

        Clear-Variable -Name creds
        
        # 5. Disconnect from all PowerShell sessions
        
        Write-Host "Completed execution and disconnecting from Microsoft 365 PowerShell sessions."
        Disconnect-MicrosoftTeams
        Disconnect-AzureAD
    }
    catch {
        Write-Host "Unable to complete the operation: $_"
    }
}
else {
    Write-Host "Content file has invalid data."
}
```

<span data-ttu-id="32177-130">Abra una sesión de Windows PowerShell en el modo de administrador.</span><span class="sxs-lookup"><span data-stu-id="32177-130">Open a Windows PowerShell session in Administrator mode.</span></span>  <span data-ttu-id="32177-131">Ejecute el script que acaba de guardar.</span><span class="sxs-lookup"><span data-stu-id="32177-131">Run the script that you just saved.</span></span>  <span data-ttu-id="32177-132">Se le pedirá que proporcione las credenciales: Use las credenciales de administrador global que recibió cuando se suscribió por primera vez a su suscripción de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="32177-132">You'll be prompted to provide the credentials - use the Global Administrator credentials you received when you first signed up for your developer subscription.</span></span>

> [!Note]
> <span data-ttu-id="32177-133">El script tardará varios minutos en ejecutarse (no cierre la sesión de PowerShell).</span><span class="sxs-lookup"><span data-stu-id="32177-133">The script will take several minutes to execute - do not close your PowerShell session.</span></span>  <span data-ttu-id="32177-134">Si ha modificado los usuarios de la suscripción con respecto a lo que se ha creado en el paquete de contenido predeterminado, es posible que algunos usuarios no se agreguen a teams.</span><span class="sxs-lookup"><span data-stu-id="32177-134">If you've modified the users in your subscription from what is created in the default content pack, some users may not be added to teams.</span></span>  <span data-ttu-id="32177-135">Cuando se ejecuta el script, se muestran las acciones correctas o fallidas.</span><span class="sxs-lookup"><span data-stu-id="32177-135">As the script executes it will output successful or failed actions.</span></span>

<span data-ttu-id="32177-136">Una vez finalizada la ejecución del script, puede iniciar sesión en el cliente de Microsoft Teams con una de las cuentas de usuario y ver los equipos recién creados.</span><span class="sxs-lookup"><span data-stu-id="32177-136">Once the script has finished execution, you can login to the Teams client with one of the user accounts and view the newly created teams.</span></span>
