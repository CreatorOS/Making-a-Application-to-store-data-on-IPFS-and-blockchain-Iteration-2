# Making a Application to store data on IPFS and blockchain - Iteration 2
__Only works in Linux and Mac for Compilation of Smart Contract as build tools are not available on windows as of now ~ 21/09/2021__

__WSL is also compatible for compilation of smart contracts.__

### Introduction

Blockchains are expensive to store data. Many blockchains starting from Bitcoin to multiutility ones such as ethereum can cost you thousands for $ to store just 1 MiB of data. To mitigate this cost pressure and store large data on blockchain in recent years we have seen IPFS. So why it’s interesting, well there are several reasons two of them for using IPFS in blockchain are:

1. Content added to IPFS gives us a CID (A Content Identifier) which can’t be changed unless data is changed.
2. It is distributed and Peer to Peer, can say similar to torrent but way more advanced.

So, In this project we will be building a user interface where we will first upload our data to IPFS (Inter Planetary File System) then get our CID, after that push our data to blockchain as CID never changes if data remains the same. 

User Interface -> IPFS -> CID -> User Interface -> To Solana Blockchain.

There are no hard prerequisites to start this quest but having a bit of knowledge of JavaScript can help as we will be building our UI in ReactJS. For our smart contract we will be compiling our smart contracts with Rust but prior knowledge is not required.

Code

curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -

sudo apt-get install -y nodejs

sudo npm i -g yarn

What happen with this code

This will install rust and nodejs on your local computer

Why that is interesting

With nodejs we will be able to develop our User Interface for the project and Rust will help us compile our smart contracts which we will deploy on solana blockchain.

Code

sh -c "$(curl -sSfL [https://release.solana.com/v1.7.12/install](https://release.solana.com/v1.7.12/install))"

sudo apt install git

sudo apt install g\+\+

sudo apt install cmake

sudo apt install build-essential

What happen with this code

This will install solana-sdk, github and c\+\+ in your local desktop.

Why that is interesting

This will install solana into your local machine which will help us when we deploy our contract to blockchain and c\+\+ will help our rust which we installed previously in compiling the smart contracts. (Please do look for instruction to add solana to you $PATH as given instruction after executing line 1 )

Code

