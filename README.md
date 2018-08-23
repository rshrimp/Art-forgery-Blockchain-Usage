# Art-forgery-Blockchain-Usage
Art forgery is a major problem for the art market, here is a framework for using blockchain to solve it


#### 1.  problem and  current solutions. 
Problems:

  a. As per wikipedia "Art forgery is the creating and selling of works of art which are falsely credited to other, usually more famous artists."

  b. It also encompasses issues with establishing the authenticity of the purported piece of art, mainly if it was created by the artist that it claims it did (IP protection)

  c.  if it has a legitimate audit/paper trail of the past purchases to rule out theft (proof of ownership)

  All the above are tied to what is referred as "provenance"- chronology of the ownership, custody or location of an object.

Current Solutions:

There are 3 markets which deal with the art currently:

  a. Legal/Legit auction houses that buy and sell physical art to collectors and retail customers

  b. Online e-commerce sites that sell digital version of art, and

  b. Illegal channels where stolen artwork is bought and sold.

  Except for the last Illegal channel where not much can be done, the first two have some credibility due to legality and auction house names.
  And then there are types of art works:

  a. Old artwork and deceased artist (high end works) - this needs additional work  due to inherent issues with establishing authenticity as well as importing existing paper trail of ownership from major auction houses.

  b. new artwork and alive artist - this is easy to deal with


#### 2. e advantages and disadvantages of using a blockchain solution. 

Advantages:

  a. _Authentication_ - The artist can authenticate that work is, in fact, created by him. This record of authentication will be on the blockchain and distributed. The artist cannot later decide the work was not his. This protects the investment of a collector indefinitely.

  b.  _Digital Editions_ - The artist can chose to offer the  artwork in a limited edition.  Each number within the edition is tracked separately on the ledger. The artist cannot later expand the edition as this information is a matter of public record on the blockchain.

  c. _Proof of Ownership_ - The audit trail of purchase can go on the blockchain.  

  d. _Provenance_ - No matter how many times art work is bought and sold, original purchase and the purchases of future owners of the work are documented and unalterable, creating a trusted provenance.

  d. _Proper mechanism to reward artist_ - Through blockchain, artists can start getting rewards they truly deserve.

Disadvantages:

  a. High initial investment to implement Blockchain

  b. Steep learning curve towards adoption of the new system by various parties involved (artists, auction houses, auditors, collectors)

  c. Concerns around personally identifiable data (PII) being part of the public domain

  d. ongoing maintenance costs

  e. complexity and lack of knowledge involved as it is still a new technology.


###  3.  a network:to help the art market. 
Broadlly speaking there will be 5 entities:
1. Artists.network
2. Auction houses
3. OnLine artshops
4. Auditors
5. Evaluators

Below is one option on how this network can be designed.

```
Artsconsortium

Organizations/Peers

1. artists.net                - a network of group of artists registered and affiliated with Artists network.
--------------------------------
2. christies.com              - This is an individual auction house.  
3. sothebys.com               - This is an individual auction house.  
4. philipsNY.com              - This is an individual auction house.  
5. AuctionHouse_xyz.com       - This is an individual auction house.  
-------------------------------
6. artspace.com               - This is an individual art shop    
7. artsy.com                  - This is an individual art shop
8. sochiArt.com               - This is an individual art shop
9. onlineArtShop_xyz.com      - This is an individual art shop
-------------------------------
10. auditors.net              - part of art consortium
------------------------------
11. evaluators.net            - a network of group of historic/forensic inspectors to certify authenticity of the old artworks for which the artists are not alive

Users:

Collectors/buyers             - registered on individual auction houses, artshops and artists.net
auditUsers                    - registered auditors on auditors.net
evaluateUsers                 - registered evaluators.net

Channels:

artworks is the blockchain to track all the artoworks. Artists who are members of this blockchain can create a new artwork.  Auction houses and artshops can create a new artwork only if the artists is deceased.  It is not available until evaluators examine and approve it, which is when it becomes available. The reason for this flow is to make sure auctionhouses and artshops dont abuse their powers to add artwork without evaluator's consent.

Auction houses and artshops can use the available artworks to list on their auction/artshop and when the auction/sale is completed, they can update the details of the auctioned/sold artwork on artworks blockhain.

Both auction houses and art shops dont have access to each others blockchain.

Artshops operate on the same premise as the

1. artworks                   - inventory of all the artoworks
2. auctions                   - auction houses are part of this Channel
3. artshops                   - art shops part of this channel

Access Controls for peers on 3 channels

1. artoworks                  - readonly for auditors, and collectors/buyers
                              - create & read for artists.net
                              - read & update for evaluators.net
                              - create, read & update for auctionhouses and artshops

2. auctions                   - readonly for auditors, artists.net and collectors
                              - read, create and update for auctionhouse
                              - no access for artshop

3. artshops                    - readonly for auditors, artists.net and collectors
                              - read, create and update for artshops
                              - no access for auctionhouses
```        

