# Blockchain

[![Build Status](https://travis-ci.org/robinmonjo/blockchain.svg?branch=master)](https://travis-ci.org/robinmonjo/blockchain)

A "naive blockchain" implementation in Elixir inspired by [this JS implementation](https://github.com/lhartikk/naivechain)

This is an umbrella project that provides the blockchain core and a REST API built with Phoenix.

## Usage

Setting up a 3 nodes blockchain locally:

- node 1: `iex -S mix phx.server` (defaults: `PORT=4000 P2P_PORT=5000`)
- node 2: `PORT=4001 P2P_PORT=5001 iex -S mix phx.server`
- node 3: `PORT=4002 P2P_PORT=5002 iex -S mix phx.server`

Then connect the nodes using the API, for example:

```bash
curl -H 'Content-Type: application/json' localhost:4001/api/peers -X POST -d '{ "uri": "localhost:5000"}'  # connect node2 to node1

curl -H 'Content-Type: application/json' localhost:4002/api/peers -X POST -d '{ "uri": "localhost:5001"}'  # connect node3 to node2
```

## API

```bash
# create a block
curl -H 'Content-Type: application/json' localhost:4000/api/blocks -X POST -d '{"data": "block data"}'

# show the blockchain
curl -H 'Content-Type: application/json' localhost:4000/api/blocks

# show connected peers
curl -H 'Content-Type: application/json' localhost:4000/api/peers

# connect to a peer
curl -H 'Content-Type: application/json' localhost:4002/api/peers -X POST -d '{ "uri": "localhost:5001"}'
```

## Resources

- [naive blockchain](https://github.com/lhartikk/naivechain) and its [medium post](https://medium.com/@lhartikk/a-blockchain-in-200-lines-of-code-963cc1cc0e54#.dttbm9afr5)
- [legion blockchain](https://github.com/aviaviavi/legion)
- [proof of work](https://en.bitcoin.it/wiki/Proof_of_work)

For future improvements:

- [minimum viable blockchain](https://www.igvita.com/2014/05/05/minimum-viable-block-chain/)
- [minimum viable blockchain Go implementation](https://github.com/izqui/blockchain)
