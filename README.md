# faas-deploy

Build and deploy the function pod:
```bash
./deploy.sh https://github.com/kholmgren/contact-functions.git run
```

Test the function pod:
```bash
ENVOY=$(kc get service envoy -o=jsonpath='{.status.loadBalancer.ingress[0].ip}')
echo "ENVOY: $ENVOY"

INVOKER=$(kc get service invoker -o=jsonpath='{.status.loadBalancer.ingress[0].ip}')
echo "INVOKER: $INVOKER"

http $INVOKER
http $INVOKER/ping
http $INVOKER/update Authorization:user1 id=123 name=kjell

http $ENVOY/create Authorization:user1 name=kjell
http $ENVOY/update Authorization:user1 id=a008897c-1833-4029-8c49-0cc849a3900c name=otto

```

Delete the function pod:
```bash
./deploy.sh https://github.com/kholmgren/contact-functions.git delete
```
