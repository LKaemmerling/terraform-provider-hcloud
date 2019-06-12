---
layout: "hcloud"
page_title: "Hetzner Cloud: hcloud_server_network"
sidebar_current: "docs-hcloud-resource-server-network"
description: |-
  Provides a Hetzner Cloud Server Network to represent a private network on a server in the Hetzner Cloud.
---

# hcloud_server_network

 Provides a Hetzner Cloud Server Network to represent a private network on a server in the Hetzner Cloud.

## Example Usage

```hcl
resource "hcloud_server" "node1" {
  name = "node1"
  image = "debian-9"
  server_type = "cx11"
}
resource "hcloud_network" "mynet" {
  name = "my-net"
  ip_range = "10.0.0.0/8"
}
resource "hcloud_network_subnet" "foonet" {
  network_id = "${hcloud_network.mynet.id}"
  type = "server"
  network_zone = "eu-central"
  ip_range   = "10.0.1.0/24"
}

resource "hcloud_server_network" "srvnetwork" {
  server_id = "${hcloud_server.node1.id}"
  network_id = "${hcloud_network.mynet.id}"
  ip = "10.0.1.5"
}
```

## Argument Reference

- `network_id` - (Required, int) ID of the network which should be added to the server.
- `server_id` - (Required, int) ID of the server.
- `ip` - (Optional, string) IP to request to be assigned to this server. If you do not provide this then you will be auto assigned an IP address.
- `alias_ips` - (Required, list[string]) Additional IPs to be assigned to this server.

## Attributes Reference

- `id` - (string) ID of the server network.
- `network_id` - (int) ID of the network.
- `server_id` - (int) ID of the server.
- `ip` - (string) IP assigned to this server.
- `alias_ips` - (list[string]) Additional IPs assigned to this server.