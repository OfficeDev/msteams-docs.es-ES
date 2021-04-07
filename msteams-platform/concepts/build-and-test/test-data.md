---
title: Agregar datos de prueba al inquilino de prueba de Microsoft 365
description: Configurar la suscripción del programa para desarrolladores de Office 365 para realizar pruebas correctas de Aplicaciones de Microsoft Teams
ms.topic: how-to
keywords: equipos de programa de desarrolladores de aplicaciones de prueba
ms.date: 11/01/2019
ms.openlocfilehash: 863f1d9843bb3ebe968ca180ee70a5b6bfa6cd7a
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596192"
---
# <a name="add-test-data-to-your-microsoft-365-test-tenant"></a><span data-ttu-id="edc4b-104">Agregar datos de prueba al inquilino de prueba de Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="edc4b-104">Add test data to your Microsoft 365 test tenant</span></span>

<span data-ttu-id="edc4b-105">Con una suscripción de desarrollador de Microsoft 365, puedes usar la aplicación de Microsoft Teams con equipos de prueba, canales y usuarios.</span><span class="sxs-lookup"><span data-stu-id="edc4b-105">With a Microsoft 365 developer subscription, you can use your Microsoft Teams app with test teams, channels, and users.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="edc4b-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="edc4b-106">Before you start</span></span>

<span data-ttu-id="edc4b-107">Si aún no tiene un inquilino de prueba, tendrá que unirse al programa para desarrolladores de Office 365 y registrarse para una suscripción de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="edc4b-107">If you don't already have a test tenant, you will need to join the Office 365 developer program and sign up for a developer subscription.</span></span> <span data-ttu-id="edc4b-108">También tendrá que instalar los módulos de PowerShell necesarios.</span><span class="sxs-lookup"><span data-stu-id="edc4b-108">You'll also need to install the necessary PowerShell modules.</span></span> <span data-ttu-id="edc4b-109">Para cualquier espacio empresarial que use, necesitará tener permisos de administrador global para ejecutar los scripts.</span><span class="sxs-lookup"><span data-stu-id="edc4b-109">For whatever tenant you use you'll need to have global administrator permissions to run the scripts.</span></span>

1. [<span data-ttu-id="edc4b-110">Unirse al programa de desarrolladores de Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="edc4b-110">Join the Microsoft 365 Developer Program</span></span>](/office/developer-program/office-365-developer-program)
2. [<span data-ttu-id="edc4b-111">Configurar una suscripción para desarrolladores de Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="edc4b-111">Set up a Microsoft 365 Developer Subscription</span></span>](/office/developer-program/office-365-developer-program-get-started)
3. [<span data-ttu-id="edc4b-112">Usar paquetes de datos de ejemplo con la suscripción de desarrollador de Microsoft 365 para instalar el paquete de contenido Usuarios</span><span class="sxs-lookup"><span data-stu-id="edc4b-112">Use sample data packs with your Microsoft 365 developer subscription to install the Users content pack</span></span>](/office/developer-program/install-sample-packs)
4. [<span data-ttu-id="edc4b-113">Instalar el módulo de PowerShell de Teams</span><span class="sxs-lookup"><span data-stu-id="edc4b-113">Install the Teams PowerShell module</span></span>](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2)
5. [<span data-ttu-id="edc4b-114">Instalar el módulo de PowerShell de Azure AD</span><span class="sxs-lookup"><span data-stu-id="edc4b-114">Install the Azure AD PowerShell module</span></span>](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module&preserve-view=true)

## <a name="optional-enable-custom-app-sideloading"></a><span data-ttu-id="edc4b-115">(Opcional) Habilitar la instalación local de aplicaciones personalizadas</span><span class="sxs-lookup"><span data-stu-id="edc4b-115">(Optional) Enable custom app sideloading</span></span>

