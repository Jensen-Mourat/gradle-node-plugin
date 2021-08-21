# About this fork

This is a fork of https://github.com/srs/gradle-node-plugin. Its a gradle great plugin, however it does not work when integrated with InterShop 7.10 and it also does not work when a project uses gradle 6. 

The plugin fails to download the nodejs file from any nodejs dist repository (or mirror) because it keeps looking for an ivy.xml file which is not available for a nodejs artifact. After days of looking for an alternative plugin or solution to run node using gradle, I was forced to get my hands dirty and try to fix this plugin.

# IMPORTANT 

This fix was only tested with having the `download=true` for the node configuration.
**Also I neither want nor have the time to publish this fork as a gradle plugin in the gradle plugins repository. Please see how to use this fork below.**

# How to use this fork

Download the jar in the `plugin-jar` folder. Or you can clone or download the repo, use `gradlew build` and then copy the jar from `./build/libs/`

Add it to your build.gradle as follows:

```
buildscript {
    dependencies {
        classpath files('gradle-node-plugin-1.4.0-fixed.jar')
    }
}

apply plugin: 'com.moowork.node'

```

Dont forget to set up the node config in your build.gradle

```
node {
    distBaseUrl = 'https://nodejs.org/dist/ or <Your_Mirror>'
    version = '<Any_Node_Version>'
    download = true
    workDir = file("node/node_install") // example path
    npmWorkDir = file("node/node_install")  // example path
    nodeModulesDir = file("node") // example path
  }

task npmCI(type: NpmTask) { // example npm ci task
      args = ['ci']
}

task test(type: NpmTask, dependsOn: npmCI) { // here is an example of how an npm script is run. This will run "npm run test" 
      args = ['run', 'test']
}
```
For more information on this plugin please check:

https://github.com/srs/gradle-node-plugin

## License

```
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
