# Democracy Features

## Voting Types

**Binary:** a traditional yes-or-no vote • Multi-Option: where individuals can select multiple choices

**Commit-Reveal:** a scheme to commit to a specific vote by posting the hash of the vote.

At the resolution of the vote the `TallyType`, changes the method by which votes are weighed. They are enumerated below:

## Tally Types

**Coin-Weight:** where votes that an individual account casts are weighed on a per coin–one coin is equivalent to one vote

**Lock-time weight:** where an account votes with a specific lock duration, with longer times corresponding to more voting power. For example, a vote may be locked for a one or two week period, with the latter time corresponding to a two-times voting power increase. Lock-time-weighting allows individual accounts with a smaller token balance to exercise more power in the governance process.

**One-person-one-vote:** where one account or identity can cast one vote. On Edgeware, one-person-one-vote may refer to a specific set of verified identities, such as verified Github accounts. 13 Initially, all referendum on Edgeware will be cast with both coin-weighting and lock-time-weighting. An important note, for coin-Weighted voting, a user cannot do a ”partial funds vote”–users can only vote and lock up all the funds for a given account for the lock period, or not vote at all.

## Implementation Delay

Following the resolution of a vote, there is a delay before implementing any change–**initially set to two weeks.**

{% hint style="info" %}
**Parameter Note:** The implementation delay for concluded referenda is set to 2 weeks.
{% endhint %}

## Delegated Voting

Additionally, the democracy module allows for delegated voting, the middle point between direct and representative democracy. At any point before a vote ends, an account can cast a vote different than how the account to whom the account may have delegated has done, essentially, **any account can overrule the decision their delegate makes.** Voluntary delegation has the potential to increase political participation, reduce strategic incentives within the election process, and ameliorate the political principal-agent problem.

**Delegation can be recursive, a delegate can re-delegate to another, using their own voting power and also the delegated voting power of others.** Edgeware mitigates an attack where a malicious individual may manipulate the depth of a delegation tree to an extreme depth. Instead of forcing all nodes tallying votes to traverse a deep tree of delegates, Edgeware limits the delegation to five. Cyclic delegation additionally prevented. Democracy will be extended by adding support for a different VotingType such as enabling rank-choice and anonymous voting, where accounts are directly linked to their cast ballot. Or by adding different TallyingTypes such as quadratic voting.

{% hint style="info" %}
Delegation is limited to 5 levels deep. No vote can be delegated more than 5 times.
{% endhint %}

