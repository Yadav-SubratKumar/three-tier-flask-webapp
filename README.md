**To Deploy a three-tier-flask application using Docker**

You need a setup that includes 

1. **Frontend (Web Layer):** Handles the user interface.
2.  **Backend (API):** Manages the request  from frontend and database.
3.  **Database** : store the data

**Prerequisites**

1. Install Docker and Docker Compose.
2. Have the application files ready (e.g., frontend code, backend configuration, database schema).
3.  Prepare a Docker network for inter-container communication
   
**To create the networks**
    `docker network create shop-network`
   
Step 1: For **Frontend Part** 

    
    cd frontend
    docker build -t flask-frontend .
    docker run -d --name frontend --network shop-network -p 80:80 flask-frontend
    
    
Step 2: For **Backend Part**
    
    cd backend
    docker build -t flask-backend .
    docker run -d --name backend-container --network shop-network  -e DB_HOST=database-container -e DB_USER=root -e DB_PASSWORD=rootpassword -e DB_NAME=shopping_db -p 5000:5000  flask-backend

Step 3: For **Database Part**
    
    cd database
    docker build -t flask-database .
    docker run -d --name database-container --network shop-network  -e MYSQL_DATABASE=shopping_db -e MYSQL_ROOT_PASSWORD=rootpassword -p 3306:3306 flask-database                  
                                                       
Step 1: For **By using Compose**
   Using docker-compose.yml `docker compose up -d`
