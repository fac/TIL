# Trust Puma-dev Certificates

If your local setup is using `puma-dev` as the webserver you'll likely be
navigating to your local development environment using https://fac.freeagent.dev.

### MacOS

For MacOS we can add the certificate to the keychain.

```bash
security add-trusted-cert -k login.keychain-db ~/Library/Application\ Support/io.puma.dev/cert.pem
```


### Firefox

Firefox might still complain, so here is a manual way to force Firefox to trust a self-signed certificate on FireFox, you'll need to manually install.

Navigate to [about:preferences#privacy](about:preferences#privacy) (Preferences > Privacy & Security) > View Certificates... > Authorities > Import

Open the Folder where the certificate will exist.
```bash
open ~/Library/Application\ Support/io.puma.dev/
```

Drag the `cert.pem` to the file finder and open it.

Choose "Trust certificate can identify websites."
