# How to test TeamCity with Docker in local machine
## Set up local machine
1. Install TeamCity by using Docker
    Open CMD/CLI and run following command

    ```CMD
    cd <directory path>
    mkdir teamcity
    cd teamcity
    mkdir data
    mkdir logs
    docker run -d --name tc-01
    -v <data directory path>:/data/teamcity_server/datadir
    -v <log directory path>:/opt/teamcity/logs -p 8111:8111 jetbrains/teamcity-server
    ```

    TeamCity downloading will start

2. Open TeamCity WebUI on http://localhost:8111

    1. Press `continue`
    2. Choose internal and press `Build`
    3. Create Administer with username and password
    4. Wait until admin page shown.

3. Create agent in local machine
    1. Open CMD/CLI and run following command
        ```CMD
        cd <teamcity directory path> :: Same directory with step 1
        dir
        ```

    2. check `dir` output. if `teamcity/` directory already have `agent/conf` directory, go to next step. if not, continue with following command

        ```CMD
        mkdir agent
        cd agent
        mkdir conf
        ```

    3. Run following command to make agent

        ```CMD
        docker run -d -e SERVER_URL= <Your IP address not localhost>:8111 --name tc-a-01 
        -v <conf directory path>:/data/teamcity_agent/conf   
        jetbrains/teamcity-minimal-agent
        ```

        TeamCity agent downloading will start
    
    4. Go to admin page of TeamCity WebUI and click `Agent` tab
    5. Click `Unauthorized` tab
    6. Check agent which you created become to `Connected` in step 3 and click `Authorize`
    7. Check the agent go to `Connection` tab

4. Connect Git and TeamCity
    TeamCity can build code in git repository for testing.
    
    1. Click Project tab in admin page of TeamCity WebUI
    2. Click Create Project
    3. Click From Github.com tab 
    4. Click register TeamCity
        1. It will be open github page for authorize third-party Application
        2. Set Application name as TeamCity
        3. Copy HomePage URL in TeamCity to paste github text box
        4. Copy CallbackURL in TeamCity to paste github text box
        5. Click save Register application
        6. Go back to TeamCity WebUI
    5. Click Sign in to Git Hub
        - Click Authorize Application
    6. Choose project that you want to connect
    7. Click Proceed
    8. Wait to detect build steps
    9. Set checkmark to all Build Step
    10. Click Use selected

5. Try run Build apps from Project tab
6. Try change some thing code and push to repository.



