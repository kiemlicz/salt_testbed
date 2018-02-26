# Salt test environment
Docker based master multi-minion environment for salt states testing and experimenting

## Usage
Start the project using docker compose:  
`docker-compose -f docker-compose.yml --project-directory=. up`
 
Minions are automatically accepted using reactor salt system

Attach to containers and experiment on your own:  
`docker exec -it salttestbed_master_1 /bin/bash`