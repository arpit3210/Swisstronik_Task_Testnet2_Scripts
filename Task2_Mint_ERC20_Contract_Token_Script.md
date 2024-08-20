
---

**Video Script: "How to Mint an ERC-20 Token Using Hardhat and OpenZeppelin Contracts Wizard"**

[**Intro Scene**]

Visual: Animated intro with the title "Minting an ERC-20 Token" with blockchain-related graphics.


Voiceover: "Welcome to this step-by-step guide on how to mint your very own ERC-20 token using Hardhat and the OpenZeppelin Contracts Wizard. In this video, we’ll cover the entire process, including:
- Setting up your project in Hardhat.
- Creating an ERC-20 smart contract using OpenZeppelin Contracts Wizard.
- Deploying the contract to a blockchain network.
- Minting 100 ERC-20 tokens.
- Transferring a token to a specific wallet address.
- Publishing your code to a GitHub repository.
- Filling in the necessary details to complete your assignment.
By the end of this video, you'll have successfully completed the task and be ready for review by our team. Let's get started!"


[**Part 1: Setting Up the Project**]

Visual: Screen recording showing a terminal window and a code editor (like VS Code).

Voiceover: "First, let’s set up our project. Open your terminal and create a new project directory by typing:"

Text on screen:
```bash
mkdir MyERC20Token
cd MyERC20Token
```

Voiceover: "Now, install Hardhat if you haven't already, and initialize a new Hardhat project with the following commands:"

Text on screen:
```bash
npm install --save-dev hardhat
npx hardhat
```

Visual: The terminal showing the project initialization process.

Voiceover: "Follow the prompts to create a JavaScript project. Hardhat will set up a basic project structure with all the necessary configuration files."


[**Part 2: Creating the ERC-20 Smart Contract**]

Visual: Screen recording showing the use of the OpenZeppelin Contracts Wizard in a web browser.

Voiceover: "Next, we'll create the ERC-20 smart contract using the OpenZeppelin Contracts Wizard. Navigate to the OpenZeppelin Contracts Wizard website."

Visual: The user selects ERC-20 from the options, configures the token name, symbol, and enables minting.

Voiceover: "The ERC-20 standard is widely used for creating fungible tokens on the Ethereum blockchain. The OpenZeppelin Contracts Wizard makes it easy to customize your token's features. Choose ERC-20, set your token's name and symbol, and enable the minting feature."

Visual: The wizard generates the code.

Voiceover: "Copy the generated Solidity code, as we'll use it in our Hardhat project."




[**Part 3: Deploying the ERC-20 Smart Contract**]

Visual: Switch back to the code editor.

Voiceover: "Now, let's deploy the smart contract using Hardhat. In your project directory, create a new file in the contracts folder and paste the code you copied from the OpenZeppelin Contracts Wizard."

Visual: The user creates and names the file `MyERC20Token.sol` and pastes the code.

Voiceover: "Name the file `MyERC20Token.sol`. This file contains the Solidity code for your ERC-20 token."


Visual: The user creates the deployment script.

Voiceover: "Next, we need to write a deployment script. Let's create a new file in the scripts folder and call it `deploy.js`."

Text on screen:
```bash
touch scripts/deploy.js
```

Visual: The user writes the deployment script in the `deploy.js` file.

Voiceover: "Here’s a basic deployment script:"

Text on screen:



```javascript


const { ethers } = require("hardhat");

async function main() {
  const MyERC20Token = await ethers.getContractFactory("MyERC20Token");
  const token = await MyERC20Token.deploy();
  await token.deployed();
  console.log("MyERC20Token deployed to:", token.address);
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```


Voiceover: "This script compiles and deploys the ERC-20 contract to the blockchain. The contract's address will be logged to the console after a successful deployment."


Visual: The terminal and editor.

Voiceover: "To deploy your contract, run the following command in your terminal:"

Text on screen:

```bash

npx hardhat run scripts/deploy.js --network <network_name>
```

Voiceover: "Replace `<network_name>` with the network you’re deploying to, such as the Ethereum testnet. If the deployment is successful, you’ll see your contract's address in the terminal output."


[**Part 4: Minting 100 ERC-20 Tokens**]

Visual: The terminal and code editor with a focus on interacting with the deployed contract.

Voiceover: "With our contract deployed, it's time to mint 100 ERC-20 tokens. To do this, we'll create another script that interacts with our deployed contract."


Text on screen:

```bash
touch scripts/mint.js
```


Visual: The user writes the minting script in the `mint.js` file.


Voiceover: "Here’s the minting script:"


Text on screen:


```javascript
const { ethers } = require("hardhat");

async function main() {
  const [deployer] = await ethers.getSigners();
  const MyERC20Token = await ethers.getContractFactory("MyERC20Token");
  const token = await MyERC20Token.attach("<deployed_contract_address>");
  
  const mintTx = await token.mint(deployer.address, ethers.utils.parseUnits("100", 18));
  await mintTx.wait();
  
  console.log("100 ERC-20 tokens minted successfully.");
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```




