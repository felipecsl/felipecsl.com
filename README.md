# My personal blog

## Running locally

```
docker build -t felipecsl-com .
docker run -itP --rm --volume="$PWD:/usr/src/app" felipecsl-com
```

## Deploying

Simply push the updated website to master and Github
pages will take care of the rest.
