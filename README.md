# Spider Devops Inductions - Task 2

## Steps to Run
1. Clone the repo
2. Cd into the dir
3. Ensure docker is installed and the engine is running, and make sure port 4000 and 4001 is free.
4. Run `docker compose up --build`

## Access the App
1. Checkout `http://localhost:4000` on your host device for the frontend and `http://localhost:4001` for the backend.
2. Frontend is running in dev mode with proxy to `http://localhost:4001`
3. Backend and Pgsql containers are also running, all in the same network

## Troubleshooting
- If frontend, backend or db is not running, run `docker ps -a` to check if all containers are running.
- If they're running, check logs or exec into the containers to see if its running locally
- If backend is not running, run `docker ps -a | grep backend`, copy the backend container id and run `docker start <id>`

## Challenges
- Rust image building took 2 mins every time. Thanks for the rust compiler.
- I saw the proxy mentioned in the Frontend/package.json, I understood it was mentioned for a reason and I didn’t remove it. The proxy only works in development mode (i.e running npm run start). If I build for production, I’ll have to serve the static build folder and no more proxy. To fix this,
  - 2.1 Replace all requests to the backend in frontend code with backend:8080 (IP will be resolved by docker resolver)
  - 2.2 Or setup nginx container to serve the builds and proxy requests to backend to the backend
- Took some time to understand that localhost:8080 proxy in the frontend container will not reach the backend unless it is changed to backend:8080 in package.json proxy
- Backend sometimes starts before db and fails to connect. So I setup Health Checks on the db container and made the backend depend on the db.
