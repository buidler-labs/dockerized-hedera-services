### Hedera local services-node

This repo provides the minimum required services to deploy a hedera network and have it ready to answer API calls. It's topology consists of 3 nodes and a postgres instance. It assumes that [the services-node docker image has already being build](https://github.com/hashgraph/hedera-services/blob/2ff1e352b4e42fbbabb8edff42ad5de60e8d3518/docs/docker-quickstart.md) and is available either locally or at a known, accessible location of which the image prefix can be set via the `REGISTRY_PREFIX` variable inside the `.env` file.

Speaking of the `.env` file, a `.env.sample` file is included and can be used as a template to create the `.env` file.

`Note`: this setup has been stripped bare from the [original `hedera-services` repo](https://github.com/hashgraph/hedera-services) and should be kept updated as seen fit. The best time to build/update this repo would be when a [new stable tag is released upstream](https://github.com/hashgraph/hedera-services/tags).

### Deployment flavours
There are currently 2 docker-compose deployment flavours: 
* a local one, triggered via `docker-compose up` which makes the 3 nodes accessible locally at ports `50220`, `50221` and `50222`
* a VPN one ment for the 3Vs VPN ecosystem triggered via `docker-compose -f docker-compose.yml -f docker-compose.vpn.yml up` which ties all the 3 nodes to an external `vpn2` network and assigns the following static ip addresses for easy reference: `10.11.0.22`, `10.11.0.23` and `10.11.0.24`. The service port is, in this case, the native `50211`