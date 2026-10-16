# Open-Webui + Ollama + Hermes Agent and OpenClaw
- [openwebui](https://docs.openwebui.com/)
- [ollama](https://docs.ollama.com/quickstart/)
- [Hermes Agent](https://hermes-agent.nousresearch.com/)
- [OpenClaw](https://openclaw.ai/)

## Check Hardware
```
~> inxi -GSaz --vs
System:
  Kernel: 7.2.10-1-default arch: x86_64 bits: 64 compiler: gcc v: 16.2.1
    clocksource: tsc avail: hpet,acpi_pm
    parameters: initrd=\opensuse-tumbleweed\7.2.10-1-default\initrd-a1f5addc3fa0fd78684512814859bfb0e6c61b90
    root=UUID=bdb7a3e2-caec-44ba-9843-645ad73d04d5 splash=silent quiet
    security=selinux selinux=1 mitigations=auto
  Desktop: KDE Plasma v: 6.7.5 tk: Qt v: N/A info: frameworks v: 6.31.0
    wm: kwin_wayland tools: avail: xscreensaver vt: 3 dm: SDDM Distro: openSUSE
    Tumbleweed 20261014
Graphics:
  Device-1: Advanced Micro Devices [AMD/ATI] Navi 44 [Radeon RX 9050 / 9060 XT] vendor: Tul / PowerColor driver: amdgpu v: kernel arch: RDNA-4
    code: Navi-4x process: TSMC n4 (4nm) built: 2025+ pcie: gen: 5
    speed: 32 GT/s lanes: 16 ports: active: HDMI-A-1
    empty: DP-1,DP-2,Writeback-1 bus-ID: 03:00.0 chip-ID: 1002:7590
    class-ID: 0300
  Device-2: Advanced Micro Devices [AMD/ATI] Granite Ridge [Radeon 610M]
    vendor: Micro-Star MSI driver: amdgpu v: kernel arch: RDNA-2 code: Navi-2x
    process: TSMC n7 (7nm) built: 2020-22 pcie: gen: 4 speed: 16 GT/s
    lanes: 16 ports: active: none empty: HDMI-A-2,Writeback-2 bus-ID: 12:00.0
    chip-ID: 1002:13c0 class-ID: 0300 temp: 32.0 C
```

## Install WebUI 
Choice docker|podman install and follow the doc [quick-start](https://docs.openwebui.com/getting-started/quick-start)  
Create a folder `/Data/WebUI/`  on Linux SLE we still need the :Z  :(
```bash
docker pull ghcr.io/open-webui/open-webui:main
docker run -d -p 3000:8080 -v /Data/WebUI:/app/backend/data:Z --name open-webui ghcr.io/open-webui/open-webui:main
```
- Set WEBUI_SECRET_KEY
> Without a persistent WEBUI_SECRET_KEY, you'll be logged out every time the container is recreated. Generate one with `openssl rand -hex 32`.
- Visit http://localhost:3000.
### Podman Install
- Follow the doc. Podman will use Quadlet. Config is in `cdc@hera:~> bat /home/cdc/.config/containers/systemd/open-webui.container`
- update using `podman pull ghcr.io/open-webui/open-webui:main`
- Activate the auto update
  ```
  [Container]
  Image=ghcr.io/open-webui/open-webui:main
  ...
  AutoUpdate=registry
  ```
  then just  run `podman auto-update`

### Docker Install
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
```
─────┬────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
     │ File: /etc/systemd/system/ollama.service
─────┼────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1 │ [Unit]
   2 │ Description=Ollama Service
   3 │ After=network-online.target
   4 │ 
   5 │ [Service]
   6 │ ExecStart=/usr/local/bin/ollama serve
   7 │ User=ollama
   8 │ Group=ollama
   9 │ Restart=always
  10 │ RestartSec=3
  11 │ Environment="PATH=/home/cdc/.local/bin:/home/cdc/.local/bin:/home/cdc/.local/bin:/home/cdc/.cargo/bin:/home/cdc/.local/share/../bin:/home/cdc/.config/nvm/versions/node/v24.16.0/bin:/home/
     │ cdc/.local/bin:/home/cdc/bin:/usr/local/bin:/usr/bin:/bin:/home/cdc/.local/share/JetBrains/Toolbox/scripts"
  12 │ 
  13 │ [Install]
  14 │ WantedBy=default.target
─────┴────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
─────┬────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
     │ File: /etc/systemd/system/ollama.service.d/override.conf
─────┼────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1 │ [Service]
   2 │ Environment="OLLAMA_MODELS=/Data/Ollama/Models"
   3 │ Environment="OLLAMA_HOST=0.0.0.0"
   4 │ Environment="ROCR_VISIBLE_DEVICES=GPU-a2302affc7237da7"
─────┴────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
```

- Use Open-Webui to install first model following [starting-with-ollama](https://docs.openwebui.com/getting-started/quick-start/connect-a-provider/starting-with-ollama/)
  
- Customize path using `systemctl edit ollama.service`
```toml
[Service]
Environment="OLLAMA_MODELS=/nouveau/chemin"
```  
- To update, just rerun `curl -fsSL https://ollama.com/install.sh | sh`

  
