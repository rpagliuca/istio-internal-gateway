First, exec into the curl pod:

    kubectl exec -ti -n outsidemesh $(kubectl get pod -n outsidemesh -l app=curl -o name) sh

Then run the following experiments from within the pod:

    # Should return a regular 301
    curl google.com -D -

    # Should still return a regular 301, because we are outside of the mesh
    curl google.com -D - -Hx-my-custom-header:my-custom-value

    # We are now proxying the traffic through the ingress, but still should see a regular 301 for the last time
    curl istio-ingressgateway.istio-system.svc.cluster.local -HHost:google.com -D -

    # Now we are through the ingress, and also sending the magic cookie. We will get the mocked response.
    curl istio-ingressgateway.istio-system.svc.cluster.local -HHost:google.com -D - -H "x-my-custom-header:my-custom-value"
