---
title: Agregar datos de prueba al inquilino de prueba de Microsoft 365
description: Configurar la suscripción del programa para desarrolladores de Office 365 para realizar pruebas correctas de Aplicaciones de Microsoft Teams
ms.topic: how-to
localization_priority: Normal
keywords: equipos de programa de desarrolladores de aplicaciones de prueba
ms.date: 11/01/2019
ms.openlocfilehash: f224ad8b97cd5dd1a4349039824abaf551ef362e
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058470"
---
# <a name="add-test-data-to-your-microsoft-365-test-tenant"></a><span data-ttu-id="40238-104">Agregar datos de prueba al inquilino de prueba de Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="40238-104">Add test data to your Microsoft 365 test tenant</span></span>

<span data-ttu-id="40238-105">Con una suscripción de desarrollador de Microsoft 365, puedes usar la aplicación de Microsoft Teams con equipos de prueba, canales y usuarios.</span><span class="sxs-lookup"><span data-stu-id="40238-105">With a Microsoft 365 developer subscription, you can use your Microsoft Teams app with test teams, channels, and users.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40238-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="40238-106">Prerequisites</span></span>

1. <span data-ttu-id="40238-107">[Únase al Programa para desarrolladores de Microsoft 365,](/office/developer-program/office-365-developer-program)si no tiene un inquilino de prueba.</span><span class="sxs-lookup"><span data-stu-id="40238-107">[Join the Microsoft 365 Developer Program](/office/developer-program/office-365-developer-program), if you do not have a test tenant.</span></span>
2. <span data-ttu-id="40238-108">[Configurar una suscripción para desarrolladores de Microsoft 365](/office/developer-program/office-365-developer-program-get-started).</span><span class="sxs-lookup"><span data-stu-id="40238-108">[Set up a Microsoft 365 Developer Subscription](/office/developer-program/office-365-developer-program-get-started).</span></span>
3. <span data-ttu-id="40238-109">Use paquetes de datos de ejemplo con su suscripción de desarrollador de [Microsoft 365 para instalar el paquete de contenido Usuarios.](/office/developer-program/install-sample-packs)</span><span class="sxs-lookup"><span data-stu-id="40238-109">[Use sample data packs with your Microsoft 365 developer subscription to install the Users content pack](/office/developer-program/install-sample-packs).</span></span>
4. <span data-ttu-id="40238-110">[Instale el módulo de PowerShell de Teams](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2).</span><span class="sxs-lookup"><span data-stu-id="40238-110">[Install the Teams PowerShell module](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2).</span></span>
5. <span data-ttu-id="40238-111">[Instale el módulo de PowerShell de Azure AD](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="40238-111">[Install the Azure AD PowerShell module](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module&preserve-view=true).</span></span>

> [!NOTE]
> <span data-ttu-id="40238-112">Para cualquier inquilino que use, debe obtener los permisos de administrador global para ejecutar los scripts.</span><span class="sxs-lookup"><span data-stu-id="40238-112">For any tenant that you use, you must get the global administrator permissions to run the scripts.</span></span>

### <a name="optional-step-to-allow-upload-of-custom-apps"></a><span data-ttu-id="40238-113">Paso opcional para permitir la carga de aplicaciones personalizadas</span><span class="sxs-lookup"><span data-stu-id="40238-113">Optional step to allow upload of custom apps</span></span>

<span data-ttu-id="40238-114">De forma predeterminada, solo los administradores globales o los administradores de servicio de teams pueden cargar aplicaciones personalizadas en el catálogo de aplicaciones de inquilino.</span><span class="sxs-lookup"><span data-stu-id="40238-114">By default, only global admins or teams service admins can upload custom apps into the tenant app catalog.</span></span> <span data-ttu-id="40238-115">También puedes permitir que todos los usuarios carguen aplicaciones personalizadas para su propio uso o en equipos para realizar pruebas.</span><span class="sxs-lookup"><span data-stu-id="40238-115">You can also enable all users to upload custom apps for their own use or to teams for testing.</span></span>

<span data-ttu-id="40238-116">Para habilitar esta configuración, tendrás que actualizar la directiva global de configuración de aplicaciones en el Portal de administración de Teams.</span><span class="sxs-lookup"><span data-stu-id="40238-116">To enable this setting, you'll need to update the global App Setup Policy in your Teams Admin Portal.</span></span>

<img width="430px" src="~/assets/images/microsoft-teams-admin-center-screenshot.png" alt="Screenshot of App Setup Policy"/>

## <a name="optional-step-to-enable-custom-app-sideloading"></a><span data-ttu-id="40238-117">Paso opcional para habilitar la instalación local de aplicaciones personalizadas</span><span class="sxs-lookup"><span data-stu-id="40238-117">Optional step to enable custom app sideloading</span></span>

<span data-ttu-id="40238-118">Habilitar la instalación local de aplicaciones personalizadas es opcional.</span><span class="sxs-lookup"><span data-stu-id="40238-118">Enabling custom app sideloading is optional.</span></span> <span data-ttu-id="40238-119">De forma predeterminada, solo los administradores globales o los administradores de servicio de Teams pueden cargar aplicaciones personalizadas en el catálogo de aplicaciones de inquilino.</span><span class="sxs-lookup"><span data-stu-id="40238-119">By default, only global admins or Teams service admins can upload custom apps into the tenant app catalog.</span></span> <span data-ttu-id="40238-120">También puedes permitir que los usuarios carguen aplicaciones personalizadas en Teams.</span><span class="sxs-lookup"><span data-stu-id="40238-120">You can also allow users to upload custom apps to Teams.</span></span> <span data-ttu-id="40238-121">Para obtener más información, consulta [Administrar directivas de configuración de aplicaciones en Teams](/microsoftteams/teams-app-setup-policies).</span><span class="sxs-lookup"><span data-stu-id="40238-121">For more information, see [manage app setup policies in Teams](/microsoftteams/teams-app-setup-policies).</span></span>

## <a name="create-teams-and-channels"></a><span data-ttu-id="40238-122">Crear equipos y canales</span><span class="sxs-lookup"><span data-stu-id="40238-122">Create teams and channels</span></span>

1. <span data-ttu-id="40238-123">Guarde el siguiente fragmento de código como **un archivo .xml** y anote la ruta de acceso del archivo.</span><span class="sxs-lookup"><span data-stu-id="40238-123">Save the following snippet as a **.xml** file and note the file path.</span></span> <span data-ttu-id="40238-124">Este XML define la estructura del equipo y el canal que se crea junto con sus miembros:</span><span class="sxs-lookup"><span data-stu-id="40238-124">This XML defines the structure of the team and channel that is created along with its members:</span></span>

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

2. <span data-ttu-id="40238-125">Guarde el siguiente fragmento de código como un script de PowerShell (.ps1) y anote dónde lo guardó.</span><span class="sxs-lookup"><span data-stu-id="40238-125">Save the following snippet as a PowerShell script (.ps1) and note where you have saved it.</span></span> <span data-ttu-id="40238-126">Este script ejecuta los pasos para crear el equipo y el canal y agregar miembros a ellos:</span><span class="sxs-lookup"><span data-stu-id="40238-126">This script executes the steps to create the team and channel, and add members to them:</span></span>

    ```powershell
    Param(
        [Parameter(Mandatory = $true)]

        # This specifies the location of your configuration XML.

        [string] $teamsFilePath 
    )

    [xml]$XmlDocument = Get-Content -Path $teamsFilePath.ToString()

    if ($XmlDocument.Teams.Team.Count -gt 0) {

        try {

            # 1. Login with the global administrator account for your O365 Developer Program tenant. This script uses these credentials to connect to the powershell modules for Azure Active Directory and Microsoft Teams

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

3. <span data-ttu-id="40238-127">Abra una Windows PowerShell sesión en modo administrador y ejecute el script que acaba de guardar.</span><span class="sxs-lookup"><span data-stu-id="40238-127">Open a Windows PowerShell session in Administrator mode, and run the script that you just saved.</span></span>
4. <span data-ttu-id="40238-128">Cuando se le pida que proporcione las credenciales, escriba las credenciales de administrador global que recibió cuando se inscribió por primera vez para la suscripción de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="40238-128">When you are prompted to provide the credentials, enter the Global Administrator credentials you received when you first signed up for your developer subscription.</span></span>

    > [!Note]
    > <span data-ttu-id="40238-129">No cierre la sesión de PowerShell, ya que el script tarda varios minutos en ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="40238-129">Do not close your PowerShell session as the script takes several minutes to execute.</span></span> <span data-ttu-id="40238-130">Si ha modificado los usuarios de la suscripción a partir de lo que se crea en el paquete de contenido predeterminado, es posible que algunos usuarios no se agregó a Teams.</span><span class="sxs-lookup"><span data-stu-id="40238-130">If you have modified the users in your subscription from what is created in the default content pack, some users may not be added to Teams.</span></span> <span data-ttu-id="40238-131">Cuando el script se ejecuta, muestra acciones correctas o con errores.</span><span class="sxs-lookup"><span data-stu-id="40238-131">As the script executes it displays successful or failed actions.</span></span>

5. <span data-ttu-id="40238-132">Una vez que el script haya finalizado la ejecución, puede iniciar sesión en el cliente de Teams con una de las cuentas de usuario y ver los equipos recién creados.</span><span class="sxs-lookup"><span data-stu-id="40238-132">After the script has finished execution, you can sign in to the Teams client with one of the user accounts and view the newly created teams.</span></span>

## <a name="see-also"></a><span data-ttu-id="40238-133">Vea también</span><span class="sxs-lookup"><span data-stu-id="40238-133">See also</span></span>

- [<span data-ttu-id="40238-134">Depurar la pestaña</span><span class="sxs-lookup"><span data-stu-id="40238-134">Debug your tab</span></span>](~/tabs/how-to/developer-tools.md)
 
- [<span data-ttu-id="40238-135">Depurar los bots</span><span class="sxs-lookup"><span data-stu-id="40238-135">Debug your bots</span></span>](~/bots/how-to/debug/locally-with-an-ide.md)

- [<span data-ttu-id="40238-136">Probar permisos de RSC</span><span class="sxs-lookup"><span data-stu-id="40238-136">Test RSC permissions</span></span>](~/graph-api/rsc/test-resource-specific-consent.md)

