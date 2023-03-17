# quorum_blockchain_smart_contract

Smart contract : Organization of Events
- This contract will allow various event organisers to organise tickets for various events.
- will have buyers to buy that tickets with the help of ethers.

**How to work with the quorum 7nodes example?**

Prerequisite required : 
- Node.js
- Docker and Docker-compose
- solc

**Steps**
1. Getting the quorum example 7 nodes
    - **git clone https://github.com/jpmorganchase/quorum-examples.git**
    - Enter into the quorum-examples directory : cd quorum-examples
    - By default , quorum has Istanbul BFT consensus so we can change by setting the environment           variable **QUORUM_CONSENSUS=raft** .
    - For those who have low system configuration and getting problem in the docker image (image           remain unhealty), they can reduce the nodes(atmost 4) by deleting the nodes encoded address in       the permissioned-nodes.json file present in the /quorum-examples/examples/7nodes.
    - Now start docker containers in the background : **docker-compose up -d**.
    - Run **docker ps** to check the status of each container and wait till the their status of           become healthy(it will take some time).

2. Compiling Smart Contract
    - compile using solc : **solc MyContract.sol --bin --bin-runtime --abi --optimize -o build/**
    - Now build directory containers contains abi and bytecode file.
    - Change the private-contract.js file and update the abi and bytecode which you get above.
    - Also remove the address from privateFor parameter (leave it as '[]').

3. Deploying Smart Contract
    - For deploying the smart contract we need to enter into geth javascript console of that node       from which you want to deploy the smart contract.
      Run : **docker exec -it quorum-examples-node1-1 geth attach /qdata/dd/geth.ipc** 
      (you can change the node by copying the names from the output of docker ps)
    - Now we have to run private-contract.js file which we have updated above.
      Run :  **loadScript('/examples/private-contract.js')**
      This will return you the transaction hash and the contract address of the deployed contract.       This address is used to call the functions of the contract you deployed.
      
      
OUTPUT: 

![result](https://user-images.githubusercontent.com/59726935/225815466-3ce55755-bc7c-41cf-b300-81ee23c1c2c9.PNG)