So here is the matrix for channel access at a Create, Read, and Update level
```
+------------------+-----------------+-----------------+-----------------+
Channels -->       + artoworks       + auctions        + artshops       +
+------------------+-----------------+-----------------+-----------------+
artists.net         create & read     readonly           readonly
+------------------+-----------------+-----------------+-----------------+
auction houses      create & read     create & updates   no access
+------------------+-----------------+-----------------+-----------------+
artshop             create & read     no access         create & updates
+------------------+-----------------+-----------------+-----------------+
auditors.net        readonly          readonly          readonly
+------------------+-----------------+-----------------+-----------------+
evaluators.net      update & read     no Access         no Access
+------------------+-----------------+-----------------+-----------------+
users/Collectors    readonly          readonly           readonly
+------------------+-----------------+-----------------+-----------------+
```

### SmartContact Functionality:
1. adding a new artwork to artworks channel:

  artists.net and auctionhouses can propose to add artwork with the following rules

  a. Only registeted artists can propose to create(add) a NEW art on artworks blockchain for which they are creators.
  b. Only acution houses and art shops can propose to create(add) OLD artwork.

  In both the cases above, only evaluators can update/approve artworks and then gets created(added) to artworks blockchain after examining and certifying its authenticity

  attributes of artwork- ID, name, artist Details, origination date, date added, authenticationStatus (yes/no), history of ownership (bought/sold/from/to/date/price). History of ownership includes whether sold by auctionhouse/online, and the details around it.

  `func createArtwork()`

  `func authenticateArtwork()`  -- this is used to finally approve by evaluators which is when it gets to the artworks blockchain as CREATED. until then it stays in pending state waiting to be added to the blockchain.

2. Each auction house is a member of auctions channle/blockchain. For an auction to be operated, auction houses read from the artworks blockchain, the items they want to put up for auction, if available. This provides them with the provenance of the artwork. They will host their own auction with their registered users. At the end of auction, they will update the artworks blockchain for the final status of the art work which will be part of history of ownership (bought/sold/from/to/date/price).

  `func listForAuction()` - details of the artwork to be auctioned

  `func listForSale()` - details of the artwork to be sold on art shops

  `func settleAuction()` - details of the settled auctions
  `func settleSale()` - details of the settled auctions

  `func updateArtworks()` - make an update to the artID on artworks blockchain with the details of the concluded auction/sale.

3. artshops.net will follow the same process as auctionhouses but will operate on artshops  channel.

4. auctionhouses and artshops will not have access to each others channels as it is not needed and for competitive purposes.

5. Auditors will have access to all 3 blockchains for auditing purposes.

### CA details

1. artists.net - with its _own_ root CA. This will be checked in `createArtwork()` for permission to create an artwork on artworks channel. Aution houses and art shops certs will be checked for `createArtwork()`

2. auction houses  - each of suthbys, christies, etc auction houses will be registered as an intermediary CA with a _auctions.net root CA_

3. art shops   each of artsy, sochiArt, etc shops will be registered as an intermediary CA with a _artshops.net root CA_

4. evaluators.net with a root _evaluators.net root CA_

5. auditors.net with a root _auditors.net CA_