git clone [https://github.com/prix0007/super-storage-starter.git](https://github.com/prix0007/super-storage-starter.git)

cd super-storage-starter

yarn

yarn start

What happen with this code

This will clone a new project in you desktop inside folder super-storage-starter

Why that is interesting

This will help us boost to the steps and will set up a start project on which we will work upon to create our application. Also after `yarn start` you can view localhost:3000 in your browser to see it running and showing a big `Super Storage`

__![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/05d970cf-613c-4f0f-914a-698c2f5839bf.jpg)__

Code

Install IPFS CLI from here: [https://docs.ipfs.io/install/command-line/\#official-distributions](https://docs.ipfs.io/install/command-line/#official-distributions)

ipfs init

ipfs add _PATH_TO_SOME_FILE

What happen with this code

Uploading a Simple file with IPFS

Why that is interesting

After this you will have an IPFS CLI. You can do many things with it. Try ipfs -h for all options. Here we are uploading a file to ipfs from `ipfs add` and you will get back a response which starts with Qm…. or ba…. , you can try looking for these in brave or opera browsers just try copying and pasting that hash to the browser url as `ipfs://_YOUR_HASH_Qm.._` and you can see your file.

Code

Goto [https://web3.storage/](https://web3.storage/) and create a new account.

To create an Storage account and Creating an API key please refer to : 

  [https://docs.web3.storage/how-tos/generate-api-token/\#create-a-new-token](https://docs.web3.storage/how-tos/generate-api-token/#create-a-new-token)

What happen with this code

You will have an API key which we will use in our code.

Why that is interesting

Web3.Storage gives us a generous limit of storing data on IPFS and Also it provides us with simple tools to do it. You can try to upload data right away with user Interface but we will be uploading data to it from Our Application later.

Code

Go to the Files section and Try to upload any files if not yet done.

What happen with this code

Introduction about IPFS and Web3.storage

Why that is interesting

Web3.Storage was built to simplify the process of uploading data on IPFS. As you can see after you have uploaded the data in a table as below:

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/8e748e64-9d31-4925-81cb-40415058907e.jpg)

As you can see here is a CID. We will be storing this field in our blockchain as this never changes for the same data, as blockchains also are immutable. 

You can also see a Pin Status and Storage Providers there, This simply signifies that our data will live on IPFS and these storage providers guarantee to store our files.

“Now open the folder `super-storage-starter` in a code editor so we can see files. You can use VSCode. And after opening the project navigate to a file named App.js which contains all of the UI and we will be making most of the changes here. ”

Code

    

       

         

           Super Storage

         

       

     

What happen with this code

Put this code by replacing the `Super App` in App function in App.js.

This will add a navigation bar in the UI Screen

Why that is interesting

This is how we can add html. You just have to return html from the function and it will be on the browser screen as html. 

Code

     

       

         

           Save it to Blocks

         

       

     

What happen with this code

Put this code below the nav in the App function.

This will add a container inside which our form field will go.

Why that is interesting

To build any application we need to have some field in place to get input. So for that html have form fields which we will use here and the button will help us to send that data later.

Code

     

           Add a name to your storage files, It will be inside our Blockchain

           

      

What happen with this code

Put this code below inside the form and above the button added in the last step.

This will add a new input field to enter the name.

Why that is interesting

This will attach the html which is required to take input from the user itself.

Code

     

           

             Files

           

           

      

What happen with this code

Put this code below inside the form and between the last added input and save button.

This will add a new input field to select multiple files.

Why that is interesting

This will attach the html which is required to take files selection from the user which he needed to upload to blockchain.

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/ad0f4326-0af8-4f24-a17d-08b46fbbd88a.jpg)

Code

    const \[name, setName\] = React.useState("");

    const \[selectedFile, setSelectedFile\] = React.useState(null);

What happen with this code

This goes before the return inside the App function. This will add variables for form.

Why that is interesting

These are variables called hooks in react. They are required to keep track of what is typed in the input field or selected to be later used for uploading to the blockchain.

Code

    	     setName(e.target.value)}

           />

What happen with this code

Change the input which you added previously for the name. This will connect our name hook or variable to name input.

Why that is interesting

After this step whenever we will be typing in input this will automatically update the hook `name` in our function. With this we can get what’s inside our input field for using it later. 

Code

    	      setSelectedFile(e.target.files)}

           />

What happen with this code

Change the input which you added previously for the files. This will connect our selectedFile hook or variable to file input.

Why that is interesting

After this step whenever we select some files from input field it will be stored in the hook and can be later used for fetching files from desktop and send to our ipfs.

Code

    	      

             {selectedFile

               ? \[...selectedFile\]

                   .map((f) => f.name)

                   .join(", ")

                   .toString()

               : ""}

           

What happen with this code

Put this just below the files input before the  tag. This will add the filename of selected files when some files are selected.

Why that is interesting

After this whenever you select some files, It will check if there’s something in the selected file. If it is then it will get all the names and put them there. It is required so that the user can know which files he has selected to upload.

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/575817b2-9940-4149-9573-445af3185b4a.jpg)

Code

  const \[errors, setErrors\] = React.useState({

   ename: "",

   efiles: "",

 });

 const handleChecks = () => {

 }

What happen with this code

Add this code just below the previously added variable for name. This will add a hook to store errors if any.

Why that is interesting

We need this to check if there is any error in the input field which we have added. Data on blockchain is immutable so checking it before is necessary here.

Code

   let flag = true;

   let eobj = {ename: "",efiles: "" };

   if (name.trim() === "") {

     eobj.ename = "Please Enter Some Name";

     flag = false;

   } else {

     eobj.ename = "";

   }

What happen with this code

Put this inside the handleChecks function. It will add functionality to check for a valid name.

Why that is interesting

Here we are checking if there is any name in our name hook. If there is, then we will go and clear out eobj.name to blank and if it’s blank then we will add text which will be displayed to the user. Also we are using flag to keep track of whether if we found any errors or not.

