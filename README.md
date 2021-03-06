# faas-deploy

Build and deploy the function pod:
```bash
./deploy.sh https://github.com/kholmgren/contact-functions.git run
```

Test the function pod:
```bash
INVOKER=$(kc get service invoker -o=jsonpath='{.status.loadBalancer.ingress[0].ip}')
echo "INVOKER: $INVOKER"

http $INVOKER/create Authorization:user1 name=kjell

http $INVOKER/update Authorization:user1 id=8742736d-cf52-41ad-82df-0619e8621b7f name=otto

```

Delete the function pod:
```bash
./deploy.sh https://github.com/kholmgren/contact-functions.git delete
```
