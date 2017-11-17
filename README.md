jeffbr13.ipfs
=============

Installs and configures the [`go-ipfs`](https://github.com/ipfs/go-ipfs) daemon with automatic forward-migration.

Unique node IDs and private keys must be configured per-host.


Requirements
------------

- Ansible 2.2 (for service.use option)


Role Variables
--------------

The IPFS peer ID and private key must be for each host in `host_vars`.

```yaml
ipfs_peer_id: ""      # see below
ipfs_private_key: ""  # ipfs-key | base64
```

You can produce valid values for `ipfs_peer_id` and `ipfs_private_key` by running `ipfs-key | base64 -w 0` (see [whyrusleeping/ipfs-key][]).

The following variables can also be set across the playbook:

```yaml
ipfs_dist_url: https://dist.ipfs.io
ipfs_version: v0.4.11
ipfs_arch: amd64
ipfs_http_api_listen_multiaddress: /ip4/127.0.0.1/tcp/5001
ipfs_http_gateway_listen_multiaddress: /ip4/127.0.0.1/tcp/8080
ipfs_storage_max: 10GB
```

The HTTP control API and Gateway addresses are both configured as an [IPFS `multiaddr`][multiaddr].
Remember to also configure your firewall if you're exposing them.


Example Playbook
----------------

```yaml
# playbook.yml

- hosts: ipfs_nodes
  roles:
     - { role: jeffbr13.ipfs, ipfs_arch: arm, ipfs_http_api_listen_multiaddress: /ip4/0.0.0.0/tcp/5001, ipfs_storage_max: 50GB}
```

```yaml
# host_vars/my.host.yml

ipfs_peer_id: Qmagy4195bsbR6YmqwKUtj7j65QdnyDiH3uzVYB8F46r6j
ipfs_private_key: CAASqAkwggSkAgEAAoIBAQDB7ltlNV4QysC3m0HOySU2jjxnmrjZmOX8vi9UU/E6xu+3S6wCe/f1bxVATgqfHMXU4Sk5g4pmM3YocadrMe/WzeSLKGB0QPgcKAtcuBJZO8vQEWmMDxrFg/pOd4Z2LIrLKIQDeRmhBhMmIWQ/M8FNVhzSv6gVs0+X72ZwMQgJ8N5IiJBtzfT0CRddsHaSqiwvRPS2bJSuSUi0Vq1l4+I6sHyP7WgE9IrUQSMVHw3kiKgk8bWKEbW8p5GWXbdYPOfGr+YUd3GtEVvkrpo0OAZcA6H+1DqNAqAQdLu47pA7pzZW4C3nxwisN1wYoEbkE+qXpJQft4+58N1ZAkULbzu/AgMBAAECggEAAnTAV5HLdS78LdcbiEDn5b77aNx+xtK25vKJqum9Pl9SneGpdgaX51XW0Q+r9sPohX+sg/v0fsLcFjsKQcNKJFBLOq/yOMax3blsG2qBYPvu4t21ln6Ceknnm6LL4ydBQr1qnpikCHQJPgxiNqKzKgWTK+AdgtjYgzYW+AjG70lF+t450PtEp2NSPUsYB3EIUTRaPpQeKIQ3z71DkpjReuQ//P+PLLj7/4qzyHH1hkhHP6AgjwCetzH+Tlor0rigpkqY1QTycPmEXoQ5oekEIpGiVaX4LtymHWSIHW/FFEb5dODECwQtLRMulJpu4y86DfAySb9jwfn2JA9NQh5boQKBgQDI7a7DQBP6oJtfmwRhxonMO2L0czTIgZEl32E3JWx49ZY+xnAIvpUB3MZZqAX4vrb8uuvpv2ced4eeSyBAFJHOX8pEpEIfmgV7eg42xMPWr6l4DeXY3sC1SaXUWIzoSQLosD8kBopQNFemskmq5m5/eAdDxLZFa4K27BmmITf9hwKBgQD3FbK6TNoq2yWoxByPY4xmqkTeqh+DME3vBzXUDv8ZKqkVTkF7kFkk3zSsFFk/BS+UALsZKyarERbZ5U9NCscNZeVIukztjJUGCPpntjGM8r8NK3CXtWc+qGHewAgNGXzn6cyNVv29olPJNK0gvDkVou4NwEVMWjzDuFaiLZKeCQKBgQC0Mm1UUCha0iTmBilU4vB8CBqD7ro8w+5/j6kpAtgYVu/q1p5tSTZrWCtPBuBsJ+YGHEEs/eomKb6n2OpQbeIhuki1bLacjs4x4dHTjn2wERQkRhqHd6ZOL4GYQd4FCE2ij0XhMjhjG74sEqL8sPISQXwKa+WntnahRHbwRcRoCwKBgQCERqR5Ih2F5e5iTCLyDJwkdjEKd08Jf3mpZlXF4gVlZrZARrW9vchLegcLvJUOrOsMs9t2HOjFmg9+tUlf+E4Z+RvndH0six9YrMPJc/tQ9r+bAE91mFLec2x5wJpO0P9SdJLic9jBhb6PL9kjdkClOaVxzSYMOx7etLgEeJtOaQKBgAVYOsf2EA3aoukh6mPTKVfKaV71mFRhIPcbT0mADaJ7mYh0fSV/FHahwRioKfweTFNEFVO15x97acBbfInA/ZARc+N08IKVfwr+vopcefXEqgE0PMGsI/fFduXYBbprdns62qGrEYAJkNE8E34AM2Afh9sWt9PJdUYpBagHc+dL
```


License
-------

MIT


Author Information
------------------

This is an Ansible Galaxy distributable role based on <https://github.com/hsanjuan/ansible-ipfs-cluster>.



<!-- references -->
[whyrusleeping/ipfs-key]: https://github.com/whyrusleeping/ipfs-key
[multiaddr]: https://multiformats.io/multiaddr/
