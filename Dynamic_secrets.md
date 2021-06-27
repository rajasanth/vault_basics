# Enabling AWS secret Engine
vault secrets enable -path=aws aws

# Configure the AWS secrets engine.

vault write aws/config/root \
    access_key=$AWS_ACCESS_KEY_ID \
    secret_key=$AWS_SECRET_ACCESS_KEY \
    region=us-east-1