Code

   if (selectedFile === null || selectedFile.length What happen with this code

Put this inside the handleChecks function and below code added in the previous step. This will add checks for selectedFiles.

Why that is interesting

Here we are checking if there are any file selected. If there isn't any file then we are setting errors and if there is then we are clearing that error. Then we are setting our new eobj back to errors hook which will tell our UI to show any error. And returning a flag to let us know if there are any errors found or not.

Code

    {!errors.ename ? (

             Looks good!

           ) : (

             {errors.ename}

           )}

What happen with this code

Put this code just below the input for name. This will show the text for error depending upon name.

Why that is interesting

After this you can see an error or a green success if you have entered a valid name. This will add the error for name in our UI.

Code

     {!errors.efiles ? (

             Looks good!

           ) : (

             {errors.efiles}

           )}

What happen with this code

Put this code just below the input for files. This will show the text for error depending upon selectedFile.

Why that is interesting

After this you can see if you have selected any file or not. It makes it simple for users to know if files are selected in our UI or not.

Code

    const handleSubmit = (e) => {

   	e.preventDefault();

   	if (handleChecks()) {

   	  console.log("checks passed");

   	}

    };

    React.useEffect(() => { handleChecks();}, \[name, selectedFile\]);

What happen with this code

Add this code below our handleChecks function. After this code will check for errors after any change in inputs.

Why that is interesting

After this we have a function which we can attach to the submit button for submitting the form. And also it will check for error whenever someone types or selected anything. 

Code

    	Save it to Blocks

What happen with this code

Replace this with a button which is inside the form. It will connect the handleSubmit function to the button.

Why that is interesting

Here we are connecting our form button to run the handleSubmit function and it will check for if form fields are correct before submitting anything.

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/34d03c5d-3b52-4303-bcee-0a4539332de3.jpg)

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/9b42eb75-8ae8-412d-ac2b-57aa5154064c.jpg)

Code

REACT_APP_WEB3_API=__YOU_API_TOKEN_FROM_WEB3.STORAGE__

What happen with this code

Inside the super-storage-starter folder create a .env file and place code inside it. In terminal press Ctrl \+ C to stop server and again run `yarn start`

Why that is interesting

This will add API token in our application and will keep it relatively safe. After this we can communicate with IPFS and Web3.Storage .

Code

import { Web3Storage } from 'web3.storage/dist/bundle.esm.min.js'

What happen with this code

Put this inside the App.js file just above the App function. 

Why that is interesting

This will import the object which we need to communicate with IPFS node at web3.storage.

Code

 async function storeFiles(files){

   const client = new Web3Storage({ token: process.env.REACT_APP_WEB3_API})

   const cid = await client.put(files)

   return cid

 }

What happen with this code

Put this just above the App function inside the App.js file.

Why that is interesting

With this function we will be able to upload the file to IPFS. It will create a client which will wait to get cid (unique identifier) from IPFS and return it back to whichever called it.

Code

 const handleSubmit = (e) => {

   e.preventDefault();

   if (handleChecks()) {

     const cid = storeFiles(selectedFile);

   }

 };

What happen with this code

Replace it with the handleSubmit function inside the App function. It will get cid from the function added in the previous step.

Why that is interesting

With this updated handleSubmit we can also upload the files which we have selected to the IPFS.

Code

const \[loading, setLoading\] = React.useState(false);

const \[cid, setCid\] = React.useState("");

What happen with this code

Add this just below the errors hook. It will add hooks to keep track of loading state and cid.

Why that is interesting

Since when we upload we don’t know whether it is processing our upload or not as files take a bit time to upload. So we will keep loading state to check if we are uploading and cid to check if we have already uploaded.

Code

{loading ? (

           Loading...

         ) : cid ? (

           Stored File With: {cid}

         ) : (

           Save it to Blocks

        )}

What happen with this code

Change the button inside the form with this code. This will show state depending upon loading and cid hooks.

Why that is interesting

After this our UI will show us if we are still uploading our data or we have successfully retrieved our cid. It will give a richer user experience to those who will be using our dapp.

Code

 const handleSubmit = async (e) => {

   e.preventDefault();

   if (handleChecks()) {

     setLoading(true);

     const cid = await storeFiles(selectedFile);

     setCid(cid);

     setLoading(false);

   }

 };

What happen with this code

Replace the handleSubmit function inside the App function. It will add loading updates according to data flow.

Why that is interesting

After this our handleSubmit function will set the loading to true before uploading which will show in UI a circular progress and after uploading we can see the cid with which we have uploaded our data on IPFS.

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/3918eb86-0830-47dd-963c-754ebe3491f9.jpg)

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/afd63c2f-b85d-4f95-9296-7e72ae957af9.jpg)

Code

import { getStorageAccountPubkey } from "./solana/accounts";

