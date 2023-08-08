# Reproduction for https://github.com/vercel/next.js/issues/53171

This is only the default reproduction template, the Dockerfile of the with-docker example and the next.js config changed to `output: 'standalone'`. No other changes were made.

## Steps

1. Clone https://github.com/darthmaim-reproductions/vercel-next.js-53171
2. Run this command to build and start the next.js app in a docker container 
    ```sh
    docker build -t vercel-next.js-53171 . && docker run --rm -p3000:3000 vercel-next.js-53171
    ```
3. Access http://localhost:3000/
4. The server responds with `Internal Server Error`
5. The server logs output
    ```raw
        - ready started server on e68ae5711fa3:3000, url: http://e68ae5711fa3:3000
    Listening on port 3000 url: http://e68ae5711fa3:3000
    - error Failed to handle request for /
    TypeError: fetch failed
        at Object.fetch (node:internal/deps/undici/undici:11576:11)
        at process.processTicksAndRejections (node:internal/process/task_queues:95:5)
        at async invokeRequest (/app/node_modules/next/dist/server/lib/server-ipc/invoke-request.js:21:12)
        at async requestHandler (/app/node_modules/next/dist/server/lib/start-server.js:336:33)
        at async Server.<anonymous> (/app/node_modules/next/dist/server/lib/start-server.js:152:13) {
      cause: Error: connect ECONNREFUSED 127.0.0.1:41303
          at TCPConnectWrap.afterConnect [as oncomplete] (node:net:1495:16) {
        errno: -111,
        code: 'ECONNREFUSED',
        syscall: 'connect',
        address: '127.0.0.1',
        port: 41303
      }
    }
    - error Failed to handle request for /favicon.ico
    TypeError: fetch failed
        at Object.fetch (node:internal/deps/undici/undici:11576:11)
        at process.processTicksAndRejections (node:internal/process/task_queues:95:5)
        at async invokeRequest (/app/node_modules/next/dist/server/lib/server-ipc/invoke-request.js:21:12)
        at async requestHandler (/app/node_modules/next/dist/server/lib/start-server.js:336:33)
        at async Server.<anonymous> (/app/node_modules/next/dist/server/lib/start-server.js:152:13) {
      cause: Error: connect ECONNREFUSED 127.0.0.1:41303
          at TCPConnectWrap.afterConnect [as oncomplete] (node:net:1495:16) {
        errno: -111,
        code: 'ECONNREFUSED',
        syscall: 'connect',
        address: '127.0.0.1',
        port: 41303
      }
    }
    ```
