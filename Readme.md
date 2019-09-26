# Specification for Fairdrive
<img width="220" height="250" src="images/Fair%20Data%20Society.jpeg">

Table of Contents
=================
   * [Fair data](#fair-data)
   * [Fair Data Society](#fair-data-society)
   * [Fairdrive](#fairdrive)
      * [Storage Layer](#storage-layer)
         * [Decentralised](#decentralised)
         * [Fault Tolerant](#fault-tolerant)
         * [Censorship-resistant](#censorship-resistant)
         * [Self-sustaining](#self-sustaining)
      * [Permission & Consent Layer](#permission--consent-layer)
   * [Fairdrive Functionality and Use cases](#fairdrive-functionality-and-use-cases)
      * [Data Access](#data-access)
      * [Permissions](#permissions)
      * [Incentivisation](#incentivisation)
   * [Types of data stored in Fairdrive](#types-of-data-stored-in-fairdrive)
      * [User-generated data](#user-generated-data)
      * [Application-generated data](#application-generated-data)
   * [Fairdrive compared to other options](#fairdrive-compared-to-other-options)
   * [Reference Implementation](#reference-implementation)
      * [Functional Architecture](#functional-architecture)
         * [Fairdrive SDK (fds.js)](#fairdrive-sdk-fdsjs)
         * [Noordung Chain](#noordung-chain)
         * [Smart Contract](#smart-contract)
         * [Swarm as a storage Layer](#swarm-as-a-storage-layer)
            * [Fault tolerance](#fault-tolerance)
            * [Censorship-resistant](#censorship-resistant-1)
            * [DDoS-resistant](#ddos-resistant)
            * [Zero downtime](#zero-downtime)
            * [Self-sustaining](#self-sustaining-1)
   * [Open-source artefacts](#open-source-artefacts)
   * [Fair Data Society-compliant apps](#fair-data-society-compliant-apps)
   * [Applications that use Fairdrive](#applications-that-use-fairdrive)
      * [Fairdrive Webapp (fairdrive.xyz)](#fairdrive-webapp-fairdrivexyz)
      * [Fairdrop (fairdrop.xyz)](#fairdrop-fairdropxyz)
      * [Chattie (chattie.xyz)](#chattie-chattiexyz)



## Fair data
Fair data represents a stand for a more equal distribution of control and value for everyone involved in data generation, exchange and processing, with the individual at the centre. It’s a concept which acknowledges that personal data is a part of the individual and can only belong to an individual.

## Fair Data Society
The Fair Data Society is the embodiment of the fair data principle. It is a decentralised autonomous organisation (DAO) at the core of a technology platform that protects people’s data, including their personal, private, and identity data. At the same time  it provides a clear and transparent set of guidelines for organisations to engage in a relationship where the role and value of personal data is completely redefined. 

While many [organisations](https://solid.inrupt.com/) are working on standards to give people ownership of their data, the question of where that data will be stored is of key importance. Cloud services and data hubs end up with control or access to people’s data. The Fair Data Society, on the other hand, creates and supports technologies that will allow people to safely store their own data in ways that nobody but the rightful owner can access, control and provide permissions around that data.

## Fairdrive
The first step for our current system to becoming a truly Fair Data Society is to reclaim our data from its centralised masters. As we reclaim more and more of our data, the need for safe storage space will increase. Currently, there are no user-friendly storage options available that are safe from corporations or governments. This specification is an attempt to jot down the specification for Fairdrive, our attempt to provide everyone with a set of tools to help them build a digital pod for storing their data safely and securely.

Fairdrive is a logical drive that will store all of the individual’s data in one place and will be controlled entirely by said individual. Think of it like a `Dropbox` that is decentralised and app friendly. Individuals can store their personal files and documents in it, while applications can store the data generated by the individual in that same Fairdrive. The individual has absolute control over all the data in his Fairdrive and can share the contents with others for free or for a fee. It is a decentralised drive where only you can own, control and decide who gets access to the stored data.

At its core it has the following subsystems:
- A decentralised storage system.
- A set of smart contracts enforcing permissions, managing incentivization, exchanging consents etc.
- An SDK to access the data.
- A set of standards and guidelines covering where data is stored, how it is encoded and how it is encrypted.
<p align="center">
<img width="650" height="450" src="images/Fairdrive%20layers.png">
</p>


### Storage Layer
To store our reclaimed data safely, we need a storage that is not controlled by anyone and still has all the features of the Web 2.0 storage. The current Web 2.0 architecture uses centralised storage servers where the data is hardly in control of the individual. Fairdrive will use a decentralised storage layer. The following are some of the properties that should be present if we want to make the data more secure and available.

#### Decentralised
To make sure that the data is not at the mercy of any one organisation or company, the storage layer should be a decentralised peer-to-peer solution. This will guarantee that the data is not stored in one (physical) place and no one can hold the individuals hostage over their data.

#### Fault Tolerant
A piece of data should be replicated across several physical storage locations. To make sure that the data is not lost due to physical hard disk failures, it should be protected by fault detection and fault correction technologies. 

#### Censorship-resistant
No third party should be able to stop the individual from accessing his data. No one else other than the individual should be able to access his/her data, except those that have been given access. 

#### Self-sustaining 
For any peer-to-peer system to be truly decentralised, there should be some form of (de)incentivisation involved to motivate the peers to maintain the system. This should make it self-sufficient and independent from powerful external parties that could influence the decision-making process.


### Permission & Consent Layer
Just having the storage layer is not sufficient. There should be a way to secure and share the data with others to drive a thriving data economy. Similar to how Unix has permissions associated with files, in a decentralised system, blockchain can be used to enforce these access rules. This layer is also used to provably exchange data between individuals and to transfer incentives in a decentralised way.


## Fairdrive Functionality and Use cases
Following are some of the use cases of Fairdrive.

### Data Access
- Store files & entire directories.
- Sync local directory to individual’s Fairdrive.
- Store application data in individual Fairdrive.
- Search information on individual’s Fairdrive.

### Permissions
- Share files with a friend/ group of friends.
- Give permission to applications to read data.

### Incentivisation
- Pay for storage and Fairdrive services.
- Individuals should be able to monetise their data.


## Types of data stored in Fairdrive
There are two major actors that use Fairdrive. One is the individual himself and the other are the applications that he/she uses.
<p align="center">
<img width="650" height="450" src="images/Typed%20of%20data%20in%20Fairdrive.png">
</p>

### User-generated data
An individual can directly store or retrieve files and documents in Fairdrive, similar to other cloud storages, like Dropbox or Google Drive. To make this easier, there will be a web-app (fairdrive.xyz) and a native app to enable the store and retrieve functions. Using this app, the individual can upload and download content or share them with others without anyone else being able to access them.

### Application-generated data
Applications that are Fair Data Society-compliant, can use the Fair Data Society SDK (fds.js) to access Fairdrive. They can store the data generated by the individual in a specific directory inside Fairdrive. Applications always point to the user generated data from the application-specific metadata and never store individual’s data anywhere else. Individuals can decide to share their data with other applications as and when needed. Also by owning the application-specific data, the individual can now make this data available to others who need it - either for free or for a fee. Applications can follow standards (like [Solid](https://github.com/solid/solid-spec)) while storing information, so that the information is discoverable and interoperable with other applications


## Fairdrive compared to other options
There is a myriad of group file sharing applications. The major difference between them and Fairdrive is that the latter stores files on a decentralised storage (not on centralised servers) and only the person controlling the private key has access to the stored files. Fairdrive gives individuals a safe zone in cyberspace, to which only they have access, while it does not exist for the rest of the world. 

Fairdrive gives individuals complete control over their data. Only they can explicitly share their data (send a file) with other individuals or applications. The vision behind Fairdrive is to enable individuals to reclaim, own and manage their data, not give companies the tools to data mine privacy for profit. Also, decentralised storage systems enable the creation of peer-to-peer networks that preserve privacy and human rights, putting the individuals at the centre and giving them full control of their digital life.


## Reference Implementation

To jumpstart the Fairdrive thought process, it is not enough that we just put down the specifications for it. We are also working on a Fairdrive reference implementation described above. The components that we chose or implemented are fully decentralised and open-sourced. This is only a reference implementation and others are welcome to add more features and use this as long as they respect the Fair Data Society [principles](https://docs.google.com/document/d/14-DM3M-cNCrq2Cn_7J8rRawhaoHOhlyXRPSQZ2thiuc/edit#heading=h.tyu66tcq1j2m).

### Functional Architecture
<p align="center">
<img width="650" height="450" src="images/Functional%20Architecture.png">
</p>

#### Fairdrive SDK ([fds.js](https://github.com/fairDataSociety/fds.js))
To access Faridrive, we have developed a SDK called fds.js. This SDK exposes APIs to interact with the Fairdrive system. Applications can do the following functionalities with the SDK:

- Create a Fairdrive for an individual given his identity.
- Connect to an individual’s Fairdrive using their identity.
- Upload a file or folder from a local disk to an individual’s Fairdrive. 
- Download a file or folder from an individual’s Fairdrive to local disk.
- Applications can create a space for themselves in the individual’s Fairdrive.
- Applications can store the individual’s data in their respective spaces.
- The individual can share any data in his Fairdrive to another user or Application.
- The individual can charge for the data they have shared with others or an application.
- Individuals can un-share the shared data.

#### Noordung Chain
For book keeping the individual’s permissions and payments in a decentralised system, we needed a blockchain with specific characteristics. Because of this we have created our own chain (based on Ethereum) which is based on Proof of Authority, [Noordung](https://en.wikipedia.org/wiki/Herman_Poto%C4%8Dnik). For now Fair Data Society is running all the sealers and other nodes. Overtime anyone should be able to run the nodes.

#### Smart Contract

The Noordung chain hosts a set of smart contracts that actually control the individual’s Fairdrive and its permissions. Another set of smart contracts controls the incentivisation aspect of Fairdrive. People need to pay for storage and also get paid when they share their data for a fee. These payment exchanges are facilitated by smart contracts ina way that makes the system trustless.


#### Swarm as a storage Layer
We decided to use Swarm as our storage layer because it satisfies all the essential necessities of a fair storage system. Swarm is an open, neutral, borderless, censorship-resistant storage and communication infrastructure. A bit more specific, it’s a decentralised network of nodes that can store and exchange data. 

It’s neatly summed up in a quote by one of the lead developers of Swarm: “If Ethereum is the world’s computer, then Swarm is the world’s hard disk”. Fairdrive can benefit from using it and in doing so decrease reliance on central servers, reduce the risk of attacks and downtime, while increasing redundancy, security and privacy.

Swarm has the following properties:

##### Fault tolerance
Data stored in Swarm is chunked and strewn across the network. These chunks are replicated across several physical swarm nodes for backup and redundancy. Swarm also has abilities to do error detection and error correction using erasure coding.

##### Censorship-resistant
Swarm is resistant to detection and attacks from central entities because of its peer-to-peer nature. Swarm nodes that store the data or any actor who is listening to the network cannot know who is the owner of the data.

##### DDoS-resistant
Individual-generated data is stored across the network. Because of this there is no central server that the adversaries can attack and bring  down.

##### Zero downtime
Swarm is a network of nodes. Even if individual nodes go down, replication of the data across several physical nodes ensures that the data is always available.

##### Self-sustaining
Perhaps the most important feature of Swarm is the ability for it to self sustain. This means that there is the element of incentivisation and de-incentivisation built in the network which ensures that the actors behave for the good of the network.


## Open-source artefacts
To realise the above architecture, we developed the following user-facing artifacts: 

For programmatic access to Fairdrive, an SDK called fds.js is available. Fds.js enables applications to access almost all of Fairdrive’s functions. 

Next are Fairdrive UI applications; a web-app and a Desktop app. The webapp is hosted on Swarm and is available at fairdrive.xyz. Individuals can use their identity to log into the app and use it from a browser. There is also a native app for popular operating systems which can be installed and configured to continuously run in the background. This architecture is similar to that of Web 2.0 apps like Dropbox.
<p align="center">
<img width="650" height="450" src="images/Open%20source%20artifacts.png">
</p>

## Fair Data Society-compliant apps

Applications that intend to use Fairdrive should be Fair Data Society-compliant. By which we mean that the application should only store the individual’s data in Fairdrive and nowhere else. In the graphics below are some of the deployment models that the applications can use today
<p align="center">
<img width="650" height="450" src="images/FDS%20compliant%20apps.png">
</p>


**API-based** deployment model is similar to Web 2.0 mode. In this model, the application connects to Faidrive using the API exposed by a Fair Data Society-owned centralised server (boxes not in red border). This server runs a node application that exposes the same API that our SDK provides. This server also hosts a Swarm node which is used by the node application. Even though this method is not properly decentralised and does not align with Fair Data Society principles, we have exposed this API to easily test an application using our SDK. This model is only recommended for testing and not for production.

**SDK-based** deployment is the current model that is supported by Fairdrive. In this model, applications can embed our SDK and use it to access Fairdrive. This model has the option of applications running their own Swarm gateway or in the worst case use the Fair Data Society’s Swarm gateway. We recommended the former.

**SWASM-based** deployment is the truly decentralised model. In this model, the application is bundled with our SDK and a “WASMised” version of Swarm. In this setup the application doesn’t need to talk to any central node. This is not available at the moment, but should be further down the road.

## Applications that use Fairdrive

### Fairdrive Webapp (fairdrive.xyz)
“Fairdrive webapp” will be the base application for individuals to access Fairdrive. This application can be used to create a new profile. Once the individual logs in, he/she is presented with a storage area similar to a folder in any operating system. With the Fairdrive app individuals can browse different app-created directories from a host of applications. 

For example: in the screenshot below you can see the directory structure on the left side. The individual’s Fairdrive shown in this example has a “Fairdrop” folder, which was created when he used the Fairdrop application. Similarly, every Fair Data Society-compliant application that he has used in the past would create a separate directory to store the contents of the respective applications. 

This app can be used to upload or download files from/to the individual’s local file system. Individuals can also share their Fairdrive-based files with other individuals or applications. Apart from managing data, this application also has a wallet to show the details of storage-related payments - either incoming or outgoing.
<p align="center">
<img width="650" height="450" src="images/Fairdrive%20App.png">
</p>

### Fairdrop ([fairdrop.xyz](https://fairdrop.xyz/))

Fairdrop is a fair, secure and unstoppable file transfer application, built with the Fairdrive SDK. It is our original web application, hosted in Swarm. Individuals can create an account and will be assigned a mailbox. The mailbox contains 2 folders, “Received” and “Sent”. Individuals can share a file from their local filesystem with another individual. These files will then be encrypted and sent to the respective individual’s “Received” folder. The sent files will be shown in the “Sent” folder. If anyone shares a file with you, you would see it in the “Received” folder for download to local file system. More about the application [here](https://blog.datafund.net/fairdrop-secure-private-unstoppable-file-transfer-for-the-free-world-f1a39adbdeab).
<p align="center">
<img width="650" height="450" src="images/Fairdrop%20App.png">
</p>

### Chattie ([chattie.xyz](https://chattie.xyz/))

Chattie is an example chat app built to show how data can be shared between two individuals using Fairdrive. You can use the same account you created in the Fairdrive webapp to login here. A logged-in individual can start a chat with another individual. The messages he/she creates are stored in the current individual’s Fairdrive and are also shared with the individual with whom he/she chats. This ensures that the Chattie application can access the chat messages of the current individual and ones typed by the receiving individual.
<p align="center">
<img width="650" height="450" src="images/Chattie%20Application.png">
</p>




