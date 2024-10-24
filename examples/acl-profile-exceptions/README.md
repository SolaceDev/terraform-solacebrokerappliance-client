# ACL Profile Exceptions Configuration Example

This directory demonstrates the configuration of a client username with [ACL profile exceptions](https://docs.solace.com/Security/Managing-Access-Control-Lists.htm) on the PubSub+ appliance, leveraging the Client Terraform module.

One set of use cases is if the assigned ACL profile is restrictive (the default value is "disallow") and individual permissions are added as exceptions. Other cases need individual exceptions to a permissive profile. Both serve the configuration of specific requirements of the client being provisioned.

The following ACL profile exceptions are supported:
* Publish topic exception
* Subscribe topic exception
* Subscribe share name exception
* Client connect exception

Also note that topic exceptions may use [substitution variables](https://docs.solace.com/Security/Granting-Clients-Access.htm#Using), which will also be demonstrated.

## Module Configuration in the Example

### Required Inputs

* `msg_vpn_name` - Set to `default` in the example.
* `client_identifier_type` - Set to `client_username`.
* `client_identifier_name` - Set to `myclient` in the example.
* `client_profile_name` - Set to `default` in the example.
* `acl_profile_name` - Set to `default` in the example. The "default" ACL profile's default actions are "allow", so all exceptions defined will be denied.

### Optional Inputs

* `acl_profile_publish_topic_exceptions`, `acl_profile_subscribe_topic_exceptions`, `acl_profile_subscribe_share_name_exceptions`, `acl_profile_client_connect_exceptions` - examples show how to define them in a list form.

Optional module input variables have the same name as the attributes of the underlying provider resource. If omitted, then the default for the related resource attribute will be configured on the broker. For a list of attributes and the corresponding defaults, see the [documentation of "solacebroker_msg_vpn_client_username"](https://registry.terraform.io/providers/SolaceProducts/solacebrokerappliance/latest/docs/resources/msg_vpn_client_username#optional).

The module default for the `enabled` variable is true, which enables the client username.

### Output

The module `client_username` output refers to the created client username and the exceptions outputs provide the list the created exceptions.

## Created Resources

This example will create the following resources:

* `solacebroker_msg_vpn_client_username`
* `solacebroker_msg_vpn_acl_profile_publish_topic_exception`
* `solacebroker_msg_vpn_acl_profile_subscribe_topic_exception`
* `solacebroker_msg_vpn_acl_profile_subscribe_share_name_exception`
* `solacebroker_msg_vpn_acl_profile_client_connect_exception`

## Running the Example

### Access to a PubSub+ Appliance

If you don't already have access to a broker, see the [Developers page](https://www.solace.dev/) for options to get started.

### Sample Source Code

The sample is available from the module GitHub repo:

```bash
git clone https://github.com/SolaceProducts/terraform-solacebrokerappliance-rest-delivery.git
cd examples/acl-profile-exceptions
```

### Adjust the Provider Configuration

Adjust the [provider parameters](https://registry.terraform.io/providers/SolaceProducts/solacebrokerappliance/latest/docs#schema) in `main.tf` according to your broker. The example configuration shows settings for a local broker running in Docker.

### Create the Resource

Tip: You can verify configuration changes on the broker, before and after, using the [PubSub+ Broker Manager Web UI](https://docs.solace.com/Admin/Broker-Manager/PubSub-Manager-Overview.htm).

Execute from this folder:

```bash
terraform init
terraform plan
terraform apply
```

Run `terraform destroy` to clean up the created resources when they are no longer needed.

## Additional Documentation

For more information, see [Configuring Client Authorization](https://docs.solace.com/Security/Configuring-Client-Authorization.htm) section in the PubSub+ documentation.
