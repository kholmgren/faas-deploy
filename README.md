# faas-deploy

```bash
./deploy.sh https://github.com/kholmgren/contact-functions.git run
```

```bash
ENVOY=$(kc get service envoy -o=jsonpath='{.status.loadBalancer.ingress[0].ip}')
echo "ENVOY: $ENVOY"

INVOKER=$(kc get service invoker -o=jsonpath='{.status.loadBalancer.ingress[0].ip}')
echo "INVOKER: $INVOKER"

http $INVOKER
http $INVOKER/ping
http $INVOKER/update Authorization:user1 id=123 name=kjell


```

