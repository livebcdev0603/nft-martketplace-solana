# CANDY MACHINE


## Creating generative art

1. Create a `traits` folder and create a list of directories for the traits (i.e. background, shirt, sunglasses). Look at the `example-traits` for guidance
2. Run the following command to create a configuration file called `traits-configuration.json`:

```
metaplex generate_art_configurations <directory>
ts-node cli generate_art_configurations <directory>
```

The following file will be generated (based off of `example-traits`):

```json
{
  "name": "",
  "symbol": "",
  "description": "",
  "creators": [],
  "collection": {},
  "breakdown": {
    "background": {
      "blue.png": 0.04,
      "brown.png": 0.04,
      "flesh.png": 0.05,
      "green.png": 0.02,
      "light-blue.png": 0.06,
      "light-green.png": 0.01,
      "light-pink.png": 0.07,
      "light-purple.png": 0.05,
      "light-yellow.png": 0.06,
      "orange.png": 0.07,
      "pink.png": 0.02,
      "purple.png": 0.03,
      "red.png": 0.05,
      "yellow.png": 0.43
    },
    "eyes": {
      "egg-eyes.png": 0.3,
      "heart-eyes.png": 0.12,
      "square-eyes.png": 0.02,
      "star-eyes.png": 0.56
    },
    "face": {
      "cyan-face.png": 0.07,
      "dark-green-face.png": 0.04,
      "flesh-face.png": 0.03,
      "gold-face.png": 0.11,
      "grapefruit-face.png": 0.07,
      "green-face.png": 0.05,
      "pink-face.png": 0.05,
      "purple-face.png": 0.02,
      "sun-face.png": 0.1,
      "teal-face.png": 0.46
    },
    "mouth": {
      "block-mouth.png": 0.23,
      "smile-mouth.png": 0.09,
      "triangle-mouth.png": 0.68
    }
  },
  "order": ["background", "face", "eyes", "mouth"],
  "width": 1000,
  "height": 1000
}
```

3. Go through and customize the fields in the `traits-configuration.json`, such as `name`, `symbol`, `description`, , `creators`, `collection`, `width`, and `height`.
4. After you have adjusted the configurations to your heart's content, you can run the following command to generate the JSON files along with the images.

```
metaplex create_generative_art -c <configuration_file_location> -n <number_of_images>
ts-node cli create_generative_art -c <configuration_file_location> -n <number_of_images>
```

5. This will create an `assets` folder, with a set of the JSON and PNG files to make it work!

Install and build

```
yarn install
yarn build
yarn run package:linuxb
OR
yarn run package:linux
OR
yarn run package:macos
```

You can now either use `metaplex` OR the `ts-node cli` to execute the following commands.

1. Upload your images and metadata. Refer to the NFT [standard](https://docs.metaplex.com/nft-standard) for the correct format.

```
metaplex upload ~/nft-test/mini_drop --keypair ~/.config/solana/id.json
ts-node cli upload ~/nft-test/mini_drop --keypair ~/.config/solana/id.json
```

2. Verify everything is uploaded. Rerun the first command until it is.

```
metaplex verify --keypair ~/.config/solana/id.json
ts-node cli verify --keypair ~/.config/solana/id.json
```

3. Create your candy machine. It can cost up to ~15 solana per 10,000 images.

```
metaplex create_candy_machine -k ~/.config/solana/id.json -p 1
ts-node cli create_candy_machine -k ~/.config/solana/id.json -p 3
```

4. Set the start date and update the price of your candy machine.

```
metaplex update_candy_machine -k ~/.config/solana/id.json -d "20 Apr 2021 04:20:00 GMT" -p 0.1
ts-node cli update_candy_machine -k ~/.config/solana/id.json -d "20 Apr 2021 04:20:00 GMT" -p 0.1
```

5. Test mint a token (provided it's after the start date)

```
metaplex mint_one_token -k ~/.config/solana/id.json
ts-node cli mint_one_token -k ~/.config/solana/id.json
```

6. Check if you received any tokens.

```
spl-token accounts
```

7. If you are listed as a creator, run this command to sign your NFTs post sale. This will sign only the latest candy machine that you've created (stored in .cache/candyMachineList.json).

```
metaplex sign_candy_machine_metadata -k ~/.config/solana/id.json
ts-node cli sign_candy_machine_metadata -k ~/.config/solana/id.json
```

8. If you wish to sign metadata from another candy machine run with the --cndy flag.

```
metaplex sign_candy_machine_metadata -k ~/.config/solana/id.json --cndy CANDY_MACHINE_ADDRESS_HERE
ts-node cli sign_candy_machine_metadata -k ~/.config/solana/id.json --cndy CANDY_MACHINE_ADDRESS_HERE
```
