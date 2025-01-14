After maybe 4 to 5 hours of "node ./scripts/watch-js/" command running on the Jetson the followign error occurred:
```
blaze@divinci:~/Desktop/server$ node ./scripts/watch-js/
Watching resource modules [models, server-globals, server-models, server-permissions, server-tools, server-utils, tools, utils]
updatedResources: [ '/home/blaze/Desktop/server/workspace/resources/models' ]
Visiting /home/blaze/Desktop/server/workspace/resources/models
Dep /home/blaze/Desktop/server/workspace/resources/utils has deps []
Visiting /home/blaze/Desktop/server/workspace/resources/server-globals
Dep /home/blaze/Desktop/server/workspace/resources/models has deps [ '/home/blaze/Desktop/server/workspace/resources/utils' ]
Dep /home/blaze/Desktop/server/workspace/resources/utils has deps []
Dep /home/blaze/Desktop/server/workspace/resources/server-utils has deps [ '/home/blaze/Desktop/server/workspace/resources/utils' ]
Dep /home/blaze/Desktop/server/workspace/resources/utils has deps []
Dep /home/blaze/Desktop/server/workspace/tarballs/openai-4.73.0.tgz has deps []
Visiting /home/blaze/Desktop/server/workspace/resources/server-models
Dep /home/blaze/Desktop/server/workspace/resources/models has deps [ '/home/blaze/Desktop/server/workspace/resources/utils' ]
Dep /home/blaze/Desktop/server/workspace/resources/server-globals has deps [
  '/home/blaze/Desktop/server/workspace/resources/models',
  '/home/blaze/Desktop/server/workspace/resources/server-utils',
  '/home/blaze/Desktop/server/workspace/resources/utils',
  '/home/blaze/Desktop/server/workspace/tarballs/openai-4.73.0.tgz'
]
Dep /home/blaze/Desktop/server/workspace/resources/models has deps [ '/home/blaze/Desktop/server/workspace/resources/utils' ]
Dep /home/blaze/Desktop/server/workspace/resources/server-globals has deps [
  '/home/blaze/Desktop/server/workspace/resources/models',
  '/home/blaze/Desktop/server/workspace/resources/server-utils',
  '/home/blaze/Desktop/server/workspace/resources/utils',
  '/home/blaze/Desktop/server/workspace/tarballs/openai-4.73.0.tgz'
]
Dep /home/blaze/Desktop/server/workspace/resources/server-utils has deps [ '/home/blaze/Desktop/server/workspace/resources/utils' ]
Dep /home/blaze/Desktop/server/workspace/resources/utils has deps []
Dep /home/blaze/Desktop/server/workspace/tarballs/openai-4.73.0.tgz has deps []
Dep /home/blaze/Desktop/server/workspace/resources/server-tools has deps [
  '/home/blaze/Desktop/server/workspace/resources/models',
  '/home/blaze/Desktop/server/workspace/resources/server-globals',
  '/home/blaze/Desktop/server/workspace/resources/server-utils',
  '/home/blaze/Desktop/server/workspace/resources/utils',
  '/home/blaze/Desktop/server/workspace/tarballs/openai-4.73.0.tgz'
]
Dep /home/blaze/Desktop/server/workspace/resources/server-utils has deps [ '/home/blaze/Desktop/server/workspace/resources/utils' ]
Dep /home/blaze/Desktop/server/workspace/resources/models has deps [ '/home/blaze/Desktop/server/workspace/resources/utils' ]
Dep /home/blaze/Desktop/server/workspace/resources/utils has deps []
Dep /home/blaze/Desktop/server/workspace/resources/tools has deps [
  '/home/blaze/Desktop/server/workspace/resources/models',
  '/home/blaze/Desktop/server/workspace/resources/utils'
]
Dep /home/blaze/Desktop/server/workspace/resources/utils has deps []
Visiting /home/blaze/Desktop/server/workspace/resources/server-permissions
Dep /home/blaze/Desktop/server/workspace/resources/models has deps [ '/home/blaze/Desktop/server/workspace/resources/utils' ]
Dep /home/blaze/Desktop/server/workspace/resources/server-globals has deps [
  '/home/blaze/Desktop/server/workspace/resources/models',
  '/home/blaze/Desktop/server/workspace/resources/server-utils',
  '/home/blaze/Desktop/server/workspace/resources/utils',
  '/home/blaze/Desktop/server/workspace/tarballs/openai-4.73.0.tgz'
]
Dep /home/blaze/Desktop/server/workspace/resources/server-models has deps [
  '/home/blaze/Desktop/server/workspace/resources/models',
  '/home/blaze/Desktop/server/workspace/resources/server-globals',
  '/home/blaze/Desktop/server/workspace/resources/server-tools',
  '/home/blaze/Desktop/server/workspace/resources/server-utils',
  '/home/blaze/Desktop/server/workspace/resources/tools',
  '/home/blaze/Desktop/server/workspace/resources/utils',
  '/home/blaze/Desktop/server/workspace/tarballs/openai-4.73.0.tgz'
]
Dep /home/blaze/Desktop/server/workspace/resources/server-utils has deps [ '/home/blaze/Desktop/server/workspace/resources/utils' ]
Dep /home/blaze/Desktop/server/workspace/resources/utils has deps []
Visiting /home/blaze/Desktop/server/workspace/resources/server-tools
Visiting /home/blaze/Desktop/server/workspace/resources/tools
Running prepare in modules serially: [
  '/home/blaze/Desktop/server/workspace/resources/models',
  '/home/blaze/Desktop/server/workspace/resources/server-globals',
  '/home/blaze/Desktop/server/workspace/resources/server-tools',
  '/home/blaze/Desktop/server/workspace/resources/tools',
  '/home/blaze/Desktop/server/workspace/resources/server-models',
  '/home/blaze/Desktop/server/workspace/resources/server-permissions'
] undefined
Running 'npm run prepare' in /home/blaze/Desktop/server/workspace/resources/models
Running 'npm run prepare' in /home/blaze/Desktop/server/workspace/resources/server-globals
Running 'npm run prepare' in /home/blaze/Desktop/server/workspace/resources/server-tools
Running 'npm run prepare' in /home/blaze/Desktop/server/workspace/resources/tools
Running 'npm run prepare' in /home/blaze/Desktop/server/workspace/resources/server-models
Running 'npm run prepare' in /home/blaze/Desktop/server/workspace/resources/server-permissions
Running prepare in modules in parallel [
  '/home/blaze/Desktop/server/workspace/clients/tests',
  '/home/blaze/Desktop/server/workspace/clients/web',
  '/home/blaze/Desktop/server/workspace/clients/embed'
] CLIENTS
Running 'npm run prepare' in /home/blaze/Desktop/server/workspace/clients/tests
Running 'npm run prepare' in /home/blaze/Desktop/server/workspace/clients/web
Running 'npm run prepare' in /home/blaze/Desktop/server/workspace/clients/embed
Running prepare in modules in parallel [
  '/home/blaze/Desktop/server/workspace/servers/public-api',
  '/home/blaze/Desktop/server/workspace/servers/public-api-live',
  '/home/blaze/Desktop/server/workspace/servers/public-api-webhook',
  '/home/blaze/Desktop/server/workspace/servers/test-api'
] SERVERS
Running 'npm run prepare' in /home/blaze/Desktop/server/workspace/servers/public-api
Running 'npm run prepare' in /home/blaze/Desktop/server/workspace/servers/public-api-live
Running 'npm run prepare' in /home/blaze/Desktop/server/workspace/servers/public-api-webhook
Running 'npm run prepare' in /home/blaze/Desktop/server/workspace/servers/test-api
node:internal/errors:983
  const err = new Error(message);
              ^

Error: Command failed: docker compose ls --format json
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.47/containers/json?filters=%7B%22label%22%3A%7B%22com.docker.compose.config-hash%22%3Atrue%2C%22com.docker.compose.project%22%3Atrue%7D%7D": dial unix /var/run/docker.sock: connect: permission denied

    at genericNodeError (node:internal/errors:983:15)
    at wrappedFn (node:internal/errors:537:14)
    at ChildProcess.exithandler (node:child_process:414:12)
    at ChildProcess.emit (node:events:513:28)
    at maybeClose (node:internal/child_process:1101:16)
    at Socket.<anonymous> (node:internal/child_process:457:11)
    at Socket.emit (node:events:513:28)
    at Pipe.<anonymous> (node:net:350:12) {
  code: 1,
  killed: false,
  signal: null,
  cmd: 'docker compose ls --format json',
  stdout: '',
  stderr: 'permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.47/containers/json?filters=%7B%22label%22%3A%7B%22com.docker.compose.config-hash%22%3Atrue%2C%22com.docker.compose.project%22%3Atrue%7D%7D": dial unix /var/run/docker.sock: connect: permission denied\n'
}

Node.js v23.3.0
```
