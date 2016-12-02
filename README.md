
```
% git clone this repository 
% docker-compose build
% docker-compose up -d
% docker-compose exec web /bin/bash
# go run tools/init.go 
# bash ./build.sh
```

Intellij IDEAで使うためには

```
% docker cp web:/usr/local/go/ golang/
```