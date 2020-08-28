# About

We first customize the regular istio-ingressgateway and change the service type to InternalIP instead of LoadBalancer.

Then we declare two namespaces:

1) insidemesh: Istio sidecar autoinjection is enabled

2) outsidemesh: Autoinjection disabled

Finally we can follow the remainder instructions from insidemesh/README.md and outsidemesh/README.md.
