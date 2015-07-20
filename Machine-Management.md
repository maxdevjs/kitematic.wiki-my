### Suggested End of Q3 3-month MVP:

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
![](https://cloud.githubusercontent.com/assets/33699/8577211/12d46500-2575-11e5-875d-48def6491733.png)
- [DockerCon Hackathon (LightningKite)](https://github.com/fsoppelsa/kitematic)


**3-month MVP**
- Providers
 - Local
  - **VirtualBox**
  - AppCatalyst?
  - XHyve _(On hold until kernel panic with vbox installed is fixed. Possibly fixed in vbox 5.x)_
  - Hyper-V
  - Working best out of the box (Mac, Windows), backwards compatibility

 - Cloud Providers
  - Choose one that is well-supported, easy to integrate (Digital Ocean)

 - Choose specific Docker Machine parameters for each provider
 - Custom-built experience for each provider, but share the same UI + Look & Feel
 - Add arbitrary key-value parameters
 - Explore other out-of-the-box providers like Xhyve, Hyper-V
 - Advanced section with custom flags read from CLI
 - Default flags from machine

- Docker Machine CLI bindings in Javascript

- Custom install flow for each provider

- Machine management in settings panel. Possibly page for machine management (like the Log In page today), or even.
- Kitematic runs without VBox installed, setup delegated to machine management.

Process
- Proposal in wiki
- List of pieces that need to be worked on
- Issue for each piece that needs to be worked on, with comment thread
- Bi-weekly meeting

Technical Process
- Javascript Style Guide
- Contributors via PRs
- `machine` branch