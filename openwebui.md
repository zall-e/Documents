### Create Network(two container in same network)
docker network create -d bridge openwebui-net

# METHOD 1
## openwebui
docker run -d -p 3000:8080 -v ollama:/root/.ollama -v open-webui:/app/backend/data --network openwebui-net --name open-webui --restart always ghcr.io/open-webui/open-webui:ollama

## pipelines
docker run -d -p 9099:9099 -v pipelines:/app/pipelines --network openwebui-net --name pipelines --restart always ghcr.io/open-webui/pipelines:main

# METHOD 2
### clone
git clone http://github.com/open-webui/open-webui.git

### build image
docker build -t openwebui .

### run image
docker run -d -p 3001:8080 -e OPENAI_API_KEY=api_key -v open-webui:/app/backend/data --network openwebui-net --name openwebui --restart always open_webui


# Setup pipline

### Clone from git
https://github.com/open-webui/pipelines.git

### Build image
docker build -t pipline .

### run image
docker run --network openwebui-net -p 9099:9099 -v $(pwd)/pipelines:/app/pipelines -v $(pwd)/data:/home -d pipline




