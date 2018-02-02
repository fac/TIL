**Background**

* [Triton][triton-cloud] is the Joyent SmartOS-powered cloud software.
* [triton][triton-npm] npm package is a cli tool to talk to the Triton cloud api

**`triton ssh`**

One of the things the triton tool makes easy is SSHing to an instance, given it's name.

You can just run `triton ssh <alias>` and it will look up `alias`'s IP and invoke `ssh` to get you into it.

If you want to pass additional arguments to ssh, you can just append them to the end of `triton ssh` command.

To forward your agent for instance:

```bash
triton ssh caius1 -A
```

[triton-cloud]: https://www.joyent.com
[triton-npm]: https://www.npmjs.com/package/triton