Voiceover: "In this script, we mint 100 ERC-20 tokens by calling the mint function on our deployed contract. The `parseUnits` function ensures we mint the correct number of tokens with the appropriate decimal places."



Visual: The terminal with the command to run the minting script.

Voiceover: "To mint your ERC-20 tokens, run the following command in your terminal:"


Text on screen:

```bash
npx hardhat run scripts/mint.js --network <network_name>
```


Voiceover: "After running this command, you'll have successfully minted 100 ERC-20 tokens."


[**Part 5: Transferring 1 ERC-20 Token**]

Visual: The terminal and code editor with a focus on interacting with the deployed contract.

Voiceover: "Now, let's transfer 1 of those tokens to a specific wallet address. We’ll modify the minting script to include this transfer."

Text on screen:


```javascript

const { ethers } = require("hardhat");

async function main() {
  const [deployer] = await ethers.getSigners();
  const MyERC20Token = await ethers.getContractFactory("MyERC20Token");
  const token = await MyERC20Token.attach("<deployed_contract_address>");
  
  const mintTx = await token.mint(deployer.address, ethers.utils.parseUnits("100", 18));
  await mintTx.wait();
  
  const transferTx = await token.transfer("0x16af037878a6cAce2Ea29d39A3757aC2F6F7aac1", ethers.utils.parseUnits("1", 18));
  await transferTx.wait();
  
  console.log("100 ERC-20 tokens minted and 1 token transferred successfully.");
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```


Voiceover: "In this updated script, we mint 100 tokens and then immediately transfer 1 token to the specified address. The transfer function handles the token transfer."



Visual: The terminal with the command to run the updated script.

Voiceover: "To mint and transfer your ERC-20 tokens, run the following command in your terminal:"


Text on screen:



```bash
npx hardhat run scripts/mint.js --network <network_name>
```


Voiceover: "After running this command, you'll have minted 100 tokens and transferred 1 token to the specified address."



[**Part 6: Publishing the Code to GitHub**]

Visual: GitHub website and the process of creating a new repository.

Voiceover: "With your project complete, it's time to publish the code to a GitHub repository. This step is essential for sharing your work and ensuring version control. Start by navigating to GitHub and creating a new repository."

Visual: The process of pushing code to the repository using the terminal.

Voiceover: "Once your repository is created, you can push your project files to GitHub. Use the following commands in your terminal to initialize Git, add your files, commit them, and push to the remote repository:"

Text on screen:
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin <your_repository_url>
git push -u origin main
```


Voiceover: "Replace `<your_repository_url>` with the URL of your GitHub repository. This will push all your project files to GitHub, making them accessible online."



[**Part 7: Completing the Task Submission**]

Visual: Task submission page with fields for the contract address, GitHub repository link, and token transaction link.

Voiceover: "Finally, to complete your assignment, you’ll need to submit the details of your deployed ERC-20 contract. Enter the deployed contract address, the link to your GitHub repository, and the transaction link for the token transfer."

Visual: Submission process on the task page.

Voiceover: "Double-check all the information before submitting **Video Script Continued: "Completing the Task Submission"**


[**Part 7 Continued: Submitting Task Details**]


Visual: A close-up view of the task submission form fields.

Voiceover: "Now, let’s go through the process of entering your submission details. Start by copying the address of your deployed ERC-20 contract from your terminal. This is the contract address you’ll need to enter in the first field."


Visual: The user copying the contract address from the terminal and pasting it into the task submission form.
Voiceover: "Paste the copied contract address into the designated field for the deployed ERC-20 contract address."

Visual: The GitHub repository link being copied from the browser and pasted into the task submission form.
Voiceover: "Next, head over to your GitHub repository and copy the URL from the address bar. This is the link to your public repository containing the project code. Paste this link into the GitHub repository field."

Visual: The user locating the token transfer transaction on a block explorer like Etherscan, copying the transaction link, and pasting it into the form.
Voiceover: "Lastly, locate the transaction link for the token transfer. You can find this link on a block explorer like Etherscan by searching for your wallet address or the contract address. Copy the transaction link and paste it into the final field labeled 'Token transaction link.'"

Visual: The user reviewing all entered information and clicking the submit button.
Voiceover: "Before you submit, double-check all the information to ensure accuracy. Once you’re confident that everything is correct, go ahead and click the submit button to complete your task submission."

[**Outro Scene**]
Visual: A recap of the steps covered, with highlights on key moments (e.g., minting tokens, transferring tokens, and submitting details).
Voiceover: "Congratulations! You've successfully minted and transferred ERC-20 tokens, deployed a smart contract using Hardhat, and submitted all the necessary details to complete the task. By following these steps, you’ve gained hands-on experience with blockchain development and the tools commonly used in the industry."

Visual: Animated thank you message and call to action.
Voiceover: "Thank you for watching this tutorial. If you found this guide helpful, don't forget to like, share, and subscribe for more blockchain development content. See you in the next video!"

---

This concludes the script, guiding the viewer through each step, from creating and deploying the ERC-20 contract to minting tokens, transferring them, and submitting the final details.
