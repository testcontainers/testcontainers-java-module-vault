# TestContainers Vault Module

Testcontainers module for [Vault](https://github.com/hashicorp/vault). Vault is a tool for managing secrets. More information on Vault [here](https://www.vaultproject.io/).

See [testcontainers.org](https://www.testcontainers.org) for more information about Testcontainers.

<!--[![Build Status](https://travis-ci.org/testcontainers/testcontainers-java-module-vault.svg?branch=master)](https://travis-ci.org/testcontainers/testcontainers-java-module-vault)-->

## Usage example

Running Vault in your Junit tests is easily done with an @Rule or @ClassRule such as the following:

```java
public class SomeTest {

    @ClassRule
    public static VaultContainer vaultContainer = new VaultContainer<>()
            .withVaultToken("my-root-token")
            .withVaultPort(8200)
            .withSecretInVault("secret/testing", "top_secret=password1","db_password=dbpassword1");
    
    @Test
    public void someTestMethod() {
       //interact with Vault via the container's host, port and Vault token. 
       
       //There are many integration clients for Vault so let's just define a general one here:
       VaultClient client = new VaultClient(
               vaultContainer.getContainerIpAddress(),
               vaultContainer.getMappedPort(8200),
               "my-root-token");
       
       List<String> secrets = client.readSecret("secret/testing");
       
    }
```

## Why Vault in Junit tests?

With the increasing popularity of Vault and secret management, applications are now needing to source secrets from Vault.
This can prove challenging in the development phase without a running Vault instance readily on hand. This library 
aims to solve your apps integration testing with Vault. You can also use it to
test how your application behaves with Vault by writing different test scenarios in Junit.

## License

See [LICENSE](LICENSE).

## Copyright

Copyright (c) 2017 Capital One Services, LLC and other authors.

See [AUTHORS](AUTHORS) for contributors.
