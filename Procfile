execution-client: geth --sepolia --http --http.api=eth,net,engine,admin --authrpc.jwtsecret=/config/jwt.hex
consensus-client: /config/prysm.sh beacon-chain --accept-terms-of-use --execution-endpoint=http://localhost:8551 --sepolia --jwt-secret=/config/jwt.hex --checkpoint-sync-url=https://sepolia.beaconstate.info --genesis-beacon-api-url=https://sepolia.beaconstate.info
# validator: /config/prysm.sh validator --sepolia  --wallet-dir=./.my_wallet_dir --wallet-password-file=/config/.wallet-password-file
