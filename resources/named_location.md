---
subcategory: "Conditional Access"
---

# Resource: azuread_named_location

Manages a Named Location within Azure Active Directory.

## API Permissions

The following API permissions are required in order to use this resource.

When authenticated with a service principal, this resource requires the following application roles: `Policy.ReadWrite.ConditionalAccess` and `Policy.Read.All`

When authenticated with a user principal, this resource requires one of the following directory roles: `Conditional Access Administrator` or `Global Administrator`

## Example Usage

```terraform
resource "azuread_named_location" "example-ip" {
  display_name = "IP Named Location"
  ip {
    ip_ranges = [
      "1.1.1.1/32",
      "2.2.2.2/32",
    ]
    trusted = true
  }
}

resource "azuread_named_location" "example-country" {
  display_name = "Country Named Location"
  country {
    countries_and_regions = [
      "GB",
      "US",
    ]
    include_unknown_countries_and_regions = false
  }
}
```

## Argument Reference

The following arguments are supported:

* `country` - (Optional) A `country` block as documented below, which configures a country-based named location.
* `display_name` - (Required) The friendly name for this named location.
* `ip` - (Optional) An `ip` block as documented below, which configures an IP-based named location.

-> Exactly one of `ip` or `country` must be specified. Changing between these forces a new resource to be created.

---

`country` block supports the following:

* `countries_and_regions` - (Required) List of countries and/or regions in two-letter format specified by ISO 3166-2. 
* `include_unknown_countries_and_regions` - (Optional) Whether IP addresses that don't map to a country or region should be included in the named location. Defaults to `false`.

---

`ip` block supports the following:

* `ip_ranges` - (Required) List of IP address ranges in IPv4 CIDR format (e.g. 1.2.3.4/32) or any allowable IPv6 format from IETF RFC596.
* `trusted` - (Optional) Whether the named location is trusted. Defaults to `false`.

---


## Attributes Reference

In addition to all arguments above, the following attributes are exported:

* `id` - The ID of the named location.

## Import

Named Locations can be imported using the `id`, e.g.

```shell
terraform import azuread_named_location.my_location 00000000-0000-0000-0000-000000000000
```
