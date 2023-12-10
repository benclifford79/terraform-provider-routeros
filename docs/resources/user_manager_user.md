# routeros_user_manager_user (Resource)


## Example Usage
```terraform
resource "routeros_user_manager_attribute" "mikrotik_wireless_comment" {
  name       = "Mikrotik-Wireless-Comment"
  type_id    = 21
  value_type = "string"
}

resource "routeros_user_manager_attribute" "mikrotik_wireless_vlanid" {
  name       = "Mikrotik-Wireless-VLANID"
  type_id    = 26
  value_type = "uint32"
}

resource "routeros_user_manager_user_group" "test" {
  name = "test"
}

resource "routeros_user_manager_user" "test" {
  attributes = [
    "${routeros_user_manager_attribute.mikrotik_wireless_comment.name}:Test Group",
    "${routeros_user_manager_attribute.mikrotik_wireless_vlanid.name}:100",
  ]
  group    = routeros_user_manager_user_group.test.name
  name     = "test"
  password = "password"
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `name` (String) Username for session authentication.

### Optional

- `attributes` (List of String) A custom set of colon-separated attributes with their values will be added to `Access-Accept` messages for users in this group.
- `caller_id` (String) Allow user's authentication with a specific Calling-Station-Id value.
- `comment` (String)
- `disabled` (Boolean)
- `group` (String) Name of the group the user is associated with.
- `otp_secret` (String) A token of a one-time code that will be attached to the password.
- `password` (String) The password of the user for session authentication.
- `shared_users` (Number) The total amount of sessions the user can simultaneously establish.

### Read-Only

- `id` (String) The ID of this resource.

## Import
Import is supported using the following syntax:
```shell
#The ID can be found via API or the terminal
#The command for the terminal is -> :put [/user-manager/user get [print show-ids]]
terraform import routeros_user_manager_user.test '*1'
```