# routeros_ip_ipsec_peer (Resource)


## Example Usage
```terraform
resource "routeros_ip_ipsec_peer" "test" {
  address       = "lv20.nordvpn.com"
  exchange_mode = "ike2"
  name          = "NordVPN"
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `name` (String) Peer name.

### Optional

- `address` (String) If the remote peer's address matches this prefix, then the peer configuration is used in authentication and establishment of Phase 1. If several peer's addresses match several configuration entries, the most specific one (i.e. the one with the largest netmask) will be used.
- `comment` (String)
- `disabled` (Boolean)
- `exchange_mode` (String) Different ISAKMP phase 1 exchange modes according to RFC 2408. the main mode relaxes rfc2409 section 5.4, to allow pre-shared-key authentication in the main mode. ike2 mode enables Ikev2 RFC 7296. Parameters that are ignored by IKEv2 proposal-check, compatibility-options, lifebytes, dpd-maximum-failures, nat-traversal.
- `local_address` (String) Routers local address on which Phase 1 should be bounded to.
- `passive` (Boolean) When a passive mode is enabled will wait for a remote peer to initiate an IKE connection. The enabled passive mode also indicates that the peer is xauth responder, and disabled passive mode - xauth initiator. When a passive mode is a disabled peer will try to establish not only phase1 but also phase2 automatically, if policies are configured or created during the phase1.
- `port` (Number) Communication port used (when a router is an initiator) to connect to remote peer in cases if remote peer uses the non-default port.
- `profile` (String) Name of the profile template that will be used during IKE negotiation.
- `send_initial_contact` (Boolean) Specifies whether to send `initial contact` IKE packet or wait for remote side, this packet should trigger the removal of old peer SAs for current source address. Usually, in road warrior setups clients are initiators and this parameter should be set to no. Initial contact is not sent if modecfg or xauth is enabled for ikev1.

### Read-Only

- `dynamic` (Boolean) Configuration item created by software, not by management interface. It is not exported, and cannot be directly modified.
- `id` (String) The ID of this resource.
- `responder` (Boolean) Whether this peer will act as a responder only (listen to incoming requests) and not initiate a connection.

## Import
Import is supported using the following syntax:
```shell
#The ID can be found via API or the terminal
#The command for the terminal is -> :put [/ip/ipsec/peer get [print show-ids]]
terraform import routeros_ip_ipsec_peer.test *3
#Or you can import a resource using one of its attributes
terraform import routeros_ip_ipsec_peer.test "name=NordVPN"
```