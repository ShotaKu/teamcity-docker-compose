# MEMO for personal use

Complete reference is [here](https://github.com/Egregors/teamcity-docker-compose)

1. Clone repository
    
    ```CMD
    git clone https://github.com/Egregors/teamcity-docker-compose.git
    ```

2. rename `env.example` to `.env`
3. Change password and username for database

    ```
    POSTGRES_PASSWORD=mysecretpass  //password
    POSTGRES_USER=postgresuser      //user

    SERVER_URL=http://teamcity-server:8111
    ```

4. Build
    ```CMD
    cd teamcity-docker-compose
    docker-compose build
    ```

5. Create container

    ```CMD
    docker-compose up
    ```

6. Go to http://localhost:8111/
7. Select **PostgreSQL** for database type
8. Click Refresh JDBC drivers
9. Fill database informations
 - Database host[:host]: postgres
 - Database name: ""(empty)
 - User name: user
 - Password: password
10. Auth agent

Option: Scaling your workers

  ```CMD
  docker-compose scale teamcity-agent=3
  ```

No docker-compose method is [here](https://github.com/ShotaKu/teamcity-docker-compose/blob/master/MEMO.md)