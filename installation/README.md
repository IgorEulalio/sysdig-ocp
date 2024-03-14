# OpenShift Install

The OpenShift installer `openshift-install` makes it easy to get a cluster
running on the public cloud or your local infrastructure.

To learn more about installing OpenShift, visit [docs.openshift.com](https://docs.openshift.com)
and select the version of OpenShift you are using.

## Installing the tools

After extracting this archive, you can move the `openshift-install` binary
to a location on your PATH such as `/usr/local/bin`, or keep it in a temporary
directory and reference it via `./openshift-install`.

## License

OpenShift is licensed under the Apache Public License 2.0. The source code for this
program is [located on github](https://github.com/openshift/installer).

## How to use

The tool will be default collect metadata from install-config.yaml file. The config backup is at ocp-template.yaml (the apply of the config deletes the config file).
Then it will trigger some terraform, so you must have access to AWS as an admin and also configure your pull secrets so OCP can properly fetch information from RedHat backend.

You can get your pull secret from here after you registered -> https://console.redhat.com/openshift/install/pull-secret

Copy the ocp-template file to a new file:
```
cp ocp-template.yaml install-config.yaml

./openshift-install create cluster --log-level debug
```

## Next steps 
```
# module.vpc.aws_subnet.public[2] will be updated in-place
  ~ resource "aws_subnet" "public" {
        id                                             = "subnet-0f3538802d0c22c44"
      ~ tags                                           = {
            "Blueprint"                            = "sysdig"
            "GithubRepo"                           = "github.com/aws-ia/terraform-aws-eks-blueprints"
            "Name"                                 = "sysdig-public-us-east-1c"
          - "kubernetes.io/cluster/igor-ocp-lzpv2" = "shared" -> null
            "kubernetes.io/role/elb"               = "1"
        }
      ~ tags_all                                       = {
          - "kubernetes.io/cluster/igor-ocp-lzpv2" = "shared" -> null
            # (4 unchanged elements hidden)
        }
        # (15 unchanged attributes hidden)
    }
```

