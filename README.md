# Solo CI

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/solo-ci/Lobby)

### Description

[中文版](README-CN.md)

A lightweight golang CI/CD tools, you only need write a simple config, it will clone, build, test, deploy

```json
{
  "get_list":[
    "github.com/asaskevich/govalidator"
  ],
  "zip_list":[
    "conf"
  ],
  "after_script":"echo hello",
  "before_script":"pwd"
}
```

### Features

- Support Gitlab, Github（application/json） webhook
- Only need very small memory and cpu, it can run on every Linux host
- You only need to start it ,it will get the env auto.
- The simple config, if you want, you don't need to write it.
- Auto clone, buil, test, clean, tar
- Support after script and before script, it will run on the project path
- Support REST API
- Every build will be saved

### Use

1. go get github.com/astaxie/beego  go get github.com/mattn/go-sqlite3  go get github.com/satori/go.uuid
2. GOPATH，GOROOT，GIT
3. Download solo-ci binary
4. Use REST API new a ci project
5. Write a config and configure your webhook
6. push!
7. The Build will save at workspace dir.
8. go-sqlite3 requires gcc pre-installed. use "sudo apt-get install build-essential" to install gcc if necessary

### REST API

| Method | Url                                      | Params                                   | Description      |
| :----: | :--------------------------------------- | :--------------------------------------- | :--------------- |
|  POST  | http://your-ip:13233/v1/solohook/:project_id | - project_id(path)                       | Run Webhook      |
|  POST  | http://your-ip:13233/v1/project          | - name(form)                             | New a project    |
|        |                                          | - type(form, gitlab or github or bitbucket) |                  |
|        |                                          | - url(form)                              |                  |
|        |                                          | - path(form，the position of solo-ci.json) |                  |
|        |                                          | - branch(form)                           |                  |
|        |                                          | - secret_token(form,not necessary)       |                  |
|        |                                          | - main_path(form,the position of main.go) |                  |
| DELETE | http://your-ip:13233/v1/project/:project_id | - project_id(path)                       | Delete project   |
|  PUT   | http://your-ip:13233/v1/project/:project_id | - project_id(path)                       | Update Project   |
|        |                                          | - name(form)                             |                  |
|        |                                          | - type(form, gitlab or github) |                  |
|        |                                          | - url(form)                              |                  |
|        |                                          | - path(form，the position of solo-ci.json) |                  |
|        |                                          | - branch(form)                           |                  |
|        |                                          | - secret_token(form,not necessary)       |                  |
|  GET   | http://your-ip:13233/v1/project/:project_id | - project_id(path)                       | Get Project Info |
|  GET   | http://your-ip:13233/v1/project          | - project_id(path)                       | Get project list |
|        |                                          | - page (default 0)                       |                  |
|        |                                          | - pageSize(default 20)                   |                  |

### Config solo-ci.json

- get_list：the go get list
- zip_list：the file you want to tar
- before_script：it will run before build
- after_script：it will run after build

If you don't want to write a config, you can write a blank config.

```json
{

}
```

### Next

- Support Web GUI
