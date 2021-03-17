Procedure for allnodes:

req: public key of a funded customer account 

1.- Run ./create_symbol_supernode <pubkey>

Produces the target dir using bootstrap, default owner account is replaced with public key supplied (empty priv key in addresses.yml)
It Creates a bonded agg tx with the link tx ready to send over to the customer.

2.- Send payload to customer with instructions to execute symbol-cli and get a valid signature

At this point customers could announce directly themselves bcs they have the payload and the signature.
  -(I've found a crash impeeding me to do it, issue https://github.com/nemtech/symbol-cli/issues/363)

The customer would execute `symbol-cli transaction payload` to sign and announce.

======= EXAMPLE OF EXECUTION
marc-os@roston:~/allnodes$ ./create_symbol_supernode 
                         _             _         _                    _         _                      
  ___  _   _  _ __ ___  | |__    ___  | |       | |__    ___    ___  | |_  ___ | |_  _ __  __ _  _ __  
 / __|| | | || '_ ` _ \ | '_ \  / _ \ | | _____ | '_ \  / _ \  / _ \ | __|/ __|| __|| '__|/ _` || '_ \ 
 \__ \| |_| || | | | | || |_) || (_) || ||_____|| |_) || (_) || (_) || |_ \__ \| |_ | |  | (_| || |_) |
 |___/ \__, ||_| |_| |_||_.__/  \___/ |_|       |_.__/  \___/  \___/  \__||___/ \__||_|   \__,_|| .__/ 
       |___/                                                                                    |_|    
2021-03-17T03:12:01.732Z warn     Password has not been provided (--noPassword)! It's recommended to use one for security!
2021-03-17T03:12:01.753Z info     Generating config from preset testnet
2021-03-17T03:12:01.753Z info     Assembly preset dual
2021-03-17T03:12:01.753Z info     Custom preset file supernode.yml
2021-03-17T03:12:01.764Z info     Generating Main account...
2021-03-17T03:12:01.784Z info     Generating Transport account...
2021-03-17T03:12:01.794Z info     Generating Remote account...
2021-03-17T03:12:01.798Z info     Generating Voting account...
2021-03-17T03:12:01.802Z info     Generating VRF account...
2021-03-17T03:12:01.813Z info     User for docker resolved: 1003:1003
2021-03-17T03:12:01.814Z info     Running image using Exec: symbolplatform/symbol-server:tools-gcc-0.10.1.8 bash createNodeCertificates.sh
2021-03-17T03:12:07.339Z info     Certificate for node api-node created
2021-03-17T03:12:07.354Z info     Running image using Exec: symbolplatform/symbol-server:tools-gcc-0.10.1.8 bash createAgentCertificate.sh
2021-03-17T03:12:12.711Z info     Agent Certificate for node api-node created
2021-03-17T03:12:12.729Z info     Generating api-node server configuration
2021-03-17T03:12:12.814Z info     Generating api-broker broker configuration
2021-03-17T03:12:12.839Z info     Running image using Exec: symbolplatform/symbol-server:tools-gcc-0.10.1.8 /usr/catapult/bin/catapult.tools.votingkey --secret=HIDDEN_KEY --startEpoch=1 --endEpoch=1460 --output=/votingKeys/private_key_tree1.dat
2021-03-17T03:12:16.609Z info     Voting key executed for node api-node!
2021-03-17T03:12:16.682Z info     Configuration generated.
replacing A0B10829E4E6985BEDC2079BAA26535DD296092725D45690BAEE572C57CEC143 with 50AC6D29B7E0BC919D4BC6AC2948E5997D798982A02EBE37BB919DBB7975C037
==========================================================================
Instructions:

Send to the customer the following instructions:

Execute the command:
symbol-cli transaction cosign

Select "transaction payload(for off-chain tx)" when prompted.
Paste the following blob:
B8010000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001984142E0AB000000000000B6D6D6E6090000007C31DA19ABE277AAF2B819DB4D522F0164C5EED66F17D6BDC2A15F83137BED241001000000000000510000000000000050AC6D29B7E0BC919D4BC6AC2948E5997D798982A02EBE37BB919DBB7975C0370000000001984C4132D46556CC107595492A8C9D31B09AC400A98704CD7344AB6D8BDEE00EE3404C0100000000000000510000000000000050AC6D29B7E0BC919D4BC6AC2948E5997D798982A02EBE37BB919DBB7975C03700000000019843428606843A3D929CE9A083B52438F04B9B4324887DABCEE68B4500EF4580DA826E0100000000000000590000000000000050AC6D29B7E0BC919D4BC6AC2948E5997D798982A02EBE37BB919DBB7975C03700000000019843414B9B84BD79E28814668FEFDAECAD6400DF4642900F707A4C19A84A9C8E4B7D8301000000B40500000100000000000000

Enter the wallet password when asked.

The last output of the command will look like:
Co-signed transaction:{"parentHash":"B7E0AB247F11E8F454C04C41B338FB1029C8407224E58271D4B987DC4D455E46","signature":"0662BA5056BA5CA3DB3358A601AA0DD195C3B7ACC007CC83AF69E92F10360645CCE53FE5215896A2D1F79CC5F9BF5A035662905C853C7E38E30F9EBB7FE7BC0F","signerPublicKey":"50AC6D29B7E0BC919D4BC6AC2948E5997D798982A02EBE37BB919DBB7975C037","version":{"lower":0,"higher":0}}

send over to allnodes.



