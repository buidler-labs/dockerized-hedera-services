### Hedera local services-node

#### The TL;DR
```
git clone https://github.com/three-Vs/dockerized-hedera-services.git
docker-compose up
```

This repo provides the minimum required services to deploy a hedera network and have it ready to answer API calls. It's topology consists of 3 nodes and a postgres instance. It assumes that [the services-node docker image has already being build](https://github.com/hashgraph/hedera-services/blob/2ff1e352b4e42fbbabb8edff42ad5de60e8d3518/docs/docker-quickstart.md) and is available either locally or at a known, accessible location of which the image prefix can be set via the `REGISTRY_PREFIX` variable inside the `.env` file.

Speaking of the `.env` file, a `.env.sample` file is included and can be used as a template to create the `.env` file.

If the `.env` file is not provided, the stack defaults to targeting the latest available [hedera-services release tag](https://github.com/hashgraph/hedera-services/releases/).

`Note`: this setup has been stripped bare from the [original `hedera-services` repo](https://github.com/hashgraph/hedera-services) and should be kept updated as seen fit. The best time to build/update this repo would be when a [new stable tag is released upstream](https://github.com/hashgraph/hedera-services/tags).

### Deployment
Simply doing a `docker-compose up` makes the 3 nodes accessible locally (eg `localhost`) at ports `50211`, `50212` and `50213`. The stack makes use of [this public docker-hub image](https://hub.docker.com/r/buidlerlabs/hedera-services).

### Making use of it
Just fire up your [SDK client of choice](https://docs.hedera.com/guides/docs/sdks) and configure it to use the network like so:

#### JS
``` javascript
const client = Client.forNetwork({
    '127.0.0.1:50211': new AccountId(3),
    '127.0.0.1:50212': new AccountId(4),
    '127.0.0.1:50213': new AccountId(5)
});
```

#### Java
``` java
Map<String, AccountId> nodes = new HashMap<>();
nodes.put("127.0.0.1:50211" ,AccountId.fromString("0.0.3"));
nodes.put("127.0.0.1:50212" ,AccountId.fromString("0.0.4"));
nodes.put("127.0.0.1:50213" ,AccountId.fromString("0.0.5"));

Client client = Client.forNetwork(nodes);
```

What's left now is for you to call any of the available hedera-services such as [querying for the account balance](https://docs.hedera.com/guides/docs/sdks/cryptocurrency/get-account-balance) or [uploading a file using hedera's file service (HFS)](https://docs.hedera.com/guides/docs/sdks/file-storage/create-a-file).

By the way, there is a pre-registered account inside the network with `50 000 000 000 ℏ` available. The credentials for it (for using it as an operator) are:
```
AccountId  : 0.0.2
PrivateKey : 91132178e72057a1d7528025956fe39b0b847f200ab59b2fdd367017f3087137 
```

### Happy hashing! 🥂
