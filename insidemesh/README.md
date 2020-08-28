First, exec into the curl pod:

    kubectl exec -ti -n insidemesh $(kubectl get pod -n insidemesh -l app=curl -o name) sh

Then run the following experiments from within the pod:

    # Should return a regular 301
    curl google.com -D -

    # Should return mocked local service response
    curl google.com -D - -Hx-my-custom-header:my-custom-value
