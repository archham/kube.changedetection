# Setup Changedetection on k3s
* https://changedetection.io/

## Prepare config
```
# Project namespace
NAMESPACE=changedetection

# Public URL
FQDN=changedetection.domain.tld
```

## create runtime config from template
```
test -d runtime && echo ERROR remove ./runtime dir first
test -d ./runtime && exit 1
mkdir ./runtime
chmod 700 ./runtime
for y in *.yml
do
  cp -av $y ./runtime/$y
  sed -i "s/__NAMESPACE__/$NAMESPACE/g"      ./runtime/$y
  sed -i "s/__FQDN__/$FQDN/g"                ./runtime/$y
done

echo "# current vars
NAMESPACE=$NAMESPACE
FQDN=$FQDN
" > ./runtime/env.sh

ls -l ./runtime

```
## setup application
```
echo "
DONE

all templates created in ./runtime
please review them and apply config

cd ./runtime/
for y in *.yml
do
  echo $y
  kubectl apply -f $y
done"

```