import storageService from "./solana/storage";

import { initWallet } from "./solana/wallet";

What happen with this code

Add these above the App function. These will import function which are required to connect to wallet.

Why that is interesting

This will import the function which will help us connect to the solana blockchain and make use of it in our dapp.

Code

// Wallet State

 const conn = React.useRef();

 const \[myWallet, setMyWallet\] = React.useState(null);

 const \[storageAccount, setStorageAccount\] = React.useState("");

What happen with this code

Add these below the cid hook or before handleChecks function. It will add new hooks to manage the state of the wallet.

Why that is interesting

With this we can connect to the wallet and also keep track of the wallet on which we will call other functions such as uploading data to the blockchain which we need to sign from our wallet.

Code

const connectWallet = () => {

   initWallet().then((\[connection, wallet\]) => {

     conn.current = connection;     setMyWallet(wallet);

     if (wallet.publicKey) {

       console.log(wallet.publicKey.toBase58());

       getStorageAccountPubkey(connection, wallet, storageService.STORAGE_SIZE).then((walletCertificatePubkey) => {

         setStorageAccount(walletCertificatePubkey.toBase58());

         getStorageData(connection,walletCertificatePubkey.toBase58());

       });

     }

   });

 };

What happen with this code

Add this function above the handleChecks function. This will add functionality to connect to the wallet and set our hooks.

Why that is interesting

With this function we first connect to our wallet and blockchain then we check if we already have a storage account in which we will store data on blockchain. If we have then we get that and if we don’t we send wallet instructions to create one. and after setting set our hooks with appropriate data. 

Code

 const getStorageData = (connection, walletStoragePubkeyStr) => {

   storageService

     .getAccountStorageHistory(connection, walletStoragePubkeyStr)

     .then((res) => {

       console.log(res);

     })

     .catch((err) => {

       alert(err.toString());

       console.log("Error", err);

     });

 };

What happen with this code

Add this function below the function added in the previous step. This will get data from our storage account from blockchain

Why that is interesting

This function will fetch the storage details for our storage account from the blockchain connection we created earlier. If we get data successfully we will log it and if there is some error we will alert the user about the error.

Code

{myWallet ? (

           

             Connected to{" "}

               {myWallet.publicKey.toBase58()}

             

              {myWallet.disconnect();setMyWallet(null);

setStorageAccount("");}}

             >Disconnect Wallet

           

         ) : (

           Connect to Wallet

         )}

What happen with this code

Add this inside the navbar below the a tag. This will add UI for connect and disconnect wallet

Why that is interesting

This will attach a button depending upon the wallet connection. While connecting it will trigger the function which we created earlier and if we are disconnecting it will reset our hooks and disconnect our wallet.

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/e0f015ba-376c-4eab-89d1-f0c4e7b83849.jpg)

