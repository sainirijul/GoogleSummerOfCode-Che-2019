# Google Summer Of Code Eclipse Che 2019
This repository reports the work done under Google Summer of Code'2019 for the [Eclipse Che](https://www.eclipse.org/che/) Project.

# Introduction
Increasingly, distributed software development teams rely on online collaboration. The proposed project aims to implement the first skeleton of CoEditing in Eclipse Che and Theia. In this project, we tried to investigate how a VS Code extension can be deployed in Che's sidecar as a remote plugin. The motivation behind this was to keep the functionality of this VS Code extension separate from the operations of Che IDE and other plugins. In addition, the aim of the project was to develop a [VS Code extension](https://marketplace.visualstudio.com/) which can utilize [Teletype](https://github.com/atom/teletype) libraries in order to create a pair programming environment in Che once the extension is executed in a sidecar as a remote plugin.

# Milestones and Current Progress
I decided to organize the overall project in different sprints in order to address the above tasks.

+ **Exploring the Che-in-Che Development (Completed on June 12, 2019)**

I started exploring different requirements required to run Eclipse Che on Minikube. These are Kubectl, Hypervisor - VirtualBox, Minikube, Helm, and Chectl. The main challenges faced during this phase were related to my device and memory issues. In addition, the Che version used by me was also having some issues. I have created a **blog** to explain how to run Eclipse Che on Minikube.

*Blog Link: [Running Eclipse Che on Minikube](https://rijul5.github.io/EclipseChe/)*

+ **Running simple VS Code extension in Che as a remote plugin (Completed on June 28, 2019)**

I developed a simple Helloworld VS Code extension and created a devfile to create a workspace in Che with this extension. The devfile has commands to build and package this extension. The devfile also has commands to install the extension as a remote plugin in the currently-running workspace Che-Theia instance. Furthermore, the extension can be installed as a remote plugin in the new hosted che-theia instance. I have created the **blog** to explain how a VS Code extension can be executed in *hosted plugin:start instance* mode.

*Blog Link: [Simple VS Code Extension in Eclipse Che as a Remote Plugin](https://rijul5.github.io/HelloWorld/)*

*code Link: [GitHub Repository with devfile](https://github.com/Rijul5/vscode-extension-che)*

+ **Developing VS Code Teletype extension for Che: Teletype Client (Completed on July 18, 2019)**

In this sprint, I worked on teletype-client library in order to use it in a VS Code extension. I started from scratch building a simple VS code extension and then used teletype-client library inside it. In order to use, teletype-client library, type declaration file (.d.ts) was created and added to the project. The major challenges in this sprint were to figure out the alternative for the pusher-js library so that a pusher channel can be established from a node process running in VS Code. Also, the issues related to window reference and global fetch were resolved. At the end of this step, I was able to create a teletype client from VS Code extension. 

*code Link: [GitHub Repository dev branch - Teletype Client commit](https://github.com/Rijul5/vscode-teletype/commit/466409c245f211261088d2fa97e18794cf3aa9a8)*

+ **Developing VS Code Teletype extension for Che: Join Portal (Completed on August 9, 2019)**

Next, *Join Portal* command along with the functionality was added so that any guest from VS Code extension can join the portal launched from Atom Teletype editor. This means it will allow the user/guest using Che to join the portal launched from Atom editor. In addition, validations were added so that user enter the right portal ID and they were further integrated with the portal module present in the teletype-client library. By the end of this step, validations and necessary calls to join portal were executing.

*code Link: [GitHub Repository dev branch - Join Portal commit](https://github.com/Rijul5/vscode-teletype/commit/cc570c7af8031ed8d83422a432526351dba562b5)*


![alt text](https://github.com/Rijul5/GoogleSummerOfCode-Che-2019/raw/master/src/common/images/Pusher-Debug-Console.png)


+ **Developing VS Code Teletype extension for Che: RTCPeerConnection and Guest-Portal Bindings (Completed on August 25, 2019)**

In this sprint I tried different packages in order to establish RTCPeerConnection between the client/guest created from VS Code extension and the portal/host launched from the Atom editor. Eventually, I decided to use [wrtc](https://www.npmjs.com/package/wrtc) package. I also used external sources available on GitHub to figure out the guest-portal and editor bindings as my main focus was on developing a simple extension with teletype libraries that work well in Che through a devfile. At the end of this step, I was able to send signals from the guest (VS code) to host(Atom Editor). There are still some challenges in this direction which I am explaining in the next step.

![alt text](https://github.com/Rijul5/GoogleSummerOfCode-Che-2019/raw/master/src/common/images/events.png)


# Challenges and Future Work

+ The RTCDataChannel readyState does not come to *open* state and therefore the RTCPeerConnection is always in *connecting* state. Also, as shown in the above screenshot, the *iceGatheringState* changes as *new* -> *gathering* -> *completed*. However, the *iceCandidateState* changes only from *new* to *checking*. It never comes to *completed* state. It might be related to network issues. This issue needs to be investigated.

+ The editor and guest bindings need to be completed.

+ Teletype-server library should be added to the above VS code extension to enable a host to create a headless server from Che so that guests can join it from different editors.

+ Synchronization challenges in live collaboration mode with multiple language servers and editors, need to be explored.
