---
title: Equinix Fabric
pcx_content_type: tutorial
weight: 3
meta:
  title: Equinix Users
---

# Equinix Users

## Order an Equinix Fabric Connection

After you confirm the locations and speed with you account team, order the Equinix Fabric connections to Cloudflare.

1.  Go to [Equinix Fabric](https://fabric.equinix.com/)
2.  Under **I want to connect to:**, select **A Service Provider**.
3.  Under **Select a Service Provider**, search for **Cloudflare** > **Select**.
4.  Select **Magic Transit** or **Cloudflare NaaS**. If you are unsure, select **Cloudflare NaaS** which can be used to configure any service.
5.  Under **Origin** > **Connect Using**, select your port.
6.  Under **Destination**, select your location. If the location you want is not listed, contact your Cloudflare account team to request a new location under the Interconnect Anywhere program.
7.  Under **Connection Information** > **VLAN ID**, enter a VLAN ID. Cloudflare chooses its own VLAN ID and Equinix Fabric maps between the two. To use the same VLAN ID as Cloudflare, ask your account team for Cloudflare's VLAN ID and they will provide it.
8.  Select **Next** and then **Submit Order**.

Cloudflare will accept the connection and your account team will contact you to establish the BGP session.