# ssh cheatsheet

## server fingerprints in ~/.ssh/known_hosts

# remove old fingerprints for a server and add new ones. No duplicates.
ssh-keygen -R bestia.dev
ssh-keyscan -H bestia.dev >> ~/.ssh/known_hosts
cat ~/.ssh/known_hosts

