### Suggested Q3 3-month MVP:

#### Tech Architecture
###### Provider Setup
1. A graphical picker chooses a provider
2. DriverSetupStore sets up provider
4. Set up info (tokens, endpoints, creds, etc.) pulled from settings (interactive?)
5. (Provider verification?)
6. VM creation and setup (from Machine)

#### Design Overview

#### Provider Support
- [ ] VirtualBox
- [ ] VMWare Fusion (AppCatalyst?)

#### Outstanding Machine Issues

- Stuck at 99% ( https://github.com/kitematic/kitematic/issues/236 ), here it seems like we need better error reporting. 
- VPN connection issue ( https://github.com/kitematic/kitematic/issues/254 ) 
- Proxy issue ( https://github.com/docker/machine/issues/1319 ) 


#### Existing Work

- Proposal: https://github.com/kitematic/kitematic/issues/777
- https://github.com/TeckniX/kitematic/tree/docker-engine-selection
- DockerCon Hackathon (LightningKite)