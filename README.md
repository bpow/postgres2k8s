# Config setup to migrate existing postgresql db to kubernetes

Well, really this is to keep track of what I did for one particular database...

This uses the [bitnami postgresql chart](https://github.com/bitnami/charts/tree/master/bitnami/postgresql/), so
first you need to add the repo if you haven't done so already:

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

Then, install the chart using both the `config-values.yaml` options (which I'm OK for you to see) and some
secrets as well. Mine are protected by git-crypt... you'll have to include some of your own, but the
`example-secret-values.yaml` shows what you need-- a password (matching for the postgres user between the
old and new db). The `primary.initdb.scripts` option takes care of dumping the old db and loading here.

So, the *TL;DR* is, come up with a release name and run:

```bash
helm install -f config-values.yaml -f secret-values.yaml release-name bitnami/postgresql
```


*TODO:* Maybe this could be made into its own chart with `bitnami/postgresql` as a subchart. I couldn't make
that work with the minimal effort I put into it, and more effort may not be worth it, because this appears
to work.
