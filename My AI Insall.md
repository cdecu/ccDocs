# Open-Webui + Ollama + Hermes Agent and OpenClaw
- [openwebui](https://docs.openwebui.com/)
- [ollama](https://docs.ollama.com/quickstart/)
- [Hermes Agent](https://hermes-agent.nousresearch.com/)
- [OpenClaw](https://openclaw.ai/)

## Install WebUI 
Choice docker install and follow the doc [quick-start](https://docs.openwebui.com/getting-started/quick-start)  
Create a folder `/Data/WebUI/`  on Linux SLE we still need the :Z  :(
```bash
docker pull ghcr.io/open-webui/open-webui:main
docker run -d -p 3000:8080 -v /Data/WebUI:/app/backend/data:Z --name open-webui ghcr.io/open-webui/open-webui:main
```
- Set WEBUI_SECRET_KEY
> Without a persistent WEBUI_SECRET_KEY, you'll be logged out every time the container is recreated. Generate one with `openssl rand -hex 32`.
- Visit http://localhost:3000.
- Create ~/bin/open-webui.sh 
```bash
#!/usr/bin/env sh
echo docker rm -f open-webui
docker run -d -p 3000:8080 -v open-webui:/app/backend/data:Z  \
         -e WEBUI_SECRET_KEY="xxxxxxxxxxxxxxxxxx" \
         -e OLLAMA_BASE_URL="http://172.17.0.1:11434" \
         -e OLLAMA_API_BASE_URL="http://172.17.0.1:11434/api" \
         --name open-webui \
         --restart always \
         ghcr.io/open-webui/open-webui:main
```



## Install Ollama 
- Just follow the doc [Linux Install](https://docs.ollama.com/linux) `curl -fsSL https://ollama.com/install.sh | sh`
- Use Open-Webui to install first model following [starting-with-ollama](https://docs.openwebui.com/getting-started/quick-start/connect-a-provider/starting-with-ollama/)
- Customize path using `systemctl edit ollama.service`
```toml
[Service]
Environment="OLLAMA_MODELS=/nouveau/chemin"
```  
