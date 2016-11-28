# Secure Headers
Secure headers are curiously obeyed by different browsers.

For instance, a `send_data disposition: inline` would fail to download a PDF on Chrome but pass on Firefox.

To allow this to pass, ensure you set the correct plugin_types allowed in the `config/initializers/secure_headers.rb`, in the instance above 'application/pdf' should be appended
