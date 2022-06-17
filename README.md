# Element Management System on Docker-compose

## Services

- EMS's Backend: `http://localhost:8080`
- EMS's Frontend: `http://localhost:3000`
- Keycloak: `http://localhost:4000`
- MySQL database for EMS: `http://localhost:3306`
- Postgres database for Keycloak: `http://localhost:5432`

## Instruction to run

### Precondition

- Make sure you have docker and docker-compose
- Enable Docker Build kit in your system: `export DOCKER_BUILDKIT=1`
- You can change services' ports in `docker-compose.yaml` file to avoid conflict, but remember to check for service configuration
- Copy `.env.example` file in ems-frontend to `.env` and adjust the values

### Run steps

- **Step 1:** Build and start the services  
  Run
  ```
  docker compose up --build -d
  ```
  to build and start services. Running this step the first time will take 5-10 minutes based on the system specs. Next time building, the dependencies for Backend is cached and won't be downloaded again
- **Step 2:** Verify  
  Check if the system is fully running by using `docker ps`. If you can see all 5 services. Congrats! If not, try running the above step again
- **Step 3:** Setup Keycloak admin account
  We will need an admin account to access the admin UI.
  Run:

  ```
  docker exec ems-keycloak /opt/jboss/keycloak/bin/add-user-keycloak.sh -u admin -p admin && docker restart ems-keycloak
  ```

to create an admin with `admin/admin` credential.  
By default, Keycloak is hosted at `http://localhost:4000`. Access this URL and you should be able to login using the above username and password

- **Step 4:** Setup auth realm  
  Import the file `reals-export.json`, Keycloak will create a realm with roles and clients for you.

- **Step 5:** Create users
  EMS has 2 roles: admin and viewer. Go to tab `Users` to create a user and assign it a role. Remember to setup the password also.

You should be able to use the app now. Access the frontend and enjoy!
