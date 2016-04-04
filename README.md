# Nulecule library

This library contains a set of working examples of composite container applications. The applications are specified using the [Nulecule](https://github.com/projectatomic/nulecule) Specification. This specification allows for reusable components and defines a full multi-container application. You may use the applications for reference or, in some cases, deployment.

These examples are all intended to be used with [atomicapp](https://github.com/projectatomic/atomicapp). There is a thorough [getting started guide](https://github.com/projectatomic/atomicapp/blob/master/docs/start_guide.md) available.

### Library format

__Files:__

Please only include the `/artifact` directory and the Nulecule, Dockerfile and README.md files in your nulecule.

__ex. projectatomic/helloapache:__

```sh
.
├── artifacts
│   ├── docker
│   │   └── hello-apache-pod_run
│   ├── kubernetes
│   │   └── hello-apache-pod.json
├── Dockerfile
├── Nulecule
└── README.md
```

README.md description:

  1. Description: What the application does
  2. Deployment: How to deploy the application using the `atomic` or `atomicapp` CLIs
  3. Interaction: How to access/use the application after deployment

### Contributing

Feel free to open a PR if you wish to contribute to the nulecule-library! We accept all kind of applications.


### Communication channels

* IRC: #nulecule (On Freenode)
* Mailing List: [container-tools@redhat.com](https://www.redhat.com/mailman/listinfo/container-tools)
