build dockerfile
```bash
docker build -t mytagname -f Dockerfile .
docker build -t mytagname -f Dockerfile --platform=linux/amd64 .
```



run
`docker run mytagname`

retag
`docker tag mytagname mynewtagname`

simple mount current dir
`docker run -v.:/pathincontainer`
