# RemovePassword Object

* `type` string - `password`.
* `origin` string (optional) - When provided, the authentication info
  related to the origin will only be removed otherwise the entire cache
  will be cleared.
* `scheme` string (optional) - Scheme of the authentication.
  Can be `basic`, `digest`, `ntlm`, `negotiate`. Must be provided if
  removing by `origin`.
* `realm` string (optional) - Realm of the authentication. Must be provided if
  removing by `origin`.
* `username` string (optional) - Credentials of the authentication. Must be
  provided if removing by `origin`.
* `password` string (optional) - Credentials of the authentication. Must be
  provided if removing by `origin`.
