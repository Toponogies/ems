# Element Management System on Docker-compose

## Services

- EMS's Backend: `http://localhost:8080`
- EMS's Frontend: `http://localhost:3000`
- Keycloak: `http://localhost:5000`
- MySQL database for EMS: `http://localhost:3306`
- Postgres database for Keycloak: `http://localhost:5432`

## Instruction to run

### Precondition

- Make sure you have docker and docker-compose
- Enable Docker Build kit in your system: `export DOCKER_BUILDKIT=1`
- You can change services' ports in `docker-compose.yaml` file to avoid conflict, but remember to check for service configuration
- Copy `.env.example` file in ems-frontend to `.env`

### Run steps
- **Step 1:** Setup host
  There are 2 cases:
  - If you are using Docker desktop, ignore this step
  - If you are using Docker-CE, edit `/etc/hosts` (if on Ubuntu), add `172.17.0.1      host.docker.internal`

- **Step 2:** Build and start the services  
  Run
  ```
  docker compose up --build -d
  ```
  to build and start services. Running this step the first time will take 5-10 minutes based on the system specs. Next time building, the dependencies for Backend is cached and won't be downloaded again
- **Step 3:** Verify  
  Check if the system is fully running by using `docker ps`. If you can see all 5 services. Congrats! If not, try running the above step again
- **Step 4:** Login into Keycloak with admin account  
  By default, Keycloak is hosted at `http://localhost:5000`. Access this URL and you should be able to login using `admin/admin`  
- **Step 5:** Setup auth realm  
  Import the file `reals-export.json`, Keycloak will create a realm with roles and clients for you.  
- **Step 6:** Create users
  EMS has 2 roles: admin and viewer. Go to tab `Users` to create a user and assign it a role. Remember to setup the password also.

You should be able to use the app now. Access the frontend and enjoy!