And while connecting it will have a few steps like unlocking if you already have a wallet and if you don’t have a wallet please do refer to this simple guide. [https://solpadfinance.medium.com/how-to-create-a-solana-wallet-in-the-sollet-web-wallet-4e050587aca6](https://solpadfinance.medium.com/how-to-create-a-solana-wallet-in-the-sollet-web-wallet-4e050587aca6)

And also do check that you have some devnet SOL Token in you wallet for that you can follow simple steps: [https://www.youtube.com/watch?v=OdzJ34Dp7c8](https://www.youtube.com/watch?v=OdzJ34Dp7c8)

We need a Devnet Solana Token to test our connection to blockchain, create our new account and deploy our solana smart contract.

Code

solana-keygen new

solana config set --url [https://api.devnet.solana.com](https://api.devnet.solana.com)

solana-keygen pubkey

solana airdrop 10 __your_pubkey__

What happen with this code

Open a new terminal and run each command line by line.

Why that is interesting

First command will create an account, next we will set our blockchain url to devent because we want to deploy our contract on blockchain. Next with command we will get a public key for our account which we will require to request a dummy sol token on devnet. And in the last command we are requesting 10 sols on devnet to the pubkey which we have git in the third command.

Code

__yarn test:program__

What happen with this code

Open a new terminal and run the command.

Why that is interesting

This will test our smart contract which we will be deploying on the blockchain.

Code

__yarn build:program__

What happen with this code

Open a new terminal and run the command.

Why that is interesting

This will build our smart contract which is a .so file and we will be deploying that file on the blockchain as solana only accepts .so files for smart contracts.

Code

solana program deploy ./dist/program/storageappprogram.so

What happen with this code

Open a new terminal and run the command.

Why that is interesting

This will first get our .so file of the smart contract which we have created in the previous step, Then it will try to deploy it on the blockchain which on success will give us a programID which makes sure that our contract is successfully deployed on the blockchain.

Code

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/33019bea-992c-43e1-9ceb-05d4266a3b14.jpg)

What happen with this code

Now goto the file named accounts.ts which is inside “src -> solana -> accounts.ts”. And change the programId with the program ID which you got after deploying in the previous step.

Why that is interesting

Here we are telling our wallet functionality to use our smart contract address for sending and retrieving transactions.

Code

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/75a23f8d-9ec5-4cca-afe9-27a80fbd9f10.jpg)

What happen with this code

After changing, do the same for file named storage.ts which is inside “src -> solana -> storage.ts” And here also similarly change the program ID. 

Why that is interesting

Here also our storage needs to know our newly deployed smart contact address to contact it on blockchain for getting our storage which we have stored on blockchain.

Code

 const handleSubmit = async (e) => {

   e.preventDefault();

   if (handleChecks()) {

     setLoading(true);

     const cid = await storeFiles(selectedFile);

     setCid(cid);

     const res =  await storageService.sendStorage(conn.current, myWallet, storageAccount, cid, name);

     setLoading(false);  

   }

 };

What happen with this code

In App.js replace the handleSubmit function. It adds sending transactions to the blockchain to submit our data.

Why that is interesting

With this update to handleSubmit function you will send out data also to the blockchain.  So now it will be like check for errors -> Upload files to IPFS -> Send data to blockchain. 

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/30066b7e-8b46-4192-97e4-4d7710696624.jpg)

Code

 // Storage State

 const \[storage, setStorage\] = React.useState(null);

What happen with this code

Add this inside the App function below other hooks which we made earlier. This will add a new hook for storing data.

Why that is interesting

We need this storage hook so as to store data which is in our storage account. We will use it later to show current data inside our storage account to users.

Code

 const getStorageData = (connection, walletStoragePubkeyStr) => {

   storageService

     .getAccountStorageHistory(connection, walletStoragePubkeyStr)

     .then((res) => {

       setStorage(res);

     })

     .catch((err) => {

       alert(err.toString());

       console.log("Error", err);

     });

 };

What happen with this code

Replace the getStorageData function with this. This will set the storage hook if it gets the data from the storage account.

Why that is interesting

After this when we get some data from a storage account it will set that data to our storage hook and if not it will alert the user about an error occurring.

Code

      getStorageData(conn.current, storageAccount)

What happen with this code

Add this inside handleSubmit function after sending the transaction to the blockchain. It will trigger the getStorageData function.

Why that is interesting

This will also try to get data from the blockchain after it is successfully sended to the blockchain. It will store data as soon as it is in the blockchain. 

Code

 const parseDate = (utc) => {

   const date = parseInt(utc)

   const d = new Date(date);

   return d.toLocaleDateString() \+ " | " \+ d.toLocaleTimeString()

 }

What happen with this code

Add this function below handleSubmit function. It will convert utc time data to human readable form.

Why that is interesting

Since storage on blockchain is expensive we are storing time of our storage data in numbers called unix timestamp. With this we will be able to convert that into human readable form.

Code

 {storage && (

       

         

           Fetched Data from Storage Account - 

             {storageAccount}

           

           

             {storage.name.replaceAll("X", "")}

             {storage.cid}

             Created On: {parseDate(storage.created_on)}

              Go to CID 

           

         

       

     )}

What happen with this code

Add this just below the navbar in code. or just above the form tag. It will add card for storage data.

Why that is interesting

With this our user can see the data which is stored in his storage account. It will check if we have data in a storage hook and if there is it will display it in formatted structure.

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/4ecc093b-6b87-4cbc-b971-b7d238595098.jpg)

__Future Option for this Quest__

1. Storage is essential and it needs to be immutable to use something like arweave to store data and build a RBAC System can be a great quest.
2. This Project can be extended to using encryption schemes on IPFS to secure data.

__Quest Creator__

Prince Anuragi

__Tested On__

Linux Mint

RAM: 8GiB

Storage Disk: 30GiB

Processor: 1 Virtual Core