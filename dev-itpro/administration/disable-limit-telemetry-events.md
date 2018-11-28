---
title: "Turn Off or Limit Telemetry Trace Events"
ms.custom: na
ms.date: 10/01/2018
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
author: jswymer
---
# Turn Off or Limit Telemetry Trace Events
The application and platform can emit many telemetry trace events, which can be collected using various event trace tools. For example, telemetry trace events are recorded in the [!INCLUDE[server](../developer/includes/server.md)] channel logs, which you can see in Event Viewer, under **Applications and Services Logs** > **Microsoft** > **Dynamics365BusinessCentral** > **Common** > **Admin**. 

The number of events can place a large demand on the logging resources on the computer running the [!INCLUDE[nav_server_md](../developer/includes/nav_server_md.md)] instance. To help eleviate this demand, the [!INCLUDE[nav_server_md](../developer/includes/nav_server_md.md)] instance includes a configuration setting called **Diagnostic Trace Level** (`TraceLevel` in the customsettings.config file) that enables you to specify the lowest severity level of customer telemetry trace events that are emitted from the application, or even turn off telemetry events altogether. Custom telemetry trace events have IDs from  700-712. 
  
To configure the **Diagnostic Trace Level** setting, you can use the [!INCLUDE[admintool](../developer/includes/admintool.md)], modify the [!INCLUDE[server](../developer/includes/server.md)] instance configuration file \(CustomSettings.config\) directly, or use the [Set-NAVServerConfiguration cmdlet](https://docs.microsoft.com/en-us/powershell/module/microsoft.dynamics.nav.management/Set-NAVServerConfiguration) of the [!INCLUDE[adminshell](../developer/includes/adminshell.md)].

>[!TIP]
>Custom telemetry events are generated by calls to the SENDTRACETAG method in code. For more information, see [Instrumenting an Application for Telemetry](../developer/devenv-instrument-application-for-telemetry.md).

## Use the [!INCLUDE[admintool](../developer/includes/admintool.md)]   
  
1.  To start the [!INCLUDE[admintool](../developer/includes/admintool.md)], select **Start**, and in the **Search programs and files** box, type **Microsoft Dynamics365 Business Central Administration**, and then choose the related link.  
  
2.  In the left pane, under **Console root**, select the [!INCLUDE[server](../developer/includes/server.md)] instance.  
  
3.  In the center pane, select the **Edit** button.  
  
4.  Under **General**, set the **Diagnostic Trace Level**: 

    You use this setting to filter out lower-level events from being emitted. For example, if you set this setting to **Error**, only **Error** and **Critical** events will be emitted.
    
    Set to **Off** if you do not want to emit telemetry trace events.
    
5.  Select the **Save** button, and then select the **OK** button.  
  
     You must restart the [!INCLUDE[server](../developer/includes/server.md)] instance for the changes to take effect.  
  
6.  To restart, the [!INCLUDE[server](../developer/includes/server.md)] instance, in the left pane, select the [!INCLUDE[prodshort](../developer/includes/prodshort.md)] computer.  
  
     Unless you are administering a remote computer, this is [!INCLUDE[prodshort](../developer/includes/prodshort.md)] \(local\).  
  
7.  In the center pane, right-click an instance, and then select **Restart**.  
  
## Modify the CustomSettings.config file  
  
1.  Open the CustomSettings.config file for the [!INCLUDE[server](../developer/includes/server.md)] instance in a text editor, such as Notepad.  
  
     By default, the file is located in the [!INCLUDE[prodinstallpath](../developer/includes/prodinstallpath.md)]\\Service folder or [!INCLUDE[prodinstallpath](../developer/includes/prodinstallpath.md)]\\Service\\Instances\\\<instancename> folder \(for multitenant installations\).  
  
2.  Set the **TraceLevel** setting to **Critical**, **Error**, **Warning**, **Normal** (this corresponds to the **Information** level), **Verbose**, or **Off**.  
  
3.  Save the file, and then restart the [!INCLUDE[server](../developer/includes/server.md)] instance.  


## Use the [!INCLUDE[adminshell](../developer/includes/adminshell.md)] 

1. Start the [!INCLUDE[adminshell](../developer/includes/adminshell.md)].
2. At the command prompt, run the following command:

    ```
    Set-NAVServerConfiguration -ServerInstance MyServerInstance -KeyName TraceLevel -KeyValue level -ApplyTo All
    ```
    Substitute `MyServerInstance` with the name of the [!INCLUDE[server](../developer/includes/server.md)] instance and `level` with either `Critical`, `Error`, `Warning`, `Normal`, `Verbose`, or `Off`.
    
For more information about how to use the [!INCLUDE[adminshell](../developer/includes/adminshell.md)], see [Business Central PowerShell Cmdlets](https://docs.microsoft.com/en-us/powershell/business-central/overview) and [Set-NAVServerConfiguration Cmdlet](https://go.microsoft.com/fwlink/?linkid=401394).

## See Also  
 [Monitoring Business Central Server Events Using Event Viewer](monitor-server-events-windows-event-log.md)   
 [Monitoring Business Central Server Events](monitor-server-events.md)   
 [Configuring Business Central Server](configure-server-instance.md#General)  