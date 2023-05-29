We started this assignment by reading the RAFT paper and taking notes, trying to understand the high level concepts
and then how that would translate into this assignment. For the milestone, we had very basic code that passed the tests,
and then started following the implementation steps from the assignment page. Overall, we implemented almost every 
single part of RAFT, except for some minor details probably. But our process of leader elections and log replication
are as close to RAFT as we could get.

We're proud of how we were able to closely follow the RAFT paper but then make some small changes in order to optimize
our code. One implementation feature we like is how we made separate classes for Follower, Candidate, and Leader. This
helped us organize our methods and be able to see when a replica transitions between states. Another feature we like is
how we hardcoded the initial leader election, and made deterministic election timeouts for each replica. This made our
code much more consistent, and hardcoding the initial election made it much more efficient. Another implementation we 
like is how we added a follower_commit field to the EntryResponse message, in order for the leader to most accurately 
update the follower's match_index. We also spent quite a while tuning the update_commit_index() method. We went through
a lot of different loop combinations but are happy with our final result, which uses the insight that the median value
in a sorted list will be the lowest number that's <= a majority of numbers in that list. 

The biggest problems with testing our code was that it seemed a little random, as in sometimes tests would pass and 
then fail, even though we changed nothing about the code. We also encountered a LOT of off by 1 errors, coming from 
the fact that Python lists index from 0, and RAFT indexes from 1. We solved this just by combing through and checking
wherever we try to use a 1-based index on an list. We also had trouble with updating match_index[] and next_index[] 
properly, which would result in message too long errors if we sent too many entries at once. 

We tested our code by continously running the configs and reading the print statements to check for any errors or 
unexpected messages. Sometimes we would comment out the "received message" print statements to just check for specific
problems. But that was really the only way we tested our code, by making small changes and then running the tests again.