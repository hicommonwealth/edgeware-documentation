# Social Module \(Deprecated\)

Public functions in the social module allow an account to register, attest, or verify that identity. Accounts first register an identity. Thereafter, individuals attest to this by linking to an external proof. Third parties may now verify that this linked identity is valid, voting whether or not the attestation is valid. Verifications must come from specifically selected verifiers, not necessarily just any third party individual. 

The initial set of verifiers are the validators on the Edgeware network. Work to validate an identity may be delegated to a daemon to manage this process. The sender of both the registration and attestation must be the same, helping to mitigate false attestations. Therefore, the blockchain serves as the single source of truth for attestations on identity registrations. A verifier should only consult the proof stored in the chain to decide whether it is valid or not and not any other form or presentation of an attestation. Examples of attestations for different settings: 

#### Github

The identity is a Github username. Upon username registration, the registrar should publish a Github Gist proof under the username’s account with a link to the registration on Edgeware. 

#### Ethereum:

 The identity is an Ethereum public key or address. Upon username registration, the registrar should send a 0 value transaction to a burn address symbolizing the public key of their corresponding Edgeware account and submit the transaction hash as the attestation. Upon inspection, a verifier should have enough proof that if the owner of the 12 Ethereum account did not also own the recipient Edgeware account \(represented as the target address on Ethereum\), then they would not issue such a transaction.

 Initially, the set of verifiers are the set of accounts that have a minimum of 0.1% of EDG tokens. The votes for identity verification are coin-weighted. Edgeware does this so that it is organically able to establish a 1p1v government for other areas of the system.

