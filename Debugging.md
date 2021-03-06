# Debugging your tests

## Development Environments

### Goland
* To run specific test change the value for `ginkgo.focus=`
* To run all tests (may take a long time) do not set a value for `ginkgo.focus`
![goland ide debug settings](goland_ide_debug_settings.png "goland ide debug settings")

### Visual Studio Code
Microsoft already has [excellent general guidance](https://github.com/Microsoft/vscode-go/wiki/Debugging-Go-code-using-VS-Code) for debugging Go in VS Code. Below is an example 
of how to set this up specifically for these BDD tests.

1. From the drop-down menus, select _Debug_ --> _Open Configurations_. This should create a `launch.json` file for you, if there wasn't one already set up.

2. Some of the default settings for this file will be fine, but others need to be changed. This is especially true if you want to test against particular repositories. VS Code's Intellisense feature will let you hover over these settings and see possibilities. 

3. This file should also contain the environment variables you'd set up were you running the tests outside of VS Code. 

Below is an example file, showing a debug configuration called __node-http__. where the node-http test will be run using the following options. 
```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "node-http",
            "type": "go",
            "request": "launch",
            "mode": "test",
            "program": "${fileDirname}",
            "env": {
                "GIT_ORGANISATION":"your-organisation",
                "GINKGO_ARGS":"-v"
            },
            "args": [
                "-test.v",
                "-ginkgo.slowSpecThreshold=50000",
                "-ginkgo.focus",
                "node-http"
            ]
        }
    ]
}
```