---
layout: doc
---
# Microsoft Teams optimization for Citrix Virtual Apps and Desktops environments

## Contributors

**Author:** [Mayank Singh](https://twitter.com/techmayank)

**Special Thanks:** Fernando Klurfan

## Overview

This document serves as a guide to prepare an IT organization for successfully evaluating Unified Communications (UC) in desktop and application virtualization environments using Microsoft Teams. Over 500,000 organizations, including 91 of the Fortune 100 (as of Mar 2019)use Teams in 44 languages across 181 markets. Without proper consideration and design for optimization, virtual desktop and virtual application users will very likely find the Microsoft Teams experience to be subpar. Citrix provides technologies to optimize this experience, to make Teams more responsive with crisp video and audio, even when working remotely in a virtual desktop. However, with multiple combinations of Teams infrastructures, clients, endpoint types, and user locations one must find the right “recipe” to deliver Teams optimally.

The **Citrix® HDX™ Optimization for Microsoft® Teams** offers clear, crisp 720p high-definition video calls @30 fps, in an optimized architecture. Users can seamlessly participate in audio-video or audio-only calls to and from other Teams users, Optimized Teams’ users and other standards-based video desktop and conference room systems. Support for screen sharing is also available.
This document will guide administrators in evaluating the Teams delivery solution in their Citrix environment. It contains best practices, tips and tricks to ensure that the deployment is the most robust.

## Optimized versus Generic delivery of Microsoft Teams

This is often what causes the most confusion about delivering a Microsoft Teams experience in a Citrix environment. The main reason is that without optimization the media must “hairpin” from your client to the server in the data center and then back to the endpoint. This can put significant load on the server (especially for video) and can cause delay and an overall degraded experience, especially if the other party in a Teams call is originating from a user in a similar virtualized experience. This method for delivering a Microsoft Teams experience is referred to as “Generic” delivery.

The preferred method of delivery is the “Optimized” method. In this case, the architect and/or administrator uses Optimization for Microsoft Teams in their environment. The “Optimized” method is like splitting the Teams client in two, as illustrated in the following comparison diagram. The user interface lives inside the virtual host, and is seen completely in the virtual desktop or application display. However, the media rendering, or media engine is separated off to run on the endpoint. This allows for a very rich rendering of the audio and video and a great desktop sharing experience.

![Optimized vs Fallback mode of delivery for Microsoft Teams](/en-us/tech-zone/build/media/deployment-guides_microsoft-teams-optimizations_1.png)

### Choosing the right Teams optimization for your environment

Optimization for Teams is not a “one size fits all” technology. For the Teams desktop app, with Windows clients, the Citrix HDX Optimization for Microsoft Teams with Citrix Workspace App is the way to go. With Linux and Mac clients being on the roadmap.
For Web based teams, with Windows and Linux clients using a Chrome browser, the Citrix HDX Optimization for Microsoft Teams with Browser Content Redirection would be the right solution.
For the remaining OS and Teams delivery format combinations, the generic delivery with the Fallback to Media over HDX is the option. Optimization for mobile OS’s is not available right now. Typically, mobile users who desire access to Teams on their devices will leverage Teams native apps from the appropriate app store.

### Pros of using Citrix HDX Optimization for Microsoft Teams

-  Richest experience, all media rendered on endpoint
-  No hair-pinning effect, media communications go point to point between clients and the Teams conferencing service homed in Office 365
-  Less resource impact on the Citrix Virtual Apps and Desktops hosts
-  Less HDX bandwidth consumed over “generic” approach
-  Allows for use of high tech Teams optimized headsets and handsets
-  Supports delivery with Citrix Virtual Apps using Windows Server OS’s
-  Simple installation on client devices, minimal prerequisites
-  Can be used remotely from the enterprise network in conjunction with Office 365
-  Wide choice of supported HDX Premium thin client devices (see [Citrix Ready list](https://citrixready.citrix.com/category-results.html?&f1=endpoints&f2=thin-clients&f3=unique-proposition/ms-teams-optimized&lang=en_us))
-  Support provided by both Microsoft and Citrix support
-  No requirement for both the sides of the optimized architecture to authenticate to the backend
-  Requires no modification to the Teams back end

## Citrix HDX Optimization for Microsoft Teams

These components are by default, bundled into Citrix Workspace app and the Virtual Delivery Agent (VDA)

### Conceptual Architecture

<Create the Visio for it>

**OS versions supported by the the Optimization for Teams with Microsoft Teams desktop app**
-  VM hosting Teams client – Install Citrix Virtual Delivery Agent (VDA) version 1909 or higher: -
    -  Single session OS - Microsoft Windows 10 64-bit, minimum version 1607 upto 1909
    -  Multi-session OS - Microsoft Windows Server 2019, 2016, 2012 R2 (Standard and Datacenter Editions)

-  Windows client machine - Install Citrix Workspace app 1907 for Windows or higher
    -  Microsoft Windows 10, 8, 7 (32-bit & 64-bit editions, including Embedded editions 2016 LTSR or 2019 LTSC)
    -  While Citrix Workspace app 1905 for Windows also supports Optimization for Teams, it doesn’t support outgoing screen sharing

**Supported Teams headsets and handsets**

The list of devices that are supported by Microsoft for [Teams](https://products.office.com/en-us/microsoft-teams/across-devices/devices) and [Skype for Business](https://docs.microsoft.com/en-us/skypeforbusiness/certification/devices-usb-devices)

Note: Microsoft Teams does not support iPhone headsets

## Installation Steps

### Prerequisites
Note - The Optimization for Teams at GA only applies to Windows Endpoints
1.  Download the latest Citrix Virtual Apps and Desktops VDA installer. On Citrix.com, select the Downloads Tab. Select Citrix Virtual Apps and Desktops as the product and select Product Software as the download type. Select Citrix Virtual Apps and Desktops 1906 or later, it will be under Components
1.  Ensure that the Teams service is reachable, from the client as well as the VDA
1.  Ensure Microsoft Teams client version 1.2.00.31357 or higher is installed in the Virtual Delivery Agent hosts or base image or on Citrix Virtual Apps servers, which will be used to deliver Microsoft Teams or on both. See instructions on how to install it below
1.  Download the latest Citrix Workspace app. Link: https://www.citrix.com/downloads/workspace-app/windows/workspace-app-for-windows-latest.html

The installation procedures are simple

## Microsoft Teams install

The installation must be done on the golden image of your catalog or in the office layer (if you are using App Layering). We recommend you follow the Microsoft Teams installation guidelines. Avoid installing Teams under Appdata. Instead, install in **C:\Program Files** by using the **ALLUSER=1** flag. 
For more information, see [Install Microsoft Teams using MSI](https://docs.microsoft.com/en-us/MicrosoftTeams/msi-deployment#vdi-installation)

If Teams was installed in user mode before on the image:
-  Users from EXE installer:
    -  Have all users in the environment manually uninstall from Control Panel > Programs & Features
-  Admin from MSI:
    -  Admin uninstalls in the normal way
    -  All users in the environment need to sign in, in order uninstallation to be completed
-  Admin from Office Pro Plus:
    -  Admin may need to uninstall as if MSI were directly installed (above)
    -  Office Pro Plus needs to be configured to not include Teams

## Citrix Virtual Apps and Desktops VDA install on the host virtual machines

The HDX Optimization for Teams is bundled as part of VDA in Citrix Virtual Apps and Desktops. It is installed on the hosts or base image of the catalog as well as Citrix Virtual Apps servers, which may be used to deliver Teams. Link to the version 1909 is [here](https://www.citrix.com/downloads/citrix-virtual-apps-and-desktops/product-software/citrix-virtual-apps-and-desktops-1909.html)

**Application requirements**

The VDA installer automatically installs the following items, which are available on the Citrix installation media in the Support folders
-  Microsoft .NET Framework 4.7.1 or later, if it is not already installed
-  Microsoft Visual C++ 2013 and 2015 Runtimes, 32-bit and 64-bit
-  BCR_x64.msi - the MSI that contains the Microsoft Teams optimization code and starts automatically from the GUI. If you’re using the command line interface for the VDA installation, don’t exclude it

For Windows Server, if you did not install and enable the Remote Desktop Services roles, the installer automatically installs and enables those roles.

3 GB of free disk space for each user profile (recommended by Microsoft)

Ensure that the Microsoft Teams client application is installed in per-machine mode on the VDA

**Install the Citrix Virtual Delivery Agent** on the host or base image, following the instrcutions [here](https://docs.citrix.com/en-us/citrix-virtual-apps-desktops/install-configure/install-vdas.html)

Using this image, create the appropriate machine catalogs and delivery groups in Citrix Studio/ Citrix Cloud Manage tab before trying to establish sessions and accessing the Teams client.

## Windows client device – Citrix Workspace app 1909 for Windows install

The Citrix Workspace app 1909 for Windows has the optimization components built into it. When you install the application on your client, they should already be present.

**System Requirements**

-  Approximately 1.8–2.0 GHz quad core CPU required for 720p HD resolution during a peer-to-peer video conference call. Quad core CPUs with lower speeds (~1.5 GHz) but equipped with Intel Turbo Boost or AMD Turbo Core that can boost up to 2.0 GHz are also supported
-  Citrix Workspace app requires a minimum of 600 MB free disk space and 1 GB RAM.
-  Microsoft .NET Framework version 4.6.2 or later is installed automatically, if it is not already installed.

Follow the instructions, to install the Citrix Workspace app for Windows [here](https://docs.citrix.com/en-us/citrix-workspace-app-for-windows/install.html#using-a-windows-based-installer)

## Policy Settings

To enable optimization, ensure the **Microsoft Teams redirection** Studio policy is set to **Allowed**
The policy is enabled by default

<Insert the screenshot>

**Note**: In addition to this policy being enabled, HDX checks to verify that the version of Citrix Workspace app is equal to or greater than the minimum required version. If both conditions are met, the below registry key is set to 1 on the VDA. The Microsoft Teams application reads the key to load in VDI mode
**HKEY_CURRENT_USER\Software\Citrix\HDXMediaStream**
Name: **MSTeamsRedirSupport**
Value: DWORD (1 - on, 0 - off)

## Network Requirements

Microsoft Teams relies on Media Processor servers in Microsoft Azure for meetings or multiparty calls, and on Azure Transport Relays for scenarios where two peers in a point-to-point call do not have direct connectivity, or where a participant does not have direct connectivity to the Media Processor. Therefore, the network health between the peer and the Office 365 cloud determines the performance of the call.

We recommend evaluating your environment to identify any risks and requirements that can influence your overall cloud voice and video deployment. Use the [Skype for Business Network Assessment Tool](https://www.microsoft.com/en-us/download/details.aspx?id=53885) to test if your network is ready for Microsoft Teams.

### Port / Firewall settings
Teams traffic will flow via Transport Relay on TCP and UDP 80, 443, UDP 3478-3481. 
Optimized traffic for peer to peer connections is routed on higher ports (40K+ UDP) at random, if they are open. For more info [read](https://docs.microsoft.com/en-us/office365/enterprise/urls-and-ip-address-ranges#skype-for-business-online-and-microsoft-teams)

For support information, see [Support](https://docs.citrix.com/en-us/citrix-virtual-apps-desktops/multimedia/opt-ms-teams.html#support) section of our documentation.

### Summary of key network recommendations for Real Time Protocol (RTP) traffic

Connect to the Office 365 network as directly as possible from the branch office
Bypass proxy servers, network SSL intercept, deep packet inspection devices, and VPN hairpins (use split tunneling if possible) at the branch office. If you must use them, make sure RTP/UDP Teams traffic is unhindered. Plan and provide enough bandwidth. Check each branch office for network connectivity and quality.
The WebRTC media engine in Workspace app (HdxTeams.exe) uses the Secure RTP protocol for multimedia streams that are offloaded to the client. The following metrics are recommended for guaranteeing a great user experience

-  Latency (one way) < 50 milli seconds
-  Latency (RTT) < 100 milli seconds
-  Packet Loss < 1% during any 15 second interval
-  Packet inter-arrival jitter < 30 ms during any 15 second interval

For more information, see [Prepare your organization’s network for Microsoft Teams](https://aka.ms/PerformanceRequirements)
In terms of bandwidth requirements, optimization for Microsoft Teams can use a wide variety of codecs for audio (OPUS/G.722/PCM/G711) and video (H264/VP9). The peers negotiate these codecs during the call establishment process using the Session Description Protocol (SDP) Offer/Answer. 

Citrix minimum recommendations for bandwidth and codes for specific type of content are:

-  Audio (each way)  ~90 kbps   G.722
-  Audio (each way)  ~60 kbps   Opus*
-  Video (each way)  ~700 kbps  H264 360p @ 30 fps 16:9
-  Video (each way)  ~2500 kbps H264 720p @ 30 fps 16:9
-  Screen sharing    ~300 kbps  H264 1080p @ 15 fps

(*) Opus supports constant and variable bitrate encoding from 6 kbps up to 510 kbps, and it is the preferred codec for p2p calls between two VDI users