<span data-ttu-id="edc4b-116">De forma predeterminada, solo los administradores globales o los administradores de servicio de Teams pueden cargar aplicaciones personalizadas en el catálogo de aplicaciones de inquilino.</span><span class="sxs-lookup"><span data-stu-id="edc4b-116">By default, only global admins or Teams service admins can upload custom apps into the tenant app catalog.</span></span> <span data-ttu-id="edc4b-117">También puedes permitir que los usuarios carguen aplicaciones personalizadas en Teams.</span><span class="sxs-lookup"><span data-stu-id="edc4b-117">You can also allow users to upload custom apps to Teams.</span></span> <span data-ttu-id="edc4b-118">Para obtener más información, [administre las directivas de configuración de aplicaciones en Teams](/microsoftteams/teams-app-setup-policies).</span><span class="sxs-lookup"><span data-stu-id="edc4b-118">For more information, [manage app setup policies in Teams](/microsoftteams/teams-app-setup-policies).</span></span>

## <a name="create-teams-and-channels"></a><span data-ttu-id="edc4b-119">Crear equipos y canales</span><span class="sxs-lookup"><span data-stu-id="edc4b-119">Create teams and channels</span></span>

<span data-ttu-id="edc4b-120">Guarde el siguiente fragmento de código como XML (.xml) y observe dónde lo guardó.</span><span class="sxs-lookup"><span data-stu-id="edc4b-120">Save the following snippet as an XML (.xml) and note where you've saved it.</span></span>  <span data-ttu-id="edc4b-121">Este XML define la estructura de los equipos y canales que se crearán, junto con sus miembros.</span><span class="sxs-lookup"><span data-stu-id="edc4b-121">This XML defines the structure of the teams and channels that will be created - along with its members.</span></span>

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

<span data-ttu-id="edc4b-122">Guarde el siguiente fragmento de código como un script de PowerShell (.ps1) y observe dónde lo guardó.</span><span class="sxs-lookup"><span data-stu-id="edc4b-122">Save the following snippet as a PowerShell script (.ps1) and note where you've saved it.</span></span>  <span data-ttu-id="edc4b-123">Este script ejecuta los pasos para crear los equipos y canales y agregar miembros a ellos.</span><span class="sxs-lookup"><span data-stu-id="edc4b-123">This script executes the steps to create the teams and channels and add members to them.</span></span>

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

<span data-ttu-id="edc4b-124">Abra una sesión Windows PowerShell en modo administrador.</span><span class="sxs-lookup"><span data-stu-id="edc4b-124">Open a Windows PowerShell session in Administrator mode.</span></span>  <span data-ttu-id="edc4b-125">Ejecute el script que acaba de guardar.</span><span class="sxs-lookup"><span data-stu-id="edc4b-125">Run the script that you just saved.</span></span>  <span data-ttu-id="edc4b-126">Se le pedirá que proporcione las credenciales: use las credenciales de administrador global que recibió cuando se inscribió por primera vez para la suscripción de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="edc4b-126">You'll be prompted to provide the credentials - use the Global Administrator credentials you received when you first signed up for your developer subscription.</span></span>

> [!Note]
> <span data-ttu-id="edc4b-127">El script llevará varios minutos en ejecutarse: no cierre la sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="edc4b-127">The script will take several minutes to execute - do not close your PowerShell session.</span></span>  <span data-ttu-id="edc4b-128">Si ha modificado los usuarios de la suscripción a partir de lo que se crea en el paquete de contenido predeterminado, es posible que algunos usuarios no se agregó a teams.</span><span class="sxs-lookup"><span data-stu-id="edc4b-128">If you've modified the users in your subscription from what is created in the default content pack, some users may not be added to teams.</span></span>  <span data-ttu-id="edc4b-129">Cuando el script se ejecuta, se mostrarán acciones correctas o con errores.</span><span class="sxs-lookup"><span data-stu-id="edc4b-129">As the script executes it will output successful or failed actions.</span></span>

<span data-ttu-id="edc4b-130">Una vez que el script haya terminado de ejecutarse, puede iniciar sesión en el cliente de Teams con una de las cuentas de usuario y ver los equipos recién creados.</span><span class="sxs-lookup"><span data-stu-id="edc4b-130">Once the script has finished execution, you can login to the Teams client with one of the user accounts and view the newly created teams.</span></span>
