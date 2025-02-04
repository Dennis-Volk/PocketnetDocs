**Pocketnet Core Node Testing and Release Process**

Some recent releases of Pocketcoin Core have introduced software defects resulting in forks or node crashes on the network.  For example, the v0.19.17 release in late October required two emergency releases within a one week time frame in order to resolve node crashes and stuck nodes.  This has caused headaches for node operators (excessive monitoring and node maintenance requirements), instability on the Bastyon social media site (disappearing posts, comments, etc), and frozen wallets on exchanges adversely affecting price and liquidity of PKOIN.
  This document proposes a formalized release process to improve stability of pocketnet core releases and earn trust of the Bastyon/Pocketnet Core community. 
  
**Goals**

- Create "stable" release designation with 99.99% uptime - defined at 1000 hours uptime for every 1 hour of downtime (not counting system maintenance and updates) 
- Catch bugs earlier in the development cycle, process rather than have these bugs be found by the community.
- Ensure compatibility of new node releases with the nodes currently on the network (fork prevention)
- More efficient use of dev time by creating a stable software tag in code to act as a launch point for new feature development
- Creation of a stable mainline software branch which new feature branches can be based upon.


**Proposed Release Process**

The release process is described in the steps below.  If any software defects are encountered at any step in the process a new issue should be created on GitHub, and the rest of the team notified.  Once the software defect is addressed the process should restart.

1. Apply version number release tag to repo at https://github.com/pocketnetteam/pocketnet.core to initiate release process
1. Set ```$BUILD_TEST = xyes``` in configure.ac file and run "make check" on Linux to verify all unit tests pass and no test regressions have been introduced.  
1. Build Windows and Linux version of packages and generate package checksum
1. TestNet: Deploy release to node connected to testnet.  Verify full sync completes, node is able to connect to front end client, complete transactions, and stake.
1. Onebox full sync/fresh install test:  Development team deploys software to a node (Linux or Windows) without an existing Pocketnet Core installation or block chain to test full sync of the node.  This ensures the consensus code of the new release is able to validate the entire block chain without error and is able to sync in a reasonable amount of time (within few days).  Progress of this node should be checked every 24 hours and release should not commence until fully synced to the main network blockchain.
1. Onebox Upgrade testing: Development team deploys new Pocketnet Core package to one Windows node and one Linux node using the existing blockchain data on disk.  Staking should be enabled on both nodes.  Run these nodes for 24 hours then verify both nodes are synced to main network without errors in log before proceeding to next step.
1. Verify each onebox node is visible on block explorer and that block explorer functions are operational
3. Dev Team Node Upgrade: Upgrade 50% of development team operated nodes with the new Pocketnet Core package after completion of (4) Onebox Upgrade testing above.  Run these nodes for 48 hours then verify all nodes are synced to main network without errors in log before proceeding.
4.  RC release: Above steps should be completed, dev team members should check status of their nodes and sign off that nodes are in stable and in sync with the main network in the Bastyon C++ node operators chat.  At this point a RC (Release Candidate) with be posted on GitHub for community download with notification posted to the Bastyon forum.
5.  Stable Release: Continue running 50% of dev nodes on release package until 10 days and 1000 hours of stable operation has been achieved (minimum 4 nodes for 10 days with no errors).  At this point the release on GitHub will be tagged or reposted as 'Stable' and notification will be posted to Bastyon.  Exchanges will be notified of stable release. 
6. Stable release complete: Update remaining dev team maintained nodes to Stable release.  
