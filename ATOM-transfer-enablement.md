# Summary

  * Lay out a plan to set up a testnet using the Cosmos SDK v0.34.0 release, along with mainnet conditions, plus transfer enablement and increased block size, as a testing ground.

  * After this proposal is passed and after successful testing, and after the software Git hash for v0.34.0 has been finalized, conduct a second proposal that includes the specific Git hash, using an expedited governance rule to determine acceptance.

  * After the second proposal is determined to be accepted, upgrade to the cosmoshub-2 chain to use the Cosmos SDK release v0.34.0, along with the necessary updates to the genesis file, at a time to be determined by the second proposal.

# Overview

The Cosmos Network was launched with no possibility to transfer ATOMS, mainly for security purposes to ensure that the release is stable and facilitate any rollbacks should the need for them arise.

More than two weeks have passed since the launch of the mainnet network and no faults have appeared in the stability and security of the network. It is our belief that the network is ready to handle the enablement of ATOM transfers, a critical feature of any blockchain network. In order to achieve this, the maximum size of each block also needs to be updated to handle the associated increase in the number of transactions.

# Original and Expedited Governance Rules

In order not to unduly delay the release process, a two-step governance setup is being proposed, in the next section, for the release of v0.34.0. Before proceeding, let us define:

 * *Original Governance Rules*, to be the governance rules as currently implemented, namely, proposals are deemed to have passed if a 50%+1 majority of cast votes, excluding Abstain votes, by the end of the governance period (i.e. two weeks after the deposit threshold has been reached) are in favour of a proposal, a quorum of 40% of bonded stake has cast their vote and there are less than 33.4% Veto votes.

 * *24-Hours Expedited Governance Rule*, to be a different acceptance mechanism via which a proposal is deemed to have passed if 2/3 + 1 of bonded stake has voted in favour of the proposal for a continuous duration of 24-hours. A buffer period of 24 hours is also put in place from the time of full deposit payment to the possible start of the continuous 24-hours required. Note that this mechanism currently requires custom querying to determine.

The 24-Hours Expedited Governance Rule aims to strike a balance between timeliness and safety by reducing the time required for proposal acceptance while increasing the necessary quorum to 2/3 of bonded stake + 1. 


# Proposal

We are proposing that:


  * The Tendermint development team push a new release (v0.34.0) of the Cosmos SDK with the following scope:
    - what is currently published under github.com/cosmos/cosmos-sdk and github.com/tendermint/tendermint in their respective develop branches
    - any further non-consequential changes or bug-fixes as determined by the Tendermint team
    - due to the expedited nature of the second proposal, no changes may intentionally be suggested that hurts the delegators in favor of the validators;

  * A new testnet (gaia-14k) is specifically set up to run and test the new release with the appropriate changes in the genesis file to:
    - enable the transfer of ATOMS
    - increase the maximum size of each block to allow more transactions per block
    - adjust the blocks_per_year parameter as indicated in proposal 1 (https://ipfs.io/ipfs/QmXqEBr56xeUzFpgjsmDKMSit3iqnKaDEL4tabxPXoz9xc), if it is approved;

  * Following the successful testing of the new release, i.e. as long as no critical issues are encountered on testnet, a subsequent second proposal is to be voted on using the defined 24-Hours Expedited Governance Rule. If this second proposal is accepted, the mainnet is upgraded to use the new release and amended parameters.

The main repercussion of these two proposals is that the fundamental feature of value transfer in a blockchain is fully enabled on the Cosmos network along with the upgrade to release v0.34.0 on the cosmoshub-2 chain. Furthermore, the maximum size of each block is increased to facilitate the transfer of value.

# Possible blockers

Apart from non-acceptance of this proposal, we see the following possible reasons for the delay of the transfer enablement milestone:

  * A critical issue is identified during the testing phase of the new release.

  * Community agreement that the launch of Voyager is imperative before the transfers can be enabled.
 
  * Community agreement that the current voting power distribution is not decentralised enough and that this should be remedied before the enablement of the transfers.
  
  * Other objections by community agreement that are decided after this or the second proposal are passed, but before the deadline for upgrading as determined by the second proposal.

# Proposed upgrade process

We propose that the transfer enablement is performed in the following way:

  1. A new v0.34.0 release of the Cosmos SDK is pushed by the Tendermint team (via the @tendermint_team twitter, https://medium.com/tendermint, and https://forum.cosmos.network).

  2. A new testnet (gaia-14k) running the new release is launched as follows:
      * Issue genesis file with the following modifications to the cosmoshub-1 genesis file:
        * 'genesis_time' set to an appropriate date
        * 'accounts' adapted from gaia-13k
        * 'chain_id' set to gaia-14k
        * 'block_size'
          - 'max_bytes' set to 200,000
          - 'max_gas' set to 2,000,000
        * 'send_enabled' set to true
        * 'withdraw_addr_enabled' set to true
        * 'blocks_per_year' set to 4,855,015 – should proposal 1 on the cosmoshub-1 chain be accepted by the community

      * Collect 'gentxs' for inclusion in the gaia-14k genesis file.
    
      * Issue final genesis file and launch new testnet.

  3. If no critical issues, such as chain halts, are identified on gaia-14k, a second proposal is proposed to be evaluated by 24-Hours Expedited Governance Rule with the following spirit:
      * The mainnet is upgraded to the new release and chain ID cosmoshub-2 after block height XXX (to be determined in the second proposal).  This will involve:
    
        * The issue of the new cosmoshub-2 genesis file with amended parameters.
    
        * The switching off of cosmoshub-1 nodes on block XXX.
    
        * The upgrade of the nodes to Cosmos SDK release v0.34.0, along with the necessary update of the genesis file.
      
        * The relaunch of the upgraded nodes on the cosmoshub-2 chain.
  
      * The second proposal should only be voted in favour of by a validator/delegator if they determine that the testnet (as defined above) was a success, and the scope of changes of for v0.34.0 is within the bounds of what is defined in this proposal. _NOTE: If any delegators determine that validators voted in favor of a second proposal that hurt the delegators in favor of the validators, they may undelegate from these validators in the future._
    
      * The second proposal may include some modifications to the process.  It is expected validators carefully follow the instructions on the second proposal, but ultimately it is the responsibility of the validators to evaluate their readiness to run the proposed software by voting YES or NO (or NO-WITH-VETO) on the second proposal.

In the event of critical issues having been identified on testnet, the enablement process should be ultimately stopped with a NO decision on the second proposal. Then, a new proposal for the enablement of the transfers will be developed, taking into consideration any repercussions of the identified issues.

# Persisting data from cosmoshub-1

We want to preserve the blockchain and app state data for cosmoshub-1.  In the future we may include these in the blockchain header perhaps as consensus parameters (which get loaded from the genesis file).

Several entities have volunteered to store the data for cosmoshub-1, including Simply VC, the Interchain Foundation, and Tendermint Inc.  All validators are encouraged to retain this data and provide it at cost to anyone who requires it to serve the chain.  A later governance proposal will determine what to do with this data.

# Forum link

The following forum can be used to discuss this proposal:
  - https://forum.cosmos.network/t/proposal-3-atom-transfer-enablement/1787

